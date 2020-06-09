---
title: Erstellen von Konfigurationselementen für Windows
titleSuffix: Configuration Manager
description: Erstellen Sie Konfigurationselemente, um Einstellungen für Windows 10-Computer mit der lokalen Verwaltung mobiler Geräte (Mobile Device Management, MDM) in Configuration Manager zu verwalten.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 23e1e4dc-623a-4521-ad04-ae9482927097
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1987ba504630ab1d4b23cdb54710f0cbaa3db28a
ms.sourcegitcommit: 7f542c97ac55bbd329f5befda97d671213c24e9a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/08/2020
ms.locfileid: "84506248"
---
# <a name="create-configuration-items-for-windows-devices-with-on-premises-mdm-in-configuration-manager"></a>Erstellen von Konfigurationselementen für Windows-Geräte mit lokalem MDM in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie das Konfigurationselement Configuration Manager **Windows 8.1 und Windows 10** , um Einstellungen für Windows-Geräte zu verwalten, die Sie mit der lokalen Verwaltung mobiler Geräte (Mobile Device Management, MDM) verwalten.

Weitere allgemeine Informationen zu Konformitäts Einstellungen in Configuration Manager finden Sie in den folgenden Artikeln:

- [Erste Schritte mit Konformitätseinstellungen](../../compliance/get-started/get-started-with-compliance-settings.md)

- [Planen und Konfigurieren von Konformitätseinstellungen](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)

## <a name="create-a-configuration-item"></a>Erstellen eines Konfigurations Elements

1. Wechseln Sie in der Configuration Manager Konsole zum Arbeitsbereich bestand **und** Kompatibilität, erweitern Sie **Konformitäts Einstellungen**, und wählen Sie dann den Knoten **Konfigurationselemente** aus.

1. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Erstellen** die Option **Konfigurationselement erstellen** aus.

1. Geben Sie auf der Seite **Allgemein** des **Assistenten zum Erstellen von Konfigurationselementen** die folgenden Informationen an:

    - **Name**: ein eindeutiger Name zum Identifizieren dieses Konfigurations Elements.

    - **Beschreibung**: eine optionale Beschreibung, um weitere Informationen zur Verwendung bereitzustellen.

    - Wählen Sie unter **Einstellungen für Geräte, die *ohne* den Configuration Manager-Client verwaltet**werden, **Windows 8.1 und Windows 10**aus.

    - **Kategorien**: Sie können Kategorien erstellen und zuweisen, um Sie beim Durchsuchen und Filtern von Konfigurationselementen in der Configuration Manager Konsole zu unterstützen.

1. Wählen Sie auf der Seite **Unterstützte Plattformen** des Assistenten die jeweiligen Windows-Plattformen zum Auswerten dieses Konfigurations Elements aus.

