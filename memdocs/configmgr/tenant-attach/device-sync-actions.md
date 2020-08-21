---
title: Anfügen von Mandanten in Microsoft Endpoint Manager
titleSuffix: Configuration Manager
description: Laden Sie Ihre Configuration Manager-Geräte in den clouddienst hoch, und nehmen Sie im Admin Center Aktionen vor.
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: 4bdfbabf27906eb8a79ec8ba24f51c3e176dc028
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700404"
---
# <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions"></a><a name="bkmk_attach"></a> Microsoft Endpoint Manager-Mandanten anfügen: Geräte Synchronisierung und Geräte Aktionen
<!--3555758 live 3/4/2020-->
*Gilt für: Configuration Manager (Current Branch)*

Microsoft Endpoint Manager ist eine integrierte Lösung für die Verwaltung all Ihrer Geräte. Microsoft vereint Configuration Manager und Intune in einer einzigen Konsole namens **Microsoft Endpoint Manager Admin Center**.

Ab Configuration Manager Version 2002 können Sie Ihre Configuration Manager Geräte in den Cloud-Dienst hochladen und im Admin Center auf dem Blatt **Geräte** Aktionen ausführen.

## <a name="prerequisites"></a>Voraussetzungen

- Ein Konto, das ein *globaler Administrator* für die Anmeldung ist, wenn diese Änderung angewendet wird. Weitere Informationen finden Sie unter [Azure Active Directory Administrator Rollen (Azure AD)](/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-ad-administrator-roles).
   - Das Onboarding erstellt eine Drittanbieter-APP und einen ersten Dienst Prinzipal in Ihrem Azure AD Mandanten.
- Eine Azure Public Cloud-Umgebung.
- Die Benutzerkonten, die Geräte Aktionen auslösen, müssen die folgenden Voraussetzungen erfüllen:
   - Wurde mit [Azure Active Directory Benutzer](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) Ermittlung und [Active Directory Benutzer](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)Ermittlung ermittelt.
      - Dies bedeutet, dass das Benutzerkonto in Azure AD ein synchroniziertes Benutzerobjekt sein muss.
   - Die Berechtigung **Configuration Manager Aktion initiieren** unter **Remote Tasks** im Microsoft Endpoint Manager Admin Center.
