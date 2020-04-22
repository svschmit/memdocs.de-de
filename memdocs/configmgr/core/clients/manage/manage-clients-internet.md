---
title: Verwalten von Clients im Internet
titleSuffix: Configuration Manager
description: In diesem Artikel erhalten Sie Informationen zum Verwalten von Clients mithilfe von Cloud Management Gateway (CMG) und zur internetbasierten Clientverwaltung in Configuration Manager.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.topic: conceptual
ms.technology: configmgr-client
ms.assetid: c667d6af-80c4-485f-910c-896c0171fd00
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c00d480b993498c5fa27e2a4d91a5f2a3bc130ee
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690028"
---
# <a name="manage-clients-on-the-internet-with-configuration-manager"></a>Verwalten von Clients im Internet mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In der Regel befinden sich in Configuration Manager die meisten verwalteten Computer und Server in demselben internen Netzwerk wie die Standortsystemserver, die Verwaltungsfunktionen ausführen. Sie können jedoch auch Clients außerhalb des internen Netzwerks verwalten, wenn sie mit dem Internet verbunden sind. Hierbei müssen Clients keine VPN-Verbindung aufbauen, um mit den Standortsystemservern zu kommunizieren.

Configuration Manager bietet zwei Methoden, mit dem Internet verbundene Clients zu verwalten:

-   Cloudverwaltungsgateway

-   Internetbasierte Clientverwaltung


## <a name="cloud-management-gateway"></a>Cloudverwaltungsgateway

Mit Cloud Management Gateway (CMG) lassen sich internetbasierte Clients verwalten. Dabei wird eine neue Standortsystemrolle verwendet, die mit einem Microsoft Azure-Clouddienst kommuniziert. Internetbasierte Clients verwenden den Clouddienst, um mit dem lokalen Configuration Manager zu kommunizieren.

#### <a name="advantages"></a>Vorteile  

-   Keine zusätzlichen Investitionen in die Infrastruktur vor Ort erforderlich.  

-   Lokale Infrastruktur bleibt vom Internet getrennt.  

-   Virtuelle Computer in der Cloud, auf denen der Dienst ausgeführt wird, werden vollständig von Azure verwaltet und erfordern keine Wartung.  

-   Einfache Einrichtung und Konfiguration in der Configuration Manager-Konsole.  

#### <a name="disadvantages"></a>Nachteile  

-   Cloud-Abonnement-Kosten.  

-   Verwaltungsdaten werden über Cloud-Dienst gesendet.  

Weitere Informationen finden Sie unter [Planen des Cloudverwaltungsgateways](cmg/plan-cloud-management-gateway.md).  



## <a name="internet-based-client-management"></a>Internetbasierte Clientverwaltung

Diese Methode beruht auf mit dem Internet verbundenen Standortsystemservern, mit denen Clients zu Verwaltungszwecken kommunizieren. Bei dieser Methode müssen Clients und Standortsystemserver für die internetbasierte Verwaltung konfiguriert werden.

#### <a name="advantages"></a>Vorteile  

-   Keine Abhängigkeit von einem Cloud-Dienst.  

-   Ohne zusätzliche Kosten eines Cloud-Abonnements.  

-   Vollständige Kontrolle von Servern und Rollen, die den Dienst bereitstellen.  

#### <a name="disadvantages"></a>Nachteile  

-   Zusätzliche Infrastrukturinvestitionen erforderlich.  

-   Gemeinkosten und Betriebskosten der zusätzlichen Infrastruktur.  

-   Infrastruktur muss mit dem Internet verbunden sein.  

Weitere Informationen finden Sie unter [Planen der internetbasierten Clientverwaltung](plan-internet-based-client-management.md).  
