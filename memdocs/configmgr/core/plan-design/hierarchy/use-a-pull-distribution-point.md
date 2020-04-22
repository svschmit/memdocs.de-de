---
title: Pullverteilungspunkt
titleSuffix: Configuration Manager
description: Erfahren Sie, welche Konfigurationen und Einschränkungen zur Verwendung eines Pullverteilungspunkts mit Configuration Manager vorhanden sind.
ms.date: 05/06/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7d8f530b-1a39-4a9d-a2f0-675b516da7e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0e88636d6854ed49e24a72518ba20ec7a1b50771
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703098"
---
# <a name="use-a-pull-distribution-point-with-configuration-manager"></a>Verwenden eines Pullverteilungspunkts mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*


Beim Verteilen von Inhalten an einen Standardverteilungspunkt in der Configuration Manager-Konsole sendet der Standortserver die Inhalte per Push an den Verteilungspunkt. Ein Pullverteilungspunkt ruft Inhalte ab, indem er diese von einem Quellspeicherort wie einem Client herunterlädt.  

Wenn Sie Inhalte an viele Verteilungspunkte verteilen, können Pullverteilungspunkte dazu beitragen, die Verarbeitungslast auf dem Standortserver zu reduzieren. Des Weiteren können Pullverteilungspunkte die Übertragung von Inhalten an die Server beschleunigen. Normalerweise sendet die Verteilungs-Manager-Komponente auf dem Standortserver die Inhalte an jeden Verteilungspunkt. Der Standort lagert die Übertragung von Inhalten nun jedoch in die Pullverteilungspunkte aus.  

Sie können einzelne Verteilungspunkte als Pullverteilungspunkte konfigurieren. Dazu geben Sie für jeden Pullverteilungspunkt mindestens einen Quellverteilungspunkt an, von dem Inhalte abgerufen werden können. Ein Pullverteilungspunkt kann Inhalte nur von einem Verteilungspunkt herunterladen, den Sie als Quellverteilungspunkt angegeben haben. 

Wenn Sie Inhalte an einen Pullverteilungspunkt in der Konsole verteilen, sendet der Standortserver diesem eine Benachrichtigung. Der Pullverteilungspunkt lädt die Inhalte anschließend von einem Quellverteilungspunkt herunter. Die Inhaltsübertragung wird vom Pullverteilungspunkt verwaltet, indem der Inhalt von einem Verteilungspunkt heruntergeladen wird, auf dem eine Kopie der Inhalte bereits verfügbar ist.  

Von Pullverteilungspunkten werden dieselben Konfigurationen und Funktionen wie von herkömmlichen Verteilungspunkten unterstützt. Ein Pullverteilungspunkt unterstützt beispielsweise Folgendes: 
- Multicast und PXE-Konfigurationen
- Inhaltsprüfung
- Bedarfsgesteuerte Inhaltsverteilung
- HTTP- oder HTTPS-Übertragungen von Clients
- dieselben Zertifikatoptionen, die auch andere Verteilungspunkte unterstützen
- die Verwaltung von einzelnen Verteilungspunkten oder von Verteilungspunkten, die Mitglieder einer Verteilungspunktgruppe sind  

Einen Pullverteilungspunkt konfigurieren Sie beim Installieren des Verteilungspunkts. Nach der Erstellung eines Verteilungspunkts konfigurieren Sie diesen als Pullverteilungspunkt, indem Sie die Eigenschaften der Rolle bearbeiten. Weitere Informationen zum Verwenden eines Verteilungspunkts als Pullverteilungspunkt finden Sie unter [Pullverteilungspunkt](../../servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pull).  

Die Konfiguration als Pullverteilungspunkt kann durch Bearbeiten der Eigenschaften des Verteilungspunkts entfernt werden. Dadurch wird der Normalzustand des Verteilungspunkts wiederhergestellt. Der Standortserver verwaltet zukünftige Inhaltsübertragungen an den Verteilungspunkt.  



### <a name="distribution-process"></a>Verteilungsprozess

Im Folgenden wird die Abfolge der Ereignisse bei der Verteilung von Inhalten an einen Pullverteilungspunkt dargestellt:

