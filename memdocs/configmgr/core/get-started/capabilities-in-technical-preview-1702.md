---
title: Funktionen in Technical Preview 1702
titleSuffix: Configuration Manager
description: Erfahren Sie mehr zu Features, die in Technical Preview für Configuration Manager-Version 1702 zur Verfügung stehen.
ms.date: 02/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aedd608d-6db3-4ea5-851d-70f2dcda6bb5
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e9fa71060b8125b7d0872a40d197f1c423217bad
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89607932"
---
# <a name="capabilities-in-technical-preview-1702-for-configuration-manager"></a>Funktionen in der Technical Preview 1702 für Configuration Manager

*Gilt für: Configuration Manager (Technical Preview-Branch)*

In diesem Artikel werden die Features vorgestellt, die in der Technical Preview-Version 1702 für Configuration Manager verfügbar sind. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen. Bevor Sie diese Version der Technical Preview installieren, lesen Sie das einführende Thema [Technical Preview für Configuration Manager](../../core/get-started/technical-preview.md), um sich mit den allgemeinen Anforderungen und Einschränkungen bei der Verwendung einer Technical Preview vertraut zu machen und um zu erfahren, wie Sie Updates für Versionen durchführen und Feedback zu den Features in einer Technical Preview geben können.    


**Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  

##  <a name="send-feedback-from-the-configuration-manager-console"></a>Feedback über die Configuration Manager-Konsole geben

Diese Vorschau stellt neue Feedbackoptionen der Configuration Manager-Konsole vor. Mit den Feedbackoptionen können Sie Feedback über die UserVoice-Feedback-Website von Configuration Manager direkt an das Entwicklungsteam senden.  

> Die **Feedback**optionen finden Sie hier:
> -  Im Menüband, ganz links von der Registerkarte „Startseite“ jedes Knotens.  
>    ![Menüband](./media/feedback-home.png)

-  Wenn Sie mit der rechten Maustaste auf ein beliebiges Objekt in der Konsole klicken.   
    ![Rechtsklick](./media/feedback-option.png)   

Wenn Sie auf **Feedback** klicken, öffnet sich die Configuration Manager UserVoice-Feedback-Website unter https://configurationmanager.uservoice.com/forums/300492-ideas.
##  <a name="changes-for-updates-and-servicing"></a>Änderungen an Updates und Wartung
Folgendes wird mit dieser Vorschau eingeführt.

**Einfachere Auswahlmöglichkeiten für Updates**  
Wenn das nächste Mal eins oder mehrere Updates für Ihre Infrastruktur zur Verfügung stehen, wird nur noch das aktuellste Update heruntergeladen. Wenn beispielsweise Ihre aktuelle Standortversion mindestens zwei Versionen älter als die aktuellste verfügbare Version ist, wird lediglich diese aktuellste Updateversion automatisch heruntergeladen.  

Sie haben die Option, auch die anderen verfügbaren Updates herunterzuladen und zu installieren, auch wenn diese nicht die aktuellsten Versionen sind. Trotzdem erhalten Sie eine Warnmeldung, dass das Update von einem aktuelleren ersetzt wurde. Um ein *verfügbares* Update herunterzuladen, wählen Sie das Update in der Konsole aus, und klicken Sie anschließend auf **Herunterladen**.

**Verbesserte Bereinigung älterer Updates**   
Wir haben eine automatische Bereinigungsfunktion hinzugefügt, die nicht mehr benötigte Downloads aus dem Ordner „EasySetupPayload“ auf Ihrem Standortserver löscht.  


## <a name="peer-cache-improvements"></a>Verbesserungen des Peercaches
Ab dieser Version lehnt ein Peercachequellcomputer eine Inhaltsanforderung ab, wenn der Peercachequellcomputer eine der folgenden Bedingungen erfüllt:  
-  Niedriger Akkustand.
-  Zum Zeitpunkt der Anforderungen des Inhalts liegt die CPU-Auslastung bei über 80 %.
-  *AvgDiskQueueLength* der Datenträger-E/A überschreitet 10.
-  Es gibt keine weiteren Verbindungen zum Computer.   

Sie können diese Einstellungen mithilfe der Client-Agentkonfigurationsklasse für das Peerquellfeature (*SMS_WinPEPeerCacheConfig*) konfigurieren, wenn Sie das Configuration Manager-SDK verwenden.

Wenn der Computer eine Anforderung von Inhalt ablehnt, sucht der anfordernde Computer bei alternativen Quellen seines Pools an verfügbaren Quellspeicherorten nach Inhalt.   

## <a name="use-azure-active-directory-domain-services-to-manage-devices-users-and-groups"></a><a name="azurediscovery"></a> Verwenden Sie Azure Active Directory-Domänendienste für das Verwalten von Geräten, Benutzern und Gruppen

Mit dieser Version der technischen Vorschau können Sie Geräte verwalten, die mit einer verwalteten Domäne von Active Directory (AD)-Domänendiensten verknüpft sind. Mit verschiedenen Methoden der Configuration Manager-Ermittlung können Sie außerdem Geräte, Benutzer und Gruppen in der Domäne ermitteln.

Die Infrastruktur, Clients und Domäne von Azure AD-Domänendiensten des Standorts der technischen Vorschau müssen alle in Azure ausgeführt werden.


