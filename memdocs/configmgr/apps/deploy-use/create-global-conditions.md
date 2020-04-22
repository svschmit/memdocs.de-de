---
title: Erstellen von globalen Bedingungen
titleSuffix: Configuration Manager
description: Erstellen Sie globale Bedingungen, die festlegen, wie eine Anwendung auf Clientgeräten bereitgestellt werden soll.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2d5f871a-19dc-4bd3-a3ad-4230c7a69f1b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ae27e50e5093d7443c35df33b1757caec6086627
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689538"
---
# <a name="how-to-create-global-conditions-in-configuration-manager"></a>Erstellen von globalen Bedingungen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In Configuration Manager sind globale Bedingungen Regeln für geschäftliche oder technische Bedingungen, mit deren Hilfe angegeben werden kann, wie eine Anwendung auf Clientgeräten bereitgestellt werden soll. Der Zugriff auf globale Bedingungen erfolgt über den Assistenten zum Erstellen neuer Bereitstellungstypen auf der Seite **Anforderungen** .  

> [!NOTE]  
>  Sie können globale Bedingungen nur von dem Standort aus bearbeiten, auf dem sie erstellt wurden.  

 Gehen Sie wie folgt vor, um globale Configuration Manager-Bedingungen zu erstellen.  

## <a name="provide-basic-information-about-the-global-condition"></a>Bereitstellen grundlegender Informationen zu der globalen Bedingung  
 Es sind verschiedene Arten von globalen Bedingungen verfügbar. Den unterschiedlichen Arten globaler Bedingungen sind auch unterschiedliche Optionen zugeordnet. Wenn Sie eine bestimmte Art von globaler Bedingung auswählen, werden in Configuration Manager die jeweils zur Auswahl passenden Optionen gezeigt.  

1.  Wählen Sie in der Configuration Manager-Konsole **Softwarebibliothek** > **Anwendungsverwaltung** > **Globale Bedingungen** aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** **Globale Bedingung erstellen** aus.  

4.  Geben Sie im Dialogfeld **Globale Bedingung erstellen** einen Namen und eine optionale Beschreibung für die globale Bedingung ein.  

5.  Wählen Sie in der Dropdownliste **Gerätetyp** aus, ob die globale Bedingung für einen **Windows**-Computer oder ein **Windows Mobile**-Gerät gelten soll.  

6.  Wählen Sie in der Dropdownliste **Bedingungstyp** eine der folgenden Optionen aus:  

    -   **Einstellung** : Mithilfe dieser Option wird das Vorhandensein von einem oder mehreren Elementen auf Clientgeräten überprüft. Sie können beispielsweise überprüfen, ob eine Datei, ein Ordner oder ein Registrierungsschlüsselwert auf einem Clientgerät vorhanden ist.  

    -   **Ausdruck**: Mithilfe dieser Option können Sie komplexere Regeln zum Überprüfen von Bedingungen auf Clientgeräten einrichten. Sie können beispielsweise überprüfen, ob der physische Arbeitsspeicher auf einem Computer zwischen 2 GB und 4 GB beträgt, oder ob ein mobiles Gerät die Eingabe über einen Touchscreen unterstützt.  

## <a name="set-up-rules-for-the-global-condition"></a>Einrichten von Regeln für die globale Bedingung  
 Das Verfahren zum Definieren der globalen Bedingungsregeln ist davon abhängig, ob Sie eine Einstellung oder einen Ausdruck konfigurieren. Verwenden Sie das jeweilige Verfahren, um eine Einstellung oder einen Ausdruck für die globale Bedingung einzurichten.  

### <a name="to-set-up-a-setting-for-the-global-condition"></a>So richten Sie eine Einstellung für die globale Bedingung ein  

1. Wählen Sie in der Dropdownliste **Bedingungstyp** die Option **Einstellung**aus.  

