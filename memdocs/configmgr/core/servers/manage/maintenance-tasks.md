---
title: Wartungstasks
titleSuffix: Configuration Manager
description: Hier finden Sie Informationen dazu, welche Wartungstasks für Configuration Manager-Standorte und -Hierarchien zu welchem Zeitpunkt durchgeführt werden müssen.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 625bb787-6d16-47a0-8b0f-b129cd909ca3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e0a71fc2f09e967944adfc4266e25eb20acfb9fe
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694438"
---
# <a name="maintenance-tasks-for-configuration-manager"></a>Einrichten von Wartungstasks für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Configuration Manager-Standorte und -Hierarchien müssen regelmäßig gewartet und überwacht werden, damit Dienste effektiv und ohne Unterbrechungen bereitgestellt werden können. Durch regelmäßige Wartung wird die ordnungsgemäße, effiziente Funktionsfähigkeit von Hardware, Software und der Configuration Manager-Standortdatenbank dauerhaft sichergestellt. Durch optimale Leistung wird das Risiko eines Ausfalls erheblich reduziert.  

 Informationen zum Konfigurieren von Benachrichtigungen sowie zum Überwachen der Integrität von Configuration Manager mit dem Statussystem finden Sie unter [Verwenden von Benachrichtigungen und des Statussystems für Configuration Manager](../../../core/servers/manage/use-alerts-and-the-status-system.md).  

## <a name="maintenance-tasks"></a><a name="bkmk_MTs"></a> Wartungstasks

 Eine regelmäßige Wartung ist wichtig, um den ordnungsgemäßen Standortbetrieb zu gewährleisten. Führen Sie ein tägliches Wartungsprotokoll, um zu dokumentieren, wann die Wartung von wem vorgenommen wurde, und um alle wartungsrelevanten Kommentare de den ausgeführten Tasks aufzuzeichnen. Für die Wartung Ihres Standorts sollten Sie eine tägliche oder zumindest wöchentliche Wartung in Erwägung ziehen. Für einige Aufgaben wird ein anderer Zeitplan vonnöten sein. Zur allgemeinen Wartung können sowohl die integrierten Wartungstasks gezählt werden als auch andere Tasks wie die Kontowartung, die Sie zur Einhaltung Ihrer Unternehmensrichtlinien verwenden.  

 Orientieren Sie sich an den folgenden Informationen, wenn Sie den Ausführungszeitpunkt verschiedener Wartungstasks planen. Verwenden Sie diese Listen als Ausgangspunkt, und fügen Sie gegebenenfalls Tasks hinzu, die Sie benötigen.  

### <a name="daily-tasks"></a>Tägliche Aufgaben
Sie sollten erwägen, die folgenden Wartungstasks täglich durchzuführen:  

- Überprüfen, ob die vordefinierten Wartungstasks, die für die tägliche Durchführung geplant sind, erfolgreich ausgeführt werden.  

- Überprüfen des Configuration Manager-Datenbankstatus.  

- Überprüfen Sie den Status des Standortservers.  

- Überprüfen der Posteingänge des Configuration Manager-Standortsystems auf Dateirückstände.  

- Überprüfen Sie den Status der Standortsysteme.  

- Überprüfen Sie die Betriebssystemereignisprotokolle in den Standortsystemen.  

- Überprüfen Sie das SQL Server-Fehlerprotokoll auf dem Standortdatenbankcomputer.  

- Überprüfen Sie die Systemleistung.  

- Überprüfen von Configuration Manager-Warnmeldungen.  

### <a name="weekly-tasks"></a>Wöchentliche Aufgaben

Sie sollten erwägen, die folgenden Wartungstasks wöchentlich durchzuführen:  

- Überprüfen, ob die vordefinierten Wartungstasks, die für die wöchentliche Durchführung geplant sind, erfolgreich ausgeführt werden  

- Löschen Sie nicht erforderliche Dateien von Standortsystemen.  

- Erstellen und verteilen Sie ggf. Endbenutzerberichte.  

