---
title: Benachrichtigungen und Statussystem
titleSuffix: Configuration Manager
description: Konfigurieren Sie Warnungen, und verwenden Sie das Statussystem, damit Sie ständig über den Status Ihrer Configuration Manager-Bereitstellung informiert werden.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7341cc6e-9e08-41e4-bcc6-6c1ff12e85ca
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c066a61380e09961192bcbe7192e2e945341c97c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704278"
---
# <a name="use-alerts-and-the-status-system-for-configuration-manager"></a>Verwenden von Benachrichtigungen und des Statussystems für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Konfigurieren Sie Warnungen, und verwenden Sie das integrierte Statussystem, damit Sie ständig über den Status Ihrer Configuration Manager-Bereitstellung informiert werden.  


##  <a name="status-system"></a><a name="bkmk_Status"></a> Statussystem  
 Alle wichtigen Standortkomponenten generieren Meldungen, die Feedback zu Standort- und Hierarchievorgängen bereitstellen.    Mit diesen Informationen bleiben Sie auf dem Laufenden hinsichtlich der Integrität unterschiedlicher Standortprozesse. Sie können das Warnungssystem optimieren, sodass bekannte Probleme weitgehend ignoriert werden, während für andere Probleme, die möglicherweise Ihrer Aufmerksamkeit bedürfen, eine frühe Sichtbarkeit erreicht wird.  

 Das Configuration Manager-Statussystem wird standardmäßig ohne Konfiguration ausgeführt, da Einstellungen verwendet werden, die für die meisten Umgebungen geeignet sind. Folgende Elemente können aber konfiguriert werden:  

-   **Statuszusammenfassungen:** Sie können die Statuszusammenfassungen an jedem Standort bearbeiten, um die Häufigkeit von Statusmeldungen zu steuern, die eine Änderung des Statusindikators für die folgenden vier Zusammenfassungen generieren:  

    -   Anwendungsbereitstellung – Zusammenfassung  

    -   Anwendungsstatistik – Zusammenfassung  

    -   Komponentenstatus – Zusammenfassung  

    -   Standortsystemstatus – Zusammenfassung  

-   **Statusfilterregeln:** Sie können für jeden Standort neue Statusfilterregeln erstellen, die Priorität der Regeln ändern, Regeln deaktivieren oder aktivieren und nicht verwendete Regeln löschen.  

    > [!NOTE]  
    >  Bei Statusfilterregeln wird die Verwendung von Umgebungsvariablen zur Ausführung externer Befehle nicht unterstützt.  

-   **Statusberichterstattung:** Sie können sowohl die Server- als auch die Clientkomponenten-Berichterstattung konfigurieren, um zu ändern, wie Meldungen an das Configuration Manager-Statussystem gemeldet werden, sowie um anzugeben, wohin die Statusmeldungen gesendet werden.  

    > [!WARNING]  
    >  Die Standardeinstellungen für die Berichterstattung eignen sich für die meisten Umgebungen und sollten nur mit großer Sorgfalt geändert werden. Wenn Sie die Ebene der Statusberichterstattung erhöhen, damit alle Statusdetails gemeldet werden, kann dies zu einer höheren Last auf dem Configuration Manager-Standort führen, da mehr Statusmeldungen verarbeitet werden müssen. Wird die Ebene der Statusberichterstattung verringert, kann dies den Nutzen der Statuszusammenfassungen einschränken.  

Da im Statussystem getrennte Konfigurationen für jeden Standort verwaltet werden, müssen Sie jeden Standort einzeln bearbeiten.  

###  <a name="procedures-for-configuring-the-status-system"></a><a name="bkmk_configstatus"></a> Vorgehensweisen zum Konfigurieren des Statussystems  

##### <a name="to-configure-status-summarizers"></a>So konfigurieren Sie Statuszusammenfassungen  

1.  Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Standortkonfiguration** >**Standorte**, und wählen Sie dann den Standort aus, für den Sie das Statussystem konfigurieren möchten.  

2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** auf **Statuszusammenfassungen**.  

3.  Wählen Sie im Dialogfeld **Statuszusammenfassungen** die Statuszusammenfassung aus, die Sie konfigurieren möchten, und klicken Sie dann auf **Bearbeiten** , um die Eigenschaften für diese Zusammenfassung zu öffnen. Wenn Sie die Zusammenfassung "Anwendungsbereitstellung" oder "Anwendungsstatistik" bearbeiten, fahren Sie mit Schritt 5 fort. Wenn Sie die Zusammenfassung "Komponentenstatus" bearbeiten, fahren Sie mit Schritt 6 fort. Wenn Sie die Zusammenfassung "Standortsystemstatus" bearbeiten, fahren Sie mit Schritt 7 fort.  

