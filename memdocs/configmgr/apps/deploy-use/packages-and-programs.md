---
title: Pakete und Programme
titleSuffix: Configuration Manager
description: Hier erfahren Sie mehr über die Unterstützung von Bereitstellungen, die Legacypakete und Programme mit Configuration Manager verwenden.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: caad0507-9913-415a-b13d-d36f8f0a1b80
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2c125212a13790e196d001f53411633d1e42d4f8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689288"
---
# <a name="packages-and-programs-in-configuration-manager"></a>Pakete und Programme in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Configuration Manager unterstützt weiterhin Pakete und Programme, die in Configuration Manager 2007 verwendet wurden. Eine Bereitstellung mit Paketen und Programmen kann beim Bereitstellen der folgenden Tools oder Skripts besser geeignet sein als eine Anwendung:  

- Verwaltungstools, bei denen keine Anwendung auf einem Computer installiert wird
- „Einmal-Skripts“, die nicht ständig überwacht werden müssen  
- Skripts, die mit regelmäßiger Wiederholung ausgeführt werden und keine globale Auswertung verwenden können

> [!TIP]  
> Ziehen Sie in Betracht, das [Scripts](create-deploy-scripts.md)-Feature in der Configuration Manager-Konsole zu verwenden. Skripte können einige der zuvor beschriebenen Szenarios besser lösen als Pakete und Programme.

Wenn Sie Pakete von einer früheren Version von Configuration Manager migrieren, können Sie diese in der Configuration Manager-Hierarchie bereitstellen. Nach dem Abschluss der Migration werden die Pakete im Arbeitsbereich **Softwarebibliothek** im Knoten **Pakete** angezeigt.

Sie können diese Pakete genauso ändern und bereitstellen wie bei der Verwendung der Softwareverteilung. In Configuration Manager ist auch weiterhin der **Assistent zum Importieren eines Pakets aus einer Definition** enthalten, um Legacypakete zu importieren. Ankündigungen werden in Bereitstellungen konvertiert, wenn sie von Configuration Manager 2007 zu einer Configuration Manager-Hierarchie migriert werden.  

> [!NOTE]  
> Mit dem Paketkonvertierungs-Manager können Sie Pakete und Programme in Configuration Manager-Anwendungen konvertieren.  
>
> Ab Version 1806 ist der Paketkonvertierungs-Manager in Configuration Manager integriert. Weitere Informationen finden Sie unter [Paketkonvertierungs-Manager](../pcm/package-conversion-manager.md).  

In Paketen können einige neue Features von Configuration Manager verwendet werden, darunter Verteilungspunktgruppen und die Überwachungsfunktion. Sie können keine App-V-Anwendungen (Microsoft Application Virtualization) mit Paketen und Programmen in Configuration Manager bereitstellen. Zum Verteilen virtueller Anwendungen erstellen Sie diese als Configuration Manager-Anwendungen. Weitere Informationen finden Sie unter [Bereitstellen von virtuellen App-V-Anwendungen](../get-started/deploying-app-v-virtual-applications.md).  


## <a name="create-a-package-and-program"></a>Erstellen eines Pakets und Programms

### <a name="use-the-create-package-and-program-wizard"></a>Verwenden des Assistenten zum Erstellen von Paketen und Programmen

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie **Anwendungsverwaltung**, und wählen Sie den Knoten **Pakete** aus.  

2. Wählen Sie auf der Registerkarte **Start** des Menübands in der Gruppe **Erstellen** die Option **Paket erstellen** aus.  