- Sichern Sie Anwendungs-, Sicherheits- und Systemereignisprotokolle und setzen Sie sie zurück.  

- Überprüfen Sie die Größe der Standortdatenbank, und stellen Sie sicher, dass ausreichend Speicherplatz auf dem Standortdatenbankserver verfügbar ist, um dem Wachstum der Standortdatenbank gerecht zu werden.  

- Durchführen einer SQL Server-Datenbankwartung für die Standortdatenbank entsprechend Ihrem SQL Server-Wartungsplan.  

- Überprüfen Sie den verfügbaren Speicherplatz auf allen Standortsystemen.  

- Führen Sie auf allen Standortsystemen Festplattendefragmentierungstools aus.  

### <a name="periodic-tasks"></a>Regelmäßige Tasks

Einige Tasks, die jedoch nicht während der täglichen oder wöchentlichen Wartung durchgeführt werden müssen, sind dennoch wichtig, um die Integrität Ihres Standorts zu gewährleisten. Diese Tasks stellen zudem sicher, dass die Sicherheit sowie die Wiederherstellungspläne auf dem neuesten Stand sind. Bei den folgenden Wartungstasks empfiehlt sich unter Umständen eine häufigere Ausführung als täglich oder wöchentlich:  

- Ggf. Ändern von Konten und Kennwörtern gemäß Ihrem Sicherheitsplan.  

- Überprüfen des Wartungsplans um sicherzustellen, dass geplante Wartungstasks in Abhängigkeit von den konfigurierten Standorteinstellungen ordnungsgemäß und effektiv geplant sind.  

- Überprüfen des Configuration Manager-Hierarchieentwurfs auf erforderliche Änderungen.  

- Prüfen der Netzwerkleistung zur Sicherstellung, dass keine Änderungen vorgenommen wurden, die Standortvorgänge beeinträchtigen.  

- Prüfen, dass Active Directory-Einstellungen, die sich auf Standortvorgänge auswirken, nicht geändert wurden. Stellen Sie beispielsweise sicher, dass Subnetze, die als Grenzen für einen Configuration Manager-Standort verwendeten Active Directory-Standorten zugewiesen sind, nicht geändert wurden.  

- Überprüfen des Wiederherstellungsplans auf erforderliche Änderungen  

- Durchführen einer Standortwiederherstellung gemäß dem Wiederherstellungsplan in einem Testlabor mithilfe einer Sicherungskopie der aktuellen Sicherung, die über den Wartungstask „Standortserver sichern“ erstellt wurde

- Überprüfen der Hardware auf Fehler oder verfügbare Hardwareupdates  

- Überprüfen der Gesamtintegrität des Standorts  

## <a name="maintain-the-operational-health-of-your-site-database"></a><a name="BKMK_UseMTs"></a> Aufrechterhalten der funktionalen Integrität Ihrer Standortdatenbank

 Während die von Ihnen geplanten und eingerichteten Tasks von Configuration Manager-Standort und -Hierarchie ausgeführt werden, werden der Configuration Manager-Datenbank durch Standortkomponenten ständig neue Daten hinzugefügt. Durch zunehmende Datenmengen werden die Datenbankleistung und der Datenbankspeicherplatz zunehmend beansprucht. Sie können Standortwartungstasks so einrichten, dass veraltete Daten, die Sie nicht mehr benötigen, entfernt werden.  

 In Configuration Manager sind vordefinierte Wartungstasks verfügbar, die Sie zur Aufrechterhaltung der Integrität der Configuration Manager-Datenbank verwenden können. Standardmäßig stehen nicht alle Wartungstasks für jeden Standort zur Verfügung. Einige Tasks sind aktiviert, andere hingegen nicht, und sie unterstützen alle einen Zeitplan, den Sie einrichten können.  

 Von den meisten Wartungstasks werden veraltete Daten in regelmäßigen Abständen aus der Configuration Manager-Datenbank entfernt. Durch das Entfernen nicht erforderlicher Daten wird die Größe der Datenbank reduziert. Hierdurch werden Leistung und Integrität der Datenbank sowie in der Folge die Effizienz von Standort und Hierarchie erhöht. Andere Tasks, wie etwa **Indizes neu erstellen**, helfen dabei, die Datenbankeffizienz zu gewährleisten. Andere Tasks, wie etwa **Standortserver sichern**, helfen Ihnen bei der Vorbereitung auf Notfallwiederherstellungen.  

