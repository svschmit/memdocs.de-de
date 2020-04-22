---
title: Objekte in Desktop Analytics
titleSuffix: Configuration Manager
description: In diesem Artikel erfahren Sie mehr über Geräte, Treiber und Apps in Desktop Analytics.
ms.date: 01/16/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: d07198cf-49bb-4712-8c63-063b4302cc11
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fe1338781cbb16a8485de050a294e34e487a2ecc
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706648"
---
# <a name="assets-in-desktop-analytics"></a>Objekte in Desktop Analytics

Nachdem Geräte Daten an Desktop Analytics gemeldet haben, wird ein Inventar der folgenden Objekte bereitgestellt:

- Geräte
- Installierte Apps  

Wählen Sie im Dienstportal im Menü „Desktop Analytics“ die Option **Objekte** aus.

## <a name="devices"></a>Geräte

Auf der Registerkarte **Geräte** werden wichtige Informationen zu allen bei Desktop Analytics registrierten Geräten in Ihrer Organisation angezeigt. Sie können nach einer beliebigen Spalte sortieren oder nach bestimmten Werten filtern.

> [!NOTE]  
> Wenn das Dashboard nicht die Anzahl der Geräte meldet, die Sie für Ihre Umgebung erwarten, sehen Sie den Artikel [Problembehandlung bei Desktop Analytics](troubleshooting.md) ein.  

In einem Bereitstellungsplan sind weitere Details zu Geräten enthalten. Weitere Informationen finden Sie unter [Planobjekte](about-deployment-plans.md#plan-assets).

## <a name="apps"></a>Apps

Auf der Registerkarte **Apps** werden alle installierten Apps angezeigt, die vom Dienst auf Ihren Windows-Geräten erkannt werden.

**Beachtenswerte** Apps sind auf mehr als 2 % der registrierten Geräte installiert.

Konfigurieren Sie die **Wichtigkeit** von Apps, indem Sie eine der folgenden Kategorien festlegen:

- Kritisch
- Wichtig
- Ignorieren
- Nicht überprüft
- Nicht wichtig<!-- 3587232 -->

Wählen Sie die App aus der Liste aus, und wählen Sie **Bearbeiten** aus. Durch diese Aktion werden Details für die App angezeigt. Wählen Sie das Dropdownmenü **Wichtigkeit** aus, und legen Sie einen Wert fest. Sie können auch einen **Besitzer**zuweisen. Wenn Sie Änderungen vornehmen, wählen Sie **Speichern** aus.

### <a name="automatic-upgrade-decision-of-system-and-store-apps"></a><a name="bkmk_plan-autoapp" /> Entscheidungen zum automatischen Upgrade von System-und Store-Apps

<!-- 3587232 -->
Das Bestimmen von **Wichtigkeit** und **Upgradeentscheidung** ist unerlässlich für alle beachtenswerten Apps im Desktop Analytics-Workflow. Um den Aufwand hinsichtlich der Kommentierung dieser Apps zu mindern, werden bestimmte App-Typen automatisch als *Nicht wichtig* markiert. Außerdem wird die Upgrade-Entscheidung des Bereitstellungsplans für diese Apps als *Bereit* markiert. Die folgenden Apps sind kompatibel und sollten nach dem Upgrade von Windows weiterhin funktionieren:

- Von Microsoft veröffentlichte Systemkomponenten und -Apps

- Im Microsoft Store verwaltete und aktualisierte Apps

> [!TIP]
> Verwalten Sie Eingaben für Apps auf globaler Ebene oder nach Bereitstellungsplan.
>
> 1. Wählen Sie im Desktop Analytics-Portal im Menü **Verwalten** die Option **Objekte** aus. Wählen Sie anschließend **Apps** aus.
>
> 2. Verwalten Sie anhand der Spalten **Typ** und **Kategorie** diese App-Kategorien:
>
>    - Filtern Sie für Store-Apps **Typ** nach **Modern**
>    - Filtern Sie für System-Apps **Kategorie** nach **Hintergrundprozess** oder **Windows-Komponente**

In einem Bereitstellungsplan können Sie auch die **Upgradeentscheidung**festlegen. Weitere Informationen finden Sie unter [Planobjekte](about-deployment-plans.md#plan-assets).

### <a name="usage"></a>Verwendung

<!-- 5533890 -->

- **Gesamtzahl der Installationen:** Dieser Wert stellt die Anzahl der Installationen der ausgewählten App auf allen Geräten dar, die für Desktop Analytics registriert sind.

- **Prozentsatz der Installationen:** Dieser Wert sagt aus, auf wie vielen Geräten die ausgewählte App prozentual zur Gesamtzahl der für Desktop Analytics registrierten Geräte installiert wurde.

- **Anzahl der Geräte, die diese App in den letzten 30 Tagen gestartet haben:** Dieser Wert gibt die Anzahl der Geräte wieder, auf denen ein Benutzer die ausgewählte App gestartet hat. Dafür werden nur Geräte berücksichtigt, von denen in den letzten 30 Tagen eine Nutzung gemeldet wurde. Dieser Wert setzt sich aus den Daten aller Geräte zusammen, auf denen Desktop Analytics unter einer beliebigen Version von Windows 10 ausgeführt wird. Es ist möglich, dass diese Anzahl innerhalb eines Bereitstellungsplans variiert.

## <a name="next-steps"></a>Nächste Schritte

- [Informationen zu Desktop Analytics-Bereitstellungsplänen](about-deployment-plans.md)  

- [Informationen zu Sicherheits- und Featureupdates](about-updates.md)  

- [Compatibility assessment in Desktop Analytics](compat-assessment.md) (Kompatibilitätsbewertung in Desktop Analytics)  
