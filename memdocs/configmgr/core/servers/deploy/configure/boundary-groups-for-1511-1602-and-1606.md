---
title: Begrenzungsgruppen für 1511, 1602 und 1606
titleSuffix: Configuration Manager
description: Verwenden von Begrenzungsgruppen mit den Configuration Manager-Versionen 1511, 1602 und 1606.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: dec1e0d7-5864-43a8-9f56-413923b3914e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 09c1b0613d36cd135ff3ac71ac7ec8472ad1e8c4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704838"
---
# <a name="boundary-groups-for-configuration-manager-version-1511-1602-and-1606"></a>Begrenzungsgruppen für die Configuration Manager-Versionen 1511, 1602 und 1606

*Gilt für: Configuration Manager (Current Branch)*
<!-- This topic drops from TOC with the release of version 1706 -->

Die Informationen in diesem Thema betreffen die Verwendung von Begrenzungsgruppen mit den Versionen 1511, 1602 und 1606 von Configuration Manager.
Wenn Sie Version 1610 oder höher verwenden, finden Sie weitere Informationen zum Verwenden der überarbeiteten Begrenzungsgruppen unter [Configure boundary groups (Konfigurieren von Begrenzungsgruppen)](boundary-groups.md).  


##  <a name="boundary-groups"></a><a name="BKMK_BoundaryGroups"></a> Boundary groups  
 Sie erstellen Begrenzungsgruppen zum logischen Gruppieren zusammenhängender Netzwerkadressen (Grenzen), um die Verwaltung Ihrer Infrastruktur zu erleichtern. Sie müssen einer Begrenzungsgruppe zunächst Grenzen hinzufügen, damit Sie die Begrenzungsgruppe verwenden können. Clients verwenden die Konfiguration der Begrenzungsgruppe für folgende Zwecke:  

-   Automatische Standortzuweisung  

-   Inhaltsort  

-   Bevorzugte Verwaltungspunkte

    Wenn Sie bevorzugte Verwaltungspunkte verwenden möchten, müssen Sie diese Option für die Hierarchie und nicht in der Konfiguration der Begrenzungsgruppe aktivieren. Weitere Informationen finden Sie weiter unten in diesem Thema im Verfahren *So aktivieren Sie die Verwendung bevorzugter Verwaltungspunkte*.  

Wenn Sie Begrenzungsgruppen einrichten, fügen Sie der Begrenzungsgruppe eine oder mehrere Grenzen hinzu. Dann konfigurieren Sie zusätzliche Einstellungen zur Verwendung durch Clients, die sich in diesen Grenzen befinden.  

#### <a name="to-create-a-boundary-group"></a>So erstellen Sie eine Begrenzungsgruppe  

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** > **Hierarchiekonfiguration** >  **Begrenzungsgruppen**.  

2.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **Begrenzungsgruppe erstellen**.  

3.  Wählen Sie im Dialogfeld **Begrenzungsgruppe erstellen** die Registerkarte **Allgemein**, und geben Sie dann unter **Name** einen Namen für diese Begrenzungsgruppe ein.  

4.  Wählen Sie **OK**, um die neue Begrenzungsgruppe zu speichern.  

#### <a name="to-set-up-a-boundary-group"></a>So richten Sie eine Begrenzungsgruppe ein  

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** > **Hierarchiekonfiguration** >  **Begrenzungsgruppen**.  

2.  Wählen Sie die Begrenzungsgruppe aus, die Sie ändern möchten.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.  

4.  Wählen Sie im Dialogfeld **Eigenschaften** für die Begrenzungsgruppe die Registerkarte **Allgemein** aus, um die Grenzen zu ändern, die Mitglieder dieser Begrenzungsgruppe sind:  

    -   Wenn Sie Grenzen hinzufügen möchten, wählen Sie **Hinzufügen**, aktivieren Sie das Kontrollkästchen für mindestens eine Grenze, und wählen Sie dann **OK**.  

    -   Wenn Sie Grenzen entfernen möchten, wählen Sie die Grenze aus, und wählen Sie dann **Entfernen**.  

