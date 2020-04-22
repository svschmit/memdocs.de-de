---
title: Entwerfen einer Standorthierarchie
titleSuffix: Configuration Manager
description: Grundlegendes zu den verfügbaren Topologien und Verwaltungsoptionen für Configuration Manager, damit Sie Ihre Standorthierarchie planen können.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 07ce872e-1558-42ad-b5ad-582c5b1bdbb4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 3c642e97589ff345e4eb3a17b63b3fdfbc2891f9
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703588"
---
# <a name="design-a-hierarchy-of-sites-for-configuration-manager"></a>Entwerfen einer Hierarchie von Standorten für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Vor der Installation des ersten Standorts einer neuen Configuration Manager-Hierarchie sollten Sie Folgendes verstehen:  

- Die verfügbaren Topologien für Configuration Manager  

- Die Typen der verfügbaren Standorte und deren Beziehung untereinander  

- Den Verwaltungsbereich, den jeder Standorttyp bietet  

- Die Optionen für die Inhaltsverwaltung, die die Anzahl der Standorte reduzieren können, die Sie installieren müssen  

Planen Sie anschließend eine Topologie, die Ihren Unternehmensanforderungen effizient gerecht wird und später für die Verwaltung zukünftigen Wachstums erweitert werden kann.  

Berücksichtigen Sie bei der Planung die Einschränkungen in Bezug auf das Hinzufügen zusätzlicher Standorte zu einer Hierarchie oder einem eigenständigen Standort:  

- Installieren Sie einen neuen primären Standort unterhalb eines Standorts der zentralen Verwaltung. Beachten Sie die maximale [unterstützte Anzahl primärer Standorte](../configs/size-and-scale-numbers.md) für die Hierarchie.  

- [Erweitern Sie einen eigenständigen primären Standort, um einen neuen Standort der zentralen Verwaltung zu installieren](../../servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand), sodass Sie danach weitere primäre Standorte installieren können.  

- Installieren Sie unterhalb eines primären Standorts neue sekundäre Standorte. Beachten Sie die [unterstützten Grenzwerte für den primären Standort](../configs/size-and-scale-numbers.md) und die Gesamthierarchie.  

- Sie können keinen zuvor installierten Standort zu einer vorhandenen Hierarchie hinzufügen, um zwei eigenständige Standorte zusammenzuführen. Configuration Manager unterstützt nur die Installation neuer Standorte in einer vorhandenen Hierarchie von Standorten.  


> [!NOTE]  
> Achten Sie bei der Planung einer neuen Configuration Manager-Installation auf die [Versionsanmerkungen](../../servers/deploy/install/release-notes.md), die aktuelle Probleme in den aktiven Versionen behandeln. Die Versionsanmerkungen gelten für alle Branches von Configuration Manager. Wenn Sie [Technical Preview-Branch](../../get-started/technical-preview.md) verwenden, finden Sie Probleme, die nur für diesen Branch spezifisch sind, in der Dokumentation für jede Version von Technical Preview.  



##  <a name="hierarchy-topology"></a><a name="bkmk_topology"></a> Hierarchietopologie  

Hierarchietopologien reichen von:  

- Einfach: ein eigenständiger primärer Standort  

- Bis zu komplex: Eine Gruppe verbundener primärer und sekundärer Standorte mit einem Standort der zentralen Verwaltung am Standort der obersten Ebene der Hierarchie  

Der Schlüsseltreiber für den Typ und die Anzahl der Standorte, die Sie in einer Hierarchie verwenden, ist normalerweise die Anzahl und die Art von Geräten, die Sie unterstützen müssen.   

### <a name="standalone-primary-site"></a>Eigenständiger primärer Standort

Verwenden Sie einen eigenständigen primären Standort, wenn er die Verwaltung sämtlicher Geräte und Benutzer unterstützen kann. Weitere Informationen finden Sie unter [Größe und Skalierung von Zahlen](../configs/size-and-scale-numbers.md). Diese Topologie ist auch erfolgreich, wenn für die geografischen Standorte Ihres Unternehmens ein einzelner primärer Standort ausreicht. Verwenden Sie mehrere Verwaltungspunkte in Begrenzungsgruppen und eine sorgfältig geplante Inhaltsinfrastruktur, um die Verwaltung von Netzwerkdatenverkehr zu vereinfachen. Weitere Informationen finden Sie unter [Konfigurieren von Begrenzungsgruppen](../../servers/deploy/configure/boundary-groups.md) und [Grundlegende Konzepte für die Inhaltsverwaltung](fundamental-concepts-for-content-management.md).  