2. Wählen Sie in der Dropdownliste **Einstellungstyp** das Element aus, das als Bedingung für die Überprüfung der Anforderungen dienen soll. Die unten angegebenen Einstellungstypen und Konfigurationen sind verfügbar.  

   - **Active Directory-Abfrage**  

     -   **LDAP-Präfix** : Geben Sie ein gültiges LDAP-Präfix für die Active Directory-Domänendiensteabfrage an, mit der die Kompatibilität auf Clientcomputern bewertet wird. Sie können **LDAP://** oder **GC://** verwenden.  

     -   **Definierter Name (DN)** : Geben Sie den Definierten Namen des Active Directory Domain Services-Diensts an, das auf Clientcomputern auf Konformität bewertet wird.  

     -   **Suchfilter** : Geben Sie einen optionalen LDAP-Filter an, mit dem die Ergebnisse der Active Directory-Domänendiensteabfrage zur Bewertung der Kompatibilität auf Clientcomputern optimiert werden.  

     -   **Suchbereich** : Geben Sie den Suchbereich in den Active Directory-Domänendiensten an:  

         -   **Basis**: Hiermit wird nur das angegebene Objekt abgefragt.  

         -   **Eine Ebene** – Diese Option wird in dieser Version von Configuration Manager nicht verwendet.  

         -   **Unterstruktur**: Hiermit werden das angegebene Objekt und dessen vollständige untergeordnete Struktur im Verzeichnis abgefragt.  

     -   **Eigenschaft** : Geben Sie die Eigenschaft des Active Directory-Domänendiensteobjekts an, mit dem auf Clientcomputern die Kompatibilität bewertet wird.  

     -   **Abfrage**: Zeigt die LDAP-Abfrage an, die aus den Einträgen unter **LDAP-Präfix**, **Definierter Name (DN)** , **Suchfilter** (falls angegeben) und **Eigenschaft**erstellt wird. Diese Abfrage wird zur Bewertung der Konformität auf Clientcomputern verwendet.  

   - **Assembly**  

     -   **Assemblyname** : Gibt den Namen des Assemblyobjekts an, nach dem gesucht wird. Der Name darf nicht mit einem Namen eines anderen Assemblyobjekts vom gleichen Typ identisch sein, und muss im globalen Assemblycache (Global Assembly Cache, GAC) registriert sein. Der Assemblyname darf maximal 256 Zeichen umfassen.  

     > [!NOTE]  
     >  Eine Assembly ist ein Programmcode, der zwischen Anwendungen freigegeben werden kann. Assemblys können die Dateinamenerweiterung .dll oder .exe haben. Der GAC ist ein Ordner mit dem Namen *%systemroot%\assembly* auf Clientcomputern, in dem alle freigegebenen Assemblys gespeichert werden.  

   - **Dateisystem**  

     - **Typ**: Wählen Sie in der Dropdownliste aus, ob Sie nach einer **Datei** oder nach einem **Ordner**suchen möchten.  

     - **Pfad** : Geben Sie den Pfad zur Datei bzw. zum Ordner auf Clientcomputern an. Sie können Systemumgebungsvariablen und die Umgebungsvariable *%USERPROFILE%* im Pfad angeben.  

       > [!NOTE]  
       >  Wenn Sie die Umgebungsvariable *%USERPROFILE%* in den Feldern **Pfad** oder **Datei- oder Ordnername** verwenden, werden alle Benutzerprofile auf dem Clientcomputer durchsucht. Dies kann dazu führen, dass mehrere Instanzen einer Datei oder eines Ordners gefunden werden.  

     - **Datei- oder Ordnername** : Geben Sie den Namen des Datei- oder Ordnerobjekts an, nach dem gesucht werden soll. Sie können Systemumgebungsvariablen und die *%USERPROFILE%* -Umgebungsvariable im Datei- oder Ordnernamen angeben. Sie können auch die Platzhalter * und ? im Dateinamen verwenden.  

       > [!NOTE]  
       >  Wenn Sie einen Datei- oder Ordnernamen angeben und dabei Platzhalter verwenden, kann dies zu einer großen Anzahl von Ergebnissen führen. Dies kann zu hoher Ressourcenauslastung auf dem Clientcomputer und zu erhöhtem Netzwerkverkehr beim Berichten von Ergebnissen an Configuration Manager führen.  

     - **Unterordner einschließen** : Aktivieren Sie diese Option, wenn auch Unterordner unter dem angegebenen Pfad durchsucht werden sollen.  

     - **Diese Datei oder dieser Ordner ist mit einer 64-Bit-Anwendung verknüpft**: Geben Sie an, ob der Speicherort der 64-Bit-Systemdatei ( *%windir%* \system32) zusätzlich zum Speicherort der 32-Bit-Systemdatei ( *%windir%* \syswow64) auf Configuration Manager-Clients durchsucht werden soll, auf denen eine 64-Bit-Version von Windows ausgeführt wird.  

       > [!NOTE]  
       >  Wenn dieselbe Datei bzw. derselbe Ordner sowohl am Speicherort der 64-Bit-Systemdatei als auch am Speicherort der 32-Bit-Systemdatei desselben 64-Bit-Computers existiert, werden von der globalen Bedingung mehrere Dateien ermittelt.  

       Die Angabe eines UNC-Pfads zu einer Netzwerkfreigabe im Feld **Pfad** wird vom Einstellungstyp **Dateisystem** nicht unterstützt.  

   - **IIS-Metabasis**  

     -   **Metabasispfad** : Geben Sie einen gültigen Pfad für die IIS-Metabasis an.  

     -   **Eigenschafts-ID** : Geben Sie die numerische Eigenschaft der IIS-Metabasiseinstellung an.  

   - **Registrierungsschlüssel**  

     -   **Struktur**: Wählen Sie aus der Dropdownliste die Registrierungsstruktur aus, die durchsucht werden soll.  

     -   **Schlüssel** : Geben Sie den Namen des Registrierungsschlüssels an, nach dem gesucht werden soll. Das zu verwendende Format ist *Schlüssel\Unterschlüssel*.  

     -   **Dieser Registrierungsschlüssel ist einer 64-Bit-Anwendung zugeordnet** : gibt an, ob auf Clients mit der 64-Bit-Version von Windows die 64-Bit-Registrierungsschlüssel zusätzlich zu den 32-Bit-Registrierungsschlüsseln gesucht werden sollen.  

         > [!NOTE]  
         >  Wenn derselbe Registrierungsschlüssel sowohl in der 64-Bit-Registrierung als auch in der 32-Bit-Registrierung desselben 64-Bit-Computers existiert, werden von der globalen Bedingung beide Registrierungsschlüssel ermittelt.  

   - **Registrierungswert**  

     -   **Struktur** : Wählen Sie aus der Dropdownliste die Registrierungsstruktur aus, die durchsucht werden soll.  

     -   **Schlüssel** : Geben Sie den Namen des Registrierungsschlüssels an, nach dem gesucht werden soll. Das zu verwendende Format ist *Schlüssel\Unterschlüssel*.  

     -   **Wert** : Geben Sie den Wert an, der im angegebenen Registrierungsschlüssel enthalten sein muss.  

     -   **Dieser Registrierungsschlüssel ist einer 64-Bit-Anwendung zugeordnet** : gibt an, ob auf Clients mit der 64-Bit-Version von Windows die 64-Bit-Registrierungsschlüssel zusätzlich zu den 32-Bit-Registrierungsschlüsseln gesucht werden sollen.  

         > [!NOTE]  
         >  Wenn derselbe Registrierungsschlüssel sowohl in der 64-Bit-Registrierung als auch in der 32-Bit-Registrierung desselben 64-Bit-Computers existiert, werden von der globalen Bedingung beide Registrierungsschlüssel ermittelt.  

   - **Skript**  

     -   **Ermittlungsskript**: Wählen Sie **Hinzufügen** aus, um ein zu verwendendes Skript einzugeben oder zu suchen. Sie können Windows PowerShell-, VBScript- oder JScript-Skripts verwenden.  

     -   **Skripts durch Verwendung der Anmeldeinformationen angemeldeter Benutzer ausführen**: Wenn Sie diese Option aktivieren, wird das Skript auf Clientcomputern unter Verwendung der Anmeldeinformationen des angemeldeten Benutzers ausgeführt.  

         > [!NOTE]  
         >  Der Wert, der vom Skript zurückgegeben wird, wird zur Bewertung der Konformität der globalen Bedingung verwendet. Bei der Verwendung von VBScript können Sie beispielsweise den Befehl **WScript.Echo Result** verwenden, um den Wert der Variablen „Result“ der globalen Bedingung zurückzugeben.  
         >   
         >  Wenn das Skript mehrere Werte zurückgibt, müssen sich diese Werte in einer einzigen Zeile befinden und durch ein Semikolon getrennt werden. Wenn sich jeder Wert in einer separaten Zeile befindet, kann die Auswertung nicht durchgeführt werden.  

   - **SQL-Abfrage**  

     -   **SQL Server-Instanz** – Wählen Sie aus, ob die SQL-Abfrage auf der Standardinstanz, allen Instanzen oder einem bestimmten Datenbankinstanznamen ausgeführt werden soll.  

         > [!NOTE]  
         >  Der Instanzname muss sich auf eine lokale Instanz von SQL Server beziehen. Verwenden Sie eine Skripteinstellung, um sich auf eine gruppierte SQL-Serverinstanz zu beziehen.  

     -   **Datenbank** : Geben Sie den Namen der Microsoft SQL Server-Datenbank an, für die die SQL-Abfrage ausgeführt wird.  

     -   **Spalte** : Geben Sie den für die Bewertung der Kompatibilität der globalen Bedingung zu verwendenden Spaltennamen an, der von der Transact-SQL-Anweisung zurückgegeben wird.  

     -   **Transact-SQL-Anweisung** : Geben Sie die vollständige SQL-Abfrage an, die für die globale Bedingung verwendet werden soll. Sie können zum Öffnen einer vorhandenen SQL-Abfrage auch **Öffnen** auswählen.  

   - **WQL-Abfrage**  

     -   **Namespace** : Geben Sie den WMI-Namespace zum Erstellen einer WQL-Abfrage an, deren Kompatibilität auf Clientcomputern bewertet wird. Der Standardwert ist "Root\cimv2".  

     -   **Klasse** : Geben Sie die WMI-Klasse zum Erstellen einer WQL-Abfrage an, deren Kompatibilität auf Clientcomputern bewertet wird.  

     -   **Eigenschaft** : Geben Sie die WMI-Eigenschaft zum Erstellen einer WQL-Abfrage an, deren Kompatibilität auf Clientcomputern bewertet wird.  

     -   **WQL-Abfrage, WHERE-Klausel** : Mithilfe des Elements **WQL-Abfrage, WHERE-Klausel** können Sie eine WHERE-Klausel angeben, die auf Clientcomputern auf den angegebenen Namespace, die Klasse und die Eigenschaft angewendet wird.  

   - **XPath-Abfrage**  

     -   **Pfad** – Geben Sie den Pfad zur XML-Datei auf Clientcomputern an, die zur Bewertung der Kompatibilität verwendet wird. Configuration Manager unterstützt im Pfadnamen die Verwendung aller Windows-Systemumgebungsvariablen und der Benutzervariablen *%USERPROFILE%* .  

     -   **XML-Dateiname**: Geben Sie den Namen der Datei an, die die XML-Abfrage enthält, die für die Bewertung der Konformität auf Clientcomputern verwendet wird.  

     -   **Unterordner einschließen** – Aktivieren Sie diese Option, wenn auch Unterordner unter dem angegebenen Pfad durchsucht werden sollen.  

     -   **Diese Datei ist mit einer 64-Bit-Anwendung verknüpft**: Geben Sie an, ob der Speicherort der 64-Bit-Systemdatei ( *%windir%* \system32) zusätzlich zum Speicherort der 32-Bit-Systemdatei ( *%windir%* \syswow64) auf Configuration Manager-Clients durchsucht werden soll, auf denen eine 64-Bit-Version von Windows ausgeführt wird.  

     -   **XPath-Abfrage** : Geben Sie eine gültige, vollständige XPath-Abfrage (XML Path Language) an, die für die Bewertung der Kompatibilität auf Clientcomputern verwendet wird.  

     -   **Namespaces** : öffnet das Dialogfeld **XML-Namespaces** zum Identifizieren von Namespaces und Präfixen, die bei der XPath-Abfrage verwendet werden sollen.  

