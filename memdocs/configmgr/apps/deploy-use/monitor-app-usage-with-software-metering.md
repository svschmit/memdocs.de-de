---
title: Überwachen der App-Verwendung mit der Softwaremessung
titleSuffix: Configuration Manager
description: Dieser Abschnitt enthält weitere Informationen zu Vorgängen, die bei der Softwaremessung in Configuration Manager verfügbar sind.
ms.date: 09/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: b1fdaee2-2816-4447-94cd-609f6948f215
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 13d8cce1811c4a27f6a3e7485eea4d65132c2888
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689248"
---
# <a name="software-metering-in-configuration-manager"></a>Softwaremessung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Dieses Thema enthält eine Übersicht über alle bei der Configuration Manager-Softwaremessung möglicherweise ausgeführten Vorgänge.

> [!IMPORTANT]
>  Die Softwaremessung dient zur Überwachung von Desktop-Apps für Windows-PCs, deren Dateinamen auf **.exe**enden. Die Softwaremessung überwacht keine modernen Windows-Apps (beispielsweise unter Windows 8 verwendete Apps).

##  <a name="prerequisites-for-software-metering"></a>Voraussetzungen für die Softwaremessung
Für die Softwaremessung liegen keine externen Abhängigkeiten, sondern nur Abhängigkeiten innerhalb des Produkts vor.

|Abhängigkeit|Weitere Informationen|
|----------------|----------------------|
|Clienteinstellungen für die Softwaremessung.|Zum Verwenden der Softwaremessung muss die Clienteinstellung **Softwaremessung auf Clients aktivieren** aktiviert und auf Computern bereitgestellt sein. Sie können allen Computern in der Hierarchie Softwaremessungseinstellungen bereitstellen, oder Sie können Computergruppen benutzerdefinierte Einstellungen bereitstellen. Weitere Informationen finden Sie unter **Konfigurieren der Softwaremessung** in diesem Thema.|
|Der Reporting Services-Punkt|Es muss ein Reporting Services-Punkt erstellt werden, bevor Softwaremessungsberichte angezeigt werden können. Weitere Informationen finden Sie unter [Einführung in die Berichterstellung](../../core/servers/manage/introduction-to-reporting.md).|

##  <a name="configure-software-metering"></a>Konfigurieren der Softwaremessung
 Mithilfe dieses Verfahrens werden die Clientstandardeinstellungen für die Softwaremessung konfiguriert und auf alle Computer in der Hierarchie angewendet. Wenn diese Einstellungen nur auf bestimmte Computer angewendet werden sollen, erstellen Sie eine benutzerdefinierte Geräteclienteinstellung, und stellen Sie diese einer Sammlung mit den Computern bereit, auf denen die Softwaremessung verwendet werden soll. Weitere Informationen zum Erstellen von benutzerdefinierten Geräteeinstellungen finden Sie unter [Configure client settings (Konfigurieren von Clienteinstellungen)](../../core/clients/deploy/configure-client-settings.md).

1. Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Clienteinstellungen** > **Clientstandardeinstellungen**.

2. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.

3. Klicken Sie im Dialogfeld **Standardeinstellungen** auf **Softwaremessung**.

4. Konfigurieren Sie in der Liste **Geräteeinstellungen** die folgenden Optionen:

   -   **Softwaremessung auf Clients aktivieren:** Wählen Sie **TRUE** aus, um diese Softwaremessung zu aktivieren.

   -   **Datensammlung planen:** Konfigurieren Sie, wie häufig Softwaremessungsdaten von Clientcomputern gesammelt werden. Verwenden Sie den Standardwert (alle **7 Tage** ), oder klicken Sie zum Festlegen eines benutzerdefinierten Zeitplans auf **Zeitplan** .

5. Klicken Sie auf **OK** , um das Dialogfeld **Standardeinstellungen** zu schließen.

   Die Clientcomputer werden beim nächsten Download der Clientrichtlinien mit diesen Einstellungen konfiguriert. Informationen zum Initiieren des Richtlinienabrufs für einen einzelnen Client finden Sie unter [Manage clients (Verwalten von Clients)](../../core/clients/manage/manage-clients.md).

##  <a name="create-software-metering-rules"></a>Erstellen von Softwaremessungsregeln
 Erstellen Sie mit dem Assistenten zum Erstellen von Softwaremessungsregeln eine neue Softwaremessungsregel für Ihren Configuration Manager-Standort.

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** > **Softwaremessung**.

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Softwaremessungsregel erstellen**.

