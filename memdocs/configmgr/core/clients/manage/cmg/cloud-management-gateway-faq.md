---
title: CMG-FAQ
titleSuffix: Configuration Manager
description: In diesem Artikel finden Sie Antworten auf häufig gestellte Fragen zu Cloud Management Gateway.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 06/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 4c1a128d-22fb-49f1-8e0b-36513a8dc117
ms.openlocfilehash: ecc91168cc90af58c40903ea3d288eeaa82be7a0
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502237"
---
# <a name="frequently-asked-questions-about-the-cloud-management-gateway"></a>Häufig gestellte Fragen zu Cloud Management Gateway

*Gilt für: Configuration Manager (Current Branch)*

In diesem Artikel finden Sie Antworten auf häufig gestellte Fragen zu Cloud Management Gateway (CMG). Weitere Informationen finden Sie unter [Planen von Cloud Management Gateway in Configuration Manager](plan-cloud-management-gateway.md).

## <a name="frequently-asked-questions"></a>Häufig gestellte Fragen

### <a name="what-certificates-do-i-need"></a>Welche Zertifikate benötige ich?

Weitere Informationen finden Sie unter [Zertifikate für Cloud Management Gateway](certificates-for-cloud-management-gateway.md).

### <a name="do-i-need-azure-expressroute"></a>Benötige ich Azure ExpressRoute?

Nein. Mit [Azure ExpressRoute](/azure/expressroute/expressroute-introduction) können Sie Ihr lokales Netzwerk mit der Microsoft-Cloud verbinden und dadurch erweitern. ExpressRoute oder andere virtuelle Netzwerkverbindungen sind nicht für das Configuration Manager-CMG erforderlich. Mit dem CMG können internetbasierte Clients ohne zusätzliche Netzwerkkonfiguration über den Azure-Dienst mit lokalen Standortsystemen kommunizieren. Weitere Informationen finden Sie unter [Planen von Cloud Management Gateway](plan-cloud-management-gateway.md).

<!-- SCCMDocs#1659 -->

### <a name="do-i-need-to-maintain-the-azure-virtual-machines"></a>Muss ich virtuelle Azure-Computer warten?

Eine Wartung ist nicht erforderlich. Das CMG nutzt die PaaS-Hostingoption (Platform-as-a-Service) von Azure. Mit dem von Ihnen bereitgestellten Abonnement erstellt Configuration Manager die notwendigen virtuellen Computer (VMs), den Speicher und das Netzwerk. Azure sichert und aktualisiert die virtuellen Computer. Anders als bei Infrastructure-as-a-Service (IaaS) sind diese VMs kein Teil Ihrer lokalen Umgebung. Das CMG ist ein PaaS-Dienst, mit der die Configuration Manager-Umgebung mit der Cloud verbunden und dadurch erweitert wird. Weitere Informationen finden Sie unter [Schützen von PaaS-Bereitstellungen](/azure/security/security-paas-deployments).

### <a name="how-can-i-ensure-service-continuity-during-service-updates"></a>Wie kann ich die Dienstkontinuität während Dienstupdates sicherstellen?

Durch die Skalierung von CMG auf zwei oder mehr Instanzen profitieren Sie automatisch von Updatedomänen in Azure. Weitere Informationen finden Sie unter [Gewusst wie: Aktualisieren eines Clouddiensts](/azure/cloud-services/cloud-services-update-azure-service).

### <a name="im-already-using-ibcm-if-i-add-cmg-how-do-clients-behave"></a>Ich verwende bereits IBCM. Wie ändert sich das Clientverhalten, wenn ich zusätzlich das CMG nutze?

Wenn Sie bereits einen [IBCM-Dienst](../plan-internet-based-client-management.md) (internet-based client management, internetbasierte Clientverwaltung) bereitgestellt haben, können Sie zusätzlich auch das CMG bereitstellen. Clients empfangen für beide Dienste Richtlinien. Sobald die Clients mit dem Internet verbunden sind, wählen sie zufällig einen dieser internetbasierten Dienste aus und nutzen diesen.

### <a name="do-the-user-accounts-have-to-be-in-the-same-azure-ad-tenant-as-the-tenant-associated-with-the-subscription-that-hosts-the-cmg-cloud-service"></a><a name="bkmk_tenant"></a> Müssen sich die Benutzerkonten im gleichen Azure AD-Mandanten befinden wie der Mandant, der mit dem Abonnement verbunden ist, das den CMG-Clouddienst hostet?
<!--SCCMDocs-pr issue #2873-->
Nein, Sie können CMG in jedem Abonnement bereitstellen, das Azure Cloud Services hosten kann.

