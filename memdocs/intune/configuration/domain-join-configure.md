---
title: Domänenbeitritts-Profileinstellungen für Windows 10 in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Erstellen Sie ein Gerätekonfigurationsprofil für den Domänenbeitritt für in Hybrid-Azure AD eingebundene Geräte. Verwenden Sie dieses Profil zum Bereitstellen von Informationen zur lokalen Active Directory-Domäne auf Geräten, die mit Windows Autopilot und Microsoft Intune bereitgestellt wurden.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 211722a02183d3b86525468f907d4093331d9de6
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988432"
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

    - **Plattform**: Wählen Sie **Windows 10 und höher** aus.
    - **Profil**: Wählen Sie **Domänenbeitritt (Vorschau)** aus.

4. Wählen Sie **Erstellen** aus.
5. Geben Sie in **Grundlagen** die folgenden Eigenschaften ein:

    - **Name:** Geben Sie einen aussagekräftigen Namen für die Richtlinie ein. Benennen Sie Ihre Richtlinien so, dass Sie diese später leicht wiedererkennen. Ein guter Richtlinienname ist beispielsweise **Windows 10: Domänenbeitrittsprofil mit lokalen Domäneninformationen zum Registrieren von in Hybrid-Azure AD eingebundenen Geräten mit Windows Autopilot**.
    - **Beschreibung:** Geben Sie eine Beschreibung für die Richtlinie ein. Diese Einstellung ist optional, wird jedoch empfohlen.

6. Wählen Sie **Weiter** aus.
7. Geben Sie in den **Konfigurationseinstellungen** die folgenden Eigenschaften ein:

    - **Computernamenspräfix:** Geben Sie ein Präfix für den Gerätenamen ein. Computernamen sind 15 Zeichen lang. Nach dem Präfix werden die verbleibenden 15 Zeichen zufällig generiert.
    - **Domänenname:** Geben Sie die FQDNs (vollqualifizierten Domänennamen) der einzubindenden Geräte ein. Geben Sie beispielsweise `americas.corp.contoso.com.` ein.
    - **Organisationseinheit** (Optional): Geben Sie den vollständigen Pfad ([Distinguished Name](https://docs.microsoft.com/windows/win32/ad/object-names-and-identities#distinguished-name)) in die Organisationseinheit (OE) der zu erstellenden Computerkonten ein. Geben Sie beispielsweise `"CN=Users,DC=Contoso,DC=com"` ein. Wenn Sie keinen Wert eingeben, wird ein bekannter Container für Computerobjekte verwendet.

      Weitere Informationen und Tipps zu dieser Einstellung finden Sie unter [Bereitstellen von in Hybrid-Azure AD eingebundene Geräte](../enrollment/windows-autopilot-hybrid.md).

8. Wählen Sie **Weiter** aus.

9. Weisen Sie in **Bereichstags** (optional) ein Tag zu, um das Profil nach bestimmten IT-Gruppen wie `US-NC IT Team` oder `JohnGlenn_ITDepartment` zu filtern. Weitere Informationen zu Bereichstags finden Sie unter [Verwenden der RBAC und von Bereichstags für verteilte IT](../fundamentals/scope-tags.md).

    Wählen Sie **Weiter** aus.

10. Wählen Sie unter **Zuweisungen** die Benutzer oder Benutzergruppen aus, denen Ihr Profil zugewiesen werden soll. Weitere Informationen zum Zuweisen von Profilen finden Sie unter [Zuweisen von Benutzer- und Geräteprofilen](device-profile-assign.md).

    Wählen Sie **Weiter** aus.

11. Überprüfen Sie die Einstellungen unter **Überprüfen + erstellen**. Wenn Sie auf **Erstellen** klicken, werden die Änderungen gespeichert, und das Profil wird zugewiesen. Die Richtlinie wird auch in der Profilliste angezeigt.

Sie können nun [in Hybrid-Azure AD eingebundene Geräte mithilfe von Intune und Windows Autopilot bereitstellen](../enrollment/windows-autopilot-hybrid.md).

## <a name="next-steps"></a>Nächste Schritte

[Überwachen Sie den Profilstatus](device-profile-monitor.md), [nachdem das Profil zugewiesen wurde](device-profile-assign.md).

[Bereitstellen von in Hybrid-Azure AD eingebundenen Geräten mit Intune und Windows Autopilot](../enrollment/windows-autopilot-hybrid.md)
