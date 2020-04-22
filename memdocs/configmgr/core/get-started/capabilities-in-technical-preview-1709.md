---
title: Technical Preview1709
titleSuffix: Configuration Manager
description: Erfahren Sie mehr zu Features, die in Technical Preview für Configuration Manager-Version 1709 zur Verfügung stehen.
ms.date: 09/28/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a3ef6bdc-a204-4c4c-a02f-2bd03f35183e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 3cefbbb9824266fd5fa057a7625332e85ec0ab32
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705118"
---
# <a name="capabilities-in-technical-preview-1709-for-configuration-manager"></a>Funktionen in der Technical Preview 1709 für Configuration Manager

*Gilt für: Configuration Manager (Technical Preview-Branch)*

In diesem Artikel werden die Features vorgestellt, die in der Technical Preview-Version 1709 für Configuration Manager verfügbar sind. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen. Bevor Sie diese Technical Preview-Version installieren, lesen Sie [Technical Preview für Configuration Manager](../../core/get-started/technical-preview.md), um sich mit den allgemeinen Anforderungen und Einschränkungen bei der Verwendung einer Technical Preview-Version vertraut zu machen und zu erfahren, wie Sie Updates für Versionen durchführen und Feedback zu den Funktionen in einer Technical Preview-Version geben können.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Bekannte Probleme in dieser Technical Preview:**
- **Beim Update auf die Vorschauversion 1709 tritt ein Fehler auf, wenn Sie einen Standortserver im passiven Modus haben**. Wenn Sie die Vorschauversion 1706, 1707 oder 1708 ausführen und über einen [primären Standortserver im passiven Modus](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) verfügen, müssen Sie den Standortserver im passiven Modus deinstallieren, bevor Sie Ihren Vorschaustandort auf Version 1709 aktualisieren können. Sie können den Standortserver im passiven Modus erneut installieren, wenn an Ihrem Standort Version 1709 ausgeführt wird.

  So deinstallieren Sie den Standortserver im passiven Modus:
  1. Navigieren Sie in der Konsole zu **Administration** > **Übersicht** > **Standortkonfiguration** > **Server und Standortsystemrollen**, und wählen Sie den Standortserver im passiven Modus aus.
  2. Klicken Sie im Bereich **Standortsystemrollen** mit der rechten Maustaste auf die Rolle **Standortserver**, und wählen Sie dann **Rolle entfernen**.
  3. Klicken Sie mit der rechten Maustaste auf den Standortserver im passiven Modus, und wählen Sie dann **Löschen**.
  4. Starten Sie nach dem Deinstallieren des Standortservers auf dem aktiven primären Standortserver den Dienst **CONFIGURATION_MANAGER_UPDATE** neu.


**Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  

## <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Verbesserte Benutzeroberfläche für VPN-Profile in der Configuration Manager-Konsole
<!-- 1313282 -->
Mit diesem Release haben wir den Assistenten zum Erstellen von VPN-Profilen und die VPN-Eigenschaftenseiten aktualisiert, sodass die Einstellungen der ausgewählten Plattform entsprechend angezeigt werden. Genauer gesagt:

- Jede Plattform hat einen eigenen Workflow. Das bedeutet, dass neue VPN-Profile nur die von der jeweiligen Plattform unterstützte Einstellung enthalten.
- Nach der Seite **Allgemein** wird nun die Seite **Unterstützte Plattformen** angezeigt.  Ab sofort wählen Sie die Plattform aus, bevor Sie Eigenschaftswerte festlegen.
- Wenn die Plattform auf **Android**, **Android for Work** oder **Windows Phone 8.1** festgelegt wird, ist die Seite **Unterstützte Plattformen** nicht erforderlich und wird nicht angezeigt.
- Der auf dem Configuration Manager-Client basierende Workflow wurde mit den Workflows aus Windows 10 kombiniert, die auf dem Client für hybrid verwaltete mobile Geräte (MDM) basieren. Diese unterstützen alle dieselben Einstellungen.
- Jeder Plattformworkflow enthält nur die für diesen Workflow geeigneten Einstellungen.  Beispiel: Der Android-Workflow enthält die für Android geeigneten Einstellungen. Die Einstellungen für iOS oder Windows 10 Mobile werden nicht länger im Android-Workflow angezeigt.
- Für Windows 8.1-Geräte werden von Configuration Manager verwaltete Einstellungen eindeutig gekennzeichnet.
- Die Seite „Automatisches VPN“ ist veraltet und wurde entfernt.

