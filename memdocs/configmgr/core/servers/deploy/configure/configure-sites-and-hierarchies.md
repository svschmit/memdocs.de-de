---
title: Konfigurieren von Standorten und Hierarchien
titleSuffix: Configuration Manager
description: Stellen Sie anhand dieser Prüfliste sicher, dass Sie die am häufigsten verwendeten Konfigurationen berücksichtigen, die Standorte und Hierarchien betreffen.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9efb4061-f642-48bd-8332-3357ff5b3118
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e996c31a4f1aaa9224e4c6d1d435f79adf7ac23c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704678"
---
# <a name="configure-sites-and-hierarchies-for-configuration-manager"></a>Konfigurieren von Standorten und Hierarchien für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Nachdem Sie Ihren ersten Configuration Manager-Standort installiert oder Ihrer Hierarchie weitere Standorte hinzugefügt haben, nutzen Sie diese Prüfliste, um sicherzustellen, dass Sie die gängigsten Konfigurationen berücksichtigen, die sich sowohl auf Standorte als auch auf Hierarchien auswirken.  

Die folgenden Hinweise zur Konfiguration gelten für die meisten Bereitstellungen:  

- Einige dieser Optionen, wie z.B. die Active Directory-Gesamtstrukturermittlung, Grenzen und Begrenzungsgruppen, bauen aufeinander auf.  

- Verschiedene Konfigurationen verfügen über Standardwerte, die Sie zumindest für den Anfang verwenden können, ohne Änderungen an der Konfiguration vornehmen zu müssen.  

- Andere Konfigurationen, wie z.B. Begrenzungsgruppen und Verteilungspunktgruppen, müssen Sie dagegen konfigurieren, bevor Sie sie verwenden können.  

