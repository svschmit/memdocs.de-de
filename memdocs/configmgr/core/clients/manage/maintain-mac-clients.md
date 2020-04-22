---
title: Warten von Macintosh-Clients
titleSuffix: Configuration Manager
description: Wartungstasks für Configuration Manager-Mac-Clients
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: cf6337a2-700c-47f3-b6f8-5814f9b81e59
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 520315c4bb740f23a9534e532f75c3bd3ee66a2a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690058"
---
# <a name="maintain-mac-clients"></a>Warten von Macintosh-Clients
*Gilt für: Configuration Manager (Current Branch)*

Es folgen Verfahren zum Deinstallieren von Mac-Clients und Verlängern ihrer Zertifikate.

##  <a name="uninstalling-the-mac-client"></a>Deinstallieren des Mac-Clients  

1.  Öffnen Sie auf dem Mac-Computer ein Terminalfenster, und navigieren Sie zum Ordner, der **macclient.dmg** enthält.  

2.  Navigieren Sie zum Ordner Tools, und geben Sie die folgende Befehlszeile ein:  

     `./CMUninstall -c`

    > [!NOTE]  
    >  Bei Angabe der Eigenschaft **-c** werden bei der Deinstallation des Clients auch die Absturzprotokolle und die Protokolldateien des Clients entfernt. Dies wird empfohlen, um Verwechslungen zu vermeiden, wenn Sie den Client später erneut installieren.  

3.  Entfernen Sie bei Bedarf manuell das Clientauthentifizierungszertifikat, das von Configuration Manager verwendet wurde, oder widerrufen Sie es. Von „CMUninstall“ wird dieses Zertifikat nicht entfernt oder widerrufen.  

##  <a name="renewing-the-mac-client-certificate"></a>Erneuern des Zertifikats für den Macintosh-Client  
 Verwenden Sie eines der folgenden Verfahren, um das Zertifikat für den Macintosh-Client zu erneuern:  