4.  Gehen Sie nach dem Öffnen der Eigenschaftenseite für die Zusammenfassung „Anwendungsbereitstellung“ oder „Anwendungsstatistik“ wie nachfolgend beschrieben vor:  

    1.  Konfigurieren Sie auf der Eigenschaftenseite für die Zusammenfassung auf der Registerkarte **Allgemein** das Zusammenfassungsintervall, und klicken Sie dann auf **OK** , um die Eigenschaftenseite zu schließen.  

    2.  Klicken Sie auf **OK** , um das Dialogfeld **Statuszusammenfassungen** zu schließen und dieses Verfahren abzuschließen.  

5.  Gehen Sie nach dem Öffnen der Eigenschaftenseite für die Zusammenfassung „Komponentenstatus“ wie nachfolgend beschrieben vor:  

    1.  Konfigurieren Sie auf der Eigenschaftenseite für die Zusammenfassung auf der Registerkarte **Allgemein** die Werte für Replikation und Schwellenwertzeitraum.  

    2.  Wählen Sie auf der Registerkarte **Schwellenwerte** den zu konfigurierenden **Meldungstyp** aus, und klicken Sie dann in der Liste **Schwellenwerte** auf den Namen einer Komponente.  

    3.  Bearbeiten Sie im Dialogfeld **Eigenschaften von Statusschwellenwerten** die Schwellenwerte für Warnungs- und kritische Meldungen, und klicken Sie dann auf **OK**.  

    4.  Wiederholen Sie bei Bedarf Schritte 6.b und 6.c, und klicken Sie abschließend auf **OK** , um die Eigenschaften für die Zusammenfassung zu schließen.  

    5.  Klicken Sie auf **OK** , um das Dialogfeld **Statuszusammenfassungen** zu schließen und dieses Verfahren abzuschließen.  

6.  Gehen Sie nach dem Öffnen der Eigenschaftenseite für die Zusammenfassung „Standortsystemstatus“ wie nachfolgend beschrieben vor:  

    1.  Konfigurieren Sie auf der Eigenschaftenseite für die Zusammenfassung auf der Registerkarte **Allgemein** die Werte für Replikation und Schwellenwertzeitraum.  

    2.  Geben Sie auf der Registerkarte **Schwellenwerte** die Werte für die **Standardschwellenwerte** an, um die Standardschwellenwerte für die Statusanzeigen „Kritisch“ und „Warnung“ zu konfigurieren.  

    3.  Die Werte für bestimmte **Speicherobjekte**können Sie bearbeiten, indem Sie das Objekt in der Liste **Spezifische Schwellenwerte** auswählen und dann auf die Schaltfläche **Eigenschaften** klicken, um die Schwellenwerte für die Statusanzeigen „Kritisch“ und „Warnung“ für Speicherobjekte aufzurufen und zu bearbeiten. Klicken Sie auf **OK** , um die Speicherobjekteigenschaften zu schließen.  

    4.  Sie können ein neues Speicherobjekt erstellen, indem Sie auf die Schaltfläche **Objekt erstellen** klicken und die Werte für das Speicherobjekt angeben. Klicken Sie auf **OK** , um die Objekteigenschaften zu schließen.  

    5.  Sie können ein Speicherobjekt löschen, indem Sie das Objekt auswählen und auf die Schaltfläche **Löschen** klicken.  

    6.  Wiederholen Sie die Schritte 7.b bis 7.e. nach Bedarf. Klicken Sie abschließend auf **OK** , um die Zusammenfassungseigenschaften zu schließen.  

    7.  Klicken Sie auf **OK** , um das Dialogfeld **Statuszusammenfassungen** zu schließen und dieses Verfahren abzuschließen.  

##### <a name="to-create-a-status-filter-rule"></a>So erstellen Sie eine Statusfilterregel  

1.  Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Standortkonfiguration** >**Standorte**, und wählen Sie dann den Standort aus, an dem Sie das Statussystem konfigurieren möchten.  

2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** auf **Statusfilterregeln**. Das Dialogfeld **Statusfilterregeln** wird geöffnet.  

