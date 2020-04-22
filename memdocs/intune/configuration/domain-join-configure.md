---
title: Domänenbeitritts-Profileinstellungen für Windows 10 in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Erstellen Sie ein Gerätekonfigurationsprofil für den Domänenbeitritt für in Hybrid-Azure AD eingebundene Geräte. Verwenden Sie dieses Profil zum Bereitstellen von Informationen zur lokalen Active Directory-Domäne auf Geräten, die mit Windows Autopilot und Microsoft Intune bereitgestellt wurden.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 207b3983c214ad4e166ae58ea0ccd18ea23bf418
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79364395"
---
# <a name="configuration-domain-join-settings-for-hybrid-azure-ad-joined-devices-in-microsoft-intune"></a>Konfigurieren von Domänenbeitrittseinstellungen für in Hybrid-Azure AD eingebundene Geräte in Microsoft Intune

Viele Umgebungen verwenden lokale Active Directory-Domänen (AD). Wenn in AD-Domänen eingebundene Geräte auch in Azure AD eingebunden werden, werden diese als in Hybrid-Azure AD eingebundene Geräte bezeichnet. Mithilfe von Windows Autopilot können Sie [in Hybrid-Azure AD eingebundene Geräte in Intune registrieren](../enrollment/windows-autopilot-hybrid.md). Für die Registrierung benötigen Sie außerdem ein Konfigurationsprofil für den **Domänenbeitritt**.

Ein Konfigurationsprofil für den **Domänenbeitritt** enthält Informationen zur lokalen Active Directory-Domäne. Wenn Geräte bereitgestellt werden (und in der Regel offline sind), dieses Profil stellt die AD-Domänendetails bereit, damit Geräten mitgeteilt wird, welche lokale Domäne eingebunden werden soll. Wenn Sie kein Domänenbeitrittsprofil erstellen, schlägt die Bereitstellung dieser Geräte möglicherweise fehl.

Diese Funktion gilt für:

- Windows 10 und höher
- In Hybrid-Azure AD eingebundene Geräte
- Hybridbereitstellung mit Autopilot und Intune

In diesem Artikel wird veranschaulicht, wie Sie ein Domänenbeitrittsprofil für eine Autopilot-Hybridbereitstellung erstellen. Sie können außerdem die verfügbaren Einstellungen anzeigen.

## <a name="create-the-profile"></a>Erstellen des Profils

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.
3. Geben Sie die folgenden Eigenschaften ein:

    - **Name:** Geben Sie einen aussagekräftigen Namen für die Richtlinie ein. Benennen Sie Ihre Richtlinien so, dass Sie diese später leicht wiedererkennen. Ein guter Richtlinienname ist beispielsweise **Windows 10: Domänenbeitrittsprofil mit lokalen Domäneninformationen zum Registrieren von in Hybrid-Azure AD eingebundenen Geräten mit Windows Autopilot**.
    - **Beschreibung:** Geben Sie eine Beschreibung für die Richtlinie ein. Diese Einstellung ist optional, wird jedoch empfohlen.
    - **Plattform**: Wählen Sie **Windows 10 und höher** aus.
    - **Profiltyp**: Wählen Sie **Domänenbeitritt (Vorschau)** aus.

4. Wählen Sie **Einstellungen** aus. Geben Sie die folgenden Eigenschaften ein:

    - **Computernamenspräfix:** Geben Sie ein Präfix für den Gerätenamen ein. Computernamen sind 15 Zeichen lang. Nach dem Präfix werden die verbleibenden 15 Zeichen zufällig generiert.
    - **Domänenname:** Geben Sie die FQDNs (vollqualifizierten Domänennamen) der einzubindenden Geräte ein. Geben Sie beispielsweise `americas.corp.contoso.com.` ein.
    - **Organisationseinheit** (Optional): Geben Sie den vollständigen Pfad ([Distinguished Name](https://docs.microsoft.com/windows/win32/ad/object-names-and-identities#distinguished-name)) in die Organisationseinheit (OE) der zu erstellenden Computerkonten ein. Geben Sie beispielsweise `"CN=Users,DC=Contoso,DC=com"` ein. Wenn Sie keinen Wert eingeben, wird ein bekannter Container für Computerobjekte verwendet.

      Weitere Informationen und Tipps zu dieser Einstellung finden Sie unter [Bereitstellen von in Hybrid-Azure AD eingebundene Geräte](../enrollment/windows-autopilot-hybrid.md).

5. Wenn Sie fertig sind, wählen Sie **OK** > **Erstellen** aus, um Ihre Änderungen zu speichern.

Das Profil wird erstellt und in der Profilliste angezeigt. Sie können nun [in Hybrid-Azure AD eingebundene Geräte mithilfe von Intune und Windows Autopilot bereitstellen](../enrollment/windows-autopilot-hybrid.md).

## <a name="next-steps"></a>Nächste Schritte

Nachdem das Profil erstellt wurde, kann es zugewiesen werden. Die nächsten Schritte sind das [Zuweisen von Benutzer- und Geräteprofilen in Microsoft Intune](device-profile-assign.md) und das [Überwachen von Geräteprofilen in Microsoft Intune](device-profile-monitor.md).

[Bereitstellen von in Hybrid-Azure AD eingebundenen Geräten mit Intune und Windows Autopilot](../enrollment/windows-autopilot-hybrid.md)
