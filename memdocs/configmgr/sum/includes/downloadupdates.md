1.  Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, und klicken Sie auf den Knoten **Softwareupdates**.  

2.  Wählen Sie das herunterzuladende Softwareupdate mit einer der folgenden Methoden aus:  

    -   Sie können über den Knoten **Softwareupdategruppen** beliebig viele Softwareupdategruppen auswählen. Klicken Sie anschließend im Menüband auf **Herunterladen**.  

    -   Wählen Sie über den Knoten **Alle Softwareupdates** mindestens ein Softwareupdate aus. Klicken Sie anschließend im Menüband auf **Herunterladen**.  

        > [!NOTE]  
        >  Im Knoten **Alle Softwareupdates** zeigt Configuration Manager nur Softwareupdates an, die die Klassifizierungen **Kritisch** und **Sicherheit** aufweisen, und in den letzten 30 Tagen veröffentlicht wurden.  

        > [!TIP]  
        >  Klicken Sie auf **Kriterien hinzufügen**, um die Softwareupdates zu filtern, die im Knoten **Alle Softwareupdates** angezeigt werden. Speichern Sie die Suchkriterien, die Sie häufig verwenden, und verwalten Sie anschließend die gespeicherten Suchanfragen auf der Registerkarte **Suchen**.  


3.  Konfigurieren Sie im Assistenten zum Herunterladen von Softwareupdates auf der Seite **Bereitstellungspaket** die folgenden Einstellungen:  

    -  **Bereitstellungspaket auswählen**: Wählen Sie diese Einstellung aus, um ein vorhandenes Bereitstellungspaket für die in der Bereitstellung enthaltenen Softwareupdates auszuwählen.  

        > [!NOTE]  
        >  Softwareupdates, die der Standort bereits in das ausgewählte Bereitstellungspaket heruntergeladen hat, werden nicht erneut heruntergeladen.  

    -  **Neues Bereitstellungspaket erstellen**: Wählen Sie diese Einstellung aus, um ein neues Bereitstellungspaket für die Softwareupdates in der Bereitstellung zu erstellen. Konfigurieren Sie die folgenden Einstellungen:  

        -   **Name**: Gibt den Namen des Bereitstellungspakets an. Das Paket muss einen eindeutigen Namen haben, der den Paketinhalt kurz beschreibt. Er ist auf 50 Zeichen begrenzt.  

        -   **Beschreibung**: Geben Sie eine Beschreibung mit Informationen zum Bereitstellungspaket an. Die optionale Beschreibung ist auf 127 Zeichen begrenzt.    

        -   **Paketquelle**: Gibt den Speicherort der Quelldateien der Softwareupdates an. Geben Sie für den Quellspeicherort einen Netzwerkpfad (beispielsweise `\\server\sharename\path`) ein, oder klicken Sie auf **Durchsuchen**, um den Netzwerkpfad zu suchen. Erstellen Sie den freigegebenen Ordner für die Quelldateien des Bereitstellungspakets, bevor Sie mit der nächsten Seite fortfahren.  

             - Sie können den angegebenen Speicherort nicht als Quelle eines anderen Softwarebereitstellungspakets verwenden.  

             - Sie können den Paketquellspeicherort in den Eigenschaften des Bereitstellungspakets ändern, nachdem das Bereitstellungspaket von Configuration Manager erstellt wurde. In diesem Fall müssen Sie jedoch zuerst den Inhalt der ursprünglichen Paketquelle an den neuen Paketquellspeicherort kopieren.  

             -  Das Computerkonto des SMS-Anbieters und der Benutzer, der den Assistenten zum Herunterladen der Softwareupdates ausführt, müssen beide über die Berechtigung **Schreiben** für den Downloadspeicherort verfügen. Beschränken Sie den Zugriff auf den Downloadspeicherort. Diese Einschränkung verringert die Gefahr, dass Angreifer die Quelldateien von Softwareupdates manipulieren.  

        - **Binäre differenzielle Replikation aktivieren**: Aktivieren Sie diese Einstellung, um den Netzwerkverkehr zwischen Standorten zu minimieren. Die binäre differenzielle Replikation (BDR) aktualisiert nur die Inhalte, die sich im Paket geändert haben, anstatt den gesamten Paketinhalt zu aktualisieren. Weitere Informationen finden Sie unter [Binäre differenzielle Replikation](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#binary-differential-replication).  

4.  Geben Sie auf der Seite **Verteilungspunkte** die Verteilungspunkte oder Verteilungspunktgruppen zum Hosten der Softwareupdatedateien an. Weitere Informationen zu Verteilungspunkten finden Sie unter [Konfigurationen für Verteilungspunkte](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs). Diese Seite ist nur verfügbar, wenn Sie ein neues Softwareupdate-Bereitstellungspaket erstellen.  

5.  Die Seite **Verteilungspunkte** ist nur verfügbar, wenn Sie ein neues Bereitstellungspaket für Softwareupdates erstellen. Geben Sie die folgenden Einstellungen an:  

    -   **Verteilungspriorität**: Verwenden Sie diese Einstellung, um die Verteilungspriorität für das Bereitstellungspaket anzugeben. Die Verteilungspriorität gilt, wenn das Bereitstellungspaket an die Verteilungspunkte an untergeordneten Standorten gesendet wird. Bereitstellungspakete werden in der Reihenfolge ihrer Priorität gesendet: „Hoch“, „Mittel“ oder „Niedrig“. Pakete mit identischer Priorität werden in der Reihenfolge ihrer Erstellung gesendet. Wenn es keinen Rückstand gibt, wird das Paket unabhängig von seiner Priorität sofort verarbeitet. Standardmäßig sendet der Standort Pakete mit der Priorität **Mittel**.  

    -   **Für bedarfsgesteuerte Verteilung aktivieren**: Verwenden Sie diese Einstellung, um die bedarfsgesteuerte Verteilung von Inhalt an Verteilungspunkte, die für dieses Feature konfiguriert sind, und in den aktuellen Begrenzungsgruppen zu aktivieren. Wenn Sie diese Einstellung aktivieren, erstellt der Verwaltungspunkt einen Trigger. Mit diesem Trigger wird der Verteilungs-Manager zur Verteilung des Inhalts an alle bevorzugten Verteilungspunkte aufgefordert, wenn der Inhalt für das Paket von einem Client angefordert wird und der Inhalt nicht verfügbar ist. Weitere Informationen finden Sie unter [Bedarfsgesteuerte Inhaltsverteilung](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution).  

    -   **Einstellungen für vorab bereitgestellten Verteilungspunkt**: Verwenden Sie diese Einstellung, um anzugeben, wie Sie Inhalte an vorab bereitgestellte Verteilungspunkte verteilen möchten. Wählen Sie eine der folgenden Optionen aus:  

        -   **Inhalt automatisch herunterladen, wenn Pakete Verteilungspunkten zugeordnet sind**: Verwenden Sie diese Einstellung, um die Einstellungen für die Vorabbereitstellung zu ignorieren und Inhalte an den Verteilungspunkt zu verteilen.   

        -   **Nur Inhaltsänderungen auf den Verteilungspunkt herunterladen**: Verwenden Sie diese Einstellung, um den ursprünglichen Inhalt am Verteilungspunkt vorab bereitzustellen und dann Inhaltsänderungen an den Verteilungspunkt zu verteilen.  

        -   **Den Inhalt dieses Pakets manuell an den Verteilungspunkt kopieren**: Verwenden Sie diese Einstellung, um Inhalte immer am Verteilungspunkt vorab bereitzustellen. Dies ist die Standardoption.  

        Weitere Informationen zur Vorabbereitstellung von Inhalten für Verteilungspunkte finden Sie unter [Use Prestaged content](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage) (Verwenden von vorab bereitgestelltem Inhalt).  


6.  Geben Sie auf der Seite **Downloadpfad** den Pfad an, der von Configuration Manager zum Herunterladen der Quelldateien für Softwareupdates verwendet wird. Verwenden Sie eine der folgenden Optionen:  

    -   **Softwareupdates aus dem Internet herunterladen**: Wählen Sie diese Einstellung aus, um die Softwareupdates von dem Speicherort im Internet herunterzuladen. Dies ist die Standardoption.  

    -   **Softwareupdates von einem Pfad auf meinem Netzwerk herunterladen**: Wählen Sie diese Einstellung aus, um die Softwareupdates aus einem lokalen Verzeichnis oder aus einem freigegebenen Ordner herunterzuladen. Diese Einstellung ist nützlich, wenn der Computer, auf dem der Assistent ausgeführt wird, keine Internetverbindung aufweist. Die Softwareupdates können von jedem Computer mit Internetzugang vorläufig heruntergeladen werden. Sie werden dann an einem Ort im lokalen Netzwerk gespeichert, auf den der Computer zugreifen kann, auf dem der Assistent ausgeführt wird.  


7.  Wählen Sie auf der Seite **Sprachauswahl** die Sprachen aus, für die der Standort die ausgewählten Softwareupdates herunterlädt. Der Standort lädt diese Updates nur dann herunter, wenn sie in den ausgewählten Sprachen verfügbar sind. Softwareupdates, die nicht sprachspezifisch sind, werden immer heruntergeladen. Standardmäßig werden vom Assistenten die Sprachen ausgewählt, die Sie in den Eigenschaften des Softwareupdatepunkts konfiguriert haben. Es muss mindestens eine Sprache ausgewählt werden, bevor die nächste Seite angezeigt werden kann. Wenn Sie nur Sprachen auswählen, die von einem Softwareupdate nicht unterstützt werden, schlägt das Herunterladen des Updates fehl.  

8. Überprüfen Sie auf der Seite **Zusammenfassung** die im Assistenten ausgewählten Einstellungen. Klicken Sie dann auf **Weiter**, um die Softwareupdates herunterzuladen.  

9. Überprüfen Sie auf der Seite **Abschluss**, ob die Softwareupdates erfolgreich heruntergeladen wurden. Klicken Sie dann auf **Schließen**.  
