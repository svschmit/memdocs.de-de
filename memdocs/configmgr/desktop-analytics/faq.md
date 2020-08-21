---
title: FAQ zu Desktop Analytics
titleSuffix: Configuration Manager
description: Hier werden häufig gestellte Fragen zu Desktop Analytics beantwortet.
ms.date: 02/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: e0db3311-2303-4013-a906-76b408172d3c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: b24369f2c2f21208f188cf5c0c2ef3a28db83c04
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700819"
---
# <a name="desktop-analytics-faq"></a>Desktop Analytics – FAQ

## <a name="prerequisites"></a>Voraussetzungen

### <a name="can-i-use-cloud-enabled-analytics-with-intune-managed-devices"></a><a name="bkmk_intune"></a> Kann ich cloudfähige Analysen mit von Intune verwalteten Geräten verwenden?

Derzeit ist dies noch nicht möglich. Aber sehen Sie sich in diesem Zusammenhang gerne die Ankündigung zur [erkenntnisgesteuerten Geräteverwaltung](https://myignite.techcommunity.microsoft.com/sessions/81690?source=sessions) von der Microsoft Ignite 2019 an. Diese geplante Lösung soll den Geräteintegritätsdienst und die Upgradebereitschaft ablösen.

Die Mehrzahl der Kunden, die vom Desktop Analytics-Workflow profitieren kann, verwendet Configuration Manager zum Bereitstellen von Windows. Wir wissen, dass Intune-Kunden die zusätzlichen Erkenntnisse aus den Analytics-Daten schätzen. Daher arbeiten wir an Möglichkeiten, diese Erkenntnisse mit ihnen zu teilen.

### <a name="its-been-over-72-hours-and-the-portal-is-still-processing-data-what-next"></a>Es dauert schon länger als 72 Stunden, und das Portal verarbeitet immer noch Daten – was sollte nun geschehen?

Nach dem erstmaligen Einrichten von Desktop Analytics zeigen die Berichte in Configuration Manager und im Desktop Analytics-Portal möglicherweise nicht sofort die kompletten Daten an. Es kann zwei bis drei Tage dauern, bis der Dienst die Daten verarbeitet hat. Wenn die Verarbeitung der Daten im Portal länger als 72 Stunden dauert, führen Sie die folgenden Schritte aus:

- Vergewissern Sie sich mit dem [Dashboard „Verbindungsintegrität“](monitor-connection-health.md), dass aktive Geräte ordnungsgemäß konfiguriert sind. Dieses Dashboard wird nicht in Echtzeit aktualisiert.
- Stellen Sie sicher, dass die Geräte Diagnosedaten an den Desktop Analytics-Dienst senden. Weitere Informationen finden Sie unter [Aktivieren der Datenfreigabe](enable-data-sharing.md).
- Stellen Sie [Azure AD-Anwendungen](troubleshooting.md#bkmk_AzureADApps) in Ihrer Azure AD-Instanz bereit.
- Überprüfen Sie die Geräte, die Sie in den letzten sieben Tagen mit Ihrer Organisation verknüpft haben. Wechseln Sie im [Desktop Analytics-Portal](https://aka.ms/desktopanalytics) zum Bereich **Verbundene Dienste**. Wählen Sie **Geräte registrieren** und **Aktuelle Daten anzeigen** aus.

  > [!IMPORTANT]
  > Die Desktop Analytics-Option **Aktuelle Daten anzeigen** ist veraltet. Diese Aktion wird in einer zukünftigen Version des Desktop Analytics-Diensts entfernt. Weitere Informationen finden Sie unter [Veraltete Features](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!--7080949-->  

Wenn die Geräte ordnungsgemäß konfiguriert sind und Sie weiterhin keine Daten in Ihrem Arbeitsbereich sehen, [kontaktieren Sie den Microsoft-Support](https://support.microsoft.com/hub/4343728/support-for-business).

## <a name="connect-configuration-manager"></a>Herstellen einer Verbindung mit Configuration Manager

### <a name="can-i-change-the-target-or-additional-collections"></a>Kann ich das Ziel oder zusätzliche Sammlungen ändern?

Ja. Führen Sie dazu den folgenden Vorgang aus:

- Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie den Eintrag **Clouddienste**, und wählen Sie anschließend den Knoten **Azure-Dienste** aus. Öffnen Sie die Eigenschaften für den Eintrag, der dem Desktop Analytics-Dienst zugeordnet ist.

- Ändern Sie auf der Registerkarte **Desktop Analytics-Verbindung** die **Zielsammlung**, oder verwalten Sie die zusätzlichen Sammlungen.

<!-- 7130169 -->
> [!Note]
> Fügen Sie nicht mehr als 20 Sammlungen in die Liste der zusätzlichen Sammlungen ein. Seien Sie vorsichtig bei der Gesamtanzahl der Geräte in jeder Sammlung. Schließen Sie immer Ihre [include- und exclude-Sammlungen des globalen Piloten](deploy-pilot.md#bkmk_GlobalPilot) ein.  

> [!IMPORTANT]  
> Configuration Manager verwendet eine Richtlinie für Einstellungen, um Geräte in der Zielsammlung zu konfigurieren. Diese Richtlinie enthält die Einstellungen für Diagnosedaten, um Geräten das Senden von Daten an Microsoft zu ermöglichen. Wenn Sie die Zielsammlung ändern, wird nicht die Einstellungsrichtlinie für Geräte aufgehoben, die nicht mehr in der Zielsammlung enthalten sind. Wenn Ihre Geräte nicht weiterhin Diagnosedaten senden sollen, müssen Sie die [Geräte neu konfigurieren](account-close.md#reconfigure-clients).

## <a name="windows-upgrade"></a>Windows-Upgrade

### <a name="can-i-upgrade-windows-and-change-architecture"></a>Kann ich ein Upgrade von Windows ausführen und die Architektur ändern?

Desktop Analytics ist auf die optimale Unterstützung von direkten Upgrades ausgelegt. Bei direkten Upgrades sind Migrationen von einer 32-Bit-Architektur zu einer 64-Bit-Architektur nicht möglich. Wenn Sie Computer in einem solchen Szenario migrieren müssen, verwenden Sie das Aktualisierungsszenario. Erkenntnisse von Desktop Analytics sind auch in diesem Szenario hilfreich, Sie können jedoch auf ein Upgrade bezogene Empfehlungen ignorieren.

Weitere Informationen finden Sie unter [Aktualisieren eines vorhandenen Computers mit einer neuen Version von Windows](../osd/deploy-use/refresh-an-existing-computer-with-a-new-version-of-windows.md).

### <a name="can-i-change-from-bios-to-uefi-when-upgrading-windows"></a>Kann ich beim Upgrade von Windows von BIOS zu UEFI wechseln?

Ja. Weitere Informationen finden Sie unter [Konvertieren von BIOS zu UEFI während eines direkten Upgrades](../osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion.md#bkmk_ipu).

### <a name="can-i-use-desktop-analytics-with-windows-10-ltsc"></a>Kann ich Desktop Analytics mit Windows 10-LTSC verwenden?

Desktop Analytics unterstützt keine Windows 10 Long-Term Servicing Channel-Geräte (LTSC). Weitere Informationen finden Sie unter [Übersicht über Windows-as-a-Service](/windows/deployment/update/waas-overview#long-term-servicing-channel).

### <a name="can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal"></a>Kann ich die Zeit verkürzen, die für das Aktualisieren von Daten in meinem Desktop Analytics-Portal benötigt wird?

Es gibt zwei Arten von Daten im Desktop Analytics-Portal: Administratordaten und Diagnosedaten. Um Administratordaten bei Bedarf zu aktualisieren, öffnen Sie das Flyout zur Datenaktualität, und wählen Sie **Änderungen übernehmen** aus. Durch diese Aktion wird sofort eine einmalige Aktualisierung der ausstehenden Änderungen von Administratordaten in Ihren Arbeitsbereichen ausgelöst. Die Änderungen werden weitergegeben und sind innerhalb von 15-60 Minuten allgemein verfügbar. Die Dauer hängt von der Größe Ihres Arbeitsbereichs und vom Umfang der ausstehenden Änderungen ab. Sie können eine Datenaktualisierung bei Bedarf bis zu sechs Mal innerhalb von 24 Stunden anfordern.

Sämtliche Daten werden automatisch einmal täglich aktualisiert, auch wenn Sie keine Datenaktualisierung nach Bedarf anfordern. Es gibt keine Möglichkeit, eine bedarfsgesteuerte Aktualisierung von Diagnosedaten auszulösen. Weitere Informationen zu den verschiedenen Arten von Daten in Desktop Analytics finden Sie unter [Datenlatenz](troubleshooting.md#data-latency).

## <a name="privacy"></a>Datenschutz

### <a name="can-desktop-analytics-be-used-without-a-direct-client-connection-to-the-microsoft-data-management-service"></a>Kann Desktop Analytics ohne direkte Clientverbindung mit dem Microsoft-Datenverwaltungsdienst verwendet werden?

Nein, der gesamte Dienst basiert auf Windows-Diagnosedaten, und diese erfordern, dass Geräte über eine solche direkte Verbindung verfügen.

### <a name="can-i-choose-the-data-center-location"></a>Kann ich den Ort des Rechenzentrums auswählen?

Für Azure Log Analytics: Ja, wenn Sie Desktop Analytics einrichten und den Log Analytics-Arbeitsbereich erstellen.

Für den Microsoft-Datenverwaltungsdienst und Azure Storage Analytics: Nein, diese beiden Dienste werden in den USA gehostet.

### <a name="where-is-my-organizations-data-stored"></a>Wo werden die Daten meiner Organisation gespeichert?

Windows-Diagnosedaten von ihren Computern werden verschlüsselt und an von Microsoft verwaltete, sichere Rechenzentren in den USA gesendet, wo sie verarbeitet werden. Microsoft übermittelt die Analyse der auf Desktop Analytics bezogenen Daten über die Desktop Analytics-Lösung im Azure-Portal an Sie. Desktop Analytics wird in den meisten Regionen unterstützt, in denen [Log Analytics verfügbar ist](https://azure.microsoft.com/global-infrastructure/services/?products=monitor&regions=all). Wenn Sie eine Azure-Region in einem anderen Land auswählen, werden Ihre Diagnosedaten dennoch an die sicheren Microsoft-Rechenzentren in den USA gesendet und dort verarbeitet.

## <a name="existing-windows-analytics-customers"></a>Vorhandene Windows Analytics-Kunden

> [!Important]  
> Der Windows Analytics-Dienst wurde am 31. Januar 2020 eingestellt.
>
> Weitere Informationen finden Sie unter [KB 4521815: Windows Analytics-Deaktivierung am 31. Januar 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).

### <a name="can-i-use-update-compliance-together-with-desktop-analytics"></a>Kann ich Updatekonformität zusammen mit Desktop Analytics verwenden?

Ja. Wenn Sie derzeit [Updatekonformität](/windows/deployment/update/update-compliance-get-started) im Azure-Portal verwenden, können Sie dies auch weiterhin und nach dem Januar 2020 tun.

Weitere Informationen finden Sie unter [KB 4521815: Windows Analytics-Deaktivierung am 31. Januar 2020](https://support.microsoft.com/help/4521815/windows-analytics-retirement).

### <a name="are-there-any-windows-analytics-features-that-arent-available-in-desktop-analytics"></a>Gibt es Windows Analytics-Funktionen, die in Desktop Analytics nicht verfügbar sind?

<!-- 3616924 -->
Ja, die folgenden Windows Analytics-Features wurden entweder eingestellt oder sind in Desktop Analytics noch nicht verfügbar:

#### <a name="general"></a>Allgemein

- Unterstützung für Szenarios, für die Configuration Manager nicht erforderlich ist. Ein Beispiel ist die [Intune-Unterstützung](#bkmk_intune).
- Erforderliche Lizenzierung mit einer gültigen Windows-Lizenz versus E3, E5
- Unterstützung für mehrere Arbeitsbereiche pro Azure AD-Mandant
- Möglichkeit, benutzerdefinierte Abfragen auszuführen und Lösungsrohdaten zu exportieren
- Datenmodelldokumentation für benutzerdefinierte Berichte

#### <a name="upgrade-readiness"></a>Upgradebereitschaft

- Internet Explorer-Site-Discovery-Daten
- Erkenntnisse von Add-Ins für Microsoft 365-Apps (jetzt [in Configuration Manager verfügbar](#bkmk_office))
- Erkenntnisse aus Feedback-Hub

#### <a name="update-compliance"></a>Updatekonformität

- Unterstützung von Windows Update for Business
- Erkenntnisse aus Übermittlungsoptimierung
- Unterstützung für Windows 10-LTSC (Long-Term Servicing Channel)
- Windows-Insider-Berichte
- Windows Defender-Status

> [!Note]
> Alle vorhandenen Features der Updatekonformität, einschließlich der in Desktop Analytics nicht verfügbaren, sind in der [Updatekonformität](/windows/deployment/update/update-compliance-get-started)-Lösung im Azure-Portal weiterhin verfügbar.

#### <a name="device-health"></a>Geräteintegrität

- Treiberintegrität
- App-Integrität (außerhalb eines Bereitstellungsplans)
- Häufig abstürzende Geräte oder durch Treiber verursachte Abstürze
- Integrität der Windows-Anmeldung
- Windows Information Protection
- Unterstützung für Windows Server

## <a name="other"></a>Andere

### <a name="can-i-use-desktop-analytics-for-my-microsoft-365-apps-upgrades"></a><a name="bkmk_office"></a> Kann ich Desktop Analytics für meine Upgrades für Microsoft 365-Apps verwenden?

Nein, der Schwerpunkt von Desktop Analytics liegt auf Windows. Microsoft hat Desktop Analytics in enger Zusammenarbeit mit vielen Kunden entwickelt. Das Kundenfeedback hat dazu beigetragen, dass Desktop Analytics ihre Möglichkeiten zur zuverlässigen Verwaltung von Windows-Bereitstellungen verbessert. Kunden haben uns zudem darauf hingewiesen, dass die [Bereitschaft für Microsoft 365-Apps](../sum/deploy-use/office-365-dashboard.md#bkmk_o365_readiness) enger in Verwaltungstools für Microsoft 365-Apps in Configuration Manager und Intune integriert werden sollte. Microsoft unternimmt weiter Anstrengungen in diesen Bereichen, konzentriert sich aber in Desktop Analytics auf Windows-Szenarios.

### <a name="how-can-i-provide-feedback-about-desktop-analytics"></a>Wie kann ich Feedback zu Desktop Analytics übermitteln?

Wenn Sie Ihr Feedback zu Desktop Analytics teilen möchten, wählen Sie oben im Portal das Symbol **Lächeln senden** aus. Schließen Sie auch einen Screenshot ein, damit Microsoft Ihr Feedback besser verstehen kann. Sie können auch Produktvorschläge einreichen und auf [UserVoice](https://configurationmanager.uservoice.com/forums/300492-ideas?category_id=366805) über andere Ideen abstimmen.

> [!Note]
> Übermitteln Sie über „Lächeln senden“ oder UserVoice nie private Informationen. Zu solchen privaten Informationen zählen Ihre Mandanten-ID und ihre kommerzielle ID. Microsoft bietet über die Kanäle „Lächeln senden“ und UserVoice keine Supportleistungen. Wenn Sie Hilfe zu Ihrem Desktop Analytics-Arbeitsbereich benötigen, wählen Sie im Navigationsmenü den Link **Hilfe und Support** aus, um ein Supportticket zu öffnen.