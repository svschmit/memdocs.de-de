---
title: Einrichten der Intune-Registrierung für unternehmenseigene Android Enterprise-Geräte mit Arbeitsprofil
titleSuffix: Microsoft Intune
description: Erfahren Sie, wie Sie unternehmenseigene Android Enterprise-Geräte mit Arbeitsprofil in Intune registrieren.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 7/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: shthilla
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9a19a78002d0655cf63a8b757ea252fb8992603f
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915261"
---
# <a name="set-up-intune-enrollment-of-android-enterprise-corporate-owned-devices-with-work-profile"></a>Einrichten der Intune-Registrierung für unternehmenseigene Android Enterprise-Geräte mit Arbeitsprofil

Unternehmenseigene Android Enterprise-Geräte mit Arbeitsprofil sind Einzelbenutzergeräte, die für die geschäftliche und private Benutzung vorgesehen sind.

Endbenutzer können ihre arbeitsbezogenen und persönlichen Daten getrennt halten und erhalten die Garantie, dass ihre persönlichen Daten und Anwendungen privat bleiben. Administratoren können einige Einstellungen und Features für das gesamte Gerät steuern, darunter:

- Festlegen der Anforderungen für das Gerätekennwort
- Steuern von Bluetooth und Datenroaming
- Konfigurieren des Schutzes vor Zurücksetzung auf Werkseinstellungen

Intune unterstützt Sie beim Bereitstellen von Apps und Einstellungen für unternehmenseigene Android Enterprise-Geräte mit Arbeitsprofil. Ausführliche Informationen über Android Enterprise finden Sie in den [Voraussetzungen für Android Enterprise](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012).

## <a name="device-requirements"></a>Geräteanforderungen

Geräte müssen die folgenden Anforderungen erfüllen, um als unternehmenseigene Android Enterprise-Geräte mit Arbeitsprofil verwaltet werden zu können:

- Android-Version 8.0 und höher
- Geräte müssen eine Android-Verteilung ausführen, die über GMS-Konnektivität (Google Mobile Services) verfügt. Geräte müssen über GMS verfügen und dazu in der Lage sein, eine Verbindung mit GMS herzustellen.

## <a name="set-up-android-enterprise-corporate-owned-work-profile-device-management"></a>Einrichten der Verwaltung für unternehmenseigene Android Enterprise-Geräte mit Arbeitsprofil

Führen Sie die folgenden Schritte aus, um die Verwaltung für unternehmenseigene Android Enterprise-Geräte mit Arbeitsprofil einzurichten:

