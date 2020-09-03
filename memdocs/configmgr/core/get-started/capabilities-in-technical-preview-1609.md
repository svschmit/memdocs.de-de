---
title: Funktionen in Technical Preview 1609
titleSuffix: Configuration Manager
description: Erfahren Sie mehr zu Features, die in Technical Preview für Configuration Manager-Version 1609 zur Verfügung stehen.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e2a59116-b2e5-4dd2-90eb-0b8a5eb50b56
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
ms.openlocfilehash: 05ed0daf56275b2e0ed46b2f9dd93fd66eb360be
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88995533"
---
# <a name="capabilities-in-technical-preview-1609-for-configuration-manager"></a>Funktionen in der Technical Preview 1609 für Configuration Manager

*Gilt für: Configuration Manager (Technical Preview-Branch)*



In diesem Artikel werden die Features vorgestellt, die in der Technical Preview-Version 1609 für Configuration Manager verfügbar sind. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen.      Bevor Sie diese Version der Technical Preview installieren, lesen Sie das einführende Thema [Technical Preview für Configuration Manager](../../core/get-started/technical-preview.md), um sich mit den allgemeinen Anforderungen und Einschränkungen bei der Verwendung einer Technical Preview vertraut zu machen und um zu erfahren, wie Sie Updates für Versionen durchführen und Feedback zu den Features in einer Technical Preview geben können.    

**Bekannte Probleme in dieser Technical Preview:**  
*  Wenn Sie auf Configuration Manager 1609 Technical Preview aktualisieren, werden alle Editionsaktualisierungsrichtlinien, die Sie bereitgestellt haben, gelöscht. Um diese Richtlinien weiterhin zu verwenden, müssen Sie sie neu erstellen und bereitstellen.


**Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  

## <a name="improvements-to-endpoint-protection"></a>Verbesserungen bei Endpoint Protection
Verbesserung der Einstellungen der Endpoint Protection-Richtlinie für Antischadsoftware: Sie können nun die Ebene angeben, auf der Cloud Protection Service von Endpoint Protection verdächtige Dateien sperrt. Eine neue Einstellung ermöglicht Administratoren das Angeben von „riskanten“ Computern basierend auf großen Mengen von Schadsoftware, die gefunden werden.

## <a name="increased-number-of-enrolled-devices"></a>Erhöhte Anzahl registrierter Geräte
Administratoren können Benutzern jetzt ermöglichen, bis zu 15 Geräte bei der hybriden Verwaltung mobiler Geräte mit Intune zu registrieren. Der Grenzwert lag zuvor bei 5 Geräten pro Benutzer.

## <a name="additional-apple-dep-settings"></a>Zusätzliche Apple-DEP-Einstellungen

Administratoren können jetzt die folgenden Einstellungen für das Apple-Programm zur Geräteregistrierung (Device Enrollment Programm, DEP) im DEP-Profil für iOS- und Mac-Geräte konfigurieren:
- **Touch ID**
- **Zoom**
- **Siri**

Wenn dieser Dienst aktiviert ist, zeigt der Setup-Assistent von Apple während der Geräteaktivierung eine Eingabeaufforderung dafür an.

## <a name="integration-with-upgrade-analytics"></a>Integration mit Upgrade Analytics

Mit Upgrade Analytics können Sie die Gerätebereitschaft und -kompatibilität mit Windows 10 bewerten und analysieren, um einfachere und reibungslose Upgrades zu ermöglichen. Durch die Integration von Upgrade Analytics in Configuration Manager können Sie auf die Upgradekompatibilitätsdaten in der Administratorkonsole von Configuration Manager zugreifen und anschließend über die Geräteliste Geräte für ein Upgrade oder eine Wiederherstellung auswählen.


## <a name="native-connection-types-for-windows-10-vpn-hybrid-profiles"></a>Native Verbindungstypen für hybride Windows 10-VPN-Profile

Bei Verwendung von Configuration Manager mit Intune können Sie jetzt Windows 10-VPN-Profile mit Microsoft Automatic-, IKEv2-, PPTP- und L2TP-Verbindungstypen in der Configuration Manager-Konsole erstellen, ohne OMA-URI zu verwenden.

## <a name="enhancements-to-windows-store-for-business-integration-with-configuration-manager"></a>Verbesserungen der Integration von Windows Store für Unternehmen in Configuration Manager

Wir haben in diesem Release die [Integration von Windows Store für Unternehmen](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md) mit diesen neuen Features aktualisiert:

**Update:** Im aktuellen Technical Preview-Release funktioniert das Feature für die sofortige Synchronisierung nicht.

- Bisher konnten nur kostenlose Apps aus dem Windows Store für Unternehmen bereitgestellt werden. Configuration Manager unterstützt darüber hinaus jetzt die Bereitstellung von kostenpflichtigen online-lizenzierten Apps (nur für Geräte, die bei Intune registriert sind).
- Sie können nun eine sofortige Synchronisierung zwischen Windows Store für Unternehmen und Configuration Manager einleiten.
- Sie können jetzt den geheimen Clientschlüssel ändern, den Sie von Azure Active Directory erhalten haben.

### <a name="try-it-out"></a>Probieren Sie es aus!

#### <a name="purchase-and-sync-a-paid-online-licensed-app"></a>Erwerben und Synchronisieren einer kostenpflichtigen online-lizenzierten App

1. Kaufen Sie eine kostenpflichtige online-lizenzierte App aus dem Windows Store für Unternehmen.
2. Klicken Sie im Arbeitsbereich **Verwaltung** der Configuration Manager-Konsole auf **Clouddienste** > **Updates und Wartung** > **Windows Store für Unternehmen**.
3. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Synchronisieren** auf **Jetzt synchronisieren**.
4. Kurz darauf wird die App, die Sie erworben haben, im Knoten **Lizenzinformationen für Store-Apps** des Arbeitsbereichs **Anwendungsverwaltung** angezeigt.

#### <a name="create-and-deploy-a-configuration-manager-application-from-the-synchronized-app-data"></a>Erstellen und Bereitstellen einer Configuration Manager-Anwendung aus den synchronisierten App-Daten

Das Verfahren zum Erstellen und Bereitstellen einer Configuration Manager-Anwendung aus einer kostenpflichtigen Store-App ist das gleiche wie das zum Erstellen einer Anwendung aus einer kostenlosen App. Weitere Informationen finden Sie im Abschnitt **Erstellen und Bereitstellen der App** in [Verwalten von Apps aus dem Microsoft Store für Unternehmen und Bildungseinrichtungen mit Configuration Manager](../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md).


