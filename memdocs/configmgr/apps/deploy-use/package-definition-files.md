---
title: Paketdefinitionsdateien
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über die Verwendung von Paketdefinitionsdateien zur Erstellung von Paketen und Programmen in Configuration Manager.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2de963d7-ffb9-43c3-9e1d-fc992b67bebd
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 0d2d0dcad06c18b13b337185ae1feb768a7ee323
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689328"
---
# <a name="package-definition-files"></a>Paketdefinitionsdateien

*Gilt für: Configuration Manager (Current Branch)*

Paketdefinitionsdateien sind Skripts, die Ihnen helfen, die Erstellung von [Paketen und Programmen](packages-and-programs.md) in Configuration Manager zu automatisieren. Sie enthalten alle Informationen, die von Configuration Manager benötigt werden, um ein Paket und Programm zu erstellen (außer dem Speicherort der Paketquelldateien).

## <a name="about-the-package-definition-file-format"></a>Informationen zum Format von Paketdefinitionsdateien

Jede Paketdefinitionsdatei liegt als ASCII- oder UTF-8-Textdatei im INI-Dateiformat vor. Sie enthält die folgenden Abschnitte:  

### <a name="pdf"></a>[PDF]

Dieser Abschnitt kennzeichnet die Datei als Paketdefinitionsdatei. Es enthält die folgende Informationen:  

- **Version:** Geben Sie hier die Version des Paketdefinitionsdateiformats an, das von der Datei verwendet wird. Diese Version entspricht der Version von Configuration Manager, für die sie geschrieben wurde. Dieser Eintrag ist obligatorisch.  

### <a name="package-definition"></a>[Package Definition]

Geben Sie hier die Eigenschaften des Pakets und des Programms an. Es enthält die folgende Informationen:  

- **Name:** Der Name des Pakets, bis zu 50 Zeichen.  

- **Version** (optional): Die Version des Pakets, bis zu 32 Zeichen.  

- **Symbol** (optional): Die Datei, die das für dieses Paket zu verwendende Symbol enthält. Wenn angegeben, ersetzt dieses Symbol das Standardpaketsymbol in der Configuration Manager-Konsole.

- **Herausgeber**: Der Herausgeber des Pakets, bis zu 32 Zeichen.

- **Sprache:** Die Sprachversion des Pakets, bis zu 32 Zeichen.

- **Kommentar** (optional): Ein Kommentar zum Paket, bis zu 127 Zeichen.

- **ContainsNoFiles**: Dieser Eintrag gibt an, ob das Paket über Quelldateien verfügt.  

- **Programme:** Die Programme, die Sie für dieses Paket definieren. Jeder Programmname entspricht einem **[Program]** -Abschnitt in dieser Paketdefinitionsdatei.  

    Beispiel:  

    `Programs=Typical, Custom, Uninstall`  

- **MIFFileName**: Der Name der MIF-Datei (Management Information Format), die den Paketstatus enthält, bis zu 50 Zeichen.  

- **MIFName**: Der Name des Pakets für den MIF-Abgleich, bis zu 50 Zeichen.  

- **MIFVersion**: Die Versionsnummer des Pakets für den MIF-Abgleich, bis zu 32 Zeichen.  

- **MIFPublisher**: Der Softwareherausgeber des Pakets für den MIF-Abgleich, bis zu 32 Zeichen.  

### <a name="program"></a>[Program]

Fügen Sie für jedes Programm, das Sie im Eintrag **Programme** im Abschnitt **[Package Definition]** angeben, einen Abschnitt [Program] ein. In diesem Abschnitt werden die einzelnen Programme definiert. Jeder Programmabschnitt enthält die folgenden Informationen:  

- **Name:** Der Name des Programms, bis zu 50 Zeichen. Dieser Eintrag muss innerhalb eines Pakets eindeutig sein.  

- **Symbol** (optional): Geben Sie hier die Datei an, die das für dieses Programm zu verwendende Symbol enthält. Dieses Symbol ersetzt das Standardprogrammsymbol in der Configuration Manager-Konsole. Der Client zeigt dieses Symbol auch an, wenn Sie das Programm in einer Sammlung bereitstellen.

- **Kommentar** (optional): Ein Kommentar zum Programm, bis zu 127 Zeichen.

- **CommandLine:** Geben Sie die Befehlszeile für das Programm an, bis zu 127 Zeichen. Der Befehl ist relativ zum Paketquellordner.