3.  Klicken Sie auf **Erstellen**.  

4.  Geben Sie im **Assistenten für neue Statusfilterregeln**auf der Seite **Allgemein** einen Namen für die neue Statusfilterregel sowie Meldungsübereinstimmungskriterien für die Regel an, und klicken Sie dann auf **Weiter**.  

5.  Geben Sie auf der Registerkarte **Aktionen** die Aktionen an, die ausgeführt werden sollen, wenn eine Statusmeldung mit der Filterregel übereinstimmt, und klicken Sie dann auf **Weiter**.  

6.  Überprüfen Sie auf der Seite **Zusammenfassung** die Details für die neue Regel, und schließen Sie dann den Assistenten ab.  

    > [!NOTE]  
    >  Configuration Manager erfordert nur, dass die neue Statusfilterregel einen Namen hat. Wenn die Regel erstellt wird, ohne Kriterien für die Verarbeitung von Statusmeldungen anzugeben, hat die Statusfilterregel keine Auswirkungen. Dadurch ist es möglich, dass Regeln vor dem eigentlichen Konfigurieren der Statusfilterkriterien für die einzelnen Regeln erstellt und organisiert werden.  

##### <a name="to-modify-or-delete-a-status-filter-rule"></a>So ändern oder löschen Sie eine Statusfilterregel  

1.  Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Standortkonfiguration** >**Standorte**, und wählen Sie dann den Standort aus, an dem Sie das Statussystem konfigurieren möchten.  

2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** auf **Statusfilterregeln**.  

3.  Wählen Sie im Dialogfeld **Statusfilterregeln** die zu ändernde Regel aus, und führen Sie dann eine der folgenden Aktionen aus:  

    -   Klicken Sie auf **Priorität erhöhen** oder **Priorität verringern** , um die Verarbeitungsreihenfolge der Statusfilterregel zu ändern. Wählen Sie dann eine andere Aktion aus, oder fahren Sie mit Schritt 8 dieses Verfahrens fort, um diesen Task abzuschließen.  

    -   Klicken Sie auf **Deaktivieren** oder **Aktivieren** , um den Status der Regel zu ändern. Wählen Sie anschließend eine andere Aktion aus, oder fahren Sie mit Schritt 8 dieses Verfahrens fort, um diesen Task abzuschließen.  

    -   Klicken Sie auf **Löschen** , um die Statusfilterregel von diesem Standort zu löschen, und klicken Sie dann auf **Ja** , um die Aktion zu bestätigen. Wählen Sie anschließend eine andere Aktion aus, oder fahren Sie mit Schritt 8 dieses Verfahrens fort, um diesen Task abzuschließen.  

    -   Klicken Sie auf **Bearbeiten** , um die Kriterien für die Regel zu ändern, und fahren Sie mit Schritt 5 dieses Verfahrens fort.  

4.  Ändern Sie auf der Registerkarte **Allgemein** des Eigenschaftendialogfeldes für die Statusfilterregel die Regel und die Meldungsübereinstimmungskriterien.  

5.  Ändern Sie auf der Registerkarte **Aktionen** die Aktionen, die ausgeführt werden sollen, wenn eine Statusmeldung mit der Filterregel übereinstimmt.  

6.  Klicken Sie zum Speichern der Änderungen auf **OK** .  

7.  Klicken Sie auf **OK** , um das Dialogfeld **Statusfilterregeln** zu schließen.  

##### <a name="to-configure-status-reporting"></a>So konfigurieren Sie die Statusberichterstattung  

1.  Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Standortkonfiguration** > **Standorte**, und wählen Sie dann den Standort aus, an dem Sie das Statussystem konfigurieren möchten.  

2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** auf **Standortkomponenten konfigurieren**, und wählen Sie dann **Statusberichterstattung**aus.  

3.  Geben Sie im Dialogfeld **Eigenschaften der Statusberichtkomponenten** die Server- und Clientkomponentenstatusmeldungen an, die berichtet oder protokolliert werden sollen:  

    1.  Konfigurieren Sie **Bericht**, um Statusmeldungen an das Configuration Manager-Statusmeldungssystem senden zu lassen.  

    2.  Konfigurieren Sie **Protokoll** , um Typ und Schweregrad von Statusmeldungen in das Windows-Ereignisprotokoll schreiben zu lassen.  

4.  Klicken Sie auf **OK**.  

