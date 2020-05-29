---
title: Registrieren von Geräten in Desktop Analytics
titleSuffix: Configuration Manager
description: In diesem Artikel wird erläutert, wie Sie Geräte in Desktop Analytics registrieren.
ms.date: 04/15/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 2ea18d09-c957-47f7-8e54-c6f2b3c74347
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 22b5461df3a560449316009471ea029967118f5d
ms.sourcegitcommit: 97fbb7db14b0c4049c0fe3a36ee16a5c0cf3407a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/26/2020
ms.locfileid: "83864894"
---
# <a name="how-to-enroll-devices-in-desktop-analytics"></a>Registrieren von Geräten in Desktop Analytics

Wenn Sie [Configuration Manager mit Desktop Analytics verbinden](connect-configmgr.md), konfigurieren Sie die Einstellungen für das Registrieren von Geräten in Desktop Analytics. Sie können diese Einstellungen jederzeit ändern. Stellen Sie außerdem sicher, dass die Geräte auf dem neuesten Stand sind.

## <a name="update-devices"></a>Aktualisieren von Geräten

Desktop Analytics verwendet zwei Hauptkomponenten von Windows:

- **Kompatibilitätskomponente**: Die Kompatibilitätskomponente (**Appraiser**) führt die Diagnose des Windows-Geräts aus, um dessen Kompatibilität mit den neuesten Versionen von Windows 10 zu bewerten.

- **Dienst „Benutzererfahrung und Telemetrie im verbundenen Modus“** : Wenn Windows-Diagnosedaten aktiviert sind, erfasst der Dienst „Benutzererfahrung und Telemetrie im verbundenen Modus“ (**DiagTrack**) System-, Anwendungs- und Treiberdaten. Microsoft analysiert diese Daten und sendet sie über Desktop Analytics an Sie zurück.

Installieren Sie die neueste Version dieser Komponenten, um die bestmögliche Erfahrung mit Desktop Analytics zu erzielen.

In der folgenden Tabelle sind die Updates für die einzelnen Komponenten der unterstützten Betriebssystemversionen aufgeführt:

