---
title: Erstellen benutzerdefinierter Konfigurationselemente
titleSuffix: Configuration Manager
description: Verwalten von Einstellungen für Windows-Computer und -Server mithilfe eines benutzerdefinierten Konfigurationselements für Windows-Desktop- und -Servercomputer
ms.date: 04/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 1eb2fcaf-acac-4388-9b31-6cccafacaabe
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 24637862326b029f974843c18ccba835ee5501ba
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240421"
---
# <a name="create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-configuration-manager-client"></a>Erstellen benutzerdefinierter Konfigurationselemente für Windows-Desktop- und -Servercomputer, die mit dem Configuration Manager-Client verwaltet werden

*Gilt für: Configuration Manager (Current Branch)*


Verwenden Sie das Configuration Manager-Konfigurationselement des Typs **Windows-Desktops und -Server (benutzerdefiniert)** zum Verwalten der Einstellungen für Windows-Computer und -Server, die durch den Configuration Manager-Client verwaltet werden.  



## <a name="start-the-wizard"></a>Starten des Assistenten

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Bestand und Konformität**, erweitern Sie **Konformitätseinstellungen**, und wählen Sie den Knoten **Konfigurationselemente** aus.  

2. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Erstellen** die Option **Konfigurationselement erstellen** aus.  

3. Geben Sie auf der Seite **Allgemein** des **Assistenten zum Erstellen von Konfigurationselementen**einen Namen und optional eine Beschreibung für das Konfigurationselement an.  

4. Wählen Sie unter **Typ des zu erstellenden Konfigurationselements angeben**den Typ **Windows-Desktops und -Server (benutzerdefiniert)** aus.  

    > [!TIP]  
    > Wenn Sie Einstellungen für Erkennungsmethoden bereitstellen möchten, mit denen überprüft wird, ob eine Anwendung vorhanden ist, wählen Sie **Dieses Konfigurationselement enthält Anwendungseinstellungen**aus.  

5. Um das Durchsuchen und Filtern von Konfigurationselementen in der Configuration Manager-Konsole zu erleichtern, wählen Sie **Kategorien** aus, um Kategorien zu erstellen und zuzuweisen.  



## <a name="detection-methods"></a>Erkennungsmethoden  

Verwenden Sie dieses Verfahren, um Informationen zur Erkennungsmethode für das Konfigurationselement bereitzustellen.  

> [!NOTE]  
> Diese Informationen gelten nur, wenn Sie **Dieses Konfigurationselement enthält Anwendungseinstellungen** auf der Seite **Allgemein** des Assistenten ausgewählt haben.  

Eine Erkennungsmethode in Configuration Manager enthält Regeln zur Erkennung, ob eine Anwendung auf einem Computer installiert ist. Diese Erkennung erfolgt, bevor der Client die Konformität des Konfigurationselements bewertet. Um zu erkennen, ob eine Anwendung installiert ist, können Sie die Anwesenheit einer Windows Installer-Datei für die Anwendung prüfen, ein benutzerdefiniertes Skript verwenden oder **Immer annehmen, dass die Anwendung installiert ist** auswählen, um die Konformität des Konfigurationselements unabhängig davon zu bewerten, ob die Anwendung installiert ist.  


### <a name="to-detect-an-application-installation-by-using-the-windows-installer-file"></a>So erkennen Sie eine Anwendungsinstallation anhand der Windows Installer-Datei  

1. Wählen Sie auf der Seite **Erkennungsmethoden** des **Assistenten zum Erstellen von Konfigurationselementen** die Option **Windows Installer-Erkennung verwenden**  aus.  

2. Wählen Sie **Öffnen** aus, suchen Sie die Windows Installer (MSI)-Datei, die Sie erkennen möchten, und wählen Sie dann **Öffnen** aus.  

3. Das Feld **Version** wird automatisch mit der Versionsnummer der ausgewählten Windows Installer-Datei aufgefüllt. Geben Sie hier eine neue Versionsnummer ein, wenn der angezeigte Wert nicht korrekt ist.  

4. Wenn jedes Benutzerprofil auf dem Computer erkannt werden soll, wählen Sie **Diese Anwendung wurde für mindestens einen Benutzer installiert** aus.  


