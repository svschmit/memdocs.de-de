---
title: Windows 10-Education-Einstellungen in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Hier finden Sie eine Liste aller Education-Einstellungen für Windows 10-Geräte. Verwenden Sie diese Einstellungen in einem Gerätekonfigurationsprofil mit der „Take a Test“-App, wählen Sie aus, mit welcher Methode Benutzer oder Kursteilnehmer sich anmelden, überwachen Sie den Bildschirm während des Tests, und nehmen Sie Weiteres in Intune vor.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/03/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 6f4de4bd-3dde-4a8d-8e22-46c5d06c3eea
ms.reviewer: kakyker
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2c6648f66c585dac5b8913fdb13adfcb98cbf927
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88912694"
---
# <a name="configure-the-take-a-test-app-on-windows-10-devices-using-intune"></a>Konfigurieren der „Take a Test“-App für Windows 10-Geräte mit Intune

Mit der Prüfungs-App können Sie Onlinetests auf den Windows 10-Geräten in Ihrem Klassenzimmer sicher verwalten. Wenn Sie die Prüfungs-App einrichten möchten, müssen Sie ein Gerätekonfigurationsprofil in Intune einrichten und Einstellungen für die sichere Bewertung konfigurieren. In diesem Artikel werden die Einstellungen der Prüfungs-App beschrieben. 

Nachdem Sie das Profil konfiguriert haben, weisen Sie es zu, und stellen Sie es für Ihre Kursteilnehmer bereit. 

[Konfigurieren von Einstellungen für Bildungseinrichtungen für Windows 10 in Microsoft Intune](education-settings-configure.md) bietet weitere Informationen zu dieser Funktion.

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen Sie eine Gerätekonfigurationsprofil.](education-settings-configure.md#create-a-device-profile)

## <a name="take-a-test-settings"></a>„Take a Test“-Einstellungen

- **Kontotyp**: Wählen Sie aus, wie Benutzer sich für den Test anmelden können. Folgende Optionen sind verfügbar:
  - Azure AD-Konto
  - Domänenkonto
  - Lokales Konto
  - Lokales Gastkonto: Nur auf Geräten mit Windows 10, Version 1903 und höher verfügbar
- **Kontobenutzername**: Geben Sie den Benutzernamen des Kontos ein, das mit der „Take a Test“-App verwendet wird. Sie können die Konten im folgenden Format eingeben:
  - `user@contoso.com`
  - `domain\username`
  - `user@contoso.com`
  - `computerName\username`
- **Kontoname**: Wenn Sie ein lokales Gastkonto einrichten möchten, geben Sie den Namen des Kontos ein, das mit der Prüfungs-App verwendet wird. Der Kontoname wird als Kachel auf dem Anmeldebildschirm angezeigt. Die Kursteilnehmer können auf die Kachel klicken, um den Test zu starten.  
- **Bewertungs-URL**: Geben Sie die URL des Tests an, den Benutzer ausführen sollen. Weitere Informationen zum Abrufen der URL finden Sie in der [„Take a Test“-Dokumentation](/education/windows/take-tests-in-windows-10).
- **Druckerverbindung:** **Anfordern** lässt nur von mit einem Drucker verbundenen Geräten aus Zugriff auf die Prüfungs-App zu. Diese Einstellung macht auch die Schaltfläche „Drucken“ der App für die Testkandidaten verfügbar. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem kann standardmäßig zulassen, dass Kursteilnehmer von Geräten aus auf die App zugreifen können, die nicht mit einem Drucker verbunden sind.  
- **Bildschirmüberwachung**: **Zulassen** überwacht die Bildschirmaktivität, während Benutzer einen Test ausführen. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem kann standardmäßig verhindern, dass Sie den Bildschirm während des Tests überwachen.
- **Textvorschläge:** Wählen Sie **Zulassen** aus, damit Testteilnehmer Textvorschläge sehen können. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Das Betriebssystem kann Textvorschläge standardmäßig blockieren, während Benutzer einen Test ausführen.

## <a name="next-steps"></a>Nächste Schritte

[Weisen Sie das Profil zu](device-profile-assign.md), und [überwachen Sie dessen Status](device-profile-monitor.md).

Weitere Informationen zur [Prüfungs-App](education-settings-configure.md).