| BS-Version | Appraiser | DiagTrack |
| --------------| ----------------------- | -------------------|
| Windows 10 1909 | Enthalten <sup>[Hinweis 1](#bkmk_note1)</sup> | [Neuestes kumulatives Update](https://support.microsoft.com/help/4529964) |
| Windows 10 1903 | Enthalten <sup>[Hinweis 1](#bkmk_note1)</sup> | [Neuestes kumulatives Update](https://support.microsoft.com/help/4498140) |
| Windows 10 1809 | Enthalten <sup>[Hinweis 1](#bkmk_note1)</sup> | [Neuestes kumulatives Update](https://support.microsoft.com/help/4464619) |
| Windows 10 1803 | Enthalten <sup>[Hinweis 1](#bkmk_note1)</sup> | [Neuestes kumulatives Update](https://support.microsoft.com/help/4099479) |
| Windows 10 1709 | Enthalten <sup>[Hinweis 1](#bkmk_note1)</sup> | [Neuestes kumulatives Update](https://support.microsoft.com/help/4043454) |
| Windows 8.1 | [KB 2976978](https://support.microsoft.com/help/2976978) <sup>[Hinweis 2](#bkmk_note2)</sup> | [Neuestes monatliches Rollup](https://support.microsoft.com/help/4009470) |
| Windows 7 SP1 | [KB 2952664](https://support.microsoft.com/help/2952664) <sup>[Hinweis 3](#bkmk_note3)</sup> | [Neuestes monatliches Rollup](https://support.microsoft.com/help/4009469) |

> [!TIP]
> Verwenden Sie Configuration Manager, um die Updates automatisch zu installieren. Weitere Informationen finden Sie unter [Bereitstellen von Softwareupdates](../sum/deploy-use/deploy-software-updates.md).
>
> Starten Sie die Geräte neu, nachdem Sie die Kompatibilitätsupdates zum ersten Mal installiert haben.

### <a name="note-1-windows-10"></a><a name="bkmk_note1"></a> Hinweis 1: Windows 10

Während Windows 10 diese Komponenten standardmäßig enthält, benötigen Windows 10-Geräte das neueste kumulative Update, um die volle Funktionalität von Desktop Analytics wie die Bewertung der Kompatibilität des Geräts mit der neuesten Betriebssystemversion zu erhalten.

### <a name="note-2-windows-81"></a><a name="bkmk_note2"></a> Hinweis 2: Windows 8.1

Microsoft inkrementiert regelmäßig die Updates für diese Komponente, die zugehörige KB-Nummer ändert sich jedoch nicht. Stellen Sie sicher, dass Sie immer über die aktuelle Version des Updates verfügen.

Diese Komponente führt die Diagnose in Windows 8.1-Systemen aus, die am Programm zur Verbesserung der Benutzerfreundlichkeit von Windows teilnehmen. Mit diesen Diagnoseinformationen können Sie feststellen, ob beim Upgrade auf Windows 10 Kompatibilitätsprobleme auftreten können.

### <a name="note-3-windows-7"></a><a name="bkmk_note3"></a> Hinweis 3: Windows 7

Wenn Ihr Unternehmen keine Updates für „monatliches Qualitätsrollup“ auf Windows 7-Geräte anwendet und nur Updates für „Nur Sicherheit“ anwendet, finden Sie einige Updates für „Nur Sicherheit“ in der [Liste der Updates, die KB 2952664 ersetzen](https://www.catalog.update.microsoft.com/ScopedViewInline.aspx?updateid=ad3652cd-2689-4726-b3ef-b086ded23c7c). Sie können diese neueren Updates anstelle von KB 2952664 installieren.

> [!NOTE]
> Bei Windows 8.1 hat Microsoft nur KB 2976978 als Teil der Updates für „monatliches Qualitätsrollup“ überarbeitet.

## <a name="device-enrollment"></a>Geräteregistrierung

Für den Desktop Analytics-Dienst müssen keine Agents installiert werden. Für die Geräteregistrierung müssen Einstellungen auf den zu überwachenden Geräten konfiguriert werden. Mit diesen Einstellungen wird gesteuert, an welche Desktop Analytics-Instanz das Gerät seine Daten senden soll; außerdem werden andere Konfigurationsoptionen festgelegt.

> [!Note]  
> Wenn Sie bisher Windows Analytics verwendet haben, verwenden Sie für Desktop Analytics denselben Arbeitsbereich. Sie müssen zuvor in Windows Analytics registrierte Geräte in Desktop Analytics erneut registrieren.
>
> Pro Azure AD-Mandant kann nur ein Desktop Analytics-Arbeitsbereich vorhanden sein. Geräte können Diagnosedaten nur an einen Arbeitsbereich senden.  

Configuration Manager bietet eine integrierte Umgebung zum Verwalten und Bereitstellen dieser Einstellungen auf Clients. Verwenden Sie Configuration Manager, um eine optimale Leistung zu erzielen.

Wenn Sie Configuration Manager mit Desktop Analytics verbinden, konfigurieren Sie die Einstellungen für das Registrieren von Geräten. Weitere Informationen finden Sie unter [Herstellen einer Verbindung zwischen Configuration Manager und Desktop Analytics](connect-configmgr.md#bkmk_connect).

Gehen Sie folgendermaßen vor, um diese Einstellungen zu ändern:

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie den Eintrag **Clouddienste**, und wählen Sie anschließend den Knoten **Azure-Dienste** aus. Wählen Sie die Verbindung mit Desktop Analytics aus, und wählen Sie im Menüband die Option **Eigenschaften** aus.

2. Nehmen Sie auf der Seite **Diagnosedaten** die erforderlichen Änderungen an den folgenden Einstellungen vor:  

    - **Kommerzielle ID**: Dieser Wert wird automatisch mit der ID Ihrer Organisation aufgefüllt. Wenn dies nicht der Fall ist, vergewissern Sie sich vor dem Fortfahren, dass der Proxyserver so konfiguriert ist, dass alle erforderlichen [Endpunkte](enable-data-sharing.md#endpoints) zulässig sind. Sie können Ihre kommerzielle ID auch manuell über das [Desktop Analytics-Portal](monitor-connection-health.md#bkmk_ViewCommercialID) abrufen.

    - **Windows 10-Diagnosedatenebene**: Weitere Informationen finden Sie unter [Diagnosedatenebenen](enable-data-sharing.md#diagnostic-data-levels).  

    - **Gerätenamen in Diagnosedaten zulassen**: Weitere Informationen finden Sie unter [Gerätename](#device-name).  

    Wenn Sie Änderungen auf dieser Seite vornehmen, wird auf der Seite **Verfügbare Funktionalität** eine Vorschau der Desktop Analytics-Funktionen mit den ausgewählten Einstellungen für Diagnosedaten angezeigt.  

3. Nehmen Sie auf der Seite **Desktop Analytics-Verbindung** die erforderlichen Änderungen an den folgenden Einstellungen vor:

    - **Anzeigename:** Im Desktop Analytics-Portal wird die Configuration Manager-Verbindung mit diesem Namen angezeigt.  

    - **Zielsammlung**: Diese Sammlung enthält alle Geräte, die von Configuration Manager mit den Einstellungen für kommerzielle ID und Diagnosedaten konfiguriert werden. Dabei handelt es sich um sämtliche Geräte, die Configuration Manager mit dem Desktop Analytics-Dienst verbindet.  

    - **Geräte in der Zielsammlung verwenden einen vom Benutzer authentifizierten Proxy für die ausgehende Kommunikation**: In der Standardeinstellung ist dieser Wert **Nein**. Sollte Ihre Umgebung etwas anderes erfordern, legen Sie ihn auf **Ja** fest. Weitere Informationen finden Sie unter [Proxyserverauthentifizierung](enable-data-sharing.md#proxy-server-authentication).

    - **Wählen Sie bestimmte Sammlungen zur Synchronisierung mit Desktop Analytics aus**: Wählen Sie **Hinzufügen** aus, um weitere Sammlungen aus Ihrer Hierarchie **Zielsammlung** einzuschließen. Diese Sammlungen können im Desktop Analytics-Portal mit Bereitstellungsplänen gruppiert werden. Sie müssen Pilotsammlungen und Pilotausschlusssammlungen einschließen.  <!-- 4097528 -->

        > [!IMPORTANT]
        > Diese Sammlungen werden auch nach Ändern ihrer Mitgliedschaft weiterhin synchronisiert. Ihr Bereitstellungsplan verwendet beispielsweise eine Sammlung mit einer Windows 7-Mitgliedschaftsregel. Wird ein Upgrade dieser Geräte auf Windows 10 durchgeführt und Configuration Manager wertet die Sammlungsmitgliedschaft aus, werden diese Geräte aus der Sammlung und dem Bereitstellungsplan entfernt.

### <a name="windows-settings"></a>Windows-Einstellungen

Wenn Configuration Manager Geräte in Desktop Analytics registriert, legt es Windows-Richtlinien fest, um das Gerät für Desktop Analytics zu konfigurieren. In den meisten Fällen konfigurieren Sie diese Einstellungen ausschließlich mit Configuration Manager. Wenden Sie diese Einstellungen nicht gleichzeitig in Domänen-Gruppenrichtlinienobjekten an.

Weitere Informationen finden Sie unter [Gruppenrichtlinieneinstellungen für Desktop Analytics](group-policy-settings.md).

### <a name="device-name"></a>Gerätename

Ab Windows 10, Version 1803 wird der Gerätename nicht mehr standardmäßig erfasst. Die Erfassung des Gerätenamens in den Diagnosedaten muss separat aktiviert werden. Ohne den Gerätenamen ist es schwieriger festzustellen, welche Geräte beim Evaluieren eines Upgrades auf eine neue Windows-Version Aufmerksamkeit erfordern.

Wenn Sie den Gerätenamen nicht senden, wird dieser in Desktop Analytics als „Unbekannt“ angezeigt:

![Desktop Analytics-Geräteliste mit „Unbekannt“ als Namenseinträge](media/unknown-device-name.png)

Diese Einstellung kann mit einer Option in den Configuration Manager-Einstellungen für Desktop Analytics konfiguriert werden: **Gerätenamen in Diagnosedaten zulassen**. Diese Configuration Manager-Einstellung steuert die [Windows-Richtlinieneinstellung](group-policy-settings.md) **AllowDeviceNameInTelemetry**.

### <a name="conflict-resolution"></a>Konfliktauflösung

Im Allgemeinen verwenden Sie Configuration Manager-Sammlungen, um Desktop Analytics-Einstellungen und -Registrierung zu steuern. Verwenden Sie direkte Mitgliedschaften oder Abfragen, um Geräte in die Sammlung einzuschließen oder aus der Sammlung auszuschließen. Weitere Informationen finden Sie unter [Erstellen von Sammlungen](../core/clients/manage/collections/create-collections.md).

Configuration Manager konfiguriert nur die Windows-Einstellungen, wenn noch kein Wert vorhanden ist. Wenn Sie abweichende Einstellungen für eine eindeutige Gruppe von Geräten konfigurieren müssen, können Sie [Gruppenrichtlinien](group-policy-settings.md) verwenden. Von der Gruppenrichtlinie gesteuerte Einstellungen haben Vorrang vor Configuration Manager-Einstellungen. Der Status von Geräten, für die die Gruppenrichtlinie gilt, wird im Dashboard [Verbindungsintegrität](monitor-connection-health.md) möglicherweise nicht korrekt angezeigt.

Beim Konfigurieren der Diagnosedatenebene legen Sie die Obergrenze für das Gerät fest. Standardmäßig können Benutzer in Windows 10, Version 1803 und höher, eine niedrigere Ebene festlegen. Sie können dieses Verhalten mithilfe der Gruppenrichtlinien-Einstellung **Benutzeroberfläche für die Festlegung der Telemetrieaktivierung konfigurieren** steuern. Weitere Informationen finden Sie unter [Gruppenrichtlinieneinstellungen für Desktop Analytics](group-policy-settings.md).

### <a name="proxy-settings"></a>Proxyeinstellungen

Wenn Ihr Unternehmen die Proxyserverauthentifizierung für den Zugriff auf das Internet verwendet, stellen Sie sicher, dass die Authentifizierung oder Ihre Geräte richtig konfiguriert sind. Weitere Informationen finden Sie unter [Proxyserverauthentifizierung](enable-data-sharing.md#proxy-server-authentication).

## <a name="next-steps"></a>Nächste Schritte

Fahren Sie mit dem nächsten Artikel fort, um mehr über das Erstellen von Bereitstellungsplänen in Desktop Analytics zu erfahren.
> [!div class="nextstepaction"]
> [Erstellen von Bereitstellungsplänen](create-deployment-plans.md)