### <a name="to-detect-a-specific-application-and-deployment-type"></a>So erkennen Sie einen bestimmten Anwendungs- und Bereitstellungstyp  

1. Wählen Sie auf der Seite **Erkennungsmethoden** des **Assistenten zum Erstellen von Konfigurationselementen** die Option **Einen bestimmten Anwendungs- und Bereitstellungstyp erkennen** aus. Klicken Sie auf **Auswählen**.   

2. Wählen Sie im Dialogfeld **Anwendung angeben** die Anwendung und einen zugeordneten Bereitstellungstyp aus, den Sie erkennen möchten.  


### <a name="to-detect-an-application-installation-by-using-a-custom-script"></a>So erkennen Sie eine Anwendungsinstallation mithilfe eines benutzerdefinierten Skripts  

1. Wählen Sie auf der Seite **Erkennungsmethoden** des **Assistenten zum Erstellen von Konfigurationselementen** die Option **Benutzerdefiniertes Skript zum Erkennen dieser Anwendung verwenden** aus.  

2. Wählen Sie in der Liste die Sprache des Skripts aus. Wählen Sie aus den folgenden Formaten:  

    - **VBScript**  

    - **JScript**  

    - **PowerShell**  

        > [!Note]  
        > Ab Version 1810 ruft der Configuration Manager-Client PowerShell mit dem Parameter `-NoProfile` auf, wenn ein Windows PowerShell-Skript als Erkennungsmethode ausgeführt wird. Diese Option startet PowerShell ohne Profile. Ein PowerShell-Profil ist ein Skript, das ausgeführt wird, wenn PowerShell gestartet wird. <!--3607762-->  

3. Wählen Sie **Öffnen** aus, suchen Sie das Skript, das Sie verwenden möchten, und wählen Sie **Öffnen** aus.  



## <a name="specify-supported-platforms"></a>Angeben unterstützter Plattformen  

Wählen Sie auf der Seite **Unterstützte Plattformen** des **Assistenten zum Erstellen von Konfigurationselementen** die Windows-Versionen aus, auf denen die Konformität des Konfigurationselements bewertet werden soll, oder wählen Sie **Alle auswählen** aus.

Sie können auch die **Windows-Version manuell angeben**. Klicken Sie auf **Hinzufügen**, und geben Sie die Teile der Windows-Buildnummer an.

> [!NOTE]
> Bei der Angabe von Windows Server 2016 umfasst die Auswahl für `All Windows Server 2016 and higher 64-bit)` auch Windows Server 2019. Um nur Windows Server 2016 anzugeben, verwenden Sie die Option **Windows-Version manuell angeben**. <!--5866480-->



##  <a name="configure-settings"></a>Konfigurieren der Einstellungen  

Verwenden Sie dieses Verfahren zum Konfigurieren der Einstellungen im Konfigurationselement.  

Einstellungen repräsentieren die geschäftlichen oder technischen Maßnahmen, die zur Bewertung der Kompatibilität auf Clientcomputern verwendet werden. Sie können eine neue Einstellung konfigurieren oder eine bestehende Einstellung auf einem Referenzcomputer verwenden.  

1. Wählen Sie im **Assistenten zum Erstellen von Konfigurationselementen** auf der Seite **Einstellungen** die Option **Neu** aus.  

