---
title: Einstellungen für gemeinsam genutzte Windows 10-Geräte – Microsoft Intune (Azure) | Microsoft-Dokumentation
description: Fügen Sie Windows 10 hinzu, um Geräte zu konfigurieren, die gemeinsam genutzt oder von mehreren Benutzern in Microsoft Intune verwendet werden. Hier finden Sie eine Liste mit allen Einstellungen und ihren Auswirkungen auf die Geräte (einschließlich Microsoft Surface). Verwalten Sie Gastkonten und sonstige Konten, löschen Sie inaktive Konten, aktivieren oder deaktivieren Sie das Speichern auf lokalen Speichermedien, legen Sie Energieoptionen und den Zeitpunkt für die Installation fest und verwenden Sie Geräte, die im Bildungsbereich eingesetzt werden, in einem Gerätekonfigurationsprofil.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/10/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: c76045413324deef395f546033d37ec47405a28f
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79361587"
---
# <a name="windows-10-and-later-settings-to-manage-shared-devices-using-intune"></a>Einstellungen für Windows 10 (und höher) für die Verwaltung von gemeinsam genutzten Geräten mithilfe von Intune

Geräte mit Windows 10 und höher (z. B. Microsoft Surface-Geräte) können von vielen Benutzern verwendet werden. Geräte mit mehreren Benutzern werden als „gemeinsam genutzte Geräte“ bezeichnet und sind in den Lösungen für die mobile Geräteverwaltung (Mobile Device Management, MDM) enthalten.

Mithilfe von Microsoft Intune können Endbenutzer sich bei gemeinsam genutzten Geräten mit einem Gastkonto anmelden. Bei der Verwendung des Geräts erhalten diese Benutzer dann nur Zugriff auf von Ihnen ausgewählte Features. Als Intune-Administrator können Sie unter anderem den Zugriff für gemeinsam genutzte Windows 10-Geräte konfigurieren, festlegen, wann Konten gelöscht werden, und Einstellungen für die Energieverwaltung vornehmen.

In diesem Artikel werden die Einstellungen aufgeführt und beschrieben, die in einem Gerätekonfigurationsprofil für Windows 10 (und höher) verwendet werden können. Wenn das Profil in Intune erstellt wird, stellen Sie das Profil für die Gerätegruppen in Ihrer Organisation bereit oder weisen es diesen zu. Sie können dieses Profil ebenfalls zu Gerätegruppen mit gemischten Gerätetypen und Betriebssystemversionen zuweisen.

