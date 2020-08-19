---
title: Netzwerk Anforderungen für Windows Autopilot
ms.reviewer: ''
manager: laurawi
description: Informieren Sie sich über die Netzwerk Anforderungen für die Windows Autopilot-Bereitstellung.
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
ms.openlocfilehash: 18031ff51e8086d29f706110946adeacb63d908e
ms.sourcegitcommit: 8fc7f2864c5e3f177e6657b684c5f208d6c2a1b4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88590904"
---
# <a name="windows-autopilot-networking-requirements"></a>Netzwerk Anforderungen für Windows Autopilot

**Gilt für: Windows 10**

Windows Autopilot ist von einer Vielzahl von internetbasierten Diensten abhängig. Der Zugriff auf diese Dienste muss bereitgestellt werden, damit Autopilot ordnungsgemäß funktioniert. Im einfachsten Fall kann die Aktivierung der richtigen Funktionalität erreicht werden, indem die folgenden Bedingungen sichergestellt werden:

- Sicherstellen der DNS-Namensauflösung (Domain Name Services) für Internet-DNS-Namen
- Erlauben Sie den Zugriff auf alle Hosts über Port 80 (http), 443 (HTTPS) und 123 (UDP/NTP).

Möglicherweise ist eine zusätzliche Konfiguration erforderlich, um den Zugriff auf die erforderlichen Dienste in Umgebungen zu gewähren, die:
- Sie haben einen restriktiveren Internet Zugang.
- fordern Sie eine Authentifizierung an, bevor der Internet Zugriff abgerufen werden kann. 

