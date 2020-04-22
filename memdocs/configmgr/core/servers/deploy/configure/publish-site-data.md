---
title: Veröffentlichen von Standortdaten
titleSuffix: Configuration Manager
description: Hier erfahren Sie, wie Configuration Manager-Standorte in Active Directory Domain Services veröffentlicht werden.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 17cf034f-eaff-43ce-bc8e-917213c1db74
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 77ca6711f86250f4a6f937d919893cf95e022567
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700978"
---
# <a name="publish-site-data-for-configuration-manager"></a>Veröffentlichen von Standortdaten für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Nachdem Sie das Active Directory-Schema für Configuration Manager erweitert haben, können Sie die Configuration Manager-Standorte in Active Directory Domain Services (AD DS) veröffentlichen. Dadurch können Active Directory-Computer Standortinformationen gesichert aus einer vertrauenswürdigen Quelle abrufen. Das Veröffentlichen von Standortinformationen in AD DS ist für die Basisfunktionen von Configuration Manager zwar nicht erforderlich, aber Sie können hierdurch den Verwaltungsaufwand reduzieren.  

-   **Wenn ein Standort für das Veröffentlichen in AD DS konfiguriert ist**, können Configuration Manager-Clients über die Active Directory-Veröffentlichung gefunden werden. Hierzu wird eine LDAP-Abfrage an einen globalen Katalogserver gestellt.  

-   **Wenn ein Standort keine Daten in AD DS veröffentlicht**, benötigen Clients einen alternativen Mechanismus zum Auffinden ihres Standardverwaltungspunkts.  

Weitere Informationen dazu, wie Clients nach einem Verwaltungspunkt suchen, finden Sie unter [Verstehen, wie Clients Standortressourcen und -dienste für Configuration Manager suchen](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

## <a name="configure-sites-to-publish-to-ad-ds"></a>Konfigurieren von Standorten für die Veröffentlichung in AD DS  
 Es folgen die allgemeinen Schritte:  

-   Sie müssen [das Active Directory-Schema für Configuration Manager](../../../../core/plan-design/network/extend-the-active-directory-schema.md) in allen Gesamtstrukturen erweitern, in denen Sie Standortdaten veröffentlichen möchten. Zudem müssen Sie sicherstellen, dass der Container **Systemverwaltung** vorhanden ist.  

-   Sie müssen dem Computerkonto aller primären Standorte, die Daten veröffentlichen, die Berechtigung **Vollzugriff** für den Container **System Management** und all seine untergeordneten Objekte erteilen.  

### <a name="to-enable-a-configuration-manager-site-to-publish-site-information-to-active-directory-forest"></a>So aktivieren Sie einen Configuration Manager-Standort für das Veröffentlichen von Standortinformationen in einer Active Directory-Gesamtstruktur

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standortkonfiguration**, und klicken Sie auf **Standorte**. Wählen Sie den Standort aus, dessen Standortdaten veröffentlicht werden sollen. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

3.  Wählen Sie auf der Registerkarte **Veröffentlichen** der Standorteigenschaften die Gesamtstrukturen aus, in denen dieser Standort Standortdaten veröffentlichen soll.  

4.  Klicken Sie auf **OK** , um die Konfiguration zu speichern.  

### <a name="to-set-up-active-directory-forests-for-publishing"></a>So richten Sie Active Directory-Gesamtstrukturen für die Veröffentlichung ein  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2.  Erweitern Sie im Arbeitsbereich **Verwaltung** den Knoten **Hierarchiekonfiguration**, und klicken Sie auf **Active Directory-Gesamtstrukturen**. Wenn eine Active Directory-Gesamtstrukturermittlung bereits ausgeführt wurde, werden die ermittelten Gesamtstrukturen im Ergebnisbereich angezeigt. Bei der Ausführung der Active Directory-Gesamtstrukturermittlung werden die lokale Gesamtstruktur und alle vertrauenswürdigen Gesamtstrukturen ermittelt. Nur nicht vertrauenswürdige Gesamtstrukturen müssen manuell hinzugefügt werden.  

    -   Wählen Sie zum Einrichten einer bereits ermittelten Gesamtstruktur die gewünschte Gesamtstruktur im Ergebnisbereich aus. Klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**, um die Gesamtstruktureigenschaften zu öffnen. Fahren Sie mit Schritt 3 fort.  

    -   Klicken Sie zum Einrichten einer nicht aufgelisteten Gesamtstruktur auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Gesamtstruktur hinzufügen**, um das Dialogfeld **Gesamtstruktur hinzufügen** zu öffnen. Fahren Sie mit Schritt 3 fort.  

3.  Schließen Sie auf der Registerkarte **Allgemein** die Konfiguration für die zu ermittelnde Gesamtstruktur ab, und geben Sie das **Konto für die Active Directory-Gesamtstruktur** an.  

    > [!NOTE]  
    >  Für die Active Directory-Gesamtstrukturermittlung ist ein globales Konto erforderlich, damit Ermittlung und Veröffentlichung in nicht vertrauenswürdigen Gesamtstrukturen möglich sind. Wenn Sie nicht das Computerkonto des Standortservers verwenden, können Sie nur ein globales Konto auswählen.  

4.  Wenn Sie planen, eine Veröffentlichung von Standortdaten in dieser Gesamtstruktur zu ermöglichen, konfigurieren Sie auf der Registerkarte **Veröffentlichen** das Veröffentlichen in dieser Gesamtstruktur.  

    > [!NOTE]  
    >  Wenn Sie Standorte für die Veröffentlichung in einer Gesamtstruktur aktivieren, müssen Sie das Active Directory-Schema dieser Gesamtstruktur für Configuration Manager erweitern. Das Konto für die Active Directory-Gesamtstruktur muss Vollzugriff auf den Systemcontainer in dieser Gesamtstruktur besitzen.  

5.  Wenn Sie die Konfiguration dieser Gesamtstruktur zur Verwendung mit der Active Directory-Gesamtstrukturermittlung abgeschlossen haben, klicken Sie auf **OK** , um die Konfiguration zu speichern.  
