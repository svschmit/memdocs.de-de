---
title: 'Verwendung von Vorlagen für Windows 10-Geräte in Microsoft Intune: Azure | Microsoft-Dokumentation'
description: Verwenden Sie administrative Vorlagen in Microsoft Intune und Endpoint Manager, um eine Vielzahl von Einstellungen für Windows 10-Geräte zu erstellen. Verwenden Sie diese Einstellungen in einem Gerätekonfigurationsprofil, um Office-Programme und Microsoft Edge zu konfigurieren, Funktionen in Internet Explorer zu sichern, den Zugriff auf OneDrive zu kontrollieren, Remotedesktopfunktionen zu verwenden, AutoPlay zu aktivieren, Energieverwaltungseinstellungen festzulegen, HTTP-Druck und unterschiedliche Anmeldeoptionen zu verwenden und die Größe des Ereignisprotokolls festzulegen.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 04/15/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f609ec62259deffb220c8ee935d0f10a98ae77b5
ms.sourcegitcommit: 0e62655fef7afa7b034ac11d5f31a2a48bf758cb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/29/2020
ms.locfileid: "82254893"
---
# <a name="use-windows-10-templates-to-configure-group-policy-settings-in-microsoft-intune"></a>Verwenden von Windows 10-Vorlagen zum Konfigurieren von Gruppenrichtlinieneinstellungen in Microsoft Intune

Wenn Sie Geräte in Ihrer Organisation verwalten, sollten Sie auch Einstellungen erstellen, die dann auf unterschiedliche Gerätegruppen angewendet werden. Nehmen Sie beispielsweise an, dass Sie über mehrere Gerätegruppen verfügen. Sie sollten Gruppe A mehrere bestimmte Einstellungen zuweisen. Gruppe B soll andere Einstellungen erhalten. Ihre Einstellungen sollen in einer einfachen, konfigurierbaren Ansicht angezeigt werden.

Sie können diese Aufgabe mithilfe der **administrativen Vorlagen** in Microsoft Intune erledigen. Die administrativen Vorlagen enthalten Hunderte Einstellungen, die Funktionen in Microsoft Edge Version 77 und höher, Internet Explorer, Microsoft Office-Programmen, Remotedesktop und OneDrive sowie die Verwendung von Kennwörtern und PINs u.v.m. kontrollieren können. Diese Einstellungen ermöglichen Gruppenadministratoren das Verwalten von Gruppenrichtlinien mithilfe der Cloud.

Diese Funktion gilt für:

- Windows 10 und höher

