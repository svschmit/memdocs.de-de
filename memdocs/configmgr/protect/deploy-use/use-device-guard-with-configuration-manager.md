---
title: Verwalten der Windows Defender-Anwendungssteuerung
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie mit Configuration Manager die Windows Defender-Anwendungssteuerung verwalten können.
ms.date: 11/19/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 5e5d854c-9cc1-4dd8-b33f-0fcac675b395
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0dcd519a7703b5de94f779dc5dbe48aa0d34a3bc
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700462"
---
# <a name="windows-defender-application-control-management-with-configuration-manager"></a>Verwalten der Windows Defender-Anwendungssteuerung mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

## <a name="introduction"></a>Einführung
Die Windows Defender-Anwendungssteuerung dient zum Schutz von PCs vor Schadsoftware und anderer nicht vertrauenswürdiger Software. Device Guard verhindert die Ausführung von Schadcode, indem sichergestellt wird, dass nur genehmigter bekannter Code ausgeführt werden kann.

Windows Defender-Anwendungssteuerung ist eine softwarebasierte Sicherheitsstufe, bei der auf einem PC nur die in einer expliziten Liste enthaltene Software ausgeführt werden darf. Für sich genommen weist die Anwendungssteuerung keine Hardware- oder Firmwareanforderungen auf. Mit Configuration Manager bereitgestellte Anwendungssteuerungsrichtlinien aktivieren eine Richtlinie auf PCs in gezielten Sammlungen, die die in diesem Artikel aufgeführten Mindestanforderungen an die Windows-Version und SKU erfüllen. Optional kann hypervisorbasierter Schutz der durch Configuration Manager bereitgestellten Anwendungssteuerungsrichtlinien über die Gruppenrichtlinie auf geeigneter Hardware aktiviert werden.

Weitere Informationen zur Windows Defender-Anwendungssteuerung finden Sie im [Bereitstellungshandbuch für Windows Defender-Anwendungssteuerung](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide).

   > [!NOTE]
   > - Ab Windows 10, Version 1709, werden konfigurierbare Codeintegritätsrichtlinien als Windows Defender-Anwendungssteuerung bezeichnet.
   > - Ab Configuration Manager Version 1710 wurden Device Guard-Richtlinien in Windows Defender-Anwendungssteuerungsrichtlinien umbenannt.

## <a name="using-windows-defender-application-control-with-configuration-manager"></a>Verwenden der Windows Defender-Anwendungssteuerung mit Configuration Manager

Mit Configuration Manager können Sie eine Windows Defender-Anwendungssteuerungsrichtlinie bereitstellen. Mit dieser Richtlinie können Sie den Modus konfigurieren, in dem die Windows Defender-Anwendungssteuerung auf PCs in einer Sammlung ausgeführt wird. 

Folgende Modi stehen zur Verfügung:

1. **Erzwingen aktiviert**: Nur vertrauenswürdige ausführbare Dateien dürfen ausgeführt werden.
2. **Nur überwachen**: Alle Programme können ausgeführt werden, allerdings werden nicht vertrauenswürdige Programme bei ihrer Ausführung im Ereignisprotokoll des lokalen Clients erfasst.

> [!Tip]  
> Dieses Feature wurde erstmals in Version 1702 als [Vorabfeature](../../core/servers/manage/pre-release-features.md) eingeführt. Ab Version 1906 ist es kein Vorabfeature mehr.  

## <a name="what-can-run-when-you-deploy-a-windows-defender-application-control-policy"></a>Was kann ausgeführt werden, wenn Sie eine Windows Defender-Anwendungssteuerungsrichtlinie bereitstellen?

Mit der Windows Defender-Anwendungssteuerung können Sie streng steuern, was auf von Ihnen verwalteten PCs ausgeführt werden kann. Dieses Feature kann für PCs in Abteilungen mit hohen Sicherheitsanforderungen nützlich sein, in denen es unerlässlich ist, die Ausführung unerwünschter Software zu verhindern.

Wenn Sie eine Richtlinie bereitstellen, wird üblicherweise die Ausführung der folgenden ausführbaren Dateien zugelassen:

- Windows-Betriebssystemkomponenten
- Entwicklungscenter-Hardwaretreiber, die über WHQL-Signaturen (Windows-Hardware Quality Labs) verfügen
- Windows Store-Apps
- Der Configuration Manager-Client 
- Sämtliche, durch Configuration Manager bereitgestellte Software, die PCs nach der Verarbeitung der Windows Defender-Anwendungssteuerungsrichtlinie installieren. 
- Updates zu Windows-Komponenten von:
    - Windows Update
    - Windows Update for Business
    - Windows Server Update Services
    - Configuration Manager
    - Optional Software, die laut Microsoft Intelligent Security Graph (ISG) einen guten Ruf hat. ISG umfasst Windows Defender SmartScreen und andere Microsoft-Dienste. Auf den Geräten müssen Windows Defender SmartScreen und Windows 10, Version 1709 oder höher, ausgeführt werden, damit die Software als vertrauenswürdig eingestuft werden kann.

>[!IMPORTANT]
>Diese Elemente enthalten keine *nicht* in Windows integrierte Software, die automatisch über das Internet bzw. über Softwareupdates von Drittanbietern aktualisiert wird, ganz gleich, ob sie über einen der zuvor genannten Aktualisierungsmechanismen oder über das Internet installiert wird. Nur Softwareänderungen, die über den Configuration Manager-Client bereitgestellt werden, können ausgeführt werden.

## <a name="before-you-start"></a>Vorbereitung

Bevor Sie Windows Defender-Anwendungssteuerungsrichtlinien konfigurieren oder bereitstellen, lesen Sie die folgenden Informationen:

- Die Verwaltung der Windows Defender-Anwendungssteuerung ist ein Vorabfeature für Configuration Manager und unterliegt Änderungen.
- Um die Windows Defender-Anwendungssteuerung mit Configuration Manager zu verwenden, muss auf PCs, die Sie verwalten, Windows 10 Enterprise in der Version 1703 oder höher ausgeführt werden.
- Sobald eine Richtlinie erfolgreich auf einem Client-PC verarbeitet wurde, wird Configuration Manager als verwaltetes Installationsprogramm auf dem Client konfiguriert. Software, die darüber bereitgestellt wird, gilt nach der Verarbeitung der Richtlinie automatisch als vertrauenswürdig. Software, die von Configuration Manager vor der Verarbeitung der Windows Defender-Anwendungssteuerungsrichtlinie installiert wurde, wird nicht automatisch vertraut.
- Standardmäßig erfolgt die Konformitätsauswertung für während der Bereitstellung konfigurierbare Anwendungssteuerungsrichtlinien täglich. Wenn bei der Verarbeitung der Richtlinie Probleme festgestellt werden, kann es sinnvoll sein, den Zeitplan für die Kompatibilitätsauswertung mit einem kürzeren Intervall zu konfigurieren, z.B. jede Stunde. Dieser Zeitplan bestimmt, wie oft Clients im Fall eines Fehlers erneut versuchen, eine Windows Defender-Anwendungssteuerungsrichtlinie zu verarbeiten.
- Wenn Sie eine Windows Defender-Anwendungssteuerungsrichtlinie bereitstellen, können Client-PCs unabhängig vom ausgewählten Erzwingungsmodus keine HTML-Anwendungen mit der Erweiterung „.hta“ ausführen.

## <a name="how-to-create-a-windows-defender-application-control-policy"></a>Erstellen einer Windows Defender-Anwendungssteuerungsrichtlinie
1. Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.
2. Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** den Knoten **Endpoint Protection**, und klicken Sie anschließend auf **Windows Defender-Anwendungssteuerung**.
3. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Anwendungssteuerungsrichtlinie erstellen**.
4. Geben Sie auf der Seite **Allgemein** des **Assistenten zum Erstellen von Anwendungssteuerungsrichtlinien** die folgenden Einstellungen an:
    - **Name**: Geben Sie einen eindeutigen Namen für diese Windows Defender-Anwendungssteuerungsrichtlinie ein. 
    - **Beschreibung**: Wenn Sie möchten, können Sie eine Beschreibung für die Richtlinie eingeben, anhand derer Sie sie in der Configuration Manager-Konsole erkennen können.
    - **Einen Neustart von Geräten erzwingen, damit diese Richtlinie für alle Prozesse durchgesetzt werden kann**: Nachdem die Richtlinie auf einem Client-PC verarbeitet wurde, wird ein Neustart auf dem Client entsprechend der **Clienteinstellungen** für **Computerneustart** geplant.
        - Geräte unter Windows 10, Version 1703 oder früher, werden immer automatisch neu gestartet.
        - Ab Windows 10, Version 1709, wird auf derzeit auf dem Gerät ausgeführte Anwendungen die neue Anwendungssteuerungsrichtlinie erst nach einem Neustart angewendet. Anwendungen, die gestartet werden, nachdem die Richtlinie angewendet wurde, berücksichtigen die neue Anwendungssteuerungsrichtlinie jedoch. 
    - **Erzwingungsmodus**: Wählen Sie eine der folgenden Erzwingungsmethoden für die Windows Defender-Anwendungssteuerung auf dem Client-PC aus.
        - **Erzwingen aktiviert**: Nur vertrauenswürdige ausführbare Dateien dürfen ausgeführt werden.
        - **Nur überwachen**: Alle Programme können ausgeführt werden, allerdings werden nicht vertrauenswürdige Programme bei ihrer Ausführung im Ereignisprotokoll des lokalen Clients erfasst.