- **StartIn:** Geben Sie hier den Arbeitsordner für das Programm an, bis zu 127 Zeichen. Dies kann ein absoluter Pfad auf dem Clientcomputer oder ein Pfad relativ zum Paketquellordner sein.

- **Run**: Geben Sie hier den Programmmodus an, in dem das Programm ausgeführt wird. Sie können **Minimized**, **Maximized**oder **Hidden**angeben. Wenn Sie diesen Eintrag nicht einbeziehen, wird das Programm im normalen Modus ausgeführt.  

- **AfterRunning:** Geben Sie hier alle speziellen Aktionen an, die nach dem erfolgreichen Programmabschluss ausgeführt werden sollen. Die verfügbaren Optionen sind **SMSRestart**, **ProgramRestart**, oder **SMSLogoff**. Wenn Sie diesen Eintrag nicht einbeziehen, führt das Programm keine spezielle Aktion aus.  

- **EstimatedDiskSpace:** Geben Sie hier den Speicherplatz an, der zur Ausführung des Programms auf dem Computer erforderlich ist. Der Standardwert ist **Unknown** (Unbekannt). Sie können den Wert als Ganzzahl größer oder gleich null festlegen. Wenn Sie einen Wert angeben, fügen Sie auch die Einheiten für den Wert hinzu.  

    Beispiel:  

    `EstimatedDiskSpace=38MB`  

- **EstimatedRunTime:** Geben Sie hier in Minuten an, wie lange das Programm voraussichtlich auf dem Clientcomputer ausgeführt wird. Der Standardwert ist **120**. Sie können den Wert als Ganzzahl größer null oder als **Unbekannt** festlegen.  

    Beispiel:  

    `EstimatedRunTime=25`  

- **SupportedClients:** Geben Sie die Prozessoren und Betriebssysteme an, auf denen das Programm ausgeführt wird. Trennen Sie die Plattformen durch Kommas. Wenn Sie diesen Eintrag nicht einbeziehen, prüft der Client die unterstützten Plattformen für dieses Programm nicht.  

- **SupportedClientMinVersionX**, **SupportedClientMaxVersionX**: Gibt den Bereich der minimalen bis zur maximalen Versionsnummer für die im Eintrag **SupportedClients** angegebenen Betriebssysteme an.  

    Beispiel:  

    ```INI
    SupportedClients=Win NT (I386),Win NT (IA64),Win NT (x64)  
    Win NT (I386) MinVersion1=5.00.2195.4  
    Win NT (I386) MaxVersion1=5.00.2195.4  
    Win NT (I386) MinVersion2=5.10.2600.2  
    Win NT (I386) MaxVersion2=5.10.2600.2  
    Win NT (I386) MinVersion3=5.20.0000.0  
    Win NT (I386) MaxVersion3=5.20.9999.9999  
    Win NT (I386) MinVersion4=5.20.3790.0  
    Win NT (I386) MaxVersion4=5.20.3790.2  
    Win NT (I386) MinVersion5=6.00.0000.0  
    Win NT (I386) MaxVersion5=6.00.9999.9999  
    Win NT (IA64) MinVersion1=5.20.0000.0  
    Win NT (IA64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion1=5.20.0000.0  
    Win NT (x64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion2=5.20.3790.0  
    Win NT (x64) MaxVersion2=5.20.9999.9999  
    Win NT (x64) MinVersion3=5.20.3790.0  
    Win NT (x64) MaxVersion3=5.20.3790.2  
    Win NT (x64) MinVersion4=6.00.0000.0  
    Win NT (x64) MaxVersion4=6.00.9999.9999
    ```  

- **AdditionalProgramRequirements** (optional): Geben Sie alle beliebigen, anderen Informationen oder Anforderungen zu Clientcomputern an, bis zu 127 Zeichen.

- **CanRunWhen:** Gibt den Benutzerstatus an, der für die Ausführung des Programms auf dem Clientcomputer erforderlich ist. Es stehen die Werte **UserLoggedOn**, **NoUserLoggedOn**, oder **AnyUserStatus**zur Verfügung. Der Standardwert ist **UserLoggedOn**.  

- **UserInputRequired:** Geben Sie hier an, ob das Programm Benutzereingriffe erfordert. Es stehen die Werte **True** oder **False**zur Verfügung. Der Standardwert ist **True**. Dieser Eintrag ist auf **False** festgelegt, wenn **CanRunWhen** nicht auf **UserLoggedOn**festgelegt ist.  