Diese Änderungen gelten für neue VPN-Profile.  

Um Kompatibilitätsrisiken zu minimieren, werden vorhandene VPN-Profile nicht geändert.  Wenn Sie ein vorhandenes Profil bearbeiten, werden die Einstellungen so wie bei der Profilerstellung angezeigt.  

### <a name="try-it-out"></a>Probieren Sie es aus!

Erstellen Sie über das übliche Verfahren ein neues VPN-Profil. Beachten Sie, dass die erste Seite in den Optionen des Assistenten zum Erstellen von VPN-Profilen geändert wurde.

1. Wechseln Sie zu **Bestand und Kompatibilität** > **Übersicht** > **Kompatibilitätseinstellungen** > **Zugriff auf Unternehmensressourcen** > **VPN-Profile**, und klicken Sie dann auf **VPN-Profil erstellen**.
2. Geben Sie einen Namen auf der Seite **Allgemein** ein, und wählen Sie eine der folgenden Optionen unter **Geben Sie den Typ des zu erstellenden VPN-Profils an** aus:

    - Windows 10  
    - Windows 8.1  
    - Windows Phone 8.1  
    - iOS und macOS  
    - Android  
    - Android for Work  

3. Falls Sie **Windows 8.1** auswählen, haben Sie auch die Möglichkeit, auf **Neues Profil erstellen** oder **Aus Datei importieren** zu klicken.
4. Schließen Sie den Assistenten ab, um die Profilerstellung fertigzustellen.

Wenn Sie unterschiedliche Plattformen auswählen, werden nur die für die ausgewählte Plattform relevanten Einstellungen angezeigt.

## <a name="co-management-for-windows-10-devices"></a>Co-Verwaltung für Windows 10-Geräte    
<!-- 1350871 -->
Viele Kunden möchten Windows 10-Geräte genauso verwalten wie mobile Geräte: mit einer einfachen, kostengünstigen und cloudbasierten Lösung. Der Übergang von einer herkömmlichen zu einer modernen Verwaltungslösung kann jedoch eine Herausforderung sein. Ab Windows 10-Version 1607 (auch Anniversary Update genannt) können Sie ein Windows 10-Gerät gleichzeitig in eine lokale Active Directory-Installation (AD) und eine cloudbasierte Azure AD-Infrastruktur einbinden (Hybrid Azure AD). Co-Verwaltung nutzt diese Verbesserung und ermöglicht es Ihnen, Windows 10-Geräte gleichzeitig mit Configuration Manager und Intune zu verwalten. Diese Lösung schlägt eine Brücke von der herkömmlichen zur modernen Verwaltung und bietet Ihnen die Möglichkeit, die Umstellung Schritt für Schritt durchzuführen. 

### <a name="prerequisites"></a>Voraussetzungen
Bevor Sie mit der Co-Verwaltung beginnen können, müssen folgende Anforderungen erfüllt sein. Es gibt allgemeine Anforderungen und spezifische für vorhandene Configuration Manager-Clients und Geräte, die keine Clients sind.

### <a name="known-issues"></a>Bekannte Probleme
Nach der Erstellung der Richtlinie für die Co-Verwaltung kann diese nicht mehr geändert werden. Wenn Sie sie dennoch ändern möchten, müssen Sie sie löschen und anschließend mit den gewünschten Einstellungen neu erstellen. 

