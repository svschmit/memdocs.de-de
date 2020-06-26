---
title: Verwendete Konten
titleSuffix: Configuration Manager
description: Identifizieren und verwalten Sie die Windows-Gruppen, Konten und SQL-Objekte in Configuration Manager.
ms.date: 05/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 72d7b174-f015-498f-a0a7-2161b9929198
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 176280452039fd42dfef1d63cfdbb48169cda545
ms.sourcegitcommit: 7b2f7918d517005850031f30e705e5a512959c3d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/15/2020
ms.locfileid: "84777023"
---
# <a name="accounts-used-in-configuration-manager"></a>In Configuration Manager verwendete Konten

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie die folgenden Informationen, um die in Configuration Manager verwendeten Windows-Gruppen, Konten und SQL-Objekte, deren Verwendung sowie ggf. geltende Anforderungen zu identifizieren.  

- [Windows-Gruppen, die von Configuration Manager erstellt und verwendet werden](#bkmk_groups)  
  - [Configuration Manager_CollectedFilesAccess](#configmgr_collectedfilesaccess)  
  - [Configuration Manager_DViewAccess](#configmgr_dviewaccess)  
  - [Configuration Manager-Remotesteuerungsbenutzer](#configmgr_rcusers)  
  - [SMS-Administratoren](#sms-admins)  
  - [SMS_SiteSystemToSiteServerConnection_MP_&lt;Standortcode\>](#bkmk_remotemp)  
  - [SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;Standortcode\>](#bkmk_remoteprov)  
  - [SMS_SiteSystemToSiteServerConnection_Stat_&lt;Standortcode\>](#bkmk_remotestat)  
  - [SMS_SiteToSiteConnection_&lt;Standortcode\>](#bkmk_filerepl)  

- [Konten, die von Configuration Manager verwendet werden](#bkmk_accounts)
  - [Konto für die Active Directory-Sicherheitsgruppenermittlung](#active-directory-group-discovery-account)  
  - [Konto für die Active Directory-Systemermittlung](#active-directory-system-discovery-account)  
  - [Konto für die Active Directory-Benutzerermittlung](#active-directory-user-discovery-account)  
  - [Konto für die Active Directory-Gesamtstruktur](#active-directory-forest-account)  
  - [Konto des Zertifikatregistrierungspunkts](#certificate-registration-point-account)  
  - [Konto zum Erfassen von Betriebssystemimages](#capture-os-image-account)  
  - [Clientpushinstallations-Konto](#client-push-installation-account)  
  - [Verbindungskonto des Anmeldungspunkts](#enrollment-point-connection-account)  
  - [Verbindungskonto für Exchange Server](#exchange-server-connection-account)  
  - [Verbindungskonto des Verwaltungspunkts](#management-point-connection-account)  
  - [Multicastverbindungskonto](#multicast-connection-account)  
  - [Netzwerkzugriffskonto](#network-access-account)  
  - [Paketzugriffskonto](#package-access-account)  
  - [Konto des Reporting Services-Punkts](#reporting-services-point-account)  
  - [Konten für zugelassene Viewer für Remotetools](#remote-tools-permitted-viewer-accounts)  
  - [Standortinstallationskonto](#site-installation-account)
  - [Standortsystem-Installationskonto](#site-system-installation-account)  
  - [Proxyserverkonto des Standortsystems](#site-system-proxy-server-account)  
  - [Verbindungskonto für SMTP-Server](#smtp-server-connection-account)  
  - [Verbindungskonto des Softwareupdatepunkts](#software-update-point-connection-account)  
  - [Konto des Quellstandorts](#source-site-account)  
  - [Konto der Datenbank des Quellstandorts](#source-site-database-account)  
  - [Domänenbeitrittskonto für Tasksequenzen](#task-sequence-domain-join-account)  
  - [Netzwerkordner-Verbindungskonto für Tasksequenzen](#task-sequence-network-folder-connection-account)  
  - [Ausführendes Konto für Tasksequenzen](#task-sequence-run-as-account)  

- [Benutzerobjekte, die von Configuration Manager in SQL verwendet werden](#bkmk_sqlusers)
  - [smsdbuser_ReadOnly](#smsdbuser_readonly)
  - [smsdbuser_ReadWrite](#smsdbuser_readwrite)
  - [smsdbuser_ReportSchema](#smsdbuser_reportschema)

- [Datenbankrollen, die von Configuration Manager in SQL verwendet werden](#bkmk_sqlroles)
  - [smsdbrole_AITool](#smsdbrole_aitool)
  - [smsdbrole_AIUS](#smsdbrole_aius)
  - [smsdbrole_AMTSP](#smsdbrole_amtsp)
  - [smsdbrole_CRP](#smsdbrole_crp)
  - [smsdbrole_CRPPfx](#smsdbrole_crppfx)
  - [smsdbrole_DMP](#smsdbrole_dmp)
  - [smsdbrole_DmpConnector](#smsdbrole_dmpconnector)
  - [smsdbrole_DViewAccess](#smsdbrole_dviewaccess)
  - [smsdbrole_DWSS](#smsdbrole_dwss)
  - [smsdbrole_EnrollSvr](#smsdbrole_enrollsvr)
  - [smsdbrole_extract](#smsdbrole_extract)
  - [smsdbrole_HMSUser](#smsdbrole_hmsuser)
  - [smsdbrole_MCS](#smsdbrole_mcs)
  - [smsdbrole_MP](#smsdbrole_mp)
  - [smsdbrole_MPMBAM](#smsdbrole_mpmbam)
  - [smsdbrole_MPUserSvc](#smsdbrole_mpusersvc)
  - [smsdbrole_siteprovider](#smsdbrole_siteprovider)
  - [smsdbrole_siteserver](#smsdbrole_siteserver)
  - [smsdbrole_SUP](#smsdbrole_sup)
  - [smsdbrole_WebPortal](#smsdbrole_webportal)
  - [smsschm_users](#smsschm_users)

## <a name="windows-groups-that-configuration-manager-creates-and-uses"></a><a name="bkmk_groups"></a> Windows-Gruppen, die von Configuration Manager erstellt und verwendet werden  

Die folgenden Windows-Gruppen werden von Configuration Manager automatisch erstellt und in vielen Fällen automatisch verwaltet:  

> [!NOTE]  
> Wenn von Configuration Manager eine Gruppe auf einem Computer erstellt wird, der ein Domänenmitglied ist, ist die Gruppe eine lokale Sicherheitsgruppe. Wenn der Computer ein Domänencontroller ist, ist die Gruppe eine lokale Gruppe der Domäne. Die Art der Gruppe wird für alle Domänencontroller in der Domäne freigegeben.  


### <a name="configuration-manager_collectedfilesaccess"></a><a name="configmgr_collectedfilesaccess"></a> Configuration Manager_CollectedFilesAccess

Diese Gruppe wird von Configuration Manager für den Zugriff auf Dateien verwendet, die von der Softwareinventur gesammelt wurden.  

Weitere Informationen finden Sie unter [Einführung in die Softwareinventur](../../clients/manage/inventory/introduction-to-software-inventory.md).

#### <a name="type-and-location"></a>Typ und Speicherort
Diese Gruppe ist eine lokale Sicherheitsgruppe, die auf dem primären Standortserver erstellt wurde.

Wenn Sie einen Standort deinstallieren, wird diese Gruppe nicht automatisch entfernt. Löschen Sie diese nach der Deinstallation eines Standorts manuell.

#### <a name="membership"></a>Membership
Die Gruppenmitgliedschaft wird von Configuration Manager automatisch verwaltet. In die Mitgliedschaft sind auch Administratoren eingeschlossen, denen die Berechtigung **Gesammelte Dateien anzeigen** für das sicherungsfähige Objekt **Sammlung** von einer zugewiesenen Sicherheitsrolle erteilt wurde.

#### <a name="permissions"></a>Berechtigungen
Standardmäßig besitzt diese Gruppe die **Leseberechtigung** für den folgenden Ordner auf dem Standortserver: `C:\Program Files\Microsoft Configuration Manager\sinv.box\FileCol`.  


### <a name="configuration-manager_dviewaccess"></a><a name="configmgr_dviewaccess"></a>Configuration Manager_DViewAccess  

Diese Gruppe ist eine lokale Sicherheitsgruppe, die von Configuration Manager auf dem Standortdatenbankserver oder dem Datenbankreplikatserver für einen untergeordneten primären Standort erstellt wird. Der Standort erstellt diese, wenn Sie verteilte Ansichten für die Datenbankreplikation zwischen Standorten in einer Hierarchie verwenden. Sie enthält den Standortserver und die SQL Server-Computerkonten des Standorts der zentralen Verwaltung.

Weitere Informationen finden Sie unter [Datenübertragungen zwischen Standorten](data-transfers-between-sites.md).


### <a name="configuration-manager-remote-control-users"></a><a name="configmgr_rcusers"></a> Configuration Manager-Remotesteuerungsbenutzer  

Diese Gruppe wird von Configuration Manager-Remotetools verwendet, um die Konten und Gruppen zu speichern, die Sie in der Liste **Zugelassene Viewer** einrichten. Der Standort ordnet diese Liste den verschiedenen Clients zu.  

Weitere Informationen finden Sie unter [Einführung in die Remotesteuerung](../../clients/manage/remote-control/introduction-to-remote-control.md).

#### <a name="type-and-location"></a>Typ und Speicherort
Diese Gruppe ist eine lokale Sicherheitsgruppe, die auf dem Configuration Manager-Client erstellt wird, wenn der Client eine Clientrichtlinie erhält, durch die Remotetools aktiviert werden.

Wenn Sie Remotetools für einen Client deaktivieren, wird diese Gruppe nicht automatisch entfernt. Löschen Sie diese manuell, nachdem Sie die Remotetools deaktiviert haben.

#### <a name="membership"></a>Membership
Diese Gruppe enthält standardmäßig keine Mitglieder. Wenn Sie der Liste **Zugelassene Viewer** Benutzer hinzufügen, werden die Benutzer auch dieser Gruppe automatisch hinzugefügt.

Verwenden Sie die Liste **Zugelassene Viewer**, um die Mitgliedschaft dieser Gruppe zu verwalten, anstatt dieser Gruppe direkt Benutzer oder Gruppen hinzuzufügen.

Administratoren müssen der Liste der zugelassenen Betrachter hinzugefügt werden, und sie benötigen die Berechtigung **Remotesteuerung** für das Objekt **Sammlung**. Weisen Sie diese Berechtigung mithilfe der Sicherheitsrolle **Remotetoolsverantwortlicher** zu.  

#### <a name="permissions"></a>Berechtigungen
Standardmäßig sind dieser Gruppe keinerlei Berechtigungen für Speicherorte auf dem Computer erteilt. Sie wird ausschließlich zum Speichern der Liste **Zugelassene Viewer** verwendet.  


### <a name="sms-admins"></a>SMS-Administratoren  

Configuration Manager verwendet diese Gruppe, um über WMI eine Verbindung mit dem SMS-Anbieter zu ermöglichen. Dieser Zugriff auf den SMS-Anbieter ist erforderlich, um Objekte in der Configuration Manager-Konsole anzuzeigen und zu ändern.  

> [!NOTE]  
> Durch die rollenbasierte Administrationskonfiguration eines Administrators wird bestimmt, welche Objekte der Administrator mithilfe der Configuration Manager-Konsole anzeigen und verwalten kann.  

Weitere Informationen finden Sie unter [Planen des SMS-Anbieters](plan-for-the-sms-provider.md).

#### <a name="type-and-location"></a>Typ und Speicherort
Diese Gruppe ist eine lokale Sicherheitsgruppe, die auf jedem Computer mit SMS-Anbieter erstellt wird. 

Wenn Sie einen Standort deinstallieren, wird diese Gruppe nicht automatisch entfernt. Löschen Sie diese nach der Deinstallation eines Standorts manuell.

#### <a name="membership"></a>Membership
Die Gruppenmitgliedschaft wird von Configuration Manager automatisch verwaltet. Standardmäßig sind alle Administratoren einer Hierarchie sowie das Computerkonto des Standortservers Mitglieder der Gruppe **SMS-Administratoren** auf allen SMS-Anbietercomputern an einem Standort.

#### <a name="permissions"></a>Berechtigungen
Sie können die Rechte und Berechtigungen der Gruppe „SMS-Administratoren“ mithilfe des MMC-Snap-Ins **WMI-Steuerung** anzeigen. Der Gruppe werden standardmäßig die Berechtigungen **Konto aktivieren** und **Remoteaktivierung** im WMI-Namespace `Root\SMS` erteilt. Der Gruppe „Authentifizierte Benutzer“ sind die Berechtigungen **Methoden ausführen**, **Anbieterschreibzugriff** und **Konto aktivieren** erteilt.

Wenn Sie eine Configuration Manager-Remotekonsole verwenden, konfigurieren Sie die DCOM-Berechtigungen für eine **Remoteaktivierung** auf dem Standortservercomputer und dem SMS-Anbieter. Erteilen Sie diese Berechtigungen der Gruppe **SMS-Administratoren**. Hierdurch wird die Verwaltung im Vergleich zum direkten Erteilen dieser Berechtigungen an Benutzer und Gruppen erleichtert. Weitere Informationen finden Sie unter [Konfigurieren von DCOM-Berechtigungen für Configuration Manager-Remotekonsolen](../../servers/manage/modify-your-infrastructure.md#BKMK_ConfigDCOMforRemoteConsole). 


### <a name="sms_sitesystemtositeserverconnection_mp_ltsitecode"></a><a name="bkmk_remotemp"></a> SMS_SiteSystemToSiteServerConnection_MP_&lt;Standortcode\>  
 
Diese Gruppe wird von Verwaltungspunkten, die sich außerhalb des Standortservers befinden, zum Herstellen einer Verbindung mit der Standortdatenbank verwendet. Mithilfe dieser Gruppe wird den Verwaltungspunkten ein Zugriff auf den Ordner Eingangsbox des Standortservers sowie der Standortdatenbank ermöglicht.  

#### <a name="type-and-location"></a>Typ und Speicherort
Diese Gruppe ist eine lokale Sicherheitsgruppe, die auf jedem Computer mit SMS-Anbieter erstellt wird.

Wenn Sie einen Standort deinstallieren, wird diese Gruppe nicht automatisch entfernt. Löschen Sie diese nach der Deinstallation eines Standorts manuell.

#### <a name="membership"></a>Membership
Die Gruppenmitgliedschaft wird von Configuration Manager automatisch verwaltet. Standardmäßig sind die Computerkonten von Remotecomputern mit einem Verwaltungspunkt für den Standort in die Mitgliedschaft eingeschlossen.

#### <a name="permissions"></a>Berechtigungen
Diese Gruppe verfügt standardmäßig über die Berechtigungen **Lesen**, **Lesen & Ausführen** und **Ordnerinhalt auflisten** für den folgenden Order auf dem Standortserver: `C:\Program Files\Microsoft Configuration Manager\inboxes`. Dieser Gruppe wurde die zusätzliche Berechtigung **Schreiben** für Unterordner von **inboxes**, in die vom Verwaltungspunkt Clientdaten geschrieben werden, erteilt.


### <a name="sms_sitesystemtositeserverconnection_smsprov_ltsitecode"></a><a name="bkmk_remoteprov"></a> SMS_SiteSystemToSiteServerConnection_SMSProv_&lt;Standortcode\>  
 
Remotecomputer des SMS-Anbieters verwenden diese Gruppe, um eine Verbindung mit dem Standortserver herzustellen.  

#### <a name="type-and-location"></a>Typ und Speicherort
Diese Gruppe ist eine lokale Sicherheitsgruppe, die auf dem Standortserver erstellt wurde.

Wenn Sie einen Standort deinstallieren, wird diese Gruppe nicht automatisch entfernt. Löschen Sie diese nach der Deinstallation eines Standorts manuell.

#### <a name="membership"></a>Membership
Die Gruppenmitgliedschaft wird von Configuration Manager automatisch verwaltet. Die Mitgliedschaft umfasst standardmäßig das Computerkonto oder ein Domänenbenutzerkonto. Dieses Konto wird verwendet, um von jedem SMS-Remoteanbieter aus eine Verbindung mit dem Standortserver herzustellen.

#### <a name="permissions"></a>Berechtigungen
Diese Gruppe verfügt standardmäßig über die Berechtigungen **Lesen**, **Lesen & Ausführen** und **Ordnerinhalt auflisten** für den folgenden Order auf dem Standortserver: `C:\Program Files\Microsoft Configuration Manager\inboxes`. Diese Gruppe besitzt für Unterordner der Posteingänge zusätzlich die Berechtigungen **Schreiben** und **Ändern**. Der SMS-Anbieter benötigt Zugriff auf diese Ordner.

Diese Gruppe besitzt für die Unterordner von `C:\Program Files\Microsoft Configuration Manager\OSD\Bin` auf dem Standortserver außerdem die Berechtigung **Lesen**. 

Sie besitzt ebenfalls folgende Berechtigungen für die Unterordner von `C:\Program Files\Microsoft Configuration Manager\OSD\boot`:
- **Lesen**  
- **Lesen & ausführen**  
- **Ordnerinhalt auflisten**  
- **Schreiben**  
- **Änderung**   


### <a name="sms_sitesystemtositeserverconnection_stat_ltsitecode"></a><a name="bkmk_remotestat"></a> SMS_SiteSystemToSiteServerConnection_Stat_&lt;Standortcode\>  

Diese Gruppe wird vom Datei-Verteilungs-Manager auf Computern in Configuration Manager-Remotestandortsystemen zum Herstellen einer Verbindung mit dem Standortserver verwendet.  

#### <a name="type-and-location"></a>Typ und Speicherort
Diese Gruppe ist eine lokale Sicherheitsgruppe, die auf dem Standortserver erstellt wurde.

Wenn Sie einen Standort deinstallieren, wird diese Gruppe nicht automatisch entfernt. Löschen Sie diese nach der Deinstallation eines Standorts manuell.

#### <a name="membership"></a>Membership
Die Gruppenmitgliedschaft wird von Configuration Manager automatisch verwaltet. Die Mitgliedschaft umfasst standardmäßig das Computerkonto oder das Domänenbenutzerkonto. Diese Konto wird verwendet, um von jedem Remotestandortsystem aus, auf dem der Datei-Verteilungs-Manager ausgeführt wird, auf den Standortserver zugreifen zu können.

#### <a name="permissions"></a>Berechtigungen
Diese Gruppe verfügt standardmäßig über die Berechtigungen **Lesen**, **Lesen & Ausführen** und **Ordnerinhalt auflisten** für den folgenden Order und dessen Unterordner auf dem Standortserver: `C:\Program Files\Microsoft Configuration Manager\inboxes`. 

Diese Gruppe besitzt zusätzlich die Berechtigungen **Schreiben** und **Ändern** für folgenden Ordner auf dem Standortserver: `C:\Program Files\Microsoft Configuration Manager\inboxes\statmgr.box`.


### <a name="sms_sitetositeconnection_ltsitecode"></a><a name="bkmk_filerepl"></a> SMS_SiteToSiteConnection_&lt;Standortcode\>  
Diese Gruppe wird von Configuration Manager verwendet, um die dateibasierte Replikation zwischen Standorten innerhalb einer Hierarchie zu aktivieren. Für jeden Remotestandort, von dem Dateien direkt an diesen Standort übertragen werden, verfügt diese Gruppe über Konten, die als **Dateireplikationskonto** eingerichtet sind.  

#### <a name="type-and-location"></a>Typ und Speicherort
Diese Gruppe ist eine lokale Sicherheitsgruppe, die auf dem Standortserver erstellt wurde.

#### <a name="membership"></a>Membership
Wenn Sie einen neuen Standort als untergeordneten Standort eines anderen Standorts installieren, wird das Computerkonto des neuen Standortservers von Configuration Manager automatisch der Gruppe auf dem übergeordneten Standortserver hinzugefügt. Außerdem fügt Configuration Manager das Computerkonto des übergeordneten Standorts der Gruppe auf dem neuen Standortserver hinzu. Wenn Sie ein anderes Konto für dateibasierte Übertragungen angeben, fügen Sie dieses Konto der Gruppe auf dem Zielstandortserver hinzu.

Wenn Sie einen Standort deinstallieren, wird diese Gruppe nicht automatisch entfernt. Löschen Sie diese nach der Deinstallation eines Standorts manuell.

#### <a name="permissions"></a>Berechtigungen
Standardmäßig besitzt diese Gruppe die Berechtigung **Vollzugriff** für folgenden Ordner: `C:\Program Files\Microsoft Configuration Manager\inboxes\despoolr.box\receive`.



## <a name="accounts-that-configuration-manager-uses"></a><a name="bkmk_accounts"></a> Konten, die von Configuration Manager verwendet werden  

Sie können die folgenden Konten für Configuration Manager einrichten.  

> [!TIP]
> Verwenden Sie kein Prozentzeichen (`%`) im Kennwort für Konten, die Sie in der Configuration Manager-Konsole angeben. Das Konto kann ansonsten nicht authentifiziert werden.<!-- SCCMDocs#1032 -->

### <a name="active-directory-group-discovery-account"></a>Konto für die Active Directory-Sicherheitsgruppenermittlung  

Der Standort verwendet das **Konto für die Active Directory-Sicherheitsgruppenermittlung**, um folgende Objekte an den von Ihnen angegebenen Orten in Active Directory Domain Services zu ermitteln:
- Lokale, globale und universelle Sicherheitsgruppen
- Die Mitgliedschaft in diesen Gruppen
- Die Mitgliedschaft in Verteilergruppen
  - Verteilergruppen werden nicht als Gruppenressourcen ermittelt.

Bei diesem Konto kann es sich um das Computerkonto des Standortservers, von dem die Ermittlung ausgeführt wird, oder um ein Windows-Benutzerkonto handeln. Sie benötigen die Zugriffsberechtigung **Lesen** für die Active Directory-Orte, die Sie für die Ermittlung angeben.  

Weitere Informationen finden Sie unter [Active Directory-Gruppenermittlung](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutGroup).


### <a name="active-directory-system-discovery-account"></a>Konto für die Active Directory-Systemermittlung  

Der Standort verwendet das **Konto für die Active Directory-Systemermittlung**, um Computer an den von Ihnen angegebenen Orten in Active Directory Domain Services zu ermitteln.  

Bei diesem Konto kann es sich um das Computerkonto des Standortservers, von dem die Ermittlung ausgeführt wird, oder um ein Windows-Benutzerkonto handeln. Sie benötigen die Zugriffsberechtigung **Lesen** für die Active Directory-Orte, die Sie für die Ermittlung angeben.  

Weitere Informationen finden Sie unter [Active Directory-Systemermittlung](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutSystem).


### <a name="active-directory-user-discovery-account"></a>Konto für die Active Directory-Benutzerermittlung  
 
Der Standort verwendet das **Konto für die Active Directory-Benutzerermittlung**, um Benutzerkonten an den von Ihnen angegebenen Orten in Active Directory Domain Services zu ermitteln.  

Bei diesem Konto kann es sich um das Computerkonto des Standortservers, von dem die Ermittlung ausgeführt wird, oder um ein Windows-Benutzerkonto handeln. Sie benötigen die Zugriffsberechtigung **Lesen** für die Active Directory-Orte, die Sie für die Ermittlung angeben.  

Weitere Informationen finden Sie unter [Active Directory-Benutzerermittlung](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser). 


### <a name="active-directory-forest-account"></a>Konto für die Active Directory-Gesamtstruktur  

Der Standort verwendet das **Konto für die Active Directory-Gesamtstruktur**, um die Netzwerkinfrastruktur von Active Directory-Gesamtstrukturen zu ermitteln. Es wird auch von zentralen Verwaltungsstandorten und primären Standorten verwendet, um Standortdaten für Active Directory-Domänendienste für eine Gesamtstruktur zu veröffentlichen.  

> [!NOTE]  
> Die Veröffentlichung in Active Directory durch sekundäre Standorte erfolgt immer über das Computerkonto des sekundären Standortservers.  

Beim Konto für die Active Directory-Gesamtstruktur muss es sich um ein globales Konto handeln, damit die Ermittlung und Veröffentlichung in nicht vertrauenswürdigen Gesamtstrukturen möglich sind. Wenn Sie nicht das Computerkonto des Standortservers verwenden, können Sie nur ein globales Konto auswählen.  

Für dieses Konto ist die Berechtigung **Lesen** für jede Active Directory-Gesamtstruktur, in der die Netzwerkinfrastruktur ermittelt werden soll, erforderlich.  

Außerdem ist die Berechtigung **Vollzugriff** für den Container **System Management** und all seine untergeordneten Objekte in jeder Active Directory-Gesamtstruktur erforderlich, in der Standortdaten veröffentlicht werden sollen. Weitere Informationen finden Sie unter [Vorbereiten von Active Directory für die Veröffentlichung eines Standorts](../network/extend-the-active-directory-schema.md).  

Weitere Informationen finden Sie unter [Active Directory-Gesamtstrukturermittlung](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest).


### <a name="certificate-registration-point-account"></a>Konto des Zertifikatregistrierungspunkts  

Der Zertifikatregistrierungspunkt verwendet das **Konto des Zertifikatregistrierungspunkts**, um eine Verbindung mit der Configuration Manager-Datenbank herzustellen. Er verwendet standardmäßig das Computerkonto, Sie können jedoch stattdessen ein Benutzerkonto konfigurieren. Wenn der Zertifikatregistrierungspunkt sich in einer nicht vertrauenswürdigen Domäne des Standortservers befindet, müssen Sie ein Benutzerkonto angeben. Für dieses Konto ist nur der **Lesezugriff** auf die Standortdatenbank erforderlich, da Schreibvorgänge vom Zustandsmeldungssystem abgewickelt werden.  

Weitere Informationen finden Sie unter [Einführung in Zertifikatprofile](../../../protect/deploy-use/introduction-to-certificate-profiles.md).


### <a name="capture-os-image-account"></a>Konto zum Erfassen von Betriebssystemimages  

Wenn Sie ein Betriebssystemimage erfassen, verwendet Configuration Manager das **Konto zum Erfassen von Betriebssystemimages**, um auf den Ordner zuzugreifen, in dem erfasste Images gespeichert werden. Wenn Sie den Schritt **Betriebssystemimage erfassen** zur Tasksequenz hinzufügen, ist dieses Konto erforderlich.  

Das Konto muss die Berechtigungen **Lesen** und **Schreiben** für die Netzwerkfreigabe aufweisen, in der erfasste Images gespeichert werden.  

Falls Sie das Kennwort des Kontos in Windows ändern, aktualisieren Sie die Tasksequenz mit dem neuen Kennwort. Der Configuration Manager-Client erhält das neue Kennwort beim nächsten Download der Clientrichtlinie.  

Wenn Sie dieses Konto verwenden müssen, erstellen Sie ein Domänenbenutzerkonto. Erteilen Sie diesem die mindestens erforderlichen Berechtigungen, um auf die benötigten Netzwerkressourcen zuzugreifen, und werden Sie es für alle Tasksequenzen, die zum Erfassen verwendet werden.  

> [!IMPORTANT]  
> Weisen Sie diesem Konto keine Rechte zur interaktiven Anmeldung zu.  
>   
> Verwenden Sie für dieses Konto nicht das Netzwerkzugriffskonto.  

Weitere Informationen finden Sie unter [Erstellen einer Tasksequenz zum Erfassen eines Betriebssystems](../../../osd/deploy-use/create-a-task-sequence-to-capture-an-operating-system.md).


### <a name="client-push-installation-account"></a>Clientpushinstallations-Konto  

Wenn Sie Clients mithilfe der Clientpushinstallation bereitstellen, verwendet der Standort das **Clientpushinstallations-Konto**, um eine Verbindung mit Computern herzustellen und die Configuration Manager-Clientsoftware zu installieren. Wenn Sie dieses Konto nicht angeben, versucht der Standortserver, das Computerkonto zu verwenden.  

Dieses Konto muss ein Mitglied der lokalen Gruppe **Administratoren** auf den angezielten Clientcomputern sein. Für dieses Konto sind keine **Domänenadministratorrechte** erforderlich.  

Sie können mehr als ein Clientpushinstallations-Konto angeben. Configuration Manager probiert diese nacheinander aus, bis eines funktioniert.  

> [!TIP]  
> Wenn Ihre Active Directory-Umgebung groß ist und Sie dieses Konto ändern müssen, gehen Sie folgendermaßen vor, um das Update des Kontos effektiver zu koordinieren: 
> 1. Erstellen Sie ein neues Konto mit einem anderen Namen.   
> 2. Fügen Sie das neue Konto zur Liste der Clientpushinstallations-Konten in Configuration Manager hinzu.  
> 3. Geben Sie Active Directory Domain Services etwas Zeit, um das neue Konto zu replizieren.  
> 4. Entfernen Sie anschließend das alte Konto aus Configuration Manager und Active Directory Domain Services  

> [!IMPORTANT]  
> Erteilen Sie diesem Konto nicht das Recht, sich lokal anzumelden.  

Weitere Informationen finden Sie unter [Clientpushinstallation](../../clients/deploy/plan/client-installation-methods.md#client-push-installation).


### <a name="enrollment-point-connection-account"></a>Verbindungskonto des Anmeldungspunkts  

Der Anmeldungspunkt verwendet das **Verbindungskonto des Anmeldungspunkts**, um eine Verbindung mit der Configuration Manager-Standortdatenbank herzustellen. Er verwendet standardmäßig das Computerkonto, Sie können jedoch stattdessen ein Benutzerkonto konfigurieren. Wenn der Anmeldungspunkt sich in einer nicht vertrauenswürdigen Domäne des Standortservers befindet, müssen Sie ein Benutzerkonto angeben. Für dieses Konto sind **Lese**- und **Schreibzugriff** auf die Standortdatenbank erforderlich.  

Weitere Informationen finden Sie unter [Installieren von Standortsystemrollen für die lokale Verwaltung mobiler Geräte](../../../mdm/get-started/install-site-system-roles-for-on-premises-mdm.md).


### <a name="exchange-server-connection-account"></a>Verbindungskonto für Exchange Server  

Der Standortserver verwendet das **Verbindungskonto für Exchange Server**, um eine Verbindung mit dem angegebenen Server von Exchange Server herzustellen. Diese Verbindung wird verwendet, um mobile Geräte zu suchen und zu verwalten, die mit Exchange Server verbunden sind. Für dieses Konto sind Exchange PowerShell-Cmdlets erforderlich, mit deren Hilfe dem Exchange Server-Computer die erforderlichen Berechtigungen bereitgestellt werden. Weitere Informationen zu den Cmdlets finden Sie unter [Installieren und Konfigurieren des Exchange Connectors](../../../mdm/deploy-use/install-configure-exchange-connector.md).  


### <a name="management-point-connection-account"></a>Verbindungskonto des Verwaltungspunkts  

Der Verwaltungspunkt verwendet das **Verbindungskonto des Verwaltungspunkts**, um eine Verbindung mit der Configuration Manager-Standortdatenbank herzustellen. Diese Verbindung wird verwendet, um Informationen für Clients zu senden und abzurufen. Der Verwaltungspunkt verwendet standardmäßig das Computerkonto, Sie können jedoch stattdessen ein Benutzerkonto konfigurieren. Wenn der Verwaltungspunkt sich in einer nicht vertrauenswürdigen Domäne des Standortservers befindet, müssen Sie ein Benutzerkonto angeben.  

Erstellen Sie das Konto als lokales Konto auf dem Computer, auf dem Microsoft SQL Server ausgeführt wird, und statten Sie es nur mit geringen Rechten aus.  

> [!IMPORTANT]  
> Erteilen Sie diesem Konto keine Rechte zur interaktiven Anmeldung.  


### <a name="multicast-connection-account"></a>Multicastverbindungskonto  

Multicastfähige Verbindungspunkte verwenden das **Multicastverbindungskonto**, um Informationen aus der Standortdatenbank zu lesen. Der Server verwendet standardmäßig das Computerkonto, Sie können jedoch stattdessen ein Benutzerkonto konfigurieren. Wenn die Standortdatenbank sich in einer nicht vertrauenswürdigen Gesamtstruktur befindet, müssen Sie ein Benutzerkonto angeben. Wenn Ihr Rechenzentrum beispielsweise über ein Umkreisnetzwerk in einer anderen Gesamtstruktur als der des Standortservers und der Standortdatenbank verfügt, können Sie mit diesem Konto die Multicastinformationen aus der Standortdatenbank lesen.  

Wenn Sie dieses Konto benötigen, sollten Sie es als lokales Konto mit geringen Rechten auf dem Computer erstellen, auf dem Microsoft SQL Server ausgeführt wird.  

> [!IMPORTANT]  
> Erteilen Sie diesem Konto keine Rechte zur interaktiven Anmeldung.  

Weitere Informationen finden Sie unter [Verwenden von Multicast zum Bereitstellen von Windows über das Netzwerk](../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).


### <a name="network-access-account"></a>Netzwerkzugriffskonto  

Clientcomputer verwenden das **Netzwerkzugriffskonto**, wenn über ihr lokales Computerkonto kein Zugriff auf Inhalte auf Verteilungspunkten möglich ist. Dies gilt vor allem für Arbeitsgruppenclients und Computer aus nicht vertrauenswürdigen Domänen. Dieses Konto wird ebenfalls während der Betriebssystembereitstellung verwendet, wenn der Computer, auf dem das Betriebssystem installiert wird, noch kein Computerkonto in der Domäne besitzt.  

> [!Important]  
> Das Netzwerkzugriffskonto wird nie als Sicherheitskontext zum Ausführen von Programmen, Installieren von Softwareupdates oder Ausführen von Tasksequenzen verwendet. Es wird nur für den Zugriff auf Ressourcen im Netzwerk verwendet.  

Ein Konfigurations-Manager-Client versucht zunächst, das Computerkonto zu verwenden, um den Inhalt herunterzuladen. Wenn dieser Vorgang fehlschlägt, wird automatisch ein erneuter Versuch mit dem Netzwerkzugriffskonto gestartet.  

Wenn Sie den Standort für HTTPS oder [erweitertes HTTP](enhanced-http.md) konfigurieren, kann eine Arbeitsgruppe oder ein mit Azure AD verknüpfter Client ohne Netzwerkzugriffskonto sicher von Verteilungspunkten auf Inhalt zugreifen. Dieses Verhalten umfasst die Bereitstellung von Betriebssystemen mit einer Tasksequenz, die über Startmedien, PXE oder das Softwarecenter ausgeführt wird.<!--1358228,1358278--> Weitere Informationen finden Sie unter [Kommunikation zwischen Client und Verwaltungspunkt](communications-between-endpoints.md#bkmk_client2mp).<!-- SCCMDocs#1345 -->

> [!Note]  
> Wenn Sie **Erweitertes HTTP** so konfigurieren, dass kein Netzwerkzugriffskonto erforderlich ist, muss auf dem Verteilungspunkt Windows Server 2012 oder höher ausgeführt werden. <!--SCCMDocs-pr issue #2696-->
>  
> Aktualisieren Sie Ihre Clients mindestens auf Version 1806, bevor Sie diese Funktion aktivieren. Wenn Sie nur Verbindungen mit **erweitertem HTTP** zulassen, können ältere Clients sich mithilfe dieser Methode nicht authentifizieren und somit keine Clientupgradepakete von Verteilungspunkten herunterladen. <!--vso2841213-->   

#### <a name="permissions"></a>Berechtigungen

Weisen Sie diesem Konto die minimal erforderlichen Berechtigungen für den Inhalt zu, der vom Client für den Zugriff auf die Software benötigt wird. Das Konto muss über die Berechtigung **Auf diesen Computer vom Netzwerk aus zugreifen** für den Verteilungspunkt verfügen. Sie können bis zu 10 Netzwerkzugriffskonten pro Standort konfigurieren.  

Erstellen Sie das Konto in einer Domäne, die den erforderlichen Zugriff auf Ressourcen ermöglicht. Das Netzwerkzugriffskonto muss immer einen Domänennamen enthalten. Pass-Through-Sicherheit wird für dieses Konto nicht unterstützt. Wenn es Verteilungspunkte in mehreren Domänen gibt, erstellen Sie das Konto in einer vertrauenswürdigen Domäne.  

> [!TIP]  
> Zur Vermeidung von Kontosperrungen sollten Sie das Kennwort für ein vorhandenes Netzwerkzugriffskonto nicht ändern. Erstellen Sie stattdessen ein neues Konto, und richten Sie das neue Konto in Configuration Manager ein. Wenn genügend Zeit verstrichen ist, sodass alle Clients die neuen Kontodetails empfangen haben, entfernen Sie das alte Konto aus den freigegebenen Netzwerkordnern, und löschen Sie es.  

> [!IMPORTANT]  
> Erteilen Sie diesem Konto keine Rechte zur interaktiven Anmeldung.  
>   
> Gewähren Sie diesem Konto nicht das Recht, der Domäne Computer hinzuzufügen. Wenn während einer Tasksequenz Computer der Domäne beitreten müssen, verwenden Sie hierfür das [Domänenbeitrittskonto für Tasksequenzen](#task-sequence-domain-join-account).  

#### <a name="configure-the-network-access-account"></a>Konfigurieren des Netzwerkzugriffskontos  

1.  Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Standorte** aus. Wählen Sie dann den Standort aus.  

2.  Klicken Sie in der Gruppe **Einstellungen** auf das Menüband, und klicken Sie anschließend auf **Standortkomponenten konfigurieren**und dann auf **Softwareverteilung**.  

3.  Wählen Sie die Registerkarte **Netzwerkzugriffskonto** aus. Konfigurieren Sie mindestens ein Konto, und wählen Sie dann **OK**.  


### <a name="package-access-account"></a>Paketzugriffskonto  

Mit einem **Paketzugriffskonto** können Sie durch Festlegen von NTFS-Berechtigungen angeben, welche Benutzer und Benutzergruppen auf Paketinhalte auf Verteilungspunkten zugreifen können. Standardmäßig wird in Configuration Manager nur Zugriff auf die allgemeinen Zugriffskonten **Benutzer** und **Administratoren** gewährt. Sie können den Zugriff für Clientcomputer über zusätzliche Windows-Konten oder -Gruppen steuern. Mobile Geräte rufen Paketinhalte immer anonym ab und verwenden daher kein Paketzugriffskonto.  

Wenn die Inhaltsdateien von Configuration Manager auf einen Verteilungspunkt kopiert werden, werden standardmäßig die folgenden Berechtigungen erteilt: **Lesen** für die lokale Gruppe **Benutzer** und **Vollzugriff** für die lokale Gruppe **Administratoren**. Die tatsächlich erforderlichen Berechtigungen hängen vom jeweiligen Paket ab. Von Clients in Arbeitsgruppen oder nicht vertrauenswürdigen Gesamtstrukturen wird das Netzwerkzugriffskonto zum Zugriff auf den Paketinhalt verwendet. Stellen Sie anhand der definierten Paketzugriffskonten sicher, dass das Netzwerkzugriffskonto über Berechtigungen für das Paket verfügt.  

Verwenden Sie Konten in einer Domäne mit Zugriff auf die Verteilungspunkte. Wenn Sie das Konto nach der Paketerstellung erstellen oder ändern, müssen Sie das Paket erneut verteilen. Beim Aktualisieren des Pakets werden die NTFS-Berechtigungen für das Paket nicht geändert.  

Das Netzwerkzugriffskonto muss nicht als Paketzugriffskonto hinzugefügt werden, da es Mitglied der Gruppe **Benutzer** ist und somit standardmäßig hinzugefügt wird. Der Zugriff von Clients auf das Paket kann nicht dadurch verhindert werden, dass das Paketzugriffskonto auf das Netzwerkzugriffskonto beschränkt wird.  

#### <a name="manage-package-access-accounts"></a>Verwalten von Paketzugriffskonten  

1.  Wählen Sie in der Configuration Manager-Konsole die Option **Softwarebibliothek** aus.  

2.  Legen Sie im Arbeitsbereich **Softwarebibliothek** den Typ des Inhalts fest, für den Sie Zugriffskonten verwalten möchten, und befolgen Sie die angegebenen Schritte:  

    - **Anwendung:** Erweitern Sie **Anwendungsverwaltung**, klicken Sie auf **Anwendung**, und wählen Sie dann die Anwendungen aus, für die Sie Zugriffskonten verwalten möchten.  

    - **Paket:** Erweitern Sie **Anwendungsverwaltung**, klicken Sie auf **Pakete**, und wählen Sie dann die Pakete aus, für die Sie Zugriffskonten verwalten möchten.  

    - **Softwareupdate-Bereitstellungspakete:** Erweitern Sie **Softwareupdates**, klicken Sie auf **Bereitstellungspakete**, und wählen Sie dann die Bereitstellungspakete aus, für die Sie Zugriffskonten verwalten möchten.  

    - **Treiberpaket:** Erweitern Sie **Betriebssysteme**, klicken Sie auf **Treiberpakete**, und wählen Sie dann die Treiberpakete aus, für die Sie Zugriffskonten verwalten möchten.  

    - **Betriebssystemabbild:** Erweitern Sie **Betriebssysteme**, klicken Sie auf **Betriebssystemabbilder**, und wählen Sie dann die Betriebssystemimages aus, für die Sie Zugriffskonten verwalten möchten.  

    - **Betriebssystem-Upgradepaket:** Erweitern Sie **Betriebssysteme**, klicken Sie auf **Betriebssysteminstallationspakete**, und wählen Sie dann die Betriebssystem-Upgradepakete aus, für die Sie Zugriffskonten verwalten möchten.  

    - **Startimage:** Erweitern Sie **Betriebssysteme**, klicken Sie auf **Startabbilder**, und wählen Sie dann das Startimage aus, für das Sie Zugriffskonten verwalten möchten.  

3.  Klicken Sie mit der rechten Maustaste auf das ausgewählte Objekt, und wählen Sie dann **Zugriffskonten verwalten**.  

4.  Geben Sie im Dialogfeld **Konto hinzufügen** den Kontotyp an, dem Zugriff auf den Inhalt gewährt werden soll, und geben Sie dann die Zugriffsrechte an, die dem Konto zugeordnet sind.  

    > [!NOTE]  
    > Wenn Sie einen Benutzernamen für das Konto hinzufügen und Configuration Manager sowohl ein lokales Benutzerkonto als auch ein Domänenbenutzerkonto mit diesem Namen findet, legt Configuration Manager Zugriffsrechte für das Domänenbenutzerkonto fest.  


### <a name="reporting-services-point-account"></a>Konto des Reporting Services-Punkts  
 
Das **Konto des Reporting Services-Punkts** wird von SQL Server Reporting Services zum Abrufen der Daten für Configuration Manager-Berichte aus der Standortdatenbank verwendet. Das von Ihnen angegebene Windows-Benutzerkonto und das dazugehörende Kennwort werden verschlüsselt und in der SQL Server Reporting Services-Datenbank gespeichert.  

> [!NOTE]  
> Das angegebene Konto muss auf dem Computer, auf dem die Reporting Services-Datenbank gehostet wird, über die Berechtigung zur **lokalen Anmeldung** verfügen.

> [!NOTE]  
> Indem das Konto in der Configuration Manager-Datenbank zur SQL-Datenbank-Rolle „smsschm_users“ hinzugefügt wird, erhält es automatisch alle erforderlichen Rechte.

Weitere Informationen finden Sie unter [Einführung in die Berichterstellung](../../servers/manage/introduction-to-reporting.md).


### <a name="remote-tools-permitted-viewer-accounts"></a>Informationen zu Konten für zugelassene Viewer für Remotetools  

Bei den Konten, die Sie als **Zugelassene Betrachter** für die Remotesteuerung festlegen, handelt es sich um eine Liste der Benutzer, die die Remotetoolsfunktion auf Clients verwenden dürfen.  

Weitere Informationen finden Sie unter [Einführung in die Remotesteuerung](../../clients/manage/remote-control/introduction-to-remote-control.md).


### <a name="site-installation-account"></a>Standortinstallationskonto
<!--SCCMDocs issue #572-->
Verwenden Sie ein Domänenbenutzerkonto, um sich bei dem Server anzumelden, auf dem das Setup von Configuration Manager ausgeführt wird, und installieren Sie einen neuen Standort.

Für dieses Konto sind folgende Rechte erforderlich:  

- **Administrator** auf den folgenden Servern:
    - Der Standortserver  
    - Jedem Server, der die Standortdatenbank hostet  
    - Jeder Instanz des SMS-Anbieters für den Standort  

- **Sysadmin** für die SQL Server-Instanz, die die Standortdatenbank hostet  

Das Setup von Configuration Manager fügt dieses Konto automatisch zur Gruppe [SMS-Administratoren](#sms-admins) hinzu.

Nach der Installation ist dieses Konto der einzige Benutzer mit Berechtigungen für die Configuration Manager-Konsole. Wenn Sie dieses Konto entfernen müssen, sollten Sie dessen Rechte zuvor an einen anderen Benutzer übertragen.

Wenn ein eigenständiger Standort um einen Standort der zentralen Verwaltung erweitert wird, benötigt dieses Konto die rollenbasierten Administratorrechte **Hauptadministrator** oder **Infrastrukturadministrator** auf dem eigenständigen primären Standort.


### <a name="site-system-installation-account"></a>Standortsystem-Installationskonto  

Die **Standortsystem-Installationskonten** werden vom Standortserver zur Installation, erneuten Installation, Deinstallation und Einrichtung von Standortsystemen verwendet. Wenn Sie das Standortsystem so einrichten, dass Verbindungen mit diesem Standortsystem vom Standortserver initiiert werden müssen, wird dieses Konto von Configuration Manager auch dazu verwendet, Daten nach der Installation des Standortsystems und der Rollen vom Standortsystem abzurufen. Jedes Standortsystem kann ein anderes Installationskonto aufweisen. Sie können aber nur ein Installationskonto für die Verwaltung aller Rollen in diesem Standortsystem einrichten.  

Für dieses Konto sind lokale Administratorberechtigungen auf den angezielten Standortsystemen erforderlich. Darüber hinaus muss dieses Konto die Berechtigung **Auf diesen Computer vom Netzwerk aus zugreifen** in der Sicherheitsrichtlinie auf den angezielten Standortsystemen aufweisen.  

> [!TIP]  
> Falls Sie mit vielen Domänencontrollern arbeiten und diese Konten domänenübergreifend verwendet werden, überprüfen Sie vor dem Setup des Standortsystems, ob Active Directory diese Konten repliziert hat.  
>   
> Das Festlegen eines lokalen Kontos auf den zu verwaltenden Standortsystemen bietet ein höheres Maß an Sicherheit als der Einsatz von Domänenkonten. Dadurch wird der Schaden reduziert, den Angreifer anrichten können, wenn das Konto kompromittiert ist. Allerdings sind Domänenkonten einfacher zu verwalten. Berücksichtigen Sie den Kompromiss zwischen Sicherheit und effektiver Verwaltung.  


### <a name="site-system-proxy-server-account"></a>Proxyserverkonto des Standortsystems
<!--SCCMDocs issue #648-->
Die folgenden Standortsystemrollen verwenden das **Proxyserverkonto des Standortsystems**, um über einen Proxyserver oder eine Firewall, für die ein authentifizierter Zugriff erforderlich ist, auf das Internet zuzugreifen:

- Asset Intelligence-Synchronisierungspunkt
- Exchange Server-Connector
- Dienstverbindungspunkt
- Softwareupdatepunkt

> [!IMPORTANT]  
> Geben Sie ein Konto mit den geringstmöglichen Berechtigungen für den erforderlichen Proxyserver bzw. für die erforderliche Firewall an.  

Weitere Informationen finden Sie unter [Unterstützung von Proxyservern](../network/proxy-server-support.md).


### <a name="smtp-server-connection-account"></a>Verbindungskonto für SMTP-Server  

Über das **Verbindungskonto für SMTP-Server** werden vom Standortserver per E-Mail Warnungen an den SMTP-Server gesendet, wenn für den SMTP-Server ein authentifizierter Zugriff erforderlich ist.  

> [!IMPORTANT]  
> Geben Sie ein Konto mit den geringstmöglichen Berechtigungen zum Senden von E-Mails an.  

Weitere Informationen finden Sie unter [Verwenden von Benachrichtigungen und Statussystem](../../servers/manage/use-alerts-and-the-status-system.md).


### <a name="software-update-point-connection-account"></a>Verbindungskonto des Softwareupdatepunkts  

Das **Verbindungskonto des Softwareupdatepunkts** wird vom Standortserver für die beiden folgenden Softwareupdatedienste verwendet:  

- Die Windows Server Update Services (WSUS), die Einstellungen wie Produktdefinitionen, Klassifizierungen und Upstreameinstellungen einrichten  

- WSUS-Synchronisierungs-Manager, von dem bei einem WSUS-Upstreamserver oder Microsoft Update eine Synchronisierung angefordert wird  

Mit dem [Standortsystem-Installationskonto](#site-system-installation-account) können zwar Komponenten für Softwareupdates installiert, aber keine softwareupdatespezifischen Funktionen auf dem Softwareupdatepunkt ausgeführt werden. Falls Sie das Computerkonto des Standortservers für diese Funktion nicht verwenden können, weil sich der Softwareupdatepunkt in einer nicht vertrauenswürdigen Gesamtstruktur befindet, müssen Sie dieses Konto zusätzlich zum Standortsystem-Installationskonto angeben.  

Dieses Konto muss ein lokaler Administrator auf dem Computer sein, auf dem Sie WSUS installieren. Zudem muss es Teil der lokalen Gruppe **WSUS-Administratoren** sein.  

Weitere Informationen finden Sie unter [Planen von Softwareupdates](../../../sum/plan-design/plan-for-software-updates.md).


### <a name="source-site-account"></a>Konto des Quellstandorts  

Über das **Konto des Quellstandorts** wird vom Migrationsprozess auf den SMS-Anbieter des Quellstandorts zugegriffen. Für dieses Konto ist die Berechtigung **Lesen** für Standortobjekte am Quellstandort erforderlich, damit Daten für Migrationsaufträge gesammelt werden können.  

Wenn Sie über Verteilungspunkte von Configuration Manager 2007 oder über sekundäre Standorte mit verbundenen Verteilungspunkten verfügen und diese auf den Current Branch von Configuration Manager upgraden, muss das Konto die Berechtigung **Löschen** für die Klasse **Standort** besitzen. Diese Berechtigung ist erforderlich, um den Verteilungspunkt während des Upgrades erfolgreich aus dem Configuration Manager 2007-Standort zu entfernen.  

> [!NOTE]  
> Sowohl das Konto des Quellstandorts als auch das [Konto der Datenbank des Quellstandorts](#source-site-database-account) werden in der Configuration Manager-Konsole im Knoten **Konten** des Arbeitsbereichs **Verwaltung** als **Migrations-Manager** bezeichnet.  

Weitere Informationen finden Sie unter [Migrieren von Daten zwischen Hierarchien](https://docs.microsoft.com/sccm/core/migration/migrate-data-between-hierarchies).


### <a name="source-site-database-account"></a>Konto der Datenbank des Quellstandorts  

Über das **Konto der Datenbank des Quellstandorts** greift der Migrationsprozess auf die SQL Server-Datenbank für den Quellstandort zu. Damit von der SQL Server-Datenbank des Quellstandorts Daten gesammelt werden können, muss das Konto der Datenbank des Quellstandorts über die Berechtigungen **Lesen** und **Ausführen** für die SQL Server-Datenbank des Quellstandorts verfügen.  

Falls Sie das Configuration Manager-Computerkonto (Current Branch) verwenden, vergewissern Sie sich, dass Folgendes auf dieses Konto zutrifft:  
  
- Es gehört der Sicherheitsgruppe **Distributed COM-Benutzer** in der Domäne an, in der sich auch der Configuration Manager 2007-Standort befindet.  
- Es gehört der Sicherheitsgruppe **SMS-Administratoren** an.  
- Es hat **Leseberechtigung** für alle Configuration Manager 2007-Objekte.  

> [!NOTE]  
> Sowohl das Konto des Quellstandorts als auch das [Konto der Datenbank des Quellstandorts](#source-site-database-account) werden in der Configuration Manager-Konsole im Knoten **Konten** des Arbeitsbereichs **Verwaltung** als **Migrations-Manager** bezeichnet.  

Weitere Informationen finden Sie unter [Migrieren von Daten zwischen Hierarchien](https://docs.microsoft.com/sccm/core/migration/migrate-data-between-hierarchies).


### <a name="task-sequence-domain-join-account"></a>Domänenbeitrittskonto für Tasksequenzen 

Windows Setup verwendet das **Domänenbeitrittskonto für Tasksequenzen**, um einen Computer, der neu aus einem Image erstellt wurde, zu einer Domäne hinzuzufügen. Dieses Konto wird vom Tasksequenzschritt [Einer Domäne oder Arbeitsgruppe beitreten](../../../osd/understand/task-sequence-steps.md#BKMK_JoinDomainorWorkgroup) mit der Option **Einer Domäne beitreten** benötigt. Dieses Konto kann optional ebenfalls mit dem Schritt [Netzwerkeinstellungen anwenden](../../../osd/understand/task-sequence-steps.md#BKMK_ApplyNetworkSettings) eingerichtet werden.  

Das Konto muss über die Berechtigung **Domäne beitreten** für die Zieldomäne verfügen.  

> [!TIP]  
> Erstellen Sie ein Domänenbenutzerkonto mit den mindestens erforderlichen Berechtigungen, um der Domäne beizutreten, und verwenden Sie diese für alle Tasksequenzen.  

> [!IMPORTANT]  
> Weisen Sie diesem Konto keine Rechte zur interaktiven Anmeldung zu.  
>   
> Verwenden Sie für dieses Konto nicht das Netzwerkzugriffskonto.  


### <a name="task-sequence-network-folder-connection-account"></a>Netzwerkordner-Verbindungskonto für Tasksequenzen  

Die Tasksequenz-Engine verwendet das **Netzwerkordner-Verbindungskonto für Tasksequenzen**, um eine Verbindung mit einem freigegebenen Ordner im Netzwerk herzustellen. Dieses Konto ist für den Tasksequenzschritt [Verbindung mit Netzwerkordner herstellen](../../../osd/understand/task-sequence-steps.md#BKMK_ConnectToNetworkFolder) erforderlich.  

Dieses Konto erfordert Berechtigungen für den Zugriff auf den angegebenen freigegebenen Ordner. Es muss ein Domänenbenutzerkonto sein.  

> [!TIP]  
> Erstellen Sie ein Domänenbenutzerkonto mit den mindestens erforderlichen Berechtigungen für den Zugriff auf die erforderlichen Netzwerkressourcen, und verwenden Sie dieses für alle Tasksequenzen.  

> [!IMPORTANT]  
> Weisen Sie diesem Konto keine Rechte zur interaktiven Anmeldung zu.  
>   
> Verwenden Sie für dieses Konto nicht das Netzwerkzugriffskonto.  


### <a name="task-sequence-run-as-account"></a>Ausführendes Konto für Tasksequenzen  

Die Tasksequenz-Engine verwendet das **ausführende Konto für die Tasksequenz**, um Befehlszeilen oder PowerShell-Skripts mit Anmeldeinformationen zu verwenden, die von denen des lokalen Systemkontos abweichen. Dieses Konto ist für die Tasksequenzschritte [Befehlszeile ausführen](../../../osd/understand/task-sequence-steps.md#BKMK_RunCommandLine) und [PowerShell-Skript ausführen](../../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript) mit der Option **Diesen Schritt mit folgendem Konto ausführen** erforderlich.  

Das Konto muss mit den mindestens erforderlichen Berechtigungen zum Ausführen der in der Tasksequenz angegebenen Befehlszeile eingerichtet sein. Für dieses Konto sind interaktive Anmelderechte erforderlich. Es muss üblicherweise dazu berechtigt sein, Software zu installieren und auf Netzwerkressourcen zuzugreifen. Für den Tasksequenzschritt „PowerShell-Skript ausführen“ benötigt dieses Konto lokale Administratorberechtigungen. 

> [!IMPORTANT]  
> Verwenden Sie für dieses Konto nicht das Netzwerkzugriffskonto.  
>   
> Versehen Sie das Konto niemals mit Domänenadministratorrechten.  
>   
> Richten Sie niemals servergespeicherte Profile für dieses Konto ein. Wenn die Tasksequenz ausgeführt wird, wird das Roamingprofil für das Konto heruntergeladen. Dadurch wird das Profil für den Zugriff auf dem lokalen Computer anfällig.  
>   
> Beschränken Sie den Kontoumfang. Erstellen Sie beispielsweise unterschiedliche ausführende Konten für jede Tasksequenz. Wenn ein Konto gefährdet ist, sind dadurch nur die Clientcomputer gefährdet, auf die dieses Konto Zugriff hat.  
>   
> Wenn für die Befehlszeile Administratorrechte auf dem Computer erforderlich sind, erwägen Sie die Erstellung eines lokalen Administratorkontos lediglich für dieses Konto auf allen Computern, um die Tasksequenz auszuführen. Löschen Sie das Konto, wenn es nicht mehr benötigt wird.  


## <a name="user-objects-that-configuration-manager-uses-in-sql"></a><a name="bkmk_sqlusers"></a> Benutzerobjekte, die von Configuration Manager in SQL verwendet werden 
<!--SCCMDocs issue #1160-->
Configuration Manager erstellt und verwaltet automatisch folgende Benutzerobjekte in SQL.  Diese Objekte befinden sich in der Configuration Manager-Datenbank unter „Sicherheit/Benutzer“.  

> [!IMPORTANT]  
>  Das Ändern oder Entfernen dieser Objekte kann in einer Configuration Manager-Umgebung zu erheblichen Problemen führen.  Es empfiehlt sich, diese Objekte nicht zu ändern.


### <a name="smsdbuser_readonly"></a>smsdbuser_ReadOnly

Dieses Objekt dient zum Ausführen von Abfragen im schreibgeschützten Kontext.  Dieses Objekt wird mit mehreren gespeicherten Prozeduren genutzt.


### <a name="smsdbuser_readwrite"></a>smsdbuser_ReadWrite

Dieses Objekt dient zum Bereitstellen von Berechtigungen für dynamische SQL-Anweisungen.


### <a name="smsdbuser_reportschema"></a>smsdbuser_ReportSchema

Dieses Objekt dient zum Ausführen von SQL Reporting-Ausführungen.  Die folgende gespeicherte Prozedur wird mit dieser Funktion verwendet: spSRExecQuery.


## <a name="database-roles-that-configuration-manager-uses-in-sql"></a><a name="bkmk_sqlroles"></a>Datenbankrollen, die von Configuration Manager in SQL verwendet werden
<!--SCCMDocs issue #1160-->
Configuration Manager erstellt und verwaltet automatisch folgende Rollenobjekte in SQL. Diese Rollen ermöglichen den Zugriff auf bestimmte gespeicherte Prozeduren, Tabellen, Sichten und Funktionen, um die erforderlichen Aktionen der einzelnen Rollen auszuführen, um Daten aus der Configuration Manager-Datenbank abzurufen oder Daten in sie einzufügen. Diese Objekte befinden sich in der Configuration Manager-Datenbank unter „Security/Roles/Database Roles“.

> [!IMPORTANT]  
> Das Ändern oder Entfernen dieser Objekte kann in einer Configuration Manager-Umgebung zu erheblichen Problemen führen. Ändern Sie diese Objekte nicht. Die folgende Liste dient nur zu Informationszwecken.

### <a name="smsdbrole_aitool"></a>smsdbrole_AITool

Asset Intelligence-Volumenlizenzimport. Configuration Manager erteilt diese Berechtigung für Benutzerkonten basierend auf dem RBA-Zugriff, um die Volumenlizenz für die Verwendung mit Asset Intelligence importieren zu können.  Dieses Konto kann mit einer vollständigen Administratorrolle oder einer Asset-Manager-Rolle hinzugefügt werden.

### <a name="smsdbrole_aius"></a>smsdbrole_AIUS

Asset Intelligence-Updatesynchronisierung. Configuration Manager erteilt dem Computerkonto, das das Konto für den Asset Intelligence-Synchronisierungspunkt hostet, Zugriff für den Abruf von Asset Intelligence-Proxydaten und das Anzeigen ausstehender KI-Daten für den Upload.

### <a name="smsdbrole_amtsp"></a>smsdbrole_AMTSP

Out-of-Band-Verwaltung. Diese Rolle wird von der Configuration Manager AMT-Rolle zum Abrufen von Daten auf Geräten verwendet, die Intel AMT unterstützt haben.

> [!NOTE]  
> Diese Rolle ist in neueren Versionen von Configuration Manager veraltet.

### <a name="smsdbrole_crp"></a>smsdbrole_CRP

Der Zertifikatregistrierungspunkt zur Unterstützung des Simple Certificate Enrollment-Protokolls (SCEP). Configuration Manager gewährt die Berechtigung für das Computerkonto des Standortsystems, das den Zertifikatregistrierungspunkt für SCEP-Unterstützung für Signierung und Erneuerung von Zertifikaten unterstützt.

### <a name="smsdbrole_crppfx"></a>smsdbrole_CRPPfx

PFX-Unterstützung des Zertifikatregistrierungspunks. Configuration Manager gewährt die Berechtigung für das Computerkonto des Standortsystems, das den Zertifikatregistrierungspunkt unterstützt, der für PFX-Unterstützung für Signierung und Erneuerung von Zertifikaten konfiguriert ist.

### <a name="smsdbrole_dmp"></a>smsdbrole_DMP

Geräteverwaltungspunkt. Configuration Manager gewährt diese Berechtigung dem Computerkonto für einen Verwaltungspunkt mit der Option „Verwendung dieses Verwaltungspunkts durch mobile Geräte und Macintosh-Computer zulassen“, um Unterstützung für bei MDM angemeldete Geräte bereitzustellen.

### <a name="smsdbrole_dmpconnector"></a>smsdbrole_DmpConnector

Dienstverbindungspunkt. Configuration Manager erteilt diese Berechtigung dem Computerkonto, das den Dienstverbindungspunkt hostet, um Telemetriedaten abzurufen und bereitzustellen, Cloud Services zu verwalten und Dienstupdates abzurufen.

### <a name="smsdbrole_dviewaccess"></a>smsdbrole_DViewAccess

Verteilte Ansichten. Configuration Manager gewährt diese Berechtigung dem Computerkonto der primären Standortserver für CAS, wenn in den Eigenschaften der Replikationsverknüpfung die Option „Verteilte SQL Server-Ansichten“ ausgewählt ist.

### <a name="smsdbrole_dwss"></a>smsdbrole_DWSS

Data Warehouse. Configuration Manager erteilt diese Berechtigung dem Computerkonto, das die Data Warehouse-Rolle hostet.

### <a name="smsdbrole_enrollsvr"></a>smsdbrole_EnrollSvr

 Anmeldungspunkt. Configuration Manager erteilt diese Berechtigung für das Computerkonto, das den Anmeldungspunkt hostet, um die Geräteregistrierung über MDM zuzulassen.

### <a name="smsdbrole_extract"></a>smsdbrole_extract

Bietet Zugriff auf alle erweiterten Schemaansichten.

### <a name="smsdbrole_hmsuser"></a>smsdbrole_HMSUser

Hierarchie-Manager-Dienst. Configuration Manager erteilt Berechtigungen für dieses Konto, um Failoverstatusmeldungen und SQL Server Broker-Transaktionen zwischen Standorten innerhalb einer Hierarchie zu verwalten.

> [!NOTE]  
> Die smdbrole_WebPortal-Rolle ist standardmäßig ein Mitglied dieser Rolle.

### <a name="smsdbrole_mcs"></a>smsdbrole_MCS

Multicast-Dienst. Configuration Manager erteilt diese Berechtigung dem Computerkonto des Verteilungspunkts, der Multicast unterstützt.

### <a name="smsdbrole_mp"></a>smsdbrole_MP

Verwaltungspunkt. Configuration Manager erteilt diese Berechtigung für das Computerkonto, das die Verwaltungspunktrolle hostet, um Unterstützung für Configuration Manager-Clients bereitzustellen.

### <a name="smsdbrole_mpmbam"></a>smsdbrole_MPMBAM

Verwaltungspunkt für Microsoft BitLocker Administration and Monitoring. Configuration Manager erteilt diese Berechtigung für das Computerkonto, das den Verwaltungspunkt hostet, der MBAM für eine Umgebung verwaltet.

### <a name="smsdbrole_mpusersvc"></a>smsdbrole_MPUserSvc

Verwaltungspunkt-Anwendungsanforderung. Configuration Manager erteilt diese Berechtigung für das Computerkonto, das den Verwaltungspunkt hostet, um benutzerbasierte Anwendungsanforderungen zu unterstützen.

### <a name="smsdbrole_siteprovider"></a>smsdbrole_siteprovider

SMS-Anbieter. Configuration Manager erteilt diese Berechtigung dem Computerkonto, das eine SMS-Anbieterrolle hostet.  

### <a name="smsdbrole_siteserver"></a>smsdbrole_siteserver

Standortserver. Configuration Manager erteilt diese Berechtigung dem Computerkonto, der den primären oder den CAS-Standort hostet.

### <a name="smsdbrole_sup"></a>smsdbrole_SUP

Softwareupdatepunkt. Configuration Manager erteilt diese Berechtigung für das Computerkonto, das den Softwareupdatepunkt für das Arbeiten mit Drittanbieterupdates hostet.

### <a name="smsdbrole_webportal"></a>smsdbrole_WebPortal

Anwendungskatalog-Websitepunkt. Configuration Manager erteilt die Berechtigung für das Computerkonto, das den Anwendungskatalog-Websitepunkt hostet, um benutzerbasierte Anwendungsbereitstellung bereitzustellen.

### <a name="smsschm_users"></a>smsschm_users

Benutzerberichtzugriff. Configuration Manager gewährt den Zugriff auf das Konto, das für das Konto des Reporting Services-Punkts verwendet wird, um den Zugriff auf die SMS-Berichtsansichten zum Anzeigen der Configuration Manager-Berichtsdaten zu ermöglichen.  Die Daten werden durch die Verwendung von RBA weiter eingeschränkt.

## <a name="elevated-permissions"></a>Erweiterte Berechtigungen

<!-- SCCMDocs#405 -->

Configuration Manager erfordert, dass einige Konten über erweiterte Berechtigungen für laufende Vorgänge verfügen. Ziehen Sie z. B. [Voraussetzungen für die Installation eines primären Standorts](../../servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_PrereqPri) zurate. In der folgenden Liste sind diese Berechtigungen aufgeführt und die Gründe zusammengefasst, warum sie benötigt werden.

- Das Computerkonto des primären Standortservers und des Standortservers der zentralen Verwaltung erfordert:

  - Lokale Administratorrechte für alle Standortsystemserver. Diese Berechtigung dient dazu, Systemdienste zu verwalten, zu installieren und zu entfernen. Beim Hinzufügen oder Entfernen von Rollen werden vom Standortserver auch lokale Gruppen auf dem Standortsystem aktualisiert.

  - Zugriff des Systemadministrators auf die SQL-Instanz für die Standortdatenbank. Diese Berechtigung dient dazu, SQL für den Standort zu konfigurieren und zu verwalten. Configuration Manager ist nicht nur eine Datenbank, sondern eng in SQL integriert.

- Benutzerkonten in der Rolle „Hauptadministrator“ erfordern Folgendes:

  - Lokale Administratorrechte auf allen Standortservern. Diese Berechtigung dient dazu, Systemdienste, Registrierungsschlüssel und -werte sowie WMI-Objekte anzuzeigen, zu bearbeiten, zu entfernen und zu installieren.

  - Zugriff des Systemadministrators auf die SQL-Instanz für die Standortdatenbank. Diese Berechtigung dient dazu, die Datenbank während des Setups oder der Wiederherstellung zu installieren und zu aktualisieren. Dies ist auch für SQL-Wartung und den Betrieb erforderlich, beispielsweise das Neuindizieren und Aktualisieren von Statistiken.

    > [!NOTE]
    > Einige Organisationen entscheiden sich möglicherweise dafür, den Systemadministratorzugriff zu entfernen und ihn nur bei Bedarf zu gewähren. Dieses Verhalten wird manchmal als „Just-in-Time (JIT)-Zugriff“ bezeichnet. In diesem Fall sollten Benutzer mit der Rolle „Hauptadministrator“ aber dennoch Zugriff zum Lesen, Aktualisieren und Ausführen gespeicherter Prozeduren in der Configuration Manager-Datenbank erhalten. Diese Berechtigungen ermöglichen es ihnen, die meisten Probleme ohne uneingeschränkten Systemadministratorzugriff zu beheben.