- **AdminRightsRequired:** Geben Sie hier an, ob administrative Anmeldeinformationen zur Ausführung des Programms auf dem Computer erforderlich sind. Es stehen die Werte **True** oder **False**zur Verfügung. Der Standardwert ist **False**. Dieser Eintrag ist auf **True** festgelegt, wenn **CanRunWhen** nicht auf **UserLoggedOn**festgelegt ist.  

- **UseInstallAccount**: Geben Sie hier an, ob das Programm das Konto für die Clientsoftwareinstallation verwendet, wenn es auf Clientcomputern ausgeführt wird. Standardmäßig ist dieser Wert **False**. Der Wert ist auch dann **False** , wenn **CanRunWhen** auf **UserLoggedOn**festgelegt ist.  

- **DriveLetterConnection:** Geben Sie hier an, ob das Programm bei der Verbindung mit den Paketdateien auf dem Verteilungspunkt die Angabe des Laufwerkbuchstabens erfordert. Sie können entweder **True** oder **False**angeben. Der Standardwert ist **False**, was dem Programm die Verwendung einer UNC-Verbindung (Universal Naming Convention) ermöglicht. Wenn dieser Wert auf **True** festgelegt ist, verwendet der Client den nächsten verfügbaren Laufwerkbuchstaben, beginnend mit „Z:“ und in absteigender Reihenfolge.  

- **SpecifyDrive** (optional): Geben Sie hier einen Laufwerkbuchstaben an, den das Programm zum Herstellen der Verbindung mit den Paketdateien auf dem Verteilungspunkt benötigt. Diese Einstellung erzwingt die Verwendung des angegebenen Laufwerkbuchstabens für Clientverbindungen mit Verteilungspunkten.

- **ReconnectDriveAtLogon**: Geben Sie an, ob der Computer die Verbindung mit dem Verteilungspunkt bei der Anmeldung des Benutzers erneut herstellen soll. Es stehen die Werte **True** oder **False**zur Verfügung. Der Standardwert ist **False**.  

- **DependentProgram:** Geben Sie hier ein Programm an, das sich in diesem Paket befindet und vor dem aktuellen Programm ausgeführt werden muss. Für diesen Eintrag wird folgendes Format verwendet: `DependentProgram=<ProgramName>`, wobei `<ProgramName>` den **Namen** für das Programm in der Paketdefinitionsdatei darstellt. Lassen Sie den Eintrag leer, wenn keine abhängigen Programme vorhanden sind.  

    Beispiele:  

    `DependentProgram=Admin`  
    `DependentProgram=`  

- **Zuweisung:** Geben Sie hier an, wie das Programm Benutzern zugewiesen wird. Folgende Werte sind zulässig:

    - **FirstUser**: Nur der erste Benutzer, der sich beim Client anmeldet, führt das Programm aus.
    - **EveryUser**: Jeder Benutzer, der sich anmeldet, führt das Programm aus.

    Dieser Eintrag ist auf **FirstUser** festgelegt, wenn **CanRunWhen** nicht auf **UserLoggedOn** festgelegt ist.  

- **Deaktiviert:** Geben Sie an, ob Sie dieses Programm für Clients bereitstellen können. Es stehen die Werte **True** oder **False**zur Verfügung. Der Standardwert ist **False**.  


## <a name="use-a-package-definition-file"></a>Verwenden einer Paketdefinitionsdatei  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie **Anwendungsverwaltung**, und wählen Sie den Knoten **Pakete** aus.  

2. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Erstellen** die Option **Paket aus Definition erstellen** aus.  

3. Wählen Sie im **Assistenten zum Erstellen eines Pakets aus einer Definition** auf der Seite **Paketdefinition** eine vorhandene Paketdefinitionsdatei aus. Wählen Sie **Durchsuchen** aus, um eine neue Paketdefinitionsdatei zu öffnen. Nachdem Sie eine neue Paketdefinitionsdatei angegeben haben, wählen Sie sie in der Liste **Paketdefinition** aus.

4. Geben Sie auf der Seite **Quelldateien** Informationen zu ggf. erforderlichen Quelldateien für das Paket und Programm an.  

5. Wenn für das Paket Quelldateien erforderlich sind, geben Sie auf der Seite **Quellordner** den Speicherort zum Abrufen der Quelldateien an.  

6. Schließen Sie den Assistenten ab.  


## <a name="see-also"></a>Weitere Informationen:

[Pakete und Programme](packages-and-programs.md)
