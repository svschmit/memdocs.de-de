---
title: Beispiel für PKI-Zertifikatbereitstellung
titleSuffix: Configuration Manager
description: Lernen Sie anhand eines ausführlichen Beispiels, wie Sie PKI-Zertifikate erstellen und bereitstellen, die von Configuration Manager verwendet werden.
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3417ff88-7177-4a0d-8967-ab21fe7eba17
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 994ee2916020ecc4e6d9d3c35f41fe24d5a31405
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701568"
---
# <a name="step-by-step-example-deployment-of-the-pki-certificates-for-configuration-manager-windows-server-2008-certification-authority"></a>Beispiel für die schrittweise Bereitstellung der PKI-Zertifikate für Configuration Manager: Windows Server 2008-Zertifizierungsstelle

*Gilt für: Configuration Manager (Current Branch)*

In diesem Beispiel für die schrittweise Bereitstellung unter Verwendung einer Windows Server 2008-Zertifizierungsstelle (CA) finden Sie Verfahren zum Erstellen und Bereitstellen von PKI-Zertifikaten (Public Key-Infrastruktur), die von Configuration Manager verwendet werden. In diesem Verfahren werden eine Unternehmenszertifizierungsstelle (CA) und Zertifikatvorlagen verwendet. Die Schritte sollten nur in einem Testnetzwerk zur Konzeptüberprüfung angewendet werden.  

Da die erforderlichen Zertifikate auf unterschiedliche Weise bereitgestellt werden, entnehmen Sie die Informationen zu den erforderlichen Vorgehensweisen und bewährten Methoden der entsprechenden Dokumentation für die PKI-Bereitstellung, um die erforderlichen Zertifikate für eine Produktionsumgebung bereitzustellen. Weitere Informationen zu den Zertifikatanforderungen finden Sie unter [PKI-Zertifikatanforderungen für System Center Configuration Manager](pki-certificate-requirements.md).  

> [!TIP]
> Die Anweisungen in diesem Thema lassen sich leicht an andere Betriebssysteme anpassen, die im Abschnitt „Voraussetzungen für ein Testnetzwerk“ nicht erwähnt werden. Wenn bei Ihnen allerdings die ausstellende Zertifizierungsstelle unter Windows Server 2012 ausgeführt wird, werden Sie nicht zur Eingabe der Zertifikatvorlagenversion aufgefordert. Geben Sie stattdessen auf der Registerkarte **Kompatibilität** die Vorlageneigenschaften ein:  
>
> - **Zertifizierungsstelle:** **Windows Server 2003**  
>   - **Zertifikatempfänger:** **Windows XP/Server 2003**  

## <a name="test-network-requirements"></a><a name="BKMK_testnetworkenvironment"></a> Voraussetzungen für ein Testnetzwerk

Für die schrittweisen Anleitungen gelten die folgenden Anforderungen:  

- Im Testnetzwerk werden die Active Directory-Domänendienste mit Windows Server 2008 ausgeführt. Zudem ist das Netzwerk als eine einzelne Domäne bzw. Gesamtstruktur installiert.  

- Sie verfügen über einen Mitgliedsserver, auf dem Windows Server 2008 Enterprise Edition ausgeführt wird und die Rolle „Active Directory-Zertifikatdienste“ installiert ist. Der Mitgliedsserver ist außerdem als Unternehmens-Stammzertifizierungsstelle konfiguriert.  

- Sie verfügen über einen Computer mit Windows Server 2008 (Standard Edition oder Enterprise Edition, R2 oder höher), der als Mitgliedsserver festgelegt wurde und auf dem Internetinformationsdienste (IIS) installiert sind. Dieser Computer übernimmt die Funktion des Configuration Manager-Standortsystemservers, den Sie mit einem Intranet-FQDN (zur Unterstützung von Clientverbindungen im Intranet) sowie einem Internet-FQDN konfigurieren, falls Sie mobile Geräte, die von System Center Configuration Manager angemeldet wurden sowie Clients im Internet unterstützen müssen.  

- Sie verfügen über einen Windows Vista-Client, auf dem das aktuelle Service Pack installiert ist. Dieser Computer ist mit einem aus ASCII-Zeichen bestehenden Computernamen eingerichtet und gehört der Domäne an. Bei diesem Computer wird es sich um einen Configuration Manager-Clientcomputer handeln.  

- Sie können sich mit einem Administratorkonto der Stammdomäne oder der Unternehmensdomäne anmelden und dieses Konto für alle in dieser Beispielbereitstellung aufgeführten Prozeduren verwenden.  

## <a name="overview-of-the-certificates"></a><a name="BKMK_overview2008"></a> Übersicht über die Zertifikate

In der folgenden Tabelle werden die PKI-Zertifikattypen aufgelistet, die möglicherweise für Configuration Manager erforderlich sind, und ihre Verwendung wird beschrieben.  

