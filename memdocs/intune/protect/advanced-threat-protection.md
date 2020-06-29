---
title: Verwenden von Microsoft Defender ATP in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Verwenden Sie Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) mit Intune, einschließlich Einrichtung und Konfiguration, Onboarding Ihrer Intune-Geräte mit ATP, und verwenden Sie dann eine ATP-Geräterisikobewertung mit Ihren Richtlinien für Intune-Gerätecompliance und bedingten Zugriff zum Schutz von Netzwerkressourcen.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1141879a282219cdac72273e47c84b51df172d04
ms.sourcegitcommit: 397ec824f1368dcf06c3870c89f52347852062bd
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/23/2020
ms.locfileid: "85264055"
---
# <a name="enforce-compliance-for-microsoft-defender-atp-with-conditional-access-in-intune"></a>Erzwingen der Konformität für Microsoft Defender ATP mit bedingtem Zugriff in Intune

Sie können Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) als Mobile Threat Defense-Lösung mit Microsoft Intune integrieren. Mit der Integration tragen Sie dazu bei, Sicherheitsverletzungen zu verhindern und deren Auswirkungen innerhalb einer Organisation zu begrenzen. Microsoft Defender ATP funktioniert mit Geräten, auf denen Windows 10 oder höher ausgeführt wird, sowie mit Android-Geräten.

Verwenden Sie die folgenden Konfigurationen gemeinsam:

- **Richten Sie eine Dienst-zu-Dienst-Verbindung zwischen Intune und Microsoft Defender ATP ein**. Diese Verbindung ermöglicht Microsoft Defender ATP das Sammeln von Daten zu Computerrisiken von unterstützten Geräten, die Sie mit Intune verwalten.
- **Verwenden Sie ein Gerätekonfigurationsprofil für das Onboarding von Geräten mit Microsoft Defender ATP**. Sie führen das Onboarding von Geräten durch, um sie für die Kommunikation mit Microsoft Defender ATP zu konfigurieren und Daten bereitzustellen, mit deren Hilfe Sie ihre Risikostufe bewerten können.
- **Verwenden Sie eine Gerätekonformitätsrichtlinie, um die Risikostufe festzulegen, die Sie zulassen möchten**. Risikostufen werden von Microsoft Defender ATP gemeldet. Geräte, die die zulässige Risikostufe überschreiten, werden als nicht konform eingestuft.
- **Verwenden Sie eine Richtlinie für bedingten Zugriff**, um den Zugriff von Benutzern auf Unternehmensressourcen mit nicht konformen Geräten zu blockieren.

Wenn Sie Intune mit Microsoft Defender ATP integrieren, können Sie die Bedrohungs- und Sicherheitsrisikenverwaltung von Microsoft Defender ATP (Thread & Vulnerability Management, TVM) nutzen und [Intune verwenden, um mittels TVM identifizierte Schwachstellen von Endpunkten zu beheben](atp-manage-vulnerabilities.md).

## <a name="example-of-using-microsoft-defender-atp-with-intune"></a>Beispiel für die Verwendung von Microsoft Defender ATP mit Intune

Im folgenden Beispiel wird erläutert, wie diese Lösungen zusammenarbeiten, um Ihre Organisation zu schützen. In diesem Beispiel sind Microsoft Defender ATP und Intune bereits integriert.

Stellen Sie sich vor, dass eine Person eine Word-Anlage mit eingebettetem bösartigem Code an einen Benutzer in Ihrer Organisation sendet.

- Der Benutzer öffnet die Anlage und aktiviert den Inhalt.
- Ein Angriff mit erhöhten Rechten beginnt, und ein Angreifer an einem Remotecomputer verfügt über Administratorrechte für das Gerät des Opfers.
- Der Angreifer greift dann remote auf die anderen Geräte des Benutzers zu. Diese Sicherheitsverletzung kann sich auf die gesamte Organisation auswirken.

Microsoft Defender ATP kann Sicherheitsereignisse wie dieses Szenario auflösen.

