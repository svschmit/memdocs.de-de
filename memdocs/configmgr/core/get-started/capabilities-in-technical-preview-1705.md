---
title: Technical Preview 1705
titleSuffix: Configuration Manager
description: Erfahren Sie mehr zu Features, die in Technical Preview für Configuration Manager-Version 1705 zur Verfügung stehen.
ms.date: 06/02/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 00684289-d21a-45f8-b1e3-c5c787d73096
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 06119bfc096564f70922249121f63c3d2039efe8
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88995448"
---
# <a name="capabilities-in-technical-preview-1705-for-configuration-manager"></a>Funktionen in der Technical Preview 1705 für Configuration Manager

*Gilt für: Configuration Manager (Technical Preview-Branch)*

In diesem Artikel werden die Features vorgestellt, die in der Technical Preview-Version 1705 für Configuration Manager verfügbar sind. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen. Bevor Sie diese Technical Preview-Version installieren, lesen Sie [Technical Preview für Configuration Manager](../../core/get-started/technical-preview.md), um sich mit den allgemeinen Anforderungen und Einschränkungen bei der Verwendung einer Technical Preview-Version vertraut zu machen und zu erfahren, wie Sie Updates für Versionen durchführen und Feedback zu den Funktionen in einer Technical Preview-Version geben können.    

