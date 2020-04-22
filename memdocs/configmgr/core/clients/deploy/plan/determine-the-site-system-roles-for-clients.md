---
title: Standortsystemrollen für Clients
titleSuffix: Configuration Manager
description: Ermitteln Sie die Standortsystemrollen für Clients in Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 984e8d92-7327-4b08-9228-0c955e6ac778
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 32895df466c41ca828d1107857212b8d5a777026
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693748"
---
# <a name="determine-the-site-system-roles-for-configuration-manager-clients"></a>Ermitteln der Standortsystemrollen für Configuration Manager-Clients

*Gilt für: Configuration Manager (Current Branch)*

Die Informationen in diesem Artikel können Ihnen beim Bestimmen der Standortsystemrollen helfen, die zum Bereitstellen von Configuration Manager-Clients erforderlich sind.

Weitere Informationen dazu, wo diese Rollen in der Hierarchie zu installieren sind, finden Sie unter [Entwerfen einer Hierarchie von Standorten](../../../plan-design/hierarchy/design-a-hierarchy-of-sites.md).  

Weitere Informationen zum Installieren und Konfigurieren dieser Rollen finden Sie unter [Install site system roles](../../../servers/deploy/configure/install-site-system-roles.md) (Installieren von Standortsystemrollen).  

## <a name="management-point"></a>Verwaltungspunkt

In der Standardeinstellung wird von allen Windows-Computern ein Verteilungspunkt zum Installieren des Configuration Manager-Clients verwendet. Wenn kein Verteilungspunkt verfügbar ist, ist auch ein Fallback auf einen Verwaltungspunkt möglich. Mithilfe der CCMSetup-Befehlszeileneigenschaft `/source:<Path>` können Windows-Clients jedoch auch von einer alternativen Quelle aus auf Computern installiert werden. Diese Aktion können Sie beispielsweise beim Installieren von Clients im Internet ausführen. Möglicherweise möchten Sie aber auch vermeiden, dass während der Clientinstallation Netzwerkpakete zwischen dem Computer und dem Verwaltungspunkt gesendet werden. Ein solches Szenario ist darauf zurückzuführen, dass eine Firewall die erforderlichen Ports blockiert oder dass eine Verbindung mit geringer Bandbreite vorliegt. Allerdings ist für alle Clients die Kommunikation mit einem Verwaltungspunkt erforderlich, damit sie einem Standort zugewiesen und von Configuration Manager verwaltet werden können.  

Weitere Informationen zu den Client-Befehlszeileneigenschaften finden Sie unter [Informationen zu Clientinstallationseigenschaften](../about-client-installation-properties.md).  

Wenn Sie mehrere Verwaltungspunkte in der Hierarchie installieren, stellen Clients basierend auf ihrer Gesamtstrukturmitgliedschaft und Netzwerkadresse automatisch eine Verbindung mit einem Punkt her. Sie können an einem sekundären Standort nicht mehr als einen Verwaltungspunkt installieren.  

Macintosh-Computerclients und mobile Geräteclients, die Sie bei Configuration Manager registrieren, erfordern für die Clientinstallation immer einen Verwaltungspunkt. Dieser Verwaltungspunkt muss sich an einem primären Standort befinden, für die Unterstützung mobiler Geräte konfiguriert sein und Clientverbindungen über das Internet akzeptieren. Für diese Clients können keine Verwaltungspunkte an sekundären Standorten verwendet werden, und es kann keine Verbindung mit Verwaltungspunkten an anderen primären Standorten hergestellt werden.  

## <a name="distribution-point"></a>Verteilungspunkt

Für die Installation von Configuration Manager-Clients auf Windows-Computern ist kein Verteilungspunkt erforderlich. In der Standardeinstellung verwendet Configuration Manager einen Verteilungspunkt, um die Clientquelldateien auf Windows-Computern zu installieren. Diese Dateien können jedoch auch im Rahmen eines Fallbacks von einem Verwaltungspunkt heruntergeladen werden. Verteilungspunkte werden nicht verwendet, um Clients für mobile Geräte zu installieren, die mithilfe von Configuration Manager registriert wurden. Sie werden allerdings bei der Installation des Legacyclients für mobile Geräte verwendet. Wenn Sie den Configuration Manager-Client im Rahmen einer Betriebssystembereitstellung installieren, wird das Betriebssystemimage auf einem Verteilungspunkt gespeichert und von dort abgerufen.

Obwohl Verteilungspunkte für die Installation der meisten Configuration Manager-Clients nicht erforderlich sind, benötigen Sie sie, um Software wie Anwendungen und Softwareupdates auf den Clients zu installieren.  

## <a name="fallback-status-point"></a>Fallbackstatuspunkt

Sie können einen Fallbackstatuspunkt verwenden, um die Clientbereitstellung für Windows-Computer zu überwachen. Sie können auch die Windows-Computerclients ermitteln, die nicht verwaltet werden, weil die Kommunikation mit einem Verwaltungspunkt nicht möglich ist.

