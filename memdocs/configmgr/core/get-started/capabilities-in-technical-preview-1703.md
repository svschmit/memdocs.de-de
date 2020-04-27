---
title: Funktionen in Technical Preview 1703
titleSuffix: Configuration Manager
description: Erfahren Sie mehr zu Features, die in Technical Preview für Configuration Manager-Version 1703 zur Verfügung stehen.
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2e801f8c-d331-41ee-8f27-908448fc0951
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: d06bda9d07a53e022de27afc68f40f9ce706867f
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076151"
---
# <a name="capabilities-in-technical-preview-1703-for-configuration-manager"></a>Funktionen in der Technical Preview 1703 für Configuration Manager

*Gilt für: Configuration Manager (Technical Preview-Branch)*

In diesem Artikel werden die Features vorgestellt, die in der Technical Preview-Version 1703 für Configuration Manager verfügbar sind. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen. Bevor Sie diese Version der Technical Preview installieren, lesen Sie das einführende Thema [Technical Preview für Configuration Manager](../../core/get-started/technical-preview.md), um sich mit den allgemeinen Anforderungen und Einschränkungen bei der Verwendung einer Technical Preview vertraut zu machen und um zu erfahren, wie Sie Updates für Versionen durchführen und Feedback zu den Features in einer Technical Preview geben können.    


**Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  

## <a name="deploy-volume-purchased-ios-apps-to-device-collections"></a>Bereitstellen per Volumenlizenz erworbener iOS-Apps in Gerätesammlungen

Sie können jetzt sowohl Geräten als auch Benutzern lizenzierte Apps bereitstellen. Je nachdem, inwieweit die App Gerätelizenzierungen unterstützt, wird eine entsprechende Lizenz wie folgt beansprucht:

|||||
|-|-|-|-|
|Configuration Manager-Version|Unterstützt die App Gerätelizenzierung?|Typ der Bereitstellungssammlung|Beanspruchte Lizenz|
|Früher als 1702|Ja|Benutzer|Benutzerlizenz|
|Früher als 1702|Nein|Benutzer|Benutzerlizenz|
|Früher als 1702|Ja|Gerät|Benutzerlizenz|
|Früher als 1702|Nein|Gerät|Benutzerlizenz|
|1702 und höher|Ja|Benutzer|Benutzerlizenz|
|1702 und höher|Nein|Benutzer|Benutzerlizenz|
|1702 und höher|Ja|Gerät|Gerätelizenz|
|1702 und höher|Nein|Gerät|Benutzerlizenz|


## <a name="direct-links-to-applications-in-software-center"></a>Direkte Links zu Anwendungen im Softwarecenter

Sie können jetzt Endbenutzern einen direkten Link zu einer Anwendung im Softwarecenter bereitstellen. Dies bedeutet, dass sie nicht mehr das Softwarecenter öffnen und nach einer Anwendung suchen müssen, bevor Sie sie installieren können. Dies ist nur für Configuration Manager-Anwendungen verfügbar, nicht für Pakete und Programme oder Tasksequenzen.

### <a name="try-it-out"></a>Probieren Sie es aus                 

Verwenden Sie das folgende URL-Format, um das Softwarecenter für eine bestimmte Anwendung zu öffnen:

**Softwarecenter:SoftwareId=_Anwendungskennung_**

### <a name="how-to-get-the-application-identifier-of-an-application"></a>So rufen Sie den Anwendungsbezeichner einer Anwendung ab

1. Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.
2. Erweitern Sie im Arbeitsbereich „Softwarebibliothek“ den Knoten **Anwendungsverwaltung**, und klicken Sie dann auf **Anwendungen**.
3. Klicken Sie mit der rechten Maustaste in der Ansicht **Anwendungen** auf eine der Spaltenüberschriften, und wählen Sie anschließend **Eindeutige CI-ID** aus der Liste aus. Sie sehen, dass die eindeutige ID jeder Anwendung jetzt in der Liste angezeigt wird.
4. Beachten Sie die **Eindeutige CI-ID** der Anwendung, der Sie einen Link bereitstellen möchten, wie z.B.: **ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f/2**
5. Entfernen Sie dann den Text, der auf die Anwendungs-GUID folgt. In diesem Fall ist es **/2**. Dadurch bleibt der Anwendungsbezeichner übrig.
6. Um die Erstellung des Links abzuschließen, stellen Sie ihr **Softwarecenter:SoftwareID=** voran. Dem obigen Beispiel folgend, wird der abschließende Link wie folgt lauten: **Softwarecenter:SoftwareId= ScopeId_1672B0CD-912A-4613-9BAB-D4EF2696D416/Application_970b1fef-1f38-405c-ad37-c753400b895f**.

