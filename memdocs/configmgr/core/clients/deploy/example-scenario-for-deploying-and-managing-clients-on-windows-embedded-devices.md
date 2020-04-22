---
title: Beispielszenario – Bereitstellen von Windows Embedded-Clients
titleSuffix: Configuration Manager
description: Stellt ein Beispielszenario für die Bereitstellung und Verwaltung von Configuration Manager-Clients auf Windows Embedded-Geräten dar.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 10049c89-b37c-472b-b317-ce4f56cd4be7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 18e6252a3528e62153e7226ff285d24cd6ecf013
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693868"
---
# <a name="example-scenario-for-deploying-and-managing-configuration-manager-clients-on-windows-embedded-devices"></a>Beispielszenario für die Bereitstellung und Verwaltung von Configuration Manager-Clients auf Windows Embedded-Geräten

*Gilt für: Configuration Manager (Current Branch)*

In diesem Szenario wird gezeigt, wie Sie mithilfe von Configuration Manager Windows Embedded-Geräte mit aktivierten Schreibfiltern verwalten können. Wenn Ihre eingebetteten Geräte keine Schreibfilter unterstützen, entspricht ihr Verhalten dem Verhalten von Configuration Manager-Standardclients, und diese Verfahren werden nicht übernommen.  

Coho Vineyard & Winery eröffnet demnächst ein Besucherzentrum und benötigt Kioske, auf denen Windows Embedded-Geräte ausgeführt werden, um interaktive Präsentationen auszuführen. Das Gebäude, in dem das neue Besucherzentrum untergebracht ist, liegt nicht in unmittelbarer Nähe der IT-Abteilung. Es ist daher wichtig, dass die Kioske remote verwaltet werden können. Zusätzlich von der Software zur Ausführung der Präsentationen muss auf den Geräten den Sicherheitsrichtlinien des Unternehmens entsprechend eine aktuelle Antischadsoftware ausgeführt werden. Die Kioske müssen während der Öffnungszeiten des Besucherzentrums sieben Tage die Woche ohne Ausfallzeiten geöffnet haben.  

 Coho führt Configuration Manager bereits zur Verwaltung von Geräten in ihrem Netzwerk aus. Configuration Manager wird so konfiguriert, dass Endpoint Protection ausgeführt wird und Softwareupdates und Anwendungen installiert werden. Allerdings hat das IT-Team keinerlei Erfahrungen mit der Verwaltung von Windows Embedded-Geräten. Der für Configuration Manager zuständige Administrator führt daher einen Pilotversuch mit zwei zu verwaltenden Kiosken im Eingangsbereich durch.   

 Zur Verwaltung dieser Windows Embedded-Geräte mit aktivierten Schreibfiltern führt der Configuration Manager-Administrator die nachstehenden Schritte aus, um den Configuration Manager-Client zu installieren, den Schutz des Clients mithilfe von Endpoint Protection zu gewährleisten und die Software für interaktive Präsentationen zu installieren.  

