---
title: Überprüfen von Erfolg oder Fehler bei Sicherheitsbaselines in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Überprüfen Sie Fehler-, Konflikt- und Erfolgsstatus bei der Bereitstellung von Sicherheitsbaselines für Benutzer und Geräte bei der Verwaltung mobiler Geräte für Microsoft Intune. Erfahren Sie, wie Sie Probleme mithilfe von Clientprotokollen und den Berichtsfunktionen in Intune behandeln.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
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
ms.openlocfilehash: 1ccf9801c7a5977485c6c1864a69be2e46a4af55
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914870"
---
# <a name="monitor-security-baselines-and-profiles-in-microsoft-intune"></a>Überwachen von Sicherheitsbaselines und Sicherheitsbaselineprofilen in Microsoft Intune

Intune umfasst mehrere Optionen zum Überwachen Ihrer Sicherheitsbaselines. Sie können:

- Eine Sicherheitsbaseline sowie alle Geräte überwachen, die den empfohlenen Werten entsprechen (oder nicht)
- Das Sicherheitsbaselineprofil überwachen, das für Ihre Benutzer und Geräte gilt
- Anzeigen der Konfiguration der Einstellungen eines ausgewählten Profils auf einem ausgewählten Gerät

Sie können auch die *Endpunktsicherheitskonfigurationen* anzeigen, die für einzelne Geräte gelten. Dies gilt auch für Sicherheitsbaselines.

In diesem Artikel werden beide Überwachungsoptionen vorgestellt.

Im Artikel [Erstellen einer Windows 10-Sicherheitsbaseline in Intune](security-baselines.md) finden Sie weitere Details zum Sicherheitsbaselinefeature in Microsoft Intune.

## <a name="monitor-the-baseline-and-your-devices"></a>Überwachen der Baseline und Ihrer Geräte

Wenn Sie eine Baseline überwachen, erhalten Sie basierend auf den Empfehlungen von Microsoft Einblicke in den Sicherheitsstatus Ihrer Geräte. Wenn Sie diese Informationen anzeigen möchten, melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an, navigieren Sie zu **Endpunktsicherheit** > **Sicherheitsbaselines**, und wählen Sie einen Sicherheitsbaselinetyp wie *MDM-Sicherheitsbaseline* aus. Wählen Sie dann im Bereich *Profil* die Profilinstanz aus, für die Sie Details anzeigen möchten. Daraufhin wird der Bereich mit den *Eigenschaften* des Profils geöffnet, in dem Sie im Abschnitt *Überwachung* einen beliebigen Profilbericht auswählen können. 

Im Anschluss an die Zuweisung einer Baseline dauert es 24 Stunden, bis die Daten angezeigt werden. Änderungen, die danach vorgenommen werden, werden innerhalb von sechs Stunden angezeigt.

Mithilfe eines Drillthroughs in Berichte und Geräte können Sie verschiedene Details anzeigen.

<!-- UI is changing, unclear how yet: 


- **Device view** – A summary of how many devices are in each status category for the baseline.
- **Per-category** - A view that displays each category in the baseline and includes the percentage of devices for each status group for each baseline category.

Each device is represented by one of the following statuses (used in the *device* view and also the *per-category* views):

- **Matches baseline** - All the settings in the baseline match the recommended settings.
- **Does not match baseline** - One or more settings in the baseline were modified from their default values in the original baseline. The default values in each security baseline are the recommended values for that baseline.

  > [!NOTE]
  > When you create or edit a baseline profile, any change that is made to a default value or configuration setting causes a *Does not match baseline* status to occur. For help to determine the settings that were changed, contact Microsoft Support. 

- **Misconfigured** - At least one setting isn't correctly configured. This status means that the setting is in a conflict, error, or pending state.
- **Not applicable** - At least one setting isn't applicable and isn't applied.

### Device view

The Overview pane displays a chart-based summary of how many devices have a specific status for the baseline; **Security baseline posture for assigned Windows 10 devices**.

![Check the status of the devices](./media/security-baselines-monitor/overview.png)

When a device has different status from different categories in the baseline, the device is represented by a single status. The status that represents the device is taken from the following order of precedence: **Misconfigured**, **Does not match baseline**, **Not applicable**, **Matches baseline**.

For example, if a device has a setting that's classified as *misconfigured* and one or more settings that are classified as *Does not match baseline*, the device is classified as *Misconfigured*.

