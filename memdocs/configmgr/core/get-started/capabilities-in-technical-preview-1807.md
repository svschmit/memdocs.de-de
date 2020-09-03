---
title: Technical Preview 1807
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über neue Features, die mit dem Technical Preview-Branch Version 1807 für Configuration Manager zur Verfügung stehen.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bcde47a7-433e-4944-964b-539b17d15d64
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: bc848cd1f6365b5a94c915a00517ca0a4abb8e4a
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88995312"
---
# <a name="capabilities-in-configuration-manager-technical-preview-version-1807"></a>Funktionen in der Technical Preview-Version 1807 für Configuration Manager 

*Gilt für: Configuration Manager (Technical Preview-Branch)*

In diesem Artikel werden die Features vorgestellt, die in der Technical Preview-Version 1807 für Configuration Manager verfügbar sind. Installieren Sie diese Version, um Features für Ihren Technical Preview-Standort zu aktualisieren oder neue Features hinzuzufügen. 

Lesen Sie den [Technical Preview](technical-preview.md)-Artikel vor der Installation dieses Updates. In diesem Artikel erhalten Sie Informationen zu den allgemeinen Anforderungen und Einschränkungen, die für die Verwendung der Technical Preview gelten. Außerdem erfahren Sie, wie Sie Updates zwischen den Versionen ausführen und Feedback übermitteln.     


<!--  Known Issues Template
## Known issues 

### <a name="ki_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



## <a name="known-issues"></a>Bekannte Probleme 

### <a name="issues-with-microsoft-365-software-updates"></a><a name="ki_o365"></a> Probleme bei Microsoft 365-Softwareupdates
<!--521365-->
Wenn Sie Microsoft 365-Updates mit Technical Preview-Branches in den Versionen 1806 und 1806.2 verwalten, können sie möglicherweise nicht auf Clients installiert werden. 

#### <a name="workaround"></a>Problemumgehung
- Löschen Sie vorhandene Bereitstellungspakete und Softwareupdategruppen für Microsoft 365.  

- Ab dem 31. Juli 2018 werden Microsoft 365-Softwareupdates synchronisiert und nur die neuesten Updates bereitgestellt.  



</br>

**In den folgenden Abschnitten werden die neuen Features beschrieben, die in dieser Version getestet werden können:**  


## <a name="community-hub"></a><a name="bkmk_hub"></a> Community Hub
<!--1357766-->

Der Community Hub ist eine zentrale Plattform, über die nützliche Configuration Manager-Objekte mit anderen Benutzern ausgetauscht werden können. Navigieren Sie zum neuen **Community**-Arbeitsbereich in der Configuration Manager-Konsole, und wählen Sie den **Hub**-Knoten aus. Laden Sie über den Community Hub die folgenden Arten von Configuration Manager-Objekten herunter: 
- Skripts
- Konfigurationselemente

![Configuration Manager-Konsole: Arbeitsbereich „Community“ > Knoten „Hub“](media/1357766-hub.png)

Um weitere Details zu einem verfügbaren Element anzuzeigen, klicken Sie im Hub darauf. Klicken Sie auf der Detailseite auf **Herunterladen**, um das Element abzurufen. Wenn Sie ein Element aus dem Hub herunterladen, wird es automatisch zu Ihrem Standort hinzugefügt. 

![Configuration Manager-Konsole: Arbeitsbereich „Community“ > Knoten „Hub“ > Detailseite](media/1357766-hub-details.png)

Der Arbeitsbereich **Community** enthält auch die folgenden Knoten:

- **Dokumentation:** Dieser Knoten enthält die [Dokumentationsbibliothek](/sccm/) von Configuration Manager.  