###  <a name="monitor-the-status-system-of-configuration-manager"></a><a name="BKMK_MonitorSystemStatus"></a> Überwachen des Statussystems für Configuration Manager  
 **Systemstatus** bietet eine Übersicht über allgemeine Standortvorgänge sowie Standortservervorgänge in Ihrer Hierarchie. Hier können Sie Funktionsprobleme bei Standortsystemservern oder Komponenten erkennen, und Sie können den Systemstatus verwenden, um bestimmte Details zu verschiedenen Configuration Manager-Vorgängen zu überprüfen. Sie können den Systemstatus in der Configuration Manager-Konsole im Arbeitsbereich **Überwachung** im Knoten **Systemstatus** überwachen.  

 Von den meisten Configuration Manager-Standortsystemrollen und -Komponenten werden Statusmeldungen generiert. Details zu Statusmeldungen werden in den Betriebsprotokollen der jeweiligen Komponenten protokolliert und zusätzlich an die Standortdatenbank übermittelt. Dort werden sie zusammengefasst und in einem allgemeinen Rollup zu den Komponenten oder zur Standortsystemintegrität angezeigt. In diesen Rollups der Statusmeldungen sind Informationen und Details zu normalen Vorgängen sowie zu Warnungen und Fehlern enthalten. Sie können die Schwellenwerte konfigurieren, bei denen Warnungen und Fehlermeldungen ausgelöst werden, und eine Feinabstimmung des Systems ausführen. So können Sie gewährleisten, dass bekannte und nicht relevante Probleme nicht in den Rollupinformationen berücksichtigt werden, während Sie auf aktuelle Probleme bei Servern oder Komponentenvorgängen, die Sie möglicherweise untersuchen möchten, hingewiesen werden.  

 Der Systemstatus wird auf andere Standorte in einer Hierarchie als Standortdaten repliziert, nicht als globale Daten. Daher können Sie nur den Status des Standorts, mit dem Ihre Configuration Manager-Konsole verbunden ist, sowie der diesem Standort untergeordneten Standorte anzeigen. Aus diesem Grund empfiehlt es sich, für die Anzeige des Systemstatus eine Verbindung zwischen der Configuration Manager-Konsole und dem Standort der obersten Ebene Ihrer Hierarchie herzustellen.  

 Mithilfe der folgenden Tabelle können Sie die verschiedenen Systemstatusansichten identifizieren und in welchen Situationen sie zu verwenden sind.  

|Knoten|Weitere Informationen|  
|----------|----------------------|  
|Standortstatus|Verwenden Sie diesen Knoten, um einen Statusrollup für jedes Standortsystem anzuzeigen und die Integrität jedes Standortsystemservers zu überprüfen. Die Integrität von Standortsystemen wird bestimmt durch Schwellenwerte, die Sie für jeden Standort unter **Standortsystemstatus – Zusammenfassung**konfigurieren können.<br /><br /> Mithilfe des Dienst-**Managers für Configuration Manager** können Sie Statusmeldungen für jedes Standortsystem anzeigen, Schwellenwerte für Statusmeldungen festlegen und den Betrieb der Komponenten auf Standortsystemen verwalten.|  
|Komponentenstatus|Verwenden Sie diesen Knoten, um einen Statusrollup für jede Configuration Manager-Komponente anzuzeigen und die Betriebsintegrität der Komponente zu überprüfen. Die Integrität von Komponenten wird bestimmt durch Schwellenwerte, die Sie für jeden Standort unter **Statuszusammenfasser für Komponenten**konfigurieren können.<br /><br /> Mithilfe des Dienst-**Managers für Configuration Manager** können Sie Statusmeldungen für jede Komponente anzeigen, Schwellenwerte für Statusmeldungen festlegen und den Betrieb der Komponenten verwalten.|  
|In Konflikt stehende Datensätze|Verwenden Sie diesen Knoten, um Statusmeldungen für Clients mit Datensatzkonflikten anzuzeigen.<br /><br /> Configuration Manager identifiziert mithilfe der Hardware-ID Clients, bei denen es sich um Duplikate handeln könnte. Sie werden über in Konflikt stehende Datensätze informiert. Wenn Sie z.B. einen Computer erneut installieren müssen, bleibt die Hardware-ID unverändert, während sich die von Configuration Manager verwendete GUID ändern kann.|  
|Statusmeldungsabfragen|Verwenden Sie diesen Knoten, um Statusmeldungen für bestimmte Ereignisse und entsprechende Details abzufragen. Mithilfe von Statusmeldungsabfragen können Sie die Statusmeldungen zu bestimmten Ereignissen finden.<br /><br /> Statusmeldungsabfragen bieten sich an, um zu ermitteln, wann eine bestimmte Komponente, ein Vorgang oder ein Configuration Manager-Objekt geändert wurde und von welchem Konto die Änderung ausgeführt wurde. Zum Beispiel können Sie die integrierte Abfrage **Erstellte, geänderte oder gelöschte Sammlungen** ausführen, um herauszufinden, wann eine bestimmte Sammlung von welchem Benutzerkonto erstellt wurde.|  

