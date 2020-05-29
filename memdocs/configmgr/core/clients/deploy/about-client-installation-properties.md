---
title: Parameter und Eigenschaften für die Clientinstallation
titleSuffix: Configuration Manager
description: Dieser Abschnitt enthält Informationen zu den ccmsetup-Befehlszeilenparametern und -Befehlszeileneigenschaften für die Installation des Konfigurations-Manager-Clients.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: c890fd27-7a8c-4f51-bbe2-f9908af1f42b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 12fee834e4f384cc180658a8e58cf3920a907831
ms.sourcegitcommit: 555cb8102715afbe06c4de5fdbc943608f00b52c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/28/2020
ms.locfileid: "84153449"
---
# <a name="about-client-installation-parameters-and-properties-in-configuration-manager"></a>Informationen zu Parametern und Eigenschaften für die Clientinstallation in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie den Befehl CCMSetup.exe für die Installation des Configuration Manager-Clients. Wenn Sie die *Parameter* für die Clientinstallation in der Befehlszeile angeben, wird dadurch das Installationsverhalten geändert. Wenn Sie die *Eigenschaften* für die Clientinstallation in der Befehlszeile angeben, wird dadurch die Erstkonfiguration des installierten Client-Agents geändert.

## <a name="about-ccmsetupexe"></a><a name="aboutCCMSetup"></a> Informationen zu „CCMSetup.exe“

Der Befehl „CCMSetup.exe“ lädt die Dateien herunter, die zum Installieren des Clients über einen Verwaltungspunkt oder einen Quellspeicherort erforderlich sind. Dazu zählen unter anderem folgende Dateien:  

- Das Windows Installer-Paket „client.msi“ für die Installation der Clientsoftware.

- Client-Voraussetzungen

- Updates und Korrekturen für den Configuration Manager-Client

> [!NOTE]
> Sie können client.msi nicht direkt installieren.  