### <a name="set-up-configuration-manager-to-use-azure-ad"></a>Einrichten von Configuration Manager für den Einsatz von Azure AD
Um Azure AD mit Configuration Manager zu verwenden, benötigen Sie Folgendes:
- Ein Azure-Abonnement.
- Azure AD mit Domänendiensten (Domain Services, DS).
- Ein Standort von Configuration Manager, der auf einer Azure-VM ausgeführt wird und der mit Ihrem Azure AD verknüpft ist.
- Configuration Manager-Clients, die in der gleichen Azure AD-Umgebung ausgeführt werden.

Informationen zur Konfiguration von Azure AD DS finden Sie unter [Get started with Azure AD Domain Services (Erste Schritte mit Azure AD-Domänendiensten)](/azure/active-directory-domain-services/create-instance).

### <a name="discover-resources"></a>Ressourcen ermitteln
Nachdem Sie Configuration Manager in Azure AD eingerichtet haben, können Sie Methoden der Configuration Manager-Ermittlung verwenden, um Azure AD nach Ressourcen zu durchsuchen:  
- Active Directory-Systemermittlung
- Active Directory-Benutzerermittlung
- Active Directory-Gruppenermittlung  

Bearbeiten Sie die LDAP-Abfrage für jede verwendete Methode, um die Azure AD OE-Strukturen statt der Container, die für lokales AD typisch sind, zu durchsuchen. Dazu müssen Sie die Abfrage anweisen, Ihr AD in Ihrem Azure-Abonnement zu durchsuchen.  

In folgenden Beispielen wird ein Azure AD von *contoso.onmicrosoft.com* verwenden:
- **Systemermittlung**   
  Azure AD speichert Geräte unter der Organisationseinheit **AADDC-Computer**.  Konfigurieren Sie Folgendes:  
  - *LDAP://OU=AADDC Computers,DC=contoso,DC=onmicrosoft,DC=com*  


- **Benutzerermittlung** AAD speichert Benutzer unter der Organisationseinheit **AADDC-Benutzer**.  Konfigurieren Sie Folgendes:
  - *LDAP://OU=AADDC Users,DC= contoso,DC=onmicrosoft,DC=com*


- **Gruppenermittlung**  
Azure AD hat keine Organisationseinheit, die Gruppen speichert. Verwenden Sie stattdessen die gleiche allgemeine Struktur wie für die Abfragen von Systemen und Benutzern, und konfigurieren Sie die LDAP-Abfrage so, dass diese auf die Organisationseinheit zeigt, die die Gruppe enthält, die Sie ermitteln möchten.