Diese Topologie bietet folgende Vorteile:  

- Einen vereinfachten Verwaltungsaufwand  

- Eine vereinfachte Clientstandortzuweisung und Ermittlung der verfügbaren Ressourcen und Dienste  

- Beseitigung möglicher Verzögerungen durch die Einführung der Datenbankreplikation zwischen Standorten  

- Option zum Erweitern eines eigenständigen primären Standorts in eine größere Hierarchie mit einem Standort der zentralen Verwaltung Mit dieser Option können Sie neue primäre Standorte installieren, um den Umfang Ihrer Bereitstellung zu erweitern.  


### <a name="central-administration-site-with-one-or-more-child-primary-sites"></a>Standort der zentralen Verwaltung mit mindestens einem untergeordneten primären Standort 

Verwenden Sie diese Topologie, wenn Sie mehr als einen primären Standort benötigen, um die Verwaltung all Ihrer Geräte und Benutzer zu unterstützen. Sie ist erforderlich, wenn Sie mehr als einen primären Standort verwenden müssen. 

Diese Topologie bietet folgende Vorteile:  

- Sie unterstützt bis zu 25 primäre Standorte, durch die Sie den Umfang Ihrer Hierarchie erweitern können.    

- Verwenden Sie daher immer den Standort der zentralen Verwaltung, sofern Sie Ihre Standorte nicht neu installieren. Diese Option ist dauerhaft. Sie können einen untergeordneten primären Standort nicht trennen, um ihn in einen eigenständigen primären Standort zu verwandeln.  



##  <a name="determine-when-to-use-a-central-administration-site"></a><a name="BKMK_ChooseCAS"></a> Ermitteln des Zeitpunkts für die Verwendung eines Standorts der zentralen Verwaltung  

Mithilfe eines Standorts der zentralen Verwaltung können Sie hierarchieweite Einstellungen konfigurieren und alle Standorte sowie Objekte in der Hierarchie überwachen. Dieser Standorttyp verwaltet Clients nicht direkt. Er koordiniert die Standort-zu-Standort-Datenreplikation. Auch die hierarchieweite Konfiguration von Standorten und Clients ist darin eingeschlossen.  

Die folgenden Informationen können Sie bei der Entscheidung unterstützen, wann ein Standort der zentralen Verwaltung installiert werden sollte:  

- Der Standort der zentralen Verwaltung ist der Standort der obersten Ebene einer Hierarchie.  

- Wenn Sie eine Hierarchie mit mehr als einem primären Standort konfigurieren, installieren Sie einen Standort der zentralen Verwaltung.  

     - Wenn Sie sofort zwei oder mehr primäre Standorte benötigen, installieren Sie zuerst den Standort der zentralen Verwaltung.  

     - Wenn Sie bereits über einen primären Standort verfügen und dann einen Standort der zentralen Verwaltung installieren möchten, [erweitern Sie den eigenständigen primären Standort](../../servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand), um den Standort der zentralen Verwaltung zu installieren.  

- Es werden nur primäre Standorte als untergeordnete Standorte vom Standort der zentralen Verwaltung unterstützt.  

- Es ist nicht möglich, dem Standort der zentralen Verwaltung Clients zuzuweisen.  

- Der Standort der zentralen Verwaltung unterstützt keine Standortsystemrollen, die eine direkte Unterstützung für Clients bieten, z.B. Verwaltungspunkte und Verteilungspunkte.  

- Verwalten Sie alle Clients in der Hierarchie, und führen Sie alle Standortverwaltungstasks mithilfe einer Configuration Manager-Konsole durch, die mit dem Standort der zentralen Verwaltung verbunden ist. Diese Tasks können das Installieren von Verwaltungspunkten oder anderen Standortsystemrollen an untergeordneten primären oder sekundären Standorten einbeziehen.  

- Wenn Sie einen Standort der zentralen Verwaltung verwenden, ist dies der einzige Ort, an dem Sie Standortdaten von sämtlichen Standorten in Ihrer Hierarchie einsehen können. Hierin sind auch Informationen wie Inventurdaten und Statusmeldungen eingeschlossen.  

- Konfigurieren Sie Ermittlungsvorgänge in der gesamten Hierarchie vom Standort der zentralen Verwaltung. Weisen Sie vom Standort der zentralen Verwaltung Ermittlungsmethoden zu, die auf einzelnen primären Standorten ausgeführt werden sollen.  