####  <a name="manage-site-status-and-component-status"></a><a name="bkmk_managestatus"></a> Verwalten von Standortstatus und Komponentenstatus  
 Verwenden Sie die folgenden Informationen zum Verwalten von Standortstatus und Komponentenstatus:  

-   Hinweise zum Konfigurieren von Schwellenwerten für das Statussystem finden Sie unter [Vorgehensweisen zum Konfigurieren des Statussystems](#bkmk_configstatus).  

-   Verwenden Sie den **Service Manager für Configuration Manager**, um einzelne Komponenten zu verwalten.  

####  <a name="view-status-messages"></a><a name="bkmk_view"></a> Anzeigen von Statusmeldungen  
 Sie können die Statusmeldungen für einzelne Standortsystemserver und Komponenten anzeigen.  

 Zum Anzeigen von Statusmeldungen in der Configuration Manager-Konsole wählen Sie einen bestimmten Standortsystemserver oder eine Komponente aus, und klicken Sie dann auf **Meldungen anzeigen**. Sie können die Anzeige der Meldungen nach bestimmten Meldungstypen, nach einem bestimmten Meldungszeitraum und nach den Details der Statusmeldungen filtern.  

##  <a name="alerts"></a><a name="bkmk_Alerts"></a> Warnungen  
 Configuration Manager-Warnungen werden bei einigen Vorgängen generiert, wenn eine bestimmte Bedingung eintritt.  

- In der Regel werden Warnungen generiert, wenn ein Fehler auftritt, der behoben werden muss.  

- Möglicherweise werden Warnungen generiert, um auf das Vorhandensein einer bestimmten Bedingung hinzuweisen, damit Sie die Situation weiterhin überwachen können.  

- Einige Warnungen können Sie konfigurieren, etwa Warnungen für Endpoint Protection und Clientstatus, während andere Warnungen automatisch konfiguriert werden.  

- Sie können warnungsbezogene Abonnements konfigurieren, die dann Details per E-Mail senden können, wodurch die Wahrnehmung von wesentlichen Problemen erhöht wird.  

  In der folgenden Tabelle finden Sie Informationen dazu, wie Warnungen und Warnungsabonnements in Configuration Manager konfiguriert werden:  


|Aktion|Weitere Informationen|  
|------------|----------------------|  
|Konfigurieren von Endpoint Protection-Warnungen für eine Sammlung|Weitere Informationen finden Sie unter **Konfigurieren Sie Warnungen für Endpoint Protection** in [Konfigurieren von Endpoint Protection](../../../protect/deploy-use/endpoint-protection-configure.md)|  
|Konfigurieren von Clientstatuswarnungen für eine Sammlung|Siehe [Konfigurieren des Clientstatus](../../../core/clients/deploy/configure-client-status.md)|  
|Verwalten von Configuration Manager-Warnungen|Weitere Informationen finden Sie in diesem Thema im Abschnitt [Management tasks for alerts](#BKMK_Manage) .|  
|Konfigurieren von E-Mail-Abonnements für Warnungen|Weitere Informationen finden Sie in diesem Thema im Abschnitt [Management tasks for alerts](#BKMK_Manage) .|  
|Überwachen von Warnungen|Weitere Informationen finden Sie in diesem Thema im Abschnitt [Überwachen von Warnungen](#BKMK_MonitorAlerts)|  

###  <a name="management-tasks-for-alerts"></a><a name="BKMK_Manage"></a> Management tasks for alerts  

##### <a name="to-manage-general-alerts"></a>So verwalten Sie allgemeine Warnungen  

1. Wechseln Sie in der Configuration Manager-Konsole zu **Überwachung** > **Warnungen**, und wählen Sie dann einen Verwaltungstask aus.  

   In der nachfolgenden Tabelle finden Sie weitere Informationen zu den Verwaltungstasks, für die möglicherweise einige Informationen benötigt werden, bevor Sie sie auswählen.  

|Verwaltungstask|Details|  
    |---------------------|-------------|  
    |**Konfigurieren Sie**|Öffnet das Dialogfeld *&lt;Warnungsname*\>**Eigenschaften**, in dem Sie den Namen, den Schweregrad sowie die Schwellenwerte für die ausgewählte Warnung ändern können. Wenn Sie den Schweregrad der Warnung ändern, wirkt sich diese Konfiguration darauf aus, wie Warnungen in der Configuration Manager-Konsole angezeigt werden.|  
    |**Kommentare bearbeiten**|Geben Sie Kommentare für die ausgewählten Warnungen ein. Diese Kommentare werden zusammen mit den Warnungen in der Configuration Manager-Konsole angezeigt.|  
    |**Verschieben**|Hält die Überwachung der Warnung an, bis das angegebene Datum erreicht ist. Zu diesem Zeitpunkt wird der Zustand der Warnung aktualisiert.<br /><br /> Sie können eine Warnung nur anhalten (verschieben), wenn sie aktiviert ist.|  
    |**Abonnement erstellen**|Öffnet das Dialogfeld **Neues Abonnement** , in dem Sie ein E-Mail-Abonnement für die ausgewählte Warnung erstellen können.|  

<!--##### To configure Endpoint Protection alerts for a collection  

1.  pending  -->

##### <a name="to-configure-client-status-alerts-for-a-collection"></a>So konfigurieren Sie Clientstatuswarnungen für eine Sammlung  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** >   **Gerätesammlungen**.  

2.  Wählen Sie in der Liste **Gerätesammlungen** die Sammlung aus, für die Sie Warnungen konfigurieren möchten, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

    > [!NOTE]  
    >  Es können keine Benachrichtigungen für Benutzersammlungen konfiguriert werden.  

3.  Klicken Sie auf der Registerkarte **Warnungen** des Dialogfelds *&lt;Sammlungsname*\>**Eigenschaften** auf **Hinzufügen**.  

    > [!NOTE]  
    >  Die Registerkarte **Warnungen** wird nur angezeigt, wenn die Ihnen zugewiesene Sicherheitsrolle über Berechtigungen für Warnungen verfügt.  

4.  Wählen Sie im Dialogfeld **Neue Sammlungswarnungen hinzufügen** die Warnungen aus, die beim Unterschreiten bestimmter Clientstatuswerte generiert werden sollen, und klicken Sie dann auf **OK**.  

5.  Wählen Sie auf der Registerkarte **Warnungen** in der Liste **Bedingungen** die einzelnen Clientstatuswarnungen aus, und geben Sie für jede Warnung die folgenden Informationen an:  

    -   **Warnungsname** – Übernehmen Sie den Standardnamen, oder geben Sie einen neuen Namen für die Warnung ein.  

    -   **Warnungsschweregrad** – Wählen Sie in der Dropdownliste den Schweregrad aus, der in der Configuration Manager-Konsole angezeigt werden soll.  

    -   **Warnung auslösen**: Geben Sie den Schwellenwert für die Warnung in Prozent an.  

6.  Klicken Sie auf **OK**, um das Dialogfeld *&lt;Sammlungsname*\>**Eigenschaften** zu schließen.  

##### <a name="to-configure-email-notification-for-alerts"></a>So konfigurieren Sie E-Mail-Benachrichtigungen für Warnungen  

1.  Wechseln Sie in der Configuration Manager-Konsole zu **Überwachung** > **Warnungen** > **Abonnements**.  

2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **E-Mail-Benachrichtigung konfigurieren**.  

3.  Geben Sie im Dialogfeld **Eigenschaften der Komponente für E-Mail-Benachrichtigungen** die folgenden Informationen an:  

    -   **E-Mail-Benachrichtigungen für Warnungen aktivieren:** Aktivieren Sie dieses Kontrollkästchen, damit Configuration Manager einen SMTP-Server verwenden kann, um E-Mail-Benachrichtigungen zu versenden.  

    -   **FQDN oder IP-Adresse des SMTP-Servers, von dem Warnungen über E-Mail verschickt werden sollen:** Geben Sie den vollqualifizierten Domänennamen (FQDN) oder die IP-Adresse sowie den SMTP-Port für den E-Mail-Server an, der für die Benachrichtigungen verwendet werden soll.  

    -   **Verbindungskonto des SMTP-Servers:** Geben Sie die Authentifizierungsmethode an, mit der Configuration Manager Verbindungen mit dem E-Mail-Server herstellen soll.  

    -   **Sender address for email alerts** (Adresse des Absenders für Warnungen über E-Mail): Geben Sie die E-Mail-Adresse an, von der aus die Warnungen über E-Mail gesendet werden.  

    -   **SMTP-Server testen...:** Es wird eine Test-E-Mail an die E-Mail-Adresse gesendet, die in **Sender address for email alerts** angegeben ist.  

4.  Klicken Sie auf **OK** , um die Einstellungen zu speichern und das Dialogfeld **Eigenschaften der E-Mail-Benachrichtigungskomponente** zu schließen.  

##### <a name="to-subscribe-to-email-alerts"></a>So abonnieren Sie E-Mail-Benachrichtigungen  

1.  Wechseln Sie in der Configuration Manager-Konsole zu **Überwachung** > **Warnungen**.  

2.  Wählen Sie eine Warnung aus, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Abonnement** auf **Abonnement erstellen**.  

3.  Geben Sie im Dialogfeld **Neues Abonnement** die folgenden Informationen an:  

    -   **Name:** Geben Sie einen Namen ein, um das E-Mail-Abonnement zu identifizieren. Sie können bis zu 255 Zeichen verwenden.  

    -   **E-Mail-Adresse:** Geben Sie die E-Mail-Adressen ein, an die die Warnung gesendet werden soll. Sie können mehrere E-Mail-Adressen durch Semikolons trennen.  

    -   **Email language** (E-Mail-Sprache): Geben Sie in der Liste die Sprache für die E-Mail an.  

4.  Klicken Sie auf **OK** , um das Dialogfeld **Neues Abonnement** zu schließen und das E-Mail-Abonnement zu erstellen.  

    > [!NOTE]  
    >  Im Arbeitsbereich **Überwachung** können Sie Abonnements bearbeiten und löschen. Erweitern Sie den Knoten **Warnungen** , und klicken Sie auf den Knoten **Abonnements** .  

###  <a name="monitor-alerts"></a><a name="BKMK_MonitorAlerts"></a> Überwachen von Warnungen  
 Sie können die Warnungen im Arbeitsbereich **Überwachung** über den Knoten **Warnungen** anzeigen. Warnungen haben einen der folgenden Warnungszustände:  

- **Niemals ausgelöst:** Die Bedingung der Warnung wurde nicht erfüllt.  

- **Aktiv:** Die Bedingung der Warnung wurde erfüllt.  

- **Abgebrochen:** Die Bedingung für eine aktive Warnung ist nicht mehr erfüllt. Dieser Status zeigt an, dass die Bedingung, die die Warnung ausgelöst hat, nun behoben ist.  

- **Verschoben:** Der Administrator hat Configuration Manager so konfiguriert, dass der Zustand der Warnung zu einem späteren Zeitpunkt ausgewertet wird.  

- **Deaktiviert:** Die Warnung wurde vom Administrator deaktiviert. Wenn sich eine Warnung in diesem Zustand befindet, aktualisiert Configuration Manager die Warnung auch dann nicht, wenn sich ihr Zustand ändert.  

  Sie können eine der folgenden Aktionen durchführen, wenn Configuration Manager eine Warnung generiert:  

- Die Bedingung beheben, die die Warnung ausgelöst hat; Sie beheben beispielsweise ein Netzwerkproblem oder ein Konfigurationsproblem, das die Warnung ausgelöst hat. Wenn Configuration Manager feststellt, dass das Problem nicht mehr besteht, wird der Warnungszustand auf **Abbrechen** gesetzt.  

- Wenn die Warnung sich auf ein bekanntes Problem bezieht, können Sie die Warnung um einen bestimmten Zeitraum verschieben. Configuration Manager aktualisiert dann die Warnung auf ihren aktuellen Zustand.  

   Sie können nur aktive Warnungen verschieben.  

- Sie können den **Kommentar** einer Warnung bearbeiten, um anderen Administratoren mitzuteilen, dass Sie die Warnung zur Kenntnis genommen haben. Im Kommentar können Sie beispielsweise bestimmen, wie eine Bedingung behoben werden kann, Informationen zum aktuellen Zustand einer Bedingung bereitstellen oder erklären, warum Sie die Warnung verschoben haben.  
