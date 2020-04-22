---
title: Funktionen in Technical Preview 1601
titleSuffix: Configuration Manager
description: Erfahren Sie mehr zu Features, die in Technical Preview für Configuration Manager-Version 1601 zur Verfügung stehen.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aae1cf2f-2c04-4f68-a03a-f4a925433c09
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ea003aef949f5624591d87dd6105d3a1cff3b691
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705728"
---
# <a name="capabilities-in-technical-preview-1601-for-configuration-manager"></a>Funktionen in der Technical Preview 1601 für Configuration Manager

*Gilt für: Configuration Manager (Technical Preview-Branch)*

In diesem Artikel werden die Features vorgestellt, die in der Technical Preview-Version 1601 für Configuration Manager verfügbar sind. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen.      Bevor Sie diese Version der Technical Preview installieren, lesen Sie das einführende Thema [Technical Preview für Configuration Manager](../../core/get-started/technical-preview.md), um sich mit den allgemeinen Anforderungen und Einschränkungen bei der Verwendung einer Technical Preview vertraut zu machen und um zu erfahren, wie Sie Updates für Versionen durchführen und Feedback zu den Features in einer Technical Preview geben können.  

 **Bekannte Probleme für diese Technical Preview:**  

-   Wenn Sie **Clientupdateoptionen** für das Heraufstufen eines Präproduktionsclients zur Produktionsversion verwalten, enthält der Text des Kontrollkästchens die Clientversion null (0) anstelle der tatsächlichen Clientbuildnummer. Die richtige Präproduktionsclientversion wird im Bereich über dieser Option angezeigt und ist die Clientversion, die zur Produktionsversion heraufgestuft wird, wenn Sie diese Option auswählen.  

-   Wenn Sie auf Technical Preview 1601 aktualisieren und das Testen des Configuration Manager-Clients in einer Präproduktionssammlung auswählen, wird kein Upgrade für das Clientpaket der Sammlung durchgeführt. Dieses Problem gilt nur für Technical Preview 1601.  

     Zur Umgehung dieser Probleme führen Sie einen der folgenden Schritte aus:  

    -   Führen Sie das folgende SQL-Skript für die Datenbank des primären Standorts aus:  

        ``` SQL
        DECLARE @PilotingPkgID NVARCHAR(8)  

        SELECT @PilotingPkgID = PilotingPackageID FROM ClientDeploymentSettings  

        MERGE INTO PkgServers_G AS T  
        USING (  
            SELECT @PilotingPkgID AS PkgID, NALPath, SiteCode, SiteName, SourceSite, RefreshTrigger, UpdateMask, [Action]  
            FROM PkgServers_G WHERE PkgID IN (SELECT UpgradePackageID FROM ClientDeploymentSettings)  
            ) AS S  
        ON T.PkgID = S.PkgID and T.NALPath = S.NALPath  

        WHEN NOT MATCHED THEN  
            INSERT (PkgID, NALPATH, SiteCode, SiteName, SourceSite, LastRefresh, RefreshTrigger, UpdateMask, [Action])  
            VALUES (S.PkgID, S.NALPath, S.SiteCode, S.SiteName, S.SourceSite, GetUTCDate(), S.RefreshTrigger, S.UpdateMask, S.[Action])  
        ;  

        ```  

    -   Fügen Sie Ihrem Laborstandort eine neue Verteilungspunkt-Standortsystemrolle hinzu. Der neue Verteilungspunkt aktualisiert die Präproduktionssammlung mit dem neuen Clientpaket.  

**Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  

##  <a name="improvements-to-microsoft-intune-integration"></a><a name="bkmk_hybrid1"></a> Verbesserungen bei der Microsoft Intune-Integration  
In der Technical Preview-Version 1601 haben wir Unterstützung für die folgenden Features hinzugefügt:  

### <a name="improvements-to-conditional-access"></a>Verbesserungen beim bedingten Zugriff  