> [!IMPORTANT]
> Wenn Sie die Ausführung von Tasks planen, von denen Daten gelöscht werden, berücksichtigen Sie die hierarchieweite Verwendung dieser Daten. Wenn von einem Task, durch den Daten gelöscht werden, an einem Standort ausgeführt wird, werden die Informationen aus der Configuration Manager-Datenbank gelöscht, und diese Änderung wird an alle Standorte in der Hierarchie repliziert. Durch diesen Löschvorgang können andere Tasks, die von diesen Daten abhängig sind, beeinträchtigt werden. So können Sie z.B. am Standort der zentralen Verwaltung einen Ermittlungstask einrichten, der monatlich ausgeführt wird, um Nicht-Clientcomputer zu ermitteln. Sie können die Installation des Configuration Manager Client auf diesen Computern innerhalb zwei Wochen vor ihrer Ermittlung planen. An einem Standort in der Hierarchie richtet jedoch ein Administrator den Task „Veraltete Ermittlungsdaten löschen“ ein, sodass dieser wöchentlich ausgeführt wird. Dies führt dazu, dass sieben Tage nach der Ermittlung von Nicht-Clientcomputern diese aus der Configuration Manager-Datenbank gelöscht werden. Sie wiederum bereiten am Standort der zentralen Verwaltung eine Pushinstallation des Configuration Manager-Clients auf den neuen Computern für Tag 10 vor. Doch da der Task „Veraltete Ermittlungsdaten löschen“ kürzlich ausgeführt wurde und dadurch Daten, die älter als sieben Tage waren, gelöscht wurden, sind die kürzlich ermittelten Computer in der Datenbank nicht mehr verfügbar.

Überprüfen Sie nach der Installation eines Configuration Manager-Standorts die verfügbaren Wartungstasks, und aktivieren Sie diejenigen, die für Ihre Vorgänge erforderlich sind. Überprüfen Sie den Standardzeitplan jedes Tasks, und richten Sie die Zeitpläne nach Bedarf ein, um eine Feinabstimmung des Tasks auf Ihre Hierarchie und Umgebung auszuführen. Der Standardzeitplan jedes Tasks ist für die meisten Umgebungen passend. Überwachen Sie dennoch die Leistung Ihrer Standorte und der Datenbank, und gehen Sie davon aus, dass eine Feinabstimmung der Tasks erforderlich ist, um die Effizienz Ihrer Bereitstellung zu steigern. Planen Sie regelmäßige Überprüfungen der Leistung von Standort und Datenbank ein, und konfigurieren Sie Wartungstasks sowie deren Zeitpläne neu, um die Effizienz zu gewährleisten.  

## <a name="set-up-maintenance-tasks"></a>Benutzerdefinierte Wartungstasks einrichten

 Von jedem Configuration Manager-Standort werden Wartungstasks unterstützt, mit denen die Betriebseffizienz der Standortdatenbank aufrechterhalten werden kann. Standardmäßig sind an jedem Standort mehrere Wartungstasks aktiviert. Von allen Tasks werden unabhängige Zeitpläne unterstützt. Wartungstasks werden einzeln für jeden Standort eingerichtet und gelten für die Datenbank an diesem Standort. Einige Tasks, wie etwa **Veraltete Ermittlungsdaten löschen** wirken sich auf Informationen aus, die an allen Standorten in der Hierarchie verfügbar sind.  

 In der Configuration Manager-Konsole werden nur die Wartungstasks angezeigt, die Sie an einem Standort einrichten können. Eine umfassende Liste mit Wartungstasks nach Standorttyp finden Sie unter [Referenz für Wartungstasks im Configuration Manager](../../../core/servers/manage/reference-for-maintenance-tasks.md).  

 Anhand des folgenden Verfahrens können Sie die allgemeinen Einstellungen von Wartungstasks einrichten.  