| Aktion | Details |  
|------------|-------------|  
| Konfigurieren der rollenbasierten Verwaltung | Trennen Sie administrative Zuständigkeiten, um zu steuern, welche Administratoren verschiedene Objekte und Daten in Ihrer Configuration Manager-Umgebung anzeigen und verwalten können.<br /><br /> Konfigurationen der rollenbasierten Verwaltung werden von allen Standorten der Hierarchie gemeinsam genutzt.   <br/><br/>Weitere Informationen finden Sie unter [Konfigurieren der rollenbasierten Verwaltung](configure-role-based-administration.md). |  
| Veröffentlichen von Standortdaten in Active Directory Domain Services | Erleichtern Sie Clients das Auffinden von Diensten und das effiziente Verwenden von Standortressourcen.<br /><br /> [Erweitern Sie zunächst das Active Directory-Schema](../../../plan-design/network/extend-the-active-directory-schema.md). Konfigurieren Sie anschließend jeden Standort zum [Veröffentlichen von Standortdaten](publish-site-data.md). |  
| Konfigurieren eines Dienstverbindungspunkts | Planen Sie die Installation und Konfiguration des Dienstverbindungspunkts auf der obersten Ebene Ihrer Hierarchie. Weitere Informationen finden Sie unter [About the service connection point (Informationen zum Dienstverbindungspunkt)](about-the-service-connection-point.md). |  
| Hinzufügen von Standortsystemrollen | Installieren und konfigurieren Sie für einzelne Standorte zusätzliche Standortsystemrollen. Weitere Informationen finden Sie unter [Hinzufügen von Standortsystemrollen](add-site-system-roles.md). |  
| Konfigurieren von Grenzen und Begrenzungsgruppen für Standorte | Geben Sie Grenzen zum Definieren der Netzwerkadressen in Ihrem Intranet an, die Geräte enthalten können, die Sie verwalten möchten. Konfigurieren Sie dann Begrenzungsgruppen, sodass Clients an diesen Netzwerkadressen Configuration Manager-Ressourcen finden können. Weitere Informationen finden Sie unter [Definieren von Standortgrenzen und Begrenzungsgruppen](define-site-boundaries-and-boundary-groups.md). |  
| Konfigurieren von Verteilungspunktgruppen | Konfigurieren Sie logische Gruppen von Verteilungspunkten, um das Verwalten von Bereitstellungen zu vereinfachen. Weitere Informationen finden Sie unter [Verwalten von Verteilungspunktgruppen](install-and-configure-distribution-points.md#bkmk_manage). |  
| Ausführen der Ermittlung | Führen Sie die Ermittlung aus, um Ressourcen in Ihrem Netzwerk zu finden, z.B. Netzwerkinfrastruktur, Gerät und Benutzer.<br /><br /> Weitere Informationen finden Sie unter [Run discovery (Ausführen der Ermittlung)](run-discovery.md). |  
| Hinzufügen von Redundanz und Kapazität für Administratoren | Installieren Sie zusätzliche SMS-Anbieter und Configuration Manager-Konsolen, um Administratoren mehr Kapazität für das Verwalten Ihrer Infrastruktur zu bieten:<br /><br /> **Installieren Sie zusätzliche SMS-Anbieter**, um Redundanz für die Konsole und die API-Verbindungen mit dem Standort bereitzustellen. Weitere Informationen finden Sie unter [Verwalten des SMS-Anbieters](../../manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider).<br /><br /> **Installieren Sie zusätzliche Configuration Manager-Konsolen** , um weiteren Administratoren Zugriff zu bieten. Weitere Informationen finden Sie unter [Installieren von Configuration Manager-Konsolen](../install/install-consoles.md). |  
| Konfigurieren von Standortkomponenten | Konfigurieren Sie an jedem Standort Standortkomponenten, um das Verhalten von Standortsystemrollen und die Statusberichterstattung des Standorts zu ändern. Weitere Informationen finden Sie unter [Standortkomponenten](site-components.md). |  
| Erstellen benutzerdefinierter Sammlungen | Erstellen Sie anhand von vom Standort ermittelten Informationen zu Geräten und Benutzern benutzerdefinierte Sammlungen von Objekten zum Vereinfachen künftiger Verwaltungsaufgaben. Weitere Informationen finden Sie unter [Erstellen von Sammlungen](../../../clients/manage/collections/create-collections.md). |  
| Konfigurieren von Einstellungen zum Verwalten risikoreicher Bereitstellungen | Konfigurieren Sie Einstellungen an einem Standort, um Administratoren zu warnen, wenn sie eine risikoreiche Bereitstellung erstellen. Weitere Informationen finden Sie unter [Settings to manage high-risk deployments (Einstellungen zum Verwalten risikoreicher Bereitstellungen)](../../manage/settings-to-manage-high-risk-deployments.md). |  
| Konfigurieren von Datenbankreplikaten für Verwaltungspunkte | Konfigurieren Sie ein Datenbankreplikat zum Verringern der CPU-Auslastung des Standortdatenbankservers mithilfe von Verwaltungspunkten, die Anforderungen von Clients erfüllen. Weitere Informationen finden Sie unter [Datenbankreplikate für Verwaltungspunkte](database-replicas-for-management-points.md). |  
| Konfigurieren einer SQL Server Always On-Verfügbarkeitsgruppe | Konfigurieren Sie Verfügbarkeitsgruppen als Lösungen für Hochverfügbarkeit und Notfallwiederherstellung zum Hosten der Standortdatenbank an primären Standorten und am Standort der zentralen Verwaltung. Weitere Informationen finden Sie unter [SQL Server Always On für eine hochverfügbare Standortdatenbank](sql-server-alwayson-for-a-highly-available-site-database.md). |  
| Ändern der Replikation zwischen Standorten | Unter [Datenübertragungen zwischen Standorten](../../../plan-design/hierarchy/data-transfers-between-sites.md) erfahren Sie mehr über die folgenden Themen:<br /><br /> Konfigurieren der [dateibasierten Replikation](../../../plan-design/hierarchy/file-based-replication.md) zwischen sekundären Standorten<br /><br /> Konfigurieren von [Datenbankreplikationslinks](../../../plan-design/hierarchy/database-replication.md)<br /><br /> Konfigurieren von [verteilten Ansichten](../../../plan-design/hierarchy/database-replication.md#bkmk_distviews) |  
| Konfigurieren von Standortservern im passiven Modus | Ab Version 1806 sollten Sie einen Standortserver für jeden primären Standort und den zentralen Verwaltungsstandort im passiven Modus konfigurieren. Mit diesem Feature wird ein Standortserver mit hoher Verfügbarkeit bereitgestellt. Weitere Informationen finden Sie unter [Site server high availability (Hochverfügbarkeit des Standortservers)](site-server-high-availability.md). |  