Die Datei CCMSetup.exe enthält mehrere *Parameter* für die Befehlszeile, mit denen das Installationsverhalten angepasst werden kann. Den Parametern wird ein Schrägstrich (`/`) vorangestellt, und sie werden üblicherweise kleingeschrieben. Den Wert eines Parameters können Sie bei Bedarf mithilfe eines Doppelpunkts (`:`) angeben, dem der Wert folgt. Weitere Informationen finden Sie unter [Befehlszeilenparameter von „CCMSetup.exe“](#ccmsetupexe-command-line-parameters).

Sie können auch über die Befehlszeile von „CCMSetup.exe“ *Eigenschaften* angeben, um das Verhalten von „client.msi“ zu ändern. Eigenschaften werden üblicherweise in Großbuchstaben geschrieben. Sie können einen Wert für eine Eigenschaft angeben, indem Sie ein Gleichheitszeichen (`=`) verwenden, dem der Wert folgt. Weitere Informationen finden Sie unter [Eigenschaften der Datei „Client.msi“](#clientMsiProps).

> [!IMPORTANT]  
> Geben Sie alle erforderlichen CCMSetup-Parameter an, bevor Sie die Eigenschaften für „client.msi“ angeben.  

Die Datei CCMSetup.exe und die unterstützenden Dateien befinden sich auf dem Standortserver im Ordner **Client** des Configuration Manager-Installationsordners. Configuration Manager gibt diesen Ordner für das Netzwerk unter der Standortfreigabe frei. Beispiel: `\\SiteServer\SMS_ABC\Client`.

Bei der Eingabeaufforderung wird vom Befehl CCMSetup.exe das folgende Format verwendet:  

`CCMSetup.exe [<Ccmsetup parameters>] [<client.msi setup properties>]`  

Beispiel:  

`CCMSetup.exe /mp:SMSMP01 /logon SMSSITECODE=S01 FSP=SMSFSP01`  

Dieses Beispiel dient zu Folgendem:  

- Gibt den Verwaltungspunkt mit dem Namen SMSMP01 an, um eine Liste mit Verteilungspunkten zum Herunterladen der Clientinstallationsdateien anzufordern.  

- Gibt an, dass die Installation beendet wird, wenn bereits eine Version des Clients auf dem Computer vorhanden ist.  

- Weist „client.msi“ an, den Client dem Standortcode „S01“ zuzuweisen.  

- Weist „client.msi“ an, den Fallbackstatuspunkt „SMSFP01“ zu verwenden.  

> [!TIP]  
> Wenn ein Parameterwert Leerräume enthält, setzen Sie diesen zwischen Anführungszeichen.  

Wenn Sie das Active Directory-Schema für Configuration Manager erweitert haben, werden viele Clientinstallationseigenschaften in den Active Directory Domain Services am Standort veröffentlicht. Der Configuration Manager-Client liest diese Eigenschaften automatisch. Weitere Informationen finden Sie unter [Informationen zu Clientinstallationseigenschaften, die in Active Directory Domain Services veröffentlicht wurden](about-client-installation-properties-published-to-active-directory-domain-services.md)  

## <a name="ccmsetupexe-command-line-parameters"></a>Befehlszeilenparameter von „CCMSetup.exe“

### <a name=""></a><a name="bkmk_help"></a> /?

Zeigt die verfügbaren Befehlszeilenparameter für „ccmsetup.exe“.  

Beispiel: `ccmsetup.exe /?`

### <a name="source"></a>/source

Gibt den Speicherort für den Dateidownload an. Verwenden Sie einen lokalen oder einen UNC-Pfad. Die Dateien werden mithilfe des SMB-Protokolls (Server Message Block) auf das Gerät heruntergeladen. Zum Verwenden von **/source** muss das Windows-Benutzerkonto der Clientinstallation über **Leseberechtigungen** für den Speicherort verfügen.

Weitere Informationen dazu, wie CCMSetup Inhalte herunterlädt, finden Sie unter [Begrenzungsgruppen – Clientinstallation](../../servers/deploy/configure/boundary-groups.md#bkmk_ccmsetup). Dieser Artikel enthält auch Details zum Verhalten von CCMSetup, wenn Sie sowohl den Parameter **/mp** als auch **/source** verwenden.

> [!TIP]  
> Sie können den Parameter **/source** mehrmals in der Befehlszeile verwenden, um alternative Downloadspeicherorte anzugeben.  

Beispiel: `ccmsetup.exe /source:"\\server\share"`

### <a name="mp"></a>/mp

Gibt einen Quellenverwaltungspunkt für Computer an, mit denen eine Verbindung hergestellt werden soll. Computer suchen über diesen Verwaltungspunkt nach dem nächstgelegenen Verteilungspunkt für die Installationsdateien. Wenn keine Verteilungspunkte vorhanden sind oder Computer die Dateien auch nach Ablauf von vier Stunden nicht von den Verteilungspunkten herunterladen können, werden die Dateien vom angegebenen Verwaltungspunkt heruntergeladen.  

Weitere Informationen dazu, wie CCMSetup Inhalte herunterlädt, finden Sie unter [Begrenzungsgruppen – Clientinstallation](../../servers/deploy/configure/boundary-groups.md#bkmk_ccmsetup). Dieser Artikel enthält auch Details zum Verhalten von CCMSetup, wenn Sie sowohl den Parameter **/mp** als auch **/source** verwenden.

> [!IMPORTANT]  
> Dieser Parameter gibt einen ersten Verwaltungspunkt für Computer an, um eine Downloadquelle zu ermitteln. Hierfür kommt jeder Verwaltungspunkt jedes Standorts in Frage. Er *weist* den Client nicht dem angegebenen Verwaltungspunkt zu.

Computer laden die Dateien je nach Standortsystemrollen-Konfiguration für Clientverbindungen über eine HTTP- oder eine HTTPS-Verbindung herunter. Für den Download kann auch die BITS-Drosselung verwendet werden, wenn Sie sie konfigurieren. Wenn Sie alle Verteilungspunkte und Verwaltungspunkte ausschließlich für HTTPS-Clientverbindungen konfigurieren, stellen Sie sicher, dass für den Clientcomputer ein gültiges Clientzertifikat verfügbar ist.  

Sie können mit dem Befehlszeilenparameter **/mp** mehrere Verwaltungspunkte angeben. Wenn der Computer keine Verbindung mit dem ersten Verwaltungspunkt herstellen kann, versucht er es mit dem nächsten in der Liste angegebenen Verwaltungspunkt. Wenn Sie mehrere Verwaltungspunkte angeben, trennen Sie die Werte durch Semikolons.

Wenn der Client per HTTPS eine Verbindung mit einem Verwaltungspunkt herstellt, geben Sie anstelle des Computernamens den vollqualifizierten Domänennamen (FQDN) an. Der Wert muss mit dem **Antragstellernamen** oder **alternativen Antragstellernamen** des PKI-Zertifikats für den Verwaltungspunkt übereinstimmen. Obwohl Configuration Manager einen Computernamen im Zertifikat für Verbindungen im Intranet unterstützt, wird die Verwendung eines vollqualifizierten Domänennamens empfohlen.

Beispiel mit dem Computernamen: `ccmsetup.exe /mp:SMSMP01`  

Beispiel mit dem FQDN: `ccmsetup.exe /mp:smsmp01.contoso.com`  

Dieser Parameter kann auch die URL eines Cloudverwaltungsgateways (Cloud Management Gateway, CMG) angeben. Verwenden Sie diese URL, um den Client auf einem internetbasierten Gerät zu installieren. Führen Sie die folgenden Schritte aus, um den Wert für diesen Parameter abzurufen:

- Erstellen Sie ein CMG. Weitere Informationen finden Sie unter [Einrichten eines CMG](../manage/cmg/setup-cloud-management-gateway.md).
- Öffnen Sie auf einem aktiven Client als Administrator eine Windows PowerShell-Eingabeaufforderung.
- Führen Sie den folgenden Befehl aus:

    ```PowerShell
    (Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP
    ```

- Fügen Sie das Präfix `https://` für die Verwendung mit dem Parameter **/mp** an.

Beispiel für die Verwendung der Cloudverwaltungsgateway-URL: `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

> [!Important]
> Wenn die URL eines Cloudverwaltungsgateways für den Parameter **/mp** angegeben wird, muss diese mit `https://` beginnen.

### <a name="regtoken"></a>/regtoken

<!--5686290-->

Ab Version 2002 verwenden Sie diesen Parameter, um ein Massenregistrierungstoken bereitzustellen. Ein internetbasiertes Gerät verwendet dieses Token im Registrierungsprozess über ein Cloudverwaltungsgateway (CMG). Weitere Informationen finden Sie unter [Tokenbasierte Authentifizierung für CMG](deploy-clients-cmg-token.md).

Wenn Sie diesen Parameter verwenden, schließen Sie auch die folgenden Parameter und Eigenschaften ein:

- [ **/mp**](#mp)
- [**CCMHOSTNAME**](#ccmhostname)
- [**SMSSiteCode**](#smssitecode)
- [**SMSMP**](#smsmp)

Die folgende Beispielbefehlszeile enthält die anderen erforderlichen Setupparameter und -eigenschaften:

`ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com /regtoken:eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik9Tbzh2Tmd5VldRUjlDYVh5T2lacHFlMDlXNCJ9.eyJTQ0NNVG9rZW5DYXRlZ29yeSI6IlN7Q01QcmVBdXRoVG9rZW4iLCJBdXRob3JpdHkiOiJTQ0NNIiwiTGljZW5zZSI6IlNDQ00iLCJUeXBlIjoiQnVsa1JlZ2lzdHJhdGlvbiIsIlRlbmFudElkIjoiQ0RDQzVFOTEtMEFERi00QTI0LTgyRDAtMTk2NjY3RjFDMDgxIiwiVW5pcXVlSWQiOiJkYjU5MWUzMy1wNmZkLTRjNWItODJmMy1iZjY3M2U1YmQwYTIiLCJpc3MiOiJ1cm46c2NjbTpvYXV0aDI6Y2RjYzVlOTEtMGFkZi00YTI0LTgyZDAtMTk2NjY3ZjFjMDgxIiwiYXVkIjoidXJuOnNjY206c2VydmljZSIsImV4cCI6MTU4MDQxNbUwNSwibmJmIjoxNTgwMTU2MzA1fQ.ZUJkxCX6lxHUZhMH_WhYXFm_tbXenEdpgnbIqI1h8hYIJw7xDk3wv625SCfNfsqxhAwRwJByfkXdVGgIpAcFshzArXUVPPvmiUGaxlbB83etUTQjrLIk-gvQQZiE5NSgJ63LCp5KtqFCZe8vlZxnOloErFIrebjFikxqAgwOO4i5ukJdl3KQ07YPRhwpuXmwxRf1vsiawXBvTMhy40SOeZ3mAyCRypQpQNa7NM3adCBwUtYKwHqiX3r1jQU0y57LvU_brBfLUL6JUpk3ri-LSpwPFarRXzZPJUu4-mQFIgrMmKCYbFk3AaEvvrJienfWSvFYLpIYA7lg-6EVYRcCAA`

### <a name="retry"></a>/retry

Wenn „CCMSetup.exe“ die Installationsdateien nicht herunterladen kann, verwenden Sie diesen Parameter, um das Wiederholungsintervall in Minuten anzugeben. Der Vorgang wird von CCMSetup wiederholt, bis die im Parameter [ **/downloadtimeout**](#downloadtimeout) angegebene Grenze erreicht ist.

Beispiel: `ccmsetup.exe /retry:20`  

### <a name="noservice"></a>/noservice

Dieser Parameter verhindert, dass CCMSetup als Dienst ausgeführt wird, was das Standardverhalten ist. Wenn CCMSetup als Dienst ausgeführt wird, erfolgt die Ausführung im Kontext des lokalen Systemkontos des Computers. Dieses Konto besitzt möglicherweise nicht ausreichend Rechte für den Zugriff auf die erforderlichen Netzwerkressourcen für die Installation. Mit **/noservice** wird „CCMSetup.exe“ im Kontext des Benutzerkontos ausgeführt, mit dem Sie die Installation starten.

Beispiel: `ccmsetup.exe /noservice`  

### <a name="service"></a>/service

Hiermit wird angegeben, dass CCMSetup mithilfe des lokalen Systemkontos als Dienst ausgeführt werden soll.  

> [!TIP]
> Wenn Sie zum Ausführen von „CCMSetup.exe“ mit dem Parameter **/service** ein Skript verwenden, wird „CCMSetup.exe“ nach dem Starten des Diensts beendet. Die Installationsdetails für das Skript werden möglicherweise nicht ordnungsgemäß gemeldet.

Beispiel: `ccmsetup.exe /service`  

### <a name="uninstall"></a>/uninstall

Mit diesem Parameter deinstallieren Sie den Configuration Manager-Client. Weitere Informationen finden Sie unter [Deinstallieren des Clients](../manage/manage-clients.md#BKMK_UninstalClient).

Beispiel: `ccmsetup.exe /uninstall`  

### <a name="logon"></a>/logon

Wenn eine Version des Clients bereits installiert wurde, gibt dieser Parameter an, dass die Clientinstallation angehalten werden sollte.  

Beispiel: `ccmsetup.exe /logon`  

### <a name="forcereboot"></a>/forcereboot

Mit diesem Parameter geben Sie an, dass ein Neustart des Clientcomputers erzwungen wird, wenn dies zum Abschließen der Installation erforderlich ist. Wenn dieser Parameter nicht angegeben ist, wird CCMSetup beendet, wenn ein Neustart erforderlich ist. Nach dem nächsten manuellen Neustart wird CCMSetup fortgesetzt.

Beispiel: `CCMSetup.exe /forcereboot`

### <a name="bitspriority"></a>/BITSPriority

Wenn das Gerät Clientinstallationsdateien über eine HTTP-Verbindung herunterlädt, verwenden Sie diesen Parameter zum Angeben der Downloadpriorität. Geben Sie einen der folgenden möglichen Werte an:

- `FOREGROUND`

- `HIGH`

- `NORMAL` (Standard)

- `LOW`

Beispiel: `ccmsetup.exe /BITSPriority:HIGH`

### <a name="downloadtimeout"></a>/downloadtimeout

Wenn CCMSetup die Clientinstallationsdateien nicht herunterladen kann, gibt dieser Parameter die maximale Zeitüberschreitung in Minuten an. Nach dieser Zeitüberschreitung versucht CCMSetup nicht mehr, die Installationsdateien herunterzuladen. Der Standardwert beträgt **1440** Minuten (ein Tag).

Verwenden Sie den Parameter [ **/retry**](#retry), um das Intervall zwischen den Wiederholungsversuchen anzugeben.

Beispiel: `ccmsetup.exe /downloadtimeout:100`

### <a name="usepkicert"></a>/UsePKICert

Geben Sie diesen Parameter an, damit der Client ein PKI-Clientauthentifizierungszertifikat verwenden soll. Wenn Sie diesen Parameter nicht einschließen oder der Client kein gültiges Zertifikat finden kann, verwendet er eine HTTP-Verbindung mit einem selbstsignierten Zertifikat.

Beispiel: `CCMSetup.exe /UsePKICert`  

> [!NOTE]
> In einigen Szenarios müssen Sie diesen Parameter nicht angeben, aber dennoch ein Clientzertifikat verwenden. Beispielsweise Clientpushinstallationen und softwareupdatebasierte Clientinstallationen. Verwenden Sie diesen Parameter, wenn Sie einen Client manuell installieren und den Parameter **/mp** mit einem HTTPS-fähigen Verwaltungspunkt verwenden.
>
> Geben Sie diesen Parameter ebenfalls an, wenn Sie einen Client für die reine Internetkommunikation installieren. Verwenden Sie die Eigenschaft **CCMALWAYSINF=1** gemeinsam mit den Eigenschaften für den internetbasierten Verwaltungspunkt (**CCMHOSTNAME**) und den Standortcode (**SMSSITECODE**). Weitere Informationen zur internetbasierten Clientverwaltung finden Sie unter [Überlegungen zur Clientkommunikation aus dem Internet oder einer nicht vertrauenswürdigen Gesamtstruktur](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).  

### <a name="nocrlcheck"></a>/NoCRLCheck

Gibt an, dass ein Client die Zertifikatssperrlisten nicht überprüfen sollte, wenn dieser über HTTPS unter Verwendung eines PKI-Zertifikats kommuniziert. Wenn Sie diesen Parameter nicht angeben, überprüft der Client die CRL, bevor eine HTTPS-Verbindung hergestellt wird. Weitere Informationen zur Client CRL-Prüfung finden Sie unter [Planen der PKI-Zertifikatsperrung](../../plan-design/security/plan-for-security.md#BKMK_PlanningForCRLs).

Beispiel: `CCMSetup.exe /UsePKICert /NoCRLCheck`  

### <a name="config"></a>/config

Dieser Parameter gibt den Namen einer Textdatei mit den Clientinstallationseigenschaften an.

- Wenn CCMSetup als Dienst ausgeführt wird, platzieren Sie diese Datei im CCMSetup-Systemordner: `%Windir%\Ccmsetup`.

- Wenn Sie den Parameter [ **/noservice**](#noservice) angeben, platzieren Sie diese Datei im selben Ordner wie „CCMSetup.exe“.

Beispiel: `CCMSetup.exe /config:"configuration file name.txt"`

Das richtige Dateiformat erhalten Sie mit der Datei **mobileclienttemplate.tcf** im Ordner `\bin\<platform>` des Configuration Manager-Installationsverzeichnisses auf dem Standortserver. Die Datei enthält Kommentare zu den Abschnitten und deren Verwendung. Geben Sie die Clientinstallationseigenschaften im Abschnitt `[Client Install]` nach folgendem Text ein: `Install=INSTALL=ALL`.

Beispielsabschnitt `[Client Install]`, Eintrag: `Install=INSTALL=ALL SMSSITECODE=ABC SMSCACHESIZE=100`  

### <a name="skipprereq"></a>/skipprereq

Dieser Parameter gibt an, dass „CCMSetup.exe“ die angegebene Voraussetzung nicht installiert. Sie können mehr als einen Wert eingeben. Verwenden Sie zum Trennen der Werte jeweils ein Semikolon (`;`).

Beispiele:

- `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe`

- `CCMSetup.exe /skipprereq:dotnetfx40_client_x86_x64.exe;windowsupdateagent30_x86.exe`

Weitere Informationen zu den Clientvoraussetzungen finden Sie unter [Voraussetzungen für Windows-Clients](prerequisites-for-deploying-clients-to-windows-computers.md).

### <a name="forceinstall"></a>/forceinstall

Gibt an, dass „CCMSetup.exe“ einen vorhandenen Client deinstalliert und einen neuen Client installiert.  

### <a name="excludefeatures"></a>/ExcludeFeatures

Dieser Parameter gibt an, dass „CCMSetup.exe“ das angegebene Feature nicht installiert.

Beispiel: `CCMSetup.exe /ExcludeFeatures:ClientUI` installiert das Softwarecenter nicht auf dem Client.  

> [!NOTE]  
> `ClientUI` ist der einzige Wert, der für den Parameter **/ExcludeFeatures** unterstützt wird.

## <a name="ccmsetupexe-return-codes"></a><a name="ccmsetupReturnCodes"></a> Rückgabecodes von „CCMSetup.exe“

Der Befehl „CCMSetup.exe“ gibt die im Folgenden aufgeführten Rückgabecodes aus. Zur Problembehandlung suchen Sie in `%WinDir%\ccmsetup\ccmsetup.log` auf dem Client nach dem Kontext und zusätzlichen Einzelheiten über Rückgabecodes.

|Rückgabecode|Bedeutung|  
|-----------|-------|  
|0|Erfolgreich|  
|6|Fehler|  
|7|Neustart erforderlich|  
|8|Setup wird bereits ausgeführt|  
|9|Fehler beim Auswerten der Voraussetzungen|  
|10|Fehler beim Überprüfen des Hashs für das Setup-Manifest|  

## <a name="ccmsetupmsi-properties"></a><a name="ccmsetupMsiProps"></a> Eigenschaften der Datei „Ccmsetup.msi“

Mit den folgenden Eigenschaften können Sie das Installationsverhalten von „ ccmsetup.msi“ ändern.

### <a name="ccmsetupcmd"></a>CCMSETUPCMD

Verwenden Sie die Eigenschaft „ccmsetup.*msi*“, um zusätzliche Befehlszeilenparameter und -eigenschaften an „ccmsetup.*exe*“ zu übergeben. Schließen Sie andere Parameter und Eigenschaften in Anführungszeichen (`"`) ein. Verwenden Sie diese Eigenschaft, wenn Sie einen Bootstrap für den Configuration Manager-Client mit der [Intune-MDM-Installationsmethode](plan/client-installation-methods.md#microsoft-intune-mdm-installation) durchführen.

Beispiel: `ccmsetup.msi CCMSETUPCMD="/mp:https://mp.contoso.com CCMHOSTNAME=mp.contoso.com"`

> [!Tip]
> Microsoft Intune beschränkt die Befehlszeile auf 1024 Zeichen.

## <a name="clientmsi-properties"></a><a name="clientMsiProps"></a> Eigenschaften der Datei „Client.msi“

Mit den folgenden Eigenschaften können Sie das Installationsverhalten von „client.msi“ ändern, das von „ccmsetup.exe“ installiert wird. Wenn Sie die [Clientpushinstallations-Methode](plan/client-installation-methods.md#client-push-installation) verwenden, geben Sie diese Eigenschaften auf der Registerkarte **Client** der **Eigenschaften der Clientpushinstallation** in der Configuration Manager-Konsole an.

### <a name="aadclientappid"></a>AADCLIENTAPPID

Gibt den Clientanwendungsbezeichner von Azure Active Directory (Azure AD) an. Sie erstellen oder importieren die Clientanwendung, wenn Sie [Azure-Dienste für die Cloudverwaltung konfigurieren](../../servers/deploy/configure/azure-services-wizard.md). Ein Azure-Administrator kann den Wert für diese Eigenschaft vom Azure-Portal abrufen. Weitere Informationen finden Sie unter [Abrufen der Anwendungs-ID](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in). Bei der Eigenschaft **AADCLIENTAPPID** ist diese Anwendungs-ID für den Anwendungstyp **Nativ** bestimmt.

Beispiel: `ccmsetup.exe AADCLIENTAPPID=aa28e7f1-b88a-43cd-a2e3-f88b257c863b`

### <a name="aadresourceuri"></a>AADRESOURCEURI

Gibt den Serveranwendungsbezeichner von Azure AD an. Sie erstellen oder importieren die Server-App, wenn Sie [Azure-Dienste für die Cloudverwaltung konfigurieren](../../servers/deploy/configure/azure-services-wizard.md). Bei der Erstellung der Server-App lautet diese Eigenschaft im Fenster „Serveranwendung erstellen“ **App-ID-URI**.

Ein Azure-Administrator kann den Wert für diese Eigenschaft vom Azure-Portal abrufen. Suchen Sie in **Azure Active Directory** unter **App-Registrierungen** nach der Server-App. Suchen Sie nach dem Anwendungstyp: **Web-App/API**. Öffnen Sie die App, wählen Sie **Einstellungen** aus, und wählen Sie dann **Eigenschaften** aus. Verwenden Sie den Wert **App-ID-URI** für die Eigenschaft **AADRESOURCEURI** für die Clientinstallation.

Beispiel: `ccmsetup.exe AADRESOURCEURI=https://contososerver`

### <a name="aadtenantid"></a>AADTENANTID

Gibt die ID des Azure AD-Mandanten an. Dieser Mandant wird bei der [Konfiguration der Azure-Dienste](../../servers/deploy/configure/azure-services-wizard.md) für Cloud Management mit Configuration Manager verknüpft. Führen Sie die folgenden Schritte aus, um den Wert für diese Eigenschaft abzurufen:

- Öffnen Sie auf einem Windows 10-Gerät, das mit demselben Azure AD-Mandanten verknüpft ist, eine Eingabeaufforderung.
- Führen Sie den folgenden Befehl aus: `dsregcmd.exe /status`
- Suchen Sie im Abschnitt „Gerätestatus“ nach dem Wert **TenantId**. Beispiel: `TenantId : 607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

  > [!Note]
  > Ein Azure-Administrator kann diesen Wert auch im Azure-Portal abrufen. Weitere Informationen finden Sie unter [Abrufen der Mandanten-ID](https://docs.microsoft.com/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in).

Beispiel: `ccmsetup.exe AADTENANTID=607b7853-6f6f-4d5d-b3d4-811c33fdd49a`

<!-- 
### AADTENANTNAME

Specifies the Azure AD tenant name. This tenant is linked to Configuration Manager when you [configure Azure services](../../servers/deploy/configure/azure-services-wizard.md) for Cloud Management. To obtain the value for this property, use the following steps:
- On a Windows 10 device that is joined to the same Azure AD tenant, open a command prompt.
- Run the following command: `dsregcmd.exe /status`
- In the Device State section, find the **TenantName** value. For example, `TenantName : Contoso`

Example: `ccmsetup.exe AADTENANTNAME=Contoso`
-->

### <a name="ccmadmins"></a>CCMADMINS  

Gibt eine oder mehrere Windows-Benutzerkonten oder -Gruppen an, denen der Zugriff auf die Clienteinstellungen und -richtlinien erlaubt werden soll. Diese Eigenschaft ist nützlich, wenn Sie über keine lokalen Administratoranmeldeinformationen auf dem Clientcomputer verfügen. Geben Sie eine Liste von Konten an, die Sie durch Semikolons (`;`) trennen.

Beispiel: `CCMSetup.exe CCMADMINS="domain\account1;domain\group1"`

### <a name="ccmallowsilentreboot"></a>CCMALLOWSILENTREBOOT

Lassen Sie den Computer bei Bedarf nach der Clientinstallation automatisch neu starten.

> [!IMPORTANT]  
> Wenn Sie diese Eigenschaft verwenden, wird der Computer ohne Warnung neu gestartet. Dieses Verhalten tritt auch dann auf, wenn ein Benutzer bei Windows angemeldet ist.

Beispiel: `CCMSetup.exe CCMALLOWSILENTREBOOT`

### <a name="ccmalwaysinf"></a>CCMALWAYSINF

Um anzugeben, dass der Client immer internetbasiert ist und keine Verbindung mit dem Intranet herstellt, setzen Sie diesen Wert auf `1`. Der angezeigte Clientverbindungstyp lautet **Immer Internet**.  

Verwenden Sie diese Eigenschaft mit [**CCMHOSTNAME**](#ccmhostname), die den FQDN des internetbasierten Verwaltungspunkts angibt. Verwenden Sie ihn auch mit dem CCMSetup-Parameter [ **/UsePKICert**](#usepkicert) und dem Standortcode ([**SMSSITECODE**](#smssitecode)).

Weitere Informationen zur internetbasierten Clientverwaltung finden Sie unter [Überlegungen zur Clientkommunikation aus dem Internet oder einer nicht vertrauenswürdigen Gesamtstruktur](../../plan-design/hierarchy/communications-between-endpoints.md#BKMK_clientspan).

Beispiel: `CCMSetup.exe /UsePKICert CCMALWAYSINF=1 CCMHOSTNAME=SERVER3.CONTOSO.COM SMSSITECODE=ABC`

### <a name="ccmcertissuers"></a>CCMCERTISSUERS

Verwenden Sie diese Eigenschaft, um die Liste der Zertifikataussteller anzugeben. Diese Liste enthält Zertifikatinformationen für die vertrauenswürdigen Stammzertifizierungsstellen, denen der Configuration Manager-Standort vertraut.  

Bei dieser Suche nach Übereinstimmungen für Antragstellerattribute im Stamm-Zertifizierungsstellenzertifikat wird die Groß-/Kleinschreibung beachtet. Trennen Sie Attribute durch ein Komma (`,`) oder ein Semikolon (`;`). Mehrere Stamm-Zertifizierungsstellenzertifikate können mithilfe einer Trennlinie (`|`) angegeben werden.

Beispiel: `CCMCERTISSUERS="CN=Contoso Root CA; OU=Servers; O=Contoso, Ltd; C=US | CN=Litware Corporate Root CA; O=Litware, Inc."`

> [!TIP]
> Verwenden Sie den Wert des Attributs **CertificateIssuers** in der Datei **mobileclient.tcf** für den Standort. Diese Datei befindet sich auf dem Standortserver im Configuration Manager-Installationsverzeichnis im Ordner `\bin\<platform>`.

Weitere Informationen zur Liste der Zertifikataussteller und deren Verwendung durch Clients beim Zertifikatauswahlvorgang finden Sie unter [Planen der PKI-Clientzertifikatauswahl](../../plan-design/security/plan-for-security.md#BKMK_PlanningForClientCertificateSelection).

### <a name="ccmcertsel"></a>CCMCERTSEL

Wenn der Client über mehr als ein Zertifikat für die HTTPS-Kommunikation verfügt, gibt diese Eigenschaft die Kriterien für die Auswahl eines gültigen Clientauthentifizierungszertifikats an.

Verwenden Sie die folgenden Schlüsselwörter, um den Zertifikatantragsteller oder alternativen Antragstellernamen zu durchsuchen:

- **Betreff**: Genaue Übereinstimmung suchen
- **SubjectStr**: Partielle Übereinstimmung suchen

Beispiele:

- `CCMCERTSEL="Subject:computer1.contoso.com"`: Sucht nach einem Zertifikat, das im Antragstellernamen oder im alternativen Antragstellernamen genau mit dem Computernamen `computer1.contoso.com` übereinstimmt.

- `CCMCERTSEL="SubjectStr:contoso.com"`: Sucht nach einem Zertifikat, das im Antragstellernamen oder alternativen Antragstellernamen `contoso.com` aufweist.

Verwenden Sie das Schlüsselwort **SubjectAttr**, um im Antragstellernamen oder alternativen Antragstellernamen nach den Attributen für Objektbezeichner (OID) oder Distinguished Name zu suchen.

Beispiele:

- `CCMCERTSEL="SubjectAttr:2.5.4.11 = Computers"`: Sucht nach dem Organisationseinheitenattribut, das als Objektbezeichner angegeben wird und `Computers` heißt.

- `CCMCERTSEL="SubjectAttr:OU = Computers"`: Sucht nach dem Organisationseinheitenattribut, das als Distinguished Name angegeben wird und `Computers` heißt.

> [!IMPORTANT]
> Wenn Sie den Antragstellernamen verwenden, muss beim Schlüsselwort **Subject** die Groß-/Kleinschreibung beachtet werden, bei **SubjectStr** dagegen nicht.
>
> Wenn Sie den alternativen Antragstellernamen verwenden, wird die Groß-/Kleinschreibung sowohl bei den Schlüsselwörtern **Subject** und **SubjectStr** beachtet.

Eine vollständige Liste der Attribute, die für die Zertifikatauswahl verwendet werden können, finden Sie unter [Unterstützte Attributwerte für die PKI-Zertifikatauswahlkriterien](#BKMK_attributevalues).

Wenn mehr als ein Zertifikat der Suche entspricht und Sie [**CCMFIRSTCERT**](#ccmfirstcert) auf `1` setzen, wählt das Clientinstallationsprogramm das Zertifikat mit der längsten Gültigkeitsdauer aus.

### <a name="ccmcertstore"></a>CCMCERTSTORE

Wenn das Clientinstallationsprogramm kein gültiges Zertifikat im **persönlichen** Standardzertifikatspeicher für den Computer finden kann, verwenden Sie diese Eigenschaft, um einen alternativen Zertifikatspeichernamen anzugeben.

Beispiel: `CCMSetup.exe /UsePKICert CCMCERTSTORE="ConfigMgr"`  

### <a name="ccmdebuglogging"></a>CCMDEBUGLOGGING

Diese Eigenschaft ermöglicht die Debugprotokollierung bei der Clientinstallation. Mit dieser Eigenschaft protokolliert der Client Basisinformationen für die Problembehandlung. Verwenden Sie diese Eigenschaft nach Möglichkeit nicht an Produktionsstandorten. Es kann zu einer übermäßigen Protokollierung kommen, wodurch es möglicherweise schwierig wird, die relevanten Informationen in den Protokolldateien zu finden. Aktivieren Sie außerdem [**CCMENABLELOGGING**](#ccmenablelogging).

Unterstützte Werte:

- `0`: Deaktivieren der Debugprotokollierung (Standard)
- `1`: Aktivieren der Debugprotokollierung

Beispiel: `CCMSetup.exe CCMDEBUGLOGGING=1`  

Weitere Informationen zu Protokolldateien finden Sie unter [Grundlegendes zu Protokolldateien](../../plan-design/hierarchy/about-log-files.md).

### <a name="ccmenablelogging"></a>CCMENABLELOGGING

Die Protokollierung wird von Configuration Manager standardmäßig aktiviert.

Unterstützte Werte:

- `TRUE`: Aktivieren der Protokollierung (Standard)
- `FALSE`: Deaktivieren der Protokollierung

Beispiel: `CCMSetup.exe CCMENABLELOGGING=TRUE`  

Weitere Informationen zu Protokolldateien finden Sie unter [Grundlegendes zu Protokolldateien](../../plan-design/hierarchy/about-log-files.md).

### <a name="ccmevalinterval"></a>CCMEVALINTERVAL

Die Ausführungshäufigkeit des Tools zur Clientintegritätsauswertung (ccmeval.exe) in Minuten. Geben Sie einen ganzzahligen Wert zwischen `1` und `1440` ein. Standardmäßig wird ccmeval einmal täglich ausgeführt (1440 Minuten).

Beispiel: `CCMSetup.exe CCMEVALINTERVAL=1440`

Weitere Informationen zur Clientintegritätsauswertung finden Sie unter [Überwachen von Clients](../manage/monitor-clients.md#bkmk_health).

### <a name="ccmevalhour"></a>CCMEVALHOUR

Die Stunde während des Tages, wenn das Tools zur Clientintegritätsauswertung (ccmeval.exe) ausgeführt wird. Geben Sie einen ganzzahligen Wert von `0` (Mitternacht) bis `23` (23:00 Uhr) an. Standardmäßig wird das Tool um Mitternacht ausgeführt.

Weitere Informationen zur Clientintegritätsauswertung finden Sie unter [Überwachen von Clients](../manage/monitor-clients.md#bkmk_health).

### <a name="ccmfirstcert"></a>CCMFIRSTCERT

Wenn Sie diese Eigenschaft auf `1` festlegen, wählt der Client das PKI-Zertifikat mit der längsten Gültigkeitsdauer aus.

Beispiel: `CCMSetup.exe /UsePKICert CCMFIRSTCERT=1`

### <a name="ccmhostname"></a>CCMHOSTNAME

Wenn der Client über das Internet verwaltet wird, gibt diese Eigenschaft den FQDN des internetbasierten Verwaltungspunkts an.  

Geben Sie diese Option nicht mit der Installationseigenschaft **SMSSITECODE=AUTO** an. Direktes Zuweisen von internetbasierten Clients zu einem internetbasierten Standort.

Beispiel: `CCMSetup.exe /UsePKICert CCMHOSTNAME="SMSMP01.corp.contoso.com"`  

Diese Eigenschaft kann die Adresse eines Cloudverwaltungsgateways (CMG) angeben. Führen Sie die folgenden Schritte aus, um den Wert für diese Eigenschaft abzurufen:

- Erstellen Sie ein CMG. Weitere Informationen finden Sie unter [Einrichten eines CMG](../manage/cmg/setup-cloud-management-gateway.md).
- Öffnen Sie auf einem aktiven Client als Administrator eine Windows PowerShell-Eingabeaufforderung.
- Führen Sie den folgenden Befehl aus:

    ```PowerShell
    (Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP`
    ```

- Verwenden Sie den zurückgegebenen Wert wie bei der Eigenschaft **CCMHOSTNAME**.

Beispiel: `ccmsetup.exe CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72057598037248100`

> [!Important]
> Wenn Sie die Adresse einer CMG für die Eigenschaft **CCMHOSTNAME** angeben, fügen Sie kein Präfix wie `https://` an. Verwenden Sie dieses Präfix nur mit der **/mp**-URL eines CMG.

### <a name="ccmhttpport"></a>CCMHTTPPORT

Gibt den Port an, den der Client bei der Kommunikation mit den Standortsystemservern über HTTP verwenden soll. Der Standardwert ist `80`.

Beispiel: `CCMSetup.exe CCMHTTPPORT=80`

### <a name="ccmhttpsport"></a>CCMHTTPSPORT

Gibt den Port an, den der Client bei der Kommunikation mit den Standortsystemservern über HTTPS verwenden soll. Der Standardwert ist `443`.

Beispiel: `CCMSetup.exe /UsePKICert CCMHTTPSPORT=443`

### <a name="ccminstalldir"></a>CCMINSTALLDIR

Verwenden Sie diese Eigenschaft, um den Ordner für die Installation der Configuration Manager-Clientdateien festzulegen. Standardmäßig wird `%WinDir%\CCM` verwendet.

> [!TIP]
> Unabhängig davon, wo Sie die Clientdateien installieren, wird immer die Datei **ccmcore.dll** im Ordner `%WinDir%\System32` installiert. Bei einem 64-Bit-Betriebssystem wird eine Kopie der Datei „ccmcore.dll“ im Ordner `%WinDir%\SysWOW64` installiert. Diese Datei unterstützt 32-Bit-Anwendungen, welche die 32-Bit-Version der Client-APIs vom Configuration Manager SDK verwenden.

Beispiel: `CCMSetup.exe CCMINSTALLDIR="C:\ConfigMgr"`

### <a name="ccmloglevel"></a>CCMLOGLEVEL

Verwenden Sie diese Eigenschaft, um die Detailebene für das Schreiben in die Configuration Manager-Protokolldateien anzugeben.

Unterstützte Werte:

- `0`: Ausführlich
- `1`: Standard
- `2`: Warnungen und Fehler
- `3`: Nur Fehler

Beispiel: `CCMSetup.exe CCMLOGLEVEL=0`

Weitere Informationen zu Protokolldateien finden Sie unter [Grundlegendes zu Protokolldateien](../../plan-design/hierarchy/about-log-files.md).

### <a name="ccmlogmaxhistory"></a>CCMLOGMAXHISTORY

Wenn eine Configuration Manager-Protokolldatei die maximale Größe erreicht, benennt der Client diese als Sicherungsdatei um und erstellt eine neue Protokolldatei. Diese Eigenschaft gibt an, wie viele vorherige Versionen der Protokolldatei beibehalten werden sollen. Der Standardwert lautet `1`. Wenn Sie den Wert auf `0` festlegen, speichert der Client keinen Protokolldateiverlauf.

Beispiel: `CCMSetup.exe CCMLOGMAXHISTORY=5`

Weitere Informationen zu Protokolldateien finden Sie unter [Grundlegendes zu Protokolldateien](../../plan-design/hierarchy/about-log-files.md).

### <a name="ccmlogmaxsize"></a>CCMLOGMAXSIZE

Diese Eigenschaft gibt die maximale Protokolldateigröße in Bytes an. Wenn ein Protokoll die angegebene Größe erreicht, benennt der Client diese als Verlaufsdatei um und erstellt eine neue Datei. Die Standardgröße beträgt 250.000 Bytes, und die Mindestgröße beträgt 10.000 Bytes.

Beispiel: `CCMSetup.exe CCMLOGMAXSIZE=300000` (300.000 Bytes)

### <a name="disablesiteopt"></a>DISABLESITEOPT

Setzen Sie diese Eigenschaft auf `TRUE`, um Administratoren daran zu hindern, den zugewiesenen Standort in den Einstellungen von Configuration Manager zu ändern.

Beispiel: **CCMSetup.exe DISABLESITEOPT=TRUE**

### <a name="disablecacheopt"></a>DISABLECACHEOPT

Wenn diese Eigenschaft auf TRUE festgelegt ist, können Administratoren die Einstellungen für Clientcacheordner in den Einstellungen von **Configuration Manager** nicht mehr ändern.  

Beispiel: `CCMSetup.exe DISABLECACHEOPT=TRUE`  

### <a name="dnssuffix"></a>DNSSUFFIX

Geben Sie eine DNS-Domäne für Clients an, um Verwaltungspunkte zu suchen, die Sie in DNS veröffentlichen. Nachdem der Client einen Verwaltungspunkt gefunden hat, informiert er diesen über andere Verwaltungspunkte in der Hierarchie. Dieses Verhalten bedeutet, dass der Verwaltungspunkt, den der Client über den DNS findet, jeder in der Hierarchie sein kann.

> [!NOTE]
> Sie müssen diese Eigenschaft nicht angeben, wenn der Client der gleichen Domäne angehört wie ein veröffentlichter Verwaltungspunkt. In diesem Fall wird die Clientdomäne automatisch verwendet, um DNS nach Verwaltungspunkten zu durchsuchen.

Weitere Informationen zur DNS-Veröffentlichung als Dienstidentifizierungsmethode für Configuration Manager-Clients finden Sie unter [Dienstidentifizierung und wie Clients den ihnen zugewiesenen Verwaltungspunkt ermitteln](../../plan-design/hierarchy/understand-how-clients-find-site-resources-and-services.md#BKMK_Plan_Service_Location).

> [!NOTE]  
> Standardmäßig wird die DNS-Veröffentlichung von Configuration Manager nicht aktiviert.

Beispiel: `CCMSetup.exe SMSSITECODE=ABC DNSSUFFIX=contoso.com`

### <a name="fsp"></a>FSP

Geben Sie den Fallbackstatuspunkt an, von dem die von Configuration Manager-Clients gesendeten Zustandsmeldungen empfangen und verarbeitet werden.

Weitere Informationen finden Sie unter [Bestimmen, ob ein Fallbackstatuspunkt installiert werden sollte](plan/determine-the-site-system-roles-for-clients.md#fallback-status-point).

Beispiel: `CCMSetup.exe FSP=SMSFP01`  

### <a name="ignoreappvversioncheck"></a>IGNOREAPPVVERSIONCHECK

Wenn Sie diese Eigenschaft auf `TRUE` festlegen, prüft das Clientinstallationsprogramm nicht, ob die mindestens erforderliche Version von Microsoft Application Virtualization (App-V) vorhanden ist.

> [!IMPORTANT]  
> Wenn Sie den Configuration Manager-Client installieren, ohne App-V zu installieren, können Sie keine [virtuellen Anwendungen bereitstellen](../../../apps/get-started/deploying-app-v-virtual-applications.md).

Beispiel: `CCMSetup.exe IGNOREAPPVVERSIONCHECK=TRUE`

### <a name="notifyonly"></a>NOTIFYONLY

Wenn Sie diese Eigenschaft aktivieren, meldet der Client den Status, aber die gefundenen Probleme werden nicht behoben.

Beispiel: `CCMSetup.exe NOTIFYONLY=TRUE`

Weitere Informationen finden Sie unter [Konfigurieren des Clientstatus](configure-client-status.md).

### <a name="provisionts"></a>PROVISIONTS

<!--5526972-->

Ab Version 2002 können Sie diese Eigenschaft verwenden, um eine Tasksequenz auf einem Client zu starten, nachdem dieser sich erfolgreich beim Standort registriert hat.

Beispielsweise können Sie ein neues Windows 10-Gerät mit Windows Autopilot bereitstellen, es automatisch für Microsoft Intune registrieren und dann den Konfigurations-Manager-Client für die Co-Verwaltung installieren. Wenn Sie diese neue Option angeben, führt der neu bereitgestellte Client eine Tasksequenz aus. Dieser Prozess bietet zusätzliche Flexibilität beim Installieren von Anwendungen und Softwareupdates oder beim Konfigurieren von Einstellungen.

Führen Sie den folgenden Vorgang aus:

1. [Erstellen Sie eine Tasksequenz, die nicht der Bereitstellung des Betriebssystems gilt](../../../osd/deploy-use/create-a-task-sequence-for-non-operating-system-deployments.md), um Apps und Softwareupdates zu installieren und Einstellungen zu konfigurieren.

1. [Stellen Sie diese Tasksequenz in der neu integrierten Sammlung bereit](../../../osd/deploy-use/deploy-a-task-sequence.md), **Alle Bereitstellungsgeräte**. Beachten Sie die Bereitstellungs-ID der Tasksequenz, z. B. `PRI20001`.

1. [Installieren Sie den Konfigurations-Manager-Client](deploy-clients-to-windows-computers.md#BKMK_Manual) auf einem Gerät, und schließen Sie die folgende Eigenschaft ein: `PROVISIONTS=PRI20001`. Legen Sie den Wert dieser Eigenschaft als Bereitstellungs-ID der Tasksequenz fest.

    - Wenn Sie den Client von Intune während der Co-Verwaltungsregistrierung installieren, finden Sie weitere Informationen unter [Vorbereiten von internetbasierten Geräten für die Co-Verwaltung](../../../comanage/how-to-prepare-Win10.md).

      > [!NOTE]
      > Für diese Methode sind möglicherweise zusätzliche Voraussetzungen erforderlich. Beispielsweise die Registrierung des Standorts bei Azure Active Directory oder das Erstellen eines inhaltsfähigen Cloudverwaltungsgateways.

Nachdem der Client installiert und ordnungsgemäß für den Standort registriert wurde, wird die Tasksequenz gestartet, auf die verwiesen wird. Wenn die Clientregistrierung fehlschlägt, wird die Tasksequenz nicht gestartet.

### <a name="resetkeyinformation"></a>RESETKEYINFORMATION

Wenn ein Client den falschen vertrauenswürdigen Configuration Manager-Stammschlüssel aufweist, kann er keine Verbindung mit dem vertrauenswürdigen Verwaltungspunkt herstellen, um eine gültige Kopie des neuen vertrauenswürdigen Stammschlüssels abzurufen. Entfernen Sie den alten vertrauenswürdigen Stammschlüssel mithilfe dieser Eigenschaft. Dieser Fall tritt möglicherweise ein, wenn Sie einen Client aus einer Standorthierarchie in eine andere verschieben. Diese Eigenschaft gilt für Clients, von denen HTTP- und HTTPS-Clientkommunikation verwendet wird. Weitere Informationen finden Sie unter [Planning for the trusted root key (Planen des vertrauenswürdigen Stammschlüssels)](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).

Beispiel: `CCMSetup.exe RESETKEYINFORMATION=TRUE`  

### <a name="sitereassign"></a>SITEREASSIGN

Ermöglicht eine automatische Standortneuzuordnung für Clientupgrades bei Verwendung mit [SMSSITECODE=AUTO](#smssitecode).

Beispiel: `CCMSetup.exe SMSSITECODE=AUTO SITEREASSIGN=TRUE`

### <a name="smscachedir"></a>SMSCACHEDIR

Hiermit wird der Speicherort des Clientcacheordners angegeben. Standardmäßig ist der Speicherort `%WinDir%\ccmcache`.

Beispiel: `CCMSetup.exe SMSCACHEDIR="C:\Temp"`  

Verwenden Sie diese Eigenschaft mit [**SMSCACHEFLAGS**](#smscacheflags), um den Speicherort des Clientcacheordners zu steuern. So installieren Sie z.B. den Clientcacheordner auf dem größten verfügbaren Clientlaufwerk: `CCMSetup.exe SMSCACHEDIR=Cache SMSCACHEFLAGS=MAXDRIVE`

### <a name="smscacheflags"></a>SMSCACHEFLAGS

Verwenden Sie diese Eigenschaft, um weitere Installationsdetails für den Clientcacheordner anzugeben. Sie können die **SMSCACHEFLAGS**-Eigenschaften einzeln oder zusammen durch Semikolons (`;`) getrennt verwenden.

Wenn Sie diese Eigenschaft nicht einschließen:

- Der Client installiert den Cacheordner gemäß der Eigenschaft [**SMSCACHEDIR**](#smscachedir).
- Der Ordner ist nicht komprimiert.
- Der Client verwendet die Eigenschaft [**SMSCACHESIZE**](#smscachesize) als Größenbeschränkung des Caches in MB.

Wenn Sie ein Upgrade für einen vorhandenen Client durchführen, wird diese Eigenschaft vom Clientinstallationsprogramm ignoriert.

#### <a name="values-for-the-smscacheflags-property"></a>Werte für die Eigenschaft „SMSCACHEFLAGS“

- **PERCENTDISKSPACE**: Legt die Cachegröße als Prozentsatz des *gesamten* Speicherplatzes auf dem Datenträger fest. Wenn Sie diese Eigenschaft angeben, legen Sie [**SMSCACHESIZE**](#smscachesize) auf einen Prozentwert fest.

- **PERCENTFREEDISKSPACE**: Gibt die Cachegröße als Prozentsatz des *freien* Speicherplatzes auf dem Datenträger an. Wenn Sie diese Eigenschaft angeben, legen Sie [**SMSCACHESIZE**](#smscachesize) auf einen Prozentwert fest. Der Datenträger verfügt beispielsweise über 10 MB freien Speicherplatz, und Sie geben `SMSCACHESIZE=50` an. Das Clientinstallationsprogramm legt die Cachegröße auf 5 MB fest. Diese Eigenschaft kann nicht in Verbindung mit der Eigenschaft **PERCENTDISKSPACE** verwendet werden.

- **MAXDRIVE**: Installieren Sie den Cache auf dem größten verfügbaren Datenträger. Wenn Sie einen Pfad mit der Eigenschaft [**SMSCACHEDIR**](#smscachedir) angeben, wird dieser Wert vom Clientinstallationsprogramm ignoriert.

- **MAXDRIVESPACE**: Installieren Sie den Cache auf dem Laufwerk mit dem meisten freien Speicherplatz. Wenn Sie einen Pfad mit der Eigenschaft [**SMSCACHEDIR**](#smscachedir) angeben, wird dieser Wert vom Clientinstallationsprogramm ignoriert.

- **NTFSONLY**: Installieren Sie den Cache nur auf einem NTFS-formatierten Laufwerk. Wenn Sie einen Pfad mit der Eigenschaft [**SMSCACHEDIR**](#smscachedir) angeben, wird dieser Wert vom Clientinstallationsprogramm ignoriert.

- **COMPRESS**: Speichert den Cache in komprimierter Form.

- **FAILIFNOSPACE**: Wenn nicht genügend Speicherplatz vorhanden ist, um den Cache zu installieren, entfernen Sie den Configuration Manager-Client.

Beispiel: `CCMSetup.exe SMSCACHEFLAGS=NTFSONLY;COMPRESS`

### <a name="smscachesize"></a>SMSCACHESIZE

> [!IMPORTANT]
> Für die Angabe der Größe des Clientcacheordners sind Clienteinstellungen verfügbar. Das Hinzufügen dieser Clienteinstellungen ersetzt SMSCACHESIZE als client.msi-Eigenschaft, um die Größe des Clientcaches anzugeben. Weitere Informationen zu den Clienteinstellungen finden Sie unter [client settings for cache size](about-client-settings.md#client-cache-settings) (Clienteinstellungen für Cachegröße).  

Wenn Sie ein Upgrade für einen vorhandenen Client durchführen, wird diese Einstellung vom Clientinstallationsprogramm ignoriert. Der Client ignoriert auch die Cachegröße beim Herunterladen von Softwareupdates.

Beispiel: `CCMSetup.exe SMSCACHESIZE=100`

> [!NOTE]  
> Wenn Sie einen Client neu installieren, können Sie **SMSCACHESIZE** und **SMSCACHEFLAGS** nicht verwenden, um die Cachegröße auf einen niedrigeren Wert als vorher festzulegen. Die vorherige Größe ist der minimale Wert.

### <a name="smsconfigsource"></a>SMSCONFIGSOURCE

Mit dieser Eigenschaft geben Sie den Speicherort und die Reihenfolge an, die das Clientinstallationsprogramm für die Überprüfung der Konfigurationseinstellungen verwendet. Es handelt sich um eine Zeichenfolge mit einem oder mehreren Zeichen, die jeweils eine spezielle Konfigurationsquelle angeben:

- `R`: Überprüfung der Konfigurationseinstellungen in der Registrierung.

  Weitere Informationen finden Sie unter [Bereitstellen von Clientinstallationseigenschaften](deploy-clients-to-windows-computers.md#BKMK_Provision).

- `P`: Überprüfung der Konfigurationseinstellungen in den Installationseigenschaften der Befehlszeile.

- `M`: Überprüfung der vorhandenen Einstellungen beim Upgrade eines älteren Clients.

- `U`: Upgrade des installierten Clients auf eine neuere Version unter Verwendung des zugewiesenen Standortcodes.

Standardmäßig verwendet das Clientinstallationsprogramm `PU`. Zuerst werden die Installationseigenschaften (`P`) und dann die vorhandenen Einstellungen (`U`) überprüft.  

Beispiel: `CCMSetup.exe SMSCONFIGSOURCE=RP`

<!--
### SMSDIRECTORYLOOKUP

Specifies whether the client can use Windows Internet Name Service (WINS) to find a management point that accepts HTTP connections. Clients use this method when they can't find a management point in Active Directory Domain Services or in DNS.  

 This property doesn't affect whether the client uses WINS for name resolution.  

 You can configure two different modes for this property:  

-   NOWINS: This value is the most secure setting for this property and prevents clients from finding a management point in WINS. When you use this setting, clients must have an alternative method to locate a management point on the intranet, such as Active Directory Domain Services or by using DNS publishing.  

-   WINSSECURE (default): In this mode, a client that uses HTTP communication can use WINS to find a management point. However, the client must have a copy of the trusted root key before it can successfully connect to the management point. For more information, see [Planning for the trusted root key](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).  

Example: `CCMSetup.exe SMSDIRECTORYLOOKUP=NOWINS`  
-->

### <a name="smsmp"></a>SMSMP

Hiermit wird ein erster Verwaltungspunkt für die Verwendung durch den Configuration Manager-Client angegeben.  

> [!IMPORTANT]  
> Wenn der Verwaltungspunkt nur Clientverbindungen über HTTPS akzeptiert, stellen Sie dem Namen des Verwaltungspunkts das Präfix `https://` voran.

Beispiele:

- `CCMSetup.exe SMSMP=smsmp01.contoso.com`

- `CCMSetup.exe SMSMP=https://smsmp01.contoso.com`  

### <a name="smspublicrootkey"></a>SMSPUBLICROOTKEY

Wenn der Client den vertrauenswürdigen Stammschlüssel von Configuration Manager aus Active Directory Domain Services nicht abrufen kann, verwenden Sie diese Eigenschaft, um den Schlüssel anzugeben. Diese Eigenschaft gilt für Clients, von denen HTTP- und HTTPS-Kommunikation verwendet wird. Weitere Informationen finden Sie unter [Planning for the trusted root key (Planen des vertrauenswürdigen Stammschlüssels)](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).

Beispiel: `CCMSetup.exe SMSPUBLICROOTKEY=<keyvalue>`

> [!TIP]
> Legen Sie den Wert für den vertrauenswürdigen Stammschlüssel des Standorts aus der Datei „mobileclient.tcf“ auf dem Standortserver ab. Weitere Informationen finden Sie unter [Vorabbereitstellung des vertrauenswürdigen Stammschlüssels an einen Client mithilfe einer Datei](../../plan-design/security/plan-for-security.md#bkmk_trk-provision-file).

### <a name="smsrootkeypath"></a>SMSROOTKEYPATH

Mit dieser Eigenschaft installieren Sie den vertrauenswürdigen Configuration Manager-Stammschlüssel neu. Sie gibt den vollständigen Pfad und den Dateinamen einer Datei mit dem vertrauenswürdigen Stammschlüssel an. Diese Eigenschaft gilt für Clients, von denen HTTP- und HTTPS-Clientkommunikation verwendet wird. Weitere Informationen finden Sie unter [Planning for the trusted root key (Planen des vertrauenswürdigen Stammschlüssels)](../../plan-design/security/plan-for-security.md#BKMK_PlanningForRTK).

Beispiel: `CCMSetup.exe SMSROOTKEYPATH=C:\folder\trk`

### <a name="smssigncert"></a>SMSSIGNCERT

Gibt den vollständigen Pfad und Namen des exportierten selbstsignierten Zertifikats auf dem Standortserver an. Der Standortserver speichert dieses Zertifikat im **SMS**-Zertifikatspeicher. Es weist den Antragstellernamen **Site Server** und den Anzeigenamen **Site Server Signing Certificate** auf.

Beispiel: `CCMSetup.exe /UsePKICert SMSSIGNCERT=C:\folder\smssign.cer`

### <a name="smssitecode"></a>SMSSITECODE

Diese Eigenschaft gibt einen Configuration Manager-Standort an, dem Sie den Client zuweisen. Dieser Wert kann entweder ein dreistelliger Standortcode oder das Wort `AUTO` sein. Wenn Sie `AUTO` angeben oder Sie diese Eigenschaft nicht angeben, wird vom Client versucht, die Standortzuweisung anhand der Active Directory-Domänendienste oder anhand eines angegebenen Verwaltungspunkts zu bestimmen. Um `AUTO` für Clientupgrades festzulegen, müssen Sie ferner [SITEREASSIGN=TRUE](#sitereassign) setzen.

> [!NOTE]  
> Wenn Sie auch einen internetbasierten Verwaltungspunkt mit der Eigenschaft [**CCMHOSTNAME**](#ccmhostname) angeben, verwenden Sie `AUTO` nicht mit **SMSSITECODE**. Weisen Sie den Client direkt dem Standort zu, indem Sie den Standortcode angeben.

Beispiel: `CCMSetup.exe SMSSITECODE=XZY`

## <a name="attribute-values-for-certificate-selection-criteria"></a><a name="BKMK_attributevalues"></a> Attributwerte für Zertifikatauswahlkriterien

Configuration Manager unterstützt die folgenden Attributwerte für die PKI-Zertifikatauswahlkriterien:

|OID-Attribut|DN-Attribut (Distinguished Name)|Attributdefinition|
|-------------|----------------------------|--------------------|
|0.9.2342.19200300.100.1.25|DC|Domänenkomponente|  
|1.2.840.113549.1.9.1|E oder E-mail|E-Mail-Adresse|  
|2.5.4.3|CN|Allgemeiner Name|  
|2.5.4.4|SN|Antragstellername|  
|2.5.4.5|SERIALNUMBER|Seriennummer|  
|2.5.4.6|C|Ländercode|  
|2.5.4.7|L|Ort|  
|2.5.4.8|S oder ST|Name des Bundeslands bzw. des Kantons|  
|2.5.4.9|STREET|Straße|  
|2.5.4.10|O|Organisationsname|  
|2.5.4.11|OU|Organisationseinheit|  
|2.5.4.12|T oder Title|Titel|  
|2.5.4.42|G oder GN oder GivenName|Vorname|  
|2.5.4.43|I oder Initials|Initialen|  
|2.5.29.17|(kein Wert)|Alternativer Antragstellername|  
