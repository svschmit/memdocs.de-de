---
title: 'Synchronisieren von Updates mit keiner Internetverbindung '
titleSuffix: Configuration Manager
description: Führen Sie die Synchronisierung von Softwareupdates auf dem obersten Softwareupdatepunkt aus, der nicht mit dem Internet verbunden ist.
ms.date: 02/13/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 1a997c30-8e71-4be5-89ee-41efb2c8d199
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: c2fd85ea9d72e0986f56e24c7ccb66826829079b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689668"
---
# <a name="synchronize-software-updates-from-a-disconnected-software-update-point"></a>Synchronisieren von Softwareupdates bei einem getrennten Softwareupdatepunkt  

*Gilt für: Configuration Manager (Current Branch)*

 Wenn der Softwareupdatepunkt am Standort der obersten Ebene nicht mit dem Internet verbunden ist, müssen Sie die Metadaten für Softwareupdates mithilfe der Export- und Importfunktionen des Tools „WSUSUtil“ synchronisieren. Sie können einen vorhandenen WSUS-Server, der nicht der Configuration Manager-Hierarchie angehört, als Synchronisierungsquelle auswählen. In diesem Artikel erfahren Sie, wie Sie die Export- und Importfunktionen des Tools „WSUSUtil“ verwenden.  

 Zum Exportieren und Importieren von Metadaten für Softwareupdates gehen Sie wie folgt vor: Sie müssen Metadaten für Softwareupdates aus der WSUS-Datenbank auf einem angegebenen Exportserver exportieren, die lokal gespeicherten Dateien mit den Lizenzbedingungen auf den getrennten Softwareupdatepunkt kopieren und dann die Metadaten für Softwareupdates in die WSUS-Datenbank auf dem getrennten Softwareupdatepunkt importieren.  

 Mithilfe der nachstehenden Tabelle können Sie den Exportserver identifizieren, auf den die Metadaten für Softwareupdates exportiert werden müssen.  

|Softwareupdatepunkt|Upstream-Updatequelle für verbundene Softwareupdatepunkte|Exportserver für getrennten Softwareupdatepunkt|  
|---------------------------|-----------------------------------------------------------------|------------------------------------------------------------|  
|Standort der zentralen Verwaltung|Microsoft Update (Internet)<br /><br /> Vorhandener WSUS-Server|Wählen Sie einen WSUS-Server aus, der anhand der in der Configuration Manager-Umgebung benötigten Softwareupdateklassifizierungen, Produkte und Sprachen mit Microsoft Update synchronisiert wurde.|  
|Eigenständiger primärer Standort|Microsoft Update (Internet)<br /><br /> Vorhandener WSUS-Server|Wählen Sie einen WSUS-Server aus, der anhand der in der Configuration Manager-Umgebung benötigten Softwareupdateklassifizierungen, Produkte und Sprachen mit Microsoft Update synchronisiert wurde.|  

 Überprüfen Sie, ob die Softwareupdatesynchronisierung auf dem ausgewählten Exportserver abgeschlossen ist, bevor Sie den Exportprozess starten. Dadurch stellen Sie sicher, dass die jüngsten Metadaten für Softwareupdates synchronisiert werden. Gehen Sie wie folgt vor, um zu überprüfen, ob die Softwareupdatesynchronisierung erfolgreich abgeschlossen wurde.  

#### <a name="to-verify-that-software-updates-synchronization-has-completed-successfully-on-the-export-server"></a>So überprüfen Sie, ob die Softwareupdatesynchronisierung auf dem Exportserver erfolgreich abgeschlossen wurde  

1.  Öffnen Sie die WSUS-Verwaltungskonsole, und stellen Sie eine Verbindung mit der WSUS-Datenbank auf dem Exportserver her.  

2.  Klicken Sie in der WSUS-Verwaltungskonsole auf **Synchronisierungen**. Im Ergebnisbereich wird eine Liste der Synchronisierungsversuche für Softwareupdates angezeigt.  

3.  Suchen Sie im Ergebnisbereich den letzten Synchronisierungsversuch für Softwareupdates, und überprüfen Sie, ob dieser erfolgreich abgeschlossen wurde.  

