---
title: Microsoft Endpoint Manager-Mandanten anfügen
titleSuffix: Configuration Manager
description: Laden Sie Ihre Configuration Manager-Geräte in den clouddienst hoch, und nehmen Sie im Admin Center Aktionen vor.
ms.date: 04/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: e2b8c07a64265d33ade0b1c2c08c2d9c4096b741
ms.sourcegitcommit: a4ec80c5dd51e40f3b468e96a71bbe29222ebafd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82693463"
---
# <a name="microsoft-endpoint-manager-tenant-attach-device-sync-and-device-actions"></a><a name="bkmk_attach"></a>Microsoft Endpoint Manager-Mandanten anfügen: Geräte Synchronisierung und Geräte Aktionen
<!--3555758 live 3/4/2020-->
*Gilt für: Configuration Manager (Current Branch)*

Microsoft Endpoint Manager ist eine integrierte Lösung für die Verwaltung all Ihrer Geräte. Microsoft vereint Configuration Manager und InTune in einer einzigen Konsole mit dem Namen **Microsoft Endpoint Manager Admin Center**.

Ab Configuration Manager Version 2002 können Sie Ihre Configuration Manager Geräte in den Cloud-Dienst hochladen und im Admin Center auf dem Blatt **Geräte** Aktionen ausführen.

## <a name="prerequisites"></a>Voraussetzungen

