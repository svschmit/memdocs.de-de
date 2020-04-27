---
title: Neue Version 1710 | Microsoft-Dokumentation
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über Änderungen und neue Funktionen, die in Version 1710 von Configuration Manager eingeführt wurden.
ms.date: 01/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: bc6c3e5f-b9e2-400e-9d9d-446ff93c520c
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: 15735b015796d2cccfa9b0a24afc8f6eb0573df1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073618"
---
# <a name="what39s-new-in-version-1710-of-configuration-manager"></a>Neuerungen in Version 1710 von Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Das Update 1710 für Configuration Manager (Current Branch) ist als konsoleninternes Update für zuvor installierte Standorte verfügbar, die Version 1610, 1702 oder 1706 ausführen.

Neben neuen Features umfasst dieses Release auch weitere Änderungen, beispielsweise Fehlerbehebungen. Weitere Informationen finden Sie unter [Zusammenfassung der Änderungen im Current Branch von Configuration Manager, Version 1710](https://support.microsoft.com/help/4056470/summary-of-changes-in-system-center-configuration-manager-current-bran).

Die folgenden zusätzlichen Updates dieses Release sind jetzt ebenfalls verfügbar:
- [Updaterollup für die Current Branch-Version 1710 von Configuration Manager](https://support.microsoft.com/help/4057517/update-rollup-for-system-center-configuration-manager-current-branch-v)
- [Updaterollup 2 für die Current Branch-Version 1710 von Configuration Manager](https://support.microsoft.com/en-us/help/4086143/update-rollup-2-for-system-center-configuration-manager-current-branch)

> [!TIP]  
> Sie müssen eine Baselineversion von Configuration Manager verwenden, um einen neuen Standort zu installieren.  
>
> Weitere Informationen:    
> - [Installieren von neuen Standorten](../../servers/deploy/install/installing-sites.md)  
> - [Installieren von Updates an Standorten](../../servers/manage/updates.md)  
> - [Baseline- und Updateversionen](../../servers/manage/updates.md#bkmk_Baselines)

Die folgenden Abschnitte enthalten Details zu Änderungen und neuen Funktionen, die in Version 1710 von Configuration Manager eingeführt wurden.  

<!--
## Deprecated features and operating systems
Learn about support changes before they are implemented in [removed and deprecated items](deprecated/removed-and-deprecated.md).

Version 1710 drops support for the following products:
-->


## <a name="site-infrastructure"></a>Infrastruktur von Standorten

### <a name="updates-for-peer-cache-----sms500850---"></a>Updates für den Peercache  <!-- sms500850 -->
Ab dieser Version ist der Peercache keine Vorabfunktion mehr.  In dieser Version werden keine weiteren Änderungen am Peercache eingeführt. Weitere Informationen finden Sie unter [Peercache für Configuration Manager-Clients](../hierarchy/client-peer-cache.md).

### <a name="cloud-distribution-point-support-for-azure-government-cloud------sms491428---"></a>Unterstützung für Cloudverteilungspunkt für die Azure Government-Cloud   <!-- sms491428 -->
Sie können jetzt [cloudbasierte Verteilungspunkte](../hierarchy/use-a-cloud-based-distribution-point.md) in der Azure Government Cloud nutzen.   

### <a name="inventory-default-unit-revision----sms503697---"></a>Revision der Standardeinheit <!-- sms503697 -->
Da Geräte heutzutage über Festplatten verfügen, deren Größe in Gigabyte (GB), Terabyte (TB) oder noch größeren Einheiten angegeben werden, wird mit diesem Release die Standardeinheit (SMS_Units), die in vielen Ansichten verwendet wird, von Megabyte (MB) in GB geändert. Beispielsweise gibt der v_gs_LogicalDisk.FreeSpace-Wert jetzt GB-Einheiten zurück.


<!-- ## Migration  -->


## <a name="client-management"></a>Clientverwaltung

### <a name="co-management-for-windows-10-devices"></a>Co-Verwaltung für Windows 10-Geräte    
<!-- 1350871 -->
In den vorherigen Windows 10-Updates können Sie bereits ein Windows 10-Gerät gleichzeitig in eine lokale Active Directory-Installation (AD) und eine cloudbasierte Azure AD-Infrastruktur einbinden (Hybrid-Azure AD). Ab der Configuration Manager-Version 1710 nutzt die Co-Verwaltung diese Verbesserung und ermöglicht Ihnen, Windows 10-Geräte mit der Version 1709 (auch als „Fall Creators Update“ bezeichnet) gleichzeitig mit Configuration Manager und Intune zu verwalten. Diese Lösung schlägt eine Brücke von der herkömmlichen zur modernen Verwaltung und bietet Ihnen die Möglichkeit, die Umstellung schrittweise durchzuführen. Weitere Informationen finden Sie unter [Co-Verwaltung für Windows 10-Geräte](../../../comanage/overview.md).

### <a name="restart-computers-from-the-configuration-manager-console-----1356283---"></a>Neustarten von Computern über die Configuration Manager-Konsole  <!-- 1356283 -->
Ab diesem Release können Sie die Configuration Manager-Konsole verwenden, um Clientgeräte zu identifizieren, die einen Neustart erfordern, und diese Geräte dann mit einer Clientbenachrichtungsaktion neu starten.

Weitere Informationen finden Sie unter [Verwalten von Clients](../../clients/manage/manage-clients.md#restart-clients).


<!-- ## Compliance settings -->


## <a name="application-management"></a>Anwendungsverwaltung
### <a name="improvements-for-run-scripts------1236459---"></a>Verbesserungen für die Funktion „Skripts ausführen“   <!-- 1236459 -->
Diese Version bringt mehrere Verbesserungen für die Funktion **Skripts ausführen**, mit der Sie PowerShell-Skripts zur Ausführung auf verwalteten Geräten bereitstellen können. Diese Funktion wurde erstmals in Version 1706 eingeführt.

Es gibt folgende Verbesserungen:
- Sicherheitsbereiche zum Steuern, wer die Funktion „Skripts ausführen“ ausführen darf
- Überwachung der von Ihnen ausgeführten Skripts in Echtzeit
- Parameter für das Skript werden im Assistenten zum Erstellen von Skripts angezeigt, unterstützen die Validierung und sind als obligatorisch oder optional gekennzeichnet.

Weitere Informationen zur Funktion „Skripts ausführen“ finden Sie unter [Erstellen und Ausführen von Skripts](../../../apps/deploy-use/create-deploy-scripts.md).

### <a name="new-mobile-application-management-policy-settings"></a>Neue Richtlinieneinstellungen für die Verwaltung mobiler Anwendungen
<!-- 1324760 -->
Die folgenden Einstellungen wurden den Richtlinieneinstellung zur Verwaltung mobiler Anwendungen hinzugefügt:
- **Kontaktsynchronisierung deaktivieren**: Verhindert, dass die App Daten in der nativen App „Kontakte“ auf dem Gerät speichert.
- **Drucken deaktivieren**: Verhindert, dass die App Geschäfts-, Schul- oder Unidaten druckt.

### <a name="software-center-no-longer-distorts-icons-larger-than-250x250"></a>Das Softwarecenter verzerrt keine Symbole mehr, die größer als 250 x 250 Pixel sind  
<!-- 1356194 -->

Seit diesem Release werden Symbole, die größer als 250 x 250 Pixel sind, im Softwarecenter nicht mehr verzerrt dargestellt. In der Vergangenheit sahen sie im Softwarecenter unscharf aus. Von nun an können Sie Symbole mit bis zu 512 x 512 Pixel ohne Verzerrung darstellen.

Informationen zum Hinzufügen eines Symbols für Ihre App im Softwarecenter finden Sie unter [Erstellen von Anwendungen](../../../apps/deploy-use/create-applications.md).

## <a name="operating-system-deployment"></a>Betriebssystembereitstellung
 > [!TIP]   
 > <!-- 1354281 -->
 > Ab der Version 1709 von Windows 10 (auch bekannt als Fall Creators Update) umfasst Windows Media mehrere Editionen. Achten Sie beim Konfigurieren einer Tasksequenz für ein Betriebssystem-Upgradepaket oder ein Betriebssystemimage darauf, eine [Edition auszuwählen, die für Configuration Manager unterstützt wird](../configs/support-for-windows-10.md#windows-10-as-a-client).

### <a name="add-child-task-sequences-to-a-task-sequence"></a>Hinzufügen von untergeordneten Tasksequenzen zu einer Tasksequenz
<!-- 1261338 -->

Sie können einen neuen Tasksequenzschritt hinzufügen, der eine andere Tasksequenz ausführt, die eine Beziehung zwischen übergeordnetem/untergeordnetem Objekt zwischen den Tasksequenzen erstellt. Dadurch können Sie modularere Tasksequenzen erstellen, die Sie wiederverwenden können.  

Weitere Informationen zur untergeordneten Tasksequenz finden Sie unter [Untergeordnete Tasksequenz](../../../osd/understand/task-sequence-steps.md#child-task-sequence).

## <a name="software-center-customization"></a>Anpassen des Softwarecenters
<!-- 1351224 -->
Im Softwarecenter können Sie Brandingelemente Ihres Unternehmens hinzufügen und die Sichtbarkeit von Registerkarten festlegen. Sie können den im Softwarecenter verwendeten Namen Ihres Unternehmens hinzufügen sowie ein Farbschema für die Softwarecenter-Konfiguration, ein Unternehmenslogo und die sichtbaren Registerkarten für Clientgeräte festlegen.

Weitere Informationen finden Sie unter [Planen und Konfigurieren der Anwendungsverwaltung](../../../apps/plan-design/plan-for-and-configure-application-management.md).

## <a name="software-updates"></a>Softwareupdates

### <a name="surface-driver-updates-----1098490---"></a>Surface-Treiberupdates  <!-- 1098490 -->
Ab dieser Version das Verwalten von Surface-Treiberupdates kein Feature einer Vorabversion mehr.  


## <a name="reporting"></a>Berichterstellung

### <a name="limit-windows-10-enhanced-data-to-only-send-data-relevant-to-windows-analytics-device-health"></a>Begrenzen der bei der Einstellung „Erweitert“ unter Windows 10 gesendeten Daten auf die Daten, die für den Geräteintegritätsdienst von Windows Analytics relevant sind
<!-- 1356148 -->

Sie können jetzt für Diagnosedaten unter Windows 10 **Erweitert (begrenzt)** als Datensammlungsebene festlegen. Mit dieser Einstellung können Sie handlungsrelevante Informationen zu Geräten in Ihrer Umgebung gewinnen, ohne dass diese alle Daten auf der Stufe **Erweitert** an Windows 10-Version 1709 oder höher melden.

<!-- ## Inventory  -->


## <a name="mobile-device-management"></a>Verwaltung mobiler Geräte

### <a name="actions-for-non-compliance"></a>Aktionen bei Nichtkonformität 
<!--1321366 -->    
Sie können nun eine zeitlich geordnete Abfolge von Aktionen konfigurieren, die auf Geräte angewendet werden, die nicht konform sind. Beispielsweise können Sie Endbenutzer nicht konformer Geräte per E-Mail benachrichtigen oder diese Geräte als nicht konform kennzeichnen.

### <a name="windows-10-arm64-device-support"></a>Unterstützung für Windows 10 ARM64-Geräte
<!-- 1355000 -->

Hybridszenarien für die Verwaltung mobiler Geräte (Mobile Device Management, MDM) werden auf ARM64-Geräte mit Windows 10 unterstützt, sobald diese Geräte verfügbar sind.

### <a name="improved-vpn-profile-experience-in-configuration-manager-console"></a>Verbesserte Benutzeroberfläche für VPN-Profile in der Configuration Manager-Konsole 
<!-- 1318232 -->

Mit diesem Release wurden der Assistent zum Erstellen von VPN-Profilen und die VPN-Eigenschaftenseiten aktualisiert, sodass die Einstellungen der ausgewählten Plattform entsprechend angezeigt werden:


- Jede Plattform hat einen eigenen Workflow. Das bedeutet, dass neue VPN-Profile nur die von der jeweiligen Plattform unterstützte Einstellung enthalten.
- Nach der Seite **Allgemein** wird nun die Seite **Unterstützte Plattformen** angezeigt.  Ab sofort wählen Sie die Plattform aus, bevor Sie Eigenschaftswerte festlegen.
- Wenn die Plattform auf **Android**, **Android for Work** oder **Windows Phone 8.1** festgelegt wird, ist die Seite **Unterstützte Plattformen** nicht erforderlich und wird nicht angezeigt.
- Der auf dem Configuration Manager-Client basierende Workflow wurde mit den Workflows aus Windows 10 kombiniert, die auf dem Client für hybrid verwaltete mobile Geräte (MDM) basieren. Diese unterstützen alle dieselben Einstellungen.
- Jeder Plattformworkflow enthält nur die für diesen Workflow geeigneten Einstellungen.  Beispiel: Der Android-Workflow enthält die für Android geeigneten Einstellungen. Die Einstellungen für iOS oder Windows 10 Mobile werden nicht länger im Android-Workflow angezeigt.
- Die Seite „Automatisches VPN“ ist veraltet und wurde entfernt.

Diese Änderungen gelten für neue VPN-Profile.  

Um Kompatibilitätsrisiken zu minimieren, werden vorhandene VPN-Profile nicht geändert.  Wenn Sie ein vorhandenes Profil bearbeiten, werden die Einstellungen so wie bei der Profilerstellung angezeigt.  

Weitere Informationen finden Sie unter [VPN-Profile für mobile Geräte](../../../protect/deploy-use/vpn-profiles.md).

### <a name="limited-support-for-cryptography-next-generation-cng-certificates----1356191---"></a>Eingeschränkte Unterstützung für Kryptografie: Next Generation-Zertifikate (CNG) <!-- 1356191 -->

Configuration Manager bietet eingeschränkte Unterstützung für Cryptography CNG-Zertifikate (Cryptography Next Generation). Configuration Manager-Clients können das PKI-Clientauthentifizierungszertifikat mit dem privaten Schlüssel im CNG-Schlüsselspeicheranbieter (KSP) verwenden. Dank der KSP-Unterstützung unterstützen Configuration Manager-Clients hardwarebasierte private Schlüssel, wie z. B. TPM KSP für PKI-Clientauthentifizierungszertifikate.

Weitere Informationen finden Sie in der [Übersicht über CNG-Zertifikate](../network/cng-certificates-overview.md).

## <a name="protect-devices"></a>Schützen von Geräten

### <a name="create-and-deploy-exploit-guard-policies"></a>Erstellen und Bereitstellen von Exploit Guard-Richtlinien
<!-- 1355468 -->

Sie können [Richtlinien erstellen und bereitstellen](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md), die alle vier Komponenten von Windows Defender Exploit Guard verwalten, einschließlich der Verkleinerung der Angriffsfläche, des kontrollierten Ordnerzugriffs, des Schutzes vor Exploits und des Netzwerkschutzes.

### <a name="create-and-deploy-windows-defender-application-guard-policy"></a>Erstellen und Bereitstellen einer Windows Defender Application Guard-Richtlinie
<!-- 1351960 -->

Sie können [Windows Defender Application Guard](../../../protect/deploy-use/create-deploy-application-guard-policy.md)-Richtlinien erstellen und bereitstellen, indem Sie den Configuration Manager-Endpunktschutz verwenden.

### <a name="device-guard-policy-changes"></a>Änderungen an Device Guard-Richtlinien
<!-- 1355092 -->
Die folgenden drei Änderungen wurden an Device Guard-Richtlinien vorgenommen:

- Die Device Guard-Richtlinien wurden in Windows Defender-Anwendungssteuerungsrichtlinien umbenannt. Der **Assistent zum Erstellen von Device Guard-Richtlinien** heißt jetzt **Assistent zum Erstellen von Windows Defender-Anwendungssteuerungsrichtlinien**.
- Geräte mit dem Fall Creators Update für Windows-Version 1709 müssen nicht mehr neu gestartet werden, um die Windows Defender Application Control-Richtlinien anzuwenden. Der Neustart ist immer noch die Standardeinstellung. Sie können jedoch [Neustarts deaktivieren](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md).
- Sie können [Geräte für das automatische Ausführen von Software](../../../protect/deploy-use/use-device-guard-with-configuration-manager.md) einrichten, die von Intelligent Security Graph als vertrauenswürdig eingestuft wird.





## <a name="next-steps"></a>Nächste Schritte
Wenn Sie zum Installieren dieser Version bereit sind, sehen Sie sich [Updates für Configuration Manager](../../servers/manage/updates.md) an.