Zur Verdeutlichung der Begriffe:

- Der _Mandant_ ist das Verzeichnis von Benutzerkonten und App-Registrierungen. Ein Mandant kann mehrere Abonnements haben.
- Mit einem _Abonnement_ werden Abrechnung, Ressourcen und Dienste getrennt. Es ist einem einzelnen Mandanten zugeordnet.

Diese Frage kommt in folgenden Szenarios häufig zur Sprache:  

- Wenn Sie unterschiedliche Azure AD-Test- und Produktionsumgebungen haben, aber nur ein einzelnes Azure-Hostingabonnement.

- Die Verwendung von Azure hat sich mit der Zeit in unterschiedlichen Teams organisch entwickelt.

Wen Sie eine Resource Manager-Bereitstellung verwenden, integrieren Sie den Azure AD-Mandanten, der dem Abonnement zugeordnet ist. Über diese Verbindung kann Configuration Manager eine Authentifizierung bei Azure vornehmen, um CMG zu erstellen, bereitzustellen und zu verwalten.  

Wenn Sie die Azure AD-Authentifizierung für die über CMG verwalteten Benutzer und Gerät nutzen, integrieren Sie diesen Azure AD-Mandanten. Weitere Informationen zu Azure-Diensten für die Cloudverwaltung finden Sie unter [Konfigurieren von Azure-Diensten zur Verwendung mit dem Configuration Manager](../../../servers/deploy/configure/azure-services-wizard.md). Wenn Sie jeden Azure AD-Mandanten integrieren, kann ein einzelnes CMG-Gateway die Azure AD-Authentifizierung für mehrere Mandanten unabhängig vom Hostingspeicherort bereitstellen.

#### <a name="example-1-one-tenant-with-multiple-subscriptions"></a>Beispiel 1: Ein Mandant mit mehreren Abonnements

Alle Benutzeridentitäten, Geräteregistrierungen und App-Registrierungen befinden sich im gleichen Mandanten. Sie können auswählen, welches Abonnement das CMG verwendet. Sie können mehrere CMG-Dienste von einer Site in separaten Abonnements bereitstellen. Die Site hat eine Eins-zu-eins-Beziehung mit dem Mandanten. Sie entscheiden, welche Abonnements aus verschiedenen Gründen wie Abrechnung oder logische Trennung verwendet werden sollen.

#### <a name="example-2-multiple-tenants"></a>Beispiel 2: Mehrere Mandanten

Das heißt, Ihre Umgebung verfügt über mehrere Azure AD-Instanzen. Wenn Sie Benutzer- und Geräteidentitäten in beiden Mandanten unterstützen müssen, müssen Sie die Site jedem Mandanten anfügen. Dieser Prozess erfordert ein administratives Konto von jedem Mandanten, um die App-Registrierungen in diesem Mandanten zu erstellen. Eine Site kann dann CMG-Dienste in mehreren Mandanten hosten. Sie können eine CMG-Instanz in einem beliebigen verfügbaren Abonnement in einem der beiden Mandanten erstellen. Geräte, die mit einer der Azure AD-Instanzen verknüpft oder hybrid verknüpft sind, können eine CMG-Instanz verwenden.

Wenn sich die Benutzer- und Geräteidentitäten in einem Mandanten befinden, das CMG-Abonnement aber in einem anderen Mandanten, müssen Sie die Site beiden Mandanten anfügen. Technisch gesehen ist die Client-App für den zweiten Mandanten, der nur über den CMG-Dienst verfügt, nicht erforderlich. Die Client-App bietet nur Benutzer- und Geräteauthentifizierung für Clients, die den CMG-Dienst verwenden.<!-- SCCMDocs#1902 -->

### <a name="how-does-cmg-affect-my-clients-connected-via-vpn"></a>Wie wirkt sich CMG auf meine über VPN verbundenen Clients aus?

