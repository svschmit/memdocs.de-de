---
title: Konfigurieren von VPN-Einstellungen für Windows 8.1-Geräte in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Fügen Sie ein VPN-Konfigurationsprofil hinzu, oder erstellen Sie ein solches Profil mithilfe der VPN-Konfigurationseinstellungen (Virtual Private Network), einschließlich der Verbindungsdetails und der Proxyeinstellungen, die die IP- oder FQDN-Adresse und den TCP-Port enthalten müssen, in Microsoft Intune auf Geräten mit Windows 8.1.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f0f242f336fadf9dd31641849462a5dd24c09e3f
ms.sourcegitcommit: 169e279ba686c28d9a23bc0a54f0a2a0d20bdee4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/19/2020
ms.locfileid: "83556352"
---
# <a name="add-vpn-settings-on-windows-81-devices-in-microsoft-intune"></a>Hinzufügen von VPN-Einstellungen für Windows 8.1-Geräte in Microsoft Intune

In diesem Artikel werden die Intune-Einstellungen veranschaulicht, die Sie verwenden können, um VPN-Verbindungen auf Windows 8.1-Geräten zu konfigurieren.

Je nach den ausgewählten Einstellungen können nicht alle Werte in der folgenden Liste konfiguriert werden.

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen Sie ein Windows 8.1-VPN-Gerätekonfigurationsprofil](vpn-settings-configure.md).

## <a name="base-vpn-settings"></a>Grundlegende VPN-Einstellungen

- **Verbindungsname:** Geben Sie einen Namen für diese Verbindung ein. Benutzern wird dieser Name angezeigt, wenn sie auf ihrem Gerät die Liste der verfügbaren VPN-Verbindungen durchsuchen. Geben Sie beispielsweise `Contoso VPN` ein.
- **Server:** Fügen Sie mindestens einen VPN-Server hinzu, mit dem Geräte eine Verbindung herstellen können. Wenn Sie einen Server hinzufügen, geben Sie folgende Informationen ein:
  - **Beschreibung:** Geben Sie einen beschreibenden Namen für den Server ein, z. B. **Contoso-VPN-Server**.
  - **IP-Adresse oder FQDN:** Geben Sie die IP-Adresse oder den vollqualifizierten Domänennamen (FQDN) des VPN-Servers ein, mit dem Geräte eine Verbindung herstellen. Geben Sie beispielsweise `192.168.1.1` oder `vpn.contoso.com` ein.
  - **Standardserver:** **TRUE** legt diesen Server als Standardserver fest, über den Geräte eine Verbindung herstellen. Legen Sie nur einen Server als Standard fest.
  - **Importieren:** Suchen Sie nach einer Datei, die eine durch Trennzeichen getrennte Liste von Servern im Format „Beschreibung, IP-Adresse oder FQDN, Standardserver“ enthält. Wählen Sie **OK** aus, um diese Server in die Liste **Server** zu importieren.
  - **Exportieren:** Exportiert die Liste der Server in eine CSV-Datei (Comma-Separated Values, durch Trennzeichen getrennte Werte).

- **Verbindungstyp:** Wählen Sie den VPN-Verbindungstyp aus. Folgende Optionen sind verfügbar:
  - **Check Point Capsule VPN**
  - **SonicWall Mobile Connect**
  - **F5 Edge Client**
  - **Pulse Secure**

<!--- **Fingerprint** (Check Point Capsule VPN only): Specify a string (for example, "Contoso Fingerprint Code") that will be used to verify that the VPN server can be trusted. A fingerprint can be sent to the client so it knows to trust any server that presents the same fingerprint when connecting. If the device doesn't already have the fingerprint, it will prompt the user to trust the VPN server that they are connecting to while showing the fingerprint. (The user manually verifies the fingerprint and chooses **trust** to connect.) --->

- **Anmeldegruppe oder -domäne** (nur SonicWall Mobile Connect): Geben Sie den Namen der Anmeldegruppe oder Domäne ein, mit der Sie eine Verbindung herstellen möchten.