Die folgenden Clienttypen verwenden keinen Fallbackstatuspunkt:

- Mac-Computer
- Von Configuration Manager registrierte mobile Geräte
- Mobile Geräte, die mithilfe des Exchange Server-Connectors verwaltet werden

Ein Fallbackstatuspunkt ist nicht erforderlich, um Clientaktivität und Clientintegrität zu überwachen.  

Die Kommunikation zwischen Fallbackstatuspunkt und Clients erfolgt immer über HTTP, wobei nicht authentifizierte Verbindungen verwendet und Daten im Klartext gesendet werden. Durch dieses Verhalten ist der Fallbackstatuspunkt insbesondere dann für Angriffe anfällig, wenn er in der internetbasierten Clientverwaltung verwendet wird. Um die Angriffsfläche zu verringern, reservieren Sie stets einen Server für die Ausführung des Fallbackstatuspunkts. Installieren Sie keine anderen Standortsystemrollen auf demselben Server in einer Produktionsumgebung.  

Installieren Sie einen Fallbackstatuspunkt, wenn Folgendes zutrifft:  

- Sie möchten erreichen, dass Clientkommunikationsfehler von Windows-Computern auch dann an den Standort gesendet werden, wenn diese Clientcomputer nicht mit einem Verwaltungspunkt kommunizieren können.  

- Sie möchten die Configuration Manager-Berichte zur Clientbereitstellung nutzen, in denen die vom Fallbackstatuspunkt gesendeten Daten angezeigt werden.  

- Sie verfügen über einen dedizierten Server für diese Standortsystemrolle und haben zusätzliche Sicherheitsmaßnahmen zum Schutz des Servers vor Angreifern ergriffen.  

- Die Vorteile der Verwendung eines Fallbackstatuspunkts überwiegen im Vergleich mit den Sicherheitsrisiken durch nicht authentifizierte Verbindungen und Klartextübertragungen über HTTP-Verkehr.  

Verzichten Sie auf die Installation eines Fallbackstatuspunkts, wenn die Sicherheitsrisiken der Ausführung einer Website mit nicht authentifizierten Verbindungen und Klartextübertragungen im Vergleich zu den Vorteilen der Identifizierung von Problemen bei der Clientkommunikation überwiegen.  

## <a name="reporting-services-point"></a>Reporting Services-Punkt

Mit Configuration Manager stehen viele Berichte zur Verfügung, mit denen Installation, Zuweisung und Verwaltung von Clients in der Configuration Manager-Konsole vereinfacht werden. Für einige Berichte zur Clientbereitstellung ist es erforderlich, dass Clients einem Fallbackstatuspunkt zugewiesen werden.  

Die Berichte sind zum Bereitstellen von Clients nicht erforderlich. Sie können einige Bereitstellungsinformationen in der Configuration Manager-Konsole einsehen oder die Clientprotokolldateien einsehen, um detaillierte Informationen zu erhalten. Die Clientberichte enthalten jedoch wertvolle Informationen für Überwachung und Problembehandlung bei der Clientbereitstellung.  

## <a name="enrollment-point-and-enrollment-proxy-point"></a>Anmeldungspunkt und Anmeldungsproxypunkt

Für Configuration Manager sind der Anmeldungspunkt und der Anmeldungsproxypunkt erforderlich, um mobile Geräte und Zertifikate für Macintosh-Computer anzumelden. Diese Standortsystemrollen sind in den folgenden Situationen nicht erforderlich:

- Sie beabsichtigen, mobile Geräte mithilfe des Exchange Server-Connectors zu verwalten.
- Sie installieren den Legacyclient für mobile Geräte, z. B. für Windows CE.
- Anforderung und Installation des Clientzertifikats auf Mac-Computern erfolgt unabhängig von Configuration Manager.

## <a name="application-catalog"></a>Anwendungskatalog

> [!Important]  
> Die Silverlight-Benutzeroberfläche für den Anwendungskatalog wird ab Current Branch-Version 1806 nicht unterstützt. Ab Version 1906 verwenden aktualisierte Clients automatisch den Verwaltungspunkt für Anwendungsbereitstellungen, die Benutzern zur Verfügung stehen. Zudem können Sie keine neuen Anwendungskatalogrollen installieren. Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910.  
>
> Weitere Informationen finden Sie in den folgenden Artikeln:
>
> - [Konfigurieren des Softwarecenters](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Entfernte und veraltete Features](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

## <a name="cloud-management-gateway-connector-point"></a>Connectorpunkt für Cloudverwaltungsgateway

Ein Cloudverwaltungsgateway-Connectorpunkt ist erforderlich, wenn Sie ein [Cloudverwaltungsgateway](../../manage/cmg/plan-cloud-management-gateway.md) zum [Verwalten von Clients im Internet](../../manage/manage-clients-internet.md) einrichten.
