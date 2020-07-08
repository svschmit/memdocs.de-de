---
title: Updates in Desktop Analytics
titleSuffix: Configuration Manager
description: In diesem Artikel werden Sicherheits- und Featureupdates in Desktop Analytics erläutert.
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 14ae894c-26fb-4fe3-b51d-e80700122df4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 96a014f4919480854b57bae82e982ce783f5f59b
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590965"
---
# <a name="updates-in-desktop-analytics"></a>Updates in Desktop Analytics

Im Desktop Analytics-Portal können Sie den Status von Sicherheits-und Featureupdates verfolgen. Wählen Sie diese Knoten in der Gruppe „Überwachen“ des Hauptmenüs von Desktop Analytics aus. Über die Knoten erhalten Sie Einblicke in den Status dieser Updates in Ihrer Umgebung.

<!--7362999-->

> [!IMPORTANT]
> Desktop Analytics zeigt den Status der Sicherheits- und Featureupdates für Geräte mit der kommerziellen ID an, die Ihrem Desktop Analytics-Arbeitsbereich zugeordnet sind. Dieses Verhalten tritt unabhängig davon auf, ob Sie die Geräte bei Configuration Manager registriert haben. Die Gesamtanzahl der Geräte auf diesen Kacheln stimmt möglicherweise nicht mit der Anzahl der registrierten Geräte in den [**verbundenen Diensten**](monitor-connection-health.md#commercial-id-configuration) überein.

## <a name="security-updates"></a>Sicherheitsupdates

Wählen Sie zum Überprüfen des aktuellen Status von Sicherheitsupdates im Abschnitt **Überwachen** von Desktop Analytics die Option **Sicherheitsupdates** aus:

![Knoten „Sicherheitsupdates“ von Desktop Analytics](media/security-updates.png)

Diese Ansicht bietet eine Zusammenfassung der *Sicherheitsupdates* für Windows 10-Geräte. Geräte im Balkendiagramm werden anhand der folgenden Bezeichnungen kategorisiert:

#### <a name="latest"></a>Neueste

Auf den Geräten wird das neueste Sicherheitsupdate für die betreffende Version und den betreffenden Kanal ausgeführt.

#### <a name="latest-1"></a>Neueste -1

Geräte mit einem Sicherheitsupdate, das um eine Version älter als das letzte verfügbare Update für diesen Kanal ist.

#### <a name="older"></a>Älter

Auf Geräten wird ein Sicherheitsupdate ausgeführt, das älter ist als „Neueste -1“.

#### <a name="not-measured"></a>Nicht gemessen

Das Gerät wurde von Desktop Analytics nicht bewertet. Diesen Status weisen Geräte unter Windows 7, Windows 8.1 oder Windows 10 auf, die für das Windows-Insider-Programm registriert sind.  

Klicken Sie für eine bestimmte Windows-Version auf **Mehr anzeigen**, um die Trends bei der Akzeptanz von Sicherheitsupdates anzuzeigen. Das gestapelte Flächendiagramm kategorisiert Geräte nach dem Sicherheitsupdate, das auf diesen im Laufe der Zeit installiert wurde.

Klicken Sie auf **Alles anzeigen**, um den Bereitstellungsstatus für Sicherheitsupdates zu überprüfen. In dieser Ansicht werden Geräte in den folgenden Kategorien aufgelistet:

- Nicht gestartet
- In Bearbeitung
- Abgeschlossen
- Eingreifen erforderlich – Geräte (sortiert nach Gerätename)
- Eingreifen erforderlich – Probleme (sortiert nach Problemtyp)

Klicken Sie auf **Aktuelle Daten anzeigen**, um Geräte mit neuen Informationen anzuzeigen, die vom Dienst noch verarbeitet werden. Desktop Analytics zeigt diese Informationen nach der nächsten vollständigen Aktualisierung der Daten an.

  > [!IMPORTANT]
  > Die Desktop Analytics-Option **Aktuelle Daten anzeigen** ist veraltet. Diese Aktion wird in einer zukünftigen Version des Desktop Analytics-Diensts entfernt. Weitere Informationen finden Sie unter [Veraltete Features](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!--7080949-->  

## <a name="feature-updates"></a>Featureupdates

Wählen Sie zum Überprüfen des aktuellen Status von Featureupdates im Abschnitt **Überwachen** von Desktop Analytics die Option **Featureupdates** aus:

![Knoten „Featureupdates“ von Desktop Analytics](media/feature-updates.png)

Diese Ansicht bietet eine Zusammenfassung der *Featureupdates* für Windows 10-Geräte.

Weitere Informationen zu Serviceintervallen finden Sie im [Informationsblatt zum Lebenszyklus von Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).  

Geräte im Balkendiagramm werden anhand der folgenden Bezeichnungen kategorisiert:

#### <a name="in-service"></a>Aktiv

Auf den Geräten wird das neueste Featureupdate für die betreffende Version und den betreffenden Kanal ausgeführt.  

#### <a name="near-end-of-service"></a>Bald Ende des Diensts

Auf Geräten wird ein Featureupdate ausgeführt, für das innerhalb von spätestens 90 Tagen der Dienst eingestellt wird.

#### <a name="end-of-service"></a>Ende des Diensts

Auf Geräten wird ein Featureupdate ausgeführt, für das der Dienst bereits eingestellt wurde. Diese Datumsangaben gelten speziell für die Editionen „Enterprise“ und „Education“ von Windows. Sie gelten nicht für die Editionen „Home“, „Pro“, „Pro Education“ oder „Pro for Workstations“. Weitere Informationen finden Sie im [Informationsblatt zum Lebenszyklus von Windows](https://support.microsoft.com/help/13853/windows-lifecycle-fact-sheet).

#### <a name="not-measured"></a>Nicht gemessen

Das Gerät wurde von Desktop Analytics nicht bewertet. Diesen Status weisen Geräte unter Windows 7, Windows 8.1 oder Windows 10 auf, die für das Windows-Insider-Programm registriert sind.

Klicken Sie auf die Kachel, um die Trends bei der Akzeptanz von Funktionsupdates anzuzeigen. Das gestapelte Flächendiagramm kategorisiert Geräte nach dem Funktionsupdate, das auf diesen im Laufe der Zeit installiert wurde.

## <a name="next-steps"></a>Nächste Schritte

- [Informationen zu Desktop Analytics-Objekten](about-assets.md): Geräte, Treiber und Apps  

- [Informationen zu Bereitstellungsplänen](about-deployment-plans.md)  