Weitere Informationen zu diesem Intune-Feature finden Sie unter [Control access, accounts, and power features on shared PC or multi-user devices (Features für das Steuern von Zugriff, Konten und Energieeinstellungen auf gemeinsam genutzten Computern oder Geräten mit mehreren Benutzern)](shared-user-device-settings.md). Weitere Informationen zum Windows-Konfigurationsdienstanbieter (Configuration Service Provider, CSP) finden Sie unter [SharedPC CSP (Konfigurationsdienstanbieter „SharedPC“)](https://docs.microsoft.com/windows/client-management/mdm/sharedpc-csp).

## <a name="before-your-begin"></a>Vorbereitungen

[Erstellen Sie das Profil.](shared-user-device-settings.md)

## <a name="shared-multi-user-device-settings"></a>Einstellungen für von mehreren Benutzern gemeinsam genutzte Geräte

Diese Einstellungen verwenden den [SharedPC-CSP](https://docs.microsoft.com/windows/client-management/mdm/sharedpc-csp).

- **Modus für gemeinsame PC-Nutzung:** Klicken Sie auf **Aktivieren**, um den Modus für gemeinsame PC-Nutzung zu aktivieren. In diesem Modus kann sich nur jeweils ein Benutzer auf dem Gerät anmelden. Ein anderer Benutzer kann sich erst anmelden, nachdem der aktuelle Benutzer sich abgemeldet hat. **Nicht konfiguriert** (Standard):Diese Einstellung wird von Intune nicht verwaltet und nicht mithilfe von Richtlinien auf den Geräten kontrolliert.
- **Gastkonto:** Aktivieren Sie diese Einstellung, damit die Option „Gast“ auf dem Anmeldebildschirm verfügbar ist. Für Gastkonten sind keine Anmeldeinformationen und keine Authentifizierung erforderlich. Für diese Einstellung wird bei jeder Verwendung ein neues lokales Konto erstellt. Folgende Optionen sind verfügbar:
  - **Gast:** Erstellt ein lokales Gastkonto auf dem Gerät.
  - **Domäne:** Erstellt ein Gastkonto in Azure Active Directory (AD).
  - **Gast und Domäne:** Erstellt ein lokales Gastkonto auf dem Gerät und ein Gastkonto in Azure Active Directory (AD).
- **Kontoverwaltung:** Legen Sie diese Option auf **Aktivieren** fest, damit lokale Gastkonten und Konten in AD und Azure AD automatisch gelöscht werden. Wenn ein Benutzer sich von einem Gerät abmeldet oder die Systemwartung ausgeführt wird, werden diese Konten gelöscht. Wenn diese Option aktiviert ist, sollten sie auch die folgenden festlegen:
  - **Kontolöschung:** Legen Sie fest, wann Konten gelöscht werden sollen: **Bei Erreichen des Schwellenwerts für Speicherplatz**, **Bei Erreichen des Schwellenwerts für Speicherplatz und inaktive Konten** oder **Sofort nach der Abmeldung**. Geben Sie außerdem Folgendes ein:
    - **Schwellenwert (%) für das Starten von Löschungen:** Geben Sie einen Prozentsatz (0 – 100) für den Speicherplatz ein. Wenn der gesamte Speicherplatz unter den eingegebenen Wert fällt, werden die zwischengespeicherten Konten gelöscht. Es werden fortlaufend Konten gelöscht, um Speicherplatz freizugeben. Die Konten, die am längsten inaktiv sind, werden zuerst gelöscht.
    - **Schwellenwert (%) für das Beenden von Löschungen:** Geben Sie einen Prozentsatz (0 – 100) für den Speicherplatz ein. Wenn der gesamte Speicherplatz dem eingegebenen Wert entspricht, werden keine Konten mehr gelöscht.

  Legen Sie die Option auf **Deaktivieren** fest, um die lokalen, AD- und Azure AD-Gastkonten beizubehalten.

- **Lokaler Speicher:** Wählen Sie **Aktiviert** aus, um zu verhindern, dass Benutzer Dateien auf der Festplatte des Geräts speichern und von dort aufrufen. Wählen Sie **Deaktiviert** aus, wenn Sie Benutzern das Aufrufen von Dateien und das lokale Speichern von Dateien über den Datei-Explorer ermöglichen möchten. **Nicht konfiguriert** (Standard):Diese Einstellung wird von Intune nicht verwaltet und nicht mithilfe von Richtlinien auf den Geräten kontrolliert.
- **Energieverwaltungsrichtlinien:** Wenn Sie diese Option auf **Aktiviert** festlegen, können Benutzer den Ruhezustand nicht deaktivieren, die Aktionen für den Energiesparmodus nicht überschreiben (z. B. das Zuklappen des Geräts) und die Energieeinstellungen nicht ändern. Wenn Sie diese Option auf **Deaktiviert** festlegen, können Benutzer das Gerät in den Ruhezustand versetzen, das Gerät schließen, um den Energiesparmodus zu aktivieren und die Energieeinstellungen ändern. **Nicht konfiguriert** (Standard):Diese Einstellung wird von Intune nicht verwaltet und nicht mithilfe von Richtlinien auf den Geräten kontrolliert.
- **Timeout für Energiesparmodus (in Sekunden):** Geben Sie an, wie viele Sekunden das Gerät inaktiv sein muss (0 bis 18000), bevor es in den Energiesparmodus versetzt wird. `0` bedeutet, dass sich das Gerät niemals im Ruhezustand befindet. Wenn Sie keine Zeit festlegen, wird das Gerät nach 3.600 Sekunden (60 Minuten) in den Energiesparmodus versetzt.
- **Anmeldung bei PC-Reaktivierung:** Legen Sie diese Option auf **Aktiviert** fest, damit sich Benutzer mit einem Kennwort anmelden müssen, wenn das Gerät aus dem Energiesparmodus gestartet wird. Legen Sie die Option auf **Deaktiviert** fest, damit die Benutzer keinen Benutzernamen und kein Kennwort eingeben müssen. **Nicht konfiguriert** (Standard):Diese Einstellung wird von Intune nicht verwaltet und nicht mithilfe von Richtlinien auf den Geräten kontrolliert.
- **Startzeitpunkt für Wartung (in Minuten ab Mitternacht):** Geben Sie die Zeit in Minuten ein (0 – 1440), zu der automatische Wartungstasks (z. B. Windows Update) ausgeführt werden sollen. Die Standardzeit für den Start ist auf Mitternacht bzw. null (`0`) Minuten festgelegt. Ändern Sie die Startzeit, indem Sie eine Startzeit in Minuten (von Mitternacht aus) eingeben. Wenn Sie die Wartung beispielsweise um 2 Uhr morgens durchführen möchten, geben Sie `120` ein. Wenn Sie die Wartung um 20 Uhr durchführen möchten, geben Sie `1200` ein.
- **Education-Richtlinien:** Wählen Sie **Aktiviert** aus, um die empfohlenen (eingeschränkteren) Einstellungen für Geräte in Bildungseinrichtungen zu verwenden. Wählen Sie **Deaktiviert** aus, damit die empfohlenen Standardrichtlinien für Geräte in Bildungseinrichtungen nicht verwendet werden. **Nicht konfiguriert** (Standard):Diese Einstellung wird von Intune nicht verwaltet und nicht mithilfe von Richtlinien auf den Geräten kontrolliert.

  Weitere Informationen zu den Bildungsrichtlinien finden Sie unter [Windows 10 configuration recommendations for education customers (Empfehlungen für die Konfiguration von Windows 10 für Kunden im Bildungsbereich)](https://docs.microsoft.com/education/windows/configure-windows-for-education).

- **Schnelle erste Anmeldung** (veraltet): Wählen Sie **Aktiviert** aus, damit Benutzer die schnelle erste Anmeldung nutzen können. Wenn für diese Einstellung die Option **Aktiviert** ausgewählt wurde, verbindet das Gerät neue Azure AD-Konten ohne Administratorberechtigungen automatisch mit den vorkonfigurierten lokalen Kandidatenkonten. Wählen Sie **Deaktiviert** aus, um die schnelle erste Anmeldung zu verhindern. **Nicht konfiguriert** (Standard):Diese Einstellung wird von Intune nicht verwaltet und nicht mithilfe von Richtlinien auf den Geräten kontrolliert.

  Diese Einstellung wird in einem zukünftigen Release entfernt. Verwenden Sie diese Einstellung nicht.

  [Authentication/EnableFastFirstSignIn CSP](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-authentication#authentication-enablefastfirstsignin)

> [!TIP]
> [Einrichten eines gemeinsam genutzten oder Gast-PC](https://docs.microsoft.com/windows/configuration/set-up-shared-or-guest-pc) (öffnet eine andere Dokumentationswebsite) ist eine großartige Ressource für dieses Windows 10-Feature. Hier finden Sie Konzepte und Gruppenrichtlinien, die im Modus für gemeinsame PC-Nutzung festgelegt werden können.

## <a name="next-steps"></a>Nächste Schritte

- [Zuweisen von Profilen](device-profile-assign.md) und [Überwachen von Profilen](device-profile-monitor.md)
- Einstellungen für [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md)
