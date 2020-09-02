---
title: Intune-Einstellungen für Geräteeinschränkungen für Windows 10 in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Eine Liste mit allen Einstellungen und ihren Beschreibungen zum Erstellen von Geräteeinschränkungen für Windows 10 und höher wird angezeigt. Verwenden Sie diese Einstellungen in einem Konfigurationsprofil zum Steuern von Screenshots, Kennwortanforderungen, Kioskeinstellungen, Apps im Store, Microsoft Edge-Browser, Microsoft Defender, des Cloudzugriffs, Startmenüs und mehr in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/13/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 38465f709cf07da97e26c36a9fabba232aca9ba2
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88912881"
---
# <a name="windows-10-and-newer-device-settings-to-allow-or-restrict-features-using-intune"></a>Einstellungen für Windows 10-Geräte (und höher) zum Zulassen oder Einschränken von Features mit Intune

In diesem Artikel werden die verschiedenen Einstellungen aufgeführt und beschrieben, die Sie auf Geräten mit Windows 10 und höher festlegen können. Verwenden Sie diese Einstellungen im Rahmen Ihrer Lösung für die mobile Geräteverwaltung (Mobile Device Management, MDM), um Features zuzulassen oder zu deaktivieren, Kennwortregeln festzulegen, den Sperrbildschirm anzupassen, Microsoft Defender zu verwenden und vieles mehr.

Diese Einstellungen werden erst einem Gerätekonfigurationsprofil in Intune hinzugefügt und dann Ihren Windows 10-Geräten zugewiesen oder für diese bereitgestellt.