-   **Unterstützung des bedingten Zugriffs für PCs, die von Configuration Manager verwaltet werden**  

     Sie können jetzt Richtlinien für den bedingten Zugriff für PCs festlegen, die von Configuration Manager verwaltet werden. Dies erfordert, dass die PCs mit der Kompatibilitätsrichtlinie übereinstimmen, um auf Exchange Online- und SharePoint Online-Dienste zugreifen zu können.  Mithilfe dieser neuen Funktion können Sie auch PCs mithilfe dieser Kompatibilitätsrichtlinie bei Azure AD registrieren sowie die Azure AD-Registrierung überwachen und Berichte dazu erstellen.  

    > [!NOTE]  
    >  Bedingter Zugriff wird unter Windows 10 noch nicht unterstützt.  

    Es folgen die Voraussetzungen für die Verwendung dieses Features:  

    -   Azure Active Directory Premium-Abonnement und AD FS-Synchronisierung.  

    -   Microsoft Intune-Abonnement. Das Microsoft Intune-Abonnement muss in der Configuration Manager-Konsole konfiguriert werden.  

    -   [Voraussetzungen für die automatische Azure AD-Registrierung](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1)  

    Zum Verwenden dieser Option müssen Sie in Configuration Manager eine Kompatibilitätsrichtlinie mit den nachstehend beschriebenen spezifischen Regeln erstellen und eine Richtlinie für den bedingten Zugriff in der Intune-Konsole festlegen.  Um außerdem sicherzustellen, dass nur kompatible PCs Zugriff haben, müssen Sie die Anforderung für Windows-PCs auf die Option **Geräte müssen kompatibel sein** festlegen. Es folgen die Regeln der Kompatibilitätsrichtlinie, die für von Configuration Manager verwaltete PCs gelten.  

    -   **Registrierung in Azure Active Directory erforderlich:** Diese Regel überprüft, ob die Arbeitsplätze des Benutzergeräts und Azure AD miteinander verknüpft sind, und falls nicht, wird das Gerät automatisch in Azure AD registriert. Die automatische Registrierung wird nur unter Windows 8.1 unterstützt. Stellen Sie für Windows 7-PCs eine MSI-Datei bereit, um die automatische Registrierung durchzuführen. Weitere Informationen finden Sie [hier](https://azure.microsoft.com/documentation/articles/active-directory-conditional-access-automatic-device-registration/?rnd=1).  

    -   **Alle mit einem Stichtag älter als eine bestimmte Anzahl von Tagen installierten benötigten Updates:** Diese Regel überprüft, ob das Gerät des Benutzers gemäß dem Stichtag und der Toleranzperiode, die Sie festgelegt haben, über alle erforderlichen Updates verfügt (entsprechend der Angabe in der Regel **Erforderliche automatische Updates**) und installiert automatisch alle ausstehenden Updates.  

    -   **BitLocker-Laufwerkverschlüsselung erfordern:** Dies ist eine Prüfung, ob das primäre Laufwerk (z. B. C:\\) auf dem Gerät mit BitLocker verschlüsselt ist. Wenn die Bitlocker-Verschlüsselung auf dem primären Gerät nicht aktiviert ist, wird der Zugriff auf E-Mail- und SharePoint-Dienste blockiert.  

    -   **Antischadsoftware erfordern:** Dies ist eine Prüfung, um herauszufinden, ob die Antischadsoftware (nur System Center Endpoint Protection oder Windows Defender) aktiviert ist und ausgeführt wird.  
         Falls nicht, wird der Zugriff auf E-Mail- und SharePoint-Dienste blockiert.  

    Endbenutzer, die aufgrund von Complianceproblemen blockiert werden, erhalten im Software Center Informationen zur Compliance. Für sie wird eine nochmalige Richtlinienauswertung ausgelöst, nachdem die Probleme behoben wurden.  

-   **Bedingter Zugriff mit Integritätsnachweisdienst** Sie können jetzt den Zugriff auf E-Mail- und 0365-Dienste basierend auf der Integrität von Geräten gemäß der Meldung des Integritätsnachweisdiensts einschränken.  Darüber hinaus werden Geräte, die von Intune verwaltet werden, in die Geräte-Integritätsberichte einbezogen.  

    Eine neue Kompatibilitätsregel wurde der Configuration Manager-Konsole hinzugefügt, mit der Sie angeben können, ob den Geräten basierend auf ihrem Integritätsstatus der Zugriff erlaubt oder nicht erlaubt werden soll.  Öffnen Sie den **Assistenten zum Erstellen von Kompatibilitätsrichtlinien**, und fügen Sie eine neue Regel hinzu, um diese Regel zu erstellen.  Wählen Sie die Option **Reported as health by Health Attestation Service** (Vom Integritätsnachweisdienst als fehlerfrei gemeldet) für die Bedingung aus, und legen Sie den Wert auf **TRUE** fest.  Dadurch wird sichergestellt, dass nur Geräte, die als fehlerfrei gemeldet werden, auf Ihre Unternehmensressourcen zugreifen können. Details zum Integritätsnachweisdienst und zur Meldung der Integrität der Geräte in Intune finden Sie unter [Nachweis der Geräteintegrität](capabilities-in-technical-preview-1512.md#bkmk_devicehealth).  

-   **Neue Kompatibilitätsrichtlinieneinstellungen:** Die neuen Kompatibilitätsrichtlinieneinstellungen dienen der Verbesserung der Sicherheit und des Schutzes auf Geräten, mit denen auf Unternehmens-E-Mail und SharePoint-Dienste zugegriffen wird:  

    -   **Automatische Updates erforderlich:** Sie können anfordern, dass Geräte ab Windows 8.1 die automatische Installation von Updates zulassen, und auch die Klasse der Updates angeben, die installiert werden.  Sie können wahlweise nur als wichtig markierte Updates oder alle empfohlenen Updates installieren.  

         Öffnen Sie den **Assistenten zum Erstellen von Kompatibilitätsrichtlinien**, und fügen Sie eine neue Regel hinzu, um eine Regel für automatische Updates zu erstellen.  Wählen Sie die **Mindestklassifizierung für erforderliche Updates** als Bedingung aus, und legen Sie den Wert auf einen der verfügbaren Werte fest: **Keine**, **Empfohlen** und **Wichtig**.  

        -   **Keine:** Updates werden nicht automatisch installiert.  

        -   **Empfohlen:** Alle empfohlenen Updates werden installiert.  

        -   **Wichtig:** Nur Updates, die als wichtig eingestuft werden, werden installiert.  

    -   **Kennwort zum Entsperren mobiler Geräte erforderlich:** Wenn diese Einstellung auf **Ja** festgelegt ist, müssen die Endbenutzer ein Kennwort eingeben, bevor er auf sein Gerät zugreifen kann.  

         Öffnen Sie den **Assistenten zum Erstellen von Kompatibilitätsrichtlinien**, und fügen Sie eine neue Regel hinzu, um eine Regel für ein Kennwort zum Entsperren mobiler Geräte zu erstellen. Wählen Sie **Kennwort zum Entsperren eines inaktiven Geräts anfordern** als Bedingung aus, und legen Sie den Wert auf **TRUE** fest.  

    -   **Minuten Inaktivität vor Anforderung des Kennworts:**  Gibt die Leerlaufzeit an, nach der ein Benutzer sein Kennwort erneut eingeben muss.  

         Öffnen Sie den **Assistenten zum Erstellen von Kompatibilitätsrichtlinien**, und fügen Sie eine neue Regel hinzu, um diese Regel zu erstellen. Wählen Sie **Minuten Inaktivität vor erneuter Anforderung des Kennworts** als Bedingung aus, und legen den Wert auf eine der verfügbaren Optionen fest: 1 Minute, 5 Minuten, 15 Minuten, 30 Minuten, 1 Stunde.  

-   **Außerkraftsetzung der Standardregel – Über Intune registrierten und kompatiblen Geräten immer lokalen Zugriff auf Exchange gewähren:**  

     Wenn Sie diese Option aktivieren, dürfen Geräte, die bei Intune registriert sind und mit den Kompatibilitätsrichtlinien übereinstimmen, auf lokales Exchange zugreifen. Diese Regel setzt die Standardregel außer Kraft, was bedeutet, dass, selbst wenn Sie die Standardregel so festlegen, dass der Zugriff isoliert bzw. blockiert wird, registrierte und kompatible Geräte weiterhin auf lokales Exchange zugreifen können.  
     Wählen Sie diese Einstellung, wenn registrierte und kompatible Geräte stets über lokales Exchange Zugriff auf E-Mail haben sollen.  

     Dies wird auf den folgenden Plattformen unterstützt:  Windows Phone 8 und höher, iOS 6 und höher. Android 4.0 und höher, Samsung KNOX Standard 4.0 und höher  

     Wechseln Sie zur Seite **Allgemein** des **Assistenten zur Konfiguration der Richtlinie zum bedingten Zugriff** für lokales Exchange, um diese Option zu verwenden.  

##  <a name="client-online-status"></a><a name="bkmk_clientStatus"></a> Onlinestatus von Clients  
Ab Technical Preview Release 1601 können Sie in der Configuration Manager-Konsole auf einen Blick erkennen, ob ein Client online oder offline ist. Über aktualisierte Symbole und Spalten in den Geräteauflistungen in der Konsole können Sie den Status von Clients in Ihrer Umgebung beurteilen, um Problembereiche und andere Aspekte auszumachen, die ggf. Ihre Aufmerksamkeit erfordern.  

Ein Client ist online, wenn er aktuell mit einer Standortsystemrolle des Typs „Configuration Manager-Verwaltungspunkt“ verbunden ist. Solange der Verwaltungspunkt Ping-ähnliche Nachrichten vom Client empfängt, ist dessen Status online. Wenn der Verwaltungspunkt ca. 5 Minuten keine Nachricht erhält, ist der Status des Clients offline.  

### <a name="icons-for-client-status"></a>Symbole für den Clientstatus  

|||  
|-|-|  
|![Symbol für den Onlinestatus des Clients](media/online-status-icon.png)|Client ist online.|  
|![Symbol für den Offlinestatus des Clients](media/offline-status-icon.png)|Client ist offline.|  
|![Symbol für den unbekannten Status des Clients](media/unknown-status-icon.png)|Clientstatus ist unbekannt.|  

### <a name="prerequisites"></a>Voraussetzungen  
 Für den Onlinestatus eines Clients gelten keine Voraussetzungen. Sie können mit seiner Nutzung beginnen, sobald Configuration Manager Technical Preview 1601 installiert ist.  

### <a name="limitations"></a>Einschränkungen  
 Der Onlinestatus des Clients ist nur für Windows-Computer mit installiertem Configuration Manager-Client verfügbar. Der Onlinestatus des Clients wird nicht für Macintosh-, Linux- oder UNIX-Computer bzw. für Geräte mit lokaler Geräteverwaltung unterstützt.  

### <a name="to-view-client-online-status"></a>So zeigen Sie den Onlinestatus von Clients an  

1. Navigieren Sie in der Configuration Manager-Konsole zu **Bestand und Kompatibilität > Übersicht > Geräte**.  

2. Klicken Sie mit der rechten Maustaste auf die Spaltenüberschrift, und klicken Sie dann auf die Felder für den Onlinestatus des Clients, um ihn der Geräteansicht hinzuzufügen. Die Felder heißen wie folgt:  

   -   Der**Onlinestatus des Geräts** gibt an, ob der Client derzeit online oder offline ist.  

   -   **Zuletzt online** gibt an, wann sich der Status des Clients von offline in online geändert hat.  

   -   **Zuletzt offline** gibt an,wann sich der Status des Clients von online in offline geändert hat.  

   Um die jüngsten Änderungen am Clientstatus anzuzeigen, aktualisieren Sie die Konsole.  

##  <a name="improvements-to-application-management"></a><a name="bkmk_appmgmt1601"></a> Verbesserungen bei der Anwendungsverwaltung  
 In der Technical Preview-Version 1601 haben wir Unterstützung für die folgenden Features hinzugefügt:  

### <a name="manage-volume-purchased-apps-for-ios-devices"></a>Verwalten von Apps für iOS-Geräte, die über ein Volumenprogramm erworben wurden  
 Einige App-Stores bieten die Möglichkeit, mehrere Lizenzen für eine App zu erwerben, die in Ihrem Unternehmen ausgeführt werden soll. Dadurch können Sie den Verwaltungsaufwand reduzieren, der durch das Nachverfolgen mehrerer erworbener App-Kopien entsteht.  

 Configuration Manager unterstützt Sie nun bei der Verwaltung von Apps, die Sie über ein solches Programm erworben haben, indem die Lizenzinformationen aus dem App-Store importiert werden und nachverfolgt wird, wie viele Lizenzen Sie verwendet haben.  

 Details finden Sie unter [Verwalten von Apps, die über ein Volumenprogramm mit Configuration Manager erworben wurden](https://technet.microsoft.com/library/mt627954.aspx).  

### <a name="ios---app-configuration-for-applicationsbr-hybrid"></a>iOS – App-Konfiguration für Einstellungen<br />Hybrid  
 Einige iOS-Apps unterstützen die Vorabkonfiguration von Einstellungen, wie z. B. eines Servers oder einer Datenbank, mit dem/der die Anwendung eine Verbindung herstellen soll. Configuration Manager unterstützt jetzt die Bereitstellung von App-Konfigurationsrichtlinien auf dem Gerät, wodurch der Benutzer die App sofort nutzen kann, ohne diese Informationen kennen zu müssen. Entwickler müssen diese Funktionalität in ihren Apps aktivieren.  

 Eine begrenzte Anzahl veröffentlichter Apps unterstützt derzeit die Vorabkonfiguration von Einstellungen, die ggf. auch von intern entwickelten spartenspezifischen Apps unterstützt werden.  

#### <a name="prerequisites-for-this-scenario"></a>Voraussetzungen für dieses Szenario  

-   Sie müssen ein Microsoft Intune-Abonnement zu Configuration Manager hinzugefügt haben.  

-   Sie müssen dem Intune-Abonnement ein gültiges Apple APNs-Zertifikat hinzugefügt haben.  

-   Sie müssen eine iOS-Anwendung bereitgestellt haben, die die Anwendungskonfiguration unterstützt.  

#### <a name="try-it-out"></a>Probieren Sie es aus!  
 Wenn die oben genannten Voraussetzungen erfüllt sind, müssen Sie eine Configuration Manager-Anwendung erstellen, die einen iOS-Bereitstellungstyp verwendet. Die App, die Sie verwenden, muss die Anwendungskonfiguration unterstützen. Konsultieren Sie die Dokumentation des App-Herstellers, um zu erfahren, welche spezifischen Elemente (Name-Wert-Paare) Sie konfigurieren können.  

 Anschließend ordnen Sie während der Bereitstellung der App die App-Konfigurationsrichtlinie dem iOS-Bereitstellungstyp zu. Sie können die Richtlinie auch mithilfe des Knotens **App-Konfigurationsrichtlinien** bereitstellen, der für eine vorhandene App und Sammlung bestimmt ist.  

 Versuchen Sie, die folgende Aufgabe auszuführen, und verwenden Sie dann die Feedbackinformationen oben in diesem Thema, um uns Ihre Erfahrungen mitzuteilen:  

-   Wenn Sie eine iOS-App haben, die die App-Konfiguration unterstützt, konsultieren Sie die Dokumentation des App-Herstellers, um die Name-Werte-Paare zu bestimmen, die Sie zum Konfigurieren der Anwendung angeben müssen.  

-   Starten Sie den **Assistenten zum Erstellen einer App-Konfigurationsrichtlinie**. Versuchen Sie auf der Seite **iOS-Richtlinie** des Assistenten die Name-Wert-Paare hinzuzufügen, die Sie in der Dokumentation des App-Herstellers gefunden haben, oder importieren Sie eine XML-Datei mit den erforderlichen Werten.  

-   Ordnen Sie im **Assistenten zum Bereitstellen von Software** auf der Seite **App-Konfigurationsrichtlinie** die von Ihnen erstellte App-Konfigurationsrichtlinie einem kompatiblen Bereitstellungstyp der Anwendung zu.  

##  <a name="improvements-to-compliance-settings"></a><a name="bkmk_compliance1601"></a> Verbesserungen für Kompatibilitätseinstellungen  
 In der Technical Preview-Version 1601 haben wir Unterstützung für die folgenden Features hinzugefügt:  

### <a name="microsoft-edge-browser-settings"></a>Microsoft Edge-Browsereinstellungen  
 Neue Einstellungen für den Microsoft Edge-Browser wurden zum Konfigurationselement **Windows 8.1 und Windows 10** hinzugefügt (Einstellungen gelten nur für Windows 10-Geräte).  

 Wählen Sie auf der Seite für die **Geräteeinstellungen** des Konfigurationselements im **Assistenten zum Erstellen von Konfigurationselementen** die Option **Microsoft Edge** aus, um die neuen Einstellungen anzuzeigen.  

 Weitere Informationen finden Sie unter [How to create configuration items for Windows 8.1 and Windows 10 devices managed without the Configuration Manager client (Erstellen von Konfigurationselementen für Windows 8.1- und Windows 10-Geräte, die ohne den Configuration Manager-Client verwaltet werden)](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="compliance-settings-for-windows-10-team-devices"></a>Kompatibilitätseinstellungen für Windows 10 Team-Geräte  
 Verwenden Sie diese neuen Kompatibilitätseinstellungen zum Konfigurieren von Geräten, auf denen Windows 10 Team ausgeführt wird, z. B. von Surface Hub-Geräten.  

 Wählen Sie auf der Seite für die **Geräteeinstellungen** des Konfigurationselements im **Assistenten zum Erstellen von Konfigurationselementen** die Option **Windows 10-Team** aus, um die neuen Einstellungen anzuzeigen.  

 Weitere Informationen finden Sie unter [How to create configuration items for Windows 8.1 and Windows 10 devices managed without the Configuration Manager client (Erstellen von Konfigurationselementen für Windows 8.1- und Windows 10-Geräte, die ohne den Configuration Manager-Client verwaltet werden)](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  

### <a name="android---kiosk-mode-for-samsung-knox-standardbr-hybrid"></a>Android – Kioskmodus für Samsung KNOX Standard<br />Hybrid  
 Sie können im Kioskmodus ein Gerät so sperren, dass nur bestimmte Features funktionieren. Beispielsweise können Sie festlegen, dass auf einem Gerät nur eine von Ihnen angegebene verwaltete App ausgeführt werden kann, oder Sie können die Lautstärkeregler eines Geräts deaktivieren. Diese Einstellungen können für ein Demomodell eines Geräts oder ein Gerät nützlich sein, das nur eine bestimmte Funktion ausführen soll, wie z. B. ein Point-of-Sale-Gerät. Diese Einstellungen sind nicht im Konfigurationselement **Windows 8.1 und Windows 10** (Einstellungen gelten nur für Windows 10-Geräte) für Samsung KNOX Standard-Geräte verfügbar.  

 Um die neuen Einstellungen anzuzeigen, wählen Sie auf der Seite für die **Geräteeinstellungen** des Konfigurationselements im Assistenten zum **Erstellen von Konfigurationselementen** die Option **Kioskmodus – Samsung KNOX** aus.  

 Weitere Informationen finden Sie unter [How to create configuration items for Windows 8.1 and Windows 10 devices managed without the Configuration Manager client (Erstellen von Konfigurationselementen für Windows 8.1- und Windows 10-Geräte, die ohne den Configuration Manager-Client verwaltet werden)](../../mdm/deploy-use/create-configuration-items-for-windows-8.1-and-windows-10-devices-managed-without-the-client.md).  
