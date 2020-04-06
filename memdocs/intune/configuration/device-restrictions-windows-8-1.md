---
title: Geräteeinschränkungen für Windows 8.1-Geräte in Microsoft Intune – Azure | Microsoft-Dokumentation
titleSuffix: ''
description: In diesem Artikel erhalten Sie Informationen zu den Intune-Einstellungen zur Steuerung von Geräteeinstellungen und -funktionen auf Windows 8.1-Geräten.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/30/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 59af48b36cb9c76ce7587457d4921356f542493f
ms.sourcegitcommit: e2877d21dfd70c4029c247275fa2b38e76bd22b8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/31/2020
ms.locfileid: "80407663"
---
# <a name="microsoft-intune-windows-81-device-restriction-settings"></a>Einstellungen für Geräteeinschränkungen für Windows 8.1 in Microsoft Intune

In diesem Artikel erhalten Sie Informationen zu den Einstellungen für Microsoft Intune-Geräteeinschränkungen, die Sie für Windows 8.1-Geräte konfigurieren können.

## <a name="general"></a>Allgemein

- **Nutzungsdaten freigeben**: Die Einstellung **Blockieren** verhindert, dass das Gerät Diagnose- und Nutzungstelemetriedaten an Microsoft sendet. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Firewall:** Mit der Einstellung **Anfordern** legen Sie fest, dass die Windows-Firewall aktiviert sein muss. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Benutzerkontensteuerung:** Hiermit wird die Benutzerkontensteuerung (UAC, User Account Control) konfiguriert. Legen Sie fest, wie Benutzer über Änderungen auf Geräten benachrichtigt werden. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
  - **Immer benachrichtigen**
  - **Bei App-Änderungen benachrichtigen**
  - **Bei App-Änderungen benachrichtigen (Desktop nicht abblenden)**
  - **Nie benachrichtigen**

## <a name="password"></a>Kennwort

- **Erforderlicher Kennworttyp:** Legen Sie fest, ob Benutzer ein Kennwort eingeben müssen, um auf das Gerät zugreifen zu können. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
  - **Alphanumerisch**: Das Kennwort muss aus einer Kombination aus Ziffern und Buchstaben bestehen.
  - **Numerisch**: Das Kennwort darf nur aus Zahlen bestehen.
