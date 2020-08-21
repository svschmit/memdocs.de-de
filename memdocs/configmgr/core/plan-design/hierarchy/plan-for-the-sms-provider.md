---
title: Planen des SMS-Anbieters
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über die Standortsystemrolle „SMS-Anbieter“ in Configuration Manager.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5d5d6273-0d8a-43c7-865a-cdb1736dcae3
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: c83d0da07474c8b078ee226d249b73f00562e0f5
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700162"
---
# <a name="plan-for-the-sms-provider"></a>Planen des SMS-Anbieters

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie zum Verwalten von Configuration Manager eine Configuration Manager-Konsole, die eine Verbindung mit einer Instanz des **SMS-Anbieters** herstellt. Standardmäßig wird ein SMS-Anbieter auf dem Standortserver installiert, wenn Sie einen Standort der zentralen Verwaltung oder einen primären Standort installieren.

## <a name="about-the-sms-provider"></a><a name="BKMK_PlanSMSProv"></a> Informationen zum SMS-Anbieter  

Der SMS-Anbieter ist ein Anbieter der Windows-Verwaltungsinstrumentation (Windows Management Instrumentation; WMI), über den der Configuration Manager-Datenbank an einem Standort **Lese-** und **Schreibzugriff** erteilt wird.  

- Für jeden Standort der zentralen Verwaltung und für jeden primären Standort ist mindestens ein SMS-Anbieter erforderlich. Sie können bei Bedarf zusätzliche Anbieter installieren.  

