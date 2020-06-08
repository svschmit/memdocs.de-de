---
title: Einstellungen für gemeinsam genutzte Windows 10-Geräte – Microsoft Intune (Azure) | Microsoft-Dokumentation
description: Fügen Sie Windows 10 hinzu, um Geräte zu konfigurieren, die gemeinsam genutzt oder von mehreren Benutzern in Microsoft Intune verwendet werden. Hier finden Sie eine Liste mit allen Einstellungen und ihren Auswirkungen auf die Geräte (einschließlich Microsoft Surface). Verwalten Sie Gastkonten und sonstige Konten, löschen Sie inaktive Konten, aktivieren oder deaktivieren Sie das Speichern auf lokalen Speichermedien, legen Sie Energieoptionen und den Zeitpunkt für die Installation fest und verwenden Sie Geräte, die im Bildungsbereich eingesetzt werden, in einem Gerätekonfigurationsprofil.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/14/2020
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
ms.openlocfilehash: f013074ac67b7622b509d8b9781de3ab5f4041e0
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429504"
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

- **Modus für gemeinsame PC-Nutzung:** **Aktivieren** aktiviert den Modus für gemeinsame PC-Nutzung. In diesem Modus kann sich nur jeweils ein Benutzer auf dem Gerät anmelden. Ein anderer Benutzer kann sich erst anmelden, nachdem der aktuelle Benutzer sich abgemeldet hat. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.
- **Gastkonto:** Aktivieren Sie diese Einstellung, damit die Option „Gast“ auf dem Anmeldebildschirm verfügbar ist. Für Gastkonten sind keine Anmeldeinformationen und keine Authentifizierung erforderlich. Für diese Einstellung wird bei jeder Verwendung ein neues lokales Konto erstellt. Folgende Optionen sind verfügbar:
  - **Gast:** Erstellt ein lokales Gastkonto auf dem Gerät.
  - **Domäne:** Erstellt ein Gastkonto in Azure Active Directory (AD).
  - **Gast und Domäne:** Erstellt ein lokales Gastkonto auf dem Gerät und ein Gastkonto in Azure Active Directory (AD).
- **Kontoverwaltung:** Entscheiden Sie, ob Konten automatisch gelöscht werden sollen. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
  - **Aktiviert**: Konten, die von Gästen erstellt werden, und Konten in AD und Azure AD werden automatisch gelöscht. Wenn ein Benutzer sich von einem Gerät abmeldet oder die Systemwartung ausgeführt wird, werden diese Konten gelöscht.

    Geben Sie außerdem Folgendes ein:

    - **Kontolöschung:** Legen Sie fest, wann Konten gelöscht werden sollen:
      - **Bei Erreichen des Schwellenwerts für Speicherplatz**
      - **Bei Erreichen des Schwellenwerts für Speicherplatz und inaktive Konten**
      - **Sofort nach der Abmeldung**

    Geben Sie außerdem Folgendes ein:

    - **Schwellenwert (%) für das Starten von Löschungen:** Geben Sie einen Prozentsatz (0 – 100) für den Speicherplatz ein. Wenn der gesamte Speicherplatz unter den eingegebenen Wert fällt, werden die zwischengespeicherten Konten gelöscht. Es werden fortlaufend Konten gelöscht, um Speicherplatz freizugeben. Die Konten, die am längsten inaktiv sind, werden zuerst gelöscht.
    - **Schwellenwert (%) für das Beenden von Löschungen:** Geben Sie einen Prozentsatz (0 – 100) für den Speicherplatz ein. Wenn der gesamte Speicherplatz dem eingegebenen Wert entspricht, werden keine Konten mehr gelöscht.
    - **Schwellenwert für inaktive Konten**: Geben Sie die Anzahl der aufeinander folgenden Tage ein, bevor das Konto gelöscht wird, das sich nicht angemeldet hat (0 bis 60 Tage).

  - **Deaktiviert:** Die lokalen und die Azure AD-Konten, die von Gästen erstellt werden, bleiben auf dem Gerät erhalten und werden nicht gelöscht.