3. Wählen Sie aus der Dropdownliste **Datentyp** das Format aus, in dem Daten von der Bedingung zurückgegeben werden, bevor sie zur Überprüfung der Anforderungen verwendet wird.  

   > [!NOTE]  
   >  Die Dropdownliste **Datentyp** wird nicht für alle Einstellungstypen angezeigt.  

4. Richten Sie weitere Details zu dieser Einstellung unterhalb der Dropdownliste **Einstellungstyp** ein. Die Elemente, die Sie einrichten können, sind je nach gewähltem Einstellungstyp unterschiedlich.  

5. Wählen Sie **OK** aus, um die Regel zu speichern, und das Dialogfeld **Globale Bedingung erstellen** zu schließen.  

### <a name="set-up-an-expression-for-the-global-condition"></a>Einrichten eines Ausdrucks für die globale Bedingung  

1.  Wählen Sie in der Dropdownliste **Bedingungstyp** die Option **Ausdruck**aus.  

2.  Wählen Sie **Klausel hinzufügen** aus, um das Dialogfeld **Klausel hinzufügen** zu öffnen.  

3.  Wählen Sie in der Dropdownliste **Kategorie auswählen** aus, ob dieser Ausdruck für ein Gerät oder einen Benutzer bestimmt ist. Sie können auch **Benutzerdefiniert** auswählen, um eine zuvor konfigurierte globale Bedingung zu verwenden.  

