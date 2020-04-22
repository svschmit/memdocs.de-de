---
title: Funktionen in Technical Preview 1604
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über Features, die in der Technical Preview-Version 1604 für Configuration Manager zur Verfügung stehen.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 684a5559-9e6e-469b-86ae-e768e9f0c9ac
author: aczechowski
ROBOTS: NOINDEX
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: ef37b5f99cda8022166972cdc015a3c60d0458a6
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705628"
---
# <a name="capabilities-in-technical-preview-1604-for-configuration-manager"></a>Funktionen in der Technical Preview 1604 für Configuration Manager

*Gilt für: Configuration Manager (Technical Preview-Branch)*

In diesem Artikel werden die Features vorgestellt, die in der Technical Preview-Version 1604 für Configuration Manager verfügbar sind. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen.      Bevor Sie diese Version der Technical Preview installieren, lesen Sie das einführende Thema [Technical Preview für Configuration Manager](../../core/get-started/technical-preview.md), um sich mit den allgemeinen Anforderungen und Einschränkungen bei der Verwendung einer Technical Preview vertraut zu machen und um zu erfahren, wie Sie Updates für Versionen durchführen und Feedback zu den Features in einer Technical Preview geben können.  

 Im Folgenden werden neue Funktionen aufgelistet, die Sie mit dieser Version ausprobieren können.  

