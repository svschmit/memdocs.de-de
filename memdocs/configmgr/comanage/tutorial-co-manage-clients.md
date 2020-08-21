---
title: 'Tutorial: Aktivieren der Co-Verwaltung für bereits vorhandene Clients'
titleSuffix: Configuration Manager
description: Konfigurieren Sie die Co-Verwaltung mit Microsoft Intune, wenn Sie bereits Windows 10-Geräte mit dem Configuration Manager verwalten.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: tutorial
ms.assetid: 140c522f-d09a-40b6-a4b0-e0d14742834a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cc05ae5a9be6c437fab60f8c4c5a45d61e8c3e65
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694881"
---
# <a name="tutorial-enable-co-management-for-existing-configuration-manager-clients"></a>Tutorial: Aktivieren der Co-Verwaltung für vorhandene Konfigurations-Manager-Clients

Mit der Co-Verwaltung können Sie Ihre bewährten Prozesse für die Verwendung von Configuration Manager zum Verwalten von PCs in Ihrem Unternehmen beibehalten. Gleichzeitig investieren Sie mit der Nutzung von Intune für Sicherheit und moderne Bereitstellung in die Cloud.  

In diesem Tutorial richten Sie die Co-Verwaltung Ihrer Windows 10-Geräte ein, die bereits im Configuration Manager registriert sind. Dieses Tutorial beginnt mit der Annahme, dass Sie den Configuration Manager bereits zur Verwaltung Ihrer Windows 10-Geräte verwenden.

Verwenden Sie dieses Tutorial in folgenden Fällen:  

- Sie haben ein lokales Active Directory, das Sie mit Azure Active Directory (Azure AD) in einer Azure AD Hybrid-Konfiguration verbinden können.

  Wenn Sie kein Azure AD Hybrid bereitstellen können, das Ihr lokales AD mit Azure AD verbindet, sollten Sie unser Begleittutorial [Aktivieren der Co-Verwaltung für neue internetbasierte Windows 10-Geräte](tutorial-co-manage-new-devices.md) lesen.
- Sie haben bestehende Konfigurations-Manager-Clients, die Sie in die Cloud einbinden möchten.

**Die Themen dieses Tutorials sind:**  
> [!div class="checklist"]
> * Überprüfen der Voraussetzungen für Azure und Ihre lokale Umgebung
> * Einrichten von Hybrid-Azure AD  
> * Konfigurieren von Konfigurations-Manager-Client-Agenten zur Registrierung bei Azure AD  
> * Konfigurieren von Intune zum automatischen Registrieren von Geräten  
> * Aktivieren der Co-Verwaltung in Configuration Manager  

## <a name="prerequisites"></a>Voraussetzungen  

### <a name="azure-services-and-environment"></a>Azure-Dienste und -Umgebung

