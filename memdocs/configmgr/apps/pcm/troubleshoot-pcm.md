---
title: Beheben von Problemen mit dem Paketkonvertierungs-Manager
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Probleme mit dem Paketkonvertierungs-Manager in Configuration Manager behoben werden.
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cb616925-bb94-4b7c-a867-b3d95aef4d5e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 05110714d3aa8ca48ff9384f0116338b0092fde1
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83877620"
---
# <a name="troubleshoot-package-conversion-manager"></a>Beheben von Problemen mit dem Paketkonvertierungs-Manager

*Gilt für: Configuration Manager (Current Branch)*

<!--1357861-->

Die Informationen in diesem Thema helfen Ihnen bei der Behandlung von Problemen mit dem Paketkonvertierungs-Manager.



## <a name="sms-provider"></a>SMS-Anbieter

Der Paketkonvertierungs-Manager nutzt den SMS-Anbieter. Weitere Informationen finden Sie unter [Planen des SMS-Anbieters](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md).

Wenn der SMS-Anbieter nicht ordnungsgemäß funktioniert, funktioniert auch die Configuration Manager-Konsole mit dem Paketkonvertierungs-Manager nicht.



## <a name="package-readiness"></a>Paketbereitschaft

Bevor ein Paket in eine Anwendung konvertiert werden kann, analysieren Sie es mit der Funktion **Analysieren** des Paketkonvertierungs-Managers. Fügen Sie nach der Analyse in der Configuration Manager-Konsole dem Knoten **Pakete** die Spalte **Bereitschaft** hinzu. In der Liste der Pakete wird einer der folgenden Bereitschaftsstatus des analysierten Pakets angezeigt:

- **Automatisch:** Das Paket kann mithilfe der Funktion **Konvertieren** direkt konvertiert werden.      

  > [!NOTE]  
  > Eine automatische Konvertierung umfasst nicht die Konvertierung von WQL-Abfragen in Anwendungsanforderungen. Verwenden Sie den Prozess **Korrigieren und konvertieren**, um diese Abfragen zu konvertieren.  

- **Manuell:** Das Paket erfordert Ergänzungen oder Änderungen, bevor Sie es mit der Funktion **Korrigieren und konvertieren** konvertieren können.  

- **Nicht zutreffend:** Das Paket ist für die Konvertierung nicht geeignet. Beheben Sie entweder die für das Paket vorliegenden Probleme, oder setzen Sie die Bereitstellung des Pakets fort.  

- **Fehler**: Das Paket enthält Fehler. Korrigieren Sie diese Fehler manuell, bevor Sie es analysieren und konvertieren.  

In der Configuration Manager-Konsole werden im Detailbereich des Knotens **Pakete** Bereitschaftsprobleme angezeigt. Klicken Sie auf das Paket und anschließend im Detailbereich auf die Registerkarte **Zusammenfassung**.



## <a name="log-files"></a>Protokolldateien

### <a name="enable-logging"></a>Aktivieren der Protokollierung

Wenn Sie die Protokollierung für den Paketkonvertierungs-Manager aktivieren, protokolliert dieser alle seine Aktionen, Ausnahmen und Fehler.

Ändern Sie zum Aktivieren der Protokollierung für diese Komponente in Configuration Manager die Datei **Microsoft.ConfigurationManagement.exe.Config**. Diese Konfigurationsdatei befindet sich standardmäßig im folgenden Pfad:  
`C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`  

> [!IMPORTANT]
> Ab Version 1910 wurde dieser Pfad so geändert, dass der `Microsoft Endpoint Manager`-Ordner verwendet wird. Stellen Sie sicher, dass Sie keine ältere Version der Datei verwenden, die möglicherweise in einem anderen Ordner vorhanden ist.

Fügen Sie die folgenden XML-Elemente für **switches** und **trace** in das Element **system.diagnostics** hinter dem letzten Element **sources** ein:

``` XML
</sources>

    <switches>
      <add name="PcmLogging" value="3"/>
    </switches>
    <trace autoflush="true" indentsize="4">
      <listeners>
        <add name="PcmTraceListener" type="Microsoft.ConfigurationManagement.UserCentric.Logging.RolloverLogTraceListener, Microsoft.ConfigurationManagement.UserCentric.Logging" initializeData="%UserProfile%\AppData\Local\Temp\PcmTrace.log"/>
      </listeners>
    </trace>

</system.diagnostics>
```

In diesem Beispiel wird die Datei **PCMTrace.log** verwendet. Dieses Protokoll befindet sich auf dem Computer, auf dem die Configuration Manager-Konsole im folgenden Pfad ausgeführt wird:  
`%UserProfile%\AppData\Local\Temp`

Ändern Sie zum Konfigurieren des Detaillierungsgrad der Ablaufverfolgung die Switcheinstellung **PcmLogging**. Legen Sie diesen Wert auf vier Detaillierungsgrade fest, von am wenigsten detailliert (`1`) bis sehr detailliert (`4`).


### <a name="smsprovlog"></a>SMSProv.log

In einigen Fällen befinden sich Informationen, die für die Problembehandlung bei der Paketkonvertierung relevant sind, in der Datei **SMSProv.log**. Diese Datei erfasst Informationen vom SMS-Anbieter von Configuration Manager.

Standardmäßig befindet sich diese Protokolldatei auf dem Configuration Manager-Standortserver im folgenden Pfad:  
`C:\Program Files\Microsoft Configuration Manager\Logs`

Wenn Sie eine der folgenden Fehlermeldungen sehen, kann die Datei **SMSProv.log** relevante Informationen zur Problembehandlung enthalten:

- `The SMS Provider reported an error`

- `Generic Failure`

Diese Fehlermeldungen weisen in der Regel darauf hin, dass auf dem Standortserver ein Fehler aufgetreten ist und die Fehlerinformationen nicht an die Configuration Manager-Konsole übermittelt wurden.

Weitere Informationen finden Sie unter [Technische Referenz zu Fehlermeldungen im Paketkonvertierungs-Manager](error-messages.md).



## <a name="changing-package-attributes-after-analysis"></a>Ändern von Paketattributen nach der Analyse

Sobald Sie ein Paket analysiert haben und es den Bereitschaftsstatus **Automatisch** oder **Manuell** hat, kann der Konvertierungsprozess fehlschlagen, wenn Sie eines der relevanten Attribute ändern.

Angenommen, Sie analysieren ein Paket und sein Bereitschaftsstatus ist **Automatisch**. Dann fügen Sie dem Paket ein weiteres Programm hinzu. Die Paketkonvertierung kann fehlschlagen.

Wenn Sie nach der Analyse Änderungen an einem Paket vornehmen müssen, führen Sie die Analyse vor der Konvertierung erneut durch. 



## <a name="see-also"></a>Weitere Informationen:

[Technische Referenz zu Fehlermeldungen im Paketkonvertierungs-Manager](error-messages.md)
