---
title: Verwalten der Softwareupdatesynchronisierung
titleSuffix: Configuration Manager
description: So planen Sie die Softwareupdatesynchronisierung, starten die Softwareupdatesynchronisierung manuell, und überwachen die Softwareupdatesynchronisierung.
ms.date: 12/20/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: ea8698c4-9df5-4cf5-8b62-ab93115b4769
manager: dougeby
author: mestew
ms.author: mstewart
ms.openlocfilehash: d1b47965fa5cc36b0c0eb6d47c2214d1dceb8ee8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692938"
---
#  <a name="synchronize-software-updates"></a><a name="BKMK_SUMSync"></a> Synchronisieren von Softwareupdates

*Gilt für: Configuration Manager (Current Branch)*

 Bei der Softwareupdatesynchronisierung in Configuration Manager werden die Metadaten für Softwareupdates abgerufen, die die von Ihnen festgelegten Kriterien erfüllen. Dies umschließt bestimmte Produkte, Klassifizierungen und Sprachen. Standardmäßig werden Metadaten vom Softwareupdatepunkt am Standort der zentralen Verwaltung bzw. an einem eigenständigen primären Standort von Microsoft Update abgerufen. Anschließend sendet der Standortserver auf oberster Ebene eine Synchronisierungsanforderung an andere Standorte. Wenn die Synchronisierungsanforderung vom übergeordneten Standort bei einem Standort eingeht, werden die Metadaten für das Softwareupdate vom Softwareupdatepunkt des Standorts aus der Upstream[synchronisierungsquelle](../plan-design/plan-for-software-updates.md#BKMK_SyncSource) abgerufen. Weitere Informationen zur Synchronisierung von Softwareupdates finden Sie unter [Software updates synchronization (Informationen zur Softwaresynchronisierung)](../understand/software-updates-introduction.md#BKMK_Synchronization).

Sie legen für die Ausführung der Softwareupdatesynchronisierung einen Zeitplan fest, wenn Sie die Eigenschaften des Softwareupdatepunkts am Standort der obersten Ebene konfigurieren. Sobald Sie den Synchronisierungszeitplan festgelegt haben, ändern Sie ihn in der Regel während des normalen Betriebs nicht mehr. Allerdings können Sie die Softwareupdatesynchronisierung bei Bedarf manuell initiieren.

  > [!NOTE]  
  >  Softwareupdatepunkte müssen mit der Upstreamsynchronisierungsquelle verbunden sein, damit Softwareupdates synchronisiert werden können. Wenn ein Softwareupdatepunkt von der Upstreamsynchronisierungsquelle getrennt ist, können Sie Softwareupdates mithilfe der Export-Import-Methode synchronisieren. Weitere Informationen finden Sie unter [Synchronisieren von Softwareupdates bei einem getrennten Softwareupdatepunkt](synchronize-software-updates-disconnected.md).  

## <a name="schedule-software-updates-synchronization"></a>Planen der Softwareupdatesynchronisierung
Wenn Sie einen Zeitplan für die Softwareupdatesynchronisierung konfigurieren, wird die Synchronisierung mit Microsoft Update vom Softwareupdatepunkt am Standort der obersten Ebene am geplanten Tag und zur geplanten Zeit gestartet. Mit einem benutzerdefinierten Zeitplan können Sie Softwareupdates zu einem Zeitpunkt synchronisieren, zu dem die Anforderungen des WSUS-Servers (Windows Server Update Services), Standortservers und Netzwerks gering sind. Beispielsweise können Sie den Zeitplan so festlegen, dass Softwareupdates jede Woche um 2:00 Uhr synchronisiert werden. Im Rahmen der geplanten Synchronisierung werden alle Änderungen, die seit der letzten geplanten Synchronisierung an den Metadaten für das Softwareupdate vorgenommen wurden, in die Standortdatenbank eingefügt. Dazu gehören neue Metadaten für das Softwareupdate und Metadaten, die geändert oder entfernt wurden bzw. zwischenzeitlich abgelaufen sind.

Gehen Sie am Standort der obersten Ebene wie folgt vor, um die Softwareupdatesynchronisierung zu planen.  

#### <a name="to-schedule-software-updates-synchronization"></a>So planen Sie die Softwareupdatesynchronisierung  

  1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

  2.  Erweitern Sie im Arbeitsbereich **Verwaltung**den Bereich **Standortkonfiguration**, und klicken Sie dann auf "Standorte".  

  3.  Klicken Sie im Ergebnisbereich auf den Standort der zentralen Verwaltung oder einen eigenständigen primären Standort.  

  4.  Erweitern Sie auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** den Eintrag **Standortkomponenten konfigurieren**, und klicken Sie dann auf **Softwareupdatepunkt**.  

  5.  Wählen Sie im Dialogfeld "Eigenschaften der Softwareupdatepunktkomponente" die Option **Synchronisierung nach Zeitplan aktivieren**aus, und geben Sie dann den Synchronisierungszeitplan an.  

## <a name="manually-start-software-updates-synchronization"></a>Manuelles Initiieren der Softwareupdatesynchronisierung
Sie können die Softwareupdatesynchronisierung am Standort der obersten Ebene in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** über den Knoten **Alle Softwareupdates** manuell initiieren.  

Gehen Sie am Standort der obersten Ebene wie folgt vor, um die Softwareupdatesynchronisierung manuell zu initiieren.  

#### <a name="to-manually-start-software-updates-synchronization"></a>So initiieren Sie die Softwareupdatesynchronisierung manuell  

1. Klicken Sie in der mit dem Standort der zentralen Verwaltung, oder einem eigenständigen primären Standort verbundenen Configuration Manager-Konsole auf **Softwarebibliothek**.  

2. Erweitern Sie im Arbeitsbereich "Softwarebibliothek" den Eintrag **Softwareupdates** , und klicken Sie auf **Alle Softwareupdates** oder **Softwareupdategruppen**.  

3. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Softwareupdates synchronisieren**. Bestätigen Sie im Dialogfeld, dass Sie die Synchronisierung initiieren möchten, indem Sie auf **Ja** klicken.  

   Nach dem Start der Synchronisierung auf dem Softwareupdatepunkt können Sie den Synchronisierungsprozess in der Configuration Manager-Konsole bei allen Softwareupdatepunkten in der Hierarchie überwachen. Gehen Sie wie folgt vor, um die Softwareupdatesynchronisierung zu überwachen.  


## <a name="monitor-software-updates-synchronization"></a>Überwachen der Softwareupdatesynchronisierung
Nach dem Start der Synchronisierung können Sie den Prozess in der Configuration Manager-Konsole für alle Softwareupdatepunkte in der Hierarchie überwachen. Gehen Sie wie folgt vor, um die Softwareupdatesynchronisierung zu überwachen. Weitere Informationen zur Überwachung von Softwareupdates und der Synchronisierung finden Sie unter [Monitor software updates (Überwachen von Softwareupdates)](../deploy-use/monitor-software-updates.md).

#### <a name="to-monitor-the-software-updates-synchronization-process"></a>So überwachen Sie die Softwareupdatesynchronisierung  

1. Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2. Klicken Sie im Arbeitsbereich **Überwachung** auf **Synchronisierungsstatus der Softwareupdatepunkte**.  

   Die Softwareupdatepunkte in der Configuration Manager-Hierarchie werden im Ergebnisbereich angezeigt. Von hier können Sie den Synchronisierungsstatus aller Softwareupdatepunkte überwachen. Ausführlichere Informationen zum Synchronisierungsprozess finden Sie in der Datei „wsyncmgr.log“, die sich auf jedem Standortserver im Ordner „<*Installationspfad von Configuration Manager*>\Logs“ befindet.  

## <a name="import-updates-from-the-microsoft-update-catalog"></a>Importieren von Updates aus dem Microsoft Update-Katalog

Der oberste Softwareupdatepunkt verwendet WSUS, um Informationen über Softwareupdates von Microsoft in Configuration Manager abzurufen. Gelegentlich benötigen Sie ein Update, das nicht automatisch mit WSUS für die von Ihnen ausgewählten Produkte und Klassifizierungen synchronisiert wird, sondern im [Microsoft Update-Katalog](https://catalog.update.microsoft.com) verfügbar ist. Updates, die nicht automatisch mit WSUS synchronisiert werden, dienen normalerweise der Lösung sehr spezifischer Probleme. Wenn ein Update im Katalog verfügbar ist, können Sie es in der Regel auch in WSUS importieren. Sie können es dann mit Configuration Manager synchronisieren und wie jedes andere Update bereitstellen.

### <a name="to-import-an-update-from-the-microsoft-update-catalog"></a>So importieren Sie ein Update aus dem Microsoft Update-Katalog

1. Öffnen Sie die WSUS-Verwaltungskonsole, und verbinden Sie sie mit dem obersten WSUS-Server in der Hierarchie.
   - Wenn Internet Explorer nicht der Standardwebbrowser des Computers ist, legen Sie ihn vorübergehend als Standardeinstellung fest.
2. Klicken Sie auf **Updates** oder auf den Namen Ihres WSUS-Servers. 
3. Wählen Sie im Bereich **Aktionen** die Option **Updates importieren...** aus, um ein Browserfenster für den [Microsoft Update-Katalog](https://catalog.update.microsoft.com) zu öffnen.
   ![Auswählen zu importierender Updates in der WSUS-Konsole](media/wsus-console-import-updates.png)
4. Installieren Sie bei Aufforderung das ActiveX-Steuerelement für den Microsoft Update-Katalog. Das Steuerelement muss installiert sein, um Updates in WSUS zu importieren. 
5. Suchen Sie im Browserfenster nach dem gewünschten Update. Klicken Sie auf die Schaltfläche **Hinzufügen** *, um es zum Auswahlkorb hinzuzufügen.
6. Klicken Sie auf **Auswahlkorb anzeigen**. Stellen Sie sicher, dass die Option **Import directly into Windows Server Update Services** (Direkt in Windows Server Update Services importieren) aktiviert ist. Klicken Sie anschließend auf **Importieren**.
    ![Importieren eines Updates aus dem Katalog in WSUS](./media/import-catalog-update-into-wsus.png)
7. Nachdem der Importvorgang abgeschlossen ist, klicken Sie im Browserfenster auf **Schließen**.
     - Setzen Sie Ihren Standardbrowser ggf. zurück.
8. Synchronisieren Sie Ihren Softwareupdatepunkt in Configuration Manager.


## <a name="next-steps"></a>Nächste Schritte
Nachdem Softwareupdates zum ersten Mal synchronisiert wurden, oder wenn neue Klassifizierungen oder Produkte verfügbar sind, müssen Sie [die neuen Klassifizierungen und Produkte so konfigurieren](configure-classifications-and-products.md), dass Softwareupdates mit den neuen Kriterien synchronisiert werden.

Nachdem Sie Softwareupdates mit den erforderlichen Kriterien synchronisiert haben, [verwalten Sie Einstellungen für Softwareupdates](manage-settings-for-software-updates.md).  
