---
title: Microsoft Store-Apps
titleSuffix: Configuration Manager
description: Verwalten Sie Apps aus dem Microsoft Store für Unternehmen und Bildungseinrichtungen mit Configuration Manager, und stellen Sie diese bereit.
ms.date: 12/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 8cdb22a6-72d7-41f5-9bed-c098b1bcf675
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b8ba727aff682e3efbba6a91941a5499f9f00e8b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689318"
---
# <a name="manage-apps-from-the-microsoft-store-for-business-and-education-with-configuration-manager"></a>Verwalten von Apps aus dem Microsoft Store für Unternehmen und Bildungseinrichtungen mit Configuration Manager

Im [Microsoft Store für Unternehmen und Bildungseinrichtungen](https://docs.microsoft.com/microsoft-store/) können Sie für Ihre Organisation nach Windows-Apps suchen und diese erwerben. Nachdem Sie den Store mit Configuration Manager verbunden haben, synchronisieren Sie die Liste mit den erworbenen Apps. Anschließend können Sie sich diese Apps in der Configuration Manager-Konsole anzeigen lassen und sie so wie jede andere App bereitstellen.

## <a name="online-and-offline-apps"></a><a name="bkmk_apps"></a> Online- und Offline-Apps

Der Microsoft Store für Unternehmen und Bildungseinrichtungen unterstützt zwei Typen von Apps:

- **Online:** Dieser Lizenztyp setzt voraus, dass Benutzer und Geräte mit dem Store verbunden sind, um eine App und die zugehörige Lizenz zu erhalten. Windows 10-Geräte müssen in Azure Active Directory (Azure AD) oder in Azure AD Hybrid eingebunden sein.  

- **Offline**: Dieser Typ ermöglicht das Zwischenspeichern von Apps und Lizenzen für die direkte Bereitstellung in Ihrem lokalen Netzwerk. Die Geräte müssen nicht mit dem Store verbunden sein oder über eine Internetverbindung verfügen.

Weitere Informationen finden Sie unter [Microsoft Store für Unternehmen und Bildungseinrichtungen – Übersicht](https://docs.microsoft.com/microsoft-store/microsoft-store-for-business-overview).

### <a name="summary-of-capabilities"></a>Zusammenfassung der Funktionen

Configuration Manager unterstützt das Verwalten von Apps für Microsoft Store für Unternehmen und Bildungseinrichtungen auf Windows 10-Geräten, auf denen der Konfigurations-Manager-Client ausgeführt wird, sowie auf Windows 10-Geräten, die in Microsoft Intune registriert sind. Configuration Manager bietet die folgenden Funktionen für Online- und Offline-Apps:

|Funktion|Offline-Apps|Online-Apps|
|------------|------------|------------|
|Synchronisieren von App-Daten mit Configuration Manager<br>(Synchronisierung erfolgt alle 24 Stunden)|Ja|Ja|
|Erstellen von Configuration Manager-Anwendungen aus Store-Apps|Ja|Ja|
|Unterstützung für kostenlose Apps aus dem Store|Ja|Ja|
|Unterstützung für kostenpflichtige Apps aus dem Store|Nein|Ja<sup>[Hinweis 1](#bkmk_note1)</sup>|
|Unterstützen von erforderlichen Bereitstellungen für Benutzer- oder Gerätesammlungen|Ja|Ja|
|Unterstützen von verfügbaren Bereitstellungen für Benutzer- oder Gerätesammlungen|Ja|Ja|
|Unterstützung von branchenspezifischen Apps aus dem Store|Ja|Ja|
|Bereitstellen einer Store-App für alle Benutzer auf einem Gerät <sup>[Hinweis 2](#bkmk_note2)</sup><!--1358310-->|Ja|Ja|

#### <a name="note-1-online-licensed-apps-version-requirement"></a><a name="bkmk_note1"></a> Hinweis 1: Versionsanforderung für online lizenzierte Apps

Wenn Sie Apps, die online lizenziert sind, für Windows 10-Geräte mit dem Konfigurations-Manager-Client bereitstellen möchten, muss Windows 10, Version 1703 oder höher auf diesen Geräten ausgeführt werden.  

#### <a name="note-2-configuration-manager-minimum-version"></a><a name="bkmk_note2"></a> Hinweis 2: Mindestversion für Configuration Manager

Ab Version 1806. Weitere Informationen finden Sie unter [Erstellen von Windows-Anwendungen](../get-started/creating-windows-applications.md#bkmk_provision).  

### <a name="deploying-online-apps-using-the-microsoft-store-for-business-and-education-to-devices-that-run-the-configuration-manager-client"></a>Bereitstellen von Online-Apps mit dem Microsoft Store für Unternehmen und Bildungseinrichtungen für Geräte, auf denen der Konfigurations-Manager-Client ausgeführt wird

Vor der Bereitstellung von Apps aus dem Microsoft Store für Unternehmen und Bildungseinrichtungen auf Geräten, auf denen der vollständige Konfigurations-Manager-Client ausgeführt wird, sollten Sie Folgendes beachten:

- Damit mit alle Funktionen genutzt werden können, muss auf den Geräten die Windows 10-Version 1703 oder höher ausgeführt werden.  

- Registrieren oder verbinden Sie Geräte mit demselben Azure AD-Mandanten, bei dem Sie den Microsoft Store für Unternehmen und Bildungseinrichtungen als Verwaltungstool registriert haben.  

- Wenn das lokale Administratorkonto auf dem Gerät angemeldet wird, kann über dieses nicht auf Apps aus dem Microsoft Store für Unternehmen und Bildungseinrichtungen zugegriffen werden.  

- Geräte benötigen eine aktive Internetverbindung zum Microsoft Store für Unternehmen und Bildungseinrichtungen. Weitere Informationen einschließlich Hinweisen zur Proxykonfiguration finden Sie unter [Voraussetzungen](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business).  

### <a name="notes-for-devices-running-earlier-versions-of-windows-10"></a>Hinweise zu Geräten, auf denen frühere Versionen von Windows 10 ausgeführt werden

Auf Geräten, auf denen der Konfigurations-Manager-Client und die Windows 10-Version 1607 oder niedriger ausgeführt werden, ist das unten beschriebene Verhalten zu berücksichtigen.  

Wenn auf dem Gerät die Installation der App durch  

- die Installation der App seitens des Benutzers,  

- den Ablauf des Installationsstichtags für die Bereitstellung oder

- die Neuauswertung für erforderliche Bereitstellungen nach der Installation erzwungen wird,  

tritt folgendes Verhalten ein:  

- Der Konfigurations-Manager-Client erzwingt die Installation der App durch den Start der Microsoft Store-App.  

- Der Benutzer muss die Installation über den Store abschließen.  

- In der Configuration Manager-Konsole wird bei einem Fehlschlag folgender Fehler vom Bereitstellungsstatus der App ausgegeben: „The Microsoft Store app was opened on the client PC and is waiting for the user to complete the installation.“ (Die Microsoft Store-App wurde auf dem Client-PC geöffnet und wartet auf den Abschluss der Installation durch den Benutzer).  

Im nächsten Evaluierungszyklus für die Anwendung:  

- Wenn der Benutzer die Anwendung über den Store installiert hat, meldet die Anwendung den Status **Erfolg**.  

- Wenn der Benutzer nicht versucht hat, die App über den Store zu installieren,  

  - startet der Konfigurations-Manager-Client die Store-App erneut für erforderliche Bereitstellungen,  

  - Configuration Manager erzwingt verfügbare Bereitstellungen nicht erneut

#### <a name="devices-running-earlier-versions-of-windows-10"></a>Geräte, auf denen frühere Versionen von Windows 10 ausgeführt werden

- Sie können keine branchenspezifischen Apps aus dem Microsoft Store für Unternehmen und Bildungseinrichtungen bereitstellen.

- Wenn Sie kostenpflichtige Apps aus dem Store bereitstellen, müssen Benutzer sich beim Store anmelden und die App selbst erwerben.  

- Wenn Sie eine Gruppenrichtlinie bereitstellen, die den Zugriff auf die Benutzerversion des Microsoft Store deaktiviert, funktionieren Bereitstellungen aus dem Microsoft Store für Unternehmen und Bildungseinrichtungen nicht. Dieses Verhalten tritt auch dann auf, wenn Sie den Microsoft Store für Unternehmen und Bildungseinrichtungen aktivieren.  

## <a name="set-up-synchronization"></a><a name="bkmk_setup"></a> Einrichten der Synchronisierung

Wenn Sie die Liste für Apps aus dem Microsoft Store für Unternehmen und Bildungseinrichtungen synchronisieren, die von Ihrem Unternehmen erworben wurden, werden Ihnen diese Apps in der Configuration Manager-Konsole angezeigt.

Verbinden Sie Ihren Configuration Manager-Standort mit Azure AD und dem Microsoft Store für Unternehmen und Bildungseinrichtungen. Weitere Informationen und Details hierzu finden Sie unter [Konfigurieren von Azure-Diensten](../../core/servers/deploy/configure/azure-services-wizard.md). Stellen Sie eine Verbindung mit dem **Microsoft Store für Unternehmen**-Dienst her.

Stellen Sie sicher, dass der Dienstverbindungspunkt und die Zielgeräte auf den Clouddienst zugreifen können. Weitere Informationen finden Sie unter [Voraussetzungen für Microsoft Store für Unternehmen und Bildungseinrichtungen – Proxykonfiguration](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration).

### <a name="supplemental-information-and-configuration"></a><a name="bkmk_config"></a> Weitere Informationen und Konfigurationen

Konfigurieren Sie auf der Seite **App** des Assistenten für Azure-Dienste zunächst die **Azure-Umgebung** und die **Web-App**. Lesen Sie anschließend unten auf der Seite den Abschnitt **Weitere Informationen**. Dort werden die folgenden zusätzlichen Aktionen für das Microsoft Store für Unternehmen und Bildungseinrichtungen-Portal beschrieben:  

- Konfigurieren von Configuration Manager als Speicherverwaltungstool. Weitere Informationen finden Sie unter [Configure management provider (Konfigurieren eines Verwaltungsanbieters)](https://docs.microsoft.com/microsoft-store/configure-mdm-provider-microsoft-store-for-business).  

- Aktivieren von offline lizenzierten Apps. Weitere Informationen finden Sie unter [Verteilen von Offline-Apps](https://docs.microsoft.com/microsoft-store/distribute-offline-apps).  

- Erwerben mindestens einer App. Weitere Informationen finden Sie unter [Suchen und Erwerben von Apps](https://docs.microsoft.com/microsoft-store/find-and-acquire-apps-overview).  

Geben Sie auf der Seite **Konfigurationen** des Assistenten für Azure-Dienste die folgenden Informationen an:  

- **Pfad zum Inhaltsspeicher der Microsoft Store für Unternehmen-App:** Geben Sie einen freigegebenen Netzwerkpfad an, einschließlich eines Ordners. Beispiel: `\\server\share\folder`. Wenn der Standortserver mit dem Store synchronisiert wird, werden die Inhalte an diesem Speicherort zwischengespeichert. Wenn Sie eine Anwendung in Configuration Manager erstellen, kopiert der Standortserver App-Inhalte aus dem lokalen Cache in die Inhaltsbibliothek des Standorts.  

- **Selected languages** (Ausgewählte Sprachen): Wählen Sie die Sprachen aus, für die Inhalte aus dem Store synchronisiert und Benutzern im Softwarecenter angezeigt werden sollen. Wenn ein Benutzer beispielsweise die deutschsprachige Version von Windows konfiguriert, werden im Softwarecenter deutsche Zeichenfolgen für Store-Apps angezeigt. Dieses Verhalten setzt voraus, dass die Inhalte für diese Sprache synchronisiert werden und für die jeweilige Anwendung vorhanden sind.

- **Standardsprache**: Wählen Sie die Standardsprache aus, die verwendet werden soll, wenn die Benutzersprache nicht verfügbar ist.  

## <a name="create-and-deploy-the-app"></a><a name="bkmk_deploy"></a>Erstellen und Bereitstellen der App

Erstellen Sie nach der Synchronisierung die Apps aus dem Microsoft Store für Unternehmen und Bildungseinrichtungen ähnlich wie jede andere Configuration Manager-Anwendung und stellen Sie sie bereit.

1. Erweitern Sie im Arbeitsbereich **Softwarebibliothek** der Configuration Manager-Konsole den Eintrag **Anwendungsverwaltung**, und wählen Sie anschließend den Knoten **Lizenzinformationen für Store-Apps** aus.  

2. Wählen Sie die App aus, die Sie bereitstellen möchten, und wählen Sie anschließend im Menüband **Anwendung erstellen** aus.  

Der Standort erstellt eine Configuration Manager-Anwendung, die die Microsoft Store für Unternehmen und Bildungseinrichtungen-App enthält.

Sie können diese Anwendung nun wie jede andere Configuration Manager-Anwendung bereitstellen und überwachen. Weitere Informationen finden Sie in den folgenden Artikeln:  

- [Bereitstellen von Anwendungen](deploy-applications.md)
- [Überwachen von Anwendungen in der Konsole](monitor-applications-from-the-console.md)

## <a name="next-steps"></a>Nächste Schritte

Erweitern Sie im Arbeitsbereich **Softwarebibliothek** die Option **Anwendungsverwaltung**, und wählen Sie anschließend den Knoten **Lizenzinformationen für Store-Apps** aus.

Sie können sich für jede verwaltete Store-App die folgenden App-Informationen anzeigen lassen:

- App-Name
- App-Plattform
- Anzahl der Lizenzen für die erworbene App
- Anzahl verfügbarer Lizenzen

Nach der Bereitstellung von Online-Apps werden alle App-Updates direkt über den Microsoft Store bereitgestellt. Configuration Manager überprüft nicht, ob unterschiedliche Versionen von Online-Apps konform sind. Stattdessen wird nur überprüft, ob die App-Installation von Windows erkannt wurde.  

Bei der Bereitstellung von Offline-Apps mit dem Konfigurations-Manager-Client auf Windows 10-Geräten müssen Sie sicherstellen, dass Benutzer nicht über die Berechtigung verfügen, Anwendungen zu aktualisieren, die nicht Teil der Configuration Manager-Bereitstellungen sind. Die Steuerung der Updates von Offline-Apps ist in Umgebungen mit mehreren Benutzern (z.B. Kursräumen) besonders wichtig. [Gruppenrichtlinien](https://docs.microsoft.com/windows/configuration/stop-employees-from-using-microsoft-store#block-microsoft-store-using-group-policy) sind eine Möglichkeit zum Deaktivieren von Microsoft Store.

Wenn der Administrator von Microsoft Store für Unternehmen und Bildungseinrichtungen eine Offline-App erwirbt, sollten Sie diese nicht über den Store für Benutzer veröffentlichen. Durch diese Konfiguration wird sichergestellt, dass Benutzer die App nicht installieren oder online aktualisieren können. Die Benutzer erhalten ausschließlich über Configuration Manager Offlineupdates für die App.

## <a name="see-also"></a>Weitere Informationen:

[Behandeln von Problemen bei der Integration des Microsoft Store für Unternehmen und Bildungseinrichtungen in Configuration Manager](troubleshoot-microsoft-store-for-business-integration.md)