2. Geben Sie auf der Registerkarte **Allgemein** des Dialogfelds **Einstellung erstellen** die folgenden Informationen an:  

    - **Name:** Geben Sie einen eindeutigen Namen für die Einstellung ein. Sie können maximal 256 Zeichen verwenden.  

    - **Beschreibung:** Geben Sie eine Beschreibung für die Einstellung ein. Sie können maximal 256 Zeichen verwenden.  

    - **Einstellungstyp:** Wählen Sie in der Liste einen der folgenden Einstellungstypen aus, der für diese Einstellung verwendet werden soll, und konfigurieren Sie ihn:  
        - [Active Directory-Abfrage](#bkmk_adquery)
        - [Assembly](#bkmk_assembly)
        - [Dateisystem](#bkmk_file)
        - [IIS-Metabasis](#bkmk_iis)
        - [Registrierungsschlüssel](#bkmk_regkey)
        - [Registrierungswert](#bkmk_regval)
        - [Skript](#bkmk_script)
        - [SQL-Abfrage](#bkmk_sql)
        - [WQL-Abfrage](#bkmk_wql)
        - [XPath-Abfrage](#bkmk_xpath)

    - **Datentyp:** Wählen Sie das Format aus, in dem die Daten von der Bedingung zurückgegeben werden, bevor sie zum Bewerten der Einstellung verwendet werden. Die **Datentyp**-Liste wird nicht für alle Einstellungstypen angezeigt.  

        > [!Tip]  
        > Vom Datentyp **Gleitkomma** werden nur drei Ziffern nach dem Dezimalkomma unterstützt.  

3. Konfigurieren Sie zusätzliche Details zu dieser Einstellung unter der **Einstellungstyp** Liste. Die Elemente, die Sie konfigurieren können, variieren je nach der Einstellung, die Sie ausgewählt haben.  

4. Wählen Sie **OK** aus, um die Einstellung zu speichern, und schließen Sie das Dialogfeld **Einstellung erstellen**.  


### <a name="active-directory-query"></a><a name="bkmk_adquery"></a> Active Directory-Abfrage

- **LDAP-Präfix**: Geben Sie ein gültiges Präfix für die Active Directory-Domänendienste-Abfrage an, mit der die Konformität auf Clientcomputern bewertet wird. Verwenden Sie entweder `LDAP://` oder `GC://`, um eine globale Katalogsuche durchzuführen.  

- **Definierter Name (DN)** : Geben Sie den definierten Namen des Active Directory-Domänendienste-Objekts an, das auf Clientcomputern auf Kompatibilität bewertet wird.  

- **Suchfilter**: Geben Sie einen optionalen LDAP-Filter an, mit dem die Ergebnisse der Active Directory-Domänendiensteabfrage zur Bewertung der Kompatibilität auf Clientcomputern eingegrenzt werden. Geben Sie `(objectclass=*)` ein, um alle Ergebnisse der Abfrage zurückzugeben.  

- **Suchbereich**: Geben Sie den Suchbereich in den Active Directory-Domänendiensten an.  

    - **Basis**: Hiermit wird nur das angegebene Objekt abgefragt.  

    - **Eine Ebene**: Diese Option wird in dieser Version von Configuration Manager nicht verwendet.  

    - **Unterstruktur**: Hiermit werden das angegebene Objekt und dessen vollständige untergeordnete Struktur im Verzeichnis abgefragt.  

- **Eigenschaft**: Geben Sie die Eigenschaft des Active Directory-Domänendienste-Objekts an, das zur Bewertung der Kompatibilität auf Clientcomputern verwendet wird.  

    Wenn Sie beispielsweise die Active Directory-Eigenschaft abfragen möchten, die speichert, wie oft ein Benutzer ein Kennwort falsch eingibt, geben Sie `badPwdCount` in dieses Feld ein.  

- **Abfrage**: Zeigt die Abfrage an, die aus den Einträgen unter **LDAP-Präfix**, **Definierter Name (DN)** , **Suchfilter** (falls angegeben) und **Eigenschaft** erstellt wird.  


### <a name="assembly"></a><a name="bkmk_assembly"></a> Assembly

Eine Assembly ist ein Programmcode, der zwischen Anwendungen freigegeben werden kann. Assemblys können die Dateinamenerweiterung DLL oder EXE haben. Auf Clientcomputern ist der Ordner `%SystemRoot%\Assembly` der globale Assemblycache. In diesem Cache speichert Windows alle freigegebenen Assemblys.  

- **Assemblyname:** Gibt den Namen des Assemblyobjekts an, nach dem Sie suchen möchten. Der Name darf nicht mit anderen Assemblyobjekten vom gleichen Typ übereinstimmen. Registrieren Sie ihn zunächst im globalen Assemblycache. Der Assemblyname kann bis zu 256 Zeichen lang sein.  


### <a name="file-system"></a><a name="bkmk_file"></a> Dateisystem

- **Typ:** Wählen Sie in der Liste aus, ob Sie nach einer **Datei** oder nach einem **Ordner** suchen möchten.  

- **Pfad:** Geben Sie den Pfad der angegebenen Datei bzw. des Ordners auf Clientcomputern an. Sie können Systemumgebungsvariablen und die `%USERPROFILE%`-Umgebungsvariable im Pfad angeben.  

    > [!NOTE]  
    > Wenn Sie die Umgebungsvariable `%USERPROFILE%` in den Feldern **Pfad** oder **Datei- oder Ordnername** angeben, durchsucht der Konfigurations-Manager-Client alle Benutzerprofile auf dem Clientcomputer. Dieses Verhalten kann dazu führen, dass mehrere Instanzen der Datei oder des Ordners gefunden werden.  
    >   
    > Wenn die Kompatibilitätseinstellungen keinen Zugriff auf den angegebenen Pfad haben, wird ein Ermittlungsfehler generiert. Wenn die gesuchte Datei zurzeit verwendet wird, wird außerdem ein Ermittlungsfehler generiert.  

    > [!Tip]  
    > Klicken Sie auf **Durchsuchen**, um die Einstellung von Werten auf einem Referenzcomputer zu konfigurieren.   

- **Datei- oder Ordnername**: Geben Sie den Namen des zu suchenden Datei- oder Ordnerobjekts an. Sie können Systemumgebungsvariablen und die Umgebungsvariable `%USERPROFILE%` im Datei- oder Ordnernamen angeben. Sie können im Dateinamen auch die Platzhalter `*` und `?` verwenden.  

    > [!NOTE]  
    > Wenn Sie einen Datei- oder Ordnernamen angeben und dabei Platzhalter verwenden, kann diese Kombination zu einer großen Anzahl von Ergebnissen führen. Es kann auch zu hoher Ressourcenauslastung auf dem Clientcomputer und zu erhöhtem Netzwerkverkehr beim Berichten von Ergebnissen an Configuration Manager führen.  

- **Unterordner einbeziehen**: Mit dieser Option können Sie auch jegliche Unterordner im angegebenen Pfad durchsuchen.  

- **Diese Datei oder dieser Ordner ist mit einer 64-Bit-Anwendung verknüpft:** Wenn diese Option aktiviert ist, werden nur 64-Bit-Speicherorte wie `%ProgramFiles%` auf 64-Bit-Computern durchsucht. Wenn diese Option nicht aktiviert ist, werden sowohl 64-Bit- als auch 32-Bit-Speicherorte wie `%ProgramFiles(x86)%` durchsucht.  

    > [!NOTE]  
    > Wenn dieselbe Datei bzw. derselbe Ordner sowohl am 64-Bit-Systemdatei- als auch am 32-Bit-Systemdateispeicherort desselben 64-Bit-Computers vorhanden ist, werden von der globalen Bedingung mehrere Dateien ermittelt.  

    Die Angabe eines UNC-Pfads zu einer Netzwerkfreigabe im Feld **Pfad** wird vom Einstellungstyp **Dateisystem** nicht unterstützt.  


### <a name="iis-metabase"></a><a name="bkmk_iis"></a> IIS-Metabasis

- **Metabasispfad**: Geben Sie einen gültigen Pfad zur IIS-Metabasis (Internet Information Services, Internetinformationsdienste) an. Beispiel: `/LM/W3SVC/`.  

- **Eigenschafts-ID**: Geben Sie die numerische Eigenschaft für die IIS-Metabasiseinstellung an.  


### <a name="registry-key"></a><a name="bkmk_regkey"></a> Registrierungsschlüssel

- **Struktur:** Wählen Sie die Registrierungsstruktur aus, die Sie durchsuchen möchten.

    > [!Tip]  
    > Klicken Sie auf **Durchsuchen**, um die Einstellung von Werten auf einem Referenzcomputer zu konfigurieren. Aktivieren Sie den Dienst **Remoteregistrierung** auf dem Remotecomputer, um zu einem Registrierungsschlüssel auf einem Remotecomputer zu navigieren.  

- **Schlüssel:** Geben Sie den Namen des Registrierungsschlüssels an, nach dem gesucht werden soll. Verwenden Sie das Format `key\subkey`.  

- **Ist dieser Registrierungsschlüssel einer 64-Bit-Anwendung zugeordnet?** : Suche nach 64-Bit-Registrierungsschlüsseln zusätzlich zu den 32-Bit-Registrierungsschlüsseln auf Clients, die eine 64-Bit-Version von Windows ausführen.  

    > [!NOTE]  
    > Wenn derselbe Registrierungsschlüssel sowohl in der 64-Bit-Registrierung als auch in der 32-Bit-Registrierung desselben 64-Bit-Computers vorhanden ist, werden von der globalen Bedingung beide Registrierungsschlüssel ermittelt.  


### <a name="registry-value"></a><a name="bkmk_regval"></a> Registrierungswert

- **Struktur:** Wählen Sie die zu durchsuchende Registrierungsstruktur aus.  

    > [!Tip]  
    > Klicken Sie auf **Durchsuchen**, um die Einstellung von Werten auf einem Referenzcomputer zu konfigurieren. Aktivieren Sie den Dienst **Remoteregistrierung** auf dem Remotecomputer, um zu einem Registrierungswert auf einem Remotecomputer zu navigieren. Für den Zugriff auf den Remotecomputer benötigen Sie außerdem Administratorberechtigungen.  

- **Schlüssel:** Geben Sie den zu suchenden Registrierungsschlüsselnamen an. Verwenden Sie das Format `key\subkey`.  

- **Wert:** Geben Sie den Wert an, der im angegebenen Registrierungsschlüssel enthalten sein muss.  

- **Ist dieser Registrierungsschlüssel einer 64-Bit-Anwendung zugeordnet?** : Suche nach den 64-Bit-Registrierungsschlüsseln zusätzlich zu den 32-Bit-Registrierungsschlüsseln auf Clients, die eine 64-Bit-Version von Windows ausführen.  

    > [!NOTE]  
    > Wenn derselbe Registrierungsschlüssel sowohl in der 64-Bit-Registrierung als auch in der 32-Bit-Registrierung desselben 64-Bit-Computers vorhanden ist, werden von der globalen Bedingung beide Registrierungsschlüssel ermittelt.  


### <a name="script"></a><a name="bkmk_script"></a> Skript

Der Wert, der vom Skript zurückgegeben wird, wird zur Bewertung der Kompatibilität der globalen Bedingung verwendet. Bei der Verwendung von VBScript können Sie beispielsweise den Befehl **WScript.Echo Result** verwenden, um den Wert der *Result* -Variablen an die globale Bedingung zurückzugeben.  

- **Ermittlungsskript:** Klicken Sie auf **Skript hinzufügen**, und geben Sie ein Skript ein, oder navigieren Sie zu diesem. Dieses Skript wird für die Suche nach dem Wert verwendet. Sie können Windows PowerShell, VBScript oder Microsoft JScript-Skripts verwenden.  

- **Bereinigungsskript (optional)** : Klicken Sie auf **Skript hinzufügen**, und geben Sie ein Skript ein, oder navigieren Sie zu diesem. Dieses Skript wird zum Beheben nicht konformer Einstellungswerte verwendet. Sie können Windows PowerShell, VBScript oder Microsoft JScript-Skripts verwenden.  

- **Skripts durch Verwendung der Anmeldeinformationen angemeldeter Benutzer ausführen**: Wenn Sie diese Option aktivieren, wird das Skript auf Clientcomputern ausgeführt, die die Anmeldeinformationen der angemeldeten Benutzer verwenden.  

> [!Note]  
> Wenn Sie Windows PowerShell ab Version 1810 für ein Ermittlungs- oder Wartungsskript verwenden, ruft der Konfigurations-Manager-Client PowerShell mit dem Parameter `-NoProfile` auf. Diese Option startet PowerShell ohne Profile. Ein PowerShell-Profil ist ein Skript, das ausgeführt wird, wenn PowerShell gestartet wird. <!--3607762-->  


### <a name="sql-query"></a><a name="bkmk_sql"></a> SQL-Abfrage

- **SQL Server-Instanz**: Wählen Sie aus, ob die SQL-Abfrage auf der Standardinstanz, allen Instanzen oder einem bestimmten Datenbankinstanz-Namen ausgeführt werden soll.  

    > [!NOTE]  
    > Der Instanzname muss sich auf eine lokale Instanz von SQL Server beziehen. Verwenden Sie eine Skripteinstellung, um sich auf eine gruppierte SQL-Serverinstanz zu beziehen.  

- **Datenbank:** Geben Sie den Namen der Microsoft SQL Server-Datenbankinstanz ein, für die die SQL-Abfrage ausgeführt werden soll.  

- **Spalte:** Geben Sie den Namen der Spalte ein, die von der Transact-SQL-Anweisung zurückgegeben wird, die zur Bewertung der Kompatibilität der globalen Bedingung verwendet wird.  

- **Transact-SQL-Anweisung**: Geben Sie die vollständige SQL-Abfrage an, die Sie für die globale Bedingung verwenden möchten. Klicken Sie auf **Öffnen**, um eine vorhandene SQL-Abfrage zu verwenden.  

    > [!IMPORTANT]  
    > SQL-Abfrageeinstellungen unterstützen keine SQL-Befehle, durch die die Datenbank geändert wird. Sie können nur SQL-Befehle verwenden, mit denen Informationen aus der Datenbank gelesen werden.  


### <a name="wql-query"></a><a name="bkmk_wql"></a> WQL-Abfrage

- **Namespace:** Geben Sie den WMI-Namespace an, dessen Konformität mit Clientcomputern bewertet wird. Der Standardwert lautet `root\cimv2`.  

- **Klasse:** Geben Sie die WMI-Zielklasse im obigen Namespace an.  

- **Eigenschaft**: Geben Sie die WMI-Zieleigenschaft in der obigen Klasse an.  

- **WQL-Abfrage, WHERE-Klausel:** Geben Sie eine qualifizierende Klausel an, um die Menge der Ergebnisse zu reduzieren. Geben Sie beispielsweise die WHERE-Klausel `Name = 'DHCP' and StartMode = 'Auto'` an, um nur den DHCP-Dienst in der Win32_Service-Klasse abzufragen.   


### <a name="xpath-query"></a><a name="bkmk_xpath"></a> XPath-Abfrage

- **Pfad:** Geben Sie den Pfad zur XML-Datei auf Clientcomputern an, die zur Bewertung der Kompatibilität verwendet wird. Configuration Manager unterstützt im Pfadnamen die Verwendung aller Windows-Systemumgebungsvariablen und der Benutzervariablen `%USERPROFILE%`.  

- **XML-Dateiname:** Geben Sie den Namen der Datei an, die die XML-Abfrage im obigen Pfad enthält.  

- **Unterordner einbeziehen**: Aktivieren Sie diese Option, wenn auch Unterordner unter dem angegebenen Pfad durchsucht werden sollen.  

- **Diese Datei ist mit einer 64-Bit-Anwendung verknüpft:** Wenn Sie diese Option aktivieren, wird der 64-Bit-Systemdateispeicherort `%Windir%\System32` zusätzlich zum 32-Bit-Systemdateispeicherort `%Windir%\Syswow64` auf Konfigurations-Manager-Clients durchsucht, die eine 64-Bit-Version von Windows ausführen.  

- **XPath-Abfrage:** Geben Sie eine gültige, vollständige XPath-Abfrage (XML-Pfadsprache) an.  

- **Namespaces:** Mit dieser Option können Sie Namespaces und Präfixe identifizieren, die bei der XPath-Abfrage verwendet werden sollen.  

Wenn Sie versuchen, eine verschlüsselte XML-Datei zu ermitteln, wird diese Datei zwar durch die Kompatibilitätseinstellungen gefunden, die XPath-Abfrage führt jedoch zu keinen Ergebnissen. Der Konfigurations-Manager-Client generiert keinen Fehler.  

Wenn die XPath-Abfrage ungültig ist, wird die Einstellung auf Clientcomputern als nicht kompatibel bewertet.  



##  <a name="configure-compliance-rules"></a>Konfigurieren von Kompatibilitätsregeln  

Mit Konformitätsregeln werden die Bedingungen angegeben, mit denen die Konformität eines Konfigurationselements definiert wird. Damit eine Einstellung auf Kompatibilität bewertet werden kann, muss sie über mindestens eine Kompatibilitätsregel verfügen. WMI, Registrierung und skripteinstellungen können Sie die Werte zu beheben, die gefunden werden, nicht kompatibel ist. Sie können neue Regeln erstellen oder suchen Sie eine vorhandene Einstellung innerhalb eines beliebigen Konfigurationselements auf Regeln aktivieren.  


### <a name="to-create-a-compliance-rule"></a>So erstellen Sie eine Konformitätsregel  

1. Klicken Sie im **Assistenten zum Erstellen von Konfigurationselementen** auf der Seite **Kompatibilitätsregeln** auf **Neu**.  

2. Geben Sie im Dialogfeld **Regel erstellen** die folgenden Informationen an:  

    - **Name:** Geben Sie einen Namen für die Kompatibilitätsregel ein.  

    - **Beschreibung:** Geben Sie eine Beschreibung für die Kompatibilitätsregel ein.  

    - **Ausgewählte Einstellung:** Wählen Sie zum Öffnen des Dialogfelds **Einstellung auswählen** die Option **Durchsuchen** aus. Wählen Sie die Einstellung aus, für die Sie eine Regel definieren möchten, oder wählen Sie **Neue Einstellung** aus. Klicken Sie dann auf **Auswählen**.  

        > [!Tip]  
        > Klicken Sie auf **Eigenschaften**, um Informationen über die jeweils ausgewählte Einstellung abzurufen.  

    - **Regeltyp:** Wählen Sie den Typ der Konformitätsregel, die Sie verwenden möchten:  

        - **Wert:** Erstellen Sie eine Regel, mit deren Hilfe der vom Konfigurationselement zurückgegebene Wert mit einem von Ihnen angegebenen Wert verglichen wird. Weitere Informationen zu den zusätzlichen Einstellungen finden Sie unter [Wertregeln](#bkmk_value).  

        - **Existenziell**: Erstellen Sie eine Regel, die die Einstellung abhängig davon auswertet, ob sie auf einem Clientgerät vorhanden ist, oder wie oft sie gefunden wird. Weitere Informationen zu den zusätzlichen Einstellungen finden Sie unter [Existenzielle Regeln](#bkmk_exist).  

3. Wählen Sie **OK** aus, um das Dialogfeld **Regel erstellen** zu schließen.  




### <a name="value-rules"></a><a name="bkmk_value"></a> Wertregeln  

- **Eigenschaft**: Die Eigenschaft des zu überprüfenden Objekts variiert abhängig von der ausgewählten Einstellung. Die verfügbaren Eigenschaften variieren je nach Typ der Einstellung. 

- **Die Einstellung muss folgende Regel erfüllen:** Die verfügbaren Regeln oder Berechtigungen variieren je nach Typ der Einstellung.

- **Nicht konforme Regeln wiederherstellen, falls dies unterstützt wird:** Wählen Sie diese Option aus, wenn nicht konforme Regeln von Configuration Manager automatisch wiederhergestellt werden sollen. Configuration Manager unterstützt diese Aktion mit den folgenden Regeltypen:  

    - **Registrierungswert:** Bei Nichtkonformität legt der Client den Registrierungswert fest. Wenn er nicht vorhanden ist, erstellt der Client den Wert.  

    - **Skript:** Der Client verwendet das Wartungsskript, das Sie mit der Einstellung angeben.  

    - **WQL-Abfrage**  

    > [!IMPORTANT]  
    > Sie können nicht kompatible Regeln nur wiederherstellen, wenn der Regeloperator auf **Ist gleich**festgelegt ist.  

- **Als nicht konform melden, wenn diese Einstellungsinstanz nicht gefunden wird**: Wenn diese Einstellung auf Clientcomputern nicht ermittelt wird, aktivieren Sie diese Option für das Konfigurationselement, um Nichtkonformität zu melden.  

- **Schweregrad der Nichtkonformität für Berichte**: Geben Sie den Schweregrad an, der in Configuration Manager-Berichten gemeldet wird, wenn bei dieser Konformitätsregel ein Fehler auftritt. Die folgenden Schweregrade sind verfügbar:  
    - **Keine**  
    - **Information**  
    - **Warnung**  
    - **Kritisch**  
    - **Kritisch mit Ereignis**: Von Computern, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** gemeldet. Dieser Schweregrad wird zudem im Anwendungsereignisprotokoll als Windows-Ereignis protokolliert.  


### <a name="existential-rules"></a><a name="bkmk_exist"></a> Existenzielle Regeln 

> [!NOTE]  
> Die angezeigten Optionen sind möglicherweise unterschiedlich, je nach Einstellungstyp, für den Sie eine Regel konfigurieren.  

- **Diese Einstellung muss auf Clientgeräten vorhanden sein.**  

- **Diese Einstellung darf auf Clientgeräten nicht vorhanden sein.**  

- **Häufigkeit des Auftretens dieser Einstellung:**  

- **Schweregrad der Nichtkonformität für Berichte**: Geben Sie den Schweregrad an, der in Configuration Manager-Berichten gemeldet wird, wenn bei dieser Konformitätsregel ein Fehler auftritt. Die folgenden Schweregrade sind verfügbar:  
    - **Keine**  
    - **Information**  
    - **Warnung**  
    - **Kritisch**  
    - **Kritisch mit Ereignis**: Von Computern, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** gemeldet. Dieser Schweregrad wird zudem im Anwendungsereignisprotokoll als Windows-Ereignis protokolliert.  


## <a name="track-configuration-item-remediations"></a><a name="bkmk_track"></a> Nachverfolgen von Konfigurationselementwartungen
<!--4261411-->
*(eingeführt in Version 2002)*

Ab Version 2002 können Sie die Option **Track remediation history when supported** (Wartungsverlauf bei Unterstützung nachverfolgen) in den Konformitätsregeln für Ihr Konfigurationselement aktivieren. Wenn diese Option aktiviert ist, wird bei jeder Wartung, die auf dem Client für das Konfigurationselement vorgenommen wird, eine Zustandsmeldung generiert. Der Verlauf wird in der Configuration Manager-Datenbank gespeichert.

Erstellen Sie benutzerdefinierte Berichte, um den Wartungsverlauf mithilfe der öffentlichen Ansicht **v_CIRemediationHistory** anzuzeigen. Die Spalte `RemediationDate` gibt die Uhrzeit in UTC an, zu der der Client die Wartung ausgeführt hat. Mit `ResourceID` wird das Gerät identifiziert. Das Erstellen benutzerdefinierter Berichte mit der Ansicht **v_CIRemediationHistory** bietet Ihnen folgende Vorteile:

- Identifizieren möglicher Probleme mit Ihrem Wartungsskript
- Erkennen von Trends in Wartungen, z. B. ein Client, der in jedem Evaluierungszyklus konsistent als nicht konform bewertet wird

### <a name="enable-the-track-remediation-history-when-supported-option"></a>Aktivieren der Option „Track remediation history when supported“ (Wartungsverlauf bei Unterstützung nachverfolgen)

- Sie können die Option **Wartungsverlauf bei Unterstützung nachverfolgen** auf der Registerkarte **Konformitätsregeln** für neue Konfigurationselemente hinzufügen, wenn Sie eine neue Einstellung auf der Seite **Einstellungen** des Assistenten erstellen.
- Sie können die Option **Wartungsverlauf bei Unterstützung nachverfolgen** für vorhandene Konfigurationselemente auf der Registerkarte **Konformitätsregeln** in den **Eigenschaften** des Konfigurationselements hinzufügen.
[ ![Die Option „Track remediation history when supported“ (Wartungsverlauf bei Unterstützung nachverfolgen) in Version 2002](./media/4261411-remediation-history.png)](./media/4261411-remediation-history.png#lightbox)

## <a name="next-steps"></a>Nächste Schritte

[Erstellen von Konfigurationsbaselines](create-configuration-baselines.md)