#### <a name="general-prerequisites"></a>Allgemeine Voraussetzungen
Hier finden Sie die allgemeinen Voraussetzungen für die Aktivierung der Co-Verwaltung:  

- Technical Preview für System Center Configuration Manager 1709
- Azure AD 
- EMS- oder Intune-Lizenzen für alle Benutzer
- Intune-Abonnement &#40;die MDM-Autorität muss in Intune auf **Intune** festgelegt sein&#41;

   > [!Note]  
   > In einer hybriden MDM-Umgebung (Intune integriert in Configuration Manager) ist keine Co-Verwaltung möglich.

#### <a name="additional-prerequisites-for-existing-configuration-manager-clients"></a>Zusätzliche Anforderungen für vorhandene Configuration Manager-Clients
- Windows 10, Version 1709 (Creators Update vom Herbst) und höher
- In Azure AD eingebundene Hybridgeräte (in AD und Azure AD eingebunden)

#### <a name="additional-prerequisites-for-new-windows-10-devices"></a>Zusätzliche Anforderungen für neue Windows 10-Geräte
- Windows 10, Version 1709 (Creators Update vom Herbst) und höher
- [Cloud Management Gateway](../clients/manage/manage-clients-internet.md#cloud-management-gateway) in Configuration Manager

### <a name="workloads-you-can-switch-to-intune"></a>Workloads, die Sie zu Intune verschieben können
Nach der Aktivierung der Co-Verwaltung verwaltet Configuration Manager weiterhin alle Workloads. Wenn Sie dazu bereit sind, können Sie die Verwaltung aller verfügbaren Workloads auf Intune umstellen. In diesem Release können Sie Intune die folgenden Workloads verwalten lassen.   

#### <a name="compliance-policies"></a>Kompatibilitätsrichtlinien
Konformitätsrichtlinien definieren die Regeln und Einstellungen, die ein Gerät erfüllen muss, damit es als mit bedingten Zugriffsrichtlinien konform eingestuft wird. Konformitätsrichtlinien ermöglichen Ihnen auch, Konformitätsprobleme bei Geräten unabhängig von bedingten Zugriffsrechten zu überwachen und zu beheben.

#### <a name="windows-update-for-business-policies"></a>Windows Update for Business-Richtlinien
Mit Windows Update for Business-Richtlinien können Sie Zurückstellungsrichtlinien für Funktionsupdates unter Windows 10 oder für Qualitätsupdates für Windows 10-Geräte konfigurieren, die direkt von Windows Update for Business verwaltet werden. Weitere Informationen finden Sie unter [Konfigurieren von Windows Update for Business-Zurückstellungsrichtlinien](https://docs.microsoft.com/sccm/sum/deploy-use/integrate-windows-update-for-business-windows-10#configure-windows-update-for-business-deferral-policies).  

### <a name="remote-actions-available-in-intune-on-azure-for-co-managed-devices"></a>Remoteaktionen, die in Intune in Azure für co-verwaltete Geräte verfügbar sind
Wenn ein Windows 10-Gerät für die Co-Verwaltung aktiviert ist, stehen Ihnen die folgenden Remoteaktionen aus Intune in Azure zur Verfügung:  
- [Zurücksetzen auf Werkseinstellungen](https://docs.microsoft.com/intune/devices-wipe#wipe)
- [Selektives Zurücksetzen](https://docs.microsoft.com/intune/apps-selective-wipe)
- [Geräte löschen](https://docs.microsoft.com/intune/devices-wipe#delete-devices-from-the-azure-active-directory-portal)
- [Geräte neu starten](https://docs.microsoft.com/intune/device-restart)
- [Sauber starten](https://docs.microsoft.com/intune/device-fresh-start)

### <a name="prepare-intune-for-co-management"></a>Vorbereiten von Intune für die Co-Verwaltung
Bevor Sie Workloads von Configuration Manager zu Intune verschieben, erstellen Sie die erforderlichen Profile und Richtlinien in Intune, um sicherzustellen, dass Ihre Geräte weiterhin geschützt werden.
Sie können Objekte in Intune auf der Grundlage der Objekte erstellen, die in Configuration Manager vorhanden sind. Wenn Ihre aktuelle Strategie aber auf einer veralteten oder herkömmlichen Verwaltung aufbaut, sollten Sie möglicherweise einen Moment innehalten und überdenken, welche Richtlinien und Profile Sie für die moderne Verwaltung benötigen. Verwenden Sie die folgenden Ressourcen, um die Richtlinien und Profile zu erstellen.    
<!-- - [Device compliance policies](https://docs.microsoft.com/intune/compliance-policy-create-windows)  -->
- [Windows Update for Business-Richtlinien](https://docs.microsoft.com/intune/windows-update-for-business-configure)  
- [Gerätekonfigurationsprofile](https://docs.microsoft.com/intune/device-profile-create)  

### <a name="architectural-overview-for-co-management"></a>Architekturübersicht für die Co-Verwaltung
Die folgende Abbildung bietet eine Architekturübersicht über die Co-Verwaltung und ihre Rolle in der vorhandenen Configuration Manager- und Intune-Infrastruktur.

![Architekturabbildung der Co-Verwaltung](./media/co-management-arch-cm1709tp.svg)

### <a name="scenarios-to-enable-co-management"></a>Szenarios zum Aktivieren der Co-Verwaltung  
Sie können die Co-Verwaltung sowohl für Windows 10-Geräte, die in Microsoft Intune registriert sind, als auch für vorhandene Windows 10-Configuration Manager-Clients aktivieren. In beiden Szenarios werden Windows 10-Geräte gleichzeitig von Configuration Manager und Intune verwaltet und in AD und Azure AD eingebunden.  

#### <a name="devices-enrolled-in-intune"></a>Bei Intune registrierte Geräte  
Wenn Windows 10-Geräte bei Intune registriert sind, können Sie den Configuration Manager-Client auf den Geräten (mit einem bestimmten Befehlszeilenargument) installieren, um die Clients für die Co-Verwaltung vorzubereiten. Anschließend aktivieren Sie die Co-Verwaltung über die Configuration Manager-Konsole, um bestimmte Workloads für bestimmte Windows 10-Geräte in Intune zu verschieben.  

Windows 10-Geräte, die noch nicht bei Intune registriert sind, können Sie automatisch bei Azure registrieren. Bei neuen Windows 10-Geräten können Sie den Eindruck beim ersten Ausführen, der die automatische Registrierung von Geräten in Intune enthält, mit Windows AutoPilot konfigurieren.  

#### <a name="configuration-manager-clients"></a>Configuration Manager-Clients
Wenn einige Ihrer Windows 10-Geräte Configuration Manager-Clients sind, können Sie diese Geräte registrieren und die Co-Verwaltung über die Configuration Manager-Konsole aktivieren. Configuration Manager registriert Geräte automatisch anhand der Azure AD-Mandanteninformationen bei Intune.  

### <a name="prepare-windows-10-devices-for-co-management"></a>Vorbereiten von Windows 10-Geräten für die Co-Verwaltung
Sie können die Co-Verwaltung auf Windows 10-Geräten aktivieren, die in AD und Azure AD eingebunden, bei Intune registriert und ein Client in Configuration Manager sind. Installieren Sie den Configuration Manager-Client auf neuen Windows 10- und bereits in Intune registrierten Geräten jedoch vor der Aktivierung der Co-Verwaltung. Windows 10-Geräte, die Configuration Manager-Clients sind, können Sie bei Intune registrieren und die Co-Verwaltung über die Configuration Manager-Konsole aktivieren.

#### <a name="command-line-to-install-configuration-manager-client"></a>Befehlszeile zum Installieren von Configuration Manager-Clients
Erstellen Sie eine App in Intune für Windows 10-Geräte, die noch keine Configuration Manager-Clients sind. Wenn Sie in den nächsten Abschnitten eine App erstellen, verwenden Sie die folgende Befehlszeile:

ccmsetup.msi CCMSETUPCMD="/mp:&#60;*URL des Cloudverwaltungsgateway-Endpunkts für die gegenseitige Authentifizierung*&#62;/ CCMHOSTNAME=&#60;*URL des Cloudverwaltungsgateway-Endpunkts für die gegenseitige Authentifizierung*&#62; SMSSiteCode=&#60;*Standortcode*&#62; SMSMP=https:&#47;/&#60;*FQDN des MPs*&#62; AADTENANTID=&#60;*AAD-Mandanten-ID*&#62; AADTENANTNAME=&#60;*Mandantenname*&#62; AADCLIENTAPPID=&#60;*Server-App-ID für die AAD-Integration*&#62; AADRESOURCEURI=https:&#47;/&#60;*Ressourcen-ID*&#62;”

Angenommen, Sie haben die folgenden Werte:

- **URL des Cloudverwaltungsgateway-Endpunkts für die gegenseitige Authentifizierung**: https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    

   >[!Note]    
   >Verwenden Sie den Wert von **MutualAuthPath** in der SQL-Ansicht **vProxy_Roles** als Wert für die **URL des Cloudverwaltungsgateway-Endpunkts für die gegenseitige Authentifizierung**.

- **FQDN des Verwaltungspunkts (Management Point, MP)** : sccmmp.corp.contoso.com    
- **Standortcode:** PS1    
- **ID des Azure AD-Mandanten:** 72F988BF-86F1-41AF-91AB-2D7CD011XXXX    
- **Name des Azure AD-Mandanten**: contoso    
- **ID der Azure AD-Client-App**: bef323b3-042f-41a6-907a-f9faf0d1XXXX     
- **URI der AAD-Ressourcen-ID:** ConfigMgrServer    

  > [!Note]    
  > Verwenden Sie den Wert von **IdentifierUri** aus der SQL-Ansicht **vSMS_AAD_Application_Ex** als Wert für den **URI der AAD-Ressourcen-ID**.

Daraus ergibt sich die folgende Befehlszeile:

ccmsetup.msi CCMSETUPCMD="/mp:https:/&#47;contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100    CCMHOSTNAME=contoso.cloudapp.net/CCM_Proxy_MutualAuth/72057594037928100 SMSSiteCode=PS1 SMSMP=https:/&#47;sccmmp.corp.contoso.com AADTENANTID=72F988BF-86F1-41AF-91AB-2D7CD011XXXX AADTENANTNAME=contoso  AADCLIENTAPPID=bef323b3-042f-41a6-907a-f9faf0d1XXXX AADRESOURCEURI=https:/&#47;ConfigMgrServer”

> [!Tip]
>Die Befehlszeilenparameter für Ihren Standort finden Sie anhand der folgenden Schritte:     
> 1. Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Übersicht** > **Clouddienste** > **Co-management** (Co-Verwaltung).  
> 2. Klicken Sie auf der Registerkarte „Home“ (Startseite) in der Gruppe „Manage“ (Verwalten) auf **Configure co-management** (Co-Verwaltung konfigurieren), um den Registrierungs-Assistenten für die Co-Verwaltung zu öffnen.    
> 3. Klicken Sie auf der Seite „Subscriptions“ (Abonnement) auf **Sign In** (Anmelden), melden Sie sich bei Ihrem Intune-Mandanten an, und klicken Sie dann auf **Next** (Weiter).    
> 4. Klicken Sie auf der Seite „Enablement“ (Aktivierung) im Abschnitt **Devices enrolled in Intune** (Bei Intune registrierte Geräte) auf **Copy** (Kopieren), um die Befehlszeile in die Zwischenablage zu kopieren. Speichern Sie sie anschließend, um die Befehlszeile bei der Erstellung einer App zu verwenden.  
> 5. Klicken Sie auf **Cancel** (Schließen), um den Assistenten zu beenden.

#### <a name="new-windows-10-devices"></a>Neue Windows 10-Geräte
Auf neuen Windows 10-Geräten können Sie mit dem Dienst „AutoPilot“ den Eindruck beim ersten Ausführen konfigurieren, der die Einbindung des Geräts in AD und Azure AD sowie die Registrierung bei Intune umfasst. Erstellen Sie anschließend eine App in Intune, um den Configuration Manager-Client bereitzustellen.  
1. Aktivieren Sie AutoPilot für die neuen Windows 10-Geräte. Weitere Informationen finden Sie unter [Übersicht über Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-10-auto-pilot).  
2. Konfigurieren Sie die automatische Registrierung in Azure AD für Ihre Geräte, damit sie automatisch in Intune registriert werden. Weitere Informationen finden Sie unter  [Windows-Geräte registrieren](https://docs.microsoft.com/intune/windows-enroll).
3. Erstellen Sie eine App in Intune mit dem Configuration Manager-Clientpaket, und stellen Sie die App für Windows 10-Geräte bereit, die Sie co-verwalten möchten. Verwenden Sie die [Befehlszeile, um den Configuration Manager-Client zu installieren](#command-line-to-install-configuration-manager-client), während Sie die Schritte zum [Installieren von Clients über das Internet mithilfe von Azure AD](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure) ausführen.   

#### <a name="windows-10-devices-not-enrolled-in-intune-or-a-configuration-manager-client"></a>Nicht in Intune oder einem Configuration Manager-Client registrierte Windows 10-Geräte
Windows 10-Geräte, die nicht in Intune registriert sind oder den Configuration Manager-Client haben, können Sie automatisch bei Intune registrieren. Erstellen Sie anschließend eine App in Intune, um den Configuration Manager-Client bereitzustellen.
1. Konfigurieren Sie die automatische Registrierung in Azure AD für Ihre Geräte, damit sie automatisch in Intune registriert werden. Weitere Informationen finden Sie unter  [Windows-Geräte registrieren](https://docs.microsoft.com/intune/windows-enroll).  
2. Erstellen Sie eine App in Intune mit dem Configuration Manager-Clientpaket, und stellen Sie die App für Windows 10-Geräte bereit, die Sie co-verwalten möchten. Verwenden Sie die [Befehlszeile, um den Configuration Manager-Client zu installieren](#command-line-to-install-configuration-manager-client), während Sie die Schritte zum [Installieren von Clients über das Internet mithilfe von Azure AD](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure) ausführen.

#### <a name="windows-10-devices-enrolled-in-intune"></a>Bei Intune registrierte Windows 10-Geräte
Erstellen Sie für Windows 10-Geräte, die bereits bei Intune registriert sind, eine App in Intune, um den Configuration Manager-Client bereitzustellen. Verwenden Sie die [Befehlszeile, um den Configuration Manager-Client zu installieren](#command-line-to-install-configuration-manager-client), während Sie die Schritte zum [Installieren von Clients über das Internet mithilfe von Azure AD](https://docs.microsoft.com/sccm/core/clients/deploy/deploy-clients-cmg-azure) ausführen.  

### <a name="switch-configuration-manager-workloads-to-intune"></a>Verschieben von Configuration Manager-Workloads zu Intune
Im vorherigen Abschnitt haben Sie Windows 10-Geräte für die Co-Verwaltung vorbereitet. Diese Geräte sind nun in AD und Azure AD eingebunden, bei Intune registriert und haben den Configuration Manager-Client. Wahrscheinlich sind aber noch nicht alle Ihrer Windows 10-Geräte, die in AD eingebunden und mit dem Configuration Manager-Client versehen sind, auch in Azure AD eingebunden oder bei Intune registriert. Das folgende Verfahren enthält eine Anleitung für die Aktivierung der Co-Verwaltung und die Vorbereitung Ihrer restlichen Windows 10-Geräte (Configuration Manager-Clients ohne Intune-Registrierung) für die Co-Verwaltung. Außerdem können Sie damit beginnen, bestimmte Configuration Manager-Workloads zu Intune zu verschieben.

1. Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Übersicht** > **Clouddienste** > **Co-management** (Co-Verwaltung).    
2. Klicken Sie auf der Registerkarte „Home“ (Startseite) in der Gruppe „Manage“ (Verwalten) auf **Configure co-management** (Co-Verwaltung konfigurieren), um den Registrierungs-Assistenten für die Co-Verwaltung zu öffnen.    
3. Klicken Sie auf der Seite „Subscriptions“ (Abonnement) auf **Sign In** (Anmelden), melden Sie sich bei Ihrem Intune-Mandanten an, und klicken Sie dann auf **Next** (Weiter).   
4. Konfigurieren Sie auf der Seite „Staging“ (Bereitstellung) die folgenden Einstellungen, und klicken Sie dann auf **Next** (Weiter):
    - **Pilotgruppe:** Die Pilotgruppe enthält eine oder mehrere Sammlungen, die Sie auswählen. Verwenden Sie diese Gruppe im Rahmen des Rollouts der Co-Verwaltung in mehreren Phasen. Sie können mit einer kleinen Testsammlung beginnen und der Pilotgruppe nach und nach weitere Sammlungen hinzufügen, während Sie die Co-Verwaltung für weitere Benutzer und Geräte ausrollen. Die Sammlungen in der Pilotgruppe lassen sich jederzeit in den Einstellungen der Co-Verwaltung ändern.
    - **Produktion:** Wenn Sie diese Einstellung auswählen, werden alle unterstützten Windows 10-Geräte für die Co-Verwaltung aktiviert. Konfigurieren Sie die **Ausschlussgruppe** mit mindestens einer Sammlung. Geräte, die einer der Sammlungen in dieser Gruppe angehören, werden von der Co-Verwaltung ausgeschlossen. 
5. Wählen Sie je nach den Einstellungen, die Sie auf der Seite „Staging“ (Bereitstellung) konfiguriert haben, auf der Seite „Enablement“ (Aktivierung) **Pilot** oder **All** (Alle), um die automatische Registrierung bei Intune zu aktivieren, und klicken Sie dann auf **Next** (Weiter). Wenn Sie **Pilot** auswählen, werden nur die Configuration Manager-Clients aus der Gruppe „Pilotprojekt“ automatisch bei Intune registriert. So können Sie die Co-Verwaltung für einen Teil der Clients aktivieren, um sie zu testen und phasenweise auszurollen. 
6. Wählen Sie auf der Seite „Workloads“ aus, ob Configuration Manager-Workloads von Intune verwaltet werden sollen, und klicken Sie dann auf **Next** (Weiter). Verwenden Sie die Schieberegler, um auszuwählen, ob die Workload in die Pilotgruppe oder, je nach den Einstellungen, die Sie auf der Seite „Staging“ (Bereitstellung) konfiguriert haben, für alle Windows 10-Clients verschoben werden soll. 
7. Schließen Sie den Assistenten, um die Co-Verwaltung zu aktivieren.  

<!--### Modify your co-management settings
After you enable co-management using the wizard, you can modify your target group and change the workloads that are managed by Configuration Manager and Intune.  
- In the Configuration Manager console, go to **Administration** > **Overview** > **Cloud Services** > **Co-management**.  
Select the co-management object, and then on the Home tab, click **Properties**. -->   

<!--### Monitor co-management
After you have enabled co-management, you can monitor which devices are managed by Configuration Manager and which are managed by Intune. You can also see which Configuration Manager workloads are managed by which product.-->

## <a name="see-also"></a>Weitere Informationen:
Weitere Informationen zur Installation oder dem Update der Technical Preview finden Sie unter [Technical Preview für Configuration Manager](technical-preview.md). 