- Wenn der Standort der zentralen Verwaltung über einen [Remote Anbieter](../core/plan-design/hierarchy/plan-for-the-sms-provider.md)verfügt, befolgen Sie die Anweisungen für die Zertifizierungsstelle mit [einem Remote Anbieter](../core/servers/manage/cmpivot-changes.md#cas-has-a-remote-provider) Szenario im cmpivot-Artikel. <!--7796824-->

## <a name="internet-endpoints"></a>Internet Endpunkte

[!INCLUDE [Internet endpoints for tenant attach](../core/plan-design/network/includes/internet-endpoints-tenant-attach.md)]

## <a name="enable-device-upload-when-co-management-is-already-enabled"></a><a name="bkmk_edit"></a> Aktivieren des Geräte Uploads, wenn die Co-Verwaltung bereits aktiviert ist

Wenn Sie derzeit die Co-Verwaltung aktiviert haben, verwenden Sie die Eigenschaften der Co-Verwaltung, um den Geräte Upload zu aktivieren. Wenn die Co-Verwaltung nicht bereits aktiviert ist, verwenden Sie stattdessen [den Assistenten zum **Konfigurieren der Co-Verwaltung** ](#bkmk_config) , um den Geräte Upload zu aktivieren.

Wenn die Co-Verwaltung bereits aktiviert ist, bearbeiten Sie die Eigenschaften der Co-Verwaltung, um den Geräte Upload mithilfe der folgenden Anweisungen zu aktivieren:

1. Navigieren Sie in der Configuration Manager-Administratorkonsole zu **Verwaltung** > **Übersicht** > **Clouddienste** > **Co-Verwaltung**.
1. Wählen Sie im Menüband die Option **Eigenschaften** für Ihre Produktions Richtlinie für die Co-Verwaltung aus.
1. Klicken Sie in der Registerkarte **Configure upload** (Upload konfigurieren) auf **Upload to Microsoft Endpoint Manager admin center** (Upload ins Microsoft Endpoint Manager Admin Center). Wählen Sie **Übernehmen**.
   - Die Standardeinstellung für den Upload von Geräten ist **All my devices managed by Microsoft Endpoint Configuration Manager** (Alle von Microsoft Endpoint Configuration Manager verwalteten Geräte). Bei Bedarf können Sie den Upload auf eine einzelne Geräte Sammlung beschränken.
1. Aktivieren Sie die Option zum **Aktivieren von Endpoint Analytics für Geräte, die in den Microsoft Endpoint Manager hochgeladen** werden, wenn Sie auch Einblicke erhalten möchten, um die Endbenutzer Funktionen in [EndPoint Analytics](../../analytics/overview.md)zu optimieren.

   [![Hochladen von Geräten in das Microsoft Endpoint Manager Admin Center](../../analytics/media/6051638-configure-upload-configmgr.png)](../../analytics/media/6051638-configure-upload-configmgr.png#lightbox)
1. Melden Sie sich mit Ihrem *globalen Administratorkonto* an, wenn Sie dazu aufgefordert werden.
1. Wählen Sie **Ja** aus, um die Benachrichtigung **Create Aad Application** zu akzeptieren. Durch diese Aktion wird ein Dienstprinzipal bereitgestellt und eine Azure AD-Anwendungsregistrierung erstellt, um das Synchronisieren zu vereinfachen.
1. Wählen Sie **OK** aus, um die Eigenschaften der Co-Verwaltung zu beenden, nachdem Sie die Änderungen vorgenommen haben.


## <a name="enable-device-upload-when-co-management-isnt-enabled"></a><a name="bkmk_config"></a> Aktivieren des Geräte Uploads, wenn die Co-Verwaltung nicht aktiviert ist

Wenn Sie die Co-Verwaltung nicht aktiviert haben, verwenden Sie den Assistenten zum **Konfigurieren der Co-Verwaltung** , um das Hochladen von Geräten zu aktivieren. Sie können Ihre Geräte hochladen, ohne die automatische Registrierung für die Co-Verwaltung zu aktivieren oder Workloads zu InTune zu wechseln. Alle von Configuration Manager verwalteten Geräte mit **Ja** in der Spalte **Client** werden hochgeladen. Bei Bedarf können Sie den Upload auf eine einzelne Geräte Sammlung beschränken. Wenn die Co-Verwaltung in Ihrer Umgebung bereits aktiviert ist, bearbeiten Sie die [Eigenschaften der Co-Verwaltung](#bkmk_edit) , um stattdessen den Geräte Upload zu aktivieren.

Wenn die Co-Verwaltung nicht aktiviert ist, verwenden Sie die nachfolgenden Anweisungen, um den Geräte Upload zu aktivieren:

1. Navigieren Sie in der Configuration Manager-Administratorkonsole zu **Verwaltung** > **Übersicht** > **Clouddienste** > **Co-Verwaltung**.
1. Wählen Sie im Menüband die **Option Co-Verwaltung konfigurieren** aus, um den Assistenten zu öffnen.
1. Wählen Sie auf der Seite **Onboarding von Mandanten** **AzurePublicCloud** als Umgebung aus. Azure Government Cloud und Azure China 21ViaNet werden nicht unterstützt.
1. Wählen Sie **Anmelden** aus. Melden Sie sich mit Ihrem *globalen Administratorkonto* an.
1. Stellen Sie sicher, dass die Option **auf das Microsoft Endpoint Manager Admin Center hochladen** auf der Seite für das **Onboarding** von Mandanten ausgewählt ist.
   - Stellen Sie sicher, dass die Option **automatische Client Registrierung für die Co-Verwaltung aktivieren** nicht aktiviert ist, wenn Sie die Co-Verwaltung jetzt nicht aktivieren möchten. Wenn Sie die Co-Verwaltung aktivieren möchten, wählen Sie die Option aus.
   - Wenn Sie die Co-Verwaltung zusammen mit dem Hochladen von Geräten aktivieren, erhalten Sie weitere Seiten im Assistenten, um den Vorgang abzuschließen. Weitere Informationen finden Sie unter [Aktivieren der Co-Verwaltung](../comanage/how-to-enable.md).

   [![Konfigurations-Assistent für die Co-Verwaltung](./media/3555758-comanagement-wizard.png)](./media/3555758-comanagement-wizard.png#lightbox)
1. Wählen Sie **weiter** aus, und klicken Sie auf **Ja** , um die Benachrichtigung **Create Aad Application** zu akzeptieren Durch diese Aktion wird ein Dienstprinzipal bereitgestellt und eine Azure AD-Anwendungsregistrierung erstellt, um das Synchronisieren zu vereinfachen.
     - Optional können Sie eine zuvor erstellte Azure AD Anwendung während des onboardings für das Anfügen von Mandanten importieren (ab Version 2006). Weitere Informationen finden Sie im Abschnitt [Importieren einer zuvor erstellten Azure AD Anwendung](#bkmk_aad_app) .
1. Wählen Sie auf der Seite **Upload konfigurieren** die empfohlene Einstellung für den Geräte Upload für alle Geräte aus, die **von Microsoft Endpoint Configuration Manager verwaltet**werden. Bei Bedarf können Sie den Upload auf eine einzelne Geräte Sammlung beschränken.
1. Aktivieren Sie die Option zum **Aktivieren von Endpoint Analytics für Geräte, die in den Microsoft Endpoint Manager hochgeladen** werden, wenn Sie auch Einblicke erhalten möchten, um die Endbenutzer Funktionen in [EndPoint Analytics](../../analytics/overview.md) zu optimieren.
1. Wählen Sie **Zusammenfassung** aus, um Ihre Auswahl zu überprüfen, **und wählen Sie**
1. Wählen Sie nach Abschluss des Assistenten die Option **Schließen**aus.  

## <a name="perform-device-actions"></a>Ausführen von Geräte Aktionen

1. Navigieren Sie in einem Browser zu. `endpoint.microsoft.com`
1. Wählen Sie **Geräte** und dann **alle Geräte** aus, um die hochgeladenen Geräte anzuzeigen. **ConfigMgr** wird in der Spalte **verwaltet von** für hochgeladene Geräte angezeigt.
   [![Alle Geräte im Microsoft Endpoint Manager Admin Center](./media/3555758-all-devices.png)](./media/3555758-all-devices.png#lightbox)
1. Wählen Sie ein Gerät aus, um seine **Übersichts** Seite zu laden.
1. Wählen Sie eine der folgenden Aktionen aus:
   - **Computerrichtlinie synchronisieren**
   - **Benutzerrichtlinie synchronisieren**
   - **App-Evaluierungszyklus**

   [![Geräte Übersicht im Microsoft Endpoint Manager Admin Center](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)

## <a name="import-a-previously-created-azure-ad-application-optional"></a><a name="bkmk_aad_app"></a> Importieren einer zuvor erstellten Azure AD Anwendung (optional)
<!--6479246-->
*(Eingeführt in Version 2006)*

Während eines [neuen onboardings](#bkmk_config)kann ein Administrator eine zuvor erstellte Anwendung während des onboardings zum Anfügen des Mandanten angeben. Sie müssen Azure AD Anwendungen nicht über mehrere Hierarchien hinweg freigeben oder wieder verwenden. Wenn Sie über mehrere Hierarchien verfügen, erstellen Sie separate Azure AD Anwendungen.

Wählen Sie im **Konfigurations-Assistenten für die Co-Verwaltung** auf der Seite **Onboarding von Mandanten** die Option **Importieren Sie optional eine separate Web-App, um Configuration Manager-Clientdaten mit dem Admin Center von Microsoft Endpoint Manager zu synchronisieren**. Diese Option fordert Sie auf, die folgenden Informationen für Ihre Azure AD-App anzugeben:

- Name des Azure AD-Mandanten
- ID des Azure AD-Mandanten
- Anwendungsname
- Client-ID
- Geheimer Schlüssel
- Ablauf des geheimen Schlüssels
- App-ID-URI

### <a name="azure-ad-application-permissions-and-configuration"></a>Azure AD von Anwendungs Berechtigungen und Konfiguration

Die Verwendung einer zuvor erstellten Anwendung während des onboardings zum Anfügen von Mandanten erfordert die folgenden Berechtigungen:

- Configuration Manager-Berechtigungen für den-Dienst:
   - Cmcollectiondata. Read
   - Cmcollectiondata. Write

- Microsoft Graph Berechtigungen:
   - Berechtigung "Directory. Read. alle [Anwendungen](/graph/permissions-reference#application-permissions) "
   - Berechtigung "Directory. Read. alle [Delegierten Verzeichnisse](/graph/permissions-reference#directory-permissions) "

- Stellen Sie sicher, dass die **Administrator Zustimmung für** den Mandanten für die Azure AD Anwendung aktiviert ist. Weitere Informationen finden Sie unter [erteilen der Administrator Zustimmung in App-Registrierungen](/azure/active-directory/manage-apps/grant-admin-consent).

- Die importierte Anwendung muss wie folgt konfiguriert werden:
   - Wird **nur für Konten in diesem Organisations Verzeichnis**registriert. Weitere Informationen finden Sie unter [Ändern der Benutzer, die auf Ihre Anwendung zugreifen können](/azure/active-directory/develop/quickstart-modify-supported-accounts#to-change-who-can-access-your-application).
   -  Hat einen gültigen Anwendungs-ID-URI und geheimen Schlüssel



## <a name="next-steps"></a>Nächste Schritte

- [Registrieren von Configuration Manager Geräten in Endpoint Analytics](../../analytics/enroll-configmgr.md#bkmk_cm_enroll)
- Informationen zum Anfügen von Protokolldateien für den Mandanten finden Sie unter Problembehandlung beim [Anfügen](troubleshoot.md)von Mandanten.