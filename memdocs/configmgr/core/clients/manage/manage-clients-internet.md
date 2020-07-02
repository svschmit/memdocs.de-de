---
title: Verwalten von Clients im Internet
titleSuffix: Configuration Manager
description: In diesem Artikel erhalten Sie Informationen zum Verwalten von Clients mithilfe von Cloud Management Gateway (CMG) und zur internetbasierten Clientverwaltung in Configuration Manager.
ms.date: 06/10/2020
ms.prod: configuration-manager
ms.topic: conceptual
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2840b30bee20d2fa73531b07c095e028979f6274
ms.sourcegitcommit: 2f1963ae208568effeb3a82995ebded7b410b3d4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/11/2020
ms.locfileid: "84715593"
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>Verwalten von Clients im Internet mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In der Regel befinden sich in Configuration Manager die meisten verwalteten Computer und Server in demselben internen Netzwerk wie die Standortsystemserver, die Verwaltungsfunktionen ausführen. Sie können jedoch auch Clients außerhalb des internen Netzwerks verwalten, wenn sie mit dem Internet verbunden sind. Hierbei müssen Clients keine VPN-Verbindung aufbauen, um mit den Standortsystemservern zu kommunizieren.

Configuration Manager bietet zwei Methoden, mit dem Internet verbundene Clients zu verwalten:

- Cloudverwaltungsgateway

- Internetbasierte Clientverwaltung

> [!NOTE]
> Eine Kombination beider Dienste für einen einzigen Standort ist möglich. Wenn ein Gerät Richtlinien vom Standort sowohl für IBCM als auch für CMG erhält, wählt es für die Kommunikation wahllos zwischen diesen. Der einzige verfügbare Mechanismus zur Steuerung der Kommunikation ist die Clientauthentifizierung. Wenn z. B. ein in Azure AD eingebundener Client dem Serverauthentifizierungszertifikat des internetbasierten Verwaltungspunkts nicht vertraut, kann er nur CMG verwenden. Wenn ein in die Domäne eingebundener Client dem Serverauthentifizierungszertifikat von CMG nicht vertraut, kann er nur den internetbasierten Verwaltungspunkt nutzen.<!-- SCCMDocs#1541 -->

## <a name="cloud-management-gateway"></a>Cloudverwaltungsgateway

Mit Cloud Management Gateway (CMG) lassen sich internetbasierte Clients verwalten. Dabei wird eine Kombination aus einem Microsoft Azure-Clouddienst und einer lokalen Standortsystemrolle verwendet, die mit diesem Dienst kommuniziert. Internetbasierte Clients verwenden den Clouddienst, um mit dem lokalen Configuration Manager zu kommunizieren.

### <a name="cmg-advantages"></a>Vorteile von CMG

- Keine zusätzlichen Investitionen in die Infrastruktur vor Ort erforderlich.  

- Lokale Infrastruktur bleibt vom Internet getrennt.  

- Virtuelle Computer in der Cloud, auf denen der Dienst ausgeführt wird, werden vollständig von Azure verwaltet und erfordern keine Wartung.  

- Einfache Einrichtung und Konfiguration in der Configuration Manager-Konsole.  

### <a name="cmg-disadvantages"></a>Nachteile von CMG  

- Cloud-Abonnement-Kosten.  

- Verwaltungsdaten werden über Cloud-Dienst gesendet.  

Weitere Informationen finden Sie unter [Planen des Cloudverwaltungsgateways](cmg/plan-cloud-management-gateway.md).  

## <a name="internet-based-client-management"></a>Internetbasierte Clientverwaltung

Diese Methode beruht auf mit dem Internet verbundenen Standortsystemservern, mit denen Clients zu Verwaltungszwecken direkt kommunizieren. Bei dieser Methode müssen Clients und Standortsystemserver für die internetbasierte Clientverwaltung (Internet-Based Client Management, IBCM) konfiguriert werden.

### <a name="ibcm-advantages"></a>Vorteile von IBCM

- Keine Abhängigkeit von einem Cloud-Dienst.  

- Ohne zusätzliche Kosten eines Cloud-Abonnements.  

- Vollständige Kontrolle von Servern und Rollen, die den Dienst bereitstellen.  

### <a name="ibcm-disadvantages"></a>Nachteile von IBCM

- Zusätzliche Infrastrukturinvestitionen erforderlich.  

- Gemeinkosten und Betriebskosten der zusätzlichen Infrastruktur.  

- Infrastruktur muss mit dem Internet verbunden sein.  

Weitere Informationen finden Sie unter [Planen der internetbasierten Clientverwaltung](plan-internet-based-client-management.md).  
