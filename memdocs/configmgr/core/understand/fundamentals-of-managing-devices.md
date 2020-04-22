---
title: Grundlagen der Verwaltung von Geräten
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Geräte mit Configuration Manager verwalten.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2bca3db9-115a-451d-8c93-f073ceefe0c7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bbe7f3a69694395f95596f7f1497c7356b33715f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707068"
---
# <a name="fundamentals-of-managing-devices-with-configuration-manager"></a>Grundlagen der Verwaltung von Geräten mit System Center Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

System Center Configuration Manager kann zwei große Gruppen von Geräten verwalten:

- *Clients* sind Geräte wie Arbeitsstationen, Laptops, Server und mobile Geräte, auf denen die Configuration Manager-Clientsoftware installiert wird. Einige Verwaltungsfunktionen, z.B. Hardwareinventur, erfordern diese Clientsoftware.  

- Zu *verwalteten Geräten* können *Clients* zählen, aber normalerweise handelt es sich um ein mobiles Gerät, auf dem die Configuration Manager-Clientsoftware nicht installiert ist. Auf dieser Art von Gerät erfolgt die Verwaltung mithilfe der in Configuration Manager integrierten lokalen mobilen Geräteverwaltung.

Sie können Geräte außerdem nicht nur anhand des Clienttyps, sondern auch anhand des Benutzers gruppieren und identifizieren.

## <a name="managing-devices-with-the-configuration-manager-client"></a>Verwalten von Geräten mit dem Configuration Manager-Client

Die Configuration Manager-Clientsoftware kann auf zwei Weisen zum Verwalten von Geräten verwendet werden. Bei der ersten wird das Gerät zunächst in Ihrem Netzwerk ermittelt. Anschließend wird die Clientsoftware auf diesem Gerät bereitgestellt. Bei der zweiten wird die Clientsoftware manuell auf einem neuen Computer installiert, der dann Ihrem Standort beitritt, wenn dieser Ihrem Netzwerk beitritt. Um Geräte zu ermitteln, auf denen die Clientsoftware nicht installiert ist, verwenden Sie eine oder mehrere der integrierten Ermittlungsmethoden. Nachdem ein Gerät erkannt wurde, können Sie die Clientsoftware mithilfe einer von mehreren Methoden installieren. Informationen zur Ermittlung finden Sie unter [Ausführen der Ermittlung für Configuration Manager](../servers/deploy/configure/run-discovery.md).  

Nach der Ermittlung der Geräte, die die Ausführung der Configuration Manager-Clientsoftware unterstützen, können Sie die Software mithilfe einer von mehreren Methoden installieren. Nachdem die Software installiert und der Client einem primären Standort zugewiesen wurde, können Sie mit dem Verwalten des Geräts beginnen. Es folgen gängige Installationsmethoden:

- Clientpushinstallation

- Auf Softwareupdate basierende Installation

- Gruppenrichtlinie

- Manuelle Installation auf einem Computer

- Hinzufügen des Clients zu einem Betriebssystemimage, das Sie bereitstellen  

Nachdem der Client installiert wurde, können Sie die Aufgaben bei der Verwaltung von Geräten mithilfe von Sammlungen vereinfachen. Sammlungen sind Gruppen von Geräten oder Benutzern, die Sie erstellen, damit Sie sie als Gruppe verwalten können. Beispielsweise kann es vorkommen, dass Sie eine mobile Geräteanwendung auf allen mobilen Geräten installieren möchten, die von Configuration Manager registriert wurden. In diesem Fall können Sie die Sammlung „Alle mobilen Geräte“ verwenden.  

Weitere Informationen finden Sie in den folgenden Artikeln:  

- [Wählen einer Geräteverwaltungslösung](../plan-design/choose-a-device-management-solution.md)  

- [Clientinstallationsmethoden](../clients/deploy/plan/client-installation-methods.md)  

- [Einführung in Sammlungen](../clients/manage/collections/introduction-to-collections.md)  

### <a name="client-settings"></a>Clienteinstellungen

