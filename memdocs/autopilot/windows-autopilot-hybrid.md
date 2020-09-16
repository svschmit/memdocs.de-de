---
title: Registrierung für Active Directory Hybrid-Geräte – Windows Autopilot
titleSuffix: ''
description: Verwenden Sie Windows Autopilot, um in Azure AD Hybrid eingebundene Geräte in Microsoft Intune zu registrieren.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/07/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 8518d8fa-a0de-449d-89b6-8a33fad7b3eb
ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
ms.custom: seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: b1580726640612325fd22ca1fa4ae55517036644
ms.sourcegitcommit: e533cdf8722156a66b1cc46f710def96587345d0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/15/2020
ms.locfileid: "90568594"
---
# <a name="deploy-hybrid-azure-ad-joined-devices-by-using-intune-and-windows-autopilot"></a>Bereitstellen von in Azure AD Hybrid eingebundenen Geräten mit Intune und Windows Autopilot
Sie können in Azure AD Hybrid eingebundene Geräte mithilfe von Intune und Windows Autopilot einrichten. Führen Sie dazu die Schritte in diesen Artikel durch.

## <a name="prerequisites"></a>Voraussetzungen

Konfigurieren Sie Ihre [Azure AD Hybrid-Geräte](/azure/active-directory/devices/hybrid-azuread-join-plan). Stellen Sie sicher, dass Sie [die Geräteregistrierung mithilfe des Cmdlets „Get-MsolDevice“ überprüfen](/azure/active-directory/devices/hybrid-azuread-join-managed-domains#verify-the-registration).

Das zu registrierende Gerät muss die folgenden Anforderungen erfüllen:
- Verwenden Sie Windows 10 v1809 oder höher.
- Sie haben Zugriff auf das Internet [nach den Netzwerk Anforderungen für Windows Autopilot](/windows/deployment/windows-autopilot/windows-autopilot-requirements#networking-requirements).
- Sie haben Zugriff auf einen Active Directory Domänen Controller. Das Gerät muss mit dem Netzwerk der Organisation verbunden sein, damit Folgendes möglich ist:
  - Auflösen Sie die DNS-Einträge für die AD-Domäne und den AD-Domänen Controller.
  - Kommunizieren Sie mit dem Domänen Controller, um den Benutzer zu authentifizieren.
- Pingen Sie den Domänen Controller der Domäne, der Sie beitreten möchten, erfolgreich.
- Bei Verwendung eines Proxys müssen WPAD-Proxyeinstellungen aktiviert und konfiguriert sein.
- Sie müssen eingerichtet worden sein.
- Verwenden Sie einen Autorisierungstyp, der von Azure Active Directory grundsätzlich unterstützt wird.

## <a name="set-up-windows-10-automatic-enrollment"></a>Einrichten der automatischen Registrierung von Windows 10

1. Melden Sie sich bei Azure an, und wählen Sie im linken Bereich **Azure Active Directory**  >  **Mobility-Microsoft InTune (MDM und MAM)** aus  >  **Microsoft Intune**.

2. Stellen Sie sicher, dass Benutzer, die mit InTune und Windows Azure AD verbundenen Geräten bereitstellen, Mitglieder einer Gruppe sind, die im **MDM-Benutzerbereich**enthalten ist.

    ![Der Bereich „Mobilität (MDM und MAM), Konfigurieren“](./media/windows-autopilot-hybrid/auto-enroll-scope.png)

3. Verwenden Sie die Standardwerte in den Feldern **URL zu den MDM-Nutzungsbedingungen**, **URL für MDM-Ermittlung** und **MDM Compliance-URL**, und klicken Sie dann auf **Speichern**.

## <a name="increase-the-computer-account-limit-in-the-organizational-unit"></a>Erhöhen des Kontolimits für den Computer in der Organisationseinheit

Der Intune-Connector für Active Directory erstellt Computer mit Registrierung per Autopilot in der lokalen Active Directory-Domäne. Der Hostcomputer des Intune-Connectors muss über die Berechtigung verfügen, die Computerobjekte innerhalb der Domäne zu erstellen. 

In einigen Domänen werden den Computern keine Rechte zum Erstellen von Computern erteilt. Darüber hinaus verfügen Domänen über ein integriertes Limit (Standardeinstellung: 10), das für alle Benutzer und Computer gilt, denen keine Berechtigungen zum Erstellen von Computerobjekten gewährt wurden. Die Rechte müssen an Computer delegiert werden, auf denen der InTune-Connector in der Organisationseinheit gehostet wird, in der Hybrid Azure AD eingebundenen Geräten erstellt werden.

Die Organisationseinheit, der die Berechtigung zum Erstellen von Computern gewährt wird, muss mit Folgendem übereinstimmen:
- Mit der Organisationseinheit, die im Domänenbeitrittsprofil eingetragen ist
- Mit dem Domänennamen des Computers für Ihre Domäne, wenn kein Profil ausgewählt ist

1. Öffnen Sie **Active Directory-Benutzer und -Computer** („DSA.msc“).

2. Klicken Sie mit der rechten Maustaste auf die Organisationseinheit, die verwendet werden soll, um Hybrid Azure AD verbundene Computer > **delegatsteuerung**zu erstellen

    ![Menübefehl „Delegate Control...“ (Objektverwaltung zuweisen...)](./media/windows-autopilot-hybrid/delegate-control.png)

3. Wählen Sie im Assistenten zum Zuweisen der **Objektverwaltung** die Optionen **Weiter** > **Hinzufügen...**  > **Objekttypen** aus.

4. Wählen Sie im Bereich **Objekttypen** die Option **Computer**  >  **OK**aus.

    ![Bereich „Object Types“ (Objekttypen)](./media/windows-autopilot-hybrid/object-types-computers.png)

5. Geben Sie im Bereich zur Auswahl von **Benutzern, Computern oder Gruppen** im Feld **Geben Sie die zu verwenden Objektnamen ein** den Namen des Computers ein, auf dem der Connector installiert ist.

    ![Bereich „Select Users, Computers, or Groups“ (Benutzer, Computer oder Gruppen auswählen)](./media/windows-autopilot-hybrid/enter-object-names.png)

6. Wählen Sie **Namen überprüfen** aus, um den Eintrag zu überprüfen, und klicken Sie auf **OK** > **Weiter**.

7. Wählen Sie **Create a custom task to delegate** > **Next** (Benutzerdefinierte Aufgaben zum Zuweisen erstellen > Weiter) aus.

8. Wählen Sie **im Ordner Computer Objekte nur die folgenden Objekte aus**  >  **Computer objects**.

9. Wählen Sie **ausgewählte Objekte in diesem Ordner erstellen aus** , und löschen Sie die **ausgewählten Objekte in diesem Ordner**.

    ![Bereich „Active Directory Object Type“ (Active Directory-Objekttyp)](./media/windows-autopilot-hybrid/only-following-objects.png)
 
10. Wählen Sie **Weiter** aus.

11. Aktivieren Sie unter **Permissions** (Berechtigungen) das Kontrollkästchen **Full Control** (Vollzugriff). Durch diese Auswahl werden auch alle anderen Optionen aktiviert.

    ![Bereich „Permissions“ (Berechtigungen)](./media/windows-autopilot-hybrid/full-control.png)

12. Klicken Sie auf **Weiter** > **Fertig stellen**.

## <a name="install-the-intune-connector"></a>Installieren des Intune-Connectors

Der Intune-Connector für Azure AD muss auf einem Computer mit Windows Server 2016 oder höher installiert werden. Der Computer muss zudem über Internetzugriff und eine Active Directory-Instanz verfügen. Für höhere Skalierbarkeit und Verfügbarkeit können Sie mehrere Connectors in der Umgebung installieren. Es wird empfohlen, den Connector auf einem Server zu installieren, auf dem keine anderen Intune-Connectors ausgeführt werden. Jeder Connector muss in der Lage sein, Computer Objekte in einer beliebigen Domäne zu erstellen, die Sie unterstützen möchten.

> [!NOTE]
> Wenn Ihre Organisation über mehrere Domänen verfügt und Sie mehrere InTune-Connectors installieren, müssen Sie ein Dienst Konto verwenden, das Computer Objekte in allen Domänen erstellen kann. Dies gilt auch, wenn Sie beabsichtigen, Hybrid Azure AD Join nur für eine bestimmte Domäne zu implementieren. Wenn es sich hierbei um nicht vertrauenswürdige Domänen handelt, müssen Sie die Connectors aus Domänen deinstallieren, in denen Sie nicht Windows Autopilot verwenden möchten. Andernfalls müssen alle Connectors in der Lage sein, Computer Objekte in allen Domänen zu erstellen, wenn mehrere Connectors über mehrere Domänen verfügen.

Der Intune-Connector benötigt die [gleichen Endpunkte wie Intune](../intune/fundamentals/intune-endpoints.md).

1. Deaktivieren Sie die verstärkte Sicherheitskonfiguration für IE. Bei Windows Server ist die verstärkte Sicherheitskonfiguration für Internet Explorer standardmäßig aktiviert. Wenn Sie sich für Active Directory nicht beim InTune-Connector anmelden können, deaktivieren Sie die verstärkte Sicherheitskonfiguration für den Administrator. [Deaktivieren der verstärkten Sicherheitskonfiguration für Internet Explorer](/archive/blogs/chenley/how-to-turn-off-internet-explorer-enhanced-security-configuration). 
2. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf die Option **Geräte** > **Windows** > **Windows-Registrierung** > **Intune-Connector für Active Directory** > **Hinzufügen**. 
3. Folgen Sie den Anweisungen, um den Connector herunterzuladen.
4. Öffnen Sie die heruntergeladene Connectorsetupdatei (*ODJConnectorBootstrapper.exe*), um den Connector zu installieren.
5. Klicken Sie am Ende des Setups auf **Konfigurieren**.
6. Klicken Sie auf **Sign In** (Anmelden).
7. Geben Sie die Anmeldedaten für die Rolle „Globaler Administrator“ oder „Intune-Administrator“ ein. 
 Dem Benutzerkonto muss eine Intune-Lizenz zugewiesen werden.
8. Navigieren Sie zu **Geräte** > **Windows** > **Windows-Registrierung** > **Intune-Connector für Active Directory**, und stellen Sie sicher, dass der Verbindungsstatus **Aktiv** lautet.

> [!NOTE]
> Nach der Anmeldung im Connector dauert es möglicherweise einige Minuten, bis er im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) angezeigt wird. Er wird nur angezeigt, wenn er mit Intune kommunizieren kann.

### <a name="configure-web-proxy-settings"></a>Konfigurieren von Webproxyeinstellungen

Wenn ein Webproxy in der Netzwerkumgebung vorhanden ist, stellen Sie sicher, dass der Intune-Connector für Active Directory ordnungsgemäß funktioniert. Informationen finden Sie unter [Verwenden von vorhandenen lokalen Proxyservern](../intune/enrollment/autopilot-hybrid-connector-proxy.md).


## <a name="create-a-device-group"></a>Erstellen einer Gerätegruppe
1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf die Option **Gruppen** > **Neue Gruppe**.

1. Wählen Sie im Bereich **Gruppe** die folgenden Optionen aus:

    1. Wählen Sie unter **Gruppentyp** die Option **Sicherheit** aus.
    2. Geben Sie einen **Gruppennamen** und eine **Gruppenbeschreibung** ein.
    3. Wählen Sie einen **Mitgliedschaftstyp** aus.

4. Wenn Sie **dynamische Geräte** als mitgliedschaftentyp ausgewählt haben, wählen Sie im Bereich **Gruppe** die Option **dynamische Geräte Mitglieder**aus.

5. Geben Sie im Feld **Erweiterte Regel** eine der folgenden Codezeilen ein:
    - Wenn Sie eine Gruppe mit all Ihren Autopilot-Geräten erstellen möchten, geben Sie `(device.devicePhysicalIDs -any _ -contains "[ZTDId]")` ein.
    - Das Intune-Feld „Gruppentag“ wird dem Attribut „OrderID“ auf Azure AD-Geräten zugeordnet. Wenn Sie eine Gruppe erstellen möchten, die alle Ihre Autopilot-Geräte mit einem bestimmten Gruppentag (OrderID) enthält, geben Sie Folgendes ein: `(device.devicePhysicalIds -any _ -eq "[OrderID]:179887111881")`
    - Wenn Sie eine Gruppe mit all Ihren Autopilot-Geräten mit einer bestimmten Bestellungs-ID erstellen möchten, geben Sie `(device.devicePhysicalIds -any _ -eq "[PurchaseOrderId]:76222342342")` ein.
 
6. Wählen **Save**Sie  >  **Erstellen**speichern aus. 

## <a name="register-your-autopilot-devices"></a>Registrieren der Autopilot-Geräte

Wählen Sie eine der folgenden Möglichkeiten, um Ihre Autopilot-Geräte zu registrieren.

### <a name="register-autopilot-devices-that-are-already-enrolled"></a>Registrieren von bereits angemeldeten Autopilot-Geräten

1. Erstellen Sie ein Autopilot-Bereitstellungsprofil, in dem **Alle als Ziel angegebenen Geräte in Autopilot konvertieren** auf **Ja** festgelegt ist. 
2. Ordnen Sie das Profil einer Gruppe zu, die die Mitglieder enthält, die Sie automatisch bei Autopilot registrieren möchten.

Weitere Informationen finden Sie unter [Erstellen eines Autopilot-Bereitstellungsprofils](enrollment-autopilot.md#create-an-autopilot-deployment-profile).

### <a name="register-autopilot-devices-that-arent-enrolled"></a>Registrieren von noch nicht angemeldeten Autopilot-Geräten

Wenn Ihre Geräte noch nicht registriert sind, können Sie sie selbst registrieren. Weitere Informationen finden Sie unter [Hinzufügen von Geräten](enrollment-autopilot.md#add-devices).

### <a name="register-devices-from-an-oem"></a>Registrieren von Geräten eines OEMs

Beim Kauf neuer Geräte können einige OEMs die Geräte für Sie registrieren. Weitere Informationen finden Sie unter [OEM-Registrierung](add-devices.md#oem-registration).

Vor der Registrierung bei InTune werden *registrierte* Autopilot-Geräte an drei Stellen angezeigt (wobei die Namen auf Ihre Seriennummern festgelegt sind):
- Im Bereich **Autopilot-Geräte** unter Intune im Azure-Portal. Klicken Sie auf **Geräteregistrierung** > **Windows-Registrierung** > **Geräte**.
- Im Bereich **Azure AD-Geräte** unter Intune im Azure-Portal. Klicken Sie auf **Geräte** > **Azure AD-Geräte**.
- Der Bereich **Alle Geräte** unter Azure Active Directory im Azure-Portal (**Geräte** > **Alle Geräte**).

Nachdem Ihre Autopilot-Geräte *registriert* wurden, werden sie an vier Stellen angezeigt:
- Im Bereich **Autopilot-Geräte** unter Intune im Azure-Portal. Klicken Sie auf **Geräteregistrierung** > **Windows-Registrierung** > **Geräte**.
- Im Bereich **Azure AD-Geräte** unter Intune im Azure-Portal. Klicken Sie auf **Geräte** > **Azure AD-Geräte**.
- Im Bereich **Alle Geräte** unter Azure Active Directory im Azure-Portal. Klicken Sie auf **Geräte** > **Alle Geräte**.
- Im Bereich **Alle Geräte** unter Intune im Azure-Portal. Klicken Sie auf **Geräte** > **Alle Geräte**.

Nachdem Ihre Autopilot-Geräte registriert wurden, werden die Gerätenamen in den Hostnamen des Geräts geändert. Standardmäßig beginnt der Hostname mit *DESKTOP-* .


## <a name="create-and-assign-an-autopilot-deployment-profile"></a>Erstellen und Zuweisen eines Autopilot-Bereitstellungsprofils
Autopilot-Bereitstellungsprofile werden verwendet, um die Autopilot-Geräte zu konfigurieren.

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Geräte** > **Windows** > **Windows-Registrierung** > **Deployment Profiles** (Bereitstellungsprofile) > **Profil erstellen**.
2. Geben Sie auf der Seite **Grundlagen** einen Wert in **Name** und eine optionale **Beschreibung** ein.
3. Wenn Sie möchten, dass alle Geräte in den zugewiesenen Gruppen automatisch in Autopilot konvertiert werden, legen Sie für **Alle Zielgeräte in Autopilot-Geräte konvertieren** den Wert **Ja** fest. Alle unternehmenseigenen, Nicht-Autopilot-Geräte in zugewiesenen Gruppen werden mit dem Autopilot-Bereitstellungsdienst registriert. Geräte, die sich im Besitz befinden, werden nicht in Autopilot konvertiert. Die Verarbeitung der Registrierung kann 48 Stunden dauern. Wenn die Registrierung des Geräts aufgehoben und es zurückgesetzt ist, registriert Autopilot es. Nachdem ein Gerät auf diese Weise registriert wurde, wird das Gerät durch Deaktivieren dieser Option oder Entfernen der Profilzuordnung nicht aus dem Autopilot-Bereitstellungsdienst entfernt. Sie müssen stattdessen [das Gerät direkt entfernen](enrollment-autopilot.md#delete-autopilot-devices).
4. Wählen Sie **Weiter** aus.
5. Wählen Sie auf der Seite **Windows-Willkommensseite** als **Bereitstellungsmodus** die Option **Benutzergesteuert** aus.
6. Wählen Sie im Feld **Azure AD beitreten als** die Option **In Azure AD Hybrid eingebunden** aus.
7. Wenn Sie Geräte aus dem Netzwerk der Organisation mithilfe von VPN-Unterstützung bereitstellen, legen Sie die Option **Domänen Konnektivität überspringen** auf **Ja**fest. Weitere Informationen finden Sie [unter der benutzergesteuerte Modus für Hybrid Azure Active Directory Join mit VPN-Unterstützung](user-driven.md#user-driven-mode-for-hybrid-azure-active-directory-join-with-vpn-support).
8. Konfigurieren Sie die restlichen Optionen auf der Seite **Windows-Willkommensseite** nach Bedarf.
9. Wählen Sie **Weiter** aus.
10. Wählen Sie auf der Seite **Bereichs Tags** die Option [Bereichs Tags](../intune/fundamentals/scope-tags.md) für dieses Profil aus.
11. Wählen Sie **Weiter** aus.
12. Wählen Sie auf der Seite **Zuweisungen** die Option **Einzuschließende Gruppen auswählen** aus, suchen Sie nach der Gerätegruppe, und wählen Sie sie durch Klicken auf **Auswählen** aus.
13. Wählen Sie **Weiter** > **Erstellen** aus.

Es dauert etwa 15 Minuten, bis sich der Status des Geräteprofils von *Nicht zugewiesen* in *Wird zugewiesen* und schließlich in *Zugewiesen* ändert.

## <a name="optional-turn-on-the-enrollment-status-page"></a>Aktivieren der Registrierungsstatusseite (optional)

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Geräte** > **Windows** > **Windows-Registrierung** > **Seite zum Registrierungsstatus**.
2. Klicken Sie im Bereich **Seite zum Registrierungsstatus** auf **Standard** > **Einstellungen**.
3. Legen Sie für **Installationsfortschritt für Apps und Profile anzeigen** **Yes** (Ja) fest.
4. Konfigurieren Sie die anderen Optionen je nach Bedarf.
5. Wählen Sie **Speichern** aus.

## <a name="create-and-assign-a-domain-join-profile"></a>Erstellen und Zuweisen eines Domänenbeitrittsprofils

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf die Option **Geräte** > **Konfigurationsprofile** > **Profil erstellen**.
2. Geben Sie die folgenden Eigenschaften ein:
    - **Name:** Geben Sie einen aussagekräftigen Namen für das neue Profil ein.
    - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein.
    - **Plattform**: Wählen Sie **Windows 10 und höher** aus.
    - **Profiltyp**: Wählen Sie **Domänenbeitritt (Vorschau)** aus.
3. Wählen Sie **Einstellungen** aus, und geben Sie ein **Computernamenpräfix** und einen **Domänennamen** an.
4. (Optional) Geben Sie eine **Organisationseinheit** (OE) im [DN-Format](/windows/desktop/ad/object-names-and-identities#distinguished-name) an. Optionen
    - Geben Sie eine OE an, in der Sie die Steuerung an Ihr Windows 2016-Gerät delegiert haben, auf dem der Intune-Connector ausgeführt wird.
    - Geben Sie eine OE an, in der Sie die Steuerung an die Stammcomputer in Ihrer lokalen Active Directory-Instanz delegiert haben.
    - Wenn Sie diese Angaben leer lassen, wird das Computerobjekt im Standardcontainer von Active Directory erstellt („CN=Computers“, falls Sie diese Einstellung nie [geändert](https://support.microsoft.com/help/324949/redirecting-the-users-and-computers-containers-in-active-directory-dom) haben).
 
    Hier sind einige gültige Beispiele:
      - OU=Level 1,OU=Level2,DC=contoso,DC=com
      - OU=Mine,DC=contoso,DC=com
 
    Im folgenden sind einige Beispiele aufgeführt, die nicht gültig sind:
      - CN = Computers, DC = Configuration Manager = com (Sie können keinen Container angeben. lassen Sie stattdessen den Wert leer, um den Standardwert für die Domäne zu verwenden.)
      - OU = mein (Sie müssen die Domäne über die DC =-Attribute angeben)
 
    > [!NOTE]
    > Verwenden Sie keine Anführungszeichen um den Wert in **Organisationseinheit**.

5. Klicken Sie auf **OK** > **Erstellen**. Das Profil wird erstellt und in der Liste angezeigt.
6. Weisen Sie der gleichen Gruppe [ein Geräte Profil](../intune/configuration/device-profile-assign.md#assign-a-device-profile) zu, das Sie im Schritt [Erstellen einer Gerätegruppe](windows-autopilot-hybrid.md#create-a-device-group)verwendet haben. Unterschiedliche Gruppen können verwendet werden, wenn Geräte mit verschiedenen Domänen oder Organisationseinheiten verknüpft werden müssen.

> [!NOTE]
> Die Benennungsfunktionen für Windows Autopilot für Azure AD Hybrid Join unterstützen keine Variablen wie %SERIAL%. Sie unterstützen ausschließlich Präfixe für den Computernamen.

## <a name="next-steps"></a>Nächste Schritte

Nachdem Sie Windows Autopilot konfiguriert haben, erfahren Sie mehr über die Verwaltung dieser Geräte. Weitere Informationen finden Sie unter [Was ist die Microsoft Intune-Geräteverwaltung?](../intune/remote-actions/device-management.md).