You can click on the chart to drill through and view a list of devices with various statuses. You can then select individual devices from that list to view details about individual devices. For example:

- Select **Device configuration** > Select the profile with an Error state:

  ![View the status of a profile](./media/security-baselines-monitor/device-configuration-profile-list.png)

- Select the Error profile. A list of all settings in the profile, and their state is shown. Now, you can scroll to find the setting causing the error:

  ![See the setting causing the error](./media/security-baselines-monitor/profile-with-error-status.png)

Use this reporting to see any settings in a profile that are causing an issue. Also get more details of policies and profiles deployed to devices.

> [!NOTE]
> When a property is set to **Not configured** in the baseline, the setting is ignored, and no restrictions are enforced. The property isn't shown in any reporting.

### Per category view

The Overview pane displays a per-category chart for the baseline named **Security baseline posture by category**.  This view displays each category from the baseline, and identifies the percentage of devices that fall into a status classification for each of those categories.

![Per-Category view of status](./media/security-baselines-monitor/monitor-baseline-per-category.png)

Status for **Matches baseline** doesn't display until 100% of devices report that status for the category.

You can sort the by-category view by each column, by selecting up-down arrow icon at the top of the column.
-->

## <a name="monitor-the-profile"></a>Überwachen des Profils

Das Überwachen des Profils bietet einen Einblick in den Bereitstellungsstatus Ihrer Geräte, aber nicht in den Sicherheitsstatus gemäß der Baselineempfehlungen.

1. Klicken Sie in Intune auf **Sicherheitsbaselines**, und wählen Sie eine Baseline aus, um den dazugehörigen Bereich *Profile* zu öffnen.

<!-- More churn  
2. Select a profile. In **Overview**, the image shows how many devices and users have this profile assigned:

   ![See how many devices and users are assigned the security baselines profile](./media/security-baselines-monitor/existing-profile-overview.png)
--> 
3. Unter **Verwalten** > **Eigenschaften** wird eine Liste aller Einstellungen in der Baseline angezeigt. Sie können auch jede dieser Einstellungen ändern:

   ![Anzeigen und Aktualisieren von Einstellungen im Sicherheitsbaselineprofil](./media/security-baselines-monitor/manage-settings.png)

4. Unter **Überwachung** sehen Sie den Bereitstellungsstatus des Profils auf einzelnen Geräten, den Status für jeden Benutzer und den Status für jede Einstellung in der Baseline:

   ![Anzeigen der verschiedenen Überwachungsoptionen für ein Sicherheitsbaselineprofil](./media/security-baselines-monitor/monitor-status-options.png)

## <a name="view-settings-from-profiles-that-apply-to-a-device"></a>Anzeigen von für ein Gerät geltenden Profileinstellungen

Sie können ein Profil für eine Sicherheitsbaseline auswählen und einen Drilldown ausführen, um eine Liste der Einstellungen dieses Profils anzuzeigen, die für ein einzelnes Gerät gelten.  Zum Aufrufen dieser Liste müssen Sie auf **Endpunktsicherheit** > **Sicherheitsbaselines** > *Typ der Sicherheitsbaseline auswählen* > *gewünschtes Profil auswählen* > **Gerätestatus** klicken. Sie können die Liste auch anzeigen, indem Sie auf **Endpunktsicherheit** > **Alle Geräte** > *Gerät auswählen* > **Konfiguration der Endpunktsicherheit** > *Baselineversion auswählen* klicken.

Nachdem Sie ein Gerät ausgewählt haben, wird im Microsoft Endpoint Manager Admin Center eine Liste der Einstellungen dieses Profils angezeigt, einschließlich der Kategorie, zu der die Einstellung gehört, und des Konfigurationsstatus auf dem Gerät. Der Konfigurationsstatus kann wie folgt lauten:

- **Erfolg:** Die Einstellung auf dem Gerät entspricht dem Wert, der im Profil konfiguriert wurde. Dies ist entweder der standardmäßige und empfohlene Wert der Baseline oder ein benutzerdefinierter Wert, der bei der Konfiguration des Profils von einem Administrator angegeben wurde.
- **Konflikt:** Die Einstellung steht in Konflikt mit einer anderen Richtlinie, weist einen Fehler auf, oder es steht ein Update aus.
- **Nicht anwendbar:** Die Einstellung wird nicht von diesem Profil angewendet.

> [!NOTE]
> Die Statuswerte für Einstellungen werden in einem zukünftigen Release aktualisiert und weiter ausdifferenziert.

