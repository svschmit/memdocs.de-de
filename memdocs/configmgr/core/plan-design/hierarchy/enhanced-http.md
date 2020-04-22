---
title: Erweitertes HTTP
titleSuffix: Configuration Manager
description: Verwenden Sie moderne Authentifizierungsmethoden, um die Clientkommunikation ohne PKI-Zertifikate zu sichern.
ms.date: 03/28/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4deac022-e397-4f1f-bc0a-cea6c6c6368d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bb14830e99600da1b71c516a44d51a0090cdc673
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703568"
---
# <a name="enhanced-http"></a>Erweitertes HTTP

*Gilt für: Configuration Manager (Current Branch)*

<!--1356889,1358460-->

> [!Tip]  
> Dieses Feature wurde erstmals in Version 1806 als [Vorabfeature](../../servers/manage/pre-release-features.md) eingeführt. Ab Version 1810 ist dieses Feature kein Vorabfeature mehr.  

Microsoft empfiehlt zwar die HTTPS-Kommunikation für alle Configuration Manager-Kommunikationspfade, diese kann jedoch aufgrund der aufwändigen Verwaltung von PKI-Zertifikaten für einige Kunden schwierig sein.

Version 1806 von Configuration Manager bietet Verbesserungen der Kommunikation von Clients mit Standortsystemen. Diese Verbesserungen verfolgen zwei Hauptziele:  

- Sie können vertrauliche Clientkommunikation ohne PKI-Serverauthentifizierungszertifikate sichern.  

- Clients können ohne Netzwerkzugriffskonto, PKI-Clientzertifikat und Windows-Authentifizierung sicher von Verteilungspunkten auf Inhalt zugreifen.  

Jegliche andere Clientkommunikation erfolgt über HTTP. Erweitertes HTTP ist nicht das Gleiche wie das Aktivieren von HTTPS für die Clientkommunikation oder ein Standortsystem.<!-- SCCMDocs issue #1212 -->

> [!Note]  
> PKI-Zertifikate eignen sich aber weiterhin für Kunden mit den folgenden Anforderungen:  
>
> - Die gesamte Clientkommunikation findet über HTTPS statt  
> - Erweiterte Kontrolle der Infrastruktur für die Signierung
>
> Wenn Sie außerdem PKI bereits verwenden, wird das in IIS eingebundene PKI-Zertifikat auch dann verwendet, wenn erweitertes HTTP aktiviert ist.



## <a name="scenarios"></a><a name="bkmk_scenario"></a> Szenarios

Die folgenden Szenarios profitieren von diesen Verbesserungen:  

### <a name="scenario-1-client-to-management-point"></a><a name="bkmk_scenario1"></a> Szenario 1: Client zu Verwaltungspunkt

<!--1356889-->
[In Azure Active Directory (Azure AD) eingebundene Geräte](/azure/active-directory/devices/concept-azure-ad-join) können mit einem Verwaltungspunkt kommunizieren, der für HTTP konfiguriert ist. Der Standortserver generiert ein Zertifikat für den Verwaltungspunkt, sodass er über einen sicheren Kanal kommunizieren kann.