- Die Sicherheitsgruppe **SMS-Administratoren** ermöglicht den Zugriff auf den SMS-Anbieter. Configuration Manager erstellt diese Gruppe automatisch auf dem Standortserver und auf jedem Computer, auf dem Sie eine Instanz des SMS-Anbieters installieren. Weitere Informationen finden Sie unter [SMS-Administratoren](accounts.md#sms-admins).  

- Sekundäre Standorte unterstützen die Rolle „SMS-Anbieter“ nicht.  

Configuration Manager-Administratoren verwenden einen SMS-Anbieter für den Zugriff auf Informationen, die in der Datenbank gespeichert sind. Hierzu können Administratoren die Configuration Manager-Konsole, den Ressourcen-Explorer, Tools und benutzerdefinierte Skripts verwenden. Es gibt keine Interaktion zwischen dem SMS-Anbieter und Konfigurations-Manager-Clients. Wenn für eine Configuration Manager-Konsole eine Verbindung zu einem Standort hergestellt wird, dann erfolgt eine Abfrage von WMI auf dem Standortserver, um eine verwendbare Instanz des SMS-Anbieters zu finden.  

Der SMS-Anbieter unterstützt die Durchsetzung der Configuration Manager-Sicherheit. Es werden nur die Informationen zurückgegeben, zur deren Anzeige der Konsolenbenutzer berechtigt ist.  

Der SMS-Anbieter bietet auch API-Interoperabilitätszugriff über HTTPS, der als **Verwaltungsdienst** bezeichnet wird. Diese REST-API kann anstelle eines benutzerdefinierten Webdiensts verwendet werden, um auf Informationen vom Standort zuzugreifen. Weitere Informationen finden Sie unter [Was ist der Verwaltungsdienst?](../../../develop/adminservice/overview.md).

> [!IMPORTANT]  
> Wenn alle Instanzen des SMS-Anbieters für einen Standort offline sind, kann von den Configuration Manager-Konsolen keine Verbindung mit dem Standort hergestellt werden.  

Weitere Informationen zum Verwalten des SMS-Anbieters finden Sie unter [Verwalten des SMS-Anbieters](../../servers/manage/modify-your-infrastructure.md#BKMK_ManageSMSprovider).  

## <a name="installation-prerequisites"></a>Installationsvoraussetzungen  

Der Zielserver muss folgende Voraussetzungen erfüllen, damit der SMS-Anbieter unterstützt wird:  

- In derselben Domäne wie der Standortserver und das Standortsystem der Standortdatenbank  

- Dem Server darf keine Standortsystemrolle eines anderen Standorts zugewiesen sein.  

- Auf dem Server darf noch kein SMS-Anbieter installiert sein.  

- Auf dem Server muss eine unterstützte Betriebssystemversion ausgeführt werden.  

- Es muss mindestens 650 MB freier Speicherplatz auf dem Datenträger vorhanden sein, damit die Windows ADK-Komponenten unterstützt werden. Weitere Informationen zum Windows ADK und den SMS-Anbieters finden Sie unter [Anforderungen der Betriebssystembereitstellung](#BKMK_WAIKforSMSProv).  

- Für die [Verwaltungsdienst](../../../develop/adminservice/overview.md)-REST-API:

  - .NET 4.5 oder höher

  - Aktivieren der Windows Server-Rolle **Webserver (IIS)**

    > [!Note]  
    > Jeder SMS-Anbieter versucht, den Verwaltungsdienst zu installieren, der ein Zertifikat erfordert. Dieser Dienst hat eine Abhängigkeit von IIS, um das Zertifikat an HTTPS-Port 443 zu binden. Wenn Sie [Erweitertes HTTP](enhanced-http.md) aktivieren, wird das Zertifikat mithilfe von IIS-APIs vom Standort gebunden. Wenn Ihr Standort PKI verwendet, müssen Sie ein PKI-Zertifikat manuell in IIS an den SMS-Anbieter binden. Ab Version 2002 verwendet der Standort automatisch das selbst signierte Zertifikat des Standorts.

## <a name="locations"></a><a name="bkmk_location"></a> Speicherorte  

Bei der Installation eines Standorts wird der erste SMS-Anbieter für diesen Standort automatisch installiert. Sie können für den SMS-Anbieter einen der folgenden unterstützten Speicherorte angeben:  

- Der Standortserver  

- Den Standortdatenbankserver  

- Einen anderen Server, der die [Voraussetzungen für die Installation](#installation-prerequisites) erfüllt  

So zeigen Sie die Speicherorte der SMS-Anbieter für einen Standort an:

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie die Option **Standortkonfiguration**, und klicken Sie dann auf den Knoten **Standorte**.  

2. Wählen Sie den gewünschten Standort aus der Liste aus, und klicken Sie dann im Menüband auf **Eigenschaften**.  

3. Sehen Sie sich auf der Registerkarte **Allgemein** unter **Eigenschaften** das Feld **Speicherort des SMS-Anbieters** an.  

Jeder SMS-Anbieter unterstützt gleichzeitige Verbindungen von mehreren Anforderungen. Diese Verbindungen unterliegen nur zwei Einschränkungen. Dabei handelt es sich um die Anzahl der Serververbindungen sowie um die zur Bearbeitung der Verbindungsanforderungen erforderlichen Ressourcen, die unter Windows bzw. auf dem Server verfügbar sind.  

Nachdem Sie einen Standort installiert haben, können Sie erneut ein Setup von Configuration Manager auf dem Standortserver ausführen. Verwenden Sie das Setup, um den Speicherort eines vorhandenen SMS-Anbieters zu ändern oder weitere SMS-Anbieter an diesem Standort zu installieren. Installieren Sie nur einen SMS-Anbieter pro Computer. Ein Computer kann keinen SMS-Anbieter von mehr als einem Standort hosten.  

### <a name="choosing-a-location"></a>Auswählen eines Speicherorts

In den folgenden Abschnitten werden die Vor- und Nachteile der verschiedenen unterstützten Speicherorte für den SMS-Anbieter beschrieben:  

#### <a name="configuration-manager-site-server"></a>Configuration Manager-Standortserver

- **Vorteile:**  

  - Vom SMS-Anbieter werden keine Systemressourcen des Standortdatenbankcomputers beansprucht.  

  - Mit diesem Speicherort für den SMS-Anbieter kann eine bessere Leistung erzielt werden als mit Speicherorten auf Computern, die keine Standortserver- oder Standortdatenbankcomputer sind.  

- **Nachteile:**  

  - Vom SMS-Anbieter werden System- und Netzwerkressourcen beansprucht, die anderen Standortservervorgängen zugewiesen werden könnten.  

#### <a name="sql-server-that-hosts-the-site-database"></a>In SQL Server gehostete Standortdatenbank

- **Vorteile:**  

  - Vom SMS-Anbieter werden keine Systemressourcen auf dem Standortserver beansprucht.  

  - Mit diesem Speicherort kann die beste Leistung von allen drei Speicherorten erzielt werden, sofern genügend Serverressourcen verfügbar sind.  

- **Nachteile:**  

  - Vom SMS-Anbieter werden System- und Netzwerkressourcen beansprucht, die anderen Standortdatenbankvorgängen zugewiesen werden könnten.  

  - Wenn die Standortdatenbank auf einer gruppierten SQL Server-Instanz gehostet wird, können Sie diesen Speicherort nicht verwenden.  

#### <a name="computer-other-than-the-site-server-or-site-database-server"></a>Anderer Computer als der Standortserver oder Standortdatenbankserver

- **Vorteile:**  

  - Vom SMS-Anbieter werden keine Ressourcen des Standortservers oder des Standortdatenbanksystems beansprucht.  

  - Bei diesem Speicherorttyp können Sie zusätzliche SMS-Anbieter bereitstellen, um für die Verbindungen Hochverfügbarkeit zu erzielen.  

- **Nachteile:**  

  - Die Leistung des SMS-Anbieters kann beeinträchtigt werden. Der Grund hierfür ist die zusätzliche Netzwerkaktivität, die zur Koordinierung mit dem Standortserver und dem Standortdatenbankcomputer erforderlich ist.  

  - Dieser Server muss für den Standortdatenbankserver und alle Computer mit installierter Configuration Manager-Konsole stets zugänglich sein.  

  - Von diesem Speicherort werden möglicherweise Systemressourcen beansprucht, die andernfalls anderen Diensten zugewiesen würden.  

## <a name="authentication"></a><a name="bkmk_auth"></a> Authentifizierung

<!--1357013-->
Ab Version 1810 können Sie die mindestens erforderliche Authentifizierungsebene für den Administratorzugriff auf Configuration Manager-Standorte angeben. Diese Funktion verpflichtet Administratoren dazu, sich mit der erforderlichen Ebene bei Windows anzumelden. Dies gilt für alle Komponenten, die auf den SMS-Anbieter zugreifen. Dazu gehören beispielswiese die Configuration Manager-Konsole, SDK-Methoden und Windows PowerShell-Cmdlets.

### <a name="configure-authentication"></a>Konfigurieren der Authentifizierung

Melden Sie sich zunächst bei Windows mit der gewünschten Authentifizierungsebene an, um diese Einstellung zu konfigurieren.

> [!Important]  
> Diese Konfiguration entspricht einer Einstellung für die gesamte Hierarchie. Überprüfen Sie vor dem Ändern dieser Einstellung, ob sich alle Configuration Manager-Administratoren mit der erforderlichen Authentifizierungsebene bei Windows anmelden können.

Führen Sie folgende Schritte durch, um diese Einstellung zu konfigurieren:

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Standorte** aus.  

2. Klicken Sie im Menüband auf **Hierarchieeinstellungen**.  

3. Wechseln Sie zur Registerkarte **Authentifizierung**. Wählen Sie die gewünschte [Authentifizierungsebene](#authentication-levels) aus, und klicken Sie auf **OK**.  

    - Klicken Sie bei Bedarf auf **Hinzufügen**, um bestimmte Benutzer oder Gruppen auszuschließen. Weitere Informationen finden Sie unter [Ausschlüsse](#exclusions).  

### <a name="authentication-levels"></a>Authentifizierungsebenen

Die folgenden Ebenen sind verfügbar:

- **Windows-Authentifizierung:** Hiermit ist eine Authentifizierung mit Active Directory-Domänenanmeldeinformationen erforderlich. Diese Einstellung entspricht dem vorherigen Verhalten und der aktuellen Standardeinstellung. Wenn Sie den Standort aktualisieren, wird die Authentifizierungsebene nicht geändert.  

- **Zertifikatauthentifizierung:** Hiermit ist einer Authentifizierung mit einem gültigen Zertifikat erforderlich, das von einer vertrauenswürdigen PKI-Zertifizierungsstelle ausgestellt wurde. Sie konfigurieren dieses Zertifikat nicht im Configuration Manager. Configuration Manager fordert, dass sich der Administrator über ein PKI-Zertifikat bei Windows anmeldet.  

- **Windows Hello for Business-Authentifizierung:** Hiermit ist eine Authentifizierung mit starker zweistufiger Authentifizierung erforderlich, die an ein Gerät gebunden ist und biometrische Daten oder eine PIN verwendet. Weitere Informationen finden Sie unter [Windows Hello for Business](/windows/security/identity-protection/hello-for-business/hello-identity-verification).  

### <a name="exclusions"></a>Ausschlüsse

In den Hierarchieeinstellungen können Sie auf der Registerkarte **Authentifizierung** auch bestimmte Benutzer oder Gruppen ausschließen. Verwenden Sie diese Option nur in Ausnahmefällen, z.B. wenn bestimmte Benutzer Zugriff auf die Configuration Manager-Konsole benötigen, sich aber nicht auf der erforderlichen Ebene bei Windows authentifizieren können. Ein anderes Anwendungsbeispiel sind Automatisierungen oder Dienste, die im Rahmen eines Systemkontos ausgeführt werden.

## <a name="about-sms-provider-languages"></a><a name="BKMK_SMSProvLanguages"></a> Informationen zu den Sprachen des SMS-Anbieters  

Die vom SMS-Anbieter verwendeten Sprachen sind nicht von der Anzeigesprache des Servers, auf dem er installiert ist, abhängig.  

Wenn ein Administrator oder Configuration Manager-Prozess Daten mithilfe des SMS-Anbieters anfordert, versucht dieser, die Daten in einem Format zurückzugeben, das der Betriebssystemsprache des anfordernden Computers entspricht.

Zum Abgleich der Sprache wird eine indirekte Methode verwendet. Informationen werden vom SMS-Anbieter nicht aus einer Sprache in eine andere übersetzt. In welcher Sprache die zurückgegebenen Daten in der Configuration Manager-Konsole angezeigt werden, hängt von der Quelle des Objekts und vom Speichertyp ab.  

Wenn Configuration Manager Daten für ein Objekt in der Datenbank speichert, hängen die verfügbaren Sprachen von folgenden Faktoren ab:  

- Configuration Manager speichert erstellte Objekte mithilfe der Unterstützung für mehrere Sprachen. Objekte werden in der Standortdatenbank gespeichert, indem die Sprachen verwendet werden, die Sie beim Setup für den Standort konfigurieren. Diese Objekte werden in der Configuration Manager-Konsole in der Anzeigesprache des anfordernden Computers angezeigt, sofern diese Sprache für das Objekt verfügbar ist. Wenn die Konsole das Objekt nicht in der Anzeigesprache des anfordernden Computers anzeigen kann, wird es in der Standardsprache (Englisch) angezeigt.  

- Configuration Manager speichert Objekte, die von einem Administrator erstellt werden, in der Sprache, in der das Objekt erstellt wurde. Diese Objekte werden in der Configuration Manager-Konsole in der gleichen Sprache angezeigt. Der SMS-Anbieter kann diese nicht übersetzen, und es gibt keine Optionen für mehrere Sprachen.  

## <a name="use-multiple-sms-providers"></a><a name="BKMK_MultiSMSProv"></a> Verwenden mehrerer SMS-Anbieter  

Wenn Sie eine Standortinstallation abgeschlossen haben, können Sie zusätzliche SMS-Anbieter für den Standort installieren. Führen Sie zu diesem Zweck das Setup für Configuration Manager auf dem Standortserver aus.

Erwägen Sie, zusätzliche SMS-Anbieter zu installieren, wenn eine der folgenden Bedingungen erfüllt ist:  

- Viele Administratoren müssen gleichzeitig die Configuration Manager-Konsole verwenden und Verbindungen mit einem Standort herstellen.  

- Sie verwenden das Configuration Manager SDK oder andere Produkte, von denen häufig Aufrufe an den SMS-Anbieter erfolgen.  

- Die Hochverfügbarkeit des SMS-Anbieters ist für Ihr Unternehmen erforderlich.  

Wenn Sie mehrere SMS-Anbieter an einem Standort installieren, erfolgt die Zuweisung jeder neuen Verbindungsanforderung zur Verwendung eines installierten SMS-Anbieters nach dem Zufallsprinzip. Es ist nicht möglich, den SMS-Anbieter zur Verwendung für eine bestimmte Sitzungsverbindung anzugeben.  

> [!NOTE]  
> Betrachten Sie die Vor- und Nachteile der einzelnen Speicherorte für SMS-Anbieter. Weitere Informationen finden Sie unter [Speicherorte](#bkmk_location). Wägen Sie diese Überlegungen gegen die Tatsache ab, dass Sie nicht steuern können, welcher SMS-Anbieter für eine neue Verbindung verwendet wird.  

Wenn Sie eine Configuration Manager-Konsole zum ersten Mal mit einem Standort verbinden, fragt die Verbindung die Windows-Verwaltungsinstrumentation auf dem Standortserver ab. Diese Abfrage ermittelt eine Instanz des SMS-Anbieters, die von der Konsole verwendet wird. Diese spezifische Instanz des SMS-Anbieters wird bis zum Ende der Sitzung von der Konsole verwendet. Wenn die Sitzung beendet wird, weil der Server des SMS-Anbieters auf dem Netzwerk nicht verfügbar ist, wird die ursprüngliche Abfrage wiederholt, wenn Sie die Konsole wieder mit dem Standort verbinden. Es ist möglich, dass der Standort die gleiche nicht verfügbar Instanz des SMS-Anbieters zuweist. Wenn dies der Fall ist, können Sie versuchen, die Konsole neu zu verbinden, bis der Standort einen verfügbaren SMS-Anbieter zurückgibt.  

## <a name="about-the-sms-provider-namespace"></a><a name="BKMK_SMSProvNamespace"></a> Informationen zum Namespace des SMS-Anbieters  

Das WMI-Schema von Configuration Manager definiert die Struktur des SMS-Anbieters. Schemanamespaces beschreiben den Speicherort von Configuration Manager-Daten innerhalb des SMS-Anbieterschemas. In der folgenden Tabelle sind einige der üblichen Namespaces aufgelistet, die vom SMS-Anbieter verwendet werden:  

|Namespace|Beschreibung|  
|---------------|-----------------|  
|`Root\SMS\site_<site code>`|Der SMS-Anbieter, der in umfangreichem Maß von der Configuration Manager-Konsole, dem Ressourcen-Explorer, den Configuration Manager-Tools und Skripts verwendet wird|  
|`Root\SMS\SMS_ProviderLocation`|Der Ort der SMS-Anbietercomputer für einen Standort.|  
|`Root\CIMv2`|Der während der Hardware- und Softwareinventur für WMI-Namespaceinformationen inventarisierte Speicherort.|  
|`Root\CCM`|Konfigurationsrichtlinien und Clientdaten von Configuration Manager|  
|`Root\CIMv2\SMS`|Der Speicherort für Inventurberichterstattungsklassen, die vom Inventurclient-Agent gesammelt werden. Die Clients kompilieren diese Einstellungen während der Evaluation der Computerrichtlinie. Diese Einstellungen basieren auf der Konfiguration der Clienteinstellungen auf dem Computer.|  

## <a name="os-deployment-requirements"></a><a name="BKMK_WAIKforSMSProv"></a> Anforderungen für die Betriebssystembereitstellung

Auf dem Computer, auf dem Sie eine Instanz des SMS-Anbieters installieren, muss eine unterstützte Version des Windows ADK vorhanden sein.  

Weitere Informationen zu dieser Anforderung finden Sie unter [Anforderungen an die Infrastruktur für die Betriebssystembereitstellung](../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#windows-adk-for-windows-10) und [Unterstützung für Windows 10](../configs/support-for-windows-10.md).  

Beim Verwalten von Betriebssystembereitstellungen kann der SMS-Anbieter mithilfe des Windows ADK verschiedene Aufgaben erfüllen. Beispiel:  

- Anzeigen von WIM-Dateidetails  

- Hinzufügen von Treiberdateien zu vorhandenen Startabbildern  

- Erstellen von ISO-Startdateien  

Von der Windows ADK-Installation können auf jedem Computer, auf dem der SMS-Anbieter installiert wird, bis zu 650 MB Speicherplatz beansprucht werden. Der hohe Speicherplatzbedarf von Configuration Manager ist erforderlich, um Startimages von Windows PE zu installieren.  

## <a name="administration-service"></a><a name="bkmk_admin-service"></a>-Verwaltungsdienst

<!--3607711, fka 1321523-->

Der SMS-Anbieter bietet API-Interoperabilitätszugriff über eine HTTPS-OData-Verbindung, die als **Verwaltungsdienst** bezeichnet wird. Diese REST-API kann anstelle eines benutzerdefinierten Webdiensts verwendet werden, um auf Informationen vom Standort zuzugreifen.

Weitere Informationen finden Sie unter [Was ist der Verwaltungsdienst?](../../../develop/adminservice/overview.md).