Roamingclients, die über ein VPN eine Verbindung mit Ihrer Umgebung herstellen, werden häufig als Clients mit Intranetzugriff erkannt. Sie versuchen, eine Verbindung mit Ihrer lokalen Infrastruktur herzustellen, z.B. Verwaltungspunkten und Verteilungspunkten. Einige Kunden bevorzugen es, diese Roamingclients auch dann von Clouddiensten verwalten zu lassen, wenn sie über VPN verbunden sind. Ab Version 1902 ordnen Sie dem CMG eine Begrenzungsgruppe zu. Dadurch werden diese Clients gezwungen, die lokalen Standortsysteme nicht zu verwendet. Weitere Informationen finden Sie unter [Configure boundary groups](setup-cloud-management-gateway.md#configure-boundary-groups) (Konfigurieren von Begrenzungsgruppen).

### <a name="if-i-enable-a-cmg-will-my-clients-only-connect-to-the-cmg-enabled-management-point-when-theyre-connected-to-the-intranet"></a>Wenn ich ein CMG aktiviere, stellen dann meine Clients nur eine Verbindung mit dem für CMG aktivierten Verwaltungspunkt her, wenn sie mit dem Intranet verbunden sind?

Um vertraulichen Datenverkehr über ein CMG zu sichern, konfigurieren Sie entweder einen HTTPS-Verwaltungspunkt oder verwenden Sie erweitertes HTTP.

Wenn Sie sich für das Bereitstellen eines CMG entscheiden und PKI-Zertifikate für die HTTPS-Kommunikation auf dem für CMG aktivierten Verwaltungspunkt verwenden, wählen Sie unter den Verwaltungspunkteigenschaften die Option **Nur Internetclients zulassen** aus. Durch diese Einstellung wird sichergestellt, dass interne Clients weiterhin HTTP-Verwaltungspunkte in Ihrer Umgebung verwenden.

Wenn Sie erweitertes HTTP verwenden, müssen Sie diese Einstellung nicht konfigurieren. Clients verwenden weiterhin HTTP bei der direkten Kommunikation mit dem für CMG aktivierten Verwaltungspunkt. Weitere Informationen finden Sie unter [Enhanced HTTP (Erweitertes HTTP)](../../../plan-design/hierarchy/enhanced-http.md).

### <a name="what-are-the-differences-with-client-authentication-between-azure-ad-and-certificates"></a>Welche Unterschiede bestehen zwischen Azure AD und Zertifikaten in Bezug auf die Clientauthentifizierung?
<!-- MEMDocs#277 -->
Sie können Azure AD oder ein [Clientauthentifizierungszertifikat](certificates-for-cloud-management-gateway.md#bkmk_clientauth) verwenden, um Geräte beim CMG-Dienst zu authentifizieren.

Wenn Sie herkömmliche Windows-Clients mit einer Identität verwalten, die der Active Directory-Domäne beigetreten ist, benötigen diese Clients PKI-Zertifikate zur Sicherung des Kommunikationskanals. Zu diesen Clients zählen u. a. Windows 8.1 und Windows 10. Sie können alle von CMG unterstützten Features verwenden, die Verteilung der Software selbst ist auf die Geräte beschränkt. Installieren Sie den Configuration Manager-Client, bevor das Gerät eine Verbindung mit dem Internet herstellt. Bei Version 2002 oder höher verwenden Sie die Tokenauthentifizierung.

Sie können auch Windows 10-Clients mit moderner Identität verwalten, die einer hybriden oder reinen Azure AD-Clouddomäne beigetreten sind. Clients verwenden Azure AD eher für die Authentifizierung als für PKI-Zertifikate. Mit Azure AD ist die Einrichtung, Konfiguration und Verwaltung einfacher als mit komplexeren PKI-Systemen. Sie können dieselben Verwaltungsaktivitäten sowie die Softwareverteilung an die Benutzer ausführen. Außerdem stehen Ihnen weitere Methoden zum Installieren des Clients auf einem Remotegerät zur Verfügung.

Microsoft empfiehlt, Geräte zu Azure AD hinzuzufügen. Internetbasierte Geräte können Azure AD verwenden, um sich mit Configuration Manager zu authentifizieren. Außerdem werden sowohl Geräte- als auch Benutzerszenarios ermöglicht, unabhängig davon, ob das Gerät mit dem Internet oder dem internen Netzwerk verbunden ist. Weitere Informationen finden Sie unter [Installieren und Registrieren des Clients mithilfe einer Azure AD-Identität](../../deploy/deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity).

## <a name="next-steps"></a>Nächste Schritte

- [Planen des Cloudverwaltungsgateways](plan-cloud-management-gateway.md)
- [Einrichten des Cloudverwaltungsgateways](setup-cloud-management-gateway.md)
- [Zertifikate für Cloud Management Gateway](certificates-for-cloud-management-gateway.md)
- [Sicherheit und Datenschutz für Cloud Management Gateway](security-and-privacy-for-cloud-management-gateway.md)
- [Größe und Skalierungszahlen für das Cloudverwaltungsgateway](../../../plan-design/configs/size-and-scale-numbers.md#bkmk_cmg)