- Verwalten Sie die Sicherheit hierarchieweit, indem Sie verschiedenen Administratoren entsprechende Sicherheitsrollen, Sicherheitsbereiche und Sammlungen zuweisen. Diese Konfigurationen sind an jedem Standort in der Hierarchie gültig.  

- Konfigurieren Sie eine Replikation, von der die Kommunikation zwischen Standorten in der Hierarchie gesteuert wird. Planen Sie die Datenbankreplikation für Standortdaten und die Verwaltung der Bandbreite für die Übertragung dateibasierter Daten zwischen Standorten.  



##  <a name="determine-when-to-use-a-primary-site"></a><a name="BKMK_ChoosePriimary"></a> Ermitteln des Zeitpunkts für die Verwendung eines primären Standorts  

Verwenden Sie primäre Standorte, um Clients zu verwalten. Installieren Sie einen primären Standort als untergeordneten Standort unter einem Standort der zentralen Verwaltung oder als ersten Standort einer neuen Hierarchie. Ein primärer Standort als erster Standort einer Hierarchie erstellt einen eigenständigen primären Standort. Sowohl untergeordnete primäre Standorte als auch eigenständige primäre Standorte unterstützen sekundäre Standorte.  

Erwägen Sie das Hinzufügen zusätzlicher primärer Standorte aus folgenden Gründen:  

- Um die Anzahl von Geräten zu erhöhen, die mit einer einzelnen Hierarchie verwaltet werden können.  

- Sie möchten die Verwaltungsanforderungen Ihrer Organisation erfüllen. Beispielsweise könnten Sie einen primären Standort an einem Remotestandort installieren, um die Übertragung von Bereitstellungsinhalt über ein Netzwerk mit geringer Bandbreite zu verwalten.  

     - Sie können auch Optionen verwenden, um die Netzwerkbandbreite zu drosseln, wenn Daten an einen Verteilungspunkt übertragen werden. Diese Inhaltsverwaltungsfunktion kann es überflüssig machen, zusätzliche Standorte zu installieren.  


Die folgenden Informationen können Sie bei der Entscheidung unterstützen, wann ein primärer Standort installiert werden sollte:  

- Bei einem primären Standort kann es sich um einen eigenständigen primären Standort oder um einen untergeordneten primären Standort in einer größeren Hierarchie handeln. Wenn ein primärer Standort Mitglied einer Hierarchie mit einem Standort der zentralen Verwaltung ist, wird von den Standorten die Datenbankreplikation verwendet, um Daten zwischen den Standorten zu replizieren. Sofern Sie nicht mehr Clients und Geräte unterstützen müssen, als mit einem einzelnen primären Standort möglich ist, sollten Sie die Installation eines eigenständigen primären Standorts in Betracht ziehen. Nachdem Sie einen eigenständigen primären Standort installiert haben, erweitern Sie diesen (falls dies zukünftig benötigt wird), um an einen neuen Standort der zentralen Verwaltung zu berichten, um Ihre Bereitstellung hochzuskalieren.  

- Von einem primären Standort wird nur ein Standort der zentralen Verwaltung als übergeordneter Standort unterstützt.  

- Ein primärer Standort unterstützt nur sekundäre Standorte als untergeordnete Standorte. Es können dabei mehrere sekundäre Standorte unterstützt werden.  

- An primären Standorten werden alle Clientdaten der zugewiesenen Clients verarbeitet.  

- Mithilfe von Datenbankreplikation erfolgt eine direkte Kommunikation von den primären Standorten an den Standort der zentralen Verwaltung. Dieses Verhalten wird automatisch konfiguriert, wenn ein neuer Standort installiert wird.  



##  <a name="determine-when-to-use-a-secondary-site"></a><a name="BKMK_ChooseSecondary"></a> Ermitteln des Zeitpunkts für die Verwendung eines sekundären Standorts  

Verwenden Sie sekundäre Standorte, um die Übertragung von Bereitstellungsinhalten und Clientdaten über Netzwerke mit geringer Bandbreite zu verwalten.  

Ein sekundärer Standort wird mithilfe seines direkt übergeordneten primären Standorts oder mithilfe eines Standorts der zentralen Verwaltung verwaltet. Sekundäre Standorte werden mit einem primären Standort verbunden. Sie können sie nicht zu einem anderen übergeordneten Standort verschieben, ohne sie zuvor zu deinstallieren und als untergeordnete Standorte unter dem neuen primären Standort zu installieren.