3. Auf der **Paket** auf der Seite der **Erstellen eines Pakets und Programms Assistenten**, geben Sie die folgende Informationen:  

    - **Name:** Geben Sie einen Namen für das Paket mit maximal 50 Zeichen an.  

    - **Beschreibung:** Geben Sie eine Paketbeschreibung mit maximal 128 Zeichen an.  

    - **Hersteller** (optional): Geben Sie einen Herstellernamen an, um das Paket in der Configuration Manager-Konsole besser identifizieren zu können. Der Name darf maximal 32 Zeichen umfassen.

    - **Sprache** (optional): Geben Sie die Sprachversion des Pakets mit maximal 32 Zeichen an.  

    - **Version** (optional): Geben Sie eine Versionsnummer für dieses Paket mit maximal 32 Zeichen an.

    - **Dieses Paket enthält Quelldateien:** Diese Einstellung gibt an, ob für das Paket Quelldateien auf Clientgeräten vorhanden sein müssen. Standardmäßig wird diese Option vom Assistenten nicht aktiviert, und Configuration Manager verwendet keine Verteilungspunkte für das Paket. Geben Sie den Paketinhalt an, der an Verteilungspunkte verteilt werden soll, wenn Sie diese Option auswählen.  

    - **Quellordner:** Wenn das Paket Quelldateien enthält, klicken Sie auf **Durchsuchen**, um das Dialogfeld **Quellordner festlegen** zu öffnen und anschließend den Quelldateipfad für das Paket anzugeben.  

        > [!NOTE]  
        > Das Computerkonto des Standortservers muss über Lesezugriffsberechtigungen für den angegebenen Quellordner verfügen.  

    - Ab Version 1906: Wenn Sie Inhalte eines Clients vorab zwischenspeichern möchten, geben Sie die **Architektur** und **Sprache** des Pakets an. Weitere Informationen finden Sie unter [Konfigurieren des zwischengespeicherten Inhalts](../../osd/deploy-use/configure-precache-content.md).<!--4224642-->  