-   Sobald Inhalte an einen Pullverteilungspunkt in der Konsole verteilt werden, wird von der Paketübertragungs-Manager-Komponente auf dem Standortserver die Standortdatenbank überprüft, um zu ermitteln, ob die Inhalte auf einem Quellverteilungspunkt verfügbar sind. Wenn die Inhalte nicht auf einem Quellverteilungspunkt für den Pullverteilungspunkt verfügbar ist, wird diese Überprüfung alle 20 Minuten wiederholt, bis die Inhalte verfügbar sind.  

-   Wenn vom Paketübertragungs-Manager die Verfügbarkeit des Inhalts bestätigt wird, wird der Pullverteilungspunkt benachrichtigt, damit der Inhalt heruntergeladen wird. Wenn bei dieser Benachrichtigung ein Fehler auftritt, wird sie entsprechend der **Wiederholungseinstellungen** der Softwareverteilungskomponente für Pullverteilungspunkte erneut gesendet. Nach Eingang dieser Benachrichtigung auf dem Pullverteilungspunkt wird versucht, die Inhalte von den Quellverteilungspunkten herunterzuladen.  

-   Während der Pullverteilungspunkt die Inhalte herunterlädt, ruft der Paketübertragungs-Manager den Status basierend auf dem **Status der Abrufeinstellungen** der Softwareverteilungskomponente für Pullverteilungspunkte ab.  Sobald das Herunterladen auf den Pullverteilungspunkt abgeschlossen ist, wird dieser Status an den Verwaltungspunkt übermittelt.  



## <a name="configure-site-component-settings"></a>Konfigurieren von Einstellungen für Standortkomponenten

Wenn Sie einen Pullverteilungspunkt verwenden, sollten Sie sich mit den folgenden Einstellungen für Standortkomponenten vertraut machen und diese konfigurieren:  

1.  Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Standorte** aus.  

2.  Wählen Sie den Standort aus. Klicken Sie im Menüband zuerst auf **Standortkomponenten konfigurieren** und anschließend auf **Softwareverteilung**.  

3. Wechseln Sie zur Registerkarte **Pullverteilungspunkt**.  

4.  Sehen Sie sich in der Gruppe **Wiederholungseinstellungen** die folgenden Werte an:  

    -   **Wiederholungsversuche:** die Anzahl der Versuche des Paketübertragungs-Managers, den Pullverteilungspunkt zu benachrichtigen, sodass dieser Inhalte herunterladen kann. Wenn die Anzahl der Wiederholungsversuche überschritten wird, bricht der Paketübertragungs-Manager die Übertragung ab. Der Standardwert beträgt 30.  

    -   **Verzögerung vor Neuversuchen (Minuten):** die Zeit in Minuten, die zwischen den Versuchen des Paketübertragungs-Managers liegt. Der Standardwert beträgt 20.  

5.  Sehen Sie sich in der Gruppe **Status der Abrufeinstellungen** die folgenden Werte an:  

    -   **Anzahl von Abrufen:** die Anzahl der Kontakte zwischen dem Paketübertragungs-Manager und dem Pullverteilungspunkt zum Abrufen des Auftragsstatus. Wenn die Anzahl der Wiederholungsversuche überschritten wird, bevor der Auftrag abgeschlossen ist, bricht der Paketübertragungs-Manager die Übertragung ab. Der Standardwert beträgt 72.   

    -   **Verzögerung vor Neuversuchen (Minuten):** die Zeit in Minuten, die zwischen den Versuchen des Paketübertragungs-Managers liegt. Der Standardwert beträgt 60.   
    
    > [!NOTE]  
    >  Der Pullverteilungspunkt lädt Inhalte auch dann weiterhin herunter, wenn der Paketübertragungs-Manager einen Auftrag aufgrund der überschrittenen Anzahl von Abrufversuchen abbricht. Nach dem Abschluss des Downloads sendet der Pullverteilungspunkt eine entsprechende Statusmeldung. Der neue Status wird in der Konsole angezeigt.  
    


## <a name="limitations"></a>Einschränkungen 

-   Sie können einen Cloudverteilungspunkt nicht als Pullverteilungspunkt konfigurieren.  