5. Wählen Sie auf der Registerkarte **Einschlüsse** des **Assistenten zum Erstellen von Anwendungssteuerungsrichtlinien** aus, ob Sie **Software autorisieren möchten, die von Intelligent Security Graph als vertrauenswürdig eingestuft wurde**.
6. Klicken Sie auf **Hinzufügen**, wenn Sie eine Vertrauensstellung für bestimmte Dateien oder Ordner auf PCs hinzufügen möchten. Im Dialogfeld **Vertrauenswürdige Dateien oder Ordner hinzufügen** können Sie eine lokale Datei oder einen Ordnerpfad angeben, die bzw. der als vertrauenswürdig gelten soll. Sie können auch eine Datei oder einen Ordnerpfad auf einem Remotegerät angeben, mit dem Sie eine Verbindung herstellen können. Wenn Sie in einer Windows Defender-Anwendungssteuerungsrichtlinie eine Vertrauensstellung für bestimmte Dateien oder Ordner hinzufügen, ermöglicht Ihnen dies Folgendes:
    - Beheben von Problemen mit dem Verhalten verwalteter Installationsprogramme
    - Vertrauen branchenspezifischer Apps, die nicht mit Configuration Manager bereitgestellt werden können
    - Vertrauen von Apps, die in einem Betriebssystemabbild für ein Betriebssystem enthalten sind 
8. Klicken Sie auf **Weiter**, um den Assistenten abzuschließen.

>[!IMPORTANT]
>Die Einbeziehung vertrauenswürdiger Dateien oder Ordner wird nur auf Client-PCs mit Version 1706 oder höher des Configuration Manager-Clients unterstützt. Wenn Einschlussregeln in einer Windows Defender-Anwendungssteuerungsrichtlinie enthalten sind, und die Richtlinie dann für einen Client-PC bereitgestellt wird, auf dem eine frühere Version des Configuration Manager-Clients ausgeführt wird, kann die Richtlinie nicht angewendet werden. Das Aktualisieren dieser älteren Clients behebt dieses Problem. Richtlinien, die keine Einschlussregeln enthalten, können möglicherweise weiterhin auf ältere Versionen des Configuration Manager-Clients angewendet werden.

## <a name="how-to-deploy-a-windows-defender-application-control-policy"></a>Bereitstellen einer Windows Defender-Anwendungssteuerungsrichtlinie
1. Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.
2. Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** den Knoten **Endpoint Protection**, und klicken Sie anschließend auf **Windows Defender-Anwendungssteuerung**.
3. Wählen Sie aus der Liste der Richtlinien die Richtlinie aus, die Sie bereitstellen möchten, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Anwendungssteuerungsrichtlinie bereitstellen**.
4. Wählen Sie im Dialogfeld **Anwendungssteuerungsrichtlinie bereitstellen** die Sammlung aus, der Sie die Richtlinie bereitstellen möchten. Konfigurieren Sie anschließend einen Zeitplan, nach dem die Clients die Richtlinie auswerten sollen. Wählen Sie abschließend aus, ob der Client die Richtlinie außerhalb konfigurierter Wartungsfenster auswerten kann.
5. Klicken Sie abschließend auf **OK**, um die Richtlinie bereitzustellen. 

<!--Reworked article to put this inline while working on VSO 1355092
### Restarting the device after deploying the policy

After the policy is processed on a client PC, a restart is scheduled on that client according to the **Client Settings** for **Computer Restart**. A restart is not required to apply policies, but it is the default. If you want to turn off restarts, follow these steps:

1. Open the **Create Windows Defender Application Policy** wizard.
2. On the **General** page, clear the check box for **Enforce a restart of devices so that this policy can be enforced for all processes**.
3. Click **Next** until the wizard completes.-->


## <a name="how-to-monitor-a-windows-defender-application-control-policy"></a>Überwachen einer Windows Defender-Anwendungssteuerungsrichtlinie

