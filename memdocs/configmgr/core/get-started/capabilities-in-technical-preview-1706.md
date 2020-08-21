---
title: Technical Preview 1706
titleSuffix: Configuration Manager
description: Erfahren Sie mehr zu Features, die in Technical Preview für Configuration Manager-Version 1706 zur Verfügung stehen.
ms.date: 09/15/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ca3b4714-2a16-495e-8a17-1d87991d5556
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 8c3624f9fc903395b36846170ff3552f32db59dd
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88692943"
---
# <a name="capabilities-in-technical-preview-1706-for-configuration-manager"></a>Funktionen in der Technical Preview 1706 für Configuration Manager

*Gilt für: Configuration Manager (Technical Preview-Branch)*

In diesem Artikel werden die Features vorgestellt, die in der Technical Preview-Version 1706 für Configuration Manager verfügbar sind. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen. Bevor Sie diese Technical Preview-Version installieren, lesen Sie [Technical Preview für Configuration Manager](../../core/get-started/technical-preview.md), um sich mit den allgemeinen Anforderungen und Einschränkungen bei der Verwendung einer Technical Preview-Version vertraut zu machen und zu erfahren, wie Sie Updates für Versionen durchführen und Feedback zu den Funktionen in einer Technical Preview-Version geben können.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
- **Issue Name**. Details
    Workaround details.
-->
**Bekannte Probleme in dieser Technical Preview:**

- **Verschieben eines Verteilungspunkts**: Die Optionen in der Konsole zum Verschieben eines Verteilungspunkts zwischen Standorten können in dieser Version aufgrund der Beschränkung der Technical Preview auf einen einzigen primären Standort nicht genutzt werden.

- **Gerätekonformitätseinstellungen**: Bei Verwenden der beiden neuen Gerätekonformitätseinstellungen kann das entgegengesetzte Verhalten auftreten:
  - **USB-Debugging auf Gerät blockieren**
  - **Apps von unbekannten Quellen blockieren**

    Wenn Administratoren beispielsweise **USB-Debugging auf Gerät blockieren** auf **TRUE** festlegen, werden alle Geräte, für die USB-Debuggen nicht aktiviert ist, als nicht konform markiert.

**Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improved-boundary-groups-for-software-update-points"></a>Verbesserte Begrenzungsgruppen für Softwareupdatepunkte
<!-- 1324591 -->
Diese Version bietet Verbesserungen dahingehend, wie Softwareupdatepunkte mit Begrenzungsgruppen arbeiten. Im Folgenden wird das neue Ausweichverhalten zusammengefasst:
- Für Softwareupdatepunkte gibt es nun einen konfigurierbaren Zeitraum (mindestens 120 Minuten) für ein Ausweichen auf benachbarte Begrenzungsgruppen.

- Unabhängig von der Konfiguration des Ausweichens versucht ein Client, den letzten Softwareupdatepunkt zu erreichen, den er 120 Minuten verwendet hat. Sollte dieser Server in diesen 120 Minuten nicht erreicht werden, überprüft der Client seinen Pool verfügbarer Softwareupdatepunkte auf einen neuen.

  - Alle Softwareupdatepunkte in der aktuellen Begrenzungsgruppe des Clients werden dem Pool des Clients sofort hinzugefügt.

  - Da ein Client 120 Minuten versucht, seinen ursprünglichen Server zu nutzen, bevor er einen neuen sucht, werden zusätzliche Server erst kontaktiert, nachdem zwei Stunden verstrichen sind.

  - Wenn das Ausweichen zu einer Nachbargruppe mit dem Mindestzeitraum von 120 Minuten konfiguriert ist, gehören Softwareupdatepunkte aus dieser benachbarten Begrenzungsgruppe zum Pool verfügbarer Server des Clients.

- Nachdem der Client seinen ursprünglichen Server zwei Stunden nicht erreicht hat, wechselt er beim Kontaktieren eines neuen Softwareupdatepunkts zu einem kürzeren Zyklus.

  Wenn also ein Client keine Verbindung mit einem neuen Server herstellen kann, wählt er rasch den nächsten Server in seinem Pool verfügbarer Server aus und versucht, diesen zu kontaktieren.

  - Dieser Zyklus wird so lange fortgesetzt, bis der Client eine Verbindung mit einem Softwareupdatepunkt hergestellt hat, der verwendet werden kann.
  - Bis der Client einen Softwareupdatepunkt gefunden hat, werden dem Pool verfügbarer Server zusätzliche Server hinzugefügt, sobald die Ausweichzeit für jede benachbarte Begrenzungsgruppe erreicht ist.