5.  Wählen Sie die Registerkarte **Referenzen**, um die Standortzuweisung und die zugeordnete Konfiguration des Standortsystemservers zu ändern:  

    -   Aktivieren Sie das Kontrollkästchen **Diese Begrenzungsgruppe für die Standortzuweisung verwenden**, und wählen Sie dann aus der Dropdownliste **Zugewiesener Standort** einen Standort aus, damit Clients diese Begrenzungsgruppe für die Standortzuweisung verwenden können.  

    -   So richten Sie die verfügbaren Standortsystemserver ein, die dieser Begrenzungsgruppe zugeordnet sind  

    1.  Wählen Sie **Hinzufügen**, und aktivieren Sie dann das Kontrollkästchen für mindestens einen Server. Die Server werden als zugeordnete Standortsystemserver für diese Begrenzungsgruppe hinzugefügt. Nur Server, auf denen die unterstützte Standortsystemrolle installiert ist, sind verfügbar.  

        > [!NOTE]  
        >  Sie können eine beliebige Kombination verfügbarer Standortsysteme von einem beliebigen Standort in der Hierarchie auswählen. Ausgewählte Standortsysteme werden in den Eigenschaften jeder Grenze, die dieser Begrenzungsgruppe angehört, auf der Registerkarte **Standortsysteme** aufgelistet.  

    2.  Wenn Sie einen Server aus dieser Begrenzungsgruppe entfernen möchten, wählen Sie den Server aus, und wählen Sie dann **Entfernen**.  

        > [!NOTE]  
        >  Wenn diese Begrenzungsgruppe nicht mehr zum Zuordnen von Standortsystemen verwendet werden soll, müssen Sie alle Server entfernen, die als zugeordnete Standortsystemserver aufgelistet sind.  

    3.  Wenn Sie die Netzwerkverbindungsgeschwindigkeit eines Standortsystemservers für diese Begrenzungsgruppe ändern möchten, wählen Sie den Server aus, und wählen Sie dann **Verbindung ändern**.  

         Die Standardeinstellung für die Verbindungsgeschwindigkeit lautet für alle Standortsysteme **Schnell**, sie kann aber auch in **Langsam** geändert werden. Über die Netzwerkverbindungsgeschwindigkeit und die Konfiguration einer Bereitstellung wird festgelegt, ob ein Client Inhalte vom Server herunterladen kann.  

6.  Wählen Sie **OK**, um die Eigenschaften der Begrenzungsgruppe zu schließen und die Konfiguration zu speichern.  

#### <a name="to-associate-a-content-deployment-server-or-management-point-with-a-boundary-group"></a>So ordnen Sie einen Inhaltsbereitstellungsserver oder Verwaltungspunkt einer Begrenzungsgruppe zu  

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** > **Hierarchiekonfiguration** >  **Begrenzungsgruppen**.  

2.  Wählen Sie die Begrenzungsgruppe aus, die Sie ändern möchten.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.  

4.  Wählen Sie im Dialogfeld **Eigenschaften** für die Begrenzungsgruppe die Registerkarte **Referenzen**.  

5.  Wählen Sie unter **Standortsystemserver auswählen** die Option **Hinzufügen**, aktivieren Sie das Kontrollkästchen für die Standortsystemserver, die dieser Begrenzungsgruppe zugeordnet werden sollen, und wählen Sie dann **OK**.  

6.  Wählen Sie **OK**, um das Dialogfeld zu schließen und die Konfiguration der Begrenzungsgruppe zu speichern.  

#### <a name="to-enable-use-of-preferred-management-points"></a>So aktivieren Sie die Verwendung bevorzugter Verwaltungspunkte  

1.  Wählen Sie in der Configuration Manager-Konsole **Verwaltung** > **Standortkonfiguration** > **Standorte**, und wählen Sie anschließend **Hierarchieeinstellungen** auf der Registerkarte **Start**.  

2.  Wählen Sie im Dialogfeld **Hierarchieeinstellungen** auf der Registerkarte **Allgemein** die Option **Clients bevorzugen die in Begrenzungsgruppen angegebenen Verwaltungspunkte**.  

3.  Wählen Sie **OK**, um das Dialogfeld zu schließen und die Konfiguration zu speichern.  

#### <a name="to-set-up-a-fallback-site-for-automatic-site-assignment"></a>So richten Sie einen Fallbackstandort für die automatische Standortzuweisung ein  

1. Wählen Sie in der Configuration Manager-Konsole **Verwaltung** > **Standortkonfiguration** >  **Standorte** aus.  

2. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Standorte** auf **Hierarchieeinstellungen**.  

3. Aktivieren Sie auf der Registerkarte **Allgemein** das Kontrollkästchen **Fallbackstandort verwenden**, und wählen Sie dann in der Dropdownliste **Fallbackstandort** einen Standort aus.  

4. Wählen Sie **OK**, um die Konfiguration zu speichern.  

   In den folgenden Abschnitten finden Sie zusätzliche Informationen zu Konfigurationen von Begrenzungsgruppen.  

###  <a name="about-site-assignment"></a><a name="BKMK_BoundarySiteAssignment"></a> Informationen zur Standortzuweisung  
 Sie können jede Begrenzungsgruppe mit einem zugewiesenen Standort für Clients einrichten.  

-   Ein neu installierter Client, der die automatische Standortzuweisung verwendet, tritt dem zugewiesenen Standort einer Begrenzungsgruppe bei, die die aktuelle Netzwerkadresse des Clients enthält.  

-   Bei einem Client, der einem Standort zugewiesen ist, ändert sich die Standortzuweisung nicht, wenn sich seine Netzwerkadresse ändert. Beim Wechseln des Clients zu einer neuen Netzwerkadresse, die von einer Grenze in einer Begrenzungsgruppe mit abweichender Standortzuweisung repräsentiert wird, bleibt der dem Client zugewiesene Standort unverändert.  

-   Wenn mithilfe von Active Directory-Systemermittlung eine neue Ressource ermittelt wird, werden die Netzwerkinformationen für diese Ressource anhand der Grenzen in Begrenzungsgruppen bewertet. Dabei wird die neue Ressource einem zugewiesenen Standort zur Verwendung bei einer Clientpushinstallation zugeordnet.  

-   Wenn eine Grenze zu mehreren Begrenzungsgruppen gehört, denen verschiedene Standorte zugewiesen sind, wählen die Clients einen dieser Standorte nach dem Zufallsprinzip aus.  

-   Änderungen an dem zugewiesenen Standort einer Begrenzungsgruppe betreffen nur neue Standortzuweisungsaktionen. Clients, die bereits einem Standort zugewiesen waren, bewerten ihre Standortzuweisung nicht basierend auf Änderungen an der Konfiguration einer Begrenzungsgruppe (oder ihrer eigenen Netzwerkadresse) neu.  