-   Sie können die Verteilungspunktrolle auf einem Standortserver nicht als Pullverteilungspunkt konfigurieren.  

-   Mit der Konfiguration für vorab bereitgestellte Inhalte wird die Konfiguration des Pullverteilungspunkts überschrieben. Wenn Sie die Option **Diesen Verteilungspunkt für vorab bereitgestellten Inhalt aktivieren** auf einem Pullverteilungspunkt aktivieren, wartet dieser auf die Bereitstellung von Inhalten. Dies bedeutet, dass er keine Inhalte vom Quellverteilungspunkt abruft. Ebenso wie ein Standardverteilungspunkt für vorab bereitgestellten Inhalt empfängt auch der Pullverteilungspunkt keine Inhalte vom Standortserver. Weitere Informationen finden Sie unter [Vorab bereitgestellter Inhalt](manage-network-bandwidth.md#BKMK_PrestagingContent).  

-   Ein Pullverteilungspunkt nutzt keinen Zeitplan oder Konfigurationen zur Begrenzung der Datenübertragungsrate. Wenn Sie einen bereits installierten Verteilungspunkt als Pullverteilungspunkt konfigurieren, werden Konfigurationen für die Planung und Begrenzung der Datenübertragungsrate zwar gespeichert, aber nicht verwendet. Wenn Sie die Konfiguration des Pullverteilungspunkts zu einem späteren Zeitpunkt entfernen, werden die Konfigurationen für die Planung und Begrenzung der Datenübertragungsrate wie vorgesehen implementiert.  

    > [!NOTE]  
    >  Die Registerkarten **Zeitplan** und **Begrenzung der Datenübertragungsrate** werden in den Eigenschaften des Verteilungspunkts nicht angezeigt.  

-   Pullverteilungspunkte verwenden die Einstellungen auf der Registerkarte **Allgemein** der **Eigenschaften der Softwareverteilungskomponente** nicht für jeden Standort. Dies schließt auch **Einstellungen für gleichzeitige Verteilung** und **Multicast-Wiederholungseinstellungen** ein.  

-   Zur Übertragung von Inhalten von einem Quellverteilungspunkt in einer Remotegesamtstruktur müssen Sie auf dem Pullverteilungspunkt den Konfigurations-Manager-Client installieren. Außerdem müssen Sie ein Netzwerkzugriffskonto konfigurieren, über das der Zugriff auf den Quellverteilungspunkt möglich ist. Wenn Sie in der Version 1806 oder höher die Standortoption **Für HTTP-Websitesysteme von Configuration Manager generierte Zertifikate verwenden** aktivieren, benötigen Sie kein Netzwerkzugriffskonto.<!--1358228-->  

-   Wenn der Pullverteilungspunkt gleichzeitig ein Konfigurations-Manager-Client ist, muss die Clientversion mit der des Configuration Manager-Standorts übereinstimmen, der den Pullverteilungspunkt installiert. Der Pullverteilungspunkt verwendet die Komponente „CCMFramework“. Diese wird sowohl vom Pullverteilungspunkt als auch vom Konfigurations-Manager-Client genutzt.  



## <a name="about-source-distribution-points"></a>Informationen zu Quellverteilungspunkten  

Beim Konfigurieren des Pullverteilungspunkts müssen Sie mindestens einen Quellverteilungspunkt angeben:  

-   Vom Assistenten werden nur Verteilungspunkte angezeigt, die als Quellverteilungspunkte infrage kommen.  

-   Ein Pullverteilungspunkt kann als Quellverteilungspunkt für einen anderen Pullverteilungspunkt angegeben werden.  

-   Nur Verteilungspunkte, die HTTP unterstützen, können als Quellverteilungspunkte angegeben werden, wenn Sie die Configuration Manager-Konsole verwenden.  

-   Mit dem Configuration Manager SDK geben Sie einen Quellverteilungspunkt an, der für HTTPS konfiguriert ist. Wenn Sie einen Quellverteilungspunkt verwenden möchten, der für HTTPS konfiguriert ist, installieren Sie den Konfigurations-Manager-Client auf dem Pullverteilungspunkt.  

-   Wenn Ihre Remotebüros über eine bessere Internetverbindung verfügen oder die Auslastung Ihrer WAN-Verbindungen reduziert werden soll, können Sie ab Version 1806 in Microsoft Azure einen [Cloudverteilungspunkt](use-a-cloud-based-distribution-point.md) als Quelle verwenden. Der Pullverteilungspunkt benötigt für die Kommunikation mit Microsoft Azure Zugriff auf das Internet. Der Inhalt muss an den Quell-Cloudverteilungspunkt verteilt werden.<!--1321554-->  

    > [!Note]  
    > Für dieses Feature fallen im Rahmen Ihres Azure-Abonnements keine Kosten für die Datenspeicherung oder ausgehenden Netzwerkdatenverkehr an. Weitere Informationen finden Sie unter [Kosten einer cloudbasierten Verteilung](use-a-cloud-based-distribution-point.md#bkmk_cost).  


> [!Tip]  
> Wenn von einem Pullverteilungspunkt Inhalt von einem Quellverteilungspunkt heruntergeladen wird, wird dieser Pullverteilungspunkt im Bericht **Verwendungsdatenzusammenfassung für Verteilungspunkt** in der Spalte **Clients mit Zugriff (eindeutig)** als Client gezählt.  


### <a name="source-priorities"></a>Prioritäten von Quellen

-   Sie können entweder jedem Quellverteilungspunkt eine gesonderte Priorität oder mehreren Quellverteilungspunkten dieselbe Priorität zuweisen.  

-   Über die Priorität wird bestimmt, in welcher Reihenfolge vom Pullverteilungspunkt Inhalte von dessen Quellverteilungspunkten angefordert werden.  

-   Zuerst wird vom Pullverteilungspunkt eine Verbindung mit einem Quellverteilungspunkt mit dem niedrigsten Wert für die Priorität hergestellt. Wenn mehrere Quellverteilungspunkte mit derselben Priorität vorhanden sind, wählt der Pullverteilungspunkt eine dieser Quellen zufällig aus.  

-   Sind die Inhalte in der ausgewählten Quelle nicht verfügbar, versucht der Pullverteilungspunkt, die Inhalte von einem anderen Verteilungspunkt mit derselben Priorität herunterzuladen.  

-   Wenn keine der Verteilungspunkte mit der angegebenen Priorität über die Inhalte verfügen, versucht der Pullverteilungspunkt, diese von einem Quellverteilungspunkt mit der nächstniedrigeren Prioritätsstufe herunterzuladen. Dieser Suchvorgang wird solange fortgesetzt, bis die Inhalte gefunden werden.   

- Wenn die Inhalte auf keinem der zugewiesenen Quellverteilungspunkte gefunden werden können, startet der Pullverteilungspunkt nach 30 Minuten den Vorgang erneut.  



## <a name="inside-the-pull-distribution-point"></a>Kernkomponenten von Pullverteilungspunkten 

-   Die Inhaltsübertragung wird von Pullverteilungspunkten mithilfe der Komponente **CCMFramework** verwaltet. Der Konfigurations-Manager-Client schließt diese Komponente ein.  

-   Wenn Sie den Pullverteilungspunkt aktivieren, führt der Standort den Installer **pulldp.msi** aus. Dabei wird auch die Komponente „CCMFramework“ installiert. Der Configuration Manager-Client ist für das Framework nicht erforderlich.  

-   Nach der Installation des Pullverteilungspunkts nutzt dieser überwiegend den Dienst **CCMExec**.  

-   Der Pullverteilungspunkt greift beim Übertragen von Inhalten auf den in Windows integrierten **Background Intelligent Transfer Service** (BITS) zurück. Die Installation der BITS-Erweiterung für den IIS-Server ist zur Nutzung des Pullverteilungspunkts nicht erforderlich.<!--sms.503672 -Clarified BITS use-->

-  Funktionsdetails finden Sie in den folgenden Protokolldateien auf dem Pullverteilungspunkt:  
    - **DataTransferService.log**
    - **PullDP.log**



## <a name="see-also"></a>Weitere Informationen:  
 [Grundlegende Konzepte für das Content Management](fundamental-concepts-for-content-management.md)   
