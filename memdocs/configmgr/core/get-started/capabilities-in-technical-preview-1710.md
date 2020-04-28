---
title: Technical Preview 1710 | Microsoft-Dokumentation
titleSuffix: Configuration Manager
description: Erfahren Sie mehr zu Features, die in Technical Preview für Configuration Manager-Version 1710 zur Verfügung stehen.
ms.date: 11/20/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f4706a58-1f11-4eab-b1eb-3d1a0da02d0f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 503bb6d2293b4b5efb1d84980225a9d7052e1656
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705108"
---
# <a name="capabilities-in-technical-preview-1710-for-configuration-manager"></a>Funktionen in der Technical Preview 1710 für Configuration Manager

*Gilt für: Configuration Manager (Technical Preview-Branch)*

In diesem Artikel werden die Features vorgestellt, die in der Technical Preview-Version 1710 für Configuration Manager verfügbar sind. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen. Bevor Sie diese Technical Preview-Version installieren, lesen Sie [Technical Preview für Configuration Manager](../../core/get-started/technical-preview.md), um sich mit den allgemeinen Anforderungen und Einschränkungen bei der Verwendung einer Technical Preview-Version vertraut zu machen und zu erfahren, wie Sie Updates für Versionen durchführen und Feedback zu den Funktionen in einer Technical Preview-Version geben können.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Bekannte Probleme in dieser Technical Preview:**
- **Unterstützung für Windows 10-Version 1709 (auch Fall Creators Update genannt)** .  Ab diesem Windows-Release umfassen Windows-Medien mehrere Editionen. Achten Sie beim Konfigurieren einer Tasksequenz für ein Betriebssystem-Upgradepaket oder ein Betriebssystemimage darauf, eine [Edition auszuwählen, die für Configuration Manager unterstützt wird](../plan-design/configs/support-for-windows-10.md#windows-10-as-a-client).
- **Beim Update auf die Vorschauversion tritt ein Fehler auf, wenn Sie einen Standortserver im passiven Modus haben**. Wenn Sie eine Vorschauversion ausführen, die über einen [primären Standortserver im passiven Modus](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) verfügt, müssen Sie den Standortserver im passiven Modus deinstallieren, bevor Sie Ihren Vorschaustandort auf diese neue Vorschauversion aktualisieren können. Sie können den Standortserver im passiven Modus erneut installieren, wenn das Update an Ihrem Standort abgeschlossen wurde.

  So deinstallieren Sie den Standortserver im passiven Modus:
  1. Navigieren Sie in der Konsole zu **Administration** > **Übersicht** > **Standortkonfiguration** > **Server und Standortsystemrollen**, und wählen Sie den Standortserver im passiven Modus aus.
  2. Klicken Sie im Bereich **Standortsystemrollen** mit der rechten Maustaste auf die Rolle **Standortserver**, und wählen Sie dann **Rolle entfernen**.
  3. Klicken Sie mit der rechten Maustaste auf den Standortserver im passiven Modus, und wählen Sie dann **Löschen**.
  4. Starten Sie nach dem Deinstallieren des Standortservers auf dem aktiven primären Standortserver den Dienst **CONFIGURATION_MANAGER_UPDATE** neu.

**Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-for-deploying-powershell-scripts-from-configuration-manager"></a>Verbesserungen für die Bereitstellung von PowerShell-Skripts aus Configuration Manager
Ab dieser Version unterstützen PowerShell-Skripts, die Sie bereitstellen, die folgenden Verbesserungen: 
- **Sicherheitsbereiche**.  Skripts verwenden jetzt Sicherheitsbereiche, um die Erstellung und Ausführung von Skripts zu steuern. Dies erfolgt durch Zuweisen von Tags, die Benutzergruppen darstellen. Weitere Informationen zu Sicherheitsbereichen finden Sie unter [Konfigurieren der rollenbasierten Verwaltung für Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).
- **Echtzeitüberwachung**. Wenn Sie die Ausführung eines Skripts überwachen, erfolgt dies nun in Echtzeit, während das Skript ausgeführt wird.
- **Validierung von Parametern**. Für jeden Parameter in Ihrem Skript gibt es das Dialogfeld **Skriptparameter – Eigenschaften**, in dem Sie eine Validierung für den jeweiligen Parameter hinzufügen können. Nach dem Hinzufügen der Validierung sollten Sie Fehlermeldungen erhalten, wenn Sie einen Wert für einen Parameter eingeben, der nicht dessen Validierung entspricht.

Die Bereitstellung von PowerShell-Skripts wurde erstmals in die [Technical Preview-Version 1706](capabilities-in-technical-preview-1706.md#create-and-run-powershell-scripts-from-the-configuration-manager-console) eingeführt. Zusätzliche Verbesserungen wurden von den Technical Preview-Versionen [1707](capabilities-in-technical-preview-1707.md#add-parameters-when-you-deploy-powershell-scripts-from-configuration-manager) und [1708](capabilities-in-technical-preview-1708.md#improvements-for-specifying-script-parameters-when-you-deploy-powershell-scripts-from-configuration-manager) geboten.


### <a name="try-it-out"></a>Probieren Sie es aus!

Informationen zur Funktion „Skripts ausführen“ finden Sie unter [Erstellen und Ausführen von Skripts](../../apps/deploy-use/create-deploy-scripts.md).



## <a name="limit-windows-10-enhanced-data-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Begrenzen der bei der Einstellung „Erweitert“ unter Windows 10 gesendeten Daten auf die Daten, die für den Geräteintegritätsdienst von Windows Analytics relevant sind
<!-- 1356148 -->

Ab diesem Release können Sie für Diagnosedaten unter Windows 10 **Erweitert (begrenzt)** als Datensammlungsebene festlegen. Mit dieser Einstellung können Sie handlungsrelevante Informationen zu Geräten in Ihrer Umgebung gewinnen, ohne dass diese alle Daten auf der Stufe **Erweitert** an Windows 10-Version 1709 oder höher melden.

Die Ebene „Erweitert (begrenzt)“ enthält Metriken aus der Ebene „Basic“ (Einfach) sowie eine Teilmenge der für Windows Analytics relevanten Daten, die auf der Ebene **Erweitert** gesammelt werden.


## <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>Das Softwarecenter verzerrt keine Symbole mehr, die größer als 250 x 250 Pixel sind  
<!-- 1356194 -->

Seit diesem Release werden Symbole, die größer als 250 x 250 Pixel sind, im Softwarecenter nicht mehr verzerrt dargestellt. In der Vergangenheit sahen sie im Softwarecenter unscharf aus. Von nun an können Sie Symbole mit bis zu 512 x 512 Pixel ohne Verzerrung darstellen.

### <a name="try-it-out"></a>Probieren Sie es aus!
Sie haben die Möglichkeit, im Softwarecenter ein Symbol für Ihre App hinzuzufügen. Lesen Sie dazu den Artikel [Erstellen von Anwendungen mit System Center Configuration Manager](../../apps/deploy-use/create-applications.md).


## <a name="check-compliance-from-software-center-for-co-managed-devices"></a>Überprüfen der Konformität co-verwalteter Geräte über das Software Center
<!-- 1356374 -->
Seit diesem Release können Benutzer die Konformität ihrer co-verwalteten Windows 10-Geräte im Softwarecenter sogar dann überprüfen, wenn der bedingte Zugriff von Intune verwaltet wird. Weitere Informationen finden Sie unter [Co-Verwaltung für Windows 10-Geräte](./capabilities-in-technical-preview-1709.md#co-management-for-windows-10-devices).


## <a name="support-for-exploit-guard"></a>Unterstützung für Exploit Guard
Dieses Release enthält mehr Unterstützung für Windows Defender Exploit Guard. Sie können Richtlinien konfigurieren und bereitstellen, die alle vier Komponenten von Exploit Guard verwalten. Zu diesen Komponenten gehören:
-   die Verringerung der Angriffsfläche
-   der überwachte Ordnerzugriff
-   der Exploit-Schutz
-   der Netzwerkschutz

Konformitätsinformationen für die Bereitstellung der Exploit Guard-Richtlinie sind in der Configuration Manager-Konsole verfügbar.

Weitere Informationen zu Exploit Guard sowie bestimmten Komponenten und Regeln finden Sie in der Windows-Dokumentationsbibliothek unter [Windows Defender Exploit Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/windows-defender-exploit-guard).

### <a name="prerequisites"></a>Voraussetzungen
Auf verwalteten Geräten muss das Windows 10 1709 Fall Creators Update oder höher ausgeführt werden, und sie müssen je nach konfigurierten Komponenten und Regeln die folgenden Anforderungen erfüllen:

|Exploit Guard-Komponente |Zusätzliche Voraussetzungen|
|------------------------|------------------------|
| Verringerung der Angriffsfläche  | Auf den Geräten muss der [Echtzeitschutz von Windows Defender AV]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) aktiviert sein.  |
| Überwachter Ordnerzugriff  | Auf den Geräten muss der [Echtzeitschutz von Windows Defender AV]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) aktiviert sein.   |
| Exploit-Schutz  | Keine  |
| Netzwerkschutz  |  Auf den Geräten muss der [Echtzeitschutz von Windows Defender AV]( https://docs.microsoft.com/windows/threat-protection/windows-defender-exploit-guard/controlled-folders-exploit-guard) aktiviert sein.  |

### <a name="create-an-exploit-guard-policy----1355468---"></a>Erstellen einer Exploit Guard-Richtlinie  <!--1355468 -->
1. Wechseln Sie in der Configuration Manager-Konsole zu **Assets und Konformität** > **Endpoint Protection**, und klicken Sie dann auf **Windows Defender Exploit Guard**.
2. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Create Exploit Policy** (Exploit-Richtlinie erstellen).
3. Geben Sie auf der Seite **Allgemein** des **Assistenten zum Erstellen von Konfigurationselementen**einen Namen und optional eine Beschreibung für das Konfigurationselement an.
4. Wählen Sie als Nächstes die Exploit Guard-Komponenten aus, die Sie mit dieser Richtlinie verwalten möchten. Für jede Komponente, die Sie auswählen, können Sie zusätzliche Details konfigurieren.
   - **Verringerung der Angriffsfläche:** Konfigurieren Sie den Schutz vor Office-, Skript- und E-Mail-Bedrohungen, die Sie überwachen oder blockieren möchten. Von dieser Regel können auch bestimmte Dateien oder Ordner ausgeschlossen werden.
   - **Überwachter Ordnerzugriff:** Konfigurieren Sie Blockierungs- und Überwachungseinstellungen, und legen Sie anschließend fest, welche Apps von dieser Richtlinie ausgenommen sind.  Es ist auch möglich, zusätzliche Ordner anzugeben, die standardmäßig nicht geschützt werden.
   - **Exploit-Schutz:**  Legen Sie eine XML-Datei mit Einstellungen fest, die das Risiko von Exploit-Vorgängen für Systemprozesse und Apps mindern. Diese Einstellungen lassen sich über die Windows Defender Security Center-App auf einem Windows 10-Gerät exportieren.
   - **Netzwerkschutz:** Legen Sie Netzwerkschutzeinstellungen fest, durch die der Zugriff auf verdächtige Domänen blockiert oder überwacht wird.
5. Schließen Sie den Assistenten ab, um die Richtlinie zu erstellen, die Sie später für Geräte bereitstellen können.

### <a name="deploy-an-exploit-guard-policy"></a>Bereitstellen einer Exploit Guard-Richtlinie     
Nach der Erstellung der Exploit Guard-Richtlinien stellen Sie sie mithilfe des Assistenten zum Bereitstellen von Exploit Guard-Richtlinien bereit. Wechseln Sie dazu in der Configuration Manager-Konsole zu **Assets und Konformität** > **Endpoint Protection**, und klicken Sie dann auf **Deploy Exploit Guard Policy** (Exploit Guard-Richtlinie bereitstellen).

## <a name="limited-support-for-cng-certificates"></a>Eingeschränkte Unterstützung für CNG-Zertifikate
<!-- 1356191 -->
Ab diesem Release können Sie Zertifikatvorlagen des Typs [Cryptography API: Next Generation (CNG)](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx) für die folgenden Szenarios verwenden:

- Clientregistrierung und Kommunikation mit einem HTTPS-Verwaltungspunkt   
- Softwareverteilung und Anwendungsbereitstellung mit einem HTTPS-Verteilungspunkt   
- Betriebssystembereitstellung  
- Client messaging SDK (mit dem aktuellen Update) und ISV-Proxy   
- Cloud Management Gateway-Konfiguration  

Um CNG-Zertifikate zu verwenden, muss die Zertifizierungsstelle (Certification Authority, CA) CNG-Zertifikatvorlagen für Zielcomputer bereitstellen.  Vorlagendetails variieren je nach Szenario. Allerdings sind die folgenden Eigenschaften erforderlich:

- Registerkarte **Kompatibilität**

    - Die **Zertifizierungsstelle** muss Windows Server 2008 oder höher sein. Empfohlen wird Windows Server 2012.

    - Der **Zertifikatempfänger** muss Windows Vista/Server 2008 oder höher sein. Empfohlen wird Windows 8/Windows Server 2012.

- Registerkarte **Kryptografie**

    - Die **Anbieterkategorie** muss der **Schlüsselspeicheranbieter** sein.  (Erforderlich)

Für optimale Ergebnisse wird empfohlen, einen Antragstellernamen aus Active Directory-Informationen zu erstellen.  Verwenden Sie den DNS-Namen für das **Format des Antragstellernamens**, und verwenden Sie den DNS-Namen im alternativen Antragstellernamen.  Andernfalls müssen Sie diese Informationen bereitstellen, wenn das Gerät beim Zertifikatprofil registriert wird.


## <a name="improved-descriptions-for-pending-computer-restarts-----1356283---"></a>Verbesserte Beschreibungen für ausstehende Computerneustarts   <!--1356283 -->
Seit [Technical Preview 1708](capabilities-in-technical-preview-1708.md#restart-computers-from-the-configuration-manager-console) ist es möglich, über die Configuration Manager-Konsole Geräte zu identifizieren, für die ein Systemneustart aussteht.

Ab dieser Technical Preview zeigt die Konsole zusätzliche Details an, die Aufschluss über den Prozess oder die Aktion geben, die den Neustart anfordert.

## <a name="device-guard-policy-changes----1355092---"></a>Änderungen an Device Guard-Richtlinien <!-- 1355092 -->
Im Technical Preview-Build 1710 wurden die folgenden drei Änderungen hinsichtlich der Device Guard-Richtlinien vorgenommen:

### <a name="device-guard-policies-renamed-to-windows-defender-application-control-policies"></a>Device Guard-Richtlinien in Windows Defender-Anwendungssteuerungsrichtlinien umbenannt
Die Device Guard-Richtlinien wurden in Windows Defender-Anwendungssteuerungsrichtlinien umbenannt. Der **Assistent zum Erstellen von Device Guard-Richtlinien** heißt jetzt **Assistent zum Erstellen von Windows Defender-Anwendungssteuerungsrichtlinien**.

### <a name="restart-is-not-required-to-apply-policies"></a>Neustart für die Umsetzung von Richtlinien nicht erforderlich
Ab dem Fall Creators Update für Windows-Version 1709 müssen Geräte mit der neuen Windows-Version nicht mehr neu gestartet werden, um die Windows Defender-Anwendungssteuerungsrichtlinien anzuwenden.

Ein Neustart ist die Standardeinstellung.

#### <a name="try-it-out"></a>Probieren Sie es aus!  

Wenn Sie Neustarts deaktivieren möchten, gehen Sie folgendermaßen vor:

1.  Öffnen Sie den **Assistenten zum Erstellen von Windows Defender-Anwendungssteuerungsrichtlinien**.
2.  Deaktivieren Sie auf der Seite **Allgemein** das Kontrollkästchen für **Einen Neustart von Geräten erzwingen, damit diese Richtlinie für alle Prozesse durchgesetzt werden kann**.
3.  Klicken Sie auf **Weiter**, bis Sie den Assistenten abgeschlossen haben.

Für frühere Versionen von Windows wird ein automatischer Neustart weiterhin erzwungen.

### <a name="automatically-run-software-trusted-by-the-intelligent-security-graph"></a>Automatisches Ausführen von Software, die von Intelligent Security Graph als vertrauenswürdig eingestuft wird

Administratoren haben jetzt die Möglichkeit zuzulassen, dass gesperrte Geräte vertrauenswürdige Software ausführen, die laut Microsoft Intelligent Security Graph (ISG) einen guten Ruf hat. ISG besteht aus Windows Defender SmartScreen und anderen Microsoft-Diensten.

Auf den Geräten muss Windows Defender SmartScreen ausgeführt werden, damit die Software als vertrauenswürdig eingestuft werden kann.

#### <a name="try-it-out"></a>Probieren Sie es aus!  

Damit ein Gerät mit Windows Defender SmartScreen vertrauenswürdige Software ausführen kann, gehen Sie folgendermaßen vor:

1.  Öffnen Sie den **Assistenten zum Erstellen von Windows Defender-Anwendungssteuerungsrichtlinien**.
2.  Aktivieren Sie auf der Seite **Einschlüsse** das Kontrollkästchen für **Software autorisieren, die vom Intelligent Security Graph als vertrauenswürdig eingestuft wird**.
3.  Fügen Sie im Feld **Trusted files or folder** (Vertrauenswürdige Dateien oder Ordner) die Dateien und Ordner hinzu, die als vertrauenswürdig gelten sollen.
4.  Klicken Sie auf **Weiter**, bis Sie den Assistenten abgeschlossen haben.

## <a name="configure-and-deploy-windows-defender-application-guard-policies----1351960---"></a>Konfigurieren und Bereitstellen von Windows Defender Application Guard-Richtlinien <!-- 1351960 -->

[Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) ist eine neue Windows-Funktion zum Schutz Ihrer Benutzer, indem nicht vertrauenswürdige Websites in einem sicheren isolierten Container geöffnet werden, auf den andere Teile des Betriebssystems keinen Zugriff haben. In dieser Technical Preview haben wir Unterstützung für diese Funktion mithilfe von Configuration Manager-Konformitätseinstellungen hinzugefügt, die Sie konfigurieren und in einer Sammlung bereitstellen. Dieses Feature wird als Vorschauversion für die 64-Bit-Version von Windows 10 Creator Update veröffentlicht. Um diese Funktion jetzt zu testen, müssen Sie eine Preview-Version dieses Updates verwenden.

### <a name="before-you-start"></a>Vorbereitung
Zum Erstellen und Bereitstellen von Windows Defender Application Guard-Richtlinien müssen die Windows 10-Geräte, auf denen Sie die Richtlinie bereitstellen, mit einer Netzwerkisolationsrichtlinie konfiguriert werden. Weitere Informationen finden Sie im Blogbeitrag, auf den später verwiesen wird. Diese Funktion funktioniert nur mit aktuellen Windows 10 Insider-Builds. Um sie zu testen, muss auf Ihren Clients ein aktueller Windows 10 Insider-Build ausgeführt werden.

### <a name="try-it-out"></a>Probieren Sie es aus!

Um sich mit den Grundlagen von Windows Defender Application Guard vertraut zu machen, lesen Sie den [Blogbeitrag](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97).

So erstellen Sie eine Richtlinie und durchsuchen die verfügbaren Einstellungen
1. Wählen Sie in der **Configuration Manager**-Konsole **Assets und Konformität** aus.
2. Wählen Sie im Arbeitsbereich **Assets und Konformität** nacheinander **Übersicht** > **Endpoint Protection** > **Windows Defender Application Guard** aus.
3. Klicken Sie auf der Registerkarte **Start** in der Gruppe **Erstellen** auf **Windows Defender Application Guard-Richtlinie erstellen**.
4. Unter Verwendung des Blogbeitrags als Referenz können Sie die verfügbaren Einstellungen zum Testen der Funktion durchsuchen und konfigurieren.
5. In dieser Version haben wir dem Assistenten die neue Seite „Netzwerkdefinition“ hinzugefügt. Geben Sie hier die Unternehmensidentität an, und definieren Sie die Grenze Ihres Unternehmensnetzwerks.

    > [!NOTE]
    > PCs unter Windows 10 speichern nur eine Netzwerkisolationsliste auf dem Client. In dieser Version können Sie zwei unterschiedliche Arten von Netzwerkisolationslisten erstellen (eine von Windows Information Protection und eine von Windows Defender Application Guard) und diese dem Client bereitstellen. Wenn Sie beide Richtlinien bereitstellen, müssen diese Netzwerkisolationlisten übereinstimmen. Wenn Sie Listen bereitstellen, die nicht mit dem gleichen Client übereinstimmen, schlägt die Bereitstellung fehl.

    Weitere Informationen über das Angeben von Netzwerkdefinition finden Sie in der Dokumentation zu Windows Information Protection – [Schützen von Unternehmensdaten mit Windows Information Protection (WIP)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)

6. Wenn Sie fertig sind, schließen Sie den Assistenten ab, und stellen Sie die Richtlinie auf einem oder mehreren Windows 10-Geräten bereit.

### <a name="further-reading"></a>Weitere Informationen

Weitere Informationen zu Windows Defender Application Guard finden Sie in [diesem Blogbeitrag](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Darüber hinaus finden Sie in [diesem Blogbeitrag](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903) weitere Informationen zum eigenständigen Modus von Windows Defender Application Guard.

## <a name="next-steps"></a>Nächste Schritte
Informationen zur Installation oder zum Update des Technical Preview-Branch finden Sie unter [Technical Preview für Configuration Manager](technical-preview.md).    