> [!IMPORTANT]  
> - Das Tool „WSUSUtil“ muss lokal auf dem Exportserver ausgeführt werden, um die Metadaten für Softwareupdates zu exportieren. Es muss außerdem lokal auf dem Server des getrennten Softwareupdatepunkts ausgeführt werden, um die Metadaten für Softwareupdates zu importieren. Der Benutzer, der das Tool „WSUSUtil“ ausführt, muss zudem auf beiden Servern der lokalen Administratorengruppe angehören.  
> - Wenn Sie Windows Server 2012 verwenden, stellen Sie sicher, dass [KB2819484](https://support.microsoft.com/help/2819484/cab-file-that-is-exported-by-using-the-wsusutil-exe-command-is-display) auf den WSUS-Servern installiert ist.

## <a name="export-process-for-software-updates"></a>Exportprozess für Softwareupdates  
 Der Exportprozess für Softwareupdates besteht aus zwei Hauptschritten. Zuerst werden lokal gespeicherte Dateien mit den Lizenzbedingungen auf den getrennten Softwareupdatepunkt kopiert, und dann werden die Metadaten für Softwareupdates aus der WSUS-Datenbank auf dem Exportserver exportiert.  

 Gehen Sie wie folgt vor, um die lokalen Metadaten für Lizenzbedingungen auf den getrennten Softwareupdatepunkt zu kopieren.  

#### <a name="to-copy-local-files-from-the-export-server-to-the-disconnected-software-update-point-server"></a>So kopieren Sie lokale Dateien vom Exportserver auf den Server des getrennten Sofwareupdatepunkts  

1. Navigieren Sie im Exportserver zu dem Order, in dem die Softwareupdates und Lizenzbedingungen für Softwareupdates gespeichert sind. Standardmäßig speichert der WSUS-Server die Dateien im Ordner „<*WSUS-Installationslaufwerk*>\WSUS\WSUSContent\\“, wobei das *WSUS-Installationslaufwerk* das Laufwerk ist, auf dem WSUS installiert ist.  

2. Kopieren Sie alle Dateien und Ordner von diesem Ort in den Ordner WSUSContent auf dem Server des getrennten Softwareupdatepunkts.  

   Gehen Sie wie folgt vor, um die Metadaten für Softwareupdates aus der WSUS-Datenbank auf dem Exportserver zu exportieren.  

#### <a name="to-export-software-updates-metadata-from-the-wsus-database-on-the-export-server"></a>So exportieren Sie Metadaten für Softwareupdates aus der WSUS-Datenbank auf dem Exportserver  

1.  Wechseln Sie an der Eingabeaufforderung des Exportservers zum Ordner, der "WSUSutil.exe" enthält. Dieses Tool befindet sich standardmäßig im Ordner "%*Programme*%\Update Services\Tools". Befindet sich das Tool beispielsweise am Standardspeicherort, geben Sie **cd %ProgramFiles%\Update Services\Tools**ein.  

2.  Geben Sie Folgendes ein, um die Metadaten für Softwareupdates in eine Paketdatei zu exportieren:  

     **wsusutil.exe export** *Paketname* *Protokolldatei*  
 
     Beispiel:  

     **wsusutil.exe export export.xml.gz export.log**  

     Das Format kann wie folgt zusammengefasst werden: Hinter „WSUSutil.exe“ stehen die Exportoption, der Name der beim Exportvorgang erstellten XML.GZ-Exportdatei und der Name einer Protokolldatei. „WSUSutil.exe“ exportiert die Metadaten des Exportservers und erstellt eine Protokolldatei des Vorgangs.  

    > [!NOTE]  
    >  Der Name des Pakets (.xml.gz) und der Protokolldatei müssen im aktuellen Ordner eindeutig sein.  

3.  Verschieben Sie das Exportpaket in den Ordner mit „WSUSutil.exe“ auf dem WSUS-Importserver.  

    > [!NOTE]  
    >  Der Importprozess wird dadurch erleichtert, dass Sie das Paket in diesen Ordner verschieben. Sie können das Paket an jeden Speicherort verschieben, auf den der Importserver Zugriff hat, und dann diesen Ort beim Ausführen von „WSUSutil.exe“ angeben.  

## <a name="import-software-updates-metadata"></a>Importieren von Metadaten für Softwareupdates  
 Gehen Sie wie folgt vor, um Metadaten für Softwareupdates vom Exportserver in den getrennten Softwareupdatepunkt zu importieren.  

> [!IMPORTANT]  
>  Importieren Sie stets ausschließlich Daten, die aus einer vertrauenswürdigen Quelle exportiert wurden. Die Sicherheit des WSUS-Servers kann durch den Import von Inhalten aus einer nicht vertrauenswürdigen Quelle beeinträchtigt werden.  

#### <a name="to-import-metadata-to-the-database-of-the-import-server"></a>So importieren Sie Metadaten in die Datenbank des Importservers  

1.  Wechseln Sie an der Eingabeaufforderung des WSUS-Importservers zum Ordner, der "WSUSutil.exe" enthält. Dieses Tool befindet sich standardmäßig im Ordner "%*Programme*%\Update Services\Tools".  

2.  Geben Sie Folgendes ein:  

     **wsusutil.exe import** *Paketname* *Protokolldatei*  

     Beispiel:  

     **wsusutil.exe import export.xml.gz import.log**  

     Das Format kann wie folgt zusammengefasst werden: Hinter „WSUSutil.exe“ stehen der Importbefehl, der Name der beim Exportvorgang erstellten Paketdatei (.xml.gz), der Pfad der Paketdatei, falls diese in einem anderen Ordner gespeichert ist, sowie der Name einer Protokolldatei. „WSUSutil.exe“ importiert die Metadaten des Exportservers und erstellt eine Protokolldatei des Vorgangs.  

## <a name="next-steps"></a>Nächste Schritte
Nachdem Softwareupdates zum ersten Mal synchronisiert wurden, oder wenn neue Klassifizierungen oder Produkte verfügbar sind, müssen Sie [die neuen Klassifizierungen und Produkte so konfigurieren](configure-classifications-and-products.md), dass Softwareupdates mit den neuen Kriterien synchronisiert werden.

Nachdem Sie Softwareupdates mit den erforderlichen Kriterien synchronisiert haben, [verwalten Sie Einstellungen für Softwareupdates](manage-settings-for-software-updates.md).   
