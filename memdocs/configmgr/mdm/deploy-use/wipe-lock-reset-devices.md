---
title: Verwalten von Geräten mit lokalem MDM
titleSuffix: Configuration Manager
description: Schützen von Gerätedaten mit vollständigem zurücksetzen, selektivem zurücksetzen, Remote Sperre und Kennungs Rückstellung mithilfe Configuration Manager lokalen Verwaltung mobiler Geräte (Mobile Device Management, MDM).
ms.date: 08/14/2018
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 770da7bd-02dd-474a-9604-93ff1ea0c1e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e9849f3bef5aa67dcc45b00f64487242230edc2e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724724"
---
# <a name="manage-devices-and-protect-data-with-on-premises-mdm-in-configuration-manager"></a>Verwalten von Geräten und schützen von Daten mit lokalem MDM in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Mobile Geräte können vertrauliche Daten speichern und einen einfachen Zugriff auf viele Organisations Ressourcen ermöglichen. Verwenden Sie Configuration Manager für die folgenden Geräte Verwaltungs Aktionen, um Geräte und Daten zu schützen:

- **Vollständiges**zurückgesetzt: Gerät auf Werkseinstellungen wiederherstellen

- **Selektives Löschen**: nur Organisationsdaten entfernen

- **Zurücksetzen**der Kennung: Entfernen oder Zurücksetzen der Kennung, wenn ein Benutzer Sie vergisst

- **Remote Sperre**: helfen Sie, ein Gerät zu sichern, das möglicherweise verloren geht

## <a name="full-wipe"></a>Vollständiges Zurücksetzen  

Wenn Sie ein verlorenes Gerät sichern oder ein Gerät von der aktiven Verwendung abkoppeln müssen, können Sie eine vollständige zurück setzung dafür starten. Durch diese Aktion wird das Gerät auf die Werkseinstellungen des Geräts wieder hergestellt. Dabei werden alle Organisations-und Benutzerdaten und-Einstellungen entfernt.

1. Wechseln Sie in der Configuration Manager Konsole zum Arbeitsbereich bestand **und** Kompatibilität, und wählen Sie den Knoten **Geräte** aus. Sie können auch **Geräte Sammlungen** auswählen und eine Sammlung auswählen, in der das Gerät Mitglied ist.

1. Wählen Sie das Gerät aus, das Sie löschen möchten.