- **Feedback:** Dieser Knoten verweist auf die [UserVoice-Website](https://configurationmanager.uservoice.com/) von Configuration Manager.  


### <a name="prerequisites"></a>Voraussetzungen

- Die Configuration Manager-Konsole muss unter einem Clientbetriebssystem ausgeführt werden.  

    - Alternative Option, die jedoch nicht empfohlen wird: Deaktivieren Sie auf einem Serverbetriebssystem die [verstärkte Sicherheitskonfiguration für Internet Explorer](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd883248(v=ws.10)).

- Der Computer mit der Konsole benötigt Internetzugriff und -konnektivität mit den folgenden Standorten:  
    - `https://aka.ms`  
    - `https://comfigmgr-hub.azurewebsites.net`  
    - `https://configmgronline.visualstudio.com`  


### <a name="known-issue"></a>Bekanntes Problem

Das Beitragen von Elementen zum Hub ist in dieser Version zurzeit nicht verfügbar. 



## <a name="specify-the-drive-for-offline-os-image-servicing"></a><a name="bkmk_osd"></a> Angeben des Laufwerks für die Offlinewartung von Betriebssystemimages  
<!--1358924-->

Geben Sie basierend auf Ihrem [UserVoice-Feedback](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/33506009-gui-option-for-offline-os-image-servicing-drive) nun das Laufwerk an, das Configuration Manager während der Offlinewartung von Betriebssystemimages verwendet. Dieser Prozess kann eine große Menge an Speicherplatz auf dem Datenträger mit temporären Dateien beanspruchen, sodass Ihnen diese Option Flexibilität bei der Auswahl des zu verwendenden Laufwerks bietet. 


### <a name="try-it-out"></a>Probieren Sie es aus!

Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie uns dann Ihr [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) mit Ihrer Meinung zu dem Feature.

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Standorte** aus. Klicken Sie im Menüband auf **Standortkomponenten konfigurieren**, und wählen Sie dann **Softwareupdatepunkt** aus.  

2. Wechseln Sie zu der Registerkarte **Offlinewartung**, und geben Sie die Option für **Ein bei der Offlinewartung von Images zu verwendendes lokales Laufwerk** an.  

Diese Einstellung ist standardmäßig auf **Automatisch** festgelegt. Mit diesem Wert wählt Configuration Manager das Laufwerk aus, auf dem es installiert ist. 

Bei der Offlinewartung speichert Configuration Manager temporäre Dateien im Ordner `<drive>:\ConfigMgr_OfflineImageServicing`. Es bindet zudem die Betriebssystemimages in diesem Ordner ein. 

Überprüfen Sie die Protokolldatei **OfflineServicingMgr.log**. 



## <a name="co-managed-device-sync-activity-from-intune"></a><a name="bkmk_comgmt"></a> Synchronisierungsaktivität gemeinsam verwalteter Geräte aus Intune
<!--1358565-->

Zeigen Sie in der Configuration Manager-Konsole an, ob ein gemeinsam verwaltetes Gerät in Microsoft Intune aktiv ist. Dieser Zustand basiert auf Daten aus [Intune Data Warehouse](/intune/reports-nav-create-intune-reports). Das Dashboard **Clientstatus** in der Configuration Manager-Konsole zeigt **Inaktive Clients mit Intune** an. Diese neue Kategorie ist für gemeinsam verwaltete Geräte bestimmt, die bei Configuration Manager inaktiv sind, aber in der letzten Woche mit dem Intune-Dienst synchronisiert wurden.


### <a name="try-it-out"></a>Probieren Sie es aus!

Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie uns dann Ihr [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) mit Ihrer Meinung zu dem Feature.

Wenn Sie Ihren Standort bereits für die Co-Verwaltung eingerichtet haben, gehen Sie wie folgt vor: 

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie den Eintrag **Cloud Services**, und wählen Sie den Knoten **Co-Verwaltung** aus. Klicken Sie im Menüband auf **Eigenschaften**.  

2. Wechseln Sie zur Registerkarte **Berichterstellung**. Klicken Sie auf **Anmelden**, und authentifizieren Sie sich. Klicken Sie dann auf **Aktualisieren**, um Leseberechtigungen für Intune Data Warehouse zu aktivieren.  

3. Nachdem der Standort mit Intune synchronisiert wurde, navigieren Sie zum Arbeitsbereich **Überwachung**, und wählen Sie den Knoten **Clientstatus** aus. Navigieren Sie im Abschnitt **Clientstatus insgesamt** zu der Zeile für **Inaktive Clients mit Intune**.  

Weitere Informationen zur Aktivierung der Co-Verwaltung finden Sie unter [Co-Verwaltung für Windows 10-Geräte](../../comanage/overview.md).



## <a name="repair-applications"></a><a name="bkmk_app-repair"></a> Reparieren von Anwendungen
<!--1357866-->

Geben Sie nun basierend auf Ihrem [UserVoice-Feedback](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/8365071-force-reinstall-of-application) eine Reparaturbefehlszeile für die Bereitstellungstypen „Windows Installer“ und „Skriptinstallationsprogramm“ an. 


### <a name="try-it-out"></a>Probieren Sie es aus!

Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie uns dann Ihr [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) mit Ihrer Meinung zu dem Feature.

1. Öffnen Sie in der Configuration Manager-Konsole die Eigenschaften des Bereitstellungstyps „Windows Installer“ oder „Skriptinstallationsprogramm“.  

2. Wechseln Sie zur Registerkarte **Programme**. Geben Sie den Befehl **Programm reparieren** an.  

3. Stellen Sie die App bereit. Aktivieren Sie auf der Registerkarte **Bereitstellungseinstellungen** der Bereitstellung die Option **Endbenutzern die Reparatur dieser Anwendung gestatten**.  


### <a name="known-issue"></a>Bekanntes Problem

Die neue Schaltfläche zum **Reparieren** der App im Softwarecenter für Benutzer ist in dieser Version nicht sichtbar.  



## <a name="approve-application-requests-via-email"></a><a name="bkmk_email-approve"></a> Genehmigen von Anwendungsanforderungen per E-Mail
<!--1321550-->

Hiermit werden E-Mail-Benachrichtigungen zum Genehmigen von Anwendungsanforderungen konfiguriert. Wenn ein Benutzer eine Anwendung anfordert, erhalten Sie eine E-Mail. Klicken Sie auf die Links in der E-Mail, um die Anforderung ohne die Configuration Manager-Konsole zu genehmigen oder abzulehnen.


### <a name="prerequisites"></a>Voraussetzungen

#### <a name="to-send-email-notifications"></a>So senden Sie E-Mail-Benachrichtigungen
- Aktivieren Sie das [optionale Feature](../servers/manage/install-in-console-updates.md#bkmk_options) **Anwendungsanforderungen für Benutzer pro Gerät genehmigen**.  

- Konfigurieren Sie [E-Mail-Benachrichtigungen für Warnungen](../servers/manage/use-alerts-and-the-status-system.md#to-configure-email-notification-for-alerts).  

#### <a name="to-approve-or-deny-requests-from-email"></a>So genehmigen oder lehnen Sie Anforderungen per E-Mail ab
Wenn Sie diese erforderlichen Komponenten nicht konfigurieren, sendet der Standort E-Mail-Benachrichtigungen für Anwendungsanforderungen ohne Links zum Genehmigen oder Ablehnen der Anforderung.  

- Navigieren Sie in den Standorteigenschaften zu **REST-Endpunkt für alle Anbieterrollen dieses Standorts aktivieren und Datenverkehr über das Configuration Manager-Cloudverwaltungsgateway zulassen**. Weitere Informationen finden Sie unter [Datenzugriff für OData-Endpunkt](capabilities-in-technical-preview-1612.md#odata-endpoint-data-access).  

    - Starten Sie den SMS_EXEC-Dienst neu, nachdem Sie den REST-Endpunkt aktiviert haben.

- [Cloudverwaltungsgateway](../clients/manage/cmg/plan-cloud-management-gateway.md)  

- Binden Sie den Standort in die [Azure-Dienste](../servers/deploy/configure/azure-services-wizard.md) für die **Cloudverwaltung** ein.  

    - Aktivieren Sie [Azure AD-Benutzerermittlung](../servers/deploy/configure/configure-discovery-methods.md#azureaadisc).  

    - Konfigurieren Sie die folgenden Einstellungen für diese native App manuell in Azure AD:  

        - **Umleitungs-URI**: `https://<CMG FQDN>/CCM_Proxy_ServerAuth/ImplicitAuth`. Verwenden Sie den vollqualifizierten Domänennamen (FQDN) des Cloud Management Gateway-Diensts (CMG), z.B. „GraniteFalls.Contoso.com“.   

        - **Manifest**: Legen Sie **oauth2AllowImplicitFlow** auf „true“ fest: `"oauth2AllowImplicitFlow": true,`  


### <a name="try-it-out"></a>Probieren Sie es aus!

Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie uns dann Ihr [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) mit Ihrer Meinung zu dem Feature.

1. Stellen Sie in der Configuration Manager-Konsole eine Anwendung bereit, sofern eine für eine Benutzersammlung verfügbar ist. Aktivieren Sie sie auf der Seite **Bereitstellungseinstellungen** zur Genehmigung. Geben Sie dann eine *einzelne* E-Mail-Adresse ein, um Benachrichtigungen zu erhalten.  

     > [!Note]  
     > Alle Benutzer in Ihrer Azure AD-Organisation, die die E-Mail erhalten, können die Anforderung genehmigen. Leiten Sie die E-Mail nur an andere Personen weiter, wenn diese bestimmte Maßnahmen durchführen sollen.  

2. Fordern Sie als Benutzer die Anwendung im Softwarecenter an.  

3. Sie erhalten eine E-Mail-Benachrichtigung ähnlich wie im folgenden Beispiel:  

![Beispiel für eine E-Mail-Benachrichtigung zur Genehmigung von Anwendungen](media/1321550-email.png)

> [!Note]  
> Der Link zum Genehmigen oder Ablehnen steht zur einmaligen Nutzung zur Verfügung. Nehmen Sie beispielsweise an, ein Gruppenalias wird für den Empfang von Benachrichtigungen konfiguriert. Meg genehmigt die Anforderung. Nun kann Bruce die Anforderung nicht ablehnen.  



## <a name="improvement-to-script-output"></a><a name="bkmk_script"></a> Verbesserung an der Skriptausgabe
<!--1236459-->

Sie können die ausführliche Skriptausgabe jetzt im nicht formatierten Format oder strukturierten JSON-Format anzeigen. Diese Formatierung vereinfacht das Lesen und Analysieren der Ausgabe. Wenn das Skript einen gültigen JSON-formatierten Text zurückgibt, zeigen Sie dann die ausführliche Ausgabe entweder als **JSON-Ausgabe** oder **Nicht formatierte Ausgabe** an. Andernfalls ist die einzige Option **Skriptausgabe**. 

#### <a name="example-script-output-is-valid-json"></a>Beispiel: Die Skriptausgabe weist ein gültiges JSON-Format auf.
Befehl: `$PSVersionTable.PSVersion`  

``` Output
Major  Minor  Build  Revision
-----  -----  -----  --------
5      1      16299  551
```

#### <a name="example-script-output-isnt-valid-json"></a>Beispiel: Die Skriptausgabe weist kein gültiges JSON-Format auf.
Befehl: `Write-Output (Get-WmiObject -Class Win32_OperatingSystem).Caption`  

``` Output
Microsoft Windows 10 Enterprise
```


### <a name="try-it-out"></a>Probieren Sie es aus!

Versuchen Sie, die Aufgaben fertig zu stellen. Senden Sie uns dann Ihr [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) mit Ihrer Meinung zu dem Feature.

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Bestand und Konformität**, und wählen Sie den Knoten **Gerätesammlungen** aus. Klicken Sie mit der rechten Maustaste auf eine Sammlung, und wählen Sie **Skript ausführen** aus. Weitere Informationen zum Erstellen und Ausführen von Skripts finden Sie unter [Erstellen und Ausführen von PowerShell-Skripts über die Configuration Manager-Konsole](../../apps/deploy-use/create-deploy-scripts.md).  

2. Führen Sie ein Skript für die Zielsammlung aus.  

3. Wählen Sie auf der Seite **Skriptstatusüberwachung** des Assistenten für die Skriptausführung im unteren Bereich die Registerkarte **Zusammenfassung** aus. Ändern Sie die beiden Dropdownlisten ganz oben in **Skriptausgabe** und **Datentabelle**. Doppelklicken Sie dann auf die Zeile mit Ergebnissen, um das Dialogfeld **Ausführliche Ausgabe** zu öffnen.  

4. Wählen Sie auf der Seite **Skriptstatusüberwachung** des Assistenten für die Skriptausführung im unteren Bereich die Registerkarte **Ausführungsdetails** aus. Doppelklicken Sie auf eine Zeile mit Ergebnissen, um das Dialogfeld „Ausführliche Ausgabe“ für dieses Gerät zu öffnen.  



## <a name="improvement-to-third-party-software-updates"></a><a name="bkmk_3pupdate"></a> Verbesserung an Updates für Drittanbietersoftware
<!--1358714-->

Ab sofort können Sie die Eigenschaften von benutzerdefinierten Katalogen ändern.

Weitere Informationen finden Sie unter [Unterstützung für benutzerdefinierte Kataloge für Drittanbieter-Softwareupdates](capabilities-in-technical-preview-1806-2.md#bkmk_3pupdate).



## <a name="next-steps"></a>Nächste Schritte

Informationen zur Installation des Technical Preview-Branch oder dessen Aktualisierung finden Sie unter [Technical Preview für Configuration Manager](technical-preview.md).    

Weitere Informationen zu den Unterschieden zwischen den verschiedenen Configuration Manager-Branches finden Sie unter [Welcher Branch von Configuration Manager soll verwendet werden?](../understand/which-branch-should-i-use.md).