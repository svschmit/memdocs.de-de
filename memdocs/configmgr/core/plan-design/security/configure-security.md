---
title: Konfigurieren der Sicherheit
titleSuffix: Configuration Manager
description: Konfigurieren von sicherheitsbezogenen Optionen für Configuration Manager.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 552e7e3d-e584-4a7c-9155-0f796a14b678
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bc9718bef61544b45a1432099ebb9d0911367ea7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701408"
---
# <a name="configure-security-in-configuration-manager"></a>Konfigurieren der Sicherheit in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Anhand der Informationen in diesem Artikel können Sie die folgenden sicherheitsbezogenen Optionen für Configuration Manager einrichten. Folgende Sicherheitsoptionen werden behandelt:
- [Kommunikation mit Clientcomputern](#BKMK_ConfigureClientPKI) für PKI-Clientzertifikate  
- [Signierung und Verschlüsselung](#BKMK_ConfigureSigningEncryption)  
- [Rollenbasierte Verwaltung](#BKMK_ConfigureRBA)  
- [Verwalten von Konten](#BKMK_ManageAccounts)  
- [Konfigurieren von Azure Active Directory](#bkmk_azuread)  
- [Konfigurieren der Authentifizierung von SMS-Anbietern](#bkmk_auth)  



##  <a name="configure-settings-for-client-pki-certificates"></a><a name="BKMK_ConfigureClientPKI"></a> Konfigurieren von Einstellungen für Client-PKI-Zertifikate  

Wenn Sie Public Key-Infrastrukturzertifikate (PKI) für Clientverbindungen mit Standortsystemen verwenden möchten, von denen Internet Information Services (IIS) verwendet werden, konfigurieren Sie die Einstellungen für diese Zertifikate mithilfe des folgenden Verfahrens.  

#### <a name="to-configure-client-pki-certificate-settings"></a>So konfigurieren Sie Einstellungen von Client-PKI-Zertifikaten  

1.  Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Standorte** aus. Wählen Sie den zu konfigurierenden primären Standort aus.  

2.  Klicken Sie im Menüband auf **Eigenschaften**. Wechseln Sie dann zur Registerkarte **Clientcomputerkommunikation**.  

    > [!Note]
    > Ab Version 1906 heißt diese Registerkarte **Sichere Kommunikation**.<!-- SCCMDocs#1645 -->  

3.  Wählen Sie die Einstellungen für Standortsysteme aus, die IIS verwenden.  

    - **Nur HTTPS:** Clients, die einem Standort zugewiesen sind, verwenden immer ein PKI-Clientzertifikat, wenn sie mit Standortsystemen verbunden werden, die IIS nutzen.  

    - **HTTPS oder HTTP:** Die Verwendung von PKI-Zertifikaten ist für Clients nicht erforderlich.  

    - **Für HTTP-Websitesysteme von Configuration Manager generierte Zertifikate verwenden:** Weitere Informationen finden Sie unter [Enhanced HTTP](../hierarchy/enhanced-http.md) (Erweitertes HTTP).  

4.  Wählen Sie die Einstellungen für Clientcomputer aus.  

    - **Use client PKI certificate (client authentication capability) when available** (PKI-Clientzertifikat (Clientauthentifizierungsfunktion) verwenden, sofern verfügbar): Wenn Sie die Standortservereinstellung **HTTPS oder HTTP** ausgewählt haben, wählen Sie diese Option aus, um ein Client-PKI-Zertifikat für HTTP-Verbindungen zu verwenden. Zur Authentifizierung bei Standortsystemen wird vom Client dieses Zertifikat anstatt eines selbstsignierten Zertifikats verwendet. Wenn Sie **Nur HTTPS** ausgewählt haben, wird diese Option automatisch ausgewählt.  

    Wenn mehrere gültige PKI-Clientzertifikate für einen Client verfügbar sind, klicken Sie auf **Ändern**, um die Auswahlmethoden für das Clientzertifikat zu konfigurieren.  

    Weitere Informationen zur Clientauswahlmethode finden Sie unter [Planning for PKI client certificate selection (Planen der PKI-Clientzertifikatauswahl)](plan-for-security.md#BKMK_PlanningForClientCertificateSelection).  

    - **Die Zertifikatsperrliste für Standortsysteme wird von Clients überprüft:** Aktivieren Sie diese Einstellung für Clients, damit diese die Zertifikatsperrliste Ihrer Organisation auf gesperrte Zertifikate überprüfen.  

    Weitere Informationen zur Überprüfung der Zertifikatsperrlisten durch Clients finden Sie unter [Planning for PKI certificate revocation (Planen der PKI-Zertifikatsperrung)](plan-for-security.md#BKMK_PlanningForCRLs).  

5.  Zum Importieren, Anzeigen und Löschen der Zertifikate für vertrauenswürdige Stammzertifizierungsstellen klicken Sie auf **Festlegen**.  

    Weitere Informationen finden Sie unter [Planen von vertrauenswürdigen PKI-Stammzertifikaten und der Liste der Zertifikataussteller](plan-for-security.md#BKMK_PlanningForRootCAs).  


Wiederholen Sie diesen Vorgang für alle primären Standorte in der Hierarchie.  



##  <a name="configure-signing-and-encryption"></a><a name="BKMK_ConfigureSigningEncryption"></a> Konfigurieren von Signierung und Verschlüsselung  

Konfigurieren Sie für Standortsysteme die sichersten Einstellungen für Signierung und Verschlüsselung, die von allen Clients des Standorts unterstützt werden können. Diese Einstellungen sind vor allem dann wichtig, wenn Sie Kommunikation zwischen Clients und Standortsystemen mithilfe selbstsignierter Zertifikate und über HTTP zulassen.  

#### <a name="to-configure-signing-and-encryption-for-a-site"></a>So konfigurieren Sie die Signierung und Verschlüsselung für einen Standort  

1.  Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Standorte** aus. Wählen Sie den zu konfigurierenden primären Standort aus.  

2.  Klicken Sie im Menüband auf **Eigenschaften**, und wechseln Sie dann zur Registerkarte **Signierung und Verschlüsselung**.  

    Diese Registerkarte ist nur an einem primären Standort verfügbar. Wenn die Registerkarte **Signierung und Verschlüsselung** nicht angezeigt wird, sollten Sie sicherstellen, dass Sie nicht mit einem Standort der zentralen Verwaltung oder einem sekundären Standort verbunden sind.  

3.  Konfigurieren Sie die Signierungs- und Verschlüsselungsoptionen für die Kommunikation von Clients mit dem Standort.  

    - **Signierung erforderlich:** Clients signieren Daten vor dem Senden an den Verwaltungspunkt.  

    - **SHA-256 erforderlich:** Clients verwenden den SHA-256-Algorithmus beim Signieren von Daten.  

    > [!WARNING]  
    >  Legen Sie **SHA-256 erforderlich** nicht fest, ohne zuvor sicherzustellen, dass alle Clients diesen Hashalgorithmus unterstützen. Zu diesen Clients gehören auch jene, die dem Standort in der Zukunft zugewiesen werden.  
    >   
    >  Wenn Sie diese Option auswählen, und Clients mit selbstsignierten Zertifikaten den SHA-256-Algorithmus nicht unterstützen, werden sie von Configuration Manager zurückgewiesen. Die Komponente SMS_MP_CONTROL_MANAGER protokolliert die Nachrichten-ID 5443.  

    - **Verschlüsselung verwenden:** Clients verschlüsseln Clientinventurdaten und Statusmeldungen vor dem Senden an den Verwaltungspunkt. Sie verwenden den 3DES-Algorithmus.  

Wiederholen Sie diesen Vorgang für alle primären Standorte in der Hierarchie.  



##  <a name="configure-role-based-administration"></a><a name="BKMK_ConfigureRBA"></a> Konfigurieren der rollenbasierten Verwaltung  

Bei der rollenbasierten Verwaltung werden Sicherheitsrollen, Sicherheitsbereiche und zugewiesene Sammlungen kombiniert, um den Verwaltungsbereich für jeden Administrator zu definieren. Zu einem Bereich gehören die Objekte, die Benutzer in der Konsole anzeigen können, und die Tasks im Zusammenhang mit diesen Objekten, zu deren Ausführung sie berechtigt sind. Die Konfigurationen der rollenbasierten Verwaltung werden auf jeden Standort in einer Hierarchie angewendet.  

Weitere Informationen finden Sie unter [Konfigurieren der rollenbasierten Verwaltung](../../servers/deploy/configure/configure-role-based-administration.md). In diesem Artikel werden folgende Aktionen erläutert:  

- Erstellen benutzerdefinierter Sicherheitsrollen  

- Konfigurieren von Sicherheitsrollen  

- Konfigurieren von Sicherheitsbereichen für ein Objekt  

- Konfigurieren von Sammlungen zum Verwalten der Sicherheit  

- Erstellen eines neuen Administrators  

- Ändern des Verwaltungsbereichs eines Administrators  

> [!IMPORTANT]  
>  Von Ihrem eigenen Verwaltungsbereich wird definiert, welche Objekte und Einstellungen Sie zuweisen können, wenn Sie die rollenbasierte Verwaltung für einen anderen Administrator konfigurieren. Informationen zur Planung der rollenbasierten Verwaltung finden Sie unter [Grundlagen der rollenbasierten Verwaltung](../../understand/fundamentals-of-role-based-administration.md).  



##  <a name="manage-accounts-that-configuration-manager-uses"></a><a name="BKMK_ManageAccounts"></a> Verwalten von Konten, die von Configuration Manager verwendet werden  

In Configuration Manager werden Windows-Konten für zahlreiche verschiedene Tasks und Verwendungen unterstützt. Gehen Sie wie folgt vor, um anzuzeigen, welche Konten für verschiedene Tasks konfiguriert sind, und um die Kennwörter zu verwalten, die in Configuration Manager für die einzelnen Konten verwendet werden:  

#### <a name="to-manage-accounts-that-configuration-manager-uses"></a>So verwalten Sie Konten, die von Configuration Manager verwendet werden  

1.  Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Sicherheit**, und wählen Sie den Knoten **Konten** aus.  

2.  Zum Ändern des Kennworts eines Kontos wählen Sie zunächst das Konto in der Liste aus. Klicken Sie dann im Menüband auf **Eigenschaften**.  

3.  Klicken Sie auf **Festlegen**, um das Dialogfeld **Windows-Benutzerkonto** zu öffnen. Geben Sie das neue Kennwort für Configuration Manager an, das für dieses Konto verwendet werden soll.  

    > [!NOTE]  
    >  Das Kennwort, das Sie festlegen, muss dem Kennwort des Kontos in Active Directory entsprechen.  

Weitere Informationen finden Sie unter [In Configuration Manager verwendete Konten](../hierarchy/accounts.md).



##  <a name="configure-azure-active-directory"></a><a name="bkmk_azuread"></a> Konfigurieren von Azure Active Directory

Integrieren Sie Configuration Manager mit Azure Active Directory (Azure AD), um Ihre Umgebung zu vereinfachen und in der Cloud verfügbar zu machen. Ermöglichen Sie das Authentifizieren von Clients und Standorten mithilfe von Azure AD. Weitere Informationen finden Sie in der Beschreibung des Diensts **Cloud Management** unter [Konfigurieren von Azure-Diensten](../../servers/deploy/configure/azure-services-wizard.md).



## <a name="configure-sms-provider-authentication"></a><a name="bkmk_auth"></a> Konfigurieren der Authentifizierung von SMS-Anbietern

Ab Version 1810 können Sie die mindestens erforderliche Authentifizierungsebene für den Administratorzugriff auf Configuration Manager-Standorte angeben. Diese Funktion verpflichtet Administratoren dazu, sich mit der erforderlichen Ebene bei Windows anzumelden. Weitere Informationen finden Sie unter [Planen des SMS-Anbieters](../hierarchy/plan-for-the-sms-provider.md#bkmk_auth). <!--1357013-->  



## <a name="see-also"></a>Weitere Informationen:

- [Planen der Sicherheit](plan-for-security.md)  

- [Sicherheit und Datenschutz für Konfigurations-Manager-Clients](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Datenübertragungen zwischen Endpunkten](../hierarchy/communications-between-endpoints.md)  

- [Technische Referenz für kryptografische Steuerelemente](cryptographic-controls-technical-reference.md)  

- [PKI-Zertifikatanforderungen](../network/pki-certificate-requirements.md)  
