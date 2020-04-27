---
title: Anpassen des Supportcenters
titleSuffix: Configuration Manager
description: Anpassen der Konfigurationsdatei für das Supportcenter.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a6f7f6b7-9ef3-4ffa-a3cf-d877ac55983b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: fc17437e508ea69a19043c29bf9ad4501cbac3e4
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82078514"
---
# <a name="customize-support-center"></a>Anpassen des Supportcenters

*Gilt für: Configuration Manager (Current Branch)*

Das Tool [Supportcenter](support-center.md) enthält eine anpassbare Konfigurationsdatei. Diese Datei befindet sich nach der Installation des Supportcenters standardmäßig unter folgendem Pfad: `C:\Program Files (x86)\Configuration Manager Support Center\ConfigMgrSupportCenter.exe.config`. Die Konfigurationsdatei ändert das Verhalten des Programms:

- [Anpassen der Datensammlung:](#bkmk_datacoll) Bearbeiten Sie die bei der Datensammlung zu berücksichtigenden Registrierungsschlüssel und WMI-Namespaces.  

- [Anpassen der Protokolldateigruppen:](#bkmk_loggroups) Definieren Sie neue Gruppen von Protokolldateien mithilfe von regulären Ausdrücken. Außerdem können Sie andere Protokolldateien zu Protokollgruppen hinzufügen.  

- [Sammeln zusätzlicher Protokolldateien mithilfe von Platzhaltern:](#bkmk_wildcards) Verwenden Sie Platzhaltersuchen zum Sammeln zusätzlicher Protokolldateien.  

Sie benötigen Administratorberechtigungen für den Client, auf dem Sie das Supportcenter installiert haben, um diese Änderungen vornehmen zu können. Verwenden Sie einen Text- oder XML-Editor wie Editor oder Visual Studio, um diese Anpassungen vorzunehmen.

> [!Important]  
> Die Supportcenter-Konfigurationsdatei ist eine XML-Datei. Dies ist für den Betrieb des Supportcenters wichtig. Das Ändern dieser Datei wird nur für Benutzer empfohlen, die mit XML und regulären Ausdrücken vertraut sind.  

Legen Sie eine Sicherungsdatei der ursprünglichen Datei an, bevor Sie die Supportcenter-Konfigurationsdatei bearbeiten. Mit dieser Sicherungsdatei können Sie die ursprüngliche Funktionsweise von Supportcenter wiederherstellen, wenn es zu Fehlern beim Bearbeiten der Datei kommt. Wenn Sie keine Sicherungsdatei anlegen und das Supportcenter nicht ordnungsgemäß funktioniert, nachdem Sie die Konfigurationsdatei bearbeitet haben, müssen Sie das Supportcenter neu installieren. Sie können auch eine Konfigurationsdatei einer anderen Installation des Supportcenters kopieren.



## <a name="customize-data-collection"></a><a name="bkmk_datacoll"></a> Anpassen der Datensammlung

Ändern Sie zum Anpassen der Datensammlung für den Client die Konfigurationsdatei des Supportcenters mithilfe der im `<dataCollectorSettings>`-Element enthaltenen XML-Elemente.


### <a name="wmi-data-collection"></a>WMI-Datensammlung

Das `<CcmWmiDataCollector>`-Element enthält ein `<collectionScopes>`-Element. Verwenden Sie dieses Element, um die WMI-Namespaces zu ändern, aus denen Supportcenter Daten sammelt. Es enthält auch ein `<ignoreScopes>`-Element. Verwenden Sie dieses Element, um die Datensammlung aus den im `<collectionScopes>`-Element definierten Teilen von Namespaces herauszufiltern.  
    
#### <a name="example"></a>Beispiel
Die Standardkonfigurationsdatei sammelt Daten aus dem `root\ccm`-Namespace. Sie enthält diesen Pfad ist in einem `<add/>`-Element in `<collectionScopes>`. 

Sie ignoriert außerdem alles unter den Pfaden `\cimodels`, `\invagt`,  `\events` und `\policy` für diesen Namespace. Diese Pfade sind in den in `<ignoreScopes>` enthaltenen `<add/>`-Elementen enthalten.

```XML
<CcmWmiDataCollector>
  <collectionScopes>
    <!-- Collect these namespaces (ignoring the sub-scopes in the ignoreScopes block) -->
    <add key="root\ccm"/>
    <add key="root\cimv2\sms"/>
  </collectionScopes>
  <ignoreScopes>
    <!-- Collecting these namespaces is known to be problematic/unnecessary -->
    <add key="root\ccm\cimodels"/>
    <add key="root\ccm\invagt"/>
    <add key="root\ccm\events"/>
    <!-- Do not collect policy, there's already a separate policy collector.-->
    <add key="root\ccm\policy"/>
  </ignoreScopes>
</CcmWmiDataCollector>
```


### <a name="registry-data-collection"></a>Registrierungsdatensammlung

Das `<RegistryDataCollector>`-Element enthält ein `<registryKeys>`-Element. Verwenden Sie dieses Element zum Ändern der Registrierungsschlüssel und Unterschlüssel, die das Supportcenter aus dem Pfad `HKEY_LOCAL_MACHINE` sammelt. Das Supportcenter unterstützt nicht die Sammlung von Registrierungsdaten aus anderen Stammregistrierungspfaden.

#### <a name="example"></a>Beispiel
Fügen Sie folgendes `<add/>`-Element in das `<registryKeys>`-Element ein, um Registrierungsschlüssel für die klassischen auf dem Gerät installierten Programme zu sammeln: `<add key="software\\microsoft\\windows\\currentversion\\uninstall"/>`

```XML
<RegistryDataCollector>
  <registryKeys>
    <!-- Registry keys (and all subkeys) to collect -->
    <add key="software\\microsoft\\ccm"/>
    <add key="software\\microsoft\\sms"/>
    <add key="software\\microsoft\\ccmsetup"/>
    <add key="software\\microsoft\\windows\\currentversion\\uninstall"/>
  </registryKeys>
</RegistryDataCollector>
```



## <a name="customize-log-file-groups"></a><a name="bkmk_loggroups"></a> Anpassen der Protokolldateigruppen

Verwenden Sie die Elemente im `<logGroups>`-Element, um anzupassen, welche Protokolldateien vom Supportcenter erfasst werden und wie sie in der Liste **Protokollgruppen** dargestellt werden. Wenn Sie das Supportcenter starten, durchsucht es diesen Abschnitt der Konfigurationsdatei. Dann wird für jeden eindeutigen Schlüsselattributwert eine Gruppe in der Liste **Protokollgruppen** erstellt, das in den im `<logGroups>`-Element enthaltenen `<add/>`-Elementen gefunden wird.

- **Komponentenprotokollgruppe:** Das `<componentLogGroup>`-Element verwendet ein Schlüsselattribut, um den Namen der Protokollgruppe zu definieren, die in der Liste angezeigt wird. Es verwendet außerdem ein Wertattribut, das einen regulären Ausdruck (RegEx) enthält. Dieser RegEx wird verwendet, um zugehörige Protokolldateien zu erfassen.  

- **Statische Protokollgruppe:** Das `<staticLogGroup>`-Element verwendet ein Schlüsselattribut, um den Namen der Protokollgruppe zu definieren, die in der Liste angezeigt wird. Es verwendet außerdem ein Wertattribut, das den Namen der Protokolldatei definiert.  

Wenn sowohl das `<componentLogGroup>`-Element als auch das `<staticLogGroup>`-Element den gleichen Schlüsselattributwert in einem `<add/>`-Element verwenden, erstellt das Supportcenter eine einzelne Gruppe. Diese Gruppe enthält die Protokolldateien, die von den beiden Elementen definiert werden, die den gleichen Schlüssel verwenden.

#### <a name="example"></a>Beispiel
```XML
<logGroups>
  <componentLogGroup>
    <add key="Application Management" value="^(app.*|ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|execmgr.*|UserAffinity.*|.*Handler$|.*Provider$)"/>
    <add key="Client Registration" value="^(clientregistration|locationservices|ccmmessaging|ccmexec)"/>
    <add key="Inventory" value="^(ccmmessaging|inventoryagent|mtrmgr|swmtrreportgen|virtualapp|mtr.*|filesystemfile)"/>
    <add key="Policy" value="^(ccmmessaging|policyagent_.*|policyevaluator_.*)"/>
    <add key="Software Updates" value="^(ci.*|contentaccess|contenttransfermanager|datatransferservice|dcm.*|update.*|wuahandler|xmlstore|scanagent)"/>
    <add key="Software Distribution" value="^(datatransferservice|execmgr.*|contenttransfermanager|locationservices|contentaccess|filebits)"/>
    <add key="Desired Configuration Management" value="^(ci.*|dcm.*)"/>
    <add key="Operating System Deployment" value="^(ts.*)"/>
  </componentLogGroup>
  <staticLogGroup>
    <add key="Application Management" value="ccmsdkprovider.log"/>
    <add key="Desired Configuration Management" value="ccmsdkprovider.log"/>
    <add key="Software Updates" value="ccmsdkprovider.log"/>
  </staticLogGroup>
</logGroups>
```



## <a name="collecting-additional-log-files-using-wildcards"></a><a name="bkmk_wildcards"></a> Sammeln zusätzlicher Protokolldateien mithilfe von Platzhaltern

Verwenden Sie Platzhalter im Dateipfad oder Dateinamen, um zusätzliche Protokolldateien zu sammeln. Zu diesem Platzhaltern gehören systemweite Umgebungsvariablen wie `%WINDIR%`. Benutzerspezifische Umgebungsvariablen wie `%USERPROFILE%` sind jedoch ausgenommen. Verwenden Sie ein `<add/>`-Element innerhalb des `<additionalLogFiles>`-Elements, um zusätzliche Protokolldateien bei Verwendung dieser nicht rekursiven Protokolldateisuche zu sammeln. 

In den folgenden Beispielen wird veranschaulicht, wie Supportcenter dieses Feature in der Standardkonfigurationsdatei anwendet.

#### <a name="example-1-collect-all-windows-update-log-files-in-the-windows-directory"></a>Beispiel 1: Sammeln aller Windows Update-Protokolldateien im Windows-Verzeichnis
Mit dem folgenden Element werden alle Dateien mit dem Namen `WindowsUpdate.log` erfasst, die im Windows-Verzeichnis gefunden werden: 

`<add key="%WINDIR%\WindowsUpdate.log" />`

#### <a name="example-2-collect-all-log-files-in-the-windows-logs-directory"></a>Beispiel 2: Sammeln aller Protokolldateien im Windows-Protokollverzeichnis
Mit dem folgenden Element werden alle Dateien erfasst, die mit `.log` enden und im Windows-Protokollverzeichnis gefunden werden: 

`<add key="%WINDIR%\logs\*.log" />`

#### <a name="full-example-xml"></a>Vollständiges XML-Beispiel
```XML
<CcmLogDataCollector>
  <additionalLogFiles>
    <!-- Collect these additional log files. Can pass in a wildcard for the filename. System variables are also supported. -->
    <!--
    <add key="%WINDIR%\WindowsUpdate.log" />
    <add key="%WINDIR%\logs\*.log" />
    -->
  </additionalLogFiles>
</CcmLogDataCollector>
```
