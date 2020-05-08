---
title: Funktionen in Technical Preview 1610
titleSuffix: Configuration Manager
description: Erfahren Sie mehr zu Features, die in Technical Preview für Configuration Manager-Version 1610 zur Verfügung stehen.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8b31fd3e-875a-4a31-9498-5b050aadce32
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: cee161747d5c0b462836b7c3a44e1460173b124c
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82905661"
---
# <a name="capabilities-in-technical-preview-1610-for-configuration-manager"></a>Funktionen in der Technical Preview 1610 für Configuration Manager

*Gilt für: Configuration Manager (Technical Preview-Branch)*



In diesem Artikel werden die Features vorgestellt, die in der Technical Preview-Version 1610 für Configuration Manager verfügbar sind. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen.      Bevor Sie diese Version der Technical Preview installieren, lesen Sie das einführende Thema [Technical Preview für Configuration Manager](../../core/get-started/technical-preview.md), um sich mit den allgemeinen Anforderungen und Einschränkungen bei der Verwendung einer Technical Preview vertraut zu machen und um zu erfahren, wie Sie Updates für Versionen durchführen und Feedback zu den Features in einer Technical Preview geben können.    


**Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  
## <a name="filter-by-content-size-in-automatic-deployment-rules"></a>Filtern nach Inhaltsgröße in automatischen Bereitstellungsregeln
Sie können jetzt nach Inhaltsgrößen für Softwareupdates in automatischen Bereitstellungsregeln filtern. Sie können z.B. den Filter **Inhaltsgröße (KB)** auf **< 2048** festlegen, um nur die Softwareupdates herunterzuladen, die kleiner als 2 MB sind. Mit diesem Filter wird verhindert, dass große Softwareupdates automatisch heruntergeladen werden, um die vereinfachte Windows-Wartung vorheriger Versionen zu unterstützen, wenn die Bandbreite eingeschränkt ist. Details finden Sie unter [Configuration Manager und vereinfachte Windows-Wartung auf vorherigen Betriebssystemebene](https://techcommunity.microsoft.com/t5/configuration-manager-archive/configuration-manager-and-simplified-windows-servicing-on-down/ba-p/274056).

#### <a name="to-configure-the-content-size-field"></a>So konfigurieren Sie das Feld für die Inhaltsgröße
Navigieren Sie zur Seite **Softwareupdates** im Assistenten zum Erstellen automatischer Bereitstellungsregeln, wenn Sie einen ADR erstellen, oder zur Registerkarte **Softwareupdates** in den Eigenschaften für einen vorhandenen ADR, um das Feld **Inhaltsgröße (KB)** zu konfigurieren.

![Feld für Inhaltsgröße](media/contentsizefield.png)

## <a name="improved-functionality-for-required-software-dialogs"></a>Verbesserte Funktionalität für erforderliche Softwaredialoge
Wenn ein Benutzer erforderliche Software von der Einstellung **Warten und erinnern:** erhält, kann er sie aus der folgenden Dropdownliste von Werten auswählen:
- Später: Gibt an, dass Benachrichtigungen basierend auf den in den Client-Agenteinstellungen konfigurierten Benachrichtigungseinstellungen geplant sind
- Feste Zeit: Gibt an, dass die Benachrichtigung nach der ausgewählten Zeit erneut angezeigt wird. Wenn ein Benutzer z.B. 30 Minuten auswählt, wird die Benachrichtigung in 30 Minuten erneut angezeigt.

![Computer-Agentseite in den Client-Agenteinstellungen](media/computeragentsettings.png)

Die maximale Wartezeit basiert immer auf den Benachrichtigungswerten, die in den Einstellungen des Client-Agents zu jedem Zeitpunkt der Bereitstellung konfiguriert sind. Wenn zum Beispiel die Einstellung **Bereitstellungsstichtag in mehr als 24 Stunden, Benutzer erinnern alle (Stunden)** auf der Seite des Computer-Agents auf 10 Stunden festgelegt ist und das Dialogfeld mehr als 24 Stunden vor Ablauf der Frist gestartet wird, erhält der Benutzer einen Satz an Warteoptionen von bis zu, aber nie mehr als 10 Stunden. Wenn sich der Stichtag nähert, wird das Dialogfeld weniger Optionen anzeigen. Dies stimmt mit den entsprechenden Client-Agenteinstellungen für jede Komponente der Bereitstellungszeit überein.

Darüber hinaus fällt bei Bereitstellungen mit hohem Risiko, z.B. einer Tasksequenz, die ein Betriebssystem bereitstellen, die Benachrichtigung des Endbenutzers deutlicher aus. Immer wenn der Benutzer benachrichtigt wird, dass eine kritische Softwarewartung erforderlich ist, wird anstatt einer vorübergehenden Benachrichtigung in der Taskleiste ein Dialogfeld wie das folgende auf dem Computer des Benutzers angezeigt:

![Erforderlicher Softwaredialog](media/requiredsoftwaredialog.png)


Weitere Informationen finden Sie unter:
- [Einstellungen zum Verwalten von Bereitstellungen mit hohem Risiko](../servers/manage/settings-to-manage-high-risk-deployments.md)
- [Konfigurieren von Clienteinstellungen](../clients/deploy/configure-client-settings.md)

## <a name="deny-previously-approved-application-requests"></a>Zuvor genehmigte Anwendungsanforderungen verweigern

Als Administrator können Sie jetzt eine zuvor genehmigte Anwendungsanforderung verweigern. Einmal verweigert, müssen spätere Benutzer eine erneute Anfrage zur Installation dieser Anwendung stellen. Die Anwendung wird durch die Verweigerung nicht deinstalliert. Stattdessen wird eine erneute Genehmigung für jede neue Anforderung für diese Anwendung von diesem Benutzer erzwungen. Bisher war die Verweigerung einer Anwendungsanforderung nur für Anwendungsanforderungen verfügbar, die nicht genehmigt wurden.

#### <a name="try-it-out"></a>Probieren Sie es aus
So verweigern Sie eine genehmigte Anwendungsanforderung:

1. [Erstellen Sie eine Anwendung](../../apps/deploy-use/create-applications.md) in der Configuration Manager-Konsole, die eine Genehmigung benötigt, und stellen Sie sie bereit.
2. Öffnen Sie das Softwarecenter auf einem Clientcomputer, und reichen Sie eine Anwendungsanforderung ein.
3. Genehmigen Sie die Anwendungsanforderung in der Configuration Manager-Konsole.
4. Genehmigte Anwendungsanforderung ablehnen: Navigieren Sie In der Configuration Manager-Konsole zu **Softwarebibliothek** > **Übersicht** > **Anwendungsverwaltung** > **Genehmigungsanforderungen**, und wählen Sie die Anwendungsanforderung aus, die Sie verweigern möchten.  Klicken Sie im Menüband auf **Verweigern**.

## <a name="exclude-clients-from-automatic-upgrade"></a>Ausschließen von Clients von automatischen Upgrades
Technical Preview 1610 führt eine neue Einstellung ein, die Sie verwenden können, um eine Clientsammlung von der automatischen Installation aktualisierter Clientversionen auszuschließen.  Dies gilt sowohl für automatische Upgrades und als auch für andere Methoden, wie Upgrades auf der Basis von Softwareupdates, Registrierungsskripts und Gruppenrichtlinien. Dies kann für eine Computersammlung genutzt werden, die bei einem Upgrade des Clients größere Sorgfalt benötigt. Ein Client, der sich in einer ausgeschlossenen Sammlung befindet, ignoriert Anforderungen zur Installation von aktualisierter Clientsoftware.

### <a name="configure-exclusion-from-automatic-upgrade"></a>Ausschluss vom automatischen Upgrade konfigurieren
So konfigurieren Sie Ausschlüsse aus automatischen Upgrades:
1. Öffnen Sie in der Configuration Manager-Konsole die **Hierarchieeinstellungen** unter **Verwaltung > Standortkonfiguration > Standorte**, und wählen Sie dann die Registerkarte **Clientupgrade** aus.
2. Aktivieren Sie die Kontrollkästchen **Exclude specified clients from upgrade** (Angegebene Clients aus Upgrades ausschließen) und **Exclusion collection** (Ausschlusssammlung), und wählen Sie die Sammlung aus, die Sie ausschließen möchten. Sie können nur eine einzelne Sammlung für den Ausschluss auswählen.
3. Klicken Sie auf **OK**, um die Konfiguration zu schließen und zu speichern. Nachdem die Clients Richtlinien aktualisiert haben, können Clients in der ausgeschlossenen Sammlung nicht mehr automatisch Updates der Clientsoftware installieren.

   ![Einstellungen für automatische Ausschlüsse aus Upgrades](media/automatic_upgrade_exclusion.png)

> [!NOTE]
> Obwohl die Benutzeroberfläche angibt, dass Upgrades für Clients nicht mit einer beliebigen Methode durchgeführt werden können, gibt es zwei Methoden, die Sie verwenden können, um diese Einstellungen außer Kraft zu setzen. Die Clientpushinstallation und eine manuelle Clientinstallation können verwendet werden, um diese Konfiguration außer Kraft zu setzen. Weitere Details erfahren Sie im nächsten Abschnitt.

### <a name="how-to-upgrade-a-client-that-is-in-an-excluded-collection"></a>So führen Sie für einen Client in einer ausgeschlossenen Sammlung ein Upgrade durch
Solange eine Sammlung für den Ausschluss konfiguriert ist, können Mitglieder dieser Sammlung ihre Clientsoftware nur mit einer der beiden Methoden, die den Ausschluss außer Kraft setzen, upgegradet werden:
- **Clientpushinstallation** – Sie können die Clientpushinstallation verwenden, um einen Client in einer ausgeschlossen Sammlung upzugraden. Dies ist zulässig, da es als Absicht des Administrators betrachtet wird und Ihnen ermöglicht, Clients upzugraden, ohne die gesamte Sammlung aus der Ausschlussliste zu entfernen.       
- **Manuelle Clientinstallation** – Sie können Clients in einer ausgeschlossenen Sammlung unter Verwendung des Befehlszeilenschalters ***/ignoreskipupgrade*** mit ccmsetup manuell upgraden.

  Wenn Sie versuchen, einen Client, der Mitglied der ausgeschlossenen Sammlung ist, manuell upzugraden, und diesen Schalter nicht verwenden, wird der Client die neue Clientsoftware nicht installieren. Weitere Informationen finden Sie unter [Manuelles Installieren von Configuration Manager-Clients](../clients/deploy/deploy-clients-to-windows-computers.md#BKMK_Manual).

Weitere Informationen zu Clientinstallationsmethoden finden Sie unter [Bereitstellen von Clients auf Windows-Computern](../clients/deploy/deploy-clients-to-windows-computers.md).

## <a name="windows-defender-configuration-settings"></a>Windows Defender-Konfigurationseinstellungen

Sie können Windows Defender-Clienteinstellungen auf Intune-registrierten Windows 10-Computern mithilfe von Konfigurationselementen in der Configuration Manager-Konsole konfigurieren.

Dabei können Sie insbesondere die folgenden Windows Defender-Einstellungen konfigurieren:
- Echtzeitüberwachung zulassen
- Verhaltensüberwachung zulassen
- Netzwerkinspektionssystem aktivieren
- Alle heruntergeladene Dateien überprüfen
- Skriptüberprüfung zulassen
- Datei- und Programmaktivität überwachen
  - Überwachte Dateien
- Tage für Nachverfolgung behandelter Schadsoftware
- Zugriff auf die Clientbenutzeroberfläche zulassen
- Systemüberprüfung planen
  - Geplanter Tag
  - Geplante Zeit
- Eine tägliche Schnellüberprüfung planen
  - Geplante Zeit
- CPU-Auslastung während einer Überprüfungen begrenzen auf % Archivdateien überprüfen
- Scannen von E-Mail-Nachrichten
- Wechseldatenträger überprüfen
- Zugeordnete Laufwerke überprüfen
- Scan files opened from net shares (Von Netzwerkfreigaben geöffnete Dateien überprüfen)
- Intervall zum Aktualisieren von Signaturen
- Cloudschutz zulassen
- Beim Senden von Beispielen beim Benutzer nachfragen
- Erkennung möglicherweise unerwünschter Anwendungen
- Ausgeschlossene Dateien und Ordner
- Ausgeschlossene Dateierweiterungen
- Ausgeschlossene Prozesse

> [!NOTE]
> Diese Einstellungen können nur auf Clientcomputern unter Windows 10 November-Update (1511) und höher konfiguriert werden.

### <a name="try-it-out"></a>Probieren Sie es aus!

1. Navigieren Sie in der Configuration Manager-Konsole zu **Bestand und Konformität** > **Überblick** > **Konformitätseinstellungen** > **Konfigurationselemente**, und erstellen Sie ein neues **Konfigurationselement**.
2. Geben Sie einen Namen ein, und wählen Sie dann unter **Settings for devices managed without the Configuration Manager client** (Einstellungen für Geräte, die ohne Configuration Manager-Client verwaltet werden) die Option **Windows 8.1 und Windows 10** aus. Klicken Sie dann auf **Weiter**.
3. Stellen Sie sicher, dass auf der Seite **Unterstützte Plattformen** die Optionen **All Windows 10 (64-bit)** (Alle Windows 10 (64-Bit)) und **All Windows 10 (32-bit)** (Alle Windows 10 (32-Bit)) ausgewählt wurden. Klicken Sie dann auf **Weiter**.
4. Wählen Sie die Einstellungsgruppe **Windows Defender** aus, und klicken Sie dann auf **Weiter**.
5. Konfigurieren Sie die gewünschten Einstellungen auf dieser Seite, und klicken Sie dann auf **Weiter**.
6. Schließen Sie den Assistenten ab.
7. Fügen Sie dieses Konfigurationselement zu einer Konfigurationsbaseline hinzu, und stellen Sie diese Baseline auf Computern bereit, auf denen das Update von November für Windows 10 (1511) oder höher ausgeführt wird.

> [!NOTE]
> Vergessen Sie nicht, das Kontrollkästchen **Nicht konforme Einstellungen wiederherstellen** zu aktivieren, wenn Sie die Konfigurationsbaseline bereitstellen.

## <a name="request-policy-sync-from-administrator-console"></a>Anfordern der Richtliniensynchronisierung von der Administratorkonsole

Sie können nun eine Richtliniensynchronisierung für ein mobiles Gerät auf der Configuration Manager-Konsole anfordern, anstatt dies auf dem Gerät selbst tun zu müssen. Informationen zum Status der Synchronisierungsanforderung stehen nun in Geräteansichten als neue Spalte **Remote Sync State** (Remotesynchronisierungsstatus) zur Verfügung. Der Status wird auch im Bereich **Ermittlungsdaten** des Dialogfelds **Eigenschaften** für jedes mobile Gerät angezeigt.

### <a name="try-it-out"></a>Probieren Sie es aus!

1. Navigieren Sie in der Configuration Manager-Konsole zu **Bestand und Konformität** > **Übersicht** > „Geräte“.
2. Wählen Sie im Menü **Remote Device Actions** (Remotegeräteaktionen) die Option **Send Sync Request** (Synchronisationsanforderung senden) aus.

Die Synchronisierung kann fünf bis zehn Minuten dauern. Alle Änderungen an der Richtlinie werden mit dem Gerät synchronisiert. Sie können den Status der Synchronisierungsanforderung in der Spalte **Remote Sync State (Remotesynchronisierungsstatus)** der Ansicht **Geräte** oder im Dialogfeld **Eigenschaften** des Geräts verfolgen.

## <a name="additional-security-role-support"></a>Unterstützung zusätzlicher Sicherheitsrollen

Zusätzlich zu „Hauptadministrator“ haben nun die folgenden integrierten Sicherheitsrollen vollen Zugriff auf Elemente im Knoten **Alle unternehmenseigenen Geräte**, einschließlich **Vorab deklarierte Geräte**, **iOS-Registrierungsprofile** und **Windows-Registrierungsprofile**:
- **Asset-Manager**
- **Zugriffs-Manager für Unternehmensressourcen**

Der Rolle **Analyst mit Leseberechtigung** wird weiterhin der schreibgeschützte Zugriff auf diese Bereiche der Configuration Manager-Konsole gewährt.

## <a name="conditional-access-for-windows-10-vpn-profiles"></a>Bedingter Zugriff für Windows 10-VPN-Profile

Sie können jetzt festlegen, dass in Azure Active Directory registrierte Windows 10-Geräte kompatibel sein müssen, damit sie VPN-Zugriff über in der Configuration Manager-Konsole erstellte Windows 10-VPN-Profile haben. Möglich ist dies über das neue Kontrollkästchen **Bedingten Zugriff für diese VPN-Verbindung aktivieren** auf der Seite **Authentifizierungsmethode** im Assistenten zum Erstellen von VPN-Profilen und in den VPN-Profileigenschaften für Windows 10-VPN-Profile. Wenn Sie den bedingten Zugriff für das Profil aktivieren, können Sie auch ein separates Zertifikat für die Einmalanmeldungsauthentifizierung angeben.

## <a name="see-also"></a>Weitere Informationen
[Technical Preview für Configuration Manager](../../core/get-started/technical-preview.md)
