---
title: Verwalten von Netzwerkbandbreite für Inhalte
titleSuffix: Configuration Manager
description: Konfigurieren Sie Zeitplanung, Bandbreiteneinschränkung und vorab bereitgestellten Inhalt für Configuration Manager.
ms.date: 02/6/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e80d1151-91db-4a27-8411-a957297b67d0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b8ee7d00f3b5c98528d9999b83b07aa393b72e36
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704158"
---
# <a name="manage-network-bandwidth-for-content"></a>Verwalten von Netzwerkbandbreite für Inhalte
Um Ihnen die Verwaltung der Netzwerkbandbreite zu erleichtern, die für den Inhaltsverwaltungsvorgang von Configuration Manager verwendet wird, können Sie die integrierten Steuerelemente für Zeitplanung und Drosselung verwenden. Sie können auch vorab bereitgestellte Inhalte nutzen. In den folgenden Abschnitten werden diese Optionen detaillierter beschrieben.

##  <a name="scheduling-and-throttling"></a><a name="BKMK_PlanningForThrottling"></a>Zeitplanung und Bandbreiteneinschränkung  

 Wenn Sie ein Paket erstellen, den Quellpfad für den Inhalt ändern oder ein Update bei Inhalt am Verteilungspunkt ausführen, werden die Dateien aus dem Quellpfad auf die Inhaltsbibliothek auf dem Standortserver kopiert. Dann wird der Inhalt aus der Inhaltsbibliothek auf dem Standortserver in die Inhaltsbibliothek an den Verteilungspunkten kopiert. Wenn ein Update bei Inhaltsquelldateien ausgeführt wird und die Quelldateien bereits verteilt wurden, werden von Configuration Manager nur die Dateien abgerufen und an den Verteilungspunkt gesendet, die neu sind oder bei denen das Update ausgeführt wurde.

 Sie können die Steuerelemente für Zeitplanung und Drosselung für die Kommunikation zwischen Standorten sowie zwischen Standortserver und Remoteverteilungspunkt verwenden. Wenn die Netzwerkbandbreite auch nach dem Einrichten der Steuerelemente für Zeitplanung und Drosselung eingeschränkt ist, sollten Sie eine Vorabbereitstellung des Inhalts auf dem Verteilungspunkt in Betracht ziehen.  

 Sie können in Configuration Manager einen Zeitplan einrichten und Drosselungseinstellungen für Remoteverteilungspunkte angeben, mit denen festgelegt wird, wann und wie die Inhaltsverteilung ausgeführt wird. Es sind für jeden Remoteverteilungspunkt andere Konfigurationen möglich, mithilfe derer Sie mit Netzwerkbandbreiteneinschränkungen zwischen Standortserver und Remoteverteilungspunkt umgehen können. Die Steuerelemente für Zeitplanung und Drosselung für den Remoteverteilungspunkt sind mit den Einstellungen für eine Standardabsenderadresse vergleichbar. In diesem Fall werden die Einstellungen von einer neuen Komponente namens Paketübertragungs-Manager verwendet.

 Vom Paketübertragungs-Manager wird Inhalt von einem Standortserver als primärem oder sekundärem Standort an einen Verteilungspunkt verteilt, der auf einem Standortsystem installiert ist. Bei einem Verteilungspunkt, der sich nicht auf einem Standortserver befindet, werden die Drosselungseinstellungen auf der Registerkarte **Begrenzung der Datenübertragungsrate** und die Zeitplaneinstellungen auf der Registerkarte **Zeitplan** konfiguriert. Die Zeiteinstellungen basieren auf der Zeitzone am sendenden Standort, nicht auf der am Verteilungspunkt.  

> [!IMPORTANT]  
>  Die Registerkarten **Begrenzung der Datenübertragungsrate** und **Zeitplan** werden nur in den Eigenschaften von Verteilungspunkten, die nicht auf einem Standortserver installiert sind, angezeigt.  

Weitere Informationen finden Sie unter [Installieren und Konfigurieren von Verteilungspunkten in Configuration Manager](../../servers/deploy/configure/install-and-configure-distribution-points.md).  

##  <a name="prestaged-content"></a><a name="BKMK_PrestagingContent"></a>Vorab bereitgestellter Inhalt  
 Sie können Inhalt vorab bereitstellen, um der Inhaltsbibliothek auf einem Standortserver oder Verteilungspunkt vor der Verteilung des Inhalts Inhaltsdateien hinzuzufügen. Da die Inhaltsdateien sich bereits in der Inhaltsbibliothek befinden, werden sie bei der Verteilung des Inhalts nicht über das Netzwerk übertragen. Sie können Inhaltsdateien für Anwendungen und Pakete vorab bereitstellen.  

Wählen Sie in der Configuration Manager-Konsole den Inhalt, den Sie vorab bereitstellen möchten, und verwenden Sie dann den **Assistenten zum Erstellen von vorab bereitgestellten Inhaltsdateien**. Durch diesen wird eine komprimierte, vorab bereitgestellte Inhaltsdatei erstellt, die die Dateien und zugeordneten Metadaten für den ausgewählten Inhalt umfasst. Anschließend können Sie den Inhalt zur Bereitstellung auf einem Standortserver oder Verteilungspunkt manuell importieren. Beachten Sie dabei folgende Punkte:  

-   Wenn Sie die vorab bereitgestellte Inhaltsdatei in einen Standortserver importieren, wird sie der Inhaltsbibliothek auf dem Standortserver hinzugefügt und dann in der Datenbank des Standortservers registriert.  