-   [Assistent zum Verlängern von Zertifikaten](#renew-certificate-wizard)  

-   [Manuelles Verlängern des Zertifikats](#renew-certificate-manually)  

###  <a name="renew-certificate-wizard"></a>Assistent zum Verlängern von Zertifikaten  

1. Konfigurieren Sie in der Datei „ccmclient.plist“ die folgenden Werte als *Zeichenfolgen*, mit denen gesteuert wird, wann der Assistent zum Verlängern von Zertifikaten geöffnet wird:  

   - **RenewalPeriod1** – Hiermit wird der erste Erneuerungszeitraum (in Sekunden) angegeben, in dem Benutzer das Zertifikat erneuern können. Der Standardwert beträgt 3.888.000 Sekunden (45 Tage). Legen Sie keinen Wert kleiner als 300 fest, da der Zeitraum auf den Standardwert zurückgesetzt wird. 

   - **RenewalPeriod2** – Hiermit wird der zweite Erneuerungszeitraum (in Sekunden) angegeben, in dem Benutzer das Zertifikat erneuern können. Der Standardwert beträgt 259.200 Sekunden (3 Tage). Wenn dieser Wert konfiguriert ist und größer gleich 300 Sekunden und kleiner gleich **RenewalPeriod1** ist, wird der Wert verwendet. Wenn **RenewalPeriod1** größer als 3 Tage ist, wird ein Wert von 3 Tagen für **RenewalPeriod2**verwendet.  Wenn **RenewalPeriod1** kleiner als 3 Tage ist, dann wird **RenewalPeriod2** auf denselben Wert wie **RenewalPeriod1**festgelegt.  

   - **RenewalReminderInterval1** – Gibt das Intervall an (in Sekunden), in dem Benutzern während des ersten Erneuerungszeitraums der Assistent zum Erneuern von Zertifikaten angezeigt wird. Der Standardwert beträgt 86.400 Sekunden (1 Tag). Wenn **RenewalReminderInterval1** größer als 300 Sekunden, aber kleiner als der für **RenewalPeriod1**konfigurierte Wert ist, wird der konfigurierte Wert verwendet. Andernfalls wird der Standardwert 1 Tag verwendet.  

   - **RenewalReminderInterval2** – Gibt das Intervall an (in Sekunden), in dem Benutzern während des zweiten Erneuerungszeitraums der Assistent zum Erneuern von Zertifikaten angezeigt wird. Der Standardwert beträgt 28.800 Sekunden (8 Stunden). Wenn **RenewalReminderInterval2** größer als 300 Sekunden, aber kleiner oder gleich **RenewalReminderInterval1** und kleiner oder gleich **RenewalPeriod2**ist, wird der konfigurierte Wert verwendet. Andernfalls wird ein Wert von 8 Stunden verwendet.  

     **Beispiel:** Werden die Standardwerte nicht geändert, dann wird der Assistent in den 45 Tagen vor dem Ablauf des Zertifikats alle 24 Stunden geöffnet.  In den letzten 3 Tagen vor Zertifikatsablauf wird der Assistent alle 8 Stunden geöffnet.  

     **Beispiel:** Legen Sie mithilfe der folgenden Befehlszeile oder einem Skript den ersten Erneuerungszeitraum auf 20 Tage fest.  

     `sudo defaults write com.microsoft.ccmclient RenewalPeriod1 1728000`  

2. Wenn der Assistent zum Verlängern von Zertifikaten geöffnet wird, sind die Felder **Benutzername** und **Servername** normalerweise bereits ausgefüllt, und der Benutzer muss bloß ein Kennwort eingeben, um das Zertifikat zu verlängern.  

   > [!NOTE]  
   >  Wird der Assistent nicht geöffnet, oder haben Sie ihn versehentlich geschlossen, dann klicken Sie auf der Einstellungsseite von **Configuration Manager** auf **Erneuern** , um den Assistenten zu öffnen.  

###  <a name="renew-certificate-manually"></a>Manuelles Verlängern des Zertifikats  
 Der typische Gültigkeitszeitraum für das Macintosh-Clientzertifikat beträgt 1 Jahr. Das während der Registrierung angeforderte Benutzerzertifikat wird von Configuration Manager nicht automatisch erneuert, weswegen Sie wie folgt vorgehen müssen, um das Zertifikat zu erneuern.  

> [!IMPORTANT]  
>  Wenn das Zertifikat abläuft, müssen Sie den Macintosh-Client deinstallieren, neu installieren und dann erneut anmelden.  

 Durch dieses Verfahren wird die SMS-ID entfernt, die zur Anforderung eines neuen Zertifikats für denselben Macintosh-Computer erforderlich ist. Wenn Sie die Client-SMS-ID entfernen und ersetzen, wird der gesamte gespeicherte Clientverlauf, wie beispielsweise der Bestand, nach dem Löschen des Clients über die Configuration Manager-Konsole gelöscht.  

1.  Erstellen Sie für die Mac-Computer, deren Benutzerzertifikate verlängert werden müssen, eine Gerätesammlung.  

    > [!WARNING]  
    >  Der Gültigkeitszeitraum des für Macintosh-Computer registrierten Zertifikats wird von Configuration Manager nicht überwacht. Dies müssen Sie unabhängig von Configuration Manager übernehmen, um die Macintosh-Computer zu identifizieren, die dieser Sammlung hinzugefügt werden müssen.  

2.  Starten Sie im Arbeitsbereich **Bestand und Kompatibilität** den **Assistenten zum Erstellen von Konfigurationselementen**.  

3.  Geben Sie auf der Seite **Allgemein** die folgenden Informationen an:  

    -   **Name:SMS-ID für Mac entfernen**  

    -   **Typ:Mac OS X**  

4.  Vergewissern Sie sich auf der Seite **Unterstützte Plattformen**, dass alle Mac OS X-Versionen ausgewählt sind.  

5.  Klicken Sie auf der Seite **Einstellungen** auf **Neu**, und geben Sie anschließend im Dialogfeld **Einstellung erstellen** die folgenden Informationen an:  

    -   **Name:SMS-ID für Mac entfernen**  

    -   **Einstellungstyp:Skript**  

    -   **Datentyp:Zeichenfolge**  

6.  Wählen Sie im Dialogfeld **Einstellung erstellen** für **Ermittlungsskript** **Skript hinzufügen** aus, um ein Skript anzugeben, mit dem Mac-Computer ermittelt werden können, die über eine konfigurierte SMSID verfügen.  

7.  Geben Sie im Dialogfeld **Ermittlungsskript bearbeiten** das folgende Shellskript ein:  

    ``` Shell
    defaults read com.microsoft.ccmclient SMSID  
    ```  

8.  Wählen Sie **OK** aus, um das Dialogfeld **Ermittlungsskript bearbeiten** zu schließen.  

9. Wählen Sie im Dialogfeld **Einstellung erstellen** für **Wiederherstellungsskript (optional)** **Skript hinzufügen** aus, um ein Skript anzugeben, mit dem die SMSID von Mac-Computern entfernt wird, wenn sie gefunden wird.  

10. Geben Sie im Dialogfeld **Wiederherstellungsskript erstellen** das folgende Shellskript ein:  

    ``` Shell
    defaults delete com.microsoft.ccmclient SMSID  
    ```  

11. Wählen Sie **OK** aus, um das Dialogfeld **Wiederherstellungsskript erstellen** zu schließen.  

12. Klicken Sie auf der Seite **Kompatibilitätsregeln** des Assistenten auf **Neu**, und geben Sie anschließend im Dialogfeld **Regel erstellen** die folgenden Informationen an:  

    -   **Name:SMS-ID für Mac entfernen**  

    -   **Ausgewählte Einstellung:** Wählen Sie **Durchsuchen** aus, und wählen Sie dann das Ermittlungsskript aus, das Sie zuvor angegeben haben.  

    -   Geben Sie im Feld **die folgenden Werte** **Das Domänen-/Standardpaar (com.microsoft.ccmclient, SMS-ID) existiert nicht**ein.  

    -   Aktivieren Sie die Option **Das angegebene Wiederherstellungsskript ausführen, wenn diese Einstellung nicht kompatibel ist**.  

13. Beenden Sie den Assistenten zum Erstellen von Konfigurationselementen.  

14. Erstellen Sie eine Konfigurationsbaseline mit dem Konfigurationselement, das Sie gerade erstellt haben, und stellen Sie es für die Gerätesammlung bereit, die Sie in Schritt 1 erstellt haben.  

     Weitere Informationen zum Erstellen und Bereitstellen von Konfigurationsbaselines finden Sie unter [Erstellen von Konfigurationsbaselines](../../../compliance/deploy-use/create-configuration-baselines.md) und [Bereitstellen von Konfigurationsbasislinien](../../../compliance/deploy-use/deploy-configuration-baselines.md).  

15. Führen Sie auf Macintosh-Computern, auf denen die SMS-ID entfernt wurde, den folgenden Befehl aus, um ein neues Zertifikat zu installieren:  

    ``` Shell
    sudo ./CMEnroll -s <enrollment_proxy_server_name> -ignorecertchainvalidation -u <'user name'>  
    ```  

     Geben Sie das Kennwort für das Administratorkonto ein, wenn Sie dazu aufgefordert werden, um den Befehl auszuführen. Geben Sie dann das Kennwort für das Active Directory-Benutzerkonto ein.  

16. Öffnen Sie auf dem Macintosh-Computer ein Terminalfenster, und nehmen Sie folgende Änderungen vor, um das registrierte Zertifikat auf Configuration Manager zu beschränken:  

    a.  Geben Sie den Befehl `sudo /Applications/Utilities/Keychain\ Access.app/Contents/MacOS/Keychain\ Access` ein.

    b.  Wählen Sie im Dialogfeld **Schlüsselbundverwaltung** im Abschnitt **Schlüsselbunde** **System** aus, und im Abschnitt **Kategorie** anschließend **Schlüssel**.  

    c.  Erweitern Sie die Schlüssel, um die Clientzertifikate anzuzeigen. Wenn Sie das Zertifikat mit einem gerade installierten privaten Schlüssel identifiziert haben, doppelklicken Sie auf dem Schlüssel.  

    d.  Wählen Sie auf der Registerkarte **Zugriffssteuerung** die Option **Confirm before allowing access** (Bestätigen, bevor Zugriff zugelassen wird) aus.  

    e.  Navigieren Sie zum Ordner **/Library/Application Support/Microsoft/CCM**, wählen Sie **CCMClient** aus, und wählen Sie dann **Hinzufügen** aus.  

    f.  Wählen Sie **Änderungen sichern** aus, und schließen Sie das Dialogfeld **Schlüsselbundverwaltung**.  

17. Starten Sie den Macintosh-Computer neu.  

