---
title: Behandlung von Problemen mit Win32-Apps in Microsoft Intune
titleSuffix: ''
description: Lernen Sie die gängigsten Methoden zum Behandeln von Win32-App-Problemen mit Microsoft Intune kennen.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: efdc196b-38f3-4678-ae16-cdec4303f8d2
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: bbdc929f5d3a9703f3d299b8e3a68dd624c450c2
ms.sourcegitcommit: 4b8c317c71535c2d464f336c03b5bebdd2c6d4c9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/15/2020
ms.locfileid: "90083912"
---
# <a name="troubleshoot-win32-app-issues"></a>Behandeln von Win32-App-Problemen

Für die Problembehandlung von in Microsoft Intune verwendeten Win32-Apps können Sie verschiedene Methoden anwenden. Dieser Artikel bietet Details zur Problembehandlung sowie weitere Informationen, um Sie beim Lösen von Problemen mit Win32-Apps zu unterstützen. Weitere Informationen finden Sie unter [Problembehandlung bei der Installation von Win32-Apps](troubleshoot-app-install.md#win32-app-installation-troubleshooting).

> [!NOTE]
> Diese App-Verwaltungsfunktion unterstützt sowohl eine 32-Bit- als auch 64-Bit-Betriebssystemarchitektur für Windows-Anwendungen.

> [!IMPORTANT]
> Bei der Bereitstellung von Win32-Apps sollten Sie ausschließlich die Methode der [Intune-Verwaltungserweiterung](../apps/intune-management-extension.md) nutzen. Dies gilt insbesondere dann, wenn Sie ein Win32-App-Installationsprogramm mit mehreren Dateien verwenden. Wenn Sie während der Autopilot-Registrierung die Installation von Win32- und branchenspezifischen Apps kombinieren, funktioniert die App-Installation möglicherweise nicht. Die Intune-Verwaltungserweiterung wird automatisch installiert, wenn ein PowerShell-Skript oder eine Win32-App dem Benutzer oder Gerät zugewiesen ist.

## <a name="app-troubleshooting-details"></a>Details zur Problembehandlung von Apps

Sie können Installationsprobleme ansehen, z. B. wann die App erstellt, geändert, ausgerichtet und auf einem Gerät bereitgestellt wurde. Im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) finden Sie diese Informationen und weitere Details im Bereich **Problembehandlung + Support**. Weitere Informationen finden Sie unter [Details zur Problembehandlung von Apps](troubleshoot-app-install.md#app-troubleshooting-details).

## <a name="troubleshooting-app-issues-by-using-logs"></a>Beheben von App-Problemen mithilfe von Protokollen

Protokollinformationen können dabei helfen, die Ursache von auftretenden Problemen zu ermitteln und diese Probleme zu lösen. Sie können sich die [in Intune angezeigten Protokolle](apps-win32-troubleshoot.md#logs-displayed-in-intune) oder die [über CMTrace angezeigten Protokolle](apps-win32-troubleshoot.md#logs-displayed-through-cmtrace) ansehen. 

### <a name="logs-displayed-in-intune"></a>In Intune angezeigte Protokolle

Wenn bei einer Win32-App ein Installationsproblem auftritt, können Sie im Intune-Bereich **Installationsdetails** für die App die Option **Protokolle sammeln** auswählen. Weitere Informationen finden Sie unter [Problembehandlung bei der Installation von Win32-Apps](troubleshoot-app-install.md#win32-app-installation-troubleshooting).

### <a name="logs-displayed-through-cmtrace"></a>Über CMTrace angezeigte Protokolle

Agent-Protokolle befinden sich auf einem Clientcomputer üblicherweise unter *C:\ProgramData\Microsoft\IntuneManagementExtension\Logs*. Sie können mit *CMTrace.exe* diese Protokolldateien anzeigen. Weitere Informationen finden Sie unter [CMTrace](https://docs.microsoft.com/configmgr/core/support/cmtrace).

![Screenshot der Agent-Protokolle auf dem Clientcomputer](./media/apps-win32-app-management/apps-win32-app-10.png)

> [!IMPORTANT]
> Um eine ordnungsgemäße Installation und Ausführung von branchenspezifischen Win32-Apps zu ermöglichen, muss in den Antischadsoftwareeinstellungen die Überprüfung der folgenden Verzeichnisse ausgeschlossen werden:<p>
> **Auf x64-Clientcomputern**:<br>
> *C:\Program Files (x86)\Microsoft Intune Management Extension\Content*<br>
> *C:\windows\IMECache*
>  
> **Auf x86-Clientcomputern**:<br>
> *C:\Program Files\Microsoft Intune Management Extension\Content*<br>
> *C:\windows\IMECache*
>
> Weitere Informationen finden Sie unter [Empfehlungen zum Virenscan auf Unternehmenscomputern, auf denen unterstützte Windows-Versionen ausgeführt werden](https://support.microsoft.com/help/822158/virus-scanning-recommendations-for-enterprise-computers).

## <a name="detecting-the-win32-app-file-version-by-using-powershell"></a>Ermitteln der Dateiversion einer Win32-App mithilfe von PowerShell

Wenn es für Sie schwierig ist, die Dateiversion einer Win32-App zu ermitteln, erwägen Sie die Verwendung oder Änderung des folgenden PowerShell-Befehls:

``` PowerShell

$FileVersion = [System.Diagnostics.FileVersionInfo]::GetVersionInfo("<path to binary file>").FileVersion
#The below line trims the spaces before and after the version name
$FileVersion = $FileVersion.Trim();
if ("<file version of successfully detected file>" -eq $FileVersion)
{
#Write the version to STDOUT by default
$FileVersion
exit 0
}
else
{
#Exit with non-zero failure code
exit 1
}
```

Ersetzen Sie im obigen PowerShell-Befehl die Zeichenfolge `<path to binary file>` durch den Pfad zu Ihrer Win32-App-Datei. Ein Beispielpfad würde etwa so aussehen:

`C:\Program Files (x86)\Microsoft SQL Server Management Studio 18\Common7\IDE\ssms.exe`

Ersetzen Sie außerdem die Zeichenfolge `<file version of successfully detected file>` durch die Dateiversion, die Sie ermitteln müssen. Eine Beispielzeichenfolge für die Dateiversion würde etwa so aussehen:

`2019.0150.18118.00 ((SSMS_Rel).190420-0019)`

Wenn Sie die Versionsinformationen zu Ihrer Win32-App abrufen müssen, können Sie den folgenden PowerShell-Befehl verwenden:

``` PowerShell

[System.Diagnostics.FileVersionInfo]::GetVersionInfo("<path to binary file>").FileVersion

```

Ersetzen Sie im obigen PowerShell-Befehl `<path to binary file>` durch Ihren Dateipfad.

## <a name="additional-troubleshooting-areas-to-consider"></a>Weitere zu berücksichtigende Problembehandlungsbereiche
- Überprüfen Sie das Ziel, um sicherzustellen, dass der Agent auf dem Gerät installiert ist. Durch eine Win32-App oder ein PowerShell-Skript, die bzw. das für eine Gruppe bestimmt ist, wird eine Richtlinie für die Agent-Installation für eine Sicherheitsgruppe erstellt.
- Überprüfen Sie die Betriebsystemversion: Windows 10, Version 1607 und höher.  
- Überprüfen Sie die Windows 10-SKU. Windows 10 S oder mit aktiviertem S-Modus ausgeführte Windows-Versionen unterstützen keine MSI-Installation.

Weitere Informationen zur Behandlung von Problemen mit Win32-Apps finden Sie unter [Win32 app installation troubleshooting (Problembehandlung bei der Win32-App-Installation)](troubleshoot-app-install.md#win32-app-installation-troubleshooting). Informationen zu App-Typen auf ARM64-Geräten finden Sie unter [Auf ARM64-Geräten unterstützte App-Typen](../apps/troubleshoot-app-install.md#app-types-supported-on-arm64-devices).

## <a name="next-steps"></a>Nächste Schritte

- [Problembehandlung bei der App-Installation](troubleshoot-app-install.md)