> [!NOTE]
> Die Smartcard-und Zertifikat basierte Authentifizierung wird während der OOBE nicht unterstützt. Weitere Informationen finden Sie unter [Smartcards und Zertifikat basierte Authentifizierung](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan#smartcards-and-certificate-based-authentication).

Weitere Informationen zu den einzelnen Diensten und ihren spezifischen Anforderungen finden Sie in den folgenden Details:

<table><th>Dienst<th>Information
<tr><td><b>Windows Autopilot-Bereitstellungs Dienst<b><td>Wenn eine Netzwerkverbindung vorhanden ist, wird von jedem Windows 10-Gerät eine Verbindung mit dem Windows Autopilot-Bereitstellungs Dienst hergestellt. Mit Windows 10, Version 1903 und höher, werden die folgenden URLs verwendet: https://ztd.dds.microsoft.com , https://cs.dds.microsoft.com . <br>

<tr><td><b>Windows-Aktivierung<b><td>Für Windows Autopilot sind Windows-Aktivierungs Dienste erforderlich. Ausführliche Informationen zu den URLs, auf die für die Aktivierungs Dienste zugegriffen werden muss, finden Sie unter <a href="https://support.microsoft.com/help/921471/windows-activation-or-validation-fails-with-error-code-0x8004fe33">Windows-Aktivierung oder-Validierung schlägt fehl mit Fehlercode 0x8004FE33</a>.<br>

<tr><td><b>Azure Active Directory<b><td>Benutzer Anmelde Informationen werden von Azure Active Directory überprüft, und das Gerät kann auch mit Azure Active Directory verknüpft werden. Weitere Informationen finden Sie unter <a href="https://docs.microsoft.com/office365/enterprise/office-365-ip-web-service">Office 365-IP-Adresse und URL-Webdienst</a>.
<tr><td><b>Intune<b><td>Nach der Authentifizierung wird Azure Active Directory die Registrierung des Geräts beim InTune-MDM-Dienst (Mobile Device Management, Verwaltung mobiler Geräte) auslöst. Weitere Informationen zu den Anforderungen für die Netzwerkkommunikation finden Sie unter dem folgenden Link: <a href="https://docs.microsoft.com/intune/network-bandwidth-use#network-communication-requirements">InTune-Anforderungen für die Netzwerkkonfiguration und Bandbreite</a>
<tr><td><b>Windows Update<b><td>Während des OOBE-Prozesses und nach der Konfiguration des Windows 10-Betriebssystems ruft der Windows Update-Dienst erforderliche Updates ab. Wenn beim Herstellen einer Verbindung mit Windows Update Probleme auftreten, finden Sie weitere Informationen unter <a href="https://support.microsoft.com/help/818018/how-to-solve-connection-problems-concerning-windows-update-or-microsof">Beheben von Verbindungsproblemen in Bezug auf Windows Update oder Microsoft Update</a>.<br>

Wenn auf Windows Update nicht zugegriffen werden kann, wird der Autopilot-Prozess trotzdem fortgesetzt, aber es sind keine kritischen Updates verfügbar.

<tr><td><b>Übermittlungsoptimierung<b><td>Autopilot kontaktiert den <a href="https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization">Bereitstellungs Optimierungs</a> Dienst beim Herunterladen von apps und Updates. Dieser Kontakt richtet die Peer-zu-Peer-Freigabe von Inhalten ein, sodass nur wenige Geräte diese aus dem Internet herunterladen müssen.
- Windows Updates - Microsoft Store Apps und APP-Updates - Office aktualisiert - InTune Win32-apps<br>

Wenn nicht auf den Bereitstellungs Optimierungs Dienst zugegriffen werden kann, wird der Autopilot-Prozess weiterhin mit Downloads zur Übermittlungs Optimierung aus der Cloud (ohne Peer-to-Peer) fortgesetzt.

<tr><td><b>Netzwerk Zeitprotokoll (NTP)-Synchronisierung<b><td>Wenn ein Windows-Gerät gestartet wird, kommuniziert es mit einem Netzwerk Zeitserver, um sicherzustellen, dass die Uhrzeit auf dem Gerät richtig ist. Stellen Sie sicher, dass der UDP-Port 123 für Time.Windows.com zugänglich ist.
<tr><td><b>DNS (Domain Name Services)<b><td>Zum Auflösen von DNS-Namen für alle Dienste kommuniziert das Gerät mit einem DNS-Server, der in der Regel über DHCP bereitgestellt wird. Dieser DNS-Server muss in der Lage sein, Internet Namen aufzulösen.
<tr><td><b>Diagnosedaten<b><td>Ab Windows 10, 1903, wird die Sammlung von Diagnosedaten standardmäßig aktiviert. Informationen zum Deaktivieren von Windows Analytics und zugehöriger Diagnosefunktionen finden Sie unter <a href="https://docs.microsoft.com/windows/privacy/configure-windows-diagnostic-data-in-your-organization#manage-enterprise-diagnostic-data-level">Verwalten der Diagnosedaten Ebene für Unternehmen</a>.<br>

Wenn keine Diagnosedaten gesendet werden können, wird der Autopilot-Prozess trotzdem fortgesetzt. Dienste, die von Diagnosedaten abhängen, wie z. b. Windows Analytics, funktionieren jedoch nicht.
<tr><td><b>Netzwerkverbindungs-Statusanzeige (NCSI)<b><td>Windows muss erkennen können, dass das Gerät auf das Internet zugreifen kann. Weitere Informationen finden Sie unter <a href="https://docs.microsoft.com/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#14-network-connection-status-indicator">Network Connection Status Indicator (NCSI)</a>.

<code>www.msftconnecttest.com</code> muss über DNS aufgelöst werden können und über HTTP zugänglich sein.
<tr><td><b>Windows-Notification Services (WNS)<b><td>Dieser Dienst wird verwendet, um Windows das Empfangen von Benachrichtigungen von apps und Diensten zu ermöglichen. Weitere Informationen finden Sie unter <a href="https://docs.microsoft.com/windows/privacy/manage-connections-from-windows-operating-system-components-to-microsoft-services#26-microsoft-store">Microsoft Store</a>.<br>

Wenn die WNS-Dienste nicht verfügbar sind, wird der Autopilot-Prozess trotzdem ohne Benachrichtigungen fortgesetzt.
<tr><td><b>Microsoft Store, Microsoft Store für Unternehmen<b><td>Apps in der Microsoft Store können per pushübertragung auf das Gerät übermittelt und über InTune (MDM) ausgelöst werden.APP-Updates und zusätzliche Apps können auch benötigt werden, wenn sich der Benutzer zum ersten Mal anmeldet. Weitere Informationen finden Sie unter <a href="https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business">Voraussetzungen für Microsoft Store für Unternehmen und Bildungseinrichtungen</a> (auch Azure AD und Windows Notification Services).<br>

Wenn kein Zugriff auf die Microsoft Store möglich ist, wird der Autopilot-Prozess weiterhin ohne Microsoft Store-Apps ausgeführt.

<tr><td><b>Office 365<b><td>Im Rahmen der InTune-Gerätekonfiguration ist möglicherweise die Installation von Microsoft 365-Apps für Unternehmen erforderlich. Weitere Informationen finden Sie unter <a href="https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2">URLs und IP-Adressbereiche von Office 365</a>. Dieser Artikel enthält alle Office-Dienste, DNS-Namen und IP-Adressen. Außerdem sind Azure AD und andere Dienste enthalten, die sich mit den oben aufgeführten Diensten überlappen können.
<tr><td><b>Zertifikat Sperr Listen (CRLs)<b><td>Einige dieser Dienste müssen auch Zertifikat Sperr Listen (CRLs) für Zertifikate überprüfen, die in den Diensten verwendet werden.Eine vollständige Liste finden Sie unter <a href="https://support.office.com/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2#bkmk_crl">URLs und IP-Adressbereiche für Office 365</a> und <a href="https://aka.ms/o365chains">Office 365-Zertifikat Ketten</a>.
<tr><td><b>Azure AD-Hybrideinbindung<b><td>Das Gerät kann Hybrid Azure AD verknüpft sein. Der Computer sollte sich im Unternehmensnetzwerk befinden, damit Hybrid Azure AD beitreten funktioniert. Details finden Sie im <a href="user-driven.md#user-driven-mode-for-hybrid-azure-active-directory-join">benutzergesteuerten Windows Autopilot-Modus</a> .
<tr><td><b>Autopilot-selbstbereitstellungs Modus und Autopilot-White-Glove<b><td>Firmware-TPM-Geräte, die nur von Intel, AMD oder Qualcomm bereitgestellt werden, enthalten nicht alle benötigten Zertifikate zur Startzeit und müssen in der Lage sein, Sie bei der ersten Verwendung vom Hersteller abzurufen. Geräte mit diskreten TPM-Chips (einschließlich Geräten von einem beliebigen anderen Hersteller) werden mit diesen Zertifikaten vorinstalliert. Weitere Informationen finden Sie unter <a href="https://docs.microsoft.com/windows/security/information-protection/tpm/tpm-recommendations">TPM-Empfehlungen</a>. Stellen Sie für jeden firmwaretpm-Anbieter sicher, dass auf diese URLs zugegriffen werden kann, damit Zertifikate erfolgreich angefordert werden können:

 <br>Intel <code>https://ekop.intel.com/ekcertservice</code>
 <br>SOCS <code>https://ekcert.spserv.microsoft.com/EKCertificate/GetEKCertificate/v1</code>
 <br>AMD <code>https://ftpm.amd.com/pki/aia</code>

</table>

**Nächste Schritte**

[Windows Autopilot-Lizenzierungsanforderungen](licensing-requirements.md)