#### <a name="modify-the-client-secret-key-from-azure-active-directory"></a>Ändern des geheimen Clientschlüssels aus Azure Active Directory

1. Klicken Sie im Arbeitsbereich **Verwaltung** der Configuration Manager-Konsole auf **Clouddienste** > **Updates und Wartung** > **Windows Store für Unternehmen**.
2. Wählen Sie Ihr Windows Store für Unternehmen-Konto aus, und klicken Sie anschließend auf **Eigenschaften**.
3. Geben Sie im Dialogfeld **Windows Store for Business Account Properties** (Windows Store für Unternehmen-Kontoeigenschaften) einen neuen Schlüssel in das Feld **Geheimer Clientschlüssel** ein, und klicken Sie anschließend auf **Überprüfen**. Sobald die Überprüfung abgeschlossen ist, klicken Sie auf **Übernehmen**, und schließen Sie dann das Dialogfeld.


## <a name="new-compliance-settings-for-configuration-items"></a>Neue Kompatibilitätseinstellungen für Konfigurationselemente

Wir haben viele neue Einstellungen hinzugefügt, die Sie in Ihren Konfigurationselementen für verschiedene Geräteplattformen verwenden können.
Dabei handelt es sich um Einstellungen, die zuvor in Microsoft Intune in einer eigenständigen Konfiguration vorhanden waren, und jetzt verfügbar sind, wenn Sie Intune mit Configuration Manager verwenden.
Wenn Sie Hilfe zu einer dieser Einstellung benötigen, öffnen Sie [Verwalten von Einstellungen und Features auf Ihren Geräten mit Microsoft Intune-Richtlinien](../../../intune/configuration/device-profiles.md), und wählen Sie dann das untergeordnete Thema zu den Einstellungen für die gewünschte Plattform aus.


### <a name="new-settings-for-android-devices"></a>Neue Einstellungen für Android-Geräte

#### <a name="password-settings"></a>Kennworteinstellungen

- **Kennwortverlauf speichern**
- **Fingerabdruckentsperrung zulassen**

#### <a name="security-settings"></a>Sicherheitseinstellungen

- **Verschlüsselung auf Speicherkarten vorschreiben**
- **Bildschirmaufnahme zulassen**
- **Übermitteln von Diagnosedaten zulassen**

#### <a name="browser-settings"></a>Browsereinstellungen

- **Webbrowser zulassen**
- **AutoAusfüllen zulassen**
- **Popupblocker zulassen**
- **Cookies zulassen**
- **Active Scripting zulassen**

#### <a name="app-settings"></a>App-Einstellungen

- **Google Play Store zulassen**

#### <a name="device-capability-settings"></a>Gerätefunktionseinstellungen

- **Wechselspeichermedien zulassen**
- **WLAN-Tethering zulassen**
- **Geolocation zulassen**
- **NFC zulassen**
- **Bluetooth zulassen**
- **Sprachroaming zulassen**
- **Datenroaming zulassen**
- **SMS/MMS-Messaging zulassen**
- **Sprach-Assistent zulassen**
- **Sprachwahl zulassen**
- **Kopieren und Einfügen zulassen**


### <a name="new-settings-for-ios-devices"></a>Neue Einstellungen für iOS-Geräte

#### <a name="password-settings"></a>Kennworteinstellungen

- **Erforderliche Anzahl komplexer Zeichen im Kennwort**
- **Einfache Kennwörter zulassen**
- **Minuten Inaktivität vor Anforderung des Kennworts**
- **Kennwortverlauf speichern**

### <a name="new-settings-for-mac-os-x-devices"></a>Neue Einstellungen für Mac OS X-Geräte

#### <a name="password-settings"></a>Kennworteinstellungen

- **Erforderliche Anzahl komplexer Zeichen im Kennwort**
- **Einfache Kennwörter zulassen**
- **Kennwortverlauf speichern**
- **Minuten Inaktivität bis zur Aktivierung des Bildschirmschoners**

### <a name="new-settings-for-windows-10-desktop-and-mobile-devices"></a>Neue Einstellungen für Windows 10 Desktop und mobile Geräte

#### <a name="password-settings"></a>Kennworteinstellungen

- **Minimale Anzahl von Zeichensätzen**
- **Kennwortverlauf speichern**
- **Kennworteingabe verlangen, wenn das Gerät aus dem Leerlauf zurückkehrt**

#### <a name="security-settings"></a>Sicherheitseinstellungen

- **Verschlüsselung auf mobilen Geräten vorschreiben**
- **Manuelle Aufhebung der Registrierung zulassen**

#### <a name="device-capability-settings"></a>Gerätefunktionseinstellungen

- **VPN über Mobilfunk zulassen**
- **VPN-Roaming über Mobilfunk zulassen**
- **Handyzurücksetzung zulassen**
- **USB-Verbindung zulassen**
- **Cortana zulassen**
- **Info-Center-Benachrichtigungen zulassen**

### <a name="new-settings-for-windows-10-team-devices"></a>Neue Einstellungen für Windows 10 Team-Geräte

#### <a name="device-settings"></a>Geräteeinstellungen

- **Azure Operational Insights aktivieren**
- **Miracast-Funkprojektion aktivieren**
- **Im Willkommensbildschirm angezeigte Besprechungsinformationen auswählen**
- **URL zum Bild für den Sperrbildschirmhintergrund**


### <a name="new-settings-for-windows-81-devices"></a>Neue Einstellungen für Windows 8.1-Geräte

#### <a name="applicability-settings"></a>Anwendbarkeitseinstellungen

- **Alle Konfigurationen auf Windows 10 anwenden**

#### <a name="password-settings"></a>Kennworteinstellungen

- **Erforderlicher Kennworttyp**
- **Minimale Anzahl von Zeichensätzen**
- **Minimale Kennwortlänge**
- **Anzahl der zulässigen wiederholten Anmeldefehler, bevor die Gerätedaten zurückgesetzt werden**
- **Inaktivität in Minuten bis zur Abschaltung des Bildschirms**
- **Kennwortablauf (Tage)**
- **Kennwortverlauf speichern**
- **Wiederverwendung vorheriger Kennwörter verhindern**
- **Bildkennwort und PIN zulassen**

#### <a name="browser-settings"></a>Browsereinstellungen

- **Automatische Erkennung des Intranets zulassen**


### <a name="new-settings-for-windows-phone-81-devices"></a>Neue Einstellungen für Windows Phone 8.1-Geräte

#### <a name="applicability-settings"></a>Anwendbarkeitseinstellungen

