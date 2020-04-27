---
title: Erstellen von Anwendungen
titleSuffix: Configuration Manager
description: Erstellen Sie Anwendungen mit Bereitstellungstypen, Erkennungsmethoden und Anforderungen für die Installation von Software.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: cc230ff4-7056-4339-a0a6-6a44cdbb2857
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 33a95ae78fdc80c6c08b59cfe5ec5b2e88485a8f
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074655"
---
# <a name="create-applications-in-configuration-manager"></a>Erstellen von Anwendungen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Eine Configuration Manager-Anwendung definiert die Metadaten der Anwendung. In einer Anwendung ist mindestens ein Bereitstellungstyp enthalten. Diese Bereitstellungstypen enthalten die Installationsdateien und Informationen, die für die Installation der Software auf Geräten erforderlich sind. Ein Bereitstellungstyp weist zudem Regeln wie etwa Erkennungsmethoden und Anforderungen auf. Diese Regeln geben an, wann und wie der Client die Software installiert.  

Es gibt die folgenden Möglichkeiten für die Erstellung von Anwendungen:  

- Erstellen Sie eine Anwendung und Bereitstellungstypen durch Lesen der Installationsdateien der Anwendung automatisch:  
  - [Erstellen einer Anwendung](#bkmk_create) und [automatisches Erkennen](#bkmk_auto-app) von Anwendungsinformationen
  - [Erstellen eines Bereitstellungstyps](#bkmk_create-dt) und [automatisches Erkennen](#bkmk_auto-dt) von Informationen zum Bereitstellungstyp

- Erstellen Sie eine Anwendung manuell, und fügen Sie Bereitstellungstypen später hinzu:  
  - [Erstellen einer Anwendung](#bkmk_create) und [manuelles Angeben](#bkmk_manual-app) von Anwendungsinformationen
  - [Erstellen eines Bereitstellungstyps](#bkmk_create-dt) und [manuelles Angeben](#bkmk_manual-dt) von Informationen zum Bereitstellungstyp

- [Importieren einer Anwendung](#bkmk_import) aus einer Datei  

Dieser Artikel enthält auch folgende Informationen zum Konfigurieren eines Bereitstellungstyps:  

- [Inhalt](#bkmk_dt-content)
- [Tasksequenz](#bkmk_dt-ts)
- [Erkennungsmethode](#bkmk_dt-detect)
- [Benutzerfreundlichkeit](#bkmk_dt-ux)
- [Requirements](#bkmk_dt-require)
- [Rückgabecodes](#bkmk_dt-return)
- [-Abhängigkeiten](#bkmk_dt-depend)

## <a name="create-an-application"></a><a name="bkmk_create"></a> Erstellen einer Anwendung  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie **Anwendungsverwaltung**, und wählen Sie den Knoten **Anwendungen** aus.  

2. Wählen Sie auf dem Menüband auf der Registerkarte **Start** in der Gruppe **Erstellen** die Option **Anwendung erstellen** aus.  

Führen Sie eine automatische Erkennung für Anwendungsinformationen durch, oder geben Sie Anwendungsinformationen manuell an:  

- Führen Sie zur Erstellung einer Basisanwendung mit einem einzigen Bereitstellungstyp eine [automatische Erkennung](#bkmk_auto-app) für Anwendungsinformationen durch. Beispiel: eine Windows Installer-Datei ohne Abhängigkeiten oder Anforderungen. Nachdem Sie eine Anwendung mithilfe dieses Verfahrens erstellt haben, bearbeiten Sie sie nach Bedarf. Sie können Bereitstellungstypen hinzufügen oder ändern und Erkennungsmethoden, Abhängigkeiten oder Anforderungen hinzufügen.  

- Erstellen Sie komplexere Anwendungen, indem Sie Anwendungsinformationen [manuell angeben](#bkmk_manual-app). Definieren Sie mehrere Bereitstellungstypen, Abhängigkeiten, Erkennungsmethoden oder Anforderungen.  

### <a name="automatically-detect-application-information"></a><a name="bkmk_auto-app"></a> Automatische Erkennung von Anwendungsinformationen  

1. Wählen Sie auf der Registerkarte **Allgemein** des Assistenten zum Erstellen von Anwendungen die Option **Informationen zu dieser Anwendung automatisch anhand der Installationsdateien erkennen**aus.  

2. Wählen Sie in der Dropdownliste **Typ** den Installationsdateityp der Anwendung aus, den Sie für die automatische Erkennung verwenden möchten. Weitere Informationen zu den verfügbaren Installationstypen finden Sie unter [Von Configuration Manager unterstützte Bereitstellungstypen](create-applications.md#bkmk_deploy-types).  

3. Geben Sie im Feld **Speicherort** die Installationsdatei der Anwendung an, die Sie für die automatische Erkennung von Anwendungsinformationen verwenden möchten. Bei diesem Speicherort handelt es sich entweder um einen Netzwerkpfad (`\\server\share\filename`) oder um einen Link zum Store. Sie benötigen Zugriff auf den Netzwerkpfad sowie auf alle Unterordner mit Anwendungsinhalten.  

    > [!IMPORTANT]  
    > Wenn Sie als Anwendungstyp **Windows Installer (\*MSI-Datei**) auswählen, werden alle Dateien im angegebenen Ordner importiert. Anschließend werden diese Dateien an den Verteilungspunkt gesendet. Stellen Sie sicher, dass der angegebene Ordner ausschließlich Dateien enthält, die zur Installation der Anwendung erforderlich sind. Configuration Manager wird von Microsoft auf die Unterstützung von bis zu 20.000 Dateien im Anwendungspaket getestet. Wenn Ihre Anwendung mehr Dateien enthält, sollten Sie mehrere Anwendungen mit weniger Dateien erstellen.  

4. Überprüfen Sie auf der Seite **Informationen importieren** des Assistenten zum Erstellen von Anwendungen die Informationen, und wählen Sie anschließend **Weiter** aus. Bei Bedarf können Sie **Zurück** auswählen, um Fehler zu korrigieren.  

5. Geben Sie auf der Seite **Allgemeine Informationen** des Assistenten zum Erstellen von Anwendungen die folgenden Informationen an:  

    > [!NOTE]  
    > Wenn Configuration Manager diese Informationen aus den Anwendungsinstallationsdateien automatisch erkennt, wird er bereits hier aufgefüllt. Zudem werden je nach erstelltem Anwendungstyp möglicherweise unterschiedliche Optionen angezeigt.  

    - Allgemeine Informationen zur Anwendung wie der **Name** der Anwendung, **Kommentare des Administrators**, **Herausgeber** und **Softwareversion**. Geben Sie eine **optionale Referenz** an, oder wählen Sie **Verwaltungskategorien** aus, damit Sie die Anwendung in der Configuration Manager-Konsole finden.  

    - **Installationsprogramm**: Geben Sie das Installationsprogramm und alle zur Installation des Bereitstellungstyps der Anwendung erforderlichen Eigenschaften an.  

        > [!TIP]  
        > Wenn das Installationsprogramm nicht angezeigt wird, wählen Sie **Durchsuchen** aus, um auf den Speicherort des Installationsprogramms zuzugreifen.  

    - **Installationsverhalten**: Wählen Sie eine der drei Optionen zur Installation dieses Bereitstellungstyps durch Configuration Manager aus. Weitere Informationen zu diesen Optionen finden Sie unter [Benutzerfreundlichkeit](#bkmk_dt-ux).  

    - **Automatische VPN-Verbindung verwenden (sofern konfiguriert):** Wenn ein VPN-Profil auf dem Gerät bereitgestellt wurde, auf dem der Benutzer die App aufruft, wird das VPN beim Starten der App verbunden. Diese Option ist nur für Windows 8.1 und Windows Phone 8.1 verfügbar. Automatische VPN-Verbindungen werden nicht unterstützt, wenn auf Geräten mit Windows Phone 8.1 mehrere VPN-Profile bereitgestellt werden. Weitere Informationen finden Sie unter [VPN-Profile](../../protect/deploy-use/vpn-profiles.md).  

    - **Diese Anwendung für alle Benutzer auf dem Gerät bereitstellen**<!--1358310-->: Stellen Sie eine Anwendung mit einem Windows-App-Paket für alle Benutzer auf dem Gerät bereit. Weitere Informationen finden Sie unter [Erstellen von Windows-Anwendungen](../get-started/creating-windows-applications.md#bkmk_provision).  

       > [!Tip]  
       > Wenn Sie eine vorhandene Anwendung bearbeiten, befindet sich diese Einstellung auf der Registerkarte **Benutzerfreundlichkeit** unter den Eigenschaften des Bereitstellungstyps des Windows-App-Pakets.  

6. Wählen Sie **Weiter** aus, überprüfen Sie die Anwendungsinformationen auf der Seite **Zusammenfassung**, und schließen Sie den Assistenten zum Erstellen von Anwendungen ab.  

Die neue Anwendung wird nun im Knoten **Anwendungen** der Configuration Manager-Konsole angezeigt. Damit ist die Erstellung der Anwendung abgeschlossen.

Informationen zum Hinzufügen weiterer Bereitstellungstypen oder zum Konfigurieren weiterer Einstellungen finden Sie unter [Erstellen von Bereitstellungstypen für die Anwendung](#bkmk_create-dt).  

### <a name="manually-specify-application-information"></a><a name="bkmk_manual-app"></a> Manuelles Angeben von Anwendungsinformationen  

1. Wählen Sie auf der Seite **Allgemein** des Assistenten zum Erstellen von Anwendungen die Option **Anwendungsinformationen manuell angeben** aus, und wählen Sie anschließend **Weiter** aus.  

2. Angeben **allgemeiner Informationen** zur Anwendung:  

    - Der **Name** der Anwendung muss angegeben werden und darf maximal 256 Zeichen enthalten.  

    - **Administratorkommentare**, **Herausgeber** und **Softwareversion** sind zusätzliche Metadaten zur weiteren Beschreibung der Anwendung.  

    - Geben Sie eine **optionale Referenz** an, oder wählen Sie **Verwaltungskategorien** aus, damit Sie die Anwendung in der Configuration Manager-Konsole finden.  

    - **Veröffentlichungsdatum**  

    - Wählen Sie Benutzer oder Gruppen, die für diese Anwendung verantwortlich sind, als **Besitzer** und **Supportansprechpartner** aus. Für diese Werte ist standardmäßig Ihr Benutzername festgelegt.  

3. Geben Sie auf der Seite **Softwarecenter** des Assistenten zum Erstellen von Anwendungen die folgenden Informationen an:  

    > [!Note]  
    > In Version 1902 und älteren Versionen hieß diese Seite **Anwendungskatalog**.

    - **Ausgewählte Sprache:** Wählen Sie in der Dropdownliste die einzurichtende Sprachversion der Anwendung aus. Wählen Sie **Hinzufügen/Entfernen** aus, um weitere Sprachen für diese Anwendung zu konfigurieren.  

    - **Lokalisierter Anwendungsname:** Geben Sie den Namen der Anwendung in der ausgewählten Sprache an.  

        > [!IMPORTANT]  
        > Sie müssen für jede Sprachversion, die eingerichtet werden soll, einen lokalisierten Anwendungsnamen angeben.  

    - **Benutzerkategorien:** Klicken Sie auf **Bearbeiten**, um die Anwendungskategorien in der ausgewählten Sprache anzugeben. Benutzer des Softwarecenters verwenden diese Kategorien zum Filtern und Sortieren der Anwendungen.  

        > [!Note]  
        > In Version 1902 und älteren Versionen gelten Benutzerkategorien nur für verfügbare Bereitstellung für Benutzersammlungen. Wenn eine Anwendung in einer Computersammlung bereitgestellt wird, werden die Benutzerkategorien ignoriert.
        >
        > Ab der Version 1906 werden Benutzerkategorien für geräteorientierte Anwendungsbereitstellungen als Filter im Softwarecenter angezeigt. Diese Bereitstellungen können entweder verfügbar oder erforderlich sein.
        >
        > <!-- 4726793 -->Wenn Sie eine Kategorie umbenennen oder löschen, wird dies nicht automatisch auch für alle Apps dieser Kategorie übernommen. Die Änderungen werden stattdessen bei der nächsten Revision der App übernommen. Sie können dieses Problem beim Umbenennen und Löschen wie folgt umgehen:
        >
        > - Deaktivieren Sie zuerst das Kontrollkästchen für jede App, die der entsprechenden Kategorie angehört. Übernehmen Sie anschließend diese Änderung. Dadurch wird die App überarbeitet.
        >     - Verwenden Sie anschließend nicht die Umbenennungsaktion, sondern erstellen Sie eine neue Kategorie mit dem neuen Namen, und fügen Sie die neue Kategorie zu den relevanten Apps hinzu.
        >     - Sie können die Kategorie löschen, nachdem Sie die Apps überarbeitet haben.

    - **Benutzerdokumentation:** Geben Sie den Speicherort einer Datei an, in der Softwarecenterbenutzer weitere Informationen zu dieser Anwendung erhalten. Bei diesem Speicherort handelt es sich um eine Websiteadresse oder einen Netzwerkpfad und Dateinamen. Stellen Sie sicher, dass Benutzer auf diesen Speicherort zugreifen können.  

    - **Linktext:** Geben Sie den Text an, der anstelle von „Zusätzliche Informationen“ angezeigt wird, wenn eine Benutzerdokumentation angegeben ist.  

    - **URL der Datenschutzrichtlinien:** Geben Sie eine Websiteadresse an, die mit der Datenschutzerklärung für die Anwendung verknüpft ist.  

    - **Lokalisierte Beschreibung:** Geben Sie eine Beschreibung dieser Anwendung in der ausgewählten Sprache ein.  

    - **Schlüsselwörter:** Geben Sie eine Liste mit Schlüsselwörtern in der ausgewählten Sprache ein. Mithilfe dieser Schlüsselwörter können Softwarecenter-Benutzer nach der Anwendung suchen.  

    - **Symbol:** Wählen Sie **Durchsuchen** aus, um ein Symbol für diese Anwendung auszuwählen. Wenn Sie kein Symbol angeben, verwendet Configuration Manager ein Standardsymbol. Symbole können mit einer Abmessung von bis zu 512 × 512 Pixel dargestellt werden.  

4. Wählen Sie auf der Seite **Bereitstellungstypen** des Assistenten zum Erstellen von Anwendungen **Hinzufügen** aus, um einen neuen Bereitstellungstyp zu erstellen. Weitere Informationen finden Sie unter [Bereitstellungstypen für die Anwendung erstellen](#bkmk_create-dt) in diesem Thema.  

5. Wählen Sie **Weiter** aus, überprüfen Sie die Anwendungsinformationen auf der Seite **Zusammenfassung**, und schließen Sie den Assistenten zum Erstellen von Anwendungen ab.  

Die neue Anwendung wird nun im Knoten **Anwendungen** der Configuration Manager-Konsole angezeigt.  

## <a name="create-deployment-types-for-the-application"></a><a name="bkmk_create-dt"></a> Erstellen von Bereitstellungstypen für die Anwendung  

Wenn [Anwendungsinformationen automatisch erkannt werden sollen](#bkmk_auto-app), müssen Sie einige der Schritte in diesem Abschnitt möglicherweise nicht durchführen.  

> [!Note]  
> Bei der Anzeige der Eigenschaften eines vorhandenen Bereitstellungstyps entsprechen die folgenden Abschnitte den jeweiligen Registerkarten im Fenster mit den Eigenschaften des Bereitstellungstyps:  
>
> - [Inhalt](#bkmk_dt-content)
> - [Tasksequenz](#bkmk_dt-ts)
> - [Erkennungsmethode](#bkmk_dt-detect)
> - [Benutzerfreundlichkeit](#bkmk_dt-ux)
> - [Requirements](#bkmk_dt-require)
> - [Rückgabecodes](#bkmk_dt-return)
> - [-Abhängigkeiten](#bkmk_dt-depend)
>  
> Informationen zur Registerkarte **Installationsverhalten** in den Eigenschaften eines Bereitstellungstyps finden Sie unter [Check for running executable files (Prüfen, ob ausgeführte ausführbare Dateien vorhanden sind)](deploy-applications.md#bkmk_exe-check).  

### <a name="start-the-create-deployment-type-wizard"></a>Starten des Assistenten zum Erstellen neuer Bereitstellungstypen  

Es gibt drei Möglichkeiten, den Assistenten zum Erstellen neuer Bereitstellungstypen zu starten:

- **Im Knoten „Anwendungen“** : Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie **Anwendungsverwaltung**, und wählen Sie den Knoten **Anwendungen** aus. Wählen Sie eine Anwendung aus, und wählen Sie dann im Menüband **Bereitstellungstyp erstellen**.  

- **Beim Erstellen einer Anwendung**: Wählen Sie beim [manuellen Angeben von Anwendungsinformationen](#bkmk_manual-app) im Assistenten zum Erstellen von Anwendungen auf der Seite „Bereitstellungstypen“ **Hinzufügen** aus.  

- **Über die Anwendungseigenschaften:** Wählen Sie im Knoten **Anwendungen** eine vorhandene Anwendung aus, und wählen Sie dann **Eigenschaften** aus. Wechseln Sie zur Registerkarte **Bereitstellungstypen**, und wählen Sie **Hinzufügen** aus.

Wenden Sie anschließend eines der folgenden Verfahren an, damit Informationen zum Bereitstellungstyp [automatisch erkannt werden](#bkmk_auto-dt) oder um Informationen zum Bereitstellungstyp [manuell anzugeben](#bkmk_manual-dt).  

### <a name="automatically-identify-deployment-type-information"></a><a name="bkmk_auto-dt"></a> Automatisches Erkennen der Informationen zum Bereitstellungstyp  

1. Führen Sie auf der Seite **Allgemein** des Assistenten zum Erstellen neuer Bereitstellungstypen folgende Schritte durch:  

    1. Wählen Sie den **Typ** der Installationsdatei für die Anwendung zur Erkennung der Informationen zum Bereitstellungstyp aus.  

    2. Wählen Sie **Informationen zu diesem Bereitstellungstyp automatisch den Installationsdateien entnehmen** aus.  

    3. Geben Sie im Feld **Speicherort** die Installationsdatei der Anwendung an, die Sie zur Erkennung der Informationen zum Bereitstellungstyp verwenden möchten. Bei diesem Speicherort handelt es sich entweder um einen Netzwerkpfad (`\\server\share\filename`) oder um einen Link zum Store. Sie benötigen Zugriff auf den Netzwerkpfad sowie auf alle Unterordner mit Anwendungsinhalten.  

2. Überprüfen Sie die Informationen im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Informationen importieren**, und wählen Sie **Weiter** aus. Bei Bedarf können Sie **Zurück** auswählen, um Fehler zu korrigieren.  

3. Geben Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Allgemeine Informationen** die folgenden Informationen an:  

    > [!NOTE]  
    > Einige Informationen zum Bereitstellungstyp können schon vorhanden sein, wenn sie aus den Anwendungsinstallationsdateien gelesen wurden. Zudem werden je nach erstelltem Bereitstellungstyp möglicherweise unterschiedliche Optionen angezeigt.  

    - **Allgemeine Informationen** zum Bereitstellungstyp:  
        - **Name** (erforderlich)  

        - **Administratorkommentare** zur weiteren Beschreibung  

        - Verfügbare **Sprachen**  

    - **Installationsprogramm**: Geben Sie das Installationsprogramm und alle zur Installation des Bereitstellungstyps erforderlichen Eigenschaften an.  

    - **Installationsverhalten**: Wählen Sie eine der drei Optionen zur Installation dieses Bereitstellungstyps durch Configuration Manager aus. Weitere Informationen zu diesen Optionen finden Sie unter [Benutzerfreundlichkeit](#bkmk_dt-ux).  

    - **Automatische VPN-Verbindung verwenden (sofern konfiguriert):** Wenn ein VPN-Profil auf dem Gerät bereitgestellt wurde, auf dem der Benutzer die App aufruft, wird das VPN beim Starten der App verbunden. Diese Option ist nur für Windows 8.1 und Windows Phone 8.1 verfügbar. Automatische VPN-Verbindungen werden nicht unterstützt, wenn auf Geräten mit Windows Phone 8.1 mehrere VPN-Profile bereitgestellt werden. Weitere Informationen finden Sie unter [VPN-Profile](../../protect/deploy-use/vpn-profiles.md).  

4. Wählen Sie **Weiter** aus, und fahren Sie anschließend mit den [Optionen für den Inhalt des Bereitstellungstyps](#bkmk_dt-content) fort.  

### <a name="manually-specify-the-deployment-type-information"></a><a name="bkmk_manual-dt"></a> Manuelles Angeben von Informationen zum Bereitstellungstyp  

1. Wählen Sie auf der Seite **Allgemein** des Assistenten zum Erstellen neuer Bereitstellungstypen in der Dropdownliste **Typ** den Typ der Anwendungsinstallationsdateien für diesen Bereitstellungstyp aus.

2. Wählen Sie **Informationen zum Bereitstellungstyp manuell angeben** aus, und wählen Sie anschließend **Weiter**.

3. Geben Sie im Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Allgemeine Informationen** einen **Namen** für den Bereitstellungstyp an. Geben Sie optional **Administratorkommentare** an, wählen Sie die **Sprachen** für diesen Bereitstellungstyp aus, und wählen Sie anschließend **Weiter**.  

4. Fahren Sie mit den [Optionen für den Inhalt des Bereitstellungstyps](#bkmk_dt-content) fort.  

### <a name="deployment-type-content-options"></a><a name="bkmk_dt-content"></a> Optionen für den **Inhalt** des Bereitstellungstyps  

Geben Sie auf der Seite **Inhalt** die folgenden Informationen an:  

> [!Note]  
> Bei der Anzeige der Eigenschaften eines vorhandenen Bereitstellungstyps werden einige dieser Optionen auf der Registerkarte **Inhalt** und einige auf der Registerkarte **Programme** angezeigt.  

- **Inhaltsort:** Geben Sie den Speicherort des Inhalts für diesen Bereitstellungstyp an, oder klicken Sie auf **Durchsuchen**, um den Inhaltsordner für den Bereitstellungstyp auszuwählen.  

    > [!IMPORTANT]  
    > Das Systemkonto des Standortservercomputers muss zum Zugriff auf den angegebenen Inhaltsort berechtigt sein.  

  - **Inhalt dauerhaft in Clientcache speichern:** Der Inhalt des Bereitstellungstyps wird im Cache des Konfigurations-Manager-Clients auf unbestimmte Zeit gespeichert. Der Client behält den Inhalt selbst dann bei, wenn die App bereits installiert wurde. Diese Option ist bei einigen Bereitstellungen nützlich, z.B. bei Windows Installer-basierter Software. Windows Installer benötigt eine lokale Kopie des Quellinhalts für die Anwendung von Updates. Mit dieser Option wird der verfügbare Cachespeicher reduziert. Wenn Sie diese Option auswählen, kann es bei einer umfangreichen Bereitstellung im späteren Verlauf zu einem Fehler kommen, falls der Cache nicht über ausreichend Speicherplatz verfügt.  

- **Installationsprogramm**: Geben Sie den Namen des Installationsprogramms und alle erforderlichen Installationsparameter an.  

  - **Installationsstart in:** Geben Sie optional den Ordner an, in dem sich das Installationsprogramm für den Bereitstellungstyp befindet. Dabei kann es sich um einen absoluten Pfad auf dem Client oder um einen Pfad zum Verteilungspunktordner handeln, in dem sich die Installationsdateien befinden.  

- **Deinstallationsprogramm:** Geben Sie optional den Namen des Deinstallationsprogramms und alle erforderlichen Parameter an.  

  - **Deinstallation starten in:** Geben Sie optional den Ordner an, in dem sich das Deinstallationsprogramm für den Bereitstellungstyp befindet. Dieser Ordner kann ein absoluter Pfad auf dem Client sein. Es kann auch ein relativer Pfad auf einem Verteilungspunkt des Ordners mit dem Paket sein.  

- **Repair program** (Reparaturprogramm): Sie können für die Bereitstellungstypen „Windows Installer“ und „Skriptinstallationsprogramm“ optional den Namen des Reparaturprogramms und alle erforderlichen Parameter angeben.<!--1357866-->  

  - **Reparatur starten in:** Geben Sie optional den Ordner an, in dem sich das Reparaturprogramm für den Bereitstellungstyp befindet. Dieser Ordner kann ein absoluter Pfad auf dem Client sein. Es kann auch ein relativer Pfad auf einem Verteilungspunkt des Ordners mit dem Paket sein.  

- **Installationsprogramm ausführen und Programm als 32-Bit-Prozess auf 64-Bit-Clients deinstallieren**: Verwenden Sie die 32-Bit-Dateipfade und 32-Bit-Registrierungspfade auf Windows-Computern zum Ausführen des Installationsprogramms für den Bereitstellungstyp.  

#### <a name="deployment-type-properties-content-options"></a>Optionen für den **Inhalt** der Eigenschaften für den Bereitstellungstyp

Beim Anzeigen der Eigenschaften eines Bereitstellungstyps werden folgende Optionen nur auf der Registerkarte **Inhalt** angezeigt:

- **Einstellungen für zu deinstallierenden Inhalt:**  

  - **Übereinstimmend mit zu installierendem Inhalt:** Wählen Sie diese Option aus, wenn die Inhalte für die Installation und die Deinstallation identisch sind. Dies ist die Standardoption.  

  - **Nicht zu deinstallierender Inhalt:** Wählen Sie diese Option aus, wenn Ihre Anwendung für die Deinstallation keine Inhalte benötigt.  

  - **Abweichend von zu installierendem Inhalt:** Wählen Sie diese Option aus, wenn die für die Deinstallation benötigten Inhalte von den Inhalten für die Installation abweichen.  

    - **Speicherort für zu deinstallierenden Inhalt:** Geben Sie den Netzwerkpfad zu dem Inhalt an, der zum Deinstallieren der Anwendung verwendet wird.  

- **Clients die Verwendung von Verteilungspunkten aus der Standard-Standortbegrenzungsgruppe gestatten**: Geben Sie an, ob Clients die Software von einem Verteilungspunkt in der standardmäßig festgelegten Standortbegrenzungsgruppe herunterladen und installieren dürfen, wenn der Inhalt nicht über einen Verteilungspunkt in der aktuellen oder benachbarten Begrenzungsgruppe verfügbar ist.  

- **Bereitstellungsoptionen**: Geben Sie an, ob Clients die Anwendung herunterladen sollen, wenn ein Verteilungspunkt in einer benachbarten Standortbegrenzungsgruppe oder in der standardmäßigen Standortbegrenzungsgruppe verwendet wird.  

- **Freigeben von Inhalten für andere Clients im gleichen Subnetz zulassen**: Geben Sie an, ob beim Download von Inhalten BranchCache verwendet werden soll. Weitere Informationen finden Sie unter [BranchCache](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache). BranchCache ist auf Clients immer aktiviert. Diese Einstellung wurde in Version 1802 entfernt, da Clients BranchCache verwenden, sofern diese Option vom Verteilungspunkt unterstützt wird.  

### <a name="deployment-type-task-sequence-options"></a>Optionen für den <a name="bkmk_dt-ts"></a>Tasksequenz-**Bereitstellungstyp**

<!--3555953-->

Weitere Informationen zum Tasksequenz-Bereitstellungstyp ab Version 2002 finden Sie unter [Tasksequenz-Bereitstellungstyp](../get-started/creating-windows-applications.md#bkmk_tsdt).

Geben Sie auf der Seite **Tasksequenz** die folgenden Informationen an:

- **Tasksequenz für Installation**: Wählen Sie eine Tasksequenz aus, die den Installationsvorgang für diese App ausführt.

- **Tasksequenz für Deinstallation** (optional): Wählen Sie eine Tasksequenz zum Entfernen dieser App aus.

> [!TIP]  
> Wenn Ihre Tasksequenz nicht in der Liste aufgeführt ist, überprüfen Sie erneut, ob sie keine Schritte zur Bereitstellung oder Aktualisierung des Betriebssystems enthält. Bestätigen Sie außerdem, dass sie nicht als Tasksequenz mit hoher Auswirkung gekennzeichnet ist. Weitere Informationen finden Sie unter den Voraussetzungen für den [Tasksequenz-Bereitstellungstyp](../get-started/creating-windows-applications.md#bkmk_tsdt).

### <a name="deployment-type-detection-method-options"></a><a name="bkmk_dt-detect"></a> Optionen für die **Erkennungsmethode** des Bereitstellungstyps

Mit dem folgenden Verfahren richten Sie eine Erkennungsmethode ein, durch die angegeben wird, ob der Bereitstellungstyp vorhanden ist. Das heißt, es wird angegeben, ob die Anwendung bereits auf dem Windows-Gerät installiert ist. Verwenden Sie eine der beiden folgenden Methoden zum Erstellen einer Erkennungsmethode:

- [Regeln zur Ermittlung dieses Bereitstellungstyps konfigurieren](#bkmk_detect-rule)
- [Benutzerdefiniertes Skript zur Ermittlung dieses Bereitstellungstyps verwenden](#bkmk_detect-script)

#### <a name="configure-rules-to-detect-the-presence-of-this-deployment-type"></a><a name="bkmk_detect-rule"></a> Regeln zur Ermittlung dieses Bereitstellungstyps konfigurieren

1. Auf der Seite **Erkennungsmethode** ist die Option **Regeln konfigurieren, um zu erkennen, ob dieser Bereitstellungstyp vorhanden ist** standardmäßig aktiviert. Wählen Sie **Klausel hinzufügen** aus.  

2. Klicken Sie im Dialogfeld **Erkennungsregel** auf **Einstellungstyp**, um herauszufinden, ob der Bereitstellungstyp vorhanden ist:  

    - **Dateisystem:** Erkennt, ob eine angegebene Datei oder ein angegebener Ordner auf einem Gerät vorhanden ist. Diese Erkennung zeigt an, dass die Anwendung installiert ist. Geben Sie die folgenden zusätzlichen Informationen an:  

        - **Typ:** Geben Sie an, ob es sich um eine Datei oder um einen Ordner handelt.  

        - **Pfad** (erforderlich): Geben Sie auf dem Gerät, auf dem sich die Datei oder der Ordner befindet, den lokalen Pfad ein, oder navigieren Sie zu diesem Pfad. Beispiel: `C:\Program Files`. Ein freigegebener Netzwerkpfad kann nicht angegeben werden. Wenn Sie **Durchsuchen** auswählen, wird das lokale Dateisystem durchsucht oder eine Verbindung mit einem repräsentativen Client zum Durchsuchen hergestellt.  

        - **Datei- oder Ordnername** (erforderlich): Geben Sie den Namen der zu suchenden Datei oder des zu suchenden Ordners im oben angegebenen Pfad an. Wenn diese Datei oder dieser Ordner auf dem Gerät erkannt wird, wird davon ausgegangen, dass die Anwendung auf dem Gerät installiert ist.  

        - **Diese Datei/dieser Ordner ist einer 32-Bit-Anwendung auf 64-Bit-Systemen zugeordnet**: Diese Option ist standardmäßig ausgewählt. Der Client sucht zunächst an Speicherorten mit 32-Bit-Dateien nach der angegebenen Datei bzw. nach dem angegebenen Ordner. Wenn die Datei bzw. der Ordner nicht gefunden wird, sucht der Client an 64-Bit-Speicherorten.  

    - **Registrierung:** Erkennt, ob ein angegebener Registrierungsschlüssel oder Registrierungswert auf einem Clientgerät vorhanden ist. Diese Erkennung zeigt an, dass die Anwendung installiert ist. Geben Sie die folgenden zusätzlichen Informationen an:  

        - **Struktur** (erforderlich): Wählen Sie in der Dropdownliste eine Registrierungsstruktur aus. Beispiel: `HKEY_LOCAL_MACHINE`.  

        - **Schlüssel** (erforderlich): Geben Sie den Registrierungsschlüssel für die Suche in der oben angegebenen Struktur an. Beispiel: `SOFTWARE\Microsoft\Office`.  

        - **Wert** (optional): Geben Sie im oben angegebenen Schlüssel einen bestimmten Wert an, nach dem gesucht werden soll. Wenn Sie möchten, dass der Client den (Standard-)Wert erkennt, aktivieren Sie die Option **Registrierungsschlüsselwert für Erkennung verwenden (Standard)** . Wenn Sie einen Wert eingeben oder diese Option aktivieren, müssen Sie einen **Datentyp** auswählen.  

        - **Dieser Registrierungsschlüssel ist mit einer 32-Bit-Anwendung auf 64-Bit-Systemen verknüpft:** Wählen Sie diese Option aus, um zuerst in 32-Bit-Registrierungspfaden nach dem angegebenen Registrierungsschlüssel zu suchen. Wenn der Registrierungsschlüssel nicht gefunden wird, sucht der Client an 64-Bit-Speicherorten.  

    - **Windows Installer:** Erkennt, ob eine angegebene Windows Installer-Datei auf einem Clientgerät vorhanden ist. Diese Erkennung zeigt an, dass die Anwendung installiert ist. Geben Sie auf dem Client den zu erkennenden MSI-**Produktcode** an. Wenn Sie auf **Durchsuchen** klicken, wählen Sie die MSI-Datei aus, aus der der Produktcode ausgelesen werden soll.

3. Geben Sie im unteren Bereich des Fensters „Erkennungsregel“ an, ob das Element vorhanden sein oder einer Regel entsprechen muss. Wenn Sie die Ermittlung beispielsweise mit einer Datei durchführen, ist die folgende Option standardmäßig aktiviert: **Die Dateisystemeinstellung muss auf dem Zielsystem vorhanden sein, um das Vorhandensein dieser Anwendung anzuzeigen**. Wählen Sie die andere Option aus, um eine Regel zur Erkennung basierend auf Datei- oder Ordnereigenschaften zu erstellen. Zu diesen Eigenschaften zählen Änderungsdatum, Erstellungsdatum, Version oder Größe. Diese Regelkriterien sind je nach Einstellungstyp unterschiedlich.  

4. Wählen Sie **OK** aus, um das Dialogfeld **Erkennungsregel** zu schließen.  

Wenn Sie für einen Bereitstellungstyp mehrere Erkennungsmethoden erstellen, können Sie durch Gruppieren der Klauseln eine komplexere Logik erstellen.  

#### <a name="group-detection-clauses-optional"></a>Gruppenerkennungsklauseln *(optional)*

1. Erstellen Sie mindestens drei Erkennungsmethodenklauseln für einen Bereitstellungstyp.  

2. Wählen Sie mindestens zwei aufeinanderfolgende Klauseln aus, und klicken Sie dann auf **Gruppe**. Dann sollten Klammern zu den zugeordneten Spalten hinzugefügt werden. Diese zeigen, wo die Gruppe startet und endet.  

    Beispiel:

    | Connector  |  ( | Klausel           |  )  |
    |------------|----|------------------|-----|
    |            |    | MSI-Produktcode |     |
    | Oder         | (  | file1.text vorhanden|     |
    | Und        |    | file2.txt vorhanden | )   |

3. Sie können die Gruppe entfernen, indem Sie die gruppierten Klauseln auswählen und dann auf **Gruppierung aufheben** klicken.  

*Fahren Sie mit dem nächsten Abschnitt zur Verwendung eines benutzerdefinierten Skripts als Erkennungsmethode fort.* Alternativ dazu können Sie die Optionen zur [Benutzerfreundlichkeit](#bkmk_dt-ux) für den Bereitstellungstyp *überspringen*.

#### <a name="use-a-custom-script-to-check-for-the-presence-of-a-deployment-type"></a><a name="bkmk_detect-script"></a> Verwenden eines benutzerdefinierten Skripts zur Überprüfung, ob ein Bereitstellungstyp vorhanden ist  

1. Wählen Sie auf der Seite **Erkennungsmethode** das Feld **Benutzerdefiniertes Skript zur Ermittlung dieses Bereitstellungstyps verwenden** aus. Klicken Sie dann auf **Bearbeiten**.  

2. Wählen Sie im Dialogfeld **Skript-Editor** einen **Skripttyp** aus, um den Bereitstellungstyp zu ermitteln: PowerShell, VBScript oder JScript.  

    > [!Note]  
    > Der Configuration Manager-Client ruft PowerShell mit dem Parameter `-NoProfile` auf, wenn ein Windows PowerShell-Skript als App-Erkennungsmethode ausgeführt wird. Diese Option startet PowerShell ohne Profile. Ein PowerShell-Profil ist ein Skript, das ausgeführt wird, wenn PowerShell gestartet wird. <!--3607762-->  

3. Geben Sie im Feld **Skriptinhalte** das gewünschte Skript ein, oder fügen Sie den Inhalt eines vorhandenen Skripts ein. Wählen Sie **Öffnen** aus, um zu einem vorhandenen gespeicherte Skript zu navigieren. Wählen Sie **Löschen** aus, um den Text im Feld „Skriptinhalte“ zu entfernen. Aktivieren Sie ggf. die Option **Skript als 32-Bit-Prozess auf 64-Bit-Clients ausführen**.  

    > [!NOTE]  
    > Die maximal zulässige Größe für ein Skript beträgt 32 KB.  

4. Wählen Sie **OK** aus, um das Skript zu speichern und das Dialogfeld **Skript-Editor** zu schließen. Im Assistenten zum Erstellen neuer Bereitstellungstypen werden die Felder **Skripttyp** und **Skriptlänge** mit Details zu Ihrem Skript aktualisiert.

#### <a name="about-custom-script-detection-methods"></a>Informationen zu benutzerdefinierten Skripterkennungsmethoden  

Configuration Manager überprüft die Ergebnisse des Skripts. Es liest die Werte, die vom Skript in den Standardausgabestream (STDOUT), den Standardfehlerstream (STDERR) und den Exitcode geschrieben wurden. Wenn das Skript mit einem Wert ungleich 0 (null) beendet wird, schlägt das Skript fehl und der Erkennungszustand der Anwendung ist *unbekannt*. Wenn der Exitcode gleich null ist und in STDOUT Daten enthalten sind, ist der Erkennungszustand der Anwendung *Installiert*.

> [!TIP]
> Wenn Sie beim Schreiben eines Erkennungsskripts einen Exitcode gleich 0 (null) zurückgeben, aber keine Ausgabe (Daten in STDOUT) zurückgeben, wird die Anwendung nicht als installiert erkannt. Weitere Informationen finden Sie in den folgenden Beispielen.

Überprüfen Sie anhand der folgenden Tabellen, ob eine Anwendung über die Ausgabe eines Skripts installiert wurde:  

##### <a name="zero-exit-code"></a>Exitcode gleich 0

|STDOUT|STDERR|Skriptergebnis|Erkennungszustand der Anwendung|
|---------|---------|---------|---------|
|Leer|Leer|Erfolgreich|Nicht installiert|
|Leer|Nicht leer|Fehler|Unbekannt|
|Nicht leer|Leer|Erfolgreich|Installiert|
|Nicht leer|Nicht leer|Erfolgreich|Installiert|

##### <a name="non-zero-exit-code"></a>Exitcode ungleich 0

|STDOUT|STDERR|Skriptergebnis|Erkennungszustand der Anwendung|
|---------|---------|---------|---------|
|Leer|Leer|Fehler|Unbekannt|
|Leer|Nicht leer|Fehler|Unbekannt|
|Nicht leer|Leer|Fehler|Unbekannt|
|Nicht leer|Nicht leer|Fehler|Unbekannt|

##### <a name="examples"></a>Beispiele

Verwenden Sie die folgenden PowerShell/VBScript-Beispiele zum Schreiben von eigenen Skripts zur Anwendungserkennung:  

**Beispiel 1**: Das Skript gibt einen Exitcode zurück, der ungleich null ist. Dieser Code gibt an, dass das Skript nicht erfolgreich ausgeführt werden konnte. In diesem Fall ist der Erkennungszustand der Anwendung Unbekannt.  

``` PowerShell
Exit 1
```

``` VBScript
WScript.Quit(1)
```

**Beispiel 2**: Das Skript gibt einen Exitcode von null zurück, aber der Wert von STDERR ist nicht leer. Dieses Ergebnis gibt an, dass das Skript nicht erfolgreich ausgeführt werden konnte. In diesem Fall ist der Erkennungszustand der Anwendung Unbekannt.  

``` PowerShell
Write-Error "Script failed"
Exit 0
```

``` VBScript
WScript.StdErr.Write "Script failed"
WScript.Quit(0)
```

**Beispiel 3:** Vom Skript wird ein Exitcode gleich null zurückgegeben, was darauf hindeutet, dass es erfolgreich ausgeführt wurde. Der Wert für STDOUT ist jedoch leer, was darauf hindeutet, dass die Anwendung nicht installiert ist.  

``` PowerShell
Exit 0
```

``` VBScript
WScript.Quit(0)
```

**Beispiel 4**: Vom Skript wird ein Exitcode gleich null zurückgegeben, was darauf hindeutet, dass es erfolgreich ausgeführt wurde. Der Wert für STDOUT ist nicht leer, was darauf hindeutet, dass die Anwendung installiert ist.  

``` PowerShell
Write-Host "The application is installed"
Exit 0
```

``` VBScript
WScript.StdOut.Write "The application is installed"
WScript.Quit(0)
```

**Beispiel 5**: Vom Skript wird ein Exitcode gleich null zurückgegeben, was darauf hindeutet, dass es erfolgreich ausgeführt wurde. Die Werte für STDOUT und STDERR sind nicht leer, was darauf hindeutet, dass die Anwendung installiert ist.  

``` PowerShell
Write-Host "The application is installed"
Write-Error "Completed"
Exit 0
```

``` VBScript
WScript.StdOut.Write "The application is installed"
WScript.StdErr.Write "Completed"
WScript.Quit(0)
```

### <a name="deployment-type-user-experience-options"></a><a name="bkmk_dt-ux"></a> Optionen für die **Benutzerfreundlichkeit** des Bereitstellungstyps

Durch diese Einstellungen wird angegeben, wie der Client die Anwendung auf Geräten installiert und was dem Benutzer angezeigt wird.  

Geben Sie auf der Seite **Benutzerfreundlichkeit** die folgenden Informationen an:  

- **Installationsverhalten**: Wählen Sie in der Dropdownliste eine der folgenden Optionen aus:  

  - **Für Benutzer installieren:** Die Anwendung wird nur für den Benutzer installiert, für den Sie die Anwendung bereitstellen.  

  - **Für System installieren:** Die Anwendung wird nur einmal installiert. Danach ist sie für alle Benutzer verfügbar.  

  - **Für System installieren, wenn Ressource ein Gerät ist, andernfalls für Benutzer installieren:** Wenn Sie die Anwendung für ein Gerät bereitstellen, wird sie für alle Benutzer installiert. Wenn Sie die Anwendung für einen Benutzer bereitstellen, wird sie nur für diesen Benutzer installiert.  

- **Anmeldeanforderung**: Wählen Sie eine der folgenden Optionen aus:  

  - **Nur wenn ein Benutzer angemeldet ist**  

  - **Unabhängig von Benutzeranmeldung**  

  - **Nur wenn kein Benutzer angemeldet ist**  

    > [!NOTE]  
    > Diese Option ist standardmäßig auf **Nur wenn ein Benutzer angemeldet ist** festgelegt. Wenn Sie in der Dropdownliste **Installationsverhalten** die Option **Für Benutzer installieren** auswählen, können Sie diese Option nicht ändern.  

- **Sichtbarkeit des Installationsprogramms:** Geben Sie den Modus an, in dem der Bereitstellungstyp auf Clientgeräten ausgeführt wird. Wählen Sie eine der folgenden Optionen aus:  

  - **Maximiert**: Der Bereitstellungstyp wird auf Clientgeräten im maximierten Modus ausgeführt. Benutzer sehen alle Installationsaktivitäten.  

  - **Normal**: Der Bereitstellungstyp wird basierend auf den Standardeinstellungen des Systems und Programms im normalen Modus ausgeführt. Dies ist der Standardmodus.  

  - **Minimiert**: Der Bereitstellungstyp wird auf Clientgeräten im minimierten Modus ausgeführt. Benutzer können die Installationsaktivität möglicherweise im Infobereich oder in der Taskleiste sehen.  

  - **Ausgeblendet:** Der Bereitstellungstyp wird auf Clientgeräten im Hintergrund ausgeführt. Benutzer sehen keine Installationsaktivitäten.  

- **Benutzern gestatten, die Programminstallation anzuzeigen und mit ihr zu interagieren:** Hiermit geben Sie an, ob der Benutzer bei der Installation des Bereitstellungstyps die Installationsoptionen einrichten darf.  

    Wenn in der Dropdownliste **Installationsverhalten** die Option **Für Benutzer installieren** ausgewählt wurde, ist diese Option standardmäßig aktiviert.  

    > [!IMPORTANT]  
    > Diese Einstellung ist optional, wenn Sie das Verhalten **Für System installieren** auswählen. Diese Änderung dient primär dazu, dass einem Benutzer während einer Tasksequenz die Interaktion mit der Installation erlaubt wird. Führen Sie beispielsweise einen Setupvorgang aus, der den Endbenutzer nach verschiedenen Optionen befragt. Einige Anwendungsinstallationsprogramme können Eingabeaufforderungen an Benutzer nicht deaktivieren, oder der Installationsprozess fordert bestimmte Konfigurationswerte an, die nur dem Benutzer bekannt sind. <!--1356976-->  
    >  
    > Eine Installation im Systemkontext und das Zulassen einer Benutzerinteraktion mit der Installation stellt keine sichere Konfiguration dar. Weitere Informationen finden Sie unter [Security and privacy for cloud management gateway (Sicherheit und Datenschutz für das Cloudverwaltungsgateway)](../plan-design/security-and-privacy-for-application-management.md#bkmk_interact).  

- **Maximal zulässige Laufzeit (Minuten):** Geben Sie in Minuten an, wie lange die Ausführung des Bereitstellungstyps auf dem Clientcomputer voraussichtlich maximal dauert. Geben Sie für diese Einstellung eine ganze Zahl größer oder gleich null an. Der Standardwert beträgt 120 Minuten (zwei Stunden).  

    Verwenden Sie diesen Wert für die folgenden Aktionen:  

  - Überwachung der Ergebnisse des Bereitstellungstyps  

  - Überprüfen Sie, ob ein Bereitstellungstyp installiert wird, wenn Sie auf Clientgeräten Wartungsfenster definiert haben. Wenn ein Wartungsfenster vorhanden ist, wird ein Bereitstellungstyp nur dann gestartet, wenn die verbleibende Dauer des Wartungsfensters noch mindestens der Einstellung unter **Maximal zulässige Laufzeit** entspricht.  

    > [!IMPORTANT]  
    > Wenn der Zeitraum für **Maximal zulässige Laufzeit** länger ist als das geplante Wartungsfenster, kann dies zu einem Problem führen. Wird die maximale Laufzeit vom Benutzer auf einen Wert festgelegt, der die Länge der verfügbaren Wartungsfenster überschreitet, wird dieser Bereitstellungstyp nicht ausgeführt.  

- **Geschätzte Installationszeit (Minuten):** Legen Sie die voraussichtliche Dauer für die Installation des Bereitstellungstyps fest. Benutzern wird diese Zeit im Softwarecenter angezeigt.  

#### <a name="deployment-type-properties-user-experience-options"></a>Optionen für die **Benutzerfreundlichkeit** der Eigenschaften für den Bereitstellungstyp

Beim Anzeigen der Eigenschaften eines Bereitstellungstyps werden folgende Optionen nur auf der Registerkarte **Benutzerfreundlichkeit** angezeigt:

Erzwingen Sie nach der Installation ein bestimmtes Verhalten. Wählen Sie eine der folgenden Optionen aus:  

- **Verhalten auf Grundlage von Rückgabecodes bestimmen:** Neustarts werden auf der Grundlage der auf der Registerkarte [Rückgabecodes](#bkmk_dt-return) konfigurierten Codes behandelt. Das Softwarecenter zeigt **Möglicherweise ist ein Neustart notwendig** an. Wenn ein Benutzer während der Installation angemeldet ist, erhält er, je nach den Einstellungen zur Benutzerfreundlichkeit der *Bereitstellung*, eine Aufforderung.  

- **Keine bestimmte Aktion:** Es ist kein Neustart nach der Installation erforderlich. Das Softwarecenter meldet, dass kein Neustart erforderlich ist.  

- **Durch das Softwareinstallationsprogramm wird möglicherweise ein Neustart erzwungen:** Configuration Manager steuert oder startet keinen Neustart, bei der tatsächlichen Installation geschieht dies jedoch möglicherweise ohne Warnung. Verwenden Sie diese Einstellung, um zu verhindern, dass Configuration Manager Installationsfehler meldet, wenn das Installationsprogramm einen Neustart initiiert. Das Softwarecenter zeigt **Möglicherweise ist ein Neustart notwendig** an.  

- **Ein verbindlicher Geräteneustart wird von Configuration Manager erzwungen:** Configuration Manager erzwingt einen Neustart des Geräts nach der erfolgreichen Installation. Das Softwarecenter meldet, dass ein Neustart erforderlich ist. Wenn ein Benutzer während der Installation angemeldet ist, erhält er, je nach den Einstellungen zur Benutzerfreundlichkeit der *Bereitstellung*, eine Aufforderung.  

### <a name="deployment-type-requirements"></a><a name="bkmk_dt-require"></a>**Anforderungen** für den Bereitstellungstyp

Vor der Installation des Bereitstellungstyps überprüft Configuration Manager diese Anforderungen auf den Geräten. Verwenden Sie Anforderungen, um die Geräte oder Benutzer, die diese Anwendung erhalten, weiter einzuschränken und zu steuern. Wenn Sie die Anwendung beispielsweise für eine Benutzersammlung bereitstellen, geben Sie hier die Hardwareanforderungen der App an.

1. Wählen Sie auf der Seite **Anforderungen** die Option **Hinzufügen** aus, um das Dialogfeld **Anforderung erstellen** zu öffnen.  

2. Wählen Sie in der Dropdownliste **Kategorie** aus, ob diese Anforderung für ein **Gerät** oder einen **Benutzer** bestimmt ist.  

    Wählen Sie **Benutzerdefiniert** aus, wenn eine zuvor erstellte globale Bedingung verwendet werden soll. Bei Auswahl von **Benutzerdefiniert** können Sie auch **Erstellen** auswählen, um eine neue globale Bedingung zu erstellen. Weitere Informationen über globale Bedingungen finden Sie unter [Erstellen von globalen Bedingungen](create-global-conditions.md).  

    > [!IMPORTANT]  
    > Der Client ignoriert sämtliche Anforderungen der Kategorie **Benutzer** mit der Bedingung **Primäres Gerät**, wenn Sie die Anwendung für eine Gerätesammlung bereitstellen.  

3. Wählen Sie in der Dropdownliste **Bedingung** die Bedingung aus, anhand derer bewertet werden soll, ob der Benutzer bzw. das Gerät den Installationsanforderungen entspricht. Die Inhalte dieser Liste sind von der ausgewählten Kategorie abhängig.  

4. Wählen Sie aus der Dropdownliste **Operator** den zu verwendenden Operator aus. Dieser Operator vergleicht die ausgewählte Bedingung mit dem angegebenen Wert. Er bewertet, ob der Benutzer bzw. das Gerät die Installationsanforderung erfüllt. Welche Operatoren verfügbar sind, ist von der ausgewählten Bedingung abhängig.  

    > [!Note]  
    > Die verfügbaren Anforderungen variieren je nach Gerätetyp, die der Bereitstellungstyp verwendet.  

5. Geben Sie im Feld **Wert** die Werte an, die für den Vergleich verwendet werden sollen. Diese Werte werden, zusammen mit der ausgewählten Bedingung und dem Operator, verwendet, um zu bewerten, ob der Benutzer bzw. das Gerät die Installationsanforderungen erfüllt. Welche Werte verfügbar sind, hängt von der ausgewählten Bedingung und dem ausgewählten Operator ab.  

6. Wählen Sie **OK** aus, um die Anforderung zu speichern und das Dialogfeld **Anforderung erstellen** zu schließen.  

### <a name="deployment-type-dependencies"></a><a name="bkmk_dt-depend"></a>**Abhängigkeiten** des Bereitstellungstyps  

Mit Abhängigkeiten wird mindestens ein Bereitstellungstyp einer anderen Anwendung definiert, der vom Client installiert werden muss, bevor der eigentliche Bereitstellungstyp installiert wird.

> [!IMPORTANT]  
> In einigen Fällen ist ein Bereitstellungstyp von einem Bereitstellungstyp abhängig, der ebenfalls über Abhängigkeiten verfügt. Die maximale Anzahl unterstützter Abhängigkeiten in der Kette beträgt fünf.  

1. Klicken Sie auf der Seite **Abhängigkeiten** auf die Option **Hinzufügen**.  

2. Geben Sie im Fenster „Abhängigkeit hinzufügen“ den **Name der Abhängigkeitsgruppe** ein. Dieser Name bezieht sich auf diese Gruppe von Anwendungsabhängigkeiten.  

3. Klicken Sie im Fenster „Abhängigkeit hinzufügen“ auf **Hinzufügen**.  

4. Wählen Sie im Fenster **Erforderliche Anwendung angeben** eine verfügbare Anwendung und mindestens einen zugehörigen Bereitstellungstyp aus, der als Abhängigkeit verwendet werden soll.  

    > [!TIP]  
    > Wählen Sie **Anzeigen** aus, um die Eigenschaften der ausgewählten Anwendung bzw. des ausgewählten Bereitstellungstyps anzuzeigen.  

5. Wählen Sie **OK** aus, um das Fenster **Erforderliche Anwendung angeben** zu schließen.  

6. Wenn Sie möchten, dass der Client die abhängige Anwendung automatisch installiert, wählen Sie **Automatisch installieren** neben der Abhängigkeit aus.  

    > [!NOTE]  
    > Eine abhängige Anwendung muss nicht bereitgestellt werden, damit der Client sie automatisch installiert.  

7. Wenn Sie mehrere Abhängigkeiten hinzufügen möchten, verwenden Sie die Schaltflächen **Priorität erhöhen** und **Priorität verringern**. Diese Aktionen ändern die Reihenfolge, in welcher der Client die einzelnen Abhängigkeiten bewertet.  

8. Wählen Sie **OK** aus, um das Fenster **Abhängigkeit hinzufügen** zu schließen.  

### <a name="deployment-type-return-codes"></a><a name="bkmk_dt-return"></a>**Rückgabecodes** des Bereitstellungstyps

> [!Note]  
> Diese Seite befindet sich nicht im Assistenten zum Erstellen neuer Bereitstellungstypen. Vielmehr handelt es sich hierbei um eine Registerkarte unter den Eigenschaften eines vorhandenen Bereitstellungstyps.  

Geben Sie zur Steuerung des Verhaltens nach Abschluss des Bereitstellungstyps Rückgabecodes an. Signalisieren Sie beispielsweise, dass ein Neustart erforderlich ist oder dass die Installation abgeschlossen ist.

1. Wählen Sie auf der Registerkarte **Rückgabecodes** im Eigenschaftenfenster des Bereitstellungstyps **Hinzufügen** aus.  

2. Geben Sie im Fenster „Rückgabecode hinzufügen“ den **Rückgabecodewert** an, den Sie von diesem Bereitstellungstyp erwarten. Bei diesem Wert handelt es sich um eine positive oder negative ganze Zahl zwischen `-2147483648` und `2147483647`.  

3. Wählen Sie in der Dropdownliste einen **Codetyp** aus. Mit dieser Einstellung wird festgelegt, wie Configuration Manager den angegebenen Rückgabecode für diesen Bereitstellungstyp interpretiert. Je nach Technologie des Bereitstellungstyps sind unterschiedliche Typen verfügbar.  

    - **Erfolgreich (kein Neustart):** Der Bereitstellungstyp wurde erfolgreich installiert, und es ist kein Neustart erforderlich.  

    - **Fehler (kein Neustart):** Der Bereitstellungstyp konnte nicht installiert werden.  

    - **Harter Neustart:** Der Bereitstellungstyp wurde erfolgreich installiert. Das Gerät muss neu gestartet werden. Erst nach einem Neustart des Geräts können weitere Installationen ausgeführt werden.  

    - **Warmneustart:** Der Bereitstellungstyp wurde erfolgreich installiert. Es wird jedoch ein Neustart des Geräts angefordert. Weitere Installationen können vor dem Neustart des Geräts ausgeführt werden.  

    - **Schneller Neuversuch:** Auf dem Gerät wird bereits eine weitere Installation ausgeführt. Der Client wiederholt den Vorgang alle zwei Stunden und das insgesamt zehnmal.  

4. Geben Sie optional einen **Namen** und eine **Beschreibung** für diesen Rückgabecode ein.

5. Wählen Sie **OK** aus, um das Fenster „Rückgabecode hinzufügen“ zu schließen.  

#### <a name="example-non-zero-success"></a>Beispiel: nicht null (0) bei Erfolg

Sie stellen eine Anwendung bereit, die bei einer erfolgreichen Installation den Exitcode `1` zurückgibt. Standardmäßig erkennt Configuration Manager diesen Rückgabecode ungleich null als nicht erfolgreiche Installation. Geben Sie für den Rückgabecode den Wert `1` an, und wählen Sie den Codetyp **Erfolgreich (kein Neustart)** aus. Nun interpretiert Configuration Manager diesen Rückgabecode als erfolgreiche Installation für diesen Bereitstellungstyp.

#### <a name="default-return-codes"></a>Standardrückgabecodes

Wenn Sie bestimmte Bereitstellungstypen erstellen, fügt Configuration Manager automatisch folgende für diese Technologie gängige Rückgabecodes hinzu:  

##### <a name="windows-installer-msi-file"></a>Windows Installer (\*.msi)

|Wert    |Codetyp|
|---------|---------|
|0        |Erfolgreich (kein Neustart)|
|1707     |Erfolgreich (kein Neustart)|
|3010     |Softneustart|
|1641     |Harter Neustart|
|1618     |Schneller Neuversuch|

##### <a name="script-installer"></a>Skriptinstallationsprogramm

|Wert    |Codetyp|
|---------|---------|
|0        |Erfolgreich (kein Neustart)|
|1641     |Harter Neustart|
|3010     |Softneustart|
|1618     |Schneller Neuversuch|

##### <a name="windows-app-package-appx-appxbundle-msix-msixbundle"></a>Windows-App-Paket (\*.appx, \*.appxbundle, \*.msix, \*.msixbundle)

|Wert    |Codetyp|
|---------|---------|
|15605    |Schneller Neuversuch|
|15618    |Schneller Neuversuch|

## <a name="additional-options-for-app-v-deployment-types"></a><a name="bkmk_appv"></a> Weitere Optionen für App-V-Bereitstellungstypen  

Konfigurieren Sie zusätzliche Optionen, die nur für Bereitstellungstypen für virtuelle Anwendungen (App-V) verwendet werden.  

### <a name="app-v-deployment-type-content-options"></a><a name="bkmk_appv-content"></a> Optionen für den **Inhalt** des App-V-Bereitstellungstyps  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie **Anwendungsverwaltung**, und wählen Sie den Knoten **Anwendungen** aus.  

2. Wählen Sie eine Anwendung mit einem App-V-Bereitstellungstyp aus, und wählen Sie **Eigenschaften**.  

3. Wechseln Sie in den Anwendungseigenschaften zur Registerkarte **Bereitstellungstypen**. Wählen Sie den App-V-Bereitstellungstyp aus, und wählen Sie **Bearbeiten**.  

4. Wechseln Sie in den Eigenschaften für den Bereitstellungstyp zur Registerkarte **Inhalt**. Konfigurieren Sie ggf. folgende Optionen:  

    - **Inhalt dauerhaft in Clientcache speichern:** Der Inhalt für diesen Bereitstellungstyp wird im Cache des Konfigurations-Manager-Clients nicht gelöscht.  

    - **Inhalt vor dem Start in den App-V-Cache laden:** Vor dem Starten der Anwendung wird der gesamte Inhalt für diesen Bereitstellungstyp in den App-V-Cache geladen. Der Inhalt wird nicht im Cache fixiert. Er wird nach Bedarf gelöscht.  

5. Wählen Sie **OK** aus, um die Eigenschaften des Bereitstellungstyps zu schließen. Wählen Sie anschließend **OK** aus, um die Eigenschaften der Anwendung zu schließen.  

### <a name="app-v-deployment-type-publishing-options"></a><a name="bkmk_appv-pub"></a> Optionen für die **Veröffentlichung** des App-V-Bereitstellungstyps

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie **Anwendungsverwaltung**, und wählen Sie den Knoten **Anwendungen** aus.  

2. Wählen Sie eine Anwendung mit einem App-V-Bereitstellungstyp aus, und wählen Sie **Eigenschaften**.  

3. Wechseln Sie in den Anwendungseigenschaften zur Registerkarte **Bereitstellungstypen**. Wählen Sie den App-V-Bereitstellungstyp aus, und wählen Sie **Bearbeiten**.  

4. Wechseln Sie in den in den Eigenschaften für den Bereitstellungstyp zur Registerkarte **Veröffentlichung**. Wählen Sie in der virtuellen Anwendung die Elemente aus, die Sie veröffentlichen möchten.  

5. Wählen Sie **OK** aus, um die Eigenschaften des Bereitstellungstyps zu schließen. Wählen Sie anschließend **OK** aus, um die Eigenschaften der Anwendung zu schließen.  

## <a name="import-an-application"></a><a name="bkmk_import"></a> Importieren einer Anwendung  

Gehen Sie wie folgt vor, um eine Anwendung in Configuration Manager zu importieren:

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie **Anwendungsverwaltung**, und wählen Sie den Knoten **Anwendungen** aus.  

2. Wählen Sie auf der Registerkarte **Start** des Menübands in der Gruppe **Erstellen** die Option **Anwendung importieren** aus.  

3. Geben Sie auf der Seite **Allgemein** des Assistenten zum Importieren von Anwendungen den Netzwerkpfad zu der **Datei** an, die importiert werden soll. Beispiel: `\\server\share\file.zip`. Hierbei handelt es sich um ein gültiges komprimiertes Archiv (ZIP-Format) einer exportierten Configuration Manager-Anwendung.  

4. Wählen Sie auf der Seite **Dateiinhalt** die Aktion aus, die ausgeführt werden soll, wenn diese Anwendung das Duplikat einer vorhandenen Anwendung ist. Erstellen Sie eine neue Anwendung, oder ignorieren Sie das Duplikat, und fügen Sie eine neue Revision zur vorhandenen Anwendung hinzu.  

5. Überprüfen Sie auf der Seite **Zusammenfassung** die Aktionen, und schließen Sie dann den Assistenten ab.  

Die neue Anwendung wird im Knoten **Anwendungen** angezeigt.  

> [!TIP]  
> Das Windows PowerShell-Cmdlet **Import-CMApplication** hat die gleiche Funktion wie dieses Verfahren. Weitere Informationen finden Sie unter [Import-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmapplication?view=sccm-ps).  

Weitere Informationen zum Exportieren von Anwendungen finden Sie unter [Verwaltungsaufgaben für Anwendungen](management-tasks-applications.md).

## <a name="supported-deployment-types"></a><a name="bkmk_deploy-types"></a> Unterstützte Bereitstellungstypen  

Configuration Manager unterstützt die Bereitstellung folgender Bereitstellungstypen für Anwendungen:

| Name des Bereitstellungstyps | Beschreibung |
|--------------------------|----------------------|  
| **Windows Installer (\*msi-Datei)** | Windows Installer-Datei |  
| **Windows-App-Paket (\*.appx, \*.appxbundle, \*.msix, \*.msixbundle)** | Windows-App-Paketdatei (.appx), Windows-App-Bundlepaket (.appxbundle), Windows 10-App-Paket (.msix) oder Windows 10-App-Bundle (.msixbundle).<!--1357427--> |  
| **Windows-App-Paket (im Windows Store)** | Geben Sie einen Link zur App im Windows Store an, oder durchsuchen Sie den Store, um die App auszuwählen.<sup>[Hinweis 1](#bkmk_note1)</sup> |  
| **Skriptinstallationsprogramm** | Geben Sie ein Skript oder ein Programm an, das auf Windows-Clients ausgeführt wird, um Inhalte zu installieren oder eine Aktion auszuführen. Verwenden Sie diesen Bereitstellungstyp für Installer vom Typ „setup.exe“ oder Skriptwrapper. |  
| **Microsoft Application Virtualization 4** | Manifest für Microsoft App-V v4 |  
| **Microsoft Application Virtualization 5** | Paketdatei für Microsoft App-V v5 |  
| **Windows Phone-App-Paket (\*.xap-Datei)** | Windows Phone-App-Paketdatei |  
| **Windows Phone-App-Paket (in Windows Phone Store)** | Geben Sie einen Link zur App im Windows Store an. |  
| **Mac OS X** | Für macOS-Computer, auf denen der Konfigurations-Manager-Client ausgeführt wird. Erstellen Sie mit dem Tool **CMAppUtil** eine CMMAC-Datei. |  
| **Webanwendung** | Geben Sie einen Link zu einer Webanwendung an. Mit dem Bereitstellungstyp wird auf dem Gerät des Benutzers eine Verknüpfung mit der Webanwendung installiert. |  
| **Windows Installer über die Verwaltung mobiler Geräte (\*.msi)** | Erstellen Sie Windows Installer-basierte Apps, und stellen Sie diese auf Windows 10-Geräten bereit. Weitere Informationen finden Sie unter [Bereitstellen von Windows Installer-Apps auf MDM-registrierten Windows 10-Geräten](../get-started/creating-windows-applications.md#bkmk_mdm-msi). |
| **Tasksequenz** | Ab Version 2002 können Sie komplexe Anwendungen mithilfe von Tasksequenzen installieren oder deinstallieren. Weitere Informationen finden Sie unter [Tasksequenz-Bereitstellungstyp](../get-started/creating-windows-applications.md#bkmk_tsdt). <!--3555953--> |

> [!NOTE]
> In der Configuration Manager-Konsole werden möglicherweise weitere Bereitstellungstypen angezeigt, aber diese gehören zu Plattformen, die nicht mehr unterstützt werden. Weitere Informationen finden Sie unter [Hybride Verwaltung mobiler Geräte](../../mdm/understand/what-happened-to-hybrid.md).

### <a name="note-1-windows-app-package-in-the-windows-store"></a><a name="bkmk_note1"></a> Hinweis 1: Windows-App-Paket (im Windows Store)

Konfigurieren Sie die Gruppenrichtlinie **Store-Anwendung deaktivieren**, um die App als Link zum Windows Store bereitzustellen. Legen Sie diese Richtlinie auf **deaktiviert** oder **nicht konfiguriert** fest. Wenn Sie diese Einstellung aktivieren, können Clients keine Verbindung mit dem Windows Store zum Herunterladen und Installieren von Anwendungen herstellen.

Bereitstellungstypen, bei denen ein Link zu einem Store verwendet wird, werden von Windows-Clients immer vor anderen Bereitstellungstypen ausgewertet. Erst danach werden Bereitstellungstypen nach Priorität ausgewertet.

> [!TIP]
> Einige Speicherlinks können den folgenden Fehler im Assistenten zum Erstellen von Anwendungen auslösen: „Ungültiger Anwendungslink“. Beispielsweise können manche vom Store *ausgewählten Apps* diesen Fehler auslösen. Sie können dann aber trotzdem auf der Seite **Allgemein** des Assistenten die Option **Weiter** auswählen. Configuration Manager erstellt die App dann, und Sie können sie bereitstellen.<!-- SCCMDocs-pr #4716 -->

## <a name="next-steps"></a>Nächste Schritte

Nach der Erstellung einer Anwendung in Configuration Manager ist der nächste Schritt das [Bereitstellen der Anwendung](deploy-applications.md).

Ab Version 1906 können Sie eine Gruppe von Anwendungen erstellen, die Sie als einzelne Bereitstellung an eine Benutzer- oder Gerätesammlung senden können. Weitere Informationen finden Sie unter [Create application groups](create-app-groups.md) (Erstellen von Anwendungsgruppen).

Weitere Informationen zum Erstellen von Anwendungen auf verschiedenen Betriebssystemplattformen finden Sie in folgenden Artikeln:  

- [Erstellen von Windows-Anwendungen](../get-started/creating-windows-applications.md)
- [Erstellen von Anwendungen für Macintosh-Computer](../get-started/creating-mac-computer-applications.md)
- [Erstellen von Linux- und UNIX-Serveranwendungen](../get-started/creating-linux-and-unix-server-applications.md)
- [Erstellen von Windows Embedded-Anwendungen](../get-started/creating-windows-embedded-applications.md)