Mithilfe dieses Links können Endbenutzer Softwarecenter direkt für die von Ihnen angegebene Anwendung öffnen.


## <a name="pfx-certificates-for-configuration-manager-windows-client-computers"></a>PFX-Zertifikate für Configuration Manager-Windows-Clientcomputer

Sie können nun PFX-Zertifikatprofile bereitstellen, die Sie für Configuration Manager-Clientcomputer unter Windows 10 importiert haben.

### <a name="try-it-out"></a>Probieren Sie es aus

Verwenden Sie die Anweisungen unter [Erstellen von PFX-Zertifikatprofilen](../../mdm/deploy-use/create-pfx-certificate-profiles.md), um ein PFX-Profil zu importieren, das Profil bereitzustellen, und dann zu überprüfen, ob das Zertifikat für den Zielbenutzer installiert wurde.



## <a name="configure-azure-services-wizard"></a>Konfigurieren des Azure Dienste-Assistenten
Technical Preview 1703 führt den Assistenten **zum Konfigurieren von Azure-Diensten** ein. Dieser Assistent bietet eine allgemeine Konfigurationserfahrung, die die einzelnen Workflows mit den Clouddiensten ersetzt, die Sie mit Configuration Manager verwenden. Dies erfolgt mithilfe einer **Azure Web-App**, um das Abonnement und Konfigurationsdetails bereitzustellen, die Sie andernfalls jedes Mal eingeben müssen, wenn Sie eine neue Configuration Manager-Komponente oder einen -Dienst mit Azure einrichten.

Mit Technical Preview 1703 wird nur Windows Store for Business (WSfB) mit diesem Assistenten konfiguriert.  Andere Clouddienste werden mithilfe ihrer eigenen Workflows konfiguriert.

