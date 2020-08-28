---
title: Anforderungen für Windows Autopilot
ms.reviewer: ''
manager: laurawi
description: Informieren Sie sich über Software-, Netzwerk-, Lizenzierungs-und Konfigurations Anforderungen für die Windows Autopilot-Bereitstellung.
keywords: MDM, Setup, Windows, Windows 10, OOBE, Manage, Bereitstellung, Autopilot, ZTD, Zero-Touchscreen, Partner, msfb, InTune
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.custom:
- CI 116757
- CSSTroubleshooting
ms.openlocfilehash: aafd83f1aa09881c9e7c4196b91798ab0d278a87
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993655"
---
# <a name="windows-autopilot-requirements"></a>Anforderungen für Windows Autopilot

**Gilt für: Windows 10**

Windows Autopilot ist von bestimmten Funktionen abhängig, die in Windows 10, Azure Active Directory und MDM-Diensten wie Microsoft InTune verfügbar sind.  Um Windows Autopilot verwenden und diese Funktionen nutzen zu können, müssen einige Anforderungen erfüllt sein.

**Hinweis**: eine Liste der OEMs, die derzeit Windows Autopilot unterstützen, finden Sie im Abschnitt Teilnehmer Gerätehersteller unter [Windows Autopilot](https://aka.ms/windowsAutopilot).

## <a name="software-requirements"></a>Softwareanforderungen

- Es ist eine [unterstützte Version](/windows/release-information/) des halbjährlichen Kanals von Windows 10 erforderlich. Windows 10 Enterprise 2019 Long-Term Service Channel (LTSC) wird ebenfalls unterstützt.
- Die folgenden Editionen werden unterstützt:
  - Windows 10 Pro
  - Windows 10 Pro Education
  - Windows 10 Pro for Workstations
  - Windows 10 Enterprise
  - Windows 10 Education
  - Windows 10 Enterprise 2019 LTSC

>[!NOTE]
>Die Verfahren für die Bereitstellung von Windows Autopilot können auf bestimmte Produkte und Versionen verweisen. Die Aufnahme dieser Produkte in diesen Inhalt impliziert keine Erweiterung der Unterstützung für eine Version, die über den Support Lebenszyklus hinausgeht. Von Windows Autopilot werden keine Produkte unterstützt, die über den Support Lebenszyklus hinausgehen. Weitere Informationen finden Sie unter [Microsoft-Lebenszyklusrichtlinie](https://go.microsoft.com/fwlink/p/?LinkId=208270).

## <a name="networking-requirements"></a>Netzwerkanforderungen

Windows Autopilot ist von einer Vielzahl von internetbasierten Diensten abhängig. Der Zugriff auf diese Dienste muss bereitgestellt werden, damit Autopilot ordnungsgemäß funktioniert. Im einfachsten Fall kann die Aktivierung der richtigen Funktionalität erreicht werden, indem Folgendes sichergestellt wird:

- DNS-Namensauflösung für Internet-DNS-Namen sicherstellen
- Erlauben Sie den Zugriff auf alle Hosts über Port 80 (http), 443 (HTTPS) und 123 (UDP/NTP).

In Umgebungen mit restriktiveren Internet Zugriff oder für diejenigen, die eine Authentifizierung erfordern, bevor der Internet Zugriff abgerufen werden kann, ist möglicherweise eine zusätzliche Konfiguration erforderlich, um den Zugriff auf die erforderlichen Dienste in die Whitelist aufzunehmen. 

> [!NOTE]
> Die Smartcard-und Zertifikat basierte Authentifizierung wird während der OOBE-Authentifizierung nicht unterstützt. Weitere Informationen finden Sie unter [Smartcards und Zertifikat basierte Authentifizierung](/azure/active-directory/devices/azureadjoin-plan#smartcards-and-certificate-based-authentication).

Weitere Informationen zu den einzelnen Diensten und ihren spezifischen Anforderungen finden Sie in den folgenden Details:

<table><th>Dienst<th>Informationen
<tr><td><b>Windows Autopilot-Bereitstellungs Dienst<b><td>Wenn eine Netzwerkverbindung vorhanden ist, wird von jedem Windows 10-Gerät eine Verbindung mit dem Windows Autopilot-Bereitstellungs Dienst hergestellt.  Mit Windows 10, Version 1903 und höher, werden die folgenden URLs verwendet: https://ztd.dds.microsoft.com , https://cs.dds.microsoft.com . <br>

<tr><td><b>Windows-Aktivierung<b><td>Windows Autopilot erfordert auch Windows-Aktivierungs Dienste. Weitere Informationen zu den URLs, auf die für die Aktivierungs Dienste zugegriffen werden muss, finden Sie <a href="https://support.microsoft.com/help/921471/windows-activation-or-validation-fails-with-error-code-0x8004fe33">unter Windows-Aktivierung oder-Überprüfung mit Fehlercode 0x8004FE33</a> .<br>

<tr><td><b>Azure Active Directory<b><td>Benutzer Anmelde Informationen werden von Azure Active Directory überprüft, und das Gerät kann auch mit Azure Active Directory verknüpft werden. Weitere Informationen finden Sie unter <a href="/office365/enterprise/office-365-ip-web-service">Office 365-IP-Adresse und URL-Webdienst</a> .
<tr><td><b>Intune<b><td>Nach der Authentifizierung wird Azure Active Directory die Registrierung des Geräts beim InTune-MDM-Dienst auslöst. Weitere Informationen zu den Anforderungen für die Netzwerkkommunikation finden Sie unter dem folgenden Link: <a href="https://docs.microsoft.com/intune/network-bandwidth-use#network-communication-requirements">InTune-Anforderungen für die Netzwerkkonfiguration und Bandbreite</a>
<tr><td><b>Windows Update<b><td>Während des OOBE-Prozesses, und nachdem das Windows 10-Betriebssystem vollständig konfiguriert wurde, wird der Windows Update-Dienst genutzt, um erforderliche Updates abzurufen. Wenn beim Herstellen einer Verbindung mit Windows Update Probleme auftreten, finden Sie weitere Informationen unter <a href="https://support.microsoft.com/help/818018/how-to-solve-connection-problems-concerning-windows-update-or-microsof">Beheben von Verbindungsproblemen in Bezug auf Windows Update oder Microsoft Update</a>.<br>

Wenn auf Windows Update nicht zugegriffen werden kann, wird der Autopilot-Prozess trotzdem fortgesetzt, aber es sind keine kritischen Updates verfügbar.

<tr><td><b>Übermittlungsoptimierung<b><td>Beim Herunterladen von Windows-Updates, Microsoft Store Apps und APP-Updates, Office-Updates und InTune-Win32-apps wird der <a href="/windows/deployment/update/waas-delivery-optimization">Bereitstellungs Optimierungs</a> Dienst kontaktiert, um die Peer-zu-Peer-Freigabe von Inhalten zu aktivieren, sodass nur wenige Geräte diese aus dem Internet herunterladen müssen.<br>

Wenn nicht auf den Bereitstellungs Optimierungs Dienst zugegriffen werden kann, wird der Autopilot-Prozess weiterhin mit Downloads zur Übermittlungs Optimierung aus der Cloud (ohne Peer-to-Peer) fortgesetzt.

<tr><td><b>Netzwerk Zeitprotokoll (NTP)-Synchronisierung<b><td>Wenn ein Windows-Gerät gestartet wird, kommuniziert es mit einem Netzwerk Zeitserver, um sicherzustellen, dass die Zeit auf dem Gerät genau ist. Stellen Sie sicher, dass der UDP-Port 123 für Time.Windows.com zugänglich ist.
<tr><td><b>DNS (Domain Name Services)<b><td>Zum Auflösen von DNS-Namen für alle Dienste kommuniziert das Gerät mit einem DNS-Server, der in der Regel über DHCP bereitgestellt wird.Dieser DNS-Server muss in der Lage sein, Internet Namen aufzulösen.
<tr><td><b>Diagnosedaten<b><td>Ab Windows 10, 1903, wird die Sammlung von Diagnosedaten standardmäßig aktiviert. Informationen zum Deaktivieren von Windows Analytics und zugehöriger Diagnosefunktionen finden Sie unter <a href="https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#manage-enterprise-diagnostic-data-level">Verwalten der Diagnosedaten Ebene für Unternehmen</a>.<br>

Wenn keine Diagnosedaten gesendet werden können, wird der Autopilot-Prozess trotzdem fortgesetzt. Dienste, die von Diagnosedaten abhängen (z. b. Windows Analytics), funktionieren jedoch nicht.
<tr><td><b>Netzwerkverbindungs-Statusanzeige (NCSI)<b><td>Windows muss erkennen können, dass das Gerät auf das Internet zugreifen kann. Weitere Informationen finden Sie unter <a href="https://docs.microsoft.com/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#14-network-connection-status-indicator">Network Connection Status Indicator (NCSI)</a>.

<code>www.msftconnecttest.com</code> muss über DNS aufgelöst werden können und über HTTP zugänglich sein.
<tr><td><b>Windows-Notification Services (WNS)<b><td>Dieser Dienst wird verwendet, um Windows das Empfangen von Benachrichtigungen von apps und Diensten zu ermöglichen. Weitere Informationen finden Sie unter <a href="/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#26-microsoft-store">Microsoft Store</a> .<br>

Wenn die WNS-Dienste nicht verfügbar sind, wird der Autopilot-Prozess trotzdem ohne Benachrichtigungen fortgesetzt.
<tr><td><b>Microsoft Store, Microsoft Store für Unternehmen<b><td>Apps in der Microsoft Store können per pushübertragung auf das Gerät übermittelt und über InTune (MDM) ausgelöst werden.APP-Updates und zusätzliche Apps können auch benötigt werden, wenn sich der Benutzer zum ersten Mal anmeldet. Weitere Informationen finden Sie unter <a href="/microsoft-store/prerequisites-microsoft-store-for-business">Voraussetzungen für Microsoft Store für Unternehmen und Bildungseinrichtungen</a> (auch Azure AD und Windows Notification Services).<br>

Wenn kein Zugriff auf die Microsoft Store möglich ist, wird der Autopilot-Prozess weiterhin ohne Microsoft Store-Apps ausgeführt.

<tr><td><b>Microsoft 365<b><td>Im Rahmen der InTune-Gerätekonfiguration ist möglicherweise die Installation von Microsoft 365-Apps für Unternehmen erforderlich. Weitere Informationen finden Sie unter <a href="https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2">URLs und IP-Adressbereiche von Office 365</a> (enthält alle Office-Dienste, DNS-Namen und IP-Adressen; umfasst Azure AD und andere Dienste, die sich mit den oben aufgeführten überlappen können).
<tr><td><b>Zertifikat Sperr Listen (CRLs)<b><td>Einige dieser Dienste müssen auch Zertifikat Sperr Listen (CRLs) für Zertifikate überprüfen, die in den Diensten verwendet werden.Eine vollständige Liste dieser Angaben finden Sie unter <a href="https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_crl">URLs und IP-Adressbereiche von Office 365</a> und <a href="https://aka.ms/o365chains">Office 365-Zertifikat Ketten</a>.
<tr><td><b>Hybrid-Aad-Join<b><td>Das Gerät kann in eine Hybrid-Aad-Einbindung aufgenommen werden. Der Computer sollte sich im Unternehmensnetzwerk befinden, damit der Hybrid-Aad-Join funktioniert. Details finden Sie im <a href="user-driven.md#user-driven-mode-for-hybrid-azure-active-directory-join">benutzergesteuerten Windows Autopilot-Modus</a> .
<tr><td><b>Autopilot-selbstbereitstellungs Modus und Autopilot-White-Glove<b><td>Firmware-TPM-Geräte, die nur von Intel, AMD oder Qualcomm bereitgestellt werden, enthalten nicht alle benötigten Zertifikate zur Startzeit und müssen in der Lage sein, Sie bei der ersten Verwendung vom Hersteller abzurufen. Geräte mit diskreten TPM-Chips (einschließlich Geräten von einem beliebigen anderen Hersteller) werden mit diesen Zertifikaten vorinstalliert. Weitere Informationen finden Sie in den <a href="/windows/security/information-protection/tpm/tpm-recommendations">TPM-Empfehlungen</a> . Stellen Sie sicher, dass diese URLs für jeden firmwaretpm-Anbieter verfügbar sind, damit Zertifikate erfolgreich angefordert werden können: 

  <br>Intel- https://www.intel.com/  <br>Qualcomm- https://ekcert.spserv.microsoft.com/EKCertificate/GetEKCertificate/v1  <br>AMD https://ftpm.amd.com/pki/aia

</table>

## <a name="licensing-requirements"></a>Lizenzanforderungen

Windows Autopilot ist von bestimmten Funktionen abhängig, die in Windows 10 und Azure Active Directory verfügbar sind. Außerdem ist ein MDM-Dienst erforderlich, z. b. Microsoft InTune. Diese Funktionen können über verschiedene Editionen und Abonnement Programme abgerufen werden:

Zum Bereitstellen der erforderlichen Azure Active Directory (automatische MDM-Registrierung und Unternehmens brandingfeatures) und MDM-Funktionalität ist eine der folgenden Anforderungen erforderlich:
- [Premium-Abonnement Microsoft 365 Business](https://www.microsoft.com/microsoft-365/business)
- [Microsoft 365 F1-oder F3-Abonnement](https://www.microsoft.com/microsoft-365/enterprise/firstline)
- [Microsoft 365 Academic a1-, a3-oder A5-Abonnement](https://www.microsoft.com/education/buy-license/microsoft365/default.aspx)
- [Microsoft 365 Enterprise E3-oder E5-Abonnement](https://www.microsoft.com/microsoft-365/enterprise), die alle Features von Windows 10, Office 365 und EM + S (Azure AD und InTune) enthalten.
- [Enterprise Mobility + Security E3-oder E5-Abonnement](https://www.microsoft.com/cloud-platform/enterprise-mobility-security), das alle benötigten Azure AD-und InTune-Features umfasst.
- [InTune for Education-Abonnement](/intune-education/what-is-intune-for-education), das alle benötigten Azure AD-und InTune-Features umfasst.
- [Azure Active Directory Premium P1 oder P2](https://azure.microsoft.com/services/active-directory/) und [Microsoft InTune Abonnement](https://www.microsoft.com/cloud-platform/microsoft-intune) (oder ein alternativer MDM-Dienst).

> [!NOTE]
> Selbst bei Verwendung Microsoft 365 Abonnements müssen Sie [den Benutzern trotzdem InTune-Lizenzen zuweisen](/intune/fundamentals/licenses-assign).

Außerdem wird Folgendes empfohlen (ist jedoch nicht erforderlich):
- [Microsoft 365 Apps für Unternehmen](https://www.microsoft.com/p/office-365-proplus/CFQ7TTC0K8R0), die problemlos über InTune (oder andere MDM-Dienste) bereitgestellt werden können.
- [Windows-Abonnement Aktivierung](/windows/deployment/windows-10-enterprise-subscription-activation), um Geräte von Windows 10 pro zu Windows 10 Enterprise automatisch zu überspringen.

## <a name="configuration-requirements"></a>Konfigurationsanforderungen

Bevor Windows Autopilot verwendet werden kann, sind einige Konfigurationsaufgaben erforderlich, um die gängigen Autopilot-Szenarien zu unterstützen.  

- Konfigurieren Azure Active Directory automatischen Registrierung.  Weitere Informationen zu Microsoft InTune finden Sie unter Aktivieren der automatischen Registrierung von [Windows 10](/intune/windows-enroll#enable-windows-10-automatic-enrollment) .  Wenn Sie einen anderen MDM-Dienst verwenden, wenden Sie sich an den Anbieter, um die für diese Dienste erforderlichen URLs oder Konfigurationen zu erhalten.
- Konfigurieren Sie Azure Active Directory benutzerdefiniertes Branding.  Um während des Autopilot-Prozesses eine organisationsspezifische Anmeldeseite anzuzeigen, müssen Azure Active Directory mit den Bildern und Text konfiguriert werden, die angezeigt werden sollen.  Weitere Informationen finden Sie [unter Schnellstart: Hinzufügen eines Unternehmensbrandings zur Anmeldeseite in Azure AD](/azure/active-directory/fundamentals/customize-branding) .  Beachten Sie, dass das "quadratische Logo" und der "Text der Anmeldeseite" die Schlüsselelemente für Autopilot sind, sowie der Name des Azure Active Directory Mandanten (separat in den Eigenschaften des Azure AD Mandanten konfiguriert).
- Aktivieren Sie bei Bedarf die [Aktivierung des Windows-Abonnements](/windows/deployment/windows-10-enterprise-subscription-activation) , um automatisch von Windows 10 pro zu Windows 10 Enterprise zu wechseln.

Bestimmte Szenarien haben dann zusätzliche Anforderungen.  Im Allgemeinen gibt es zwei spezielle Aufgaben:

- Geräteregistrierung.  Geräte müssen Windows Autopilot hinzugefügt werden, um die meisten Windows Autopilot-Szenarien zu unterstützen.  Weitere Informationen finden [Sie unter Hinzufügen von Geräten zu Windows Autopilot](add-devices.md) .
- Profil Konfiguration.  Nach dem Hinzufügen von Geräten zu Windows Autopilot muss ein Profil mit Einstellungen auf jedes Gerät angewendet werden.  Weitere Informationen finden Sie unter [Konfigurieren von Autopilot-Profilen](profiles.md) .  Beachten Sie, dass Microsoft InTune diese Profil Zuweisung automatisieren kann. Weitere Informationen finden Sie unter [Erstellen einer Autopilot-Gerätegruppe](/intune/enrollment-Autopilot#create-an-Autopilot-device-group) und [Zuweisen eines Autopilot-Bereitstellungs Profils zu einer Gerätegruppe](/intune/enrollment-Autopilot#assign-an-Autopilot-deployment-profile-to-a-device-group) .

Weitere Informationen finden Sie unter [Windows Autopilot-Szenarios](windows-Autopilot-scenarios.md) .

Eine exemplarische Vorgehensweise für einige dieser und verwandte Schritte finden Sie in diesem Video:

</br>

<iframe width="560" height="315" src="https://www.youtube.com/embed/KYVptkpsOqs" frameborder="0" allow="accelerometer; autoplay; encrypted-media" gyroscope; picture-in-picture" allowfullscreen></iframe>


Es gibt keine zusätzlichen Hardwareanforderungen für die Verwendung von Windows 10 Autopilot, außer den [Anforderungen zum Ausführen von Windows 10](https://www.microsoft.com/windows/windows-10-specifications).

## <a name="related-topics"></a>Zugehörige Themen

[Übersicht über Windows Autopilot](windows-Autopilot.md)