1. Wählen Sie im Menüband in der Gruppe Geräte die Option **Remote Geräte Aktionen**aus, und wählen Sie dann abkoppeln **/** zurücksetzen aus.

1. Wählen Sie im Fenster **aus Configuration Manager außer** Kraft setzen die Option zum Zurücksetzen **des mobilen Geräts aus, und ziehen Sie es von Configuration Manager außer**Kraft.

## <a name="selective-wipe"></a>Selektives Zurücksetzen

Um nur Organisationsdaten von einem Gerät zu entfernen, starten Sie ein selektives Löschen.

### <a name="behaviors-by-os-version"></a>Verhalten nach Betriebssystemversion

In den folgenden Tabellen werden die Daten, die entfernt werden, und die Auswirkung auf die Daten, die nach einer selektiven Löschung auf dem Gerät verbleiben, beschrieben.

#### <a name="windows-10-windows-81-windows-rt-81-and-windows-rt"></a>Windows 10, Windows 8.1, Windows RT 8.1 und Windows RT

|Inhalt|Selektives Verhalten beim Löschen|  
|-------|--------|
|Apps und zugehörige Daten, die von Configuration Manager installiert werden|Dabei werden die apps deinstalliert, und alle Sideload-Schlüssel werden entfernt. Der Verschlüsselungsschlüssel für apps, die das selektive Windows-löschen verwenden, wird aufgehoben, und die Daten sind nicht mehr verfügbar.|
|VPN- und WLAN-Profile|Entfernt die Profile|
|Zertifikate|Entfernt und widerruft die Zertifikate.|
|Einstellung|Entfernt Anforderungen|
|E-Mail-Profile|Entfernt EFS-aktivierte e-Mails, darunter die e-Mail-App für Windows-e-Mails und-Anlagen.|

#### <a name="windows-10-mobile-windows-phone-80-and-windows-phone-81"></a>Windows 10 Mobile, Windows Phone 8.0 und Windows Phone 8.1

|Inhalt|Selektives Verhalten beim Löschen|  
|-------|--------|
|Unternehmens-apps und zugehörige, von Configuration Manager installierte Daten|Dabei werden die apps deinstalliert und die Daten der Organisations-APP entfernt.|
|VPN- und WLAN-Profile|Entfernt die Profile für Windows 10 Mobile und Windows Phone 8,1|
|Zertifikate|Entfernt die Zertifikate für Windows Phone 8,1|
|E-Mail-Profile|Entfernt die Profile (außer Windows Phone 8,0).|

Die folgenden Einstellungen werden ebenfalls aus Windows 10 Mobile- und Windows Phone 8.1-Geräten entfernt:  

- **Kennwort zum Entsperren mobiler Geräte erforderlich**  
- **Einfache Kennwörter zulassen**  
- **Minimale Kennwortlänge**  
- **Erforderlicher Kennworttyp**
- **Kennwortablauf (Tage)**  
- **Kennwortverlauf speichern**  
- **Anzahl der zulässigen wiederholten Anmeldefehler, bevor die Gerätedaten zurückgesetzt werden**  
- **Minuten Inaktivität vor Anforderung des Kennworts**  
- **Erforderlicher Kennworttyp – Mindestanzahl von Zeichensätzen**  
- **Kamera zulassen**
- **Verschlüsselung auf mobilen Geräten vorschreiben**  
- **Wechselspeichermedien zulassen**  
- **Webbrowser zulassen**  
- **App Store zulassen**  
- **Bildschirmaufnahme zulassen**  
- **Geolocation zulassen**  
- **Microsoft-Konto zulassen**  
- **Kopieren und Einfügen zulassen**  
- **WLAN-Tethering zulassen**  
- **Automatische Verbindung mit freien WLAN-Hotspots zulassen**  
- **Berichterstellung für WLAN-Hotspots zulassen**  
- **Zurücksetzen auf Werkseinstellungen zulassen**
- **Bluetooth zulassen**  
- **NFC zulassen**
- **WLAN zulassen**

### <a name="start-a-selective-wipe"></a>Selektives Löschen starten

1. Wechseln Sie in der Configuration Manager Konsole zum Arbeitsbereich bestand **und** Kompatibilität, und wählen Sie den Knoten **Geräte** aus. Sie können auch **Geräte Sammlungen** auswählen und eine Sammlung auswählen, in der das Gerät Mitglied ist.

1. Wählen Sie das Gerät aus, das Sie löschen möchten.

1. Wählen Sie im Menüband in der Gruppe Geräte die Option **Remote Geräte Aktionen**aus, und wählen Sie dann abkoppeln **/** zurücksetzen aus.

1. Wählen Sie im Fenster **aus Configuration Manager außer** Kraft setzen die folgende Option aus: **Unternehmens Inhalt zurücksetzen und mobiles Gerät von Configuration Manager abkoppeln**.

### <a name="recommendations-for-selective-wipe"></a>Empfehlungen für das selektive löschen

- Richten Sie für ein erfolgreiches Löschen von e-Mails e-Mail-Profile zum Windows Phone 8,1-Geräten ein.

- Zum erfolgreichen Zurücksetzen von Apps stellen Sie sicher, dass die Apps über die App-Verwaltung für mobile Geräte verteilt werden.

## <a name="passcode-reset"></a>Zurücksetzen der Kennung

Wenn ein Benutzer seine Kennung vergisst, verwenden Sie diese Aktion, um eine neue temporäre Kennung auf dem Gerät zu erzwingen. Sie können die Kennung auch vollständig entfernen. Die folgende Tabelle erläutert, wie das Zurücksetzen der Kennung auf verschiedenen mobilen Plattformen funktioniert.

| Betriebssystemversion | Zurücksetzen der Kennung |
|------------|----------------|
| Windows 10 | Nicht unterstützt |
| Windows 10 Mobile | Unterstützt, ohne Azure Active Directory verbundene Geräte |
| Windows Phone 8 und Windows Phone 8.1 | Unterstützt |
| Windows RT 8.1 | Nicht unterstützt |
| Windows 8.1 | Nicht unterstützt |

