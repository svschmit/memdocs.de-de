---
title: Verwenden von Sicherheitsrichtlinien in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Schützen Sie Benutzer und Daten auf Geräten mit Microsoft Intune zur Verwaltung mobiler Geräte mit den empfohlenen Windows-Sicherheitseinstellungen. Aktivieren der Verschlüsselung, Konfigurieren von Microsoft Defender Advanced Threat Protection, Steuern von Internet Explorer, Festlegen lokaler Sicherheitsrichtlinien, Anfordern eines Kennworts, Blockieren von Internetdownloads und vieles mehr.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/21/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: laarrizz
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d533acfa60672bed3d6919116f11f43d525b6551
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988329"
---
# <a name="use-security-baselines-to-configure-windows-10-devices-in-intune"></a>Konfigurieren von Windows 10-Geräten in Intune mithilfe von Sicherheitsbaselines

Nutzen Sie die Sicherheitsbaselines von Intune, um Ihre Benutzer und Geräte abzusichern und zu schützen. Sicherheitsbaselines sind vorkonfigurierte Gruppen von Windows-Einstellungen, die Ihnen helfen, eine bekannte Zusammenstellung von Einstellungen und Standardwerten anzuwenden, die von den maßgeblichen Sicherheitsteams empfohlen werden. Wenn Sie in Intune ein Sicherheitsbaselineprofil erstellen, erstellen Sie damit eine Vorlage, die aus mehreren Profilen für die *Gerätekonfiguration* besteht.

Diese Funktion gilt für:

- Windows 10, Version 1809 und höher

Sie stellen Sicherheitsbaselines für Gruppen von Benutzern oder Geräten in Intune bereit. Die Einstellungen gelten für Geräte, auf denen Windows 10 oder höher ausgeführt wird. Die *MDM-Sicherheitsbaselinie* aktiviert beispielsweise für Wechseldatenträger u.a. automatisch BitLocker, fordert automatisch ein Kennwort zum Entsperren eines Geräts an und deaktiviert automatisch die Standardauthentifizierung. Wenn eine Standardeinstellung für Ihre Umgebung nicht funktioniert, passen Sie die Baseline so an, dass die benötigten Einstellungen angewendet werden.

Separate Baselinetypen können zwar die gleichen Einstellungen enthalten, aber unterschiedliche Standardwerte für diese Einstellungen verwenden. Es ist wichtig, die Standardwerte in den von Ihnen gewählten Baselines zu verstehen und anschließend jede Baseline an Ihre Unternehmensanforderungen anzupassen.

> [!NOTE]
> Microsoft empfiehlt nicht, Vorschauversionen von Sicherheitsbaselines in einer Produktionsumgebung einzusetzen. Die Einstellungen in einer Vorschaubaseline können sich im Laufe der Vorschau ändern.

Sicherheitsbaselines bieten Ihnen die Möglichkeit eines durchgängig sicheren Workflows beim Arbeiten mit Microsoft 365. Einige Vorteile sind:

- Eine Sicherheitsbaseline enthält Best Practices und Empfehlungen für Einstellungen, die sich auf die Sicherheit auswirken. Partner von Intune ist dasselbe Windows-Sicherheitsteam, das Gruppenrichtlinien-Sicherheitsbaselines erstellt. Diese Empfehlungen basieren auf Anleitungen und umfassenden Erfahrungen.
- Wenn Sie noch keine Erfahrung mit Intune haben und nicht sicher sind, wo Sie anfangen sollen, sind Sicherheitsbaselines ein guter Einstieg. Sie können schnell ein sicheres Profil erstellen und bereitstellen und sicher sein, dass Sie so die Ressourcen und Daten Ihrer Organisation schützen.
- Wenn Sie zurzeit die Gruppenrichtlinie verwenden, ist mit diesen Baselines die Migration zu Intune zur Verwaltung viel einfacher. Diese Baselines sind nativ in Intune integriert und weisen eine moderne Benutzeroberfläche auf.

