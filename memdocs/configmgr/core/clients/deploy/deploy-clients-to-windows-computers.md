---
title: Bereitstellen von Clients unter Windows
titleSuffix: Configuration Manager
description: Erfahren Sie, wie der Configuration Manager-Client auf Windows-Computern bereitgestellt wird.
ms.date: 09/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 341f0d0b-f907-44cf-9e10-e1b41fc15f82
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2eea75f39430f1cc38ff994280425ca918eaa432
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694558"
---
# <a name="how-to-deploy-clients-to-windows-computers-in-configuration-manager"></a>Bereitstellen von Clients auf Windows-Computern in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Dieser Artikel beschreibt, wie der Konfigurations-Manager-Client auf Windows-Computern bereitgestellt wird. Weitere Informationen zu Planung und Vorbereitung der Clientbereitstellung finden Sie in den diesen Artikeln:

- [Clientinstallationsmethoden](plan/client-installation-methods.md)  
- [Voraussetzungen für die Bereitstellung von Clients auf Windows-Computern](prerequisites-for-deploying-clients-to-windows-computers.md)
- [Sicherheit und Datenschutz für Konfigurations-Manager-Clients](plan/security-and-privacy-for-clients.md)  
- [Bewährte Methoden für die Clientbereitstellung](plan/best-practices-for-client-deployment.md)  


## <a name="client-push-installation"></a><a name="BKMK_ClientPush"></a> Clientpushinstallation

Es gibt drei Hauptmethoden für die Verwendung von Clientpush:  

- Wenn Sie die Clientpushinstallation für einen Standort konfigurieren, wird die Installation automatisch auf den Computern ausgeführt, die an dem Standort vorhanden sind. Diese Methode gilt für die konfigurierten Grenzen des Standorts, wenn diese Grenzen als Begrenzungsgruppen festgelegt sind.  

- Starten Sie die Clientpushinstallation, indem Sie den Clientpushinstallations-Assistenten für eine bestimmte Sammlung oder für eine bestimmte Ressource innerhalb einer Sammlung ausführen.  

- Sie können den Clientpushinstallations-Assistenten verwenden, um den Configuration Manager-Client zum [Abfragen](../../servers/manage/introduction-to-queries.md) des Ergebnisses zu installieren. Die Installation ist nur dann erfolgreich, wenn eines der von der Abfrage zurückgegebenen Elemente das **ResourceID**-Attribut der **System Resource**-Klasse ist.

Wenn vom Standortserver kein Kontakt zum Clientcomputer hergestellt oder der Setupvorgang nicht gestartet werden kann, wird automatisch stündlich ein weiterer Installationsversuch gestartet. Der Server setzt die Installationsversuche bis zu sieben Tage lang fort.  

Installieren Sie einen Fallbackstatuspunkt, bevor Sie die Clients installieren, um den Clientinstallationsprozess besser nachverfolgen zu können. Wenn Sie einen Fallbackstatuspunkt installieren, wird er automatisch Clients zugewiesen, wenn diese mithilfe von Clientpushinstallation installiert werden. Verfolgen Sie den Clientinstallationsfortschritt anhand der Clientbereitstellungs- und -zuweisungsberichte nach.

Clientprotokolldateien bieten ausführlichere Informationen zur Problembehebung. Für die Protokolldateien ist kein Fallbackstatuspunkt erforderlich. In der Datei „CCM.log“ auf dem Standortserver werden beispielsweise alle Probleme aufgezeichnet, die auftreten, wenn der Standortserver eine Verbindung mit dem Computer herstellt. In der Datei „CCMSetup.log“ auf dem Client wird der Installationsprozess aufgezeichnet.  