4.  Geben Sie im Assistenten zum Erstellen von Softwaremessungsregeln auf der Seite **Allgemein** die folgenden Informationen an:

    -   **Name** – der Name der Softwaremessungsregel. Dieser Name sollte beschreibend und eindeutig sein.

        > [!NOTE]
        >  Mehrere Softwaremessungsregeln können denselben Namen tragen, wenn der in den Regeln enthaltene Dateiname unterschiedlich ist.

    -   **Dateiname** : Name der zu messenden Programmdatei. Wenn Sie auf **Durchsuchen** klicken, wird das Dialogfeld **Öffnen** angezeigt, in dem Sie die zu verwendende Programmdatei auswählen können.

        > [!NOTE]
        >  Wenn Sie den Dateinamen der ausführbaren Datei im Feld **Dateiname** eingeben, wird nicht überprüft, ob diese Datei vorhanden ist oder ob sie die erforderlichen Headerinformationen enthält. Wenn möglich, klicken Sie auf **Durchsuchen** , und wählen Sie die zu messende ausführbare Datei aus.
        >
        >  Der Dateiname darf keine Platzhalterzeichen enthalten.
        >
        >  Dieses Feld ist optional, wenn ein Wert für **Ursprünglicher Dateiname** angegeben ist.

    -   **Ursprünglicher Dateiname** : Name der zu messenden ausführbaren Datei. Dieser Name entspricht den Informationen im Dateiheader, nicht dem Dateinamen selbst. Er ist hilfreich, wenn die ausführbare Datei umbenannt wurde, Sie sie jedoch gemäß ihrem ursprünglichen Namen messen möchten.

        > [!NOTE]
        >  Der ursprüngliche Dateiname darf keine Platzhalterzeichen enthalten.
        >
        >  Dieses Feld ist optional, wenn ein Wert für **Dateiname** angegeben ist.

    -   **Version** : Version der zu messenden ausführbaren Datei. Sie können das Platzhalterzeichen (&#42;) stellvertretend für eine beliebige Zeichenfolge und das Platzhalterzeichen (? ) stellvertretend für ein beliebiges einzelnes Zeichen angeben. Wenn Sie alle Versionen einer ausführbaren Datei messen möchten, verwenden Sie den Standardwert (&#42;).

    -   **Sprache** – die Sprache der zu messenden ausführbaren Datei. Der Standardwert ist das aktuelle Gebietsschema des von Ihnen verwendeten Betriebssystems. Wenn Sie eine zu messende ausführbare Datei durch Klicken auf die Schaltfläche **Durchsuchen** auswählen, wird dieses Feld automatisch aufgefüllt, wenn Sprachinformationen im Dateiheader vorhanden sind. Wenn Sie alle Sprachversionen einer Datei messen möchten, wählen Sie in der Dropdownliste den Eintrag **Beliebig** aus.

    -   **Beschreibung** – eine optionale Beschreibung für die Softwaremessungsregel.

    -   **Diese Softwaremessungsregel auf die folgenden Clients anwenden** : Wählen Sie aus, ob Sie die Softwaremessungsregel auf alle Clients in der Hierarchie oder nur auf die Clients anwenden möchten, die dem in der Liste **Standort** ausgewählten Standort zugewiesen sind.

5.  Klicken Sie zum Fortfahren auf **Weiter**.

6.  Überprüfen Sie die Einstellungen, und schließen Sie dann den Assistenten ab, um die Softwaremessungsregel zu erstellen. Die neue Softwaremessungsregel wird im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Softwaremessung** angezeigt.

##  <a name="configure-automatic-software-metering-rules"></a>Konfigurieren automatischer Softwaremessungsregeln
 In Configuration Manager können Sie die Softwaremessung zur automatischen Generierung deaktivierter Softwaremessungsregeln aus Inventurdaten über die letzte Verwendung konfigurieren, die in der Standortdatenbank aufbewahrt werden. Sie können diese Inventurdaten so konfigurieren, dass nur für Anwendungen, die auf einem bestimmten Prozentsatz der Computer verwendet werden, Messungsregeln erstellt werden. Außerdem können Sie die auf dem Standort maximal zulässige Anzahl von automatisch generierten Softwaremessungsregeln angeben.

> [!NOTE]
>  Automatisch erzeugte Softwaremessungsregeln sind standardmäßig deaktiviert. Zum Sammeln von Nutzungsdaten über diese Regeln müssen die Regeln erst aktiviert wurden.

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** > **Softwaremessung** und anschließend auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** auf **Softwaremessungseigenschaften**.

3.  Konfigurieren Sie im Dialogfeld **Softwaremessungseigenschaften** die folgenden Optionen:

    -   **Beibehaltung der Daten (Tage)** : Gibt an, wie lange die von den Softwaremessungsregeln generierten Daten in der Standortdatenbank gespeichert werden. Der Standardwert ist **90** Tage.

    -   Aktivieren Sie die Option **Deaktivierte Messungsregeln automatisch aus den Inventurdaten für die letzte Verwendung erstellen**.

    -   **Den Prozentsatz der Computer in der Hierarchie angeben, auf denen ein Programm verwendet werden muss, bevor eine Softwaremessungsregel automatisch erstellt wird** – Der Standardwert ist **10** Prozent.

    -   **Anzahl von Softwaremessungsregeln angeben, die überschritten werden muss, bevor die automatische Erstellung von Regeln deaktiviert wird** – Der Standardwert ist **100** Regeln.

4.  Klicken Sie zum Schließen des Dialogfelds **Softwaremessungseigenschaften** auf **OK** .

##  <a name="manage-software-metering-rules"></a>Verwalten von Softwaremessungsregeln
 Wählen Sie im Arbeitsbereich **Bestand und Kompatibilität** die Option **Softwaremessung**aus, markieren Sie die zu verwaltende Softwaremessungsregel, und wählen Sie dann einen Verwaltungstask aus.

 In der nachfolgenden Tabelle finden Sie weitere Informationen zu den Verwaltungstasks, für die möglicherweise einige Informationen benötigt werden, bevor Sie sie auswählen.

|Verwaltungstask|Details|
|---------------------|-------------|
|**Aktivieren**<br /><br /> **Deaktivieren**|Aktiviert bzw. deaktiviert eine Softwaremessungsregel. Diese Einstellung wird auf Clientcomputer gemäß dem **Clientrichtlinien-Abrufintervall** im Abschnitt **Clientrichtlinie** der Clienteinstellungen (standardmäßig alle 60 Minuten) heruntergeladen.<br /><br /> Weitere Informationen finden Sie unter [Configure client settings (Konfigurieren von Clienteinstellungen)](../../core/clients/deploy/configure-client-settings.md).|

##  <a name="monitor-software-metering"></a>Überwachen der Softwaremessung
 Die Softwaremessung in Configuration Manager umfasst mehrere integrierte Berichte, die das Überwachen der Daten von Softwaremessvorgängen erlauben. Die Berichte gehören zur Berichtkategorie **Softwaremessung**.

 Weitere Informationen zum Konfigurieren der Berichterstellung in Configuration Manager finden Sie unter [Einführung in die Berichterstellung](../../core/servers/manage/introduction-to-reporting.md).

 Außerdem können Abfragen und Sammlungen auf Basis der Daten erstellt werden, die bei der Softwaremessung in der Configuration Manager-Datenbank gespeichert wurden.

 Weitere Informationen zu Sammlungen in Configuration Manager finden Sie unter [Introduction to collections (Einführung in Sammlungen)](../../core/clients/manage/collections/introduction-to-collections.md).

 Weitere Informationen zu Abfragen in Configuration Manager finden Sie unter [Introduction to queries (Einführung in Abfragen)](../../core/servers/manage/introduction-to-queries.md).

##  <a name="security-and-privacy-for-software-metering"></a>Sicherheit und Datenschutz für die Softwaremessung

### <a name="security-issues-for-software-metering"></a>Sicherheitsprobleme bei der Softwaremessung
 Ein Angreifer könnte ungültige Softwaremessungsinformationen an Configuration Manager senden. Diese werden vom Verwaltungspunkt auch dann akzeptiert, wenn die Softwaremessung-Clienteinstellung deaktiviert ist. Dies könnte dazu führen, dass sehr viele Messungsregeln in der gesamten Hierarchie repliziert werden, was zu einem DoS im Netzwerk und auf den Configuration Manager-Standortservern führen würde.

 Da ein Angreifer ungültige Softwaremessungsdaten erstellen kann, sollten Sie Softwaremessungsinformationen nicht als autoritative Informationen betrachten.

 Die Softwaremessung ist standardmäßig als Clienteinstellung aktiviert.

###  <a name="privacy-information-for-software-metering"></a>Informationen zum Datenschutz für die Softwaremessung
 Die Softwaremessung überwacht die Anwendungsnutzung auf Clientcomputern. Diese Option ist standardmäßig aktiviert. Sie müssen konfigurieren, welche Anwendungen gemessen werden sollen. Messungsinformationen werden in der Configuration Manager-Datenbank gespeichert. Die Informationen werden beim Übertragen an einen Verwaltungspunkt verschlüsselt, aber in nicht verschlüsselter Form in der Configuration Manager-Datenbank gespeichert.

 Diese Informationen bleiben in der Datenbank, bis sie von den Standortwartungstasks **Veraltete Softwaremessungsdaten löschen** (alle fünf Tage) und **Veraltete Softwaremessungs-Zusammenfassungsdaten löschen** (alle 270 Tage) gelöscht werden. Sie können das Löschintervall konfigurieren. Die Messungsinformationen werden nicht an Microsoft gesendet.

 Berücksichtigen Sie beim Konfigurieren der Softwaremessung Ihre Datenschutzanforderungen.

## <a name="example-scenario-for-using-software-metering"></a>Beispielszenario für die Verwendung der Softwaremessung
 In diesem Abschnitt erstellen Sie eine Beispielregel für die Softwaremessung, mit der Sie die folgenden Unternehmensanforderungen erfüllen können:

- Feststellen, wie viele Kopien einer bestimmten App in Ihrem Unternehmen vorhanden sind

- Ermitteln nicht verwendeter Kopien einer App

- Feststellen, welche Benutzer eine bestimmte App regelmäßig verwenden

  Die Woodgrove Bank hat Microsoft Office 2010 als standardmäßiges Bürosoftwarepaket bereitgestellt. Allerdings muss zur Unterstützung einer älteren Anwendung auf einigen Computern weiterhin Microsoft Office Word 2003 ausgeführt werden. Zur Reduzierung der Support- und Lizenzkosten möchte die IT-Abteilung Kopien von Word 2003 entfernen, wenn die ältere Anwendung nicht mehr verwendet wird. Das Helpdesk möchte außerdem wissen, welche Benutzer die ältere Anwendung verwenden.

  Der IT-Systemmanager der Woodgrove Bank verwendet die Softwaremessung in Configuration Manager, um diese Unternehmensziele zu erreichen. Der Administrator führt die folgenden Aktionen aus:

- Er überprüft die Voraussetzungen für die Softwaremessung und vergewissert sich, dass der Reporting Services-Punkt installiert und betriebsbereit ist.
- Er konfiguriert die Clientstandardeinstellungen für die Softwaremessung:<br>Der Administrator aktiviert die Softwaremessung und verwendet die standardmäßige geplante Datensammlung alle sieben Tage.<br>Der Administrator konfiguriert die Softwareinventur für das Inventarisieren von Dateien mit der Erweiterung „.exe“, indem er die Clienteinstellung **Diese Dateitypen inventarisieren** für die Softwareinventur konfiguriert.<br>Der Administrator fügt eine neue Softwaremessungsregel mit dem Namen **woodgrove.exe** hinzu, mit der die ältere Anwendung überwacht werden soll.
- Er wartet sieben Tage. Danach beginnen die Clientcomputer, die Nutzungsdaten für die ausführbare Datei **woodgrove.exe** zu melden.
- Der Administrator ermittelt anhand des Configuration Manager-Berichts **Installationsbasis für alle gemessenen Softwareprogramme**, welche Computer die Anwendung **woodgrove.exe** geladen haben.
- Nach 6 Monaten führt der Administrator den Bericht **Computer, auf denen ein gemessenes Programm installiert ist, das aber seit dem angegebenen Datum nicht mehr ausgeführt wurde** unter Angabe der Softwaremessungsregel und eines 6 Monate zurückliegenden Datums aus. In diesem Bericht sind 120 Computer angegeben, die das Programm in den letzten 6 Monaten nicht ausgeführt haben.
- Der Administrator nimmt einige weitere Prüfungen vor, um sicherzustellen, dass die ältere Anwendung auf den ermittelten Computern nicht erforderlich ist. Dann deinstalliert der Administrator die ältere Anwendung und die Kopie von Word 2003 auf diesen Computern.<br>Der Administrator führt den Bericht **Benutzer, die ein bestimmtes gemessenes Softwareprogramm ausgeführt haben** aus, um dem Helpdesk eine Liste von Benutzern bereitzustellen, die die ältere Anwendung weiterhin verwenden.
- Der Administrator prüft weiterhin wöchentlich die Softwaremessungsberichte und führt bei Bedarf Abhilfemaßnahmen durch.

  Als Resultat dieser Vorgehensweise werden durch das Entfernen der nicht mehr benötigten Anwendungen die Kosten für IT-Support und Lizenzen gesenkt. Darüber hinaus verfügt das Helpdesk jetzt über die gewünschte Liste der Benutzer, die die ältere Anwendung ausführen.
