---
title: Planen der Berichterstellung
titleSuffix: Configuration Manager
description: Die Berichterstellung in Configuration Manager zu planen ist wichtig. Dies gilt von Installationsdetails über die Sicherheit bis hin zur Netzwerkbandbreite.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ff920c84-d5c8-458c-b67f-bc7219b05690
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2621a6a364734a1146700aa8eef8fded3a6e58ab
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694368"
---
# <a name="plan-for-reporting-in-configuration-manager"></a>Planen der Berichterstellung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Zur Berichterstellung in Configuration Manager gehören mehrere Tools und Ressourcen, mit deren Hilfe Sie die erweiterten Berichterstellungsfunktionen der SQL Server Reporting Services oder des Power BI-Berichtsservers nutzen können. Anhand der folgenden Abschnitte können Sie die Berichterstellung in Configuration Manager planen.

## <a name="where-to-install-the-reporting-services-point"></a>Installationsort für den Reporting Services-Punkt

Beim Ausführen von Configuration Manager-Berichten an einem Standort sind die Informationen in der Standortdatenbank für die Berichte zugänglich. Anhand der folgenden Abschnitte können Sie festlegen, wo der Reporting Services-Punkt installiert und welche Datenquelle verwendet werden soll.

> [!NOTE]
> Weitere Informationen zur Planung der Standortsysteme finden Sie unter [Hinzufügen von Standortsystemrollen](../deploy/configure/add-site-system-roles.md).

### <a name="supported-site-system-servers"></a>Unterstützte Standortsystemserver

Sie können den Reporting Services-Punkt auf einem Standort der zentralen Verwaltung und auf primären Standorten installieren. Dies funktioniert auf mehreren Standortsystemen an einem Standort sowie anderen Standorten in der Hierarchie. Configuration Manager unterstützt den Reporting Services-Punkt an sekundären Standorten. Der erste Reporting Services-Punkt an einem Standort wird als Standardberichtsserver festgelegt. Sie können weitere Reporting Services-Punkte zu einem Standort hinzufügen, jedoch verwenden Configuration Manager-Berichte nur den Standardberichtsserver jedes Standorts aktiv. Installieren Sie den Reporting Services-Punkt auf dem Standortserver oder einem Remotestandortsystem. Verwenden Sie SQL Server Reporting Services auf einem Remotestandort-Systemserver, um die beste Leistung zu erzielen.

### <a name="data-replication-considerations"></a>Überlegungen zur Datenreplikation

Berücksichtigen Sie bei der Entscheidung, wo die Reporting Services-Punkte installiert werden soll, folgende Faktoren:

- Ein Reporting Services-Punkt mit der Datenbank des Standorts der zentralen Verwaltung als Berichtsdatenquelle verfügt über Zugriff auf alle globalen Daten und alle Standortdaten in der Configuration Manager-Hierarchie. Wenn Sie Berichte benötigen, die Standortdaten für mehrere Standorte in einer Hierarchie enthalten, sollten Sie die Installation des Reporting Services-Punkts auf einem Standortsystem am Standort der zentralen Verwaltung in Betracht ziehen. Verwenden Sie dann dessen Datenbank als Berichtsdatenquelle.

- Ein Reporting Services-Punkt mit einer untergeordneten primären Standortdatenbank als Datenquelle verfügt über Zugriff auf die globalen Daten und Standortdaten des lokalen primären Standorts sowie dessen untergeordneten sekundären Standorte. Standortdaten für andere primäre Standorte in der Configuration Manager-Hierarchie werden nicht an diesem primären Standort repliziert. Reporting Services kann nicht auf Standortdaten anderer primärer Standorte zugreifen. Wenn Sie Berichte benötigen, die Standortdaten für einen spezifischen primären Standort oder globale Daten enthalten, und Sie den Benutzern keinen Zugriff auf Standortdaten anderer primärer Standorte gewähren möchten, installieren Sie einen Reporting Services-Punkt auf einem Standortsystem am primären Standort. Verwenden Sie dann die Datenbank des primären Standorts als Berichtsdatenquelle.

