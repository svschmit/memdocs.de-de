---
title: Hinzufügen oder Konfigurieren von Education-Einstellungen in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Verwenden Sie die „Take a Test“-App in einem Gerätekonfigurationsprofil für Geräte auf Windows 10 und höher in Microsoft Intune. Erstellen Sie ein Konfigurationsprofil mithilfe der Education-Einstellungen, und geben Sie eine Test-App-URL ein; wählen Sie aus, wie Benutzer sich anmelden, überwachen Sie den Bildschirm während des Tests, und lassen Sie Textvorschläge während des Tests zu, oder verhindern Sie sie.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 6f4de4bd-3dde-4a8d-8e22-46c5d06c3eea
ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 52eae65e6735ad655c2e8db53e34383ccc5e3b30
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988388"
---
# <a name="use-the-take-a-test-app-on-windows-10-devices-in-microsoft-intune"></a>Verwenden der „Take a Test“-App für Windows 10-Geräte in Microsoft Intune

Education-Profile in Intune sind dafür konzipiert, dass Kursteilnehmer einen Test oder eine Prüfung auf Geräten absolvieren. Dieses Feature umfasst die **Take a Test**-App und Einstellungen zum Hinzufügen einer Test-URL, das Auswählen der Methode, mit der Endbenutzer sich bei dem Test anmelden, und Sonstiges. Dieses Feature unterstützt die folgende Plattform:

- Windows 10 und höher

Wenn der Benutzer sich anmeldet, wird die „Take a Test“-App automatisch mit dem Test geöffnet, den Sie eingegeben haben. Keine anderen Apps können auf dem Gerät ausgeführt werden, während der Test ausgeführt wird. [Durchführen von Prüfungen in Windows 10](https://docs.microsoft.com/education/windows/take-tests-in-windows-10) enthält weitere Details zur „Take a Test“-App.

In diesem Artikel sind die Schritte zum Erstellen eines Gerätekonfigurationsprofil in Microsoft Intune aufgelistet. Darüber hinaus enthält er Informationen zum Lesen und Lernen der verfügbaren Education-Einstellungen für Ihre Windows 10-Geräte.

## <a name="create-a-device-profile"></a>Erstellen eines Geräteprofils

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.
3. Geben Sie die folgenden Eigenschaften ein:

    - **Plattform**: Wählen Sie **Windows 10 und höher** aus.
    - **Profil**: Wählen Sie **Sicheres Assessment (Education)** aus.

4. Wählen Sie **Erstellen** aus.
5. Geben Sie in **Grundlagen** die folgenden Eigenschaften ein:

    - **Name:** Geben Sie einen aussagekräftigen Namen für das neue Profil ein.
    - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.

6. Wählen Sie **Weiter** aus.
7. Geben Sie unter **Konfigurationseinstellungen** die Einstellungen ein, die Sie konfigurieren möchten:

    - [Windows 10 und höher](education-settings-windows.md)

8. Wählen Sie **Weiter** aus.

9. Weisen Sie in **Bereichstags** (optional) ein Tag zu, um das Profil nach bestimmten IT-Gruppen wie `US-NC IT Team` oder `JohnGlenn_ITDepartment` zu filtern. Weitere Informationen zu Bereichstags finden Sie unter [Verwenden der RBAC und von Bereichstags für verteilte IT](../fundamentals/scope-tags.md).

    Wählen Sie **Weiter** aus.

10. Wählen Sie unter **Zuweisungen** die Benutzer oder Benutzergruppen aus, denen Ihr Profil zugewiesen werden soll. Weitere Informationen zum Zuweisen von Profilen finden Sie unter [Zuweisen von Benutzer- und Geräteprofilen](device-profile-assign.md).

    Wählen Sie **Weiter** aus.

11. Überprüfen Sie die Einstellungen unter **Überprüfen + erstellen**. Wenn Sie auf **Erstellen** klicken, werden die Änderungen gespeichert, und das Profil wird zugewiesen. Die Richtlinie wird auch in der Profilliste angezeigt.

Wenn die Geräte das nächste Mal einchecken, wird die Richtlinie angewendet.

## <a name="next-steps"></a>Nächste Schritte

Lesen Sie eine Liste mit den [Education-Einstellungen für Windows 10](education-settings-windows.md) und deren Beschreibungen.

[Überwachen Sie den Profilstatus](device-profile-monitor.md), [nachdem das Profil zugewiesen wurde](device-profile-assign.md).