1. Der Configuration Manager-Administrator informiert sich darüber, wie Schreibfilter von Windows Embedded-Geräten eingesetzt werden, und wie dieser Vorgang mithilfe von Configuration Manager erleichtert werden kann, indem die Schreibfilter automatisch deaktiviert und erneut aktiviert werden, um eine Softwareinstallation beizubehalten.  

    Weitere Informationen finden Sie unter [Planen der Clientbereitstellung auf Windows Embedded-Geräten](../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

2. Der Administrator erstellt zunächst eine neue abfragebasierte Gerätesammlung für die Windows Embedded-Geräte, bevor er den Configuration Manager-Client installiert. Da für die Computer des Unternehmens ein Standardbenennungsformat verwendet wird, kann der Administrator die Windows Embedded-Geräte anhand der ersten sechs Buchstaben des jeweiligen Computernamens eindeutig identifizieren: **WEMDVC**. Anhand der folgenden WQL-Abfrage erstellt der Administrator diese Sammlung: **select SMS_R_System.NetbiosName from SMS_R_System where SMS_R_System.NetbiosName like "WEMDVC%"**  

    Mithilfe dieser Sammlung kann der Administrator die Windows Embedded-Geräte mit anderen Konfigurationsoptionen als die anderen Geräte verwalten. Mit dieser Sammlung kann der Administrator Neustarts steuern, Endpoint Protection mit Clienteinstellungen bereitstellen und die Anwendung für interaktive Präsentationen bereitstellen.  

    Weitere Informationen finden Sie unter [Erstellen von Sammlungen](../../../core/clients/manage/collections/create-collections.md).  

3. Der Administrator konfiguriert die Sammlung für ein Wartungsfenster, um sicherzustellen, dass keine der Neustarts, die möglicherweise bei der Installation der Präsentationsanwendung und von Upgrades erforderlich sind, während der Öffnungszeiten des Besucherzentrums ausgeführt werden. Die Öffnungszeiten sind täglich von 09:00 bis 18:00 Uhr. Der Administrator konfiguriert das Wartungsfenster für 18:30 bis 06:00 Uhr täglich.  

4. Weitere Informationen finden Sie unter [Verwenden von Wartungsfenstern](../../../core/clients/manage/collections/use-maintenance-windows.md).  

5. Anschließend konfiguriert der Administrator eine benutzerdefinierte Geräteclienteinstellung zur Installation des Endpoint Protection-Clients. Dazu wählt er für die nachfolgenden Einstellungen **Ja** aus und stellt dann diese Clienteinstellung der Windows Embedded-Gerätesammlung bereit:  

   - **Installieren des Endpoint Protection-Clients auf Clientcomputern**  

   - **Für Windows Embedded-Geräte mit Schreibfiltern Commit für Endpoint Protection-Clientinstallation ausführen (hierdurch werden Neustarts erforderlich)**  

   - **Endpoint Protection-Clientinstallation und Neustarts außerhalb der Wartungsfenster zulassen**  

     Wenn der Configuration Manager-Client installiert ist, wird mit diesen Einstellungen der Endpoint Protection-Client installiert und sichergestellt, dass er nicht lediglich in die Überlagerung geschrieben, sondern im Betriebssystem als Teil der Installation beibehalten wird. Den Sicherheitsrichtlinien des Unternehmens entsprechend muss die Antischadsoftware stets installiert sein. Der Administrator möchte zudem nicht das Risiko eingehen, die Kioske bei einem Neustart auch nur für kurze Zeit ungeschützt zu lassen.  

   > [!NOTE]  
   >  Die bei der Installation des Endpoint Protection-Clients erforderlichen Neustarts finden lediglich während der Setupphase für die Geräte statt und bevor das Besucherzentrum eröffnet wird. Im Gegensatz zur periodischen Bereitstellung von Anwendungen oder Softwaredefinitionsupdates wird der Endpoint Protection-Client wahrscheinlich erst wieder auf dem gleichen Gerät installiert, wenn das Unternehmen das Upgrade auf die nächste Version von Configuration Manager durchführt.  

    Weitere Informationen finden Sie unter [Konfigurieren von Endpoint Protection](../../../protect/deploy-use/endpoint-protection-configure.md).  

6. Da die Konfigurationseinstellungen für den Client nun festliegen, bereitet der Administrator die Installation der Configuration Manager-Clients vor. Der Administrator muss den Schreibfilter auf den Windows Embedded-Geräten manuell deaktivieren, bevor er die Clients installieren kann. Der Administrator liest die den Kiosken beiliegende OEM-Dokumentation und befolgt die dort beschriebenen Anweisungen zur Deaktivierung der Schreibfilter.  

    Der Administrator benennt das Gerät so um, dass es dem im Unternehmen geltenden Standardbenennungsformat entspricht. Dann installiert er den Client manuell. Dazu führt er CCMSetup mit folgendem Befehl von einem zugeordneten Laufwerk aus, auf dem sich die Clientquelldateien befinden: **CCMSetup.exe /MP:mpserver.cohovineyardandwinery.com SMSSITECODE=CO1**  

    Mit diesem Befehl wird der Client installiert und dem Verwaltungspunkt mit dem Intranet-FQDN **mpserver.cohovineyardandwinery.com**sowie dem primären Standort **CO1**zugewiesen.  

    Der Administrator weiß, dass es immer eine Weile dauert, bis die Installation von Clients abgeschlossen ist und der Clientstatus an den entsprechenden Standort gesendet wird. Darum prüft der Administrator erst nach einer gewissen Wartezeit, ob die Clients installiert und dem Standort zugewiesen wurden und ob sie in der Sammlung, die er für die Windows Embedded-Geräte erstellt hat, als Clients erscheinen.  

    Zusätzlich prüft der Administrator Eigenschaften von Configuration Manager in der Systemteuerung der Geräte und vergleicht diese mit Windows-Standardcomputern, die vom Standort verwaltet werden. Beispielsweise wird auf der Registerkarte **Komponenten** unter **Hardwareinventur-Agent** die Einstellung **Aktiviert**angezeigt. Auf der Registerkarte **Aktionen** sind 11 Aktionen verfügbar, darunter **Evaluationszyklus für die Anwendungsbereitstellung** und **Ermittlungsdaten-Sammlungszyklus**.  

    Der Administrator ist sich nun sicher, dass die Clients erfolgreich installiert und zugewiesen wurden und dass bei ihnen Clientrichtlinien vom Verwaltungspunkt eingehen. Als Nächstes aktiviert er die Schreibfilter anhand der OEM-Anweisungen manuell.  

    Weitere Informationen finden Sie in folgenden Quellen:  

   -   [Bereitstellen von Clients auf Windows-Computern](../../../core/clients/deploy/deploy-clients-to-windows-computers.md)  

   -   [Zuweisen von Clients zu einem Standort](../../../core/clients/deploy/assign-clients-to-a-site.md)  

7. Der Configuration Manager-Client ist jetzt auf den Windows Embedded-Geräten installiert. Der Administrator vergewissert sich nun, dass er die Geräte genau wie Windows-Standardclients verwalten kann. Beispielsweise kann der Administrator die Geräte über die Configuration Manager-Konsole mithilfe der Remotesteuerung remote verwalten, Clientrichtlinien für sie starten sowie Clienteigenschaften und eine Hardwareinventur anzeigen.  

    Da diese Geräte einer Active Directory-Domäne hinzugefügt werden, muss der Administrator sie nicht manuell als vertrauenswürdige Clients genehmigen, und bestätigt über die Configuration Manager-Konsole, dass die Geräte genehmigt sind.  

    Weitere Informationen finden Sie unter [Verwalten von Clients](../../../core/clients/manage/manage-clients.md).  

8. Der Administrator führt den **Assistenten zum Bereitstellen von Software** aus und konfiguriert eine erforderliche Anwendung, um die Software für interaktive Präsentationen zu installieren. Auf der Seite **Benutzerfreundlichkeit** des Assistenten akzeptiert er im Bereich **Schreibfilterverarbeitung für Windows Embedded-Geräte** die Standardoption **Änderungen zum Stichtag oder während eines Wartungsfensters ausführen (erfordert Neustart)** .  

    Der Administrator behält diese Standardoption für Schreibfilter bei, um sicherzustellen, dass die Anwendung nach einem Neustart beibehalten wird und somit den Besuchern, die die Kioske benutzen, stets zur Verfügung steht. Mit dem täglichen Wartungsfenster wird ein sicherer Zeitraum bereitgestellt, in dem die bei Installationen und Updates erforderlichen Neustarts stattfinden können.  

    Der Administrator stellt die Anwendung der Windows Embedded-Gerätesammlung bereit.  

    Weitere Informationen finden Sie unter [Bereitstellen von Anwendungen mit Configuration Manager](../../../apps/deploy-use/deploy-applications.md).  

9. Der Administrator verwendet Softwareupdates und führt den Assistenten zum Erstellen automatischer Bereitstellungsregeln aus, um Definitionsupdates für Endpoint Protection zu konfigurieren. Er wählt die Vorlage **Definitionsupdates** aus, um den Assistenten mit Einstellungen aufzufüllen, die für Endpoint Protection geeignet sind.  

     Dazu gehören die folgenden Einstellungen auf der Seite **Benutzerfreundlichkeit** des Assistenten:  

   - **Verhalten am Stichtag**: Das Kontrollkästchen **Softwareinstallation** ist nicht aktiviert.  

   - **Schreibfilterverarbeitung für Windows Embedded-Geräte**: Das Kontrollkästchen **Änderungen zum Stichtag oder während eines Wartungsfensters ausführen (erfordert Neustart)** ist nicht aktiviert.  

     Der Administrator behält diese Standardeinstellungen bei. Wenn diese beiden Optionen diese Konfiguration aufweisen, können alle Softwaredefinitionsupdates für Endpoint Protection tagsüber im Overlay installiert werden. Es ist nicht notwendig, mit Installation und Commit bis zum Wartungsfenster zu warten. Mit dieser Konfiguration wird die Sicherheitsrichtlinie des Unternehmens, laut der auf Computern aktuelle Antischadsoftware ausgeführt werden muss, am besten erfüllt.  

     > [!NOTE]  
     >  Anders als Softwareinstallationen für Anwendungen können Softwaredefinitionsupdates für Endpoint Protection sehr häufig und sogar mehrmals täglich auftreten. Dabei handelt es sich oft um kleine Dateien. Für diese Arten sicherheitsbezogener Bereitstellungen ist es oft von Vorteil, immer im Overlay zu installieren, anstatt bis zum Wartungsfenster zu warten. Die Softwaredefinitionsupdates werden bei einem Geräteneustart schnell vom Configuration Manager-Client erneut installiert, da mit dieser Aktion eine Auswertungsüberprüfung gestartet und nicht auf die nächste geplante Auswertung gewartet wird.  

     Der Administrator wählt die Windows Embedded-Gerätesammlung für die automatische Bereitstellungsregel aus.  

     Weitere Informationen finden Sie unter  
               Schritt 3: Konfigurieren von Configuration Manager-Softwareupdates zum Bereitstellen von Definitionsupdates für Clientcomputer unter [Konfigurieren von Endpoint Protection](../../../protect/deploy-use/endpoint-protection-configure.md)  

10. Der Administrator entscheidet sich dazu, einen Wartungstask zu konfigurieren, von dem für alle Änderungen im Overlay regelmäßig ein Commit ausgeführt wird. Mit diesem Task soll nicht nur die Bereitstellung von Softwaredefinitionsupdates unterstützt, sondern auch die Anzahl der Updates reduziert werden, die sich ansammeln und bei jedem Geräteneustart erneut installiert werden müssen. Nach der Erfahrung des Administrators trägt dies zu einer effizienteren Ausführung der Antischadsoftware bei.  

    > [!NOTE]  
    >  Für diese Softwaredefinitionsupdates würde automatisch ein Commit auf das Abbild ausgeführt, falls auf den eingebetteten Geräten ein anderer Verwaltungstask ausgeführt wird, von dem die Ausführung eines Commits für Änderungen unterstützt wird. Beispielsweise würde bei der Installation einer neuen Version der Software für interaktive Präsentationen auch ein Commit für die Änderungen an Softwaredefinitionsupdates ausgeführt. Ein Commit für die Änderungen an Softwaredefinitionsupdates könnte auch bei der monatlichen, während des Wartungsfensters stattfindenden Installation von Standardsoftwareupdates ausgeführt werden. In diesem Szenario jedoch werden keine Standardsoftwareupdates ausgeführt, und Updates für die Software für interaktive Präsentationen dürften eher selten vorkommen. Es könnte daher einige Monate dauern, bis für die Softwaredefinitionsupdates ein automatischer Commit auf das Abbild ausgeführt wird.  

     Der Administrator erstellt zuerst eine benutzerdefinierte Tasksequenz, die außer dem Namen keinerlei Einstellungen aufweist. Er führt den Tasksequenzerstellungs-Assistenten aus:  

    1. Auf der Seite **Neue Tasksequenz erstellen** wählt der Administrator die Option **Neue benutzerdefinierte Tasksequenz erstellen** aus und klickt dann auf **Weiter**.  

    2. Auf der Seite **Informationen zur Tasksequenz** gibt der Administrator den Tasksequenznamen **Maintenance task to commit changes on embedded devices** ein und klickt dann auf **Weiter**.  

    3. Auf der Seite **Zusammenfassung** klickt der Administrator auf **Weiter** und schließt den Assistenten ab.  

       Dann stellt der Administrator diese benutzerdefinierte Tasksequenz der Windows Embedded-Gerätesammlung bereit und legt im Zeitplan fest, dass die Tasksequenz jeden Monat ausgeführt werden soll. Im Rahmen der Bereitstellungseinstellungen aktiviert er das Kontrollkästchen **Änderungen zum Stichtag oder während eines Wartungsfensters ausführen (erfordert Neustart)** , damit die Änderungen nach einem Neustart beibehalten werden. Zum Konfigurieren dieser Bereitstellung wählt der Administrator die von ihm erstellte benutzerdefinierte Tasksequenz aus. Dann klickt er auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Bereitstellen**, um den Assistenten zum Bereitstellen von Software zu starten:  

    4. Auf der Seite **Allgemein** wählt der Administrator die Windows Embedded-Gerätesammlung aus und klickt dann auf **Weiter**.  

    5. Auf der Seite **Bereitstellungseinstellungen** wählt der Administrator für **Erforderlich** den **Zweck** aus und klickt dann auf **Weiter**.  

    6. Auf der Seite **Zeitplanung** klickt der Administrator auf **Neu**, um einen wöchentlichen Zeitplan während des Wartungsfensters anzugeben, und klickt dann auf **Weiter**.  

    7. Der Administrator schließt den Assistenten ohne weitere Änderungen ab.  

       Weitere Informationen finden Sie unter  
                 [Verwalten von Tasksequenzen zum Automatisieren von Tasks](../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md).  

11. Die Kioske sollen automatisch ausgeführt werden. Der Administrator schreibt daher ein Skript, um die Geräte für die folgenden Einstellungen zu konfigurieren:  

    - Verwenden der automatischen Anmeldung mithilfe eines Gastkontos ohne Kennwort  

    - Automatisches Ausführen der Software für interaktive Präsentationen beim Start  

      Der Administrator verwendet Pakete und Programme, um dieses Skript für die Windows Embedded-Gerätesammlung bereitzustellen. Beim Ausführen des Assistenten zum Bereitstellen von Software aktiviert der Administrator das Kontrollkästchen **Änderungen zum Stichtag oder während eines Wartungsfensters ausführen (erfordert Neustart)** wieder, damit die Änderungen nach einem Neustart beibehalten werden.  

      Weitere Informationen finden Sie unter [Pakete und Programme](../../../apps/deploy-use/packages-and-programs.md).  

12. Am nächsten Morgen überprüft der Administrator die Windows Embedded-Geräte. Er bestätigt Folgendes:  

    - Der Kiosk wurde mithilfe des Gastkontos automatisch angemeldet.  

    - Die Software für interaktive Präsentationen wird ausgeführt.  

    - Der Endpoint Protection-Client wurde installiert und verfügt über die aktuellen Softwaredefinitionsupdates.  

    - Das Gerät wurde während des Wartungsfensters neu gestartet.  

      Weitere Informationen finden Sie in folgenden Quellen:  

    - [So überwachen Sie Endpoint Protection](../../../protect/deploy-use/monitor-endpoint-protection.md)  

    - [Überwachen von Anwendungen mit Configuration Manager](../../../apps/deploy-use/monitor-applications-from-the-console.md)  

13. Der Administrator überwacht die Kioske und meldet deren erfolgreiche Verwaltung seinem Manager. Das Ergebnis ist, dass 20 Kioske für das Besucherzentrum bestellt werden.  

     Zum Vermeiden der manuellen Installation des Configuration Manager-Clients, die manuelles Deaktivieren und Aktivieren der Schreibfilter erfordert, stellt der Administrator sicher, dass die Bestellung ein benutzerdefiniertes Image mit den Installationsdaten und der Standortzuweisung des Configuration Manager-Clients enthält. Darüber hinaus werden die Geräte gemäß dem Benennungsformat des Unternehmens benannt.  

     Die Kioske werden eine Woche vor der Eröffnung an das Besucherzentrum geliefert. Während dieses Zeitraums sind die Kioske mit dem Netzwerk verbunden, und die gesamte Geräteverwaltung erfolgt automatisch, sodass kein lokaler Administrator erforderlich ist. Der Administrator vergewissert sich, dass die Kioske wie gewünscht funktionieren:  

    -   Von den Clients auf den Kiosken wird die Standortzuweisung durchgeführt, und die vertrauenswürdigen Stammschlüssel werden aus den Active Directory-Domänendiensten heruntergeladen.  

    -   Die Clients auf den Kiosken werden automatisch der Windows Embedded-Gerätesammlung hinzugefügt und per Wartungsfenster konfiguriert.  

    -   Der Endpoint Protection-Client wurde installiert und verfügt über die aktuellen Softwaredefinitionsupdates für den Antischadsoftware-Schutz.  

    -   Die Software für interaktive Präsentationen wurde installiert, wird automatisch ausgeführt und ist für Besucher bereit.  

14. Nach diesem ersten Setup werden Neustarts, die für Updates ggf. erforderlich sind, nur bei geschlossenem Besucherzentrum ausgeführt.  
