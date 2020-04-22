---
title: Updates in Desktop Analytics
titleSuffix: Configuration Manager
description: In diesem Artikel werden Sicherheits- und Featureupdates in Desktop Analytics erläutert.
ms.date: 08/21/2019
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 14ae894c-26fb-4fe3-b51d-e80700122df4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ec510414f11aa312e6c1a7d1d5bfa8126f473fe3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706578"
---
# <a name="updates-in-desktop-analytics"></a>Updates in Desktop Analytics

Im Desktop Analytics-Portal können Sie den Status von Sicherheits-und Featureupdates verfolgen. Wählen Sie diese Knoten in der Gruppe „Überwachen“ des Hauptmenüs von Desktop Analytics aus. Über die Knoten erhalten Sie Einblicke in den Status dieser Updates in Ihrer Umgebung.


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

Weist ein Windows 10-Gerät *keine Authentifizierung* mit einem Microsoft-Konto auf, werden diese Daten von Windows nicht gemeldet. Diese Authentifizierung wird im Allgemeinen im Rahmen der Out-of-Box-Experience (OOBE) des Windows Setup ausgeführt.<!-- 5148153 -->


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

Weist ein Windows 10-Gerät *keine Authentifizierung* mit einem Microsoft-Konto auf, werden diese Daten von Windows nicht gemeldet. Diese Authentifizierung wird im Allgemeinen im Rahmen der Out-of-Box-Experience (OOBE) des Windows Setup ausgeführt.<!-- 5148153 -->


## <a name="next-steps"></a>Nächste Schritte

- [Informationen zu Desktop Analytics-Objekten](about-assets.md): Geräte, Treiber und Apps  

- [Informationen zu Bereitstellungsplänen](about-deployment-plans.md)  