##  <a name="manage-volume-purchased-apps-from-the-windows-store-for-business"></a><a name="BKMK_WindowsVPP"></a> Verwalten von per Volumenlizenz aus dem Windows Store für Unternehmen erworbenen Apps  
 Im [Windows Store für Unternehmen](https://www.microsoft.com/business-store) können Sie Apps für Ihre Organisation finden und entweder einzeln oder per Volumenlizenz erwerben. Indem Sie den Store mit Configuration Manager verbinden, können Sie per Volumenlizenz erworbene Apps in der Configuration Manager-Konsole verwalten, zum Beispiel:  

-   Sie können die Liste der erworbenen Apps mit Configuration Manager synchronisieren  

-   Synchronisierte Apps werden in der Configuration Manager-Konsole angezeigt, und Sie können sie wie alle anderen Apps bereitstellen.  

-   In der Configuration Manager-Konsole können Sie überwachen, wie viele Lizenzen verfügbar sind und wie viele Lizenzen gerade verwendet werden.  

### <a name="try-it-out"></a>Probieren Sie es aus!  

##### <a name="scenario-1-set-up-windows-store-for-business-synchronization"></a>Szenario 1: Einrichten der Synchronisierung mit Windows Store für Unternehmen  

1.  Registrieren Sie Configuration Manager als „Web-Anwendung und/oder Web-API“-Verwaltungstool in Azure Active Directory. Sie erhalten eine Client-ID, die Sie später benötigen.  

    1.  Wählen Sie im Knoten **Active Directory** von [https://manage.windowsazure.com](https://manage.windowsazure.com) Ihr Azure Active Directory aus, und klicken Sie dann auf **Anwendungen** > **Hinzufügen**.  

    2.  Klicken Sie auf **Eine von meinem Unternehmen entwickelte Anwendung hinzufügen**.  

    3.  Geben Sie einen Namen für die App ein, wählen Sie **Web-App** und/oder **Web-API** aus, und klicken Sie dann auf den Pfeil „Weiter“.  

    4.  Geben Sie die gleiche URL für die **Registrierungs-URL** und die **App-ID-URI** ein.  Dabei kann es sich um eine beliebige URL handeln, die nicht in eine reale Adresse aufgelöst werden muss. Sie können z.B. **https://&lt;Ihre Domäne\>/sccm** eingeben.  

    5.  Schließen Sie den Assistenten ab.  

2.  Erstellen Sie in Azure Active Directory einen Clientschlüssel für das registrierte Verwaltungstool.  

    1.  Markieren Sie die App, die Sie soeben erstellt haben, und klicken Sie auf **Konfigurieren**.  

    2.  Wählen Sie unter **Schlüssel** eine Dauer aus der Liste aus, und klicken Sie anschließend auf **Speichern**.  Dadurch wird ein neuer Clientschlüssel erstellt.  Verlassen Sie diese Seite nicht, bevor Sie Windows Store für Unternehmen erfolgreich in Configuration Manager eingebunden haben.  

3.  Konfigurieren von Configuration Manager als Speicherverwaltungstool im Windows Store für Unternehmen.  

    1.  Öffnen Sie [https://businessstore.microsoft.com/en-us/managementtools](https://businessstore.microsoft.com/en-us/managementtools), und melden Sie sich an, wenn Sie dazu aufgefordert werden.  

    2.  Akzeptieren Sie gegebenenfalls die Nutzungsbedingungen.  

    3.  Klicken Sie unter **Verwaltungstools** auf **Verwaltungstool hinzufügen**.  

    4.  Geben Sie unter **Tool nach Namen suchen** den Namen der App ein, die Sie zuvor in AAD erstellt haben, und klicken Sie anschließend auf **Hinzufügen**.  

    5.  Klicken Sie neben der App, die Sie gerade importiert haben, auf **Aktivieren**.  

    6.  Klicken Sie im Assistenten **Offline lizenzierte Apps anzeigen** auf **Ja**, wenn Sie den Erwerb offline lizenzierter Apps zulassen möchten.  

4.  Kaufen Sie mindestens eine App aus dem Windows Store für Unternehmen.  

5.  Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Verwaltung** den Eintrag **Clouddienste**, und klicken Sie dann auf **Windows Store für Unternehmen**.  

6.  Klicken Sie auf der Registerkarte **Start** in der Gruppe **Erstellen** auf **Windows Store für Unternehmen-Konto hinzufügen**.  

7.  Fügen Sie Mandanten-ID, Client-ID und Clientschlüssel aus Azure Active Directory hinzu, und schließen Sie den Assistenten ab.  

8.  Sobald Sie fertig sind, wird das von Ihnen konfigurierte Konto in der Liste der **Windows Store für Unternehmen-Konten** in der Configuration Manager-Konsole aufgeführt.  

##### <a name="scenario-2-create-and-deploy-a-configuration-manager-application-from-a-windows-store-for-business-offline-licensed-app"></a>Szenario 2: Erstellen und Bereitstellen einer Configuration Manager-App aus einer offline lizenzierten App aus dem Windows Store für Unternehmen  

1.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** der Configuration Manager-Konsole den Eintrag **Anwendungsverwaltung**, und klicken Sie anschließend auf **Lizenzinformationen für Store-Apps**.  

2.  Die Liste der **aus dem Windows Store für Unternehmen erworbenen Apps** zeigt eine Liste von Apps, die aus dem Store synchronisiert wurden. Wählen Sie zunächst die App aus, die Sie bereitstellen möchten. Klicken Sie anschließend auf der Registerkarte **Start** in der Gruppe **Erstellen** auf **Anwendung erstellen**.  

3.  Eine Configuration Manager-App wird erstellt, die eine App aus dem Windows Store für Unternehmen enthält. Sie können diese App dann wie jede andere Configuration Manager-App bereitstellen und überwachen.  

##  <a name="improvements-to-microsoft-passport-for-work-management"></a><a name="BKMK_PFW"></a> Verbesserungen an der Microsoft Passport for Work-Verwaltung  
 Sie können nun Passport for Work-Richtlinien für in Domänen eingebundene Windows 10-Geräte bereitstellen, die vom Configuration Manager-Client verwaltet werden.  

##  <a name="option-for-clients-to-switch-to-a-new-software-update-point"></a><a name="bkmk_switchsup"></a> Option für Clients zum Wechsel zu einem neuen Softwareupdatepunkt  
 In Technical Preview 1604 können Sie die Option zum Wechsel zu einem neuen Softwareupdatepunkt für Configuration Manager-Clients aktivieren, wenn beim aktiven Softwareupdatepunkt Probleme auftreten. Für diese Option müssen an einem primären Standort mehrere Softwareupdatepunkte verfügbar sein. Aktivieren Sie diese Option auf einer Gerätesammlung und einmal aktiviert, suchen die Clients in der Sammlung während der nächsten Überprüfung nach einem anderen Softwareupdatepunkt, wenn der Client keine Verbindung mit dem aktiven Softwareupdatepunkt herstellen kann. Je nach Ihrer WSUS-Konfigurationseinstellung (Updateklassifizierungen, Produkte, usw.) führt der Wechsel auf einen neuen Softwareupdatepunkt zu zusätzlichem Netzwerkdatenverkehr. Aus diesem Grund sollten Sie diese Option nur bei Bedarf verwenden.  

#### <a name="to-enable-the-option-to-switch-software-update-points"></a>So aktivieren Sie die Option zum Wechseln von Softwareupdatepunkten  

1.  Gehen Sie in der Configuration Manager-Konsole zu **Bestand und Kompatibilität > Übersicht > Gerätesammlungen**.  

2.  Klicken Sie auf der Registerkarte **Start** in der Gruppe **Sammlung** auf **Clientbenachrichtigung**, und klicken Sie anschließend auf **Zum nächsten Softwareupdatepunkt wechseln**.  

> [!NOTE]  
>  Diese Option ist nur an Standorten verfügbar, die über mehrere Softwareupdatepunkte verfügen.  

##  <a name="client-settings-to-manage-client-cache-settings-and-client-peer-cache"></a><a name="bkmk_peercache"></a> Clienteinstellungen zum Verwalten von Clientcacheeinstellungen und Clientpeercache  
 In der Technical Preview-Version 1604 werden zwei neue Einstellungen für Geräteclients eingeführt, die sich auf die Verwendung des Clientcaches auswirken. Beide sind einzeln verwendbar, werden jedoch auf demselben Eigenschaftenblatt für Clienteinstellungen konfiguriert und helfen Ihnen beim Verwalten der Bereitstellung von Inhalten für Ihre Clients an Remotestandorten.  

-   Die erste Option ist der **Clientpeercache**, eine integrierte Configuration Manager-Lösung für das Freigeben von Inhalten für andere Clients direkt aus ihrem lokalen Cache. Damit Peercacheclients Inhalte gemeinsam nutzen können, müssen sie Mitglieder der gleichen Begrenzungsgruppe sein. Der Peercache ersetzt nicht die Verwendung anderer Lösungen wie BranchCache, sondern wird parallel eingesetzt, um Ihnen weitere Optionen zur Verfügung zu stellen und herkömmliche Lösungen für die Inhaltsbereitstellung (z.B. Verteilungspunkte) zu erweitern.  

     Nachdem Sie Clienteinstellungen bereitgestellt haben, die den Peercache für eine Sammlung aktivieren, können Mitglieder dieser Sammlung als Peerinhaltsquelle für andere Clients in der Begrenzungsgruppe fungieren.  Der Client, der als Peerinhaltsquelle fungiert, wird eine Liste der verfügbaren Inhalte einreichen, die er auf seinem Verwaltungspunkt zwischengespeichert hat. Wenn der nächste Client innerhalb dieser Begrenzungsgruppe diesen Inhalt anfordert, wird die Peercachequelle dann als mögliche Inhaltsquelle zusammen mit allen Verteilungspunkten angeboten, die als schnell konfiguriert sind. Der Client wählt eine zufällige Inhaltsquelle aus diesem kombinierten Pool von Inhaltsquellen aus. Clients werden nur Inhalte von einem Verteilungspunkt suchen, der als langsam konfiguriert wurde, wenn keine schnellen Verteilungspunkte oder Peercachequellen in der Begrenzungsgruppe vorhanden sind.  

-   Mit der zweiten neuen Einstellung können Sie die **Cachegrößen auf Clients verwalten**. Sie können den Cache auf eine maximale Größe in Megabyte und auf einen maximalen Prozentanteil des Speicherplatzes auf dem Laufwerk des Clients festlegen.  Der Client erzwingt die Einstellung, die zuerst erreicht wird.  

Um besser zu verstehen, wann der Clientpeercache erfolgreich verwendet wird, sehen Sie sich das Dashboard **Clientdatenquellen** an. Wechseln Sie in der Konsole zu **Überwachung > Clientstatus > Clientdatenquellen**. Hier können Sie einen Zeitraum auswählen, der auf das Dashboard angewendet werden soll. Anschließend können Sie in der Anzeige die Begrenzungsgruppe oder das Paket auswählen, für die bzw. das Sie Informationen anzeigen möchten. Beim Anzeigen der Informationen können Sie Ihre Maus über der Oberfläche bewegen, um weitere Details zu den verschiedenen Inhalts- oder Richtlinienquellen zu erhalten.  

 Sie können auch einen neuen Bericht, **Clientdatenquellen – Zusammenfassung**, verwenden, um eine Zusammenfassung der Clientdatenquellen für die einzelnen Begrenzungsgruppen anzuzeigen.   
**Anforderungen für die Verwendung des Peercaches:**  

-   Sie müssen Ihren Standort mit einem **Netzwerkzugriffskonto** konfigurieren, das auf jedem Client **Vollzugriff** auf den Cacheordner besitzt. Standardmäßig ist dies **%windir%\ccmcache**  

-   Clients können Inhalte nur mithilfe von Peercache übertragen, wenn sie Mitglieder der gleichen Begrenzungsgruppe sind.  

#### <a name="to-configure-client-peer-cache-client-settings"></a>So konfigurieren Sie Clienteinstellungen für Clientpeercache  

1.  Beide Einstellungen werden auf derselben Seite der Clienteinstellungen konfiguriert. Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung > Clienteinstellungen**, und öffnen Sie dann die Geräteclienteinstellungen, die Sie verwenden möchten. Außerdem können Sie das Objekt „Clientstandardeinstellungen“ ändern.  

2.  Wählen Sie aus der Liste der verfügbaren Einstellungen **Clientcacheeinstellungen** aus.  

3.  Um die Größe des Caches zu verwalten, legen Sie **Clientcachegröße konfigurieren** auf **Ja** fest. Anschließend können Sie die maximale Cachegröße in MB oder als Prozentsatz des Client-Speicherplatzes konfigurieren.  

4.  Setzen Sie zum Aktivieren von Clients zur Teilnahme an Clientpeercache **Configuration Manager-Client in vollständigem Betriebssystem zur Freigabe von Inhalten aktivieren** auf **Ja** fest. Anschließend können Sie die Ports konfigurieren, die Clients verwenden, einschließlich HTTP oder HTTPS.  

### <a name="try-it-out"></a>Probieren Sie es aus!  
 Versuchen Sie, die folgenden Aufgaben durchzuführen, und verwenden Sie dann die Feedbackinformationen oben in diesem Thema, um uns Ihre Erfahrungen mitzuteilen:  

1.  Ändern Sie die Clienteinstellungen, um eine neue Größe für den Clientcache anzugeben, und bestätigen Sie diese Einstellung dann auf einem Client.  

2.  Verwenden Sie die Clienteinstellungen, um mehrere Clients für die Verwendung des Peercaches zu konfigurieren.  

3.  Stellen Sie Inhalt für Clients bereit, damit einige oder die meisten Clients diese Inhalte von einem anderen Client über den Peercache abrufen können.  Sie können die verwendete Inhaltsquelle überprüfen, indem Sie das neue Dashboard ansehen.  

    > [!NOTE]  
    >  Um diese Aufgabe mit der technischen Vorschau und einem einzelnen Verteilungspunkt durchzuführen, konfigurieren Sie den Verteilungspunkt für die Netzwerkadresse all Ihrer Clients als langsam. Verteilen Sie dann den Inhalt an einen einzelnen Client.  Nachdem der Client den Inhalt erhalten hat, können Sie den Inhalt an weitere Clients verteilen. Diese sollten eher lokale Peers als Inhaltsquelle finden, bevor sie den Verteilungspunkt verwenden, der vom Standort des Clients aus als langsam gilt.  

##  <a name="support-for-passport-for-work-as-a-ksp"></a><a name="bkmk_passport"></a> Unterstützung für Passport for Work als KSP  
 Configuration Manager ermöglicht die Integration in Microsoft Passport for Work. Dies ist eine alternative Anmeldemethode, die Active Directory oder ein Azure Active Directory-Konto verwendet, um ein Kennwort, eine Smartcard oder eine virtuelle Smartcard zu ersetzen.  
Mit Passport können Sie anstelle eines Kennworts eine Benutzeraktion zur Anmeldung verwenden. Eine Benutzeraktion kann eine einfache PIN, eine biometrische Authentifizierung wie Windows Hello oder ein externes Gerät sein, z. B. ein Fingerabdruckleser.  

-   Mit Configuration Manager können Sie steuern, welche Gesten Benutzer zum Anmelden verwenden können und welche nicht. Außerdem können Sie die Anforderungen an die PIN-Komplexität konfigurieren.  

-   Sie können Authentifizierungszertifikate im Passport for Work-Schlüsselspeicheranbieter (Key Storage Provider, KSP) speichern.  

Wenn ein Benutzer eine Passport-PIN erstellt, sendet Windows eine Benachrichtigung, auf die Configuration Manager lauscht.  So kann Configuration Manager schnell erkennen, welche Benutzer eine Passport-PIN erstellt haben. Configuration Manager kann diesen Benutzern dann auch neue Zertifikate ausstellen, wenn Passport als Schlüsselspeicheranbieter in einem Zertifikatprofil dient.  

##  <a name="on-premises-device-health-attestation"></a><a name="bkmk_onpremdha"></a> Integritätsnachweis für lokale Geräte  
 Der Integritätsnachweis für Windows 10-Geräte kann jetzt so konfiguriert werden, dass die Kommunikation über die lokale Infrastruktur erfolgt.  Administratoren können angeben, ob die Berichterstellung über die Cloud oder über lokale Ressourcen durchgeführt wird.  Wenn für die Berichterstellung für den Integritätsnachweis **lokal** ausgewählt wird, kann ein URI für den Dienst angegeben werden. Dadurch können Client-PCs ohne Internetzugriff Geräte nutzen, aktivieren und verwalten, die den Integritätsnachweis verwenden.  

#### <a name="enable-health-attestation-for-on-premises-devices"></a>Aktivieren des Integritätsnachweises für lokale Geräte  

1.  Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Übersicht** > **Clienteinstellungen**, und legen Sie anschließend **Lokalen Integritätsnachweisdienst verwenden** auf **Ja**fest.  

2.  Geben Sie die **URL für lokalen Integritätsnachweisdienst**an, und klicken Sie anschließend auf **OK**.  

Konfigurieren Sie zu Testzwecken den lokalen Health Attestation-Dienst anhand der Client-Agent-Einstellungen.  

##  <a name="smartlock-setting-for-android-devices"></a><a name="BKMK_Smart"></a> SmartLock-Einstellung für Android-Geräte  
 Eine neue Einstellung, **Allow SmartLock and other trust agents** (SmartLock und andere vertrauenswürdigen Agents zulassen), wurde dem Konfigurationselement **Android und Samsung KNOX** hinzugefügt. Mit dieser Einstellung können Sie das Smart Lock-Feature auf kompatiblen Android-Geräten steuern. Diese Telefonfunktion wird manchmal als Vertrauens-Agent bezeichnet und ermöglicht Ihnen das Deaktivieren oder Umgehen des Kennworts für den Gerätesperrbildschirm, wenn sich das Gerät an einem vertrauenswürdigen Standort befindet, z. B. wenn es mit einem bestimmten Bluetooth-Gerät verbunden ist oder sich in der Nähe eines NFC-Tags befindet. Mit dieser Einstellung können Sie verhindern, dass Endbenutzer Smart Lock konfigurieren.  
