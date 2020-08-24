---
title: Konfigurieren von Microsoft Defender ATP in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Konfigurieren Sie Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) in Intune, einschließlich Herstellen einer Verbindung mit ATP, Integrieren von Geräten per Onboarding, Zuweisen von Konformität für Risikostufen und Einrichten von Richtlinien für den bedingten Zugriff.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/12/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ad02078d2a8b9926de463e01d3dcbc675c721e4a
ms.sourcegitcommit: d1bfd5b8481439babc7eae43493f28edaebe647a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179518"
---
# <a name="configure-microsoft-defender-atp-in-intune"></a>Konfigurieren von Microsoft Defender ATP in Intune

Die Informationen und Verfahren in diesem Artikel unterstützen Sie dabei, die Integration von Microsoft Defender ATP in Intune zu konfigurieren. Die Konfiguration umfasst die folgenden allgemeinen Schritte:

- Aktivieren von Microsoft Defender ATP für Ihren Mandanten
- Integrieren von Geräten unter Windows und Android
- Verwenden von Konformitätsrichtlinien zum Festlegen von Geräterisikostufen
- Verwenden von Richtlinien für den bedingten Zugriff zum Blockieren von Geräten, die Ihre erwarteten Risikostufen überschreiten

Bevor Sie beginnen, muss Ihre Umgebung die [Voraussetzungen](../protect/advanced-threat-protection.md#prerequisites) für die Verwendung von Microsoft Defender ATP in Intune erfüllen.

## <a name="enable-microsoft-defender-atp-in-intune"></a>Aktivieren von Microsoft Defender ATP in Intune

Der erste Schritt ist das Einrichten einer Dienst-zu-Dienst-Verbindung zwischen Intune und Microsoft Defender ATP. Richten Sie Administratorzugriff auf Microsoft Defender Security Center und Intune ein.

Sie müssen Microsoft Defender ATP nur einmal pro Mandant aktivieren.

### <a name="to-enable-microsoft-defender-atp"></a>Aktivieren von Microsoft Defender ATP

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Endpunktsicherheit** > **Microsoft Defender ATP** aus und dann **Microsoft Defender Security Center öffnen**.

   ![Wählen Sie die Option zum Öffnen von Microsoft Defender Security Center aus.](./media/advanced-threat-protection-configure/atp-device-compliance-open-microsoft-defender.png)

3. In **Microsoft Defender Security Center**:
   1. Wählen Sie **Einstellungen** > **Erweiterte Features** aus.
   2. Wählen Sie für **Microsoft Intune-Verbindung** die Option **Ein** aus:

      ![Aktivieren der Verbindung mit Intune](./media/advanced-threat-protection-configure/atp-security-center-intune-toggle.png)

   3. Wählen Sie **Voreinstellungen speichern** aus.

4. Kehren Sie im Microsoft Endpoint Manager Admin Center zu **Microsoft Defender ATP** zurück. Unter **Einstellungen für die MDM-Konformitätsrichtlinie**, je nach den Anforderungen Ihres Unternehmens:
   - Legen Sie **Windows-Geräte der Version 10.0.15063 und höher mit „Microsoft Defender ATP“ verbinden** auf **Ein** fest.
   - Legen Sie **Android-Geräte der Version 6.0.0 und höher mit Microsoft Defender ATP verbinden** auf **Ein** fest.

5. Wählen Sie **Speichern** aus.

> [!TIP]
> Wenn Sie eine neue Anwendung in Intune Mobile Threat Defense integrieren und die Verbindung mit Intune aktivieren, erstellt Intune eine klassische Richtlinie für den bedingten Zugriff in Azure Active Directory. Jede MTD-App, die Sie integrieren (einschließlich [Microsoft Defender ATP](advanced-threat-protection.md) oder jedes unserer zusätzlichen [MTD-Partner](mobile-threat-defense.md#mobile-threat-defense-partners)), erstellt eine neue klassische Richtlinie für bedingten Zugriff. Diese Richtlinien können ignoriert werden, dürfen jedoch nicht bearbeitet, gelöscht oder deaktiviert werden.
>
> Wenn die klassische Richtlinie gelöscht wird, müssen Sie die zur Erstellung dieser Richtlinie verantwortliche Verbindung mit Intune löschen und anschließend erneut einrichten. Auf diese Weise wird die klassische Richtlinie neu erstellt. Es wird keine Unterstützung für die Migration klassischer Richtlinien für MTD-Apps zum neuen Richtlinientyp für bedingten Zugriff bereitgestellt.
>
> Klassische bedingte Zugriffsrichtlinien für MTD-Apps:
>
> - Sie werden von Intune MTD verwendet und verlangen, dass Geräte in Azure AD registriert werden, damit sie eine Geräte-ID erhalten, bevor Kommunikation mit MTD-Partnern erfolgt. Die ID ist erforderlich, damit Geräte ihren Status erfolgreich an Intune melden können.
> - Sie haben keine Auswirkung auf andere Cloud-Apps oder Ressourcen.
> - Die Zugriffsrichtlinien unterscheiden sich von Richtlinien für bedingten Zugriff, die Sie möglicherweise erstellen, damit sie Ihnen bei der Verwaltung von MTD helfen.
> - Standardmäßig interagieren sie nicht mit anderen Richtlinien für den bedingten Zugriff, die Sie für die Auswertung verwenden.
>
> Wenn Sie klassische Richtlinien für den bedingten Zugriff in [Azure](https://portal.azure.com/#home) anzeigen möchten, wechseln Sie zu **Azure Active Directory** > **Bedingter Zugriff** > **Klassische Richtlinien**.

## <a name="onboard-devices"></a>Integrieren von Geräten

Als Sie die Unterstützung für Microsoft Defender ATP in Intune aktiviert haben, haben Sie eine Dienst-zu-Dienst-Verbindung zwischen Intune und Microsoft Defender ATP eingerichtet. Sie können Geräte in Microsoft Defender ATP integrieren, die Sie mit Intune verwalten, um die Erfassung von Daten zu Risikostufen auf den Geräten zu ermöglichen.

### <a name="onboard-windows-devices"></a>Integrieren von Windows-Geräten

Als Sie die Verbindung zwischen Intune und Microsoft Defender ATP hergestellt haben, hat Intune ein Microsoft Defender ATP-Onboardingkonfigurationspaket von Microsoft Defender ATP empfangen. Dieses Konfigurationspaket stellen Sie mithilfe eines Gerätekonfigurationsprofils für Microsoft Defender ATP auf Ihren Windows-Geräten bereit.

Das Konfigurationspaket konfiguriert Geräte für die Kommunikation mit [Microsoft Defender ATP-Diensten](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection), um Dateien zu überprüfen und Bedrohungen zu erkennen. Die Geräte melden Microsoft Defender ATP auch die Geräterisikostufe, basierend auf den von Ihnen erstellten Konformitätsrichtlinien.

Nachdem Sie ein Gerät über das Konfigurationspaket integriert haben, müssen Sie dies nicht erneut tun. Sie können das Onboarding von Geräten auch mit einer [Gruppenrichtlinie oder Microsoft Endpoint Configuration Manager](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints) durchführen.

### <a name="create-the-device-configuration-profile-to-onboard-windows-devices"></a>Erstellen des Gerätekonfigurationsprofils zum Integrieren von Windows-Geräten

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.
3. Wählen Sie unter **Plattform** die Option **Windows 10 und höher** aus.
4. Wählen Sie für **Profiltyp** die Option **Microsoft Defender ATP (Windows 10 Desktop)** und dann **Erstellen** aus.
5. Geben Sie auf der Seite **Grundeinstellungen** einen *Namen* und eine *Beschreibung* (optional) für das Profil ein, und wählen Sie dann **Weiter** aus.
6. Konfigurieren Sie auf der Seite **Einstellungen** Folgendes:

   - **Pakettyp für die Microsoft Defender ATP-Clientkonfiguration**: Wählen Sie **Onboarding** aus, um das Konfigurationspaket zum Profil hinzuzufügen. Klicken Sie auf **Offboard** (Integration aufheben), um das Konfigurationspaket aus dem Profil zu entfernen.
  
     > [!NOTE]
     > Wenn Sie eine ordnungsgemäße Verbindung mit Microsoft Defender ATP hergestellt haben, führt Intune automatisch ein **Onboarding** für das Konfigurationsprofil für Sie durch, und die Einstellung **Pakettyp für die Microsoft Defender ATP-Clientkonfiguration** ist nicht verfügbar.
  
   - **Beispielfreigabe für alle Dateien**: Durch das **Aktivieren** dieser Option werden Stichproben erfasst und mit Microsoft Defender ATP geteilt. Wenn Sie z. B. eine verdächtige Datei sehen, können Sie sie zur gründlichen Analyse an Microsoft Defender ATP senden. Wenn **Nicht konfiguriert** festgelegt ist, werden keine Stichproben mit Microsoft Defender ATP geteilt.
   - **Häufigkeit von Telemetrieberichten erhöhen**: Bei Geräten mit hohem Risiko werden durch das **Aktivieren** dieser Option häufiger Telemetriedaten an den Microsoft Defender ATP-Dienst gemeldet.

     [Onboarding von Windows 10-Computern mit Configuration Manager](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-sccm) enthält nähere Informationen zu diesen Microsoft Defender ATP-Einstellungen.

7. Wählen Sie **Weiter** aus, um die Seite **Bereichstags** zu öffnen. Bereichstags sind optional. Wählen Sie **Weiter** aus, um den Vorgang fortzusetzen.

8. Wählen Sie auf der Seite **Zuweisungen** die Gruppen aus, die dieses Profil erhalten sollen. Weitere Informationen zum Zuweisen von Profilen finden Sie unter [Zuweisen von Benutzer- und Geräteprofilen](../configuration/device-profile-assign.md).

   Wählen Sie **Weiter** aus.

9. Klicken Sie, wenn Sie fertig sind, auf der Seite **Bewerten + erstellen** auf **Erstellen**. Das neue Profil wird in der Liste angezeigt, wenn Sie den Richtlinientyp für das Profil auswählen, das Sie erstellt haben.
 **OK**, und dann **Erstellen**, um Ihre Änderungen zu speichern. Dadurch wird das Profil erstellt.

### <a name="onboard-android-devices"></a>Durchführen des Onboardings für Android-Geräte

Nachdem Sie die Dienst-zu-Dienst-Verbindung zwischen Intune und Microsoft Defender ATP eingerichtet haben, können Sie Android-Geräte per Onboarding in Microsoft Defender Android ATP integrieren. Beim Onboarding werden Geräte für die Kommunikation mit Defender ATP konfiguriert, und ATP erfasst dann Daten zur Risikostufe der Geräte.

Anders als bei Windows-Geräten gibt es für Geräte unter Android kein Konfigurationspaket. Informationen zu Voraussetzungen und Onboardinganweisungen für Android finden Sie in der Dokumentation zu Microsoft Defender ATP unter [Übersicht über Microsoft Defender ATP für Android](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-android).

Bei Android-Geräten können Sie auch eine Intune-Richtlinie verwenden, um Microsoft Defender ATP unter Android zu ändern. Weitere Informationen finden Sie unter [Webschutz in Microsoft Defender ATP](../protect/advanced-threat-protection-manage-android.md).

## <a name="create-and-assign-compliance-policy-to-set-device-risk-level"></a>Erstellen und Zuweisen von Konformitätsrichtlinien zum Festlegen der Risikostufe für Geräte

Die Konformitätsrichtlinie bestimmt für Windows- und Android-Geräte die Risikostufe, die Sie für ein Gerät als akzeptabel einstufen.

Wenn Sie mit dem Erstellen von Konformitätsrichtlinien nicht vertraut sind, lesen Sie den Abschnitt [Erstellen der Richtlinie](../protect/create-compliance-policy.md#create-the-policy) im Artikel *Erstellen einer Konformitätsrichtlinie in Microsoft Intune*. Die folgenden Informationen beziehen sich speziell auf die Konfiguration von Microsoft Defender ATP im Rahmen einer Konformitätsrichtlinie.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Geräte** > **Konformitätsrichtlinien** > **Richtlinien** > **Richtlinie erstellen** aus.

3. Verwenden Sie das Dropdownfeld, um eine der folgenden Optionen für **Plattform** auszuwählen:
   - **Windows 10 und höher**
   - **Android-Geräteadministrator**
   - **Android Enterprise**

   Klicken Sie dann auf **Erstellen**, um das Konfigurationsfenster **Richtlinie erstellen** zu öffnen.

4. Geben Sie einen **Namen** an, der Ihnen hilft, diese Richtlinie später zu identifizieren. Sie können auch eine **Beschreibung** angeben.
  
5. Erweitern Sie auf der Registerkarte **Konformitätseinstellungen** die Gruppe **Microsoft Defender ATP**, und legen Sie für **Anfordern, dass das Gerät höchstens das angegebene Computerrisiko aufweist** die bevorzugte Stufe fest.

   Bedrohungsstufenklassifizierungen werden [von Microsoft Defender ATP bestimmt](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/alerts-queue).

   - **Löschen**: Diese Stufe ist die sicherste Einstellung. Solange auf einem Gerät Bedrohungen vorhanden sind, ist kein Zugriff auf Unternehmensressourcen möglich. Wenn Bedrohungen gefunden werden, wird das Gerät als nicht kompatibel bewertet. (Microsoft Defender ATP verwendet den Wert *Sicher*.)
   - **Niedrig:** Das Gerät ist konform, wenn nur Bedrohungen auf niedriger Stufe vorliegen. Geräte mit mittleren oder hohen Bedrohungsstufen sind nicht konform.
   - **Mittel**: Das Gerät ist konform, wenn auf dem Gerät Bedrohungen niedriger oder mittlerer Stufe gefunden werden. Wenn auf dem Gerät Bedrohungen hoher Stufen erkannt werden, wird es als nicht kompatibel bewertet.
   - **Hoch**: Dies ist die unsicherste Stufe, die alle Bedrohungsstufen zulässt. Geräte mit hohen, mittleren oder niedrigen Bedrohungsstufen werden als konform angesehen.

6. Vervollständigen Sie die Konfiguration der Richtlinie einschließlich der Zuweisung der Richtlinie zu den entsprechenden Gruppen.


## <a name="create-a-conditional-access-policy"></a>Erstellen einer Richtlinie für den bedingten Zugriff

Die Richtlinien für bedingten Zugriff können Daten aus Microsoft Defender ATP verwenden, um den Zugriff auf Ressourcen für Geräte, die die von Ihnen in der Konformitätsrichtlinie festgelegte Bedrohungsstufe überschreiten, zu blockieren. Sie können den Zugriff des Geräts auf Unternehmensressourcen wie SharePoint oder Exchange Online blockieren.

> [!TIP]
> Der bedingte Zugriff ist eine Technologie von Azure Active Directory (Azure AD). Bei dem Knoten für *bedingten Zugriff* im Microsoft Endpoint Manager Admin Center handelt es sich um den Knoten aus *Azure AD*.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Endpunktsicherheit** > **Bedingter Zugriff** > **Neue Richtlinie** aus.

3. Geben Sie einen **Namen** für die Richtlinie ein, und wählen Sie **Benutzer und Gruppen** aus. Fügen Sie mit den Optionen „Einschließen“ oder „Ausschließen“ Ihre Gruppen für die Richtlinie hinzu, und wählen Sie **Fertig** aus.

4. Wählen Sie **Cloud-Apps** und die zu schützenden Apps aus. Wählen Sie z.B. **Apps auswählen** und **Office 365 SharePoint Online** sowie **Office 365 Exchange Online** aus.

   Wählen Sie **Fertig** aus, um die Änderungen zu speichern.

5. Wählen Sie **Bedingungen** > **Client-Apps** aus, um die Richtlinie auf Apps und Browser anzuwenden. Wählen Sie z.B. **Ja** aus, und aktivieren Sie dann **Browser** sowie **Mobile Apps und Desktopclients**.

   Wählen Sie **Fertig** aus, um die Änderungen zu speichern.

6. Wählen Sie **Gewähren** aus, um den bedingten Zugriff basierend auf der Gerätekonformität anzuwenden. Wählen Sie z.B. **Zugriff gewähren** > **Markieren des Geräts als kompatibel erforderlich** aus.

    Wählen Sie **OK** aus, um die Änderungen zu speichern.

7. Wählen Sie **Richtlinie aktivieren** und dann **Erstellen** zum Speichern der Änderungen aus.

## <a name="next-steps"></a>Nächste Schritte

- [Konfigurieren von Microsoft Defender ATP-Einstellungen unter Android](../protect/advanced-threat-protection-manage-android.md)
- [Überwachen der Konformität für Risikostufen](../protect/advanced-threat-protection-monitor.md)

In der Intune-Dokumentation erhalten Sie weitere Informationen:

- [Verwenden von Intune zum Korrigieren von mit Microsoft Defender ATP identifizierten Sicherheitsrisiken](atp-manage-vulnerabilities.md)
- [Erste Schritte mit den Gerätekonformitätsrichtlinien in Intune](device-compliance-get-started.md)

Weitere Informationen finden Sie in der Dokumentation zu Microsoft Defender ATP:

- [Microsoft Defender ATP – bedingter Zugriff](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Microsoft Defender ATP – Risikodashboard](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)