Weitere Informationen finden Sie im Thema zu Begrenzungsgruppen unter [Softwareupdatepunkte](../servers/deploy/configure/boundary-groups.md#bkmk_sup) für den Current Branch.


## <a name="site-server-role-high-availability"></a>Hohe Verfügbarkeit der Standortserverrolle
<!-- 1128774 -->
Hohe Verfügbarkeit der Standortserverrolle ist eine auf Configuration Manager basierende Lösung zum Installieren eines weiteren primären Standortservers im *passiven* Modus. Der Standortserver im passiven Modus ist zusätzlich zu Ihrem primären Standortserver vorhanden, der sich im *aktiven* Modus befindet. Ein Standortserver im passiven Modus ist bei Bedarf sofort einsatzbereit.

Für einen primären Standortserver im passiven Modus gilt Folgendes:
- Verwendet die gleiche Standortdatenbank wie Ihr aktiver Standortserver.
- Empfängt eine Kopie der Inhaltsbibliothek des aktiven Standortservers, die synchron gehalten wird.
- Überschreibt keine Daten in der Standortdatenbank, solange er sich im passiven Modus befindet.
- Unterstützt nicht die Installation oder Entfernung optionaler Standortsystemrollen, solange er sich im passiven Modus befindet.

Um den Standortserver im passiven Modus zu Ihrem Standortserver im aktiven Modus zu machen, müssen Sie ihn manuell höher stufen. Dadurch wird der aktive Standortserver zum passiven Standortserver. Die Standortsystemrollen, die auf dem ursprünglichen Server im aktiven Modus verfügbar sind, bleiben verfügbar, solange auf diesen Computer zugegriffen werden kann. Nur die Standortserverrolle wird zwischen aktivem und passivem Modus umgeschaltet.

Um einen Standortserver im passiven Modus zu installieren, verwenden Sie den **Assistenten zum Erstellen von Standortsystemservern**, um einen neuen Standortserver des Typs **Primärer Standortserver** und mit dem Modus **Passiv** zu konfigurieren. Der Assistent führt dann das Configuration Manager-Setup auf dem angegebenen Server aus, um den neuen Standortserver im passiven Modus zu installieren. Nach Abschluss der Installation hält der Standortserver im aktiven Modus den Standortserver im passiven Modus und dessen Inhaltsbibliothek mit Änderungen oder Konfigurationen synchron, die Sie auf dem aktiven Standortserver vornehmen.

### <a name="prerequisites-and-limitations"></a>Voraussetzungen und Einschränkungen
- Ein einzelner Standortserver im passiven Modus wird an jedem primären Standort unterstützt.

- Der Standortserver im passiven Modus kann entweder lokal oder in der Azure-Cloud vorhanden sein.

- Die Standortserver im aktiven und passiven Modus müssen sich in derselben Domäne befinden.

- Die Standortserver im aktiven und passiven Modus müssen dieselbe Standortdatenbank verwenden, die für die Computer der einzelnen Standortserver remote sein muss.

    - Die SQL-Server-Instanz, die die Datenbank hostet, kann eine Standardinstanz, benannte Instanz, einen SQL Server-Cluster oder eine Always On-Verfügbarkeitsgruppe verwenden.

    - Der Standortserver im passiven Modus ist für die Verwendung der gleichen Datenbank wie der Standortserver im aktiven Modus konfiguriert. Doch der Standortserver im passiven Modus verwendet diese Datenbank erst, nachdem er in den aktiven Modus höher gestuft wurde.

- Für den Computer, auf dem der Standortserver im passiven Modus ausgeführt wird, gilt Folgendes:

    - Muss die [Voraussetzungen für die Installation eines primären Standorts](/sccm/core/servers/deploy/install/prerequisites-for-installing-sites#primary-sites-and-the-central-administration-site) erfüllen.

    - Wird mit Quelldateien installiert, deren Version der des Standortservers im aktiven Modus entsprechen.

    - Kann vor der Installation des Standorts im passiven Modus keine Standortsystemrollen eines beliebigen Standorts aufweisen.

- Die Standortservercomputer im aktiven und passiven Modus können mit verschiedenen Betriebssystemen oder Service Pack-Versionen ausgeführt werden, solange diese von Ihrer Version von Configuration Manager unterstützt werden.

- Das Höherstufen des Standortservers im passiven Modus zum Server im aktiven Modus erfolgt manuell. Es findet kein automatisches Failover statt.

- Standortsystemrollen können nur auf dem Standortserver installiert werden, der sich im aktiven Modus befindet.

    - Ein Standortserver im aktiven Modus unterstützt alle Standortsystemrollen. Sie können Standortsystemrollen nicht auf einem Server im passiven Modus installieren.

    - Bei Standortsystemrollen, die eine Datenbank (z.B. für den Berichterstattungspunkt) verwenden, muss sich die Datenbank auf einem Server befinden, der für die Standortserver im aktiven und passiven Modus remote ist.

    - Der SMS-Anbieter wird nicht auf dem Standortserver im passiven Modus installiert. Da Sie für das manuelle Höherstufen des Standortserver vom passiven in den aktiven Modus eine Verbindung mit einem SMS-Anbieter herstellen müssen, empfehlen wir das [Installieren von mindestens einer zusätzlichen Instanz des Anbieters](../plan-design/hierarchy/plan-for-the-sms-provider.md) auf einem zusätzlichen Computer.

**Bekanntes Problem**:   
Bei dieser Version wird der **Status** der folgenden Bedingungen in der Konsole als numerischer Wert anstatt als lesbarer Text angezeigt:
- 131071: Fehler bei der Installation des Standortservers
- 720895: Fehler bei der Deinstallation der Standortserverrolle
- 851967: Fehler beim Failover

### <a name="add-a-site-server-in-passive-mode"></a>Hinzufügen eines Standortservers im passiven Modus
1. Wechseln Sie in der Konsole zu **Verwaltung** > **Standortkonfiguration** > **Standorte**, und starten Sie den [Assistenten zum Hinzufügen von Standortsystemrollen](../servers/deploy/configure/install-site-system-roles.md). Sie können auch den **Assistenten zum Erstellen von Standortsystemservern** verwenden.

2. Geben Sie auf der Seite **Allgemein** den Server an, der den Standortserver im passiven Modus hostet. Der Server, den Sie angeben, kann Standortsystemrollen erst dann hosten, nachdem ein Standortserver im passiven Modus installiert wurde.

3. Wählen Sie auf der Seite **Systemrollenauswahl** nur **Primärer Standortserver im passiven Modus** aus.

4. Zum Abschließen des Assistenten müssen Sie die folgenden Informationen bereitstellen, die verwendet werden, um das Setup auszuführen und die Standortserverrolle auf dem angegebenen Server zu installieren:
    - Wählen Sie die Option zum Kopieren der Installationsdateien vom aktiven Standortserver auf den neuen Standortserver im passiven Modus, oder geben Sie einen Pfad zu einem Speicherort an, der den Inhalt des Ordners **CD.Latest** des aktiven Standortservers enthält.

    - Geben Sie den gleichen Standortdatenbankserver- und Datenbanknamen an, der vom Standortserver im aktiven Modus verwendet wird.

5. Configuration Manager installiert dann den Standortserver im passiven Modus auf dem angegebenen Server.

Detaillierte Informationen zum Installationsstatus finden Sie unter **Verwaltung** > **Standortkonfiguration** > **Standorte**.
- Der Status des Standortservers im passiven Modus wird als **Wird installiert** angezeigt.

- Wählen Sie den Server aus, und klicken Sie dann auf **Status anzeigen**, um die Seite mit dem **Status der Standortserverinstallation** mit detaillierteren Informationen zu öffnen.



### <a name="promote-the-passive-mode-site-server-to-active-mode"></a>Höherstufen des Standortservers im passiven Modus in den aktiven Modus
Wenn Sie den Standortserver im passiven Modus in den aktiven Modus ändern möchten, wechseln Sie unter **Verwaltung** > **Standortkonfiguration** > **Standorte** zum Bereich **Knoten**. Solange Sie Zugriff auf eine Instanz des SMS-Anbieters haben, können Sie auf den Standort zugreifen, um diese Änderung vorzunehmen.
1. Wählen Sie in der Configuration Manager-Konsole im Bereich **Knoten** den Standortserver im passiven Modus aus, und klicken Sie dann im Menüband auf **In den aktiven Modus höher stufen**.

2. Der einfache **Status** des Servers, den Sie höher stufen, wird im Bereich **Knoten** als **Wird höher gestuft** angezeigt.

3. Nach Abschluss der Höherstufung wird **OK** in der Spalte **Status** für sowohl den neuen Standortserver im Modus *Aktiv* als auch für den neuen Standortserver im Modus *Passiv* angezeigt.

4. Unter **Verwaltung** > **Standortkonfiguration** > **Standorte** wird der Name des primären Standortservers jetzt als der Name des neuen Standortservers im Modus *Aktiv* angezeigt.
Ausführliche Statusinformationen finden Sie unter **Überwachung** > **Status des Standortservers**.
    - Die Spalte **Modus** gibt an, welcher Server *Aktiv* oder *Passiv* ist.

    - Wählen Sie beim Höherstufen eines Servers aus dem passiven in den aktiven Modus den Standortserver aus, den Sie auf aktiv höher stufen, und klicken Sie dann im Menüband auf **Status anzeigen**. Daraufhin wird das Fenster mit dem **Status der Höherstufung des Standortservers** mit zusätzlichen Details zum Prozess angezeigt.

Wenn ein Standortserver im aktiven Modus in den passiven Modus wechselt, ändert sich nur die Standortsystemrolle in passiv. Alle anderen Standortsystemrollen, die auf diesem Computer installiert sind, bleiben aktiv, sodass Clients weiter Zugriff darauf haben.


### <a name="daily-monitoring"></a>Tägliche Überwachung
Wenn Sie über einen primären Standort im passiven Modus verfügen, überwachen Sie diesen täglich, um sicherzustellen, dass er mit dem Standortserver im aktiven Modus synchron und einsatzbereit bleibt. Wechseln Sie hierfür zu **Überwachung** > **Status des Standortservers**. Hier können Sie sowohl den Standortserver im aktiven als auch den Standortserver im passiven Modus überprüfen.

Inhalt der Registerkarte **Zusammenfassung**:
- Die Spalte **Modus** gibt an, welcher Server „Aktiv“ oder „Passiv“ ist.
- Die Spalte **Status** enthält **OK**, wenn der Server im passiven Modus mit dem Server im aktiven Modus synchron ist.
- Um zusätzliche Details zum Status der Inhaltssynchronisierung anzuzeigen, klicken Sie in „Status der Inhaltssynchronisierung“ auf **Status anzeigen**. Daraufhin wird die Registerkarte „Inhaltsbibliothek“ geöffnet, auf der Sie versuchen können, Probleme bei der Synchronisierung von Inhalten zu beheben.

Inhalt der Registerkarte **Inhaltsbibliothek**:
- In der Spalte **Status** finden Sie Inhalte, die vom aktiven Standortserver auf den Standortserver im passiven Modus synchronisiert werden.
- Sie können Inhalt mit dem Status **Fehler** auswählen und dann im Menüband **Ausgewählte Elemente synchronisieren** wählen. Diese Aktion versucht eine erneute Synchronisierung dieses Inhalts aus der Quelle des Inhalts auf den Standortserver im passiven Modus. Während der Wiederherstellung wird der Status als **In Bearbeitung** und bei Synchronität als **Erfolg** angezeigt.

### <a name="try-it-out"></a>Probieren Sie es aus!
Versuchen Sie, die folgenden Aufgaben auszuführen, und senden Sie uns dann **Feedback** über die Registerkarte **Start** des Menübands, um uns zu wissen zu lassen, wie es funktioniert hat:
- Ich kann einen primären Standort im passiven Modus installieren.
- Ich kann mithilfe der Konsole den Standortserver im passiven Modus zum Standortserver im aktiven Modus höher stufen und die Änderung des Status für beide Standortserver bestätigen.


## <a name="include-trust-for-specific-files-and-folders-in-a-device-guard-policy"></a>Einbeziehen einer Vertrauensstellung für bestimmte Dateien und Ordner in eine Device Guard-Richtlinie
<!-- 1324676 -->
In diesem Release haben wir der [Device Guard](../../protect/deploy-use/use-device-guard-with-configuration-manager.md)-Richtlinienverwaltung weitere Funktionen hinzugefügt.

Sie können jetzt einer Device Guard-Richtlinie optional eine Vertrauensstellung für bestimmte Dateien oder Ordner hinzufügen. Dies ermöglicht Ihnen Folgendes:

1. Beheben von Problemen mit dem Verhalten verwalteter Installationsprogramme
2. Vertrauen branchenspezifischer Apps, die nicht mit Configuration Manager bereitgestellt werden können
3. Vertrauen von Apps, die in einem Betriebssystemabbild für ein Betriebssystem enthalten sind

### <a name="try-it-out"></a>Probieren Sie es aus!

1. Klicken Sie beim Erstellen einer Device Guard-Richtlinie im Assistenten zum Erstellen von Device Guard-Richtlinien auf der Registerkarte „Einschlüsse“ auf **Hinzufügen**.
2. Geben Sie im Dialogfeld **Vertrauenswürdige Dateien oder Ordner hinzufügen** Informationen zur Datei bzw. zum Ordner an, der bzw. dem vertraut werden soll. Sie können einen lokalen Datei- oder Ordnerpfad angeben oder eine Verbindung mit einem Remotegerät herstellen, für das Sie über eine entsprechende Berechtigung verfügen, und einen Datei- oder Ordnerpfad auf diesem Gerät angeben.
3. Schließen Sie den Assistenten ab.


## <a name="hide-task-sequence-progress"></a>Ausblenden des Tasksequenzstatus
<!-- 1354291 -->
In dieser Version können Sie mithilfe einer neuen Variablen steuern, wann Endbenutzern der Tasksequenzstatus angezeigt wird. Verwenden Sie in der Tasksequenz den Schritt **Tasksequenzvariable festlegen** zum Festlegen des Werts der Variablen **TSDisableProgressUI**, um den Tasksequenzstatus ein- oder auszublenden. Den Schritt „Tasksequenzvariable festlegen“ können Sie in einer Tasksequenz mehrmals verwenden, um den Wert der Variablen zu ändern. Dadurch können Sie den Tasksequenzstatus in unterschiedlichen Abschnitten der Tasksequenz anzeigen oder ausblenden.

#### <a name="to-hide-task-sequence-progress"></a>So blenden Sie den Tasksequenzstatus aus
Verwenden Sie im Tasksequenz-Editor den Schritt [Tasksequenzvariable festlegen](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) zum Festlegen des Werts der Variablen **TSDisableProgressUI** auf **TRUE**, um den Tasksequenzstatus auszublenden.

#### <a name="to-display-task-sequence-progress"></a>So zeigen Sie den Tasksequenzstatus an
Verwenden Sie im Tasksequenz-Editor den Schritt [Tasksequenzvariable festlegen](../../osd/understand/task-sequence-steps.md#BKMK_SetTaskSequenceVariable) zum Festlegen des Werts der Variablen **TSDisableProgressUI** auf **FALSE**, um den Tasksequenzstatus anzuzeigen.

## <a name="specify-a-different-content-location-for-install-content-and-uninstall-content"></a>Angeben eines unterschiedlichen Inhaltsspeicherorts für zu installierende und zu deinstallierende Inhalte
<!-- 1097546 -->
Derzeit geben Sie im Configuration Manager den Installationsspeicherort an, der die Setupdateien einer App enthält. Wenn Sie einen Installationsspeicherort angeben, wird dieser auch als Speicherort für die Deinstallation des Anwendungsinhalts verwendet.
Basierend auf Ihrem Feedback gilt Folgendes: Wenn Sie eine bereitgestellte Anwendung deinstallieren möchten und sich deren Inhalt nicht auf dem Clientcomputer befindet, lädt der Client alle Setupdateien der App erneut herunter, ehe die Anwendung deinstalliert wird.
Um dieses Problem zu beheben, können Sie jetzt sowohl einen Speicherort für zu installierenden Inhalt und optional einen Speicherort für zu deinstallierenden Inhalt angeben. Sie können darüber hinaus auch auf das Angeben eines Speicherorts für zu deinstallierenden Inhalt verzichten.

### <a name="try-it-out"></a>Probieren Sie es aus!

1. Klicken Sie in den Eigenschaften des Bereitstellungstyps der Anwendung auf die Registerkarte **Inhalt**.
2. Konfigurieren Sie den **Speicherort für zu installierenden Inhalt** wie gewohnt.
3. Wählen Sie für **Einstellungen für zu deinstallierenden Inhalt** eine der folgenden Optionen aus:
   - **Übereinstimmend mit zu installierendem Inhalt**: Unabhängig davon, ob Sie die Anwendung installieren oder deinstallieren, wird derselbe Inhaltsspeicherort verwendet.
   - **Nicht zu deinstallierender Inhalt**: Wählen Sie diese Option, wenn Sie für die Anwendung keinen Speicherort für zu deinstallierenden Inhalt angeben möchten.
   - **Abweichend von zu installierendem Inhalt**: Wählen Sie diese Option, wenn Sie einen Speicherort für zu deinstallierenden Inhalt angeben möchten, der sich vom Speicherort für zu installierenden Inhalt unterscheidet.
5. Wenn Sie **Abweichend von zu installierendem Inhalt** ausgewählt haben, können Sie zum Speicherort des Anwendungsinhalts navigieren oder diesen eingeben, der zum Deinstallieren der Anwendung verwendet wird.
6. Klicken Sie auf **OK**, um das Dialogfeld zu Bereitstellungstyp-Eigenschaften zu schließen.


## <a name="accessibility-improvements"></a>Verbesserungen der Barrierefreiheit  
<!--1253000 -->
Diese Vorschauversion bietet mehrere Verbesserungen der [Barrierefreiheitsfunktionen](../understand/accessibility-features.md) in der Configuration Manager-Konsole. Dazu gehören:     

**Neue Tastenkombinationen, um sich in der Konsole zu bewegen:**
- STRG+M: Legt den Fokus auf den Hauptbereich in der Mitte fest.
- STRG+T: Legt den Fokus auf den obersten Knoten im Navigationsbereich fest. Wenn sich der Fokus bereits in diesem Bereich befand, wird er auf den letzten besuchten Knoten festgelegt.
- STRG+I: Legt den Fokus auf die Breadcrumb-Leiste unter dem Menüband fest.
- STRG+L: Legt den Fokus auf das Feld **Suchen** fest, sofern verfügbar.
- STRG+D: Legt den Fokus auf den Detailbereich fest, sofern verfügbar.
- ALT-TASTE: Schaltet den Fokus auf das Menüband ein und aus.

**Allgemeine Verbesserungen:**
- Verbesserte Navigation im Navigationsbereich, wenn Sie die Buchstaben eines Knotennamens eingeben.
- Die Tastaturnavigation durch die Hauptansicht und das Menüband erfolgt jetzt kreisförmig.
- Die Tastaturnavigation im Detailbereich erfolgt jetzt kreisförmig. Um zum vorherigen Objekt oder Bereich zurückzukehren, drücken Sie STRG+D und dann UMSCHALT+TAB.
- Nach der Aktualisierung einer Arbeitsbereichsansicht wird der Fokus auf den Hauptbereich des jeweiligen Arbeitsbereichs festgelegt.
- Ein Problem beim Aktivieren von Sprachausgaben zum Mitteilen der Namen von Listenelementen wurde behoben.
- Es wurden barrierefreie Namen für mehrere Steuerelemente auf der Seite hinzugefügt, die es Sprachausgaben ermöglichen, wichtige Informationen mitzuteilen.


## <a name="changes-to-the-azure-services-wizard-to-support-upgrade-readiness"></a>Änderungen am Assistenten für Azure-Dienste zur Unterstützung der Funktion „Upgradebereitschaft“
<!-- 1353331 -->
Ab diesem Release wird der Assistent für Azure-Dienste zum Konfigurieren einer Verbindung zwischen Configuration Manager und Upgradebereitschaft verwendet. Die Verwendung des Assistenten vereinfacht die Konfiguration des Connectors durch Nutzen eines allgemeinen Assistenten für verwandte Azure-Dienste.   

Obwohl die Methode zum Konfigurieren der Verbindung geändert wurde, bleiben die Voraussetzungen für die Verbindung mit und zur Verwendung von Upgradebereitschaft unverändert.   

### <a name="prerequisites-for-upgrade-readiness"></a>Voraussetzungen für Upgradebereitschaft
Die Voraussetzungen für eine Verbindung mit der Upgradebereitschaft unterscheiden sich nicht von denen, die für den aktuellen Branch von Configuration Manager gelten. Sie werden hier der Einfachheit halber wiederholt:  

**Voraussetzungen**
- Um der Configuration Manager-Umgebung eine Verbindung hinzuzufügen, müssen Sie zunächst einen [Dienstverbindungspunkt](../servers/deploy/configure/about-the-service-connection-point.md) in einem [Onlinemodus](../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes) konfigurieren. Wenn Sie Ihrer Umgebung eine Verbindung hinzufügen, wird auch der Microsoft Monitoring Agent auf dem Computer installiert, auf dem die Standortsystemrolle ausgeführt wird.
- Registrieren Sie Configuration Manager als „Webanwendung und/oder Web-API”-Verwaltungstool, und rufen Sie die [Client-ID dieser Registrierung](/azure/active-directory/develop/quickstart-register-app) ab.
- Erstellen Sie für das registrierte Verwaltungstool in Azure Active Directory einen Clientschlüssel.
- Geben Sie im Azure-Portal die registrierte Web-App mit Zugriffsberechtigung für die OMS an.

> [!IMPORTANT]       
> Achten Sie beim Konfigurieren der OMS-Zugriffsberechtigung darauf, dass Sie die Rolle **Mitwirkender** auswählen, und weisen Sie ihr Berechtigungen für die Ressourcengruppe der registrierten App zu.

Sobald die Voraussetzungen erfüllt sind, können Sie mithilfe des Assistenten die Verbindung herstellen.

### <a name="use-the-azure-services-wizard-to-configure-upgrade-readiness"></a>Konfigurieren von Upgradebereitschaft mit dem Assistenten für Azure-Dienste
1. Wechseln Sie in der Konsole zu **Verwaltung** > **Übersicht** > **Clouddienste** > **Azure-Dienste**, und wählen Sie dann **Azure-Dienste konfigurieren** auf der Registerkarte **Start** im Menüband aus, um den **Assistenten für Azure-Dienste** zu starten.

2. Wählen Sie auf der Seite **Azure-Dienste** den **Connector für Upgradebereitschaft** aus, und klicken Sie dann auf **Weiter**.

3. Geben Sie auf der Seite **App** Ihre **Azure-Umgebung** an (die Technical Preview unterstützt nur die öffentliche Cloud). Klicken Sie dann auf **Importieren**, um das Fenster **Apps importieren** zu öffnen.

4. Geben Sie im Fenster **Apps importieren** Details einer Web-App an, die bereits in Ihrem Azure Active Directory (AD) vorhanden ist.
    - Geben Sie einen Anzeigenamen für den Azure AD-Mandantennamen an. Geben Sie dann die Mandanten-ID, den Anwendungsnamen, die Client-ID, den geheimen Schlüssel für die Azure-Web-App und den App-ID-URI an.
    - Klicken Sie auf **Überprüfen** und, sofern erfolgreich, auf **OK**, um den Vorgang fortzusetzen.

5.  Geben Sie auf der Seite **Konfiguration** das Abonnement, die Ressourcengruppe und den Windows Analytics-Arbeitsbereich an, den Sie für diese Verbindung mit Upgradebereitschaft verwenden möchten.  

6. Klicken Sie auf **Weiter**, um zur Seite **Zusammenfassung** zu gelangen. Schließen Sie dann den Assistenten ab, um die Verbindung herzustellen.


## <a name="new-client-settings-for-cloud-services"></a>Neue Clienteinstellungen für Clouddienste
<!-- 1319883 -->

In dieser Version haben wir Configuration Manager zwei neue Clienteinstellungen hinzugefügt. Sie finden diese im Abschnitt **Clouddienste**.  Diese Einstellungen bieten Ihnen folgende Möglichkeiten:

- Steuern, welche Configuration Manager-Clients auf ein konfiguriertes Cloud Management Gateway zugreifen können.
- Automatisches Registrieren von einer Windows 10-Domäne beigetretenen Configuration Manager-Clients bei Azure Active Directory.

Diese neuen Einstellungen helfen Ihnen beim Realisieren der in [Technical Preview 1705 von Configuration Manager](capabilities-in-technical-preview-1705.md#new-capabilities-for-azure-ad-and-cloud-management) beschriebenen Möglichkeiten.

### <a name="before-you-start"></a>Vorbereitung

Azure AD Connect muss zwischen Ihrem lokalen Active Directory und Ihrem Azure AD-Mandanten installiert und konfiguriert sein.

Wenn Sie die Verbindung entfernen, wird die Registrierung von Geräten nicht aufgehoben, aber neue Geräte können sich nicht registrieren.

### <a name="try-it-out"></a>Probieren Sie es aus!

1. Konfigurieren Sie die folgenden Clienteinstellungen im Abschnitt „Clouddienste“ anhand der Informationen in [Konfigurieren von Clienteinstellungen in System Center Configuration Manager](../clients/deploy/configure-client-settings.md).
   - **Automatische Registrierung neuer einer Windows 10-Domäne beigetretener Geräte mit Azure Active Directory**: Legen Sie diese Option auf **Ja** (Standard) oder **Nein** fest.
   - **Clients die Verwendung eines Cloudverwaltungsgateways ermöglichen**: Legen Sie diese Option auf **Ja** (Standard) oder **Nein** fest.
2. Stellen Sie die Clienteinstellungen in der gewünschten Sammlung von Geräten bereit.

Um zu bestätigen, dass das Gerät Azure AD beigetreten ist, führen Sie in einem Eingabeaufforderungsfenster **dsregcmd.exe /status** aus. Im Feld **AzureAdjoined** in den Ergebnissen wird **YES** angezeigt, wenn das Gerät Azure AD beigetreten ist.

## <a name="create-and-run-powershell-scripts-from-the-configuration-manager-console"></a>Erstellen und Ausführen von PowerShell-Skripts über die Configuration Manager-Konsole
<!-- 1236459 -->

In Configuration Manager können Sie mithilfe von Paketen und Programmen Skripts auf Clientgeräten bereitstellen. In dieser Technical Preview haben wir neue Funktionen hinzugefügt, mit denen Sie die folgenden Aktionen ausführen können:

- Importieren von PowerShell-Skripts in Configuration Manager
- Bearbeiten von Skripts in der Configuration Manager-Konsole (nur bei nicht signierten Skripts)
- Markieren von Skripts als „Genehmigt“ oder „Abgelehnt“ zum Verbessern der Sicherheit
- Anwenden von Skripts auf Sammlungen von Windows-Client-PCs und lokal verwaltete Windows-PCs. Sie stellen Skripts nicht bereit, sondern diese werden stattdessen nahezu in Echtzeit auf Clientgeräten ausgeführt.
- Überprüfen der Ergebnisse, die vom Skript in der Configuration Manager-Konsole zurückgegeben werden


### <a name="prerequisites"></a>Voraussetzungen

Um Skripts zu verwenden, müssen Sie Mitglied der entsprechenden Configuration Manager-Sicherheitsrolle sein.

- **Importieren und Erstellen von Skripts**: Ihr Konto benötigt in der Sicherheitsrolle **Hauptadministrator** die Berechtigung **Erstellen** für **SMS-Skripts**.
- **Genehmigen und Ablehnen von Skripts**: Ihr Konto benötigt in der Sicherheitsrolle **Hauptadministrator** die Berechtigung **Genehmigen** für **SMS-Skripts**.
- **Ausführen von Skripts**: Ihr Konto benötigt in der Sicherheitsrolle **Konformitätseinstellungs-Manager** die Berechtigung **Skript ausführen** für **Sammlungen**.

Weitere Informationen zu Configuration Manager-Sicherheitsrollen finden Sie unter [Grundlagen der rollenbasierten Verwaltung für System Center Configuration Manager](../understand/fundamentals-of-role-based-administration.md).

Standardmäßig können Benutzer kein Skript genehmigen, das sie erstellt haben. Da Skripts leistungsstark und vielseitig sind und auf vielen Geräten bereitgestellt werden können, haben wir ein neues Konzept eingeführt. Es bietet die Möglichkeit, die Rollen zwischen der Person, die das Skript erstellt, und der Person, die es genehmigt, zu trennen. Dies bietet einen zusätzlichen Grad an Sicherheit zum Verhindern des unbeaufsichtigten Ausführens eines Skripts. Sie können zur Vereinfachung von Tests diese sekundäre Genehmigung, insbesondere in der Technical Preview-Phase, deaktivieren.

So ermöglichen Sie Benutzern das Genehmigen ihrer eigenen Skripts

1. Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.
2. Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standortkonfiguration**, und klicken Sie dann auf **Standorte**.
3. Wählen Sie in der Liste der Standorte Ihren Standort aus, und klicken Sie dann auf der Registerkarte **Start** in der Gruppe **Standorte** auf **Hierarchieeinstellungen**.
4. Deaktivieren Sie im Dialogfeld **Eigenschaften von Hierarchieeinstellungen** auf der Registerkarte **Allgemein** das Kontrollkästchen **Skriptautoren nicht das Genehmigen ihrer eigenen Skripts erlauben**.


### <a name="try-it-out"></a>Probieren Sie es aus!

#### <a name="import-and-edit-a-script"></a>Importieren und Bearbeiten eines Skripts

1. Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.
2. Klicken Sie im Arbeitsbereich **Softwarebibliothek** auf **Skripts**.
3. Klicken Sie auf der Registerkarte **Start** in der Gruppe **Erstellen** auf **Skript erstellen**.
4. Konfigurieren Sie im Assistenten **Skript erstellen** auf der Seite **Skript** Folgendes:
   - **Skriptname**: Geben Sie einen Namen für das Skript ein. Obwohl Sie mehrere Skripts mit dem gleichen Namen erstellen können, wird dadurch das Auffinden des benötigten Skripts in der Configuration Manager-Konsole erschwert.
   - **Skriptsprache**: Derzeit werden nur **PowerShell**-Skripts unterstützt.
   - **Importieren**: Importieren Sie ein PowerShell-Skript in die Konsole. Das Skript wird im Feld **Skript** angezeigt.
   - **Löschen**: Entfernt das aktuelle Skript aus dem Feld **Skript**.
   - **Skript**: Zeigt das gerade importierte Skript. Sie können das Skript in diesem Feld nach Bedarf bearbeiten.
5. Schließen Sie den Assistenten ab. Das neue Skript wird in der Liste **Skript** mit dem Status **Warten auf Genehmigung** angezeigt. Bevor Sie dieses Skript auf Clientgeräten ausführen können, müssen Sie es genehmigen.


#### <a name="approve-or-deny-a-script"></a>Genehmigen oder Ablehnen eines Skripts



Bevor Sie ein Skript ausführen können, muss es genehmigt werden. So genehmigen Sie ein Skript

1. Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.
2. Klicken Sie im Arbeitsbereich **Softwarebibliothek** auf **Skripts**.
3. Wählen Sie in der Liste **Skript** das Skript, das Sie genehmigen oder ablehnen möchten. Klicken Sie dann in der Gruppe **Skript** auf der Registerkarte **Start** auf **Genehmigen/Ablehnen**.
4. Im Dialogfeld **Skript genehmigen oder ablehnen** können Sie das Skript **genehmigen** oder **ablehnen** und optional einen Kommentar zu Ihrer Entscheidung eingeben. Wenn Sie ein Skript ablehnen, kann es nicht auf Clientgeräten ausgeführt werden.
5. Schließen Sie den Assistenten ab. In der Liste **Skript** ändert sich die Spalte **Genehmigungsstatus** abhängig von der Aktion, die Sie durchgeführt haben.

#### <a name="run-a-script"></a>Ausführen eines Skripts

Nachdem ein Skript genehmigt wurde, kann es für die von Ihnen gewählte Sammlung ausgeführt werden.

1. Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.
2. Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Gerätesammlungen**.
3. Klicken Sie in der Liste **Gerätesammlungen** auf die Sammlung von Geräten, auf denen das Skript ausgeführt werden soll.
3. Klicken Sie auf der Registerkarte **Start** in der Gruppe **Alle Systeme** auf **Skript ausführen**.
4. Wählen Sie im Assistenten **Skript ausführen** auf der Seite **Skript** ein Skript in der Liste aus. Es werden nur genehmigte Skripts angezeigt. Klicken Sie auf **Weiter**, und schließen Sie den Assistenten ab.

#### <a name="monitor-a-script"></a>Überwachen eines Skripts

Nachdem Sie ein Skript auf Clientgeräten ausgeführt haben, gehen Sie wie folgt vor, um den Erfolg des Vorgangs zu überwachen.

1. Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.
2. Klicken Sie im Arbeitsbereich **Überwachung** auf **Skriptergebnisse**.
3. In der Liste **Skriptergebnisse** sehen Sie die Ergebnisse für jedes Skript, das Sie auf Clientgeräten ausgeführt haben. Der Exitcode **0** eines Skripts bedeutet im Allgemeinen, dass das Skript erfolgreich ausgeführt wurde.

## <a name="pxe-network-boot-support-for-ipv6"></a>PXE-Netzwerkstartunterstützung für IPv6
<!-- 1269793 -->
Sie können jetzt die PXE-Netzwerkstartunterstützung für IPv6 aktivieren, um eine Tasksequenz des Typs „Betriebssystembereitstellung“ zu starten. Bei Verwenden dieser Einstellung unterstützen PXE-fähige Verteilungspunkte sowohl IPv4 als auch IPv6. Diese Option erfordert nicht die Windows-Bereitstellungsdienste und beendet diese, sofern sie vorhanden sind.

#### <a name="to-enable-pxe-boot-support-for-ipv6"></a>So aktivieren Sie die PXE-Startunterstützung für IPv6
Gehen Sie wie folgt vor, um die IPv6-Unterstützung für PXE zu aktivieren.

1. Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Übersicht** > **Verteilungspunkte**, und klicken Sie für PXE-fähige Verteilungspunkte auf **Eigenschaften**.
2. Wählen Sie auf der Registerkarte **PXE** die Option **IPv6 unterstützen** aus, um die IPv6-Unterstützung für PXE zu aktivieren.

## <a name="manage-microsoft-surface-driver-updates"></a>Verwalten von Microsoft Surface-Treiberupdates
<!-- 1098490 -->
Sie können Configuration Manager jetzt zum Verwalten von Microsoft Surface-Treiberupdates verwenden.

### <a name="prerequisites"></a>Voraussetzungen
Auf allen Softwareupdatepunkten muss Windows Server 2016 ausgeführt werden.

### <a name="try-it-out"></a>Probieren Sie es aus!
Versuchen Sie, die folgenden Aufgaben auszuführen, und senden Sie uns dann **Feedback** über die Registerkarte **Start** des Menübands, um uns zu wissen zu lassen, wie es funktioniert hat:
1. Aktivieren Sie „Synchronisierung für Microsoft Surface-Treiber“. Befolgen Sie das Verfahren unter [Konfigurieren von Klassifizierung und Produkten](../../sum/get-started/configure-classifications-and-products.md), und wählen Sie auf der Registerkarte **Klassifizierungen** die Option **Microsoft Surface-Treiber und Firmwareupdates einbeziehen** aus, um Surface-Treiber zu aktivieren.
2. [Synchronisieren Sie die Microsoft Surface-Treiber](../../sum/get-started/synchronize-software-updates.md).
3. [Stellen Sie die synchronisierten Microsoft Surface-Treiber bereit](../../sum/deploy-use/deploy-software-updates.md).

## <a name="configure-windows-update-for-business-deferral-policies"></a>Konfigurieren von Windows Update for Business-Zurückstellungsrichtlinien
<!-- 1290890 -->
Sie können jetzt Zurückstellungsrichtlinien für Funktions- oder Qualitätsupdates für Windows 10 für Windows 10-Geräte konfigurieren, die von Windows Update for Business direkt verwaltet werden. Sie können die Zurückstellungsrichtlinien im neuen Knoten **Windows Update for Business-Richtlinien** unter **Softwarebibliothek** > **Windows 10-Wartung** verwalten.

### <a name="prerequisites"></a>Voraussetzungen
Windows 10-Geräte, die von Windows Update for Business verwaltet werden, benötigen Internetzugriff.

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Sie erstellen Sie eine Windows Update for Business-Zurückstellungsrichtlinie
1. In **Softwarebibliothek** > **Windows 10-Wartung** > **Windows Update for Business-Richtlinien**
2. Wählen Sie auf der Registerkarte **Start** in der Gruppe **Erstellen** die Option **Windows Update for Business-Richtlinie erstellen** aus, um den Assistenten für das Erstellen von Windows Update for Business-Richtlinien zu öffnen.
3. Geben Sie auf der Seite **Allgemein** einen Namen und eine Beschreibung für die Richtlinie ein.
4. Konfigurieren Sie auf der Seite **Zurückstellungsrichtlinien**, ob Sie Funktionsupdates zurückstellen oder anhalten möchten.    
    Funktionsupdates bieten in der Regel neue Funktionen für Windows. Nach dem Konfigurieren der Einstellung **Branchbereitschaftsniveau** können Sie dann festlegen, ob und wie lange Sie das Empfangen von Funktionsupdates zurückstellen möchten, sobald diese verfügbar sind.
    - **Branchbereitschaftsniveau:** Legen Sie den Branch fest, für den das Gerät Windows-Updates erhält (Current Branch oder Current Branch for Business).
    - **Zurückstellungszeitraum (Tage):**  Geben Sie die Anzahl der Tage an, die Funktionsupdates verzögert werden. Sie können den Empfang dieser Funktionsupdates für einen Zeitraum von 180 Tagen nach ihrer Veröffentlichung verzögern.
    - **Anhalten von Funktionsupdates ab:** Wählen Sie aus, ob Sie das Empfangen von Funktionsupdates für einen Zeitraum von bis zu 60 Tagen ab dem von Ihnen angegebenen Zeitpunkt anhalten möchten. Nach Ablauf der maximalen Anzahl von Tagen läuft die Anhaltefunktion automatisch ab, sodass das Gerät in Windows Update nach in Frage kommenden Updates sucht. Nach diesem Suchvorgang können Sie die Updates erneut anhalten. Sie können das Anhalten von Funktionsupdates beenden, indem Sie das Kontrollkästchen deaktivieren.   
5. Wählen Sie aus, ob Qualitätsupdates zurückgestellt oder angehalten werden sollen.     
    Qualitätsupdates sind meist Korrekturen und Verbesserungen an vorhandener Windows-Funktionalität und werden in der Regel am ersten Dienstag jedes Monats veröffentlicht, wenngleich sie jederzeit von Microsoft veröffentlicht werden können. Sie können festlegen, ob und wie lange Sie Qualitätsupdates nach deren Verfügbarkeit zurückstellen möchten.
    - **Zurückstellungszeitraum (Tage):** Geben Sie die Anzahl der Tage an, die Funktionsupdates verzögert werden. Sie können den Empfang dieser Funktionsupdates für einen Zeitraum von 180 Tagen nach ihrer Veröffentlichung verzögern.
    - **Anhalten von Qualitätsupdates ab:** Wählen Sie aus, ob Sie das Empfangen von Qualitätsupdates für einen Zeitraum von bis zu 35 Tagen ab dem von Ihnen angegebenen Zeitpunkt anhalten möchten. Nach Ablauf der maximalen Anzahl von Tagen läuft die Anhaltefunktion automatisch ab, sodass das Gerät in Windows Update nach in Frage kommenden Updates sucht. Nach diesem Suchvorgang können Sie die Updates erneut anhalten. Sie können das Anhalten von Qualitätsupdates beenden, indem Sie das Kontrollkästchen deaktivieren.
6. Wählen Sie **Updates aus anderen Microsoft-Produkten installieren** aus, um die Gruppenrichtlinieneinstellung zu aktivieren, mit deren Hilfe Zurückstellungseinstellungen auf Microsoft Update sowie auf Windows-Updates angewendet werden können.
7. Wählen Sie **Treiber in Windows-Updates einschließen** aus, um Treiber automatisch über Windows-Updates zu aktualisieren. Wenn Sie diese Einstellung deaktivieren, werden Treiberupdates nicht von Windows-Updates heruntergeladen.
8. Schließen Sie den Assistenten ab, um die neue Zurückstellungsrichtlinie zu erstellen.

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>So stellen Sie eine Windows Update for Business-Zurückstellungsrichtlinie bereit
1. In **Softwarebibliothek** > **Windows 10-Wartung** > **Windows Update for Business-Richtlinien**
2. Aktivieren Sie auf der Registerkarte **Start** in der Gruppe **Bereitstellung** die Option **Windows Update for Business-Richtlinie bereitstellen**.
3. Konfigurieren Sie die folgenden Einstellungen:
    - **Bereitzustellende Konfigurationsrichtlinie:** Wählen Sie die Windows Update for Business-Richtlinie aus, die Sie bereitstellen möchten.
    - **Sammlung:** Klicken Sie auf **Durchsuchen**, um die Sammlung auszuwählen, in der Sie die Richtlinie bereitstellen möchten.
    - **Nicht konforme Regeln wiederherstellen, falls dies unterstützt wird:** Wählen Sie diese Option aus, um Regeln automatisch wiederherzustellen, die nicht mit der Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI), der Registrierung, Skripts und sämtlichen Einstellungen für die von Configuration Manager registrierten mobilen Geräte konform sind.
    - **Wiederherstellung außerhalb des Wartungsfensters zulassen:** Wenn ein Wartungsfenster für die Sammlung konfiguriert wurde, für die Sie die Richtlinie bereitstellen, aktivieren Sie diese Option, um Konformitätseinstellungen zum Wiederherstellen des Werts außerhalb des Wartungsfensters zuzulassen. Weitere Informationen zu Wartungsfenstern finden Sie unter [Verwenden von Wartungsfenstern](../clients/manage/collections/use-maintenance-windows.md).
    - **Warnung generieren:** Konfiguriert eine Warnung, die generiert wird, sobald die Konformität einer Konfigurationsbaseline zu einem bestimmten Datum und einer bestimmten Uhrzeit unterhalb eines angegebenen Prozentsatzes liegt. Sie können außerdem angeben, ob eine Warnung an System Center Operations Manager gesendet werden soll.
    - **Zufällige Verzögerung (Stunden):** Gibt ein Verzögerungsfenster an, um eine übermäßige Verarbeitung im Registrierungsdienst für Netzwerkgeräte zu vermeiden. Der Standardwert ist 64 Stunden.
    - **Zeitplan:** Geben Sie den Zeitplan für die Auswertung der Konformität an, gemäß dem das bereitgestellte Profil auf Clientcomputern ausgewertet wird. Dabei kann es sich um einen einfachen oder benutzerdefinierten Zeitplan handeln. Das Profil wird von Clientcomputern ausgewertet, wenn sich der Benutzer anmeldet.
4.  Schließen Sie den Assistenten ab, um das Profil bereitzustellen.



## <a name="support-for-entrust-certification-authorities"></a>Unterstützung für Entrust-Zertifizierungsstellen
<!-- 1350740 -->
Configuration Manager unterstützt jetzt Entrust-Zertifizierungsstellen. Dadurch können PFX-Zertifikate an Geräte übermittelt werden, die bei Microsoft Intune registriert sind.

Sie können Entrust als Zertifizierungsstelle konfigurieren, wenn Sie in Configuration Manager die Rolle „Zertifikatregistrierungspunkt“ hinzufügen. Beim Hinzufügen eines neuen Zertifikatprofils, das PFX-Zertifikate ausstellt, können Sie entweder eine Microsoft- oder Entrust-Zertifizierungsstelle auswählen.

**Bekanntes Problem:** In der Technical Preview-Version 1706 werden für Microsoft-Zertifizierungsstellen keine PFX-Zertifikate ausgestellt. Dies wirkt sich nicht auf importierte PFX-Zertifikate oder SCEP-Profile aus.


## <a name="cisco-ipsec-support-for-ios-vpn-profiles"></a>Cisco-Unterstützung (IPsec) für iOS-VPN-Profile
<!-- 1321367 -->

Sie können ein iOS-VPN-Profil mit Cisco (IPsec) als Verbindungstyp erstellen. Weitere Informationen finden Sie unter [Erstellen von VPN-Profilen](../../protect/deploy-use/create-vpn-profiles.md#create-a-vpn-profile).


## <a name="new-windows-configuration-item-settings"></a>Neue Einstellungen für Windows-Konfigurationselemente
<!-- 1354715 -->

In dieser Version haben wir die folgenden neuen Einstellungen hinzugefügt, die Sie in Windows-Konfigurationselementen verwenden können:

### <a name="password"></a>Kennwort

- **Geräteverschlüsselung**

### <a name="device"></a>Gerät

- **Änderung der Regionseinstellungen (nur Desktop)**
- **Änderung der Energie- und Energiesparmoduseinstellungen**
- **Änderung der Spracheinstellungen**
- **Änderung der Systemzeit**
- **Änderung des Gerätenamens**

### <a name="store"></a>Speicher

- **Apps aus Store automatisch aktualisieren**
- **Nur privaten Store verwenden**
- **Store-App starten**

### <a name="microsoft-edge"></a>Microsoft Edge

- **Zugriff auf about:flags-Seite blockieren**
- **Außerkraftsetzen von SmartScreen-Aufforderung verhindern**
- **Außerkraftsetzen von SmartScreen-Aufforderung für Dateien verhindern**
- **WebRTC-LocalHost-IP-Adresse**
- **Standardsuchmaschine**
- **OpenSearch-XML-URL**
- **Homepages (nur Desktop)**

Weitere Informationen zu Konformitätseinstellungen finden Sie unter [Sicherstellen der Gerätekonformität](../../compliance/understand/ensure-device-compliance.md).


## <a name="new-device-compliance-policy-rules"></a>Neue Konformitätsrichtlinienregeln für Geräte

* **Erforderlicher Kennworttyp**. Gibt an, ob Benutzer ein alphanumerisches oder numerisches Kennwort erstellen müssen. Geben Sie für alphanumerische Kennwörter außerdem die Mindestanzahl von Zeichengruppen an, die das Kennwort enthalten muss. Es gibt vier Zeichensätze: Kleinbuchstaben, Großbuchstaben, Symbole und Zahlen.

  **Unterstützt auf:**
  * Windows Phone 8+
  * Windows 8.1+
  * iOS 6+
<br></br>
* **USB-Debugging auf Gerät blockieren**. Sie müssen diese Einstellungen nicht konfigurieren, da USB-Debuggen bereits auf Android for Work-Geräten deaktiviert ist.

  **Unterstützt auf:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
<br></br>
* **Apps von unbekannten Quellen blockieren**. Fordert an, dass Geräte die Installation von Apps aus unbekannten Quellen verhindern. Sie müssen diese Einstellung nicht konfigurieren, da Android for Work-Geräte die Installation aus unbekannten Quellen stets einschränken.

  **Unterstützt auf:**
  * Android 4.0+
  * Samsung KNOX Standard 4.0+
<br></br>
* **Bedrohungsüberprüfung für Apps erzwingen**. Diese Einstellung gibt an, dass die Funktion „Apps überprüfen“ auf dem Gerät aktiviert ist.

  **Unterstützt auf:**
  * Android 4.2 bis 4.4
  * Samsung KNOX Standard 4.0+


## <a name="new-mobile-application-management-policy-settings"></a>Neue Richtlinieneinstellungen für die Verwaltung mobiler Anwendungen
Ab dieser Version können Sie drei neue Richtlinieneinstellungen für die Verwaltung mobiler Anwendungen verwenden:

- **Bildschirmaufnahme blockieren** (nur Android-Geräte): Gibt an, dass die Screen Capture-Funktionen des Geräts blockiert werden, wenn Sie diese App verwenden.

- **Kontaktsynchronisierung deaktivieren:** Verhindert, dass die App Daten in der nativen App „Kontakte“ auf dem Gerät speichert.

- **Drucken deaktivieren:** Verhindert, dass die App Geschäfts-, Schul- oder Unidaten druckt.

## <a name="android-and-ios-enrollment-restrictions"></a>Registrierungseinschränkungen bei Android und iOS
<!-- 1290826 -->
Ab dieser Version können Administratoren angeben, dass Benutzer private Android- oder iOS-Geräte nicht in ihrer Hybridumgebung registrieren können. Dies ermöglicht das Begrenzen registrierter Geräte auf vorab festgelegte unternehmenseigene Geräte bzw. auf iOS-Geräte, die ausschließlich mit dem Programm zur Geräteregistrierung registriert werden.

### <a name="try-it-out"></a>Probieren Sie es aus
1. Wechseln Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** zu **Clouddienste** > **Microsoft Intune-Abonnement**.
2. Wählen Sie auf der Registerkarte **Start** in der Gruppe **Abonnement** zunächst **Plattformen konfigurieren** und dann **Android** oder **iOS** aus.
3. Aktivieren Sie **Nur unternehmenseigenen Geräten die Registrierung erlauben**.

## <a name="android-for-work-application-management-policy-for-copy-paste"></a>Android for Work-Anwendungsverwaltungsrichtlinie für Kopieren und Einfügen
Wir haben die Einstellungsbeschreibungen für Android for Work-Konfigurationselemente für **Datenfreigabe zwischen Arbeits- und persönlichem Profil zulassen** geändert.

|Vor Technical Preview 1706 | Name der neuen Option | Verhalten|
|-|-|-|
|Grenzübergreifende Freigaben verhindern| Standardeinschränkungen für Freigabe| Geschäftlich zu privat: Standard (soll für alle Versionen blockiert werden) <br>Privat zu geschäftlich: Standard (für 6.x und höher zugelassen, für 5.x blockiert)|
|Keine Einschränkungen| Apps im persönlichen Profil können Anforderungen des geschäftlichen Profils verarbeiten| Geschäftlich zu privat: Zulässig  <br>Privat zu geschäftlich: Zulässig|
|Apps im geschäftlichen Profil können Anforderungen des privaten Profils verarbeiten |Apps im geschäftlichen Profil können Anforderungen des privaten Profils verarbeiten |Geschäftlich zu privat: Standard<br>Privat zu geschäftlich: Zulässig<br>(Nur zweckmäßig für 5.x, da geschäftlich zu privat blockiert ist)|

Keine dieser Optionen verhindern das Kopier- und Einfügeverhalten direkt. Wir haben der Dienst- und Unternehmensportal-App in der Version 1704 eine benutzerdefinierte Einstellung hinzugefügt, die zum Verhindern von Kopieren und Einfügen konfiguriert werden kann. Diese kann mithilfe eines benutzerdefinierten URI festgelegt werden.

- OMA-URI: ./Vendor/MSFT/WorkProfile/DisallowCrossProfileCopyPaste
- Werttyp: Boolesch

Durch Festlegen von „DisallowCrossProfileCopyPaste“ auf TRUE wird das Kopier- und Einfügeverhalten zwischen privaten und geschäftlichen Android for Work-Profilen verhindert.

### <a name="try-it-out"></a>Probieren Sie es aus
1. Klicken Sie in der Configuration Manager-Konsole auf **Assets und Konformität** > **Übersicht** > **Konformitätseinstellungen** > **Konfigurationselemente**.
2. Klicken Sie auf **Erstellen**, um ein neues Konfigurationselement zu erstellen, und geben Sie **Name** und **Android for Work** an.
3. Wählen Sie in den auf dem Gerät zu konfigurierenden Einstellungsgruppen **Android for Work-Profil** aus, und klicken Sie auf **Weiter**.
4. Wählen Sie den Wert für **Datenfreigabe zwischen Arbeits- und persönlichen Profilen zulassen** aus, und schließen Sie den Assistenten ab.

## <a name="device-health-attestation-assessment-for-compliance-policies-for-conditional-access"></a>Bewertung für den Integritätsnachweis für Geräte für Konformitätsrichtlinien für bedingten Zugriff
<!-- 1097546 -->
Ab dieser Version können Sie den Status von „Integritätsnachweis für Geräte“ als Konformitätsrichtlinienregel für den bedingten Zugriff auf Unternehmensressourcen verwenden.

### <a name="try-it-out"></a>Probieren Sie es aus
Wählen Sie eine Regel für den Integritätsnachweis für Geräte als Teil einer Bewertung einer Konformitätsrichtlinie aus.