> [!IMPORTANT]  
> Die Clientpushinstallation ist nur erfolgreich, wenn alle Voraussetzungen erfüllt sind. Weitere Informationen finden Sie unter [Installationsmethodenabhängigkeiten](prerequisites-for-deploying-clients-to-windows-computers.md#installation-method-dependencies).

### <a name="configure-the-site-to-automatically-use-client-push-for-discovered-computers"></a>Konfigurieren des Standorts für die automatische Verwendung von Clientpush für ermittelte Computer

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Standorte** aus.  

2. Wählen Sie den Standort aus, für den Sie die automatische standortweite Clientpushinstallation konfigurieren möchten.  

3. Klicken Sie auf der Registerkarte **Start** des Menübands in der Gruppe **Einstellungen** auf **Clientinstallationseinstellungen**, und wählen Sie dann **Clientpushinstallation** aus.  

4. Aktivieren Sie im Eigenschaftenfenster der Clientpushinstallation auf der Registerkarte **Allgemein** das Kontrollkästchen **Automatische standortweite Clientpushinstallation aktivieren**.

5. Wenn Sie den Standort aktualisieren, wird ab Version 1806 eine Kerberos-Überprüfung für Clientpush aktiviert. Die Option **Verbindungsfallback auf NTLM zulassen** ist standardmäßig aktiviert, was vorherigem Verhalten entspricht. Wenn der Standort den Client nicht mithilfe von Kerberos authentifizieren kann, wiederholt er den Verbindungsversuch mit NTLM. Zur Verbesserung der Sicherheit ist es empfehlenswert, diese Einstellung zu deaktivieren, bei der Kerberos ohne Fallback auf NTLM erforderlich ist.<!--1358204-->  

    > [!NOTE]  
    > Bei Verwendung von Clientpush zum Installieren des Konfigurations-Manager-Clients stellt der Standortserver eine Remoteverbindung mit dem Client her. Ab Version 1806 kann der Standort die gegenseitige Kerberos-Authentifizierung erfordern, indem vor dem Herstellen der Verbindung kein Fallback auf NTLM zugelassen wird. Diese Verbesserung sichert die Kommunikation zwischen dem Server und dem Client.  
    >
    > Je nach Ihren Sicherheitsrichtlinien kann Ihre Umgebung möglicherweise bereits Kerberos anstelle der älteren NTLM-Authentifizierung bevorzugen oder erfordern. Weitere Informationen zu den Sicherheitsaspekten dieser Authentifizierungsprotokolle finden Sie im Artikel zur [Windows-Sicherheitsrichtlinieneinstellung zum Beschränken von NTLM](/windows/security/threat-protection/security-policy-settings/network-security-restrict-ntlm-outgoing-ntlm-traffic-to-remote-servers#security-considerations).  
    >
    > Um dieses Feature verwenden zu können, müssen Clients sich in einer vertrauenswürdigen Active Directory-Gesamtstruktur befinden. Kerberos unter Windows hängt zur gegenseitigen Authentifizierung von Active Directory ab.  

6. Wählen Sie die Systemtypen aus, auf denen die Clientsoftware per Push installiert werden soll. Wählen Sie aus, ob der Client auf Domänencontrollern installiert werden soll.  

7. Geben Sie auf der Registerkarte **Konten** mindestens ein Konto an, das von Configuration Manager verwendet werden soll, wenn eine Verbindung mit dem Zielcomputer hergestellt wird. Klicken Sie auf das Symbol **Erstellen**, geben Sie den **Benutzernamen** und das **Kennwort** ein (maximal 38 Zeichen), bestätigen Sie das Kennwort, und klicken Sie dann auf **OK**. Geben Sie mindestens ein Clientpushinstallationskonto an. Für dieses Konto sind lokale Administratorrechte auf dem Zielcomputer erforderlich, auf dem der Client installiert werden soll. Wenn Sie kein Clientpushinstallationskonto angeben, versucht Configuration Manager, das Konto des Standortsystemcomputers zu verwenden. Bei Verwendung des Kontos des Standortsystemcomputers schlägt der domänenübergreifende Clientpush fehl.  

    > [!NOTE]  
    > Geben Sie das Konto am sekundären Standort an, das den Clientpush initiiert, um den Clientpush von einem sekundären Standort aus zu verwenden.  
    >
    > Weitere Informationen zum Clientpushinstallationskonto finden Sie im nächsten Abschnitt [Use the Client Push Installation Wizard (Verwenden des Clientpushinstallations-Assistenten)](#use-the-client-push-installation-wizard).  

8. Geben Sie erforderliche Installationseigenschaften auf der Registerkarte **Installationseigenschaften** an.

    Wenn Sie das Active Directory-Schema für Configuration Manager erweitert haben, veröffentlicht der Standort die angegebenen [Clientinstallationseigenschaften](about-client-installation-properties.md) in Active Directory Domain Services. Wenn „CCMSetup“ ohne Installationseigenschaften ausgeführt wird, werden diese Eigenschaften aus Active Directory gelesen.  

    > [!NOTE]  
    > Wenn Sie die Clientpushinstallation auf einem sekundären Standort aktivieren, legen Sie die Eigenschaft **SMSSITECODE** auf den Configuration Manager-Standortcode des übergeordneten primären Standorts fest. Wenn Sie das Active Directory-Schema für Configuration Manager erweitert haben, legen Sie diese Eigenschaft auf den Wert **AUTO** fest, um die korrekte Standortzuweisung automatisch suchen zu lassen.

### <a name="use-the-client-push-installation-wizard"></a>Verwenden des Clientpushinstallations-Assistenten

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Standorte** aus.  

2. Wählen Sie den Standort aus, für den Sie die automatische standortweite Clientpushinstallation konfigurieren möchten.  

3. Klicken Sie auf der Registerkarte **Start** des Menübands in der Gruppe **Einstellungen** auf **Clientinstallationseinstellungen**, und wählen Sie dann **Clientpushinstallation** aus.  

4. Geben Sie erforderliche Installationseigenschaften auf der Registerkarte **Installationseigenschaften** an.  

    Wenn Sie das Active Directory-Schema für Configuration Manager erweitert haben, veröffentlicht der Standort die angegebenen [Clientinstallationseigenschaften](about-client-installation-properties.md) in Active Directory Domain Services. Wenn „CCMSetup“ ohne Installationseigenschaften ausgeführt wird, werden diese Eigenschaften aus Active Directory gelesen.

5. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**.  

6. Wählen Sie auf dem Knoten **Geräte** einen oder mehrere Computer aus. Sie können auch eine Sammlung von Computern auf dem Knoten **Gerätesammlungen** auswählen.  

7. Wählen Sie auf der Registerkarte **Start** des Menübands eine der folgenden Optionen aus:  

    - Wählen Sie **Client installieren** in der Gruppe **Geräte** aus, um den Client mithilfe von Push auf ein oder mehrere Geräte zu übertragen.  

    - Wählen Sie **Client installieren** in der Gruppe **Sammlung** aus, um den Client mithilfe von Push in eine Sammlung von Geräten zu übertragen.  

8. Überprüfen Sie im Assistenten zum Installieren von Configuration Manager-Clients auf der Seite **Vorbereitung** die Informationen, und klicken Sie dann auf **Weiter**.  

9. Wählen Sie auf der Seite **Installationsoptionen** die gewünschten Optionen aus.  

10. Überprüfen Sie die Installationseinstellungen, und schließen Sie dann den Assistenten ab.  

> [!NOTE]  
> Verwenden Sie diesen Assistenten, um Clients zu installieren, auch wenn der Standort nicht für Clientpush konfiguriert ist.  

## <a name="software-update-based-installation"></a><a name="BKMK_ClientSUP"></a> Auf Softwareupdate basierende Installation  

Bei der auf Softwareupdate basierenden Clientinstallation wird der Client als Softwareupdate auf einem Softwareupdatepunkt veröffentlicht. Verwenden Sie diese Methode für Erstinstallationen oder Upgrades.  

Wenn der Configuration Manager-Client auf einem Computer installiert ist, empfängt der Computer die Clientrichtlinie vom Standort. Diese Richtlinie umfasst den Servernamen und Port des Softwareupdatepunkts, über den Softwareupdates abgerufen werden.

> [!IMPORTANT]  
> Verwenden Sie zum Installieren des Clients und für Softwareupdates den gleichen WSUS-Server (Windows Server Update Services), wenn Sie die auf Softwareupdate basierende Installation verwenden möchten. Dieser Server muss an einem primären Standort der aktive Softwareupdatepunkt sein. Weitere Informationen finden Sie unter [Install a software update point (Installieren eines Softwareupdatepunkts)](../../../sum/get-started/install-a-software-update-point.md).

Wenn der Configuration Manager-Client nicht auf einem Computer installiert ist, konfigurieren und weisen Sie ein Gruppenrichtlinienobjekt zu. Die Gruppenrichtlinie gibt den Servernamen des Softwareupdatepunkts an.  

Sie können keine Befehlszeileneigenschaften zu der auf Softwareupdates basierenden Clientinstallation hinzufügen. Wenn Sie das Active Directory-Schema für Configuration Manager erweitert haben, fragt die Clientinstallation automatisch Active Directory Domain Services nach den Installationseigenschaften ab.  

Wenn Sie das Active Directory-Schema nicht erweitert haben, verwenden Sie die Gruppenrichtlinie zum Bereitstellen von Einstellungen für die Clientinstallation. Diese Einstellungen werden bei allen auf Softwareupdate basierenden Clientinstallationen automatisch angewendet. Weitere Informationen finden Sie im Abschnitt [So stellen Sie Clientinstallationseigenschaften bereit](#BKMK_Provision) und dem Artikel [Zuweisen von Clients zu einem Standort](assign-clients-to-a-site.md).  

Verwenden Sie die folgende Prozedur, um Computer ohne Konfigurations-Manager-Client für die Verwendung eines Softwareupdatepunkts zu konfigurieren. Es gibt außerdem eine Prozedur, um die Clientsoftware auf dem Softwareupdatepunkt zu veröffentlichen.  

> [!TIP]  
> Wenn sich Computer im Anschluss an eine vorherige Softwareinstallation im Status „Neustart steht aus“ befinden, kann eine auf dem Softwareupdate basierende Clientinstallation zum Neustart des Computers führen.  

### <a name="configure-a-group-policy-object-to-specify-the-software-update-point"></a>Konfigurieren eines Gruppenrichtlinienobjekts zum Angeben des Softwareupdatepunkts  

1. Verwenden Sie die **Gruppenrichtlinien-Verwaltungskonsole**, um ein neues oder vorhandenes Gruppenrichtlinienobjekt zu öffnen.  

2. Erweitern Sie nacheinander **Computerkonfiguration**, **Administrative Vorlagen** und **Windows-Komponenten**, und klicken Sie dann auf **Windows Update**.  

3. Öffnen Sie die Eigenschaften der Einstellung **Internen Pfad für den Microsoft Updatedienst angeben**, und klicken Sie dann auf **Aktiviert**.  

4. **Set the intranet update service for detecting updates** (Interner Updatedienst zum Ermitteln von Updates festlegen): Geben Sie den Namen und den Port des Softwareupdatepunkt-Servers ein.  

    - Falls Sie das Configuration Manager-Standortsystem mit einem vollständig qualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) konfiguriert haben, verwenden Sie dieses Format.  

    - Wenn das Configuration Manager-Standortsystem nicht für ein FQDN-Format konfiguriert ist, verwenden Sie ein Kurznamenformat.

    > [!TIP]  
    > Weitere Informationen zur Bestimmung der Portnummer finden Sie unter [How to determine the port settings used by WSUS (Bestimmen der von WSUS verwendeten Porteinstellungen)](../../../sum/plan-design/plan-for-software-updates.md).

    Beispiel im FQDN-Format: `http://server1.contoso.com:8530`  

5. **Set the intranet statistics server** (Intranetserver für die Statistik festlegen): Diese Einstellung ist in der Regel mit demselben Servernamen konfiguriert.

6. Weisen Sie das Gruppenrichtlinienobjekt den Computern zu, auf denen Sie den Client installieren und Softwareupdates erhalten möchten.  

### <a name="publish-the-configuration-manager-client-to-the-software-update-point"></a>Veröffentlichen des Configuration Manager-Clients auf dem Softwareupdatepunkt  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Standorte** aus.  

2. Wählen Sie den Standort aus, für den Sie die auf Softwareupdate basierende Clientinstallation konfigurieren möchten.  

3. Klicken Sie auf der Registerkarte **Start** des Menübands in der Gruppe **Einstellungen** auf **Clientinstallationseinstellungen** und dann auf **Auf Softwareupdate basierende Clientinstallation**.  

4. Wählen Sie **Auf Softwareupdate basierende Clientinstallation aktivieren** aus.  

5. Wenn die Clientversion des Standorts aktueller ist als die Version des Softwareupdatepunkts, wird das Dialogfeld **Höhere Version des Clientpakets erkannt** angezeigt. Klicken Sie auf **Ja**, um die neueste Version zu veröffentlichen.  

    > [!NOTE]  
    > Wenn Sie die Clientsoftware noch nicht auf dem Softwareupdatepunkt veröffentlicht haben, ist dieses Dialogfeld leer.

Das Softwareupdate für den Configuration Manager-Client wird nicht automatisch aktualisiert, wenn eine neue Version vorhanden ist. Wiederholen Sie diese Prozedur beim Aktualisieren des Standorts, um den Client zu aktualisieren.  

## <a name="group-policy-installation"></a><a name="BKMK_ClientGP"></a> Gruppenrichtlinieninstallation

Verwenden Sie Gruppenrichtlinien in Active Directory Domain Services, um den Konfigurations-Manager-Client zu veröffentlichen oder zuzuweisen. Der Client wird installiert, wenn der Computer gestartet wird. Wenn Sie Gruppenrichtlinien verwenden, wird der Client in der Systemsteuerung in **Software** angezeigt. Der Benutzer kann ihn dort installieren.  

Verwenden Sie bei auf Gruppenrichtlinien basierenden Installationen das Windows Installer-Paket „CCMSetup.msi“. Sie finden diese Datei auf dem Standortserver im Ordner `<ConfigMgr installation directory>\bin\i386`. Sie können dieser Datei keine Eigenschaften hinzufügen, um das Installationsverhalten zu ändern.  

> [!IMPORTANT]  
> Sie müssen über Administratorberechtigungen verfügen, um auf die Clientinstallationsdateien zugreifen zu können.  

- Wenn Sie das Active Directory-Schema für Configuration Manager erweitert und im Dialogfeld **Standorteigenschaften** auf der Registerkarte **Veröffentlichen** die Domäne ausgewählt haben, durchsuchen Clientcomputer Active Directory Domain Services automatisch nach Installationseigenschaften. Weitere Informationen finden Sie unter [Informationen zu Clientinstallationseigenschaften, die in Active Directory Domain Services veröffentlicht wurden](about-client-installation-properties-published-to-active-directory-domain-services.md).  

- Wenn Sie das Active Directory-Schema nicht erweitert haben, finden Sie weitere Informationen zum Speichern von Installationseigenschaften in der Windows-Registrierung von Computern im Abschnitt zum [Bereitstellen von Clientinstallationseigenschaften](#BKMK_Provision). Der Client verwendet diese Installationseigenschaften bei der Installation.  

Weitere Informationen finden Sie unter [Remoteinstallation von Software in Windows Server 2008 und Windows Server 2003 mithilfe von Gruppenrichtlinien](https://support.microsoft.com/help/816102/how-to-use-group-policy-to-remotely-install-software-in-windows-server).  

## <a name="manual-installation"></a><a name="BKMK_Manual"></a> Manuelle Installation

Installieren Sie die Clientsoftware manuell auf Computern, indem Sie „CCMSetup.exe“ verwenden. Sie finden dieses Programm und die unterstützenden Dateien im Ordner „Client“ des Configuration Manager-Installationsordners auf dem Standortserver. Dieser Standort gibt diesen Ordner wie folgt an das Netzwerk frei:  

`\\<site server name>\SMS_<site code>\Client\`  

`<site server name>` ist der Name des primären Standortservers. `<site code>` ist der Code des primären Standorts, dem der Client zugewiesen ist. Zum Ausführen von „CCMSetup.exe“ in der Befehlszeile auf dem Client müssen Sie eine Verbindung mit dieser Netzwerkadresse herstellen und dann den Befehl ausführen.  

> [!IMPORTANT]  
> Sie müssen über Administratorberechtigungen verfügen, um auf die Clientinstallationsdateien zugreifen zu können.  

Von CCMSetup.exe werden alle notwendigen Voraussetzungen auf den Clientcomputer kopiert, und das Windows Installer-Paket (Client.msi) wird aufgerufen, um den Client zu installieren. Sie können „Client.msi“ nicht direkt ausführen.  

Geben Sie zum Ändern des Verhaltens dieser Clientinstallation die Befehlszeilenoptionen für „CCMSetup.exe“ und „Client.msi“ an. Stellen Sie sicher, dass Sie zuerst die CCMSetup-Parameter angeben, die mit `/` beginnen, bevor Sie die Eigenschaften für „Client.msi“ angeben. Beispiel:  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=AUTO FSP=SMSFP01`

In diesem Beispiel wird der Client mit den folgenden Optionen installiert:  

|Option|Beschreibung|  
|--------------|-----------------|  
|`/mp:SMSMP01`|Mit diesem CCMSetup-Parameter wird der Verwaltungspunkt SMSMP01 zum Herunterladen der erforderlichen Clientinstallationsdateien angegeben.|  
|`/logon`|Mit diesem „CCMSetup“-Parameter wird angegeben, dass die Installation beendet werden soll, wenn ein vorhandener Konfigurations-Manager-Client auf dem Computer gefunden wird.|  
|`SMSSITECODE=AUTO`|Mit dieser Eigenschaft in „Client.msi“ wird angegeben, dass vom Client versucht werden soll, den zu verwendenden Configuration Manager-Standortcode zu finden, beispielsweise mithilfe von Active Directory Domain Services.|  
|`FSP=SMSFP01`|Mit dieser Client.msi-Eigenschaft wird angegeben, dass der Fallbackstatuspunkt SMSFP01 verwendet werden soll, um vom Clientcomputer gesendete Zustandsmeldungen zu empfangen.|  

Weitere Informationen finden Sie unter [Informationen zu Parametern und Eigenschaften für die Clientinstallation ](about-client-installation-properties.md).  

> [!TIP]  
> Informationen zum Verfahren für die Installation des Configuration Manager-Clients auf einem modernen Windows 10-Gerät mit Azure Active Directory-Identität (Azure AD) finden Sie unter [Installieren und Zuweisen von Configuration Manager-Windows 10-Clients über das Internet mit Authentifizierung über Azure AD](deploy-clients-cmg-azure.md). Dieses Verfahren ist für Clients in einem Intranet oder im Internet vorgesehen.  

### <a name="manual-installation-examples"></a>Beispiele für die manuelle Installation

Die folgenden Beispiele sind für in Active Directory eingebundene Clients in einem Intranet bestimmt. Sie verwenden die folgenden Werte:  

- **MPSERVER**: Der Server, der den Verwaltungspunkt hostet
- **FSPSERVER**: Der Server, der den Fallbackstatuspunkt hostet  
- **ABC**: Der Standortcode  
- **contoso.com**: Der Domänenname  

Angenommen, Sie haben alle Standortsystemserver mit einem Intranet-FQDN konfiguriert und die Standortinformationen in Active Directory veröffentlicht.  

Beginnen Sie mit den folgenden Schritten auf dem Clientcomputer:  

1. Melden Sie sich als lokaler Administrator an.  
2. Ordnen Sie `\\MPSERVER\SMS_ABC\Client` Laufwerk Z: zu.  
3. Ändern Sie die Eingabeaufforderung in Laufwerk Z:.  

Führen Sie anschließend einen der folgenden Befehle aus:  

#### <a name="manual-example-1"></a>Manuelles Beispiel 1  

`CCMSetup.exe`  

Mit diesem Befehl wird der Client ohne zusätzliche Parameter oder Eigenschaften installiert. Der Client wird automatisch mit den in Active Directory Domain Services veröffentlichten Clientinstallationseigenschaften konfiguriert, zu denen diese Einstellungen gehören:  

- Standortcode: Für diese Einstellung muss die Netzwerkadresse des Clients in einer Begrenzungsgruppe enthalten sein, die Sie für die Clientzuweisung konfiguriert haben.  
- Verwaltungspunkt
- Fallbackstatuspunkt
- Kommunikation nur über HTTPS  

Weitere Informationen finden Sie unter [Informationen zu Clientinstallationseigenschaften, die in Active Directory Domain Services veröffentlicht wurden](about-client-installation-properties-published-to-active-directory-domain-services.md).  

#### <a name="manual-example-2"></a>Manuelles Beispiel 2  

`CCMSetup.exe /MP:mpserver.contoso.com /UsePKICert SMSSITECODE=ABC CCMHOSTNAME=server05.contoso.com CCMFIRSTCERT=1 FSP=server06.constoso.com`
  
Bei diesem Befehl wird die automatische Konfiguration überschrieben, die von Active Directory Domain Services bereitgestellt wird. Die Netzwerkadresse des Clients müssen Sie nicht in eine Begrenzungsgruppe einschließen, die für die Clientzuweisung konfiguriert wurde. Stattdessen gibt die Installation diese Einstellungen an:

- Standortcode
- Intranetbasierter Verwaltungspunkt
- Internetbasierter Verwaltungspunkt
- Fallbackstatuspunkt, der Verbindungen aus dem Intranet akzeptiert
- Sofern verfügbar, Verwenden eines PKI-Clientzertifikats (Public Key-Infrastruktur) mit der längsten Gültigkeitsdauer

## <a name="logon-script-installation"></a><a name="BKMK_ClientLogonScript"></a> Anmeldeskriptinstallation

Configuration Manager unterstützt Anmeldeskripts für die Installation der Configuration Manager-Clientsoftware. Verwenden Sie die Programmdatei „CCMSetup.exe“ in einem Anmeldeskript, um die Clientinstallation auszulösen.  

Bei der Anmeldeskriptinstallation werden dieselben Methoden wie bei der manuellen Clientinstallation verwendet. Geben Sie den Installationsparameter `/logon` für „CCMSsetup.exe“ an. Wenn auf dem Computer bereits eine Clientversion vorhanden ist, verhindert dieser Parameter, dass der Client installiert wird. Durch dieses Verhalten wird verhindert, dass der Client bei Ausführung des Anmeldeskripts jedes Mal neu installiert wird.  

Wenn Sie mit dem Parameter `/Source` keine Installationsquelle angeben und der Parameter `/MP` keinen Verwaltungspunkt zum Abrufen der Installation angibt, ermittelt „CCMSetup.exe“ den Verwaltungspunkt über Active Directory Domain Services. Dieses Verhalten tritt nur auf, wenn Sie das Schema für Configuration Manager erweitert und den Standort in Active Directory Domain Services veröffentlicht haben. Alternativ können DNS oder WINS vom Client verwendet werden, um einen Verwaltungspunkt zu finden.  

## <a name="package-and-program-installation"></a><a name="BKMK_ClientApp"></a> Installation des Pakets und Programms

Verwenden Sie Configuration Manager zum Erstellen und Bereitstellen von Paketen und Programmen, mit denen die Clientsoftware für ausgewählte Geräte in Ihrer Hierarchie aktualisiert wird. Configuration Manager stellt eine Paketdefinitionsdatei bereit, die die Paketeigenschaften mit häufig verwendeten Werten auffüllt. Passen Sie das Verhalten der Clientinstallation an, indem Sie zusätzliche Befehlszeilenparameter und -eigenschaften angeben.  

> [!NOTE]  
> Mit dieser Methode können keine Upgrades von Configuration Manager 2007-Clients durchgeführt werden. Verwenden Sie stattdessen ein automatisches Clientupgrade, bei dem automatisch ein Paket erstellt und bereitgestellt wird, das die aktuelle Clientversion enthält. Weitere Informationen finden Sie unter [Upgrade clients (Aktualisieren von Clients)](../manage/upgrade/upgrade-clients.md).  
>
> Weitere Informationen zum Migrieren einer älteren Version des Configuration Manager-Clients finden Sie unter [Planning a client migration strategy (Planen einer Strategie für die Clientmigration)](../../migration/planning-a-client-migration-strategy.md).  

### <a name="create-a-package-and-program-for-the-client-software"></a>Erstellen eines Pakets und Programms für die Clientsoftware  

Gehen Sie wie folgt vor, um ein Configuration Manager-Paket und -Programm für die Bereitstellung auf Configuration Manager-Clientcomputern zum Ausführen eines Upgrades der Clientsoftware zu erstellen.  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie **Anwendungsverwaltung**, und wählen Sie den Knoten **Pakete** aus.  

2. Wählen Sie auf der Registerkarte **Start** des Menübands in der Gruppe **Erstellen** die Option **Paket aus Definition erstellen** aus.  

3. Wählen Sie im auf der Seite **Paketdefinition** des Assistenten in der Liste **Herausgeber** die Option **Microsoft** aus. Wählen Sie in der Liste **Paketdefinition** die Option **Aktualisierung des Configuration Manager-Clients** aus.  

4. Aktivieren Sie auf der Seite **Quelldateien** die Option **Dateien immer aus dem Quellordner abrufen**.  

5. Wählen Sie auf der Seite **Quellordner** den Eintrag **Netzwerkpfad (UNC-Name)** aus. Geben Sie anschließend den Netzwerkpfad zum Server und zur Freigabe mit den Clientinstallationsdateien ein.  

    > [!NOTE]  
    > Der Computer, auf dem die Configuration Manager-Bereitstellung ausgeführt wird, muss Zugriff auf den von Ihnen angegebenen Netzwerkordner haben. Andernfalls tritt ein Fehler bei der Clientinstallation auf.  

    Wenn Sie die Eigenschaften der Clientinstallation ändern möchten, können Sie die Befehlszeile für „CCMSetup.exe“ im Dialogfeld **Configuration Manager agent silent upgrade Properties** (Eigenschaften von „Automatisches Upgrade des Configuration Manager-Agents“) auf der Registerkarte **Allgemein** ändern. Die Standardinstallationseigenschaften sind `/noservice SMSSITECODE=AUTO`.  

6. Verteilen Sie das Paket an alle Verteilungspunkte, auf denen das Clientupgradepaket gehostet werden soll. Stellen Sie das Paket anschließend in Gerätesammlungen bereit, die Clients enthalten, die Sie aktualisieren möchten.  

## <a name="intune-mdm-managed-windows-devices"></a><a name="bkmk_mdm"></a> Mit Intune MDM verwaltete Windows-Geräte

Stellen Sie die Installationsdateien des Konfigurations-Manager-Clients auf Computern bereit, die mit Microsoft Intune registriert sind.

Dieses Verfahren ist für einen herkömmlichen Client vorgesehen, der mit einem Intranet verbunden ist. Es verwendet Authentifizierungsmethoden für herkömmliche Clients. Um sicherzustellen, dass das Gerät nach der Installation des Clients in einem verwalteten Zustand bleibt, muss sich der Client im Intranet und innerhalb einer Configuration Manager-Standortgrenze befinden.  

Informationen zum Verfahren für die Installation des Configuration Manager-Clients auf einem modernen Windows 10-Gerät mit Azure AD-Identität finden Sie unter [Installieren und Zuweisen von Configuration Manager-Windows 10-Clients über das Internet mit Authentifizierung über Azure AD](deploy-clients-cmg-azure.md).

Nachdem Sie den Configuration Manager-Client installiert haben, wird die Registrierung von Geräten bei Intune nicht aufgehoben. Sie können zur gleichen Zeit den Configuration Manager-Client und die MDM-Registrierung verwenden. Weitere Informationen finden Sie unter [Übersicht über die Co-Verwaltung](../../../comanage/overview.md).  

> [!Note]
> Sie können andere Clientinstallationsmethoden verwenden, um den Configuration Manager-Client auf einem von Intune verwalteten Gerät zu installieren. Wenn sich beispielsweise ein mit Intune verwaltetes Gerät im Intranet befindet und der Active Directory-Domäne hinzugefügt wird, können Sie die Gruppenrichtlinie zum Installieren des Configuration Manager-Clients verwenden.<!-- SCCMDocs#757 -->

### <a name="install-the-configuration-manager-client-by-using-intune"></a>Installieren des Configuration Manager-Clients mit Intune

1. Fügen Sie in Intune [eine branchenspezifische Windows-App hinzu](https://docs.microsoft.com/mem/intune/apps/lob-apps-windows), die die Installationsdatei des Configuration Manager-Clients, **CCMSetup.msi**, enthält. Sie finden diese Datei auf dem Standortserver im Configuration Manager-Installationsverzeichnis im Ordner `\bin\i386`.  

2. Geben Sie im Intune-Softwareherausgeber die Befehlszeilenparameter ein. Verwenden Sie z.B. diesen Befehl mit einem herkömmlichen Client in einem Intranet:  

    `CCMSETUPCMD="/MP:<FQDN of management point> SMSMP=<FQDN of management point> SMSSITECODE=<your site code> DNSSUFFIX=<DNS suffix of management point>"`  

    > [!NOTE]  
    > Eine beispielhafte Befehlszeile für die Verwendung mit einem modernen Windows 10-Client mit Azure AD-Authentifizierung finden Sie unter [Vorbereiten internetbasierter Geräte für die Co-Verwaltung](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client).  

3. [Weisen Sie die App zu](../../../../intune/apps/apps-deploy.md), und zwar einer Gruppe der registrierten Windows-Computer.  

## <a name="os-image-installation"></a><a name="BKMK_ClientImage"></a> Installation mit Betriebssystemimage

Installieren Sie den Konfigurations-Manager-Client auf einem Referenzcomputer vor, den Sie für die Erstellung eines Betriebssystemimages verwenden.

> [!IMPORTANT]  
> Bei der Verwendung der Configuration Manager-Tasksequenz für die Bereitstellung eines Betriebssystemimages wird der Configuration Manager-Client im Schritt [Configuration Manager-Client vorbereiten](../../../osd/understand/task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture) vollständig entfernt.  

### <a name="prepare-the-client-computer-for-imaging"></a>Vorbereiten des Clientcomputers auf die Imageerstellung  

1. Installieren Sie die Configuration Manager-Clientsoftware manuell auf dem Referenzcomputer. Weitere Informationen finden Sie im Abschnitt [Manuelle Installation](#BKMK_Manual).  

    > [!IMPORTANT]  
    > Geben Sie in den Befehlszeileneigenschaften der Datei „CCMSetup.exe“ keinen Configuration Manager-Standortcode für den Client an.  

2. Geben Sie in einer Eingabeaufforderung `net stop ccmexec` ein, um den Dienst SMS-Agent-Host (CcmExec.exe) auf dem Referenzcomputer anzuhalten.  

3. Löschen Sie auf dem Referenzcomputer die Datei SMSCFG.INI aus dem Ordner „Windows“.  

4. Entfernen Sie alle im lokalen Computerspeicher auf dem Referenzcomputer gespeicherten Zertifikate. Wenn Sie beispielsweise PKI-Zertifikate (Public Key-Infrastruktur) verwenden, müssen Sie vor dem Erstellen des Images die Zertifikate im **privaten** Speicher für **Computer** und **Benutzer** entfernen.  

5. Wenn die Clients in anderen Configuration Manager-Hierarchien als der Referenzcomputer installiert sind, entfernen Sie den vertrauenswürdigen Stammschlüssel vom Referenzcomputer.  

    > [!NOTE]  
    > Wenn Clients Active Directory Domain Services nicht zum Suchen eines Verwaltungspunkts abfragen können, verwenden sie den vertrauenswürdigen Stammschlüssel, um vertrauenswürdige Verwaltungspunkte zu finden. Wenn Sie alle Clients, von denen ein Image erstellt wurde, in der Hierarchie des Mastercomputers bereitstellen, lassen Sie den vertrauenswürdigen Stammschlüssel unverändert.
    >
    > Wenn Sie die Clients in unterschiedlichen Hierarchien bereitstellen, entfernen Sie den vertrauenswürdigen Stammschlüssel. Stellen Sie zudem den vertrauenswürdigen Stammschlüssel für diese Clients bereit. Weitere Informationen finden Sie unter [Planning for the trusted root key (Planen des vertrauenswürdigen Stammschlüssels)](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

6. Erfassen Sie das Image des Mastercomputers mit Ihrer Imaging-Software.  

7. Stellen Sie das Image auf den Zielcomputern bereit.  

## <a name="workgroup-computers"></a><a name="BKMK_ClientWorkgroup"></a> Arbeitsgruppencomputer

Configuration Manager unterstützt die Clientinstallation auf Computern in Arbeitsgruppen. Installieren Sie den Client mithilfe der in [Manuelle Installation](#BKMK_Manual) angegebenen Methode auf Arbeitsgruppencomputern.  

### <a name="prerequisites"></a>Voraussetzungen  

- Installieren Sie den Client manuell auf jedem Arbeitsgruppencomputer. Während der Installation muss der interaktive Benutzer über die Rechte eines lokalen Administrators verfügen.  

- Konfigurieren Sie das Netzwerkzugriffskonto für den Standort, um auf Ressourcen in der Configuration Manager-Standortserverdomäne zugreifen zu können. Geben Sie dieses Konto in der Softwareverteilungskomponente des Standorts an. Weitere Informationen finden Sie unter [Standortkomponenten](../../servers/deploy/configure/site-components.md).  

### <a name="limitations"></a>Einschränkungen  

- Arbeitsgruppenclients können keine Verwaltungspunkte von Active Directory Domain Services lokalisieren. Verwenden Sie stattdessen DNS, WINS oder andere Verwaltungspunkte.  

- Globales Roaming wird nicht unterstützt. Arbeitsgruppenclients können Active Directory Domain Services nicht nach Standortinformationen abfragen.  

- Über die Active Directory-Ermittlungsmethoden können keine Computer in Arbeitsgruppen ermittelt werden.  

- Sie können keine Software für Benutzer von Arbeitsgruppencomputern bereitstellen.  

- Sie können die Clientpushinstallation nicht zum Installieren des Clients auf Arbeitsgruppencomputern verwenden.  

- Arbeitsgruppenclients können Kerberos nicht für die Authentifizierung verwenden, sodass möglicherweise eine manuelle Genehmigung erforderlich ist.  

- Sie können keinen Arbeitsgruppenclient als Verteilungspunkt konfigurieren. Configuration Manager erfordert, dass Verteilungspunktcomputer Mitglied einer Domäne sind.  

### <a name="install-the-client-on-workgroup-computers"></a>Installieren des Clients auf Arbeitsgruppencomputern  

Prüfen Sie die Voraussetzungen, und befolgen Sie anschließend die Anweisungen im Abschnitt [Manuelles Installieren von Configuration Manager-Clients](#BKMK_Manual).  

#### <a name="workgroup-example-1"></a>Arbeitsgruppe Beispiel 1

Dieses Beispiel dient folgenden Aktionen:

- Installieren des Clients für die Clientverwaltung über das Intranet
- Angeben des Standortcodes
- Angeben des DNS-Suffix zur Lokalisierung eines Verwaltungspunkts  

`CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=constoso.com`  

#### <a name="workgroup-example-2"></a>Arbeitsgruppe Beispiel 2

In diesem Beispiel muss sich der Client an einer Netzwerkadresse befinden, die in einer Begrenzungsgruppe konfiguriert wurde. Wenn diese Voraussetzung nicht erfüllt ist, funktioniert die automatische Standortzuweisung nicht. Der Befehl enthält einen Fallbackstatuspunkt auf dem Server FSPSERVER. Diese Eigenschaft dient als Unterstützung bei der Nachverfolgung der Clientbereitstellung und bei der Ermittlung von Problemen bei der Clientkommunikation.

`CCMSetup.exe FSP=fspserver.constoso.com`  

## <a name="internet-based-client-management"></a><a name="BKMK_ClientInternet"></a> Internetbasierte Clientverwaltung  

> [!NOTE]  
> Dieser Abschnitt gilt nicht für Clients, die eine [Cloud Management Gateway](../manage/cmg/plan-cloud-management-gateway.md)-Instanz verwenden. Informationen zur Installation internetbasierter Clients über eine Cloud Management Gateway-Instanz finden Sie unter [Installieren und Zuweisen von Configuration Manager-Windows 10-Clients über das Internet mit Authentifizierung über Azure AD](deploy-clients-cmg-azure.md).  

Wenn der Configuration Manager-Standort die [internetbasierte Clientverwaltung](../manage/plan-internet-based-client-management.md) für Clients unterstützt, die sich manchmal in einem Intranet befinden, stehen Ihnen beim Installieren von Clients im Intranet zwei Optionen zur Verfügung:  

- Schließen die Client.msi-Eigenschaft `CCMHOSTNAME=<internet FQDN of the internet-based management point>` ein, wenn Sie den Client beispielsweise mithilfe der manuellen Installation oder der Clientpushinstallation installieren. Wenn Sie diese Methode verwenden, müssen Sie den Client direkt dem Standort zuweisen. Sie können die automatische Standortzuweisung nicht verwenden. Im Abschnitt [Manuelle Installation](#BKMK_Manual) finden Sie ein Beispiel für diese Konfigurationsmethode.  

- Installieren Sie den Client für die Clientverwaltung über das Intranet, und weisen Sie dem Client anschließend einen internetbasierten Clientverwaltungspunkt zu. Ändern Sie den Verwaltungspunkt mithilfe der Clienteigenschaften auf der Seite **Configuration Manager** in der Systemsteuerung oder mithilfe eines Skripts. Beim Verwenden dieser Methode können Sie die automatische Clientzuweisung verwenden. Weitere Informationen finden Sie im Abschnitt [So konfigurieren Sie Clients für die internetbasierte Clientverwaltung nach der Clientinstallation](#BKMK_ConfigureIBCM_MP).  

Verwenden Sie eine der folgenden unterstützten Methoden, um Clients zu installieren, die sich im Internet befinden:  

- Geben Sie einen Mechanismus für diese Clients an, damit diese vorübergehend mit VPN mit dem Intranet verbunden werden. Installieren Sie anschließend den Client mit einer geeigneten Clientinstallationsmethode.  

- Verwenden Sie eine von Configuration Manager unabhängige Installationsmethode. Sie können die Quelldateien für die Clientinstallation beispielsweise auf Wechselmedien bündeln und diese für die Installation an Benutzer senden. Die Quelldateien für die Clientinstallation befinden sich im Ordner `<installation path>\Client` auf dem Configuration Manager-Standortserver. Schließen Sie auf den Medien ein Skript ein, mit dem Daten manuell über den Clientordner kopiert werden. Installieren Sie den Client über diesen Ordner, indem Sie „CCMSetup.exe“ und die jeweiligen „CCMSetup“-Befehlszeileneigenschaften verwenden.  

> [!NOTE]  
> Configuration Manager unterstützt die direkte Installation eines Clients von einem internetbasierten Verwaltungspunkt oder von einem Internetbasierten Softwareupdatepunkt nicht.

Über das Internet verwaltete Clients müssen mit internetbasierten Standortsystemen kommunizieren. Stellen Sie vor der Installation der Clients sicher, dass diese auch über PKI-Zertifikate (Public Key Infrastructure) verfügen. Installieren Sie diese Zertifikate unabhängig von Configuration Manager. Weitere Informationen zu PKI-Zertifikatanforderungen finden Sie unter [PKI-Zertifikatanforderungen](../../plan-design/network/pki-certificate-requirements.md).  

### <a name="install-clients-on-the-internet-by-specifying-ccmsetup-command-line-properties"></a>Installieren von Clients im Internet durch Angabe von CCMSetup-Befehlszeileneigenschaften  

1. Befolgen Sie die Anweisungen im Abschnitt [Manuelles Installieren von Konfigurations-Manager-Clients](#BKMK_Manual). Schließen Sie immer die folgenden Optionen ein:  

    - CCMSetup-Befehlszeilenparameter `/source:<local path of the copied Client folder>`  

    - CCMSetup-Befehlszeilenparameter `/UsePKICert`  

    - „Client.msi“-Eigenschaft `CCMHOSTNAME=<FQDN of internet-based management point>`  

    - „Client.msi“-Eigenschaft `SMSSIGNCERT=<local path of exported site server signing certificate>`  

    - „Client.msi“-Eigenschaft `SMSSITECODE=<site code of internet-based management point>`  

    > [!NOTE]  
    > Wenn der Standort über mehrere internetbasierte Verwaltungspunkte verfügt, können Sie für die Eigenschaft `CCMHOSTNAME` einen beliebigen angeben. Wenn ein Konfigurations-Manager-Client eine Verbindung mit dem angegebenen internetbasierten Verwaltungspunkt herstellt, wird eine Liste aller am Standort verfügbaren internetbasierten Verwaltungspunkte an den Client gesendet. Der Client wählt nach dem Zufallsprinzip einen Verwaltungspunkt aus.

2. Geben Sie den CCMSetup-Befehlszeilenparameter `/NoCRLCheck` an, wenn Sie nicht wünschen, dass die Zertifikatssperrliste vom Client überprüft wird.  

3. Wenn Sie einen internetbasierten Fallbackstatuspunkt verwenden, geben Sie die „Client.msi“-Eigenschaft `FSP=<internet FQDN of the internet-based fallback status point>` an.  

4. Wenn Sie den Client für rein internetbasierte Clientverwaltung installieren, geben Sie die „Client.msi“-Eigenschaft `CCMALWAYSINF=1` an.  

5. Bestimmen Sie, ob Sie zusätzliche CCMSetup-Befehlszeilenparameter angeben müssen. Beispielsweise kann es erforderlich sein, ein Kriterium für die Auswahl eines Zertifikats anzugeben, wenn der Client über mehrere gültige PKI-Zertifikate verfügt. Eine Liste aller verfügbaren Eigenschaften finden Sie unter [Informationen zu Parametern und Eigenschaften für die Clientinstallation](about-client-installation-properties.md).  

#### <a name="internet-based-example"></a>Beispiel für internetbasierte Clients

`CCMSetup.exe /source: D:\Clients /UsePKICert CCMHOSTNAME=server1.contoso.com SMSSIGNCERT=siteserver.cer SMSSITECODE=ABC FSP=server2.contoso.com CCMALWAYSINF=1 CCMFIRSTCERT=1`

In diesem Beispiel wird der Client mit dem folgenden Verhalten installiert:

- Verwenden von Quelldateien in einem Ordner auf Laufwerk D:
- Verwenden des PKI-Clientzertifikats
- Auswählen des Zertifikats mit der längsten Gültigkeitsdauer
- Reine Internetverwaltung von Clients
- Zuweisen des Clients zur Verwendung des internetbasierten Verwaltungspunkts SERVER1
- Zuweisen des internetbasierten Fallbackstatuspunkts in der Domäne contoso.com
- Zuweisen des Clients zum Standort „ABC“  

### <a name="to-configure-clients-for-internet-based-client-management-after-client-installation"></a><a name="BKMK_ConfigureIBCM_MP"></a> So konfigurieren Sie Clients für die internetbasierte Clientverwaltung nach der Clientinstallation  

Wenden Sie eine der folgenden Prozeduren an, um den internetbasierten Verwaltungspunkt nach der Clientinstallation zuzuweisen. Das erste erfordert die manuelle Konfiguration und eignet sich für eine geringe Anzahl von Clients. Das zweite ist besser zum Konfigurieren einer großen Anzahl von Clients geeignet.  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-from-the-configuration-manager-control-panel"></a>Konfigurieren von Clients für die internetbasierte Clientverwaltung nach der Clientinstallation über die Configuration Manager-Systemsteuerung  

1. Öffnen Sie die **Configuration Manager**-Systemsteuerung für den Client.  

2. Geben Sie auf der Registerkarte **Internet** den vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) des internetbasierten Verwaltungspunkts als **Internet-FQDN** ein.  

    > [!NOTE]  
    > Die Registerkarte **Internet** ist nur verfügbar, wenn der Client über ein Client-PKI-Zertifikat verfügt.  

3. Geben Sie die Proxyservereinstellungen ein, wenn der Client über einen Proxyserver auf das Internet zugreift.  

#### <a name="configure-clients-for-internet-based-client-management-after-client-installation-by-using-a-script"></a>Konfigurieren von Clients für die internetbasierte Clientverwaltung nach der Clientinstallation mithilfe eines Skripts  

##### <a name="powershell"></a>PowerShell

1. Öffnen Sie einen PowerShell-Inline-Editor wie PowerShell ISE oder Visual Studio Code. Sie können auch einen Texteditor wie Editor verwenden.

2. Kopieren Sie die folgenden Codezeilen, und fügen Sie sie in den Editor ein. Ersetzen Sie `'mp.contoso.com'` durch den Internet-FQDN des internetbasierten Verwaltungspunkts.

    ``` PowerShell
    $newInternetBasedManagementPointFQDN = 'mp.contoso.com'
    $client = New-Object -ComObject Microsoft.SMS.Client
    $client.SetInternetManagementPointFQDN($newInternetBasedManagementPointFQDN)
    Restart-Service CcmExec
    $client.GetInternetManagementPointFQDN()
    ```

    > [!NOTE]  
    > Die letzte Zeile dient nur zur Bestätigung des neuen Werts des Internetverwaltungspunkts.
    >
    > Entfernen Sie den FQDN-Wert des Servers innerhalb der Anführungszeichen, um einen angegebenen internetbasierten Verwaltungspunkt zu löschen. Die Zeile wird zu `$newInternetBasedManagementPointFQDN = ''`.

3. Speichern Sie die Datei mit der Erweiterung PS1.  

4. Führen Sie das Skript mit erhöhten Rechten auf Clientcomputern aus. Verwenden Sie eine der folgenden Methoden:  

    - Stellen Sie die Datei mithilfe eines Pakets und Programms auf vorhandenen Configuration Manager-Clients bereit.  

    - Führen Sie die Datei auf vorhandenen Configuration Manager-Clients lokal aus, indem Sie im Explorer auf die Skriptdatei doppelklicken.  

Möglicherweise müssen Sie den Client neu starten, damit die Änderungen wirksam werden.  

## <a name="provision-client-installation-properties"></a><a name="BKMK_Provision"></a> Bereitstellen von Clientinstallationseigenschaften

Stellen Sie Clientinstallationseigenschaften für auf einer Gruppenrichtlinie oder einem Softwareupdate basierende Clientinstallationen bereit. Verwenden Sie Windows-Gruppenrichtlinien, um Eigenschaften für die Konfigurations-Manager-Clientinstallation für Computer bereitzustellen. Diese Eigenschaften werden in der Registrierung des Computers gespeichert. Der Client liest diese während der Installation. Dieses Verfahren wäre normalerweise nicht erforderlich, wird aber möglicherweise für einige Clientinstallationsszenarien benötigt. Beispiele:  

- Sie verwenden die Gruppenrichtlinieneinstellungen oder auf einem Softwareupdate basierende Clientinstallationsmethoden. Sie haben das Active Directory-Schema für Configuration Manager nicht erweitert.  

- Sie möchten Clientinstallationseigenschaften auf bestimmten Computern außer Kraft setzen.  

> [!NOTE]  
> Wenn Sie Installationseigenschaften mit dem Befehl CCMSetup.exe bereitstellen, werden die auf Computern bereitgestellten Installationseigenschaften nicht verwendet.

Eine administrative Vorlage für Gruppenrichtlinien mit dem Namen `ConfigMgrInstallation.adm` ist auf den Configuration Manager-Installationsmedien vorhanden. Verwenden Sie diese Vorlage für die Bereitstellung von Installationseigenschaften auf Clientcomputern.

> [!TIP]
> Standardmäßig unterstützt `ConfigMgrInstallation.adm` keine Zeichenfolgen mit mehr als 255 Zeichen. Diese Konfiguration kann sich auf das Hinzufügen mehrerer Parameter oder Parameter mit langen Werten auswirken, z. B. CCMCERTISSUERS.<!-- SCCMDocs#1648 -->
>
> So umgehen Sie dieses Problem:
>
> 1. Bearbeiten Sie `ConfigMgrInstallation.adm` im Editor.
> 2. Ändern Sie für die Eigenschaft `VALUENAME SetupParameters` den Wert `MAXLEN` in eine größere ganze Zahl. Beispiel: `MAXLEN 511`.

### <a name="configure-and-assign-client-installation-properties-by-using-a-group-policy-object"></a>Konfigurieren und Zuweisen von Clientinstallationseigenschaften mithilfe eines Gruppenrichtlinienobjekts  

1. Importieren Sie die administrative Vorlage „ConfigMgrInstallation.adm“ mithilfe eines Editors wie dem Gruppenrichtlinienobjekt-Editor (Group Policy Object, GPO) von Windows in ein neues oder vorhandenes Gruppenrichtlinienobjekt. Sie finden diese Datei auf den Configuration Manager-Installationsmedien im Ordner `TOOLS\ConfigMgrADMTemplates`.  

2. Öffnen Sie die Eigenschaften der importierten Einstellung **Clientbereitstellungseigenschaften konfigurieren**.  

3. Wählen Sie **Aktiviert** aus.  

4. Geben Sie in das Feld **CCMSetup** die erforderlichen CCMSetup-Befehlszeileneigenschaften ein. Eine Liste aller CCMSetup-Befehlszeileneigenschaften mit Verwendungsbeispielen finden Sie unter [Informationen zu Parametern und Eigenschaften für die Clientinstallation](about-client-installation-properties.md).  

5. Weisen Sie den Computern das GPO zu, auf denen Sie die Configuration Manager-Clientinstallationseigenschaften bereitstellen möchten.