- Azure-Abonnement ([kostenlose Testversion](https://azure.microsoft.com/free))
- Azure Active Directory Premium
- Microsoft Intune-Abonnement
  > [!TIP]  
  > Ein Enterprise Mobility + Security-Abonnement (EMS) umfasst Azure Active Directory Premium und Microsoft Intune. EMS-Abonnement ([kostenlose Testversion](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)).  

Sofern nicht bereits in Ihrer Umgebung erfolgt, führen Sie während dieses Tutorials Folgendes aus:

- Konfigurieren von [Azure AD Connect](/azure/active-directory/hybrid/how-to-connect-install-select-installation) zwischen Ihrem lokalen Active Directory und Ihrem Azure AD-Mandanten

> [!TIP]
> Sie müssen nicht mehr einzelne Intune- oder EMS-Lizenzen kaufen und Ihren Benutzern zuweisen. Weitere Informationen finden Sie unter [Häufig gestellte Fragen zum Produkt und zur Lizenzierung](../core/understand/product-and-licensing-faq.md#bkmk_mem).

### <a name="on-premises-infrastructure"></a>Lokale Infrastruktur

- Eine [unterstützte Version](../core/servers/manage/updates.md#supported-versions) von Configuration Manager (Current Branch)
- Die Autorität für die mobile Geräteverwaltung (MDM) muss auf Intune festgelegt sein.  

### <a name="permissions"></a>Berechtigungen

Verwenden Sie in diesem Tutorial durchgehend die folgenden Berechtigungen, um Aufgaben auszuführen:

- Ein Konto, das *Domänenadministrator* in Ihrer lokalen Infrastruktur ist  
- Ein Konto, das *Hauptadministrator* für *alle* Bereiche in Configuration Manager ist
- Ein Konto, das ein *globaler Administrator* in Azure Active Directory (Azure AD) ist
   - Stellen Sie sicher, dass Sie dem Konto, mit dem Sie sich bei Ihrem Mandanten anmelden, eine Intune-Lizenz zugewiesen haben. Andernfalls schlägt die Anmeldung mit der Fehlermeldung „Benutzer nicht erkannt“ fehl. <!--mem issue 169-->

## <a name="set-up-hybrid-azure-ad"></a>Einrichten von Hybrid-Azure AD

Wenn Sie ein Azure AD Hybrid einrichten, richten Sie tatsächlich die Integration eines lokalen AD mit Azure AD über Azure AD Connect und Active Directory Federated Services (ADFS) ein. Nach erfolgreicher Konfiguration können sich Ihre Mitarbeiter mit ihren lokalen AD-Anmeldeinformationen nahtlos bei externen Systemen anmelden.

> [!IMPORTANT]  
> Dieses Tutorial beschreibt einen Bare-Bones-Prozess zur Einrichtung des Azure AD Hybrid für eine verwaltete Domäne. Wir empfehlen Ihnen, sich mit dem Prozess vertraut zu machen und sich nicht auf dieses Tutorial als Anleitung zum Verständnis und zur Implementierung des Azure AD Hybrid zu verlassen.
>
> Weitere Informationen zu Azure AD Hybrid finden Sie in den folgenden Artikeln in der Azure Active Directory-Dokumentation:
>
> - [Planen Ihrer Azure AD Join -Implementierung](/azure/active-directory/devices/azureadjoin-plan)
> - [Planen Ihrer Azure AD Hybrid Join -Implementierung](/azure/active-directory/devices/hybrid-azuread-join-plan)
> - [Steuern des Azure AD Hybrid Join Ihrer Geräte](/azure/active-directory/devices/hybrid-azuread-join-control)
> - [Konfigurieren von Azure AD Hybrid Join für Verbunddomänen](/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  

### <a name="set-up-azure-ad-connect"></a>Einrichten von Azure AD Connect

Azure AD Hybrid erfordert die Konfiguration von Azure AD Connect, um die Computerkonten in Ihrem lokalen Active Directory (AD) und das Geräteobjekt in Azure AD zu synchronisieren.

Ab der Version 1.1.819.0 bietet Ihnen Azure AD Connect einen Assistenten zur Konfiguration von Azure AD Hybrid Join. Dieser Assistent vereinfacht die Konfiguration.  

Um Azure AD Connect zu konfigurieren, benötigen Sie die Anmeldeinformationen eines globalen Administrators für Azure AD.  

> [!TIP]  
> Die folgende Prozedur sollte nicht als maßgebend für die Einrichtung von Azure AD Connect angesehen werden. Es wird jedoch hier beschrieben, um die Konfiguration der Co-Verwaltung zwischen Intune und Configuration Manager zu optimieren. Für den maßgeblichen Inhalt dieser und verwandter Verfahren zur Einrichtung von Azure AD lesen Sie [Konfigurieren von Azure AD Hybrid Join für verwaltete Domänen](/azure/active-directory/devices/hybrid-azuread-join-managed-domains) in der Azure AD-Dokumentation.  

#### <a name="configure-a-hybrid-azure-ad-join-using-azure-ad-connect"></a>Konfigurieren von Azure AD Hybrid Join mit Azure AD Connect

1. Installieren Sie die [neueste Version von Azure AD Connect](https://www.microsoft.com/download/details.aspx?id=47594) (1.1.819.0 oder höher).  
2. Starten Sie Azure AD Connect, und wählen Sie **Konfigurieren** aus.
3. Wählen Sie auf der Seite **Zusätzliche Aufgaben** die Option **Geräteoptionen konfigurieren** und dann **Weiter** aus.
4. Wählen Sie auf der Seite **Übersicht** die Option **Weiter** aus.
5. Geben Sie auf der Seite **Mit Azure AD verbinden** die Anmeldeinformationen eines globalen Administrators für Azure AD ein.
6. Wählen Sie auf der Seite **Geräteoptionen** die Option **Azure AD Hybrid Join konfigurieren** und dann **Weiter** aus.
7. Wählen Sie auf der Seite **Gerätebetriebssysteme** die Betriebssysteme aus, die von Geräten in Ihrer Active Directory-Umgebung verwendet werden, und dann **Weiter**.  

   Sie können die Option zur Unterstützung von in Domänen eingebundene kompatible Windows-Geräten aktivieren, aber denken Sie daran, dass die Co-Verwaltung von Geräten nur für Windows 10 unterstützt wird.
8. Führen Sie auf der Seite **SCP** für jede lokale Gesamtstruktur, in der Azure AD Connect den Service Connection Point (SCP) konfigurieren soll, die folgenden Schritte aus, und wählen Sie dann **Weiter**:  
   1. Wählen Sie die Gesamtstruktur aus.  
   2. Wählen Sie den Authentifizierungsdienst aus.  Wenn Sie eine Verbunddomäne haben, wählen Sie AD FS-Server, es sei denn, Ihre Organisation hat ausschließlich Windows 10-Clients und Sie haben die Computer/Gerätesynchronisierung konfiguriert oder Ihre Organisation verwendet [SeamlessSSO](/azure/active-directory/hybrid/how-to-connect-sso).  
   3. Klicken Sie auf **Hinzufügen**, um die Enterprise-Administratoranmeldeinformationen einzugeben.  
9. Bei einer verwalteten Domäne können Sie diesen Schritt überspringen.  

   Geben Sie auf der Seite **Verbundkonfiguration** die Anmeldeinformationen Ihres AD FS-Administrators ein, und wählen Sie dann **Weiter**.
10. Wählen Sie auf der Seite **Bereit für Konfiguration** die Option **Konfigurieren**.
11. Wählen Sie auf der Seite **Konfiguration abgeschlossen** die Option **Beenden**.

Wenn Sie Probleme mit der Fertigstellung von Azure AD Hybrid Join für domänengebundene Windows-Geräte haben, lesen Sie [Problembehandlung in Azure AD Join für aktuelle Windows-Geräte](/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).

## <a name="configure-client-settings-to-direct-clients-to-register-with-azure-ad"></a>Konfigurieren von Clienteinstellungen für direkte Clients zum Registrieren bei Azure AD

Verwenden Sie Clienteinstellungen, um Configuration Manager-Clients für die automatische Registrierung mit Azure AD zu konfigurieren.  

1. Öffnen Sie die **Configuration Manager-Konsole** > **Administration** > **Übersicht** > **Clienteinstellungen**, und bearbeiten Sie dann die **Clientstandardeinstellungen**.  

2. Wählen Sie **Clouddienste** aus.  

3. Stellen Sie auf der Seite **Standardeinstellungen** **Registrierung neuer einer Windows 10-Domäne beigetretener Geräte mit Azure Active Directory** auf = **Ja** ein.  

4. Klicken Sie auf **OK**, um diese Konfiguration zu speichern.  

## <a name="configure-auto-enrollment-of-devices-to-intune"></a>Konfigurieren der automatischen Registrierung von Geräten in Intune

Als Nächstes richten wir die automatische Registrierung von Geräten mit Intune ein. Bei der automatischen Registrierung registrieren sich Geräte, die Sie mit dem Configuration Manager verwalten, automatisch mit Intune.

Die automatische Registrierung ermöglicht es Benutzern auch, ihre Windows 10-Geräte für Intune zu registrieren. Geräte werden registriert, wenn ein Benutzer sein Geschäftskonto zu seinem persönlichen Gerät hinzufügt oder wenn ein unternehmenseigenes Gerät mit Azure Active Directory verbunden wird.  

1. Melden Sie sich beim [Azur-Portal](https://portal.azure.com/) an, und wählen Sie **Azure Active Directory** > **Mobilität (MDM und MAM)**  > **Microsoft Intune** aus.  

2. Konfigurieren Sie den **MDM-Benutzerbereich**. Geben Sie einen der folgenden Parameter an, um zu konfigurieren, welche Geräte der Benutzer von Microsoft Intune verwaltet werden, und übernehmen Sie die Standardwerte für die URL-Werte.  

   - **Einige:** Wählen Sie die **Gruppen** aus, die ihre Windows 10-Geräte automatisch registrieren können.  

   - **Alle:** Alle Benutzer können ihre Windows 10-Geräte automatisch registrieren.

   - **Keine**: Deaktivieren der automatische MDM-Registrierung

   > [!IMPORTANT]  
   > Wenn sowohl **MAM-Benutzerbereich** als auch die automatische MDM-Registrierung (**MDM-Benutzerbereich**) für eine Gruppe aktiviert sind, ist nur MAM aktiviert. Die mobile Anwendungsverwaltung (Mobile Application Management, MAM) wird nur für Benutzer in dieser Gruppe hinzugefügt, wenn Sie ein persönliches Gerät am Arbeitsplatz einbinden. Es findet keine automatische MDM-Registrierung von Geräten statt.  

3. Wählen Sie **Speichern** aus, um die Konfiguration der automatischen Registrierung abzuschließen.  

4. Kehren Sie zu **Mobilität (MDM und MAM)** zurück, und wählen Sie dann **Microsoft Intune-Registrierung** aus.  

    > [!NOTE]
    > Bei manchen Mandanten können diese Optionen möglicherweise nicht konfiguriert werden.<!-- SCCMDocs#1230 -->
    >
    > Mit **Microsoft Intune** konfigurieren Sie die MDM-App für Azure AD. **Microsoft Intune-Registrierung** ist eine bestimmte Azure AD-App, die erstellt wird, wenn Sie Richtlinien für mehrstufige Authentifizierung für iOS- und Android-Registrierung anwenden. Weitere Informationen finden Sie unter [Mehrstufige Authentifizierung für Geräteregistrierung in Intune erfordern](/intune/enrollment/multi-factor-authentication).

5. Wählen Sie für den MDM-Benutzerbereich **Alle** und dann **Speichern** aus.  

## <a name="enable-co-management-in-configuration-manager"></a>Aktivieren der Co-Verwaltung in Configuration Manager

Wenn Azure AD Hybrid eingerichtet und der Configuration Manager-Client konfiguriert ist, können Sie jetzt die Co-Verwaltung für Ihre Windows 10-Geräte aktivieren.  

> [!TIP]
> - Wenn Sie die Co-Verwaltung aktivieren, weisen Sie eine Sammlung als *Pilotgruppe*zu. Dies ist eine Gruppe, die eine kleine Anzahl von Clients enthält, um Ihre Co-Verwaltungskonfigurationen zu testen. Wir empfehlen Ihnen, vor Beginn des Verfahrens eine geeignete Sammlung anzulegen. Dann können Sie diese Sammlung auswählen, ohne das Verfahren zu beenden.
> - Ab Configuration Manager, Version 1906 benötigen Sie u. U. mehrere Sammlungen, da Sie für jede Workload eine andere *Pilotgruppe* zuweisen können.

### <a name="enable-co-management-starting-in-version-1906"></a>Aktivieren von Co-Verwaltung ab Version 1906

[!INCLUDE [Enable Co-management in version 1906 and later](includes/enable-co-management-1906-and-higher.md)]

### <a name="enable-co-management-in-version-1902-and-earlier"></a>Aktivieren von Co-Verwaltung in Version 1902 und früher

[!INCLUDE [Enable Co-management in version 1902 and earlier](includes/enable-co-management-1902-and-earlier.md)]

## <a name="next-steps"></a>Nächste Schritte

- Überprüfen des Status von Geräten Co-Verwaltung über das [Co-Verwaltungs-Dashboard](how-to-monitor.md)
- Abrufen des [unmittelbaren Werts](quickstarts.md#immediate-value) aus der Co-Verwaltung
- Verwenden von Regeln für den [bedingten Zugriff](quickstart-conditional-access.md) und die Intune Compliance zum Verwalten des Benutzerzugriff auf Unternehmensressourcen