- **Alle Konfigurationen auf Windows 10 anwenden**

#### <a name="password-settings"></a>Kennworteinstellungen

- **Minimale Anzahl von Zeichensätzen**
- **Einfache Kennwörter zulassen**
- **Kennwortverlauf speichern**

#### <a name="device-capability-settings"></a>Gerätefunktionseinstellungen

- **Automatische Verbindung mit freien WLAN-Hotspots zulassen**


## <a name="improvements-for-boundary-groups"></a>Verbesserungen für Begrenzungsgruppen
Diese Preview umfasst wichtige Änderungen an Begrenzungsgruppen und deren Zusammenarbeit mit Verteilungspunkten. Diese Änderungen helfen bei der Vereinfachung des Entwurfs Ihrer Inhaltsinfrastruktur, wobei Sie mehr Kontrolle darüber erhalten, wie und wann ein Fallback der Clients erfolgt, um zusätzliche Verteilungspunkte als Quellspeicherorte für Inhalt zu suchen. Dies schließt sowohl lokale als auch cloudbasierte Verteilungspunkte ein.

Diese Verbesserungen ersetzen Konzepte und Verhaltensweisen, mit denen Sie möglicherweise heute vertraut sind (wie das Konfigurieren von Verteilungspunkten, um schnell oder langsam zu sein), durch ein neues Modell, das einfacher einzurichten und zu verwalten sein sollte. Diese Änderungen stellen auch die Grundlage für zukünftige Änderungen dar, die andere Standortsystemrollen verbessern, die Sie Begrenzungsgruppen zuordnen.  

