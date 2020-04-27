---
title: Tipps zur Problembehandlung für App-Bereitstellungen
titleSuffix: Configuration Manager
description: Hier finden Sie Tipps zur Behandlung von Problemen bei der Bereitstellung von Anwendungen in Configuration Manager.
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 4e8b46a3-3e11-475f-a4d7-6bf9ddf14145
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 4723a85c55a2a5f7a4fbd0a99a14fbf31e7511c6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689968"
---
# <a name="troubleshooting-tips-for-application-deployments"></a>Tipps zur Problembehandlung für Anwendungsbereitstellungen

*Gilt für: Configuration Manager (Current Branch)*

Übliche Probleme bei Anwendungsbereitstellungen fallen in die folgenden Kategorien:

- Fehler beim Herunterladen der Anwendung

- Die Konformität der Anwendungsbereitstellung hängt bei 0 %

Wenn eines dieser Probleme bei Ihnen auftritt, können Sie die in diesem Artikel bereitgestellten Schritte zur Problembehandlung anwenden. Ausführlichere Informationen zur Problembehandlung finden Sie unter [Technische Referenz zur Problembehandlung bei der Bereitstellung einer Anwendung](../understand/app-deployment-technical-reference.md).


## <a name="download-failures"></a>Fehler beim Download

Folgende Probleme gehören zu Fehlern beim Download der Anwendung:

- Der Client reagiert beim Herunterladen einer Anwendung nicht mehr

- Der Client kann den Anwendungsinhalt nicht herunterladen

- Der Client bleibt beim Herunterladen der Anwendung bei 0 % hängen

Bei Problemen beim Herunterladen von Anwendungen sollten Sie zunächst überprüfen, ob Begrenzungen und Begrenzungsgruppen fehlen oder fehlerhaft konfiguriert sind. Wenn der Client sich beispielsweise im Intranet befindet oder nicht für die reine Internetverwaltung konfiguriert ist, muss sich seine Netzwerkadresse in einer konfigurierten Begrenzung befinden. Außerdem muss dieser Begrenzung eine Begrenzungsgruppe zugewiesen sein, damit der Client Inhalte herunterladen kann. Weitere Informationen finden Sie unter [Definieren von Standortgrenzen und Begrenzungsgruppen](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).

Gehen Sie folgendermaßen vor, wenn Sie keine Begrenzung für einen Client konfigurieren können oder eine spezifische Begrenzungsgruppe kein Mitglied einer anderen Begrenzungsgruppe sein kann:

1. Öffnen Sie die Eigenschaften des **Bereitstellungstyps** in der Configuration Manager-Konsole.  

1. Wechseln Sie zur Registerkarte **Inhalt**.

1. Ändern Sie die **Bereitstellungsoptionen** im Abschnitt zur Verwendung eines Verteilungspunkts aus einer benachbarten Begrenzungsgruppe in **Inhalt vom Verteilungspunkt herunterladen und lokal ausführen**. (Für diese Einstellung ist standardmäßig **Inhalt nicht herunterladen** festgelegt.)

Stellen Sie sicher, dass der Anwendungsinhalt an einen Verteilungspunkt verteilt ist, wenn der Client ihn nicht herunterladen kann. Verwenden Sie die in die Konsole integrierten Feature zum Überwachen der Verteilung von Inhalten an die Verteilungspunkte, um diese Konfiguration zu überprüfen. Weitere Informationen finden Sie unter [Überwachen von mit System Center Configuration Manager verteilten Inhalten](../../core/servers/deploy/configure/monitor-content-you-have-distributed.md).  


## <a name="compliance-stuck-at-0"></a>Konformität hängt bei 0 %

Wenn die Bereitstellungskonformität der Anwendung bei 0 % hängt, überprüfen Sie den Bereitstellungsstatus der Anwendung im Arbeitsbereich **Überwachung** im Knoten **Bereitstellungen**.

- **In Bearbeitung:** Der Client könnte beim [Herunterladen des Inhalts](#download-failures) hängen.

- **Fehler**: Weitere Informationen zur Behandlung dieses Problems finden Sie im folgenden Blogbeitrag: [Tipps und Tricks: Aktionen für Ressourcen, die eine fehlerhafte Bereitstellung melden](https://techcommunity.microsoft.com/t5/Configuration-Manager-Archive/Tips-and-Tricks-How-to-Take-Action-on-Assets-That-Report-a/ba-p/273019)

- **Unbekannt**: Dieser Status bedeutet in der Regel, dass der Client eine Richtlinie nicht empfangen hat. Aktualisieren Sie die Clientrichtlinie manuell, um zu überprüfen, ob der Client die Richtlinie empfängt. Weitere Informationen finden Sie unter [Initiieren des Richtlinienabrufs für einen Konfigurations-Manager-Client](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).
  
Überprüfen Sie den Clientstatus, wenn das Problem mithilfe dieser Maßnahmen nicht gelöst werden kann. Beim Client kann ein umfassenderes Problem vorliegen. Weitere Informationen finden Sie unter [Überwachen von Clients in Configuration Manager](../../core/clients/manage/monitor-clients.md).


## <a name="next-steps"></a>Nächste Schritte

- [Überwachen von Anwendungen](monitor-applications-from-the-console.md)
- [Bereitstellen von Anwendungen](deploy-applications.md)
- [Verwaltungstasks für Anwendungen](management-tasks-applications.md)
- [Technische Referenz zur Problembehandlung bei der Bereitstellung einer Anwendung](../understand/app-deployment-technical-reference.md)
