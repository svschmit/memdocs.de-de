---
title: Einstellungen für Geräteeinschränkungen für Windows Phone 8.1 in Microsoft Intune
titleSuffix: ''
description: In diesem Artikel erhalten Sie Informationen zu den Intune-Einstellungen zur Steuerung von Geräteeinstellungen und -funktionen auf Windows Phone 8.1-Geräten.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ROBOTS: NOINDEX
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6a655ea2c3770e00ccc685cbe9d59f0fe7e49cd6
ms.sourcegitcommit: 8999e197f10fb72d1b82f30a599d1e588db237b7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88146217"
---
# <a name="microsoft-intune-windows-phone-81-device-restriction-settings"></a>Einstellungen für Geräteeinschränkungen für Windows Phone 8.1 in Microsoft Intune

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]

In diesem Artikel erhalten Sie Informationen zu den Einstellungen für Microsoft Intune-Geräteeinschränkungen, die Sie für Windows Phone 8.1-Geräte konfigurieren können.

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen Sie ein Profil für Windows Phone 8.1-Geräteeinschränkungen](device-restrictions-configure.md).

## <a name="general"></a>Allgemein

- **Kamera:** Wenn **Blockieren** festgelegt wird, wird der Zugriff auf die Kamera des Geräts verhindert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

  Intune verwaltet nur den Zugriff auf die Kamera des Geräts. Das Programm kann nicht auf Bilder oder Videos zugreifen.

- **Kopieren und Einfügen:** Wenn **Blockieren** festgelegt wird, werden Kopier- und Einfügevorgänge zwischen Apps auf dem Gerät verhindert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Wechselmedien:** Wenn **Blockieren** festgelegt wird, wird die Verwendung von externen Speichergeräten wie SD-Karten verhindert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Geolocation**: Wenn **Blockieren** festgelegt wird, wird das Aktivieren der Standortdienste auf Geräten verhindert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Microsoft-Konto**: Wenn **Blockieren** festgelegt wird, werden Benutzer daran gehindert, dem Gerät ein Microsoft-Konto zuzuordnen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Bildschirmaufnahme:** Wenn **Blockieren** festgelegt wird, wird das Erfassen von Screenshots verhindert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Übermittlung von Diagnosedaten:** Wenn **Blockieren** festgelegt wird, werden Geräte daran gehindert, Diagnose- und Nutzungstelemetriedaten an Microsoft zu senden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Synchronisierung benutzerdefinierter E-Mail-Konten:** Wenn **Blockieren** festgelegt wird, können Geräte keine Verbindungen mit E-Mail-Konten herstellen, die nicht von Microsoft stammen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

## <a name="password"></a>Kennwort

- **Kennwort:** Wenn **Erforderlich** festgelegt wird, müssen Benutzer ein Kennwort eingeben, um auf Geräte zuzugreifen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Diese Einstellung gilt nur für lokale Konten. Kennwörter für Domänenkonten werden weiterhin von Active Directory (AD) und Azure AD konfiguriert.
  - **Erforderlicher Kennworttyp:** Wählen Sie den Kennworttyp aus. Folgende Optionen sind verfügbar:
    - **Gerätestandard:** Das Kennwort kann Zahlen und Buchstaben enthalten.
    - **Alphanumerisch**: Das Kennwort muss aus einer Kombination aus Ziffern und Buchstaben bestehen.
    - **Numerisch**: Das Kennwort darf nur aus Zahlen bestehen.
  - **Minimale Kennwortlänge:** Geben Sie die erforderliche Mindestanzahl von Zeichen ein (zwischen 4 und 16). Geben Sie z.B. `6` ein, um ein mindestens sechs Zeichen langes Kennwort zu verlangen.
  - **Einfache Kennwörter:** Wenn **Blockieren** festgelegt wird, werden Benutzer daran gehindert, einfache Kennwörter wie `1234` oder `1111` zu erstellen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
  - **Anzahl von fehlgeschlagenen Anmeldungen, bevor das Gerät zurückgesetzt wird:** Geben Sie an, wie häufig ein falsches Kennwort eingegeben werden kann, bevor Geräte zurückgesetzt werden.
  - **Maximaler Zeitraum der Inaktivität (in Minuten) bis zur Bildschirmsperrung:** Geben Sie den Zeitraum an, für den sich Geräte im Leerlauf befinden müssen, bevor der Bildschirm automatisch gesperrt wird. Geben Sie zum Beispiel `5` ein, um Geräte nach 5 Minuten im Leerlauf zu sperren. Wenn die Einstellung **Nicht konfiguriert** oder nichts festgelegt ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.
  - **Kennwortablauf (Tage):** Geben Sie den Zeitraum in Tagen an, nach dem das Kennwort für das Gerät geändert werden muss (zwischen 1 und 255). Geben Sie beispielsweise `90` an, damit das Kennwort nach 90 Tagen abläuft. Wenn kein Wert angegeben ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.
  - **Wiederverwendung vorheriger Kennwörter verhindern:** Geben Sie die Anzahl der zuvor verwendeten Kennwörter ein, die nicht erneut verwendet werden können, von 1–24. Geben Sie z.B. `5` an, damit ein Benutzer sein neues Kennwort nicht auf sein aktuelles Kennwort oder eines seiner vorherigen vier Kennwörter festlegen kann. Wenn kein Wert angegeben ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.
