---
title: Technical Preview 1803
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über neue Features, die mit der Technical Preview-Version 1803 für System Center Configuration Manager zur Verfügung stehen.
ms.date: 03/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 56dc4b07-5aa4-43e2-9be8-d26ae5ff5613
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: bb8224df3ccbb086ca0c83d08f29522cf3289c32
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701948"
---
# <a name="capabilities-in-technical-preview-1803-for-configuration-manager"></a>Funktionen in der Technical Preview 1803 für Configuration Manager

*Gilt für: Configuration Manager (Technical Preview-Branch)*

In diesem Artikel werden die Features vorgestellt, die in der Technical Preview-Version 1803 für System Center Configuration Manager verfügbar sind. Sie können diese Version installieren, um Funktionen für Ihren Technical Preview-Standort zu aktualisieren oder neue Funktionen hinzuzufügen. 

Lesen Sie den [Technical Preview](technical-preview.md)-Artikel vor der Installation dieses Updates. In diesem Artikel erhalten Sie Informationen zu den allgemeinen Anforderungen und Einschränkungen, die für die Verwendung der Technical Preview gelten. Außerdem erfahren Sie, wie Sie Updates zwischen den Versionen ausführen und Feedback übermitteln.     


<!--  Known Issues Template   
## Known Issues in this Technical Preview:
-   **Issue Name**. Details
    Workaround details.
-->


</br>

**Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  



 
## <a name="pull-distribution-points-support-cloud-distribution-points-as-source"></a>Pullverteilungspunkte unterstützen Cloudverteilungspunkte als Quelle  
<!--1321554-->
Viele Kunden verwenden in Remotebüros oder Filialen [Pullverteilungspunkte](../plan-design/hierarchy/use-a-pull-distribution-point.md), die Inhalte über das WAN von einem Quellverteilungspunkt herunterladen. Wenn Ihre Remotebüros über eine bessere Internetverbindung verfügen oder die Belastung Ihrer WAN-Verbindungen reduziert werden soll, können Sie in Microsoft Azure einen [Cloudverteilungspunkt](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md) als Quelle verwenden. Wenn Sie auf der Registerkarte **Pullverteilungspunkt** der Verteilungspunkteigenschaften eine Quelle hinzufügen, werden anschließend alle Cloudverteilungspunkte am Standort als verfügbare Verteilungspunkte aufgeführt. Ansonsten ändert sich das Verhalten der beiden Standortsystemrollen nicht. 

### <a name="prerequisites"></a>Voraussetzungen
- Der Pullverteilungspunkt benötigt für die Kommunikation mit Microsoft Azure Zugriff auf das Internet.
- Der Inhalt muss an den Quell-Cloudverteilungspunkt verteilt werden.

