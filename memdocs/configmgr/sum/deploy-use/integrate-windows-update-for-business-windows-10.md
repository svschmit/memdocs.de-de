---
title: Integrieren von Windows Update for Business
titleSuffix: Configuration Manager
description: Verwenden Sie Windows Update for Business (WUfB), um Windows 10-Geräte, die mit Windows Update verbunden sind, auf dem neuesten Stand zu halten.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 04/07/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 183315fe-27bd-456f-b2c5-e8d25e05229b
ms.openlocfilehash: 8ea95a04977038514c00f0199df42c8070e813c3
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127653"
---
# <a name="integrate-with-windows-update-for-business"></a>Integrieren mit Windows Update for Business

*Gilt für: Configuration Manager (Current Branch)*

Mit Windows Update for Business (WUfB) können Sie Windows 10-Geräte in Ihrer Organisation hinsichtlich der neuesten Schutzmaßnahmen und Windows-Features auf dem neuesten Stand halten, wenn diese Geräte eine direkte Verbindung mit dem Windows Update-Dienst herstellen. Configuration Manager kann zwischen Windows 10-Computern unterscheiden, die WUfB und WSUS zum Abrufen von Softwareupdates verwenden.  

> [!WARNING]
> Wenn Sie die Co-Verwaltung für Ihre Geräte nutzen und die [Windows Update-Richtlinien](../../comanage/workloads.md#windows-update-policies) in Intune verschoben haben, erhalten Ihre Geräte die [Windows Update for Business-Richtlinien von Intune](https://docs.microsoft.com/intune/windows-update-for-business-configure).
> - Ist der Configuration Manager-Client noch auf dem gemeinsam verwalteten Gerät installiert, werden Einstellungen für kumulative Updates und Featureupdates von Intune verwaltet. Sind Patches von Drittanbietern in den [**Clienteinstellungen**](../../core/clients/deploy/about-client-settings.md#enable-third-party-software-updates) aktiviert, werden sie weiterhin von Configuration Manager verwaltet.  

 Einige Configuration Manager-Features sind nicht mehr verfügbar, wenn Configuration Manager-Clients so konfiguriert sind, dass sie Updates von Windows Update empfangen, was Windows Update for Business (WUfB) oder Windows Insider einbezieht:  

- Windows Update-Berichterstellung zur Kompatibilität:  
  - Configuration Manager wird nicht über die Updates informiert, die auf Windows Update veröffentlicht werden. Die Configuration Manager-Clients, die für den Empfang von Updates von WU konfiguriert sind, zeigen für diese Updates in der Configuration Manager-Konsole **Unbekannt** an.  

  - Die Problembehandlung für den gesamten Konformitätsstatus ist schwierig, weil der Status **Unbekannt** nur für Clients galt, die keinen Überprüfungsstatus von WSUS zurückgemeldet haben. Jetzt werden auch Configuration Manager-Clients einbezogen, die Updates von Windows Update erhalten.  

  - Die Konformität der Definitionsupdates ist Teil der gesamten Berichterstellung zur Updatekonformität und funktioniert auch nicht wie erwartet.

- Die allgemeine Endpoint Protection-Berichterstellung für Defender, die auf dem Status der Updatekonformität basiert, zeigt aufgrund der fehlenden Überprüfungsdaten keine exakten Ergebnisse an.  

- Configuration Manager kann keine Microsoft-Updates beispielsweise für Microsoft 365-Apps, Internet Explorer und Visual Studio auf Clients bereitstellen, die zum Abrufen von Updates mit WUfB verbunden sind.  

- Configuration Manager kann weiterhin in WSUS veröffentlichte und über Configuration Manager verwaltete Updates von Drittanbietern für Clients bereitstellen, die für den Empfang von Updates mit WUfB verbunden sind. Wenn Updates von Drittanbietern nicht auf Clients installiert werden sollen, die mit WUfB verbunden sind, deaktivieren Sie die Clienteinstellung [Softwareupdates auf Clients aktivieren](../../core/clients/deploy/about-client-settings.md#software-updates).

- Die vollständige Clientbereitstellung von Configuration Manager, die die Softwareupdateinfrastruktur verwendet, funktioniert nicht für Clients, die für den Empfang von Updates mit WUfB verbunden sind.  

## <a name="identify-clients-that-use-wufb-for-windows-10-updates"></a>Identifizieren von Clients, die WUfB für Windows 10-Updates verwenden

Mit den folgenden Schritten ermitteln Sie Clients, die zum Abrufen von Windows 10-Updates und -Upgrades WUfB verwenden. Anschließend konfigurieren Sie diese Clients so, dass sie zum Abrufen von Updates nicht mehr WSUS verwenden, und stellen eine Einstellung für den Client-Agent bereit, um den Softwareupdateworkflow für diese Clients zu deaktivieren.  

### <a name="prerequisites-for-wufb"></a>Voraussetzungen für WUfB

- Clients, die Windows 10 Desktop Pro oder Windows 10 Enterprise Edition Version 1511 oder höher ausführen

- [Windows Update for Business](https://docs.microsoft.com/windows/deployment/update/waas-manage-updates-wufb) wird bereitgestellt und die Clients verwenden WUfB zum Abrufen von Windows 10-Updates und -Upgrades.  

### <a name="to-identify-clients-that-use-wufb"></a>So identifizieren Sie Clients, die WUfB verwenden  

1. Vergewissern Sie sich, dass der Windows Update-Agent nicht WSUS abfragt, wenn diese Option zuvor aktiviert wurde. Der folgende Registrierungsschlüssel kann verwendet werden, um anzugeben, ob der Computer WSUS oder Windows Update abfragt. Wenn der Registrierungsschlüssel nicht vorhanden ist, wird WSUS nicht abgefragt.
    - **HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate\AU\UseWUServer**
1. Im Ressourcen-Explorer von Configuration Manager befindet sich unter dem Knoten **Windows Update** das neue Attribut **UseWUServer**.
1. Erstellen Sie eine Sammlung auf Basis des **UseWUServer** -Attributs für alle Computer, die für Updates und Upgrades über WUfB verbunden sind. Mithilfe einer Abfrage, die der folgenden ähnlich ist, können Sie eine Sammlung erstellen:  

    ```wql
    Select sr.* from SMS_R_System as sr join SMS_G_System_WINDOWSUPDATE as su on sr.ResourceID=su.ResourceID where su.UseWUServer is null
    ```

1. Erstellen Sie eine Client-Agent-Einstellung zur Deaktivierung des Workflows für das Softwareupdate. Stellen Sie die Einstellung für die Sammlung von Computern bereit, die direkt mit WUfB verbunden sind.
1. Die Computer, die über WUfB verwaltet werden, zeigen als Kompatibilitätsstatus **Unbekannt** an und werden im Gesamtprozentsatz der Kompatibilität nicht berücksichtigt.  

## <a name="configure-windows-update-for-business-deferral-policies"></a>Konfigurieren von Windows Update for Business-Zurückstellungsrichtlinien
<!-- 1290890 -->
Ab Version 1706 des Configuration Manager können Sie Zurückstellungsrichtlinien für Funktions- oder Qualitätsupdates für Windows 10-Geräte konfigurieren, die von Windows Update for Business direkt verwaltet werden. Sie können die Zurückstellungsrichtlinien im neuen Knoten **Windows Update for Business-Richtlinien** unter **Softwarebibliothek** > **Windows 10-Wartung** verwalten.

> [!NOTE]
> Ab Configuration Manager Version 1802 können Sie Rückstellungsrichtlinien für Windows-Insider festlegen. <!--507201-->  
Weitere Informationen zum Windows-Insider-Programm finden Sie unter [Erste Schritte mit dem Windows-Insider-Programm für Unternehmen](https://docs.microsoft.com/windows/deployment/update/waas-windows-insider-for-business).

### <a name="prerequisites-for-deferral-policies"></a>Voraussetzungen für Zurückstellungsrichtlinien

- Windows 10, Version 1703 oder höher
- Windows 10-Geräte, die von Windows Update for Business verwaltet werden, benötigen Internetzugriff.

#### <a name="to-create-a-windows-update-for-business-deferral-policy"></a>Sie erstellen Sie eine Windows Update for Business-Zurückstellungsrichtlinie

1. In **Softwarebibliothek** > **Windows 10-Wartung** > **Windows Update for Business-Richtlinien**
1. Wählen Sie auf der Registerkarte **Start** in der Gruppe **Erstellen** die Option **Windows Update for Business-Richtlinie erstellen** aus, um den Assistenten für das Erstellen von Windows Update for Business-Richtlinien zu öffnen.
1. Geben Sie auf der Seite **Allgemein** einen Namen und eine Beschreibung für die Richtlinie ein.
1. Konfigurieren Sie auf der Seite **Zurückstellungsrichtlinien**, ob Sie Funktionsupdates zurückstellen oder anhalten möchten. Funktionsupdates bieten in der Regel neue Funktionen für Windows. Nach dem Konfigurieren der Einstellung **Branchbereitschaftsniveau** können Sie dann festlegen, ob und wie lange Sie das Empfangen von Funktionsupdates zurückstellen möchten, sobald diese verfügbar sind.
    - **Branchbereitschaftsniveau:** Legen Sie den Branch fest, für den das Gerät Windows-Updates erhält. Wählen Sie „Halbjährlicher Kanal (gezielt)“, „Halbjährlicher Kanal“ oder einen Windows Insider-Build aus.

        > [!NOTE]
        > Stellen Sie Richtlinien für **Halbjährlicher Kanal (gezielt)** für Windows 10, *Version 1903 oder höher* bereit. Stellen Sie Richtlinien für **Halbjährlicher Kanal** für Windows 10, *Version 1809 oder früher* bereit.
        >
        > Wenn Sie eine Richtlinie für **Halbjährlichen Kanal** für Windows 10, Version 1903 oder höher, bereitstellen, tritt bei der Bereitstellung ein Fehler auf: **0x8004100c**.<!-- 5593139 -->

    - **Zurückstellungszeitraum (Tage):**  Geben Sie die Anzahl der Tage an, die Funktionsupdates verzögert werden. Sie können den Empfang dieser Funktionsupdates für einen Zeitraum von bis zu 365 Tagen nach ihrer Veröffentlichung verzögern.
    - **Anhalten von Funktionsupdates ab:** Wählen Sie aus, ob Sie das Empfangen von Funktionsupdates für bis zu 35 Tage ab dem von Ihnen angegebenen Zeitpunkt anhalten möchten. Nach Ablauf der maximalen Anzahl von Tagen läuft die Anhaltefunktion automatisch ab, sodass das Gerät in Windows Update nach in Frage kommenden Updates sucht. Nach diesem Suchvorgang können Sie die Updates erneut anhalten. Sie können das Anhalten von Funktionsupdates beenden, indem Sie das Kontrollkästchen deaktivieren.
1. Wählen Sie aus, ob Qualitätsupdates zurückgestellt oder angehalten werden sollen. Qualitätsupdates sind meist Korrekturen und Verbesserungen an vorhandener Windows-Funktionalität und werden in der Regel am ersten Dienstag jedes Monats veröffentlicht, wenngleich sie jederzeit von Microsoft veröffentlicht werden können. Sie können festlegen, ob und wie lange Sie Qualitätsupdates nach deren Verfügbarkeit zurückstellen möchten.
    - **Zurückstellungszeitraum (Tage):** Geben Sie die Anzahl der Tage an, um die Qualitätsupdates verzögert werden sollen. Sie können den Empfang dieser Qualitätsupdates für einen Zeitraum von 30 Tagen nach ihrer Veröffentlichung verzögern.
    - **Anhalten von Qualitätsupdates ab:** Wählen Sie aus, ob Sie das Empfangen von Qualitätsupdates für bis zu 35 Tage ab dem von Ihnen angegebenen Zeitpunkt anhalten möchten. Nach Ablauf der maximalen Anzahl von Tagen läuft die Anhaltefunktion automatisch ab, sodass das Gerät in Windows Update nach in Frage kommenden Updates sucht. Nach diesem Suchvorgang können Sie die Updates erneut anhalten. Sie können das Anhalten von Qualitätsupdates beenden, indem Sie das Kontrollkästchen deaktivieren.
1. Wählen Sie **Updates aus anderen Microsoft-Produkten installieren** aus, um die Gruppenrichtlinieneinstellung zu aktivieren, mit deren Hilfe Zurückstellungseinstellungen auf Microsoft Update sowie auf Windows-Updates angewendet werden können.
1. Wählen Sie **Treiber in Windows-Updates einschließen** aus, um Treiber automatisch über Windows-Updates zu aktualisieren. Wenn Sie diese Einstellung deaktivieren, werden Treiberupdates nicht von Windows-Updates heruntergeladen.
1. Schließen Sie den Assistenten ab, um die neue Zurückstellungsrichtlinie zu erstellen.

#### <a name="to-deploy-a-windows-update-for-business-deferral-policy"></a>So stellen Sie eine Windows Update for Business-Zurückstellungsrichtlinie bereit

1. In **Softwarebibliothek** > **Windows 10-Wartung** > **Windows Update for Business-Richtlinien**
1. Aktivieren Sie auf der Registerkarte **Start** in der Gruppe **Bereitstellung** die Option **Windows Update for Business-Richtlinie bereitstellen**.
1. Konfigurieren Sie die folgenden Einstellungen:
    - **Bereitzustellende Konfigurationsrichtlinie:** Wählen Sie die Windows Update for Business-Richtlinie aus, die Sie bereitstellen möchten.
    - **Sammlung:** Klicken Sie auf **Durchsuchen**, um die Sammlung auszuwählen, in der Sie die Richtlinie bereitstellen möchten.
    - **Wiederherstellung außerhalb des Wartungsfensters zulassen:** Wenn ein Wartungsfenster für die Sammlung konfiguriert wurde, für die Sie die Richtlinie bereitstellen, aktivieren Sie diese Option, um Richtlinieneinstellungen zum Wiederherstellen des Werts außerhalb des Wartungsfensters zuzulassen. Weitere Informationen zu Wartungsfenstern finden Sie unter [Verwenden von Wartungsfenstern](../../core/clients/manage/collections/use-maintenance-windows.md).
    - **Zeitplan:** Geben Sie den Zeitplan für die Auswertung der Konformität an, gemäß dem die bereitgestellte Richtlinie auf Clientcomputern ausgewertet wird. Dabei kann es sich um einen einfachen oder benutzerdefinierten Zeitplan handeln.
1. Schließen Sie den Assistenten ab, um die Richtlinie bereitzustellen.
