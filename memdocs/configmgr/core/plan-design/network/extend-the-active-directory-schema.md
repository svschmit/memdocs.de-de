---
title: Veröffentlichung und das Active Directory-Schema
titleSuffix: Configuration Manager
description: Das Erweitern des Active Directory-Schemas für Configuration Manager vereinfacht das Bereitstellen und Konfigurieren von Clients.
ms.date: 09/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc15ee7e-4d0a-4463-ae2c-f72d8d45d65d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 3595273d55bf01158691fb46587ac264af16bffa
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701548"
---
# <a name="prepare-active-directory-for-site-publishing"></a>Vorbereiten von Active Directory für die Veröffentlichung eines Standorts

*Gilt für: Configuration Manager (Current Branch)*

Beim Erweitern des Active Directory-Schemas für Configuration Manager führen Sie neue Strukturen in Active Directory ein, die von Configuration Manager-Standorten zum Veröffentlichen wichtiger Informationen an einem sicheren Speicherort genutzt werden, wo Clients einfach auf sie zugreifen können.  

Zur Verwaltung lokaler Clients empfiehlt sich der Einsatz von Configuration Manager mit einem erweiterten Active Directory-Schema. Ein erweitertes Schema kann den Vorgang zum Bereitstellen und Einrichten von Clients vereinfachen. Durch ein erweitertes Schema können Clients außerdem Ressourcen wie Inhaltsserver und zusätzliche Dienste effizient lokalisieren, die von den verschiedenen Configuration Manager-Standortsystemrollen bereitgestellt werden.  

-   Wenn Sie nicht mit den Vorteilen eines erweiterten Schemas für eine Configuration Manager-Bereitstellung vertraut sind, kann der Artikel [Schemaerweiterungen für Configuration Manager](../../../core/plan-design/network/schema-extensions.md) Sie bei der Entscheidung unterstützen.  