**Bekannte Probleme in dieser Technical Preview:**
-   **Operations Manager Suite-Connector (OMS) lässt sich nicht aktualisieren**. Beim Upgrade einer früheren Technical Preview-Version, in der der OMS-Connector konfiguriert war, wird dieser Connector nicht aktualisiert und steht in der Konsole nicht mehr zur Verfügung. Nach dem Upgrade müssen Sie [den Assistenten für Azure-Dienste verwenden](capabilities-in-technical-preview-1705.md#use-azure-services-wizard-to-configure-a-connection-to-oms) und die Verbindung mit Ihrem OMS-Arbeitsbereich wiederherstellen.
-   **Surface-Treiber werden nicht erfolgreich synchronisiert**. Obwohl die Unterstützung für Surface-Treiber im Abschnitt **Neuerungen** in der Configuration Manager-Konsole für die Technical Preview aufgeführt ist, funktioniert dies noch nicht wie erwartet.
-   **Windows Update for Business-Zurückstellungsrichtlinien können nicht erstellt werden**. Obwohl die Fähigkeit zum Konfigurieren von Windows Update for Business-Zurückstellungsrichtlinien im Abschnitt **Neuerungen** in der Configuration Manager-Konsole für die Technical Preview aufgeführt ist, wird der Assistent nicht geöffnet, sodass Sie keine Richtlinien konfigurieren können.


<!--  Known Issues Template
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="update-reset-tool"></a>Tool zum Zurücksetzen von Updates  
Sie können das Configuration Manager-Tool zum Zurücksetzen von Updates **CMUpdateReset.exe** verwenden, sollten bei konsoleninternen Updates Probleme beim Herunterladen oder Replizieren auftreten. Dieses Tool ist in der Technical Preview-Version 1705 enthalten. Sie finden es auf dem Standortserver Ihres Technical Preview-Standorts im Ordner ***\cd.latest\SMSSETUP\TOOLS***, nachdem Sie die Preview-Version installiert haben.

Sie können dieses Tool ab der Technical Preview-Version 1606 verwenden. Diese Abwärtskompatibilität wird bereitgestellt, damit das Tool mit einer Vielzahl von Technical Preview-Updateszenarien genutzt werden kann und nicht so lange gewartet werden muss, bis die nächste Technical Preview verfügbar ist.

Sie können dieses Tool verwenden, wenn ein konsoleninternes Update noch nicht installiert wurde und einen fehlerhaften Status hat. Ein fehlerhafter Status kann bedeuten, dass der Download des Updates zwar läuft, aber ins Stocken geraten ist und übermäßig lange dauert, u.U. viele Stunden länger als dies bei Updatepaketen ähnlicher Größe bislang der Fall war. Es kann sich auch um einen Fehler beim Replizieren des Updates an untergeordnete primäre Standorte handeln.  

Wenn Sie das Tool ausführen, wird es für das Update ausgeführt, das Sie angeben. Erfolgreich installierte oder heruntergeladene Updates werden von diesem Tool standardmäßig nicht gelöscht.  

### <a name="prerequisites"></a>Voraussetzungen
Das Konto, das Sie verwenden, um das Tool auszuführen, benötigt die folgenden Berechtigungen:
-   Die Berechtigungen **Lesen** und **Schreiben** für die Standortdatenbank des Standorts der zentralen Verwaltung und jeden primären Standort in Ihrer Hierarchie. Zum Festlegen dieser Berechtigungen können Sie das Benutzerkonto der Configuration Manager-Datenbank an jedem Standort als Mitglied der [festen Datenbankrollen](/sql/relational-databases/security/authentication-access/database-level-roles#fixed-database-roles) **db_datawriter** und **db_datareader** hinzufügen. Das Tool interagiert nicht mit sekundären Standorten.
-   **Lokaler Administrator** am Standort der obersten Ebene Ihrer Hierarchie.
-   **Lokaler Administrator** auf dem Computer, der den Dienstverbindungspunkt hostet.

Sie benötigen die GUID des Updatepakets, das Sie zurücksetzen möchten. So rufen Sie die GUID ab
-   Wechseln Sie in der Konsole zu **Verwaltung** > **Updates und Wartung**, und klicken Sie dann im Anzeigebereich mit der rechten Maustaste auf die Überschrift einer der Spalten (z.B. **Status**). Wählen Sie dann **Paket-GUID** aus. Dadurch wird diese Spalte, die die GUID des Updatepakets enthält, der Anzeige hinzugefügt.

> [!TIP]  
> Um die GUID zu kopieren, wählen Sie die Zeile des Updatepakets aus, das Sie zurücksetzen möchten, und drücken dann STRG+C, um diese Zeile zu kopieren. Wenn Sie die kopierte Auswahl in einen Texteditor einfügen, können Sie anschließend nur die GUID zur Verwendung als Befehlszeilenparameter kopieren, wenn Sie das Tool ausführen.

### <a name="run-the-tool"></a>Ausführen des Tools    
Das Tool muss für den Standort der obersten Ebene der Hierarchie ausgeführt werden.

Wenn Sie das Tool ausführen, verwenden Sie Befehlszeilenparameter zum Angeben der SQL Server-Instanz am Standort der obersten Ebene der Hierarchie, des Namens der Standortdatenbank und der GUID des Updatepakets, das Sie zurücksetzen möchten. Das Tool ermittelt dann die zusätzlichen Server, auf die es Zugriff benötigt, anhand des Updatestatus.   

Wenn das Updatepaket den Status*Nach Download* hat, wird das Paket nicht vom Tool bereinigt. Optional können Sie das Entfernen eines erfolgreich heruntergeladenen Updates mithilfe des Parameters „FDELETE“ erzwingen (siehe die Befehlszeilenparameter weiter unten in diesem Thema).

Nach Ausführung des Tools:
-   Nachdem ein Paket gelöscht wurde, starten Sie an den Standorten auf oberster Ebene den SMS_Executive-Dienst neu, und führen Sie danach eine Überprüfung auf Updates durch, um das Paket erneut herunterzuladen.
-   Wenn ein Paket nicht gelöscht wurde, müssen Sie keine Maßnahmen ergreifen, da das Update erneut initialisiert und die Replikation oder Installation neu gestartet wird.

**Befehlszeilenparameter:**  


|                        Parameter                         |                                                            Beschreibung                                                            |
|----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------|
| **-S &lt;Vollqualifizierter Domänenname der SQL Server-Instanz Ihres Standorts der obersten Ebene>** | *Erforderlich* <br> Sie müssen den vollqualifizierten Domänennamen der SQL Server-Instanz angeben, die die Standortdatenbank für den Standort der obersten Ebene Ihrer Hierarchie hostet. |
|                **-D &lt;Datenbankname>**                 |                             *Erforderlich* <br> Sie müssen den Namen der Datenbank des Standorts der obersten Ebene angeben.                             |
|                 **-P &lt;Paket-GUID>**                 |                        *Erforderlich* <br> Sie müssen die GUID des Updatepakets angeben, das Sie zurücksetzen möchten.                        |
|           **-I &lt;SQL Server-Instanzname>**           |                   *Optional* <br> Dient zum Bestimmen der SQL Server-Instanz, die die Standortdatenbank hostet.                   |
|                       **-FDELETE**                       |                      *Optional* <br> Dient zum Erzwingen des Löschens eines erfolgreich heruntergeladenen Updatepakets.                      |

 **Beispiele:**  
 In einem typischen Szenario möchten Sie ein Update zurücksetzen, wenn beim Herunterladen Probleme aufgetreten sind. Der vollqualifizierte Domänenname Ihrer SQL Server-Instanz lautet *server1.fabrikam.com*, die Standortdatenbank heißt *CM_XYZ*, und die Paket-GUID lautet *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Führen Sie Folgendes aus: ***CMUpdateReset.exe -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

 In einem extremeren Szenario möchten Sie das Löschen eines problematischen Updatepakets erzwingen. Der vollqualifizierte Domänenname Ihrer SQL Server-Instanz lautet *server1.fabrikam.com*, die Standortdatenbank heißt *CM_XYZ*, und die Paket-GUID lautet *61F16B3C-F1F6-4F9F-8647-2A524B0C802C*.  Führen Sie Folgendes aus: ***CMUpdateReset.exe  -FDELETE -S server1.fabrikam.com -D CM_XYZ -P 61F16B3C-F1F6-4F9F-8647-2A524B0C802C***

### <a name="test-the-tool-with-the-technical-preview"></a>Testen des Tools mit der Technical Preview-Version  
Sie können dieses Tool ab der Technical Preview-Version 1606 verwenden. Diese Abwärtskompatibilität wird bereitgestellt, damit das Tool mit einer größeren Anzahl von Technical Preview-Updateszenarien genutzt werden kann und nicht so lange gewartet werden muss, bis die nächste Technical Preview-Version verfügbar ist.

Führen Sie das Tool für ein Updatepaket für eine Technical Preview vor diesem Update aus, und führen Sie die entsprechende Überprüfung der Voraussetzungen durch. Der Status einer erfolgten Überprüfung der Voraussetzungen wird durch einen der folgenden Status für das Paket unter **Verwaltung** > **Updates und Wartung** bestimmt:  
-   **Die Voraussetzungsprüfung war erfolgreich**
-   **Die Überprüfung der Voraussetzung war mit einer Warnung erfolgreich**
-   **Fehler bei der Voraussetzungsüberprüfung**


## <a name="high-dpi-console-support"></a>Unterstützung einer hohen DPI-Einstellung in der Konsole

Ab dieser Version sollten Probleme damit, wie die Configuration Manager-Konsole skaliert wird und verschiedene Teile der Benutzeroberfläche bei Betrachtung auf Geräten mit hohen DPI-Einstellungen angezeigt werden (z.B. Surface Book), behoben sein.


## <a name="peer-cache-improvements"></a>Verbesserungen des Peercaches
Ab dieser Technical Preview wird von Peercache [nicht mehr das Netzwerkzugriffskonto verwendet](../plan-design/hierarchy/client-peer-cache.md), um Downloadanforderungen von Peers zu authentifizieren.


## <a name="improvements-for-sql-server-always-on-availability-groups"></a>Verbesserungen für SQL Server Always On-Verfügbarkeitsgruppen  
Ab dieser Version können Sie jetzt Replikate mit asynchronem Commit in den SQL Server Always On-Verfügbarkeitsgruppen verwenden, die Sie mit Configuration Manager nutzen.  Dies bedeutet, dass Sie Ihren Verfügbarkeitsgruppen zusätzliche Replikate hinzufügen können, die Sie als standortexterne (Remote-) Sicherungen und bei Bedarf in einem Notfallwiederherstellungsszenario einsetzen können.  

- Configuration Manager unterstützt das Verwenden von Replikaten mit asynchronem Commit zum Wiederherstellen Ihres synchronen Replikats.  Unter [Wiederherstellungsoptionen für die Standortdatenbank](../servers/manage/recover-sites.md#site-database-recovery-options) finden Sie im Thema zu Sicherung und Wiederherstellung weiterführende Informationen dazu.

- Diese Version unterstützt kein Failover, um das Replikat mit asynchronem Commit als Standortdatenbank zu verwenden.
  > [!CAUTION]  
  > Da Configuration Manager nicht den Status des Replikats mit asynchronem Commit dahingehend überprüft, ob es aktuell ist, und [ein solches Replikat asynchron sein kann](/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server?view=sql-server-2014#AvailabilityModes), kann das Verwenden eines Replikats mit asynchronem Commit als Standortdatenbank die Integrität Ihres Standorts und Ihrer Daten gefährden.  

- Sie können die gleiche Anzahl und Art von Replikaten in einer Verfügbarkeitsgruppe nutzen, die von der von Ihnen verwendeten Version von SQL Server unterstützt wird.   (Zuvor war die Unterstützung auf zwei Replikate mit synchronem Commit beschränkt.)

### <a name="configure-an-asynchronous-commit-replica"></a>Konfigurieren eines Replikats mit asynchronem Commit
Zum Hinzufügen eines asynchronen Replikats zu einer [mit Configuration Manager verwendeten Verfügbarkeitsgruppe](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md) müssen Sie nicht die Konfigurationsskripts ausführen, die zum Konfigurieren eines synchronen Replikats erforderlich sind. (Der Grund ist, dass das Verwenden eines asynchronen Replikats als Standortdatenbank nicht unterstützt wird.) Weitere Informationen finden Sie unter [Add a secondary replica to an availability group](/sql/database-engine/availability-groups/windows/add-a-secondary-replica-to-an-availability-group-sql-server?view=sql-server-2014) (Hinzufügen eines sekundären Replikats zu einer Verfügbarkeitsgruppe).

### <a name="use-the-asynchronous-replica-to-recover-your-site"></a>Wiederherstellen Ihres Standorts mithilfe des asynchronen Replikats
Bevor Sie ein asynchrones Replikat zum Wiederherstellen der Standortdatenbank verwenden, müssen Sie den aktiven primären Standort beenden, um weitere Schreibvorgänge in die Standortdatenbank zu verhindern. Nachdem Sie den Standort beendet haben, können Sie ein asynchrones Replikat anstelle einer [manuell wiederhergestellten Datenbank](../servers/manage/recover-sites.md#use-a-site-database-that-has-been-manually-recovered) verwenden.

Zum Beenden des Standorts können Sie das [Hierarchieverwaltungstool](../servers/manage/hierarchy-maintenance-tool-preinst.exe.md) verwenden, mit dem die wichtigen Dienste auf dem Standortserver beendet werden. Verwenden Sie die Befehlszeile: **Preinst.exe /stopsite**   

Das Beenden des Standorts ist gleichbedeutend mit dem Beenden des Standortkomponenten-Manager-Diensts (sitecomp) gefolgt vom SMS_Executive-Dienst auf dem Standortserver.


## <a name="improved-user-notifications-for-microsoft-365-updates"></a>Verbesserte Benutzerbenachrichtigungen zu Microsoft 365-Updates
Verbesserungen sind erfolgt, um die Office-Klick-und-Los-Benutzeroberfläche zu nutzen, wenn ein Client ein Microsoft 365-Update installiert. Dazu gehören Popup- und In-App-Benachrichtigungen sowie ein Countdown. Wenn vor dieser Version ein Microsoft 365-Update an einen Client gesendet wurde, wurden geöffnete Office-Anwendungen ohne Warnung automatisch geschlossen. Nach diesem Update werden Office-Anwendungen nicht mehr unerwartet geschlossen.

### <a name="prerequisites"></a>Voraussetzungen
Dieses Update gilt für Microsoft 365 Apps for Enterprise-Clients.

### <a name="known-issues"></a>Bekannte Probleme
Wenn ein Client eine Microsoft 365-Updatezuweisung erstmals prüft und für das Update eine in der Vergangenheit liegende Frist geplant war, es sofort geplant oder binnen 30 Minuten geplant ist, kann die Servicequalität für Microsoft 365-Benutzer uneinheitlich sein. Der Client kann beispielsweise ein 30-minütiges Countdown-Dialogfeld für das Update angezeigt bekommen, doch die tatsächliche Erzwingung kann vor dem Ende des Countdowns starten. Um dieses Verhalten zu vermeiden, beachten Sie Folgendes:
- Stellen Sie das Microsoft 365-Update mit einer Frist bereit, die mehr als 60 Minuten nach dem jeweils aktuellen Zeitpunkt in der Zukunft liegt.
- Konfigurieren Sie ein Wartungsfenster außerhalb der Geschäftszeiten für die Sammlung oder eine Karenzzeit für die Erzwingung der Bereitstellung.

### <a name="try-it-out"></a>Probieren Sie es aus!
Versuchen Sie, die folgenden Aufgaben auszuführen, und senden Sie uns dann **Feedback** über die Registerkarte **Start** des Menübands, um uns zu wissen zu lassen, wie es funktioniert hat:
- Stellen Sie auf einem Client ein Microsoft 365-Update mit einer Frist bereit, die mehr als 60 Minuten nach dem aktuellen Zeitpunkt in der Zukunft liegt. Beobachten Sie das neue Verhalten auf dem Client.


## <a name="configure-and-deploy-windows-defender-application-guard-policies"></a>Konfigurieren und Bereitstellen von Windows Defender Application Guard-Richtlinien

[Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) ist eine neue Windows-Funktion zum Schutz Ihrer Benutzer, indem nicht vertrauenswürdige Websites in einem sicheren isolierten Container geöffnet werden, auf den andere Teile des Betriebssystems keinen Zugriff haben. In dieser Technical Preview haben wir Unterstützung für diese Funktion mithilfe von Configuration Manager-Konformitätseinstellungen hinzugefügt, die Sie konfigurieren und in einer Sammlung bereitstellen.
Dieses Feature wird als Vorschauversion für die 64-Bit-Version von Windows 10 Creator Update veröffentlicht. Um diese Funktion jetzt zu testen, müssen Sie eine Preview-Version dieses Updates verwenden.


### <a name="before-you-start"></a>Vorbereitung

Zum Erstellen und Bereitstellen von Windows Defender Application Guard-Richtlinien müssen die Windows 10-Geräte, auf denen Sie die Richtlinie bereitstellen, mit einer Netzwerkisolationsrichtlinie konfiguriert werden. Weitere Informationen finden Sie im Blogbeitrag, auf den später verwiesen wird.
Diese Funktion funktioniert nur mit aktuellen Windows 10 Insider-Builds. Um sie zu testen, muss auf Ihren Clients ein aktueller Windows 10 Insider-Build ausgeführt werden.

### <a name="try-it-out"></a>Probieren Sie es aus!

Lesen Sie unbedingt den Blogbeitrag, um sich mit den Grundlagen von Windows Defender Application Guard vertraut zu machen.

So erstellen Sie eine Richtlinie und durchsuchen die verfügbaren Einstellungen

1.  Wählen Sie in der Configuration Manager-Konsole **Assets und Konformität** aus.
2.  Wählen Sie im Arbeitsbereich **Assets und Konformität** nacheinander **Übersicht** > **Endpoint Protection** > **Windows Defender Application Guard** aus.
3.  Klicken Sie auf der Registerkarte **Start** in der Gruppe **Erstellen** auf **Windows Defender Application Guard-Richtlinie erstellen**.
4.  Unter Verwendung des Blogbeitrags als Referenz können Sie die verfügbaren Einstellungen zum Testen der Funktion durchsuchen und konfigurieren.
5.  Wenn Sie fertig sind, schließen Sie den Assistenten ab, und stellen Sie die Richtlinie auf einem oder mehreren Windows 10-Geräten bereit.

### <a name="further-reading"></a>Weitere Informationen

Weitere Informationen zu Windows Defender Application Guard finden Sie in [diesem Blogbeitrag]( https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97).
Darüber hinaus finden Sie in [diesem Blogbeitrag](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903) weitere Informationen zum eigenständigen Modus von Windows Defender Application Guard.




## <a name="new-capabilities-for-azure-ad-and-cloud-management"></a>Neue Funktionen für Azure AD und Cloudverwaltung

In dieser Version können Sie Clouddienste so konfigurieren, dass Azure AD zur Unterstützung des folgenden Szenarios verwendet wird:

- Manuelles Herunterladen und Installieren des Configuration Manager-Client aus dem Internet, der anschließend einem Configuration Manager-Standort zugewiesen wird
- Verwenden von Intune zum Bereitstellen des Configuration Manager-Clients auf Geräten im Internet

### <a name="advantages"></a>Vorteile

Durch Verwenden von Clouddiensten und Azure AD ist das Verwenden von Clientauthentifizierungszertifikaten nicht mehr notwendig.

Sie können Azure AD-Benutzer an Ihrem Standort ermitteln, um Sie in Sammlungen und anderen Configuration Manager-Vorgängen zu verwenden.

### <a name="before-you-start"></a>Vorbereitung

- Sie benötigen einen Azure AD-Mandanten.
- Auf Ihren Geräten, die in Azure AD eingebunden sein müssen, muss Windows 10 ausgeführt werden.  Clients können zusätzlich zu Azure AD auch einer Domäne beitreten.
- Zusätzlich zum Erfüllen der [geltenden Voraussetzungen](../plan-design/configs/site-and-site-system-prerequisites.md) für die Standortsystemrolle „Verwaltungspunkt“ müssen Sie außerdem sicherstellen, dass **ASP.NET 4.5** (und alle anderen Optionen, die automatisch damit ausgewählt werden) auf dem Computer aktiviert sind, der diese Standortsystemrolle hostet.
- So verwenden Sie Intune zum Bereitstellen des Configuration Manager-Clients
    - Sie benötigen einen funktionierenden Intune-Mandanten (Configuration Manager und Intune müssen nicht verbunden sein).
    - In Intune haben Sie eine App, die den Configuration Manager-Client enthält, erstellt und bereitgestellt. Informationen dazu finden Sie unter „Installieren von Clients für mit Intune MDM verwaltete Windows-Geräte“.
- So stellen Sie den Client mithilfe von Configuration Manager bereit
    - Mindestens ein Verwaltungspunkt muss für den HTTPS-Modus konfiguriert sein.
    - Sie müssen ein Cloud Management Gateway einrichten.


### <a name="set-up-the-cloud-management-gateway"></a>Einrichten des Cloud Management Gateways

Richten Sie Cloud Management Gateway ein, damit Clients ohne Zertifikate im Internet auf Ihren Configuration Manager-Standort zugreifen können.

Hilfe dazu finden Sie in den folgenden Themen:

- [Planen des Cloud Management Gateways in Configuration Manager](../clients/manage/cmg/plan-cloud-management-gateway.md)
- [Einrichten des Cloud Management Gateways für Configuration Manager](../clients/manage/cmg/setup-cloud-management-gateway.md)
- [Überwachen des Cloud Management Gateways in Configuration Manager](../clients/manage/cmg/monitor-clients-cloud-management-gateway.md)

### <a name="set-up-the-azure-services-app-in-configuration-manager-cloud-services"></a>Einrichten der Azure-Dienste-App in Configuration Manager-Clouddiensten

Hiermit wird Ihr Configuration Manager-Standort mit Azure AD verbunden, was eine Voraussetzung für alle anderen Vorgänge in diesem Abschnitt ist. Dazu ist Folgendes erforderlich:

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** den Eintrag **Clouddienste**, und klicken Sie dann auf **Azure-Dienste**.
2. Klicken Sie auf der Registerkarte **Start** in der Gruppe **Azure-Dienste** auf **Azure-Dienste konfigurieren**.
3. Wählen Sie im Assistenten für Azure-Dienste auf der Seite **Azure-Dienste** die Option **Cloudverwaltung** aus, damit sich Clients in der Hierarchie mithilfe von Azure AD authentifizieren können.
4. Geben Sie auf der Seite **Allgemein** des Assistenten einen Namen und eine Beschreibung für den Azure-Dienst ein.
5. Wählen Sie auf der Seite **App** des Assistenten in der Liste Ihre Azure-Umgebung aus, und klicken Sie auf **Durchsuchen**, um die Server- und Client-Apps auszuwählen, die zum Konfigurieren des Azure-Diensts verwendet werden:
   - Wählen Sie im Fenster **Server App** (Server-App) die Server-App aus, die Sie verwenden möchten, und klicken Sie dann auf **OK**. Server-Apps sind Azure-Web-Apps, die Konfigurationen für Ihr Azure-Konto enthalten, einschließlich Ihrer Mandanten-ID, Client-ID und eines geheimen Schlüssels für Clients. Wenn Sie nicht über eine verfügbare Server-App verfügen, verwenden Sie eine der folgenden:
       - **Erstellen:** Wenn Sie eine neue Server-App erstellen möchten, klicken Sie auf **Erstellen**. Geben Sie einen Anzeigenamen für die App und den Mandanten an. Nachdem Sie sich bei Azure angemeldet haben, erstellt Configuration Manager daraufhin die Web-App in Azure für Sie, einschließlich der Client-ID und des geheimen Schlüssels für den Gebrauch mit der Web-App. Später können Sie diese im Azure-Portal anzeigen.
       - **Importieren:** Wenn Sie eine Web-App verwenden möchten, die in Ihrem Azure-Abonnement bereits vorhanden ist, klicken Sie auf **Importieren**. Stellen Sie einen Anzeigenamen für die App und den Mandanten bereit, und geben Sie dann die Mandanten-ID, Client-ID und den geheimen Schlüssel für die Web-App an, die Configuration Manager verwenden soll. Nachdem Sie die Informationen überprüft haben, klicken Sie auf **OK**, um fortzufahren. Diese Option ist in dieser Technical Preview derzeit nicht verfügbar.
   - Wiederholen Sie den gleichen Vorgang für die Client-App.

   Sie müssen bei Verwenden von „Anwendungsimport“ die Anwendungsberechtigung *Verzeichnisdaten lesen* erteilen, damit im Portal die ordnungsgemäßen Berechtigungen festgelegt werden. Bei Verwenden von „Anwendungserstellung“ werden die Berechtigungen automatisch mit der Anwendung erstellt, doch Sie müssen der Anwendung im Azure-Portal weiterhin Ihre Zustimmung geben.
6. Aktivieren Sie auf der Seite **Ermittlung** des Assistenten optional **Azure Active Directory-Benutzerermittlung aktivieren**, und klicken Sie dann auf **Einstellungen**.
   Konfigurieren Sie im Dialogfeld **Einstellungen der Azure AD-Benutzerermittlung** einen Zeitplan für die Ermittlung. Sie können auch die Deltaermittlung aktivieren, bei der nur eine Überprüfung auf neue oder geänderte Konten in Azure AD erfolgt.
7. Schließen Sie den Assistenten ab.

An diesem Punkt haben Sie Ihren Configuration Manager-Standort mit Azure AD verbunden.


### <a name="install-the-cm-client-from-the-internet"></a>Installieren des Configuration Manager-Clients aus dem Internet

Bevor Sie beginnen, stellen Sie sicher, dass die Quelldateien für die Clientinstallation lokal auf dem Gerät gespeichert sind, auf dem der Client installiert werden soll.
Befolgen Sie anschließend die Anweisungen unter [Bereitstellen von Clients auf Windows-Computern](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual) zum Verwenden der folgenden Befehlszeile für die Installation (ersetzen Sie die Werte im Beispiel durch Ihre eigenen Werte):

**ccmsetup.exe /NoCrlCheck /Source:C:\CLIENT  CCMHOSTNAME=SCCMPROXYCONTOSO.CLOUDAPP.NET/CCM_Proxy_ServerAuth/72457598037527932 SMSSiteCode=HEC AADTENANTID=780433B5-E05E-4B7D-BFD1-E8013911E543 AADTENANTNAME=contoso  AADCLIENTAPPID=\<GUID> AADRESOURCEURI=<code>https://contososerver</code>**

- **/NoCrlCheck:** Wenn Ihr Verwaltungspunkt oder Cloud Management Gateway ein nicht öffentliches Serverzertifikat verwendet, kann der Client ggf. nicht auf den Speicherort der Zertifikatssperrliste zugreifen.
- **/Source:** Lokaler Ordner:   Speicherort der Clientinstallationsdateien.
- **CCMHOSTNAME:** Der Name Ihres Internetverwaltungspunkts. Sie finden diese Informationen, indem Sie **gwmi -namespace root\ccm\locationservices -class SMS_ActiveMPCandidate** an einer Eingabeaufforderung auf einem verwalteten Client ausführen.
- **SMSMP:** Der Name des anfänglichen Verwaltungspunkts, der sich in Ihrem Intranet befinden kann.
- **SMSSiteCode:** Der Standortcode Ihres Configuration Manager-Standorts.
- **AADTENANTID**, **AADTENANTNAME:** Die ID und der Name des Azure AD-Mandanten, den Sie mit Configuration Manager verknüpft haben. Diese Informationen können Sie herausfinden, indem Sie auf einem Azure AD beigetretenen Gerät „dsregcmd.exe /status“ an einer Eingabeaufforderung ausführen.
- **AADCLIENTAPPID:** Die ID der Azure AD-Client-App. Hilfe zum Ermitteln dieses Werts finden Sie unter [Erstellen einer Azure Active Directory-Anwendung und eines Dienstprinzipals mit Ressourcenzugriff mithilfe des Portals](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in).
- **AADResourceUri:** Der Bezeichner-URI der eingebundenen Azure AD-Server-App.

## <a name="use-azure-services-wizard-to-configure-a-connection-to-oms"></a>Verwenden des Assistenten für Azure-Dienste zum Konfigurieren einer Verbindung mit Microsoft Operations Management Suite (OMS)
Ab der Technical Preview-Version 1705 verwenden Sie den **Assistenten für Azure-Dienste** zum Konfigurieren der Verbindung zwischen Configuration Manager und dem Clouddienst Operations Management Suite (OMS). Der Assistent ersetzt vorherige Workflows zum Konfigurieren dieser Verbindung.

-   Der Assistent dient zum Konfigurieren von Clouddiensten für Configuration Manager wie OMS, Windows Store für Unternehmen (WSfB) und Azure Active Directory (Azure AD).  

-   Configuration Manager verbindet sich mit OMS für Features wie Log Analytics oder die Upgradebereitschaft.

### <a name="prerequisites-for-the-oms-connector"></a>Voraussetzungen für den OMS-Connector
Die Voraussetzungen zum Konfigurieren einer Verbindung mit OMS unterscheiden sich nicht von denjenigen, die [für die Current Branch-Version 1702 dokumentiert sind](/azure/azure-monitor/platform/collect-sccm). Diese Informationen werden hier wiederholt:  

-   Erteilen der Configuration Manager-Berechtigung für OMS.

-   Der OMS-Connector muss auf dem Computer installiert werden, der einen [Dienstverbindungspunkt](../servers/deploy/configure/about-the-service-connection-point.md) hostet, der sich in [Onlinemodus](../servers/deploy/configure/about-the-service-connection-point.md#bkmk_modes) befindet.

-   Sie müssen Microsoft Monitoring Agent für OMS auf den Dienstverbindungspunk zusammen mit den OMS-Connector installieren. Der Agent und der OMS-Connector müssen so konfiguriert werden, dass sie den gleichen **OMS-Arbeitsbereich** nutzen. In der OMS-Dokumentation unter [Herunterladen und Installieren des Agents](/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) finden Sie Informationen zur Installation des Agents.
-   Nachdem Sie den Connector und den Agent installiert haben, müssen Sie OMS für die Verwendung von Configuration Manager-Daten konfigurieren. Dazu gehen Sie im OMS-Portal unter [Importieren von Sammlungen](/azure/log-analytics/log-analytics-sccm#import-collections).

### <a name="use-the-azure-services-wizard-to-configure-the-connection-to-oms"></a>Verwenden des Assistenten für Azure-Dienste zum Konfigurieren der Verbindung mit OMS

1.  Wechseln Sie in der Konsole zu **Verwaltung** > **Übersicht** > **Clouddienste** > **Azure-Dienste**, und wählen Sie dann **Azure-Dienste konfigurieren** auf der Registerkarte **Start** im Menüband aus, um den **Assistenten für Azure-Dienste** zu starten.

2.  Wählen Sie auf der Seite **Azure-Dienste** den Clouddienst „Operation Management Suite“ aus. Geben Sie einen Anzeigenamen für den **Azure-Dienstnamen** und eine optionale Beschreibung ein, und klicken Sie dann auf **Weiter**.

3.  Geben Sie auf der Seite **App** Ihre Azure-Umgebung an (die Technical Preview unterstützt nur die öffentliche Cloud). Klicken Sie dann auf **Durchsuchen**, um das Server-App-Fenster zu öffnen.

4.  Wählen Sie eine Web-App aus:

    -   **Importieren:** Wenn Sie eine Web-App verwenden möchten, die in Ihrem Azure-Abonnement bereits vorhanden ist, klicken Sie auf **Importieren**. Stellen Sie einen Anzeigenamen für die App und den Mandanten bereit, und geben Sie dann die Mandanten-ID, Client-ID und den geheimen Schlüssel für die Web-App an, die Configuration Manager verwenden soll. Nachdem Sie die Informationen **überprüft** haben, klicken Sie auf **OK**, um fortzufahren.   

    > [!NOTE]   
    > Bei Konfiguration von OMS in dieser Preview-Version unterstützt OMS nur die Funktion *Importieren* für eine Web-App. Das Erstellen einer neuen Web-App wird nicht unterstützt. Sie können auch keine vorhandene App für OMS wiederverwenden.

5.  Wenn Sie alle anderen Schritte erfolgreich ausgeführt haben, werden die Informationen auf dem Bildschirm **OMS-Verbindungskonfiguration** automatisch auf dieser Seite angezeigt. Informationen zu den Verbindungseinstellungen müssen für Ihr **Azure-Abonnement**, die **Azure-Ressourcengruppe** und den **Operations Management Suite-Arbeitsbereich** angezeigt werden.

6.  Der Assistent stellt eine Verbindung mit dem OMS-Dienst unter Verwendung der von Ihnen eingegebenen Informationen her. Wählen Sie die Gerätesammlungen aus, die Sie mit OMS synchronisieren möchten, und klicken Sie dann auf **Hinzufügen**.

7.  Überprüfen Sie die Verbindungseinstellungen auf dem Bildschirm **Zusammenfassung**, und wählen Sie dann **Weiter** aus. Auf dem Bildschirm **Status** wird der Verbindungsstatus angezeigt. Anschließend sollte **Abgeschlossen** angezeigt werden.

8.  Nach Abschluss des Assistenten zeigt die Configuration Manager-Konsole, dass Sie **Operation Management Suite** als **Clouddiensttyp** konfiguriert haben.