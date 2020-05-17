---
title: Neues in Desktop Analytics
titleSuffix: Configuration Manager
description: In diesem Artikel erhalten Sie eine Übersicht über die neuen Funktionen in der aktuellen monatlichen Release des Desktop Analytics-Clouddiensts.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: fa300181-86cb-4afe-8fbf-895a7572378d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 1d45d115f279603fa74e143c603c116146278ffe
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268162"
---
# <a name="whats-new-in-desktop-analytics"></a>Neues in Desktop Analytics

Informieren Sie sich jeden Monat über Neuigkeiten in Desktop Analytics.

> [!TIP]
> Das Rollout eines monatlichen Updates kann bis zu drei Tage dauern. Die Einführung einiger Funktionen dauert möglicherweise mehrere Wochen, sodass sie in der ersten Woche nicht für alle Kunden verfügbar sind.

Um bei einer Aktualisierung dieser Seite benachrichtigt zu werden, kopieren Sie die folgende URL, und fügen Sie sie in Ihren RSS-Feedreader ein: `https://docs.microsoft.com/api/search/rss?search=%22what%27s+new+in+desktop+analytics+-+Configuration+Manager%22&locale=en-us`
<!-- a locale is required for the RSS search string -->

## <a name="may-2020"></a>Mai 2020

### <a name="reduce-the-number-of-apps-for-review"></a>Reduzieren der Anzahl von Apps für die Überprüfung

<!-- 5542186 -->

Um die Apps zu konsolidieren und ihre Anzahl auf der Objektseite im Portal zu reduzieren, werden nun alle Versionen von Apps mit dem gleichen Namen und Herausgeber zusammengefasst. Die App-Anzahl auf der Kachel **Beachtenswerte Apps** spiegelt diese Einstellung wider. Anstatt Hunderte von Instanzen von Microsoft Edge aufzulisten, wird jetzt eine Instanz für alle Versionen angezeigt. Sie können Entscheidungen einmal für alle Versionen treffen. Wenn Sie Entscheidungen für bestimmte Versionen einer App treffen müssen, ist dieses Verhalten konfigurierbar.