> [!Note]
> Nicht alle Optionen sind in allen Windows-Editionen verfügbar. Die unterstützten Editionen finden Sie in unter [Konfigurationsdienstanbieter für Richtlinien](/windows/client-management/mdm/policy-configuration-service-provider) (öffnet eine andere Microsoft-Website).
>  
> Die meisten konfigurierbaren Einstellungen in einem Windows 10-Geräteeinschränkungsprofil werden mithilfe von Gerätegruppen auf Geräteebene bereitgestellt. Für Benutzergruppen bereitgestellte Richtlinien gelten für die Zielbenutzer sowie für Benutzer, die über eine Intune-Lizenz verfügen und sich an diesem Gerät anmelden.

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen Sie ein Profil für Windows 10-Geräteeinschränkungen](device-restrictions-configure.md#create-the-profile).

## <a name="app-store"></a>App Store

Diese Einstellungen verwenden den [ApplicationManagement-Richtlinien-CSP](/windows/client-management/mdm/policy-csp-applicationmanagement), der auch die unterstützten Windows-Editionen auflistet.

- **App Store (nur mobil)** : Mit der Option **Blockieren** wird verhindert, dass Benutzer über mobile Geräte auf den App Store zugreifen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Benutzer auf den App Store zugreifen.
- **Apps aus Store automatisch aktualisieren**: Mit der Option **Blockieren** wird verhindert, dass Updates automatisch über den Microsoft Store installiert werden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Apps, die aus dem Microsoft Store heruntergeladen und installiert werden, automatisch aktualisiert werden.

  [ApplicationManagement/AllowAppStoreAutoUpdate-CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowappstoreautoupdate)

- **Installation vertrauenswürdiger Apps**: Wählen Sie diese Option aus, wenn Apps installiert werden können, die nicht aus dem Microsoft Store stammen. Dies wird auch als Querladen bezeichnet. Querladen bedeutet Installieren und anschließendes Ausführen oder Testen einer App, die nicht durch den Microsoft Store zertifiziert ist. Beispielsweise kann es sich um eine App handeln, die nur für Ihr Unternehmen intern ist. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
  - **Blockieren:** Verhindert Querladen. Apps, die nicht auf dem Microsoft Store stammen, können nicht installiert werden.
  - **Zulassen:** Ermöglicht Querladen. Apps, die nicht auf dem Microsoft Store stammen, können installiert werden.

- **Entwicklersperre aufheben**: Ermöglicht es Benutzern, Windows-Entwicklereinstellungen – z. B. das Zulassen quergeladener Apps – zu ändern. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
  - **Blockieren:** Verhindert den Entwicklermodus und das Querladen von Apps.
  - **Zulassen:** Erlaubt den Entwicklermodus und das Querladen von Apps.

  Unter [Aktivieren des Geräts für die Entwicklung](/windows/uwp/get-started/enable-your-device-for-development) finden Sie weitere Informationen zu dieser Funktion.
  
  [ApplicationManagement/AllowAllTrustedApps-CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowalltrustedapps)

- **Gemeinsam genutzte App-Benutzerdaten:** Wählen Sie **Zulassen** aus, um Anwendungsdaten für verschiedene Benutzer auf dem gleichen Gerät und andere Instanzen dieser App freizugeben. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise verhindert das Betriebssystem standardmäßig das Freigeben von Daten für andere Benutzer und andere Instanzen der gleichen App.

  [ApplicationManagement/AllowSharedUserAppData-CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowshareduserappdata)

- **Nur privaten Store verwenden:** **Zulassen** erlaubt nur das Herunterladen von Apps aus einem privaten Store und nicht aus dem öffentlichen Store (einschließlich eines Einzelhandelskatalogs). Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Apps aus privaten und öffentlichen Stores heruntergeladen werden.

  [ApplicationManagement/RequirePrivateStoreOnly-CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-requireprivatestoreonly)

- **Store-App starten:** **Blockieren**: Mit dieser Option deaktivieren Sie auf Geräten alle Apps, die vorinstalliert waren oder aus dem Microsoft Store heruntergeladen wurden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass diese Apps geöffnet werden.

  [ApplicationManagement/DisableStoreOriginatedApps-CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-disablestoreoriginatedapps)

- **App-Daten in Systemvolume installieren:** **Blockieren** hindert Apps daran, Daten im Systemvolume des Geräts zu speichern. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Apps Daten auf dem Systemdatenträgervolume speichern.

  [ApplicationManagement/RestrictAppDataToSystemVolume-CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-restrictappdatatosystemvolume)

- **Apps auf Systemlaufwerk installieren:** **Blockieren** hindert Apps daran, eine Installation auf dem Systemlaufwerk des Geräts auszuführen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Apps auf dem Systemlaufwerk gespeichert werden.

  [ApplicationManagement/RestrictAppToSystemVolume-CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-restrictapptosystemvolume)

- **Game DVR (nur Desktop):** **Blockieren** deaktiviert die Windows-Spieleaufzeichnung und -übertragung. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Spiele aufgezeichnet und übertragen werden.

  [ApplicationManagement/AllowGameDVR-CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowgamedvr)

- **Apps nur aus Store:** Diese Einstellung bestimmt, was geschieht, wenn Benutzer Apps aus anderen Quellen als dem Microsoft Store installieren. Sie verhindert nicht die Installation von Inhalten von USB-Geräten, Netzwerkfreigaben oder anderen Quellen außerhalb des Internets. Verwenden Sie einen vertrauenswürdigen Browser, um sicherzustellen, dass diese Schutzmaßnahmen wie erwartet funktionieren.

  Folgende Optionen sind verfügbar:

  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Benutzer Apps aus anderen Quellen als dem Microsoft Store herunterladen und installieren (einschließlich Apps, die in anderen Richtlinieneinstellungen definiert sind).  
  - **Anywhere:** Diese Einstellung deaktiviert App-Empfehlungen und ermöglicht Benutzern die Installation von Apps aus beliebigen Quellen.  
  - **Nur Store:** Damit soll verhindert werden, dass schädliche Inhalte Ihre Benutzergeräte beeinträchtigen, wenn Sie ausführbare Inhalte aus dem Internet herunterladen. Wenn Benutzer versuchen, Apps aus dem Internet zu installieren, wird die Installation blockiert. Benutzern wird eine Nachricht angezeigt, in der der Download von Apps aus dem Microsoft Store empfohlen wird.
  - **Empfehlungen:** Diese Einstellung legt fest, dass dem Benutzer eine Meldung angezeigt wird, die den Download aus dem Microsoft Store empfiehlt, wenn er eine App aus dem Internet installiert, die auch im Store verfügbar ist.  
  - **Store bevorzugen:** Bei dieser Einstellung werden Benutzer gewarnt, wenn sie Apps aus anderen Quellen als dem Microsoft Store installieren.

  [SmartScreen/EnableAppInstallControl-CSP](/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-enableappinstallcontrol)

- **Benutzerkontrolle über Installationen**: Mit der Option **Blockieren** wird verhindert, dass Benutzer die Installationsoptionen ändern, die in der Regel für Systemadministratoren reserviert sind, etwa durch Eingeben des Installationsverzeichnisses. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise verhindert der Windows Installer standardmäßig, dass Benutzer diese Installationsoptionen ändern, und einige der Sicherheitsfeatures des Windows Installers werden umgangen.

  [ApplicationManagement/MSIAllowUserControlOverInstall CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msiallowusercontroloverinstall)

- **Apps mit erhöhten Rechten installieren**: **Blockieren** weist den Windows Installer an, bei der Installation von Programmen auf dem System erhöhte Rechte anzuwenden. Diese Berechtigungen werden auf alle Programme ausgeweitet. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise wendet das System standardmäßig bei der Installation von Programmen die Berechtigungen des aktuellen Benutzers an, die nicht von einem Systemadministrator bereitgestellt oder angeboten werden.

  [ApplicationManagement/MSIAlwaysInstallWithElevatedPrivileges CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msialwaysinstallwithelevatedprivileges)

- **Start-Apps**: Geben Sie eine Liste der Apps ein, die nach der Anmeldung eines Benutzers beim Gerät gestartet werden sollen. Achten Sie darauf, eine durch Semikolons getrennte Liste von Paketfamiliennamen (PFN) von Windows-Anwendungen zu verwenden. Damit diese Richtlinie funktioniert, muss das Manifest in den Windows-Apps eine Startaufgabe verwenden.

  [ApplicationManagement/LaunchAppAfterLogOn CSP](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-launchappafterlogon)

## <a name="cellular-and-connectivity"></a>Mobilfunk und Konnektivität

Diese Einstellungen verwenden die [Konnektivitätsrichtlinien](/windows/client-management/mdm/policy-csp-connectivity)- und [WLAN-Richtlinien](/windows/client-management/mdm/policy-csp-wifi)-CSPs, die auch die unterstützten Windows-Editionen auflisten.

- **Mobilfunkdatenkanal:** Ermöglicht, dass Benutzer Daten verbrauchen (z. B. beim Browsen im Web), wenn sie mit einem Mobilfunknetz verbunden sind. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Benutzer können diese Funktion deaktivieren.
  - **Blockieren:** Der Mobilfunkdatenkanal ist unzulässig. Benutzer können diese Funktion nicht aktivieren.
  - **Zulassen (Bearbeitung nicht möglich)** : Lässt den Mobilfunkdatenkanal zu. Benutzer können diese Funktion nicht deaktivieren.

- **Datenroaming:** **Blockieren** verhindert Mobilfunkdatenroaming auf dem Gerät. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig kann das Roaming zwischen Netzwerken beim Zugriff auf Daten zulässig sein.
- **VPN over the cellular network** (VPN über das Mobilfunknetz): **Blockieren** verhindert, dass das Gerät auf VPN-Verbindungen zugreifen kann, wenn es mit einem Mobilfunknetz verbunden ist. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass das VPN eine beliebige Verbindung (einschließlich Mobilfunk) nutzt.
- **VPN roaming over the cellular network** (VPN-Roaming über das Mobilfunknetz): **Blockieren** hindert das Gerät beim Roaming in einem Mobilfunknetz am Zugriff auf VPN-Verbindungen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig VPN-Verbindungen beim Roaming zu.
- **Dienst für verbundene Geräte:** **Blockieren** deaktiviert die CDP-Komponente (Connected Devices Platform, Plattform für verbundene Geräte). CDP ermöglicht die Erkennung von und die Verbindung mit anderen Geräten (über Bluetooth/LAN oder die Cloud), um den Start von Remote-Apps, Remotemessaging, App-Remotesitzungen und andere geräteübergreifende Funktionen zu unterstützen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig den Dienst für verbundene Geräte zu, der die Ermittlung von und Verbindung mit anderen Bluetooth-Geräten ermöglicht.
- **NFC:** **Blockieren** unterbindet die NFC-Funktionen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Benutzer NFC-Funktionen auf dem Gerät aktivieren und konfigurieren.
- **WLAN:** **Blockieren** verhindert, dass Benutzer WLAN-Verbindungen auf dem Gerät aktivieren, konfigurieren und verwenden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig WLAN-Verbindungen zu.
- **Automatically connect to Wi-Fi hotspots** (Automatische Verbindung mit WLAN-Hotspots): **Blockieren** verhindert, dass Geräte automatisch eine Verbindung mit WLAN-Hotspots herstellen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Geräte sich automatisch mit unverschlüsselten WLAN-Hotspots verbinden und die Geschäftsbedingungen für die Verbindung akzeptieren.
- **Manuelle WLAN-Konfiguration:** **Blockieren** verhindert, dass Geräte mit eine Verbindung mit einem WLAN außerhalb der MDM-serverinstallierten Netzwerke herstellen können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Benutzer eigene WLAN-Verbindungsnetzwerk-SSIDs hinzufügen und konfigurieren.
- **Intervall für WLAN-Suche:** Geben Sie ein, wie häufig Geräte nach WLAN-Netzwerken suchen sollen. Geben Sie einen Wert zwischen 1 (am häufigsten) und 500 (am seltensten) ein. Der Standardwert ist `0` (null).

### <a name="bluetooth"></a>Bluetooth

Diese Einstellungen verwenden den [Bluetooth-Richtlinien-CSP](/windows/client-management/mdm/policy-csp-bluetooth), der auch die unterstützten Windows-Editionen auflistet.

- **Bluetooth**: **Blockieren** verhindert, dass Benutzer Bluetooth aktivieren können. **Nicht konfiguriert** (Standard) ermöglicht die Verwendung von Bluetooth auf dem Gerät.
- **Bluetooth-Erkennbarkeit**: **Blockieren** verhindert die Erkennung dieses Geräts durch andere für Bluetooth aktivierte Geräte. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass andere Bluetooth-fähige Geräte (z. B. ein Kopfhörer) das Gerät erkennen.

  [Bluetooth/AllowDiscoverableMode-CSP](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

- **Bluetooth-Vorabkopplung:** **Blockieren** verhindert die automatische Kopplung bestimmter Bluetooth-Geräte mit einem Hostgerät. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig eine automatische Koppelung mit dem Hostgerät zu.

  [Bluetooth/AllowPrepairing-CSP](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowprepairing)

- **Bluetooth-Ankündigung**: **Blockieren** verhindert, dass das Gerät Bluetooth-Ankündigungen sendet. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass das Gerät Bluetooth-Ankündigungen sendet.

  [Bluetooth/AllowAdvertising-CSP](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

- **Bluetooth-Nahbereichsverbindungen:** Mit der Option **Blockieren** werden Benutzer daran gehindert, die schnelle Kopplung und andere Nahbereichsfunktionen zu verwenden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass das Gerät Bluetooth-Ankündigungen sendet.

  [Bluetooth/AllowPromptedProximalConnections-CSP](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowpromptedproximalconnections)

- **Zulässige Bluetooth-Dienste:** **Fügen Sie** eine Liste zulässiger Bluetooth-Dienste und -Profile gibt in Form von hexadezimalen Zeichenfolgen hinzu, wie etwa `{782AFCFC-7CAA-436C-8BF0-78CD0FFBD4AF}`.

  [Im Leitfaden zu ServicesAllowedList](/windows/client-management/mdm/policy-csp-bluetooth#servicesallowedlist-usage-guide) finden Sie weitere Informationen zur Liste der Dienste.

  [Bluetooth/ServicesAllowedList-CSP](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-servicesallowedlist)

## <a name="cloud-and-storage"></a>Cloud und Speicher

Diese Einstellungen verwenden den [Kontenrichtlinien-CSP](/windows/client-management/mdm/policy-csp-accounts), der auch die unterstützten Windows-Editionen auflistet.

> [!IMPORTANT]
> Das Blockieren oder Deaktivieren dieser Microsoft-Kontoeinstellungen kann sich auf Registrierungsszenarien auswirken, bei denen sich Benutzer bei Azure AD anmelden müssen. Sie verwenden z. B. [AutoPilot mit intensiver Benutzerunterstützung](/windows/deployment/windows-autopilot/white-glove). Normalerweise wird den Benutzern im Fenster ein Azure AD-Zeichen angezeigt. Wenn diese Einstellungen auf **Blockieren** oder **Deaktivieren** festgelegt sind, wird das Azure AD-Zeichen in der Option möglicherweise nicht angezeigt. Stattdessen werden die Benutzer aufgefordert, die EULA zu akzeptieren und ein lokales Konto zu erstellen, was möglicherweise nicht Ihren Wünschen entspricht.

- **Microsoft-Konto**: Wenn **Blockieren** festgelegt wird, werden Benutzer daran gehindert, dem Gerät ein Microsoft-Konto zuzuordnen. Die Option **Blockieren** kann sich auch auf Registrierungsszenarien auswirken, in denen Benutzer den Registrierungsvorgang abschließen müssen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass ein Microsoft-Konto hinzugefügt und verwendet wird.
- **Nicht-Microsoft-Konto:** **Blockieren** verhindert, dass Benutzer Nicht-Microsoft-Konten über die Benutzeroberfläche hinzufügen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Benutzer E-Mail-Konten hinzufügen, die nicht mit einem Microsoft-Konto verknüpft sind.
- **Settings synchronization for Microsoft account** (Einstellungssynchronisierung für das Microsoft-Konto): **Blockieren** verhindert das Synchronisieren der mit einem Microsoft-Konto verknüpften Geräte- und App-Einstellungen zwischen Geräten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem diese Synchronisierung standardmäßig zu.
- **Anmelde-Assistent für Microsoft-Konten:** Dieser Betriebssystemdienst ermöglicht Benutzern die Anmeldung bei ihrem Microsoft-Konto. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Benutzer den **Anmelde-Assistenten für Microsoft-Konten** (wlidsvc-Dienst) starten und beenden.
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Benutzer den **Anmelde-Assistenten für Microsoft-Konten** (wlidsvc-Dienst) starten und beenden.
  - **Deaktiviert:** Legt den Anmelde-Assistenten für Microsoft-Konten (wlidsvc-Dienst) auf „Deaktiviert“ fest und verhindert, dass Benutzer ihn manuell starten können.

      Die Option **Deaktivieren** kann sich auch auf Registrierungsszenarien auswirken, in denen Benutzer die Registrierung abschließen müssen. Sie verwenden z. B. [AutoPilot mit intensiver Benutzerunterstützung](/windows/deployment/windows-autopilot/white-glove). Normalerweise wird den Benutzern im Fenster ein Azure AD-Zeichen angezeigt. Bei Festlegung auf **Deaktivieren** wird die Azure AD-Anmeldeoption möglicherweise nicht angezeigt. Stattdessen werden die Benutzer aufgefordert, die EULA zu akzeptieren und ein lokales Konto zu erstellen, was möglicherweise nicht Ihren Wünschen entspricht.

## <a name="cloud-printer"></a>Clouddrucker

Diese Einstellungen verwenden den [EnterpriseCloudPrint-Richtlinien-CSP](/windows/client-management/mdm/policy-csp-enterprisecloudprint), der auch die unterstützten Windows-Editionen auflistet.

- **URL für Druckerermittlung:** Geben Sie die URL zum Finden von Clouddruckern ein. Geben Sie beispielsweise `https://cloudprinterdiscovery.contoso.com` ein.
- **Autoritäts-URL für Druckerzugriff:** Geben Sie die Authentifizierungsendpunkt-URL zum Abrufen von OAuth-Token ein. Geben Sie beispielsweise `https://azuretenant.contoso.com/adfs` ein.
- **GUID für native Azure-Client-App:** Geben Sie die GUID einer Clientanwendung ein, die OAuth-Token von der OAuthAuthority abrufen darf. Geben Sie beispielsweise `E1CF1107-FF90-4228-93BF-26052DD2C714` ein.
- **Druckdienstressourcen-URI:** Geben Sie den OAuth-Ressourcen-URI für den im Azure-Portal konfigurierten Druckdienst ein. Geben Sie beispielsweise `http://MicrosoftEnterpriseCloudPrint/CloudPrint` ein.
- **Maximal abgefragte Drucker (nur Mobilgeräte)** : geben Sie die maximale Anzahl von Druckern ein, die abgefragt werden sollen. Der Standardwert lautet `20`.
- **Ressourcen-URI für Druckerermittlungsdienst:** Geben Sie den OAuth-Ressourcen-URI für den im Azure-Portal konfigurierten Druckererkennungsdienst ein. Geben Sie beispielsweise `http://MopriaDiscoveryService/CloudPrint` ein.

> [!TIP]
> Nachdem Sie [Windows Server Hybrid Cloud Print](/windows-server/administration/hybrid-cloud-print/hybrid-cloud-print-overview) eingerichtet haben, können Sie diese Einstellungen konfigurieren und auf Ihren Windows-Geräten bereitstellen.

## <a name="control-panel-and-settings"></a>Systemsteuerung und Einstellungen

- **App „Einstellungen“:** **Blockieren** verhindert, dass Benutzer auf die Windows-Einstellungen-App zugreifen können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Benutzer die Einstellungen-App auf dem Gerät öffnen.
  - **System:** **Blockieren**  verhindert den Zugriff auf den Systembereich der Einstellungen-App. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
    - **Änderung der Energie- und Energiesparmoduseinstellungen (nur Desktopgeräte)** : **Blockieren** hindert Benutzer daran, die Einstellungen für die Stromversorgung und den Standbymodus zu ändern. **Nicht konfiguriert** (Standard) ermöglicht Benutzern, die Energie- und Energiesparmoduseinstellungen zu ändern.
  - **Geräte:** **Blockieren** verhindert den Zugriff auf den Gerätebereich der Einstellungen-App auf dem Gerät. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
  - **Netzwerk und Internet:** **Blockieren** verhindert den Zugriff auf den Netzwerk- und Internetbereich der Einstellungen-App auf dem Gerät. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
  - **Personalisierung:** **Blockieren** verhindert den Zugriff auf den Personalisierungsbereich der Einstellungen-App auf dem Gerät. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
  - **Apps**: **Blockieren** verhindert den Zugriff auf den Apps-Bereich der Einstellungen-App auf dem Gerät. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
  - **Konten**: **Blockieren** verhindert den Zugriff auf den Apps-Bereich der Einstellungen-App auf dem Gerät. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
  - **Time and Language** (Zeit und Sprache): **Blockieren** verhindert den Zugriff auf den Uhrzeit- und Sprachenbereich der Einstellungen-App auf dem Gerät. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
    - **Änderung der Systemzeit**: **Blockieren** hindert Benutzer daran, die Datums- und Uhrzeiteinstellungen auf dem Gerät zu ändern. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Benutzer können diese Einstellungen ändern.
    - **Änderung von Regionseinstellungen** (nur Desktop): **Blockieren** hindert Benutzer daran, die Regionseinstellungen auf dem Gerät zu ändern. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Benutzer können diese Einstellungen ändern.
    - **Änderung der Spracheinstellungen (nur Desktop):** **Blockieren** hindert Benutzer daran, die Spracheinstellungen auf dem Gerät zu ändern. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Benutzer können diese Einstellungen ändern.

      [Einstellungsrichtlinien-CSP](/windows/client-management/mdm/policy-csp-settings)

  - **Gaming:** **Blockieren** verhindert den Zugriff auf den Gamingbereich der Einstellungen-App auf dem Gerät. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
  - **Ease of Access** (Erleichterte Bedienung): **Blockieren** verhindert den Zugriff auf den Bereich für erleichterte Bedienung der Einstellungen-App auf dem Gerät. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
  - **Datenschutz:** **Blockieren** verhindert den Zugriff auf den Datenschutzbereich der Einstellungen-App auf dem Gerät. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
  - **Update and Security** (Update und Sicherheit): **Blockieren** verhindert den Zugriff auf den Bereich „Update und Sicherheit“ der Einstellungen-App auf dem Gerät. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

## <a name="display"></a>Anzeige

Diese Einstellungen verwenden den [Anzeigerichtlinien-CSP](/windows/client-management/mdm/policy-csp-display), der auch die unterstützten Windows-Editionen auflistet.

Mit der GDI-DPI-Skalierung können Anwendungen, die nicht mit DPI-Werten kompatibel sind, mit monitorspezifischen DPI-Werten kompatibel sein.

- **GDI-Skalierung für Apps aktivieren**: **Fügen** Sie die Legacy-Apps hinzu, für die GDI-DPI-Skalierung aktiviert werden soll. Geben Sie beispielsweise `filename.exe` oder `%ProgramFiles%\Path\Filename.exe` ein.

  GDI-DPI-Skalierung ist für alle Legacyanwendungen in der Liste aktiviert.

- **GDI-Skalierung für Apps deaktivieren**: **Fügen** Sie die Legacy-Apps hinzu, für die GDI-DPI-Skalierung deaktiviert werden soll. Geben Sie beispielsweise `filename.exe` oder `%ProgramFiles%\Path\Filename.exe` ein.

  GDI-DPI-Skalierung ist für alle Legacyanwendungen in der Liste deaktiviert.

Sie können auch eine CSV-Datei mit der Liste der Apps **importieren**.

## <a name="general"></a>Allgemein

Diese Einstellungen verwenden den [Benutzeroberflächenrichtlinien-CSP](/windows/client-management/mdm/policy-csp-experience), der auch die unterstützten Windows-Editionen auflistet. 

- **Bildschirmaufnahme (nur Mobilgeräte)** : **Blockieren** verhindert, dass Benutzer Screenshots auf dem Gerät erstellen können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Copy and paste (mobile only)** (Kopieren und Einfügen (nur Mobilgeräte)): **Blockieren** verhindert, dass Benutzer Kopieren und Einfügen für Apps auf dem Gerät verwenden können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Manuelles Aufheben der Registrierung**: **Blockieren** verhindert, dass Benutzer das Arbeitsplatzkonto über die Arbeitsplatz-Systemsteuerung auf dem Gerät löschen können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

  Diese Richtlinieneinstellung wird nicht angewendet, wenn der Computer mit Azure Active Directory (Azure AD) verknüpft ist und die automatische Registrierung aktiviert ist.

- **Manuelle Installation von Stammzertifikaten (nur Mobilgeräte)** : **Blockieren** hindert Benutzer daran, Stammzertifikate und CAP-Zwischenzertifikate manuell zu installieren. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Kamera:** **Blockieren** verhindert, dass Benutzer die Kamera auf dem Gerät verwenden können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise den Zugriff auf die Kamera des Geräts zu.

  Intune verwaltet nur den Zugriff auf die Kamera des Geräts. Das Programm kann nicht auf Bilder oder Videos zugreifen.

  [Camera-CSP](/windows/client-management/mdm/policy-csp-camera)

- **OneDrive-Dateisynchronisierung:** **Blockieren** hindert Benutzer daran, Dateien vom Gerät mit OneDrive zu synchronisieren. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

  [System/DisableOneDriveFileSync-CSP](/windows/client-management/mdm/policy-csp-system#system-disableonedrivefilesync)

- **Wechselmedien:** **Blockieren** verhindert, dass Benutzer externe Speichergeräte wie SD-Karten mit dem Gerät verwenden können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Geolocation**: **Blockieren** verhindert, dass Benutzer Ortungsdienste auf dem Gerät aktivieren können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

  [System/AllowLocation-CSP](/windows/client-management/mdm/policy-csp-system#system-allowlocation)

- **Internetfreigabe:** **Blockieren** verhindert die gemeinsame Nutzung der Internetverbindung auf dem Gerät. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Zurücksetzung des Telefons:** **Blockieren** verhindert, dass Benutzer das Gerät zurücksetzen oder eine Zurücksetzung auf die Werkseinstellungen ausführen können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **USB-Verbindung**: **Blockieren** verhindert den Zugriff auf externe Speichergeräte über eine USB-Verbindung des Geräts. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Der Ladevorgang über USB ist von dieser Einstellung nicht betroffen.

  [Connectivity/AllowUSBConnection-CSP](/windows/client-management/mdm/policy-csp-connectivity#connectivity-allowusbconnection)

- **Diebstahlschutzmodus** (nur Mobilgeräte): **Blockieren** verhindert, dass Benutzer die Einstellung für den Diebstahlschutzmodus auf dem Gerät auswählen können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Cortana**: **Blockieren** deaktiviert den Sprach-Assistenten Cortana auf dem Gerät. Wenn Cortana deaktiviert ist, können Benutzer trotzdem suchen, um Elemente auf dem Gerät zu finden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem Cortana standardmäßig zu.

  [Experience/AllowCortana-CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowcortana)

- **Sprachaufzeichnung (nur Mobilgerät)** : **Blockieren** verhindert, dass Benutzer die Sprachaufzeichnung auf dem Gerät verwenden können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig Sprachaufzeichnungen für Apps zu.
- **Gerätenamensänderung** (nur Mobilgeräte): **Blockieren** verhindert, dass Benutzer den Namen des Geräts ändern können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Bereitstellungspakete hinzufügen:** **Blockieren** verhindert, dass der Laufzeitkonfigurations-Agent Bereitstellungspakete auf dem Gerät installieren kann. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Bereitstellungspakete entfernen:** **Blockieren** verhindert, dass der Laufzeitkonfigurations-Agent Bereitstellungspakete vom dem Gerät entfernt. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Geräteerkennung:** **Blockieren** verhindert, dass ein Gerät von anderen Geräten erkannt wird. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

  [Experience/AllowDeviceDiscovery](/windows/client-management/mdm/policy-csp-experience#experience-allowdevicediscovery)

- **Programmumschaltung (nur mobile Geräte):** **Blockieren** verhindert Programmumschaltung auf dem Gerät. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Dialogfeld bei SIM-Kartenfehler** (nur mobile Geräte): **Blockiert** die Anzeige einer Fehlermeldung auf dem Gerät, wenn keine SIM-Karte erkannt wird. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise zeigt das Betriebssystem die Fehlermeldungen standardmäßig an.
- **Ink-Arbeitsbereich:** Wählen Sie aus, ob und wie Benutzer Zugriff auf den Ink-Arbeitsbereich besitzen. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Möglicherweise aktiviert das Betriebssystem standardmäßig den Ink-Arbeitsbereich, und Benutzer können ihn auf dem Sperrbildschirm verwenden.
  - **Für Sperrbildschirm deaktiviert**: Der Ink-Arbeitsbereich ist aktiviert, und die Funktion ist aktiviert. Benutzer können jedoch nicht auf dem Sperrbildschirm darauf zugreifen.
  - **Deaktiviert:** Der Zugriff auf den Ink-Arbeitsbereich ist deaktiviert. Die Funktion ist deaktiviert.

  [WindowsInkWorkspace-Richtlinien-CSP](/windows/client-management/mdm/policy-csp-windowsinkworkspace)

- **Autopilot-Zurücksetzung**: Wählen Sie **Zulassen** aus, damit Benutzer mit Administratorrechten alle Benutzerdaten und -einstellungen über **STRG+Windows+R** vom Sperrbildschirm des Geräts aus löschen können. Das Gerät wird automatisch neu konfiguriert und bei der Verwaltung erneut registriert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig könnte das Betriebssystem diese Funktion verhindern.
- **Benutzer müssen während der Geräteeinrichtung eine Netzwerkverbindung herstellen**: Klicken Sie auf **Anfordern**, damit das Gerät eine Verbindung mit einem Netzwerk herstellen muss, bevor es während der Einrichtung von Windows mit dem Prozess nach der Seite „Netzwerk“ fortfährt. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Benutzer auch dann über die Seite „Netzwerk“ hinausgehen, wenn keine Verbindung mit einem Netzwerk besteht.

  Die Einstellung wird beim nächsten Zurücksetzen des Geräts wirksam. Wie jede andere Intune-Konfiguration muss das Gerät von Intune registriert und verwaltet werden, um Konfigurationseinstellungen zu empfangen. Sobald es jedoch registriert ist und Richtlinien empfängt, erzwingt das Zurücksetzen des Geräts die Einstellung während des nächsten Setups von Windows.

  [TenantLockdown-CSP](/windows/client-management/mdm/tenantlockdown-csp)

- **Direkter Speicherzugriff**: Die **Blockierung** verhindert den direkten Speicherzugriff (Direct Memory Access, DMA) für alle Hot-Plug-PCI-Downstreamports, bis sich ein Benutzer bei Windows anmeldet. **Aktiviert** (Standardeinstellung) ermöglicht den Zugriff auf DMA selbst dann, wenn ein Benutzer nicht angemeldet ist.

  [DataProtection/AllowDirectMemoryAccess-CSP](/windows/client-management/mdm/policy-csp-dataprotection#dataprotection-allowdirectmemoryaccess)

- **End processes from Task Manager** (Prozesse über den Task-Manager beenden): Diese Einstellung bestimmt, ob der Task-Manager von anderen Benutzern als Administratoren zum Beenden von Tasks verwendet werden darf. Die Option **Blockieren** verhindert, dass Standardbenutzer (also keine Administratoren) den Task-Manager zum Beenden von Prozessen oder Tasks auf dem Gerät verwenden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Standardbenutzer Prozesse oder Tasks über den Task-Manager beenden können.

  [TaskManager/AllowEndTask-CSP](/windows/client-management/mdm/policy-csp-taskmanager#taskmanager-allowendtask)

## <a name="locked-screen-experience"></a>Gesperrter Bildschirm

- **Benachrichtigungen des Info-Centers (nur Mobilgerät):** **Blockieren** verhindert die Anzeige von Info-Center-Benachrichtigungen auf dem Gerätesperrbildschirm. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Benutzer auswählen können, welche Apps Benachrichtigungen auf dem Sperrbildschirm anzeigen können.

  [AboveLock/AllowActionCenterNotifications-CSP](/windows/client-management/mdm/policy-configuration-service-provider#AboveLock_AllowActionCenterNotifications)

- **URL zu Bild für gesperrten Bildschirm (nur Desktop):** Geben Sie die URL zu einem Bild im JPG-, JPEG- oder PNG-Format ein, das als Hintergrund für den Windows-Sperrbildschirm verwendet wird. Geben Sie beispielsweise `https://contoso.com/image.png` ein. Diese Einstellung sperrt das Bild und kann nicht nachträglich geändert werden.

  [Personalization/LockScreenImageUrl-CSP](/windows/client-management/mdm/personalization-csp)

- **Vom Benutzer konfigurierbares Bildschirmtimeout (nur Mobilgeräte):** **Zulassen** ermöglicht Benutzern das Konfigurieren des Bildschirmtimeouts. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise stellt das Betriebssystem diese Option standardmäßig nicht für Benutzer zur Verfügung.

  [DeviceLock/AllowScreenTimeoutWhileLockedUserConfig-CSP](/windows/client-management/mdm/policy-configuration-service-provider#DeviceLock_AllowScreenTimeoutWhileLockedUserConfig)

- **Cortana auf Sperrbildschirm (nur Desktopgeräte)** : **Blockieren** verhindert, dass Benutzer mit Cortana interagieren, wenn auf dem Gerät der Sperrbildschirm zu sehen ist. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig eine Interaktion mit Cortana zu.

  [AboveLock/AllowCortanaAboveLock-CSP](/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowcortanaabovelock)

- **Toast notifications on locked screen** (Popupbenachrichtigungen auf Sperrbildschirm): **Blockieren** verhindert die Anzeige von Popupbenachrichtigungen auf dem Gerätesperrbildschirm. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem diese Benachrichtigungen standardmäßig zu.

  [AboveLock/AllowToasts-CSP](/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowtoasts)

- **Bildschirmtimeout (nur Mobilgeräte):** Legt die Dauer (in Sekunden) zwischen der Bildschirmsperre und dem Abschalten des Bildschirms fest. Die Werte 11 bis 1.800 werden unterstützt. Geben Sie z.B. `300` ein, um diesen Timeoutwert auf 5 Minuten festzulegen.

  [DeviceLock/ScreenTimeoutWhileLocked-CSP](/windows/client-management/mdm/policy-configuration-service-provider#DeviceLock_ScreenTimeoutWhileLocked)

## <a name="messaging"></a>Messaging

Diese Einstellungen verwenden den [Messagingrichtlinien-CSP](/windows/client-management/mdm/policy-csp-messaging), der auch die unterstützten Windows-Editionen auflistet.

- **Nachrichtensynchronisierung (nur mobil):** **Blockieren** deaktiviert die Sicherung und Wiederherstellung von SMS-Nachrichten sowie die Synchronisierung zwischen Windows-Geräten. Die Deaktivierung verhindert, dass Informationen auf Servern gespeichert werden, deren Kontrolle außerhalb der Organisation liegt. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Benutzer diese Einstellungen ändern und ihre Nachrichten synchronisieren können.
- **MMS (nur mobil):** **Blockieren** deaktiviert die Funktion zum Senden/Empfangen von MMS auf dem Gerät. Verwenden Sie diese Richtlinie für Unternehmen, um MMS im Rahmen der Überwachungs- oder Verwaltungsanforderungen auf Geräten zu deaktivieren. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass MMS gesendet und empfangen werden.
- **RCS (nur mobil)** : **Blockieren** deaktiviert die Funktion für RCS-Sendevorgänge/Empfangsvorgänge (Rich Communication Services) auf dem Gerät. Verwenden Sie diese Richtlinie für Unternehmen, um RCS im Rahmen der Überwachungs- oder Verwaltungsanforderungen auf Geräten zu deaktivieren. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass RCS gesendet und empfangen werden.

## <a name="microsoft-edge-browser"></a>Microsoft Edge-Browser

Diese Einstellungen verwenden den [Browserrichtlinien-CSP](/windows/client-management/mdm/policy-csp-browser), der auch die unterstützten Windows-Editionen auflistet.

> [!NOTE]
> Die Verwendung des Browserrichtlinien-CSP gilt für Microsoft Edge-Version 45 und früher. Für Microsoft Edge Enterprise-Version 77 und höher finden Sie Informationen unter [Konfigurieren von Microsoft Edge-Richtlinieneinstellungen mit Microsoft Intune](/DeployEdge/configure-edge-with-intune).

### <a name="use-microsoft-edge-kiosk-mode"></a>Verwenden des Microsoft Edge-Kioskmodus

Die verfügbaren Einstellungen hängen davon ab, was Sie wählen. Folgende Optionen sind verfügbar:

- **Nein** (Standard): Microsoft Edge wird nicht im Kioskmodus ausgeführt. Sie können alle Microsoft Edge-Einstellungen ändern und konfigurieren.
- **Digitale/interaktive Beschilderung (Kiosk mit einzelner App)** : Filtert Microsoft Edge-Einstellungen, die für „Digitale/interaktive Beschilderung“ in Frage kommen. Der Kioskmodus von Microsoft Edge ist nur für die Verwendung auf Windows 10-Kiosks mit einzelner App vorgesehen. Wählen Sie diese Einstellung, um eine URL im Vollbildmodus zu öffnen und nur den Inhalt dieser Website anzuzeigen. Weitere Informationen zu diesem Feature finden Sie unter [Einrichten digitaler Beschilderungen](/windows/configuration/setup-digital-signage).
- **Öffentliches Browsen (InPrivate, Kiosk mit einzelner App)** : Filtert Microsoft Edge-Einstellungen, die für „Öffentliches Browsen (InPrivate)“ in Frage kommen. Der Kioskmodus von Microsoft Edge ist für die Verwendung auf Windows 10-Kiosks mit einzelner App vorgesehen. Führt eine Version von Microsoft Edge mit mehreren Registerkarten aus.
- **Normalmodus (Kiosk mit mehreren Apps)** : Filtert Microsoft Edge-Einstellungen, die für den normalen Kioskmodus von Microsoft Edge gelten. Führt eine Vollversion von Microsoft Edge mit sämtlichen Funktionen für das Browsen aus.
- **Öffentliches Browsen (Kiosk mit mehreren Apps)** : Filtert Microsoft Edge-Einstellungen, die für das öffentliche Browsen auf einem Windows 10-Kiosk mit mehreren Apps gelten.  Führt eine Version von Microsoft Edge-InPrivate mit mehreren Registerkarten aus.

> [!TIP]
> Weitere Informationen zur Aufgabe dieser Optionen finden Sie unter [Konfigurationstypen für den Microsoft Edge-Kioskmodus](/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-configuration-types).

Dieses Geräteeinschränkungsprofil steht in direktem Zusammenhang mit dem Kioskprofil, das Sie mithilfe der [Windows-Kioskeinstellungen](kiosk-settings-windows.md) erstellen. Zusammenfassung:

1. Erstellen Sie das Profil [Windows-Kioskeinstellungen](kiosk-settings-windows.md), um das Gerät im Kioskmodus auszuführen. Wählen Sie Microsoft Edge als Anwendung aus, und legen Sie den Microsoft Edge-Kioskmodus im Profil „Kiosk“ fest.
2. Erstellen Sie das in diesem Artikel beschriebene Profil für Geräteeinschränkungen, und konfigurieren Sie spezifische Funktionen und Einstellungen, die in Microsoft Edge zulässig sind. Stellen Sie sicher, dass Sie den gleichen Microsoft Edge-Kioskmodustyp wie in Ihrem Kioskprofil wählen ([Windows-Kioskeinstellungen](kiosk-settings-windows.md)). 

    Unter [Unterstützte Einstellungen für den Kioskmodus ](/microsoft-edge/deploy/microsoft-edge-kiosk-mode-deploy#supported-policies-for-kiosk-mode) finden Sie hilfreiche Informationen.

> [!IMPORTANT] 
> Achten Sie darauf, dass dieses Microsoft Edge-Profil den gleichen Geräten wie Ihr Kioskprofil zugewiesen wird ([Windows-Kioskeinstellungen](kiosk-settings-windows.md)).

[CSP: ConfigureKioskMode](/windows/client-management/mdm/policy-csp-browser#browser-configurekioskmode)

### <a name="start-experience"></a>Startoberfläche

- **Start Microsoft Edge with** (Microsoft Edge starten mit): Wählen Sie aus, welche Seiten beim Starten von Microsoft Edge geöffnet werden. Folgende Optionen sind verfügbar:
  - **Benutzerdefinierte Startseiten**: Geben Sie die Startseiten ein, z. B. `http://www.contoso.com`. Microsoft Edge lädt die Startseiten, die Sie eingeben.
  - **Neue Registerkartenseite:** Microsoft Edge lädt, was in der Einstellung **URL für neue Registerkartenseite** eingegeben wird.
  - **Seite der letzten Sitzung**: Microsoft Edge lädt die Seite der letzten Sitzung.
  - **Startseiten in lokalen App-Einstellungen**: Microsoft Edge beginnt mit der vom Betriebssystem definierten Standardstartseite.

- **Benutzern das Ändern von Startseiten gestatten**: Wenn die Option **Ja** (Standard) ausgewählt ist, können Benutzer die Startseiten ändern. Administratoren können mithilfe der `EdgeHomepageUrls` die Startseiten eingeben, die Benutzern standardmäßig beim Öffnen von Microsoft Edge angezeigt werden. **Nein** hindert Benutzer daran, Änderungen an den Startseiten vorzunehmen.
- **Webinhalte auf neuer Registerkartenseite zulassen**: Bei Festlegung auf **Ja** (Standard) öffnet Microsoft Edge die URL, die in der Einstellung **URL der neuen Registerkarte** eingegeben wurde. Wenn die Einstellung **URL der neuen Registerkarte** leer ist, öffnet Microsoft Edge die neue Registerkartenseite, die in den Microsoft Edge-Einstellungen aufgeführt wird. Benutzer können diese Angabe ändern. Bei Festlegung auf **Nein** öffnet Microsoft Edge eine neue Registerkarte mit einer leeren Seite. Benutzer können dies nicht ändern.
- **URL der neuen Registerkarte**: Geben Sie die URL an, die auf der neuen Registerkartenseite geöffnet werden soll. Geben Sie beispielsweise `https://www.bing.com` oder `https://www.contoso.com` ein.

- **Startschaltfläche:** Wählen Sie aus, was geschieht, wenn die Startschaltfläche ausgewählt wird. Folgende Optionen sind verfügbar:
  - **Startseiten:** Öffnet die Option, die Sie für die Einstellung **Microsoft Edge starten mit** ausgewählt haben.
  - **Neue Registerkartenseite:** Öffnet die URL, die Sie in der Einstellung **URL der neuen Registerkarte** eingegeben haben.
  - **URL der Startschaltfläche**: Geben Sie die zu öffnende URL ein. Geben Sie beispielsweise `https://www.bing.com` oder `https://www.contoso.com` ein.
  - **Startschaltfläche ausblenden:** blendet die Startschaltfläche aus.
- **Benutzern das Ändern der Startschaltfläche gestatten**: Wenn die Option **Ja** ausgewählt ist, können Benutzer die Startschaltfläche ändern. Die Änderungen des Benutzers setzen Administratoreinstellungen für die Startschaltfläche außer Kraft. **Nein** (Standard) verhindert, dass Benutzer ändern können, wie der Administrator die Startschaltfläche konfiguriert hat.
- **Willkommensseite anzeigen (nur Mobilgeräte)** : **Ja** (Standard) zeigt die Willkommensseite zur ersten Verwendung in Microsoft Edge an. **Nein** verhindert, dass die Einführungsseite bei der ersten Ausführung von Microsoft Edge angezeigt wird. Diese Funktion ermöglicht Unternehmen (z.B. Organisationen, die in Nullemissionskonfigurationen registriert sind), diese Seite zu blockieren.
- **Speicherort für URL-Liste für Windows-Willkommensseite** (nur mobile Windows 10-Geräte): Geben Sie die URL ein, die auf die XML-Datei verweist, die die URL(s) der Willkommensseite enthält. Geben Sie beispielsweise `https://www.contoso.com/sites.xml` ein.

- **Browser nach Leerlaufzeit aktualisieren:** Geben Sie die Anzahl der Leerlaufminuten bis zur Aktualisierung des Browsers ein (von 0–1440 Minuten). Der Standardwert ist `5` Minuten. Bei Festlegung auf `0` wird der Browser nach einem Leerlauf nicht aktualisiert.

  Diese Einstellung ist nur bei Ausführung im Modus [Öffentliches Browsen (InPrivate, Kiosk mit einzelner App)](#use-microsoft-edge-kiosk-mode) verfügbar.

- **Popups zulassen** (nur Desktop): **Ja** (Standard) lässt Popups im Webbrowser zu. **Nein** verhindert Popupfenster im Browser.
- **Intranetdatenverkehr an Internet Explorer senden**: Die Option **Ja** erlaubt Benutzern, Websites im Intranet im Internet Explorer anstatt in Microsoft Edge zu öffnen. Diese Einstellung dient der Abwärtskompatibilität. **Nein** ermöglicht Benutzern die Verwendung von Microsoft Edge.
- **Speicherort der Websiteliste für den Unternehmensmodus** (nur Desktop): Geben Sie die URL ein, die auf die XML-Datei verweist, die eine Liste der Websites enthält, die im Unternehmensmodus geöffnet werden. Benutzer können diese Liste nicht ändern. Geben Sie beispielsweise `https://www.contoso.com/sites.xml` ein.
- **Message when opening sites in Internet Explorer** (Meldung beim Öffnen von Websites im Internet Explorer): Verwenden Sie diese Einstellung, um zu konfigurieren, dass Microsoft Edge eine Benachrichtigung anzeigt, bevor eine Website in Internet Explorer 11 geöffnet wird. Folgende Optionen sind verfügbar:
  - **Meldung nicht anzeigen**: Das Standardverhalten des Betriebssystems wird verwendet, d. h. möglicherweise wird keine Meldung angezeigt.
  - **Meldung anzeigen, dass Website in Internet Explorer 11 geöffnet wird**: zeigt die Meldung beim Öffnen von Websites im Internet Explorer an. Websites werden im Internet Explorer geöffnet. 
  - **Meldung mit Option zum Öffnen von Websites in Microsoft Edge anzeigen**: Meldung beim Öffnen von Websites in Microsoft Edge anzeigen: Die Meldung enthält einen Link **Weiter in Microsoft Edge**, damit Benutzer Microsoft Edge anstelle von Internet Explorer auswählen können.

  > [!IMPORTANT]
  > Für diese Einstellung müssen Sie die Einstellung **Unternehmensmodus-Websiteliste** konfigurieren, die Einstellung **Intranetdatenverkehr an Internet Explorer senden** oder beide Einstellungen aktivieren.

- **Microsoft-Kompatibilitätsliste zulassen**: **Ja** (Standard) ermöglicht die Verwendung einer Microsoft-Kompatibilitätsliste. **Nein** verhindert die Microsoft-Kompatibilitätsliste in Microsoft Edge. Mithilfe dieser Liste von Microsoft kann Microsoft Edge Websites mit bekannten Kompatibilitätsproblemen ordnungsgemäß anzeigen.
- **Startseiten und neue Registerkartenseite vorab laden**: **Ja** (Standard) verwendet das Standardverhalten des Betriebssystems, d. h. die Seiten werden möglicherweise vorab geladen. Das Vorabladen minimiert die Zeit zum Starten von Microsoft Edge und Laden neuer Registerkarten. **Nein** verhindert, dass Microsoft Edge Startseiten und die neue Registerkartenseite vorab lädt.
- **Prelaunch Start pages and New Tab page** (Startseiten und neue Registerkartenseite vorab starten): **Ja** (Standard) verwendet das Standardverhalten des Betriebssystems, d. h. die Seiten werden möglicherweise vorab gestartet. Vorabstarten steigert die Leistung von Microsoft Edge und minimiert die zum Starten von Microsoft Edge erforderliche Zeit. **Nein** verhindert, dass Microsoft Edge Startseiten und die neue Registerkartenseite vorab startet.

### <a name="favorites-and-search"></a>Favoriten und Suche

- **Favoritenleiste anzeigen**: Wählen Sie aus, was mit der Favoritenleiste auf einer beliebigen Seite von Microsoft Edge geschehen soll. Folgende Optionen sind verfügbar:
  - **Auf Start- und neuen Registerkartenseiten**: Zeigt die Favoritenleiste beim Starten von Microsoft Edge und auf allen Registerkartenseiten an. Benutzer können diese Einstellung ändern.
  - **Auf allen Seiten**: zeigt die Favoritenleiste auf allen Seiten an. Benutzer können diese Einstellung nicht ändern.
  - **Ausgeblendet:** blendet die Favoritenleiste auf allen Seiten aus. Benutzer können diese Einstellung nicht ändern.
- **Änderungen an Favoriten zulassen**: **Ja** (Standard) verwendet die Standardeinstellung des Betriebssystems, die Benutzern das Ändern der Liste ermöglicht. **Nein** verhindert, dass Benutzer die Favoritenliste hinzufügen, importieren, sortieren oder bearbeiten können.
  - **Favoritenliste:** Fügt eine Liste von URLs zur Favoritendatei hinzu. Fügen Sie z.B. `http://contoso.com/favorites.html` hinzu.
- **Das Synchronisieren von Favoriten zwischen Microsoft-Browsern zulassen** (nur Desktopgeräte): Die Option **Ja** erzwingt, dass Windows die Favoriten zwischen Internet Explorer und Microsoft Edge synchronisiert. Favoriten betreffende Hinzufügungen, Löschungen, Änderungen und Anordnungsänderungen werden zwischen Browsern freigegeben.  **Nein** (Standard) verwendet den Betriebssystemstandard, sodass Benutzer möglicherweise die Synchronisierung von Favoriten zwischen den Browsern auswählen können.
- **Default search engine** (Standardsuchmaschine): Wählen Sie die Standardsuchmaschine für das Gerät aus. Benutzer können diesen Wert jederzeit ändern. Folgende Optionen sind verfügbar:
  - Suchmodul in Microsoft Edge-Clienteinstellungen
  - Bing
  - Google
  - Yahoo
  - Benutzerdefinierter Wert: Geben Sie in **OpenSearch-XML-URL** eine HTTPS-URL mit der XML-Datei ein, die mindestens den Kurznamen und die URL für das Suchmodul enthält. Geben Sie beispielsweise `https://www.contoso.com/opensearch.xml` ein.
- **Suchvorschläge anzeigen**: Die Option **Ja** (Standard) ermöglicht es der Suchmaschine, Websites während der Eingabe von Suchausdrücken in der Adressleiste vorzuschlagen. **Nein** verhindert die Verwendung dieser Funktion.
- **Änderungen am Suchmodul zulassen**: **Ja** (Standard) ermöglicht es Benutzern, neue Suchmaschinen hinzuzufügen oder die Standardsuchmaschine in Microsoft Edge zu ändern. Wählen Sie **Nein**, um zu verhindern, dass Benutzer die Suchmaschine anpassen.

  Diese Einstellung ist nur bei Ausführung im [Normalmodus (Kiosk mit mehreren Apps)](#use-microsoft-edge-kiosk-mode) verfügbar.

### <a name="privacy-and-security"></a>Datenschutz und Sicherheit

- **InPrivate-Browsen zulassen**: **Ja** (Standard) ermöglicht das InPrivate-Browsen in Microsoft Edge. Nach dem Schließen alle InPrivate-Registerkarten löscht Microsoft Edge die Browserdaten vom Gerät. **Nein** verhindert, dass Benutzer InPrivate-Browsersitzungen öffnen.
- **Browserverlauf speichern:** **Ja** (Standard) lässt das Speichern des Browserverlaufs in Microsoft Edge zu. **Nein** verhindert, dass der Browserverlauf gespeichert wird.
- **Browserdaten beim Beenden löschen (Nur Desktopgeräte)** : Die Option **Ja** löscht den Verlauf sowie die Browserdaten, wenn Benutzer Microsoft Edge beenden. **Nein** (Standard) verwendet den Betriebssystemstandard, d.h. die Browserdaten werden möglicherweise zwischengespeichert.
- **Sync browser settings between user's devices** (Browsereinstellungen zwischen Benutzergeräten synchronisieren): Legen Sie fest, wie die Browsereinstellungen zwischen den Geräten synchronisiert werden sollen. Folgende Optionen sind verfügbar:
  - **Zulassen:** Lässt die Synchronisierung von Microsoft Edge-Browsereinstellungen zwischen Benutzergeräten zu.
  - **Block and enable user override** (Außerkraftsetzung durch Benutzer blockieren und aktivieren): Blockiert die Synchronisierung von Microsoft Edge-Browsereinstellungen zwischen Benutzergeräten. Benutzer können diese Einstellung überschreiben.
  - **Blockieren:** Blockieren der Synchronisierung von Microsoft Edge-Browsereinstellungen zwischen Geräten von Benutzern. Benutzer können diese Einstellung nicht überschreiben.

Wenn „Außerkraftsetzung durch Benutzer blockieren und aktivieren“ ausgewählt ist, kann der Benutzer die Administratorfestlegung überschreiben.

- **Kennwort-Manager zulassen**: **Ja** (Standard) ermöglicht es, dass Microsoft Edge automatisch den Kennwort-Manager verwendet. Dies ermöglicht es Benutzern, Kennwörter auf dem Gerät zu speichern und zu verwalten. **Nein** verhindert, dass Microsoft Edge den Kennwort-Manager verwendet.
- **Cookies**: Wählen Sie aus, wie Cookies im Webbrowser verarbeitet werden sollen. Folgende Optionen sind verfügbar:
  - **Zulassen:** ermöglicht das Speichern von Cookies auf dem Gerät.
  - **Block all cookies** (Alle Cookies blockieren): Cookies werden nicht auf dem Gerät gespeichert.
  - **Nur Cookies von Drittanbietern blockieren:** Cookies von Drittanbietern oder Partnern werden nicht auf dem Gerät gespeichert.
- **AutoAusfüllen in Formularen zulassen**: **Ja** (Standard) ermöglicht Benutzern das Ändern der Einstellungen für automatische Vervollständigung im Browser und automatisches Auffüllen der Felder eines Formulars mit Daten. **Nein** deaktiviert das Feature „AutoAusfüllen“ in Microsoft Edge.
- **DNT-Kopfzeilen senden**: **Ja** sendet DNT-Kopfzeilen an Websites, die Nachverfolgungsinformationen anfordern (empfohlen). **Nein** (Standard) sendet keine Header, die Websites das Nachverfolgen von Benutzern ermöglichen. Diese Einstellung kann von Benutzern konfiguriert werden.
- **WebRTC-Localhost-IP-Adresse anzeigen**: **Ja** (Standard) ermöglicht die Anzeige der Localhost-IP-Adressen von Benutzern bei Telefonaten mit diesem Protokoll. **Nein** verhindert, dass die Localhost-IP-Adresse des Benutzers angezeigt wird. 
- **Datensammlung für Livekacheln zulassen**: **Ja** (Standard) ermöglicht es Microsoft Edge, Informationen von Livekacheln zu erfassen, die an das Startmenü angeheftet sind. **Nein** verhindert, dass diese Informationen erfasst werden. Dies kann für Benutzer zu eingeschränkten Funktionen führen.
- **User can override certificate errors** (Benutzer kann Zertifikatfehler außer Kraft setzen): **Ja** (Standard) ermöglicht Benutzern den Zugriff auf Websites, die SSL-/TLS-Fehler (Secure Sockets Layer/Transport Layer Security) enthalten. **Nein** (für erhöhte Sicherheit empfohlen) verhindert, dass Benutzer auf Websites mit SSL- oder TLS-Fehlern zugreifen können.

### <a name="additional"></a>Zusätzliche Informationen

- **Microsoft Edge-Browser zulassen** (nur Mobilgeräte): **Ja** (Standard) ermöglicht die Verwendung des Microsoft Edge-Webbrowsers auf dem mobilen Gerät. **Nein** verhindert die Verwendung von Microsoft Edge auf Geräten. Wenn Sie **Nein** auswählen, gelten die anderen individuellen Einstellungen nur für den Desktop.
- **Adressleisten-Dropdownliste zulassen**: **Ja** (Standard) ermöglicht es Microsoft Edge, die Adressleisten-Dropdownliste mit einer Liste der Vorschläge anzuzeigen. **Nein** verhindert, dass Microsoft Edge bei der Eingabe weiterhin eine Liste mit Vorschlägen in einer Dropdownliste anzeigt. Wenn Sie diese Einstellung auf **Nein** festlegen:
  - Kann die zwischen Microsoft Edge und Microsoft-Diensten genutzte Netzwerkbandbreite minimiert werden.
  - Deaktivieren Sie die **Such- und Websitevorschläge während der Eingabe anzeigen** in „Microsoft Edge > Einstellungen“.
- **Vollbildmodus zulassen**: **Ja** (Standard) ermöglicht es Microsoft Edge, den Vollbildmodus zu verwenden, der nur die Webinhalte anzeigt und die Benutzeroberfläche von Microsoft Edge ausblendet. **Nein** verhindert den Vollbildmodus in Microsoft Edge.
- **Seite "Informationen zu Flags" zulassen**: **Ja** (Standard) verwendet den Betriebssystemstandard, sodass Benutzer auf die `about:flags`-Seite zugreifen können. Die `about:flags`-Seite ermöglicht Benutzern das Ändern der Entwicklereinstellungen und das Aktivieren experimenteller Features. **Nein** verhindert, dass Benutzer auf die `about:flags`-Seite in Microsoft Edge zugreifen können.
- **Entwicklertools zulassen**: **Ja** (Standard) ermöglicht Benutzern standardmäßig die Verwendung der F12-Entwicklertools zum Erstellen und Debuggen von Webseiten. **Nein** verhindert, dass Benutzer die F12-Entwicklertools verwenden können.
- **JavaScript zulassen**: **Ja** (Standard) Lässt die Ausführung von Skripts wie z. B. JavaScript im Microsoft Edge-Browser zu. **Nein** verhindert, dass Java-Skripts im Browser ausgeführt werden.
- **Benutzer können Erweiterungen installieren**: Die Option **Ja** (Standard) lässt zu, dass Benutzer Microsoft Edge-Erweiterungen auf Geräten installieren. **Nein** verhindert die Installation.
- **Querladen von Entwicklererweiterungen zulassen**: **Ja** (Standard) verwendet den Betriebssystemstandard, der das Querladen möglicherweise erlaubt. Das Querladen installiert nicht überprüfte Erweiterungen und führt sie aus. **Nein** verhindert, dass Microsoft Edge mit dem Feature **Erweiterungen laden** Erweiterungen querladen kann. Die Angabe „Nein“ verhindert nicht das Querladen von Erweiterungen mit anderen Methoden, z.B. mit PowerShell.
- **Erforderliche Erweiterungen:** Wählen Sie aus, welche Erweiterungen in Microsoft Edge nicht von Benutzern deaktiviert werden können. Geben Sie die Paketfamiliennamen ein, und wählen Sie **Hinzufügen** aus. Einige hilfreiche Informationen finden Sie unter [Suchen eines Paketfamiliennamens (PFN) für das Pro-App-VPN](/configmgr/protect/deploy-use/find-a-pfn-for-per-app-vpn).

  Sie können auch eine CSV-Datei **Importieren**, die die Paketfamiliennamen enthält. Oder **exportieren** Sie die Paketfamiliennamen, die Sie eingeben.

## <a name="network-proxy"></a>Netzwerkproxy

Diese Einstellungen verwenden den [NetworkProxy-Richtlinien-CSP](/windows/client-management/mdm/networkproxy-csp), der auch die unterstützten Windows-Editionen auflistet.

- **Proxyeinstellungen automatisch erkennen:** **Blockieren** deaktiviert, dass Geräte ein Skript für die automatische Proxykonfiguration (PAC-Skript) automatisch erkennen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise aktiviert das Betriebssystem dieses Feature standardmäßig, und Geräte versuchen, den Pfad zu einem PAC-Skript zu finden.
- **Use proxy script** (Proxyskript verwenden): Wählen Sie **Zulassen** aus, um einen Pfad zu Ihrem PAC-Skript zum Konfigurieren des Proxyservers anzugeben. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig nicht zu, dass Sie die URL zu einem PAC-Skript eingeben können.
  - **Adress-URL für Setupskript:** Geben Sie die URL eines PAC-Skripts an, das Sie verwenden möchten, um den Proxyserver zu konfigurieren.
- **Use manual proxy server** (Manuellen Proxyserver verwenden): Wählen Sie **Zulassen** aus, um den Namen oder die IP-Adresse und die TCP-Portnummer eines Proxyservers manuell einzugeben. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise nicht zu, dass Sie Details eines Proxyservers manuell eingeben.
  - **Adresse**: Geben Sie den Namen oder die IP-Adresse des Proxyservers an.
  - **Portnummer:** Geben Sie die Portnummer Ihres Proxyservers ein.
  - **Proxyausnahmen:** Geben Sie URLs an, die den Proxyserver nicht verwenden dürfen. Trennen Sie die einzelnen Elemente durch Semikola (`;`).
  - **Bypass proxy server for local address** (Proxyserver für lokale Adressen umgehen): Bei Auswahl von **Zulassen** wird der Proxyserver nicht für lokale Adressen (Intranet) verwendet. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise verwendet das Betriebssystem standardmäßig einen Proxyserver für lokale Adressen in Ihrem Intranet.

## <a name="password"></a>Kennwort

Diese Einstellungen verwenden den [DeviceLock-Richtlinien-CSP](/windows/client-management/mdm/policy-csp-devicelock), der auch die unterstützten Windows-Editionen auflistet.

- **Kennwort:** Wenn **Anfordern** festgelegt wird, müssen Benutzer ein Kennwort eingeben, um auf das Gerät zuzugreifen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem den Zugriff auf Geräte möglicherweise ohne Kennwort zu. Diese Einstellung gilt nur für lokale Konten. Kennwörter für Domänenkonten werden weiterhin von Active Directory (AD) und Azure AD konfiguriert.

  [DeviceLock/DevicePasswordEnabled-CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordenabled)

  - **Erforderlicher Kennworttyp:** Wählen Sie den Kennworttyp aus. Folgende Optionen sind verfügbar:
    - **Nicht konfiguriert:** Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise zu, dass das Kennwort Zahlen und Buchstaben enthält.
    - **Alphanumerisch**: Das Kennwort muss aus einer Kombination aus Ziffern und Buchstaben bestehen.
    - **Numerisch**: Das Kennwort darf nur aus Zahlen bestehen.

    [DeviceLock/AlphanumericDevicePasswordRequired-CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-alphanumericdevicepasswordrequired)

  - **Minimale Kennwortlänge:** Geben Sie die erforderliche Mindestanzahl von Zeichen ein (zwischen 4 und 16). Geben Sie z.B. `6` ein, um ein mindestens sechs Zeichen langes Kennwort zu verlangen. Möglicherweise legt das Betriebssystem diesen Wert standardmäßig auf `4` fest.
  
    [DeviceLock/MinDevicePasswordLength-CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-mindevicepasswordlength)
  
    > [!IMPORTANT]
    > Wenn die Kennwortanforderung auf einem Windows-Desktop geändert wird, wirkt sich das auf die nächste Anmeldung der Benutzer aus, da Geräte in diesem Moment aus dem Leerlauf in den aktiven Zustand wechseln. Benutzer mit Kennwörtern, die die Anforderungen erfüllen, werden trotzdem aufgefordert, ihre Kennwörter ändern.

  - **Anzahl von fehlgeschlagenen Anmeldungen, bevor das Gerät zurückgesetzt wird:** Geben Sie an, wie häufig ein falsches Kennwort eingegeben werden kann, bevor das Gerät zurückgesetzt wird (bis zu 11 Mal). Die einzugebende gültige Zahl hängt von der Edition ab. Unter [DeviceLock/MaxDevicePasswordFailedAttempts-CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxdevicepasswordfailedattempts) werden die unterstützten Werte aufgeführt. Durch `0` (null) kann die Funktion zum Zurücksetzen des Geräts deaktiviert werden.

    Diese Einstellung besitzt zudem je nach Edition unterschiedliche Auswirkungen. Spezifische Details zu dieser Einstellung finden Sie im [DeviceLock/MaxDevicePasswordFailedAttempts-CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxdevicepasswordfailedattempts).

  - **Maximaler Zeitraum der Inaktivität (in Minuten) bis zur Bildschirmsperrung:** Geben den Zeitraum an, für den sich das Gerät im Leerlauf befinden muss, bevor der Bildschirm gesperrt wird. Geben Sie zum Beispiel `5` ein, um Geräte nach 5 Minuten im Leerlauf zu sperren. Wenn die Einstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert. Möglicherweise legt das Betriebssystem diesen Wert standardmäßig auf `0` (Null) fest, sodass kein Timeout festgelegt wird.

    [DeviceLock/MaxInactivityTimeDeviceLock-CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-maxinactivitytimedevicelock)

  - **Kennwortablauf (Tage):** Geben Sie den Zeitraum in Tagen an, nach dem das Kennwort für das Gerät geändert werden muss (zwischen 1 und 365). Geben Sie beispielsweise `90` an, damit das Kennwort nach 90 Tagen abläuft. Wenn kein Wert angegeben ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert. Möglicherweise legt das Betriebssystem diesen Wert standardmäßig auf `0` (Null) fest, sodass kein Ablauf festgelegt wird.

    [DeviceLock/DevicePasswordExpiration-CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordexpiration)

  - **Wiederverwendung vorheriger Kennwörter verhindern:** Geben Sie die Anzahl der zuvor verwendeten Kennwörter ein, die nicht erneut verwendet werden können, von 1–24. Geben Sie z.B. `5` an, damit ein Benutzer sein neues Kennwort nicht auf sein aktuelles Kennwort oder eines seiner vorherigen vier Kennwörter festlegen kann. Wenn kein Wert angegeben ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.

    [DeviceLock/DevicePasswordHistory-CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-devicepasswordhistory)

  - **Kennwort anfordern, wenn Gerät aus Leerlaufzustand zurückkehrt (Mobile und Holographic)** : Bei Auswahl von **Erforderlich** müssen Benutzer ein Kennwort eingeben, um das Gerät nach dem Leerlauf zu entsperren. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig fordert das Betriebssystem möglicherweise keine PIN und kein Kennwort nach dem Leerlauf an.

    [DeviceLock/AllowIdleReturnWithoutPassword-CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowidlereturnwithoutpassword)

  - **Einfache Kennwörter:** Wenn **Blockieren** festgelegt wird, werden Benutzer daran gehindert, einfache Kennwörter wie `1234` oder `1111` zu erstellen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Benutzer einfache Kennwörter erstellen. Mit dieser Einstellung wird zudem verhindert, dass Bildcodes verwendet werden.

    [DeviceLock/AllowSimpleDevicePassword-CSP](/windows/client-management/mdm/policy-csp-devicelock#devicelock-allowsimpledevicepassword)

- **Automatische Verschlüsselung bei AADJ**: Die Wahl von **Blockieren** verhindert die automatische BitLocker-Geräteverschlüsselung, wenn Geräten für die erste Verwendung vorbereitet werden und wenn das Gerät in Azure AD eingebunden wird. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise aktiviert das Betriebssystem standardmäßig die Verschlüsselung.

  Weitere Informationen zur [Geräteverschlüsselung mit BitLocker](/windows/security/information-protection/bitlocker/bitlocker-device-encryption-overview-windows-10#bitlocker-device-encryption).

  [CSP: Security/PreventAutomaticDeviceEncryptionForAzureADJoinedDevices](/windows/client-management/mdm/policy-csp-security#security-preventautomaticdeviceencryptionforazureadjoineddevices)

- **FIPS-Richtlinie (Federal Information Processing Standard)** : Bei Wahl von **Zulassen** wird die FIPS-Richtlinie (Federal Information Processing Standard) verwendet, die in den USA ein bundesgesetzlicher Standard für Verschlüsselung, Hashing und Signatur ist. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem FIPS standardmäßig nicht zu.

  [CSP: Cryptography/AllowFipsAlgorithmPolicy](/windows/client-management/mdm/policy-csp-cryptography#cryptography-allowfipsalgorithmpolicy)

- **Windows Hello-Geräteauthentifizierung**: Bei Wahl von **Zulassen** wird es Benutzern ermöglicht, sich mit einem Windows Hello-Begleitgerät, wie beispielsweise einem Smartphone, Fitnessband oder IoT-Gerät, bei einem Windows 10-Computer anzumelden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig keine Authentifizierung von Windows Hello-Begleitgeräten zu.

  [CSP: Authentication/AllowSecondaryAuthenticationDevice](/windows/client-management/mdm/policy-csp-authentication#authentication-allowsecondaryauthenticationdevice)

- **Bevorzugte Azure AD-Mandantendomäne**: Geben Sie einen in Ihrer Azure AD-Organisation vorhandenen Domänennamen ein. Wenn sich Benutzer bei dieser Domäne anmelden, müssen sie den Domänennamen nicht eingeben. Geben Sie beispielsweise `contoso.com` ein. Benutzer in der Domäne `contoso.com` können sich mit ihrem Benutzernamen (beispielsweise „`abby`“) anstatt mit „`abby@contoso.com`“ anmelden.

  [CSP: Authentication/PreferredAadTenantDomainName](/windows/client-management/mdm/policy-csp-authentication#authentication-preferredaadtenantdomainname)

## <a name="per-app-privacy-exceptions"></a>App-bezogene Datenschutzausnahmen

Wählen Sie für Apps, die ein anderes Datenschutzverhalten aufweisen als das unter „Standarddatenschutz“ definierte Verhalten die Option **Hinzufügen** aus.

- **Paketname:** Name der App-Paketfamilie.
- **App-Name:** Der Name der App.

### <a name="exceptions"></a>Ausnahmen

- **Kontoinformationen:** Legen Sie fest, ob diese App auf den Benutzernamen, das Bild und andere Kontaktinformationen zugreifen darf.
- **Hintergrund-Apps:** Legen Sie fest, ob diese App im Hintergrund ausgeführt werden darf.
- **Kalender:** Legen Sie fest, ob diese App auf den Kalender zugreifen darf.
- **Anrufliste:** Legen Sie fest, ob diese App auf Ihre Anrufliste zugreifen darf.
- **Kamera:** Legen Sie fest, ob diese App auf die Kamera zugreifen darf.
- **Kontakte:** Legen Sie fest, ob diese App auf Kontakte zugreifen darf.
- **E-Mail:** Legen Sie fest, ob diese App auf E-Mails zugreifen und diese versenden darf.
- **Speicherort:** Legen Sie fest, ob diese App auf Standortinformationen zugreifen darf.
- **Nachrichten:** Legen Sie fest, ob diese App SMS oder MMS-Nachrichten lesen oder senden darf.
- **Mikrofon:** Legen Sie fest, ob diese App das Mikrofon verwenden darf.
- **Bewegung:** Legen Sie fest, ob diese App auf Gerätebewegungsinformationen zugreifen darf.
- **Benachrichtigungen:** Legen Sie fest, ob diese App auf Benachrichtigungen zugreifen darf.
- **Telefon:** Legen Sie fest, ob diese App auf das Telefon zugreifen darf.
- **Funkempfang:** Einige Apps verwenden Funkempfang (z. B. Bluetooth) auf Ihrem Gerät, um Daten zu senden und zu empfangen, und müssen diesen ein- oder ausschalten. Legen Sie fest, ob diese App diese Radios steuern kann.
- **Aufgaben:** Legen Sie fest, ob diese App auf Ihre Aufgaben zugreifen darf.
- **Vertrauenswürdige Geräte:** Legen Sie fest, ob diese App vertrauenswürdige Geräte verwenden kann. Als vertrauenswürdige Geräte wird Hardware angesehen, mit der Sie bereits eine Verbindung hergestellt haben oder die in das Gerät integriert ist. Verwenden Sie z. B. Fernsehgeräte oder Projektoren als vertrauenswürdige Geräte.
- **Feedback and diagnostics** (Feedback und Diagnose): Legen Sie fest, ob diese App auf Diagnoseinformationen zugreifen darf.
- **Sync with devices** (Mit Geräten synchronisieren): Legen Sie fest, ob diese App automatisch Informationen mit Drahtlosgeräten teilen und synchronisieren darf, die nicht explizit an das Gerät gekoppelt sind.

## <a name="personalization"></a>Personalization

Diese Einstellungen verwenden den [Personalisierungsrichtlinien-CSP](/windows/client-management/mdm/personalization-csp), der auch die unterstützten Windows-Editionen auflistet.

- **URL zu Desktophintergrundbild (nur Desktop):** Geben Sie die URL zu einem Bild im JPG-, JPEG-- oder PNG-Format an, das Sie als Windows-Desktophintergrund verwenden möchten. Benutzer können das Bild nicht ändern. Geben Sie beispielsweise `https://contoso.com/logo.png` ein.

  Wenn kein Wert angegeben wird, ändert oder aktualisiert Intune diese Einstellung nicht.

## <a name="printer"></a>Drucker

- **Drucker:** Fügen Sie Drucker unter Verwendung ihrer Netzwerkhostnamen (DNS-Namen) hinzu. Das Betriebssystem sucht für jeden Drucker auf dem Gerät nach einem passenden Druckertreiber und installiert ihn. Wenn Sie keinen Wert eingeben, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

  [Education/PrinterNames-CSP](/windows/client-management/mdm/policy-csp-education#education-printernames)

- **Standarddrucker:** Geben Sie den Netzwerkhostnamen (DNS-Namen) eines installierten Druckers ein, der als Standarddrucker verwendet werden soll. Wenn Sie keinen Wert eingeben, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

  [Education/DefaultPrinterName-CSP](/windows/client-management/mdm/policy-csp-education#education-defaultprintername)

- **Neue Drucker hinzufügen**: Wenn **Blockieren** festgelegt wird, können Benutzer keine neuen Drucker hinzufügen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise das Hinzufügen neuer Drucker zu.

  [Education/PreventAddingNewPrinters-CSP](/windows/client-management/mdm/policy-csp-education#education-preventaddingnewprinters)

## <a name="privacy"></a>Datenschutz

Diese Einstellungen verwenden den [Datenschutzrichtlinien-CSP](/windows/client-management/mdm/policy-csp-privacy), der auch die unterstützten Windows-Editionen auflistet.

- **Datenschutzoberfläche**: Mit **Blockieren** wird verhindert, dass die Datenschutzoberfläche bei der Anmeldung von Benutzern oder für neue und aktualisierte Benutzer angezeigt wird. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

  [Privacy/DisablePrivacyExperience](/windows/client-management/mdm/policy-csp-privacy#privacy-disableprivacyexperience)

- **Eingabepersonalisierung:** **Blockieren** verhindert, dass Benutzer Sprache zum Diktieren verwenden und mit Cortana und anderen Apps sprechen können, die cloudbasierte Microsoft -Spracherkennung verwenden. Die Option ist deaktiviert, und Benutzer können Onlinespracherkennung mithilfe von Einstellungen nicht aktivieren. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Benutzer eine Auswahl treffen. Wenn Sie diese Dienste zulassen, kann Microsoft Voice-Daten erfassen, um den Dienst zu verbessern.

  [Privacy/AllowInputPersonalization-CSP](/windows/client-management/mdm/policy-csp-privacy#privacy-allowinputpersonalization)

- **Automatisches Akzeptieren der Zustimmungsaufforderung des Benutzers zu Kopplung und Datenschutz:** Wählen Sie **Zulassen** aus, um Windows das automatische Akzeptieren der Zustimmungsaufforderung des Benutzers zu Kopplung und Datenschutz zu ermöglichen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise verhindert das Betriebssystem standardmäßig das automatische Akzeptieren.

  [Privacy/AllowAutoAcceptPairingAndPrivacyConsentPrompts-CSP](/windows/client-management/mdm/policy-csp-privacy#privacy-allowautoacceptpairingandprivacyconsentprompts)

- **Benutzeraktivitäten veröffentlichen**: **Blockieren** verhindert, dass Apps und das Betriebssystem Benutzeraktivitäten veröffentlichen. Darüber hinaus werden geteilte Aktivitäten und die Ermittlung von kürzlich verwendeten Ressourcen im Aktivitätsfeed verhindert. Mit Benutzeraktivitäten wird der Status von Benutzeraufgaben in einer App oder im Betriebssystem verfolgt. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise aktiviert das Betriebssystem diese Funktion standardmäßig, sodass Apps Benutzeraktivitäten veröffentlichen können.

  [Privacy/PublishUserActivities-CSP](/windows/client-management/mdm/policy-csp-privacy#privacy-publishuseractivities)

- **Nur lokale Aktivitäten**: Die Option **Blockieren** verhindert geteilte Aktivitäten und Ermittlungen von kürzlich in der Programmumschaltung verwendeten Ressourcen anhand von ausschließlich lokalen Aktivitäten. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

Sie können Informationen definieren, auf die alle Apps auf dem Gerät zugreifen können. Definieren Sie ebenfalls Ausnahmen für jede App mithilfe von **App-bezogenen Datenschutzausnahmen**.

### <a name="exceptions"></a>Ausnahmen

- **Kontoinformationen:** Legen Sie fest, ob diese App auf den Benutzernamen, das Bild und andere Kontaktinformationen zugreifen darf.
- **Hintergrund-Apps:** Legen Sie fest, ob diese App im Hintergrund ausgeführt werden darf.
- **Kalender:** Legen Sie fest, ob diese App auf den Kalender zugreifen darf.
- **Anrufliste:** Legen Sie fest, ob diese App auf Ihre Anrufliste zugreifen darf.
- **Kamera:** Legen Sie fest, ob diese App auf die Kamera zugreifen darf.
- **Kontakte:** Legen Sie fest, ob diese App auf Kontakte zugreifen darf.
- **E-Mail:** Legen Sie fest, ob diese App auf E-Mails zugreifen und diese versenden darf.
- **Speicherort:** Legen Sie fest, ob diese App auf Standortinformationen zugreifen darf.
- **Nachrichten:** Legen Sie fest, ob diese App SMS oder MMS-Nachrichten lesen oder senden darf.
- **Mikrofon:** Legen Sie fest, ob diese App das Mikrofon verwenden darf.
- **Bewegung:** Legen Sie fest, ob diese App auf Gerätebewegungsinformationen zugreifen darf.
- **Benachrichtigungen:** Legen Sie fest, ob diese App auf Benachrichtigungen zugreifen darf.
- **Telefon:** Legen Sie fest, ob diese App auf das Telefon zugreifen darf.
- **Funkempfang:** Einige Apps verwenden Funkempfang (z. B. Bluetooth) auf Ihrem Gerät, um Daten zu senden und zu empfangen, und müssen diesen ein- oder ausschalten. Legen Sie fest, ob diese App diese Radios steuern kann.
- **Aufgaben:** Legen Sie fest, ob diese App auf Ihre Aufgaben zugreifen darf.
- **Vertrauenswürdige Geräte:** Legen Sie fest, ob diese App vertrauenswürdige Geräte verwenden kann. Als vertrauenswürdige Geräte wird Hardware angesehen, mit der Sie bereits eine Verbindung hergestellt haben oder die in das Gerät integriert ist. Verwenden Sie z. B. Fernsehgeräte oder Projektoren als vertrauenswürdige Geräte.
- **Feedback and diagnostics** (Feedback und Diagnose): Legen Sie fest, ob diese App auf Diagnoseinformationen zugreifen kann.
- **Mit Geräten synchronisieren**: Legen Sie fest, ob diese App automatisch Informationen mit Drahtlosgeräten teilen und synchronisieren darf, die nicht explizit mit Ihrem PC, Tablet oder Telefon gekoppelt sind.

## <a name="projection"></a>Projektion

Diese Einstellungen verwenden den [WirelessDisplay-Richtlinien-CSP](/windows/client-management/mdm/policy-csp-wirelessdisplay), der auch die unterstützten Windows-Editionen auflistet.

- **Benutzereingabe über Empfänger der drahtlosen Anzeige:** **Blockieren** verhinder die Benutzereingabe über Empfänger der drahtlosen Anzeige. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass eine drahtlose Anzeige Tastatur-, Maus-, Stift- und Toucheingaben zurück an das Quellgerät sendet.

  [WirelessDisplay/AllowUserInputFromWirelessDisplayReceiver-CSP](/windows/client-management/mdm/policy-csp-wirelessdisplay#wirelessdisplay-allowuserinputfromwirelessdisplayreceiver)

- **Projection to this PC** (Projektion auf diesen PC): **Blockieren** verhindert, dass andere Geräte das Gerät für die Projektion finden. Außerdem wird eine Projektion auf andere Geräte verhindert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass das Gerät erkannt werden kann und eine Projektion auf den Sperrbildschirm des Geräts zulässig ist.

  [WirelessDisplay/AllowProjectionFromPC-CSP](/windows/client-management/mdm/policy-csp-wirelessdisplay#wirelessdisplay-allowprojectionfrompc)

- **PIN für Kopplung erforderlich:** Wählen Sie **Erforderlich** aus, um Benutzer beim Herstellen einer Verbindung mit einem Projektionsgerät immer zur Eingabe einer PIN aufzufordern. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise fordert das Betriebssystem keine PIN an, um das Gerät zu koppeln.

  [WirelessDisplay/RequirePinForPairing-CSP](/windows/client-management/mdm/policy-csp-wirelessdisplay#wirelessdisplay-requirepinforpairing)

## <a name="reporting-and-telemetry"></a>Berichterstellung und Telemetrie

- **Nutzungsdaten freigeben**: Wählen Sie die Ebene der Diagnosedaten aus, die gesendet werden. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Es wird keine Einstellung erzwungen. Benutzer wählen die Ebene für die Übermittlung aus. Möglicherweise gibt das Betriebssystem standardmäßig keine Daten frei.
  - **Sicherheit**: Informationen, die erforderlich sind, um Windows sicherer zu machen, einschließlich Daten zu den Einstellungen der Komponente „Benutzererfahrung und Telemetrie im verbundenen Modus“, zum Tool zum Entfernen bösartiger Software und zu Microsoft Defender
  - **Standard**: Grundlegende Geräteinformationen, z. B. qualitätsbezogene Daten, App-Kompatibilität, App-Nutzungsdaten und Daten aus der Sicherheitsebene
  - **Erweitert**: Zusätzliche Informationen, z. B. zur Verwendung von Windows, Windows Server, System Center oder Anwendungen, Leistungsdaten, erweiterte Zuverlässigkeitsdaten sowie Daten der Ebenen „Standard“ und „Sicherheit“
  - **Vollständig**: Alle Daten, die zur Identifizierung und Behebung von Problemen erforderlich sind, sowie Daten der Ebenen „Sicherheit“, „Standard“ und „Erweitert“.

  [System/AllowTelemetry-CSP](/windows/client-management/mdm/policy-csp-system#system-allowtelemetry)

- **Send Microsoft Edge browsing data to Microsoft 365 Analytics** (Microsoft Edge-Browserdaten an die Microsoft 365-Analyse senden): Damit Sie dieses Feature verwenden können, müssen Sie die Einstellungen für die Option **Nutzungsdaten freigeben** auf **Erweitert** oder **Full** (Vollständig) festlegen. Dieses Feature steuert, welche Daten Microsoft Edge an Microsoft 365 Analytics für Unternehmensgeräte mit einer konfigurierten kommerziellen ID sendet. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert:** Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig kein Erfassen oder Senden von Daten zum Browserverlauf zu.
  - **Only send intranet data** (Nur Intranetdaten senden): Ermöglicht es dem Administrator, den Intranetdatenverlauf zu senden.
  - **Only send internet data** (Nur Internetdaten senden): Ermöglicht es dem Administrator, den Internetdatenverlauf zu senden.
  - **Send intranet and internet data** (Intranet- und Internetdaten senden): Ermöglicht es dem Administrator, den Intranet- und den Internetdatenverlauf zu senden.

  [Browser/ConfigureTelemetryForMicrosoft365Analytics-CSP](/windows/client-management/mdm/policy-csp-browser#browser-configuretelemetryformicrosoft365analytics)

- **Telemetrieproxyserver:** Geben Sie den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) oder die IP-Adresse eines Proxyservers ein, um Anforderungen zu Benutzerservicequalität und Telemetrie im verbundenen Modus über eine SSL-Verbindung (Secure Sockets Layer) weiterzuleiten. Das Format dieser Einstellung lautet *Server*:*Port*. Wenn beim benannten Proxy ein Fehler auftritt oder kein Proxy angegeben wurde, werden die Daten zu Benutzererfahrung und Telemetrie im verbundenen Modus nicht gesendet. Sie verbleiben auf dem lokalen Gerät.

  Wenn Sie keinen Wert eingeben, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig sendet das Betriebssystem die Daten zu Benutzererfahrung und Telemetrie im verbundenen Modus möglicherweise unter Verwendung der Standardproxykonfiguration an Microsoft.

  Beispiele für das Format:

  ```
  IPv4: 192.246.246.106:100
  IPv6: [2001:4898:4010:4013:95c1:a8b2:953c:c633]:100
  FQDN: www.contoso.com:345
  ```

  [System/TelemetryProxy-CSP](/windows/client-management/mdm/policy-csp-system#system-telemetryproxy)

## <a name="search"></a>Suchen

Diese Einstellungen verwenden den [Suchrichtlinien-CSP](/windows/client-management/mdm/policy-csp-search), der auch die unterstützten Windows-Editionen auflistet.

- **SafeSearch (nur Mobilgeräte):** steuert, wie Cortana nicht jugendfreie Inhalte in den Suchergebnissen filtert. Folgende Optionen sind verfügbar:
  - **Benutzerdefiniert**: Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Es wird keine Einstellung erzwungen. Benutzer wählen ihre Einstellungen selbst aus.
  - **Streng**: Höchste Filterung jugendgefährdender Inhalte
  - **Mittel**: Mittlere Filterung nicht jugendfreier Inhalte. Gültige Suchergebnisse werden nicht gefiltert.
- **Display web results in search** (Webergebnisse in der Suche anzeigen): **Blockieren** verhindert, dass Benutzer Windows Search für die Internetsuche verwenden. Suchergebnisse aus dem Web werden nicht in Search angezeigt. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Benutzer im Web suchen, und die Ergebnisse werden auf dem Gerät angezeigt.
- **Diakritische Zeichen**: Mit **Blockieren** wird verhindert, dass diakritische Zeichen in Windows Search angezeigt werden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem zeigt diakritische Zeichen möglicherweise standardmäßig an.

  [Search/AllowUsingDiacritics-CSP](/windows/client-management/mdm/policy-csp-search#search-allowusingdiacritics)

- **Automatische Spracherkennung**: Mit **Blockieren** wird verhindert, dass die Sprache beim Indizieren von Inhalten oder Eigenschaften automatisch von Windows Search erkannt wird. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Es besteht die Möglichkeit, dass das Betriebssystem dieses Feature standardmäßig nicht zulässt.

  [Search/AlwaysUseAutoLangDetection-CSP](/windows/client-management/mdm/policy-csp-search#search-alwaysuseautolangdetection)

- **Standortsuche**: **Blockieren** verhindert, dass Windows Search den Standort verwendet. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Es besteht die Möglichkeit, dass das Betriebssystem dieses Feature standardmäßig nicht zulässt.

  [Search/AllowSearchToUseLocation-CSP](/windows/client-management/mdm/policy-csp-search#search-allowsearchtouselocation)

- **Backoff bei Indexerstellung**: Mit **Blockieren** wird die Suchfunktion „Backoff bei Indexerstellung“ deaktiviert. Die Indizierung wird auch dann mit voller Geschwindigkeit fortgesetzt, wenn die Systemaktivität hoch ist. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise verwendet das Betriebssystem standardmäßig Backofflogik, um die Indizierungsaktivität bei hoher Systemaktivität zu drosseln.

  [Search/DisableBackoff-CSP](/windows/client-management/mdm/policy-csp-search#search-disablebackoff)

- **Indizierung von Wechseldatenträgern**: Mit **Blockieren** wird verhindert, dass Speicherorte auf Wechseldatenträgern zu Bibliotheken hinzugefügt und indiziert werden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Es besteht die Möglichkeit, dass das Betriebssystem dieses Feature standardmäßig nicht zulässt.

  [Search/DisableRemovableDriveIndexing-CSP](/windows/client-management/mdm/policy-csp-search#search-disableremovabledriveindexing)

- **Indizierung bei geringem Speicherplatz**: Bei Auswahl von **Aktivieren** ist die automatische Indizierung auch dann möglich, wenn der Speicherplatz gering ist. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise deaktiviert das Betriebssystem standardmäßig die automatische Indizierung, wenn der Speicherplatz auf dem Datenträger 600 MB oder weniger beträgt. Wenn der Speicherplatz auf Geräten in Ihrer Organisation beschränkt ist, sollten Sie für diese Einstellung **Nicht konfiguriert** festlegen.

  [Search/PreventIndexingLowDiskSpaceMB-CSP](/windows/client-management/mdm/policy-csp-search#search-preventindexinglowdiskspacemb)

- **Remoteabfragen**: Bei Auswahl von **Aktivieren** sind Remoteabfragen für den Geräteindex zulässig. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem hindert Benutzer möglicherweise standardmäßig daran, Remoteabfragen für den Index des Geräts auszuführen.

  [Search/PreventRemoteQueries-CSP](/windows/client-management/mdm/policy-csp-search#search-preventremotequeries)

## <a name="start"></a>Starten

Diese Einstellungen verwenden den [Startrichtlinien-CSP](/windows/client-management/mdm/policy-csp-start), der auch die unterstützten Windows-Editionen auflistet.  

- **Startmenülayout:** Sie können eine XML-Datei hochladen, die Ihre Anpassungen einschließlich der Reihenfolge der aufgeführten Apps und vieles mehr enthält. Die XML-Datei setzt das standardmäßige Startlayout außer Kraft. Benutzer können das von Ihnen festgelegte Startmenülayout nicht ändern.

  Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

  [Start/StartLayout-CSP](/windows/client-management/mdm/policy-csp-start#start-startlayout)

- **Pin websites to tiles in Start menu** (Websites an Kacheln im Startmenü anheften): Import von Bildern aus Microsoft Edge. Diese Bilder werden im Windows-Startmenü von Desktopgeräten als Links angezeigt. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

  [Start/ImportEdgeAssets-CSP](/windows/client-management/mdm/policy-csp-start#start-importedgeassets)

- **Unpin apps from task bar** (Apps von der Taskleiste lösen): **Blockieren** verhindert, dass Benutzer Apps von der Taskleiste lösen können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise zu, dass Benutzer Apps von der Taskleiste lösen.

  [Start/NoPinningToTaskbar-CSP](/windows/client-management/mdm/policy-csp-start#start-nopinningtotaskbar)

- **Schneller Wechsel zwischen Benutzern:** **Blockieren** verhindert das Wechseln zwischen zwei gleichzeitig angemeldeten Benutzern ohne Abmeldung. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise zeigt das Betriebssystem standardmäßig auf der Benutzerkachel **Benutzer wechseln** an.

  [Start/HideSwitchAccount-CSP](/windows/client-management/mdm/policy-csp-start#start-hideswitchaccount)

- **Most used apps** (Meistverwendete Apps): **Blockieren** blendet die Anzeige der meistverwendeten Apps im Startmenü aus. Damit wird auch der entsprechende Schalter in der App „Einstellungen“ deaktiviert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig zeigt das Betriebssystem möglicherweise die am häufigsten verwendeten Apps an.

  [Start/HideFrequentlyUsedApps-CSP](/windows/client-management/mdm/policy-csp-start#start-hidefrequentlyusedapps)

- **Zuletzt hinzugefügte Apps:** **Blockieren** blendet die Anzeige der zuletzt hinzugefügten Apps im Startmenü aus. Damit wird auch der entsprechende Schalter in der App „Einstellungen“ deaktiviert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise zeigt das Betriebssystem standardmäßig die zuletzt hinzugefügten Apps im Startmenü an.

  [Start/HideRecentlyAddedApps-CSP](/windows/client-management/mdm/policy-csp-start#start-hiderecentlyaddedapps)

- **Startbildschirmmodus:** Wählen Sie die Größe des Startbildschirms aus. Folgende Optionen sind verfügbar:
  - **Benutzerdefiniert**: Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Es wird keine Einstellung erzwungen. Benutzer können die Größe festlegen.
  - **Vollbild:** Erzwingt das Vollbild des Startbildschirms.
  - **Kein Vollbild**: Erzwingt eine nicht auf Vollbild vergrößerte Darstellung des Startbildschirms.

  [Start/ForceStartSize-CSP](/windows/client-management/mdm/policy-csp-start#start-forcestartsize)

- **Recently opened items in Jump Lists** (Zuletzt geöffnete Elemente in Sprunglisten): **Blockieren** blendet die Anzeige zuletzt verwendeter Sprunglisten im Startmenü aus. Damit wird auch der entsprechende Schalter in der App „Einstellungen“ deaktiviert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise zeigt das Betriebssystem standardmäßig die zuletzt geöffneten Elemente in den Sprunglisten an.

  [Start/HideRecentJumplists-CSP](/windows/client-management/mdm/policy-csp-start#start-hiderecentjumplists)

- **App-Liste:** Wählen Sie aus, wie die App-Listen angezeigt werden. Folgende Optionen sind verfügbar:
  - **Benutzerdefiniert**: Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Es wird keine Einstellung erzwungen. Benutzer wählen aus, wie die App-Liste auf angezeigt wird.
  - **Reduzieren**: Blendet die Liste mit allen Apps aus.
  - **Die App „Einstellungen“ reduzieren und deaktivieren**: Blendet die Liste mit allen Apps aus und deaktiviert die Option **App-Liste im Startmenü anzeigen** in der App „Einstellungen“.
  - **Die App „Einstellungen“ entfernen und deaktivieren**: Blendet die Liste mit allen Apps aus, entfernt die Schaltfläche „Alle Apps“ und deaktiviert die Option **App-Liste in Startmenü anzeigen** in der App „Einstellungen“.

  [Start/HideAppList-CSP](/windows/client-management/mdm/policy-csp-start#start-hideapplist)

- **Netzschaltersymbol:** **Blockieren** blendet die Ein/Aus-Schaltfläche im Startmenü aus. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig zeigt das Betriebssystem die Ein/Aus-Schaltfläche möglicherweise an.

  [Start/HidePowerButton-CSP](/windows/client-management/mdm/policy-csp-start#start-hidepowerbutton)

- **Benutzerkachel:** **Blockieren** blendet die Benutzerkachel im Startmenü aus. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise zeigt das Betriebssystem die Benutzerkachel standardmäßig an. Konfigurieren Sie die folgenden Einstellungen:
  - **Sperren:** **Blockieren** blendet die Option **Sperren** auf der Benutzerkachel im Startmenü aus.  Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise zeigt das Betriebssystem standardmäßig die Option **Sperren** an.
  - **Abmelden:** **Blockieren** blendet die Option **Abmelden** auf der Benutzerkachel im Startmenü aus. **Nicht konfiguriert** (Standard) zeigt die Option **Abmelden** an.

  [Start/HideUserTile-CSP](/windows/client-management/mdm/policy-csp-start#start-hideusertile)

- **Herunterfahren:** **Blockieren** blendet die Optionen **Aktualisieren und herunterfahren** und **Herunterfahren** der Ein/Aus-Schaltfläche im Startmenü aus. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

  [Start/HideShutDown-CSP](/windows/client-management/mdm/policy-csp-start#start-hideshutdown)

- **Standbymodus:** **Blockieren** blendet die Option **Energie sparen** der Ein/Aus-Schaltfläche im Startmenü aus. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

  [Start/HideSleep-CSP](/windows/client-management/mdm/policy-csp-start#start-hidesleep)

- **Ruhezustand:** **Blockieren** blendet die Option **Ruhezustand** der Ein/Aus-Schaltfläche im Startmenü aus. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

  [Start/HideHibernate-CSP](/windows/client-management/mdm/policy-csp-start#start-hidehibernate)

- **Konto wechseln:** **Blockieren** blendet die Option **Konto wechseln** auf der Benutzerkachel im Startmenü aus. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

  [Start/HideSwitchAccount-CSP](/windows/client-management/mdm/policy-csp-start#start-hideswitchaccount)

- **Neustartoptionen:**  **Blockieren** blendet die Optionen **Aktualisieren und neu starten** und **Neu starten** der Ein/Aus-Schaltfläche im Startmenü aus. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

  [Start/HideRestart-CSP](/windows/client-management/mdm/policy-csp-start#start-hiderestart)

- **Documents on Start** (Dokumente im Startmenü): Blendet den Ordner „Dokumente“ im Windows-Startmenü aus oder ein. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Es wird keine Einstellung erzwungen. Benutzer können auswählen, ob die Verknüpfung ein- oder ausgeblendet werden soll.
  - **Ausblenden:** Die Verknüpfung wird ausgeblendet, und die Einstellung wird in der Einstellungen-App deaktiviert.
  - **Anzeigen:** Die Verknüpfung wird angezeigt, und die Einstellung wird in der Einstellungen-App deaktiviert.

  [Start/AllowPinnedFolderDocuments-CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderdocuments)

- **Downloads on Start** (Downloads im Startmenü): Blendet den Ordner „Downloads“ im Windows-Startmenü aus oder ein. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Es wird keine Einstellung erzwungen. Benutzer können auswählen, ob die Verknüpfung ein- oder ausgeblendet werden soll.
  - **Ausblenden:** Die Verknüpfung wird ausgeblendet, und die Einstellung wird in der Einstellungen-App deaktiviert.
  - **Anzeigen:** Die Verknüpfung wird angezeigt, und die Einstellung wird in der Einstellungen-App deaktiviert.

  [Start/AllowPinnedFolderDownloads-CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderdownloads)

- **File Explorer on Start** (Datei-Explorer im Startmenü): Blendet den Datei-Explorer im Windows-Startmenü aus oder ein. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Es wird keine Einstellung erzwungen. Benutzer können auswählen, ob die Verknüpfung ein- oder ausgeblendet werden soll.
  - **Ausblenden:** Die Verknüpfung wird ausgeblendet, und die Einstellung wird in der Einstellungen-App deaktiviert.
  - **Anzeigen:** Die Verknüpfung wird angezeigt, und die Einstellung wird in der Einstellungen-App deaktiviert.

  [Start/AllowPinnedFolderFileExplorer-CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderfileexplorer)

- **HomeGroup on Start** (Heimnetzgruppe im Startmenü): Blendet die Verknüpfung „Heimnetzgruppe“ im Windows-Startmenü aus oder ein. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Es wird keine Einstellung erzwungen. Benutzer können auswählen, ob die Verknüpfung ein- oder ausgeblendet werden soll.
  - **Ausblenden:** Die Verknüpfung wird ausgeblendet, und die Einstellung wird in der Einstellungen-App deaktiviert.
  - **Anzeigen:** Die Verknüpfung wird angezeigt, und die Einstellung wird in der Einstellungen-App deaktiviert.

  [Start/AllowPinnedFolderHomeGroup-CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderhomegroup)

- **Music on Start** (Musik im Startmenü): Blendet den Ordner „Musik“ im Windows-Startmenü aus oder ein. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Es wird keine Einstellung erzwungen. Benutzer können auswählen, ob die Verknüpfung ein- oder ausgeblendet werden soll.
  - **Ausblenden:** Die Verknüpfung wird ausgeblendet, und die Einstellung wird in der Einstellungen-App deaktiviert.
  - **Anzeigen:** Die Verknüpfung wird angezeigt, und die Einstellung wird in der Einstellungen-App deaktiviert.

  [Start/AllowPinnedFolderMusic-CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldermusic)

- **Network on Start** (Netzwerk im Startmenü): Blendet das Netzwerk im Windows-Startmenü aus oder ein. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Es wird keine Einstellung erzwungen. Benutzer können auswählen, ob die Verknüpfung ein- oder ausgeblendet werden soll.
  - **Ausblenden:** Die Verknüpfung wird ausgeblendet, und die Einstellung wird in der Einstellungen-App deaktiviert.
  - **Anzeigen:** Die Verknüpfung wird angezeigt, und die Einstellung wird in der Einstellungen-App deaktiviert.

  [Start/AllowPinnedFolderNetwork-CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldernetwork)

- **Personal folder on Start** (Persönlicher Ordner im Startmenü): Blendet den persönlichen Ordner im Windows-Startmenü aus oder ein. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Es wird keine Einstellung erzwungen. Benutzer können auswählen, ob die Verknüpfung ein- oder ausgeblendet werden soll.
  - **Ausblenden:** Die Verknüpfung wird ausgeblendet, und die Einstellung wird in der Einstellungen-App deaktiviert.
  - **Anzeigen:** Die Verknüpfung wird angezeigt, und die Einstellung wird in der Einstellungen-App deaktiviert.

  [Start/AllowPinnedFolderPersonalFolder-CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderpersonalfolder)

- **Pictures on Start** (Bilder im Startmenü): Blendet den Ordner für Bilder im Windows-Startmenü aus oder ein. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Es wird keine Einstellung erzwungen. Benutzer können auswählen, ob die Verknüpfung ein- oder ausgeblendet werden soll.
  - **Ausblenden:** Die Verknüpfung wird ausgeblendet, und die Einstellung wird in der Einstellungen-App deaktiviert.
  - **Anzeigen:** Die Verknüpfung wird angezeigt, und die Einstellung wird in der Einstellungen-App deaktiviert.

  [Start/AllowPinnedFolderPictures-CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfolderpictures)

- **Settings on Start** (Einstellungen im Startmenü): Blendet die Verknüpfung „Einstellungen“ im Windows-Startmenü aus oder ein. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Es wird keine Einstellung erzwungen. Benutzer können auswählen, ob die Verknüpfung ein- oder ausgeblendet werden soll.
  - **Ausblenden:** Die Verknüpfung wird ausgeblendet, und die Einstellung wird in der Einstellungen-App deaktiviert.
  - **Anzeigen:** Die Verknüpfung wird angezeigt, und die Einstellung wird in der Einstellungen-App deaktiviert.

  [Start/AllowPinnedFolderSettings-CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldersettings)

- **Videos on Start** (Videos im Startmenü): Blendet den Ordner für Videos im Windows-Startmenü aus oder ein. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Es wird keine Einstellung erzwungen. Benutzer können auswählen, ob die Verknüpfung ein- oder ausgeblendet werden soll.
  - **Ausblenden:** Die Verknüpfung wird ausgeblendet, und die Einstellung wird in der Einstellungen-App deaktiviert.
  - **Anzeigen:** Die Verknüpfung wird angezeigt, und die Einstellung wird in der Einstellungen-App deaktiviert.

  [Start/AllowPinnedFolderVideos-CSP](/windows/client-management/mdm/policy-csp-start#start-allowpinnedfoldervideos)

## <a name="microsoft-defender-smartscreen"></a>Microsoft Defender SmartScreen

- **SmartScreen für Microsoft Edge**: **Erforderlich** aktiviert Microsoft Defender SmartScreen und hindert Benutzer an der Deaktivierung dieses Features. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem aktiviert SmartScreen möglicherweise standardmäßig und gestattet Benutzern das Aktivieren/Deaktivieren dieses Features.

  Microsoft Edge verwendet Microsoft Defender SmartScreen (aktiviert), um Benutzer vor potenziellen Phishingangriffen und Schadsoftware zu schützen.

  [Browser/AllowSmartScreen-CSP](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

- **Zugriff auf schädliche Websites:** **Blockieren** hindert Benutzer daran, die Warnungen des Microsoft Defender SmartScreen-Filters zu ignorieren, und blockiert den Besuch der Website. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Benutzer die Warnungen ignorieren und die Website dennoch besuchen können.

  [Browser/PreventSmartScreenPromptOverride-CSP](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

- **Download nicht überprüfter Dateien:** **Blockieren** hindert Benutzer daran, Warnungen des Microsoft Defender SmartScreen-Filters zu ignorieren und nicht überprüfte Dateien herunterzuladen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Benutzer die Warnungen ignorieren und die nicht überprüften Dateien dennoch herunterladen können.

  [Browser/PreventSmartScreenPromptOverrideForFiles-CSP](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)

## <a name="windows-spotlight"></a>Windows-Blickpunkt

Diese Einstellungen verwenden den [Benutzeroberflächenrichtlinien-CSP](/windows/client-management/mdm/policy-csp-experience), der auch die unterstützten Windows-Editionen auflistet.

- **Windows-Blickpunkt:** **Blockieren** deaktiviert Windows-Blickpunkt auf dem Sperrbildschirm, Windows-Tipps, Microsoft-Features für Endbenutzer und weitere ähnliche Features. Wenn es Ihr Ziel ist, den Netzwerkdatenverkehr von Geräten zu minimieren, wählen Sie **Ja** aus. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig Windows-Blickpunkt-Funktionen zu, die von Benutzern gesteuert werden können.

  [Experience/AllowWindowsSpotlight-CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlight)

  Wenn diese Option auf **Nicht konfiguriert** festgelegt ist, können Sie auch die folgenden Einstellungen zulassen oder blockieren:

  - **Windows Spotlight on lock screen** (Windows-Blickpunkt auf dem Sperrbildschirm): **Blockieren** verhindert, dass Windows-Blickpunkt Informationen auf dem Sperrbildschirm des Geräts anzeigt. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise zeigt das Betriebssystem standardmäßig Windows-Blickpunkt-Informationen auf dem Sperrbildschirm an.

    [Experience/ConfigureWindowsSpotlightOnLockScreen-CSP](/windows/client-management/mdm/policy-csp-experience#experience-configurewindowsspotlightonlockscreen)

  - **Third-party suggestions in Windows Spotlight** (Drittanbietervorschläge in Windows-Blickpunkt): **Blockieren** verhindert, dass Windows-Blickpunkt Inhalte vorschlägt, die nicht von Microsoft stammen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig Partnervorschläge zu Apps und Inhalten zu und zeigt vorgeschlagene Apps im Startmenü sowie Windows-Tipps an.

    [Experience/AllowThirdPartySuggestionsInWindowsSpotlight-CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowthirdpartysuggestionsinwindowsspotlight)

  - **Endbenutzerfeatures:** **Blockieren** deaktiviert Funktionen, die normalerweise für Endbenutzer bestimmt sind, beispielsweise Startvorschläge, Mitgliedschaftsbenachrichtigungen, App-Installation nach Anzeige der Windows-Willkommensseite und Kachelumleitungen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

    [Experience/AllowWindowsConsumerFeatures-CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsconsumerfeatures)

  - **Windows-Tipps:** **Blockieren** deaktiviert Windows-Tipps in Popupfenstern. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig die Anzeige von Windows-Tipps zu.

    [Experience/AllowWindowsTips-CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowstips)

  - **Windows Spotlight in action center** (Windows-Blickpunkt im Info-Center): **Blockieren** verhindert, dass Benachrichtigungen von Windows-Blickpunkt im Info-Center angezeigt werden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise zeigt das Betriebssystem standardmäßig Benachrichtigungen im Info-Center an, die Apps oder Features vorschlagen, mit denen Benutzer unter Windows produktiver werden können.

    [Experience/AllowWindowsSpotlightOnActionCenter-CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlightonactioncenter)

  - **Personalisierung von Windows-Blickpunkt:** **Blockieren** verhindert, dass Windows Diagnosedaten verwendet, um angepasste Funktionen für Benutzer bereitzustellen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Microsoft Diagnosedaten verwendet, um personalisierte Empfehlungen, Tipps und Angebote bereitzustellen und Windows an die Anforderungen des Benutzers anpasst.

    [Experience/AllowTailoredExperiencesWithDiagnosticData-CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowtailoredexperienceswithdiagnosticdata)

  - **Windows-Begrüßungsseite:** **Blockieren** deaktiviert die Windows-Willkommensfunktion von Windows-Blickpunkt. Die Windows-Begrüßungsseite wird nicht angezeigt, wenn Updates und Änderungen an Windows und den zugehörigen Apps vorgenommen wurden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem die Windows-Begrüßungsseite standardmäßig zu, die Benutzern Informationen zu neuen oder aktualisierten Features anzeigt.

    [Experience/AllowWindowsSpotlightWindowsWelcomeExperience-CSP](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlightwindowswelcomeexperience)

## <a name="microsoft-defender-antivirus"></a>Microsoft Defender Antivirus

Diese Einstellungen verwenden den [Defender-Richtlinien-CSP](/windows/client-management/mdm/policy-csp-defender), der auch die unterstützten Windows-Editionen auflistet.

- **Real-time monitoring** (Echtzeitüberwachung): **Aktivieren** ermöglicht die Echtzeitüberprüfung auf Schadsoftware, Spyware und andere unerwünschte Software. Benutzer können diese Funktion nicht deaktivieren. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Dieses Feature wird standardmäßig vom Betriebssystem aktiviert, jedoch können Benutzer es ändern.

  Wenn Sie diese Einstellung aktivieren und anschließend wieder in **Nicht konfiguriert** ändern, behält Intune die Einstellung im zuvor konfigurierten Zustand bei.

  Dieses Feature wird nicht von Intune deaktiviert. Verwenden Sie einen benutzerdefinierten URI, um es zu deaktivieren.

  [Defender/AllowRealtimeMonitoring-CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

- **Verhaltensüberwachung:** **Aktivieren** schaltet auf Geräten die Verhaltensüberwachung ein und prüft auf bestimmte bekannte Muster verdächtiger Aktivitäten. Benutzer können die Verhaltensüberwachung nicht deaktivieren. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise aktiviert das Betriebssystem standardmäßig die Verhaltensüberwachung und lässt zu, dass Benutzer die Einstellung ändern.

  Wenn Sie die Einstellung aktivieren und anschließend wieder in **Nicht konfiguriert** ändern, behält Intune die Einstellung im zuvor konfigurierten Zustand bei.

  Dieses Feature wird nicht von Intune deaktiviert. Verwenden Sie einen benutzerdefinierten URI, um es zu deaktivieren.

  [Defender/AllowBehaviorMonitoring-CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowbehaviormonitoring)

- **Netzwerkinspektionssystem (NIS):** Das NIS trägt zum Schutz von Geräten vor netzwerkbasierten Exploits bei. Es verwendet die Signaturen bekannter Sicherheitsrisiken aus dem Microsoft Endpoint Protection Center, um schädlichen Datenverkehr zu erkennen und zu blockieren.

  - **Aktivieren**: Aktiviert den Netzwerkschutz und die Netzwerkblockierung. Benutzer können diese Funktion nicht deaktivieren. Wenn diese Option aktiviert ist, wird verhindert, dass Benutzer eine Verbindung mit bekannten Sicherheitsrisiken herstellen.

  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Das NIS (Netzwerkinspektionssystem) wird standardmäßig vom Betriebssystem aktiviert, jedoch können Benutzer diese Einstellung ändern.

  Wenn Sie die Einstellung aktivieren und anschließend wieder in **Nicht konfiguriert** ändern, behält Intune die Einstellung im zuvor konfigurierten Zustand bei.

  Dieses Feature wird nicht von Intune deaktiviert. Verwenden Sie einen benutzerdefinierten URI, um es zu deaktivieren.

  [Defender/EnableNetworkProtection-CSP](/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

- **Alle Downloads überprüfen:** Diese Einstellung wird über die Option **Aktivieren** aktiviert. Daraufhin überprüft Defender alle Dateien, die aus dem Internet heruntergeladen werden. Diese Einstellung kann von Benutzern nicht deaktiviert werden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise aktiviert das Betriebssystem diese Einstellung standardmäßig und lässt zu, dass Benutzer die Einstellung ändern.

  Wenn Sie die Einstellung aktivieren und anschließend wieder in **Nicht konfiguriert** ändern, behält Intune die Einstellung im zuvor konfigurierten Zustand bei.

  Dieses Feature wird nicht von Intune deaktiviert. Verwenden Sie einen benutzerdefinierten URI, um es zu deaktivieren.

  [Defender/AllowIOAVProtection-CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowioavprotection)

- **Scan scripts loaded in Microsoft web browsers** (In Microsoft-Webbrowsern geladene Skripts überprüfen): **Aktivieren** ermöglicht Defender die Überprüfung von Skripts, die in Internet Explorer verwendet werden. Diese Einstellung kann von Benutzern nicht deaktiviert werden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise aktiviert das Betriebssystem diese Einstellung standardmäßig und lässt zu, dass Benutzer die Einstellung ändern.

  Wenn Sie die Einstellung aktivieren und anschließend wieder in **Nicht konfiguriert** ändern, behält Intune die Einstellung im zuvor konfigurierten Zustand bei.

  Dieses Feature wird nicht von Intune deaktiviert. Verwenden Sie einen benutzerdefinierten URI, um es zu deaktivieren.

  [Defender/AllowScriptScanning-CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowscriptscanning)

- **End user access to Defender** (Endbenutzerzugriff auf Defender): **Blockieren** blendet die Benutzeroberfläche von Microsoft Defender für Benutzer aus. Alle Benachrichtigungen von Microsoft Defender werden ebenfalls unterdrückt. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Benutzer auf die Microsoft Defender-Benutzeroberfläche zugreifen und Einstellungen ändern.

  Wenn Sie die Einstellung blockieren und anschließend wieder in **Nicht konfiguriert** ändern, behält Intune die Einstellung im zuvor konfigurierten Zustand bei.

  Dieses Feature wird nicht von Intune deaktiviert. Verwenden Sie einen benutzerdefinierten URI, um es zu deaktivieren.

  Wird diese Einstellung geändert, wird die Änderung mit dem nächsten Neustart des Geräts wirksam.

  [Defender/AllowUserUIAccess-CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowuseruiaccess)

- **Intervall für Security Intelligence-Aktualisierung (in Stunden):** Mit dieser Einstellung geben Sie das Intervall an, zu dem Defender nach neuen Security Intelligence-Updates prüft. Werte von 0 bis 24 sind zulässig. Folgende Optionen sind verfügbar:

  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Gemäß der Standardeinstellung des Betriebssystems wird alle 8 Stunden nach Updates geprüft.
  - **Nicht überprüfen:** Bei dieser Einstellung prüft Defender nicht auf neue Security Intelligence-Updates.
  - **1 – 24**: `1` überprüft ein Mal pro Stunde, `2` überprüft alle zwei Stunden, `24` überprüft täglich und so weiter.
  
  [Defender/SignatureUpdateInterval-CSP](/windows/client-management/mdm/policy-csp-defender#defender-signatureupdateinterval)
  
- **Datei- und Programmaktivität überwachen:** Ermöglicht Defender die Überwachung der Datei- und Programmaktivität auf Geräten. Folgende Optionen sind verfügbar:

  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Gemäß der Standardeinstellung des Betriebssystems können alle Dateien überwacht werden.
  - **Überwachung deaktiviert**
  - **Alle Dateien überwachen**
  - **Nur eingehende Dateien überwachen**
  - **Nur ausgehende Dateien überwachen**

  [Defender/RealTimeScanDirection-CSP](/windows/client-management/mdm/policy-csp-defender#defender-realtimescandirection)

- **Days before deleting quarantined malware** (Tage bis zum Löschen von in Quarantäne befindlicher Schadsoftware): Ermöglicht die fortgesetzte Nachverfolgung behandelter Schadsoftware für die eingegebene Anzahl von Tagen, damit Sie zuvor betroffene Geräte manuell überprüfen können. 

  Wenn Sie diese Einstellung nicht konfigurieren oder auf `0` Tage festlegen, verbleibt Schadsoftware im Quarantäneordner und wird nicht automatisch entfernt. Bei Festlegung auf `90` werden Quarantäneelemente 90 Tage lang im System gespeichert und anschließend entfernt.

  [Defender/DaysToRetainCleanedMalware-CSP](/windows/client-management/mdm/policy-csp-defender#defender-daystoretaincleanedmalware)

- **CPU usage limit during a scan** (CPU-Auslastung während einer Überprüfung): Einschränken der CPU-Kapazität, die von Überprüfungen genutzt werden darf (von `0` bis `100` Prozent). Möglicherweise legt das Betriebssystem diesen Wert standardmäßig auf 50 % fest.
- **Archivdateien überprüfen:** Wenn **Aktivieren** festgelegt wird, wird Defender aktiviert, sodass Archivdateien wie ZIP- oder CAB-Dateien überprüft werden. Diese Einstellung kann von Benutzern nicht deaktiviert werden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise aktiviert das Betriebssystem diese Überprüfung standardmäßig und lässt zu, dass Benutzer die Einstellung ändern.

  Wenn Sie die Einstellung aktivieren und anschließend wieder in **Nicht konfiguriert** ändern, behält Intune die Einstellung im zuvor konfigurierten Zustand bei.

  Dieses Feature wird nicht von Intune deaktiviert. Verwenden Sie einen benutzerdefinierten URI, um es zu deaktivieren.

  [Defender/AllowArchiveScanning-CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowarchivescanning)

- **Eingehende E-Mail überprüfen:** Bei Auswahl von **Aktivieren** kann Defender E-Mail-Nachrichten beim Eingang auf dem Gerät überprüfen. Wenn diese Einstellung aktiviert ist, analysiert die Engine das Postfach und die E-Mail-Dateien, um den Text und die Anhänge der E-Mails zu überprüfen. Sie können die folgenden Dateiformate überprüfen: „.pst“ (Outlook), „.dbx“, „.mbx“, MIME (Outlook Express) und BinHex (Mac).

  Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Diese Überprüfung ist gemäß der Standardeinstellung des Betriebssystem deaktiviert, jedoch können Benutzer dies ändern.

  Wenn Sie die Einstellung aktivieren und anschließend wieder in **Nicht konfiguriert** ändern, behält Intune die Einstellung im zuvor konfigurierten Zustand bei.

  Dieses Feature wird nicht von Intune deaktiviert. Verwenden Sie einen benutzerdefinierten URI, um es zu deaktivieren.

  [Defender/AllowEmailScanning-CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowemailscanning)

- **Scan removable drives during a full scan** (Bei einer vollständigen Überprüfung Wechseldatenträger überprüfen): Wenn Sie diese Einstellung **aktivieren**, wird die Defender-Überprüfung von Wechseldatenträgern bei vollständigen Überprüfungen aktiviert. Diese Einstellung kann von Benutzern nicht deaktiviert werden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Defender Wechseldatenträger wie USB-Sticks überprüfen kann und Benutzer diese Einstellung ändern können.

  Wenn Sie die Einstellung aktivieren und anschließend wieder in **Nicht konfiguriert** ändern, behält Intune die Einstellung im zuvor konfigurierten Zustand bei.

  Wechseldatenträger können auch während einer Schnellüberprüfung überprüft werden.

  Dieses Feature wird nicht von Intune deaktiviert. Verwenden Sie einen benutzerdefinierten URI, um es zu deaktivieren.

  [Defender/AllowFullScanRemovableDriveScanning-CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanremovabledrivescanning)

- **Scan mapped network drives during a full scan** (Bei einer vollständigen Überprüfung zugeordnete Netzlaufwerke überprüfen): **Aktivieren** ermöglicht Defender das Überprüfen von Dateien auf zugeordneten Netzwerklaufwerken. Wenn die Dateien auf dem Laufwerk schreibgeschützt sind, kann Defender gefundene Schadsoftware nicht entfernen. Diese Einstellung kann von Benutzern nicht deaktiviert werden.

  Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Dieses Feature wird standardmäßig vom Betriebssystem aktiviert, jedoch können Benutzer es ändern.

  Wenn Sie die Einstellung aktivieren und anschließend wieder in **Nicht konfiguriert** ändern, behält Intune die Einstellung im zuvor konfigurierten Zustand bei. 

  Zugeordnete Netzwerklaufwerke können auch während einer Schnellüberprüfung überprüft werden.

  Dieses Feature wird nicht von Intune deaktiviert. Verwenden Sie einen benutzerdefinierten URI, um es zu deaktivieren.

  [Defender/AllowFullScanOnMappedNetworkDrives-CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanonmappednetworkdrives)

- **Scan files opened from network folders** (Über Netzwerkordner geöffnete Dateien überprüfen): Wenn Sie diese Einstellung **aktivieren**, überprüft Defender Dateien, die über Netzwerkordner oder freigegebene Netzwerklaufwerke geöffnet wurden, z. B. Dateien, auf die über einen UNC-Pfad zugegriffen wird. Diese Einstellung kann von Benutzern nicht deaktiviert werden. Wenn die Dateien auf dem Laufwerk schreibgeschützt sind, kann Defender gefundene Schadsoftware nicht entfernen.

  Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig überprüft das Betriebssystem Dateien, die über Netzwerkordner geöffnet wurden, und erlaubt Benutzern das Ändern dieser Einstellung.

  Wenn Sie die Einstellung aktivieren und anschließend wieder in **Nicht konfiguriert** ändern, behält Intune die Einstellung im zuvor konfigurierten Zustand bei.

  Dieses Feature wird nicht von Intune deaktiviert. Verwenden Sie einen benutzerdefinierten URI, um es zu deaktivieren.

  [Defender/AllowScanningNetworkFiles-CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowscanningnetworkfiles)

- **Cloudschutz:** **Aktivieren** lässt den Empfang von Informationen über Schadsoftwareaktivitäten der von Ihnen verwalteten Geräte durch Microsoft Active Protection Service zu. Benutzer können diese Einstellung nicht ändern. 

  Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem lässt standardmäßig zu, dass Microsoft Active Protection Service Informationen abruft und dass Benutzer diese Einstellung ändern können.

  Wenn Sie die Einstellung aktivieren und anschließend wieder in **Nicht konfiguriert** ändern, behält Intune die Einstellung im zuvor konfigurierten Zustand bei.

  Dieses Feature wird nicht von Intune deaktiviert. Verwenden Sie einen benutzerdefinierten URI, um es zu deaktivieren.

  [Defender/AllowCloudProtection-CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

- **Prompt users before sample submission** (Vor dem Senden von Beispielen bei Benutzern nachfragen): steuert, ob potenziell schädliche Dateien, die möglicherweise genauer analysiert werden müssen, automatisch an Microsoft gesendet werden. Folgende Optionen sind verfügbar:

  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Das Betriebssystem kann standardmäßig sichere Beispiele automatisch senden.
  - **Immer bestätigen**
  - **Vor dem Senden persönlicher Daten nachfragen**
  - **Nie Daten senden**
  - **Alle Daten ohne Nachfrage senden**: Die Daten werden automatisch gesendet.

  [Defender/SubmitSamplesConsent-CSP](/windows/client-management/mdm/policy-csp-defender#defender-submitsamplesconsent)

- **Time to perform a daily quick scan** (Uhrzeit für die Durchführung einer täglichen Schnellüberprüfung): Wählen Sie die Stunde aus, zu der eine tägliche Schnellüberprüfung ausgeführt werden soll. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise führt das Betriebssystem diese Überprüfung standardmäßig um 2:00 Uhr durch.

  Wenn Sie eine weitere Anpassung wünschen, konfigurieren Sie die Einstellung **Art der durchzuführenden Systemüberprüfung**.

  [Defender/ScheduleQuickScanTime (CSP)](/windows/client-management/mdm/policy-csp-defender#defender-schedulequickscantime)

- **Type of system scan to perform** (Art der durchzuführenden Systemüberprüfung): Planen Sie eine Systemüberprüfung, einschließlich des Grads der Überprüfung, sowie Tag und Uhrzeit der Ausführung der Überprüfung. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert:** Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Es wird keine Einstellung erzwungen. Benutzer können Überprüfungen nach Bedarf manuell auf ihren Geräten durchführen.
  - **Deaktivieren:** Deaktiviert die Systemüberprüfung auf Geräten. Wählen Sie diese Option, wenn Sie eine Antivirenlösung eines Partners verwenden, die Geräte überprüft.
  - **Schnellüberprüfung**: Dient zum Überprüfen gängiger Speicherorte, an denen Schadsoftware registriert sein kann (z. B. Registrierungsschlüssel und bekannte Windows-Startordner).
    - **Geplanter Tag**: Wählen Sie den Tag der Ausführung der Überprüfung aus.
    - **Geplante Zeit**: Wählen Sie die Stunde der Ausführung der Überprüfung aus.
  - **Vollständige Überprüfung**: Dient zum Überprüfen gängiger Speicherorte, an denen Schadsoftware registriert sein kann sowie aller Dateien und Ordner auf dem Gerät.
    - **Geplanter Tag**: Wählen Sie den Tag der Ausführung der Überprüfung aus.
    - **Geplante Zeit**: Wählen Sie die Stunde der Ausführung der Überprüfung aus.

  > [!TIP]
  > Diese Einstellung steht ggf. in Konflikt mit der Einstellung **Uhrzeit für die Durchführung einer täglichen Schnellüberprüfung**. Empfehlungen:  
  >
  > - Gehen Sie folgendermaßen vor, wenn Sie eine tägliche Schnellüberprüfung planen möchten:
  >   1. Konfigurieren Sie die Einstellung **Uhrzeit für die Durchführung einer täglichen Schnellüberprüfung**.
  >   2. Konfigurieren Sie eine vollständige Überprüfung für die Einstellung **Art der durchzuführenden Systemüberprüfung**.
  > 
  > - Wenn Sie nur eine Schnellüberprüfung am Tag möchten, d. h. keine vollständige Überprüfung, dann wählen Sie eine der beiden Einstellungen aus: **Uhrzeit für die Durchführung einer täglichen Schnellüberprüfung** oder **Art der durchzuführenden Systemüberprüfung** Um beispielsweise jeden Dienstag um 6 Uhr eine Schnellüberprüfung durchzuführen, konfigurieren Sie die Einstellung **Art der durchzuführenden Systemüberprüfung**.
  > 
  > - Konfigurieren Sie **Uhrzeit für die Durchführung einer täglichen Schnellüberprüfung** nicht parallel mit auf **Schnellüberprüfung** festgelegter Einstellung **Art der durchzuführenden Systemüberprüfung**. Diese Einstellungen können in Konflikt stehen und eine Überprüfung möglicherweise verhindern.

  [CSP: Defender/ScanParameter](/windows/client-management/mdm/policy-csp-defender#defender-scanparameter)  
  [CSP: Defender/ScheduleScanDay](/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday)  
  [CSP: Defender/ScheduleScanTime](/windows/client-management/mdm/policy-csp-defender#defender-schedulescantime)

- **Möglichweise unerwünschte Software erkennen:** Mit dieser Funktion werden potenziell unerwünschte Anwendungen ermittelt und blockiert, sodass diese Anwendungen in Ihrem Netzwerk nicht heruntergeladen und installiert werden können. Diese Anwendungen werden nicht als Viren, Schadsoftware oder andere Arten von Bedrohungen betrachtet. Sie können jedoch Aktionen auf Endpunkten ausführen, die deren Leistung oder Verwendung beeinträchtigen. Wählen Sie die gewünschte Schutzebene aus, wenn Windows potenziell unerwünschte Anwendungen erkennt. Folgende Optionen sind verfügbar:

  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Möglicherweise wird diese Funktion standardmäßig von Microsoft Defender deaktiviert.
  - **Off**: Der PUA-Schutz ist deaktiviert.
  - **Aktivieren**: Microsoft Defender erkennt potenziell unerwünschte Anwendungen, und erkannte Elemente werden blockiert. Diese Elemente werden Im Verlauf zusammen mit anderen Bedrohungen angezeigt.
  - **Überwachung**: Microsoft Defender erkennt potenziell unerwünschte Anwendungen, führt jedoch keine Aktion aus. Sie können Informationen zu den Anwendungen überprüfen, gegen die Microsoft Defender Maßnahmen einleiten würde. Suchen Sie z. B. in der Ereignisanzeige nach durch Microsoft Defender erstellten Ereignissen.

  Weitere Informationen zu potenziell unerwünschten Apps finden Sie unter [Erkennen und Blockieren möglicherweise unerwünschter Anwendungen](/windows/security/threat-protection/microsoft-defender-antivirus/detect-block-potentially-unwanted-apps-microsoft-defender-antivirus).

  [Defender/PUAProtection-CSP](/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

- **Zustimmung für Stichproben senden:** Diese Einstellung hat derzeit keine Auswirkungen. Verwenden Sie diese Einstellung nicht. Möglicherweise wird sie in einem zukünftigen Release entfernt.

- **Zugriffsschutz:** Die Option **Blockieren** verhindert das Scannen von Dateien, auf die zugegriffen wurde oder die heruntergeladen wurden. Benutzer können diese Funktion nicht aktivieren. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise wird diese Funktion standardmäßig vom Betriebssystem aktiviert, und Benutzer können sie ändern.

  Wenn Sie die Einstellung blockieren und anschließend wieder in **Nicht konfiguriert** ändern, behält Intune die Einstellung im zuvor vom Betriebssystem konfigurierten Zustand bei.

  Diese Funktion wird nicht von Intune aktiviert. Verwenden Sie einen benutzerdefinierten URI, um sie zu aktivieren.

  [Defender/AllowOnAccessProtection-CSP](/windows/client-management/mdm/policy-csp-defender#defender-allowonaccessprotection)

- **Actions on detected malware threats** (Aktionen für erkannte Schadsoftwarebedrohungen): Legen Sie für diese Einstellung **Aktivieren** fest, um die Aktionen auszuwählen, die Defender bei den einzelnen erkannten Bedrohungsstufen („Niedrig“, „Mittel“, „Hoch“ und „Schwerwiegend“) ergreifen soll. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Microsoft Defender die am besten geeignete Option auswählt.

  Wenn Sie für diese Einstellung **Aktivieren** festlegen, wählen Sie die Aktion aus:
  
  - **Bereinigen**
  - **Quarantäne**
  - **Entfernen**
  - **Zulassen**
  - **Benutzerdefiniert**
  - **Blockieren**

  Wenn Ihre Aktion nicht möglich ist, wird die beste Option von Microsoft Defender ausgewählt, um sicherzustellen, dass die Bedrohung entschärft wird.

  [Defender/ThreatSeverityDefaultAction-CSP](/windows/client-management/mdm/policy-csp-defender#defender-threatseveritydefaultaction)

### <a name="microsoft-defender-antivirus-exclusions"></a>Microsoft Defender Antivirus-Ausschlüsse

Sie können bestimmte Dateien aus Microsoft Defender Antivirus-Scans ausschließen, indem Sie Ausschlusslisten bearbeiten. **Im Allgemeinen sollten Sie keine Ausschlüsse anwenden**. Microsoft Defender Antivirus umfasst eine Reihe von automatischen Ausschlüssen, die auf bekannten Betriebssystemverhalten und typischen Verwaltungsdateien basieren, wie z. B. solchen, die in der Unternehmensverwaltung, Datenbankverwaltung und anderen Unternehmensszenarien und -situationen verwendet werden.

> [!WARNING]
> **Durch das Definieren von Ausschlüsse wird der von Microsoft Defender Antivirus angebotene Schutz gesenkt**. Bewerten Sie immer die Risiken, die mit der Implementierung von Ausschlüssen einhergehen. Schließen Sie nur Dateien aus, von denen Sie wissen, dass sie nicht schädlich sind.

- **Files and folders to exclude from scans and real-time protection** (Dateien und Ordner, die bei Überprüfungen und Echtzeitschutz ausgeschlossen werden sollen): Fügt Dateien und Ordner wie **C:\Pfad** oder **%ProgramFiles%\Pfad\Dateiname.exe** der Ausschlussliste hinzu. Diese Dateien und Ordner werden in Echtzeitüberprüfungen oder geplanten Überprüfungen nicht berücksichtigt.
- **File extensions to exclude from scans and real-time protection** (Dateierweiterungen, die bei Überprüfungen und Echtzeitschutz ausgeschlossen werden sollen): Fügen Sie Dateierweiterungen wie **JPG** oder **TXT** der Ausschlussliste hinzu. Dateien mit diesen Erweiterungen werden nicht in Echtzeitüberprüfungen oder geplante Überprüfungen einbezogen.
- **Processes to exclude from scans and real-time protection** (Prozesse, die bei Überprüfungen und Echtzeitschutz ausgeschlossen werden sollen): Fügen Sie Prozesse des Typs **.exe**, **.com** oder **.scr** der Ausschlussliste hinzu. Diese Prozesse werden nicht in Echtzeitüberprüfungen oder geplante Überprüfungen einbezogen.

## <a name="power-settings"></a>Energieeinstellungen

Diese Einstellungen verwenden den [Energierichtlinien-CSP](/windows/client-management/mdm/policy-csp-power), der auch die unterstützten Windows-Editionen auflistet.

### <a name="battery"></a>Akku

- **Akkustand zum Aktivieren des Energiesparmodus:** Wenn sich das Gerät im Akkubetrieb befindet, können Sie mit dieser Einstellung den Akkustand von 0 bis 100 festlegen, ab dem der Energiesparmodus aktiviert wird. Geben Sie einen Prozentwert ein, der den Akkustand angibt. Wenn beispielsweise `80` festgelegt wird, wird der Energiesparmodus aktiviert, sobald der Akkustand 80 % oder weniger erreicht.

  Wenn Sie keinen Wert eingeben, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise legt das Betriebssystem diesen Wert standardmäßig auf 70 % fest.

  [Power/EnergySaverBatteryThresholdOnBattery-CSP](/windows/client-management/mdm/policy-csp-power#power-energysaverbatterythresholdonbattery)

- **Deckel schließen (nur Mobilgerät):** Diese Einstellung gibt an, was geschieht, wenn ein Gerät im Akkubetrieb zugeklappt wird. Folgende Optionen sind verfügbar:

  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Benutzer diese Einstellung festlegen können.
  - **Keine Aktion:** Bei dieser Einstellung bleibt das Gerät eingeschaltet und nutzt weiterhin Akkuleistung.
  - **Standbymodus:** Das Gerät wird in den Energiesparmodus versetzt und nutzt nur eine geringe Menge des Akkustands. Der Computer ist weiterhin eingeschaltet, und geöffnete Apps und Dateien werden im Arbeitsspeicher gespeichert.
  - **Ruhezustand:** Bei dieser Einstellung wird das Gerät in den Ruhezustand versetzt. Geöffnete Apps und Dateien werden auf dem Datenträger gespeichert, und das Gerät wird ausgeschaltet.
  - **Herunterfahren:** Bei dieser Einstellung wird das Gerät heruntergefahren. Geöffnete Apps und Dateien werden ohne Speichern geschlossen.

  [Power/SelectLidCloseActionOnBattery-CSP](/windows/client-management/mdm/policy-csp-power#power-selectlidcloseactiononbattery)

- **Netzschaltersymbol:** Wenn sich das Gerät im Akkubetrieb befindet, können Sie auswählen, was geschieht, wenn der Netzschalter betätigt wird. Folgende Optionen sind verfügbar:

  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Benutzer diese Einstellung festlegen können.
  - **Keine Aktion:** Bei dieser Einstellung bleibt das Gerät eingeschaltet und nutzt weiterhin Akkuleistung.
  - **Standbymodus:** Das Gerät wird in den Energiesparmodus versetzt und nutzt nur eine geringe Menge des Akkustands. Der Computer ist weiterhin eingeschaltet, und geöffnete Apps und Dateien werden im Arbeitsspeicher gespeichert.
  - **Ruhezustand:** Bei dieser Einstellung wird das Gerät in den Ruhezustand versetzt. Geöffnete Apps und Dateien werden auf dem Datenträger gespeichert, und das Gerät wird ausgeschaltet.
  - **Herunterfahren:** Bei dieser Einstellung wird das Gerät heruntergefahren. Geöffnete Apps und Dateien werden ohne Speichern geschlossen.

  [Power/SelectPowerButtonActionOnBattery-CSP](/windows/client-management/mdm/policy-csp-power#power-selectpowerbuttonactiononbattery)

- **Standbytaste**: Wenn sich das Gerät im Akkubetrieb befindet, können Sie auswählen, was geschieht, wenn die Schaltfläche „Standby“ betätigt wird. Folgende Optionen sind verfügbar:

  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Benutzer diese Einstellung festlegen können.
  - **Keine Aktion:** Bei dieser Einstellung bleibt das Gerät eingeschaltet und nutzt weiterhin Akkuleistung.
  - **Standbymodus:** Das Gerät wird in den Standbymodus versetzt und nutzt nur eine geringe Menge des Akkustands. Der Computer ist weiterhin eingeschaltet, und geöffnete Apps und Dateien werden im Arbeitsspeicher gespeichert.
  - **Ruhezustand:** Bei dieser Einstellung wird das Gerät in den Ruhezustand versetzt. Geöffnete Apps und Dateien werden auf dem Datenträger gespeichert, und das Gerät wird ausgeschaltet.
  - **Herunterfahren:** Bei dieser Einstellung wird das Gerät heruntergefahren. Geöffnete Apps und Dateien werden ohne Speichern geschlossen.

  [Power/SelectSleepButtonActionOnBattery-CSP](/windows/client-management/mdm/policy-csp-power#power-selectsleepbuttonactiononbattery)

- **Hybrider Standbymodus:** Aktivieren oder deaktivieren Sie den hybriden Standbymodus, wenn sich das Gerät im Akkubetrieb befindet.

  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Benutzer diese Einstellung festlegen können.
  - **Aktivieren**: Geräte können in den hybriden Standbymodus wechseln. Geöffnete Apps und Dateien werden im RAM und auf dem Datenträger gespeichert. Dabei wird nur eine kleine Menge des Akkustands verwendet.
  - **Deaktivieren:** Verhindert, dass Geräte in den hybriden Standbymodus wechseln.

  [Power/TurnOffHybridSleepOnBattery-CSP](/windows/client-management/mdm/policy-csp-power#power-turnoffhybridsleeponbattery)

### <a name="pluggedin"></a>PluggedIn

- **Akkustand zum Aktivieren des Energiesparmodus:** Wenn sich das Gerät im Netzbetrieb befindet, können Sie mit dieser Einstellung den Akkustand von 0 bis 100 festlegen, ab dem der Energiesparmodus aktiviert wird. Geben Sie einen Prozentwert ein, der den Akkustand angibt. Wenn beispielsweise `80` festgelegt wird, wird der Energiesparmodus aktiviert, sobald der Akkustand 80 % oder weniger erreicht.

  Wenn Sie keinen Wert eingeben, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Möglicherweise legt das Betriebssystem diesen Wert standardmäßig auf 70 % fest.

  [Power/EnergySaverBatteryThresholdPluggedIn-CSP](/windows/client-management/mdm/policy-csp-power#power-energysaverbatterythresholdpluggedin)

- **Deckel schließen (nur Mobilgerät):** Diese Einstellung gibt an, was geschieht, wenn ein Gerät zugeklappt wird, das sich im Netzbetrieb befindet. Folgende Optionen sind verfügbar:

  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
  - **Keine Aktion:** Das Gerät bleibt eingeschaltet.
  - **Standbymodus:** Das Gerät wird in den Standbymodus versetzt. Der Computer ist weiterhin eingeschaltet, und geöffnete Apps und Dateien werden im Arbeitsspeicher gespeichert.
  - **Ruhezustand:** Bei dieser Einstellung wird das Gerät in den Ruhezustand versetzt. Geöffnete Apps und Dateien werden auf dem Datenträger gespeichert, und das Gerät wird ausgeschaltet.
  - **Herunterfahren:** Bei dieser Einstellung wird das Gerät heruntergefahren. Geöffnete Apps und Dateien werden ohne Speichern geschlossen.
  
    [Power/SelectLidCloseActionPluggedIn-CSP](/windows/client-management/mdm/policy-csp-power#power-selectlidcloseactionpluggedin)
  
- **Netzschaltersymbol:** Wenn sich das Gerät im Netzbetrieb befindet, können Sie auswählen, was geschieht, wenn der Netzschalter betätigt wird. Folgende Optionen sind verfügbar:

  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
  - **Keine Aktion:** Das Gerät bleibt eingeschaltet.
  - **Standbymodus:** Das Gerät wird in den Standbymodus versetzt. Der Computer ist weiterhin eingeschaltet, und geöffnete Apps und Dateien werden im Arbeitsspeicher gespeichert.
  - **Ruhezustand:** Bei dieser Einstellung wird das Gerät in den Ruhezustand versetzt. Geöffnete Apps und Dateien werden auf dem Datenträger gespeichert, und das Gerät wird ausgeschaltet.
  - **Herunterfahren:** Bei dieser Einstellung wird das Gerät heruntergefahren. Geöffnete Apps und Dateien werden ohne Speichern geschlossen.

  [Power/SelectPowerButtonActionPluggedIn-CSP](/windows/client-management/mdm/policy-csp-power#power-selectpowerbuttonactionpluggedin)

- **Standbytaste**: Wenn sich das Gerät im Netzbetrieb befindet, können Sie auswählen, was geschieht, wenn die Schaltfläche „Standby“ betätigt wird. Folgende Optionen sind verfügbar:

  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
  - **Keine Aktion:** Das Gerät bleibt eingeschaltet.
  - **Standbymodus:** Das Gerät wird in den Standbymodus versetzt. Der Computer ist weiterhin eingeschaltet, und geöffnete Apps und Dateien werden im Arbeitsspeicher gespeichert.
  - **Ruhezustand:** Bei dieser Einstellung wird das Gerät in den Ruhezustand versetzt. Geöffnete Apps und Dateien werden auf dem Datenträger gespeichert, und das Gerät wird ausgeschaltet.
  - **Herunterfahren:** Bei dieser Einstellung wird das Gerät heruntergefahren. Geöffnete Apps und Dateien werden ohne Speichern geschlossen.

  [Power/SelectSleepButtonActionPluggedIn-CSP](/windows/client-management/mdm/policy-csp-power#power-selectsleepbuttonactionpluggedin)

- **Hybrider Standbymodus:** Aktivieren oder deaktivieren Sie den hybriden Standbymodus, wenn das Gerät mit dem Stromnetz verbunden ist.

  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert. Möglicherweise lässt das Betriebssystem standardmäßig zu, dass Benutzer diese Einstellung festlegen können.
  - **Aktivieren**: Geräte können in den hybriden Standbymodus wechseln. Geöffnete Apps und Dateien werden im RAM und auf dem Datenträger gespeichert.
  - **Deaktivieren:** Verhindert, dass Geräte in den hybriden Standbymodus wechseln.

  [Power/TurnOffHybridSleepPluggedIn-CSP](/windows/client-management/mdm/policy-csp-power#power-turnoffhybridsleeppluggedin)

## <a name="next-steps"></a>Nächste Schritte

Weitere technische Details zu den einzelnen Einstellungen und den unterstützten Windows-Editionen finden Sie in der Referenz zum [Richtlinien-Konfigurationsdienstanbieter für Windows 10](/windows/client-management/mdm/policy-configuration-service-provider).

[Weisen Sie das Profil zu](device-profile-assign.md), und [überwachen Sie dessen Status](device-profile-monitor.md).