- **Verschlüsselung:** Wenn **Erforderlich** festgelegt wird, wird die Verschlüsselung auf Geräten, einschließlich Dateien, vorgeschrieben. Nicht alle Geräte unterstützen die Verschlüsselung. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Konfigurieren Sie außerdem Folgendes, um diese Einstellung zu konfigurieren und sie ordnungsgemäß als konform zu melden:
  - **Kennwort anfordern**: Legen sie **Erfordern** fest.
  - **Erforderlicher Kennworttyp:** Legen Sie mindestens **Numerisch** fest.
  - **Minimale Kennwortlänge:** Legen Sie mindestens `4` fest.

## <a name="app-store"></a>App Store

- **App Store:** Wenn **Blockieren** festgelegt wird, können Benutzer nicht auf den App Store zugreifen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

## <a name="restricted-apps"></a>Eingeschränkte Apps

In der Liste der eingeschränkten Apps können Sie eine der folgenden Listen konfigurieren:

- **Blockierte Apps:** Listet die (nicht von Intune verwalteten) Apps auf, die Benutzer nicht installieren und ausführen dürfen.
- **Zulässige Apps:** Listet die Apps auf, die Benutzer installieren dürfen. Apps, die von Intune verwaltet werden, sind automatisch zugelassen.

Klicken Sie zum Konfigurieren einer Liste auf **Hinzufügen**. Geben Sie einen Namen Ihrer Wahl sowie die URL zur App im App-Store und optional den Herausgeber der App an.

### <a name="how-to-specify-the-url-to-an-app-in-the-store"></a>Angeben der URL zu einer App im Store

Verwenden Sie das folgende Format, um eine App-URL in der Liste zulässiger und blockierter Apps anzugeben:

Suchen Sie im [Windows Phone Store](https://www.microsoft.com/store/apps/windows-phone) nach der App, die Sie verwenden möchten.

Öffnen Sie die Seite der App, und kopieren Sie die URL in die Zwischenablage. Sie können diese URL nun in der Liste kompatibler oder nicht kompatibler Apps verwenden.

Beispiel: Durchsuchen Sie den Store nach der Skype-App. Verwenden Sie dazu die URL `http://www.windowsphone.com/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51`.

### <a name="additional-options"></a>Zusätzliche Optionen

Sie können auch auf **Importieren** klicken, um die Liste mithilfe einer CSV-Datei im Format <*App-URL*>, <*App-Name*>, <*App-Herausgeber*> aufzufüllen. Stattdessen können Sie aber auch auf **Exportieren** klicken, um eine CSV-Datei mit dem Inhalt der Liste der eingeschränkten Apps im gleichen Format zu erstellen.

## <a name="browser"></a>Browser

- **Webbrowser:** Wenn **Blockieren** festgelegt wird, wird der integrierte Webbrowser auf Geräten deaktiviert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

## <a name="cellular-and-connectivity"></a>Mobilfunk und Konnektivität

- **WLAN:** Wenn **Blockieren** festgelegt wird, wird die WLAN-Funktionalität der Geräte deaktiviert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **WLAN-Tethering:** Wenn **Blockieren** festgelegt wird, wird das WLAN-Tethering auf Geräten verhindert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Automatically connect to Wi-Fi hotspots** (Automatische Verbindung mit WLAN-Hotspots): Mit dieser Einstellung können Geräte automatisch Verbindungen mit kostenlosen WLAN-Hotspots herstellen und Nutzungsbedingungen akzeptieren.
- **Berichterstellung für WLAN-Hotspots:** Wenn **Blockieren** festgelegt wird, können Geräte keine Verbindungsinformationen zu WLAN-Hotspots senden. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **NFC:** Wenn **Blockieren** festgelegt wird, werden Vorgänge deaktiviert, die NFC (Near Field Communication, Nahfeldkommunikation) auf Geräten verwenden, die dieses Feature unterstützen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Bluetooth**: **Blockieren** verhindert, dass Benutzer Bluetooth aktivieren können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

## <a name="next-steps"></a>Nächste Schritte

Eine allgemeine Übersicht über das Geräteeinschränkungsprofil finden Sie unter [Konfigurieren der Geräteeinschränkungseinstellungen in Microsoft Intune](device-restrictions-configure.md).