Sie können jedoch Inhalt zwischen zwei sekundären Peer-Standorten weiterleiten, um die dateibasierte Replikation von Bereitstellunginhalt zu verwalten. Clientdaten werden vom sekundären Standort mithilfe von dateibasierter Replikation an einen primären Standort übertragen. Die dateibasierte Replikation wird vom sekundären Standort auch zur Kommunikation mit dem übergeordneten primären Standort verwendet.  

Erwägen Sie die Installation eines sekundären Standorts, wenn eine der folgenden Bedingungen erfüllt ist:  

- Sie benötigen keinen lokalen Verbindungspunkt für einen Administrator.  

- Sie müssen die Übertragung von Bereitstellungsinhalt an Standorte verwalten, die sich in der Hierarchie weiter unten befinden.  

- Sie müssen Clientinformationen verwalten, die an Standorte gesendet werden, die sich in der Hierarchie weiter oben befinden.  

Wenn Sie keinen sekundären Standort installieren möchten, und Sie über Clients an Remotestandorten verfügen, sollten Sie eine der folgenden Optionen in Betracht ziehen:  

- Die Verwendung von Peer-zu-Peer-Technologien wie Windows BranchCache  

- Die Aktivierung von Verteilungspunkten zur Planung und Steuerung der Bandbreite   

Verwenden Sie diese Optionen der Inhaltsverwaltung mit oder ohne sekundäre Standorte. Sie tragen zur Verringerung der Größe Ihrer Configuration Manager-Infrastruktur bei. Weitere Informationen zu Inhaltsverwaltungsoptionen in Configuration Manager finden Sie unter [Ermitteln des Zeitpunkts für die Verwendung der Optionen für die Inhaltsverwaltung](#BKMK_ChooseSecondaryorDP).  


Die folgenden Informationen können Sie bei der Entscheidung unterstützen, wann ein sekundärer Standort installiert werden sollte:  

- Falls keine lokale SQL Server-Instanz verfügbar ist, wird SQL Server Express im Rahmen der Standortinstallation von sekundären Standortservern automatisch installiert.  

- Die Installation des sekundären Standorts wird über die Configuration Manager-Konsole eingeleitet, anstatt das Setup direkt auf einem Computer auszuführen.  

- Sekundäre Standorte verwenden eine Teilmenge der Informationen in der Standortdatenbank. Dieses Verhalten verringert die Menge der Daten, die SQL zwischen dem übergeordneten primären Standort und dem sekundären Standort repliziert.  

- Das Routing dateibasierter Inhalte an andere sekundäre Standorte mit dem gleichen übergeordneten primären Standort wird von sekundären Standorten unterstützt.  

- Bei der Installation eines sekundären Standorts werden auf dem sekundären Standortserver automatisch ein Verwaltungspunkt und die Standortsystemrolle „Verteilungspunkt“ installiert.  



##  <a name="determine-when-to-use-content-management-options"></a><a name="BKMK_ChooseSecondaryorDP"></a> Ermitteln des Zeitpunkts für die Verwendung der Optionen für die Inhaltsverwaltung  

Falls es Clients an Remotenetzwerkorten gibt, sollten Sie erwägen, anstatt eines primären oder sekundären Standorts einige Inhaltsverwaltungsoptionen zu verwenden. Mit den folgenden Optionen ist es häufig nicht mehr notwendig, einen Standort zu installieren:  

- Übermittlungsoptimierung für Windows 10  

- Configuration Manager-Peercache  

- Windows BranchCache  

- Konfigurieren von Verteilungspunkten für die Bandbreitensteuerung  

- Manuelles Kopieren von Inhalt an Verteilungspunkte (vorab bereitstellen von Inhalt)  


Erwägen Sie, einen Verteilungspunkt bereitzustellen, anstatt einen weiteren Standort zu installieren, falls Folgendes zutrifft:  

- Ihre Netzwerkbandbreite reicht für die Kommunikation zwischen Clientcomputern am Remotestandort und einem Verwaltungspunkt am primären Standort aus. Clients kommunizieren mit einem Verwaltungspunkt, um Clientrichtlinien herunterzuladen und Inventurdaten, Statusberichte und Ermittlungsinformationen zu senden.  

- Die von Background Intelligent Transfer Service (BITS) bereitgestellte Bandbreitensteuerung deckt sich nicht mit Ihren Netzwerkanforderungen.  

Weitere Informationen zu Optionen für die Inhaltsverwaltung in Configuration Manager finden Sie unter [Grundlegende Konzepte für die Inhaltsverwaltung](fundamental-concepts-for-content-management.md).  



##  <a name="beyond-hierarchy-topology"></a><a name="bkmk_beyond"></a> Jenseits der Hierarchietopologie  

Berücksichtigen Sie zusammen mit Ihrer anfänglichen Hierarchietopologie auch die folgenden Fragen:  

- Welche Standortsystemrollen bieten Dienste oder Funktionen von verschiedenen Standorten in der Hierarchie?  

- Wie verwalten Sie hierarchieweite Konfigurationen und Funktionen in Ihrer Infrastruktur?  


Die folgenden allgemeinen Überlegungen werden in separaten Artikeln behandelt. Diese Informationen sind wichtig, da sie Ihren Hierarchieentwurf beeinflussen, oder von diesem beeinflusst werden können:  

- Wenn Sie die [Verwaltung von Computern und Geräten](../../clients/manage/manage-clients.md) vorbereiten, sollten Sie berücksichtigen, ob die Geräte sich an Ihrem Standort oder in der Cloud befinden, oder ob eigene Geräte der Benutzer darunter sind (BYOD). Berücksichtigen Sie außerdem, wie Sie Geräte verwalten werden, die mehrere Verwaltungsoptionen unterstützen. Sie können z.B. Windows 10-Geräte mit Configuration Manager oder durch die Integration in Microsoft Intune verwalten. Weitere Informationen finden Sie unter [Wählen einer Geräteverwaltungslösung](../choose-a-device-management-solution.md).  

- Verstehen Sie mögliche Auswirkungen Ihrer verfügbaren Netzwerkinfrastruktur auf den Datenfluss zwischen Remotestandorten. Weitere Informationen finden Sie unter [Einrichten von Firewalls, Ports und Domänen](../network/configure-firewalls-ports-domains.md). Berücksichtigen Sie auch den geografischen Standort Ihrer Benutzer und Geräte und ob diese Zugriff auf Ihre Infrastruktur über Ihr lokales Netzwerk oder das Internet benötigen.  

- Planen Sie eine Inhaltsinfrastruktur für die effiziente Verteilung des Inhalts, den Sie für die von Ihnen verwalteten Geräte bereitstellen. Dieser Inhalt kann aus Anwendungen, Softwareupdates oder Betriebssystemen bestehen. Weitere Informationen finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur](../../servers/deploy/configure/manage-content-and-content-infrastructure.md).  

