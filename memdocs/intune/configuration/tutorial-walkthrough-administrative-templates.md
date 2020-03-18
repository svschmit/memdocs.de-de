---
title: 'Exemplarische Vorgehensweise: Erstellen von administrativen Vorlagen in Microsoft Intune – Azure | Microsoft-Dokumentation'
description: In diesem Tutorial bzw. dieser exemplarischen Vorgehensweise wird Microsoft Intune verwendet, um Office-, Windows- und Microsoft Edge-ADMX-Vorlagen auf Geräten mit Windows 10 und höher zu konfigurieren.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 02/18/2020
ms.topic: tutorial
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: ''
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 936634a26dee315c7ad452ac408f9cc0eac00dfe
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79343270"
---
# <a name="tutorial-use-the-cloud-to-configure-group-policy-on-windows-10-devices-with-admx-templates-and-microsoft-intune"></a>Tutorial: Verwenden der Cloud zum Konfigurieren einer Gruppenrichtlinie für Windows 10-Geräte mit ADMX-Vorlagen und Microsoft Intune

> [!NOTE]
> Dieses Tutorial wurde als technischer Workshop für die Microsoft Ignite erstellt. Es hat mehr Voraussetzungen als normale Tutorials, da das Verwenden und Konfigurieren von ADMX-Richtlinien in Intune und lokal verglichen wird.

Administrative Vorlagen für Gruppenrichtlinien (auch als ADMX-Vorlagen bezeichnet) umfassen Einstellungen, die Sie auf Windows 10-Geräten, einschließlich PCs, konfigurieren können. Die Einstellungen für ADMX-Vorlagen sind in verschiedenen Diensten verfügbar. Diese Einstellungen werden von MDM-Anbietern (Verwaltung mobiler Geräte) verwendet, darunter auch Microsoft Intune. Sie können beispielsweise in PowerPoint Designideen aktivieren, eine Startseite in Microsoft Edge festlegen, ActiveX-Steuerelemente in Internet Explorer blockieren und vieles mehr.

ADMX-Vorlagen sind für die folgenden Dienste verfügbar:

- **Microsoft Edge**: Download unter [Microsoft Edge-Richtliniendatei](https://www.microsoftedgeinsider.com/en-us/enterprise)
- **Office:** Download unter [Office 365 ProPlus, Office 2019 und Office 2016](https://www.microsoft.com/download/details.aspx?id=49030)
- **Windows**: In das Betriebssystem Windows 10 integriert

Weitere Informationen zu ADMX-Richtlinien finden Sie unter [Grundlegendes zu durch ADMX unterstützten Richtlinien](https://docs.microsoft.com/windows/client-management/mdm/understanding-admx-backed-policies).

In Microsoft Intune sind diese Vorlagen in den Intune-Dienst integriert und als Profile unter **Administrative Vorlagen** verfügbar. In diesem Profil konfigurieren Sie die Einstellungen, die dieses Profil umfassen soll, und weisen es dann Ihren Geräten zu.

Inhalt des Tutorials:

> [!div class="checklist"]
> * Lernen Sie das [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) kennen.
> * Erstellen Sie Benutzergruppen und Gerätegruppen.
> * Vergleichen Sie die Einstellungen in Intune mit lokalen ADMX-Einstellungen.
> * Erstellen Sie verschiedene administrative Vorlagen, und konfigurieren Sie die Einstellungen für die verschiedenen Gruppen.

Am Ende dieses Labs werden Sie mit Intune und Microsoft 365 Ihre Benutzer verwalten und administrative Vorlagen bereitstellen können.

Diese Funktion gilt für:

- Windows 10, Version 1703 und höher

## <a name="prerequisites"></a>Voraussetzungen

- Ein Abonnement für Microsoft 365 E3 oder E5, in dem Intune und Azure Active Directory (AD) Premium enthalten sind, ist erforderlich. Sollten Sie kein E3- oder E5-Abonnement haben, [können Sie ein kostenloses Testabonnement abschließen](https://docs.microsoft.com/office365/admin/try-or-buy-microsoft-365?view=o365-worldwide).

  Weitere Informationen dazu, was in den verschiedenen Microsoft 365-Lizenzen enthalten ist, finden Sie unter [Mit Microsoft 365 zum digitalen Unternehmen](https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans).

- Microsoft Intune ist als **Intune-MDM-Autorität** konfiguriert. Weitere Informationen finden Sie unter [Festlegen der Autorität für die Verwaltung mobiler Geräte](../fundamentals/mdm-authority-set.md).

  > [!div class="mx-imgBorder"]
  > ![Festlegen von Microsoft Intune als MDM-Autorität im Mandantenstatus](./media/tutorial-walkthrough-administrative-templates/tenant-status.png)

- Bei einem lokalen Active Directory-Domänencontroller (DC):

  1. Kopieren Sie die folgenden Office- und Microsoft Edge-Vorlagen in den [zentralen Speicher (Ordner SYSVOL)](https://support.microsoft.com/help/3087759/how-to-create-and-manage-the-central-store-for-group-policy-administra):

      - [Administrative Vorlagen für Office](https://www.microsoft.com/download/details.aspx?id=49030)
      - [Administrative Vorlagen für Microsoft Edge > Richtliniendatei](https://www.microsoftedgeinsider.com/en-us/enterprise)

  2. Erstellen Sie eine Gruppenrichtlinie, um diese Vorlagen auf einem Windows 10 Enterprise-Administratorcomputer in derselben Domäne wie der Domänencontroller abzulegen. In diesem Tutorial:

      - heißt die mit diesen Vorlagen erstellte Gruppenrichtlinie **OfficeandEdge**. Diesen Namen werden Sie auf den Bildern sehen.
      - wird der verwendete Windows 10 Enterprise-Administratorcomputer als **Administratorcomputer** bezeichnet.

      In manchen Organisationen haben Domänenadministratoren zwei Konten: ein normales Domänengeschäftskonto und ein separates Domänenadministratorkonto, das nur für Domänenadministratoraufgaben wie Gruppenrichtlinien verwendet wird.

      Auf diesem **Administratorcomputer** können sich Administratoren mit ihrem Domänenadministratorkonto anmelden und auf Tools zum Verwalten von Gruppenrichtlinien zugreifen.

- Auf diesem **Administratorcomputer**:

  - Melden Sie sich mit einem Domänenadministratorkonto an.

  - Installieren Sie **RSAT: Tools für die Gruppenrichtlinienverwaltung**:

    1. Öffnen Sie die App **Einstellungen** > **Apps** > **Optionale Features** > **Add feature** (Feature hinzufügen).
    2. Klicken Sie auf **RSAT: Tools für die Gruppenrichtlinienverwaltung** > **Installieren**.

        Warten Sie, während Windows das Feature installiert. Sobald die Installation abgeschlossen ist, wird es in der App **Windows-Verwaltungsprogramme** angezeigt.

        > [!div class="mx-imgBorder"]
        > ![App „Windows-Verwaltungsprogramme“ mit der App „Gruppenrichtlinienverwaltung“](./media/tutorial-walkthrough-administrative-templates/windows-administrative-tools-app.png)

  - Stellen Sie sicher, dass Sie über Internetzugriff verfügen sowie über Administratorrechte für das Microsoft 365-Abonnement, in dem das Endpoint Manager Admin Center enthalten ist.

## <a name="open-the-endpoint-manager-admin-center"></a>Öffnen des Endpoint Manager Admin Centers

1. Öffnen Sie einen Chromium-Webbrowser, z. B. Microsoft Edge Version 77 und höher.
2. Navigieren Sie zum [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) (https://devicemanagement.microsoft.com). Melden Sie sich mit dem folgenden Konto an:

    **Benutzer:** Geben Sie das Administratorkonto Ihres Microsoft 365-Mandantenabonnements ein.  
    **Kennwort:** Geben Sie das entsprechende Kennwort ein.

Das Admin Center ist hauptsächlich auf Geräteverwaltung ausgelegt und umfasst Azure-Dienste wie Azure AD und Intune. Auch wenn Sie möglicherweise kein **Azure Active Directory**- oder **Intune**-Branding sehen, verwenden Sie dennoch diese Dienste.

Sie können das Endpoint Manager Admin Center auch aus dem [Microsoft 365 Admin Center](https://admin.microsoft.com) heraus öffnen:

1. Wechseln Sie zu [https://admin.microsoft.com](https://admin.microsoft.com).
2. Melden Sie sich mit dem Administratorkonto Ihres Microsoft 365-Mandantenabonnements an.
3. Klicken Sie unter **Admin Center** auf **Alle Admin Center** > **Endpoint management** (Endpunktverwaltung). Das Endpoint Manager Admin Center wird geöffnet.

    > [!div class="mx-imgBorder"]
    > ![Alle Admin Center im Microsoft 365 Admin Center](./media/tutorial-walkthrough-administrative-templates/microsoft365-admin-centers.png)

## <a name="create-groups-and-add-users"></a>Gruppen erstellen und Benutzer hinzufügen

Lokale Richtlinien werden in der Reihenfolge LSDOU (lokal, Standort, Domäne und Organisationseinheit) angewendet. In dieser Hierarchie überschreiben OE-Richtlinien lokale Richtlinien, Domänenrichtlinien Standortrichtlinien usw.

In Intune werden Richtlinien auf Benutzer und von Ihnen erstellte Gruppen angewendet. Es gibt keine Hierarchie. Wenn in zwei Richtlinien dieselbe Einstellung aktualisiert wird, wird diese Einstellung als Konflikt angezeigt. Wenn zwei Konformitätsrichtlinien miteinander in Konflikt stehen, gilt die restriktivere Richtlinie. Wenn zwei Konfigurationsprofile miteinander in Konflikt stehen, wird die Einstellung nicht angewendet. Weitere Informationen finden Sie unter [Häufige Fragen, Probleme und entsprechende Behebungen mit Geräterichtlinien und -profilen in Microsoft Intune](device-profile-troubleshoot.md#if-multiple-policies-are-assigned-to-the-same-user-or-device-how-do-i-know-which-settings-gets-applied).

In den folgenden Schritten werden Sie Sicherheitsgruppen erstellen und Benutzer zu diesen Gruppen hinzufügen. Sie können Benutzer zu mehreren Gruppen hinzufügen. So ist es beispielsweise normal, dass ein Benutzer mehrere Geräte hat, z. B. ein Surface Pro für die Arbeit und ein mobiles Android-Gerät für den Privatgebrauch. In der Regel greifen diese Personen dann auch über ihre verschiedenen Geräte auf Organisationsressourcen zu.

1. Klicken Sie im Endpoint Manager Admin Center auf **Gruppen** > **Neue Gruppe**.

2. Legen Sie folgende Einstellungen fest:

    - **Gruppentyp**: Klicken Sie auf **Sicherheit**.
    - **Gruppenname**: Geben Sie **Alle Geräte von Studenten mit Windows 10** ein.
    - **Mitgliedschaftstyp**: Klicken Sie auf **Zugewiesen**.

3. Klicken Sie auf **Members** (Mitglieder) und fügen Sie Geräte hinzu.

    Das Hinzufügen von Geräten ist optional. Ziel ist es, das Erstellen von Gruppen zu üben und zu wissen, wie Geräte hinzugefügt werden. Seien Sie vorsichtig, wenn Sie dieses Tutorial in einer Produktionsumgebung verwenden.

4. Klicken Sie auf **Auswählen** > **Erstellen**, um die Änderungen zu speichern.

    Wird Ihre Gruppe nicht angezeigt? Klicken Sie auf **Aktualisieren**.

5. Klicken Sie auf **Neue Gruppe**, und geben Sie die folgenden Einstellungen ein:

    - **Gruppentyp**: Klicken Sie auf **Sicherheit**.
    - **Gruppenname**: Geben Sie **Alle Windows-Geräte** ein.
    - **Mitgliedschaftstyp**: Klicken Sie auf **Dynamisches Gerät**.
    - **Dynamische Gerätemitglieder:** Konfigurieren Sie Ihre Abfrage:

        - **Eigenschaft**: Klicken Sie auf **deviceOSType**.
        - **Operator:** Klicken Sie auf **ist gleich**.
        - **Wert:** Geben Sie **Windows** ein.

        1. Klicken Sie auf **Ausdruck hinzufügen**. Ihr Ausdruck wird nun in der **Regelsyntax** angezeigt:

            > [!div class="mx-imgBorder"]
            > ![Erstellen einer dynamischen Abfrage und Hinzufügen eines Ausdrucks zu einer administrativen Vorlage in Microsoft Intune](./media/tutorial-walkthrough-administrative-templates/dynamic-group-query.png)

            Benutzer oder Geräte, auf die die von Ihnen eingegebenen Kriterien zutreffen, werden automatisch zu den dynamischen Gruppen hinzugefügt. In diesem Beispiel werden Geräte automatisch zu dieser Gruppe hinzugefügt, wenn ihr Betriebssystem Windows ist. Seien Sie vorsichtig, wenn Sie dieses Tutorial in einer Produktionsumgebung verwenden. Ziel ist es, das Erstellen von dynamischen Gruppen zu üben.

        2. Klicken Sie auf **Speichern** > **Erstellen**, um die Änderungen zu speichern.

6. Erstellen Sie die Gruppe **Alle Dozenten** mit den folgenden Einstellungen:

    - **Gruppentyp**: Klicken Sie auf **Sicherheit**.
    - **Gruppenname**: Geben Sie **Alle Dozenten** ein.
    - **Mitgliedschaftstyp**: Klicken Sie auf **Dynamischer Benutzer**.
    - **Dynamische Mitglieder:** Konfigurieren Sie Ihre Abfrage:

      - **Eigenschaft**: Klicken Sie auf **Abteilung**.
      - **Operator:** Klicken Sie auf **ist gleich**.
      - **Wert:** Geben Sie **Dozenten** ein.

        1. Klicken Sie auf **Ausdruck hinzufügen**. Ihr Ausdruck wird nun in der **Regelsyntax** angezeigt.

            Benutzer oder Geräte, auf die die von Ihnen eingegebenen Kriterien zutreffen, werden automatisch zu den dynamischen Gruppen hinzugefügt. In diesem Beispiel werden Benutzer automatisch zu dieser Gruppe hinzugefügt, wenn ihre Abteilung Dozenten ist. Sie können die Abteilung und andere Eigenschaften eingeben, wenn Benutzer zu Ihrer Organisation hinzugefügt werden. Seien Sie vorsichtig, wenn Sie dieses Tutorial in einer Produktionsumgebung verwenden. Ziel ist es, das Erstellen von dynamischen Gruppen zu üben.

        2. Klicken Sie auf **Speichern** > **Erstellen**, um die Änderungen zu speichern.

### <a name="talking-points"></a>Anmerkungen

- Dynamische Gruppen sind ein Feature in Azure AD Premium. Wenn Sie kein Azure AD Premium haben, können Sie mit Ihrer Lizenz nur zugewiesene Gruppen erstellen. Weitere Informationen zu dynamischen Gruppen finden Sie unter:

  - [Dynamische Gruppenmitgliedschaft in Azure Active Directory (Teil 1)](https://blogs.technet.microsoft.com/pauljones/2017/08/28/dynamic-group-membership-in-azure-active-directory-part-1/)
  - [Dynamische Gruppenmitgliedschaft in Azure Active Directory (Teil 2)](https://blogs.technet.microsoft.com/pauljones/2017/08/29/dynamic-group-membership-in-azure-active-directory-part-2/)

- Azure AD Premium umfasst weitere Dienste, die beim Verwalten von Apps und Geräten häufig verwendet werden, darunter [Multi-Factor Authentication (MFA)](https://docs.microsoft.com/azure/active-directory/authentication/concept-mfa-howitworks) und [bedingter Zugriff](https://docs.microsoft.com/azure/active-directory/conditional-access/overview).

- Viele Administratoren fragen, wann sie Benutzergruppen und wann Gerätegruppen verwenden sollen. Der Abschnitt [Benutzer- und Gerätegruppen im Vergleich](device-profile-assign.md#user-groups-vs-device-groups) kann Ihnen hierfür als Orientierung dienen.

- Denken Sie daran, dass ein Benutzer zu mehreren Gruppen gehören kann. Im Folgenden finden Sie einige weitere Beispiele für Gruppen, die Sie für dynamische Benutzer und Geräte erstellen können:

  - Alle Studenten
  - Alle Android-Geräte
  - Alle iOS-/iPadOS-Geräte
  - Marketing
  - Personalabteilung
  - Alle Mitarbeiter in Charlotte
  - Alle Mitarbeiter in Redmond
  - IT-Administratoren an der Westküste
  - IT-Administratoren an der Ostküste

Die erstellten Benutzer und Gruppen können auch im [Microsoft 365 Admin Center](https://admin.microsoft.com), in Azure AD im Azure-Portal und in [Microsoft Intune im Azure-Portal](https://go.microsoft.com/fwlink/?linkid=2090973) angezeigt werden. Sie können für Ihr Mandantenabonnement Gruppen in all diesen Bereichen erstellen und verwalten. **Wenn Ihr Ziel die Geräteverwaltung ist, verwenden Sie das [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).**

### <a name="review-group-membership"></a>Gruppenmitgliedschaft prüfen

1. Klicken Sie im Endpoint Manager Admin Center auf **Benutzer** und dann auf den Namen eines vorhanden Benutzers.

    > [!div class="mx-imgBorder"]
    > ![Im Endpoint Manager Admin Center auf „Benutzer“ klicken](./media/tutorial-walkthrough-administrative-templates/select-users-endpoint-manager-admin-center.png)

2. Überprüfen Sie Informationen, die Sie hinzufügen oder ändern können. Sehen Sie sich beispielsweise die Eigenschaften an, die Sie konfigurieren können, wie Position, Abteilung, Stadt, Bürostandort. Sie können diese Eigenschaften beim Erstellen von dynamischen Gruppen in Ihren dynamischen Abfragen verwenden.
3. Klicken Sie auf **Gruppen**, um die Mitgliedschaften dieses Benutzers zu sehen. Sie können den Benutzer auch aus einer Gruppe entfernen.
4. Klicken Sie auf ein paar der anderen Optionen, um weitere Informationen zu sehen und sich einen Überblick darüber zu verschaffen, was Sie alles tun können. Sehen Sie sich z. B. die zugewiesene Lizenz oder die Geräte des Benutzers an.

### <a name="what-did-i-just-do"></a>Abgeschlossene Aufgaben

Sie haben im Endpoint Manager Admin Center neue Sicherheitsgruppen erstellt und vorhandene Benutzer und Geräte zu diesen Gruppen hinzugefügt. Diese Gruppen werden Sie später in diesem Tutorial noch verwenden.

## <a name="create-a-template-in-intune"></a>Erstellen einer Vorlage in Intune

In diesem Abschnitt erstellen Sie eine administrative Vorlage in Intune und sehen sich Einstellungen in der **Gruppenrichtlinienverwaltung** an, die Sie dann mit den entsprechenden Einstellungen in Intune vergleichen. Ziel ist es, eine Einstellung im Tool „Gruppenrichtlinie“ und die entsprechende Einstellung in Intune anzuzeigen.

1. Klicken Sie im Endpoint Manager Admin Center auf **Geräte** > **Konfigurationsprofile** > **Profil erstellen**.
2. Geben Sie die folgenden Eigenschaften ein:

    - **Name:** Geben Sie einen aussagekräftigen Namen für das Profil ein. Benennen Sie Ihre Profile, damit Sie diese später leicht wiedererkennen. Geben Sie zum Beispiel **Administratorvorlage – Geräte von Studenten mit Windows 10** ein.
    - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.
    - **Plattform**: Wählen Sie **Windows 10 und höher** aus.
    - **Profiltyp**: Klicken Sie auf **Administrative Vorlagen**.

3. Wählen Sie **Erstellen** aus. Klicken Sie in der Dropdownliste **Kategorie auswählen** auf **Alle Produkte**. Es werden alle Einstellungen angezeigt. Sehen Sie sich in diesen Einstellungen die folgenden Eigenschaften an:

    - Der **Pfad** zur Richtlinie ist derselbe wie bei der Gruppenrichtlinienverwaltung oder GPEdit.
    - Die Einstellung gilt für Benutzer und Geräte.

### <a name="open-group-policy-management"></a>Öffnen der Gruppenrichtlinienverwaltung

In diesem Abschnitt sehen Sie sich eine Richtlinie in Intune und die entsprechende Richtlinie im Gruppenrichtlinienverwaltungs-Editor an.

#### <a name="compare-a-device-policy"></a>Vergleichen einer Geräterichtlinie

1. Öffnen Sie auf dem **Administratorcomputer** die App **Gruppenrichtlinienverwaltung**.

    Diese App installieren Sie mit **RSAT: Tools für die Gruppenrichtlinienverwaltung**. Dabei handelt es sich um ein optionales Feature, das unter Windows installiert wird. Die Schritte, die für die Installation erforderlich sind, finden Sie im Abschnitt [Voraussetzungen](#prerequisites) (in diesem Artikel).

2. Klappen Sie **Domänen** auf, und klicken Sie auf Ihre Domäne. Klicken Sie beispielsweise auf **contoso.net**.
3. Klicken Sie mit der rechten Maustaste auf die Richtlinie **OfficeandEdge**, und klicken Sie dann auf **Bearbeiten**. Dadurch wird die App „Gruppenrichtlinienverwaltungs-Editor“ geöffnet.

    > [!div class="mx-imgBorder"]
    > ![Rechtsklick auf die ADMX-Gruppenrichtlinie für Office und Edge und dann auf „Bearbeiten“](./media/tutorial-walkthrough-administrative-templates/open-group-policy-management.png)

    **OfficeandEdge** ist eine Gruppenrichtlinie, die die ADMX-Vorlagen für Office und Microsoft Edge umfasst. Diese Richtlinie wird im Abschnitt [Voraussetzungen](#prerequisites) (in diesem Artikel) beschrieben.

4. Klappen Sie **Computerkonfiguration** > **Richtlinien** > **Administrative Vorlagen** > **Systemsteuerung** > **Darstellung und Anpassung** auf. Sehen Sie sich die verfügbaren Einstellungen an.

    > [!div class="mx-imgBorder"]
    > ![Im Gruppenrichtlinienverwaltungs-Editor „Computerkonfiguration“ aufklappen und zu „Darstellung und Anpassung“ navigieren](./media/tutorial-walkthrough-administrative-templates/open-group-policy-management-editor-admx-policy.png)

    Doppelklicken Sie auf **Prevent enabling lock screen camera** (Aktivieren der Kamera auf dem Sperrbildschirm verhindern), und sehen Sie sich die verfügbaren Optionen an:

    > [!div class="mx-imgBorder"]
    > ![Verfügbare Einstellungen unter „Computerkonfiguration“ im Tool „Gruppenrichtlinie“ ansehen](./media/tutorial-walkthrough-administrative-templates/prevent-enabling-lock-screen-camera-admx-policy.png)

5. Navigieren Sie im Admin Center für die Geräteverwaltung zu Ihrer Vorlage **Administratorvorlage – Geräte von Studenten mit Windows 10**.
6. Klicken Sie in der Dropdownliste auf **Alle Produkte**, und suchen Sie nach **Darstellung und Anpassung**:

    > [!div class="mx-imgBorder"]
    > ![Suche nach „Darstellung und Anpassung“ in der administrativen Vorlage in Microsoft Intune](./media/tutorial-walkthrough-administrative-templates/search-personalization-administrative-template.png)

    Sehen Sie sich die verfügbaren Einstellungen an.

    Der Einstellungstyp ist **Gerät** und der Pfad ist **\Systemsteuerung\Darstellung und Anpassung**. Dieser Pfad ähnelt dem, was Sie soeben im Gruppenrichtlinienverwaltungs-Editor gesehen haben. Wenn Sie die Einstellung öffnen, sehen Sie die gleichen Optionen wie im Gruppenrichtlinienverwaltungs-Editor: **Nicht konfiguriert**, **Aktiviert** und **Deaktiviert**.

#### <a name="compare-a-user-policy"></a>Vergleichen einer Benutzerrichtlinie

1. Suchen Sie in Ihrer Administratorvorlage nach **InPrivate-Browsen**. Beachten Sie den Pfad und dass diese Einstellung für Benutzer und Geräte gilt.

2. Finden Sie die entsprechenden Einstellungen für Benutzer und Geräte im **Gruppenrichtlinienverwaltungs-Editor**:

    - Gerät: Klappen Sie **Computerkonfiguration** > **Richtlinien** > **Administrative Vorlagen** > **Windows-Komponenten** > **Internet Explorer** > **Datenschutz** > **InPrivate-Browsen deaktivieren** auf.
    - Benutzer: Klappen Sie **Benutzerkonfiguration** > **Richtlinien** > **Administrative Vorlagen** > **Windows-Komponenten** > **Internet Explorer** > **Datenschutz** > **InPrivate-Browsen deaktivieren** auf.

    > [!div class="mx-imgBorder"]
    > ![InPrivate-Browsen in Internet Explorer deaktivieren mithilfe einer ADMX-Vorlage](./media/tutorial-walkthrough-administrative-templates/group-policy-turn-off-inprivate-browsing.png)

> [!TIP]
> Sie können auch GPEdit (die App **Gruppenrichtlinie bearbeiten**) verwenden, um sich die integrierten Windows-Richtlinien anzusehen.

#### <a name="compare-an-edge-policy"></a>Vergleichen einer Edge-Richtlinie

1. Navigieren Sie im Admin Center für die Geräteverwaltung zu Ihrer Vorlage **Administratorvorlage – Geräte von Studenten mit Windows 10**.
2. Klicken Sie in der Dropdownliste auf **Microsoft Edge, Version 77 und höher**.
3. Suchen Sie nach **Start**. Sehen Sie sich die verfügbaren Einstellungen an.
4. Suchen Sie im Gruppenrichtlinienverwaltungs-Editor nach den folgenden Einstellungen:

    - Gerät: Klappen Sie **Computerkonfiguration** > **Richtlinien** > **Administrative Vorlagen** > **Microsoft Edge** > **Startup, homepage and new tab page** (Start, Startseite und neue Registerkartenseite) auf.
    - Benutzer: Klappen Sie **Benutzerkonfiguration** > **Richtlinien** > **Administrative Vorlagen** > **Microsoft Edge** > **Startup, homepage and new tab page** (Start, Startseite und neue Registerkartenseite) auf.

### <a name="what-did-i-just-do"></a>Abgeschlossene Aufgaben

Sie haben eine administrative Vorlage in Intune erstellt. In dieser Vorlage haben Sie sich ADMX-Einstellungen und die entsprechenden ADMX-Einstellungen in der Gruppenrichtlinienverwaltung angesehen.

## <a name="add-settings-to-the-students-admin-template"></a>Hinzufügen von Einstellungen zur Studenten-Administratorvorlage

In dieser Vorlage konfigurieren Sie bestimmte Internet Explorer-Einstellungen, um Geräte, die von mehreren Studenten genutzt werden, zu sperren.

1. Suchen Sie in Ihrer Vorlage **Administratorvorlage – Geräte von Studenten mit Windows 10** nach **InPrivate-Browsen deaktivieren**, und klicken Sie auf die Geräterichtlinie:

    > [!div class="mx-imgBorder"]
    > ![Geräterichtlinie „InPrivate-Browsen deaktivieren“ in einer administrativen Vorlage in Microsoft Intune](./media/tutorial-walkthrough-administrative-templates/turn-off-inprivate-browsing-administrative-template.png)

2. Sehen Sie sich in diesem Fenster die Beschreibung und die Werte an, die Sie festlegen können. Diese Optionen ähneln dem, was Sie im Tool „Gruppenrichtlinie“ sehen.
3. Klicken Sie auf **Aktiviert** > **OK**, um die Änderungen zu speichern.
4. Konfigurieren Sie außerdem die folgenden Internet Explorer-Einstellungen. Stellen Sie sicher, dass Sie auf **OK** klicken, um die Änderungen zu speichern.

    - **Ziehen und Ablegen oder Kopieren und Einfügen von Dateien zulassen**
      - **Typ:** Gerät
      - **Pfad:** \Windows-Komponenten\Internet Explorer\Internetsystemsteuerung\Sicherheitsseite\Internetzone
      - **Wert:** Deaktiviert

    - **Ignorieren von Zertifikatfehlern verhindern**
      - **Typ:** Gerät
      - **Pfad:** \Windows-Komponenten\Internet Explorer\Internetsystemsteuerung
      - **Wert:** Aktiviert

    - **Änderung der Homepage-Einstellungen deaktivieren**
      - **Typ:** Benutzer
      - **Pfad:** \Windows-Komponenten\Internet Explorer
      - **Wert:** Aktiviert
      - **Startseite:** Geben Sie eine URL ein, z. B. `contoso.com`.

5. Löschen Sie Ihren Suchfilter. Beachten Sie, dass sich die von Ihnen konfigurierten Einstellungen oben in der Liste befinden:

    > [!div class="mx-imgBorder"]
    > ![Konfigurierte Einstellungen befinden sich oben in der Liste in Microsoft Intune](./media/tutorial-walkthrough-administrative-templates/configured-settings-administrative-template.png)

### <a name="assign-your-template"></a>Vorlage zuweisen

1. Klicken Sie in Ihrer Vorlage auf **Zuweisungen**. Sie müssen möglicherweise Ihre Vorlage schließen und in der Liste **Geräte – Konfigurationsprofile** auswählen:

    > [!div class="mx-imgBorder"]
    > ![Profil Ihrer administrativen Vorlage in der Liste von Konfigurationsprofilen für Geräte in Microsoft Intune auswählen](./media/tutorial-walkthrough-administrative-templates/filter-administrative-template-device-configuration-profiles-list.png)

2. Klicken Sie auf **Wählen Sie die Gruppen aus, die eingeschlossen werden sollen.** Eine Liste der vorhandenen Benutzer und Gruppen wird angezeigt.
3. Klicken Sie auf die Gruppe **Alle Geräte von Studenten mit Windows 10**, die Sie vorhin erstellt haben, und dann auf **Auswählen**.

    Wenn Sie dieses Tutorial in einer Produktionsumgebung verwenden, wird empfohlen, leere Gruppen hinzuzufügen. Ziel ist es, das Zuweisen Ihrer Vorlage zu üben.

4. **Speichern** Sie die Änderungen.

Sobald das Profil gespeichert wurde, gilt es für die Geräte, sobald diese sich bei Intune einchecken. Wenn die Geräte mit dem Internet verbunden sind, kann dies sofort geschehen. Weitere Informationen zu den Aktualisierungszeiten von Richtlinien finden Sie unter [Wie lange dauert es, bis Geräte Richtlinien, Profile oder Apps nach ihrer Zuweisung abrufen?](device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

Denken Sie daran, sich nicht selbst auszusperren, wenn Sie strenge oder restriktive Richtlinien und Profile zuweisen. Es wird empfohlen, eine Gruppe zu erstellen, die von Ihren Richtlinien und Profilen ausgenommen ist. Diese Gruppe dient dazu, Zugriff zu haben, um Probleme behandeln zu können. Überwachen Sie diese Gruppe, um sicherzustellen, dass sie wie vorgesehen verwendet wird.

### <a name="what-did-i-just-do"></a>Abgeschlossene Aufgaben

Sie haben im Endpoint Manager Admin Center ein Gerätekonfigurationsprofil in Form einer administrativen Vorlage erstellt und dieses Profil einer von Ihnen erstellten Gruppe zugewiesen.

## <a name="create-a-onedrive-template"></a>Erstellen einer OneDrive-Vorlage

In diesem Abschnitt werden Sie in Intune eine Administratorvorlage für OneDrive erstellen, um bestimmte Einstellungen zu steuern. Diese Einstellungen wurden ausgewählt, da sie häufig von Organisationen verwendet werden.

1. Erstellen Sie ein weiteres Profil (**Geräte** > **Konfigurationsprofile** > **Profil erstellen**).

2. Geben Sie die folgenden Eigenschaften ein:

    - **Name:** Geben Sie **Administratorvorlage – OneDrive-Richtlinien, die für alle Windows 10-Benutzer gelten** ein.
    - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.
    - **Plattform**: Wählen Sie **Windows 10 und höher** aus.
    - **Profiltyp**: Klicken Sie auf **Administrative Vorlagen**.

3. Wählen Sie **Erstellen** aus.
4. Klicken Sie in der Dropdownliste auf **Office**.
5. **Aktivieren** Sie die folgenden Einstellungen. Stellen Sie sicher, dass Sie auf **OK** klicken, um die Änderungen zu speichern.

    - **Benutzer automatisch mit ihren Windows-Anmeldeinformationen beim OneDrive-Synchronisierungsclient anmelden**
    - **OneDrive-Dateien bei Bedarf verwenden**
    - **Benutzer an der Synchronisierung persönlicher OneDrive-Konten hindern**

Ihre Einstellungen sehen ähnlich aus wie die folgenden:

> [!div class="mx-imgBorder"]
> ![Erstellen einer Administratorvorlage für OneDrive in Microsoft Intune](./media/tutorial-walkthrough-administrative-templates/one-drive-administrative-template.png)

Weitere Informationen zu Einstellungen für den OneDrive-Client finden Sie unter [Verwenden von Gruppenrichtlinien zum Steuern der Einstellungen für die OneDrive-Synchronisierung](https://docs.microsoft.com/onedrive/use-group-policy).

### <a name="assign-your-template"></a>Vorlage zuweisen

1. Klicken Sie in Ihrer Vorlage auf **Zuweisungen**.
2. Klicken Sie auf **Wählen Sie die Gruppen aus, die eingeschlossen werden sollen.** Eine Liste der vorhandenen Benutzer und Gruppen wird angezeigt.
3. Klicken Sie auf die Gruppe **Alle Windows-Geräte**, die Sie vorhin erstellt haben, und dann auf **Auswählen**.

    Wenn Sie dieses Tutorial in einer Produktionsumgebung verwenden, wird empfohlen, leere Gruppen hinzuzufügen. Ziel ist es, das Zuweisen Ihrer Vorlage zu üben.

4. **Speichern** Sie die Änderungen.

Mittlerweile haben Sie einige administrative Vorlagen erstellt und von Ihnen erstellten Gruppen zugewiesen. Im nächsten Schritt erstellen Sie eine administrative Vorlage mit Windows PowerShell und der Microsoft Graph-API für Intune.

## <a name="optional-create-a-policy-using-powershell-and-graph-api"></a>Optional: Erstellen einer Richtlinie mit PowerShell und der Graph-API

In diesem Abschnitt werden die folgenden Ressourcen verwendet. Diese Ressourcen werden in diesem Abschnitt installiert.

- [Intune PowerShell-SDK](https://github.com/microsoft/Intune-PowerShell-SDK)
- [Microsoft Graph-API für Intune](https://docs.microsoft.com/graph/api/resources/intune-graph-overview?view=graph-rest-1.0)

1. Öffnen Sie auf dem **Administratorcomputer** **Windows PowerShell** als Administrator:

    1. Geben Sie in die Suchleiste **powershell** ein.
    2. Klicken Sie mit der rechten Maustaste auf **Windows PowerShell**, und klicken Sie dann auf **Als Administrator ausführen**.

    > [!div class="mx-imgBorder"]
    > ![Windows PowerShell als Administrator ausführen](./media/tutorial-walkthrough-administrative-templates/run-windows-powershell-administrator.png)

2. Rufen Sie die Ausführungsrichtlinie ab und legen Sie diese fest.

    1. Geben Sie `get-ExecutionPolicy` ein.

        Notieren Sie sich den festgelegten Wert, der möglicherweise **Restricted** (Eingeschränkt) ist. Setzen Sie nach Abschluss dieses Tutorials die Richtlinie wieder auf den ursprünglichen Wert zurück.

    2. Geben Sie `Set-ExecutionPolicy -ExecutionPolicy Unrestricted` ein.

    3. Geben Sie `Y` ein, um Änderungen vorzunehmen.

    Die Ausführungsrichtlinie von PowerShell hilft dabei, das Ausführen bösartiger Skripts zu verhindern. Weitere Informationen finden Sie unter [Informationen zu Ausführungsrichtlinien](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_execution_policies).

3. Geben Sie `Install-Module -Name Microsoft.Graph.Intune` ein.

    Geben Sie `Y` ein, wenn:

    - Sie gebeten werden, den NuGet-Anbieter zu installieren.
    - Sie gebeten werden, die Module aus einem nicht vertrauenswürdigen Repository zu installieren.

    Die Ausführung kann mehrere Minuten dauern. Sobald sie abgeschlossen ist, wird eine ähnliche Aufforderung wie die folgende angezeigt:

    > [!div class="mx-imgBorder"]
    > ![Aufforderung in Windows PowerShell nach Installation eines Moduls](./media/tutorial-walkthrough-administrative-templates/powershell-prompt.png)

4. Navigieren Sie in Ihrem Webbrowser zu [https://github.com/Microsoft/Intune-PowerShell-SDK/releases](https://github.com/Microsoft/Intune-PowerShell-SDK/releases), und klicken Sie auf die Datei **Intune-PowerShell-SDK_v6.1907.00921.0001.zip**.

    1. Klicken Sie auf **Speichern unter**, und wählen Sie einen Ordner aus, den Sie sich merken können. `c:\psscripts` ist eine gute Wahl.
    2. Öffnen Sie Ihren Ordner, klicken Sie mit der rechten Maustaste auf die ZIP-Datei, und klicken Sie dann auf **Alle extrahieren** > **Extrahieren**. Ihre Ordnerstruktur sieht dann ähnlich aus wie der folgende Ordner:

        > [!div class="mx-imgBorder"]
        > ![Ordnerstruktur für das Intune PowerShell-SDK nach dem Extrahieren](./media/tutorial-walkthrough-administrative-templates/psscripts-directory.png)

5. Aktivieren Sie in der Registerkarte **Ansicht** **Dateinamenerweiterungen**:

    > [!div class="mx-imgBorder"]
    > ![Dateinamenerweiterungen in der Registerkarte „Ansicht“ im Explorer aktivieren](./media/tutorial-walkthrough-administrative-templates/file-names-extension.png)

6. Navigieren Sie in Ihrem Ordner zu `c:\psscripts\Intune-PowerShell-SDK_v6.1907.00921.0001\drop\outputs\build\Release\net471`. Klicken Sie mit der rechten Maustaste auf alle DLL-Dateien, und klicken Sie dann auf **Eigenschaften** > **Unblock** (Zulassen).

    > [!div class="mx-imgBorder"]
    > ![Zulassen der DLL-Dateien](./media/tutorial-walkthrough-administrative-templates/unblock-dll.png)

7. Geben Sie in der App **Windows PowerShell** Folgendes ein:

    ```powershell
    Import-Module c:\psscripts\Intune-PowerShell-SDK_v6.1907.00921.0001\drop\outputs\build\Release\net471\Microsoft.Graph.Intune.psd1
    ```

    Geben Sie `R` ein, wenn Sie dazu aufgefordert werden, Dateien eines nicht vertrauenswürdigen Herausgebers auszuführen.

8. Administrative Vorlagen in Intune verwenden die Betaversion von Graph:

    1. Geben Sie `Update-MSGraphEnvironment -SchemaVersion 'beta'` ein.

    2. Geben Sie `Connect-MSGraph -AdminConsent` ein.

    3. Melden Sie sich mit demselben Microsoft 365-Administratorkonto an, wenn Sie dazu aufgefordert werden. Durch diese Cmdlets wird die Richtlinie in Ihrer Mandantenorganisation erstellt.

        **Benutzer:** Geben Sie das Administratorkonto Ihres Microsoft 365-Mandantenabonnements ein.  
        **Kennwort:** Geben Sie das entsprechende Kennwort ein.

    4. Klicken Sie auf **Accept** (Akzeptieren).

9. Erstellen Sie ein Konfigurationsprofil namens **Testkonfiguration**. Eingeben:

    ```powershell
    $configuration = Invoke-MSGraphRequest -Url https://graph.microsoft.com/beta/deviceManagement/groupPolicyConfigurations -Content '{"displayName":"Test Configuration","description":"A test configuration created through PS"}' -HttpMethod POST
    ```

    Wenn diese Cmdlets erfolgreich ausgeführt werden, wird das Profil erstellt. Navigieren Sie zum Endpoint Manager Admin Center > **Konfigurationsprofile**, um dies zu überprüfen. Ihr Profil **Testkonfiguration** sollte in der Liste zu finden sein.

10. Rufen Sie alle Einstellungsdefinitionen ab. Eingeben:

    ```powershell
    $settingDefinitions = Invoke-MSGraphRequest -Url https://graph.microsoft.com/beta/deviceManagement/groupPolicyDefinitions -HttpMethod GET
    ```

11. Suchen Sie die Definitions-ID mithilfe des Anzeigenamens der Einstellung. Eingeben:

    ```powershell
    $desiredSettingDefinition = $settingDefinitions.value | ? {$_.DisplayName -Match "Silently sign in users to the OneDrive sync client with their Windows credentials"}
    ```

12. Konfigurieren Sie eine Einstellung. Eingeben:

    ```powershell
    $configuredSetting = Invoke-MSGraphRequest -Url "https://graph.microsoft.com/beta/deviceManagement/groupPolicyConfigurations('$($configuration.id)')/definitionValues" -Content ("{""enabled"":""true"",""configurationType"":""policy"",""definition@odata.bind"":""https://graph.microsoft.com/beta/deviceManagement/groupPolicyDefinitions('$($desiredSettingDefinition.id)')""}") -HttpMethod POST
    ```

    ```powershell
    Invoke-MSGraphRequest -Url "https://graph.microsoft.com/beta/deviceManagement/groupPolicyConfigurations('$($configuration.id)')/definitionValues('$($configuredSetting.id)')" -Content ("{""enabled"":""false""}") -HttpMethod PATCH
    ```

    ```powershell
    $configuredSetting = Invoke-MSGraphRequest -Url "https://graph.microsoft.com/beta/deviceManagement/groupPolicyConfigurations('$($configuration.id)')/definitionValues('$($configuredSetting.id)')" -HttpMethod GET
    ```

### <a name="see-your-policy"></a>Ansehen Ihrer Richtlinie

1. Klicken Sie im Endpoint Manager Admin Center auf **Konfigurationsprofile** > **Aktualisieren**.
2. Klicken Sie auf Ihr Profil **Testkonfiguration** > **Einstellungen**.
3. Klicken Sie in der Dropdownliste auf **Alle Produkte**.

Sie werden sehen, dass die Einstellung **Benutzer automatisch mit ihren Windows-Anmeldeinformationen beim OneDrive-Synchronisierungsclient anmelden** konfiguriert wurde.

## <a name="policy-best-practices"></a>Best Practices für Richtlinien

Beim Erstellen von Richtlinien und Profilen in Intune sind bestimmte Empfehlungen und Best Practices zu berücksichtigen. Weitere Informationen finden Sie unter [Empfehlungen](device-profile-create.md#recommendations).

## <a name="clean-up-resources"></a>Bereinigen der Ressourcen

Wenn Sie diese nicht mehr benötigen, können Sie:

- Die von Ihnen erstellten Gruppen löschen:

  - **Alle Geräte von Studenten mit Windows 10**
  - **Alle Windows-Geräte**
  - **Alle Dozenten**

- Die von Ihnen erstellten Administratorvorlagen löschen:

  - **Administratorvorlage – Geräte von Studenten mit Windows 10**
  - **Administratorvorlage – OneDrive-Richtlinien, die für alle Windows 10-Benutzer gelten**
  - **Testkonfiguration**

- Setzen Sie die PowerShell-Ausführungsrichtlinie auf ihren ursprünglichen Wert zurück. Im folgenden Beispiel wird die Ausführungsrichtlinie zurück auf „Restricted“ (Eingeschränkt) gesetzt.

  ```powershell
  Set-ExecutionPolicy -ExecutionPolicy Restricted
  ```

## <a name="next-steps"></a>Nächste Schritte

In diesem Tutorial haben Sie sich weiter mit dem [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) vertraut gemacht, mithilfe des Abfragegenerators dynamische Gruppen erstellt und in Intune administrative Vorlagen zum Konfigurieren von [ADMX-Einstellungen](https://docs.microsoft.com/windows/client-management/mdm/understanding-admx-backed-policies) erstellt. Außerdem haben Sie die lokale Verwendung von ADMX-Vorlagen mit der Verwendung in der Cloud mit Intune verglichen. Darüber hinaus haben Sie mithilfe von PowerShell-Cmdlets eine administrative Vorlage erstellt.

Weitere Informationen zu administrativen Vorlagen in Intune finden Sie unter:

> [!div class="nextstepaction"]
> [Verwenden von Windows 10-Vorlagen zum Konfigurieren von Gruppenrichtlinieneinstellungen in Microsoft Intune](administrative-templates-windows.md)