4. Wählen Sie auf der Seite **Programmtyp** im **Assistent zum Erstellen von Paketen und Programmen** den Typ des zu erstellenden Programms aus, und wählen Sie dann **Weiter** aus. Sie können ein Programm für einen [Computer](#create-a-standard-program) oder für ein [Gerät](#create-a-device-program) erstellen oder diesen Schritt überspringen und später ein Programm erstellen.  

    > [!TIP]  
    > Um ein neues Programm für ein vorhandenes Paket zu erstellen, müssen Sie zuerst das Paket auswählen. Wählen Sie dann auf der Registerkarte **Startseite** in der Gruppe **Paket** die Option **Programm erstellen** aus, um den **Assistenten zum Erstellen einer Anwendung** zu öffnen.  

#### <a name="create-a-standard-program"></a>Erstellen eines Standardprogramms

1. Wählen Sie auf der Seite **Programmtyp** im **Assistent zum Erstellen von Paketen und Programmen** die Option **Standardprogramm** und danach die Option **Weiter** aus.  

2. Geben Sie auf der Seite **Standardprogramm** folgende Informationen an:  

    - **Name:** Geben Sie einen Namen für das Programm mit maximal 50 Zeichen an.  

        > [!NOTE]  
        > Programmnamen müssen innerhalb eines Pakets eindeutig sein. Nachdem Sie ein Programm erstellt haben, können Sie seinen Namen nicht mehr ändern.  

    - **Befehlszeile:** Geben Sie die Befehlszeile zum Starten dieses Programms ein, oder wählen Sie **Durchsuchen** aus, um nach dem Speicherort der Datei zu suchen.  

        Wenn Sie für den Dateinamen keine Erweiterung angeben, versucht Configuration Manager „.com“, „.exe“ und „.bat“ als mögliche Erweiterungen zu verwenden.  

        Wenn der Client das Programm ausführt, sucht Configuration Manager an den folgenden Speicherorten nach der Datei:

        - Innerhalb des Pakets
        - Lokaler Windows-Ordner
        - Lokaler *%Pfad%*

        Wird die Datei nicht gefunden, schlägt das Programm fehl.  

    - **Startordner** (optional): Geben Sie hier den Ordner an, aus dem das Programm ausgeführt wird (bis zu 127 Zeichen). Dieser Ordner kann ein absoluter Pfad auf dem Client sein. Es kann sich auch um einen Pfad handeln, der relativ zu dem Verteilungspunktordner angegeben ist, in dem das Paket enthalten ist.

    - **Run**: Geben Sie den Modus an, in dem das Programm auf Clientcomputern ausgeführt wird. Wählen Sie eine der folgenden Optionen aus:  

        - **Normal**: Das Programm wird basierend auf den Standardeinstellungen des Systems und Programms im normalen Modus ausgeführt. Dies ist der Standardmodus.  

        - **Minimiert**: Das Programm wird auf Clientgeräten minimiert ausgeführt. Benutzer können Installationsaktivitäten möglicherweise im Infobereich oder in der Taskleiste sehen.  

        - **Maximiert**: Das Programm wird auf Clientgeräten maximiert ausgeführt. Benutzer sehen alle Installationsaktivitäten.  

        - **Ausgeblendet:** Die Anwendung wird auf Clientgeräten im Hintergrund ausgeführt. Benutzer sehen keine Installationsaktivitäten.  

    - **Programm kann ausgeführt werden:** Geben Sie an, ob das Programm nur ausgeführt werden kann, wenn ein Benutzer beim Clientcomputer angemeldet ist, wenn kein Benutzer angemeldet ist, oder ob die Ausführung in beiden Fällen möglich sein soll.  

    - **Ausführmodus:** Geben Sie an, ob das Programm mit den Administratorberechtigungen oder den Berechtigungen des angemeldeten Benutzers ausgeführt werden soll.  

    - **Benutzern gestatten, die Programminstallation anzuzeigen und mit ihr zu interagieren:** Verwenden Sie diese Einstellung, falls verfügbar, um anzugeben, ob der Benutzer mit der Programminstallation interagieren darf. Diese Option ist nur verfügbar, wenn die folgenden Bedingungen zutreffen:

        - Die Einstellung **Programm kann ausgeführt werden** wird für **Nur wenn kein Benutzer angemeldet ist** und **Unabhängig von Benutzeranmeldung** verwendet.
        - Die Einstellung **Ausführmodus** wird für **Mit Administratorrechten ausführen** verwendet.  

    - **Laufwerkmodus:** Geben Sie hier Informationen zur Ausführung des Programms im Netzwerk an. Wählen Sie eine der folgenden Optionen aus:  

        - **Unterstützt UNC-Namen:** Hiermit wird angegeben, dass das Programm mit einem UNC-Namen (Universal Naming Convention) ausgeführt wird. Dies ist die Standardeinstellung.  

        - **Erfordert Laufwerkbuchstaben:** Hiermit wird angegeben, dass das Programm zur vollständigen Kennzeichnung seines Speicherortes einen Laufwerkbuchstaben erfordert. Für diese Einstellung kann von Configuration Manager jeder verfügbare Laufwerkbuchstabe auf dem Client verwendet werden.  

        - **Erfordert einen bestimmten Laufwerkbuchstaben:** : Legen Sie fest, dass das Programm einen bestimmten Laufwerkbuchstaben erfordert, den Sie angeben, um den Speicherort vollständig zu qualifizieren. Beispiel: **Z:** . Wenn der Client bereits den angegebenen Laufwerkbuchstaben verwendet, kann das Programm nicht ausgeführt werden.  

    - **Verbindung mit dem Verteilungspunkt beim Anmelden wiederherstellen:** Geben Sie an, ob der Client die Verbindung mit dem Verteilungspunkt bei der Anmeldung des Benutzers erneut herstellen soll. Standardmäßig aktiviert der Assistent diese Option nicht.

3. Geben Sie im **Assistent zum Erstellen von Paketen und Programmen** auf der Seite **Anforderungen** die folgenden Informationen an:  

    - **Ein anderes Programm zuerst ausführen**: Geben Sie ein Paket und Programm an, das vor diesem Paket und Programm ausgeführt werden soll.  

    - **Plattformanforderungen:** Wählen Sie die Option **Dieses Programm kann auf jeder Plattform ausgeführt werden** oder **Dieses Programm kann nur auf angegebenen Clientplattformen ausgeführt werden** aus. Wählen Sie dann die Betriebssystemversionen aus, die Clients zur Installation dieses Pakets und Programms benötigen.  

    - **Geschätzter Speicherplatz:** Geben Sie hier den Speicherplatz auf dem Datenträger an, der zur Ausführung des Programms auf dem Computer erforderlich ist. Die Standardeinstellung lautet **Unbekannt**. Geben Sie bei Bedarf eine ganze Zahl an, die größer oder gleich 0 (Null) ist. Wenn Sie einen Wert festlegen, wählen Sie auch Einheiten für den Wert aus.  

    - **Maximal zulässige Laufzeit (Minuten):** Geben Sie die maximal zulässige Zeit für die Ausführung des Programms auf dem Clientcomputer an. Der Standardwert beträgt **120** Minuten. Verwenden Sie nur ganze Zahlen, die größer als 0 (Null) sind.  

        > [!IMPORTANT]  
        > Wenn Sie in derselben Sammlung Wartungsfenster verwenden, in der Sie dieses Programm bereitstellen, kann ein Konflikt auftreten, wenn die **Maximal zulässige Laufzeit** länger als das geplante Wartungsfenster ist. Wenn Sie die maximal zulässige Laufzeit auf **Unbekannt** festlegen, wird das Programm innerhalb des Wartungsfensters ausgeführt. Nach dem Schließen des Wartungsfensters wird die Ausführung dann je nach Bedarf fortgesetzt. Wenn Sie die maximal zulässige Laufzeit auf einen bestimmten Zeitraum festlegen, der die Länge aller verfügbaren Wartungsfenster überschreitet, wird das Programm nicht vom Client ausgeführt.  

        Wenn Sie diesen Wert auf **Unbekannt** festlegen, legt Configuration Manager für die maximal zulässige Laufzeit 12 Stunden (720 Minuten) fest.  

        > [!NOTE]  
        > Wenn das Programm die maximal zulässige Laufzeit überschreitet, wird es von Configuration Manager beendet, wenn die folgenden Bedingungen erfüllt sind:
        >
        > - Sie aktivieren die Option **Mit Administratorrechten ausführen**.
        > - Sie aktivieren die Option **Benutzern gestatten, die Programminstallation anzuzeigen und mit ihr zu interagieren** nicht.  

#### <a name="create-a-device-program"></a>Erstellen eines Geräteprogramms  

1. Wählen Sie auf der Seite **Programmtyp** im **Assistent zum Erstellen von Paketen und Programmen** die Option **Programm für Gerät** aus, und wählen Sie dann **Weiter** aus.  

2. Geben Sie auf der Seite **Programm für Gerät** die folgenden Einstellungen an:  

    - **Name:** Geben Sie einen Namen für das Programm mit maximal 50 Zeichen an.  

        > [!NOTE]  
        > Programmnamen müssen innerhalb eines Pakets eindeutig sein. Nachdem Sie ein Programm erstellt haben, können Sie seinen Namen nicht mehr ändern.  

    - **Kommentar** (optional): Geben Sie einen Kommentar für dieses Geräteprogramm mit maximal 127 Zeichen an.  

    - **Downloadordner**: Geben Sie den Namen des Ordners auf dem Gerät an, in dem die Paketquelldateien gespeichert werden sollen. Der Standardwert lautet `\Temp\`.  

    - **Befehlszeile:** Geben Sie die Befehlszeile zum Starten dieses Programms ein. Klicken Sie auf **Durchsuchen**, um zum Speicherort der Datei zu navigieren.  

    - **Befehlszeile im Downloadordner ausführen:** Wählen Sie diese Option aus, um das Programm aus dem Downloadordner auszuführen.  

    - **Befehlszeile in diesem Ordner ausführen:** Bei Auswahl dieser Option können Sie einen anderen Ordner angeben, von dem aus das Programm ausgeführt wird.  

3. Geben Sie auf der Seite **Anforderungen** die folgenden Einstellungen an:  

    - **Geschätzter Speicherplatz:** Geben Sie die Menge des Speicherplatzes an, der für die Software erforderlich ist. Der Client zeigt diesen Wert Benutzern von mobilen Geräten vor der Installation des Programms an.  

    - **Programm herunterladen:** Geben Sie Informationen dazu an, wann das Programm vom mobilen Gerät heruntergeladen werden kann. Zur Auswahl stehen die Optionen **So bald wie möglich**, **Nur über ein schnelles Netzwerk**oder **Nur, wenn das Gerät in der Dockingstation ist**.  

    - **Zusätzliche Anforderungen:** Geben Sie ggf. zusätzliche Anforderungen für dieses Programm an. Benutzern werden diese Anforderungen vor dem Installieren der Software angezeigt. Sie können z. B. die Benutzer benachrichtigen, die sie benötigen, um alle anderen Programme schließen, bevor Sie das Programm ausführen.  

## <a name="deploy-packages-and-programs"></a>Bereitstellen von Paketen und Programmen  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie **Anwendungsverwaltung**, und wählen Sie den Knoten **Pakete** aus.  

2. Wählen Sie das bereitzustellende Paket aus. Wählen Sie auf der Registerkarte **Start** des Menübands in der Gruppe **Bereitstellung** die Option **Bereitstellen** aus.  

3. Geben Sie auf der Seite **Allgemein** vom **Assistent zum Bereitstellen von Software** die Namen des Pakets und Programms an, die Sie bereitstellen möchten. Wählen Sie die Sammlung aus, für die Sie das Paket und Programm sowie optionale Kommentare bereitstellen möchten.  

    Wenn der Paketinhalt in der Standardverteilungspunktgruppe der Sammlung gespeichert werden soll, wählen Sie **Standard-Verteilungspunktgruppen verwenden, die dieser Sammlung zugeordnet sind** aus. Wenn die Sammlung keiner Verteilungspunktgruppe zugeordnet wurde, ist diese Option nicht verfügbar.  

4. Klicken Sie auf der Seite **Inhalt** auf **Hinzufügen**. Wählen Sie die Verteilungspunkte oder Verteilungspunktgruppen aus, auf denen Sie den Inhalt für dieses Paket und Programm verteilen möchten.  

5. Konfigurieren Sie auf der Seite **Bereitstellungseinstellungen** die folgenden Einstellungen:  

    - **Zweck**: Wählen Sie eine der folgenden Optionen aus:

        - **Verfügbar**: Dem Benutzer werden das veröffentlichte Paket und das Programm im Softwarecenter angezeigt, sodass er diese bei Bedarf installieren kann.  

        - **Erforderlich**: Das Paket und das Programm werden entsprechend dem konfigurierten Zeitplan automatisch bereitgestellt. Im Softwarecenter können Sie den Bereitstellungsstatus nachverfolgen und das Paket vor dem Stichtag installieren.  

        > [!NOTE]
        > Wenn mehrere Benutzer auf dem Gerät angemeldet sind, werden Paket- und Tasksequenzbereitstellungen möglicherweise im Softwarecenter nicht angezeigt.

    - **Aktivierungspakete senden**: Wenn Sie den Bereitstellungszweck auf **Erforderlich** festlegen und auf diese Option klicken, sendet der Standort zum Installationsstichtag zunächst ein Aktivierungspaket an Computer. Bevor Sie diese Option verwenden können, müssen Sie Computer für Wake-On-LAN konfigurieren. Weitere Informationen finden Sie unter [Konfigurieren von Wake-On-LAN](../../core/clients/deploy/configure-wake-on-lan.md).  

    - **Clients mit einer getakteten Internetverbindung dürfen den Inhalt nach dem Installationsstichtag herunterladen (Zusatzkosten können anfallen)**  

    > [!NOTE]  
    > Wenn Sie ein Paket und ein Programm bereitstellen, ist die Option **Software vorab auf dem primären Gerät des Benutzers bereitstellen** nicht verfügbar.  

6. Konfigurieren Sie auf der Seite **Zeitplanung**, wann dieses Paket und dieses Programm für Clientgeräte bereitgestellt werden sollen.  

    Welche Optionen auf dieser Seite verfügbar sind, ist davon abhängig, ob die Bereitstellungsaktion auf **Verfügbar** oder **Erforderlich** festgelegt ist.  

    Für Bereitstellungen mit der Einstellung **Erforderlich** konfigurieren Sie dann im Dropdownmenü **Verhalten beim erneuten Ausführen** das Verhalten für das erneute Ausführen des Programms. Wählen Sie aus den folgenden Optionen:  

    | Verhalten beim erneuten Ausführen | Beschreibung |
    |----------------|-------------|
    | **Bereitgestelltes Programm nie erneut ausführen** | Der Client führt das Programm nicht noch mal aus. Dieses Verhalten tritt auch dann auf, wenn das Programm ursprünglich fehlgeschlagen ist oder Programmdateien geändert wurden. |
    | **Programm immer erneut ausführen** | Der Client führt das Programm immer noch mal aus, wenn die Bereitstellung geplant ist. Dieses Verhalten tritt auch dann auf, wenn das Programm bereits erfolgreich ausgeführt wurde. Dies ist bei wiederkehrenden Bereitstellungen beim Aktualisieren des Programms nützlich. |
    | **Bei fehlgeschlagenem vorherigen Versuch erneut ausführen** | Das Programm wird bei geplanter Bereitstellung nur dann erneut vom Client ausgeführt, wenn bei der vorherigen Ausführung ein Fehler aufgetreten ist. |
    | **Bei erfolgreichem vorherigen Versuch erneut ausführen** | Der Client führt das Programm nur dann erneut aus, wenn es zuvor erfolgreich auf dem Client ausgeführt wurde. Dieses Verhalten ist für wiederkehrende Bereitstellungen nützlich, wenn Sie regelmäßig das Programm aktualisieren und für eine erfolgreiche Installation für jedes Update das vorherige Update erforderlich ist. |

7. Geben Sie auf der Seite **Benutzerfreundlichkeit** die folgenden Informationen an:  

    - **Benutzern zuweisungsunabhängige Programmausführung erlauben:** Benutzer können diese Software unabhängig von der geplanten Installationszeit aus dem Softwarecenter installieren.  

    - **Softwareinstallation**: Ermöglicht die Installation der Software außerhalb konfigurierter Wartungsfenster.  

    - **Systemneustart (falls dieser zum Abschluss der Installation erforderlich ist)** : Wenn für den Abschluss der Softwareinstallation ein Geräteneustart erforderlich ist, kann diese Aktion auch außerhalb konfigurierter Wartungsfenster ausgeführt werden.  

    - **Eingebettete Geräte:** Beim Bereitstellen von Paketen und Programmen für Windows Embedded-Geräte mit Schreibfilteraktivierung können Sie angeben, dass die Installationspakete und Programme auf dem temporären Overlay gespeichert und die Änderungen später ausgeführt werden. Alternativ können Sie die Änderungen auch am Installationsstichtag oder während eines Wartungsfensters bereitstellen. Falls die Änderungen am Installationsstichtag oder während eines Wartungsfensters bereitgestellt werden, ist ein Neustart erforderlich, und die Änderungen werden auf dem Gerät beibehalten.  

        > [!NOTE]  
        > Wenn Sie ein Paket oder ein Programm auf einem Windows Embedded-Gerät bereitstellen, stellen Sie sicher, dass das Gerät Mitglied einer Sammlung mit einem konfigurierten Wartungsfenster. Weitere Informationen zur Verwendung von Wartungsfenstern beim Bereitstellen von Paketen und Programmen auf Windows Embedded-Geräten finden Sie unter [Creating Windows Embedded applications (Erstellen von Windows Embedded-Anwendungen)](../get-started/creating-windows-embedded-applications.md).  

8. Geben Sie auf der Seite **Verteilungspunkte** die folgenden Informationen an:  

    - **Bereitstellungsoptionen**: Geben Sie die Aktion an, die ein Client für Verteilungspunkte in der aktuellen Begrenzungsgruppe verwenden soll. Wählen Sie auch die Aktion für den Client aus, wenn dieser einen Verteilungspunkt aus einer benachbarten Begrenzungsgruppe oder die standardmäßige eingerichtete Standortbegrenzungsgruppe verwendet.

        > [!IMPORTANT]  
        > Wenn Sie die Bereitstellungsoption **Programm vom Verteilungspunkt ausführen** konfigurieren, sollten Sie sicherstellen, dass die Option **Den Inhalt in diesem Paket in eine Paketfreigabe auf Verteilungspunkten kopieren** auf der Registerkarte **Datenzugriff** der Paketeigenschaften aktiviert ist. Andernfalls kann das Paket nicht von Verteilungspunkten aus ausgeführt werden.  

    - **Clients die Verwendung von Verteilungspunkten aus der Standard-Standortbegrenzungsgruppe gestatten**: Wenn dieser Inhalt nicht über einen Verteilungspunkt in den aktuellen oder benachbarten Begrenzungsgruppen verfügbar ist, aktivieren Sie diese Option, damit Clients Verteilungspunkte in der standardmäßig festgelegten Standortbegrenzungsgruppe verwenden dürfen.

9. Schließen Sie den Assistenten ab.  

Zeigen Sie die Bereitstellung im Arbeitsbereich **Überwachung** im Knoten **Bereitstellungen** im Detailbereich der Registerkarte für die Paketbereitstellung an, wenn Sie die Bereitstellung auswählen. Weitere Informationen finden Sie unter [Überwachen von Paketen und Programmen](#monitor-packages-and-programs).  


## <a name="monitor-packages-and-programs"></a>Überwachen von Paketen und Programmen

Zum Überwachen von Paket- und Programmbereitstellungen verwenden Sie dieselben Verfahren wie zur Überwachung von Anwendungen. Diese Verfahren werden unter [Überwachen von Anwendungen](monitor-applications-from-the-console.md) beschrieben.  

Pakete und Programme umfassen darüber hinaus mehrere integrierte Berichte, mit denen eine Überwachung der Informationen zum Bereitstellungsstatus von Paketen und Programmen möglich ist. Diesen Berichten sind die Berichtskategorien **Softwareverteilung – Paket- und Programmbereitstellung** und **Softwareverteilung – Status der Paket- und Programmbereitstellung**zugeordnet.  

Weitere Informationen zum Konfigurieren der Berichterstellung in Configuration Manager finden Sie unter [Einführung in die Berichterstellung in Configuration Manager](../../core/servers/manage/introduction-to-reporting.md).  


## <a name="manage-packages-and-programs"></a>Verwalten von Paketen und Programmen

Erweitern Sie im Arbeitsbereich **Softwarebibliothek** die Option **Anwendungsverwaltung**, und wählen Sie dann den Knoten **Pakete** aus. Wählen Sie zunächst das Paket, das Sie verwalten möchten, und anschließend einen Verwaltungstask aus.  

### <a name="create-prestage-content-file"></a>Datei für vorab bereitgestellten Inhalt erstellen

Hiermit wird der **Assistent zum Erstellen von vorab bereitgestellten Inhaltsdateien** geöffnet, um eine Datei mit dem Paketinhalt zu erstellen. Verwenden Sie diese Datei, um das Paket manuell auf einen Remoteverteilungspunkt zu importieren. Diese Aktion bietet sich an, wenn die Bandbreite zwischen Standortserver und Verteilungspunkt eingeschränkt ist.

### <a name="create-program"></a>Programm erstellen

Öffnet den **Assistenten zum Erstellen von Programmen**, um ein neues Programm für dieses Paket zu erstellen.

### <a name="export"></a>Exportieren

Öffnet den **Assistenten zum Exportieren von Paketen**, um das ausgewählte Paket und dessen Inhalt in eine Datei zu exportieren. Verwenden Sie diese Datei, um die Datei in eine andere Hierarchie zu importieren.

Informationen zum Importieren von Paketen und Programmen finden Sie unter [Erstellen von Paketen und Programmen](#create-a-package-and-program).

### <a name="deploy"></a>Bereitstellen

Öffnet den **Assistenten zum Bereitstellen von Software**, um das ausgewählte Paket und Programm in einer Sammlung bereitzustellen. Weitere Informationen finden Sie unter [Bereitstellen von Paketen und Programmen](#deploy-packages-and-programs).

### <a name="distribute-content"></a>Verteilen von Inhalt

Hiermit wird der **Assistent für die Verteilung von Inhalt** geöffnet, mit dem Sie den Inhalt für ein Paket und ein Programm an ausgewählte Verteilungspunkte oder Verteilungspunktgruppen senden können.

### <a name="update-distribution-points"></a>Verteilungspunkte aktualisieren

Aktualisiert Verteilungspunkte mit dem neuesten Inhalt für das ausgewählte Paket und Programm.


## <a name="see-also"></a>Weitere Informationen:

- [Skripts](create-deploy-scripts.md)

- [Paketkonvertierungs-Manager](../pcm/package-conversion-manager.md)

- [Paketdefinitionsdateien](package-definition-files.md)