Verwenden Sie die Informationen im Artikel [Überwachen von Konformitätseinstellungen](../../compliance/deploy-use/monitor-compliance-settings.md), um sicherzustellen, dass die bereitgestellte Richtlinie ordnungsgemäß auf alle PCs angewendet wurde.

Um die Verarbeitung einer Windows Defender-Anwendungssteuerungsrichtlinie zu überwachen, verwenden Sie die folgende Protokolldatei auf Client-PCs:

**%WINDIR%\CCM\Logs\DeviceGuardHandler.log**

Informationen dazu, welche Software blockiert oder überwacht wird, finden Sie in den folgenden Ereignisprotokollen des lokalen Clients:

1. Verwenden Sie zum Sperren und Überwachen von ausführbaren Dateien **Anwendungs- und Dienstprotokolle** > **Microsoft** > **Windows** > **Codeintegrität** > **Betrieb**.
2. Verwenden Sie zum Sperren und Überwachung von Windows Installer- und Skriptdateien **Anwendungs- und Dienstprotokolle** > **Microsoft** > **Windows** > **AppLocker** > **MSI and Script**.

<!--Reworked article to put this inline while working on VSO 1355092
## Automatically let software run if it is trusted by Intelligent Security Graph

You can let locked-down devices run software with a good reputation as determined by the Microsoft Intelligent Security Graph (ISG). The ISG includes [Windows Defender SmartScreen](/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview) and other Microsoft services. The devices must be running Windows Defender SmartScreen for this software to be trusted.

1. Open the **Create Windows Defender Application Policy** wizard.
2. On the **Inclusions** page, check the box for **Authorize software that is trusted by the Intelligent Security Graph**.
3. Click **Next** until the wizard completes.
-->


## <a name="security-and-privacy-information-for-windows-defender-application-control"></a>Informationen zu Sicherheit und Datenschutz für die Windows Defender-Anwendungssteuerung

- Wenden Sie in dieser Vorabversion keine Windows Defender-Anwendungssteuerungsrichtlinien mit dem Erzwingungsmodus **Nur überwachen** in einer Produktionsumgebung an. Dieser Modus ist nur dazu bestimmt, Ihnen beim Testen der Funktionen in einer Laborumgebung helfen.
- Geräte, auf denen eine Richtlinie im Modus **Nur überwachen** oder **Erzwingen aktiviert** bereitgestellt wurde und die noch nicht neu gestartet wurden, um die Richtlinie zu erzwingen, sind anfällig für die Installation nicht vertrauenswürdiger Software.
In diesem Fall kann die Software möglicherweise weiterhin ausgeführt werden, auch wenn das Gerät neu gestartet wird oder eine Richtlinie im Modus **Erzwingen aktiviert** empfängt.
- Bereiten Sie das Gerät in einer Laborumgebung vor, um sicherzustellen, dass die Windows Defender-Anwendungssteuerungsrichtlinie angewendet wird. Stellen Sie anschließend die Richtlinie **Erzwingung aktiviert** bereit. Starten Sie das Gerät abschließend neu, bevor Sie das Gerät dem Endbenutzer übergeben.
- Stellen Sie keine Richtlinie mit dem aktivierten Modus **Erzwingen aktiviert** und dann später eine Richtlinie mit **Nur überwachen** auf demselben Gerät bereit. Diese Konfiguration kann dazu führen, dass nicht vertrauenswürdige Software ausgeführt werden darf.
- Wenn Sie Configuration Manager verwenden, um die Windows Defender-Anwendungssteuerung auf Client-PCs zu aktivieren, werden Benutzer mit lokalen Administratorrechten nicht durch die Richtlinie daran gehindert, die Anwendungssteuerungsrichtlinien zu umgehen oder nicht vertrauenswürdige Software auf anderem Wege auszuführen. 
- Die einzige Möglichkeit zu verhindern, dass Benutzer mit lokalen Administratorrechten die Anwendungssteuerung deaktivieren, besteht darin, eine signierte binäre Richtlinie bereitzustellen. Diese Bereitstellung kann prinzipiell über eine Gruppenrichtlinie erfolgen, wird aber aktuell in Configuration Manager nicht unterstützt.
- Beim Einrichten von Configuration Manager als verwaltetes Installationsprogramm auf Client-PCs wird die AppLocker-Richtlinie verwendet. AppLocker wird nur zum Identifizieren verwalteter Installationsprogramme verwendet. Die gesamte Erzwingung erfolgt über die Windows Defender-Anwendungssteuerung. 

## <a name="next-steps"></a>Nächste Schritte

 [Verwalten von Firewalleinstellungen und Richtlinien für Antischadsoftware](endpoint-antimalware-firewall.md)