- **Minimale Kennwortlänge:** Geben Sie die erforderliche Mindestanzahl von Zeichen ein (zwischen 6 und 16). Geben Sie z. B. `6` ein, um ein mindestens sechs Zeichen langes Kennwort zu verlangen.
- **Anzahl von fehlgeschlagenen Anmeldungen, bevor das Gerät zurückgesetzt wird:** Geben Sie an, wie häufig ein falsches Kennwort eingegeben werden kann, bevor das Gerät zurückgesetzt wird (zwischen 1 und 14).
- **Maximaler Zeitraum der Inaktivität (in Minuten) bis zur Bildschirmsperrung:** Geben Sie den Zeitraum an, für den sich ein Gerät im Leerlauf befinden muss, bevor der Bildschirm automatisch gesperrt wird (zwischen 1 und 60 Minuten). Geben Sie zum Beispiel `5` ein, um Geräte nach 5 Minuten im Leerlauf zu sperren. Wenn die Einstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.
- **Kennwortablauf (Tage):** Geben Sie den Zeitraum in Tagen an, nach dem das Kennwort für das Gerät geändert werden muss (zwischen 1 und 255). Geben Sie beispielsweise `90` an, damit das Kennwort nach 90 Tagen abläuft. Wenn kein Wert angegeben ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.
- **Wiederverwendung vorheriger Kennwörter verhindern:** Geben Sie die Anzahl der zuvor verwendeten Kennwörter ein, die nicht erneut verwendet werden können, von 1–24. Geben Sie z.B. `5` an, damit ein Benutzer sein neues Kennwort nicht auf sein aktuelles Kennwort oder eines seiner vorherigen vier Kennwörter festlegen kann. Wenn kein Wert angegeben ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.
- **Bildcode und PIN:** Die Einstellung **Blockieren** verhindert die Verwendung eines Bilds oder einer PIN als Kennwort. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Mit einem Bildkennwort kann sich der Benutzer mit Gesten auf einem Bild anmelden. Mit einer PIN kann sich der Benutzer mit einem vierstelligen Code schnell anmelden.
- **Verschlüsselung:** Mit der Einstellung **Anfordern** wird Verschlüsselung auf Geräten vorgeschrieben, einschließlich Dateien. Nicht alle Geräte unterstützen die Verschlüsselung. Wenn die Einstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.

  Konfigurieren Sie außerdem Folgendes, um diese Einstellung zu konfigurieren und sie ordnungsgemäß als konform zu melden:
  - **Erforderlicher Kennworttyp:** Legen Sie mindestens **Numerisch** fest.
  - **Minimale Kennwortlänge:** Legen Sie mindestens `4` fest.

  Um die Verschlüsselung auf Geräten zu erzwingen, die Windows 8.1 ausführen, installieren Sie das [MDM-Clientupdate für Windows von Dezember 2014](https://support.microsoft.com/kb/3013816) auf jedem Gerät.

  Wenn Sie diese Einstellung für Windows 8.1-Geräte aktivieren, müssen alle Benutzer des Geräts ein Microsoft-Konto haben.

  Damit die Verschlüsselung funktioniert, muss das Gerät die Hardwarezertifizierungsanforderungen für [Microsoft InstantGo](https://blogs.windows.com/windowsexperience/2014/06/19/instantgo-a-better-way-to-sleep/#IBHULcTfI4PokO8X.97) erfüllen.

  Wenn Sie die Verschlüsselung auf einem Gerät erzwingen, ist der Wiederherstellungsschlüssel nur über das Microsoft-Konto des Benutzers zugänglich, auf das dieser über sein eigenes OneDrive-Konto zugreift. Sie können diesen Schlüssel nicht für einen Benutzer wiederherstellen.

## <a name="browser"></a>Browser

- **AutoAusfüllen:** Die Einstellung **Blockieren** verhindert, dass Benutzer die Einstellungen für das automatische Ausfüllen im Browser ändern und Formularfelder automatisch ausfüllen lassen können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig lässt das Betriebssystem möglicherweise automatisches Ausfüllen zu.
- **Betrugswarnungen:** Mit der Einstellung **Anfordern** werden bei potenziell betrügerischen Websites Betrugswarnungen im Browser angezeigt. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **SmartScreen für Microsoft Edge**: Die Einstellung **Blockieren** schaltet Microsoft Defender SmartScreen aus. SmartScreen sucht beim Zugriff auf Websites und heruntergeladene Dateien nach potenziellen betrügerischen Phishing-Versuchen und Malware. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig ist im Betriebssystem möglicherweise SmartScreen eingeschaltet.
- **JavaScript:** Die Einstellung **Blockieren** verhindert die Ausführung von Skripts wie z. B. JavaScript im Browser. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Popups**: Mit der Einstellung **Blockieren** wird ein Popupblocker eingeschaltet, der Popups im Webbrowser verhindert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **DNT-Kopfzeilen:** Mit der Einstellung **Blockieren** werden Geräte daran gehindert, DNT-Kopfzeilen (Do Not Track) an Websites zu senden, die Nachverfolgungsinformationen anfordern. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Plug-Ins:** Die Einstellung **Blockieren** verhindert, dass Benutzer Plug-Ins in Internet Explorer hinzufügen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Eingabe eines einzelnen Worts auf Intranetsite zulassen:** Diese Einstellung ermöglicht es Benutzern, zu einer Intranetsite zu navigieren, indem sie ein einzelnes Wort eingeben, z. B. `hr` oder `benefits`. **Blockieren** verhindert die Verwendung dieser Funktion. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Automatische Erkennung von Intranetsite:** Mit der Einstellung **Blockieren** wird der Browser daran gehindert, Intranetsites automatisch zu erkennen. Intranetzuordnungsregeln werden blockiert. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Internetsicherheitsebene:** Mit dieser Einstellung wird die Sicherheitsebene für Internetsites festgelegt. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
  - **Mittel**
  - **Mittelhoch**
  - **Hoch**
- **Intranetsicherheitsebene:** Mit dieser Einstellung wird die Sicherheitsebene für Intranetsites festgelegt. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
  - **Niedrig**
  - **Mittel bis niedrig**
  - **Mittel**
  - **Mittelhoch**
  - **Hoch**
- **Sicherheitsstufe für vertrauenswürdige Sites:** Konfiguriert die Sicherheitsstufe für die Zone vertrauenswürdiger Sites. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
  - **Niedrig**
  - **Mittel bis niedrig**
  - **Mittel**
  - **Mittelhoch**
  - **Hoch**
- **Hohe Sicherheit für eingeschränkte Sites:** Konfiguriert die Sicherheitsstufe für Zone eingeschränkter Sites. Die Einstellung **Konfiguriert** erzwingt hohe Sicherheit für eingeschränkte Sites. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Menüzugriff im Unternehmensmodus:** Die Einstellung **Blockieren** hindert Benutzer daran, in Internet Explorer auf die Menüoptionen für den Unternehmensmodus zuzugreifen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Geben Sie auch Folgendes an, wenn **Blockieren** festgelegt ist:
  - **URL zum Speicherort des Protokollberichts:** Geben Sie eine URL an, unter der Berichte mit Websites abgerufen werden können, für die der Menüzugriff im Unternehmensmodus aktiviert ist.
- **Speicherort der Websiteliste für den Unternehmensmodus (nur Desktop):** Geben Sie den Speicherort der Liste mit Websites an, die im Unternehmensmodus geöffnet werden können.

## <a name="cellular"></a>Mobilfunk

- **Datenroaming:** Die Einstellung **Blockieren** verhindert Datenroaming bei Geräten im Mobilfunknetz. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

## <a name="cloud-and-storage"></a>Cloud und Speicher

- **URL der Arbeitsordner:** Geben Sie die URL des Arbeitsordners an, damit Dokumente auf verschiedenen Geräten synchronisiert werden können. Wenn die Standardeinstellung **Nicht konfiguriert** oder nichts festgelegt ist, wird diese Einstellung von Intune nicht geändert oder aktualisiert.
- **Zugriff auf Windows Mail-App ohne Microsoft-Konto:** Die Einstellung **Blockieren** verhindert den Zugriff auf die Windows Mail-Anwendung ohne Microsoft-Konto. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

## <a name="next-steps"></a>Nächste Schritte

Erstellen Sie unter [Windows 10 und höher](device-restrictions-windows-10.md) ein Geräteeinschränkungsprofil.