Weitere Informationen zu Azure AD finden Sie in den folgenden Themen:  
- [Azure Active Directory Domain Services](https://azure.microsoft.com/services/active-directory-ds) auf azure.microsoft.com.
- [Active Directory Domain Services Documentation (Dokumentation von Active Directory Domain Services)](/azure/active-directory-domain-services) auf docs.microsoft.com.

## <a name="conditional-access-device-compliance-policy-improvements"></a>Verbesserungen bei Gerätekompatibilitätsrichtlinien für bedingten Zugriff

Eine neue Regel für die Gerätekompatibilitätsrichtlinie ist verfügbar; sie hilft Ihnen beim Verweigern des Zugriffs auf Unternehmensressourcen, die bedingten Zugriff unterstützen, wenn Benutzer Anwendungen verwenden, die auf einer Liste nicht kompatibler Anwendungen stehen. Die Liste nicht kompatibler Anwendungen kann von Administrator beim Hinzufügen der neuen Regel **Nicht installierbare Apps** definiert werden. Für diese Regel muss der Administrator den **App-Namen**, die **Apple-ID** und den **App-Herausgeber** (optional) eingeben, wenn er eine Anwendung auf die Liste „Nicht kompatibel“ setzen möchte. Diese Einstellung gilt nur für iOS- und Android-Geräte.

Des Weiteren hilft sie Organisationen dabei, Datenlecks durch unsichere Apps zu beheben und einen außerordentlich hohe Datenverbrauch von gewissen Apps zu verhindern.

### <a name="try-it-out"></a>Probieren Sie es aus

**Szenario:** Identifizieren Sie Apps, die möglicherweise Datenlecks verursachen, indem sie Daten an einen Ort außerhalb Ihres Unternehmens senden, oder die einen außerordentlich hohen Datenverbrauch verursachen, und [erstellen Sie anschließend eine Richtlinie zur Gerätekompatibilität für bedingten Zugriff](../../mdm/understand/what-happened-to-hybrid.md), die diese Apps auf die Liste nicht kompatibler Apps setzt. Diese verweigert den Zugriff auf Unternehmensressourcen, die bedingten Zugriff unterstützen, solange bis der Benutzer die blockierte App entfernt.

## <a name="antimalware-client-version-alert"></a>Warnungen für Clientversionen der Antischadsoftware
Ab dieser Vorschauversion stellt Configuration Manager Endpoint Protection eine Warnmeldung zur Verfügung, die Sie darüber informiert, wenn mehr als 20 % (Standard) der verwalteten Clients eine abgelaufene Version des Antischadsoftwareclients verwenden (d.h. die Clients Windows Defender oder Endpoint Protection).

### <a name="try-it-out"></a>Probieren Sie es aus
Stellen Sie sicher, dass Endpoint Protection auf allen Desktop- und Serverclients aktiviert ist, die die Clienteinstellungsrichtlinie verwenden. Jetzt können Sie sich die **Clientversionen der Antischadsoftware** und den **Bereitstellungsstatus von Endpoint Protection** anschauen, indem Sie zu **Bestand und Kompatibilität** > **Übersicht** > **Geräte** > **Alle Desktop- und Serverclients** navigieren. Sie können die Warnungen im Arbeitsbereich **Überwachung** über den Knoten **Warnungen** überprüfen. Wenn mehr als 20 % der verwalteten Clients mit abgelaufenen Versionen der Antischadsoftware ausgeführt werden wird die Warnmeldung „Die Antischadsoftware-Clientversion ist veraltet“ angezeigt. Diese Warnmeldung wird auf der Registerkarte **Überwachung** > **Übersicht** nicht angezeigt. Aktivieren Sie Softwareupdates für Antischadsoftwareclients, um die abgelaufenen Antischadsoftwareclients zu aktualisieren.

Um die Prozentzahl, aber der die Warnung generiert wird, zu konfigurieren, erweitern Sie **Überwachung** > **Warnungen** > **Alle Warnungen**, doppelklicken Sie auf **Antischadsoftwareclients veraltet**, und passen Sie die Option **Warnung ausgeben, wenn der Prozentsatz verwalteter Clients mit veralteter Version des Antischadsoftwareclients höher ist als** entsprechend an.

## <a name="compliance-assessment-for-windows-update-for-business-updates"></a>Bewertung der Kompatibilität für Updates von Windows Update for Business
Sie können jetzt Ihre Regel für die Kompatibilitätsrichtlinie so konfigurieren, dass ein Bewertungsergebnis von Windows Update for Business als Teil der Bewertung des bedingten Zugriffs beinhaltet ist.
> [!IMPORTANT]
> Sie müssen Windows 10 Insider Preview Build 15019 oder höher besitzen, damit Sie die Kompatibilitätsbewertung für Updates von Windows Updates for Business verwenden können.

### <a name="allow-windows-update-for-business-to-manage-windows-10-updates"></a>Windows Update for Business erlauben, Windows 10-Updates zu verwalten
Um Kompatibilitätsbewertungsinformationen für Updates von Windows Update for Business zu erfassen, verwenden Sie folgenden Ablauf, um die Client-Agent-Einstellung so zu konfigurieren, sodass es Windows Update for Business erlaubt ist, Windows 10-Updates zu verwalten.
1. Navigieren Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Clienteinstellungen**.
2. Gehen Sie in den Eigenschaften für die Client-Einstellungen zu **Softwareupdates**, und wählen Sie anschließen **Ja** für die Einstellung **Windows 10-Updates mit Windows Update for Business verwalten** aus.

### <a name="create-a-compliance-policy-for-windows-update-for-business-assessment"></a>Bewertung der Kompatibilität für Updates von Windows Update for Business
1. Navigieren Sie in der Configuration Manager-Konsole zu **Bestand und Kompatibilität** > **Kompatibilitätseinstellungen** > **Konfigurationsrichtlinien**.
2. Klicken Sie auf **Kompatibilitätsrichtlinie erstellen**, oder wählen Sie eine vorhandene Kompatibilitätsrichtlinie, die Sie ändern möchten.
3. Geben sie auf der Seite „Allgemein“ einen Namen und eine Beschreibung an, wählen Sie dann **Kompatibilitätsregeln für Geräte, die mit dem Configuration Manager-Client verwaltet werden** aus, legen Sie die Nichtkompatibilitätsschwere für die Berichterstattung fest, und klicken Sie anschließend auf **Weiter**.
4. Wählen Sie auf der Seite **Unterstützte Plattformen** Windows 10 aus, und klicken Sie anschließend auf **Weiter**.
5. Klicken Sie auf der Seite „Regeln“ auf **Neu...** , und wählen Sie dann als **Bedingung** **Require Windows Update for Business compliance (Kompatibilität mit Windows Update for Business erforderlich)** aus. Die Einstellung **Wert** ist automatisch auf **TRUE** festgelegt.

Die neue Richtlinie wird im Knoten **Kompatibilitätsrichtlinien** im Arbeitsbereich **Bestand und Kompatibilität** angezeigt.

### <a name="deploy-a-compliance-policy"></a>Bereitstellen einer Konformitätsrichtlinie
1. Gehen Sie in der Configuration Manager-Konsole zu **Bestand und Kompatibilität** > **Kompatibilitätseinstellungen**, und klicken Sie anschließend auf **Kompatibilitätsrichtlinien**.
2. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Bereitstellen**.
3. Klicken Sie im Dialogfeld **Kompatibilitätsrichtlinien bereitstellen** auf **Durchsuchen** , um die Benutzersammlung auszuwählen, für die Sie die Richtlinie bereitstellen möchten.
   Darüber hinaus können Sie Optionen auswählen, um Warnungen zu generieren, wenn die Richtlinie nicht befolgt wird. Sie können auch den Zeitplan konfigurieren, gemäß dem diese Richtlinie auf Konformität ausgewertet wird.
4. Klicken Sie abschließend auf **OK**.

### <a name="monitor-the-compliance-policy"></a>Überwachen der Konformitätsrichtlinie
Nachdem Sie die Kompatibilitätsrichtlinie erstellt haben, können Sie die Kompatibilitätsergebnisse in der Configuration Manager-Konsole überwachen. Weitere Informationen finden Sie unter [Überwachen der Konformitätsrichtlinie](../../mdm/understand/what-happened-to-hybrid.md).


## <a name="improvements-to-software-center-settings-and-notification-messages-for-high-impact-task-sequences"></a>Verbesserungen bei den Einstellungen und Benachrichtigungen für Tasksequenzen mit schwerwiegenden Auswirkungen im Softwarecenter
Diese Version beinhaltet folgende Verbesserungen der Einstellungen und Benachrichtigungen für Tasksequenzen mit schwerwiegenden Auswirkungen im Softwarecenter:

- In den Eigenschaften der Tasksequenz können Sie jede beliebige Tasksequenz konfigurieren, einschließlich Tasksequenzen, die nicht zum Betriebssystem gehören, wie etwa risikoreiche Bereitstellungen. Jede Tasksequenz, die bestimmte Bedingungen erfüllt, wird automatisch als „high-impact“ (mit schwerwiegenden Auswirkungen) definiert. Weitere Informationen finden Sie unter [Verwalten risikoreicher Bereitstellungen](../servers/manage/settings-to-manage-high-risk-deployments.md).
- In den Eigenschaften der Tasksequenz können Sie die Standardbenachrichtigung festlegen oder Ihre eigene benutzerdefinierte Benachrichtigung für Bereitstellungen mit schwerwiegenden Auswirkungen erstellen.
- In den Eigenschaften der Tasksequenz können Sie die Eigenschaften vom Softwarecenter konfigurieren, zu denen „Make a restart required“ (Neustart erforderlich), die Downloadgröße der Tasksequenz und die geschätzte Laufzeit gehören.
- Die Standardmeldung für Bereitstellungen mit schwerwiegenden Auswirkungen für direkte Aktualisierungen gibt jetzt an, dass Ihre App, Daten und Einstellungen automatisch migriert werden. Zuvor gab die Standardmeldung für jede Installation des Betriebssystems an, dass alle Apps, Daten und Einstellungen verloren gingen, was jedoch für eine direkte Aktualisierung nicht galt.

### <a name="set-a-task-sequence-as-a-high-impact-task-sequence"></a>Festlegen einer Tasksequenz als Tasksequenz mit schwerwiegenden Auswirkungen
Gehen Sie wie folgt vor, um eine Tasksequenz als Tasksequenz mit schwerwiegenden Auswirkungen festzulegen:
> [!NOTE]
> Jede Tasksequenz, die bestimmte Bedingungen erfüllt, wird automatisch als „high-impact“ (mit schwerwiegenden Auswirkungen) definiert. Weitere Informationen finden Sie unter [Verwalten risikoreicher Bereitstellungen](../servers/manage/settings-to-manage-high-risk-deployments.md).

1. Navigieren Sie in der Configuration Manager-Konsole zu **Softwarebibliothek** > **Betriebssysteme** > **Tasksequenzen**.
2. Wählen Sie die zu bearbeitende Tasksequenz aus, und klicken Sie anschließend auf **Eigenschaften**.
3. Wählen Sie in der Registerkarte **Benutzerbenachrichtigung** **Dies ist eine Tasksequenz mit schwerwiegenden Auswirkungen** aus.

### <a name="create-a-custom-notification-for-high-risk-deployments"></a>Erstellen einer benutzerdefinierten Benachrichtigung für risikoreiche Bereitstellungen
1. Navigieren Sie in der Configuration Manager-Konsole zu **Softwarebibliothek** > **Betriebssysteme** > **Tasksequenzen**.
2. Wählen Sie die zu bearbeitende Tasksequenz aus, und klicken Sie anschließend auf **Eigenschaften**.
3. Wählen Sie in der Registerkarte **Benutzerbenachrichtigung** **Benutzerdefinierten Text verwenden** aus.
   > [!NOTE]
   >  Sie können den Text von Benutzerbenachrichtigungen nur festlegen, wenn **Dies ist eine Tasksequenz mit schwerwiegenden Auswirkungen** ausgewählt ist.

4. Konfigurieren Sie folgende Einstellungen (maximal 255 Zeichen pro Text):

   **Überschriftentext für Benutzerbenachrichtigung:** Gibt den blauen Text an, der in der Benutzerbenachrichtigung vom Softwarecenter angezeigt wird. In der Standardbenutzerbenachrichtigung enthält dieser Abschnitt beispielsweise folgenden Text: „Bestätigen Sie, dass Sie das Betriebssystem auf diesem Computer aktualisieren möchten“ o.Ä.

   **Text der Benutzerbenachrichtigung:** Es gibt drei Textfelder, die den Text der benutzerdefinierten Benachrichtigungen enthalten.
   - Erstes Textfeld: Gibt den Hauptteil des Texts an, der üblicherweise Anweisungen an den Benutzer enthält. In der Standardbenutzerbenachrichtigung enthält dieser Abschnitt beispielsweise folgenden Text: „Das Upgrade des Betriebssystems kann einige Zeit dauern und mehrere Neustarts des Computers erfordern“ o.Ä.
   - Zweites Textfeld: Gibt den fettmarkierten Text unterhalb des Hauptteils an. In der Standardbenutzerbenachrichtigung enthält dieser Abschnitt beispielsweise folgenden Text: „Dieses direkte Upgrade installiert das neue Betriebssystem und führt eine automatische Migration Ihrer Apps, Daten und Einstellungen durch“ o.Ä.
   - Drittes Textfeld: Gibt die letzte Textzeile unterhalb des fettmarkierten Texts an. In der Standardbenutzerbenachrichtigung enthält dieser Abschnitt beispielsweise folgenden Text: „Klicken Sie auf Installieren, um den Vorgang zu starten. Klicken Sie andernfalls auf Abbrechen.“   

   Angenommen, Sie konfigurieren folgende benutzerdefinierte Benachrichtigung in den Eigenschaften.

   ![Benutzerdefinierte Benachrichtigung für eine Tasksequenz – Eigenschaften](./media/user-notification.png)

   Folgende Benachrichtigung wird angezeigt, wenn der Endbenutzer die Installation aus dem Softwarecenter öffnet.

   ![Benutzerdefinierte Benachrichtigung für eine Tasksequenz – Softwarecenter](./media/user-notification-enduser.png)

### <a name="configure-software-center-properties"></a>Konfigurieren der Eigenschaften des Softwarecenters
Gehen Sie wie folgt vor, um die Angaben für die Tasksequenz, die im Softwarecenter angezeigt werden, zu konfigurieren. Diese Angaben dienen nur zu Informationszwecken.  
1. Navigieren Sie in der Configuration Manager-Konsole zu **Softwarebibliothek** > **Betriebssysteme** > **Tasksequenzen**.
2. Wählen Sie die zu bearbeitende Tasksequenz aus, und klicken Sie anschließend auf **Eigenschaften**.
3. Auf der Registerkarte **Allgemein** stehen folgende neuen Einstellungen für das Softwarecenter zur Verfügung:
   - **Neustart erforderlich:** Informiert den Benutzer, ob während der Installation ein Neustart erforderlich ist.
   - **Downloadgröße (MB):** Gibt an, wie viele Megabytes für die Tasksequenz im Softwarecenter angezeigt werden.  
   - **Geschätzte Laufzeit (Min.):** Gibt die geschätzte Laufzeit in Minuten an, die für die Tasksequenz im Softwarecenter angezeigt wird.


## <a name="check-for-running-executable-files-before-installing-an-application"></a>Prüfen Sie auf ausgeführte ausführbare Dateien, bevor Sie eine Anwendung installieren

Sie können jetzt auf der Registerkarte „Installationsverhalten“ im Dialogfeld *\<deployment type name>* -**Eigenschaften** eines Bereitstellungstyps eine von mehreren ausführbaren Dateien festlegen, die, falls ausgeführt, die Installation des Bereitstellungstyps verhindert. Der Benutzer muss die ausgeführte ausführbare Datei schließen bevor der Bereitstellungstyp installiert werden kann – die Datei kann aber auch automatisch für Bereitstellungen mit dem Zweck „Erforderlich“ geschlossen werden.

### <a name="try-it-out"></a>Probieren Sie es aus.

1. Wählen Sie in den Eigenschaften eines Bereitstellungstyps von Configuration Manager die Registerkarte **Installationsverhalten** aus.
2. Wählen Sie **Hinzufügen** aus, um eine oder mehrere ausführbare Dateinamen hinzuzufügen, auf die Sie prüfen möchten. Außerdem können Sie einen Anzeigenamen hinzufügen, um es Benutzern zu erleichtern, Anwendungen in der Liste zu identifizieren.
3. Wenn die Bereitstellungen den Zweck „Erforderlich“ im Assistenten zum Bereitstellen von Software aufweist, können Sie die Option **Ausgeführte ausführbare Dateien automatisch schließen, die im Eigenschaftendialogfeld des Bereitstellungstyps auf der Registerkarte "Installationsverhalten" angegeben wurden** wählen.

Wenn die Anwendung als **Verfügbar** bereitgestellt wurde, und ein Endbenutzer versucht, eine Anwendung zu installieren, wird er dazu aufgefordert, alle ausgeführten ausführbaren, von Ihnen festgelegten Dateien zu schließen, bevor er mit der Installation fortfahren kann.

Wenn die Anwendung als **Erforderlich** bereitgestellt wurde, und die Option **Ausgeführte ausführbare Dateien automatisch schließen, die im Eigenschaftendialogfeld des Bereitstellungstyps auf der Registerkarte "Installationsverhalten" angegeben wurden** ausgewählt ist, wird dem Endbenutzer ein Dialogfeld angezeigt, das ihn darüber informiert, dass ausführbare, von Ihnen festgelegte Dateien automatisch geschlossen werden, wenn die Frist der Installation abgelaufen ist. Sie können diese Dialogfelder unter **Clienteinstellungen** > **Computer-Agent** zeitlich festlegen. Wenn Sie nicht möchten, dass Endbenutzer diese Meldungen sehen, wählen Sie in den Bereitstellungseigenschaften auf der Registerkarte **Benutzerfreundlichkeit** die Option **In Softwarecenter und allen Benachrichtigungen ausblenden** aus.

Wenn die Anwendung als **Erforderlich** bereitgestellt wurde, und die Option **Ausgeführte ausführbare Dateien automatisch schließen, die im Eigenschaftendialogfeld des Bereitstellungstyps auf der Registerkarte "Installationsverhalten" angegeben wurden** nicht ausgewählt ist, schlägt die Installation der Anwendung fehl, wenn mindestens eine der angegebenen Anwendungen ausgeführt wird.

## <a name="create-pfx-certificates-with-s-mime-support"></a>Erstellen von PFX-Zertifikaten mit S-MIME-Unterstützung

Sie können jetzt ein PFX-Zertifikatprofil erstellen, dass S/MIME unterstützt und dieses für den User bereitstellen.  Dieses Zertifikat kann dann für die Verschlüsselung und Entschlüsselung von Geräten, die der Benutzer registriert hat, mit S/MIME verwendet werden.

Zusätzlich können Sie jetzt mehrere Zertifizierungsstellen (certification authorities, CAs) auf mehreren Standortsystemrollen des Zertifikatregistrierungspunkts festlegen und dann anschließend zuweisen, welche CAs Abfragen im Rahmen des Zertifikatprofils verarbeiten.

Sie können ein PFX-Zertifikatprofil für iOS-Geräte mit einem E-Mail-Profil verknüpfen und die Verschlüsselung mit S/MIME aktivieren.  Dadurch wird S/MIME im nativen E-Mail-Client auf iOS aktiviert und verknüpft das korrekte S/MIME-Verschlüsselungszertifikat.

Weitere Informationen zu Zertifikaten in Configuration Manager finden Sie unter [Einführung in Zertifikatprofile]( /sccm/protect/deploy-use/introduction-to-certificate-profiles).


## <a name="new-compliance-settings-for-ios-devices"></a>Neue Kompatibilitätseinstellungen für iOS-Geräte

Es wurden neue Einstellungen hinzugefügt, die Sie in Ihren Konfigurationselementen für iOS-Geräte verwenden können. Dabei handelt es sich um Einstellungen, die zuvor in Microsoft Intune in einer eigenständigen Konfiguration vorhanden waren, und jetzt verfügbar sind, wenn Sie Intune mit Configuration Manager verwenden. Hilfe zu diesen Einstellungen finden Sie unter [iOS policy settings in Microsoft Intune (Einstellungen für iOS-Richtlinien in Microsoft Intune)](../../../intune/configuration/device-restrictions-ios.md).

- **Daten aus verwalteten Apps mit iCloud synchronisieren**
- **Aktivitäten mit HandOff auf einem anderen Gerät fortsetzen**
- **iCloud-Fotofreigabe**
- **iCloud-Fotomediathek**
- **Neuen Unternehmens-App-Autoren vertrauen**
- **Benutzern das Herunterladen von iBook Store-Inhalt mit der Kennzeichnung „Erotik“ gestatten** (nur im überwachten Modus)
- **Handgelenkerkennung für gekoppelte Apple Watch-Geräte erzwingen**
- **Kennwort für ausgehende AirPlay-Anforderungen**
- **Kontoeinstellungen ändern** (nur im überwachten Modus)
- **Änderungen an den Einstellungen zur App-Mobilfunkdatennutzung** (nur im überwachten Modus)
- **Gesamten Inhalt und alle Einstellungen löschen** (nur im überwachten Modus)
- **Einschränkungen auf Gerät konfigurieren** (nur im überwachten Modus)
- **Hostkopplung zum Steuern der Geräte verwenden, mit denen ein iOS-Gerät gekoppelt werden kann** (nur im überwachten Modus)
- **Konfigurationsprofile und Zertifikate installieren** (nur im überwachten Modus)
- **Bearbeitung des Gerätenamens** (nur im überwachten Modus)
- **Änderung des Passcodes** (nur im überwachten Modus)
- **Apple Watch-Kopplung** (nur im überwachten Modus)
- **Änderung der Benachrichtigungseinstellungen** (nur im überwachten Modus)
- **Hintergrundbild ändern** (nur im überwachten Modus)
- **Änderung der Einstellungen zur Diagnoseübermittlung** (nur im überwachten Modus)
- **Bluetooth-Änderung** (nur im überwachten Modus)
- **AirDrop** (nur im überwachten Modus)
- **Siri zur Abfrage von benutzergeneriertem Inhalt aus dem Internet verwenden** (nur im überwachten Modus)
- **Siri-Filter für anstößige Ausdrücke** (nur im überwachten Modus)
- **Ergebnisse aus dem Internet in Spotlight-Suche zurückgeben** (nur im überwachten Modus)
- **Suche nach Wortdefinition** (nur im überwachten Modus)
- **Tastaturwortvorschläge** (nur im überwachten Modus)
- **Autokorrektur** (nur im überwachten Modus)
- **Rechtschreibprüfung über Tastatur** (nur im überwachten Modus)
- **Tastenkombinationen** (nur im überwachten Modus)
  <!--- - **Enterprise app trust settings modification** --->
- **Apps nur mit Apple Configurator und iTunes installieren** (nur im überwachten Modus)
- **Automatische App-Downloads** (nur im überwachten Modus)
- **Änderungen an den Einstellungen der App " Meine Freunde suchen"**  (nur im überwachten Modus)
- **Zugriff auf den iBooks Store** (nur im überwachten Modus)
- **Nachrichten-App** (nur im überwachten Modus)
- **Podcasts** (nur im überwachten Modus)
- **Apple Music** (nur im überwachten Modus)
- **iTunes Radio** (nur im überwachten Modus)
- **Apple News** (nur im überwachten Modus)
- **Game Center** (nur im überwachten Modus)
- **AirDrop als nicht verwaltetes Ziel behandeln**

## <a name="android-for-work-support"></a>Unterstützung für Android for Work

Ab Technical Preview Version 1702 können Sie ein Google-Konto an Ihren hybriden MDM-Mandanten binden. Dadurch können Sie Folgendes:

- [Unterstützte Android-Geräte](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012) in Android for Work registrieren, sodass Arbeitsprofile auf diesen registrierten Geräten erstellt werden
- Apps im Play for Work-Store genehmigen, diese mit der Configuration Manager-Konsole synchronisieren und sie anschließend in den Arbeitsprofilen der Geräte bereitstellen
- Erstellen Sie Konfigurationselemente, und stellen Sie diese bereit, um Arbeitsprofile und Passworteinstellungen für diese Geräte zu konfigurieren
- Erstellen Sie Kompatibilitätsrichtlinien und Profile für den Ressourcenzugriff für Android for Work-Geräte, genauso wie Sie es bereits für Android-Geräte machen, und stellen Sie diese bereit
- Führen Sie selektives Zurücksetzen auf Android for Work-Geräten durch

Beim Registrieren eines Geräts in Android for Work wird ein Arbeitsprofil auf dem Gerät erstellt, das von Intune verwaltet werden kann. Dieses Arbeitsprofil existiert neben dem persönlichen Profil auf dem Android-Gerät. Benutzer können ganz einfach zwischen Apps des Arbeits- und des persönlichen Profils wechseln. Sie können Elemente im persönlichen Profil nicht verwalten. Persönliche Apps und Daten bleiben unverwaltet. Configuration Manager kann das gesamte Arbeitsprofil mitsamt dessen Inhalten steuern und es auch vom Gerät löschen.

Android for Work ist eine separate Android-Plattform; Sie müssen entscheiden, welche Art der Verwaltung Sie für Android-Geräte einsetzen möchten, die Arbeitsprofile unterstützen.

### <a name="try-it-out"></a>Probieren Sie es aus!
Die folgenden Abschnitte beschreiben die Verwaltung mit Android for Work.

#### <a name="enable-android-for-work-management"></a>Aktivieren Sie die Verwaltung mit Android for Work
1. Erstellen Sie unter https://accounts.google.com/SignUp ein Google-Konto, das Sie als Ihr Administratorkonto für Android for Work verwenden können, und das mit allen Verwaltungsaufgaben von Android for Work für diesen Intune-Mandanten verbunden ist. Dieses Google-Konto kann auch für die verschiedenen Administratoren des Android-Geräts freigegeben werden. Mit diesem Google-Konto verwaltet und veröffentlicht Ihre Organisation Apps in der Play for Work-Konsole. Sie verwenden diesen Account, um Apps im Play for Work-Store zu genehmigen – deshalb sollten Sie den Kontonamen und das Passwort nicht vergessen.
2. Aktivieren Sie die Android-Registrierung, indem Sie das Google-Konto an den von Configuration Manager verwalteten Intune-Mandanten binden:
   1. Navigieren Sie zu **Verwaltung** > **Übersicht** > **Cloud Services** > **Microsoft Intune-Abonnements**, und wählen Sie Ihr Intune-Abonnement aus.
   2. Klicken Sie im Menüband auf **Plattformen konfigurieren** > **Android**, und stellen Sie sicher, dass ein Häkchen bei **Android-Registrierung aktivieren** gesetzt ist.
   3. Klicken Sie im Menüband auf **Plattform konfigurieren** > **Android for Work**.
   4. Klicken Sie im Dialogfeld auf **Android for Work in der Intune-Konsole konfigurieren**. Die Intune-Konsole wird in Ihrem Webbrowser geöffnet.
   5. Verwenden Sie Ihre Administratoranmeldeinformationen für Intune, um sich im Intune-Portal anzumelden.
   6. Klicken Sie auf **Konfigurieren**, um die Android for Work-Website von Google Play zu öffnen.
   7. Geben Sie auf der Google-Anmeldeseite die Anmeldeinformationen Ihres Google-Kontos aus dem ersten Schritt ein, und machen Sie anschließen Angaben zu Ihrem Unternehmen.
3. Wenn Sie zum Intune-Portal zurückkehren, ist Android for Work aktiviert, und Sie haben drei verschiedene Registrierungsoptionen für Android for Work-Geräte:
   - **Alle Geräte wie Android verwalten**: (Deaktiviert) Alle Android-Geräte, einschließlich der Geräte, die Android for Work unterstützen, werden als herkömmliche Android-Geräte registriert
   - **Unterstützte Geräte als Android for Work verwalten**: (Aktiviert) Alle Geräte, die Android for Work unterstützen, werden als Android for Work-Geräte registriert. Jedes Android-Gerät, das Android for Work nicht unterstützt, wird als herkömmliches Android-Gerät registriert.
   - **Unterstützte Geräte nur für Benutzer dieser Gruppen als Android for Work verwalten**: (Test) Damit können Sie die Android for Work-Verwaltung auf eine begrenzte Gruppe von Benutzern ausrichten. Nur Geräte der Mitglieder der ausgewählten Gruppen, die ein Gerät registrieren, das Android for Work unterstützt, werden als Android for Work-Geräte registriert. Alle anderen werden als Android-Geräte registriert.
  
> [!NOTE]
> Ein bekanntes Problem verhindert, dass die Option **Unterstützte Geräte nur für Benutzer dieser Gruppen als Android for Work verwalten** ordnungsgemäß ausgeführt wird. Geräte von Benutzern in den angegebenen Azure AD-Gruppen werden als Android anstelle von Android for Work registriert. Um Android for Work zu testen, müssen Sie **Manage all supported devices as Android for Work** (Verwalten aller unterstützten Geräte als Android for Work) verwenden.


  Um die Registrierung mit Android for Work zu aktivieren, müssen Sie eine der beiden unteren Optionen wählen. Für die Option **Unterstützte Geräte nur für Benutzer dieser Gruppen als Android for Work verwalten** müssen Sie zuerst Sicherheitsgruppen von Azure Active Directory einrichten.

Den Namen des Kontos und der Organisation finden Sie im Intune-Portal, wenn die Bindung abgeschlossen ist; jetzt können Sie beide Browser schließen.

#### <a name="approve-and-deploy-android-for-work-apps"></a>Genehmigen und Bereitstellen von Android for Work Apps
Gehen Sie wie folgt vor, um Apps im Play for Work-Store zu genehmigen, diese mit der Configuration Manager-Konsole zu synchronisieren und sie anschließend in verwalteten Android for Work-Geräten bereitzustellen. Um Apps in die Arbeitsprofile von Benutzern bereitzustellen, müssen Sie die Apps zunächst in Play for Work genehmigen und anschließend mit der Configuration Manager-Konsole synchronisieren.

1. Öffnen Sie einen Browser, und navigieren Sie zu https://play.google.com/work.
2. Melden Sie sich mit dem Google-Administratorkonto an, das Sie an Ihren Intune-Mandanten gebunden haben.
3. Suchen Sie nach Apps, die Sie in Ihrer Umgebung bereitstellen möchten, und klicken Sie jeweils auf **Genehmigen**.
4. Gehen Sie in der Configuration Manager-Konsole zu **Adminisitrator** > **Übersicht** > **Cloud Services** > **Android for Work**, und klicken Sie dann auf **Synchronisierung**.
5. Es kann bis zu zehn Minuten dauern, bis Apps synchronisiert sind; navigieren Sie anschließend zu **Softwarebibliothek** > **Übersicht** > **Anwendungsverwaltung** > **Lizenzinformationen für Store-Apps**.
6. Klicken Sie auf eine App, die mit Play for Work synchronisiert wurde, und klicken Sie dann auf **Anwendung erstellen**.
7. Schließen Sie den Assistenten ab, und klicken Sie auf **Schließen**.
8. Gehen Sie zu **Softwarebibliothek** > **Übersicht** > **Anwendungsverwaltung** > **Anwendungen**, wählen Sie eine Android for Work-App aus, und stellen Sie diese wie gewohnt bereit.

Um Play for Work-Apps mit Configuration Manager zu synchronisieren müssen Sie mindestens eine App auf der Play for Work-Website genehmigen.

#### <a name="enroll-an-android-for-work-device"></a>Registrieren eines Android for Work-Geräts
Das Registrieren von Android for Work-Geräten ist der Registrierung von Android-Geräten ähnlich. Laden Sie die Portal-App für Android auf Ihr mobiles Gerät herunter und führen Sie diese aus. Sie werden aufgefordert, ein Arbeitsprofil als Teil der Registrierung zu erstellen.  Sobald das Arbeitsprofil erstellt wurde, müssen Sie zur verwalteten Version des Unternehmensportals wechseln. Das verwaltetet Unternehmensportal ist mit einem kleinen, orangen Koffer in der rechten unteren Ecke markiert.

#### <a name="create-and-deploy-a-configuration-item"></a>Erstellen und Bereitstellen eines Konfigurationselements
Android for Work hat zwei Einstellungsgruppen für Konfigurationselemente:
- Kennwort
- Arbeitsprofil

Sie können die Freigabe von Inhalt zwischen Arbeitsprofilen sowie folgende Konfigurationselemente auf Geräten mit Android 6 oder höher konfigurieren:
- Das Verhalten für Apps, die spezifische Zustimmung fordern
- Die Sichtbarkeit von Benachrichtigungen für Anwendungen des Arbeitsprofils auf dem Sperrbildschirm

Sie können dies ausprobieren, indem Sie ein Konfigurationselement mithilfe des Standardworkflows erstellen; wählen Sie dazu **Android for Work** auf der Seite **Allgemein** aus, und konfigurieren Sie die Einstellungen für jede der Einstellungsgruppen, indem Sie das Konfigurationselement in die Baseline einfügen und wie gewohnt bereitstellen. Diese Einstellungen gelten nur für Geräte, die als Android for Work registriert sind, und nicht für die, die nur als Android registriert wurden.

#### <a name="perform-selective-wipe"></a>Selektives Zurücksetzen durchführen
Nur Geräte, die als Android for Work registriert sind, können selektiv zurückgesetzt werden, da Sie nur das Arbeitsprofil verwalten. Das schützt das persönliche Profil vor dem Zurücksetzen. Wenn Sie ein Android for Work-Gerät selektiv zurücksetzen, wird das Arbeitsprofil entfernt, einschließlich aller Apps und Daten, und das Gerät ist nicht mehr registriert.

Um ein Android for Work-Gerät selektiv zurückzusetzen, verwenden Sie den gewohnten [Ablauf zum selektiven Zurücksetzen](/sccm/mdm/deploy-use/wipe-lock-reset-devices#selective-wipe) in der Configuration Manager-Konsole.

#### <a name="known-issues-for-android-for-work"></a>Bekannte Probleme bei Android for Work
**Das Konfigurieren des Synchronisierungszeitplans in E-Mail-Profilen von Android for Work schlägt bei der Bereitstellung fehl** Eine Option in der ConfigMgr-Benutzeroberfläche für E-Mail-Profile von Android for Work ist „Schedule“ (Zeitplan). Auf anderen Plattformen kann der Administrator dadurch einen Zeitplan für die Synchronisierung von E-Mails und anderen E-Mail-Kontendaten bis hin zu den mobilen Geräten konfigurieren, auf denen er bereitgestellt wird. Dies funktioniert allerdings nicht für Android for Work-E-Mail-Profile. Die Auswahl einer anderen Option als „Nicht konfiguriert“ führt dazu, dass das Profil auf keinem Gerät bereitgestellt wird.