Weitere Informationen zur automatischen Standortzuweisung finden Sie unter [Zuweisen von Clients zu einem Standort](../../../../core/clients/deploy/assign-clients-to-a-site.md) im Abschnitt [Verwenden der automatischen Standortzuweisung für Computer](../../../../core/clients/deploy/assign-clients-to-a-site.md#BKMK_AutomaticAssignment).  

###  <a name="about-content-location"></a><a name="BKMK_BoundaryContentLocation"></a> Informationen zu Inhaltsorten  
 Sie können jede Begrenzungsgruppe mit einem oder mehreren Verteilungspunkten und Zustandsmigrationspunkten einrichten. Ferner können Sie dieselben Verteilungspunkte und Zustandsmigrationspunkte mehreren Begrenzungsgruppen zuordnen.  

-   **Während der Softwareverteilung**fordern Clients einen Speicherort für Bereitstellungsinhalte an. Configuration Manager sendet dem Client eine Liste der Verteilungspunkte, die den einzelnen Begrenzungsgruppen zugeordnet sind, die den aktuellen Netzwerkort des Clients einbeziehen.  

-   **Während der Bereitstellung des Betriebssystems** fordern Clients einen Speicherort zum Senden oder Empfangen ihrer Zustandsmigrationsinformationen an. Configuration Manager sendet dem Client eine Liste der Zustandsmigrationspunkte, die den einzelnen Begrenzungsgruppen zugeordnet sind, die den aktuellen Netzwerkort des Clients einbeziehen.  

So kann von den Clients der am nächsten liegende Server zur Übertragung der Inhalts- oder Zustandsmigrationsinformationen ausgewählt werden.  

###  <a name="about-preferred-management-points"></a><a name="BKMK_PreferredMP"></a> Informationen zu bevorzugten Verwaltungspunkten  
 Bevorzugte Verwaltungspunkte ermöglichen einem Client die Identifikation eines Verwaltungspunkts, der seiner aktuellen Netzwerkadresse (oder Begrenzung) zugeordnet ist.  

-   Ein Client versucht zunächst, einen bevorzugten Verwaltungspunkt seines zugewiesenen Standorts zu verwenden, bevor er einen Verwaltungspunkt seines zugewiesenen Standorts verwendet, der nicht als bevorzugt eingerichtet wurde.  

-   Um diese Option verwenden zu können, müssen Sie sie für die Hierarchie aktivieren. Außerdem müssen Sie Begrenzungsgruppen an den einzelnen primären Standorten so einrichten, dass sie die Verwaltungspunkte enthalten, die den Grenzen dieser Begrenzungsgruppe zugeordnet sein sollen.  

-   Wenn bevorzugte Verwaltungspunkte eingerichtet werden und ein Client seine Liste der Verwaltungspunkte organisiert, platziert er die bevorzugten Verwaltungspunkte ganz oben in der Liste der zugewiesenen Verwaltungspunkte, die alle Verwaltungspunkte des zugewiesenen Standorts des Clients enthält.  

> [!NOTE]  
>  Wenn ein Client seinen Standort wechselt (wenn beispielsweise ein Laptop an einen Remotestandort wechselt und seine Netzwerkadresse ändert), kann er an seinem neuen Standort einen Verwaltungspunkt (bzw. Proxyverwaltungspunkt) des lokalen Standorts verwenden, bevor er versucht, einen Verwaltungspunkt seines zugewiesenen Standorts zu verwenden (was die bevorzugten Verwaltungspunkte einschließt).  Weitere Informationen finden Sie unter [Understand how clients find site resources and services for System Center Configuration Manager (Verstehen, wie Clients Standortressourcen und -dienste für Configuration Manager suchen)](../../../../core/plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md).  

###  <a name="about-overlapping-boundaries"></a><a name="BKMK_BoundaryOverlap"></a> Informationen zu überlappenden Grenzen  
 Bei der Abfrage von Inhaltsorten werden überlappende Grenzkonfigurationen von Configuration Manager unterstützt:  

-   **Wenn ein Client Inhalt anfordert**und die Netzwerkadresse des Clients zu mehreren Begrenzungsgruppen gehört, erhält der Client von Configuration Manager eine Liste mit allen Verteilungspunkten, die über diesen Inhalt verfügen.  

-   **Wenn von einem Client Zustandsmigrationsinformationen bei einem Server angefordert bzw. an diesen gesendet werden**und das Netzwerk des Clients Mitglied mehrerer Begrenzungsgruppen ist, erhält der Client von Configuration Manager eine Liste mit allen Zustandsmigrationspunkten, die einer Begrenzungsgruppe mit der aktuellen Netzwerkadresse des Clients zugeordnet sind.  

So kann von den Clients der am nächsten liegende Server zur Übertragung der Inhalts- oder Zustandsmigrationsinformationen ausgewählt werden.  

###  <a name="about-network-connection-speed"></a><a name="BKMK_BoudnaryNetworkSpeed"></a> Informationen zur Netzwerkverbindungsgeschwindigkeit  
 Sie können die Netzwerkverbindungsgeschwindigkeit für jeden Standortsystemserver in einer Begrenzungsgruppe festlegen. Diese Einstellung gilt für Clients, die sich basierend auf der Konfiguration dieser Begrenzungsgruppe mit einem Standortsystem verbinden. Der gleiche Standortsystemserver kann in verschiedenen Begrenzungsgruppen unterschiedliche Verbindungsgeschwindigkeiten aufweisen.  

 Standardmäßig wird die Netzwerkverbindungsgeschwindigkeit auf **Schnell** festgelegt, aber Sie können sie in **Langsam** ändern. Anhand der Netzwerkverbindungsgeschwindigkeit und der Bereitstellungskonfiguration wird geprüft, ob Inhalt von einem Verteilungspunkt heruntergeladen werden kann, wenn der Client in einer zugeordneten Begrenzungsgruppe enthalten ist.  

 Weitere Informationen zum Einfluss der Netzwerkverbindungsgeschwindigkeit auf den Inhaltsabruf durch Clients finden Sie unter [Quellspeicherortszenarios für Inhalte](../../../../core/plan-design/hierarchy/content-source-location-scenarios.md).  