> [!Note]  
> Für dieses Feature fallen im Rahmen Ihres Azure-Abonnements keine Kosten für die Datenspeicherung oder ausgehenden Netzwerkdatenverkehr an. Weitere Informationen finden Sie im Abschnitt „Kosten einer cloudbasierten Verteilung“ unter [Verwenden eines cloudbasierten Verteilungspunkts mit System Center Configuration Manager](../plan-design/hierarchy/use-a-cloud-based-distribution-point.md#bkmk_cost).



## <a name="partial-download-support-in-client-peer-cache-to-reduce-wan-utilization"></a>Unterstützung von Teildownloads im Clientpeercache zum Reduzieren der WAN-Auslastung
<!--1357346-->
Clientpeercache-Quellen können Inhalte jetzt in mehrere Teile untergliedern. Diese Teile minimieren die Netzwerkdatenübertragung, um die WAN-Auslastung zu reduzieren. Der Verwaltungspunkt erlaubt eine genauere Nachverfolgung der Inhaltsteile. Er versucht, mehrere Downloads desselben Inhalts pro Begrenzungsgruppe zu vermeiden. 

### <a name="example-scenario"></a>Beispielszenario
Contoso hat einen einzigen primären Standort mit zwei Begrenzungsgruppen: Hauptsitz (HQ) und Filiale. Zwischen den Begrenzungsgruppen besteht eine Fallbackbeziehung mit einer Fallbackzeit von 30 Minuten. Der Verwaltungs- und Verteilungspunkt für den Standort befindet sich nur innerhalb der HQ-Grenze. Der Filialstandort hat keinen lokalen Verteilungspunkt. Zwei der vier Clients in der Filiale sind als Peercachequellen konfiguriert. 

![Diagramm der Netzwerkkonfiguration für das beschriebene Beispielszenario](media/1357346-peer-cache-source-parts.png)

1. Sie beabsichtigen eine Bereitstellung mit Inhalt für alle vier Clients in der Filiale. Sie haben den Inhalt nur an den Verteilungspunkt verteilt.
2. Client3 und Client4 haben keine lokale Quelle für die Bereitstellung. Der Verwaltungspunkt weist die Clients an, bis zu einem Fallback auf die Remotebegrenzungsgruppe 30 Minuten zu warten.
3. Client1 (PCS1) ist die erste Peercachequelle, die die Richtlinie mit dem Verwaltungspunkt aktualisiert. Da dieser Client als Peercachequelle aktiviert ist, weist der Verwaltungspunkt ihn an, unverzüglich mit dem Herunterladen von Teil A vom Verteilungspunkt zu beginnen.  
4. Wenn Client2 (PCS2) den Verwaltungspunkt kontaktiert, während Teil A bereits heruntergeladen wird, aber noch nicht abgeschlossen ist, weist der Verwaltungspunkt ihn an, unverzüglich mit dem Herunterladen von Teil B vom Verteilungspunkt zu beginnen.
5. PCS1 beendet das Herunterladen von Teil A und benachrichtigt unverzüglich den Verwaltungspunkt. Da Teil B bereits heruntergeladen wird, aber noch nicht abgeschlossen ist, weist der Verwaltungspunkt ihn an, unverzüglich mit dem Herunterladen von Teil C vom Verteilungspunkt zu beginnen.
6. PCS2 beendet das Herunterladen von Teil B und benachrichtigt unverzüglich den Verwaltungspunkt. Der Verwaltungspunkt weist ihn an, mit dem Herunterladen von Teil D vom Verteilungspunkt zu beginnen. 
7. PCS1 beendet das Herunterladen von Teil C und benachrichtigt unverzüglich den Verwaltungspunkt. Der Verwaltungspunkt teilt mit, dass keine weiteren Teile vom Remoteverteilungspunkt verfügbar sind. Der Verwaltungspunkt weist ihn an, Teil B von seinem lokalen Peer, PCS2, herunterzuladen.
8. Dieser Prozess wird so lange fortgesetzt, bis beide Client-Peercachequellen gegenseitig alle Teile heruntergeladen haben. Der Verwaltungspunkt priorisiert Teile vom Remoteverteilungspunkt, bevor er die Peercachequellen anweist, Teile von lokalen Peers herunterzuladen. 
9. Client3 ist der erste Client, der die Richtlinie aktualisiert, nachdem die Fallbackzeit von 30 Minuten abgelaufen ist. Er meldet sich erneut beim Verwaltungspunkt, der den Client über neue lokale Quellen informiert. Anstatt den Inhalt vollständig vom Verteilungspunkt über das WAN herunterzuladen, lädt er den Inhalt vollständig von einer der Client-Peercachequellen herunter. Clients priorisieren lokale Peerquellen. 

> [!Note]  
> Wenn die Anzahl der Client-Peercachequellen größer ist als die Anzahl der Inhaltsteile, weist der Verwaltungspunkt die weiteren Peercachequellen an, wie ein normaler Client auf einen Fallback zu warten. 


### <a name="try-it-out"></a>Probieren Sie es aus!
 Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie dann über die Registerkarte **Start** im Menüband **Feedback** zu den Funktionen.

1. Richten Sie wie gewohnt [Begrenzungsgruppen](../servers/deploy/configure/boundary-groups.md) und [Peercachequellen](../plan-design/hierarchy/client-peer-cache.md) ein.
2. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie **Standorte** aus. Klicken Sie im Menüband auf **Hierarchieeinstellungen**. 
3. Aktivieren Sie auf der Registerkarte **Allgemein** die Option **Configure client peer cache sources to divide content into parts** (Client-Peercachequellen so konfigurieren, dass Inhalt in Teile untergliedert wird). 
4. Erstellen Sie eine erforderliche Bereitstellung mit Inhalt.  

   > [!Note]  
   > Diese Funktion ist nur verfügbar, wenn der Client Inhalt im Hintergrund herunterlädt, wie bei einer erforderlichen Bereitstellung. Bedarfsgesteuerte Downloads, z.B. wenn der Benutzer eine verfügbare Bereitstellung im Softwarecenter installiert, verhalten sich wie gewohnt.  

1. Um zu sehen, wie das Herunterladen von Inhalten in Teilen abgewickelt wird, prüfen Sie das Protokoll **ContentTransferManager.log** auf der Client-Peercachequelle und das Protokoll **MP_Location.log** auf dem Verwaltungspunkt.  
 



## <a name="maintenance-windows-in-software-center"></a>Wartungsfenster im Softwarecenter
<!--1358131-->
Das Softwarecenter zeigt jetzt das nächste geplante Wartungsfenster an. Wechseln Sie auf der Registerkarte „Installationsstatus“ von „Alle“ zu „Bevorstehend“. Nun werden der Zeitraum und die Liste der geplanten Bereitstellungen angezeigt. Die Liste ist leer, wenn es keine kommenden Wartungsfenster gibt. 

![Liste der künftigen Bereitstellungen auf der Registerkarte „Installationsstatus“ von Softwarecenter](media/1358131-software-center-maintenance-windows.png)


## <a name="custom-tab-for-webpage-in-software-center"></a>Registerkarte „Benutzerdefiniert“ für Webseite im Softwarecenter
<!--1358132-->
Sie können nun eine benutzerdefinierte Registerkarte erstellen, um eine Webseite in Softwarecenter zu öffnen. Mit diesem Feature können Sie Ihren Endbenutzern Inhalte auf eine konsistente und zuverlässige Weise anzeigen. Die folgende Liste enthält einige Beispiele:
- IT kontaktieren: Informationen, wie die IT-Abteilung Ihrer Organisation kontaktiert werden kann
- IT-Supportcenter: IT-Self-Service-Aktionen wie das Durchsuchen einer Wissensdatenbank oder das Öffnen eines Supporttickets.
- Endbenutzerdokumentation: Artikel für Benutzer in Ihrer Organisation zu verschiedenen IT-Themen wie beispielsweise die Verwendung von Anwendungen oder die Aufrüstung auf Windows 10.


### <a name="try-it-out"></a>Probieren Sie es aus!
 Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie dann über die Registerkarte **Start** im Menüband **Feedback** zu den Funktionen.

1. Öffnen Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** im Knoten **Clienteinstellungen** die Richtlinie **Clientstandardeinstellungen**.
2. Wählen Sie die Gruppe **Softwarecenter** aus.
3. Klicken Sie unter **Software Center settings** (Softwarecenter-Einstellungen) auf **Anpassen**.
4. Wechseln Sie zur Registerkarte **Registerkarten**.
5. Aktivieren Sie die Option **Specify a custom tab for Software Center** (Benutzerdefinierte Registerkarte für Softwarecenter angeben).
    1. Geben Sie einen Namen in das Textfeld **Registerkartenname** ein. Dieser Name wird dem Benutzer im Softwarecenter angezeigt.
    2. Geben Sie eine gültige URL in das Textfeld **Inhalts-URL** ein. Diese URL bezieht sich auf den Inhalt, der in Softwarecenter angezeigt wird, wenn Benutzer auf diese Registerkarte klicken.

> [!Tip]  
> Softwarecenter verwendet Internet Explorer-Komponenten für das Rendern der Webseite.

## <a name="enable-third-party-software-update-support-on-clients"></a>Aktualisierungsunterstützung für Drittanbietersoftware auf Clients aktivieren

Sie können nun die Konfiguration von Konfigurations-Manager-Clients für Drittanbietersoftwareupdates aktivieren. Wenn Sie die Option **Enable third party software updates** (Drittanbietersoftwareupdates aktivieren) für die SUP-Komponenteneigenschaften auswählen, lädt der SUP das Signaturzertifikat herunter, das von WSUS für Updates von Drittanbietern verwendet wird. <!--1357605-->

Das Aktivieren von **Enable third party software updates** (Drittanbietersoftwareupdates aktivieren) in den Clienteinstellungen bewirkt Folgendes: 
- Auf dem Client wird die Richtlinie für das Zulassen signierter Updates für einen Intranetspeicherort für den Microsoft-Updatedienst festgelegt. 
- Das Signaturzertifikat des Speichers für vertrauenswürdige Herausgeber wird auf dem Client installiert. 

### <a name="try-it-out"></a>Probieren Sie es aus!
 Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie dann über die Registerkarte **Start** im Menüband **Feedback** zu den Funktionen.

1. Wechseln Sie auf dem obersten Standort in der Configuration Manager-Hierarchie zum Knoten **Verwaltung**, erweitern Sie **Standortkonfiguration**, und klicken Sie dann auf **Standorte**.
2. Klicken Sie mit der rechten Maustaste auf den obersten Standortserver, und wählen Sie **Standortkomponenten konfigurieren** und danach **Softwareupdatepunkt** aus.
3. Klicken Sie auf die Registerkarte **Third Party Updates** (Drittanbieterupdates), und aktivieren Sie **Enable third party software updates** (Drittanbietersoftwareupdates aktivieren).
4. Öffnen Sie **Clienteinstellungen**, und rufen Sie die Einstellungen für **Softwareupdates** auf.
5. Vergewissern Sie sich, dass **Enable third party software updates** (Drittanbietersoftwareupdates aktivieren) auf **Ja** gesetzt ist.

## <a name="enable-copypaste-of-asset-details-from-monitoring-views"></a>Aktivieren von Kopier- und Einfügevorgängen von Bestandsdetails von Überwachungsansichten
Dank Ihres [Benutzerfeedbacks](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/20234866-allow-us-to-copy-information-out-of-the-asset-det) können Sie nun die Funktion „Kopieren/Einfügen“ im Bereich „Bestandsdetails“ in den Statusüberwachungsansichten für die Bereitstellung und Verteilung aktivieren.  <!--1357552-->

## <a name="scap-extensions"></a>SCAP-Erweiterungen
Die Vorabversion von SCAP-Erweiterungen ist im Ordner „Cd.latest“ unter SMSSETUP\TOOLS\ConfigMgrSCAPExtension\ConfigMgrExtensionsForSCAP.msi verfügbar. Diese Vorabversion der SCAP-Erweiterungen kann unter allen derzeit unterstützten Versionen von Configuration Manager Current Branch und LTSB 1606 installiert werden.



## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zur Installation oder dem Update der Technical Preview finden Sie unter [Technical Preview für Configuration Manager](technical-preview.md).    