Der Artikel [Windows-Sicherheitsgrundsätze](https://docs.microsoft.com/windows/security/threat-protection/windows-security-baselines) ist eine hervorragende Ressource, um mehr über dieses Feature zu erfahren. Der Artikel [Mobile Geräteverwaltung](https://docs.microsoft.com/windows/client-management/mdm/) (Mobile Device Management, MDM) ist eine hervorragende Ressource zu MDM und den Möglichkeiten, die Ihnen Windows-Geräte bieten.

## <a name="available-security-baselines"></a>Verfügbare Sicherheitsbaselines

Die folgenden Sicherheitsbaseline-Instanzen können für Intune verwendet werden. Klicken Sie auf die Links, um die Einstellungen für die neueste Instanz jeder Baseline anzuzeigen.

- **MDM-Sicherheitsbaseline**
  - [MDM-Sicherheitsbaseline für Mai 2019](security-baseline-settings-mdm-all.md?pivots=mdm-may-2019)
  - [Vorschau: MDM-Sicherheitsbaseline für Oktober 2018](security-baseline-settings-mdm-all.md?pivots=mdm-preview)

- **Microsoft Defender ATP-Baseline**
   *(Um diese Baseline verwenden zu können, muss Ihre Umgebung die Voraussetzungen für die Verwendung von [Microsoft Defender Advanced Threat Protection](advanced-threat-protection.md#prerequisites) erfüllen)* .
  - [Microsoft Defender ATP-Baseline aus dem April 2020: Version 4](security-baseline-settings-defender-atp.md?pivots=atp-april-2020)
  - [Microsoft Defender ATP-Baseline aus dem März 2020: Version 3](security-baseline-settings-defender-atp.md?pivots=atp-march-2020)

  > [!NOTE]
  > Die Microsoft Defender ATP-Sicherheitsbaseline wurde für physische Geräte optimiert und ist zurzeit nicht für die Verwendung auf virtuellen Computern (VMs) oder VDI-Endpunkten empfehlenswert. Bestimmte Baselineeinstellungen können sich auf interaktive Remotesitzungen in virtualisierten Umgebungen auswirken.  Weitere Informationen finden Sie unter [Increase compliance to the Microsoft Defender ATP security baseline (Erhöhung der Compliance für die Microsoft Defender ATP-Sicherheitsbaseline)](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-machines-security-baseline).

- **Microsoft Edge-Sicherheitsbaseline**
  - [Microsoft Edge-Sicherheitsbaseline für April 2020 (Edge-Version 80 und höher)](security-baseline-settings-edge.md?pivots-edge-april-2020)
  - [Vorschau: Microsoft Edge-Sicherheitsbaseline für Oktober 2019 (Edge-Version 77 und höher)](security-baseline-settings-edge.md?pivots=edge-october-2019)

Sie können die zuvor auf der Grundlage einer Vorschauvorlage erstellten Profile weiterhin nutzen und bearbeiten, auch wenn diese Vorschauvorlage für die Erstellung neuer Profile nicht mehr verfügbar ist.

Wenn Sie bereit sind, zu einer neueren Version einer von Ihnen verwendeten Baseline zu wechseln, finden Sie weitere Informationen unter [Ändern der Baselineversion für ein Profil](#change-the-baseline-version-for-a-profile) in diesem Artikel. 

## <a name="about-baseline-versions-and-instances"></a>Informationen zu Baselineversionen und Instanzen

Bei jeder neuen Versionsinstanz einer Baseline können Einstellungen hinzugefügt oder entfernt oder andere Änderungen vorgenommen werden. Wenn beispielsweise in neuen Versionen von Windows 10 neue Windows 10-Einstellungen verfügbar werden, erhält die MDM-Sicherheitsbaseline möglicherweise eine neue Versionsinstanz, die die neuesten Einstellungen enthält.

Im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) wird unter **Endpunktsicherheit** > **Sicherheitsbaselines** eine Liste der verfügbaren Baselines angezeigt. Die Liste enthält:
- den Namen der Baselinevorlage,
- die Anzahl der Profile, die diesen Baselinetyp verwenden,
- die Anzahl der verfügbaren separaten Instanzen (Versionen) des Baselinentyps,
- ein Datum *Zuletzt veröffentlicht*, das angibt, wann die neueste Version der Baselinevorlage verfügbar wurde.

Um weitere Informationen zu den von Ihnen verwendeten Baselineversionen anzuzeigen, wählen Sie eine Baseline aus, um deren Blatt *Übersicht* zu öffnen, und wählen Sie dann **Versionen** aus. Intune zeigt Details zu den Versionen dieser Baseline an, die von Ihren Profilen verwendet werden. Die Details umfassen die neueste und die aktuelle Baselineversion. Sie können auf eine einzelne Version klicken, um nähere Informationen über die Profile einzusehen, die diese Version verwenden.

Sie können die [Version einer Baseline ändern](#change-the-baseline-version-for-a-profile), die mit einem bestimmten Profil verwendet wird. Wenn Sie die Version ändern, müssen Sie kein neues Baselineprofil erstellen, um die Vorteile aktualisierter Versionen nutzen zu können. Stattdessen können Sie ein Baselineprofil auswählen und die integrierte Option verwenden, um die Instanzversion für dieses Profil in eine neue Version zu ändern.

### <a name="compare-baseline-versions"></a>Vergleichen von Baselineversionen

Im Bereich **Versionen** für eine Sicherheitsbaseline finden Sie eine Liste der einzelnen Versionen dieser Baseline, die Sie bereitgestellt haben. Diese Liste enthält auch die neueste und aktive Version der Baseline. Wenn Sie ein neues *Sicherheitsbaselineprofil* erstellen, verwendet dieses Profil die neueste Version der Sicherheitsbaseline.  Sie können zuvor erstellte Profile, die eine frühere Baselineversion verwenden, weiterhin einsetzen und bearbeiten, einschließlich der mit einer Vorschauversion erstellten Baselines.

Wenn Sie wissen möchten, was sich zwischen zwei Versionen geändert hat, aktivieren Sie bei zwei verschiedenen Versionen die Kontrollkästchen, und klicken Sie dann auf **Compare baselines** (Baselines vergleichen). Sie werden aufgefordert, eine CSV-Datei herunterzuladen, die diese Unterschiede detailliert erläutert.

In der heruntergeladenen Datei wird jede Einstellung in den beiden Baselineversionen aufgeführt und angegeben, ob sich diese Einstellung geändert hat (*notEqual*) oder unverändert geblieben ist (*equal*). Darüber hinaus ist der Standardwert für die jeweilige Einstellung nach Version angegeben sowie ob die Einstellung in der neueren Version *hinzugefügt* oder *entfernt* wurde.

![Baselines vergleichen](./media/security-baselines/compare-baselines.png)

## <a name="avoid-conflicts"></a>Vermeiden von Konflikten

Sie können eine oder mehrere der verfügbaren Baselines in Ihrer Intune-Umgebung gleichzeitig verwenden. Sie können auch mehrere Instanzen derselben Sicherheitsbaselines verwenden, die unterschiedliche Anpassungen aufweisen.

Wenn Sie mehrere Sicherheitsbaselines verwenden, überprüfen Sie die Einstellungen in jeder einzelnen Baseline, um festzustellen, ob die verschiedenen Baselinekonfigurationen zu widersprüchlichen Werten für dieselbe Einstellung führen. Da Sie Sicherheitsbaselines bereitstellen können, die für verschiedene Zwecke konzipiert sind, und mehrere Instanzen derselben Baseline bereitgestellt werden können, die benutzerdefinierte Einstellungen umfassen, kann es zu Konfigurationskonflikten für Geräte kommen, die untersucht und gelöst werden müssen.

Außerdem verwalten Sicherheitsbaselines häufig dieselben Einstellungen, die Sie möglicherweise mit [Gerätekonfigurationsprofilen](../configuration/device-profiles.md) oder anderen Arten von Richtlinien festlegen. Beachten Sie daher die zusätzlichen Richtlinien und Profile für Einstellungen, wenn Sie versuchen, Konflikte zu vermeiden oder zu lösen.

Verwenden Sie die Informationen unter den folgenden Links, um Konflikte zu identifizieren und zu beheben:

- [Richtlinien und Profile zur Problembehandlung in Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
- [Überwachen Ihrer Sicherheitsbaselines](security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## <a name="manage-baselines"></a>Verwalten von Baselines

Zu den üblichen Aufgaben beim Arbeiten mit Sicherheitsbaselines gehören:

- [Erstellen eines Profils](#create-the-profile): Konfigurieren Sie die Einstellungen, die Sie verwenden möchten, und weisen Sie die Baseline dann Gruppen zu.
- [Ändern der Version](#change-the-baseline-version-for-a-profile): Ändern Sie die Baselineversion, die von einem Profil verwendet wird.
- [Entfernen einer Baselinezuweisung](#remove-a-security-baseline-assignment): Stellen Sie fest, was passiert, wenn Sie das Verwalten von Einstellungen mit einer Sicherheitsbaseline beenden.


### <a name="prerequisites"></a>Voraussetzungen

- Wenn Sie Baselines in Intune verwalten möchten, muss Ihr Konto über die integrierte Rolle [Policy and Profile Manger](../fundamentals/role-based-access-control.md#built-in-roles) (Richtlinien- und Profilmanager) verfügen.

- Einige Baselines können ein aktives Abonnement für zusätzliche Dienste wie Microsoft Defender ATP erfordern.

### <a name="create-the-profile"></a>Erstellen des Profils

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Klicken Sie auf **Endpunktsicherheit** > **Sicherheitsbaselines**, um die Liste der verfügbaren Baselines abzurufen.

   ![Auswählen einer Sicherheitsbaseline zum Konfigurieren](./media/security-baselines/available-baselines.png)

3. Wählen Sie die Baseline, die Sie verwenden möchten, und dann **Profil erstellen** aus.

4. Geben Sie auf der Registerkarte **Grundlagen** die folgenden Eigenschaften an:

   - **Name:** Geben Sie einen Namen für Ihr Sicherheitsbaselinesprofil ein. Geben Sie beispielsweise *Standardprofil für Defender ATP* ein.

   - **Beschreibung:** Geben Sie einen Text ein, der die Funktion dieser Baseline beschreibt. Sie können einen beliebigen Text als Beschreibung eingeben. Dies ist optional, wird jedoch empfohlen.

   Klicken Sie auf **Weiter**, um zur nächsten Registerkarte zu gelangen. Nachdem Sie zu einer neuen Registerkarte gewechselt sind, können Sie den Namen der Registerkarte auswählen, um zu einer zuvor angezeigten Registerkarte zurückzukehren.

5. Zeigen Sie auf der Registerkarte „Konfigurationseinstellungen“ die Gruppen von **Einstellungen** an, die in der von Ihnen ausgewählten Baseline verfügbar sind. Sie können eine Gruppe aufklappen, um die Einstellungen in dieser Gruppe und die Standardwerte für diese Einstellungen in der Baseline anzuzeigen. So finden Sie bestimmte Einstellungen
   - Wählen Sie eine Gruppe aus, um die verfügbaren Einstellungen aufzuklappen und zu überprüfen.
   - Geben Sie Stichwörter in die *Suchleiste* an, um die Ansicht so zu filtern, dass nur die Gruppen angezeigt werden, die Ihren Suchkriterien entsprechen.

   Jede Einstellung in einer Baseline hat für die jeweilige Baselineversion eine Standardkonfiguration. Konfigurieren Sie die Standardeinstellungen neu, damit sie ihre geschäftlichen Anforderungen erfüllen. Verschiedene Baselines können die gleiche Einstellung enthalten und je nach Zweck der Baseline unterschiedliche Standardwerte für die Einstellung verwenden.

   ![Erweitern einer Gruppe, um die Einstellungen dafür anzuzeigen](./media/security-baselines/sample-list-of-settings.png)

6. Wählen Sie auf der Registerkarte **Bereichstags** den Befehl **Bereichstags auswählen** aus, um den Bereich *Tags auswählen* zu öffnen, in dem Sie dem Profil Bereichstags zuweisen.

7. Wählen Sie auf der Registerkarte **Zuweisungen** den Befehl **Einzuschließende Gruppen auswählen**, und weisen Sie dann die Baseline einer oder mehreren Gruppen zu. Wählen Sie **Auszuschließende Gruppen auswählen**, um die Zuweisung anzupassen.

   ![Zuweisen eines Profils](./media/security-baselines/assignments.png)

8. Wenn Sie die Baseline bereitstellen möchten, wechseln Sie zur Registerkarte **Überprüfen + erstellen**, um die Details der Baseline zu überprüfen. Klicken Sie auf **Erstellen**, um das Profil zu speichern und bereitzustellen.

   Sobald Sie das Profil erstellt haben, gilt es in der zugewiesenen Gruppe möglicherweise sofort.

   > [!TIP]
   > Wenn Sie ein Profil speichern, ohne es zuvor Gruppen zuzuweisen, können Sie es später bearbeiten.

   ![Überprüfen der Baseline](./media/security-baselines/review.png)

9. Nachdem Sie ein Profil erstellt haben, können Sie es bearbeiten, indem Sie zu **Endpunktsicherheit** > **Sicherheitsbaselines** wechseln, den konfigurierten Baselinetyp auswählen und auf **Profile** klicken. Wählen Sie das Profil in der Liste der verfügbaren Profile aus, und klicken Sie dann auf **Eigenschaften**. Sie können Einstellungen auf allen verfügbaren Konfigurationsregisterkarten bearbeiten und auf **Überprüfen + speichern** klicken, um Ihre Änderungen zu übernehmen.

### <a name="change-the-baseline-version-for-a-profile"></a>Ändern der Baselineversion für ein Profil

Sie können die Version der Baselineinstanz ändern, die mit einem Profil verwendet wird.  Wenn Sie die Version ändern, wählen Sie eine verfügbare Instanz derselben Baseline aus. Sie können nicht zwischen zwei verschiedenen Baselinetypen wechseln. Es ist also beispielsweise nicht möglich, für ein Profil von der Verwendung einer Baseline für Defender ATP zur Verwendung der MDM-Sicherheitsbaseline zu wechseln.

Während Sie eine Änderung der Baselineversion konfigurieren, können Sie eine CSV-Datei herunterzuladen, die die Änderungen zwischen den beiden beteiligten Baselineversionen auflistet. Außerdem haben Sie die Möglichkeit, alle Anpassungen von der ursprünglichen Baselineversion zu übernehmen oder die neue Version mit allen ihren Standardwerten zu implementieren. Es ist Ihnen nicht möglich, Änderungen an einzelnen Einstellungen vorzunehmen, wenn Sie die Version einer Baseline für ein Profil ändern.

Nach dem Speichern im Anschluss an die Konvertierung wird die Baseline für zugewiesene Gruppen sofort erneut bereitgestellt.

**Während der Konvertierung**:

- Neue nicht in der Originalversion vorhandene Einstellungen werden hinzugefügt und so festgelegt, dass sie die Standardwerte verwenden.

- Nicht in der von Ihnen ausgewählten neuen Baselineversion enthaltene Einstellungen werden entfernt und von diesem Sicherheitsbaseline-Profil nicht mehr erzwungen.

  Wenn eine Einstellung nicht mehr von einem Baselineprofil verwaltet wird, wird diese Einstellung auf dem Gerät nicht zurückgesetzt. Stattdessen bleibt die Einstellung auf dem Gerät auf ihre letzte Konfiguration festgelegt, bis ein anderer Prozess die Einstellung ändert. Beispiele für Prozesse, die eine Einstellung ändern können, nachdem Sie die Verwaltung eingestellt haben, sind ein anderes Baselineprofil, eine Gruppenrichtlinieneinstellung oder eine auf dem Gerät vorgenommene manuelle Konfiguration.

#### <a name="to-change-the-baseline-version-for-a-profile"></a>So ändern Sie die Baselineversion für ein Profil

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an. 

2. Klicken Sie auf **Endpunktsicherheit** > **Sicherheitsbaselines**, und wählen Sie dann die Kachel für den Baselinetyp mit dem Profil aus, das Sie ändern möchten.

3. Wählen Sie anschließend **Profile** aus, und aktivieren Sie dann das Kontrollkästchen des Profils, das Sie bearbeiten möchten. Klicken Sie anschließend auf **Version ändern**.

   ![Auswählen einer Baseline](./media/security-baselines/select-baseline.png)

4. Klicken Sie im Bereich **Version ändern** auf das Dropdownmenü **Hiermit wählen Sie eine Sicherheitsbaseline aus, auf die aktualisiert werden soll**, und wählen Sie die gewünschte Versionsinstanz aus.

   ![Auswählen einer Version](./media/security-baselines/select-instance.png)

5. Klicken Sie auf **Update überprüfen**, um eine CSV-Datei herunterzuladen, die die Unterschiede zwischen der aktuellen Instanzversion des Profils und der von Ihnen ausgewählten neuen Version zeigt. Überprüfen Sie diese Datei, um zu verstehen, welche Einstellungen neu sind oder entfernt wurden und welche Standardwerte für diese Einstellungen im aktualisierten Profil enthalten sind.

   Wenn Sie fertig sind, fahren Sie mit dem nächsten Schritt fort.

6. Wählen Sie eine der beiden Optionen für **Methode zum Aktualisieren des Profils auswählen**:
   - **Baselineänderungen akzeptieren, aber meine vorhandenen Einstellungsanpassungen beibehalten**: Bei Wahl dieser Option werden die Anpassungen, die Sie am Baselineprofil vorgenommen haben, beibehalten und auf die neue Version angewendet, die Sie verwenden möchten.
   - **Baselineänderungen akzeptieren und vorhandene Einstellungsanpassungen verwerfen**: Bei Wahl dieser Option wird Ihr ursprüngliches Profil vollständig überschrieben. Im aktualisierten Profil werden für alle Einstellungen die Standardwerte verwendet.

7. Klicken Sie auf **Senden**. Das Profil wird auf die ausgewählte Baselineversion aktualisiert. Nach der Konvertierung wird die Baseline zugewiesenen Gruppen sofort wieder bereitgestellt.

### <a name="remove-a-security-baseline-assignment"></a>Aufheben der Zuweisung einer Sicherheitsbaseline

Wenn eine Einstellung der Sicherheitsbaseline nicht mehr für ein Gerät gilt oder die Einstellungen in einer Baseline auf *Nicht konfiguriert* festgelegt sind, werden diese Einstellungen auf einem Gerät nicht auf eine zuvor verwaltete Konfiguration zurückgesetzt. Stattdessen behalten die zuvor verwalteten Einstellungen auf dem Gerät ihre letzten Konfigurationen, wie sie von der Baseline empfangen wurden, bis ein anderer Prozess diese Einstellungen auf dem Gerät aktualisiert.

Andere Prozesse, die später die Einstellungen auf dem Gerät ggf. ändern, sind eine andere oder neue Sicherheitsbaseline, ein Gerätekonfigurationsprofil, Gruppenrichtlinienkonfigurationen oder die manuelle Bearbeitung der Einstellungen auf dem Gerät.

### <a name="duplicate-a-security-baseline"></a>Duplizieren einer Sicherheitsbaseline

Sie können Duplikate ihrer Sicherheitsbaselines erstellen. Ein Szenario, in dem das Duplizieren einer Baseline nützlich ist, liegt beispielsweise vor, wenn Sie einer Teilmenge von Geräten eine ähnliche, aber unterschiedliche Baseline zuweisen möchten. Indem Sie ein Duplikat erstellen, müssen Sie die gesamte Baseline nicht manuell neu erstellen. Stattdessen können Sie jede der aktuellen Baselines duplizieren und dann nur die Änderungen vornehmen, die für die neue Instanz erforderlich sind. Sie können z. B. nur eine bestimmte Einstellung und die Gruppe ändern, der die Baseline zugewiesen wird.

Wenn Sie ein Duplikat erstellen, müssen Sie der Kopie einen neuen Namen geben. Die Kopie wird mit denselben Einstellungskonfigurationen und Bereichstags wie das Original erstellt, aber ohne Zuweisungen. Sie müssen die neue Baseline bearbeiten, um Zuweisungen hinzuzufügen.

Alle Sicherheitsbaselines unterstützen das Erstellen eines Duplikats.

Nachdem Sie eine Baseline dupliziert haben, überprüfen und bearbeiten Sie die neue Instanz, um Änderungen an der Konfiguration vorzunehmen.

#### <a name="to-duplicate-a-baseline"></a>So duplizieren Sie eine Baseline

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Navigieren Sie zu **Endpunktsicherheit** > **Sicherheitsbaselines**, wählen Sie den Typ der Baseline aus, die Sie duplizieren möchten, und wählen Sie dann **Profile** aus.
3. Klicken Sie mit der rechten Maustaste auf das Profil, das Sie duplizieren möchten, und wählen Sie **Duplizieren** aus, oder wählen Sie die Auslassungspunkte ( **...** ) rechts neben der Baseline aus, und wählen Sie dann **Duplizieren** aus.
4. Geben Sie einen **neuen Namen** für die Basislinie an, und wählen Sie dann **Speichern** aus.

Nach einer *Aktualisierung* wird das neue Baselineprofil in Admin Center angezeigt.

#### <a name="to-edit-a-baseline"></a>So bearbeiten Sie eine Baseline

1. Wählen Sie die Baseline aus, und wählen Sie dann **Eigenschaften** aus.
2. Wählen Sie **Einstellungen** aus, um die Liste der Einstellungskategorien in der Baseline zu erweitern. Sie können die Einstellungen in dieser Ansicht nicht ändern, aber Sie können überprüfen, wie sie konfiguriert sind.
3. Um die Einstellungen zu ändern, wählen Sie **Bearbeiten** für jede Kategorie aus, in der Sie eine Änderung vornehmen möchten:
   - Grundlagen
   - Zuweisungen
   - Festlegen von Tags
   - Konfigurationseinstellungen
4. Nachdem Sie Änderungen vorgenommen haben, wählen Sie **Speichern** aus, um Ihre Änderungen zu speichern.  Sie müssen Änderungen an einer Kategorie speichern, bevor Sie Änderungen an weiteren Kategorien vornehmen können.

### <a name="older-baseline-versions"></a>Ältere Baselineversionen

Der Microsoft Endpoint Manager aktualisiert die Versionen von integrierten Sicherheitsbaselines abhängig von den sich ändernden Anforderungen einer typischen Organisation. Jedes neue Release führt zu einem Versionsupdate für eine bestimmte Baseline. Es wird erwartet, dass Kunden die jeweils aktuelle Baselineversion als Ausgangspunkt für ihre Gerätekonfigurationsprofile verwenden.

Wenn keine Profile mehr vorhanden sind, die eine ältere in Ihrem Mandanten aufgeführte Baseline verwenden, führt Microsoft Endpoint Manager nur die neueste verfügbare Baselineversion auf.

Wenn Sie über ein Profil verfügen, das mit einer älteren Baseline verknüpft ist, wird diese ältere Baseline weiterhin aufgeführt.

## <a name="co-managed-devices"></a>Gemeinsam verwaltete Geräte

Sicherheitsbaselines für von Intune verwaltete Geräten ähneln denen mit Configuration Manager gemeinsam verwalteter Geräte. Bei gemeinsam verwalteten Geräten werden Configuration Manager und Microsoft Intune simultan zum Verwalten der Windows 10-Geräte verwendet. Sie können Ihre vorhandene Configuration Manager-Investition in der Cloud mit den Vorteilen von Intune verbinden. Der Artikel [Was ist gemeinsame Verwaltung?](https://docs.microsoft.com/configmgr/comanage/overview) ist eine großartige Ressource, wenn Sie Configuration Manager verwenden und auch die Vorteile der Cloud genießen möchten.

Wenn Sie gemeinsam verwaltete Geräte verwenden, müssen Sie die **Gerätekonfiguration**-Workload (ihre Einstellungen) auf Intune verlagern. Im Abschnitt [Gerätekonfiguration](https://docs.microsoft.com/configmgr/comanage/workloads#device-configuration) finden Sie weitere Informationen.

## <a name="q--a"></a>Q & A

### <a name="why-these-settings"></a>Warum diese Einstellungen?

Diese Empfehlungen basieren auf der jahrelangen Erfahrung des Microsoft-Sicherheitsteams in der direkten Zusammenarbeit mit Windows-Entwicklern und der Sicherheitscommunity. Die Einstellungen in dieser Baseline werden als die wichtigsten sicherheitsbezogenen Konfigurationsoptionen betrachtet. In jedem neuen Build von Windows passt das Team die Empfehlungen basierend auf neu herausgegebenen Features an.

### <a name="is-there-a-difference-in-the-recommendations-for-windows-security-baselines-for-group-policy-vs-intune"></a>Gibt es einen Unterschied in den Empfehlungen für die Windows-Sicherheitsbaselines für die Gruppenrichtlinie im Vergleich zu Intune?

Das gleiche Microsoft-Sicherheitsteam hat die Einstellungen für jede Baseline ausgewählt und organisiert. Intune umfasst alle relevanten Einstellungen in der Intune-Sicherheitsbaseline. Es gibt einige Einstellungen in der Gruppenrichtlinienbaseline, die für einen lokalen Domänencontroller spezifisch sind. Diese Einstellungen werden von den Intune-Empfehlungen ausgeschlossen. Alle anderen Einstellungen sind identisch.

### <a name="are-the-intune-security-baselines-cis-or-nsit-compliant"></a>Sind die Intune-Sicherheitsbaselines CIS- oder NSIT-kompatibel?

Streng genommen, nicht. Das Microsoft-Sicherheitsteam berät Unternehmen wie CIS, um Empfehlungen zusammenzutragen. Allerdings gibt es keine 1:1-Zuordnung von „CIS-konformen“ und Microsoft-Baselines.

### <a name="what-certifications-does-microsofts-security-baselines-have"></a>Welche Zertifizierungen weisen die Sicherheitsbaselines von Microsoft auf? 

- Microsoft veröffentlicht weiterhin Sicherheitsbaselines für Gruppenrichtlinien (GPOs) und das [Security Compliance Toolkit](https://docs.microsoft.com/windows/security/threat-protection/security-compliance-toolkit-10), wie seit vielen Jahren. Diese Baselines werden von vielen Organisationen verwendet. Die Empfehlungen in diesen Baselines entstammen der Zusammenarbeit des Microsoft-Sicherheitsteams mit Unternehmenskunden und externen Einrichtungen, einschließlich des Department of Defense (DoD, Verteidigungsministerium der USA), National Institute of Standards and Technology (NIST, Nationales Institut für Standards und Technologie) und anderer. Wir teilen unsere Empfehlungen und Baselines mit diesen Organisationen. Diese Organisationen haben auch ihre eigenen Empfehlungen, die die Empfehlungen von Microsoft sehr genau widerspiegeln. Da die mobile Geräteverwaltung (MDM) in der Cloud zunimmt, hat Microsoft entsprechende MDM-Empfehlungen zu diesen Gruppenrichtlinien-Baselines erstellt. Diese zusätzlichen Baselines sind in Microsoft Intune integriert und enthalten Konformitätsberichte zu Benutzern, Gruppen und Geräten, die die Baseline befolgen (oder nicht).

- Viele Kunden nutzen die Intune-Baselineempfehlungen als Ausgangspunkt und passen sie ihren IT- und Sicherheitsanforderungen an. Die **MDM-Sicherheitsbaseline** für Windows 10 RS5 von Microsoft ist die erste Baseline, die freigegeben wird. Diese Baseline wird als allgemeine Infrastruktur erstellt, die Kunden ermöglicht, schließlich andere, auf CIS, NIST und anderen Standards basierende Sicherheitsbaselines zu importieren. Derzeit ist sie für Windows verfügbar und wird schließlich iOS/iPadOS und Android einschließen.

- Das Migrieren von lokalen Active Directory-Gruppenrichtlinien zu einer reinen Cloudlösung mithilfe von Azure Active Directory (AD) mit Microsoft Intune ist eine Reise. Zur Unterstützung sind im [Security Compliance Toolkit](https://docs.microsoft.com/windows/security/threat-protection/security-compliance-toolkit-10) Gruppenrichtlinienvorlagen enthalten, die bei der Verwaltung von in hybrides Active Directory und Azure Active Directory eingebundenen Geräten helfen können. Diese Geräte können MDM-Einstellungen aus der Cloud (Intune) und Gruppenrichtlinieneinstellungen vom lokalen Domänencontroller nach Bedarf abrufen.

## <a name="next-steps"></a>Nächste Schritte

- Prüfen Sie die Einstellungen in den neuesten Versionen der verfügbaren Baselines:
  - [MDM-Sicherheitsbaseline](security-baseline-settings-mdm-all.md)
  - [Microsoft Defender ATP-Baseline](security-baseline-settings-defender-atp.md)

- Überprüfen Sie den Status, und überwachen Sie [Baseline und Profil](security-baselines-monitor.md).
