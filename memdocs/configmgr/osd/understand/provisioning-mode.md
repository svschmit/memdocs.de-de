---
title: Bereitstellungsmodus
titleSuffix: Configuration Manager
description: Hier erfahren Sie mehr über den Clientbereitstellungsmodus während der Configuration Manager-Tasksequenz.
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: troubleshooting
ms.assetid: 3e3ff3a4-7a75-41bb-bdf9-33ede9c0e3a3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b0039648c6f444efdbbaeb16f55d29b630ee7f16
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124269"
---
# <a name="provisioning-mode"></a>Bereitstellungsmodus

*Gilt für: Configuration Manager (Current Branch)*

Der Client wird während einer Tasksequenz zur Betriebssystembereitstellung von Configuration Manager in den Bereitstellungsmodus versetzt. (Eine Tasksequenz für die Betriebssystembereitstellung enthält ein direktes Upgrade auf Windows 10.) In diesem Modus werden vom Client keine Richtlinien vom Standort verarbeitet. Aufgrund dieses Verhaltens kann die Tasksequenz ausgeführt werden, ohne Gefahr zu laufen, dass auf dem Client weitere Bereitstellungen ausgeführt werden. Nach Abschluss der Tasksequenz, ob erfolgreich oder nach behandeltem Fehler, wird der Bereitstellungsmodus des Clients beendet.

Wenn bei der Tasksequenz ein unerwarteter Fehler auftritt, bleibt der Client möglicherweise im Bereitstellungsmodus. Dies kann beispielsweise vorkommen, wenn das Gerät während der Verarbeitung der Tasksequenz neu gestartet wird und nicht wiederhergestellt werden kann. Clients in diesem Zustand müssen vom Administrator ausfindig gemacht und wiederhergestellt werden.


## <a name="manually-remove-provisioning-mode"></a>Manuelles Entfernen des Bereitstellungsmodus

Wenn ein Client im Bereitstellungsmodus gelassen wird, können Sie diesen manuellen Prozess durchführen, um den Client wieder in den normalen Betrieb zu versetzen.

```PowerShell
Invoke-WmiMethod -Namespace root\CCM -Class SMS_Client -Name SetClientProvisioningMode -ArgumentList $false
```

> [!Important]  
> Eine der von dieser WMI-Methode angewandten Änderungen besteht im Festlegen eines Registrierungswerts, es werden aber auch andere Änderungen vorgenommen. Das Ändern des Registrierungswerts reicht nicht aus, um den Client vollständig aus dem Bereitstellungsmodus zu nehmen. Wenn Sie die Registrierung manuell bearbeiten, kann der Client unerwartete Verhaltensweisen aufweisen.  


## <a name="client-provisioning-mode-timeout"></a>Timeout für den Clientbereitstellungsmodus

Die Tasksequenz setzt ab Version 1902 einen Zeitstempel, sobald der Client in den Bereitstellungsmodus versetzt wird. Ein Client im Bereitstellungsmodus prüft alle 60 Minuten, wie viel Zeit seit dem Zeitstempel vergangen ist. Wenn sich der Client länger als 48 Stunden im Bereitstellungsmodus befindet, wird der Bereitstellungsmodus automatisch beendet und der Vorgang neu gestartet.

48 Stunden ist der standardmäßige Timeoutwert für den Bereitstellungsmodus. Diesen Timer können Sie auf einem Gerät anpassen, indem Sie den Wert **ProvisioningMaxMinutes** im folgenden Registrierungsschlüssel entsprechend festlegen: `HKLM\Software\Microsoft\CCM\CcmExec`. Wenn dieser Wert nicht vorhanden ist oder `0` lautet, wird vom Client der Standardwert 48 Stunden verwendet.

Der Zeitstempel **ProvisioningEnabledTime** befindet sich in folgendem Registrierungsschlüssel: `HKLM\Software\Microsoft\CCM\CcmExec`. Der Zeitstempel hat den Wert des letzten Zeitpunkts, an dem das Gerät in den Bereitstellungsmodus gewechselt ist. Das Format ist „Epoche“ (Unix-Zeitstempel) und in UTC.

Dieser Zeitstempel wird auch auf die aktuelle Zeit zurückgesetzt, wenn Sie den Computer manuell in den Bereitstellungsmodus versetzen, indem Sie den folgenden Befehl verwenden:

```powershell
Invoke-WmiMethod -Namespace root\CCM -Class SMS_Client -Name SetClientProvisioningMode -ArgumentList $true
```

## <a name="process-flow-diagrams"></a>Prozessflussdiagramm

In den folgenden Diagrammen werden die Prozessflüsse für die Tasksequenz und den Client dargestellt.

### <a name="task-sequence"></a>Tasksequenz

Im folgenden Diagramm wird gezeigt, wie die Tasksequenz den Bereitstellungsmodus festlegt:

![Flussdiagramm der Festlegung des Bereitstellungsmodus durch die Tasksequenz](media/3197824-ts-flow.png)

### <a name="client-remediation"></a>Clientwiederherstellung

Im folgenden Diagramm wird gezeigt, wie der Client den Bereitstellungsmodus beendet:

![Flussdiagramm zum Beenden des Bereitstellungsmodus durch den Client](media/3197824-client-flow.png)


## <a name="see-also"></a>Weitere Informationen:

[Setup Windows and ConfigMgr (Einrichten von Windows und ConfigMgr)](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr)

[Upgrade Operating System (Aktualisieren des Betriebssystems)](task-sequence-steps.md#BKMK_UpgradeOS)