-   Wenn Sie kein erweitertes Schema verwenden, können Sie andere Methoden wie z.B. DNS und WINS einrichten, um Dienste und Standortsystemserver zu identifizieren. Diese Methoden der Dienstidentifizierung erfordern zusätzliche Konfigurationen und stellen nicht die bevorzugte Methode für die Dienstidentifizierung durch Clients dar. Weitere Informationen finden Sie unter [Understand how clients find site resources and services for Configuration Manager (Informationen dazu, wie Clients Standortressourcen und -dienste für Configuration Manager suchen)](../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

-   Wenn Ihr Active Directory-Schema für Configuration Manager 2007 oder System Center 2012 Configuration Manager erweitert wurde, müssen Sie keine weiteren Schritte durchführen. Die Schemaerweiterungen sind unverändert und bereits vorhanden.  

Das Erweitern des Schemas für jede Gesamtstruktur ist eine einmalige Aktion. Führen Sie die folgenden Schritte aus, um das Active Directory-Schema zu erweitern und dann zu verwenden:  

## <a name="step-1-extend-the-schema"></a>Schritt 1: Erweitern des Schemas  
So erweitern Sie das Schema für Configuration Manager  

-   Verwenden Sie ein Konto, das Mitglied der Sicherheitsgruppe „Schema-Admins“ ist.  

-   Sie müssen am Schemamaster-Domänencontroller angemeldet sein.  

-   Führen Sie das Tool **Extadsch.exe** aus, oder verwenden Sie das Befehlszeilenprogramm LDIFDE mit der Datei **ConfigMgr_ad_schema.ldf** . Das Tool und die Datei befinden sich beide auf dem Configuration Manager-Installationsmedium im Ordner **SMSSETUP\BIN\X64**.  

#### <a name="option-a-use-extadschexe"></a>Option A: Verwenden Sie „extadsch.exe“.  

1.  Führen Sie **extadsch.exe** zum Hinzufügen der neuen Klassen und Attribute zum Active Directory-Schema aus.  

    > [!TIP]  
    >  Führen Sie dieses Tool über die Befehlszeile aus, um während der Ausführung Feedback anzuzeigen.  

2.  Überprüfen Sie in der Datei „extadsch.log“ im Stammverzeichnis des Systemlaufwerks, ob die Schemaerweiterung erfolgreich war.  

#### <a name="option-b-use-the-ldif-file"></a>Option B: Verwenden Sie die LDIF-Datei.  

1.  Bearbeiten Sie die Datei **ConfigMgr_ad_schema.ldf** zum Definieren der Active Directory-Stammdomäne, die Sie erweitern möchten:  

    -   Ersetzen Sie alle Vorkommen des Texts **DC=x** in der Datei durch den vollständigen Namen der zu erweiternden Domäne.  

    -   Beispiel: Lautet der vollständige Name der zu erweiternden Domäne „widgets.microsoft.com“, ändern Sie in der Datei jedes Vorkommen von „DC=x“ in **DC=widgets, DC=microsoft, DC=com**.  

2.  Importieren Sie den Inhalt der Datei **ConfigMgr_ad_schema.ldf** mithilfe des Befehlszeilenprogramms LDIFDE in Active Directory Domain Services:  

    -   Durch die folgende Befehlszeile werden z.B. die Schemaerweiterungen in Active Directory Domain Services importiert, die ausführliche Protokollierung aktiviert und eine Protokolldatei während des Importvorgangs erstellt: **ldifde -i -f ConfigMgr_ad_schema.ldf -v -j &lt;Speicherort der Protokolldatei\>** .  

3.  Um zu prüfen, ob die Schemaerweiterung erfolgreich war, untersuchen Sie die Protokolldatei, die mithilfe der Befehlszeile aus dem vorherigen Schritt erstellt wurde.  

## <a name="step-2--create-the-system-management-container-and-grant-sites-permissions-to-the-container"></a>Schritt 2:  Erstellen des System Management-Containers und Gewähren von Standortberechtigungen für den Container  
 Nach dem Erweitern des Schemas müssen Sie in Active Directory Domain Services (AD DS) einen Container **Systemverwaltung** erstellen:  

-   Sie erstellen diesen Containers einmal in jeder Domäne, die über einen primären oder sekundären Standort verfügt, der Daten in Active Directory veröffentlicht.  

-   Jedem Container erteilen Sie Berechtigungen für das Computerkonto jedes primären und sekundären Standortservers, der Daten in dieser Domäne veröffentlicht. Jedes Konto benötigt **Vollzugriff** auf den Container mit der erweiterten Berechtigung **Anwenden auf**, die auf **Dieses und alle untergeordneten Objekte** festgelegt sein muss.  

#### <a name="to-add-the-container"></a>So fügen Sie den Container hinzu  

1.  Verwenden Sie ein Konto, das im Container **System** in den Active Directory-Domänendiensten über die Berechtigung **Alle untergeordneten Objekte erstellen** verfügt.  

2.  Führen Sie **ADSI Bearbeiten** (adsiedit.msc) aus, und stellen Sie eine Verbindung mit der Domäne des Standortservers her.  

3.  Erstellen des Containers:  

    -   Erweitern Sie **Domain** &lt;vollständig qualifizierter Domänenname des Computers\>, erweitern Sie &lt;Distinguished Name\>, klicken Sie mit der rechten Maustaste auf **CN=System**, wählen Sie **Neu**, und wählen Sie dann **Objekt** aus.  

    -   Wählen Sie im Dialogfeld **Objekt erstellen** die Option **Container**, und wählen Sie **Weiter**.  

    -   Geben Sie in das Feld **Wert** die Zeichenfolge **System Management** ein, und wählen Sie dann **Weiter**.  

4.  Zuweisen von Berechtigungen:  

    > [!NOTE]  
    >  Nach Wunsch können Sie mit anderen Tools wie „Active Directory-Benutzer und -Computer“ (dsa.msc) dem System Management-Container Berechtigungen hinzufügen.  

    -   Klicken Sie mit der rechten Maustaste auf **CN=System Management**, und wählen Sie dann **Eigenschaften**.  

    -   Wählen Sie die Registerkarte **Sicherheit**, wählen Sie **Hinzufügen**, und fügen Sie anschließend das Computerkonto des Standortservers mit der Berechtigung **Vollzugriff** hinzu.  

    -   Wählen Sie **Erweitert**, wählen Sie das Computerkonto des Standortservers, und wählen Sie dann **Bearbeiten**.  

    -   Wählen Sie in der Liste **Anwenden auf** den Eintrag **Dieses und alle untergeordneten Objekte** aus.  

5.  Wählen Sie **OK**, um die Konsole zu schließen und die Konfiguration zu speichern.  

## <a name="step-3-set-up-sites-to-publish-to-active-directory-domain-services"></a>Schritt 3. Einrichten von Standorten zur Veröffentlichung in Active Directory Domain Services  
 Nachdem der Container eingerichtet wurde, Berechtigungen gewährt wurden und Sie einen primären Configuration Manager-Standort installiert haben, können Sie diesen Standort für das Veröffentlichen von Daten in Active Directory einrichten.  

 Informationen zum Veröffentlichen finden Sie unter [Veröffentlichen von Standortdaten für Configuration Manager](../../../core/servers/deploy/configure/publish-site-data.md).  
