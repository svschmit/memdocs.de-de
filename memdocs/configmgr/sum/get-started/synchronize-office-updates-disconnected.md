---
title: Synchronisieren von Office 365-Updates ohne Internetverbindung
titleSuffix: Configuration Manager
description: Synchronisieren Sie Office 365-Updates auf dem obersten Softwareupdatepunkt, der nicht mit dem Internet verbunden ist.
ms.date: 04/21/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: a8fa7e7a-bf55-42de-b0c2-c56777dc1508
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 3627d2f7772b7b9e133d742b0ee4f94dba6e457a
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110354"
---
# <a name="synchronize-office-365-updates-from-a-disconnected-software-update-point"></a><a name="bkmk_O365"></a> Synchronisieren von Office 365-Updates bei einem getrennten Softwareupdatepunkt

*Gilt für: Configuration Manager (Current Branch)*
<!--4065163-->
Ab Version 2002 von Configuration Manager können Sie ein neues Tool verwenden, um Office 365-Updates von einem mit dem Internet verbundenen WSUS-Server in eine nicht verbundene Configuration Manager-Umgebung zu importieren. Bisher konnten Sie beim Exportieren und Importieren von Metadaten für Softwareupdates in nicht verbundenen Umgebungen keine Office 365-Updates bereitstellen. Für Office 365-Updates sind zusätzliche Metadaten erforderlich, die über eine Office-API vom Office-CDN heruntergeladen werden, was in nicht verbundenen Umgebungen nicht möglich ist.

> [!Note]
> Ab dem 21. April 2020 wird Office 365 ProPlus in **Microsoft 365 Apps for Enterprise** umbenannt. Weitere Informationen finden Sie unter [Namensänderung für Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). Möglicherweise finden Sie während des Updates der Konsole noch Verweise auf den alten Namen in der Configuration Manager-Konsole und der unterstützenden Dokumentation.

## <a name="prerequisites"></a>Voraussetzungen

- Ein mit dem Internet verbundener WSUS-Server, auf dem mindestens Windows Server 2012 ausgeführt wird.
- Der WSUS-Server benötigt Konnektivität zu diesen beiden Internetendpunkten:
   - `officecdn.microsoft.com`
   - `config.office.com`
- Kopieren Sie das OfflineUpdateExporter-Tools und die zugehörigen Abhängigkeiten auf den mit dem Internet verbundenen WSUS-Server.
  - Das Tool und die zugehörigen Abhängigkeiten befinden sich im Verzeichnis **&lt;ConfigMgrInstallDir>/tools/OfflineUpdateExporter**.
- Der Benutzer, der das Tools ausführt, muss zur Gruppe **WSUS-Administratoren** gehören.
- Das zum Speichern der Metadaten und Inhalte der Office-Updates erstellte Verzeichnis muss über geeignete Zugriffssteuerungslisten zum Sichern der Dateien verfügen.
    - Dieses Verzeichnis muss leer sein.
- Daten sollten auf sichere Weise vom WSUS-Server mit Internetverbindung in die nicht verbundene Umgebung übertragen werden.

> [!IMPORTANT]
> Inhalte werden für alle Office 365-Sprachen heruntergeladen. Jedes Update kann ca. 10 GB an Inhalten enthalten.

## <a name="synchronize-then-decline-unneeded-office-365-updates"></a>Synchronisieren und anschließendes Ablehnen von nicht benötigten Office 365-Updates