- Ein Konto, das ein *globaler Administrator* für die Anmeldung ist, wenn diese Änderung angewendet wird. Weitere Informationen finden Sie unter [Azure Active Directory Administrator Rollen (Azure AD)](https://docs.microsoft.com/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-ad-administrator-roles).
   - Das Onboarding erstellt eine Drittanbieter-APP und einen ersten Dienst Prinzipal in Ihrem Azure AD Mandanten.
- Eine Azure Public Cloud-Umgebung.
- Die Benutzerkonten, die Geräte Aktionen auslösen, müssen die folgenden Voraussetzungen erfüllen:
   - Wurde mit [Azure Active Directory Benutzer](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) Ermittlung und [Active Directory Benutzer](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser)Ermittlung ermittelt.
      - Dies bedeutet, dass das Benutzerkonto in Azure AD ein synchroniziertes Benutzerobjekt sein muss.
   - Die Berechtigung **Configuration Manager Aktion initiieren** unter **Remote Tasks** im Microsoft Endpoint Manager Admin Center.


## <a name="internet-endpoints"></a>Internet Endpunkte

- `https://aka.ms/configmgrgateway`
- `https://gateway.configmgr.manage.microsoft.com`
- `https://us.gateway.configmgr.manage.microsoft.com`
- `https://eu.gateway.configmgr.manage.microsoft.com`


## <a name="enable-device-upload"></a>Aktivieren des Geräte Uploads

- Wenn Sie derzeit die Co-Verwaltung aktiviert haben, bearbeiten Sie die [Eigenschaften der Co-Verwaltung](#bkmk_edit) , um den Geräte Upload zu aktivieren.
- Wenn Sie die Co-Verwaltung nicht aktiviert haben, [verwenden Sie den Assistenten zum **Konfigurieren der Co-Verwaltung** ](#bkmk_config) , um den Geräte Upload zu aktivieren.
   - Sie können Ihre Geräte hochladen, ohne die automatische Registrierung für die Co-Verwaltung zu aktivieren oder Workloads zu InTune zu wechseln.
- Alle von Configuration Manager verwalteten Geräte mit **Ja** in der Spalte **Client** werden hochgeladen. Bei Bedarf können Sie den Upload auf eine einzelne Geräte Sammlung beschränken.

### <a name="edit-co-management-properties-to-enable-device-upload"></a><a name="bkmk_edit"></a>Bearbeiten der Eigenschaften der Co-Verwaltung zum Aktivieren des Geräte Uploads

Wenn Sie derzeit die Co-Verwaltung aktiviert haben, bearbeiten Sie die Eigenschaften der Co-Verwaltung, um den Geräte Upload mithilfe der folgenden Anweisungen zu aktivieren:

1. Wechseln Sie in der Configuration Manager-Verwaltungskonsole zu **Verwaltung** > **Übersicht** > **Cloud Services** > **Co-Verwaltung**.
1. Klicken Sie mit der rechten Maustaste auf die Co-Verwaltungs Einstellungen, und wählen Sie **Eigenschaften**.
1. Wählen Sie auf der Registerkarte **Upload konfigurieren** die Option **in das Microsoft Endpoint Manager Admin Center hochladen**aus. Klicken Sie auf **Anwenden**.
   - Die Standardeinstellung für den Geräte Upload sind **alle meine Geräte, die von Microsoft Endpoint Configuration Manager verwaltet werden**. Bei Bedarf können Sie den Upload auf eine einzelne Geräte Sammlung beschränken.

   [![Konfigurations-Assistent für die Co-Verwaltung](./media/3555758-configure-upload.png)](./media/3555758-configure-upload.png#lightbox)
1. Melden Sie sich bei entsprechender Aufforderung mit Ihrem *globalen Administrator* Konto an.
1. Klicken Sie auf **Ja** , um die Benachrichtigung **Create Aad Application** zu akzeptieren. Diese Aktion stellt einen Dienst Prinzipal bereit und erstellt eine Azure AD Anwendungs Registrierung, um die Synchronisierung zu vereinfachen.
1. Klicken Sie auf **OK** , um die Eigenschaften der Co-Verwaltung zu beenden, nachdem Sie die Änderungen vorgenommen haben.


### <a name="use-the-configure-co-management-wizard-to-enable-device-upload"></a><a name="bkmk_config"></a>Aktivieren des Geräte Uploads mithilfe des Assistenten zum Konfigurieren der Co-Verwaltung
Wenn Sie die Co-Verwaltung nicht aktiviert haben, verwenden Sie den Assistenten zum **Konfigurieren der Co-Verwaltung** , um den Geräte Upload zu aktivieren. Sie können Ihre Geräte hochladen, ohne die automatische Registrierung für die Co-Verwaltung zu aktivieren oder Workloads zu InTune zu wechseln. Aktivieren Sie den Geräte Upload mithilfe der folgenden Anweisungen:

1. Wechseln Sie in der Configuration Manager-Verwaltungskonsole zu **Verwaltung** > **Übersicht** > **Cloud Services** > **Co-Verwaltung**.
1. Klicken Sie im Menüband auf **Co-Verwaltung konfigurieren** , um den Assistenten zu öffnen.
1. Wählen Sie auf der Seite für das Mandanten- **Onboarding** die Option **azurepubliccloud** für Ihre Umgebung aus. Azure Government Cloud wird nicht unterstützt.
1. Klicken Sie auf **Anmelden**. Melden Sie sich mit Ihrem *globalen Administrator* Konto an.
1. Stellen Sie sicher, dass die Option **auf das Microsoft Endpoint Manager Admin Center hochladen** auf der Seite für das **Onboarding** von Mandanten ausgewählt ist.
   - Stellen Sie sicher, dass die Option **automatische Client Registrierung für die Co-Verwaltung aktivieren** nicht aktiviert ist, wenn Sie die Co-Verwaltung jetzt nicht aktivieren möchten. Wenn Sie die Co-Verwaltung aktivieren möchten, wählen Sie die Option aus.
   - Wenn Sie die Co-Verwaltung zusammen mit dem Hochladen von Geräten aktivieren, erhalten Sie weitere Seiten im Assistenten, um den Vorgang abzuschließen. Weitere Informationen finden Sie unter [Aktivieren der Co-Verwaltung](../comanage/how-to-enable.md).

   [![Konfigurations-Assistent für die Co-Verwaltung](./media/3555758-comanagement-wizard.png)](./media/3555758-comanagement-wizard.png#lightbox)
1. Klicken Sie auf **weiter** und dann auf **Ja** , um die Benachrichtigung **Create Aad Application** zu akzeptieren. Diese Aktion stellt einen Dienst Prinzipal bereit und erstellt eine Azure AD Anwendungs Registrierung, um die Synchronisierung zu vereinfachen.
1. Wählen Sie auf der Seite **Upload konfigurieren** die empfohlene Einstellung für den Geräte Upload für alle Geräte aus, die **von Microsoft Endpoint Configuration Manager verwaltet**werden. Bei Bedarf können Sie den Upload auf eine einzelne Geräte Sammlung beschränken.
1. Klicken Sie auf **Zusammenfassung** , um Ihre Auswahl zu überprüfen, **und klicken Sie**
1. Wenn der Assistent abgeschlossen ist, klicken Sie auf **Schließen**.  


## <a name="review-your-upload"></a><a name="bkmk_review"></a>Überprüfen des Uploads

1. Öffnen Sie **cmgatewaysyncuploadworker. log** aus &lt;ConfigMgr-Installationsverzeichnis> \Logs.
1. Der nächste Synchronisierungs Zeitpunkt wird durch Protokolleinträge wie angegeben `Next run time will be at approximately: 02/28/2020 16:35:31`.
1. Suchen Sie `Batching N records`für Geräte Uploads nach Protokoll Einträgen ähnlich wie. **N** ist die Anzahl von Geräten, die in die Cloud hochgeladen werden. 
1. Der Upload erfolgt alle 15 Minuten, wenn Änderungen vorgenommen werden. Nachdem die Änderungen hochgeladen wurden, kann es bis zu 10 Minuten dauern, bis Client Änderungen im **Microsoft Endpoint Manager Admin Center**angezeigt werden.

## <a name="perform-device-actions"></a>Ausführen von Geräte Aktionen

1. Navigieren Sie in einem Browser zu.`endpoint.microsoft.com`
1. Wählen Sie **Geräte** und dann **alle Geräte** aus, um die hochgeladenen Geräte anzuzeigen. **ConfigMgr** wird in der Spalte **verwaltet von** für hochgeladene Geräte angezeigt.
   [![Alle Geräte im Microsoft Endpoint Manager Admin Center](./media/3555758-all-devices.png)](./media/3555758-all-devices.png#lightbox)
1. Klicken Sie auf ein Gerät, um seine **Übersichts** Seite zu laden.
1. Klicken Sie auf eine der folgenden Aktionen:
   - **Synchronisierungs Computer Richtlinie**
   - **Benutzer Richtlinie synchronisieren**
   - **App-Evaluierungszeitraum**

   [![Geräte Übersicht im Microsoft Endpoint Manager Admin Center](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)

## <a name="known-issues"></a>Bekannte Probleme

### <a name="specific-devices-dont-synchronize"></a>Bestimmte Geräte werden nicht synchronisiert

<!--7099564-->
Es ist möglich, dass bestimmte Geräte, die Configuration Manager Clients sind, nicht in den Dienst hochgeladen werden.

**Betroffene Geräte:** Wenn ein Gerät ein Verteilungs Punkt ist, von dem das gleiche PKI-Zertifikat für die Verteilungs Punkt Funktion und den Client-Agent verwendet wird, wird das Gerät nicht in die Synchronisierung des Anfüge Geräts des Geräts eingeschlossen.

**Verhalten:** Wenn Sie während der Onboarding-Phase das Anfügen von Mandanten durchführen, wird beim ersten Mal eine vollständige Synchronisierung durchgeführt. Nachfolgende Synchronisierungs Zyklen sind Delta Synchronisierungs Zyklen. Jedes Update der betroffenen Geräte bewirkt, dass das Gerät aus der Synchronisierung entfernt wird.

## <a name="log-files"></a>Protokolldateien
Verwenden Sie die folgenden Protokolle auf dem Dienst Verbindungspunkt:

- **Cmgatewaysyncuploadworker. log**
- **Cmgatewaynotificationworker. log**

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zum Anfügen von Protokolldateien für den Mandanten finden Sie unter Problembehandlung beim [Anfügen](technical-reference.md)von Mandanten.