- Verwenden Sie die Informationen in diesem Preview-Thema, um die Konfigurationsschritte im Abschnitt [Einrichten der Synchronisierung](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#bkmk_setup) des Current Branch-Themas [Verwalten von Apps aus dem Windows Store für Unternehmen und Bildungseinrichtungen mit Configuration Manager](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) zu ersetzen.

- Weitere Informationen zu Web-Apps, finden Sie unter [Authentifizierung und Autorisierung in Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview), und [Web-Apps – Übersicht](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).

### <a name="prerequisites-and-planning"></a>Erforderliche Komponenten und Planung
Wenn Sie eine Verbindung zwischen Configuration Manager und dem Windows Store für Unternehmen herstellen, müssen Sie einen Ordner angeben, in dem App-Inhalte, die aus dem Store synchronisiert werden, gespeichert werden. Um sicherzustellen, dass es sich um einen sicheren Ordner handelt, und dass der Inhalt auf Geräten bereitgestellt werden kann, müssen Sie sichergehen, dass die folgenden Berechtigungen vorhanden sind:
- Der Computer, auf dem Sie die Standortsystemrolle „Dienstverbindungspunkt“ installieren (der Standort der obersten Ebene in der Hierarchie), muss über Lese- und Schreibberechtigungen für den Ordner verfügen, den Sie bei der Verwendung des Kontos **Computer$** angegeben haben.  

- Der Autor der App muss über Leseberechtigungen für den angegebenen Ordner verfügen.  

- Das Konto **Computer$** jedes Computers, der eine Instanz des SMS-Anbieters hostet, muss den angegebenen Ordner verwenden können.

Registrieren Sie Configuration Manager über Webanwendung oder Web-API als Verwaltungstool in Azure Active Directory. Dadurch kann die Client-ID erstellt werden, die Sie später benötigen werden.

### <a name="use-the-wizard-to-configure-the-wsfb-cloud-service"></a>Verwenden des Assistenten zum Konfigurieren des WSfB-Clouddiensts

1. Wechseln Sie in der Konsole zu **Verwaltung** > **Übersicht** > **Cloud Services Management** (Verwaltung der Clouddienste) > **Azure** > **Azure-Dienste**, und wählen Sie dann **Configure Azure Services** (Azure-Dienste konfigurieren) aus, um den **Azure-Dienste-Assistenten** zu starten.

2. Wählen Sie auf der Seite **Azure-Dienste** den Dienst aus, den Sie konfigurieren möchten, und klicken Sie dann auf **Weiter**. Mit dieser Vorschau kann nur WSfB konfiguriert werden.

3. Geben Sie auf der Seite **Allgemein** einen Anzeigenamen für den **Azure-Dienstnamen** und eine optionale Beschreibung ein, und klicken Sie dann auf **Weiter**.

4. Auf der **App** Seite geben Sie Ihre Azure-Umgebung an und klicken dann auf **Durchsuchen**, um das Fenster „Server-App“ zu öffnen.

5. Wählen Sie im Fenster **Server App** (Server-App) die Server-App aus, die Sie verwenden möchten, und klicken Sie dann auf **OK**.
   Server-Apps sind Azure-Web-Apps, die Konfigurationen für Ihr Azure-Konto enthalten, einschließlich Ihrer Mandanten-ID, Client-ID und eines geheimen Schlüssels für Clients. Wenn Sie nicht über eine verfügbare Server-App verfügen, verwenden Sie eine der folgenden:
   - **Erstellen:** Wenn Sie eine neue Server-App erstellen möchten, klicken Sie auf **Erstellen**. Geben Sie einen Anzeigenamen für die App und den Mandanten an. Nachdem Sie sich bei Azure angemeldet haben, erstellt Configuration Manager daraufhin die Web-App in Azure für Sie, einschließlich der Client-ID und des geheimen Schlüssels für den Gebrauch mit der Web-App. Später können Sie diese im Azure-Portal anzeigen.
   - **Importieren:** Wenn Sie eine Web-App verwenden möchten, die in Ihrem Azure-Abonnement bereits vorhanden ist, klicken Sie auf **Importieren**. Stellen Sie einen Anzeigenamen für die App und den Mandanten bereit, und geben Sie dann die Mandanten-ID, Client-ID und den geheimen Schlüssel für die Web-App an, die Configuration Manager verwenden soll. Nachdem Sie die Informationen **überprüft** haben, klicken Sie auf **OK**, um fortzufahren.  </br></br>

6. Überprüfen Sie die Seite **Informationen**, und schließen Sie alle zusätzlichen Schritte und Konfigurationen so wie angegeben ab. Diese Konfigurationen sind erforderlich, um den Dienst mit Configuration Manager zu verwenden.
   So konfigurieren Sie z.B. WSfB:

   1. In Azure müssen Sie Configuration Manager als eine Web-Anwendung oder eine Web-API registrieren und die Client-ID notieren. Außerdem geben Sie einen Clientschlüssel für die Verwendung durch das Verwaltungstool (das ist Configuration Manager) an.

   2.    In der WSfB-Konsole müssen Sie Configuration Manager als Speicherverwaltungstool angeben, Unterstützung für Offline-lizenzierte Apps aktivieren und anschließen mindestens eine App kaufen.   </br>

   Klicken Sie zum Fortfahren auf **Weiter**.

7. Schließen Sie auf der Seite **App Configurations** (App-Konfigurationen) die Konfigurationen für den App-Katalog und die Sprache für diesen Dienst ab, und klicken Sie dann auf **Weiter**.
8. Nach Abschluss des Assistenten zeigt die Configuration Manager-Konsole, dass Sie **Windows Store for Business** als **Clouddiensttyp** konfiguriert haben.

Jetzt können Sie den Rest des [Current Branch-Inhalts](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) für das Verwalten von Apps von WSfB zum Synchronisieren, Erstellen und Bereitstellen sowie zum Überwachen von Windows Store for Business-Apps verwenden.

### <a name="modify-a-cloud-service-configuration"></a>Ändern einer Clouddienstkonfiguration
Sie können die Eigenschaften eines Clouddiensts anzeigen und bearbeiten, um die Konfiguration zu ändern.

Wechseln Sie in der Konsole zu **Verwaltung** > **Übersicht** > **Cloud Services Management** (Verwaltung der Clouddienste) > **Azure** > **Azure-Dienste**, und wählen Sie dann **Configure Azure Services** (Azure-Dienste konfigurieren) au, wählen Sie einen Clouddienst aus und anschließend **Eigenschaften**.

## <a name="convert-from-bios-to-uefi-during-an-in-place-upgrade"></a>Konvertieren von BIOS zu UEFI während eines direkten Upgrades
Windows 10 Creators Update führt ein einfaches Konvertierungstool ein, womit der Prozess der Neupartitionierung der Festplatte für UEFI-aktivierte Hardware automatisiert werden kann und das Konvertierungstool in den direkten Upgradeprozess von Windows 7 zu Windows 10 integriert werden kann. Wenn Sie dieses Tool mit Ihrer Tasksequenz des Betriebssystemupgrades und dem OEM-Tool kombinieren, der die Firmware von BIOS zu UEFI konvertiert, können Sie Ihre Computer von BIOS zu UEFI während eines direkten Upgrades zu Windows 10 Creators Update konvertieren. Weitere Informationen finden Sie unter [Task sequence steps to manage BIOS to UEFI conversion (Tasksequenzschritte für das Verwalten einer Konvertierung von BIOS zu UEFI)](../../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#convert-from-bios-to-uefi-during-an-in-place-upgrade).

## <a name="collapsible-task-sequence-groups"></a>Reduzierbare Tasksequenzgruppen
Diese Version bietet die Möglichkeit zum Erweitern und Reduzieren von Tasksequenzgruppen. Sie können einzelne Gruppen erweitern oder reduzieren oder alle Gruppen auf einmal erweitern oder reduzieren.


## <a name="client-settings-to-configure-windows-analytics-for-upgrade-readiness"></a>Clienteinstellungen zum Konfigurieren von Windows Analytics für Upgrade Readiness
Ab dieser Version können Sie Clienteinstellungen für Geräte verwenden, um die Konfiguration der Windows-Diagnosedaten zu vereinfachen, die für die Verwendung von Windows Analytics-Lösungen wie z. B. Upgradebereitschaft mit Configuration Manager erforderlich sind. Configuration Manager kann Daten aus Windows Analytics abrufen, die wertvolle Informationen über den aktuellen Zustand Ihrer Umgebung liefern. Diese Informationen basieren auf den Windows-Diagnosedaten, die von Ihren Clientcomputern gemeldet werden. Windows-Diagnosedaten werden von Clientcomputern an den Windows-Diagnosedienst gemeldet. Anschließend werden relevante Daten an Windows Analytics-Lösungen übertragen, die in einem der OMS-Arbeitsbereiche Ihrer Organisation gehostet werden. Die Upgradebereitschaft ist eine Windows Analytics-Lösung, die Sie bei der Priorisierung von Entscheidungen über Windows-Upgrades für Ihre verwalteten Geräte unterstützt.

### <a name="prerequisites"></a>Voraussetzungen
- Sie müssen Ihren Standort zur Verwendung des Clouddiensts für die Upgradebereitschaft konfiguriert haben.

### <a name="configure-windows-analytics-client-settings"></a>Konfigurieren von Clienteinstellungen für Windows Analytics
Wechseln Sie zum Konfigurieren von Windows Analytics in der Configuration Manager-Konsole zu **Verwaltung** > **Clienteinstellungen**, doppelklicken Sie auf **Benutzerdefinierte Clienteinstellungen für Geräte erstellen**, und aktivieren Sie dann **Windows Analytics**.  

Wechseln Sie zur Registerkarte mit den Einstellungen für **Windows Analytics**, und konfigurieren Sie Folgendes:
- **Kommerzielle ID**  
Der Schlüssel „Kommerzielle ID“ ordnet Informationen der von Ihnen verwalteten Geräte zu dem OMS-Arbeitsbereich zu, der die Windows Analytics-Daten Ihrer Organisation hostet. Wenn Sie bereits einen kommerziellen ID-Schlüssel für die Verwendung mit der Upgradebereitschaft konfiguriert haben, verwenden Sie diese ID. Wenn Sie noch keinen kommerziellen ID-Schlüssel haben, generieren Sie Ihren kommerziellen ID-Schlüssel.

- Legen Sie eine **Diagnosedatenebene für Windows 10-Geräte fest**.

- **Stimmen Sie der Sammlung kommerzieller Daten auf Geräten unter Windows 7, 8 und 8.1 zu**   

- **Konfigurieren der Datensammlung von Internet Explorer**: Auf Geräten unter Windows 8.1 oder früher kann die Internet Explorer-Datensammlung es der Upgradebereitschaft ermöglichen, Inkompatibilitäten von Web-Apps zu erkennen, die ein reibungsloses Upgrade auf Windows 10 verhindern könnten. Die Internet Explorer-Datensammlung kann für einzelne Internetzonen aktiviert werden.
