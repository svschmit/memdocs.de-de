---
title: Deployment Monitoring Tool
titleSuffix: Configuration Manager
description: Mit dem Deployment Monitoring Tool können Sie Fehler in Softwarebereitstellungen auf einem Konfigurations-Manager-Client beheben.
ms.date: 09/24/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9edc214f-f405-456d-80df-8adcc2a5428d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 5a27e96cf69ab01b58910ae02fc732940eda8a04
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707828"
---
# <a name="deployment-monitoring-tool"></a>Deployment Monitoring Tool

*Gilt für: Configuration Manager (Current Branch)*

Das Deployment Monitoring Tool ist eines der [Configuration Manager-Tools](tools.md). Es handelt sich hierbei um eine grafische Benutzeroberfläche, die bei der Fehlerbehandlung bei Anwendungs- und Softwareupdates sowie bei Bereitstellungen für Konfigurationsbaselines auf einem Konfigurations-Manager-Client als Unterstützung dient. Das Tool ist schreibgeschützt, da kein Status auf dem Client geändert wird. Sie können das Tool bedenkenlos zum Diagnostizieren von Bereitstellungsszenarios verwenden.


## <a name="features"></a>Features

- Führen Sie das Tool als Administrator aus, um die Problembehandlung in Bereitstellungen auf einem lokalen Client durchzuführen.  

- Führen Sie die Problembehandlung in Bereitstellungen auf einem Remoteclient durch. Starten Sie das Tool, und stellen Sie als Administrator eine Verbindung mit einem Remotecomputer her.  

- Exportieren Sie alle im Tool erfassten Daten in das XML-Format. Geben Sie die XML-Datei für andere Benutzer frei, und verwenden Sie diese als gemeinsame Plattform für den Austausch in Bezug auf die Problembehandlung in Bereitstellungen.  

- Importieren Sie zuvor exportierte Daten auf einem anderen Computer, und verwenden Sie diese zur Ausführung des Tools im Offlinemodus.   


## <a name="usage"></a>Verwendung

Das Deployment Monitoring Tool unterstützt nur die grafische Benutzeroberfläche. Führen Sie **DeploymentMonitoringTool.exe** als Administrator aus, um das Tool zu starten. Es gibt drei Ansichten:  

- **Clienteigenschaften:** Eine Liste mit nützlichen Attributen für das Gerät und den Konfigurations-Manager-Client. Dies ist die Standardansicht.   

- **Bereitstellungen:** Ansicht aller aktuellen Zielbereitstellungen. Wählen Sie im Ergebnisbereich eine Bereitstellung aus, um im Detailbereich weitere Informationen anzuzeigen.  

- **Alle Updates:** Ansicht aller Softwareupdates und der zugehörigen Status.  

Wenn Sie Daten in einer Ansicht kopieren möchten, wählen Sie eine Zelle aus, und drücken Sie **STRG** + **C**.


### <a name="actions-menu"></a>Menü „Aktionen“

Im Menü **Aktionen** sind die folgenden Aktionen verfügbar:  

- **Connect to remote machine** (Mit Remotecomputer verbinden): Hier können Sie einen Computer auswählen, mit dem eine Verbindung hergestellt werden soll. Wenn Sie keinen Benutzernamen mit zugehörigem Kennwort eingeben, werden die aktuellen Anmeldeinformationen verwendet. Klicken Sie auf **Speichern**, um eine Verbindung mit dem Remotecomputer herzustellen.  

- **Daten exportieren:** Hier können Sie eine Datei auswählen, in die die Daten geschrieben werden sollen. Klicken Sie anschließend auf **Speichern**. Verwenden Sie die exportierte XML-Datei für die Remote-Fehlerbehebung auf einem anderen Computer.  

- **Daten importieren:** Hier können Sie eine Datei für den Import in das Tool auswählen.  

- **Protokoll anzeigen:** Öffnet je nach Ansicht eine zugeordnete Protokolldatei:  
    - Clienteigenschaften: `\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - Bereitstellungen: `\\<hostname>\c$\Windows\CCM\Logs\PolicyAgent.log`
    - Alle Updates: `C:\Windows\WindowsUpdate.log`



## <a name="see-also"></a>Weitere Informationen:

- [Bereitstellen von Anwendungen](../../apps/deploy-use/deploy-applications.md)
- [Bereitstellen von Softwareupdates](../../sum/deploy-use/deploy-software-updates.md)
- [Bereitstellen von Konfigurationsbaselines](../../compliance/deploy-use/deploy-configuration-baselines.md)