-   Wenn Sie die vorab bereitgestellte Inhaltsdatei auf einem Verteilungspunkt importieren, werden die Inhaltsdateien zur Inhaltsbibliothek auf dem Verteilungspunkt hinzugefügt. Eine Statusmeldung wird an den Standortserver gesendet, in der der Standort über die Verfügbarkeit des Inhalts auf dem Verteilungspunkt informiert wird.  

Optional können Sie den Verteilungspunkt als **vorab bereitgestellt** konfigurieren, um die Inhaltsverteilung einfacher verwalten zu können. Anschließend können Sie beim Verteilen von Inhalt zwischen folgenden Möglichkeiten auswählen:  

-   Inhalt wird immer vorab auf dem Verteilungspunkt bereitgestellt.  

-   Der Anfangsinhalt des Pakets wird vorab bereitgestellt, Inhaltsaktualisierungen erfolgen mithilfe des regulären Inhaltsverteilungsvorgangs.  

-   Für Inhalt des Pakets wird stets der reguläre Inhaltsverteilungsvorgang verwendet.  

###  <a name="determine-whether-to-prestage-content"></a><a name="BKMK_DetermineToPrestageContent"></a>Bestimmen, ob Inhalt vorab bereitgestellt werden soll  
 Erwägen Sie, in den folgenden Szenarien Inhalte für Anwendungen und Pakete vorab bereitzustellen:  

-   **Beheben des Problems der begrenzten Netzwerkbandbreite zwischen Standortserver und Verteilungspunkt.** Wenn Planung und Drosselung zum Beheben Ihrer Bandbreitenprobleme nicht ausreichen, ziehen Sie die Vorabbereitstellung des Inhalts auf dem Verteilungspunkt in Betracht. Bei jedem Verteilungspunkt können Sie in den Verteilungspunkteigenschaften die Einstellung **Diesen Verteilungspunkt für vorab bereitgestellten Inhalt aktivieren** wählen. Wenn Sie diese Option aktivieren, wird der Verteilungspunkt als vorab bereitgestellter Verteilungspunkt identifiziert, und Sie können auswählen, wie der Inhalt pro Paket verwaltet werden soll.  

    Die folgenden Einstellungen stehen in den Eigenschaften für eine Anwendung, ein Paket, ein Treiberpaket, ein Startabbild, ein Installationsprogramm für Betriebssysteme und ein Image zur Verfügung. Mit diesen Einstellungen können Sie auswählen, wie die Inhaltsverteilung auf Remoteverteilungspunkten verwaltet wird, die als vorab bereitgestellt identifiziert werden:  

    -   **Inhalt automatisch herunterladen, wenn Pakete Verteilungspunkten zugeordnet sind**: Verwenden Sie diese Option, wenn Sie kleinere Pakete haben und die Zeitplanungs- und Drosselungseinstellungen für die Inhaltsverteilung eine ausreichende Steuerung bieten.  

    -   **Nur Inhaltsänderungen auf den Verteilungspunkt herunterladen**: Verwenden Sie diese Option, wenn Sie damit rechnen, dass zukünftige Aktualisierungen des Paketinhalts im Allgemeinen kleiner sind als das Anfangspaket. Beispielsweise könnten Sie eine Anwendung wie Microsoft Office vorab bereitstellen, da die Größe des Anfangspakets mehr als 700 MB beträgt, sodass das Paket nicht über das Netzwerk gesendet werden kann. Die Inhaltsupdates bei diesem Paket könnten jedoch kleiner als 10 MB und damit über das Netzwerk verteilbar sein. Ein weiteres Beispiel wären Treiberpakete, bei denen das Anfangspaket groß ist, inkrementelle Treiberergänzungen zum Paket jedoch klein sind.  

    -   **Den Inhalt dieses Pakets manuell an den Verteilungspunkt kopieren**: Verwenden Sie diese Option, wenn Sie große Pakete mit Inhalt wie einem Betriebssystem haben, die sie niemals über das Netzwerk an den Verteilungspunkt verteilen möchten. Wenn Sie diese Option auswählen, müssen Sie den Inhalt am Verteilungspunkt vorab bereitstellen.  

    > [!IMPORTANT]  
    >  Die genannten Optionen sind pro Paket anwendbar und können nur dann verwendet werden, wenn ein Verteilungspunkt als vorab bereitgestellt identifiziert wurde. Von Verteilungspunkten, die nicht als vorab bereitgestellt identifiziert wurden, werden diese Einstellungen ignoriert. In diesem Fall wird Inhalt vom Standortserver stets über das Netzwerk an diese Verteilungspunkte verteilt.  

-   **Wiederherstellen der Inhaltsbibliothek auf einem Standortserver.** Beim Ausfall eines Standortservers werden Informationen zu Paketen und Anwendungen, die in der Inhaltsbibliothek enthalten sind, im Rahmen des Wiederherstellungsvorgangs auf der Standortdatenbank wiederhergestellt. Die Dateien der Inhaltsbibliothek werden bei diesem Vorgang jedoch nicht wiederhergestellt. Wenn Sie nicht über eine Sicherung des Dateisystems verfügen, um die Inhaltsbibliothek wiederherzustellen, können Sie eine vorab bereitgestellte Inhaltsdatei mit den erforderlichen Paketen und Anwendungen von einem anderen Standort erstellen. Anschließend können Sie die vorab bereitgestellte Inhaltsdatei auf dem wiederhergestellten Standortserver extrahieren. Weitere Informationen zur Standortserversicherung und -wiederherstellung finden Sie unter [Sicherung und Wiederherstellung in Configuration Manager](../../servers/manage/backup-and-recovery.md).  