- **Lokaler Speicher:** Mit dem lokalen Speicher können Benutzer Dateien auf der Festplatte des Geräts speichern und anzeigen. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
  - **Aktiviert**: Verhindert, dass Benutzer Dateien auf der Festplatte des Geräts speichern und von dort anzeigen.
  - **Deaktiviert:** Ermöglicht Benutzern das Aufrufen von Dateien und das lokale Speichern von Dateien über den Datei-Explorer.

- **Energieverwaltungsrichtlinien:** Erlaubt oder verhindert, dass Benutzer die Energieeinstellungen ändern können. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
  - **Aktiviert**: Benutzer können den Ruhezustand nicht deaktivieren, die Aktionen für den Energiesparmodus nicht überschreiben (z. B. das Zuklappen des Geräts) und die Energieeinstellungen nicht ändern.
  - **Deaktiviert:** Benutzer können das Gerät in den Ruhezustand versetzen, das Gerät schließen, um den Energiesparmodus zu aktivieren und die Energieeinstellungen ändern.

- **Timeout für Energiesparmodus (in Sekunden):** Geben Sie an, wie viele Sekunden das Gerät inaktiv sein muss (0 bis 18000), bevor es in den Energiesparmodus versetzt wird. `0` bedeutet, dass sich das Gerät niemals im Ruhezustand befindet. Wenn Sie keine Zeit festlegen, wird das Gerät nach 3.600 Sekunden (60 Minuten) in den Energiesparmodus versetzt.

- **Anmeldung bei PC-Reaktivierung:** Wählen Sie aus, ob sich Benutzer anmelden müssen, wenn das Gerät den Energiesparmodus verlässt. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
  - **Aktiviert**: Verlangt, dass sich Benutzer mit einem Kennwort anmelden müssen, wenn das Gerät aus dem Energiesparmodus reaktiviert wird.
  - **Deaktiviert:** Benutzer müssen keinen Benutzernamen und kein Kennwort eingeben.

- **Startzeitpunkt für Wartung (in Minuten ab Mitternacht):** Geben Sie die Zeit in Minuten ein (0 – 1440), zu der automatische Wartungstasks (z. B. Windows Update) ausgeführt werden sollen. Die Standardzeit für den Start ist auf Mitternacht bzw. null (`0`) Minuten festgelegt. Ändern Sie die Startzeit, indem Sie eine Startzeit in Minuten (von Mitternacht aus) eingeben. Wenn Sie die Wartung beispielsweise um 2 Uhr morgens durchführen möchten, geben Sie `120` ein. Wenn Sie die Wartung um 20 Uhr durchführen möchten, geben Sie `1200` ein.

  Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert.

- **Education-Richtlinien:** Wählen Sie diese Option aus, wenn Richtlinien für Bildungseinrichtungen aktiviert sind. Folgende Optionen sind verfügbar:
  - **Nicht konfiguriert** (Standardeinstellung): Diese Einstellung wird von Intune nicht geändert oder aktualisiert.
  - **Aktiviert**: Verwendet die empfohlenen (eingeschränkteren) Einstellungen für Geräte in Bildungseinrichtungen.
  - **Deaktiviert:** Die empfohlenen Standardrichtlinien für Geräte in Bildungseinrichtungen werden nicht verwendet.

  Weitere Informationen zu den Bildungsrichtlinien finden Sie unter [Windows 10 configuration recommendations for education customers (Empfehlungen für die Konfiguration von Windows 10 für Kunden im Bildungsbereich)](https://docs.microsoft.com/education/windows/configure-windows-for-education).

> [!TIP]
> [Einrichten eines gemeinsam genutzten oder Gast-PC](https://docs.microsoft.com/windows/configuration/set-up-shared-or-guest-pc) (öffnet eine andere Dokumentationswebsite) ist eine großartige Ressource für dieses Windows 10-Feature. Hier finden Sie Konzepte und Gruppenrichtlinien, die im Modus für gemeinsame PC-Nutzung festgelegt werden können.

## <a name="next-steps"></a>Nächste Schritte

- [Zuweisen von Profilen](device-profile-assign.md) und [Überwachen von Profilen](device-profile-monitor.md)
- Einstellungen für [Windows Holographic for Business](shared-user-device-settings-windows-holographic.md)
