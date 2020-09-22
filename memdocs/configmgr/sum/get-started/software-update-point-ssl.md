---
title: 'Tutorial: Konfigurieren eines Softwareupdatepunkts für die Verwendung von TLS/SSL mit einem PKI-Zertifikat'
titleSuffix: Configuration Manager
description: 'Tutorial: Konfigurieren von Windows Server Update Services (WSUS)-Servern und Softwareupdatepunkten für die Verwendung von TLS/SSL mit einem PKI-Zertifikat.'
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 09/16/2020
ms.topic: tutorial
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: bd9989b8-ccaf-4d51-8262-b4a99b600d12
ms.openlocfilehash: e8359077ac363d2d732b2ffa6712c9b938a2c709
ms.sourcegitcommit: 6176a7825d6c663faa318a6818b7764bc70f08fc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90718931"
---
# <a name="tutorial-configure-a-software-update-point-to-use-tlsssl-with-a-pki-certificate"></a>Tutorial: Konfigurieren eines Softwareupdatepunkts für die Verwendung von TLS/SSL mit einem PKI-Zertifikat

*Gilt für: Configuration Manager (Current Branch)*

Indem Sie die Windows Server Update Services (WSUS)-Server und die entsprechenden Softwareupdatepunkte (SUP) für die Verwendung von TLS/SSL konfigurieren, schränken Sie die Möglichkeiten für einen potenziellen Angreifer ein, Clients von einem Remotestandort aus zu kompromittieren und Berechtigungen zu erhöhen. Um die Verwendung der besten Sicherheitsprotokolle zu gewährleisten, empfehlen wir Ihnen dringend, das TLS/SSL-Protokoll zu implementieren, um Ihre Softwareupdateinfrastruktur zu schützen. Dieser Artikel führt Sie durch die Schritte, die erforderlich sind, um jeden Ihrer WSUS-Server und Softwareupdatepunkt für die Verwendung von HTTPS zu konfigurieren. Weitere Informationen zum Schützen von WSUS finden Sie unter [Schützen von WSUS mit dem Secure Sockets Layer-Protokoll](/windows-server/administration/windows-server-update-services/deploy/2-configure-wsus#25-secure-wsus-with-the-secure-sockets-layer-protocol) in der WSUS-Dokumentation.

In diesem Lernprogramm lernen Sie Folgendes:
> [!div class="checklist"]
> * Abrufen eines PKI-Zertifikats, falls erforderlich
> * Binden des Zertifikats an die WSUS-Verwaltungssite
> * Konfigurieren der WSUS-Webdienste, um SSL anzufordern
> * Konfigurieren der WSUS-Anwendung für die Verwendung von SSL
> * Überprüfen, ob die WSUS-Konsolenverbindung SSL verwenden kann
> * Konfigurieren des Softwareupdatepunkts zum Erzwingen der SSL-Kommunikation mit dem WSUS-Server
> * Überprüfen der Funktionalität mit Configuration Manager

## <a name="considerations-and-limitations"></a>Überlegungen und Einschränkungen

TLS/SSL wird von WSUS zur Authentifizierung von Clientcomputern und WSUS-Downstreamservern gegenüber dem WSUS-Upstreamserver verwendet. TLS/SSL wird von WSUS auch zum Verschlüsseln von Metadaten für Updates verwendet. WSUS verwendet kein TLS/SSL für die Inhaltsdateien eines Updates. Die Inhaltsdateien sind signiert, und der Hash der Datei ist in den Metadaten des Updates enthalten. Bevor die Dateien vom Client heruntergeladen und installiert werden, werden die digitale Signatur und der Hashwert überprüft. Wenn eine der beiden Überprüfungen fehlschlägt, wird das Update nicht installiert.

Beachten Sie die folgenden Einschränkungen, wenn Sie TLS/SSL zum Sichern einer WSUS-Bereitstellung verwenden:

- Die Verwendung von TLS/SSL erhöht den Serverworkload. Sie sollten davon ausgehen, dass bei der Verschlüsselung aller Metadaten, die über das Netzwerk gesendet werden, ein kleiner Leistungsverlust auftritt.
- Wenn Sie WSUS mit einer Remote SQL Server-Datenbank verwenden, wird die Verbindung zwischen dem WSUS-Server und dem Datenbankserver nicht durch TLS/SSL gesichert. Wenn die Verbindung mit der Datenbank gesichert werden muss, sollten Sie folgende Empfehlungen berücksichtigen:
   - Verschieben Sie die WSUS-Datenbank auf den WSUS-Server.
   - Verschieben Sie die Remotedatenbankserver und den WSUS-Server in ein privates Netzwerk.
   - Stellen Sie Internet Protocol Security (IPsec) bereit, um den Netzwerkverkehr zu sichern.

Wenn Sie WSUS-Server und deren Softwareupdatepunkte für die Verwendung von TLS/SSL konfigurieren, sollten Sie die Änderungen für große Configuration Manager-Hierarchien schrittweise einführen. Wenn Sie sich für eine schrittweise Einführung dieser Änderungen entscheiden, beginnen Sie am unteren Ende der Hierarchie, und arbeiten Sie sich nach oben bis zum Standort der zentralen Verwaltung vor.

## <a name="prerequisites"></a>Voraussetzungen

In diesem Tutorial wird die gängigste Methode zum Abrufen eines Zertifikats für die Verwendung mit Internetinformationsdiensten (IIS) behandelt. Stellen Sie unabhängig davon, welche Methode Ihre Organisation verwendet, sicher, dass das Zertifikat die [PKI-Zertifikatsanforderungen](../../core/plan-design/network/pki-certificate-requirements.md) für einen Configuration Manager-Softwareupdatepunkt erfüllt. Wie bei jedem Zertifikat müssen die mit dem WSUS-Server kommunizierenden Geräte der Zertifizierungsstelle vertrauen.

- Ein WSUS-Server mit installierter Softwareupdatepunkt-Rolle
- Stellen Sie sicher, dass Sie die [bewährten Methoden](/troubleshoot/mem/configmgr/windows-server-update-services-best-practices#disable-recycling-and-configure-memory-limits) zum Deaktivieren der Wiederverwendung und Konfigurieren von Arbeitsspeicher-Grenzwerten für WSUS befolgt haben, bevor Sie TLS/SSL aktivieren.
- Eine der beiden folgenden Optionen:
   - Ein entsprechendes PKI-Zertifikat, das sich bereits im **persönlichen** Zertifikatspeicher des WSUS-Servers befindet.
   - Die Möglichkeit, ein entsprechendes PKI-Zertifikat für den WSUS-Server von der Stammzertifizierungsstelle für Ihr Unternehmen anzufordern und zu erhalten.
      - Standardmäßig werden die meisten Zertifikatvorlagen, einschließlich der WebServer-Zertifikatvorlage, nur für Domänenadministratoren ausgegeben. Wenn der angemeldete Benutzer kein Domänenadministrator ist, muss seinem Benutzerkonto die Berechtigung **Registrieren** für die Zertifikat Vorlage erteilt werden.

## <a name="obtain-the-certificate-from-the-ca-if-needed"></a><a name="bkmk_pki"></a> Abrufen des Zertifikats bei Bedarf von der Zertifizierungsstelle

Wenn Sie bereits über ein entsprechendes Zertifikat im **persönlichen** Zertifikatspeicher des WSUS-Servers verfügen, überspringen Sie diesen Abschnitt, und beginnen Sie mit dem Abschnitt [Binden des Zertifikats](#bkmk_bind). Befolgen Sie die Anweisungen in diesem Abschnitt, um an Ihre interne Zertifizierungsstelle eine Zertifikatanforderung zum Installieren eines neuen Zertifikats zu senden.
 
1. Führen Sie `certlm.msc` über eine Administratoreingabeaufforderung auf dem WSUS-Server aus. Ihr Benutzerkonto muss ein lokaler Administrator sein, um Zertifikate für den lokalen Computer verwalten zu können.

   Das Certificate Manager-Tool für das lokale Gerät wird angezeigt.

1. Erweitern Sie **Persönlich**, und klicken Sie dann mit der rechten Maustaste auf **Zertifikate**.
1. Wählen Sie **Alle Aufgaben** und dann **Neues Zertifikat anfordern** aus.
1. Wählen Sie **Weiter** aus, um die Zertifikatregistrierung zu starten.
1. Wählen Sie den Typ des zu registrierenden Zertifikats aus. Der Zertifikatzweck ist **Serverauthentifizierung**, und die zu verwendende Microsoft-Zertifikatvorlage ist **Webserver** oder eine benutzerdefinierte Vorlage, für die **Serverauthentifizierung** als **erweiterte Schlüsselverwendung** angegeben ist. Möglicherweise werden Sie zur Eingabe zusätzlicher Informationen aufgefordert, um das Zertifikat zu registrieren. In der Regel geben Sie mindestens die folgenden Informationen an:
   - **Allgemeiner Name:** Legen Sie auf der Registerkarte **Antragsteller** den Wert auf den FQDN des WSUS-Servers fest.
   - **Anzeigename:** Legen Sie auf der Registerkarte **Allgemein** den Wert auf einen beschreibenden Namen fest, damit Sie das Zertifikat später leichter identifizieren können.
:::image type="content" source="media/certificate-properties.png" alt-text="Fenster „Zertifikateigenschaften“, um weitere Informationen zur Registrierung festzulegen":::
1. Wählen Sie **Registrieren** und dann **Fertig stellen** aus, um die Registrierung abzuschließen.
1. Öffnen Sie das Zertifikat, wenn Sie Details dazu anzeigen möchten, wie z. B. den Fingerabdruck des Zertifikats.

> [!TIP]
> Wenn Ihr WSUS-Server mit dem Internet verbunden ist, benötigen Sie den externen FQDN als Antragstellernamen oder alternativen Antragstellernamen (SAN) im Zertifikat.

## <a name="bind-the-certificate-to-the-wsus-administration-site"></a><a name="bkmk_bind"></a> Binden des Zertifikats an die WSUS-Verwaltungssite

Nachdem Sie das Zertifikat im persönlichen Zertifikatspeicher des WSUS-Servers gespeichert haben, binden Sie es an die WSUS-Verwaltungssite in IIS.

1. Öffnen Sie auf dem WSUS-Server den Internetinformationsdienste-Manager.
1. Wechseln Sie zu **Sites** > **WSUS-Verwaltung**.
1. Wählen Sie **Bindungen** entweder aus dem Aktionsmenü oder durch Klicken mit der rechten Maustaste auf die Site aus.
1. Wählen Sie im Fenster **Sitebindungen** die Zeile für **HTTPS** und dann **Bearbeiten** aus.
   - Entfernen Sie die HTTP-Sitebindung nicht. WSUS verwendet HTTP für die Updateinhaltsdateien.
1. Wählen Sie unter der Option **SSL-Zertifikat** das Zertifikat aus, das an die WSUS-Verwaltungssite gebunden werden soll. Der Anzeigename des Zertifikats wird im Dropdownmenü angezeigt. Wenn kein Anzeigename angegeben wurde, wird das `IssuedTo`-Feld des Zertifikats angezeigt. Wenn Sie nicht sicher sind, welches Zertifikat verwendet werden soll, wählen Sie **Ansicht** aus, und überprüfen Sie, ob der Fingerabdruck demjenigen entspricht, den Sie abgerufen haben.  
   :::image type="content" source="media/edit-site-binding.png" alt-text="Fenster „Sitebindung bearbeiten“ mit SSL-Zertifikatauswahl":::
1. Wählen Sie **OK** aus, wenn Sie fertig sind, und dann **Schließen**, um die Sitebindungen zu beenden. Lassen Sie den IIS-Manager (Internetinformationsdienste) für die nächsten Schritte geöffnet.



## <a name="configure-the-wsus-web-services-to-require-ssl"></a><a name="bkmk_webserv"></a> Konfigurieren der WSUS-Webdienste, um SSL anzufordern

1. Wechseln Sie im IIS-Manager auf dem WSUS-Server zu **Sites** > **WSUS-Verwaltung**.
1. Erweitern Sie die WSUS-Verwaltungssite, um die Liste der Webdienste und virtuellen Verzeichnisse für WSUS anzuzeigen.
1. Für jeden der folgenden WSUS-Webdienste:
   - ApiRemoting30
   - ClientWebService
   - DSSAuthWebService
   - ServerSyncWebService
   - SimpleAuthWebService

   Nehmen Sie die folgenden Änderungen vor:

      1. Wählen Sie **SSL-Einstellungen** aus.
      1. Aktivieren Sie die Option **SSL erforderlich**.
      1. Vergewissern Sie sich, dass die Option **Clientzertifikate** auf **Ignorieren** festgelegt ist.
      1. Klicken Sie auf **Übernehmen**.

Legen Sie die SSL-Einstellungen nicht für die WSUS-Verwaltungssite der obersten Ebene fest, da für bestimmte Funktionen, z. B. Inhalt, HTTP verwendet werden muss.

## <a name="configure-the-wsus-application-to-use-ssl"></a><a name="bkmk_wsusutil"></a> Konfigurieren der WSUS-Anwendung für die Verwendung von SSL

Nachdem die Webdienste so konfiguriert wurden, dass sie SSL erfordern, muss die WSUS-Anwendung benachrichtigt werden, damit sie zusätzliche Konfigurationsschritte ausführen kann, um die Änderung zu unterstützen.

1. Öffnen Sie eine Administratoreingabeaufforderung auf dem WSUS-Server. Das Benutzerkonto, mit dem dieser Befehl ausgeführt wird, muss Mitglied der Gruppe „WSUS-Administratoren“ oder „Lokale Administratoren“ sein.
1. Wechseln Sie in das Verzeichnis mit den Tools für WSUS:  
   `cd "c:\Program Files\Update Services\Tools"`
1. Konfigurieren Sie WSUS für die Verwendung von SSL mit dem folgenden Befehl:

    `WsusUtil.exe configuressl server.contoso.com`
   
   Dabei ist *server.contoso.com* der FQDN des WSUS-Servers.
1. WsusUtil gibt die URL des WSUS-Servers zurück, wobei die Portnummer am Ende angegeben ist. Der Port ist entweder 8531 (Standard) oder 443. Vergewissern Sie sich, dass die erwartete URL zurückgegeben wird. Wenn etwas falsch geschrieben wurde, können Sie den Befehl erneut ausführen.

   :::image type="content" source="media/wsusutil.png" alt-text="Der Befehl „wsusutil configuressl“, der die HTTPS-URL für WSUS zurückgibt":::

> [!TIP] 
> Wenn der WSUS-Server mit dem Internet verbunden ist, geben Sie beim Ausführen von `WsusUtil.exe configuressl` den externen FQDN an.

## <a name="verify-the-wsus-console-can-connect-using-ssl"></a><a name="bkmk_wsus_console"></a> Überprüfen, ob die WSUS-Konsole eine Verbindung über SSL herstellen kann

Die WSUS-Konsole verwendet den ApiRemoting30-Webdienst für die Verbindung. Der Configuration Manager-Softwareupdatepunkt (SUP) verwendet den gleichen Webdienst auch, um den WSUS anzuweisen, bestimmte Aktionen durchzuführen, z. B:

- Initiieren einer Softwareupdatesynchronisierung
- Festlegen des richtigen Upstreamservers für WSUS, und zwar abhängt davon, wo sich der Standort des SUP in Ihrer Configuration Manager-Hierarchie befindet
- Hinzufügen oder Entfernen von Produkten und Klassifikationen für die Synchronisierung auf dem WSUS-Server der obersten Ebene der Hierarchie.
- Entfernen abgelaufener Updates

Öffnen Sie die WSUS-Konsole, um zu überprüfen, ob Sie eine SSL-Verbindung zum ApiRemoting30-Webdienst des WSUS-Servers verwenden können. Einige andere Webdienste werden später getestet.

1. Öffnen Sie die WSUS-Konsole, und wählen Sie **Aktion** > **Verbindung mit Server herstellen** aus.
1. Geben Sie den voll qualifizierten Namen des WSUS-Servers für die Option **Servername** ein.
1. Wählen Sie die **Portnummer** aus, die in der URL von WSUSutil zurückgegeben wird.
1. Wenn Sie entweder 8531 (Standard) oder 443 als Portnummer auswählen, wird die Option **Verbindung mit diesem Server über SSL (Secure Sockets Layer) herstellen** automatisch aktiviert.
       :::image type="content" source="media/connect-wsus-console.png" alt-text="Herstellen der Verbindung mit der WSUS-Konsole über den HTTPS-Port":::
1. Wenn Ihr Configuration Manager-Standortserver über eine Remoteverbindung mit dem Softwareupdatepunkt verbunden ist, starten Sie die WSUS-Konsole vom Standortserver aus, und vergewissern Sie sich, dass die WSUS-Konsole eine Verbindung über SSL herstellen kann.
   - Wenn die WSUS-Remotekonsole keine Verbindung herstellen kann, deutet dies wahrscheinlich auf ein Problem mit der Vertrauensstellung des Zertifikats oder der Namensauflösung oder die Blockierung des Ports hin.

## <a name="configure-the-software-update-point-to-require-ssl-communication-to-the-wsus-server"></a><a name="bkmk_cm_sup"></a> Konfigurieren des Softwareupdatepunkts zum Erzwingen der SSL-Kommunikation mit dem WSUS-Server

Sobald WSUS für die Verwendung von TLS/SSL eingerichtet ist, müssen Sie den entsprechenden Softwareupdatepunkt von Configuration Manager aktualisieren, damit auch er SSL erfordert. Wenn Sie diese Änderung vornehmen, wird Configuration Manager folgende Aktionen ausführen:

- Überprüfen, ob er den WSUS-Server für den Softwareupdatepunkt konfigurieren kann
- Clients anweisen, den SSL-Port zu verwenden, wenn sie zur Überprüfung dieses WSUS-Servers aufgefordert werden.

Um den Softwareupdatepunkt zum Erzwingen der SSL-Kommunikation mit dem WSUS-Server zu konfigurieren, führen Sie die folgenden Schritte aus: 

1. Öffnen Sie die Configuration Manager-Konsole, und stellen Sie eine Verbindung entweder zu Ihrem Standort der zentralen Verwaltung oder zum primären Standortserver für den Softwareupdatepunkt her, den Sie bearbeiten müssen.
1. Wechseln Sie zu **Verwaltung** > **Übersicht** >  **-Standortkonfiguration** > **Server und Standortsystemrollen**.
1. Wählen Sie den Standortsystemserver aus, auf dem WSUS installiert ist, und wählen Sie dann die Standortsystemrolle des Softwareupdatepunkts aus.
1. Wählen Sie im Menüband **Eigenschaften** aus.
1. Aktivieren Sie die Option **SSL-Kommunikation mit dem WSUS-Server erforderlich**.

   :::image type="content" source="media/sup-properties.png" alt-text="SUP-Eigenschaften mit der Option zum Erzwingen der SSL-Kommunikation mit dem WSUS-Server":::
1. Das [**WCM.log**](../../core/plan-design/hierarchy/log-files.md#BKMK_SUPLog) für die Site enthält die folgenden Einträge, wenn Sie die Änderung anwenden:

   ```
   SCF change notification triggered.
   Populating config from SCF
   Setting new configuration state to 1 (WSUS_CONFIG_PENDING)
   ...
   Attempting connection to local WSUS server
   Successfully connected to local WSUS server
   ...
   Setting new configuration state to 2 (WSUS_CONFIG_SUCCESS)
   ```

Die Beispiele für die Protokolldatei wurden bearbeitet, indem nicht benötigte Informationen für dieses Szenario entfernt wurden.  

## <a name="verify-functionality-with-configuration-manager"></a><a name="bkmk_cm_verify"></a> Überprüfen der Funktionalität mit Configuration Manager

### <a name="verify-the-site-server-can-sync-updates"></a>Überprüfen, ob der Standortserver Updates synchronisieren kann

1. Verbinden Sie die Configuration Manager-Konsole mit dem Standort der obersten Ebene.
1. Wechseln Sie zu **Softwarebibliothek** > **Übersicht** > **Softwareupdates** > **Alle Softwareupdates**.
1. Wählen Sie im Menüband die Option **Softwareupdates synchronisieren** aus.
1. Wählen Sie in der Benachrichtigung **Ja** aus, wenn Sie eine standortweite Synchronisierung für Softwareupdates initiieren möchten.
   - Da die WSUS-Konfiguration geändert wurde, erfolgt anstelle einer Deltasynchronisierung eine vollständige Synchronisierung der Softwareupdates.
1. Öffnen Sie die Datei **wsyncmgr.log** für die Site. Wenn Sie einen untergeordneten Standort überwachen, müssen Sie warten, bis die Synchronisierung des übergeordneten Standorts abgeschlossen ist. Vergewissern Sie sich, dass der Server erfolgreich synchronisiert wurde, indem Sie überprüfen, ob das Protokoll Einträge ähnlich der folgenden enthält:

   ```
   Starting Sync
   ...
   Full sync required due to changes in main WSUS server location.
   ...
   Found active SUP SERVER.CONTOSO.COM from SCF File.
   ...
   https://SERVER.CONTOSO.COM:8531
   ...
   Done synchronizing WSUS Server SERVER.CONTOSO.COM
   ...
   sync: Starting SMS database synchronization
   ...
   Done synchronizing SMS with WSUS Server SERVER.CONTOSO.COM
   ```

### <a name="verify-a-client-can-scan-for-updates"></a>Vergewissern Sie sich, dass ein Client nach Updates suchen kann

Wenn Sie den Softwareupdatepunkt so ändern, dass SSL erforderlich ist, erhalten Configuration Manager-Clients die aktualisierte WSUS-URL, wenn sie eine Standortanforderung für einen Softwareupdatepunkt stellen. Durch das Testen eines Clients ist Folgendes möglich:
-  Bestimmen, ob der Client dem Zertifikat des WSUS-Servers vertraut. 
- Bestimmen, ob SimpleAuthWebService und ClientWebService für WSUS funktionsfähig sind.
-  Sicherstellen, dass das virtuelle Verzeichnis des WSUS-Inhalts funktionsfähig ist, wenn der Client während der Überprüfung einen EULA-Wert erhält.

1. Identifizieren eines Clients, der den Softwareupdatepunkt überprüft, der vor kurzem für die Verwendung von TLS/SSL geändert wurde. Verwenden Sie [Skripts ausführen](../..//apps/deploy-use/create-deploy-scripts.md) mit dem folgenden PowerShell-Skript, wenn Sie Hilfe bei der Identifizierung eines Clients benötigen:

   ```powershell
   $Last = (Get-CIMInstance -Namespace "root\CCM\Scanagent" -Class "CCM_SUPLocationList").LastSuccessScanPath
   $Current= Write-Output (Get-CIMInstance -Namespace "root\CCM\Scanagent" -Class "CCM_SUPLocationList").CurrentScanPath
   Write-Host "LastGoodSUP- $last"
   Write-Host "CurrentSUP- $current"
   ```

1. Führen Sie auf Ihrem Testclient einen Überprüfungszyklus für Softwareupdates aus. Sie können einen Scan mit dem folgenden PowerShell-Skript erzwingen:

   ```powershell
   Invoke-WMIMethod -Namespace root\ccm -Class SMS_CLIENT -Name TriggerSchedule "{00000000-0000-0000-0000-000000000113}"
   ```

1. Schauen Sie sich das **ScanAgent.log** des Clients an, um zu überprüfen, ob die Nachricht zum Scannen des Softwareupdatepunkts empfangen wurde.

   ```
   Message received: '<?xml version='1.0' ?>
   <UpdateSourceMessage MessageType='ScanByUpdateSource'>
      <ForceScan>TRUE</ForceScan>
      <UpdateSourceIDs>
            <ID>{A1B2C3D4-1234-1234-A1B2-A1B2C3D41234}</ID>
      </UpdateSourceIDs>
    </UpdateSourceMessage>'
   ```

1. Schauen Sie sich das **LocationServices.log** an, um sicherzustellen, dass dem Client die richtige WSUS-URL angezeigt wird.
**LocationServices.log**
   ```
   WSUSLocationReply : <WSUSLocationReply SchemaVersion="1
   ...
   <LocationRecord WSUSURL="https://SERVER.CONTOSO.COM:8531" ServerName="SERVER.CONTOSO.COM"
   ...
   </WSUSLocationReply>
   ```

1. Schauen Sie sich das **WUAHandler.log** an, um sich zu vergewissern, dass der Client erfolgreich scannen kann.

   ```
   Enabling WUA Managed server policy to use server: https://SERVER.CONTOSO.COM:8531
   ...
   Successfully completed scan.
   ```

## <a name="next-steps"></a>Nächste Schritte

[Bereitstellen von Softwareupdates](../deploy-use/deploy-software-updates.md)