- **Rolle** (nur Pulse Secure): Geben Sie den Namen der Benutzerrolle ein, die auf diese Verbindung zugreifen kann. Eine Benutzerrolle definiert persönliche Einstellungen und Optionen und aktiviert oder deaktiviert bestimmte Zugriffsfeatures.

- **Bereich** (nur Pulse Secure): Geben Sie den Namen des gewünschten Authentifizierungsbereichs ein. Ein Authentifizierungsbereich ist eine Gruppe von Authentifizierungsressourcen, die vom Verbindungstyp „Pulse Secure“ verwendet werden.

- **Benutzerdefiniertes XML:** Geben Sie benutzerdefinierte XML-Befehle zum Konfigurieren der VPN-Verbindung an.

  **Pulse Secure-Beispiel**:

  ```xml
  <pulse-schema><isSingleSignOnCredential>true</isSingleSignOnCredential></pulse-schema>
  ```

  **CheckPoint Mobile VPN-Beispiel**:

  ```xml
  <CheckPointVPN port="443" name="CheckPointSelfhost" sso="true" debug="3" />
  ```

  **SonicWall Mobile Connect-Beispiel**:

  ```xml
  <MobileConnect><Compression>false</Compression><debugLogging>True</debugLogging><packetCapture>False</packetCapture></MobileConnect>
  ```

  **F5 Edge Client-Beispiel**:

  ```xml
  <f5-vpn-conf><single-sign-on-credential /></f5-vpn-conf>
  ```

  Weitere Informationen zum Erstellen von benutzerdefinierten XML-Befehlen finden Sie in der VPN-Dokumentation des Herstellers.

- **Getrenntes Tunneln:** Wählen Sie **Aktivieren** für diese Option aus, damit die Geräte anhand des Datenverkehrs selbst entscheiden können, welche Verbindung verwendet werden soll. Beispiel: Ein Benutzer in einem Hotel verwendet die VPN-Verbindung zum Zugreifen auf Arbeitsdateien, jedoch das Standardnetzwerk des Hotels für normales Webbrowsen. Legen Sie **Deaktivieren** fest, um zu erzwingen, dass der gesamte Datenverkehr den VPN-Tunnel durchläuft, wenn die VPN-Verbindung aktiv ist.

## <a name="proxy-settings"></a>Proxyeinstellungen

- **Automatisches Konfigurationsskript:** Verwenden Sie eine Datei, um den Proxyserver zu konfigurieren. Geben Sie die **Proxyserver-URL** ein, die die Konfigurationsdatei enthält. Geben Sie beispielsweise `http://proxy.contoso.com` ein.
- **Adresse**: Geben Sie die Adresse des Proxyservers ein, z. B. eine IP-Adresse oder `vpn.contoso.com`.
- **Portnummer:** Geben Sie die von Ihrem Proxyserver verwendete TCP-Portnummer ein.
- **Proxyeinstellungen automatisch erkennen:** Wenn der VPN-Server einen Proxyserver für die Verbindung erfordert, wenn Sie aus, ob Geräte die Verbindungseinstellungen automatisch erkennen können sollen. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
  - **Aktivieren**: Erkennt automatisch die Verbindungseinstellungen.
  - **Deaktivieren:** Die Verbindungseinstellungen werden nicht automatisch erkannt.
- **Proxy für lokale Adressen umgehen:** Verwendet den Proxyserver für lokale Adressen. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
  - **Aktivieren**: Verwendet keinen Proxyserver für lokale Adressen.
  - **Deaktivieren:** Verwendet einen Proxyserver für lokale Adressen.

## <a name="next-steps"></a>Nächste Schritte

[Weisen Sie das Profil zu](device-profile-assign.md), und [überwachen Sie dessen Status](device-profile-monitor.md).

Konfigurieren Sie VPN-Einstellungen für [Android-](vpn-settings-android.md), [Android Enterprise-](vpn-settings-android-enterprise.md), [macOS-](vpn-settings-macos.md) und [Windows 10-](vpn-settings-windows-10.md)-Geräte.
