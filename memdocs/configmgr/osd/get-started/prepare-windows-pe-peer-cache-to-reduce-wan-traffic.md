---
title: Vorbereiten des Windows PE-Peercache zum Reduzieren des WAN-Datenverkehrs
titleSuffix: Configuration Manager
description: Der Windows PE-Peercache funktioniert in der Windows PE, von wo Inhalt von einem lokalen Peer abgerufen und WAN-Datenverkehr minimiert wird, wenn kein lokaler Verteilungspunkt vorhanden ist.
ms.date: 06/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 6c64f276-b88c-4b1e-8073-331876a03038
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fd622c1a54c1dd3cd3b5071cc62d1b6860a118e3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708778"
---
# <a name="prepare-windows-pe-peer-cache-to-reduce-wan-traffic-in-configuration-manager"></a>Vorbereiten des Windows PE-Peercache zum Reduzieren des WAN-Datenverkehrs in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Beim Bereitstellen eines neuen Betriebssystems in Configuration Manager können Computer, auf denen die Tasksequenz ausgeführt wird, Windows PE-Peercache verwenden, um Inhalte von einem lokalen Peer (einer Peercachequelle) abzurufen, anstatt sie von einem Verteilungspunkt herunterzuladen. Auf diese Weise können Sie WAN-Datenverkehr in Zweigstellenszenarios minimieren, wenn kein lokaler Verteilungspunkt vorhanden ist.  

 Windows PE-Peercache gleicht [Windows BranchCache](../../core/plan-design/configs/support-for-windows-features-and-networks.md#bkmk_branchcache), funktioniert jedoch in Windows Preinstallation Environment (Windows PE). Die folgenden Begriffe werden verwendet, um die Clients zu beschreiben, auf denen Windows PE-Peercache verwendet wird:  

-   Ein **Peercacheclient** ist ein Computer, der für die Verwendung von Windows PE-Peercache konfiguriert ist.  

-   Eine **Peercachequelle** ist ein Client, der für Peercache konfiguriert ist und anderen Peercacheclients, die Inhalt anfordern, diesen zur Verfügung stellt.  

In den folgenden Abschnitten erfahren Sie, wie Sie Peercache verwalten.

##  <a name="objects-stored-on-a-peer-cache-source"></a><a name="BKMK_PeerCacheObjects"></a> In einer Peercachequelle gespeicherte Objekte  
 Eine für die Verwendung von Windows PE-Peercache konfigurierte Tasksequenz kann die folgenden Inhaltsobjekte bei der Ausführung in Windows PE abrufen:  

- Betriebssystemabbild  

- Treiberpaket  

- Pakete und Programme (Wenn der Client die Tasksequenz weiterhin in der Vollversion des Betriebssystems ausführt, ruft der Client diese Inhalte aus einer Peercachequelle ab, sofern die Tasksequenz ursprünglich bei der Ausführung in Windows PE für Peercache konfiguriert wurde.)  

- Zusätzliche Startimages  

  Die folgenden Inhaltsobjekte werden nie unter Verwendung von Peercache übertragen. Stattdessen werden sie von einem Verteilungspunkt oder durch Windows BranchCache übertragen, sofern Windows BranchCache in Ihrer Umgebung konfiguriert wurde:  

- Applications  

- Softwareupdates  

##  <a name="how-does--windows-pe-peer-cache-work"></a><a name="BKMK_PeerCacheWork"></a> Funktionsweise von Windows PE-Peercache  
 Stellen sie sich ein Szenario mit einer Zweigstelle vor, die über keinen Verteilungspunkt, aber über mehrere Clients verfügt, die für die Verwendung von Windows PE-Peercache aktiviert sind. Sie stellen die Tasksequenz, die für die Verwendung von Peerchache konfiguriert ist, auf mehreren Clients bereit, die als Teil der Peercachequelle konfiguriert sind. Der erste Client, der die Tasksequenz ausführt, sendet eine Anforderung nach einem Peer mit dem Inhalt. Er findet keinen, daher erhält er den Inhalt von einem Verteilungspunkt über das WAN. Der Client installiert das neue Image und speichert den Inhalt dann in seinem Configuration Manager-Clientcache, sodass er anschließend als Peercachequelle für andere Clients fungieren kann. Wenn der nächste Client die Tasksequenz ausführt, sendet er eine Anforderung zur Suche nach einer Peercachequelle im Subnetz, und der erste Client antwortet und stellt den zwischengespeicherten Inhalt zur Verfügung.  

##  <a name="determine-what--clients-will-be-part-of-the-windows-pe-peer-cache-source"></a><a name="BKMK_PeerCacheDetermine"></a> Ermitteln der Clients, die Teil der Windows PE-Peercachequelle sein werden  
 Es müssen verschiedene Dinge berücksichtigt werden, um Sie bei der Ermittlung der Computer zu unterstützen, die als Windows PE-Peercachequelle ausgewählt werden:  

-   Die Windows PE-Peercachequelle sollte ein Desktopcomputer sein, der immer eingeschaltet und für Peercacheclients verfügbar ist.  

-   Der Windows PE-Peercache verfügt über einen ausreichend großen Clientcache, um die Images zu speichern.  

##  <a name="requirements-for-a-client-to-use-a--windows-pe-peer-cache-source"></a><a name="BKMK_PeerCacheRequirements"></a> Anforderungen für einen Client zur Verwendung einer Windows PE-Peercachequelle  
 Damit Clients eine Windows PE-Peercachequelle verwenden können, müssen die folgenden Anforderungen erfüllt werden:  

-   Der Configuration Manager-Client muss in der Lage sein, über die folgenden Ports in Ihrem Netzwerk zu kommunizieren:  

    -   Port für die erste Netzwerkübertragung, um eine Peercachequelle zu finden: Die Standardeinstellung hierfür ist UDP-Port 8004.  

    -   Port für Inhalte, die von einer Peercachequelle (HTTP und HTTPS) heruntergeladen werden: Die Standardeinstellung hierfür ist TCP-Port 8003.  
    
        Weitere Informationen finden Sie unter [Für Verbindungen verwendete Ports](../../core/plan-design/hierarchy/ports.md#BKMK_PortsClient-ClientWakeUp).  

        > [!TIP]  
        >  Die Clients werden HTTPS zum Herunterladen von Inhalten verwenden, wenn es verfügbar ist. Allerdings wird für HTTP oder HTTPS dieselbe Portnummer verwendet.  

-   [Konfigurieren des Clientcaches für Configuration Manager-Clients](../../core/clients/manage/manage-clients.md#BKMK_ClientCache) auf Clients, um sicherzustellen, dass ausreichend Speicherplatz für die bereitzustellenden Images verfügbar ist. Windows PE-Peercache wirkt sich nicht auf die Konfiguration oder das Verhalten des Clientcaches aus.  

-   Die Bereitstellungsoptionen für die Bereitstellung der Tasksequenz müssen als „Inhalt lokal herunterladen, wenn er von der Tasksequenz benötigt wird“ konfiguriert werden.  

##  <a name="configure-windows-pe-peer-cache"></a><a name="BKMK_PeerCacheConfigure"></a> Konfigurieren des Windows PE-Peercaches  
 Sie können die folgenden Methoden verwenden, um einem Client Peercacheinhalt bereitzustellen, damit dieser als Peercachequelle dienen kann:  

- Ein Peercacheclient, der keine Peercachequelle mit dem Inhalt finden kann, lädt den Inhalt von einem Verteilungspunkt herunter.  Wenn der Client Clienteinstellungen empfängt, die Peercache aktivieren, und die Tasksequenz so konfiguriert ist, dass zwischengespeicherter Inhalt erhalten bleibt, wird der Client zu einer Peercachequelle.  

- Ein Peercacheclient kann von einem anderen Peercacheclient (einer Peercachequelle) Inhalt abrufen.  Da der Client für Peercache konfiguriert wurde, wird er zu einer Peercachequelle, wenn er eine Tasksequenz ausführt, die so konfiguriert ist, dass zwischengespeicherter Inhalt erhalten bleibt.  

- Ein Client führt eine Tasksequenz aus, die den optionalen Schritt [Download Package Content](../understand/task-sequence-steps.md#BKMK_DownloadPackageContent)enthält, der verwendet wird, den relevanten Inhalt vorab bereitzustellen, der in der Windows PE-Peercache-Tasksequenz enthalten ist. Wenn Sie diese Methode verwenden:  

  -   Der Client muss das bereitgestellte Image nicht installieren.  

  -   Zusätzlich zur Option **Paketinhalt herunterladen** muss die Tasksequenz auch die Option **Configuration Manager-Clientcache** verwenden. Sie verwenden diese Option, um den Inhalt im Clientcache zu speichern, damit der Client als Peercachequelle für andere Peercacheclients fungieren kann.  

  Mit den folgenden Verfahren können Sie Windows PE-Peercache auf Clients und Tasksequenzen zur Unterstützung von Peercache konfigurieren.  

### <a name="to-configure-the-windows-pe-peer-cache-source-computers"></a>So konfigurieren Sie die Quellcomputer für Windows PE-Peercache  

1. Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Clienteinstellungen**, und erstellen Sie dann ein neues Objekt **Benutzerdefinierte Geräteclienteinstellungen**, oder bearbeiten Sie ein vorhandenes Einstellungsobjekt. Außerdem können Sie diese Konfiguration für das Objekt **Clientstandardeinstellungen** vornehmen.  

   > [!TIP]  
   >  Verwenden Sie ein "Benutzerdefinierte Einstellungen"-Objekt, um zu verwalten, welche Clients diese Konfiguration erhalten. Möglicherweise möchten Sie z. B. vermeiden, diese Konfiguration auf den Laptops von Benutzern vorzunehmen, die häufig unterwegs sind. Ein stark mobile genutztes System kann eine ungeeignete Quelle zum Bereitstellen von Inhalt für andere Peercacheclients sein.  
   >   
   >  Bedenken Sie außerdem, dass sich die Konfiguration auf alle Clients in Ihrer Umgebung auswirkt, wenn Sie diese Einstellung als Teil der **Clientstandardeinstellungen**konfigurieren.  

2. Legen Sie unter **Einstellungen für Clientcache** die Option **Configuration Manager-Client in vollständigem Betriebssystem zur Freigabe von Inhalten aktivieren** auf **Ja** fest.  

   -   Standardmäßig ist nur HTTP aktiviert. Wenn Sie Clients das Herunterladen von Inhalt über HTTPS ermöglichen möchten, legen Sie **HTTPS für Clientpeerkommunikation aktivieren** auf **Ja**fest.  

   -   Standardmäßig ist der Port für Broadcasts auf 8004 und der Port für den Download von Inhalten auf 8003 festgelegt. Sie können beide Werte ändern.  

3. Speichern Sie die Clienteinstellungen, und stellen Sie sie auf den Clients bereit, die Sie als Peercachequelle auswählen.  

   Nachdem ein Gerät mit diesem Einstellungsobjekt konfiguriert wurde, kann es als Peercachequelle fungieren. Diese Einstellungen sollten auf potenziellen Peercacheclients bereitgestellt werden, um die erforderlichen Ports und Protokolle zu konfigurieren.  

###  <a name="configure-a-task-sequence-for-windows-pe-peer-cache"></a><a name="BKMK_PeerCacheConfigureTS"></a> Konfigurieren einer Tasksequenz für Windows PE-Peercache  
 Verwenden Sie beim Konfigurieren der Tasksequenz die folgenden Tasksequenzvariablen als Sammlungsvariablen in der Sammlung, der die Tasksequenz bereitgestellt wird:  

- **SMSTSPeerDownload**  

   Wert:  TRUE  

   Ermöglicht dem Client die Verwendung von Windows PE-Peercache.  

- **SMSTSPeerRequestPort**  

   Wert: <Portnummer\>  

   Wenn Sie nicht den in den Clienteinstellungen konfigurierten Standardport (8004) verwenden, müssen Sie diese Variable mit einem benutzerdefinierten Wert für den Netzwerkport konfigurieren, der für die erste Übertragung verwendet werden soll.  

- **SMSTSPreserveContent**  

   Wert: TRUE  

   Dies kennzeichnet den Inhalt in der Tasksequenz, der im Configuration Manager-Clientcache nach der Bereitstellung erhalten bleiben soll. Dies ist anders als mit SMSTSPersisContent, bei dem der Inhalt nur für die Dauer der Tasksequenz behalten wird, und der den Tasksequenzcache verwendet und nicht die Configuration Manager-Clientcache.  

  Weitere Informationen finden Sie unter [Tasksequenzvariablen](../understand/task-sequence-variables.md).  

###  <a name="validate-the-success-of-using-windows-pe-peer-cache"></a><a name="BKMK_PeerCacheValidate"></a> Überprüfen, ob Windows PE-Peercache erfolgreich verwendet werden kann  
 Nach der Verwendung von Windows PE-Peercache zum Bereitstellen und Installieren einer Tasksequenz können Sie überprüfen, ob der Peercache im Prozess erfolgreich verwendet wurde, indem Sie **smsts.log** auf dem Client anzeigen, auf dem die Tasksequenz ausgeführt wurde.  

 Suchen Sie im Protokoll einen Eintrag ähnlich dem folgenden, in dem <*Quellservername*> den Computer identifiziert, von dem der Client den Inhalt erhalten hat. Dieser Computer sollte eine Peercachequelle und kein Verteilungspunktserver sein. Die weiteren Details variieren basierend auf Ihrer lokalen Umgebung und den Konfigurationen.  

-   *<![LOG[Datei heruntergeladen von http:// <Quellservername\>:8003/SCCM_BranchCache$/SS10000C/sccm?/install.wim auf C:\\_SMSTaskSequence\Packages\SS10000C\install.wim ]LOG]!><time="14:24:33.329+420" date="06-26-2015" component="ApplyOperatingSystem" context="" type="1" thread="1256" file="downloadcontent.cpp:1626">*  