- In unserem Beispiel erkennt Microsoft Defender ATP, dass das Gerät nicht ordnungsgemäßen Code ausgeführt hat, seine Prozessrechte erhöht wurden, dass es bösartigen Code eingeschleust und eine verdächtige Remoteshell aufgerufen hat.
- Basierend auf diesen Aktionen des Geräts [klassifiziert Microsoft Defender ATP das Gerät als hochriskant](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/alerts-queue#severity) und legt einen detaillierten Bericht über verdächtige Aktivitäten im Microsoft Defender Security Center-Portal ab.

Da Sie über eine Intune-Gerätekonformitätsrichtlinie verfügen, um Geräte mit der Risikostufe *Mittel* oder *Hoch* als nicht konform zu klassifizieren, wird das gefährdete Gerät als nicht konform klassifiziert. Diese Klassifizierung ermöglicht Ihrer Richtlinie für bedingten Zugriff, den Zugriff von diesem Gerät auf Ihre Unternehmensressourcen zu blockieren.

Sie können auch Intune-Richtlinien verwenden, um einige Konfigurationen für Microsoft Defender ATP für Android zu bearbeiten. Weitere Informationen erhalten Sie weiter unten in diesem Artikel unter [Konfigurieren des Features „Webschutz“ für Android-Geräte](#configure-web-protection-on-devices-that-run-android).

## <a name="prerequisites"></a>Voraussetzungen

Um Microsoft Defender ATP mit Intune zu verwenden, stellen Sie sicher, dass Sie Folgendes konfiguriert haben und verwenden können:

- Lizenzierter Mandant für Enterprise Mobility + Security E3 und Windows E5 (oder Microsoft 365 Enterprise E5)
- Microsoft Intune-Umgebung mit [Intune-verwalteten](../enrollment/windows-enroll.md) Windows 10- oder Android-Geräten, die auch mit Azure AD verknüpft sind
- [Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) und Zugriff auf das Microsoft Defender Security Center (ATP-Portal)

> [!NOTE]
> Microsoft Defender ATP wird für Intune-App-Schutzrichtlinien für iOS/iPadOS und Android nicht unterstützt.

## <a name="enable-microsoft-defender-atp-in-intune"></a>Aktivieren von Microsoft Defender ATP in Intune

Der erste Schritt ist das Einrichten einer Dienst-zu-Dienst-Verbindung zwischen Intune und Microsoft Defender ATP. Dies erfordert Administratorzugriff auf Microsoft Defender Security Center und Intune.

### <a name="to-enable-microsoft-defender-atp"></a>Aktivieren von Microsoft Defender ATP

Sie müssen Microsoft Defender ATP nur einmal pro Mandant aktivieren.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Endpunktsicherheit** > **Microsoft Defender ATP** aus und dann **Microsoft Defender Security Center öffnen**.

   ![Wählen Sie die Option zum Öffnen von Microsoft Defender Security Center aus.](./media/advanced-threat-protection/atp-device-compliance-open-microsoft-defender.png)

3. In **Microsoft Defender Security Center**:
   1. Wählen Sie **Einstellungen** > **Erweiterte Features** aus.
   2. Wählen Sie für **Microsoft Intune-Verbindung** die Option **Ein** aus:

      ![Aktivieren der Verbindung mit Intune](./media/advanced-threat-protection/atp-security-center-intune-toggle.png)

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

## <a name="onboard-windows-devices-by-using-a-configuration-profile"></a>Onboarding von Windows-Geräten mithilfe eines Konfigurationsprofils durchführen

Nachdem Sie für die Windows-Plattform die Dienst-zu-Dienst-Verbindung zwischen Intune und Microsoft Defender ATP hergestellt haben, führen Sie das Onboarding Ihrer von Intune verwalteten Geräte in Microsoft Defender ATP durch, damit Daten über ihre Risikostufe gesammelt und verwendet werden können. Verwenden Sie zum Onboarding der Geräte ein Gerätekonfigurationsprofil für Microsoft Defender ATP.

Wenn Sie die Verbindung mit Microsoft Defender ATP hergestellt haben, empfängt Intune ein Microsoft Defender ATP-Onboardingkonfigurationspaket von Microsoft Defender ATP. Dieses Paket wird auf Geräten mit dem Gerätekonfigurationsprofil bereitgestellt. Das Konfigurationspaket konfiguriert Geräte zur Kommunikation mit [Microsoft Defender ATP-Diensten](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection), um Dateien zu überprüfen, Bedrohungen zu erkennen und das Risiko an Microsoft Defender ATP zu melden. Nachdem Sie ein Gerät über das Konfigurationspaket integriert haben, müssen Sie dies nicht erneut tun. Sie können das Onboarding von Geräten auch mit einer [Gruppenrichtlinie oder Microsoft Endpoint Configuration Manager](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints) durchführen.

### <a name="create-the-device-configuration-profile"></a>Erstellen des Gerätekonfigurationsprofils

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.
3. Geben Sie einen **Namen** und eine **Beschreibung** ein.
4. Wählen Sie unter **Plattform** die Option **Windows 10 und höher** aus.
5. Wählen Sie für **Profiltyp** die Option **Microsoft Defender ATP (Windows 10 Desktop)** aus.
6. Konfigurieren Sie die Einstellungen:

   - **Pakettyp für die Microsoft Defender ATP-Clientkonfiguration**: Wählen Sie **Onboarding** aus, um das Konfigurationspaket zum Profil hinzuzufügen. Klicken Sie auf **Offboard** (Integration aufheben), um das Konfigurationspaket aus dem Profil zu entfernen.
  
     > [!NOTE]
     > Wenn Sie eine ordnungsgemäße Verbindung mit Microsoft Defender ATP hergestellt haben, führt Intune automatisch ein **Onboarding** für das Konfigurationsprofil für Sie durch, und die Einstellung **Pakettyp für die Microsoft Defender ATP-Clientkonfiguration** ist nicht verfügbar.
  
   - **Beispielfreigabe für alle Dateien**: Durch das **Aktivieren** dieser Option werden Stichproben erfasst und mit Microsoft Defender ATP geteilt. Wenn Sie z. B. eine verdächtige Datei sehen, können Sie sie zur gründlichen Analyse an Microsoft Defender ATP senden. Wenn **Nicht konfiguriert** festgelegt ist, werden keine Stichproben mit Microsoft Defender ATP geteilt.
   - **Häufigkeit von Telemetrieberichten erhöhen**: Bei Geräten mit hohem Risiko werden durch das **Aktivieren** dieser Option häufiger Telemetriedaten an den Microsoft Defender ATP-Dienst gemeldet.

     [Onboarding von Windows 10-Computern mit Configuration Manager](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-endpoints-sccm) enthält nähere Informationen zu diesen Microsoft Defender ATP-Einstellungen.

7. Klicken Sie auf **OK** und dann auf **Erstellen**, um Ihre Änderungen zu speichern. Dadurch wird das Profil erstellt.
8. [Weisen Sie das Gerätekonfigurationsprofil Geräten zu, die Sie mit Microsoft Defender ATP bewerten möchten.](../configuration/device-profile-assign.md)

## <a name="onboard-android-devices"></a>Durchführen des Onboardings für Android-Geräte
Nachdem Sie die Dienst-zu-Dienst-Verbindung zwischen Intune und Microsoft Defender ATP hergestellt haben, führen Sie das Onboarding für verwaltete Geräte in Microsoft Defender ATP durch, damit Daten über ihre Risikostufe gesammelt und verwendet werden können.

Eine detaillierte Anleitung für das Onboarding von Android-Geräten, einschließlich der Voraussetzungen für Endbenutzer und Administratoren, finden Sie in der Dokumentation zu Microsoft Defender ATP unter [Microsoft Defender Advanced Threat Protection für Android](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-android).

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

## <a name="configure-web-protection-on-devices-that-run-android"></a>Konfigurieren des Features „Webschutz“ für Android-Geräte

Standardmäßig schließt Microsoft Defender ATP für Android das Feature „Webschutz“ ein und aktiviert es. [Webschutz](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview) unterstützt das Schützen von Geräten vor Bedrohungen im Web und schützt Benutzer vor Phishingangriffen.

Das Feature ist zwar standardmäßig aktiviert, es gibt aber verschiedene Gründe, aus denen dieser Schutz auf manchen Android-Geräten deaktiviert werden sollte. Sie könnten sich beispielsweise dazu entscheiden, nur das Feature zum Scannen von Apps von Microsoft Defender ATP zu verwenden, oder das Feature „Webschutz“ daran zu hindern, Ihr VPN beim Scan schädlicher URLs zu verwenden.

Intune unterstützt das Deaktivieren des gesamten sowie Teilen des Features „Webschutz“. Die Methode, die Sie verwenden, und die Funktionen, die Sie deaktivieren, hängen davon ab, wie das Android-Gerät für Intune registriert wurde:

- **Android-Geräteadministrator**: Verwenden Sie ein Konfigurationsprofil, um benutzerdefinierte OMA-URI-Einstellungen auf dem Gerät festzulegen, um das gesamte Webschutz-Feature zu deaktivieren, oder deaktivieren Sie nur die Verwendung von VPNs. Allgemeine Informationen zu benutzerdefinierten Einstellungen auf Android-Geräten finden Sie unter [Verwenden benutzerdefinierter Einstellungen für Android-Geräte in Microsoft Intune](../configuration/custom-settings-android.md).

- **Android Enterprise (Arbeitsprofil):** Verwenden Sie ein App-Konfigurationsprofil und den *Konfigurations-Designer*, um das Feature „Webschutz“ zu deaktivieren. Diese Methode und dieser Registrierungstyp unterstützen das Deaktivieren aller Funktionen des Webschutz-Features, jedoch nicht das ausschließliche Deaktivieren der Verwendung von VPNs. Allgemeine Informationen zu App-Konfigurationsrichtlinien finden Sie unter [Verwenden des Konfigurations-Designers](../apps/app-configuration-policies-use-android.md#use-the-configuration-designer).

Zum Konfigurieren des Webschutz-Features auf Geräten verwenden Sie das folgende Vorgehen, um die entsprechende Konfiguration zu erstellen und bereitzustellen.

### <a name="disable-web-protection-for-android-device-administrator"></a>Deaktivieren des Features „Webschutz“ für Android-Geräteadministratoren

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.

3. Legen Sie folgende Einstellungen fest:

   - **Plattform**: Wählen Sie **Android-Geräteadministrator** aus.
   - **Profil**: Klicken Sie auf **Benutzerdefiniert**.

   Wählen Sie **Erstellen** aus.

4. Geben Sie unter den **Grundlegenden Einstellungen** die folgenden Informationen ein:

   - **Name:** Geben Sie einen aussagekräftigen Namen für das Profil ein. Benennen Sie Ihre Profile, damit Sie diese später leicht wiedererkennen. Wählen Sie beispielsweise einen Namen wie *Benutzerdefiniertes Android-Profil für das Feature „Webschutz“ in Microsoft Defender ATP* aus.
   - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.

5. Klicken Sie unter **Konfigurationseinstellungen** auf **Hinzufügen**.

   Geben Sie die Einstellungen für die Konfiguration an, die Sie bereitstellen möchten:

   - **Deaktivieren des Features „Webschutz“:**
     - **Name:** Geben Sie einen eindeutigen Namen für diese OMA-URI-Einstellung ein, damit Sie diese leicht finden können. Wählen Sie beispielsweise einen Namen wie *Feature „Webschutz“ in Microsoft Defender ATP deaktivieren* aus.
     - **Beschreibung:** Geben Sie optional eine Beschreibung ein, die einen Überblick über die Einstellung und andere wichtige Details bietet.
     - **OMA-URI**: Geben Sie **./Vendor/MSFT/DefenderATP/AntiPhishing** ein.
     - **Datentyp:** Verwenden Sie das Dropdownmenü, und klicken Sie auf **Integer**.
     - **Wert:** Geben Sie **0** ein, um das Feature „Webschutz“ einschließlich des VPN-basierten Scans zu deaktivieren.
       > [!NOTE]
       > Geben Sie **1** ein, um das Feature „Webschutz“ zu aktivieren. Dies ist die Standardeinstellung für das Feature „Webschutz“.

   - **Ausschließliches Deaktivieren der Verwendung von VPNs durch das Feature „Webschutz“:**
     - **Name:** Geben Sie einen eindeutigen Namen für diese OMA-URI-Einstellung ein, damit Sie diese leicht finden können. Wählen Sie beispielsweise einen Namen wie *Verwendung von VPNs durch das Feature „Webschutz“ in Microsoft Defender ATP deaktivieren* aus.
     - **Beschreibung:** Geben Sie optional eine Beschreibung ein, die einen Überblick über die Einstellung und andere wichtige Details bietet.
     - **OMA-URI**: Geben Sie **./Vendor/MSFT/DefenderATP/Vpn** ein.
     - **Datentyp:** Verwenden Sie das Dropdownmenü, und klicken Sie auf **Integer**.
     - **Wert:** Geben Sie **0** ein, um den VPN-basierten Scan zu deaktivieren.
       > [!NOTE]
       > Geben Sie **1** ein, um das Feature „Webschutz“ zu aktivieren. Dies ist die Standardeinstellung für das Feature „Webschutz“.

   Klicken Sie auf **Hinzufügen**, um die OMA-URI-Einstellungskonfiguration zu speichern, und klicken Sie dann zum Fortfahren auf **Weiter**.

6. Geben Sie auf der Seite **Zuweisungen** die Gruppen an, die dieses Profil erhalten sollen. Weitere Informationen zum Zuweisen von Profilen finden Sie unter [Zuweisen von Benutzer- und Geräteprofilen](../configuration/device-profile-assign.md).

7. Klicken Sie, wenn Sie fertig sind, auf der Seite **Überprüfen + erstellen** auf **Erstellen**. Das neue Profil wird in der Liste angezeigt, wenn Sie den Richtlinientyp für das Profil auswählen, das Sie erstellt haben.

### <a name="disable-web-protection-for-android-enterprise-work-profile"></a>Deaktivieren des Features „Webschutz“ für Android Enterprise (Arbeitsprofil)

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Klicken Sie auf **Apps** > **App-Konfigurationsrichtlinien** > **Hinzufügen**, und klicken Sie dann auf „Verwaltete Geräte“.

3. Geben Sie unter den **Grundlegenden Einstellungen** die folgenden Informationen ein:

   - **Name:** Geben Sie einen aussagekräftigen Namen für das Profil ein. Benennen Sie Ihre Profile, damit Sie diese später leicht wiedererkennen. Wählen Sie beispielsweise einen Namen wie *Android-App-Konfiguration für das Feature „Webschutz“ in Microsoft Defender ATP* aus.
   - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.
   - **Plattform**: Wählen Sie **Android Enterprise** aus.
   - **Profiltyp**: Wählen Sie die Option **Nur Arbeitsprofil** aus.
   - **Ziel-App:** Klicken Sie auf **App auswählen**.

4. Suchen Sie unter **Zugeordnete App** nach **Defender ATP**, und klicken Sie darauf, und klicken Sie dann auf **OK** > **Weiter**.

5. Klicken Sie unter **Einstellungen** im Dropdownmenü **Format der Konfigurationseinstellungen** auf **Konfigurations-Designer verwenden** und dann auf **Hinzufügen**. Der JSON-Editor wird geöffnet.

6. Suchen Sie nach dem Feature **Webschutz**, und klicken Sie darauf, und klicken Sie dann auf **OK**, um zur Seite **Einstellungen** zurückzukehren.

7. Geben Sie als **Konfigurationswert** den Wert **0** ein, um das Feature „Webschutz“ zu deaktivieren.

   > [!NOTE]
   > Geben Sie **1** ein, um das Feature „Webschutz“ zu aktivieren. Dies ist die Standardeinstellung für das Feature „Webschutz“.

   Wählen Sie **Weiter** aus, um den Vorgang fortzusetzen.

8. Geben Sie auf der Seite **Zuweisungen** die Gruppen an, die dieses Profil erhalten sollen. Weitere Informationen zum Zuweisen von Profilen finden Sie unter [Zuweisen von Benutzer- und Geräteprofilen](../configuration/device-profile-assign.md).

9. Klicken Sie, wenn Sie fertig sind, auf der Seite **Überprüfen + erstellen** auf **Erstellen**. Das neue Profil wird in der Liste angezeigt, wenn Sie den Richtlinientyp für das Profil auswählen, das Sie erstellt haben.

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

## <a name="monitor-device-compliance"></a>Überwachen der Gerätekonformität

Überwachen Sie den Status von Geräten, auf die die Microsoft Defender ATP-Konformitätsrichtlinie angewandt wird.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Geräte** > **Überwachen** > **Richtlinienkonformität** aus.

3. Suchen Sie Ihre Microsoft Defender ATP-Richtlinie in der Liste, und sehen Sie, welche Geräte konform bzw. nicht konform sind.

Sie können für nicht konforme Geräte am gleichen Speicherort auch die Option für einen *operational report* (Betriebsbericht) verwenden:

1. Klicken Sie auf **Geräte** > **Überwachen** > **Noncompliant devices** (Nicht konforme Geräte).

Weitere Informationen zu Berichten finden Sie unter [Intune-Berichte](../fundamentals/reports.md).

## <a name="view-onboarding-status"></a>Anzeigen des Onboardingstatus

Navigieren Sie zu **Endpunktsicherheit** > **Microsoft Defender ATP**, um den Onboardingstatus aller von Intune verwalteten Geräte anzuzeigen. Auf dieser Seite können Sie auch die Erstellung eines Gerätekonfigurationsprofils für das Onboarding mehrerer Geräte in Microsoft Defender ATP initiieren.

## <a name="next-steps"></a>Nächste Schritte

[Microsoft Defender ATP – bedingter Zugriff](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/conditional-access)

[Microsoft Defender ATP – Risikodashboard](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)

[Verwenden von Intune zum Korrigieren von mit Microsoft Defender ATP identifizierten Sicherheitsrisiken](atp-manage-vulnerabilities.md).

[Erste Schritte mit den Gerätekonformitätsrichtlinien in Intune](device-compliance-get-started.md)