Die Windows-Einstellungen ähneln den Einstellungen für Gruppenrichtlinienobjekte in Active Directory (AD). Diese Einstellungen sind in Windows integriert und sind [durch ADMX unterstützte Einstellungen](https://docs.microsoft.com/windows/client-management/mdm/understanding-admx-backed-policies), die XML verwenden. Die Office- und Microsoft Edge-Einstellungen sind in ADMX erfasst und verwenden die ADMX-Einstellungen in [administrativen Office-Vorlagendateien](https://www.microsoft.com/download/details.aspx?id=49030) und [administrativen Microsoft Edge-Vorlagendateien](https://www.microsoftedgeinsider.com/enterprise). Die Intune-Vorlagen sind außerdem vollständig cloudbasiert. Sie bieten eine einfache und unkomplizierte Möglichkeit, die Einstellungen zu konfigurieren und die Einstellungen zu suchen, die Sie nutzen möchten.

**Administrative Vorlagen** sind in Intune integriert, einschließlich der Verwendung des OMA-URI, und erfordern keine weiteren Anpassungen. Als Bestandteil Ihrer Lösung für die mobile Geräteverwaltung (Mobile Device Management, MDM) verwenden Sie diese Vorlageneinstellungen als Anlaufstelle, um Ihre Windows 10-Geräte zu verwalten.

In diesem Artikel sind die Schritte zum Erstellen einer Vorlage für Windows 10-Geräte aufgeführt. Zudem wird erläutert, wie alle verfügbaren Einstellungen in Intune gefiltert werden können. Wenn Sie die Vorlage erstellen, wird ein Gerätekonfigurationsprofil erstellt. Sie können dieses Profil dann Windows 10-Geräten in Ihrer Organisation zuweisen oder für diese bereitstellen.

## <a name="before-you-begin"></a>Vorbereitung

- Einige dieser Einstellungen sind ab Windows 10, Version 1709 (RS2/Build 15063), verfügbar. Einige Einstellungen sind nicht in allen Windows-Editionen enthalten. Um optimale Ergebnisse zu erzielen, wird empfohlen, Windows 10 Enterprise, Version 1903 (19H1/Build 18362) oder höher, zu verwenden.

- In den Windows-Einstellungen werden [Windows-Richtlinien-CSPs](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies) verwendet. Die CSPs funktionieren unter verschiedenen Windows-Editionen, z. B. Home, Professional, Enterprise. Wenn Sie herausfinden möchten, ob ein CSP unter einer bestimmten Edition funktioniert, klicken Sie auf [Windows-Richtlinien-CSPs](https://docs.microsoft.com/windows/client-management/mdm/policy-configuration-service-provider#policies-supported-by-group-policy-and-admx-backed-policies).

## <a name="create-the-template"></a>Vorlage erstellen

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.
3. Geben Sie die folgenden Eigenschaften ein:

    - **Plattform**: Wählen Sie **Windows 10 und höher** aus.
    - **Profil**: Wählen Sie **Administrative Vorlagen** aus.

4. Wählen Sie **Erstellen** aus.
5. Geben Sie in **Grundlagen** die folgenden Eigenschaften ein:

    - **Name:** Geben Sie einen aussagekräftigen Namen für das Profil ein. Benennen Sie Ihre Profile, damit Sie diese später leicht wiedererkennen. Ein guter Profilname ist beispielsweise **Administratorvorlage: Windows 10-Administratorvorlage, mit der XYZ-Einstellungen in Microsoft Edge konfiguriert werden**.
    - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.

6. Wählen Sie **Weiter** aus.

7. Konfigurieren Sie in **Konfigurationseinstellungen** Einstellungen für das Gerät (**Computerkonfiguration**) und Einstellungen, die für Benutzer **(Benutzerkonfiguration**) gelten:

    > [!div class="mx-imgBorder"]
    > ![Anwenden von ADMX-Vorlageneinstellungen auf Benutzer und Geräte in Microsoft Intune Endpoint Manager](./media/administrative-templates-windows/administrative-templates-choose-computer-user-configuration.png)

8. Wenn Sie **Computerkonfiguration** auswählen, werden die Einstellungskategorien angezeigt. Sie können eine beliebige Kategorie auswählen, um die verfügbaren Einstellungen anzuzeigen.

    Wählen Sie z. B. **Computerkonfiguration** > **Windows-Komponenten** > **Internet Explorer** aus, um alle Geräteeinstellungen anzuzeigen, die für Internet Explorer gelten:

    > [!div class="mx-imgBorder"]
    > ![Alle Geräteeinstellungen anzeigen, die für Internet Explorer in Microsoft Intune Endpoint Manager gelten](./media/administrative-templates-windows/administrative-templates-all-internet-explorer-settings-device.png)

9. Sie können auch **Alle Einstellungen** auswählen, um alle Geräteeinstellungen anzuzeigen. Scrollen Sie nach unten, um die Pfeile „Zurück“ und „Vor“ zur Anzeige weiterer Einstellungen zu verwenden:

    > [!div class="mx-imgBorder"]
    > ![Liste mit Beispieleinstellungen und Verwendung des Zurück- und Weiter-Pfeils](./media/administrative-templates-windows/administrative-templates-sample-settings-list.png)

10. Wählen Sie eine beliebige Einstellung aus. Filtern Sie beispielsweise nach **Office**, und wählen Sie **Eingeschränktes Browsing aktivieren** aus. Es wird eine detaillierte Beschreibung der Einstellung angezeigt. Wählen Sie **Aktiviert** oder **Deaktiviert** aus, oder übernehmen Sie die Standardeinstellung **Nicht konfiguriert**. In der detaillierten Beschreibung wird erläutert, was geschieht, wenn Sie **Aktiviert**, **Deaktiviert** oder **Nicht konfiguriert** auswählen.

    > [!TIP]
    > Die Windows-Einstellungen in Intune korrelieren mit dem lokalen Gruppenrichtlinienpfad, der im Editor für lokale Gruppenrichtlinien (`gpedit`) angezeigt wird.

11. Klicken Sie auf **OK**, um die Änderungen zu speichern.

    Gehen Sie die Liste der Einstellungen durch, und konfigurieren Sie die gewünschten Einstellungen für Ihre Umgebung. Hier sind einige Beispiele:

    - Verwenden Sie die Einstellung **Einstellungen für VBA-Makrobenachrichtigungen**, um VBA-Makros in verschiedenen Microsoft Office-Programmen zu verarbeiten, einschließlich in Word und Excel.
    - Verwenden Sie die Einstellung **Dateidownloads zulassen**, um Downloads von Internet Explorer zuzulassen oder zu verhindern.
    - Verwenden Sie **Kennwort anfordern, wenn ein Computer reaktiviert wird (Netzbetrieb)** , um Benutzer aufzufordern, ein Kennwort einzugeben, sobald das Gerät wieder aktiviert und der Energiesparmodus beendet wird.
    - Verwenden Sie die Einstellung **Download von unsignierten ActiveX-Steuerelementen**, um das Herunterladen unsignierter ActiveX-Steuerelemente aus Internet Explorer für Benutzer zu blockieren.
    - Verwenden Sie die Einstellung **Systemwiederherstellung deaktivieren**, um Benutzern zu erlauben oder sie daran zu hindern, eine Systemwiederherstellung auf dem Gerät auszuführen.
    - Verwenden Sie die Einstellung **Allow importing of favorites** (Importieren von Favoriten zulassen), um Benutzern das Importieren von Favoriten aus anderen Browsern in Microsoft Edge zu erlauben oder zu blockieren.
    - Und vieles mehr!

12. Wählen Sie **Weiter** aus.
13. Weisen Sie in **Bereichstags** (optional) ein Tag zu, um das Profil nach bestimmten IT-Gruppen wie `US-NC IT Team` oder `JohnGlenn_ITDepartment` zu filtern. Weitere Informationen zu Bereichstags finden Sie unter [Verwenden der RBAC und von Bereichstags für verteilte IT](..//fundamentals/scope-tags.md).

    Wählen Sie **Weiter** aus.

14. Wählen Sie unter **Zuweisungen** die Benutzer oder Gruppen aus, denen das Profil zugewiesen werden soll. Weitere Informationen zum Zuweisen von Profilen finden Sie unter [Zuweisen von Benutzer- und Geräteprofilen](device-profile-assign.md).

    Wenn das Profil Benutzergruppen zugeordnet ist, gelten die konfigurierten ADMX-Einstellungen für jedes Gerät, das der Benutzer registriert und bei dem er sich anmeldet. Wenn das Profil Gerätegruppen zugeordnet ist, gelten die konfigurierten ADMX-Einstellungen für jeden Benutzer, der sich bei diesem Gerät anmeldet. Diese Zuweisung erfolgt, wenn die ADMX-Einstellung eine Computerkonfiguration (`HKEY_LOCAL_MACHINE`) oder eine Benutzerkonfiguration (`HKEY_CURRENT_USER`) ist. Bei einigen Einstellungen kann sich eine einem Benutzer zugewiesene Computereinstellung auch auf die Erfahrung anderer Benutzer mit diesem Gerät auswirken.
    
    Weitere Informationen finden Sie unter [Benutzer- und Gerätegruppen im Vergleich](device-profile-assign.md#user-groups-vs-device-groups).

    Wählen Sie **Weiter** aus.

15. Überprüfen Sie die Einstellungen unter **Überprüfen + erstellen**. Wenn Sie auf **Erstellen** klicken, werden die Änderungen gespeichert, und das Profil wird zugewiesen. Die Richtlinie wird auch in der Profilliste angezeigt.

Wenn das Gerät das nächste Mal nach Konfigurationsupdates sucht, werden die von Ihnen konfigurierten Einstellungen angewendet.

## <a name="find-some-settings"></a>Suchen von Einstellungen

In diesem Vorlagen sind Hunderte von Einstellungen verfügbar. Nutzen Sie die integrierten Funktionen, um bestimmte Einstellungen einfacher zu finden:

- Wählen Sie in der Vorlage die Spalte **Einstellungen**, **Status**, **Einstellungstyp** oder **Pfad** aus, um die Liste entsprechend zu sortieren. Wenn Sie beispielsweise die Spalte **Pfad** auswählen, werden alle Einstellungen im `Microsoft Excel`-Pfad angezeigt:

- Verwenden Sie das **Suchfeld** in Ihrer Vorlage, um nach bestimmten Einstellungen zu suchen. Sie können eine Suche nach Einstellung oder Pfad durchführen. Suchen Sie beispielsweise nach `copy`. Es werden alle Einstellungen mit `copy` angezeigt:

  > [!div class="mx-imgBorder"]
  > ![Suchen Sie nach „copy“, um in den administrativen Vorlagen in Intune alle Geräteeinstellungen anzuzeigen.](./media/administrative-templates-windows/search-copy-settings.png) 

  Suchen Sie in einem anderen Beispiel nach `microsoft word`. Es werden die Einstellungen angezeigt, die Sie für das Microsoft Word-Programm festlegen können. Suchen Sie nach `explorer`, um die Internet Explorer-Einstellungen anzuzeigen, die Sie Ihrer Vorlage hinzufügen können.

## <a name="next-steps"></a>Nächste Schritte

Die Vorlage ist nun erstellt, führt aber vielleicht noch keine Aktionen durch. [Weisen Sie anschließend die Vorlage (auch Profil genannt) zu](device-profile-assign.md), und [überwachen Sie deren Status](device-profile-monitor.md).

Aktualisieren Sie [Office 365 mithilfe administrativer Vorlagen](administrative-templates-update-office.md).

[Tutorial: Verwenden der Cloud zum Konfigurieren einer Gruppenrichtlinie für Windows 10-Geräte mit ADMX-Vorlagen und Microsoft Intune](tutorial-walkthrough-administrative-templates.md)