Bei der Erstinstallation von Configuration Manager werden alle Clients in der Hierarchie mit den Clientstandardeinstellungen konfiguriert, die Sie ändern können. Die Clienteinstellungen umfassen diese Konfigurationsoptionen:

- Wie häufig die Geräte mit dem Standort kommunizieren

- Ob der Client für Softwareupdates und andere Verwaltungsvorgänge eingerichtet ist

- Ob Benutzer ihre mobilen Geräte so registrieren können, dass sie von Configuration Manager verwaltet werden  

Sie können benutzerdefinierte Clienteinstellungen erstellen und diese dann Sammlungen zuweisen. Elemente der Sammlung sind so konfiguriert, dass sie die benutzerdefinierten Einstellungen haben. Sie können auch mehrere benutzerdefinierte Clienteinstellungen erstellen, die in der angegebenen (numerischen) Reihenfolge angewendet werden. Bei Konflikten setzt die Einstellung mit der niedrigsten Reihenfolgennummer die anderen Einstellungen außer Kraft.  

Die folgende Abbildung zeigt ein Beispiel der Erstellung und Anwendung benutzerdefinierter Clienteinstellungen.  

![Clienteinstellungen](media/ClientSettings.gif)  

Weitere Informationen zu Clienteinstellungen finden Sie in den folgenden Artikeln:

- [Konfigurieren von Clienteinstellungen](../clients/deploy/configure-client-settings.md)
- [Informationen zu Clienteinstellungen](../clients/deploy/about-client-settings.md)


## <a name="managing-devices-without-the-configuration-manager-client"></a>Verwalten von Geräten ohne Configuration Manager-Client

Configuration Manager unterstützt die Verwaltung einiger Geräte, auf denen die Clientsoftware nicht installiert ist und die nicht von Intune verwaltet werden. Weitere Informationen finden Sie unter [Verwalten mobiler Geräte mithilfe lokaler Infrastruktur in Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) und [Verwalten von mobilen Geräten mit Configuration Manager und Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

## <a name="user-based-management"></a>Benutzerbasierte Verwaltung

Configuration Manager unterstützt Sammlungen von Azure Active Directory- und Active Directory Domain Services-Benutzern. Wenn Sie eine Benutzersammlung verwenden, können Sie Software auf allen Computern installieren, die von Mitgliedern der Sammlung verwendet werden. Um sicherzustellen, dass die von Ihnen bereitgestellte Software nur auf den Geräten installiert wird, die als primäres Gerät eines Benutzers angegeben sind, richten Sie die Affinität zwischen Benutzer und Gerät ein. Ein Benutzer kann über ein oder mehrere primäre Geräte verfügen.  

Eine der Möglichkeiten, mit denen Benutzer die Softwarebereitstellung auf ihren Geräten steuern können, ist die Verwendung der Clientbenutzeroberfläche **Softwarecenter**. Das **Softwarecenter** wird automatisch auf Clientcomputern installiert und über das **Startmenü** von Windows aufgerufen. Mithilfe des **Softwarecenters** können Benutzer ihre eigene Software verwalten und folgende Aufgaben ausführen:  

- Installieren von Software  

- Planen der automatischen Installation der Software außerhalb der Arbeitszeit  

- Konfigurieren, wann die Installation von Software auf einem Gerät durch Configuration Manager zulässig ist  

- Konfigurieren der Zugriffseinstellungen für die Remotesteuerung, wenn die Remotesteuerung in Configuration Manager eingerichtet ist  

- Konfigurieren von Optionen für die Energieverwaltung, sofern diese von einem Administrator eingerichtet wurde  

- Suchen, Installieren und Anfordern von Software

- Konfigurieren von Einstellungen

- Angeben eines primären Geräts für die Affinität zwischen Benutzer und Gerät (sofern eingerichtet)

Weitere Informationen finden Sie in den folgenden Artikeln:

- [Planen für Software Center](../../apps/plan-design/plan-for-software-center.md)
- [Verknüpfen von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)
- [Benutzerleitfaden des Softwarecenters](software-center.md)