Weitere Informationen finden Sie unter [Informationen zu Objekten: Apps](about-assets.md#apps).

## <a name="march-2020"></a>März 2020

### <a name="support-for-multiple-hierarchies"></a>Unterstützung mehrerer Hierarchien

<!-- 4814075, 6079184 -->

Sie können jetzt mehrere Configuration Manager-Hierarchien mit einem einzelnen Azure Active Directory-Mandanten mit einer einzelnen kommerziellen ID für Desktop Analytics verbinden. Im Portal werden Geräte aus unterschiedlichen Hierarchien kategorisiert, und die Oberfläche für globale Pilotprojekte und Bereitstellungspläne wird verbessert.

- Wenn Sie beim Konfigurieren des globalen Pilotprojekts Sammlungen mit mehr als 20% der insgesamt registrierten Geräte hinzufügen, wird im Portal eine Warnung angezeigt.
- Wenn Sie beim Erstellen eines Bereitstellungsplans Sammlungen für mehrere Hierarchien auswählen, wird im Portal eine Warnung angezeigt.

> [!NOTE]
> Die Unterstützung mehrerer Hierarchien erfordert Configuration Manager-Version 1910 oder höher.

Weitere Informationen finden Sie in den folgenden Artikeln:

- [Globaler Pilot](deploy-pilot.md#bkmk_GlobalPilot)
- [Erstellen von Bereitstellungsplänen](create-deployment-plans.md)

### <a name="identify-compatibility-safeguards"></a>Ermitteln von Safeguard-Tags aufgrund von Kompatibilitätsproblemen

<!-- 5746559 -->

In den Windows-Kompatibilitätsdaten sind einige Apps und Treiber mit *Safeguard*-Tags klassifiziert, aufgrund derer beim Update auf Windows 10 möglicherweise ein Fehler auftritt oder ein Rollback durchgeführt wird. In Desktop Analytics können diese Tags jetzt vorab ermittelt werden, damit Sie ein Objekt entsprechend korrigieren können, bevor Sie das Update bereitstellen. Weitere Informationen finden Sie unter [Kompatibilitätsbewertung in Desktop Analytics](compat-assessment.md#safeguards).

## <a name="january-2020"></a>Januar 2020

### <a name="additional-app-usage-detail"></a>Weitere Informationen zur App-Verwendung

<!-- 5533890 -->

Wenn Sie eine App auswählen und weitere Informationen dazu aufrufen, finden Sie im Detailbereich nun zusätzliche Informationen zur Verwendung. Anhand dieser Daten erfahren Sie, wie oft eine App installiert wurde und auf welchen Geräten Benutzer sie regelmäßig verwenden. Weitere Informationen finden Sie unter [Informationen zu Objekten: App-Verwendung](about-assets.md#usage).

### <a name="provide-feedback-on-desktop-analytics"></a>Senden von Feedback zu Desktop Analytics

<!-- 5451636 -->

Klicken Sie oben im Portal auf das Symbol **Send a smile** (Lächeln senden), wenn Sie Feedback an Desktop Analytics übermitteln möchten. Weitere Informationen finden Sie unter [Senden von Produktfeedback](get-support.md#bkmk_feedback).

## <a name="october-2019"></a>Oktober 2019

### <a name="improvements-to-compatibility-recommendations"></a>Verbesserungen der Empfehlungen zur Kompatibilität

<!-- 3594545 -->

Wenn erkannt wird, dass eine Anwendung oder ein Treiber durch das Windows-Upgrade vollständig oder teilweise entfernt wird, bietet Desktop Analytics nun weitere Details. Weitere Informationen finden Sie unter [Bewertung der Kompatibilität](compat-assessment.md#asset-is-removed-during-upgrade).

### <a name="migrate-from-windows-analytics-to-existing-tenant"></a>Migrieren von Windows Analytics zu einem vorhandenen Mandanten

<!-- 5202803 -->

Sie können jetzt Eingaben aus einem vorhandenen Windows Analytics-Arbeitsbereich nach dem Onboarding in Desktop Analytics migrieren.

## <a name="september-2019"></a>September 2019

### <a name="migrate-inputs-from-windows-analytics"></a>Migrieren von Eingaben aus Windows Analytics

<!-- 4252663 -->

Während des Onboardings können Sie nun Eingaben aus einem vorhandenen Windows Analytics-Arbeitsbereich migrieren.

### <a name="offboard-from-desktop-analytics"></a>Offboarding aus Desktop Analytics

<!-- 4972396 -->

Wenn Sie Desktop Analytics in Ihrer Umgebung eingerichtet haben, den Dienst jedoch nicht mehr verwenden möchten, können Sie Ihr Konto nun schließen. Wenn Sie innerhalb von 90 Tagen Ihre Meinung ändern, können Sie das Konto erneut aktivieren. Weitere Informationen erhalten Sie unter [Schließen Ihres Kontos](account-close.md).

## <a name="august-2019"></a>August 2019

### <a name="reset-your-account"></a>Zurücksetzen Ihres Kontos

<!-- 3733897 -->

Wenn Sie Desktop Analytics in Ihrer Umgebung eingerichtet haben, jedoch mit dem Onboarding und der Registrierung von vorn beginnen möchten, können Sie es zurücksetzen. Weitere Informationen zu diesem Vorgang finden Sie unter [Zurücksetzen Ihres Kontos](account-reset.md).

### <a name="automatic-upgrade-decision-of-system-and-store-apps"></a>Entscheidungen zum automatischen Upgrade von System-und Store-Apps

<!-- 3587232 -->

Um den Aufwand hinsichtlich der Kommentierung von wichtigen Apps zu mindern, werden bestimmten App-Typen automatisch als *Nicht wichtig* markiert. Außerdem wird die Upgrade-Entscheidung des Bereitstellungsplans für diese Apps als *Bereit* markiert. Die folgenden Apps sind kompatibel und sollten nach dem Upgrade von Windows weiterhin funktionieren:

- Von Microsoft veröffentlichte Systemkomponenten und -Apps

- Im Microsoft Store verwaltete und aktualisierte Apps

Weitere Informationen erhalten Sie unter [Entscheidungen zum automatischen Upgrade von System-und Store-Apps](about-assets.md#bkmk_plan-autoapp).

## <a name="whats-new-in-configuration-manager"></a>Neuerungen in Configuration Manager

Die Desktop Analytics-Dokumentation bezieht sich immer auf die Funktionen in der aktuellen Version des Current Branch von Configuration Manager. Weitere Informationen zu den aktuellen Änderungen in Configuration Manager finden Sie in den folgenden Artikeln:

<!-- - [What's new in version 1910](../core/plan-design/changes/whats-new-in-version-1910.md#bkmk_da) -->

- [Neuerungen in Version 1906](../core/plan-design/changes/whats-new-in-version-1906.md#bkmk_da)

## <a name="deprecated-features"></a>Veraltete Features

Wenn Microsoft plant, ein wichtiges Feature des Desktop Analytics-Diensts zu entfernen, wird diese Änderung im Voraus als veraltetes Feature von Configuration Manager angekündigt. Weitere Informationen finden Sie unter [Veraltete Features](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features).
