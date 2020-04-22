---
title: Grundlagen der Sicherheit
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über die Sicherheitsschichten von Configuration Manager.
ms.date: 10/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 035b7f73-8b78-4ed1-835e-a31f9a5c4a02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 95b8bf41d74e7011eed40116f4fe34e2c356d67e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707058"
---
# <a name="fundamentals-of-security-for-configuration-manager"></a>Grundlagen der Sicherheit für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In diesem Artikel werden die folgenden grundlegenden Sicherheitskomponenten einer jeden Configuration Manager-Umgebung zusammengefasst:
- [Sicherheitsschichten](#bkmk_layers)
- [Rollenbasierte Verwaltung](#bkmk_rba)
- [Sichern von Clientendpunkten](#bkmk_endpoints)
- [Konten und Gruppen in Configuration Manager](#bkmk_accounts)
- [Datenschutz](#bkmk_privacy)

## <a name="security-layers"></a><a name="bkmk_layers"></a> Sicherheitsschichten

Die Sicherheit für Configuration Manager besteht aus den folgenden Schichten: 
- [Windows-Betriebssystem- und Netzwerksicherheit](#bkmk_layer-windows)
- [Netzwerkinfrastruktur: Firewalls, Angriffserkennung, Public Key-Infrastruktur (PKI)](#bkmk_layer-network)
- [Configuration Manager-Sicherheitssteuerung](#bkmk_layer-cm)
- [SMS-Anbieter](#bkmk_layer-provider)
- [Standortdatenbankberechtigungen](#bkmk_layer-db)

#### <a name="windows-os-and-network-security"></a><a name="bkmk_layer-windows"></a> Windows-Betriebssystem- und Netzwerksicherheit
Die erste Schicht wird von Windows-Sicherheitsfeatures für Betriebssystem und Netzwerk bereitgestellt. Zu dieser Schicht gehören die folgenden Komponenten:  

-   Dateifreigabe zur Übertragung von Dateien zwischen Configuration Manager-Komponenten  

-   Zugriffssteuerungslisten (Access Control Lists, ACLs) zum Schutz von Dateien und Registrierungsschlüsseln  

-   Internetprotokollsicherheit (IPsec), um sichere Kommunikation zu unterstützen  

-   Gruppenrichtlinie zum Festlegen von Sicherheitsrichtlinien  

-   DCOM-Berechtigungen (Distributed Component Object Model) für verteilte Anwendungen wie die Configuration Manager-Konsole  

-   Active Directory-Domänendienste zum Sichern von Sicherheitsprinzipalen  

-   Windows-Kontosicherheit einschließlich einiger Gruppen, die beim Configuration Manager-Setup erstellt werden  

#### <a name="network-infrastructure"></a><a name="bkmk_layer-network"></a> Netzwerkinfrastruktur

Zusätzliche Sicherheitskomponenten wie Firewalls und die Angriffserkennung ermöglichen einen umfassenden Schutz der gesamten Umgebung. Zertifikate, die über mit dem Industriestandard konforme Public Key-Infrastrukturimplementierungen (PKI) ausgestellt werden, ermöglichen Authentifizierung, Signatur und Verschlüsselung.  

#### <a name="configuration-manager-security-controls"></a><a name="bkmk_layer-cm"></a> Configuration Manager-Sicherheitssteuerung

Zusätzlich zu der durch die Server- und Netzwerkinfrastruktur von Windows bereitgestellten Sicherheit steuert Configuration Manager den Zugriff auf die zugehörige Konsole und die Ressourcen auf unterschiedliche Weise. Standardmäßig verfügen nur lokale Administratoren über Zugriffsrechte für die Dateien und Registrierungsschlüssel, die für die Configuration Manager-Konsole auf den Computern erforderlich sind, auf denen Sie sie installieren.  

#### <a name="sms-provider"></a><a name="bkmk_layer-provider"></a> SMS-Anbieter

Die nächste Sicherheitsebene basiert auf dem Zugriff über die Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI), speziell über den SMS-Anbieter. Der SMS-Anbieter ist eine Configuration Manager-Komponente, die einem Benutzer Zugriff gewährt, damit dieser Informationen aus der Standortdatenbank abfragen kann. Der Zugriff auf den Anbieter ist standardmäßig auf Mitglieder der lokalen Gruppe „SMS-Administratoren“ beschränkt. Diese Gruppe enthält zunächst nur den Benutzer, der Configuration Manager installiert hat. Um anderen Konten die Berechtigung für den Zugriff auf das CIM-Repository (Common Information Model) und den SMS-Anbieter zu erteilen, fügen Sie die anderen Konten der Gruppe „SMS-Administratoren“ hinzu.  

Ab Version 1810 können Sie die mindestens erforderliche Authentifizierungsebene für den Administratorzugriff auf Configuration Manager-Standorte angeben. Diese Funktion verpflichtet Administratoren dazu, sich mit der erforderlichen Ebene bei Windows anzumelden. <!--1357013-->  

Weitere Informationen finden Sie unter [Planen des SMS-Anbieters](../plan-design/hierarchy/plan-for-the-sms-provider.md).

#### <a name="site-database-permissions"></a><a name="bkmk_layer-db"></a> Standortdatenbankberechtigungen

Die letzte Sicherheitsebene basiert auf Berechtigungen für Objekte in der Standortdatenbank. Standardmäßig können mit dem lokalen Systemkonto und dem Benutzerkonto, das Sie für die Installation von Configuration Manager verwendet haben, alle Objekte in der Standortdatenbank verwaltet werden. Mithilfe der rollenbasierten Verwaltung erteilen oder verwehren Sie weiteren Administratoren in der Configuration Manager-Konsole Berechtigungen.  



## <a name="role-based-administration"></a><a name="bkmk_rba"></a> Rollenbasierte Verwaltung  

 In Configuration Manager wird die rollenbasierte Verwaltung verwendet, um Objekte wie Sammlungen, Bereitstellungen und Standorte zu sichern. Über dieses Verwaltungsmodell werden Sicherheitszugriffseinstellungen für alle Standorte und Standorteinstellungen hierarchieweit zentral definiert und verwaltet. 

 Ein Administrator kann Administratoren und Gruppenberechtigungen *Sicherheitsrollen* zuweisen. Die Berechtigungen sind mit verschiedenen Configuration Manager-Objekttypen verbunden, z.B. zum Erstellen oder Ändern von Clienteinstellungen. 

 Mithilfe von *Sicherheitsbereichen* werden bestimmte Instanzen von Objekten gruppiert, für deren Verwaltung ein Administrator verantwortlich ist, z.B. eine Anwendung zum Installieren von Microsoft Office. 

 Durch die Kombination aus Sicherheitsrollen, Sicherheitsbereichen und Sammlungen wird definiert, welche Objekte ein Administrator anzeigen und verwalten kann. Von Configuration Manager werden einige Standardsicherheitsrollen für häufige Verwaltungsaufgaben installiert. Erstellen Sie Ihre eigenen Sicherheitsrollen zur Unterstützung Ihrer spezifischen Geschäftsanforderungen.  

 Weitere Informationen finden Sie unter [Konfigurieren der rollenbasierten Verwaltung](../servers/deploy/configure/configure-role-based-administration.md).  



## <a name="securing-client-endpoints"></a><a name="bkmk_endpoints"></a> Sichern von Clientendpunkten  

 Configuration Manager sichert die Kommunikation zwischen Clients und Standortsystemrollen entweder mit selbstsignierten bzw. PKI-Zertifikaten oder mit Azure Active Directory-Tokens. Für einige Szenarios sind PKI-Zertifikate erforderlich. Zum Beispiel für die [internetbasierte Clientverwaltung](../clients/manage/plan-internet-based-client-management.md) und die [Verwaltung mobiler Geräte](../../mdm/plan-design/plan-on-premises-mdm.md).  

 Sie können die Standortsystemrollen, mit denen Clients Verbindungen herstellen, für die Clientkommunikation über HTTP oder HTTPS konfigurieren. Clientcomputer kommunizieren immer über die sicherste verfügbare Methode. Dabei wird nur dann auf die weniger sichere Kommunikationsmethode zurückgegriffen, wenn Sie über Standortsystemrollen verfügen, die HTTP-Kommunikation zulassen.  

 Weitere Informationen finden Sie unter [Planen der Sicherheit](../plan-design/security/plan-for-security.md).



## <a name="configuration-manager-accounts-and-groups"></a><a name="bkmk_accounts"></a> Konten und Gruppen in Configuration Manager  

 In Configuration Manager wird das lokale Systemkonto für den Großteil der Standortvorgänge verwendet. Für einige Verwaltungsaufgaben kann es erforderlich sein, zusätzliche Konten zu erstellen und zu verwalten. Configuration Manager erstellt beim Setup mehrere Standardgruppen und SQL Server-Rollen. Es kann erforderlich sein, diesen Standardgruppen und SQL Server-Rollen manuell Computer- oder Benutzerkonten hinzuzufügen.  

 Weitere Informationen finden Sie unter [In Configuration Manager verwendete Konten](../plan-design/hierarchy/accounts.md).  



## <a name="privacy"></a><a name="bkmk_privacy"></a> Datenschutz  

 Berücksichtigen Sie vor der Implementierung von Configuration Manager Ihre Datenschutzanforderungen. Verwaltungsprodukte für Unternehmen bieten zwar zahlreiche Vorteile, da sie viele Clients effektiv verwalten können. Allerdings wirkt sich diese Software möglicherweise auf den Datenschutz der Benutzer in Ihrem Unternehmen aus. Configuration Manager enthält zahlreiche Tools zum Sammeln von Daten und Überwachen von Geräten. Einige dieser Tools können in Ihrem Unternehmen Bedenken bezüglich des Datenschutzes auslösen.  

 Beispielsweise werden viele Verwaltungseinstellungen bei der Installation des Configuration Manager-Clients standardmäßig aktiviert. Diese Konfiguration führt dazu, dass Informationen von der Clientsoftware an den Configuration Manager-Standort gesendet werden. Der Standort speichert Clientinformationen in der Standortdatenbank. Die Clientinformationen werden nicht direkt an Microsoft gesendet. Weitere Informationen finden Sie unter [Diagnose- und Nutzungsdaten](../plan-design/diagnostics/diagnostics-and-usage-data.md).



## <a name="see-also"></a>Weitere Informationen:

- [Planen der Sicherheit](../plan-design/security/plan-for-security.md)  

- [Sicherheit und Datenschutz für Konfigurations-Manager-Clients](../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Konfigurieren der Sicherheit](../plan-design/security/configure-security.md)   

- [Datenübertragungen zwischen Endpunkten](../plan-design/hierarchy/communications-between-endpoints.md)  

- [Technische Referenz für kryptografische Steuerelemente](../plan-design/security/cryptographic-controls-technical-reference.md)  