4.  Wählen Sie in der Dropdownliste **Wählen Sie eine Bedingung aus** die Bedingung aus, mit der bewertet werden soll, ob der Benutzer bzw. das Gerät die Regelanforderungen erfüllt. Der Inhalt dieser Liste ist von der ausgewählten Kategorie abhängig.  

5.  Wählen Sie in der Dropdownliste **Operator auswählen** den Operator aus, der zum Vergleichen der ausgewählten Bedingung mit dem angegebenen Wert verwendet werden soll, um zu bewerten, ob der Benutzer bzw. das Gerät den Regelanforderungen entspricht. Welche Operatoren verfügbar sind, ist von der ausgewählten Bedingung abhängig.  

6.  Geben Sie im Feld **Wert** die Werte ein, die zusammen mit der ausgewählten Bedingung und dem Operator verwendet werden sollen, um zu bewerten, ob der Benutzer bzw. das Gerät die Regelanforderungen erfüllt. Welche Werte verfügbar sind, ist von der ausgewählten Bedingung und dem ausgewählten Operator abhängig.  

7.  Wählen Sie **OK** aus, um den Ausdruck zu speichern und das Dialogfeld **Klausel hinzufügen** zu schließen.  

8.  Wenn der globalen Bedingung alle gewünschten Klauseln hinzugefügt wurden, wählen Sie**OK** aus, um die globale Bedingung zu speichern und das Dialogfeld **Globale Bedingung erstellen** zu schließen.  