1. Öffnen Sie auf dem mit dem Internet verbundenen WSUS-Server die WSUS-Konsole.
1. Wählen Sie **Optionen** und dann **Produkte und Klassifikationen** aus.
1. Klicken Sie auf der Registerkarte **Produkte** auf **Office 365-Client**, und klicken Sie auf der Registerkarte **Klassifizierungen** auf **Updates**. [![Produkte und Klassifizierungen für Office 365-Updates in WSUS](./media/4065163-o365-updates-product-classification.png)](./media/4065163-o365-updates-product-classification.png#lightbox)
1. Wechseln Sie zu **Synchronisierung**, und wählen Sie **Jetzt synchronisieren** aus, um die Office 365-Updates in WSUS abzurufen.
1. Wenn die Synchronisierung abgeschlossen ist, lehnen Sie alle Office 365-Updates ab, die Sie nicht mit Configuration Manager bereitstellen möchten. Sie müssen Office 365-Updates nicht genehmigen, damit diese heruntergeladen werden.  
   - Die Ablehnung von nicht gewünschten Office 365-Updates in WSUS verhindert nicht, dass diese während eines WsusUtil.exe-Exports exportiert werden. Es wird aber verhindert, dass das OfflineUpdateExporter-Tool die Inhalte für die Updates herunterlädt.
   - Das OfflineUpdateExporter-Tool führt den Download von Office 365-Updates für Sie aus. Für andere Produkte muss der Download weiterhin genehmigt werden, wenn Sie Updates für diese Produkte exportieren.
    - Erstellen Sie eine [neue Updateansicht in WSUS](https://docs.microsoft.com/windows-server/administration/windows-server-update-services/manage/viewing-and-managing-updates#to-create-a-new-update-view-on-wsus), um nicht benötigte Office 365-Updates in WSUS einfach anzeigen und ablehnen zu können.
1. Wenn Sie andere Produktupdates zum Download und Export genehmigen, warten Sie, bis die Inhalt heruntergeladen wurden, bevor Sie den WsusUtil.exe-Export ausführen und die Inhalte des WSUSContent-Ordners kopieren. Weitere Informationen finden Sie unter [Synchronisieren von Softwareupdates bei einem getrennten Softwareupdatepunkt](synchronize-software-updates-disconnected.md).

## <a name="exporting-the-office-365-updates"></a>Exportieren der Office 365-Updates

1. Kopieren Sie den OfflineUpdateExporter-Ordner aus Configuration Manager auf den mit dem Internet verbundenen WSUS-Server.
    - Das Tool und die zugehörigen Abhängigkeiten befinden sich im Verzeichnis **&lt;ConfigMgrInstallDir>/tools/OfflineUpdateExporter**.
1. Führen Sie das Tool auf dem mit dem Internet verbundenen WSUS-Server an einer Eingabeaufforderung mit folgenden Werten aus: **OfflineUpdateExporter.exe -O -D &lt;Zielpfad>**

   |Parameter für OfflineUpdateExporter|Beschreibung|
   |---|---|
   |**-O**|  **-Office**. Gibt Office 365 als Produkt für den Updateexport an.|
   |**-D**|**-Destination**. „Destination“ ist ein erforderlicher Parameter. Es wird der gesamte Pfad zum Zielordner benötigt.|

   - Das Tool **OfflineUpdateExporter** führt Folgendes aus:
      - Herstellen einer Verbindung mit WSUS
      - Lesen der Office 365-Updatemetadaten in WSUS
      - Herunterladen von Inhalten und allen von den Office 365-Updates benötigten zusätzlichen Metadaten in den Zielordner

1. Wechseln Sie an der Eingabeaufforderung auf dem mit dem Internet verbundenen WSUS-Server zu dem Ordner, der "WsusUtil.exe" enthält. Dieses Tool befindet sich standardmäßig im Ordner „%*Programme*%\Update Services\Tools“. Befindet sich das Tool beispielsweise am Standardspeicherort, geben Sie **cd %ProgramFiles%\Update Services\Tools**ein.
   - Wenn Sie Windows Server 2012 verwenden, stellen Sie sicher, dass [KB2819484](https://support.microsoft.com/help/2819484/cab-file-that-is-exported-by-using-the-wsusutil-exe-command-is-display) auf den WSUS-Servern installiert ist.
   - Der Benutzer, der das Tool „WsusUtil“ ausführt, muss Mitglied der lokalen Administratorengruppe auf dem Server sein.

1. Geben Sie Folgendes ein, um die Metadaten für Softwareupdates in eine GZIP-Datei zu exportieren:  

    **WsusUtil.exe export**  *Paketname*  *Protokolldatei*  

    Beispiel:  

    **WsusUtil.exe export export.xml.gz export.log**

1. Kopieren Sie die Datei **export.xml.gz** auf den WSUS-Server der obersten Ebene im nicht verbundenen Netzwerk.
1. Wenn Sie Updates für andere Produkte genehmigt haben, kopieren Sie den Inhalt des Ordners „WSUSContent“ in den Ordner „WSUSContent“ auf dem nicht verbundenen WSUS-Server der obersten Ebene.
1. Kopieren Sie den für **OfflineUpdateExporter** verwendeten Zielordner auf den nicht verbundenen Configuration Manager-Standortserver der obersten Ebene.

## <a name="import-the-office-365-updates"></a>Importieren der Office 365-Updates

1. Importieren Sie auf dem nicht verbundenen WSUS-Server der obersten Ebene die Updatemetadaten aus der Datei **export.xml.gz**, die Sie auf dem mit dem Internet verbundenen WSUS-Server generiert haben.
   
    Beispiel:  

    **WsusUtil.exe import export.xml.gz import.log**
    
    Das WsusUtil.exe-Tool befindet sich standardmäßig im Ordner „%*Programme*%\Update Services\Tools“.

1. Nachdem der Import abgeschlossen ist, müssen Sie auf dem nicht verbundenen Configuration Manager-Standortserver der obersten Ebene eine Eigenschaft zur Standortsteuerung konfigurieren. Diese Konfigurationsänderung verweist Configuration Manager auf die Inhalte für Office 365. So ändern Sie die Konfiguration der Eigenschaft:
   1. Kopieren Sie das [PowerShell-Skript „O365OflBaseUrlConfigured“](#bkmk_o365_script) auf den nicht verbundenen Configuration Manager-Standortserver der obersten Ebene.
   1. Ändern Sie `"D:\Office365updates\content"` in den vollständigen Pfad des kopierten Verzeichnisses, das die von OfflineUpdateExporter generierten Office-Inhalte und -Metadaten enthält.
      > [!IMPORTANT]
      > Bei der O365OflBaseUrlConfigured-Eigenschaft funktionieren nur lokale Pfade.
   1. Speichern Sie das Skript als `O365OflBaseUrlConfigured.ps1`.
   1. Führen Sie `.\O365OflBaseUrlConfigured.ps1` auf dem nicht verbundenen Configuration Manager-Standortserver der obersten Ebene in einem PowerShell-Fenster mit erhöhten Rechten aus.
   1. Starten Sie den Dienst **SMS_Executive** auf dem Standortserver neu.
1. Wechseln Sie in der **Configuration Manager**-Konsole zu **Verwaltung** > **Standortkonfiguration** > **Standorte**.
1. Klicken Sie mit der rechten Maustaste auf den Standortserver der obersten Ebene, und wählen Sie **Standortkomponenten konfigurieren**  >  **Softwareupdatepunkt** aus.
1. Wählen Sie auf der Registerkarte **Klassifizierungen** die Option *Updates* aus. Wählen Sie auf der Registerkarte **Produkte** die Option *Office 365-Client* aus.
1. [Synchronisieren von Softwareupdates](synchronize-software-updates.md#manually-start-software-updates-synchronization) für Configuration Manager
1. Wenn die Synchronisierung abgeschlossen ist, wenden Sie Ihr übliches Verfahren zum Bereitstellen von Office 365-Updates an.

## <a name="proxy-configuration"></a><a name="bkmk_O365_ki"></a> Proxykonfiguration

- Die Proxykonfiguration ist nicht nativ in das Tool integriert. Wenn auf dem Server, auf dem das Tool ausgeführt wird, in den Internetoptionen ein Proxy festgelegt ist, sollte dieser verwendet werden und ordnungsgemäß funktionieren.
   - Führen Sie `netsh winhttp show proxy` an einer Eingabeaufforderung aus, um den konfigurierten Proxy anzuzeigen.



## <a name="modify-o365oflbaseurlconfigured-property"></a><a name="bkmk_o365_script"></a> Ändern der O365OflBaseUrlConfigured-Eigenschaft

```powershell
# Name: O365OflBaseUrlConfigured.ps1
#
# Description: This sample sets the O365OflBaseUrlConfigured property for the SMS_WSUS_CONFIGURATION_MANAGER component on the top-level site.
# This script must be run on the disconnected top-level Configuration Manager site server
#
# Replace "D:\Office365updates\content" with the full path to the copied directory containing all the Office metadata and content generated by the OfflineUpdateExporter tool.
# Only local paths work for the O365OflBaseUrlConfigured property.

$PropertyValue = "D:\Office365updates\content"

# Don't change any of the lines below
$PropertyName = "O365OflBaseUrlConfigured"

# Get provider instance
$providerMachine = Get-WmiObject -namespace "root\sms" -class "SMS_ProviderLocation"

if($providerMachine -is [system.array])
{
    $providerMachine=$providerMachine[0]
}

$SiteCode = $providerMachine.SiteCode

$component = gwmi -ComputerName $providerMachine.Machine -namespace root\sms\site_$SiteCode -query 'select comp.* from sms_sci_component comp join SMS_SCI_SiteDefinition sdef on sdef.SiteCode=comp.SiteCode where sdef.ParentSiteCode="" and comp.componentname="SMS_WSUS_CONFIGURATION_MANAGER"'
$properties = $component.props

Write-host "Updating $PropertyName property for site " $SiteCode

foreach ($property in $properties)
{
  if ($property.propertyname -eq $PropertyName) 
  {
    Write-host "Current value for $PropertyName is $($property.value2)"
    $property.value2 = $PropertyValue
    Write-host "Updating value for $PropertyName to $($property.value2)"
    break
  }
}

$component.props = $properties
$component.put()
```

## <a name="next-steps"></a>Nächste Schritte

[Hinzufügen von Softwareupdates zu einer Updategruppe](../deploy-use/add-software-updates-to-an-update-group.md)