> [!Note]  
> Dieses Verhalten stellt eine Änderung gegenüber der aktuellen Version 1802 von Configuration Manager dar, die einen HTTPS-fähigen Verwaltungspunkt für in Azure AD eingebundene Clients erfordert, die über ein Cloud Management Gateway kommunizieren. Weitere Informationen finden Sie unter [Verwaltungspunkt für HTTPS aktivieren](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

### <a name="scenario-2-client-to-distribution-point"></a><a name="bkmk_scenario2"></a> Szenario 2: Client zu Verteilungspunkt

<!--1358228-->
Eine Arbeitsgruppe oder ein in Azure AD eingebundener Client kann über einen sicheren Kanal von einem für HTTP konfigurierten Verteilungspunkt Inhalt authentifizieren und herunterladen. Diese Art von Geräten kann außerdem ohne ein PKI-Zertifikat für den Client Inhalt von einem Verteilungspunkt authentifizieren und herunterladen, der für HTTPS konfiguriert ist. Das Hinzufügen eines Clientauthentifizierungszertifikats zu einer Arbeitsgruppe oder einem mit Azure AD verbundenen Client ist kompliziert.

Dieses Verhalten umfasst die Bereitstellung von Betriebssystemen mit einer Tasksequenz, die über Startmedien, PXE oder das Softwarecenter ausgeführt wird. Weitere Informationen finden Sie unter [Netzwerkzugriffskonto](accounts.md#network-access-account).<!--1358278-->

### <a name="scenario-3-azure-ad-device-identity"></a><a name="bkmk_scenario3"></a> Szenario 3: Azure AD-Geräteidentität

<!--1358460-->
Ein in Azure AD eingebundenes oder [hybrides Azure AD-Gerät](/azure/active-directory/devices/concept-azure-ad-join-hybrid) kann sicher mit seinem zugewiesenen Standort kommunizieren, ohne dass ein Azure AD-Benutzer angemeldet ist. Die cloudbasierte Geräteidentität reicht jetzt für die CMG- und Verwaltungspunktauthentifizierung für geräteorientierte Szenarios aus. (In benutzerorientierten Szenarios ist weiterhin ein Benutzertoken erforderlich.)  


## <a name="features"></a>Features

Die folgenden Features von Configuration Manager unterstützen oder erfordern erweitertes HTTP:

- [Cloudverwaltungsgateway](../../clients/manage/cmg/plan-cloud-management-gateway.md)
- [Betriebssystembereitstellung ohne Netzwerkzugriffskonto](../../../osd/plan-design/planning-considerations-for-automating-tasks.md#enhanced-http)
- [Aktivieren der Co-Verwaltung für neue internetbasierte Windows 10-Geräte](../../../comanage/tutorial-co-manage-new-devices.md)
- [Genehmigen von Apps per E-Mail](../../../apps/deploy-use/app-approval.md#bkmk_email-approve)
- [Verwaltungsdienst](../../../develop/adminservice/overview.md)
- [Anzeigen kürzlich verbundener Konsolen](../../servers/manage/admin-console.md#bkmk_viewconnected)

> [!Note]  
> Der Softwareupdatepunkt und die zugehörigen Szenarios haben schon immer den sicheren HTTP-Datenverkehr mit Clients und Cloud Management Gateway unterstützt. Dabei wird ein Mechanismus mit dem Verwaltungspunkt verwendet, der sich von der zertifikat- oder tokenbasierten Authentifizierung unterscheidet.<!-- SCCMDocs issue #1148 -->


## <a name="prerequisites"></a>Voraussetzungen  

- Ein Verwaltungspunkt, der für HTTP-Clientverbindungen konfiguriert ist. Legen Sie diese Option auf der Registerkarte **Allgemein** der Eigenschaften der Verwaltungspunktrolle fest.  

- Ein für HTTP-Clientverbindungen konfigurierter Verteilungspunkt. Legen Sie diese Option auf der Registerkarte **Kommunikation** der Eigenschaften der Verteilungspunktrolle fest. Aktivieren Sie nicht die Option **Allow clients to connect anonymously** (Anonyme Verbindung von Clients zulassen).  

- Integrieren Sie den Standort zur Cloudverwaltung in Azure AD.  

    - Wenn diese Voraussetzung für Ihren Standort bereits erfüllt ist, müssen Sie die Azure AD-Anwendung aktualisieren. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Clouddienste**, und wählen Sie **Azure Active Directory-Mandanten** aus. Wählen Sie den Azure AD-Mandanten und die Webanwendung im Bereich **Anwendungen** aus, und klicken Sie anschließend im Menüband auf **Update application setting** (Anwendungseinstellungen aktualisieren).  

- *Nur[ für ](#bkmk_scenario3)Szenario 3*: Ein in Azure AD eingebundener Client, auf dem Windows 10, Version 1803 oder höher, ausgeführt wird. Der Client erfordert diese Konfiguration für die Azure AD-Geräteauthentifizierung.<!-- SCCMDocs issue 1126 -->


## <a name="configure-the-site"></a>Konfigurieren des Standorts

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie die Option **Standortkonfiguration**, und klicken Sie auf den Knoten **Standorte**. Wählen Sie den Standort aus, und klicken Sie im Menüband auf **Eigenschaften**.  

2. Wechseln Sie zur Registerkarte **Clientcomputerkommunikation**.

    > [!Note]
    > Ab Version 1906 heißt diese Registerkarte **Sichere Kommunikation**.<!-- SCCMDocs#1645 -->  

    Wählen Sie die Option für **HTTPS oder HTTP** aus. Aktivieren Sie anschließend die Option **Für HTTP-Websitesysteme von Configuration Manager generierte Zertifikate verwenden**.

> [!Tip]
> Es dauert bis zu 30 Minuten, bis der Verwaltungspunkt das neue Zertifikat vom Standort empfängt und konfiguriert.

<!--3798957-->
Ab Version 1902 können Sie erweitertes HTTP auch für den Standort der zentralen Verwaltung aktivieren. Führen Sie den gleichen Prozess durch, und öffnen Sie die Eigenschaften des Standorts der zentralen Verwaltung. Durch diese Aktion wird erweitertes HTTP nur für die SMS-Anbieterrollen am Standort der zentralen Verwaltung aktiviert. Dies ist keine globale Einstellung, die für alle Standorte in der Hierarchie gilt.

Sie können diese Zertifikate in der Configuration Manager-Konsole anzeigen. Wechseln Sie zum Arbeitsbereich **Verwaltung**, erweitern Sie **Sicherheit**, und wählen Sie den **Zertifikate**-Knoten aus. Suchen Sie nach dem **SMS-Ausgabe**-Stammzertifikat sowie den vom „SMS-Ausgabe“-Stamm ausgegebenen Standortserverrollen-Zertifikaten.

Weitere Informationen zur Kommunikation zwischen dem Client und dem Verwaltungs- und Verteilungspunkt mit dieser Konfiguration finden Sie unter [Communications from clients to site systems and services (Kommunikation zwischen Clients und Standortsystemen und -diensten)](communications-between-endpoints.md#Planning_Client_to_Site_System).


## <a name="see-also"></a>Weitere Informationen:

- [Planen der Sicherheit](../security/plan-for-security.md)  

- [Sicherheit und Datenschutz für Konfigurations-Manager-Clients](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Konfigurieren der Sicherheit](../security/configure-security.md)  

- [Datenübertragungen zwischen Endpunkten](communications-between-endpoints.md)  