1. Sie müssen [**Microsoft Intune** als MDM-Autorität (mobile Geräteverwaltung) festlegen](../fundamentals/mdm-authority-set.md), um die Verwaltung von mobilen Geräten vorzubereiten. Sie legen dieses Element nur einmal fest, wenn Sie die Ersteinrichtung von Intune für die Verwaltung mobiler Geräte durchführen.
2. [Verknüpfen Sie Ihr Intune-Mandantenkonto mit Ihrem verwalteten Google Play-Konto](connect-intune-android-enterprise.md).
3. [Erstellen Sie ein Registrierungsprofil](#create-an-enrollment-profile).
4. [Erstellen Sie eine Gerätegruppe](#create-a-device-group).
5. [Registrieren Sie die unternehmenseigenen Geräte mit Arbeitsprofil.](#enroll-the-corporate-owned-work-profile-devices)

### <a name="create-an-enrollment-profile"></a>Erstellen eines Anmeldungsprofils

> [!NOTE]
> Token für unternehmenseigene Geräte mit Arbeitsprofil laufen nicht automatisch ab. Wenn ein Administrator sich entschließt, ein Token aufzuheben, wird das zugehörige Profil nicht unter **Geräte** > **Android** > **Android-Registrierung** > **Unternehmenseigene Geräte mit Arbeitsprofil (Vorschau)** angezeigt. Klicken Sie auf **Filter**, und aktivieren Sie die Kontrollkästchen für die beiden Richtlinienstatus „Aktiv“ und „Inaktiv“, um alle Profile anzuzeigen, die den Token „Aktiv“ und „Inaktiv“ zugeordnet sind. 

Sie müssen ein Registrierungsprofil erstellen, damit Benutzer unternehmenseigene Geräte mit Arbeitsprofil registrieren können. Wenn das Profil erstellt wird, wird ein Registrierungstoken (zufällige Zeichenfolge) und ein QR-Code bereitgestellt. Je nach Android-Betriebssystem und Version des Geräts können Sie entweder das Token oder den QR-Code zum [Registrieren des dedizierten Geräts](#enroll-the-corporate-owned-work-profile-devices) verwenden.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an, und navigieren Sie zu **Geräte** > **Android** > **Android-Registrierung** > **Unternehmenseigene Geräte mit Arbeitsprofil (Vorschau)** .
2. Klicken Sie auf **Profil erstellen**, und füllen Sie die Felder aus.
    - **Name:** Geben Sie einen Namen ein, den Sie zum Zuweisen des Profils zu einer dynamischen Gerätegruppe verwenden.
    - **Beschreibung:** Fügen Sie eine Profilbeschreibung hinzu (optional).
3. Wählen Sie **Weiter** aus.
5. Klicken Sie auf der Seite **Überprüfen + erstellen** auf **Erstellen**, um das Profil zu erstellen.

### <a name="create-a-device-group"></a>Erstellen einer Gerätegruppe

Sie können Apps und Richtlinien auf zugewiesene oder dynamische Gerätegruppen ausrichten. Sie können dynamische Azure AD-Gerätegruppen konfigurieren, um Geräte, die mit einem bestimmten Registrierungsprofil registriert werden, automatisch einzufügen, indem Sie die folgenden Schritte ausführen:

1. Melden Sie sich im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an, und navigieren Sie zu **Gruppen** > **Alle Gruppen** > **Neue Gruppe**.
2. Füllen Sie auf dem Blatt **Gruppe** die erforderlichen Felder wie folgt aus:
    - **Gruppentyp**: Sicherheit
    - **Gruppenname**: Geben Sie einen aussagekräftigen Namen ein (z.B. Factory 1-Geräte)
    - **Mitgliedschaftstyp**: Dynamisches Gerät
3. Klicken Sie auf **Dynamische Abfrage hinzufügen**.
4. Füllen Sie die Felder auf dem Blatt **Dynamische Mitgliedschaftsregeln** wie folgt aus:
    - **Regel für dynamische Mitgliedschaft hinzufügen**: Einfache Regel
    - **Geräte hinzufügen, wobei:** enrollmentProfileName
    - Klicken Sie im mittleren Feld auf **Ist gleich**.
    - Geben Sie im letzten Feld den Namen des Registrierungsprofils ein, das Sie zuvor erstellt haben.
    Weitere Informationen über Regeln für die dynamische Mitgliedschaft finden Sie unter [Regeln für eine dynamische Mitgliedschaft für Gruppen in Azure Active Directory](/azure/active-directory/users-groups-roles/groups-dynamic-membership). 
5. Klicken Sie auf **Abfrage hinzufügen** > **Erstellen**.

### <a name="revoke-tokens"></a>Widerrufen von Tokens

Sie können das Token bzw. den QR-Code sofort für ungültig erklären. Von diesem Zeitpunkt an kann das Token bzw. der QR-Code nicht mehr verwendet werden. Sie können diese Option verwenden, wenn Sie:
  - das Token bzw. den QR-Code versehentlich mit nicht autorisierten Personen geteilt haben
  - alle Registrierungen abgeschlossen haben und das Token bzw. den QR-Code nicht mehr benötigen

Das Widerrufen eines Tokens bzw. QR-Codes hat keine Auswirkungen auf Geräte, die bereits registriert sind.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an, und navigieren Sie zu **Geräte** > **Android** > **Android-Registrierung** > **Unternehmenseigene Geräte mit Arbeitsprofil (Vorschau)** .
2. Wählen Sie das Profil aus, mit dem Sie arbeiten möchten.
3. Klicken Sie auf **Token**.
5. Klicken Sie auf **Token widerrufen** > **Ja**, um das Token zu widerrufen.

## <a name="enroll-the-corporate-owned-work-profile-devices"></a>Registrieren von unternehmenseigenen Geräten mit Arbeitsprofil

Benutzer können nun [ihre unternehmenseigenen Geräte mit Arbeitsprofil registrieren](android-dedicated-devices-fully-managed-enroll.md).

> [!NOTE]
> Während der Registrierung eines unternehmenseigenen Geräts mit Arbeitsprofil wird die **Microsoft Intune**-App automatisch installiert.  Die App ist für die Registrierung erforderlich und kann nicht deinstalliert werden. 

## <a name="managing-apps-on-android-enterprise-corporate-owned-work-profile-devices"></a>Verwalten von Apps auf unternehmenseigenen Android Enterprise-Geräten mit Arbeitsprofil

Nur Apps, deren Zuweisungstyp [auf „Erforderlich“ festgelegt](../apps/apps-deploy.md#assign-an-app) ist, können auf unternehmenseigenen Android Enterprise-Geräten mit Arbeitsprofil installiert werden. Apps werden über den verwalteten Google Play Store auf die gleiche Weise installiert wie bei Android Enterprise-Arbeitsprofilgeräten.

Apps werden auf verwalteten Geräten automatisch aktualisiert, wenn der App-Entwickler ein Update auf Google Play veröffentlicht.

Sie können eine der folgenden Aktionen durchführen, um eine App von unternehmenseigenen Android Enterprise-Geräten mit Arbeitsprofil zu entfernen:
- Löschen Sie die erforderliche App-Bereitstellung.
- Erstellen Sie eine Deinstallationsdatei für die App.

## <a name="next-steps"></a>Nächste Schritte
- [Bereitstellen von Android-Apps](../apps/apps-deploy.md)
- [Hinzufügen von Android-Konfigurationsrichtlinien](../configuration/device-profiles.md)