- Bestimmen Sie, welche [Features und Funktionen von Configuration Manager](../changes/features-and-capabilities.md) Sie verwenden möchten. Andere Features erfordern andere Standortsystemrollen oder eine andere Windows-Infrastruktur. Entscheiden Sie in einer Hierarchie mit mehreren Standorten, wo Sie diese bereitstellen, um die effizienteste Nutzung Ihres Netzwerks und Ihrer Serverressourcen zu gewährleisten.  

- Berücksichtigen Sie die Daten- und Gerätesicherheit, einschließlich der Verwendung einer Public Key-Infrastruktur (PKI). Weitere Informationen zu PKI-Zertifikatanforderungen finden Sie unter [PKI-Zertifikatanforderungen](../network/pki-certificate-requirements.md).  


In den folgenden Artikeln finden Sie standortspezifische Konfigurationen:  

- [Planen des SMS-Anbieters](plan-for-the-sms-provider.md)  

- [Planen der Standortdatenbank](plan-for-the-site-database.md)  

- [Planen für Standortsystemserver und Standortsystemrollen](plan-for-site-system-servers-and-site-system-roles.md)  

- [Planen der Sicherheit](../security/plan-for-security.md)  

- [Managing network bandwidth](manage-network-bandwidth.md) bei der Bereitstellung von Inhalten innerhalb eines Standorts  


Ziehen Sie Konfigurationen in Betrachten, die Standorte und Hierarchien umfassen:  

- [High availability options](../../servers/deploy/configure/high-availability-options.md) (Optionen für Hochverfügbarkeit) für Standorte und Hierarchien

- [Erweitern des Active Directory-Schemas](../network/extend-the-active-directory-schema.md) und Konfigurieren von Standorten für die [Veröffentlichung von Standortdaten](../../servers/deploy/configure/publish-site-data.md)  

- [Datenübertragungen zwischen Standorten](data-transfers-between-sites.md)  

- [Grundlagen der rollenbasierten Verwaltung](../../understand/fundamentals-of-role-based-administration.md)  

- [Verwalten von Clients im Internet](../../clients/manage/manage-clients-internet.md)  

