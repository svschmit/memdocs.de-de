---
title: Netzwerkinfrastruktur
titleSuffix: Configuration Manager
description: Richten Sie zur Vorbereitung der Configuration Manager-Kommunikation Firewalls, Ports und Domänen ein.
ms.date: 06/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: d6993bba-f6bd-4639-adbf-efc1c638b2f3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 816b48f7dac3703c1d45fdbc0bf8ad7dc9528caa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703088"
---
# <a name="network-infrastructure-considerations-for-configuration-manager"></a>Überlegungen zur Netzwerkinfrastruktur für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Um Ihr Netzwerk auf die Unterstützung von Configuration Manager vorzubereiten, müssen Sie möglicherweise einige Infrastrukturkomponenten konfigurieren. Beispielsweise müssen Sie Firewallports öffnen, um die von Configuration Manager verwendete Kommunikation weiterzuleiten.  

## <a name="ports-and-protocols"></a>Ports und Protokolle

Verschiedene Configuration Manager-Features verwenden verschiedene Netzwerkports. Einige Ports sind erforderlich, einige können Sie anpassen.

Für einen Großteil der Configuration Manager-Kommunikation werden allgemeine Ports wie z.B. 80 für HTTP oder 443 für HTTPS verwendet. Einige Standortsystemrollen unterstützen die Verwendung benutzerdefinierter Websites und Ports. Weitere Informationen finden Sie unter [Websites für Standortsystemserver](websites-for-site-system-servers.md).

Identifizieren Sie vor der Bereitstellung von Configuration Manager die Ports, die Sie verwenden möchten, und richten Sie die Firewalls entsprechend ein.

Wenn Sie nach der Installation von Configuration Manager einen Port ändern müssen, denken Sie daran, die Firewalls auf Geräten und im Netzwerk zu aktualisieren. Ändern Sie auch die Konfiguration des Ports in Configuration Manager.

Weitere Informationen finden Sie in den folgenden Artikeln:

- [Konfigurieren von Clientkommunikationsports](../../clients/deploy/configure-client-communication-ports.md)
- [In Configuration Manager verwendete Ports](../hierarchy/ports.md)


## <a name="internet-access-requirements"></a>Erforderliche Berechtigungen für den Internetzugriff

Einige Configuration Manager-Features benötigen für die vollständige Funktionalität eine Internetverbindung. Wenn Ihre Organisation die Netzwerkkommunikation mit dem Internet über ein Firewall- oder Proxygerät einschränkt, stellen Sie sicher, dass die erforderlichen Endpunkte zugelassen sind.

Weitere Informationen finden Sie unter [Internetzugriffsanforderungen](internet-endpoints.md).


## <a name="proxy-servers"></a>Proxyserver

Sie können separate Proxyserver für verschiedene Standortsystemserver und Clients angeben. Sie können diese Einstellungen beim Installieren einer Standortsystemrolle oder eines Clients konfigurieren oder später nach Bedarf ändern.

Weitere Informationen finden Sie unter [Unterstützung von Proxyservern](proxy-server-support.md).