Weitere Informationen zu globalen und Standortdaten finden Sie unter [Datentypen](../../plan-design/hierarchy/database-replication.md#types-of-data).

### <a name="network-bandwidth-considerations"></a>Überlegungen zur Netzwerkbandbreite

Je nachdem, wie Sie den Standort konfigurieren, kommunizieren die Standortsysteme am selben Standort über SMB (Server Message Block), HTTP oder HTTPS miteinander. Configuration Manager verwaltet diese Kommunikation nicht. Sie kann jederzeit und ohne Steuerung der Netzwerkbandbreite auftreten. Überprüfen Sie Ihre verfügbare Netzwerkbandbreite, bevor Sie die Rolle „Reporting Services-Punkt“ auf einem Standortsystem installieren.

Weitere Informationen zur Planung der Standortsysteme finden Sie unter [Hinzufügen von Standortsystemrollen](../deploy/configure/add-site-system-roles.md).

## <a name="plan-for-role-based-administration"></a>Planen der rollenbasierten Verwaltung

Das Sicherheitskonzept bei der Berichterstattung ist mit dem vieler anderer Objekte in Configuration Manager vergleichbar: Sie können Sicherheitsrollen und Berechtigungen an Administratoren vergeben. Administratoren können nur Berichte ausführen und ändern, bei denen sie über die entsprechenden Sicherheitsrechte verfügen. Zum Ausführen der Berichte in der Configuration Manager-Konsole benötigen Benutzer das Recht **Lesen** für die Berechtigung **Standort** sowie für bestimmte Objekte konfigurierte Berechtigungen.

Im Gegensatz zu anderen Objekten in Configuration Manager werden die Sicherheitsrechte, die Sie in der Configuration Manager-Konsole für Administratoren festlegen, auch in Reporting Services konfiguriert. Beim Konfigurieren der Sicherheitsrechte in der Configuration Manager-Konsole wird vom Reporting Services-Punkt eine Verbindung mit Reporting Services hergestellt, und es werden entsprechende Berechtigungen für die Berichte eingeholt.

Beispielsweise verfügt die Sicherheitsrolle **Softwareupdate-Manager** über die Berechtigungen **Bericht ausführen** und **Bericht ändern**. Benutzer mit der Rolle **Softwareupdate-Manager** können Berichte nur für Softwareupdates ausführen und ändern. Die Configuration Manager-Konsole zeigt dieser Rolle keine Berichte zu anderen Objekten an. Die Ausnahme dieses Verhaltens besteht darin, dass einige Berichte keinen bestimmten sicherungsfähigen Configuration Manager-Objekten zugeordnet werden. Bei solchen Berichten benötigen Administratoren das Recht **Schreiben** für die Berechtigung **Standort** , um die Berichte auszuführen, und das Recht **Ändern** für die Berechtigung **Standort** , um die Berichte zu ändern.  

> [!IMPORTANT]
> Damit Benutzer, die zu einer anderen Domäne als dem Reporting Services-Punktkonto gehören, Berichte erfolgreich ausführen können, muss eine bidirektionale Vertrauensstellung zwischen den beiden Domänen eingerichtet werden.

Berichte sind für die rollenbasierte Verwaltung komplett aktiviert. Configuration Manager filtert die Daten auf alle enthaltenen Berichte basierend auf Berechtigungen des Benutzers, der den Bericht ausführt. Benutzer mit spezifischen Rollen können nur Informationen anzeigen, die für ihre Rollen definiert sind.

Weitere Informationen zu Sicherheitsrechten für die Berichterstellung finden Sie unter [Konfigurieren der Berichterstellung](configuring-reporting.md).

Weitere Informationen zur rollenbasierten Verwaltung in Configuration Manager finden Sie unter [Konfigurieren einer rollenbasierten Verwaltung](../deploy/configure/configure-role-based-administration.md).

## <a name="reporting-recommendations"></a>Empfehlungen zur Berichterstellung

Beachten Sie die folgenden Empfehlungen und Tipps für die Berichterstellung in Configuration Manager:

- Installieren Sie den Reporting Services-Punkt auf einem Remotestandortsystem, um die beste Leistung zu erzielen. Obwohl Sie ihn auf dem Standortserver installieren können, erzielt der Reporting Services-Punkt die beste Leistung, wenn Sie ihn auf einem Remotestandortsystem installieren. Wenn diese Rolle Hintergrundverarbeitung durchführt, kann sie mit anderen Rollen um Systemressourcen konkurrieren. Es gibt viele Variablen, die bei der Leistung von Standorten und Rollen berücksichtigt werden sollten, im Allgemeinen verbessert diese Konfiguration die Berichterstellung und die allgemeine Leistung des Standorts.

- Optimieren Sie die Abfragen von SQL Server Reporting Services. In der Regel sind Verzögerungen bei der Berichterstattung darauf zurückzuführen, dass das Ausführen von Abfragen und das Abrufen der Ergebnisse Zeit kosten. Microsoft SQL Server-Tools wie Query Analyzer und Profiler können Sie beim Optimieren von Abfragen unterstützen.

- Planen Sie die Verarbeitung von Berichtsabonnements für die Ausführung außerhalb der üblichen Geschäftszeiten. Wenn Abonnements weitgehend außerhalb der Geschäftszeiten verarbeitet werden, wird die CPU-Verarbeitung des Configuration Manager-Standortdatenbankservers reduziert. Durch dieses Vorgehen wird auch die Verfügbarkeit von unvorhergesehenen Berichtsanforderungen verbessert.

- Bei Standortupdates werden integrierte Berichte beibehalten. Wenn Sie einen Standardbericht ändern, wird dem Namen des Berichts beim Aktualisieren des Standorts ein Unterstrich (`_`) als Präfix vorangestellt. Durch dieses Verhalten wird sichergestellt, dass der geänderte Bericht beim Aktualisieren des Standorts nicht durch den Standardbericht überschrieben wird.

## <a name="security-and-privacy"></a>Sicherheit und Datenschutz

In Configuration Manager-Berichten werden Informationen angezeigt, die bei Standardverwaltungsvorgängen in Configuration Manager gesammelt werden. Sie können beispielsweise einen Bericht mit Informationen anzeigen, die Configuration Manager anhand der Ermittlung oder der Inventur erfasst hat. Außerdem können Berichte aktuelle Statusinformationen zu Clientverwaltungsvorgängen wie Softwarebereitstellung und Kompatibilitätsprüfung enthalten.

Weitere Informationen über Sicherheitsempfehlungen und Datenschutzinformationen für Configuration Manager-Vorgänge, die möglicherweise Daten generieren, die Sie in Berichten anzeigen können, finden Sie unter [Sicherheit und Datenschutz für Configuration Manager](../../plan-design/security/security-and-privacy.md).  

## <a name="next-steps"></a>Nächste Schritte

[Voraussetzungen für die Berichterstellung](prerequisites-for-reporting.md)