## <a name="view-endpoint-security-configurations-per-device"></a>Anzeigen der Endpunktsicherheitskonfigurationen pro Gerät

Sie können Details zu den Sicherheitskonfigurationen anzeigen, die für ein bestimmtes Gerät gelten. Dadurch können Sie gegebenenfalls Einstellungen identifizieren, die fehlerhaft konfiguriert wurden.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Navigieren Sie zu **Geräte**  >  **Alle Geräte**, und wählen Sie das Gerät aus, das Sie anzeigen möchten.

3. Klicken Sie in der Kategorie *Überwachen* auf **Endpoint security configuration** (Endpunktsicherheitskonfiguration), um die Liste der Sicherheitskonfigurationen anzuzeigen, die für das Gerät gelten.

4. Sie können auf eine Endpunktsicherheitskonfiguration klicken, um sie aufzuklappen und weitere Informationen zur Bewertung dieser Sicherheitskonfiguration auf dem Gerät anzuzeigen.

## <a name="troubleshoot-using-per-setting-status"></a>Problembehandlung bei der Verwendung von Status pro Einstellung

Sie haben eine Sicherheitsbaseline bereitgestellt, aber der Bereitstellungsstatus zeigt einen Fehler an. Die folgenden Schritte bieten Ihnen eine Anleitung zur Problembehandlung.

1. Klicken Sie in Intune auf **Sicherheitsbaselines**, wählen Sie eine Baseline aus, und klicken Sie auf **Profile**.

2. Wählen Sie ein Profil unter **Überwachung** > **Status pro Einstellung** aus.

3. Die Tabelle enthält alle Einstellungen und den Status jeder Einstellung. Wählen Sie die Spalte **Fehler** oder **Konflikt** aus, um die Einstellung anzuzeigen, die Ursache des Fehlers ist.

### <a name="mdm-diagnostic-information"></a>MDM-Diagnoseinformationen

Jetzt kennen Sie die problematische Einstellung. Der nächste Schritt ist, herauszufinden, warum diese Einstellung einen Fehler oder Konflikt verursacht.

Auf Windows 10-Geräten ist ein integrierter MDM-Diagnoseinformationsbericht verfügbar. Dieser Bericht enthält Standardwerte, aktuelle Werte, listet die Richtlinie auf, zeigt an, ob sie für das Gerät oder den Benutzer bereitgestellt wird, und vieles mehr. Verwenden Sie diesen Bericht, um zu ermitteln, warum die Einstellung einen Konflikt oder Fehler verursacht hat.

1. Navigieren Sie auf dem Gerät zu **Einstellungen** > **Konten** > **Zugriff auf Geschäfts-, Schul- oder Unikonto**.

2. Wählen Sie das Konto und dann **Informationen** > **Erweiterter Diagnosebericht** > **Bericht erstellen** aus.

3. Wählen Sie **Exportieren** aus, und öffnen Sie die generierte Datei.

4. Suchen Sie in den verschiedenen Abschnitten des Berichts nach der Fehler- oder Konflikteinstellung.

  Schauen Sie z.B. in den Abschnitt **Registrierte Konfigurationsquellen und Zielressourcen** oder **Nicht verwaltete Richtlinien**. So können Sie erfahren, warum der Fehler oder Konflikt verursacht wird.

[Diagnostizieren von MDM-Fehlern in Windows 10](/windows/client-management/mdm/diagnose-mdm-failures-in-windows-10) enthält weitere Informationen zu diesen integrierten Bericht.

> [!TIP]
>
> - Einige Einstellungen werden auch in der GUID aufgelistet. Sie können für diese GUID in der lokalen Registrierung (Regedit) nach festgelegten Werten suchen.
> - Die Protokolle der Ereignisanzeige können auch einige Fehlerinformationen zu der problematischen Einstellung enthalten (**Ereignisanzeige** > **Anwendungs- und Dienstprotokolle** > **Microsoft** > **Windows** > **DeviceManagement-Enterprise-Diagnostics-Provider** > **Admin** ).

## <a name="next-steps"></a>Nächste Schritte

- [Informationen zu Sicherheitsbaselines](security-baselines.md)
- [Vermeiden von Konflikten](security-baselines.md#avoid-conflicts)
- [Überwachen von Geräteprofilen](../configuration/device-profile-monitor.md) 
- [Häufige Probleme und Lösungen](../configuration/device-profile-troubleshoot.md)
- [Richtlinien und Profile zur Problembehandlung in Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)