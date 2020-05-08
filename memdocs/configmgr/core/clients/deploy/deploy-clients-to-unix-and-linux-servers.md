---
title: Bereitstellen von UNIX-/Linux-Clients
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Clients auf UNIX- oder Linux-Servern in Configuration Manager bereitstellen.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15a4e323-9f42-4fea-bb14-f2b905d1f77c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c9e8e40a6bdfa129a03e6042985e4956ffb21b5c
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906317"
---
# <a name="how-to-deploy-clients-to-unix-and-linux-servers-in-configuration-manager"></a>Bereitstellen von Clients auf UNIX- und Linux-Servern in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

> [!Important]  
> Ab Version 1902 unterstützt Configuration Manager keine Linux- oder UNIX-Clients mehr. 
> 
> Ziehen Sie deshalb Microsoft Azure Management zum Verwalten von Linux-Servern in Betracht. Azure-Lösungen verfügen über umfangreiche Linux-Unterstützung, die i.d.R. über die Funktionen von Configuration Manager hinausgeht (einschließlich der End-to-End-Patchverwaltung für Linux).


Bevor Sie einen Linux- oder UNIX-Server mit Configuration Manager verwalten können, müssen Sie den Configuration Manager-Client für Linux und UNIX auf jedem Linux- oder UNIX-Server installieren. Sie können die Clientinstallation auf jedem Computer manuell ausführen oder ein Shellskript verwenden, um den Client remote zu installieren. Configuration Manager unterstützt keine Clientpushinstallation für Linux- oder UNIX-Server. Optional können Sie ein Runbook für System Center Orchestrator konfigurieren, um die Clientinstallation auf dem Linux- oder UNIX-Server zu automatisieren.  

 Unabhängig von der verwendeten Installationsmethode erfordert der Installationsvorgang die Verwendung eines Skripts namens **install** , um den Installationsvorgang zu verwalten. Dieses Skript ist enthalten, wenn Sie den Client für Linux und UNIX herunterladen.  

 Das Installationsskript für den Configuration Manager-Client für Linux und UNIX unterstützt Befehlszeileneigenschaften. Einige Befehlszeileneigenschaften sind erforderlich, während andere optional sind. Bei der Installation des Clients müssen Sie z. B. einen Verwaltungspunkt, von der Website angeben, die von Linux oder UNIX-Server für den ersten Kontakt mit dem Standort verwendet wird. Die vollständige Liste der Befehlszeileneigenschaften finden Sie unter [Befehlszeileneigenschaften zur Installation des Clients auf Linux- und UNIX-Servern](#BKMK_CmdLineInstallLnUClient).  

 Nach der Installation des Clients geben Sie die Clienteinstellungen in der Configuration Manager-Konsole an, um den Client-Agent auf die gleiche Weise wie Windows-basierte Clients zu konfigurieren. Weitere Informationen finden Sie unter  [Clienteinstellungen für Linux- und UNIX-Server](../../../core/clients/manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ClientSettingsforLnU).  

##  <a name="about-client-installation-packages-and-the-universal-agent"></a><a name="BKMK_AboutInstallPackages"></a>Informationen zu Clientinstallationspaketen und der universelle Agent  
 Um den Client für Linux und UNIX auf einer bestimmten Plattform zu installieren, müssen Sie das entsprechende Clientinstallationspaket für den Computer verwenden, auf dem Sie den Client installieren. Die jeweiligen Clientinstallationspakete sind in jedem Clientdownload aus dem [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=47719)enthalten. Zusätzlich zu den Clientinstallationspaketen umfasst das Clientdownload das **install** -Skript zur Verwaltung der Clientinstallation auf den einzelnen Computern.  

 Wenn Sie einen Client installieren, können Sie unabhängig vom verwendeten Clientinstallationspaket die gleichen Schritte und Befehlszeileneigenschaften verwenden.  

 Informationen zu den Betriebssystemen, Plattformen und Clientinstallationspaketen, die von den einzelnen Releases des Configuration Manager-Clients für Linux und UNIX unterstützt werden, finden Sie unter [Linux- und UNIX-Server](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#linux-and-unix-servers).  

##  <a name="install-the-client-on-linux-and-unix-servers"></a><a name="BKMK_InstallLnUClient"></a> Installieren des Clients auf Linux- und UNIX-Servern  
 Zum Installieren des Clients für Linux und UNIX, führen Sie ein Skript auf jedem Linux- oder UNIX-Computer. Das Skript namens **install** unterstützt Befehlszeileneigenschaften, die das Installationsverhalten ändern und auf das Clientinstallationspaket verweisen. Das Skript und Client-Installation Installationspaket muss auf dem Client befinden. Das Clientinstallationspaket enthält die Configuration Manager-Clientdateien für ein bestimmtes Linux oder UNIX-Betriebssystem und die entsprechende Plattform.
Jedes Client-Installationspaket enthält alle erforderlichen Dateien zum Abschließen der Clientinstallation. Im Gegensatz zu Windows-basierten Computern lädt es keine zusätzlichen Dateien aus einem Verwaltungspunkt oder anderem Quellspeicherort herunter.  

 Nach der Installation des Configuration Manager-Clients für Linux und UNIX muss der Computer nicht neu gestartet werden. Sobald die Softwareinstallation abgeschlossen ist, kann der Client betrieben werden. Wenn Sie den Computer neu starten, wird auch der Configuration Manager-Client automatisch neu gestartet.  

 Der installierte Client führt mit Root-Anmeldeinformationen. Stammanmeldeinformationen sind erforderlich, um Hardwareinventurdaten zu sammeln und die Softwarebereitstellung auszuführen.  

 Verwenden Sie das folgende Befehlsformat:  

 `./install -mp <computer> -sitecode <sitecode> <property #1> <property #2> <client installation package>`  

-   `install` ist der Name der Skriptdatei, die vom Client für Linux und UNIX installiert wird. Diese Datei wird mit der Client-Software bereitgestellt.  

-   `-mp <computer>` gibt den ersten Verwaltungspunkt an, der vom Client verwendet wird. Beispiel: `smsmp.contoso.com`  

-   `-sitecode <site code>` gibt den Standortcode an, dem der Client zugewiesen wurde. Beispiel: `S01`  

-   `<property #1> <property #2>` gibt die mit dem Installationsskript zu verwendenden Befehlszeileneigenschaften an.  

    > [!NOTE]  
    >  Weitere Informationen finden Sie unter [Befehlszeileneigenschaften zur Installation des Clients auf Linux- und UNIX-Servern](#BKMK_CmdLineInstallLnUClient).  

-   Das**Clientinstallationspaket** ist der Name des TAR-Pakets der Clientinstallation für das Betriebssystem, die Version und die CPU-Architektur des Computers. Die Client-Installation TAR-Datei muss zuletzt angegeben werden. Beispiel: `ccm-Universal-x64.<build>.tar`  

###  <a name="to-install-the-configuration-manager-client-on-linux-and-unix-servers"></a><a name="BKMK_ToInstallLnUClinent"></a> Installieren des Configuration Manager-Clients auf Linux- und UNIX-Servern  

1.  Auf einem Windows-Computer müssen Sie [die entsprechende Clientdatei für den Linux- oder UNIX-Server herunterladen](https://www.microsoft.com/download/details.aspx?id=47719) , den Sie verwalten möchten.  

2.  Führen Sie die selbstextrahierende EXE-Datei auf dem Windows-Computer aus, um das Installationsskript und die TAR-Datei für die Clientinstallation zu extrahieren.  

3.  Kopieren Sie das **install** -Skript und die TAR-Datei in einen Ordner auf dem Server, den Sie verwalten möchten.  

4.  Führen Sie auf dem UNIX- oder Linux-Server den folgenden Befehl aus, um die Ausführung des Skripts als Programm zu ermöglichen: `chmod +x install`  

    > [!IMPORTANT]  
    >  Sie müssen Anmeldeinformationen zum Installieren des Clients verwenden.  

5.  Führen Sie als Nächstes den folgenden Befehl für die Installation des Configuration Manager-Clients aus: `./install -mp <hostname> -sitecode <code> ccm-Universal-x64.<build>.tar`  

     Wenn Sie diesen Befehl eingeben, verwenden Sie zusätzliche Befehlszeileneigenschaften, die Sie benötigen. Die Liste der Befehlszeileneigenschaften finden Sie unter [Befehlszeileneigenschaften zur Installation des Clients auf Linux- und UNIX-Servern](#BKMK_CmdLineInstallLnUClient).  

6.  Nachdem das Skript ausgeführt wurde, überprüfen Sie die Installation anhand der Datei **/var/opt/microsoft/scxcm.log** . Darüber hinaus können Sie überprüfen, ob der Client installiert wurde und mit dem Standort kommuniziert, indem Sie die Details für den betreffenden Client unter dem Knoten **Geräte** im Arbeitsbereich **Bestand und Kompatibilität** der Configuration Manager-Konsole anzeigen.  

###  <a name="command-line-properties-for-installing-the-client-on-linux-and-unix-servers"></a><a name="BKMK_CmdLineInstallLnUClient"></a> Befehlszeileneigenschaften zur Installation des Clients auf Linux- und UNIX-Servern  
 Die folgenden Eigenschaften sind zum Ändern des Verhaltens des Installationsskripts verfügbar:  

> [!NOTE]  
>  Verwenden Sie die Eigenschaft `-h` zum Anzeigen dieser Liste von unterstützten Eigenschaften.  

-   `-mp <server FQDN>`  

     Erforderlich. Gibt den Verwaltungspunktserver, den der Client als ersten Kontaktpunkt verwendet, mithilfe des FQDNs an.  

    > [!IMPORTANT]  
    >  Diese Eigenschaft dient nicht zur Angabe des Verwaltungspunkts, dem der Client nach der Installation zugewiesen wird.  

    > [!NOTE]  
    >  Wenn Sie mit der `-mp`-Eigenschaft einen Verwaltungspunkt angeben, der ausschließlich für die Annahme von HTTPS-Clientverbindungen konfiguriert wurde, müssen Sie auch die `-UsePKICert`-Eigenschaft verwenden.  

-   `-sitecode <sitecode>`  

     Erforderlich. Gibt den primären Configuration Manager-Standort an, um diesem den Configuration Manager-Client zuzuweisen. Beispiel: `-sitecode S01`  

-   `-fsp <server_FQDN>`  

     (Optional) Gibt an, über den FQDN der Fallbackstatuspunkt-Server, die der Client verwendet, um Status-Nachrichten zu senden. Weitere Informationen finden Sie unter [Bestimmen, ob ein Fallbackstatuspunkt erforderlich ist](plan/determine-the-site-system-roles-for-clients.md#fallback-status-point).  

-   `-dir <directory>`  

     (Optional) Gibt einen alternativen Speicherort zum Installieren der Configuration Manager-Clientdateien an. Standardmäßig wird vom Client an den folgenden Speicherort installiert: `/opt/microsoft`  

-   `-nostart`  

     (Optional) Verhindert den automatischen Start des Configuration Manager-Clientdiensts **ccmexec.bin**, nachdem die Clientinstallation abgeschlossen wurde.  

     Nach der Installation auf dem Client müssen Sie den Client-Dienst manuell starten.  

     Standardmäßig beginnt der Client-Dienst nach Abschluss der Clientinstallations und bei jedem des Computers Neustart.  

-   `-clean`  

     (Optional) Gibt an, dass alle Clientdateien und Daten von einem zuvor installierten Client für Linux und UNIX, vor Beginn der neue Installation. Durch diese Aktion werden Datenbank und Zertifikatspeicher des Clients entfernt.  

-   `-keepdb`  

     (Optional) Gibt an, dass die lokale Clientdatenbank beibehalten und bei der Neuinstallation eines Clients wiederverwendet wird. Wenn Sie einen Client neu installieren, wird standardmäßig dieser Datenbank gelöscht.  

-   `-UsePKICert <parameter>`  

     (Optional) Gibt den vollständigen Pfad und Namen mit einem x. 509-PKI-Zertifikat im Format Public Key Certificate Standard (PKCS #12). Dieses Zertifikat wird zur Client-Authentifizierung verwendet. Wenn während der Installation kein Zertifikat angegeben wird und Sie ein Zertifikat hinzufügen oder ändern müssen, verwenden Sie das Hilfsprogramm **certutil** . Weitere Informationen finden Sie unter [Verwalten von Zertifikaten auf dem Client für Linux und UNIX](../manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts).  

     Bei Verwendung von `-UsePKICert` müssen Sie außerdem den `-certpw`-Befehlszeilenparameter verwenden, um das der PKCS #12-Datei zugeordnete Kennwort anzugeben.  

     Wenn Sie diese Eigenschaft zur Angabe eines PKI-Zertifikats nicht verwenden, verwendet der Client ein selbstsigniertes Zertifikat, und die gesamte Kommunikation mit Standortsystemen erfolgt über HTTP.  

     Bei Angabe ein ungültiges Zertifikats auf den Client über die Befehlszeile zu installieren, werden keine Fehler zurückgegeben. Die Zertifikatüberprüfung erfolgt nach der Installation des Clients. Beim Start des Clients werden Zertifikate mit dem Verwaltungspunkt überprüft. Wenn die Überprüfung eines Zertifikats fehlschlägt, wird in **scxcm.log** die folgende Meldung angezeigt: **Failed validate the certificate for Management Point** (Fehler beim Überprüfen des Zertifikats für den Verwaltungspunkt). Der Standardspeicherort der Protokolldatei ist:  **/var/opt/microsoft/scxcm.log**.  

     > [!NOTE]  
     > Sie müssen diese Eigenschaft immer angeben, wenn Sie einen Client installieren, und die Eigenschaft `-mp` verwenden, um einen Verwaltungspunkt anzugeben, der ausschließlich für Clientverbindungen über HTTPS konfiguriert wurde.  

     Beispiel: `-UsePKICert <full path and filename> -certpw <password>`  

-   `-certpw <parameter>`  

     (Optional) Gibt das Kennwort an, das der PKCS#12-Datei zugeordnet ist, die Sie mithilfe der `-UsePKICert`-Eigenschaft angegeben haben.  

     Beispiel: `-UsePKICert <full path and filename> -certpw <password>`  

-   `-NoCRLCheck`  

     (Optional) Gibt an, dass ein Client die Zertifikatssperrlisten nicht überprüfen sollte, wenn er über HTTPS unter Verwendung eines PKI-Zertifikats kommuniziert. Wenn diese Option nicht angegeben wird, überprüft der Client die Zertifikatsperrliste vor dem Einrichten einer HTTPS-Verbindung mithilfe von PKI-Zertifikaten. Weitere Informationen zu Client CRL-Prüfung finden Sie unter Planen der PKI-zertifikatsperrung.  

     Beispiel: `-UsePKICert <full path and filename> -certpw <password> -NoCRLCheck`  

-   `-rootkeypath <file location>`  

     (Optional) Hiermit werden der vollständige Pfad- und Dateiname des vertrauenswürdigen Configuration Manager-Stammschlüssels angegeben. Der vertrauenswürdige Configuration Manager-Stammschlüssel bietet einen Mechanismus, mit dem Linux- und UNIX-Clients überprüfen können, ob sie mit einem Standortsystem verbunden sind, das der richtigen Hierarchie angehört.  

     Wenn Sie den vertrauenswürdigen Stammschlüssel nicht in der Befehlszeile angeben, vertraut der Client dem ersten Verwaltungspunkt, mit dem er kommuniziert, und ruft automatisch den vertrauenswürdigen Stammschlüssel von diesem Verwaltungspunkt ab.  

     Weitere Informationen finden Sie unter  [Planning for the Trusted Root Key](../../../core/plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

     Beispiel: `-rootkeypath <full path and filename>`  

-   `-httpport <port>`  

     (Optional) Gibt den Port an, der für Verwaltungspunkte konfiguriert ist, die vom Client verwendet wird, wenn die Kommunikation mit Verwaltungspunkten über HTTP. Wenn der Anschluss nicht angegeben wurde, wird der Standardwert 80 verwendet.  

     Beispiel: `-httpport 80`  

-   `-httpsport <port>`  

     (Optional) Gibt den Port an, der für Verwaltungspunkte, der Client konfiguriert ist bei der Kommunikation mit Verwaltungspunkten über HTTPS verwendet. Wenn der Anschluss nicht angegeben wurde, wird der Standardwert 443 verwendet.  

     Beispiel: `-UsePKICert <full path and certificate name> -httpsport 443`  

-   `-ignoreSHA256validation`  

     (Optional) Gibt an, dass die Clientinstallation SHA-256-Überprüfung übersprungen. Verwenden Sie diese Option bei der Installation des Clients unter Betriebssystemen, die ohne OpenSSL-Version mit SHA-256-Unterstützung freigegeben wurden. Weitere Informationen finden Sie unter [Informationen zu Linux- und UNIX-Betriebssystemen, die SHA-256 nicht unterstützen](../../../core/clients/deploy/plan/planning-for-client-deployment-to-linux-and-unix-computers.md#BKMK_NoSHA-256).  

-   `-signcertpath <file location>`  

     (Optional) Gibt den vollständigen Pfad und **CER** Dateinamen des exportierten selbstsignierten Zertifikats auf dem Standortserver. Wenn keine PKI-Zertifikate verfügbar sind, generiert der Configuration Manager-Standortserver automatisch selbstsignierte Zertifikate.  

     Diese Zertifikate werden verwendet, um sicherzustellen, dass die Clientrichtlinien vom Verwaltungspunkt heruntergeladen aus dem gewünschten Standort gesendet wurden. Wenn während der Installation kein selbstsigniertes Zertifikat angegeben wird und Sie das Zertifikat ändern müssen, verwenden Sie das Hilfsprogramm **certutil** . Weitere Informationen finden Sie unter [Verwalten von Zertifikaten auf dem Client für Linux und UNIX](../manage/manage-clients-for-linux-and-unix-servers.md#BKMK_ManageLinuxCerts).  

     Dieses Zertifikat kann über den **SMS** -Zertifikatspeicher unter dem Antragstellernamen **Standortserver** und dem Anzeigenamen **Signaturzertifikat des Standortservers**abgerufen werden.  

     Wenn diese Option während der Installation nicht angegeben wird, vertrauen Linux- und UNIX-Clients dem ersten Verwaltungspunkt, mit dem sie kommunizieren. Sie rufen das Signaturzertifikat automatisch von diesem Verwaltungspunkt ab.  

     Beispiel: `-signcertpath <full path and file name>`  

-   `-rootcerts`  

     (Optional) Gibt zusätzliche zu importierende PKI-Zertifikate an, die der Hierarchie der Verwaltungspunkt-Zertifizierungsstelle nicht angehören. Wenn Sie mehrere Zertifikate in der Befehlszeile angeben, sollten sie durch Trennzeichen getrennt sein.  

     Verwenden Sie diese Option, wenn Sie PKI-Clientzertifikate verwenden, die mit keinem für die Verwaltungspunkte Ihres Standorts vertrauenswürdigen Zertifikat der Stammzertifizierungsstelle verkettet sind. Verwaltungspunkte lehnen den Client ab, wenn das Clientzertifikat nicht mit einem vertrauenswürdigen Stammzertifikat in der Zertifikatausstellerliste des Standorts verkettet ist.  

     Wenn Sie diese Option nicht verwenden, überprüft der Linux- und UNIX-Client die Vertrauenshierarchie nur anhand des Zertifikats in der `-UsePKICert`-Option.  

     Beispiel: `-rootcerts <full path and file name>,<full path and file name>`  

###  <a name="uninstalling-the-client-from-linux-and-unix-servers"></a><a name="BKMK_UninstallLnUClient"></a> Deinstallieren des Clients von Linux- und UNIX-Servern  
 Zum Deinstallieren des Configuration Manager-Clients für Linux und UNIX verwenden Sie das Hilfsprogramm **uninstall**. Standardmäßig befindet sich diese Datei der **/opt/Microsoft/Configuration Manager/Bin/** Ordner auf dem Clientcomputer. Dieser Deinstallationsbefehl unterstützt keine Befehlszeilenparameter und entfernt alle Dateien, die im Zusammenhang mit der Clientsoftware stehen, vom Server.  

 Um den Client zu deinstallieren, verwenden Sie die folgende Befehlszeile: **/opt/microsoft/configmgr/bin/uninstall**  

 Sie müssen nach der Deinstallation des Configuration Manager-Clients für Linux und UNIX den Computer nicht neu starten.  

##  <a name="configure-request-ports-for-the-client-for-linux-and-unix"></a><a name="BKMK_ConfigLnUClientCommuincations"></a> Konfigurieren von Anforderungsports für den Client für Linux und UNIX  
 Ähnlich wie Windows-basierte Clients verwendet der Configuration Manager-Client für Linux und UNIX HTTP und HTTPS zur Kommunikation mit Configuration Manager-Standortsystemen. Die Ports, die der Configuration Manager-Client für die Kommunikation verwendet, werden als Anforderungsports bezeichnet.  

 Wenn Sie den Configuration Manager-Client für Linux und UNIX installieren, können Sie die Standardanforderungsports des Clients ändern, indem Sie die Installationseigenschaften **-httpport** und **-httpsport** angeben. Wenn Sie die Installationseigenschaft und einen benutzerdefinierten Wert nicht angeben, verwendet der Client die Standardwerte. Die Standardwerte sind **80** für HTTP-Datenverkehr und **443** für HTTPS-Datenverkehr.  

 Nachdem Sie den Client installiert haben, können Sie die Konfiguration von dessen Anforderungsport nicht ändern. Stattdessen müssen Sie zum Ändern der Portkonfiguration neu zu installieren und die neue Portkonfiguration angeben. Wenn Sie den Client neu installieren, um die Anforderungsportnummern zu ändern, führen Sie den Befehl **install** ähnlich wie bei der Installation neuer Clients aus, verwenden dabei jedoch die zusätzliche Befehlszeileneigenschaft **-keepdb**. Durch diese Option wird die Installation angewiesen, die Clientdatenbank und die Dateien einschließlich der GUID und des Zertifikatspeichers des Clients beizubehalten.  

 Weitere Informationen zu Portnummern für die Clientkommunikation finden Sie unter [Konfigurieren von Clientkommunikationsports](../../../core/clients/deploy/configure-client-communication-ports.md).  

##  <a name="configure-the-client-for-linux-and-unix-to-locate-management-points"></a><a name="BKMK_ConfigClientMP"></a> Konfigurieren Sie den Client für Linux und UNIX nach Verwaltungspunkten suchen  
 Beim Installieren des Configuration Manager-Clients für Linux und UNIX müssen Sie einen Verwaltungspunkt als ersten Kontaktpunkt angeben.  

 Der Configuration Manager-Client für Linux und UNIX stellt bei der Clientinstallation eine Verbindung mit diesem Verwaltungspunkt her. Wenn der Client keine Verbindung mit dem Verwaltungspunkt herstellen kann, wiederholt die Clientsoftware den Vorgang so lange, bis die Verbindung erfolgreich hergestellt wird.  

 Weitere Informationen dazu, wie Clients Verwaltungspunkte suchen, finden Sie unter [Suchen von Verwaltungspunkten](assign-clients-to-a-site.md#locating-management-points).
