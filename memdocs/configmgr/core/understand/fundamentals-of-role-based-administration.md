---
title: Grundlagen der rollenbasierten Verwaltung
titleSuffix: Configuration Manager
description: Verwenden Sie die rollenbasierte Verwaltung zum Steuern des administrativen Zugriffs auf Configuration Manager und Objekte, die Sie verwalten.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0a2d6c3f-a4e4-4c19-b087-3caada480de9
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c39d3380212debe97c2d2f33de6a98fecfb8402e
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126051"
---
# <a name="fundamentals-of-role-based-administration-for-configuration-manager"></a>Grundlagen der rollenbasierten Verwaltung für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Bei Configuration Manager verwenden Sie die rollenbasierte Verwaltung, um den Zugriff zu schützen, der zum Verwalten von Configuration Manager erforderlich ist. Ferner schützen Sie damit den Zugriff auf die Objekte, die Sie verwalten, wie Sammlungen, Bereitstellungen und Standorte. Nachdem Sie sich mit den in diesem Artikel behandelten Konzepten vertraut gemacht haben, können Sie mit dem [Konfigurieren der rollenbasierten Verwaltung für Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md) fortfahren.  

 Über das rollenbasierte Verwaltungsmodell werden Sicherheitszugriffseinstellungen für alle Standorte und Standorteinstellungen hierarchieweit zentral definiert und verwaltet. Dazu dienen die folgenden Elemente:  

- *Sicherheitsrollen* werden Administratoren zugewiesen, um diesen Benutzern (oder Benutzergruppen) Berechtigungen für verschiedene Configuration Manager-Objekte zu erteilen. Dies ist z.B. zum Erstellen oder Ändern von Clienteinstellungen der Fall.  

- Mithilfe von *Sicherheitsbereichen* werden bestimmte Instanzen von Objekten gruppiert, für deren Verwaltung ein Administrator verantwortlich ist, z. B. eine Anwendung zum Installieren von Microsoft 365 Apps.  

- *Sammlungen* dienen zum Angeben von Gruppen von Benutzer- und Geräteressourcen, die der Administrator verwalten kann.  

  Mit der Kombination aus Sicherheitsrollen, Sicherheitsbereichen und Sammlungen trennen Sie die administrativen Aufgaben, die die Anforderungen Ihres Unternehmens erfüllen. Wenn sie zusammen verwendet werden, definieren sie den Verwaltungsumfang eines Benutzers, den dieser Benutzer in Ihrer Configuration Manager-Bereitstellung anzeigen und verwalten kann.  

## <a name="benefits-of-role-based-administration"></a>Vorteile der rollenbasierten Verwaltung  

- Standorte fungieren nicht als Verwaltungsgrenzen.  
- Sie richten Administratoren für die Hierarchie ein und müssen für diese nur eine einmalige Sicherheitszuweisung ausführen.  
- Alle Sicherheitszuweisungen werden repliziert und sind in der gesamten Hierarchie verfügbar.  
- Es gibt integrierte Sicherheitsrollen, die zum Zuweisen der typischen Verwaltungsaufgaben verwendet werden. Sie können eigene benutzerdefinierte Sicherheitsrollen für Ihre speziellen Geschäftsanforderungen erstellen.  
- Administratoren können nur die Objekte ansehen, für die sie über Berechtigungen zum Verwalten verfügen.  
- Sie können Verwaltungssicherheitsvorgänge überwachen.  

Beim Entwerfen und Implementieren der administrativen Sicherheit für Configuration Manager nutzen Sie Folgendes, um einen *Verwaltungsbereich* für einen Administrator zu erstellen:  