|Zertifikatanforderung|Zertifikatbeschreibung|  
|-----------------------------|-----------------------------|  
|Webserverzertifikat für Standortsysteme, an denen IIS ausgeführt werden|Dieses Zertifikat wird zum Verschlüsseln von Daten und zum Authentifizieren des Servers bei Clients verwendet. Es muss extern von Configuration Manager auf Standortsystemservern installiert werden, von denen Internetinformationsdienste (IIS) ausgeführt werden und die zur Verwendung von HTTPS in Configuration Manager konfiguriert sind.<br /><br /> Die Schritte zum Einrichten und Installieren dieses Zertifikats finden Sie unter [Bereitstellen des Webserverzertifikats für Standortsysteme, von denen IIS ausgeführt werden](#BKMK_webserver2008_cm2012) in diesem Thema.|  
|Servicezertifikat für Clients für die Verbindung mit cloudbasierten Verteilungspunkten|Die Schritte zum Konfigurieren und Installieren dieses Zertifikats finden Sie unter [Bereitstellen des Dienstzertifikats für cloudbasierte Verteilungspunkte](#BKMK_clouddp2008_cm2012) in diesem Thema.<br /><br /> **Wichtig:** Dieses Zertifikat wird in Verbindung mit dem Windows Azure-Verwaltungszertifikat verwendet. Weitere Informationen zu diesem Verwaltungszertifikat finden Sie unter [Erstellen eines Verwaltungszertifikats](https://docs.microsoft.com/azure/cloud-services/cloud-services-certs-create#create-a-new-self-signed-certificate) und [Gewusst wie: Hinzufügen eines Verwaltungszertifikats zu einem Windows Azure-Abonnement](https://docs.microsoft.com/azure/cloud-services/cloud-services-configure-ssl-certificate-portal#step-3-upload-a-certificate) im Abschnitt zur Windows Azure-Plattform in der MSDN Library.|  
|Clientzertifikat für Windows-Computer|Dieses Zertifikat wird zum Authentifizieren von Configuration Manager-Clientcomputern auf Standortsystemen verwendet, die zum Verwenden von HTTPS eingerichtet sind. Es kann auch für Verwaltungspunkte und Zustandsmigrationspunkte verwendet werden, um deren Betriebsstatus zu überwachen, wenn sie zum Verwenden von HTTPS eingerichtet sind. Es muss extern von Configuration Manager auf Computern installiert werden.<br /><br /> Die Schritte zum Einrichten und Installieren dieses Zertifikats finden Sie unter [Bereitstellen des Clientzertifikats für Windows-Computer](#BKMK_client2008_cm2012) in diesem Thema.|  
|Clientzertifikat für Verteilungspunkte|Von diesem Zertifikat werden zwei Zwecke erfüllt:<br /><br /> Das Zertifikat wird zum Authentifizieren des Verteilungspunkts bei einem für HTTPS aktivierten Verwaltungspunkt verwendet, bevor Statusmeldungen vom Verteilungspunkt gesendet werden.<br /><br /> Wenn die Verteilungspunktoption **PXE-Unterstützung für Clients aktivieren** ausgewählt ist, wird das Zertifikat an Computer gesendet, von denen ein PXE-Start ausgeführt wird, um während der Bereitstellung des Betriebssystems eine Verbindung mit dem für HTTPS aktivierten Verwaltungspunkt zu ermöglichen.<br /><br /> Die Schritte zum Konfigurieren und Installieren dieses Zertifikats finden Sie unter [Bereitstellen des Clientzertifikats für Verteilungspunkte](#BKMK_clientdistributionpoint2008_cm2012) in diesem Thema.|  
|Anmeldungszertifikat für mobile Geräte|Dieses Zertifikat wird zum Authentifizieren von Configuration Manager-Clients für mobile Geräte bei Standortsystemen verwendet, die zum Verwenden von HTTPS eingerichtet sind. Das Zertifikat muss im Rahmen der Registrierung mobiler Geräte in Configuration Manager installiert werden, und Sie wählen die konfigurierte Zertifikatvorlage als Clienteinstellung von mobilen Geräten aus.<br /><br /> Die Schritte zum Konfigurieren dieses Zertifikats finden Sie unter [Bereitstellen des Registrierungszertifikats für mobile Geräte](#BKMK_mobiledevices2008_cm2012) in diesem Thema.|  
|Clientzertifikat für Macintosh-Computer|Sie können dieses Zertifikat von einem Macintosh-Computer anfordern und installieren, wenn Sie die Configuration Manager-Registrierung verwenden und die konfigurierte Zertifikatvorlage als Clienteinstellung für mobile Geräte auswählen.<br /><br /> Die Schritte zum Einrichten dieses Zertifikats finden Sie unter [Bereitstellen des Clientzertifikats für Macintosh-Computer](#BKMK_MacClient_SP1) in diesem Thema.|  

## <a name="deploy-the-web-server-certificate-for-site-systems-that-run-iis"></a><a name="BKMK_webserver2008_cm2012"></a> Bereitstellen des Webserverzertifikats für Standortsysteme, von denen IIS ausgeführt werden

Diese Zertifikatbereitstellung besteht aus den folgenden Prozeduren:  

- Erstellen und Ausstellen der Webserver-Zertifikatvorlage bei der Zertifizierungsstelle  

- Anfordern des Webserverzertifikats  

- Konfigurieren von IIS für die Verwendung des Webserverzertifikats  

### <a name="create-and-issue-the-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_webserver22008"></a> Erstellen und Ausstellen der Webserver-Zertifikatvorlage bei der Zertifizierungsstelle

Dieses Verfahren erstellt eine Zertifikatvorlage für Configuration Manager-Standortsysteme und fügt sie der Zertifizierungsstelle hinzu.  

##### <a name="to-create-and-issue-the-web-server-certificate-template-on-the-certification-authority"></a>So können Sie die Webserver-Zertifikatvorlage bei der Zertifizierungsstelle generieren und ausstellen

1.  Erstellen Sie eine Sicherheitsgruppe mit der Bezeichnung **ConfigMgr IIS Servers**, die die Mitgliedsserver für die Installation der Configuration Manager-Standortsysteme, von denen IIS ausgeführt werden, enthält.  

2.  Klicken Sie auf dem Mitgliedsserver, auf dem die Zertifikatdienste installiert sind, in der Zertifizierungsstellenkonsole mit der rechten Maustaste auf **Zertifikatvorlagen**, und wählen Sie dann **Verwalten** aus, um die Konsole **Zertifikatvorlagen** zu laden.  

3.  Klicken Sie im Ergebnisbereich mit der rechten Maustaste auf den Eintrag, für den in der Spalte **Vorlagenanzeigename** der Name **Webserver** angezeigt wird, und wählen Sie dann **Doppelte Vorlage** aus.  

4.  Vergewissern Sie sich, dass im Dialogfeld **Doppelte Vorlage** die Option **Windows 2003 Server Enterprise Edition** ausgewählt ist, und wählen Sie dann **OK** aus.  

    > [!IMPORTANT]  
    >  Wählen Sie nicht **Windows 2008 Server Enterprise Edition**aus.  

5.  Geben Sie im Dialogfeld **Eigenschaften der neuen Vorlage** auf der Registerkarte **Allgemein** einen Vorlagennamen ein, z.B. **ConfigMgr-Webserverzertifikat**, um die Webzertifikate zu generieren, die auf Configuration Manager-Standortsystemen verwendet werden.  

6.  Wählen Sie die Registerkarte **Antragstellername** aus, und vergewissern Sie sich, dass **Informationen werden in der Anforderung angegeben** ausgewählt ist.  

7.  Wählen Sie die Registerkarte **Sicherheit** aus, und entfernen Sie aus den Sicherheitsgruppen **Domänen-Admins** und **Organisations-Admins** die Berechtigung **Registrieren**.  

8.  Wählen Sie **Hinzufügen** aus, geben Sie in das Textfeld **ConfigMgr-IIS-Server** ein, und wählen Sie dann **OK** aus.  

9. Wählen Sie für diese Gruppe die Berechtigung **Registrieren** aus, und lassen Sie die Berechtigung **Lesen** aktiviert.  

10. Wählen Sie **OK** aus, und schließen Sie die **Zertifikatvorlagenkonsole**.  

11. Klicken Sie in der Zertifizierungsstellenkonsole mit der rechten Maustaste auf **Zertifikatvorlagen**, wählen Sie **Neu** und dann **Auszustellende Zertifikatvorlage** aus.  

12. Wählen Sie im Dialogfeld **Zertifikatvorlagen aktivieren** die neu erstellte Vorlage **ConfigMgr-Webserverzertifikat** aus, und wählen Sie dann **OK** aus.  

13. Wenn Sie mit dem Erstellen und Ausstellen von Zertifikaten fertig sind, schließen Sie die Konsole **Zertifizierungsstelle**.  

###  <a name="request-the-web-server-certificate"></a><a name="BKMK_webserver32008"></a> Anfordern des Webserverzertifikats  
 Bei dieser Prozedur können Sie Werte für Intranet- und Internet-FQDN angeben, die in den Eigenschaften des Standortsystemservers eingerichtet werden, bevor das Webserverzertifikat auf dem Mitgliedsserver installiert wird, auf dem IIS ausgeführt werden.  

##### <a name="to-request-the-web-server-certificate"></a>So fordern Sie das Webserverzertifikat an  

1.  Starten Sie den Mitgliedsserver neu, auf dem IIS ausgeführt werden. Dadurch stellen Sie sicher, dass mithilfe der Berechtigungen **Lesen** und **Registrieren**, die Sie konfiguriert haben, für den Computer ein Zugriff auf die Zertifikatvorlage, die Sie erstellt haben, möglich ist.  

2.  Wählen Sie **Start** und anschließend **Ausführen** aus, und geben Sie dann **mmc.exe** ein. Wählen Sie in der leeren Konsole **Datei** und anschließend **Snap-In hinzufügen/entfernen** aus.  

3.  Wählen Sie im Dialogfeld **Snap-In hinzufügen/entfernen** aus der Liste **Verfügbare Snap-Ins** die Option **Zertifikate** aus, und wählen Sie dann **Hinzufügen** aus.  

4.  Wählen Sie im Dialogfeld **Zertifikat-Snap-In** die Option **Computerkonto** und dann **Weiter** aus.  

5.  Vergewissern Sie sich, dass im Dialogfeld **Computer auswählen** die Option **Lokaler Computer: (der Computer, auf dem diese Konsole ausgeführt wird)** ausgewählt ist. Wählen Sie anschließend **Fertig stellen** aus.  

6.  Wählen Sie im Dialogfeld **Snap-Ins hinzufügen/entfernen** **OK** aus.  

7.  Erweitern Sie in der Konsole **Zertifikate (Lokaler Computer)** , und wählen Sie dann **Persönlich** aus.  

8.  Klicken Sie mit der rechten Maustaste auf **Zertifikate**, wählen Sie **Alle Tasks** und dann **Neues Zertifikat anfordern** aus.  

9. Wählen Sie auf der Seite **Vorbereitung** die Option **Weiter** aus.  

10. Wenn die Seite **Zertifikatregistrierungsrichtlinie auswählen** angezeigt wird, wählen Sie **Weiter** aus.  

11. Wählen Sie auf der Seite **Zertifikate anfordern** in der Liste der verfügbaren Zertifikate das **ConfigMgr-Webserverzertifikat** aus, und wählen Sie anschließend Folgendes aus: **Es werden zusätzliche Informationen für diese Zertifikatregistrierung benötigt. Klicken Sie hier, um die Einstellungen zu konfigurieren**.  

12. Im Dialogfeld **Zertifikateigenschaften** auf der Registerkarte **Antragsteller** muss der **Antragstellername** unverändert bleiben. Dies bedeutet, dass das Feld **Wert** für den Abschnitt **Antragstellername** leer bleibt. Wählen Sie stattdessen im Abschnitt **Alternativer Name** die Dropdownliste **Typ** aus, und wählen Sie dann **DNS** aus.  

13. Geben Sie im Feld **Wert** die FQDN-Werte an, die Sie in den Standortsystemeigenschaften von Configuration Manager angeben werden, und wählen Sie dann **OK** aus, um das Dialogfeld **Zertifikateigenschaften** zu schließen.  

     Beispiele:  

    - Wenn vom Standortsystem nur Clientverbindungen aus dem Intranet akzeptiert werden und der Intranet-FQDN des Standortsystemservers **server1.internal.contoso.com** lautet: Geben Sie **server1.internal.contoso.com** ein, und wählen Sie dann **Hinzufügen** aus.  

    - Wenn vom Standortsystem Clientverbindungen aus dem Intranet und Internet akzeptiert werden, der Intranet-FQDN des Standortsystemservers **server1.internal.contoso.com** und der Internet-FQDN des Standortsystemservers **server.contoso.com** lauten:  

        1.  Geben Sie **server1.internal.contoso.com** ein, und wählen Sie dann **Hinzufügen** aus.  

        2.  Geben Sie **server.contoso.com** ein, und wählen Sie dann **Hinzufügen** aus.  

        > [!NOTE]  
        >  Sie können die FQDNs für Configuration Manager in jeder beliebigen Reihenfolge angeben. Vergewissern Sie sich jedoch, dass von allen Geräten, von denen das Zertifikat verwendet wird (beispielsweise mobile Geräte und Proxywebserver), ein alternativer Antragstellername (SAN) für das Zertifikat sowie mehrere Werte für den SAN verwendet werden können. Wenn die Unterstützung der Geräte von SAN-Werten in den Zertifikaten begrenzt ist, müssen Sie möglicherweise die Reihenfolge der FQDNs ändern oder stattdessen den Antragsteller-Wert verwenden.  

14. Wählen Sie auf der Seite **Zertifikate anfordern** in der Liste der angezeigten Zertifikate die Vorlage **ConfigMgr-Webserverzertifikat** aus, und wählen Sie dann **Registrieren** aus.  

15. Warten Sie, bis auf der Seite mit den **Ergebnissen der Zertifikatinstallation** angezeigt wird, dass das Zertifikat installiert wurde. Wählen Sie dann **Fertig stellen** aus.  

16. Schließen Sie das Dialogfeld **Zertifikate (Lokaler Computer)** .  

###  <a name="configure-iis-to-use-the-web-server-certificate"></a><a name="BKMK_webserver42008"></a> Konfigurieren von IIS für die Verwendung des Webserverzertifikats  
 Durch diese Prozedur wird das installierte Zertifikat an die IIS- **Standardwebsite**gebunden.  

##### <a name="to-set-up-iis-to-use-the-web-server-certificate"></a>So richten Sie IIS für die Verwendung des Webserverzertifikats ein  

1. Wählen Sie auf dem Mitgliedsserver mit IIS **Start**, **Programme**, **Verwaltung** und dann **Internetinformationsdienste-Manager** aus.  

2. Erweitern Sie **Sites**, klicken Sie mit der rechten Maustaste auf **Standardwebsite**, und wählen Sie dann **Bindungen bearbeiten** aus.  

3. Klicken Sie auf den Eintrag **HTTPS** und dann auf **Bearbeiten**.  

4. Wählen Sie im Dialogfeld **Websitebindung bearbeiten** das Zertifikat aus, das Sie mithilfe der Vorlage „ConfigMgr-Webserverzertifikat“ angefordert haben, und wählen Sie dann **OK** aus.  

   > [!NOTE]  
   >  Wenn Sie sich nicht sicher sind, welches das richtige Zertifikat ist, wählen Sie ein Zertifikat und dann **Ansicht** aus. Dadurch können Sie die ausgewählten Zertifikatdetails mit den Zertifikaten im Zertifikat-Snap-in vergleichen. Beispielsweise wird mit dem Zertifikat-Snap-In die Zertifikatvorlage angezeigt, die für die Zertifikatanforderung verwendet wurde. Anschließend können Sie den Fingerabdruck des Zertifikats, das mit der Vorlage „ConfigMgr-Webserverzertifikat“ angefordert wurde, mit dem Fingerabdruck des Zertifikats vergleichen, das aktuell im Dialogfeld **Websitebindung bearbeiten** ausgewählt ist.  

5. Wählen Sie im Dialogfeld **Websitebindung bearbeiten** **OK** und dann **Schließen** aus.  

6. Schließen Sie das Dialogfeld **Internetinformationsdienste-Manager**.  

   Der Mitgliedsserver ist nun mit einem Webserverzertifikat für Configuration Manager eingerichtet.  

> [!IMPORTANT]  
>  Wenn Sie den Configuration Manager-Standortsystemserver auf diesem Computer installieren, vergewissern Sie sich, dass Sie in den Standortsystemeigenschaften die gleichen FQDNs angeben wie bei der Anforderung des Zertifikats.  

##  <a name="deploy-the-service-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddp2008_cm2012"></a> Bereitstellen des Dienstzertifikats für cloudbasierte Verteilungspunkte  

Diese Zertifikatbereitstellung besteht aus den folgenden Prozeduren:  

- [Erstellen und Ausstellen der benutzerdefinierten Webserver-Zertifikatvorlage bei der Zertifizierungsstelle](#BKMK_clouddpcreating2008)  

- [Anfordern des benutzerdefinierten Webserverzertifikats](#BKMK_clouddprequesting2008)  

- [Exportieren des benutzerdefinierten Webserverzertifikats für cloudbasierte Verteilungspunkte](#BKMK_clouddpexporting2008)  

###  <a name="create-and-issue-a-custom-web-server-certificate-template-on-the-certification-authority"></a><a name="BKMK_clouddpcreating2008"></a> Erstellen und Ausstellen der benutzerdefinierten Webserver-Zertifikatvorlage bei der Zertifizierungsstelle  
 Mit dieser Prozedur wird eine benutzerdefinierte Zertifikatvorlage erstellt, die auf der Zertifikatvorlage für Webserver basiert. Das Zertifikat gilt für cloudbasierte Verteilungspunkte in Configuration Manager, und der private Schlüssel muss exportierbar sein. Nachdem die Vorlage erstellt wurde, wird sie zur Zertifizierungsstelle hinzugefügt.  

> [!NOTE]
>  In dieser Prozedur wird eine andere Zertifikatvorlage als die Zertifikatvorlage für Webserver verwendet, die Sie für IIS ausführende Standortsysteme erstellt haben. Obwohl beide Zertifikate eine Serverauthentifizierungsfunktion erfordern, erfordert das Zertifikat für cloudbasierte Verteilungspunkte, dass Sie einen benutzerdefinierten Wert als Antragstellernamen eingeben. Des Weiteren muss der private Schlüssel exportiert werden. Aus Sicherheitsgründen wird empfohlen, Zertifikatvorlagen nur dann so einzurichten, dass der private Schlüssel exportiert werden kann, wenn dies erforderlich ist. Diese Konfiguration ist für den cloudbasierten Verteilungspunkt erforderlich, da Sie das Zertifikat als Datei importieren müssen, anstatt es aus dem Zertifikatspeicher auszuwählen.  
> 
>  Wenn Sie für dieses Zertifikat eine neue Zertifikatvorlage erstellen, können Sie beschränken, von welchen Computern Zertifikate, deren privater Schlüssel exportiert werden kann, angefordert werden können. In einem Produktionsnetzwerk sollten Sie außerdem die folgenden Änderungen für dieses Zertifikat erwägen:  
> 
> - Verlangen Sie eine Genehmigung zum Installieren des Zertifikats, um die Sicherheit zu erhöhen.  
>   - Verlängern Sie die Gültigkeitsdauer des Zertifikats. Da Sie das Zertifikat jedes Mal vor Ablauf exportieren und importieren müssen, müssen Sie diese Prozedur seltener wiederholen, wenn Sie die Gültigkeitsdauer verlängern. Wenn Sie jedoch die Gültigkeitsdauer verlängern, reduzieren Sie damit auch die Sicherheit des Zertifikats, da Angreifern mehr Zeit zum Entschlüsseln des privaten Schlüssels und zum Stehlen des Zertifikats zur Verfügung steht.  
>   - Verwenden Sie im Zertifikat Alternativer Antragstellername einen benutzerdefinierten Wert, um dieses Zertifikat unter den standardmäßigen Webserverzertifikaten zu identifizieren, die Sie mit IIS verwenden.  

##### <a name="to-create-and-issue-the-custom-web-server-certificate-template-on-the-certification-authority"></a>So können Sie die benutzerdefinierte Zertifikatvorlage für Webserver bei der Zertifizierungsstelle erstellen und ausstellen  

1.  Erstellen Sie eine Sicherheitsgruppe mit der Bezeichnung **ConfigMgr-Standortserver**, in der die Mitgliedsserver für die Installation der primären Standortserver von Configuration Manager enthalten sind, von denen die cloudbasierten Verteilungspunkte verwaltet werden.  

2.  Klicken Sie auf dem Mitgliedsserver, auf dem die Zertifizierungsstellenkonsole ausgeführt wird, mit der rechten Maustaste auf **Zertifikatvorlagen**, und wählen Sie dann **Verwalten** aus, um die Verwaltungskonsole für Zertifikatvorlagen zu laden.  

3.  Klicken Sie im Ergebnisbereich mit der rechten Maustaste auf den Eintrag, für den in der Spalte **Vorlagenanzeigename** der Name **Webserver** angezeigt wird, und wählen Sie dann **Doppelte Vorlage** aus.  

4.  Vergewissern Sie sich, dass im Dialogfeld **Doppelte Vorlage** die Option **Windows 2003 Server Enterprise Edition** ausgewählt ist, und wählen Sie dann **OK** aus.  

    > [!IMPORTANT]  
    >  Wählen Sie nicht **Windows 2008 Server Enterprise Edition**aus.  

5.  Geben Sie im Dialogfeld **Eigenschaften der neuen Vorlage** auf der Registerkarte **Allgemein** einen Vorlagennamen ein, z.B. **ConfigMgr – cloudbasiertes Verteilungspunktzertifikat**, um das Webserverzertifikat für cloudbasierte Verteilungspunkte zu erstellen.  

6.  Wählen Sie die Registerkarte **Anforderungsverarbeitung** aus, und wählen Sie **Exportieren von privatem Schlüssel zulassen** aus.  

7.  Wählen Sie die Registerkarte **Sicherheit** aus, und entfernen Sie aus der Sicherheitsgruppe **Organisations-Admins** die Berechtigung **Registrieren**.  

8.  Wählen Sie **Hinzufügen** aus, geben Sie in das Textfeld **ConfigMgr – Standortserver** ein, und wählen Sie dann **OK** aus.  

9. Wählen Sie für diese Gruppe die Berechtigung **Anmelden** aus, und lassen Sie die Berechtigung **Lesen** aktiviert.  

10. Klicken Sie auf die Registerkarte **Kryptografie**, und stellen Sie sicher, dass **Minimale Schlüsselgröße** auf **2048** festgelegt wurde.

11. Wählen Sie **OK** aus, und schließen Sie die **Zertifikatvorlagenkonsole**.  

12. Klicken Sie in der Zertifizierungsstellenkonsole mit der rechten Maustaste auf **Zertifikatvorlagen**, wählen Sie **Neu** und dann **Auszustellende Zertifikatvorlage** aus.  

13. Wählen Sie im Dialogfeld **Zertifikatvorlagen aktivieren** die neu erstellte Vorlage **ConfigMgr – cloudbasiertes Verteilungspunktzertifikat** aus, und wählen Sie dann **OK** aus.  

14. Wenn Sie mit dem Erstellen und Ausstellen von Zertifikaten fertig sind, schließen Sie die Konsole **Zertifizierungsstelle**.  

###  <a name="request-the-custom-web-server-certificate"></a><a name="BKMK_clouddprequesting2008"></a> Anfordern des benutzerdefinierten Webserverzertifikats  
 Mit dieser Prozedur können Sie das benutzerdefinierte Webserverzertifikat anfordern und auf dem Mitgliedsserver installieren, auf dem der Standortserver ausgeführt wird.  

##### <a name="to-request-the-custom-web-server-certificate"></a>So fordern Sie das benutzerdefinierte Webserverzertifikat an  

1.  Führen Sie einen Neustart des Mitgliedsservers aus, nachdem Sie die Sicherheitsgruppe **ConfigMgr – Standortserver** erstellt und konfiguriert haben, um sicherzustellen, dass der Computer auf die von Ihnen erstellte Zertifikatvorlage zugreifen kann; verwenden Sie die von Ihnen konfigurierten Berechtigungen **Lesen** und **Registrieren**.  

2.  Wählen Sie **Start** und anschließend **Ausführen** aus, und geben Sie dann **mmc.exe** ein. Wählen Sie in der leeren Konsole **Datei** und anschließend **Snap-In hinzufügen/entfernen** aus.  

3.  Wählen Sie im Dialogfeld **Snap-In hinzufügen/entfernen** aus der Liste **Verfügbare Snap-Ins** die Option **Zertifikate** aus, und wählen Sie dann **Hinzufügen** aus.  

4.  Wählen Sie im Dialogfeld **Zertifikat-Snap-In** die Option **Computerkonto** und dann **Weiter** aus.  

5.  Vergewissern Sie sich, dass im Dialogfeld **Computer auswählen** die Option **Lokaler Computer: (der Computer, auf dem diese Konsole ausgeführt wird)** ausgewählt ist. Wählen Sie anschließend **Fertig stellen** aus.  

6.  Wählen Sie im Dialogfeld **Snap-Ins hinzufügen/entfernen** **OK** aus.  

7.  Erweitern Sie in der Konsole **Zertifikate (Lokaler Computer)** , und wählen Sie dann **Persönlich** aus.  

8.  Klicken Sie mit der rechten Maustaste auf **Zertifikate**, wählen Sie **Alle Tasks** und dann **Neues Zertifikat anfordern** aus.  

9. Wählen Sie auf der Seite **Vorbereitung** die Option **Weiter** aus.  

10. Wenn die Seite **Zertifikatregistrierungsrichtlinie auswählen** angezeigt wird, wählen Sie **Weiter** aus.  

11. Wählen Sie auf der Seite **Zertifikate anfordern** in der Liste der verfügbaren Zertifikate das **ConfigMgr – cloudbasiertes Verteilungspunktzertifikat** aus, und wählen Sie dann **Es werden zusätzliche Informationen für diese Zertifikatregistrierung benötigt. Klicken Sie hier, um die Einstellungen zu konfigurieren.** aus.  

12. Wählen Sie im Dialogfenster **Zertifikateigenschaften** auf der Registerkarte **Antragsteller** für **Antragstellername** als **Typ** die Option **Allgemeiner Name** aus.  

13. Geben Sie im Feld **Wert** Ihre Auswahl für den Dienstnamen sowie Ihren Domänennamen ein, indem Sie das Format FQDN verwenden. Beispiel: **clouddp1.contoso.com**.  

    > [!NOTE]  
    >  Stellen Sie sicher, dass der Dienstname in Ihrem Namespace einmalig ist. Mit DNS legen Sie einen Alias (CNAME-Datensatz) an, um diesen Dienstnamen zu einer automatisch generierten ID (GUID) und einer IP-Adresse von Windows Azure zuzuordnen.  

14. Wählen Sie **Hinzufügen** und dann **OK** aus, um das Dialogfenster **Zertifikateigenschaften** zu schließen.  

15. Wählen Sie auf der Seite **Zertifikate anfordern** in der Liste der verfügbaren Zertifikate das **ConfigMgr – cloudbasierte Verteilungspunktzertifikat** aus, und wählen Sie dann **Registrieren** aus.  

16. Warten Sie, bis auf der Seite mit den **Ergebnissen der Zertifikatinstallation** angezeigt wird, dass das Zertifikat installiert wurde. Wählen Sie dann **Fertig stellen** aus.  

17. Schließen Sie das Dialogfeld **Zertifikate (Lokaler Computer)** .  

###  <a name="export-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a><a name="BKMK_clouddpexporting2008"></a> Exportieren des benutzerdefinierten Webserverzertifikats für cloudbasierte Verteilungspunkte  
 Mithilfe dieser Prozedur können Sie das benutzerdefinierte Webserverzertifikat in eine Datei exportieren, damit sie beim Erstellen eines cloudbasierten Verteilungspunktes importiert werden kann.  

##### <a name="to-export-the-custom-web-server-certificate-for-cloud-based-distribution-points"></a>So exportieren Sie das benutzerdefinierten Webserverzertifikat für cloudbasierte Verteilungspunkte  

1. Klicken Sie in der Konsole **Zertifikate (Lokaler Computer)** mit der rechten Maustaste auf das soeben installierte Zertifikat, und wählen Sie **Alle Tasks** und dann **Exportieren** aus.  

2. Wählen Sie im Assistenten zum Exportieren von Zertifikaten **Weiter** aus.  

3. Wählen Sie auf der Seite **Privaten Schlüssel exportieren** die Option **Ja, privaten Schlüssel exportieren** aus, und wählen Sie dann **Weiter** aus.  

   > [!NOTE]  
   >  Ist diese Option nicht verfügbar, wurde das Zertifikat ohne Option zum Exportieren des privaten Schlüssels erstellt. In diesem Szenario können Sie das Zertifikat nicht im erforderlichen Format exportieren. Sie müssen die Zertifikatvorlage so einrichten, dass der private Schlüssel exportiert werden kann, und dann das Zertifikat erneut anfordern.  

4. Auf der Seite **Format der zu exportierenden Datei** muss die Option **Privater Informationsaustausch - PKCS #12 (.PFX)** ausgewählt sein.  

5. Geben Sie auf der Seite **Kennwort** ein sicheres Kennwort zum Schutz des exportierten Zertifikats mit seinem privaten Schlüssel an, und wählen Sie dann **Weiter** aus.  

6. Geben Sie auf der Seite **Zu exportierende Datei** den Namen der Datei an, die exportiert werden soll, und wählen Sie **Weiter** aus.  

7. Wählen Sie **Fertig stellen** aus, um den **Assistenten zum Exportieren von Zertifikaten** zu schließen, und wählen Sie dann im Bestätigungsdialogfeld **OK** aus.  

8. Schließen Sie das Dialogfeld **Zertifikate (Lokaler Computer)** .  

9. Speichern Sie die Datei an einem sicheren Ort, und gewährleisten Sie, dass Sie von der Configuration Manager-Konsole darauf zugreifen können.  

   Das Zertifikat kann nun importiert werden, wenn Sie einen cloudbasierten Verteilungspunkt erstellen.  

##  <a name="deploy-the-client-certificate-for-windows-computers"></a><a name="BKMK_client2008_cm2012"></a> Bereitstellen des Clientzertifikats für Windows-Computer  
 Diese Zertifikatbereitstellung besteht aus den folgenden Prozeduren:  

- Erstellen und Ausstellen der Zertifikatvorlage zur Arbeitsstationsauthentifizierung bei der Zertifizierungsstelle  

- Konfigurieren der automatischen Registrierung der Vorlage zur Arbeitsstationsauthentifizierung mithilfe einer Gruppenrichtlinie  

- Automatisches Registrieren des Zertifikats zur Arbeitsstationsauthentifizierung und Überprüfen der Installation auf Computern  

###  <a name="create-and-issue-the-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_client02008"></a> Erstellen und Ausstellen der Zertifikatvorlage zur Arbeitsstationsauthentifizierung bei der Zertifizierungsstelle  
 Dieses Verfahren erstellt eine Zertifikatvorlage für Configuration Manager-Clientcomputer und fügt sie der Zertifizierungsstelle hinzu.  

##### <a name="to-create-and-issue-the-workstation-authentication-certificate-template-on-the-certification-authority"></a>So können Sie die Zertifikatvorlage zur Arbeitsstationsauthentifizierung bei der Zertifizierungsstelle generieren und ausstellen  

1.  Klicken Sie auf dem Mitgliedsserver, auf dem die Zertifizierungsstellenkonsole ausgeführt wird, mit der rechten Maustaste auf **Zertifikatvorlagen**, und wählen Sie dann **Verwalten** aus, um die Verwaltungskonsole für Zertifikatvorlagen zu laden.  

2.  Klicken Sie im Ergebnisbereich mit der rechten Maustaste auf den Eintrag, für den in der Spalte **Vorlagenanzeigename** der Name **Arbeitsstationsauthentifizierung** angezeigt wird, und wählen Sie **Doppelte Vorlage** aus.  

3.  Vergewissern Sie sich, dass im Dialogfeld **Doppelte Vorlage** die Option **Windows 2003 Server Enterprise Edition** ausgewählt ist, und wählen Sie dann **OK** aus.  

    > [!IMPORTANT]  
    >  Wählen Sie nicht **Windows 2008 Server Enterprise Edition**aus.  

4.  Geben Sie im Dialogfeld **Eigenschaften der neuen Vorlage** auf der Registerkarte **Allgemein** einen Vorlagennamen ein, z.B. **ConfigMgr-Clientzertifikat**, um die Clientzertifikate zu generieren, die auf Configuration Manager-Clientcomputern verwendet werden.  

5.  Wählen Sie die Registerkarte **Sicherheit** und dann die Gruppe **Domänencomputer** aus. Wählen Sie anschließend die zusätzlichen Berechtigungen **Lesen** und **Automatisch registrieren** aus. Lassen Sie **Anmelden**aktiviert.  

6.  Wählen Sie **OK** aus, und schließen Sie die **Zertifikatvorlagenkonsole**.  

7.  Klicken Sie in der Zertifizierungsstellenkonsole mit der rechten Maustaste auf **Zertifikatvorlagen**, wählen Sie **Neu** und dann **Auszustellende Zertifikatvorlage** aus.  

8.  Wählen Sie im Dialogfeld **Zertifikatvorlagen aktivieren** die neu erstellte Vorlage **ConfigMgr-Clientzertifikat** aus, und wählen Sie dann **OK** aus.  

9. Wenn Sie mit dem Erstellen und Ausstellen von Zertifikaten fertig sind, schließen Sie die Konsole **Zertifizierungsstelle**.  

###  <a name="configure-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a><a name="BKMK_client12008"></a> Konfigurieren der automatischen Registrierung der Vorlage zur Arbeitsstationsauthentifizierung mithilfe einer Gruppenrichtlinie  
 Mit dieser Prozedur richten Sie die Gruppenrichtlinie zum automatischen Registrieren des Clientzertifikats auf Computern ein.  

##### <a name="to-set-up-autoenrollment-of-the-workstation-authentication-template-by-using-group-policy"></a>So richten Sie die automatische Registrierung der Vorlage zur Arbeitsstationsauthentifizierung mithilfe einer Gruppenrichtlinie ein  

1.  Wählen Sie auf dem Domänencontroller **Start**, **Verwaltung** und dann **Gruppenrichtlinienverwaltung** aus.  

2.  Wechseln Sie zu Ihrer Domäne. Klicken Sie mit der rechten Maustaste auf die Domäne, und wählen Sie dann **Gruppenrichtlinienobjekt hier erstellen und verknüpfen** aus.  

    > [!NOTE]  
    >  Für diesen Schritt hat es sich bewährt, eine neue Gruppenrichtlinie für benutzerdefinierte Einstellungen zu erstellen, statt die mit den Active Directory-Domänendiensten installierte Standarddomänenrichtlinie zu bearbeiten. Wenn Sie diese Gruppenrichtlinie auf Domänenebene zuweisen, wird sie auf alle Computer in der Domäne angewendet. In einer Produktionsumgebung können Sie die automatische Registrierung jedoch auf ausgewählte Computer einschränken. Sie können die Gruppenrichtlinie auf einer Organisationseinheitsebene zuweisen oder die Gruppenrichtlinie auf Domänenebene mit einer Sicherheitsgruppe filtern, sodass sie nur für die Computer in der Gruppe gilt. Wenn Sie die automatische Registrierung einschränken, müssen Sie unbedingt den als Verwaltungspunkt eingerichteten Server einschließen.  

3.  Geben Sie im Dialogfeld **Neues Gruppenrichtlinienobjekt** einen Namen für die neue Gruppenrichtlinie ein, z.B. **Zertifikate automatisch registrieren**, und wählen Sie dann **OK** aus.  

4.  Klicken Sie im Ergebnisbereich auf der Registerkarte **Verknüpfte Gruppenrichtlinienobjekte** mit der rechten Maustaste auf die neue Gruppenrichtlinie, und wählen Sie dann **Bearbeiten** aus.  

5.  Erweitern Sie im **Gruppenrichtlinienverwaltungs-Editor** unter **Computerkonfiguration** den Knoten **Richtlinien**, und wechseln Sie dann zu **Windows-Einstellungen** / **Sicherheitseinstellungen** / **Richtlinien für öffentliche Schlüssel**.  

6.  Klicken Sie mit der rechten Maustaste auf den Objekttyp mit dem Namen **Zertifikatdiensteclient – Automatische Registrierung**, und wählen Sie anschließend **Eigenschaften** aus.  

7.  Wählen Sie in der Dropdown-Liste **Konfigurationsmodell** **Aktiviert** aus, wählen Sie **Abgelaufene Zertifikate erneuern, ausstehende Zertifikate aktualisieren und gesperrte Zertifikate entfernen** aus, wählen Sie **Zertifikate aktualisieren, die Zertifikatvorlagen verwenden** aus, und wählen Sie dann **OK** aus.  

8.  Schließen Sie die **Gruppenrichtlinienverwaltung**.  

###  <a name="automatically-enroll-the-workstation-authentication-certificate-and-verify-its-installation-on-computers"></a><a name="BKMK_client22008"></a> Automatisches Registrieren des Zertifikats zur Arbeitsstationsauthentifizierung und Überprüfen der Installation auf Computern  
 Mit dieser Prozedur wird das Clientzertifikat auf Computern installiert, und die Installation wird überprüft.  

##### <a name="to-automatically-enroll-the-workstation-authentication-certificate-and-verify-its-installation-on-the-client-computer"></a>So registrieren Sie das Zertifikat zur Arbeitsstationsauthentifizierung automatisch und überprüfen die Installation auf dem Clientcomputer  

1. Starten Sie die Arbeitsstation neu, und warten Sie einige Minuten, bevor Sie sich anmelden.  

   > [!NOTE]  
   >  Das Neustarten eines Computers ist die zuverlässigste Methode, eine erfolgreiche automatische Registrierung von Zertifikaten sicherzustellen.  

2. Melden Sie sich mit einem Konto an, das über Administratorrechte verfügt.  

3. Geben Sie in das Suchfeld **mmc.exe.** ein, und drücken Sie dann die **EINGABETASTE**.  

4. Wählen Sie in der leeren Verwaltungskonsole **Datei** und anschließend **Snap-In hinzufügen/entfernen** aus.  

5. Wählen Sie im Dialogfeld **Snap-In hinzufügen/entfernen** aus der Liste **Verfügbare Snap-Ins** die Option **Zertifikate** aus, und wählen Sie dann **Hinzufügen** aus.  

6. Wählen Sie im Dialogfeld **Zertifikat-Snap-In** die Option **Computerkonto** und dann **Weiter** aus.  

7. Vergewissern Sie sich, dass im Dialogfeld **Computer auswählen** die Option **Lokaler Computer: (der Computer, auf dem diese Konsole ausgeführt wird)** ausgewählt ist. Wählen Sie anschließend **Fertig stellen** aus.  

8. Wählen Sie im Dialogfeld **Snap-Ins hinzufügen/entfernen** **OK** aus.  

9. Erweitern Sie in der Konsole **Zertifikate (Lokaler Computer)** , erweitern Sie **Persönlich**, und wählen Sie dann **Zertifikate** aus.  

10. Überprüfen Sie, ob im Ergebnisbereich ein Zertifikat angezeigt wird, für das in der Spalte **Beabsichtigter Zweck** der Wert **Clientauthentifizierung** und in der Spalte **Zertifikatvorlage** der Wert **ConfigMgr-Clientzertifikat** angegeben ist.  

11. Schließen Sie das Dialogfeld **Zertifikate (Lokaler Computer)** .  

12. Wiederholen Sie die Schritte 1 bis 11 für den Mitgliedsserver, um sicherzustellen, dass der als Verwaltungspunkt eingerichtete Server ebenfalls über ein Clientzertifikat verfügt.  

    Der Computer ist nun mit einem Configuration Manager-Clientzertifikat eingerichtet.  

##  <a name="deploy-the-client-certificate-for-distribution-points"></a><a name="BKMK_clientdistributionpoint2008_cm2012"></a> Bereitstellen des Clientzertifikats für Verteilungspunkte  

> [!NOTE]  
>  Dieses Zertifikat kann auch für Medienabbilder verwendet werden, die keinen PXE-Start verwenden, da die gleichen Zertifikatanforderungen bestehen.  

 Diese Zertifikatbereitstellung besteht aus den folgenden Prozeduren:  

- Erstellen und Ausstellen einer benutzerdefinierten Zertifikatvorlage zur Arbeitsstationsauthentifizierung bei der Zertifizierungsstelle  

- Anfordern des benutzerdefinierten Zertifikats zur Arbeitsstationsauthentifizierung  

- Exportieren des Clientzertifikats für Verteilungspunkte  

###  <a name="create-and-issue-a-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a><a name="BKMK_clientdistributionpoint02008"></a> Erstellen und Ausstellen einer benutzerdefinierten Zertifikatvorlage zur Arbeitsstationsauthentifizierung bei der Zertifizierungsstelle  
 Mit diesem Verfahren wird eine benutzerdefinierte Zertifikatvorlage für Configuration Manager-Verteilungspunkte erstellt, sodass der private Schlüssel exportiert werden kann, und die Zertifikatvorlage der Zertifizierungsstelle hinzugefügt.  

> [!NOTE]
>  In dieser Prozedur wird eine andere Zertifikatvorlage als die Zertifikatvorlage für Webserver verwendet, die Sie für IIS ausführende Standortsysteme erstellt haben. Obwohl für beide Zertifikate Clientauthentifizierungsfunktionen erforderlich sind, ist für das Verteilungspunktzertifikat erforderlich, dass der private Schlüssel exportiert wird. Aus Sicherheitsgründen wird empfohlen, Zertifikatvorlagen nur dann so einzurichten, dass der private Schlüssel exportiert werden kann, wenn dies erforderlich ist. Diese Konfiguration ist für den Verteilungspunkt erforderlich, da Sie das Zertifikat als Datei importieren müssen, anstatt es aus dem Zertifikatspeicher auszuwählen.  
> 
>  Wenn Sie für dieses Zertifikat eine neue Zertifikatvorlage erstellen, können Sie beschränken, von welchen Computern Zertifikate, deren privater Schlüssel exportiert werden kann, angefordert werden können. In unserer Beispielbereitstellung ist dies die Sicherheitsgruppe, die Sie zuvor für Configuration Manager-Standortsysteme, auf denen IIS ausgeführt werden, erstellt haben. Erwägen Sie in einem Produktionsnetzwerk, von dem die IIS-Standortsystemrollen verteilt werden, die Erstellung einer neuen Sicherheitsgruppe für die Server, auf denen Verteilungspunkte ausgeführt werden, sodass Sie das Zertifikat nur auf diese Standortsystemserver beschränken können. Außerdem sollten Sie die folgenden Änderungen für dieses Zertifikat erwägen:  
> 
> - Verlangen Sie eine Genehmigung zum Installieren des Zertifikats, um die Sicherheit zu erhöhen.  
>   - Verlängern Sie die Gültigkeitsdauer des Zertifikats. Da Sie das Zertifikat jedes Mal vor Ablauf exportieren und importieren müssen, müssen Sie diese Prozedur seltener wiederholen, wenn Sie die Gültigkeitsdauer verlängern. Wenn Sie jedoch die Gültigkeitsdauer verlängern, reduzieren Sie damit auch die Sicherheit des Zertifikats, da Angreifern mehr Zeit zum Entschlüsseln des privaten Schlüssels und zum Stehlen des Zertifikats zur Verfügung steht.  
>   - Verwenden Sie für das Zertifikat einen benutzerdefinierten Wert im Feld Antragsteller oder als alternativen Antragstellernamen (SAN), um die Unterscheidung dieses Zertifikats von den Standardclientzertifikaten zu vereinfachen. Dies ist vor allem dann nützlich, wenn Sie das gleiche Zertifikat für mehrere Verteilungspunkte verwenden möchten.  

##### <a name="to-create-and-issue-the-custom-workstation-authentication-certificate-template-on-the-certification-authority"></a>So können Sie die benutzerdefinierte Zertifikatvorlage zur Arbeitsstationsauthentifizierung bei der Zertifizierungsstelle generieren und ausstellen  

1.  Klicken Sie auf dem Mitgliedsserver, auf dem die Zertifizierungsstellenkonsole ausgeführt wird, mit der rechten Maustaste auf **Zertifikatvorlagen**, und wählen Sie dann **Verwalten** aus, um die Verwaltungskonsole für Zertifikatvorlagen zu laden.  

2.  Klicken Sie im Ergebnisbereich mit der rechten Maustaste auf den Eintrag, für den in der Spalte **Vorlagenanzeigename** der Name **Arbeitsstationsauthentifizierung** angezeigt wird, und wählen Sie **Doppelte Vorlage** aus.  

3.  Vergewissern Sie sich, dass im Dialogfeld **Doppelte Vorlage** die Option **Windows 2003 Server Enterprise Edition** ausgewählt ist, und wählen Sie dann **OK** aus.  

    > [!IMPORTANT]  
    >  Wählen Sie nicht **Windows 2008 Server Enterprise Edition**aus.  

4.  Geben Sie im Dialogfeld **Eigenschaften der neuen Vorlage** auf der Registerkarte **Allgemein** einen Namen ein, z.B. **ConfigMgr-Clientzertifikat für den Verteilungspunkt**, um das Clientauthentifizierungszertifikat für Verteilungspunkte zu generieren.  

5.  Wählen Sie die Registerkarte **Anforderungsverarbeitung** aus, und wählen Sie **Exportieren von privatem Schlüssel zulassen** aus.  

6.  Wählen Sie die Registerkarte **Sicherheit** aus, und entfernen Sie aus der Sicherheitsgruppe **Organisations-Admins** die Berechtigung **Registrieren**.  

7.  Wählen Sie **Hinzufügen** aus, geben Sie in das Textfeld **ConfigMgr-IIS-Server** ein, und wählen Sie dann **OK** aus.  

8.  Wählen Sie für diese Gruppe die Berechtigung **Anmelden** aus, und lassen Sie die Berechtigung **Lesen** aktiviert.  

9. Wählen Sie **OK** aus, und schließen Sie die **Zertifikatvorlagenkonsole**.  

10. Klicken Sie in der Zertifizierungsstellenkonsole mit der rechten Maustaste auf **Zertifikatvorlagen**, wählen Sie **Neu** und dann **Auszustellende Zertifikatvorlage** aus.  

11. Wählen Sie im Dialogfeld **Zertifikatvorlagen aktivieren** die neu erstellte Vorlage **ConfigMgr-Clientzertifikat für den Verteilungspunkt** aus, und wählen Sie dann **OK** aus.  

12. Wenn Sie mit dem Erstellen und Ausstellen von Zertifikaten fertig sind, schließen Sie die Konsole **Zertifizierungsstelle**.  

###  <a name="request-the-custom-workstation-authentication-certificate"></a><a name="BKMK_clientdistributionpoint12008"></a> Anfordern des benutzerdefinierten Zertifikats zur Arbeitsstationsauthentifizierung  
 Mit dieser Prozedur fordern Sie das benutzerdefinierte Clientzertifikat an und installieren es auf dem Mitgliedsserver, auf dem IIS ausgeführt werden und der als Verteilungspunkt eingerichtet werden soll.  

##### <a name="to-request-the-custom-workstation-authentication-certificate"></a>So fordern Sie das benutzerdefinierte Zertifikat zur Arbeitsstationsauthentifizierung an  

1.  Wählen Sie **Start** und anschließend **Ausführen** aus, und geben Sie dann **mmc.exe** ein. Wählen Sie in der leeren Konsole **Datei** und anschließend **Snap-In hinzufügen/entfernen** aus.  

2.  Wählen Sie im Dialogfeld **Snap-In hinzufügen/entfernen** aus der Liste **Verfügbare Snap-Ins** die Option **Zertifikate** aus, und wählen Sie dann **Hinzufügen** aus.  

3.  Wählen Sie im Dialogfeld **Zertifikat-Snap-In** die Option **Computerkonto** und dann **Weiter** aus.  

4.  Vergewissern Sie sich, dass im Dialogfeld **Computer auswählen** die Option **Lokaler Computer: (der Computer, auf dem diese Konsole ausgeführt wird)** ausgewählt ist. Wählen Sie anschließend **Fertig stellen** aus.  

5.  Wählen Sie im Dialogfeld **Snap-Ins hinzufügen/entfernen** **OK** aus.  

6.  Erweitern Sie in der Konsole **Zertifikate (Lokaler Computer)** , und wählen Sie dann **Persönlich** aus.  

7.  Klicken Sie mit der rechten Maustaste auf **Zertifikate**, wählen Sie **Alle Tasks** und dann **Neues Zertifikat anfordern** aus.  

8.  Wählen Sie auf der Seite **Vorbereitung** die Option **Weiter** aus.  

9. Wenn die Seite **Zertifikatregistrierungsrichtlinie auswählen** angezeigt wird, wählen Sie **Weiter** aus.  

10. Wählen Sie auf der Seite **Zertifikate anfordern** in der Liste der verfügbaren Zertifikate das **ConfigMgr-Clientzertifikat für den Verteilungspunkt** aus, und wählen Sie dann **Registrieren** aus.  

11. Warten Sie, bis auf der Seite mit den **Ergebnissen der Zertifikatinstallation** angezeigt wird, dass das Zertifikat installiert wurde. Wählen Sie dann **Fertig stellen** aus.  

12. Vergewissern Sie sich, dass im Ergebnisbereich ein Zertifikat angezeigt wird, für das in der Spalte **Beabsichtigter Zweck** der Wert **Clientauthentifizierung** und in der Spalte **Zertifikatvorlage** der Wert **ConfigMgr-Clientzertifikat für den Verteilungspunkt** angezeigt wird.  

13. Lassen Sie das Dialogfeld **Zertifikate (Lokaler Computer)** geöffnet.  

###  <a name="export-the-client-certificate-for-distribution-points"></a><a name="BKMK_exportclientdistributionpoint22008"></a> Exportieren des Clientzertifikats für Verteilungspunkte  
 Mithilfe dieser Prozedur können Sie das benutzerdefinierte Zertifikat zur Arbeitsstationsauthentifizierung in eine Datei exportieren, um diese in die Eigenschaften des Verteilungspunkts zu importieren.  

##### <a name="to-export-the-client-certificate-for-distribution-points"></a>So exportieren Sie das Clientzertifikat für Verteilungspunkte  

1. Klicken Sie in der Konsole **Zertifikate (Lokaler Computer)** mit der rechten Maustaste auf das soeben installierte Zertifikat, und wählen Sie **Alle Tasks** und dann **Exportieren** aus.  

2. Wählen Sie im Assistenten zum Exportieren von Zertifikaten **Weiter** aus.  

3. Wählen Sie auf der Seite **Privaten Schlüssel exportieren** die Option **Ja, privaten Schlüssel exportieren** aus, und wählen Sie dann **Weiter** aus.  

   > [!NOTE]  
   >  Ist diese Option nicht verfügbar, wurde das Zertifikat ohne Option zum Exportieren des privaten Schlüssels erstellt. In diesem Szenario können Sie das Zertifikat nicht im erforderlichen Format exportieren. Sie müssen die Konfiguration der Zertifikatvorlage einrichten, sodass der private Schlüssel exportiert werden kann, und dann das Zertifikat erneut anfordern.  

4. Auf der Seite **Format der zu exportierenden Datei** muss die Option **Privater Informationsaustausch - PKCS #12 (.PFX)** ausgewählt sein.  

5. Geben Sie auf der Seite **Kennwort** ein sicheres Kennwort zum Schutz des exportierten Zertifikats mit seinem privaten Schlüssel an, und wählen Sie dann **Weiter** aus.  

6. Geben Sie auf der Seite **Zu exportierende Datei** den Namen der Datei an, die exportiert werden soll, und wählen Sie **Weiter** aus.  

7. Wählen Sie **Fertig stellen** aus, um den **Assistenten zum Exportieren von Zertifikaten** zu schließen, und wählen Sie dann im Bestätigungsdialogfeld **OK** aus.  

8. Schließen Sie das Dialogfeld **Zertifikate (Lokaler Computer)** .  

9. Speichern Sie die Datei an einem sicheren Ort, und gewährleisten Sie, dass Sie von der Configuration Manager-Konsole darauf zugreifen können.  

   Das Zertifikat kann nun im Rahmen der Einrichtung des Verteilungspunkts importiert werden.  

> [!TIP]  
>  Dieselbe Zertifikatdatei können Sie verwenden, wenn Sie Medienabbilder für eine Betriebssystembereitstellung einrichten, bei der kein PXE-Start verwendet wird; die Tasksequenz zur Installation des Abbilds muss einen Verwaltungspunkt kontaktieren, der HTTPS-Clientverbindungen erfordert.  

##  <a name="deploy-the-enrollment-certificate-for-mobile-devices"></a><a name="BKMK_mobiledevices2008_cm2012"></a> Bereitstellen des Registrierungszertifikats für mobile Geräte  
 Diese Zertifikatbereitstellung besteht aus einer einzigen Prozedur zum Erstellen und Ausstellen der Anmeldungszertifikatvorlage bei der Zertifizierungsstelle.  

### <a name="create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>Erstellen und Ausstellen der Registrierungszertifikatvorlage bei der Zertifizierungsstelle  
 Dieses Verfahren erstellt eine Registrierungszertifikatvorlage für mobile Geräte für Configuration Manager und fügt sie der Zertifizierungsstelle hinzu.  

##### <a name="to-create-and-issue-the-enrollment-certificate-template-on-the-certification-authority"></a>So erstellen Sie die Anmeldungszertifikatvorlage und stellen sie bei der Zertifizierungsstelle aus  

1. Erstellen Sie eine Sicherheitsgruppe mit Benutzern, die mobile Geräte in Configuration Manager registrieren werden.  

2. Klicken Sie auf dem Mitgliedsserver, auf dem die Zertifikatdienste installiert sind, in der Zertifizierungsstellenkonsole mit der rechten Maustaste auf **Zertifikatvorlagen**, und wählen Sie dann **Verwalten** aus, um die Verwaltungskonsole für Zertifikatvorlagen zu laden.  

3. Klicken Sie im Ergebnisbereich mit der rechten Maustaste auf den Eintrag, für den in der Spalte **Vorlagenanzeigename** der Text **Authentifizierte Sitzung** angezeigt wird, und wählen Sie dann **Doppelte Vorlage** aus.  

4. Vergewissern Sie sich, dass im Dialogfeld **Doppelte Vorlage** die Option **Windows 2003 Server Enterprise Edition** ausgewählt ist, und wählen Sie dann **OK** aus.  

   > [!IMPORTANT]  
   >  Wählen Sie nicht **Windows 2008 Server Enterprise Edition**aus.  

5. Geben Sie im Dialogfeld **Eigenschaften der neuen Vorlage** auf der Registerkarte **Allgemein** einen Vorlagennamen ein, z. B. **ConfigMgr-Registrierungszertifikat für mobile Geräte**, um die Registrierungszertifikate für die mobilen Geräte zu generieren, die von Configuration Manager verwaltet werden sollen.  

6. Wählen Sie die Registerkarte **Antragsteller** aus, überprüfen Sie, ob **Aus diesen Informationen in Active Directory erstellen** ausgewählt ist, wählen Sie für **Format des Antragstellernamens** die Option **Allgemeiner Name** aus, und löschen Sie dann unter **Informationen im alternativen Antragstellernamen einbeziehen** den Eintrag **Benutzerprinzipalname (UPN)** .  

7. Wählen Sie die Registerkarte **Sicherheit** aus, wählen Sie die Sicherheitsgruppe mit Benutzern aus, die mobile Geräte registrieren müssen, und wählen Sie die zusätzliche Berechtigung **Registrieren** aus. Lassen Sie **Lesen**aktiviert.  

8. Wählen Sie **OK** aus, und schließen Sie die **Zertifikatvorlagenkonsole**.  

9. Klicken Sie in der Zertifizierungsstellenkonsole mit der rechten Maustaste auf **Zertifikatvorlagen**, wählen Sie **Neu** und dann **Auszustellende Zertifikatvorlage** aus.  

10. Wählen Sie im Dialogfeld **Zertifikatvorlagen aktivieren** die neu erstellte Vorlage **ConfigMgr-Registrierungszertifikat für mobile Geräte** und dann **OK** aus.  

11. Wenn Sie mit dem Erstellen und Ausstellen von Zertifikaten fertig sind, schließen Sie die Zertifizierungsstellenkonsole.  

    Sie können die Registrierungszertifikatvorlage für mobile Geräte jetzt in den Clienteinstellungen beim Einrichten eines Registrierungsprofils für mobile Geräte auswählen.  

##  <a name="deploy-the-client-certificate-for-mac-computers"></a><a name="BKMK_MacClient_SP1"></a> Bereitstellen des Clientzertifikats für Macintosh-Computer  

Diese Zertifikatbereitstellung besteht aus einer einzigen Prozedur zum Erstellen und Ausstellen der Anmeldungszertifikatvorlage bei der Zertifizierungsstelle.  

###  <a name="create-and-issue-a-mac-client-certificate-template-on-the-certification-authority"></a><a name="BKMK_MacClient_CreatingIssuing"></a> Erstellen und Ausstellen einer Clientzertifikatvorlage für Macintosh bei der Zertifizierungsstelle  
 Dieses Verfahren erstellt eine benutzerdefinierte Zertifikatvorlage für Macintosh-Computer für Configuration Manager und fügt das Zertifikat der Zertifizierungsstelle hinzu.  

> [!NOTE]  
>  In dieser Prozedur wird eine andere Zertifikatvorlage verwendet als die Zertifikatvorlage, die Sie möglicherweise für Windows-Clientcomputer oder für Verteilungspunkte erstellt haben.  
>   
>  Durch das Erstellen einer neuen Zertifikatvorlage für dieses Zertifikat können Sie die Zertifikatanforderung auf berechtigte Benutzer beschränken.  

##### <a name="to-create-and-issue-the-mac-client-certificate-template-on-the-certification-authority"></a>So erstellen Sie die Clientzertifikatvorlage für Macintosh bei der Zertifizierungsstelle  

1. Erstellen Sie eine Sicherheitsgruppe mit Benutzerkonten für Administratoren, die das Zertifikat auf dem Macintosh-Computer über Configuration Manager registrieren.  

2. Klicken Sie auf dem Mitgliedsserver, auf dem die Zertifizierungsstellenkonsole ausgeführt wird, mit der rechten Maustaste auf **Zertifikatvorlagen**, und wählen Sie dann **Verwalten** aus, um die Verwaltungskonsole für Zertifikatvorlagen zu laden.  

3. Klicken Sie im Ergebnisbereich mit der rechten Maustaste auf den Eintrag, für den in der Spalte **Vorlagenanzeigename** der Text **Authentifizierte Sitzung** angezeigt wird, und wählen Sie dann **Doppelte Vorlage** aus.  

4. Vergewissern Sie sich, dass im Dialogfeld **Doppelte Vorlage** die Option **Windows 2003 Server Enterprise Edition** ausgewählt ist, und wählen Sie dann **OK** aus.  

   > [!IMPORTANT]  
   >  Wählen Sie nicht **Windows 2008 Server Enterprise Edition**aus.  

5. Geben Sie im Dialogfeld **Eigenschaften der neuen Vorlage** auf der Registerkarte **Allgemein** einen Vorlagennamen ein, z.B. **ConfigMgr – Macintosh-Clientzertifikat**, um das Macintosh-Clientzertifikat zu generieren.  

6. Wählen Sie die Registerkarte **Antragsteller** aus, überprüfen Sie, ob **Aus diesen Informationen in Active Directory erstellen** ausgewählt ist, wählen Sie für **Format des Antragstellernamens** die Option **Allgemeiner Name** aus, und löschen Sie unter **Informationen im alternativen Antragstellernamen einbeziehen** den Eintrag **Benutzerprinzipalname (UPN)** .  

7. Wählen Sie die Registerkarte **Sicherheit** aus, und entfernen Sie aus den Sicherheitsgruppen **Domänen-Admins** und **Organisations-Admins** die Berechtigung **Registrieren**.  

8. Wählen Sie **Hinzufügen** aus, geben Sie die Sicherheitsgruppe an, die Sie im ersten Schritt erstellt haben, und wählen Sie dann **OK** aus.  

9. Wählen Sie für diese Gruppe die Berechtigung **Registrieren** aus, und lassen Sie die Berechtigung **Lesen** aktiviert.  

10. Wählen Sie **OK** aus, und schließen Sie die **Zertifikatvorlagenkonsole**.  

11. Klicken Sie in der Zertifizierungsstellenkonsole mit der rechten Maustaste auf **Zertifikatvorlagen**, wählen Sie **Neu** und dann **Auszustellende Zertifikatvorlage** aus.  

12. Wählen Sie im Dialogfeld **Zertifikatvorlagen aktivieren** die neu erstellte Vorlage **ConfigMgr – Macintosh-Clientzertifikat** aus, und wählen Sie dann **OK** aus.  

13. Wenn Sie mit dem Erstellen und Ausstellen von Zertifikaten fertig sind, schließen Sie die Konsole **Zertifizierungsstelle**.  

    Die Clientzertifikatvorlage für Macintosh kann jetzt ausgewählt werden, wenn Sie Clienteinstellungen für die Registrierung einrichten.
