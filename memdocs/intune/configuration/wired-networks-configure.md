---
title: 'Konfigurieren der 802.1x-Einstellungen für kabelgebundene Netzwerke für macOS-Geräte in Microsoft Intune: Azure | Microsoft-Dokumentation'
titleSuffix: ''
description: Erstellen Sie ein Gerätekonfigurationsprofil für das kabelgebundene Netzwerk für macOS-Desktopcomputergeräte, oder fügen Sie eines hinzu. Erfahren Sie mehr über die verschiedenen Einstellungen, das Hinzufügen von Zertifikaten sowie das Auswählen eines EAP-Typs und einer Authentifizierungsmethode in Microsoft Intune.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 06/11/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f237daa5e95cb5428e707828f0104c697e338718
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85095769"
---
# <a name="add-and-use-wired-networks-settings-on-your-macos-devices-in-microsoft-intune"></a>Hinzufügen und Verwenden von Einstellungen für kabelgebundene Netzwerke auf macOS-Geräten in Microsoft Intune

Kabelgebundene Netzwerke werden von vielen Organisationen verwendet, um Desktopcomputern den Netzwerkzugriff zu ermöglichen. Microsoft Intune umfasst integrierte Einstellungen, die für macOS-Benutzer und -Geräte in Ihrer Organisation bereitgestellt werden können. Diese Gruppe von Einstellungen wird als „Profil“ bezeichnet. In Ihrem Profil können Sie allgemeine Einstellungen einschließen. Dazu zählen beispielsweise die Netzwerkschnittstelle, akzeptierte EAP-Typen und Einstellungen für die Serververtrauensstellung.

Wenn das Profil bereit ist, kann es anderen Benutzern und Gruppen zugewiesen werden. Nach der Zuweisung können Ihre Benutzer Zugriff auf das kabelgebundene Netzwerk Ihrer Organisation erhalten, ohne es selbst zu konfigurieren.

Als Teil der Lösung für die mobile Geräteverwaltung (MDM) verwenden Sie dieses Feature, um 802.1x-Profile zu erstellen und somit die kabelgebundenen Netzwerke zu verwalten. Dann stellen Sie diese kabelgebundenen Netzwerke für Ihre macOS-Geräte zur Verfügung.

Diese Funktion gilt für:

- macOS

Sie verfügen beispielsweise über ein kabelgebundenes Netzwerk namens **Contoso wired network** (Kabelgebundenes Contoso-Netzwerk). Sie möchten alle macOS-Desktopgeräte so einrichten, dass sie sich mit diesem Netzwerk verbinden. Gehen Sie dazu folgendermaßen vor:

1. Erstellen Sie ein kabelgebundenes Netzwerkprofil, das die Einstellungen zum Herstellen einer Verbindung mit dem **Contoso wired network** (Kabelgebundenes Contoso-Netzwerk) umfasst.
2. Weisen Sie das Profil einer Gruppe zu, die alle macOS-Desktopcomputer der Benutzer enthält. Empfehlungen zum Verwenden von Gruppentypen finden Sie unter [Benutzer- und Gerätegruppen im Vergleich](device-profile-assign.md#user-groups-vs-device-groups).
3. Auf den Desktopcomputern finden Benutzer das **Contoso wired netzwork** (Kabelgebundenes Contoso-Netzwerk) in der Liste der Netzwerke. Sie können sich dann über die von Ihnen ausgewählte Authentifizierungsmethode mit dem Netzwerk verbinden.

In diesem Artikel sind die Schritte zum Erstellen eines kabelgebundenen Netzwerkprofils aufgelistet. Er enthält auch einen Link zu den Beschreibungen der unterschiedlichen Einstellungen.

## <a name="create-the-profile"></a>Erstellen des Profils

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.
3. Geben Sie die folgenden Eigenschaften ein:

    - **Plattform**: Klicken Sie auf **macOS**.
    - **Profil**: Klicken Sie auf **Kabelgebundenes Netzwerk**.

4. Wählen Sie **Erstellen** aus.
5. Geben Sie in **Grundlagen** die folgenden Eigenschaften ein:

    - **Name:** Geben Sie einen aussagekräftigen Namen für das Profil ein. Benennen Sie Ihre Profile, damit Sie diese später leicht wiedererkennen. Ein angemessener Profilname ist beispielsweise **Kabelgebundenes Netzwerkprofil für alle macOS-Geräte in der Organisation**.
    - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.

6. Wählen Sie **Weiter** aus.
7. Wählen Sie unter **Konfigurationseinstellungen** die Netzwerkschnittstelle des Netzwerks und den EAP-Typ (Extensible Authentication Protocol) aus. Eine Liste aller Einstellungen und ihrer Funktionen finden Sie unter:

    - [macOS](wired-network-settings-macos.md)

8. Wählen Sie **Weiter** aus.
9. Wählen Sie unter **Zuweisungen** die Benutzergruppen oder Gerätegruppen aus, denen das Profil zugewiesen werden soll. Weitere Informationen zum Zuweisen von Profilen finden Sie unter [Zuweisen von Benutzer- und Geräteprofilen](device-profile-assign.md).

    Wählen Sie **Weiter** aus.

10. Überprüfen Sie die Einstellungen unter **Überprüfen + erstellen**. Wenn Sie auf **Erstellen** klicken, werden die Änderungen gespeichert, und das Profil wird zugewiesen. Die Richtlinie wird auch in der Profilliste angezeigt.

> [!TIP]
> Wenn Sie die zertifikatbasierte Authentifizierung für Ihr kabelgebundenes Netzwerkprofil verwenden, stellen Sie das kabelgebundene Netzwerkprofil, das Zertifikatprofil und das vertrauenswürdige Stammprofil für dieselben Gruppen bereit. Mit dieser Bereitstellung wird sichergestellt, dass jedes Gerät die Rechtmäßigkeit Ihrer Zertifizierungsstelle erkennen kann. Weitere Informationen finden Sie unter [Verwenden von Zertifikaten zur Authentifizierung in Microsoft Intune](../protect/certificates-configure.md).

## <a name="next-steps"></a>Nächste Schritte

Das Profil ist nun erstellt, führt aber vielleicht keine Aktionen durch. Denken Sie daran, dieses [Profil zuzuweisen](device-profile-assign.md) und seinen [Status zu überwachen](device-profile-monitor.md).