- [Sicherheitsrollen](#bkmk_Planroles)  

- [Sammlungen](#bkmk_planCol)  

- [Sicherheitsbereichen](#bkmk_PlanScope)  

 Mit diesem Verwaltungsbereich werden die Objekte, die ein Administrator in der Configuration Manager-Konsole anzeigen kann, sowie die Berechtigungen dieses Benutzers in Bezug auf diese Objekte verwaltet. Konfigurationen der rollenbasierten Administration werden als globale Daten an allen Standorten in der Hierarchie repliziert und auf alle Verwaltungsverbindungen angewendet.  

> [!IMPORTANT]  
> Aufgrund von Verzögerungen bei der standortübergreifenden Replikation können Änderungen an der rollenbasierten Verwaltung möglicherweise nicht von einem Standort empfangen werden. Informationen zur Überwachung der standortübergreifenden Datenbankreplikation finden Sie unter [Datenübertragungen zwischen Standorten](../plan-design/hierarchy/data-transfers-between-sites.md).  

##  <a name="security-roles"></a><a name="bkmk_Planroles"></a> Sicherheitsrollen

 Verwenden Sie Sicherheitsrollen, um Administratoren Sicherheitsberechtigungen zu erteilen. Bei Sicherheitsrollen handelt es sich um Gruppen von Sicherheitsberechtigungen, die Sie Administratoren zuweisen, damit diese ihre Verwaltungsaufgaben erfüllen können. Aus diesen Sicherheitsberechtigungen geht hervor, welche Verwaltungsaufgaben ein Administrator ausführen darf und welche Berechtigungen ihm für bestimmte Objekttypen gewährt werden. Aus Sicherheitsgründen wird empfohlen, die Sicherheitsrollen zuzuweisen, mit denen die wenigsten Berechtigungen erteilt werden.  

 In Configuration Manager gibt es mehrere integrierte Sicherheitsrollen zur Unterstützung typischer Gruppen von Verwaltungsaufgaben. Sie können auch benutzerdefinierte Sicherheitsrollen erstellen, die im Einklang mit Ihren Geschäftsanforderungen stehen. Beispiele für die integrierten Sicherheitsrollen:  

- *Hauptadministrator* gewährt sämtliche Berechtigungen in Configuration Manager.  

- Der *Asset-Manager* gewährt Berechtigungen zum Verwalten des Asset Intelligence-Synchronisierungspunkts, von Asset Intelligence-Berichtsklassen, Softwareinventur, Hardwareinventur sowie Messungsregeln.  

- *Softwareupdate-Manager* gewährt Berechtigungen zum Definieren und Bereitstellen von Softwareupdates. Administratoren, denen diese Rolle zugeordnet ist, können Sammlungen, Softwareupdategruppen, Bereitstellungen und Vorlagen erstellen.  

- Der *Sicherheitsadministrator* gewährt Berechtigungen, um Administratoren hinzuzufügen und zu entfernen und Administratoren Sicherheitsrollen, Sammlungen und Sicherheitsbereiche zuzuordnen. Administratoren, denen diese Rolle zugeordnet ist, können auch Sicherheitsrollen sowie diesen zugewiesene Sicherheitsbereiche und Sammlungen erstellen, ändern und löschen.

> [!TIP]  
> Sie können die Liste der integrierten und benutzerdefinierten Sicherheitsrollen mit ihren Beschreibungen in der Configuration Manager-Konsole anzeigen. Um die Rollen anzuzeigen, erweitern Sie im Arbeitsbereich **Verwaltung** den Knoten **Sicherheit**, und wählen Sie dann **Sicherheitsrollen** aus.  

 Jeder Sicherheitsrolle sind bestimmte Berechtigungen für die verschiedenen Objekttypen zugeordnet. Die Sicherheitsrolle *Anwendungsautor* umfasst zum Beispiel die folgenden Berechtigungen für Anwendungen: Genehmigen, Erstellen, Löschen, Ändern, Ordner ändern, Objekt verschieben, Lesen, Bericht ausführen und Sicherheitsbereiche festlegen.

 Sie können die Berechtigungen der integrierten Sicherheitsrollen nicht ändern. Es ist aber möglich, eine Rolle zu kopieren, zu ändern und die geänderte Rolle als neue benutzerdefinierte Sicherheitsrolle zu speichern. Sie können außerdem Sicherheitsrollen importieren, die Sie aus einer anderen Hierarchie exportiert haben, z. B. aus einem Testnetzwerk. Überprüfen Sie die Sicherheitsrollen und deren Berechtigungen, um festzustellen, ob Sie die integrierten Sicherheitsrollen verwenden können oder ob Sie eigene benutzerdefinierte Sicherheitsrollen erstellen müssen.  

### <a name="to-help-you-plan-for-security-roles"></a>Nützliche Hinweise für das Planen von Sicherheitsrollen  

1. Identifizieren Sie die Tasks, die Administratoren in Configuration Manager ausführen. Dabei kann es sich um Gruppen von Verwaltungstasks handeln, wie z. B. Bereitstellen von Anwendungen und Paketen, Bereitstellen von Betriebssystemen und Kompatibilitätseinstellungen, Konfigurieren von Standorten und Sicherheit, Überwachung, Remotesteuerung von Computern und Sammeln von Inventurdaten.  

2. Ordnen Sie diese Verwaltungstasks mindestens einer der integrierten Sicherheitsrollen zu.  

3. Wenn einige Administratoren die Tasks mehrerer Sicherheitsrollen ausführen, weisen Sie diesen Administratoren alle relevanten Sicherheitsrollen zu, statt eine neue Sicherheitsrolle zu erstellen, in der diese Tasks enthalten sind.  

4. Wenn die identifizierten Tasks den integrierten Sicherheitsrollen nicht zugewiesen werden können, erstellen und testen Sie neue Sicherheitsrollen.  

Informationen zum Erstellen und Konfigurieren von Sicherheitsrollen für die rollenbasierte Verwaltung finden Sie unter [Erstellen benutzerdefinierter Sicherheitsrollen](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_CreateSecRole) und [Konfigurieren von Sicherheitsrollen](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecRole) im Artikel [Konfigurieren der rollenbasierten Verwaltung für Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).  

##  <a name="collections"></a><a name="bkmk_planCol"></a> Sammlungen

 Mithilfe von Sammlungen werden die Benutzer- und Computerressourcen angegeben, die ein Administrator anzeigen oder verwalten kann. Damit Administratoren beispielsweise Anwendungen bereitstellen oder die Remotesteuerung ausführen können, müssen sie einer Sicherheitsrolle zugewiesen werden, mit der Zugriff auf eine Sammlung gewährt wird, die diese Ressourcen enthält. Sie können Sammlungen von Benutzern oder Geräten auswählen.  

 Weitere Informationen zu Sammlungen finden Sie unter [Einführung in Sammlungen](../../core/clients/manage/collections/introduction-to-collections.md).  

 Überprüfen Sie vor dem Konfigurieren der rollenbasierten Verwaltung, ob folgende Gründe für das Erstellen neuer Sammlungen vorliegen:  

- Funktionsorganisation. Beispielsweise getrennte Sammlungen von Servern und Arbeitsstationen.  
- Geografische Ausrichtung. Beispielsweise getrennte Sammlungen für Nordamerika und Europa.  
- Sicherheitsanforderungen und Geschäftsprozesse. Beispielsweise getrennte Sammlungen für Produktions- und Testcomputer.  
- Organisationsausrichtung. Beispielsweise getrennte Sammlungen für jeden Geschäftsbereich.  

Informationen zum Konfigurieren von Sammlungen für die rollenbasierte Verwaltung finden Sie unter [Konfigurieren von Sammlungen zum Verwalten der Sicherheit](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigColl) im Artikel [Konfigurieren der rollenbasierten Verwaltung für Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).  

## <a name="security-scopes"></a><a name="bkmk_PlanScope"></a> Sicherheitsbereichen

 Mithilfe von Sicherheitsbereichen können Sie Administratoren Zugriff auf sicherungsfähige Objekte gewähren. Bei einem Sicherheitsbereich handelt es sich um benannte Sätze von sicherungsfähigen Objekten, die Administratoren als Gruppe zugewiesen werden. Alle sicherungsfähigen Objekte müssen mindestens einem Sicherheitsbereich zugewiesen werden. Configuration Manager verfügt über zwei integrierte Sicherheitsbereiche:  

- Der integrierte Sicherheitsbereich *Alle* gewährt Zugriff auf alle Bereiche. Diesem Sicherheitsbereich können keine Objekte zugewiesen werden.  

- Der integrierte Sicherheitsbereich *Standard* wird standardmäßig für alle Objekte verwendet. Bei der Erstinstallation von Configuration Manager werden alle Objekte diesem Sicherheitsbereich zugewiesen.  

Wenn Sie die Objekte beschränken möchten, die von Administratoren angezeigt und verwaltet werden können, müssen Sie eigene benutzerdefinierte Sicherheitsbereiche erstellen und verwenden. Sicherheitsbereiche unterstützen keine hierarchische Struktur und können nicht geschachtelt werden. Sicherheitsbereiche können mehrere Objekttypen enthalten, darunter die folgenden Objekte:  

- Benachrichtigungsabonnements  
- Applications  
- Startabbilder  
- Begrenzungsgruppen  
- Konfigurationselemente  
- Benutzerdefinierte Clienteinstellungen  
- Verteilungspunkte und Verteilungspunktgruppen  
- Treiberpakete
- Ordner (ab Version 1906) <!--3600867-->
- Globale Bedingungen  
- Migrationsaufträge
- Betriebssystemabbilder
- Installationspakete für Betriebssysteme  
- Pakete  
- Abfragen  
- Standorte  
- Softwaremessungsregeln  
- Softwareupdategruppen  
- Softwareupdatepakete  
- Tasksequenzpakete  
- Windows CE-Geräteeinstellungselemente und -pakete  

Einige Objekte können Sicherheitsbereichen nicht zugewiesen werden, da sie nur durch Sicherheitsrollen gesichert werden. Der Administratorzugriff auf diese Objekte kann nicht auf eine Teilmenge der verfügbaren Objekte beschränkt werden. Zum Beispiel erstellt ein Administrator Begrenzungsgruppen, die für einen bestimmten Standort verwendet werden. Da für das Grenzobjekt keine Sicherheitsbereiche unterstützt werden, ist es nicht möglich, diesem Benutzer einen Sicherheitsbereich zuzuweisen, der den Zugriff nur auf die diesem Standort zugeordneten Grenzen gewährt. Da Grenzobjekte Sicherheitsbereichen nicht zugeordnet werden können, erhält dieser Benutzer Zugriff auf alle Grenzen in der Hierarchie, wenn Sie ihm eine Sicherheitsrolle zuweisen, die ihm Zugriff auf Grenzobjekte gewährt.  

Zu den Objekten, die nicht durch Sicherheitsbereiche eingeschränkt sind, zählen folgende Objekte:  

- Active Directory-Gesamtstrukturen  
- Administratoren  
- Warnungen  
- Richtlinien für Antischadsoftware  
- Standortgrenzen  
- Computerzuordnungen  
- Clientstandardeinstellungen  
- Bereitstellungsvorlagen  
- Gerätetreiber  
- Exchange Server-Connector  
- Zuordnungen der Migration zwischen Standorten  
- Anmeldungsprofile für mobile Geräte  
- Sicherheitsrollen  
- Sicherheitsbereichen  
- Standortadressen  
- Standortsystemrollen  
- Softwaretitel  
- Softwareupdates  
- Statusmeldungen  
- Affinitäten zwischen Benutzer und Gerät  

Erstellen Sie Sicherheitsbereiche, wenn Sie den Zugriff auf separate Instanzen von Objekten beschränken müssen. Beispiel:  

- Eine Gruppe von Administratoren muss Produktionsanwendungen anzeigen können, jedoch keine Testanwendungen. Erstellen Sie einen Sicherheitsbereich für Produktionsanwendungen und eine weitere für die Testanwendungen.  

- Verschiedene Administratoren benötigen unterschiedliche Zugriffsberechtigungen für einige Instanzen eines Objekttyps. Zum Beispiel benötigt eine Administratorengruppe die Berechtigung „Lesen“ für bestimmte Softwareupdategruppen, und eine andere Administratorengruppe benötigt die Berechtigungen „Ändern“ und „Löschen“ für andere Softwareupdategruppen. Erstellen Sie unterschiedliche Sicherheitsbereiche für diese Softwareupdategruppen.  

Informationen zum Konfigurieren von Sicherheitsbereichen für die rollenbasierte Verwaltung finden Sie unter [Konfigurieren von Sicherheitsbereichen für ein Objekt](../../core/servers/deploy/configure/configure-role-based-administration.md#BKMK_ConfigSecScope) im Artikel [Konfigurieren der rollenbasierten Verwaltung für Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).  

## <a name="next-steps"></a>Nächste Schritte

[Konfigurieren der rollenbasierten Verwaltung für Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md)