> [!Note]
> Starten Sie die Aktion zum Zurücksetzen der Kennung vom Standort der obersten Ebene aus. Wenn Sie z. b. einen Standort der zentralen Verwaltung verwenden, können Sie die Aktion nur an diesem Standort durchführen. Wenn Sie einen eigenständigen primären Standort verwenden, können Sie die Aktion nur von diesem Standort aus durchführen.

### <a name="remotely-reset-the-passcode-on-a-mobile-device"></a>Remote Zurücksetzung der Kennung auf einem mobilen Gerät

1. Wechseln Sie in der Configuration Manager Konsole zum Arbeitsbereich bestand **und** Kompatibilität, und wählen Sie den Knoten **Geräte** aus. Sie können auch **Geräte Sammlungen** auswählen und eine Sammlung auswählen, in der das Gerät Mitglied ist.

1. Wählen Sie die Geräte aus, auf denen die Kennung zurückgesetzt werden soll.

1. Wählen Sie im Menüband in der Gruppe Geräte die Option **Remote Geräte Aktionen**aus, und wählen Sie dann Kennung **Zurücksetzen**aus.  

### <a name="show-the-state-of-the-passcode-reset"></a>Anzeigen des Status der zurück setzung der Kennung  

1. Wechseln Sie in der Configuration Manager Konsole zum Arbeitsbereich bestand **und** Kompatibilität, und wählen Sie den Knoten **Geräte** aus. Sie können auch **Geräte Sammlungen** auswählen und eine Sammlung auswählen, in der das Gerät Mitglied ist.

1. Wählen Sie die Geräte aus, auf denen Sie den Zustand beim Zurücksetzen der Kennung anzeigen möchten.

1. Wählen Sie im Menüband in der Gruppe Geräte die Option **Remote Geräte Aktionen**aus, und wählen Sie dann Kennung **anzeigen**aus.  

## <a name="remote-lock"></a>Remotesperre

Wenn ein Benutzer sein Gerät verliert, können Sie es remote sperren. In der folgenden Tabelle ist die Funktionsweise der Remotesperrung auf verschiedenen mobilen Plattformen aufgeführt.  

|Betriebssystemversion|Remotesperre|
|----------|-----------|
|Windows 10|Nicht unterstützt|
|Windows Phone 8 und Windows Phone 8.1|Unterstützt|
|Windows RT 8.1|Unterstützt, wenn der aktuelle Benutzer des Geräts derselbe Benutzer ist, der das Gerät registriert hat.|
|Windows 8.1|Unterstützt, wenn der aktuelle Benutzer des Geräts derselbe Benutzer ist, der das Gerät registriert hat.|

> [!Note]
> Starten Sie die Aktion "Remote Sperre" vom Standort der obersten Ebene aus. Wenn Sie z. b. einen Standort der zentralen Verwaltung verwenden, können Sie die Aktion nur an diesem Standort durchführen. Wenn Sie einen eigenständigen primären Standort verwenden, führen Sie die Aktion von diesem Standort aus.

### <a name="remotely-lock-a-mobile-device"></a>Remote Sperren eines mobilen Geräts

1. Wechseln Sie in der Configuration Manager Konsole zum Arbeitsbereich bestand **und** Kompatibilität, und wählen Sie den Knoten **Geräte** aus. Sie können auch **Geräte Sammlungen** auswählen und eine Sammlung auswählen, in der das Gerät Mitglied ist.

1. Wählen Sie die zu sperrenden Geräte aus.

1. Wählen Sie im Menüband in der Gruppe Geräte die Option **Remote Geräte Aktionen**aus, und wählen Sie dann **Remote Sperre**aus. Bestätigen Sie die Aktion.

### <a name="show-the-state-of-the-remote-lock"></a>Anzeigen des Status der Remote Sperre

1. Wechseln Sie in der Configuration Manager Konsole zum Arbeitsbereich bestand **und** Kompatibilität, und wählen Sie den Knoten **Geräte** aus. Sie können auch **Geräte Sammlungen** auswählen und eine Sammlung auswählen, in der das Gerät Mitglied ist.

1. Wählen Sie die Geräte aus, auf denen Sie den Zustand der Remotesperre anzeigen möchten.

1. Wählen Sie im Menüband in der Gruppe Geräte die Option **Remote Geräte Aktionen**aus, und wählen Sie dann **Remote Sperr Status anzeigen**aus.