Während des Upgrades auf 1609 konvertiert das Upgrade Ihre aktuellen Begrenzungsgruppenkonfigurationen so, dass sie an das neue Modell angepasst sind, damit diese Änderungen Ihre Inhaltsverteilungskonfigurationen nicht stören (weitere Informationen finden Sie im Abschnitt [Update existing boundary groups to the new model (Aktualisieren vorhandener Begrenzungsgruppen auf das neue Modell)](capabilities-in-technical-preview-1609.md#bkmk_update)).

Die folgenden Abschnitte enthalten eine Beschreibung der Änderungen, die diese Preview umfasst, der Funktionsweise des Modells sowie dessen, was Sie erwarten können, wenn Sie einen Standort upgraden, für den bereits Begrenzungsgruppen konfiguriert wurden.



### <a name="changes-in-ui-and-behavior-for-boundary-groups-and-content-locations"></a>Änderungen an der Benutzeroberfläche und dem Verhalten für Begrenzungsgruppen und Speicherorte für Inhalt
Beim Folgenden handelt es sich um wichtige Änderungen an Begrenzungsgruppen und daran, wie Clients Inhalt suchen. Viele dieser Änderungen und Konzepte arbeiten zusammen.
- **Konfigurationen für „Schnell“ und „Langsam“ wurden entfernt:** Sie konfigurieren einzelne Verteilungspunkte nicht mehr so, dass diese schnell oder langsam sind.  Stattdessen wird jedes Standortsystem, das einer Begrenzungsgruppe zugeordnet ist, auf die gleiche Weise behandelt. Aufgrund dieser Änderung unterstützt die Registerkarte **Referenz** der Begrenzungsgruppeneigenschaften die Konfiguration von „schnell“ und „langsam“ nicht mehr.
- **Neue Standardbegrenzungsgruppe an jedem Standort:**  Jeder primäre Standort verfügt über eine neue Standardbegrenzungsgruppe mit dem Namen ***Default-Site-Boundary-Group\<sitecode>***.  Wenn sich ein Client nicht an einem Netzwerkstandort befindet, der einer Begrenzungsgruppe zugewiesen ist, verwendet dieser Client die Standortsysteme, die der Standardgruppe seines zugewiesenen Standorts zugeordnet sind. Planen Sie, diese Begrenzungsgruppe als Ersatz für das Konzept der Fallbackinhaltsquelle zu verwenden.    
  -  **Fallbackquellpfade für Inhalt zulassen** wird entfernt: Sie konfigurieren für das Fallback nicht mehr explizit einen Verteilungspunkt, und die entsprechenden Optionen wurden von der Benutzeroberfläche entfernt.

  Darüber hinaus hat sich das Ergebnis geändert, das auftritt, wenn die Einstellung **Die Verwendung eines Fallbackquellpfads für den Inhalt durch Clients zulassen** auf einem Bereitstellungstyp für Anwendungen festgelegt wird. Diese Einstellung auf einem Bereitstellungstyp ermöglicht es einem Client nun, die Standard-Standortbegrenzungsgruppe als Quellspeicherort für Inhalt zu verwenden.

  -  **Beziehungen von Begrenzungsgruppen:** Jede Begrenzungsgruppe kann mit mindestens einer weiteren Begrenzungsgruppe verknüpft werden. Diese Links bilden Beziehungen, die auf der neuen Registerkarte der Begrenzungsgruppeneigenschaften mit dem Namen **Beziehungen** konfiguriert sind:
  -   Jede Begrenzungsgruppe, der ein Client direkt zugewiesen ist, wird **aktuelle** Begrenzungsgruppe genannt.  
  -   Jede Begrenzungsgruppe, die ein Client aufgrund einer Zuweisung zwischen der *aktuellen* Begrenzungsgruppe des Clients und einer anderen Gruppe verwenden kann, wird als **benachbarte** Begrenzungsgruppe bezeichnet.
  -  Auf der Registerkarte **Beziehungen** können Sie Begrenzungsgruppen hinzufügen, die als *Nachbarbegrenzungsgruppe* verwendet werden können. Sie können auch eine Zeit in Minuten konfigurieren, die bestimmt, wann ein Client, der keinen Inhalt von einem Verteilungspunkt in der *aktuellen* Gruppe findet, beginnt, Speicherorte für Inhalt von diesen *Nachbarbegrenzungsgruppen* zu suchen.

      Beim Hinzufügen oder Ändern einer Begrenzungsgruppenkonfiguration verfügen Sie über die Option, das Fallback auf diese bestimmte Begrenzungsgruppe von der aktuellen Gruppe zu blockieren, die Sie konfigurieren.

  Um die neue Konfiguration zu verwenden, definieren Sie explizite Zuordnungen (Links) von einer Begrenzungsgruppe zu einer anderen, und konfigurieren Sie alle Verteilungspunkte in dieser zugeordneten Gruppe mit der gleichen Zeit in Minuten. Die Zeit, die Sie konfigurieren, bestimmt, wann ein Client, der keine Inhaltsquelle von seiner *aktuellen* Begrenzungsgruppe findet, beginnt, Inhaltsquellen von dieser Nachbarbegrenzungsgruppe zu suchen.

  Zusätzlich zu Begrenzungsgruppen, die Sie explizit konfigurieren, verfügt jede Begrenzungsgruppe über einen implizierten Link zur Standard-Standortbegrenzungsgruppe. Dieser Link wird nach 120 Minuten aktiv, wenn die Standard-Standortbegrenzungsgruppe zu einer Nachbarbegrenzungsgruppe wird, was den Clients ermöglicht, die Verteilungspunkte zu verwenden, die dieser Begrenzungsgruppe als Quellspeicherort für Inhalt zugeordnet sind.

  Dieses Verhalten ersetzt, was zuvor als Fallback für den Inhalt bezeichnet wurde.  Sie können dieses Standardverhalten von 120 Minuten außer Kraft setzen, indem Sie die Standardbegrenzungsgruppe einer *aktuellen* Gruppe zuordnen und eine bestimmte Zeit in Minuten festlegen oder das Fallback vollständig blockieren, um dessen Verwendung zu verhindern.


- **Clients versuchen bis zu zwei Minuten lang, Inhalte aus den einzelnen Verteilungspunkten abzurufen:** Wenn ein Client nach einem Quellspeicherort für Inhalt sucht, versucht er zwei Minuten lang auf jeden Verteilungspunkt zuzugreifen, bevor er anschließend einen anderen Verteilungspunkt ausprobiert. Dabei handelt es sich um eine Änderung gegenüber früheren Versionen, bei denen Clients bis zu 2 Stunden lang versucht haben, eine Verbindung zu einem Verteilungspunkt herzustellen.

  - Der erste Verteilungspunkt, den ein Client versucht zu verwenden, wird zufällig aus dem Pool verfügbarer Verteilungspunkte in der *aktuellen* Begrenzungsgruppe (bzw. den aktuellen Begrenzungsgruppen) des Clients ausgewählt.

  - Wenn der Client den Inhalt nach zwei Minuten nicht gefunden hat, wechselt er zu einem neuen Verteilungspunkt und versucht, Inhalt von diesem Server zu erhalten. Dieser Vorgang wird alle zwei Minuten wiederholt, bis der Client den Inhalt findet oder den letzten Server im Pool erreicht.

  - Wenn ein Client in seinem *aktuellen* Pool keinen gültigen Quellspeicherort für Inhalt findet, bevor der Zeitraum für ein Fallback auf eine *Nachbarbegrenzungsgruppe* erreicht ist, fügt der Client die Verteilungspunkte aus dieser *Nachbarbegrenzungsgruppe* zum Ende seiner aktuellen Liste hinzu und durchsucht anschließend die erweiterte Gruppe von Quellspeicherorten, die die Verteilungspunkte aus beiden Begrenzungsgruppen umfasst.

      > [!TIP]  
      > Wenn Sie einen expliziten Link von der aktuellen Begrenzungsgruppe zu der Standard-Standortbegrenzungsgruppe erstellen und eine Fallbackzeit festlegen, die kürzer ist als die Fallbackzeit für einen Link zu einer Nachbarbegrenzungsgruppe, beginnen Clients, Quellspeicherorte aus der Standard-Standortbegrenzungsgruppe zu durchsuchen, bevor sie die Nachbargruppe einschließen.

  - Wenn der Client vom letzten Server im Pool keinen Inhalt abrufen kann, beginnt er den Prozess erneut.


### <a name="how-the-new-model-works"></a>So funktioniert das neue Modell
Wenn Sie Begrenzungsgruppen konfigurieren, ordnen Sie der Begrenzungsgruppe Grenzen (Netzwerkspeicherorte) und Standortsystemrollen wie Verteilungspunkte zu. Dadurch können Clients mit Standortsystemservern wie Verteilungspunkten verknüpft werden, die sich in der Nähe der Clients auf dem Netzwerk befinden.   
- Sie können die gleiche Grenze mehreren Begrenzungsgruppen zuweisen.
- Standortsystemserver wie Verteilungspunkte können mehreren Begrenzungsgruppen zugeordnet und damit für eine größere Anzahl von Netzwerkspeicherorten verfügbar gemacht werden.
- Wenn ein Verteilungspunkt keiner Begrenzungsgruppe zugeordnet ist, können Clients diesen Verteilungspunkt nicht als Quellspeicherort für Inhalt verwenden.

Ab dieser Technical Preview definieren Sie die Begrenzungsgruppenbeziehungen, um das Fallbackverhalten für die Quellspeicherorte für Inhalt zu konfigurieren. Dieses neue Verhalten wird auf der neuen Registerkarte **Beziehungen** der Begrenzungsgruppeneigenschaften konfiguriert und ersetzt das Konfigurieren von Standortsystemen, damit diese schnell oder langsam sind, sowie das Konfigurieren einer Begrenzungsgruppe, um das Fallback für den Quellspeicherort für Inhalt zuzulassen.

Fügen Sie auf der Registerkarte „Beziehungen“ andere Begrenzungsgruppen hinzu, um eine Beziehung zu diesen Gruppen zu konfigurieren. Jede Beziehung ist ein unidirektionaler Link von der **aktuellen** Begrenzungsgruppe zu der Begrenzungsgruppe, die Sie hinzufügen und die als **Nachbar** bezeichnet wird. Für jeden Link, den Sie erstellen, können Sie Verteilungspunkte mit einer Fallbackzeit in Minuten konfigurieren. Dadurch wird bestimmt, nach welcher Zeit Clients in der *aktuellen* Begrenzungsgruppe beginnen können, Verteilungspunkte in der *Nachbarbegrenzungsgruppe* zu verwenden, wenn sie in Ihrer aktuellen Begrenzungsgruppe keinen gültigen Quellspeicherort für Inhalt finden können.

Wenn ein Client keinen Inhalt findet und beginnt, Speicherorte in benachbarten Begrenzungsgruppen zu durchsuchen, wird der Pool verfügbarer Verteilungspunkte für diesen Client kontrolliert vergrößert.  

- Eine Begrenzungsgruppe kann mehr als eine Beziehung haben. Dadurch können Sie Fallbacks auf verschiedene Nachbarn konfigurieren, die nach Ablauf verschiedener Zeiten eintreten.
- Der Fallback der Clients erfolgt nur auf eine Begrenzungsgruppe, die ein direkter Nachbar ihrer aktuellen Begrenzungsgruppe ist.
- Wenn ein Client Mitglied mehrerer Begrenzungsgruppen ist, wird die aktuelle Begrenzungsgruppe als die Gesamtheit aller Begrenzungsgruppen dieses Clients definiert.  Anschließend kann ein Fallback dieses Clients auf einen Nachbar einer beliebigen dieser ursprünglichen Begrenzungsgruppen erfolgen.

Zusätzlich zu den Links, die Sie definieren, wird zwischen den Begrenzungsgruppen, die Sie erstellen, und der Standardbegrenzungsgruppe, die automatisch für jeden Standort erstellt wird, automatisch ein implizierter Link erstellt. Dieser automatische Link:
- Wird von Clients verwendet, die sich nicht in einer Begrenzungsgruppe befinden, die einer anderen Begrenzungsgruppe in Ihrer Hierarchie zugeordnet ist, und die automatisch die Standardbegrenzungsgruppe des zugewiesenen Standorts verwenden, um gültige Quellspeicherorte für Inhalt zu ermitteln.   
-  Ist eine Standardoption für ein Fallback von der aktuellen Begrenzungsgruppe auf die Standardbegrenzungsgruppe der Standorte, die nach 120 Minuten verwendet wird.

**Beispiel für die Verwendung des neuen Modells:** Sie erstellen drei Begrenzungsgruppen, die keine Grenzen oder Standortsystemserver teilen:
- Gruppe BG_A mit den Verteilungspunkten DP_A1 und DP_A2, die der Gruppe zugeordnet sind
- Gruppe BG_B mit den Verteilungspunkten DP_B1 und DP_B2, die der Gruppe zugeordnet sind
- Gruppe BG_C mit den Verteilungspunkten DP_C1 und DP_C2, die der Gruppe zugeordnet sind

Fügen Sie die Netzwerkspeicherorte Ihres Clients nur der Begrenzungsgruppe BG_A als Grenze hinzu, und konfigurieren Sie anschließend Beziehungen von dieser Begrenzungsgruppe zu den anderen beiden Begrenzungsgruppen:
- Konfigurieren Sie Verteilungspunkte für die erste *Nachbargruppe* (BG_B), die nach 10 Minuten verwendet wird. Diese Gruppe enthält die Verteilungspunkte DP_B1 und DP_B2. Beide verfügen über eine gute Verbindung mit den Grenzspeicherorten der ersten Gruppe.
- Konfigurieren Sie die zweite *Nachbargruppe* (BG_C), die nach 20 Minuten verwendet wird. Diese Gruppe enthält die Verteilungspunkte DP_C1 und DP_C2. Beide sind über ein WAN von den anderen Begrenzungsgruppen aus zugänglich.
- Fügen Sie auch einen zusätzlichen Verteilungspunkt hinzu, der sich auf dem Standortserver der Standard-Standortbegrenzungsgruppe der Standorte befindet. Dies ist der am wenigsten bevorzugte Quellspeicherort für Inhalt, der sich jedoch zu all Ihren Begrenzungsgruppen zentral befindet.

  Beispiel für Begrenzungsgruppen und Fallbackzeiten:

  ![BG_Fallback](media/BG_Fallback.png)


Mit dieser Konfiguration:
- Beginnt der Client die Suche nach Inhalt aus Verteilungspunkten in seiner *aktuellen* Begrenzungsgruppe (BG_A), wobei er jeden Verteilungspunkt 2 Minuten lang durchsucht, bevor er zum nächsten Verteilungspunkt in der Begrenzungsgruppe wechselt. Der Pool des Clients mit gültigen Quellspeicherorten für Inhalt umfasst DP_A1 und DP_A2.
- Wenn der Client 10 Minuten lang keinen Inhalt aus der *aktuellen* Begrenzungsgruppe findet, fügt er die Verteilungspunkte aus der Begrenzungsgruppe BG_B zur Suche hinzu. Anschließend setzt er die Suche nach Inhalt von einem Verteilungspunkt in seinem kombinierten Pool von Verteilungspunkten fort, der nun die Verteilungspunkte der Begrenzungsgruppen BG_A und BG_B enthält. Der Client kontaktiert weiterhin jeden Verteilungspunkt zwei Minuten lang, bevor er zum nächsten Verteilungspunkt seines Pools wechselt. Der Pool des Clients mit gültigen Quellspeicherorten für Inhalt umfasst DP_A1, DP_A2, DP_B1 und DP_B2.
- Nach weiteren 10 Minuten (insgesamt 20 Minuten), in denen der Client immer noch keinen Verteilungspunkt mit Inhalt gefunden hat, erweitert er seinen Pool mit verfügbaren Verteilungspunkten um die Verteilungspunkte der zweiten *Nachbargruppe*, also der Begrenzungsgruppe BG_C. Der Client verfügt nun über 6 Verteilungspunkte, die er durchsuchen kann (DP_A1, DP_A2, DP_B2, DP_B2, DP_C1 und DP_C2), und wechselt weiterhin alle zwei Minuten zu einem neuen Verteilungspunkt, bis er Inhalt gefunden hat.
- Wenn der Client nach maximal 120 Minuten keinen Inhalt gefunden hat, greift er darauf zurück, die *Standard-Standortbegrenzungsgruppe* als Teil der kontinuierlichen Suche einzuschließen. In den Pool mit Verteilungspunkten werden nun alle Verteilungspunkte aus den drei konfigurierten Begrenzungsgruppen sowie der letzte Verteilungspunkt eingeschlossen, der sich auf dem Standortservercomputer befindet.  Der Client setzt die Suche nach Inhalt anschließend fort und wechselt alle zwei Minuten den Verteilungspunkt, bis er Inhalt gefunden hat.

Indem Sie die verschiedenen Nachbargruppen so konfigurieren, dass diese zu verschiedenen Zeiten verfügbar sind, steuern Sie, wann bestimmte Verteilungspunkte als Quellspeicherort für Inhalt hinzugefügt werden, sowie wann bzw. ob der Client ein Fallback auf die Standard-Standortbegrenzungsgruppe als Sicherheitsnetz für Inhalt verwendet, der von einem anderen Speicherort nicht verfügbar ist.


### <a name="update-existing-boundary-groups-to-the-new-model"></a><a name="bkmk_update"></a>Aktualisieren vorhandener Begrenzungsgruppen auf das neue Modell
Wenn Sie die Version 1609 installieren und Ihren Standort aktualisieren, werden die folgenden Konfigurationen automatisch vorgenommen. Diese sollen sicherstellen, dass Ihr aktuelles Fallbackverhalten verfügbar bleibt, bis Sie neue Begrenzungsgruppen und Beziehungen konfigurieren.  
- Ungeschützte Verteilungspunkte an einem Standort werden zur Begrenzungsgruppe *Default-Site-Boundary-Group\<sitecode>* dieses Standorts hinzugefügt.
- Von jeder vorhandenen Begrenzungsgruppe, die einen Standortserver umfasst, der mit einer langsamen Verbindung konfiguriert wurde, wird eine Kopie erstellt. Der Name der neuen Gruppe ist ***\<original boundary group name>-Slow-Tmp***:  
  -   Standortsysteme, die über eine schnelle Verbindung verfügen, bleiben in der ursprünglichen Begrenzungsgruppe.
  -   Eine Kopie der Standortsysteme, die über eine langsame Verbindung verfügen, wird der Kopie der Begrenzungsgruppe hinzugefügt. Die ursprünglichen Standortsysteme, die als langsam konfiguriert wurden, bleiben zur Abwärtskompatibilität in der ursprünglichen Begrenzungsgruppe, werden von dieser Begrenzungsgruppe jedoch nicht verwendet.
  -   Dieser Begrenzungsgruppenkopie sind keine Grenzen zugeordnet. Jedoch wird ein Fallbacklink zwischen der ursprünglichen Gruppe und der neuen Begrenzungsgruppe erstellt, deren Fallbackzeit auf 0 festgelegt ist.

  Die folgende Tabelle ermittelt das neue Fallbackverhalten, das Sie von der Kombination aus den ursprünglichen Bereitstellungseinstellungen und den Verteilungspunktkonfigurationen erwarten können:

Ursprüngliche Bereitstellungskonfiguration für „Programm nicht ausführen“ im langsamen Netzwerk  |Ursprüngliche Verteilungspunktkonfiguration für „Zulassen, dass der Client einen Fallbackquellpfad für Inhalt verwendet“  |Neues Fallbackverhalten  
---------|---------|---------
Ausgewählt     |  Ausgewählt    |  **Kein Fallback** – Verwenden Sie nur die Verteilungspunkte in der aktuellen Begrenzungsgruppe.       
Ausgewählt     |  Nicht ausgewählt|  **Kein Fallback** – Verwenden Sie nur die Verteilungspunkte in der aktuellen Begrenzungsgruppe.       
Nicht ausgewählt |  Nicht ausgewählt|  **Fallback auf Nachbar** – Verwenden Sie die Verteilungspunkte in der aktuellen Begrenzungsgruppe, und fügen Sie anschließend die Verteilungspunkte aus der Nachbarbegrenzungsgruppe hinzu. Sofern kein expliziter Link zur Standard-Standortbegrenzungsgruppe konfiguriert wurde, erfolgt kein Fallback der Clients auf diese Gruppe.    
Nicht ausgewählt | Ausgewählt |   **Normales Fallback** – Verwenden Sie die Verteilungspunkte in der aktuellen Begrenzungsgruppe und anschließend die der Nachbar- und der Standard-Standortbegrenzungsgruppen.

 Alle anderen Bereitstellungskonfigurationen führen zum **Normalen Fallback**.  



## <a name="office-365-client-management-dashboard"></a>Office 365-Clientverwaltungsdashboard  
Configuration Manager 1609 Technical Preview enthält ein neues Dashboard. Wechseln Sie in der Configuration Manager-Konsole zu **Softwarebibliothek** > **Übersicht** > **Office 365-Clientverwaltung**, um das Dashboard anzuzeigen.
>[!NOTE]
>Im Arbeitsbereich **Neuigkeiten** in der Configuration Manager-Konsole trägt das Dashboard den falschen Namen **Office 365-Verwaltungsdashboard**.

Das Dashboard zeigt Diagramme für Folgendes an:

- Anzahl der Office 365-Clients
- Office 365-Clientversionen
- Office 365-Clientsprachen
- Office 365-Clientkanäle     
Weitere Informationen finden Sie unter [Übersicht über die Updatekanäle für Microsoft 365-Apps](https://docs.microsoft.com/deployoffice/overview-update-channels).
- Regeln zur automatischen Bereitstellung, die Office 365-Client in der Gruppe verfügbarer Produkte ausgewählt haben.

Über das Dashboard können Sie die folgenden Aktionen ausführen:
- Verwenden Sie am oberen Rand des Dashboards die Dropdowneinstellung **Sammlung**, um die Dashboarddaten nach Mitgliedern einer bestimmten Sammlung zu filtern.
- Klicken Sie oben rechts im Dashboard auf **Office 365-Installer**, um den Office 365-Installationsassistenten zu starten, um Microsoft 365-Apps für Clients bereitzustellen. Weitere Informationen finden Sie unter [Bereitstellen von Microsoft 365-Apps für Clients](#deploy-microsoft-365-apps-to-clients).
- Klicken Sie rechts von der Mitte im Dashboard auf **Create an ADR** (Erstellen einer ADR), um den Assistent zum Erstellen automatischer Bereitstellungsregeln zu öffnen, um eine neue automatische Bereitstellungsregel (automatic deployment rule, ADR) zu erstellen. Wählen Sie zum Erstellen einer ADR für Microsoft 365-Apps bei der Auswahl des Produkts **Office 365-Client** aus. Weitere Informationen finden Sie unter [Automatically deploy software updates (Automatisches Bereitstellen von Softwareupdates)](../../sum/deploy-use/automatically-deploy-software-updates.md).
- Klicken Sie auf der unteren rechten Seite des Dashboards auf **Create Client Agent Settings** (Client-Agent-Einstellungen erstellen), um die Client-Agent-Einstellungen zu öffnen. Weitere Informationen finden Sie unter [About client settings (Informationen zu Clienteinstellungen)](../clients/deploy/about-client-settings.md).



Weitere Informationen zu Microsoft 365 Apps for Enterprise-Updates finden Sie unter [Verwalten von Microsoft 365-Apps-Updates mit Configuration Manager](../../sum/deploy-use/manage-office-365-proplus-updates.md).

## <a name="deploy-microsoft-365-apps-to-clients"></a>Bereitstellen von Microsoft 365-Apps für Clients
In diesem Release können Sie vom Office 365-Clientverwaltungsdashboard aus den Office 365-Installer starten, mit dem Sie Microsoft 365-Installationseinstellungen konfigurieren, Dateien aus Office Content Delivery Networks (CDNs) herunterladen und die Dateien als Anwendung in Configuration Manager bereitstellen können.

### <a name="limitations-of-microsoft-365-deployment"></a>Einschränkungen bei Microsoft 365-Bereitstellungen
- Möglicherweise haben Sie Probleme beim Versuch, vorhandene Clienteinstellungen (XML) in den Office 365-App-Installationsassistenten zu importieren. Sie können die Clienteinstellungen ohne Probleme manuell konfigurieren.

#### <a name="to-deploy-microsoft-365-apps-to-clients"></a>Bereitstellen von Microsoft 365-Apps für Clients
1. Navigieren Sie in der Configuration Manager-Konsole zu **Softwarebibliothek** > **Übersicht** > **Office 365-Clientverwaltung**.
2. Klicken Sie im oberen rechten Bereich auf **Office 365-Installer**. Der Office 365-Installations-Assistent wird geöffnet.
3. Geben Sie auf der Seite **Anwendungseinstellungen** einen Namen und eine Beschreibung für die App an, geben Sie den Downloadpfad für die Dateien ein, und klicken Sie anschließend auf **Weiter**. Beachten Sie, dass der Pfad im folgenden Format angegeben sein muss: &#92;&#92;*Server*&#92;*Freigabe*.
4. Wählen Sie auf der Seite **Clienteinstellungen importieren** aus, ob Sie die Microsoft 365-Clienteinstellungen aus einer vorhandenen XML-Konfigurationsdatei importieren oder die Einstellungen manuell angeben möchten, und klicken Sie anschließend auf **Weiter**.
Wenn Sie über eine vorhandene Konfigurationsdatei verfügen, geben Sie den Speicherort für die Datei an, und fahren Sie mit Schritt 7 fort. Beachten Sie, dass der Speicherort im folgenden Format angegeben werden muss: &#92;&#92;*Server*&#92;*Freigabe*&#92;*Dateiname*.XML.

    > [!IMPORTANT]
    >Möglicherweise haben Sie Probleme beim Versuch, vorhandene Clienteinstellungen (XML) in diese Technical Preview zu importieren.

5. Wählen Sie auf der Seite **Clientprodukte** die Microsoft 365-Suite aus, die Sie verwenden, wählen Sie die Anwendungen aus, die Sie einschließen möchten, wählen Sie etwaige zusätzliche Office-Produkte aus, die enthalten sein sollen, und klicken Sie anschließend auf **Weiter**.
6. Wählen Sie auf der Seite **Clienteinstellungen** die einzuschließenden Einstellungen aus, und klicken Sie anschließend auf **Weiter**.
7. Wählen Sie auf der Seite **Bereitstellung** aus, ob die Anwendung bereitgestellt werden soll, und klicken Sie anschließend auf **Weiter**.
Wenn Sie auswählen, das Paket nicht im Assistenten bereitzustellen, fahren Sie mit Schritt 9 fort.
8. Konfigurieren Sie die restlichen Seiten des Assistenten, wie Sie dies bei einer normalen Anwendungsbereitstellung tun würden. Weitere Informationen finden Sie unter [Create and deploy an application with System Center Configuration Manager (Erstellen und Bereitstellen einer Anwendung mit System Center Configuration Manager)](../../apps/get-started/create-and-deploy-an-application.md).
9. Schließen Sie den Assistenten ab.
10. Sie können die Anwendung über **Softwarebibliothek** > **Übersicht** > **Anwendungsverwaltung** > **Anwendungen** genauso bereitstellen und ändern, wie Sie dies bei jeder anderen Anwendung in Configuration Manager tun würden.

>[!NOTE]
>Nach der Bereitstellung von Microsoft 365-Apps können Sie Regeln zur automatischen Bereitstellung erstellen, um die Apps zu verwalten. Klicken Sie zum Erstellen einer ADR für Microsoft 365-Apps bei der Auswahl des Produkts auf **ADR erstellen** und anschließend auf **Office 365-Client**. Weitere Informationen finden Sie unter [Automatically deploy software updates (Automatisches Bereitstellen von Softwareupdates)](../../sum/deploy-use/automatically-deploy-software-updates.md).

## <a name="improvements-for-bios-to-uefi-conversion"></a><a name="BKMK_UEFIConversion"></a>Verbesserungen für die Konvertierung von BIOS zu UEFI
Sie können eine Tasksequenz einer Betriebssystembereitstellung nun mit einer neuen Variable (TSUEFIDrive) so anpassen, dass durch den Schritt „Computer neu starten“ auf der Festplatte eine FAT32-Partition für den Übergang zu UEFI vorbereitet wird. Das folgende Verfahren stellt ein Beispiel dar, wie Sie Tasksequenzschritte erstellen können, um die Festplatte auf die Konvertierung von BIOS zu UEFI vorzubereiten.

#### <a name="to-prepare-the-fat32-partition-for-the-conversion-to-uefi"></a>So bereiten Sie die FAT32-Partition für die Konvertierung zu UEFI vor:
Fügen Sie in einer vorhandenen Tasksequenz zum Installieren eines Betriebssystems eine neue Gruppe mit Schritten zum Konvertieren von BIOS zu UEFI hinzu.

1. Erstellen Sie eine neue Tasksequenzgruppe nach den Schritten zum Erfassen von Dateien und Einstellungen und vor den Schritten zum Installieren des Betriebssystems. Erstellen Sie z.B. eine Gruppe nach der Gruppe **Dateien und Einstellungen erfassen** namens **BIOS zu UEFI**.
2. Fügen Sie auf der Registerkarte **Optionen** der neuen Gruppe eine neue Tasksequenzvariable als Bedingung hinzu, wobei **_SMSTSBootUEFI** **ungleich** **TRUE** ist. Dadurch wird verhindert, dass die Schritte in der Gruppe ausgeführt werden, wenn sich ein Computer bereits im UEFI-Modus befindet.
![Gruppe „BIOS zu UEFI“](media/BIOS-to-UEFI-group.png)
3. Fügen Sie der neuen Gruppe den Tasksequenzschritt **Computer neu starten** hinzu. Wählen Sie unter **Geben Sie an, was nach dem Neustart ausgeführt werden soll** **The boot image assigned to this task sequence is selected** (Das dieser Tasksequenz zugewiesene Startimage wird ausgewählt) aus, um den Computer in Windows PE zu starten.  
4. Fügen Sie auf der Registerkarte **Optionen** eine Tasksequenzvariable als Bedingung hinzu, wobei **_SMSTSInWinPE ist gleich FALSE**. Dadurch wird verhindert, dass dieser Schritt ausgeführt, wenn sich der Computer bereits in Windows PE befindet.

    ![Schritt „Computer neu starten“](media/Restart-in-Windows-PE.png)
5. Fügen Sie einen Schritt zum Starten des OEM-Tools hinzu, das die Firmware von BIOS in UEFI konvertiert. Dabei handelt es sich normalerweise um einen Tasksequenzschritt **Befehlszeile ausführen** mit einer Befehlszeile zum Starten des OEM-Tools.
5. Fügen Sie den Tasksequenzschritt „Datenträger formatieren und partitionieren“ hinzu, durch den die Festplatte formatiert und partitioniert wird. Führen Sie im Schritt Folgendes aus:
    1. Erstellen Sie die FAT32-Partition, die in UEFI konvertiert wird, bevor das Betriebssystem installiert wird. Wählen Sie **GPT** als **Datenträgertyp** aus.
    ![Schritt „Datenträger formatieren und partitionieren“](media/Format-and-partition-disk.png)
    2. Wechseln Sie zu den Eigenschaften für die FAT32-Partition. Geben Sie **TSUEFIDrive** in das Feld **Variable** ein. Wenn diese Variable von der Tasksequenz erkannt wird, wird diese sich vor dem Neustart des Computers auf den Übergang zu UEFI vorbereiten.
    ![Partitionseigenschaften](media/Partition-properties.png)
    3. Erstellen Sie eine NTFS-Partition, die von der Tasksequenz-Engine verwendet wird, um dessen Zustand sowie Protokolldateien zu speichern.
6. Fügen Sie den Tasksequenzschritt **Computer neu starten** hinzu. Wählen Sie unter **Geben Sie an, was nach dem Neustart ausgeführt werden soll** **The boot image assigned to this task sequence is selected** (Das dieser Tasksequenz zugewiesene Startimage wird ausgewählt) aus, um den Computer in Windows PE zu starten.  




## <a name="intune-compliance-charts"></a>Intune-Kompatibilitätsdiagramme
In diesem Release erhalten Sie eine schnelle Übersicht der gesamten Kompatibilität für Geräte und die häufigsten Gründe für Nichtkompatibilität, indem neue Diagramme in der Configuration Manager-Konsole im **Arbeitsbereich „Überwachung“** verwendet werden.

#### <a name="to-view-the-intune-compliance-charts"></a>So zeigen Sie Intune-Kompatibilitätsdiagramme an
1. Wechseln Sie in der Configuration Manager-Konsole zu **Überwachung** > **Übersicht** > **Kompatibilitätseinstellungen**.
2. Das Diagramm **Gesamtgerätekompatibilität** wird angezeigt.
3. Klicken Sie auf den Knoten **Kompatibilitätsrichtlinien**, um die Diagramme **Gesamtgerätekompatibilität** und **Häufigste Gründe für Nichtkompatibilität** anzuzeigen.

### <a name="limitations-of-intune-compliance-charts-in-tp-1609"></a>Einschränkungen der Intune-Kompatibilitätsdiagramme in TP 1609
- Das Anzeigen der Detailinformationen für das Diagramm **Gesamtgerätekompatibilität** erzeugt derzeit einen Fehler.
- Das Diagramm **Häufigste Gründe für Nichtkompatibilität** listet den Richtliniennamen und nicht die einzelnen Gründe für Nichtkompatibilität auf. Sie können auf die Richtlinie klicken, um einen Drilldown auszuführen und die Geräte anzuzeigen, die mit dieser Richtlinie nicht kompatibel sind.

### <a name="try-it-out"></a>Probieren Sie es aus
Schließen Sie die folgenden Abschnitte der Reihe nach ab:

#### <a name="check-overall-compliance-chart"></a>Überprüfen des Diagramms „Gesamtkompatibilität“
1. Fügen Sie zwei iOS-Kompatibilitätsrichtlinien in Configuration Manager hinzu. Eine Richtlinie sollte über eine Reihe von Einstellungen für Geräte verfügen (z.B. das Festlegen der PIN-Länge auf 6). Die andere Richtlinie sollte über eine andere Reihe von Einstellungen verfügen (z.B. die Komplexität der PIN). Die Richtlinieneinstellungen sollten sich nicht überlappen oder miteinander in Konflikt stehen.
2. Stellen Sie die zwei Richtlinien für eine Reihe von Benutzern bereit.
3. Registrieren Sie zwei iOS-Geräte in Intune mit demselben Benutzerkonto und einem Konto, das die Richtlinien im vorherigen Schritt erhalten hat. Die Geräte sollten nicht den Kriterien der Kompatibilitätsrichtlinie entsprechen.
4. Überprüfen Sie in Configuration Manager das Diagramm **Gesamtgerätekompatibilität**. Beide Geräte sollten als nicht kompatibel gemeldet werden.
<!-- 5. Click the **Non-compliant** section of the chart. Both devices should appear in the filtered view under **Assets and Compliance** > **Overview** > **Device**. -->

#### <a name="check-the-top-non-compliance-reasons-chart"></a>Überprüfen des Diagramms „Häufigste Gründe für Nichtkompatibilität“
5. Überprüfen Sie das Diagramm **Häufigste Gründe für Nichtkompatibilität**. In diesem Diagramm werden die 5 häufigsten Gründe für Nichtkompatibilität aufgeführt, wenn jedoch richtlinienübergreifend nur zwei Kompatibilitätseinstellungen festgelegt wurden, werden nur die häufigsten 2 Gründe für Nichtkompatibilität angezeigt.
6. Klicken Sie auf einen der Abschnitte im Diagramm. Beide Geräte sollten in der gefilterten Ansicht unter **Bestand und Kompatibilität** > **Übersicht** > **Gerät** angezeigt werden.

#### <a name="make-devices-compliant-and-check-the-charts"></a>Hersteller der Kompatibilität von Geräten und Überprüfen der Diagramme
7. Stellen Sie für eines der Geräte die Kompatibilität mit einer der Richtlinien her. Überprüfen Sie erneut das Diagramm **Gesamtgerätekompatibilität**. Das Diagramm sollte ein kompatibles und ein nicht kompatibles Gerät anzeigen.
8. Stellen Sie für das andere Gerät die Kompatibilität mit der gleichen Richtlinie her. Dadurch ist ein Gerät mit beiden Richtlinien und ein Gerät mit nur einer der Richtlinien kompatibel.
9. Überprüfen Sie das Diagramm **Häufigste Gründe für Nichtkompatibilität**. Es sollte nur ein Grund für Nichtkompatibilität aufgelistet sein.
<!--7. Click the **Compliant** section of the chart. Only the compliant device should appear in the filtered view. -->





## <a name="see-also"></a>Weitere Informationen
[Technical Preview für Configuration Manager](../../core/get-started/technical-preview.md)