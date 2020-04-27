---
title: Office 365-Clientverwaltungsdashboard
titleSuffix: Configuration Manager
description: Überprüfen von Office 365-Clientinformationen aus dem Office 365-Clientverwaltungsdashboard
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/21/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 69f234a2-b04b-445a-b81f-6b4acfc00eaf
ms.openlocfilehash: 7e6ed38d0f4217bfc70d3ddb196527d421e5d7c1
ms.sourcegitcommit: 2cafbba6073edca555594deb99ae29e79cd0bc79
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/24/2020
ms.locfileid: "82110388"
---
# <a name="office-365-client-management-dashboard"></a>Office 365-Clientverwaltungsdashboard

*Gilt für: Configuration Manager (Current Branch)*

> [!Note]
> Ab dem 21. April 2020 wird Office 365 ProPlus in **Microsoft 365 Apps for Enterprise** umbenannt. Weitere Informationen finden Sie unter [Namensänderung für Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). Möglicherweise finden Sie während des Updates der Konsole noch Verweise auf den alten Namen in der Configuration Manager-Konsole und der unterstützenden Dokumentation.

Ab der Configuration Manager-Version 1802 können Sie Office 365-Clientinformationen aus dem Office 365-Clientverwaltungsdashboard überprüfen. Im Office 365-Clientverwaltungsdashboard wird eine Liste von relevanten Geräten angezeigt, wenn Diagrammabschnitte ausgewählt werden. <!--1357281 -->

## <a name="prerequisites"></a>Voraussetzungen

### <a name="enable-hardware-inventory"></a>Aktivieren der Hardwareinventur

Die im Office 365-Clientverwaltungsdashboard angezeigten Daten kommen aus der Hardwareinventur. Aktivieren Sie die Hardwareinventur, und wählen Sie die Hardwareinventurklasse **Office 365 ProPlus Configurations** aus, damit Daten im Dashboard angezeigt werden.
 
1. Aktivieren Sie die Hardwareinventur, falls diese noch nicht aktiviert wurde. Weitere Informationen finden Sie unter [Konfigurieren der Hardwareinventur](../../core/clients/manage/inventory/configure-hardware-inventory.md).
2. Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** > **Clienteinstellungen** > **Clientstandardeinstellungen** aus.  
3. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  
4. Klicken Sie im Dialogfeld **Clientstandardeinstellungen** auf **Hardwareinventur**.  
5. Klicken Sie in der Liste **Geräteeinstellungen** auf **Klassen festlegen**.  
6. Im Dialogfeld der **Hardwareinventurklassen**wählen Sie **Office 365 ProPlus-Configurations** (Office 365 ProPlus-Konfigurationen) aus.  
7. Klicken Sie auf **OK** , um die Änderungen zu speichern und das Dialogfeld **Hardwareinventurklassen** zu schließen.

Das Office 365-Clientverwaltungsdashboard zeigt Daten dann an, während die Hardwareinventur ausgewertet wird.

### <a name="connectivity-for-top-level-site-server"></a>Konnektivität für Standortserver der obersten Ebene

*(In Version 1906 als Voraussetzung eingeführt)*

Der Standortserver der obersten Ebene benötigt Zugriff auf den folgenden Endpunkt, um die Bereitschaftsdatei herunterzuladen:

`https://contentstorage.osi.office.net/sccmreadinessppe/sot_sccm_addinreadiness.cab`

> [!NOTE]
> Die Clientgeräte benötigen für keines dieser Szenarios eine Internetverbindung.

### <a name="enable-data-collection-for-office-365-proplus"></a>Aktivieren der Datensammlung für Office 365 ProPlus

*(In Version 1910 als Voraussetzung eingeführt)*

Ab Version 1910 müssen Sie die Datensammlung für Office 365 ProPlus aktivieren, damit das **Office 365 ProPlus-Pilot- und -Integritätsdashboard** mit den Daten befüllt wird. Die Daten werden in der Configuration Manager-Standortdatenbank gespeichert und nicht an Microsoft gesendet.

