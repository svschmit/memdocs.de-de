---
title: XML-Elemente in der Konfigurationsdatei des Plug-Ins
titleSuffix: Configuration Manager
description: Technische Referenz für die XML-Elemente des Plug-Ins „Paketkonvertierungs-Manager“
ms.date: 08/24/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 940cc075-4066-44d5-972a-927c0b0a1143
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 9178b595ba67723c623979b4c29290e42fe5f6ac
ms.sourcegitcommit: a77ba49424803fddcaf23326f1befbc004e48ac9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83877752"
---
# <a name="technical-reference-for-the-package-conversion-manager-plug-in-configuration-xml"></a>Technische Referenz für die XML-Elemente in der Konfigurationsdatei des Plug-Ins „Paketkonvertierungs-Manager“

*Gilt für: Configuration Manager (Current Branch)*

<!--1357861-->

In diesem Thema werden die XML-Elemente in der Configuration Manager-Konfigurationsdatei (Microsoft.ConfigurationManagement.exe.config) beschrieben, mit denen das Plug-In „Paketkonvertierungs-Manager“ gesteuert wird. Weitere Informationen finden Sie unter [Verwenden des Plug-Ins „Paketkonvertierungs-Manager“](how-to-use-plug-in.md).



## <a name="xml-configuration-elements"></a>XML-Konfigurationselemente

In der folgenden Tabelle werden die zum Plug-In „Paketkonvertierungs-Manager“ gehörigen XML-Elemente in der Configuration Manager-Konfigurationsdatei beschrieben.

|Element  |Typ  |Beschreibung  |
|---------|---------|---------|
|**PcmPlugIn**|Zeichenfolge|Der Name des Skripts oder der ausführbaren Datei, das bzw. als das Plug-In „Paketkonvertierungs-Manager“ verwendet wird.|
|**PcmPlugInTimeoutMilliseconds**|Ganze Zahl|Die maximale Wartezeit (in Millisekunden), die gewartet wird, bis das Skript bzw. die ausführbare Datei für das Plug-In „Paketkonvertierungs-Manager“ die Verarbeitung eines Pakets abgeschlossen hat.|
|**PcmPluginExitCode**|Ganze Zahl|Der erwartete Exitcode des Plug-In-Prozesses. Dieser Wert gibt an, dass der Vorgang erfolgreich ausgeführt wurde. Alle anderen Codes werden als Fehler betrachtet.|
|**ForceRequirementsExtraction**|Boolesch|Ermöglicht der automatischen Konvertierung die Verwendung von Sammlungsanforderungen, die mit einem Paket verbunden sind. Diese Einstellung darf nur dann auf TRUE festgelegt werden, wenn Sie mit einem Plug-In „Paketkonvertierungs-Manager“ arbeiten, das darauf ausgelegt ist, Entscheidungen über zu verwendende Anforderungen zu treffen.|



## <a name="sample-configuration-xml"></a>XML-Elemente der Beispielkonfiguration

In diesem Abschnitt finden Sie ein Beispiel der XML-Elemente in der Konfiguration des Paketkonvertierungs-Managers in der Configuration Manager-Konfigurationsdatei **Microsoft.ConfigurationManagement.exe.config**. Die Datei befindet sich standardmäßig im folgenden Pfad:  
`C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

> [!IMPORTANT]
> Ab Version 1910 wurde dieser Pfad so geändert, dass der `Microsoft Endpoint Manager`-Ordner verwendet wird. Stellen Sie sicher, dass Sie keine ältere Version der Datei verwenden, die möglicherweise in einem anderen Ordner vorhanden ist. 

In diesem Beispiel befinden sich die zum Paketkonvertierungs-Manager gehörigen Elemente im folgenden Element: `Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings`

``` XML
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
...
    </Microsoft.ConfigurationManagement.AdminConsole.Properties.Settings>
    <Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
      <setting name="DecisionVerbosity" serializeAs="String">
        <value>2</value>
      </setting>
      <setting name="PcmPlugIn" serializeAs="String">
        <value>pcmplugin.vbs</value>
      </setting>
      <setting name="PcmPlugInTimeoutMilliseconds" serializeAs="String">
        <value>10000</value>
      </setting>
      <setting name="PcmPluginExitCode" serializeAs="String">
        <value>0</value>
      </setting>
      <setting name="ForceRequirementsExtraction" serializeAs="String">
        <value>True</value >
      </setting>
    </Microsoft.ConfigurationManagement.UserCentric.Workflow.Properties.Settings>
  </applicationSettings>
...
```