1. Wählen Sie auf der Seite **Geräteeinstellungen** die Einstellungs Gruppen aus, die Sie konfigurieren möchten. Weitere Informationen zu den verfügbaren Einstellungen finden Sie unter [Einstellungs Referenz](#bkmk_setref).

    > [!TIP]
    > Wenn die gewünschte Einstellung nicht aufgeführt ist, wählen Sie die Option zum **Konfigurieren zusätzlicher Einstellungen aus, die nicht in den Standard Einstellungs Gruppen vorhanden sind**. Mit dieser Option wird dem Assistenten die Seite **zusätzliche Einstellungen** hinzugefügt.

1. Konfigurieren Sie auf jeder Einstellungsseite die erforderlichen Einstellungen. Wenn Sie von den Einstellungen unterstützt werden, können Sie auch **nicht kompatible Einstellungen**wiederherstellen. Wenn ein Gerät die Einstellung als nicht kompatibel mit diesem Konfigurationselement auswertet, wird die Einstellung auf "kompatibel" festgelegt.

    Sie können für jede Einstellungs Gruppe auch den Schweregrad konfigurieren, den er meldet, wenn die Einstellung nicht kompatibel ist. Wählen Sie einen der folgenden Werte für die Option **Schweregrad der Nichtkonformität für Berichte aus** :

    - **Keiner**: Für Geräte, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird kein Fehlerschweregrad für Configuration Manager-Berichte gemeldet.

    - **Informationen**

    - **Warning**

    - **Critical** (Kritisch)

    - **Kritisch mit Ereignis**: Für Geräte, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet. Außerdem wird der nicht kompatible Zustand im Anwendungs Ereignisprotokoll als Windows-Ereignis protokolliert.

1. Überprüfen Sie auf der Seite **Platt Form Anwendbarkeit** des Assistenten alle Einstellungen, die mit den ausgewählten unterstützten Plattformen nicht kompatibel sind. Gehen Sie zurück, und entfernen Sie diese Einstellungen, ändern Sie die Support Plattformen, oder fahren Sie fort.

    > [!IMPORTANT]
    > Geräte bewerten nicht die Konformität von nicht unterstützten Einstellungen.

1. Schließen Sie den Assistenten ab.

Sie können das neue Konfigurationselement im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Konfigurationselemente** anzeigen.

## <a name="settings-reference"></a><a name="bkmk_setref"></a>Einstellungs Referenz  

In den folgenden Abschnitten werden die in den einzelnen Gruppen verfügbaren spezifischen Einstellungen ausführlich beschrieben. Konfigurieren Sie diese Einstellungen auf der Seite **Geräteeinstellungen** des **Assistenten zum Erstellen von Konfigurations** Elementen für **Windows 8.1-und Windows 10-** Geräte, die *ohne* den Configuration Manager-Client verwaltet werden.

### <a name="password"></a>Kennwort

Diese Einstellungen gelten nur für Geräte, auf denen Windows 10 und höher ausgeführt wird.

- Kenn **Wort Einstellungen auf Geräten erforderlich**: erfordert ein Kennwort auf unterstützten Geräten.
- **Minimale Kenn Wort Länge (Zeichen)**: die Mindestlänge für das Kennwort.
- Kenn **Wort Ablauf in Tagen**: die Anzahl der Tage, bevor der Benutzer sein Kennwort ändern muss.
- **Anzahl der**gespeicherten Kenn Wörter: verhindert die Wiederverwendung zuvor verwendeter Kenn Wörter.
- **Anzahl der fehlgeschlagenen Anmeldeversuche vor**dem Zurücksetzen des Geräts: Wenn diese Anzahl von Anmelde versuchen fehlschlägt, setzt MDM das Gerät zurück.
- **Leerlaufzeit vor dem Sperren des Geräts**: Geben Sie die Zeitspanne an, die ein Gerät im Leerlauf sein kann, bevor es gesperrt ist. Das Gerät befindet sich im Leerlauf, wenn keine Benutzereingaben vorhanden sind.
- Kenn **Wort Komplexität**: Wählen Sie aus, ob Sie eine numerische PIN wie angeben `1234` oder ob Sie ein sicheres Kennwort angeben müssen.
  - **Anzahl komplexer Zeichensätze, die im Kennwort erforderlich**sind: Wenn die Kenn Wort Komplexität **stark**ist, wählen Sie aus, wie viele Zeichen Typen für das Kennwort erforderlich sind: Großbuchstaben, Kleinbuchstaben, Ziffern oder Symbole. Standardmäßig ist dieser Wert auf `2` festgelegt.
- **Kennwortwiederherstellungs-PIN an Exchange Server senden**

### <a name="device"></a>Sicherungsmedium

- **Bildschirmaufnahme**: Aktivieren Sie diese Einstellung, um dem Benutzer zu ermöglichen, einen Screenshot der Geräte Anzeige zu erstellen. (ausschließlich Windows 10)
- **Übermittlung von Diagnosedaten**: Aktivieren Sie diese Einstellung, um Windows-Diagnosedaten für die Analyse zuzulassen. (ausschließlich Windows 8.1)
- **Übermittlung von Diagnosedaten zulassen (Windows 10)**: Hiermit wird die Ebene der Windows-Diagnosedaten für die Analyse festgelegt: deaktivieren, Basic, erweitert oder vollständig. (ausschließlich Windows 10)
- **Geolokation**: Aktivieren Sie diese Einstellung, damit das Gerät Standort Dienst Informationen verwenden kann. (ausschließlich Windows 10)
- **Kopieren und Einfügen**: Aktivieren Sie diese Einstellung, wenn Sie zum Übertragen von Daten zwischen apps kopieren und Einfügen verwenden möchten. (ausschließlich Windows 10)
- **Zurück**setzung auf Werkseinstellungen: Aktivieren Sie diese Einstellung, damit der Benutzer das Gerät auf seine ursprünglichen Einstellungen zurücksetzen kann. (ausschließlich Windows 10)
- **Bluetooth**: Hiermit wird die Verwendung der Bluetooth-Funktion des Geräts zugelassen oder untersagt.
- **Modus für Bluetooth**-Erkennung: Hiermit wird zugelassen oder verhindert, dass das Gerät von anderen Bluetooth-Geräten ermittelt werden kann. (ausschließlich Windows 10)
- **Bluetooth-Werbung**: Hiermit wird die Verwendung von Bluetooth-Werbung zugelassen oder untersagt. (ausschließlich Windows 10)
- **Sprachaufzeichnung**: Hiermit wird die Verwendung der sprach Aufzeichnungs Features des Geräts zugelassen oder untersagt. (ausschließlich Windows 10)
- **Cortana**: Hiermit wird die Verwendung des Cortana-sprach-Assistenten zugelassen oder untersagt. (ausschließlich Windows 10)
- **Info-Center-Benachrichtigungen**: Aktivieren oder deaktivieren Sie den Benachrichtigungsbereich in Windows 10. (ausschließlich Windows 10)
- **Änderung der Regions Einstellungen (nur Desktop)**: Hiermit wird der Benutzer daran gehindert, die regionalen Einstellungen auf dem Gerät zu ändern.
- **Änderung von Energie-und Energiespareinstellungen (nur Desktop)**: Hiermit wird dem Benutzer das Ändern von Energie-und Energiespareinstellungen auf dem Gerät gestattet oder untersagt.
- **Änderung der Spracheinstellungen (nur Desktop)**: Hiermit wird dem Benutzer das Ändern der Spracheinstellungen auf dem Gerät gestattet oder untersagt.
- **Änderung der System Zeit**: Hiermit wird der Benutzer daran gehindert, das Datum und die Uhrzeit des Geräts zu ändern.
- **Änderung des Geräte namens**: Hiermit wird der Benutzer daran gehindert, den Gerätenamen zu ändern.

### <a name="email-management"></a>E-Mail-Verwaltung

Diese Einstellungen gelten nur für Geräte unter Windows 8.1 und Windows 10.  

- **Pop-und IMAP-e-Mail**: Hiermit werden Verbindungen mit e-Mail-Konten, die die Pop-und IMAP-Standards verwenden
- **Maximale Zeit für die Aufbewahrung von e-Mails**: gibt an, wie lange e-Mails aufbewahrt werden sollen, bevor der Server Sie löscht.
- **Zulässige Nachrichtenformate**: Geben Sie an, ob e-Mails nur **Text** oder **HTML und nur-Text**sind.
- **Maximale Größe für nur-Text-e-Mails (automatisch heruntergeladen)**: Legen Sie die maximale Größe von nur-Text-e-Mails beim automatischen Herunterladen fest
- **Maximale Größe für HTML-e-Mails (automatisch heruntergeladen)**: Legen Sie die maximale Größe von HTML-e-Mails fest, wenn Sie automatisch heruntergeladen werden.
- **Maximale Größe einer Anlage (automatisch heruntergeladen)**: legt die maximale Größe von e-Mail-Anlagen fest, die automatisch heruntergeladen werden.
- **Kalender Synchronisierung**: Hiermit wird die Synchronisierung von Kalendern auf das Gerät zugelassen oder untersagt.
- **Benutzerdefiniertes e-Mail-Konto**: Hiermit wird die Verwendung eines nicht-Organisations-e-Mail-Kontos auf dem Gerät zugelassen
- **Microsoft-Konto in Windows Mail-App optional machen**: Aktivieren Sie diese Option, damit keine Microsoft-Konto in Windows Mail erforderlich ist.

### <a name="store"></a>Speicher

Diese Einstellungen gelten nur für Geräte, auf denen Windows 10 und höher ausgeführt wird.

- **Anwendungs Speicher**: Hiermit wird der Zugriff auf die Microsoft Store auf dem Gerät zugelassen oder untersagt.
- **Geben Sie ein Kennwort für den Zugriff auf den Anwendungs Speicher ein**: Aktivieren Sie diese Option, damit Benutzer ein Kennwort eingeben müssen, um auf die Microsoft Store App zuzugreifen.
- **In-App-Käufe**: Hiermit wird Benutzern das tätigen in-App-Käufen gestattet oder untersagt.
- **Store-app starten**: Deaktivieren Sie alle apps, die auf dem Gerät vorinstalliert oder vom Microsoft Store installiert wurden.
- **Apps aus Store automatisch aktualisieren**: Hiermit wird das automatische Update von apps zugelassen oder untersagt, die vom Microsoft Store installiert werden.
- **Installieren von apps auf dem Systemlaufwerk**: Hiermit wird das Gerät für die Installation von apps auf dem Systemlaufwerk zugelassen oder untersagt, das in der Regel das `C:` Laufwerk ist.
- **App-Daten auf System Volume installieren**: Aktivieren Sie diese Option, damit apps Daten auf dem Systemlaufwerk speichern können.
- **Nur privaten Store verwenden**: verlangen Sie, dass Benutzer Apps aus Ihrem privaten Store herunterladen.
- **Game DVR**: Deaktivieren der Windows-Spiel Aufzeichnung und-Übertragung

### <a name="browser"></a>Browser

Diese Einstellungen gelten nur für Geräte unter Windows 8.1 und Windows 10.

- **Webbrowser zulassen**: Hiermit wird die Verwendung des Webbrowsers auf dem Gerät zugelassen oder untersagt.
- **AutoFill**: Hiermit wird das Ändern der Einstellungen für Auto Vervollständigen im Browser zugelassen oder untersagt.
- **Active Scripting**: zulassen oder verweigern, ob der Browser Skripts ausführen kann, z. b. ActiveX-Skripts.
- **Plug-ins**: Hiermit wird das Hinzufügen von Plug-ins zu Internet Explorer zugelassen oder untersagt.
- **Popup Blocker**: Hiermit wird der Popup Blocker des Browsers zugelassen oder untersagt.
- **Cookies**: Hiermit wird das Speichern von Cookies auf dem Gerät zugelassen oder untersagt.
- **Betrugswarnung**: Hiermit werden Warnungen zu potenziell betrügerischen Websites zugelassen oder untersagt.

### <a name="internet-explorer"></a>Internet Explorer

Diese Einstellungen gelten nur für Geräte unter Windows 8.1 und Windows 10.

- **Immer "do not Track"-Header senden**: Hiermit wird das Senden von Browserinformationen an Websites von Drittanbietern zugelassen oder untersagt.
- **Intranetsicherheitszone**: Hiermit wird die Zuweisung einer Sicherheitsebene zur Intranetsicherheitszone zugelassen oder untersagt.
- **Sicherheitsstufe für Internet Zone**: Legen Sie die Sicherheitsstufe für die Internet Zone fest: hoch, Mittel hoch oder Mittel.
- **Sicherheitsstufe für Intranetzone**: Legen Sie die Sicherheitsstufe für die Intranetzone fest: hoch, Mittel hoch, Mittel, Mittel niedrig oder niedrig.
- **Sicherheitsstufe für Zone vertrauenswürdiger Sites**: Legen Sie die Sicherheitsstufe für die Zone vertrauenswürdiger Sites fest: hoch, Mittel hoch, Mittel, Mittel niedrig oder niedrig.
- **Sicherheitsstufe für Zone eingeschränkter Sites**: Legen Sie die Sicherheitsstufe für die Zone Eingeschränkte Sites fest: hoch.
- **Namespaces für Intranetzone**: Konfigurieren Sie Websites, die der Intranetzone hinzugefügt oder daraus entfernt werden
- Wechseln **Sie zur Intranetsite für einen einzelnen Word-Eintrag**: Hiermit wird Internet Explorer das automatische wechseln zu einer Intranetsite zugelassen oder untersagt, wenn der Benutzer einen gültigen Website Namen ohne vorangestelltes Protokoll eingibt `https://` .
- **Menüoption für Unternehmens Modus**: ermöglichen Sie Benutzern das Aktivieren und Deaktivieren des Unternehmens Modus über das **Internet Explorer-** Menü Extras.
  - **Speicherort des Protokollierungs Berichts (URL)**: Wenn der Unternehmens Modus aktiv ist, geben Sie eine URL zum Protokollieren der besuchten Websites an.
- **Speicherort für Unternehmens Modus-Standortliste (URL)**: Wenn der Unternehmens Modus aktiv ist, geben Sie die Liste der Websites an, die ihn verwenden.

### <a name="cloud"></a>Cloud

Diese Einstellungen gelten nur für Geräte unter Windows 8.1 und Windows 10.

- **Einstellungs Synchronisierung**: Hiermit werden Einstellungen für die Synchronisierung zwischen Geräten zugelassen oder untersagt.
- **Synchronisierung von Anmelde**Informationen: Hiermit werden Anmelde Informationen zum Synchronisieren zwischen Geräten zugelassen oder untersagt.
- **Microsoft-Konto**: Aktivieren Sie diese Einstellung, um die Verwendung einer Microsoft-Konto auf dem Gerät zuzulassen.
- **Synchronisierung von Einstellungen über**getaktete Verbindungen: Hiermit wird die Synchronisierung von Einstellungen zugelassen oder verhindert, wenn die Netzwerkverbindung gemessen wird.

### <a name="security"></a>Sicherheit

- **Installation nicht signierter Dateien**: ermöglicht, wer eine nicht signierte Datei installieren darf. (ausschließlich Windows 10)
- **Nicht signierte Anwendungen**: Hiermit wird die Installation nicht signierter Apps zugelassen oder untersagt. (ausschließlich Windows 10)
- **SMS-und MMS-Messaging**: zulassen oder verbieten von Textnachrichten Protokollen auf dem Gerät. (ausschließlich Windows 10)
- Wechsel **Medien: Hiermit**wird die Verwendung von Wechselmedien, z. b. einer SD-Karte, zugelassen oder untersagt. (ausschließlich Windows 10)
- **Kamera**: Hiermit wird die Verwendung der Gerätekamera zugelassen oder untersagt. (ausschließlich Windows 10)
- **Near Field Communication (NFC)**: zulassen oder verbieten der Kommunikation mit NFC. (ausschließlich Windows 10)
- **AntiTheft-Modus**: Hiermit wird die Verwendung des Windows 10-AntiTheft-Modus zugelassen oder untersagt. (ausschließlich Windows 10)
- **USB-Verbindung zulassen**: Hiermit können andere Geräte über eine USB-Verbindung eine Verbindung mit diesem Gerät zulassen oder verbieten. (ausschließlich Windows 10)
- **Windows RT-VPN-Profil**: stellt ein VPN-Profil für Windows RT-Geräte bereit (nur Windows 8.1).

### <a name="peak-synchronization"></a>Hauptzeitsynchronisierung

Diese Einstellungen gelten nur für Geräte, auf denen Windows 10 und höher ausgeführt wird.

- **Hauptzeit angeben**: Hiermit werden die Spitzenzeiten und Wochentage für die Synchronisierung mobiler Geräte festgelegt.
- **Häufigkeit der Hauptzeitsynchronisierung**: Konfigurieren Sie, wie oft die Synchronisierung während der Spitzenzeiten erfolgt.
- **Häufigkeit der Nebenzeitsynchronisierung**: Konfigurieren Sie, wie oft die Synchronisierung außerhalb der Spitzenzeiten erfolgt.

### <a name="roaming"></a>Roaming

- **Geräteverwaltung beim Roaming**: Hiermit wird die Verwaltung des Geräts beim Roaming durch Configuration Manager zugelassen oder untersagt. (ausschließlich Windows 10)
- **Software Download beim Roaming**: Hiermit wird das Herunterladen von apps und Software beim Roaming zugelassen oder untersagt. (ausschließlich Windows 10)
- **E-Mail-Download beim Roaming**: e-Mail-Downloads beim Roaming zulassen oder verbieten. (ausschließlich Windows 10)
- **Datenroaming**: Hiermit wird das Roaming zwischen Netzwerken beim Zugriff auf Daten zugelassen oder untersagt.
- **VPN über Mobilfunk**: Hiermit wird verhindert, dass das Gerät während der Verbindung mit einem Mobilfunknetz eine VPN-Verbindung verwendet. (ausschließlich Windows 10)
- **VPN-Roaming über Mobilfunk**: Hiermit wird verhindert, dass das Gerät beim Roaming in einem Mobilfunknetz eine VPN-Verbindung verwendet. (ausschließlich Windows 10)

### <a name="encryption"></a>Verschlüsselung

- **Speicherkarten Verschlüsselung**: der Wert ist auf festgelegt, sodass der Benutzer alle Speicherkarten verschlüsseln muss, die auf dem Gerät verwendet werden. (ausschließlich Windows 10)
- **Dateiverschlüsselung auf dem Gerät**: Legen Sie auf fest, um auf dem Gerät gespeicherte Dateien zu verschlüsseln.
- **E-Mail-Signierung erforderlich**: der Benutzer muss e-Mails digital signieren, bevor Sie gesendet werden.
  - **Signatur Algorithmus**: Wählen Sie den Algorithmus zum Signieren von e-Mails aus: Standard, SHA oder MD5.
- **E-Mail-Verschlüsselung erforderlich**: der Benutzer muss e-Mails verschlüsseln, bevor diese gesendet werden.
  - **Verschlüsselungsalgorithmus**: Wählen Sie den Algorithmus zum Verschlüsseln von e-Mails aus: Standard, Triple des, des, RC2 128-Bit, RC2 64-Bit, RC2 40-Bit

### <a name="wireless-communications"></a>Funkkommunikation

Diese Einstellungen gelten nur für Geräte, auf denen Windows 10 und höher ausgeführt wird.

- **Drahtlose Netzwerkverbindung**: Hiermit wird die Wi-Fi-Funktion des Geräts zugelassen oder untersagt.
- **Wi-Fi-Tethering**: ermöglichen Sie dem Benutzer die Verwendung des Geräts als mobilen Hotspot.
- Auslagern **von Daten an Wi-Fi, wenn möglich**: Aktivieren Sie das Gerät so weit wie möglich, um die WLAN-Verbindung zu verwenden.
- **Wi-Fi-Hotspot-Bericht**Erstellung: Aktivieren Sie das Gerät zum Senden von Informationen über WLAN-Verbindungen, um dem Benutzer zu helfen, nahe gelegene Verbindungen zu ermitteln.
- **Manuelle WLAN-Konfiguration**: ermöglichen Sie es dem Benutzer, drahtlos Verbindungen manuell zu konfigurieren.

#### <a name="configured-wireless-network-connections"></a>Konfigurierte drahtlos Netzwerkverbindungen

1. Wählen Sie auf der Seite Einstellungen für die **drahtlose Kommunikation mobiler Geräte konfigurieren** die Option **Hinzufügen**aus.

1. Geben Sie im Fenster **drahtlose Netzwerkverbindung** die folgenden Informationen zur drahtlos Verbindung an, die auf mobilen Geräten bereitgestellt werden soll:

    - **Netzwerkname (SSID)**: Geben Sie den Namen des WLAN-Netzwerks ein.
    - **Netzwerkverbindung**: Wählen Sie entweder **Internet** oder **Arbeit**aus.
    - **Authentifizierung**: Wählen Sie die Authentifizierungsmethode für die drahtlos Verbindung aus:
        - **Öffnen**
        - **Freigegeben**
        - **WPA**
        - **WPA-PSK**
        - **WPA2**
        - **WPA2-PSK**
    - **Datenverschlüsselung**: Wählen Sie die Verschlüsselungsmethode aus, die von dieser Verbindung verwendet wird. Die verfügbaren Werte ändern sich je nach ausgewählter **Authentifizierungs** Methode:
        - **Deaktiviert**
        - **WEP**
        - **TKIP**
        - **AES**
    - **Schlüssel Index**: Wenn Sie die **Datenverschlüsselung** auf **WEP**festlegen, wählen Sie einen Schlüssel Index von **1** bis **4**aus.
    - **Dieses Netzwerk stellt eine Verbindung mit dem Internet**her: Proxy Einstellungen angeben, damit Mobile Geräte in einem Drahtlos Netzwerk eine Verbindung mit dem Internet herstellen können.
        - **Proxy Servereinstellungen**: Konfigurieren Sie **die Server** -und **Port** Einstellungen für **http**-, **WAP**-und **Sockets** -Proxys.
    - **802.1 x-Einstellungen**:
        - **802.1 x-Netzwerk Zugriff aktivieren**: Sichern Sie die Verbindung, indem Sie einen EAP-Typ angeben.
        - **EAP-Typ**: Wählen Sie eines der folgenden Authentifizierungsprotokolle aus:
            - **PEAP**
            - **Smartcard oder Zertifikat**

### <a name="certificates"></a>Zertifikate

Importieren Sie Zertifikate, die auf mobilen Geräten installiert werden sollen.

Wählen Sie **importieren**aus, und geben Sie dann die folgenden Werte an:

- **Zertifikatsdatei**: Navigieren Sie zu der zu importierenden Zertifikatsdatei (**CER**-Datei), und wählen Sie Sie aus.
- **Zielspeicher**: Wählen Sie einen oder mehrere der folgenden Zertifikat Speicher aus:
  - **Fasst**
  - **CA**
  - **Normal**
  - **Privilegiert**
  - **SPC**
  - **Peer**
- **Rolle**: Wenn Sie den Zertifikat Speicher des **SPC** -Zertifikats (Software Herausgeber Zertifikat) auswählen, wählen Sie die Rolle aus, die dem Zertifikat zugeordnet werden soll:
  - **Mobilfunkanbieter**
  - **Manager**
  - **Benutzer authentifiziert**
  - **IT-Administrator**
  - **Benutzer nicht authentifiziert**
  - **Vertrauenswürdiger Bereitstellungsserver**

### <a name="system-security"></a>System

- **Benutzerkontensteuerung**: Konfigurieren Sie das Verhalten der Windows-Benutzerkontensteuerung auf dem Gerät.
- **Netzwerk Firewall**: erfordert die Aktivierung der integrierten Firewall durch Windows. (Windows 8.1)
- **Updates**: Konfigurieren Sie das Verhalten von Windows-Software Updates. (Windows 8.1)
  - **Minimale Klassifizierung von Updates**: Wählen Sie die minimale Klassifizierung der herunter zuladenden und zu installierenden Updates aus: **keine**, **wichtig**oder **empfohlen**.
- **Updates (Windows 10)**: Konfigurieren Sie das Verhalten von Windows-Software Updates. (ausschließlich Windows 10)
  - **Installationstag**: Wählen Sie den geplanten Tag aus, an dem das Gerät Updates automatisch installiert und neu gestartet werden soll. (ausschließlich Windows 10)
  - **Installationszeit**: Wählen Sie die geplante Zeit für das automatische Installieren von Updates und Neustarts durch das Gerät aus. (ausschließlich Windows 10)
- **SmartScreen**: aktiviert oder deaktiviert den Windows-SmartScreen.
- **Virenschutz**: erfordert, dass Windows Antivirussoftware aufweist.
- **Virenschutz Signaturen sind auf dem neuesten Stand**: Es ist erforderlich, dass die Antivirensignaturdateien auf dem neuesten Stand sind.
- **Benachrichtigungs Ansicht des Sperr Bildschirms**: Aktivieren oder Deaktivieren von Benachrichtigungen, die auf dem Sperrbildschirm angezeigt werden.
- **Features der Vorabversion**: Konfigurieren Sie, ob das Gerät Einstellungen und Features der Vorabversion akzeptiert. (ausschließlich Windows 10)
- **Manuelle Installation**von Stamm Zertifikaten: Aktivieren oder deaktivieren Sie den Benutzer für die manuelle Installation eines Stamm Zertifikats, wodurch die Vertrauenswürdigkeit für alle von diesem Stamm ausgestellten Zertifikate aktiviert wird. (ausschließlich Windows 10)
- **Manuelle**Aufhebung der Registrierung zulassen: Hiermit wird dem Benutzer das Aufheben der Registrierung des Geräts bei der lokalen Verwaltung mobiler Geräte mit Configuration Manager gestattet oder untersagt.

### <a name="windows-server-work-folders"></a>Arbeitsordner von Windows Server

Diese Einstellungen gelten nur für Geräte unter Windows 8.1 und Windows 10.

- **Arbeitsordner-URL**: Geben Sie den Speicherort eines Windows Server-Arbeits Ordners an, mit dem Benutzer über Ihr Gerät eine Verbindung herstellen können.

### <a name="allowed-and-blocked-apps-list"></a>Liste zulässiger und blockierter apps

Diese Einstellungen gelten nur für Geräte, auf denen Windows Phone ausgeführt wird, die Configuration Manager lokale MDM nicht unterstützt. Weitere Informationen finden Sie unter [Hybride Verwaltung mobiler Geräte](../understand/what-happened-to-hybrid.md).

### <a name="windows-10-team"></a>Windows 10 Team

Diese Einstellungen gelten nur für Geräte, auf denen Windows 10 Team ausgeführt wird.

- **Automatische Aktivierung des Bildschirms zulassen, wenn Sensoren eine Person im Raum erkennen**: Hiermit wird die automatische Aktivierung des Geräts zugelassen oder untersagt, wenn der Sensor eine Person im Raum erkennt.
- **PIN für Funk Projektion**anfordern: Aktivieren oder deaktivieren Sie, ob Sie eine PIN eingeben müssen, damit ein anderes Gerät für die Projektion drahtlos eine Verbindung herstellen kann.
- **Wartungsfenster**: Aktivieren Sie diese Einstellung, um das Fenster zu konfigurieren, wenn Updates das Gerät installieren und neu starten können.
  - **Startzeit**: Legen Sie die Startzeit für das Wartungsfenster fest.
  - **Dauer (Stunden)**: Legen Sie die Länge des Wartungs Fensters in Stunden fest.
- **Azure-Operational Insights**: erlauben Sie [Azure Operational Insights](https://azure.microsoft.com/resources/videos/azure-operational-insights-overview/) , Protokolldatei Daten von Windows 10 Team-Geräten zu erfassen, zu speichern und zu analysieren.
  - **Arbeitsbereichkennung**: Geben Sie eine gültige Arbeitsbereichs-ID
  - **Arbeitsbereichs Schlüssel**: Geben Sie den Schlüssel für den zugehörigen Arbeitsbereich ein.
- **Miracast-Funk Projektion**: zulassen, dass miracast-fähige Geräte auf dieses Windows 10 Team-Gerät projizieren können.
  - **Miracast-Kanal**: Wählen Sie einen miracast-Kanal aus, um Inhalte zu projizieren.
- **Auf dem Begrüßungsbildschirm angezeigte Besprechungs Informationen**: Wählen Sie die Art der Informationen aus, die das Gerät auf der Kachel " **Besprechungen** " auf der **Willkommens** Seite anzeigt:
  - **Nur Organisator und Zeit anzeigen**
  - **Organisator, Zeit und Thema anzeigen (Thema bei privaten Besprechungen ausblenden)**
- **URL des Hintergrund Bilds für den Sperrbildschirm**: Geben Sie eine URL an, um einen benutzerdefinierten Hintergrund auf dem **Begrüßungs** Bildschirm eines Windows 10 Team-Geräts anzuzeigen. Starten Sie die URL mit, `https://` und verwenden Sie das PNG-Format.

### <a name="windows-information-protection"></a>Windows Information Protection  

Weitere Informationen zum Konfigurieren des Unternehmens Datenschutzes mit Configuration Manager finden [Sie Unterschützen von Unternehmensdaten mit Windows Information Protection (WIP)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip).

### <a name="microsoft-edge-legacy"></a>Microsoft Edge-Legacy

Diese Einstellungen gelten nur für Geräte, auf denen Windows 10 und höher ausgeführt wird.  

- **Suchvorschläge in Adressleiste zulassen**: lassen Sie das Suchmodul beim Eingeben von Such Ausdrücken Websites vorschlagen.
- **Nicht verfolgen zulassen**: informieren Sie Websites, dass Sie Ihren Besuch nicht verfolgen sollen.
- **SmartScreen aktivieren**: Überprüfen Sie, ob heruntergeladene Dateien keinen bösartigen Code enthalten.
- **Popups zulassen**: Konfigurieren Sie Browser-Popups.
- **Cookies zulassen**: Konfigurieren Sie die Verwendung von Cookies.
- **AutoFill zulassen**: lassen Sie den Browser Formulare automatisch mit gespeicherten Informationen wie Name, Adresse und Telefon ausfüllen.
- **Kennwort-Manager zulassen**: lassen Sie den Browser Kenn Wörter für Websites speichern und verwalten.
- **Entwicklertools**: Hiermit wird das Feature "Entwickler Tools" von Edge zugelassen oder untersagt.
- **Extensions**: Edge-Erweiterungen zulassen oder verbieten.
- **InPrivate-Browsen**: Hiermit wird das InPrivate-Browsen zugelassen oder verhindert, das den Verlauf oder Cookies nicht speichert
- **Webrtc-localhost-IP-Adresse**: Hiermit wird die Anzeige der localhost-IP-Adresse des Geräts zugelassen oder untersagt, wenn der Benutzer Telefonanrufe mithilfe des Web-RTC-Protokolls ausführt.
- **Zugriff auf about: Flags blockieren**: Hiermit wird dem Benutzer der Zugriff auf die Seite gestattet oder untersagt `about:flags` , die Entwickler-und experimentelle Einstellungen enthält.
- **Außer Kraft setzen von SmartScreen-Aufforderung für Dateien**: Hiermit wird dem Benutzer das umgehen von SmartScreen-Filter Warnungen zum Herunterladen potenziell schädlicher Dateien gestattet oder untersagt.
- **Außer Kraft setzen von SmartScreen-Aufforderung**: Hiermit wird dem Benutzer das umgehen von SmartScreen-Filter Warnungen zu potenziell schädlichen Websites gestattet oder untersagt.
- **URL zum ersten Ausführen**: Geben Sie eine Website an, die angezeigt werden soll, wenn ein Benutzer zum ersten Mal Edge öffnet.

### <a name="windows-defender-antivirus"></a>Windows Defender Antivirus

Diese Einstellungen gelten nur für Geräte, auf denen Windows 10 und höher ausgeführt wird.

- **Echtzeitüberwachung zulassen**: Aktivieren Sie Echtzeitüberprüfung für Schadsoftware, Spyware und andere unerwünschte Software.
- **Verhaltens Überwachung zulassen**: Defender prüft auf bestimmte bekannte Muster verdächtiger Aktivitäten auf Geräten.
- **Netzwerkinspektionssystem aktivieren**: die Netzwerkinspektionssystem (NIS) trägt zum Schutz von Geräten vor netzwerkbasierten Exploits bei. Es verwendet die Signaturen bekannter Sicherheitsrisiken aus dem Microsoft Endpoint Protection Center, um schädlichen Datenverkehr zu erkennen und zu blockieren.
- **Alle Downloads**überprüfen: Defender scannt alle Dateien, die Sie aus dem Internet herunterladen.
- Skript Überprüfung zulassen: Defender scannt **Skripts**, die in Internet Explorer verwendet werden.
- **Datei-und Programm Aktivität überwachen**: Defender überwacht die Datei-und Programm Aktivität auf Geräten.
  - Überwachte Dateien: Wählen Sie den zu über **wachenden**Dateityp aus: alle, eingehenden oder ausgehenden Dateien.
- **Tage für Nachverfolgung behandelter Schadsoftware**: Defender verfolgt weiterhin behandelte Schadsoftware für die angegebene Anzahl von Tagen nach. Anschließend können Sie die zuvor betroffenen Geräte manuell überprüfen. Wenn Sie die Anzahl von Tagen auf 0 festlegen, verbleibt Schadsoftware im Quarantäne Ordner und wird nicht automatisch entfernt. Der Höchstwert ist 90.
- **Client Zugriff**auf Benutzeroberfläche zulassen: steuert, ob die Defender-Benutzeroberfläche für Benutzer ausgeblendet werden soll. Wenn Sie diese Einstellung ändern, wird Sie bei der nächsten Geräte Neustarts wirksam.
- **Systemscan planen**: Wählen Sie entweder eine vollständige oder eine schnell Überprüfung aus, die regelmäßig am ausgewählten Tag und zur ausgewählten Uhrzeit erfolgt:
  - **Geplanter Tag**: Wählen Sie den geplanten Tag aus, an dem Defender die Überprüfung ausführt.
  - **Geplante Zeit**: Wählen Sie die geplante Zeit aus, zu der Defender die Überprüfung ausführt.
- **Tägliche schnell Überprüfung planen**: Wählen Sie den geplanten Zeitpunkt aus, an dem Defender jeden Tag eine schnell Überprüfung ausführt.
- **CPU-Auslastung während einer**Überprüfung begrenzen: Legen Sie den Prozentsatz des Prozessors fest, den Defender beim Ausführen einer Überprüfung verwenden kann. Geben Sie einen Wert zwischen 1 und 100 ein.
- **Archivdateien**überprüfen: Defender scannt komprimierte Archive, wie z. b. zip-oder CAB-Dateien.
- **E-Mail-Nachrichten**überprüfen: Defender überprüft e-Mail-Nachrichten beim Eintreffen auf dem Gerät
- Wechsel **Laufwerke**überprüfen: Defender scannt Wechsel Datenträger wie USB-Sticks.
- Zugeordnete **Laufwerke**überprüfen: Defender scannt Laufwerke, die Netzwerkfreigaben zugeordnet sind. Beispielsweise `H:` wird dem persönlichen Laufwerk eines Benutzers zugeordnet. Wenn die Dateien auf dem Laufwerk schreibgeschützt sind, kann Defender Schadsoftware, die dort gefunden wird, nicht entfernen.
- Dateien überprüfen, die in frei **gegebenen Netzwerk Ordnern geöffnet**wurden: Defender scannt Dateien, wenn ein Benutzer Sie über einen freigegebenen Netzwerkpfad öffnet. Beispiel: `\\server\share\file.doc`. Wenn die Datei auf der Freigabe schreibgeschützt ist, kann Defender die gefundene Malware nicht entfernen.
- **Intervall für Signatur Aktualisierung**: Wählen Sie das Zeitintervall aus, in dem Defender auf neue Signatur Dateien prüft.
- **Cloud-Schutz zulassen**: Defender verwendet die Microsoft-Cloud, um Informationen über Malware Aktivitäten zu erhalten, und ermöglicht Features wie blockieren im ersten Blick.
- **Benutzer zur Eingabe von Beispielen auffordern**: Wählen Sie das Verhalten für Defender aus, wenn Dateien möglicherweise weiter analysiert werden müssen. Defender kann z. b. automatisch Dateien an Microsoft senden, um zu ermitteln, ob Sie schädlich sind.
- **Erkennung potenziell unerwünschter Anwendungen**: schützt das Gerät vor der Ausführung von Software, die von Defender als potenziell unerwünscht eingestuft wird. Sie können vor der Ausführung dieser Anwendungen schützen oder den Überwachungsmodus verwenden, um zu melden, wenn ein Benutzer eine potenziell unerwünschte Anwendung installiert.
- **Datei-und Ordner Ausschlüsse**: Fügen Sie der Ausschlussliste eine oder mehrere Dateien und Ordner hinzu. Zum Beispiel: `C:\Path` oder `%ProgramFiles%\Path\filename.exe`. Defender enthält diese Dateien und Ordner nicht in Echt Zeit Überprüfungen oder geplante Überprüfungen.
- **Datei Erweiterungs Ausschlüsse**: Fügen Sie der Ausschlussliste eine oder mehrere Dateierweiterungen hinzu. Zum Beispiel: `java` oder `exe`. Defender enthält keine Dateien mit diesen Erweiterungen in Echt Zeit Überprüfungen oder geplanten Überprüfungen.
- **Prozess Ausschlüsse**: Fügen Sie der Ausschlussliste bestimmte Prozesse hinzu. Beispiel: `C:\path\myproc.exe`. Dieser Ausschlusstyp unterstützt nur die folgenden Erweiterungen: `exe` , `com` oder `scr` . Defender schließt diese Prozesse nicht in Echt Zeit Überprüfungen oder geplante Scans ein.

### <a name="additional-settings"></a>Zusätzliche Einstellungen

Wenn Sie auf der Seite **Geräteeinstellungen** des Assistenten die Option **zusätzliche Einstellungen konfigurieren, die in den Standard Einstellungs Gruppen nicht angezeigt werden**, können Sie diese Einstellungen auf dieser Seite mit **zusätzlichen Einstellungen** konfigurieren. Wählen Sie **Hinzufügen** , und wählen Sie dann aus der Liste der verfügbaren mobilen Einstellungen aus. Wählen Sie **auswählen** aus, um die integrierte Einstellung zu ändern, oder erstellen Sie die **Einstellung** , um einen benutzerdefinierten Registrierungs Wert oder Oma-URI-Einstellungstyp zu erstellen

## <a name="next-steps"></a>Nächste Schritte

[Überwachen von Konformitätseinstellungen](../../compliance/deploy-use/monitor-compliance-settings.md)