Sie unterscheiden sich von den Diagnosedaten, die unter [Diagnosedaten, die von Office 365 ProPlus an Microsoft gesendet werden](https://docs.microsoft.com/deployoffice/privacy/overview-privacy-controls#diagnostic-data-sent-from-office-365-proplus-to-microsoft) beschrieben sind.

Sie können die Datensammlung entweder mithilfe einer Gruppenrichtlinie oder durch Bearbeiten der Registrierung aktivieren.

#### <a name="enable-data-collection-from-group-policy"></a>Aktivieren der Datensammlung über eine Gruppenrichtlinie

1. Laden Sie die neuesten [Verwaltungsvorlagendateien aus dem Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=49030) herunter.
2. Aktivieren Sie die Richtlinieneinstellung **Telemetrie-Datensammlung aktivieren** unter `User Configuration\Policies\Administrative Templates\Microsoft Office 2016\Telemetry Dashboard`.
    - Alternativ können Sie die Richtlinieneinstellung mit dem [Office-Clouddienst für Richtlinien](https://docs.microsoft.com/DeployOffice/overview-office-cloud-policy-service) anwenden.
    - Die Richtlinieneinstellung wird auch vom Office-Telemetriedashboard verwendet, das Sie für diese Datensammlung nicht bereitstellen müssen.

#### <a name="enable-data-collection-from-the-registry"></a>Aktivieren der Datensammlung über die Registrierung

Der folgende Befehl ist ein Beispiel dafür, wie Sie die Datensammlung über die Registrierung aktivieren:

```cmd
reg add HKCU\Software\Policies\Microsoft\office\16.0\OSM /v EnableLogging /t REG_DWORD /d 1
```

## <a name="viewing-the-office-365-client-management-dashboard"></a>Anzeigen des Office 365-Clientverwaltungsdashboards

Wechseln Sie in der Configuration Manager-Konsole zu **Softwarebibliothek** > **Übersicht** > **Office 365-Clientverwaltung**, um das Office 365-Clientverwaltungsdashboard anzuzeigen. Verwenden Sie am oberen Rand des Dashboards die Dropdowneinstellung **Sammlung**, um die Dashboarddaten nach Mitgliedern einer bestimmten Sammlung zu filtern. Ab der Configuration Manager-Version 1802 kann über das Office 365-Clientverwaltungsdashboard eine Liste relevanter Geräte angezeigt werden, wenn Diagrammabschnitte ausgewählt werden.

Das Office 365-Clientverwaltungsdashboard enthält Diagramme für die folgenden Informationen:

- Anzahl der Office 365-Clients
- Office 365-Clientversionen
- Office 365-Clientsprachen
- Office 365-Clientkanäle Weitere Informationen finden Sie unter [Übersicht über Updatekanäle für Office 365 ProPlus](/DeployOffice/overview-of-update-channels-for-office-365-proplus).


## <a name="integration-for-office-365-proplus-readiness"></a><a name="bkmk_o365_readiness"></a> Integration für Office 365 ProPlus-Bereitschaft
<!--3735402-->
Ab der Configuration Manager-Version 1902 können Sie über das Dashboard Geräte, die für ein Upgrade auf Office 365 ProPlus bereit sind, mit hoher Zuverlässigkeit identifizieren. Diese Integration bietet Erkenntnisse zu möglichen Kompatibilitätsproblemen mit Office-Add-Ins und -Makros in Ihrer Umgebung. Verwenden Sie den Configuration Manager anschließend zum Bereitstellen von Office auf Geräten, die dafür bereit sind.

Das Office 365-Clientverwaltungsdashboard enthält die neue Kachel **Office365 ProPlus-Upgradebereitschaft**. Diese Kachel ist ein Balkendiagramm mit Geräten in den folgenden Zuständen:
- Nicht bewertet
- Bereit für Upgrade
- Überprüfung erforderlich

Wählen Sie einen Zustand aus, um eine Geräteliste zu durchlaufen. Dieser Bereitschaftsbericht zeigt weitere Details zu Geräten an. Er enthält Spalten für den Kompatibilitätsstatus von Office-Add-Ins und -Makros.

### <a name="prerequisites-for-office-365-proplus-readiness-integration"></a>Voraussetzungen für die Integration von Office 365 ProPlus-Bereitschaft

- Aktivieren Sie die Hardwareinventur in den Clienteinstellungen. Weitere Informationen finden Sie im Abschnitt [Voraussetzungen](#prerequisites).  

- Das Gerät benötigt Konnektivität mit dem Office Content Delivery Network (CDN), um eine Add-In-Bereitschaftsdatei herunterzuladen. Weitere Informationen finden Sie unter [Netzwerke für die Inhaltsübermittlung](https://docs.microsoft.com/office365/enterprise/content-delivery-networks). Wenn das Gerät diese Datei nicht herunterladen kann, lautet der Add-In-Status *Überprüfung erforderlich*.  

    > [!Note]  
    > Für dieses Feature werden keine Daten an Microsoft gesendet.  

### <a name="detailed-macro-readiness"></a><a name="bkmk_ort"></a> Ausführliche Makrobereitschaft

Standardmäßig prüft der Überprüfungs-Agent auf jedem Gerät die Liste zuletzt verwendeter Dateien. Er zählt die Dateien in dieser Liste, die Makros unterstützen. Zu diesen Dateien zählen folgende Typen:
- Office-Dateiformate mit Makros, z.B. Excel-Arbeitsmappen mit Makros (.xlsm) oder Word-Dokumente mit Makros (.docm)  
- Ältere Office-Dateiformate, in denen nicht angegeben wird, ob Makroinhalte vorhanden sind. Beispiel: eine Arbeitsmappe in Excel 97–2003 (XLS).

Wenn Sie ausführlichere Informationen zur Makrokompatibilität benötigen, stellen Sie das **Readiness Toolkit for Office add-ins and VBA** bereit, um den Code innerhalb der Makrodateien zu analysieren. Es überprüft, ob potenziellen Kompatibilitätsprobleme vorliegen. Beispielsweise verwendet die Datei eine Funktion, die in einer neueren Version von Office geändert wurde. Nachdem Sie das Readiness Toolkit for Office add-ins and VBA ausgeführt und die Option **Most recently used Office documents and installed add-ins on this computer** (Zuletzt auf diesem Computer verwendete Office-Dokumente und installierte Add-Ins) ausgewählt oder das Flag `-mru` in der Befehlszeile verwendet haben, können die Ergebnisse vom Agent der Konfigurations-Manager-Hardwareinventur abgerufen werden. Diese zusätzlichen Daten verbessern die Berechnung der Gerätebereitschaft. Weitere Informationen finden Sie unter [Verwenden des Readiness Toolkits für Office zum Bewerten der Anwendungskompatibilität von Office 365 ProPlus](https://aka.ms/readinesstoolkit).

Beachten Sie, dass das Readiness Toolkit for Office add-ins and VBA nicht auf jedem Zielgerät installiert werden muss, um die Überprüfung auszuführen. Sie können das folgende Beispiel für eine Befehlszeilenoption verwenden, um jedes gewünschte Gerät zu überprüfen.  Das Ausgabeflag ist erforderlich. Die Dateien werden jedoch nicht dazu verwendet, die Ergebnisse im Dashboard zu generieren, sodass ein beliebiger gültiger Speicherort ausgewählt werden kann.

```cmd
ReadinessReportCreator.exe -mru -output c:\temp -silent
```

Weitere Informationen finden Sie unter [Abrufen von Bereitschaftsinformationen für mehrere Benutzer in einem Unternehmen](/deployoffice/use-the-readiness-toolkit-to-assess-application-compatibility-for-office-365-pro#getting-readiness-information-for-multiple-users-in-an-enterprise).

## <a name="office-365-proplus-upgrade-readiness-dashboard"></a><a name="bkmk_readiness-dash"></a> Office 365 ProPlus-Dashboard für die Upgradebereitschaft

*(Eingeführt in Version 1906)*

<!--4021125-->
Ab Version 1906 gibt es ein neues Bereitschaftsdashboard, mit dem Sie ermitteln können, welche Geräte für ein Upgrade auf Office 365 ProPlus bereit sind. Es enthält die Kachel **Office 365 ProPlus upgrade readiness** (Office 365 ProPlus-Upgradebereitschaft), die in der aktuellen Configuration Manager-Branchversion 1902 veröffentlicht wurde. Die folgenden neuen Kacheln auf diesem Dashboard helfen Ihnen bei der Bewertung der Bereitschaft von Office-Add-Ins und -Makros:

- Bereitstellung
- Gerätebereitschaft
- „Add-in readiness“ (Add-In-Bereitschaft)
- „Add-in support statements“ (Add-In-Unterstützungsanweisungen)
- „Top add-ins by count of version“ (Führende Add-Ins nach Versionsnummer)
- „Number of devices that have macros“ (Anzahl von Geräten mit Makros)
- „Macro readiness“ (Makrobereitschaft)
- Empfehlungen für Makros

Das folgende Video wurde auf der Ignite 2019 aufgenommen und bietet weitere Informationen:

> [!VIDEO https://medius.studios.ms/Embed/Video-nc/IG19-BRK3090]

[Best Practices die Bewertung der Kompatibilität und Microsoft Office 365 ProPlus-Upgrades mit Office Readiness in Configuration Manager](https://myignite.techcommunity.microsoft.com/sessions/79338?source=sessions)

### <a name="using-the-office-365-proplus-upgrade-readiness-dashboard"></a>Verwenden des Office 365 ProPlus-Dashboards für die Upgradebereitschaft

Nachdem Sie sichergestellt haben, dass Sie alle [Voraussetzungen](#prerequisites) erfüllt sind, verwenden Sie das Dashboard mithilfe der folgenden Anleitung:
 
1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, und erweitern Sie **Office 365-Clientverwaltung**.
1. Klicken Sie auf den Knoten **Office 365 ProPlus Upgrade Readiness** (Office 365 ProPlus-Upgradebereitschaft).
1. Ändern Sie die **Sammlung** und **Target Office Architecture** (Office-Zielarchitektur), um die an das Dashboard übertragenen Informationen zu ändern.

![Office 365 ProPlus-Dashboard für die Upgradebereitschaft](./media/4021125-office-365-upgrade-readiness-dashboard.png)

![Office 365 ProPlus-Dashboard für die Upgradebereitschaft](./media/4021125-office-365-to-add-ins.png)

![Office 365 ProPlus-Dashboard für die Upgradebereitschaft](./media/4021125-office-365-macro-advisories.png)

### <a name="device-readiness-information"></a>Informationen zur Gerätebereitschaft

Nachdem das Add-In und die Makroinventur auf jedem Gerät ausgewertet wurden, werden die Geräte entsprechend den Informationen gruppiert. Bei Geräten mit dem Status **Zum Upgrade bereit** bestehen wahrscheinlich keinerlei Kompatibilitätsprobleme.

Wenn Sie im Diagramm die Kategorie **Zum Upgrade bereit** auswählen, werden weitere Details zu den Geräten in der begrenzenden Sammlung angezeigt. Sie können die Geräteliste überprüfen, eine Auswahl gemäß Ihren Geschäftsanforderungen treffen und eine neue Gerätesammlung aus Ihrer Auswahl erstellen. Verwenden Sie die neue Sammlung, um Office 365 ProPlus mit Configuration Manager bereitzustellen.

Geräte, für die das Risiko von Kompatibilitätsproblemen besteht, werden mit dem Status **Überprüfung erforderlich** gekennzeichnet. Für diese Geräte müssen möglicherweise Maßnahmen ergriffen werden, bevor Sie sie auf Office 365 ProPlus aktualisieren. Sie sollten beispielsweise für wichtige Add-Ins ein Update auf eine neuere Version ausführen.

### <a name="add-in-information"></a>Informationen zu Add-Ins

 Auf jedem Gerät wird ein Inventar aller installierten Add-Ins erfasst. Dieses Inventar wird anschließend mit den Informationen verglichen, die Microsoft über die Leistung der Add-Ins in Office 365 ProPlus vorliegen. Wenn ein Add-in gefunden wird, das nach dem Upgrade wahrscheinlich Probleme verursacht, werden alle Geräte mit dem Add-in mit „Überprüfung erforderlich“ gekennzeichnet.

### <a name="macro-information"></a>Informationen zu Makros

Configuration Manager prüft die zuletzt verwendeten Dateien auf jedem Gerät. Das Tool zählt die Dateien in dieser Liste, die Makros unterstützen, einschließlich der folgenden Typen:

- Office-Dateiformate mit Makros
- Ältere Office-Formate, die nicht angeben, ob Makroinhalte vorhanden sind

Mit diesem Bericht kann ermittelt werden, auf welchen Geräten sich zuletzt verwendete Dateien befinden, die möglicherweise Makros enthalten. Das **Readiness Toolkit for Office add-ins and VBA** kann dann mithilfe von Configuration Manager bereitgestellt werden, um beliebige Geräte zu überprüfen, auf denen ausführlichere Informationen erforderlich sind, und zu prüfen, ob möglicherweise Kompatibilitätsprobleme vorliegen. Ein Beispiel wäre eine Datei, die eine Funktion enthält, die in einer neueren Version von Office geändert wurde.

Weitere Informationen zum Durchführen der Überprüfung finden Sie unter [Ausführliche Makrobereitschaft](#bkmk_ort).

## <a name="office-365-proplus-pilot-and-health-dashboard"></a><a name="bkmk_pilot"></a> Office 365 ProPlus-Pilot- und Integritätsdashboard
<!--4488272, 4488301-->
*(eingeführt in Version 1910)*

Ab Version 1910 können Sie mit dem **Office 365 ProPlus-Pilot- und -Integritätsdashboard** Ihre Office 365 ProPlus-Bereitstellung planen, testen und ausführen. Das Dashboard bietet Einblicke in die Integrität von Geräten mit Office 365 ProPlus, um mögliche Probleme zu identifizieren, die sich möglicherweise auf Ihre Bereitstellungspläne auswirken. Das **Office 365 ProPlus-Pilotprojekt und -Integritätsdashboard** bieten eine Empfehlung für Pilotgeräte, die auf einem Add-In-Bestand basieren. Das Dashboard verfügt über die folgenden Kacheln:

- Generieren des Pilotprojekts
- Empfohlene Pilotgeräte
- Bereitstellen des Pilotprojekts
- Geräte, die Integritätsdaten senden
- Geräte, die die Integritätsziele nicht erfüllen
- Add-Ins, die die Integritätsziele nicht erfüllen
- Makros, die die Integritätsziele nicht erfüllen

### <a name="using-the-office-365-proplus-pilot-and-health-dashboard"></a>Verwenden des Office 365 ProPlus-Pilot- und Integritätsdashboards

Nachdem Sie sichergestellt haben, dass Sie alle [Voraussetzungen](#prerequisites) erfüllt sind, verwenden Sie das Dashboard mithilfe der folgenden Anleitung:

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, und erweitern Sie **Office 365-Clientverwaltung**.
1. Wählen Sie den Knoten **Office 365 Pilot and Health** (Office 365-Pilot und -Integrität) aus.

![Office 365 ProPlus-Pilot- und Integritätsdashboard](./media/4488272-office-365-pro-plus-pilot.png)


### <a name="generate-pilot"></a>Generieren des Pilotprojekts

Generieren Sie mit nur einem Mausklick eine Pilotempfehlung aus einer einschränkenden Sammlung. Sobald die Aktion gestartet wurde, beginnt ein Hintergrundtask mit der Berechnung der Pilotsammlung. Die einschränkende Sammlung muss mindestens ein Gerät mit einer Office-Version enthalten, die nicht ProPlus ist.

### <a name="recommended-pilot-devices"></a>Empfohlene Pilotgeräte

**Empfohlene Pilotgeräte** sind eine minimale Gruppe von Geräten, die alle installierten Add-Ins über die einschränkende Sammlung hinweg darstellen, die Sie beim Erstellen des Pilotprojekts verwendet haben. Führen Sie einen Drilldown aus, um eine Liste dieser Geräte abzurufen. Verwenden Sie dann die Details, um bei Bedarf Geräte aus dem Pilotprojekt auszuschließen. Wenn alle Ihre Add-Ins bereits auf Office 365 ProPlus-Geräten vorhanden sind, werden Geräte mit diesen Add-Ins nicht in die Berechnung einbezogen. Dies bedeutet auch, dass Sie möglicherweise in ihrer Pilotsammlung keine Ergebnisse erhalten, da alle Ihre Add-Ins auf Geräten gefunden werden, auf denen Office 365 ProPlus installiert ist.

### <a name="deploy-pilot"></a>Bereitstellen des Pilotprojekts

Nachdem Sie Ihre Pilotgeräte akzeptiert haben, stellen Sie Office 365 ProPlus mit dem Assistenten für stufenweise Bereitstellung für die Pilotsammlung bereit. Administratoren können das Pilotprojekt und die einschränkende Sammlung im Assistenten zum Verwalten von Bereitstellungen definieren.

### <a name="health-data"></a>Integritätsdaten

Nachdem Office 365 ProPlus installiert wurde, aktivieren Sie Integritätsdaten für Ihre Pilotgeräte. Die Integritätsdaten geben Aufschluss darüber, welche Add-Ins und Makros die Integritätsziele nicht erfüllen. Das Diagramm **Geräte, die für die Bereitstellung bereit sind** identifiziert Nicht-Pilotgeräte, die für die Bereitstellung bereit sind, mithilfe von Einblicken in die Integrität. Rufen Sie die Anzahl von Geräten, die Integritätsdaten senden, aus dem Diagramm **Geräte, die Integritätsdaten senden** ab.

### <a name="devices-not-meeting-health-goals"></a>Geräte, die die Integritätsziele nicht erfüllen

Auf dieser Kachel werden Geräte zusammengefasst, bei denen Probleme mit Add-Ins, Makros oder beidem auftreten.

### <a name="add-ins-not-meeting-health-goals"></a>Add-Ins, die die Integritätsziele nicht erfüllen

- Fehler beim Laden: Das Add-In wurde nicht gestartet.
- Abstürze: Bei der Ausführung des Add-Ins ist ein Fehler aufgetreten.
- Fehler: Das Add-In hat einen Fehler gemeldet.
- Mehrere Probleme: Das Add-In weist mehr als eins der oben genannten Probleme auf.

### <a name="macros-not-meeting-health-goals"></a>Makros, die die Integritätsziele nicht erfüllen

- Fehler beim Laden: Das Dokument konnte nicht geladen werden.
- Laufzeitfehler: Bei der Ausführung des Makros ist ein Fehler aufgetreten. Diese Fehler können von den Eingaben abhängig sein, treten also nicht immer auf.
- Fehler beim Kompilieren: Das Makro wurde nicht ordnungsgemäß kompiliert, daher wird nicht versucht, es auszuführen.
- Mehrere Probleme: Das Makro weist mehr als eins der oben genannten Probleme auf.

> [!NOTE]
> Der Makrobestand wird aus Daten des Readiness Toolkits für Office und der zuletzt verwendeten Datendateien aufgefüllt. Die Makrointegrität wird aus Integritätsdaten aufgefüllt. Aufgrund der verschiedenen Datenquellen ist es möglich, dass der Integritätsstatus von Makros **Überprüfung erforderlich** ist, wenn der Makrobestand **Nicht überprüft** ist. <!--5922845-->

### <a name="known-issues"></a>Bekannte Probleme

Es gibt ein bekanntes Problem mit der Kachel **Deploy Pilot** (Pilot bereitstellen). Zurzeit lassen sich darüber keine Pilotsammlungen bereitstellen. Die Problemumgehung besteht in der Bereitstellung einer Anwendung mithilfe des Assistenten für die graduelle Bereitstellung (vorhandener Workflow ). <!--5525871-->

## <a name="next-steps"></a>Nächste Schritte

[Verwalten von Office 365 ProPlus mit Configuration Manager](manage-office-365-proplus-updates.md)
