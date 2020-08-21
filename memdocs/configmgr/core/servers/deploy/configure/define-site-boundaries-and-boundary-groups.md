---
title: Verwenden von Grenzen und Begrenzungsgruppen
titleSuffix: Configuration Manager
description: Verwenden Sie die Standortgrenzen und Begrenzungsgruppen zum Definieren von Netzwerkadressen und zugänglichen Standortsystemen für Geräte, die Sie verwalten.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 54aa20d5-791e-4416-9db4-5aaea472c0b7
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 385dc1b2f542c964b52515e755a9202ee951bc5c
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126374"
---
# <a name="define-site-boundaries-and-boundary-groups"></a>Definieren von Grenzen und Begrenzungsgruppen für Standorte

*Gilt für: Configuration Manager (Current Branch)*

*Grenzen* in Configuration Manager definieren Netzwerkadressen in Ihrem Intranet. Diese Adressen umfassen Geräte, die Sie verwalten möchten. *Begrenzungsgruppen* sind logische Gruppen von Grenzen, die Sie konfigurieren.

Eine Hierarchie kann eine beliebige Anzahl von Begrenzungsgruppen enthalten. Jede Begrenzungsgruppe kann eine beliebige Kombination der folgenden Grenztypen enthalten:  

- IP-Subnetz  
- Active Directory-Standortname  
- IPv6-Präfix  
- IP-Adressbereich  
- VPN (ab Version 2006)

Clients im Intranet bewerten ihre aktuelle Adresse im Netzwerk und bestimmen anhand dieser Informationen Begrenzungsgruppen, zu denen sie gehören.  

Clients nutzen Begrenzungsgruppen für folgende Zwecke:  

- **Suchen eines zugewiesenen Standorts:** Begrenzungsgruppen ermöglichen es Clients, einen primären Standort für die Clientzuweisung zu finden. Dieses Verhalten wird auch als *automatische Standortzuweisung* bezeichnet.  

- **Suchen bestimmter Standortsystemrollen, die sie verwenden können:** Ordnen Sie eine Begrenzungsgruppe mit bestimmten Standortsystemrollen zu. Dann stellt der Standort diese Liste von Standortsystemen in der Begrenzungsgruppe für Clients bereit. Clients nutzen diese Standortsysteme für Aktionen wie das Suchen von Inhalten oder einem Verwaltungspunkt in der Nähe.  

Clients, die sich im Internet befinden oder als reine Internetclients konfiguriert sind, verwenden keine Begrenzungsinformationen. Diese Clients können die automatische Standortzuweisung nicht verwenden. Sie können Inhalte von einem internetbasierten Verteilungspunkt an ihrem zugewiesenen Standort oder von einem cloudbasierten Verteilungspunkt herunterladen.  

Ab Version 1902 können Sie einer Begrenzungsgruppe ein Cloudverwaltungsgateway (Cloud Management Gateway, CMG) zuordnen. Weitere Informationen finden Sie im Artikel „Planen von Cloud Management Gateway in Configuration Manager“ unter [Hierarchieentwurf](../../../clients/manage/cmg/plan-cloud-management-gateway.md#hierarchy-design).<!--3640932-->


## <a name="recommendations"></a><a name="BKMK_BoundaryBestPractices"></a> Empfehlungen

### <a name="use-a-mix-of-the-fewest-boundaries-that-meet-your-needs"></a>Verwenden einer Kombination aus einer möglichst geringen Anzahl von Grenzen, die Ihren Anforderungen entsprechen

Verwenden Sie Begrenzungstypen, die für Ihre Umgebung funktionieren. Um Ihre Verwaltungsaufgaben zu vereinfachen, wählen Sie Begrenzungstypen aus, die es ermöglichen, eine möglichst geringe Anzahl von Grenzen zu verwenden.

### <a name="avoid-overlapping-boundaries-for-automatic-site-assignment"></a>Vermeiden von überlappenden Grenzen bei der automatischen Standortzuweisung

Zwar unterstützt jede Begrenzungsgruppe sowohl die Standortzuweisung als auch Standortsystemverweise, dennoch sollten Sie einen getrennten Satz von Begrenzungsgruppen erstellen, die nur für die Standortzuweisung genutzt werden. Achten Sie darauf, dass in einer Begrenzungsgruppe enthaltene Grenzen nicht gleichzeitig einer anderen Begrenzungsgruppe mit abweichender Standortzuweisung angehören.

- Eine einzelne Grenze kann zu mehreren Begrenzungsgruppen gehören.  

- Jede Begrenzungsgruppe kann für die Standortzuweisung einem anderen primären Standort zugeordnet werden.  

- Bei einer Grenze, die zu zwei verschiedenen Begrenzungsgruppen mit verschiedenen Standortzuweisungen gehört, wählen Clients zufällig aus, welchem Standort sie beitreten. Dieses Verhalten kann dazu führen, dass Clients nicht dem gewünschten Standort beitreten. Diese Konfiguration wird als *überlappende Grenzen* bezeichnet.  

    Überlappende Grenzen sind kein Problem bei Inhaltsstandorten. Hierbei kann diese Konfiguration nützlich sein, weil sie Clients zusätzliche Ressourcen oder Inhaltsstandorte bereitstellt, die von den Clients genutzt werden können.  


## <a name="next-steps"></a>Nächste Schritte

- [Definieren von Netzwerkpfaden als Begrenzungsgruppen](boundaries.md)

- [Konfigurieren von Begrenzungsgruppen](boundary-groups.md)