### <a name="to-set-up-maintenance-tasks-for-configuration-manager-version-1906"></a><a name="bkmk_MTs1906"></a>Einrichten von Wartungstasks für Configuration Manager, Version 1906
<!--3555894-->
Ab Version 1906 können Wartungsaufgaben für Standortserver auf ihrer eigenen Registerkarte in der Detailansicht eines Standortservers angezeigt, bearbeitet und überwacht werden. Wie in früheren Configuration Manager-Versionen können Sie Wartungsaufgaben bearbeiten, indem Sie in der Gruppe **Einstellungen** die Option **Standortwartung** auswählen.

1. Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Standortkonfiguration** >**Standorte**.
1. Wählen Sie einen Standort in der Liste aus, und klicken Sie dann auf die Registerkarte **Wartungstasks** im Detailbereich.
1. Es werden nur die Tasks angezeigt, die am ausgewählten Standort verfügbar sind. Klicken Sie mit der rechten Maustaste auf einen der Wartungstasks, und wählen Sie eine der folgenden Optionen aus:
   - **Aktivieren** – Aktivieren des Tasks.
   - **Deaktivieren** – Deaktivieren des Tasks.
   - **Bearbeiten** – Bearbeiten des Taskzeitplans oder seiner Eigenschaften.

![Registerkarte für Wartungstasks in der Detailansicht eines Standortservers](./media/3555894-maintenance-tasks.png)

Die Registerkarte **Wartungstasks** bietet Ihnen Informationen wie z. B.:

- Ob der Task aktiviert ist
- Der Taskzeitplan
- Letzte Startzeit
- Letzte Abschlusszeit
- Ob der Task erfolgreich abgeschlossen wurde
 
### <a name="to-set-up-maintenance-tasks-for-configuration-manager-version-1902-and-prior"></a>Einrichten von Wartungstasks für Configuration Manager, Version 1902 und früher

1. Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Standortkonfiguration** >**Standorte**.
2. Wählen Sie den Standort mit dem einzurichtenden Wartungstask aus.  
3. Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** **Standortwartung** aus, und wählen Sie dann den Wartungstask aus, den Sie einrichten möchten. Es werden nur die Tasks angezeigt, die am ausgewählten Standort verfügbar sind.

4. Wählen Sie **Bearbeiten**aus, um den Task einzurichten. Vergewissern Sie sich, dass das Kontrollkästchen **Diese Aufgabe aktivieren** aktiviert ist, und richten Sie einen Zeitplan zum Ausführen des Tasks ein. Wenn mithilfe des Tasks auch veraltete Daten gelöscht werden, legen Sie fest, in welchem Alter Daten bei der Taskausführung aus der Datenbank gelöscht werden sollen. Klicken Sie auf **OK**, um die **Eigenschaften** des Tasks zu schließen.

   > [!NOTE]  
   > Legen Sie für **Veraltete Statusmeldungen löschen** fest, in welchem Alter Daten beim Einrichten von Statusfilterregeln gelöscht werden sollen.  

5. Klicken Sie auf die Schaltflächen **Aktivieren** oder **Deaktivieren**, um den Task zu aktivieren bzw. zu deaktivieren, ohne die Taskeigenschaften zu ändern. Die Bezeichnung der Schaltfläche ändert sich je nach aktueller Konfiguration des Tasks.  
6. Wenn Sie die Wartungstasks konfiguriert haben, klicken Sie auf **OK**, um den Vorgang abzuschließen.

## <a name="next-steps"></a>Nächste Schritte

[Referenz für Wartungstasks](reference-for-maintenance-tasks.md)
