---
title: Ready for Windows
titleSuffix: Configuration Manager
description: Informationen zur Einstellung der Ready for Windows-Website
ms.date: 04/21/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 3f09226c-4ca7-4e43-9ae8-5ee6e78e6bc2
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ROBOTS: NOINDEX
ms.openlocfilehash: 63aba639eea221c3a13f7ebeabaa1b96a8439a72
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700768"
---
# <a name="ready-for-modern-desktop-retirement-faq"></a>Häufig gestellte Fragen zur Einstellung von „Ready for Modern Desktop“

<!-- placeholder -->

## <a name="ready-for-windows-adoption-status"></a>Status „Für Windows-Einführung bereit“

Der Einführungsstatus basiert auf Informationen von kommerziellen Geräten, die Daten an Microsoft weitergeben. Der Status ist in Supporthinweise von Softwareanbietern integriert.

Desktop Analytics gibt den Einführungsstatus für jede Version eines Objekts an, das auf kommerziellen Geräten gefunden wurde. Dieser Status enthält keine Daten von Endanwendergeräten oder Geräten, die keine Daten übermitteln. Der Status ist möglicherweise nicht repräsentativ für die Einführungsrate auf allen Windows 10-Geräten.

Mögliche Kategorien:

- **Umfassend eingeführt**: Diese App wurde auf mindestens 100.000 kommerziellen Windows 10-Geräten installiert.

- **Eingeführt**: Diese App wurde auf mindestens 10.000 kommerziellen Windows 10-Geräten installiert.

- **Unzureichende Daten**: Zu wenige kommerzielle Windows 10-Geräte teilen Informationen zu dieser App mit Microsoft, sodass die Einführung nicht kategorisiert werden kann.

- **Entwickler kontaktieren**: Möglicherweise treten Kompatibilitätsprobleme mit dieser Version der App auf. Microsoft empfiehlt, den Softwareanbieter zu kontaktieren, um weitere Informationen einzuholen.

- **Unbekannt**: Für diese Version der Anwendung sind keine Informationen verfügbar. Eventuell sind Informationen zu anderen Versionen der Anwendung vorhanden.

## <a name="general"></a>Allgemein

### <a name="what-happened-to-the-ready-for-windows-website"></a>Was hat sich bei der Ready for Windows-Website geändert?

Für viele Kunden ist es eine Herausforderung, zu Windows 10 und Office 365 ProPlus immer auf dem neuesten Stand zu bleiben. Die größte Herausforderung ist das Testen von Anwendungen, da dieser Vorgang in der Regel manuell erfolgt. IT-Administratoren und Anwendungsbesitzer verbringen viel Zeit damit, vorhandene Anwendungen laufend zu analysieren und dann auftretende Probleme zu beheben.

Im Verzeichnis *Ready for modern desktop* werden Softwarelösungen aufgeführt, die auf kommerziellen Geräten mit Windows 10 und Office 365 ProPlus unterstützt und in der Praxis verwendet werden. Das Verzeichnis unterstützt IT-Manager, die die neuesten Versionen von Windows 10 und Office 365 für Ihre Bereitstellungen in Erwägung ziehen.

IT-Managern haben den Wunsch geäußert, dass diese Informationen in die von ihnen bereits verwendeten Tools zur Planung der Bereitstellungspläne integriert werden. Mit [Desktop Analytics](https://aka.ms/dadocs) und [Office 365 ProPlus Readiness-Funktionen](/deployoffice/readiness-tools#office-365-proplus-readiness-features-in-configuration-manager-current-branch) in Configuration Manager können Sie Ihre Upgradeprojekte für Windows 10 und Office 365 ProPlus planen. 

> [!Note]
> Ab dem 21. April 2020 wird Office 365 ProPlus in **Microsoft 365 Apps for Enterprise** umbenannt. Weitere Informationen finden Sie unter [Namensänderung für Office 365 ProPlus](/deployoffice/name-change). Möglicherweise finden Sie während des Updates der Konsole noch Verweise auf den alten Namen in der Configuration Manager-Konsole und der unterstützenden Dokumentation.

### <a name="what-is-desktop-analytics"></a>Was ist Desktop Analytics?

[Desktop Analytics](https://aka.ms/dadocs) ist ein cloudbasierter Dienst, der in Configuration Manager integriert ist. Der Dienst bietet Einblicke und Informationen, mit denen Sie fundiertere Entscheidungen zur Updatebereitschaft Ihrer Windows-Endpunkte treffen können. Er kombiniert die Daten, die für Ihre Organisation spezifisch sind, mit aggregierten Erkenntnissen zu Millionen von Windows-Geräten, die mit den Clouddiensten von Microsoft verbunden sind.

-    Verschaffen Sie sich einen umfassenden Überblick über die Endpunkte, Anwendungen und Treiber, die in Ihrer Organisation verwaltet werden.

-    Bewerten Sie die Anwendungs- und Treiberkompatibilität mit den neuesten Windows-Featureupdates. Erhalten Sie Empfehlungen zur Behebung bekannter Probleme sowie erweiterte Einblicke für branchenspezifische Apps.

-    Verwenden Sie künstliche Intelligenz (KI) aus der Microsoft-Cloud, um die Gruppe von Pilotgeräten zu optimieren, die ein repräsentatives Bild Ihrer Gesamtumgebung abgeben.

### <a name="why-should-i-use-desktop-analytics-for-my-windows-deployment-plans"></a>Warum sollte ich Desktop Analytics für meine Windows-Bereitstellungspläne verwenden?

Desktop Analytics bietet die folgenden Vorteile:

-    **Geräte- und Softwareinventar**: Inventuraufnahme von Schlüsselfaktoren wie Apps und Windows-Versionen.

-    **Identifizieren für die Pilotphase**: Identifizieren der kleinsten Gruppe von Geräten, mit der die größte Abdeckung von Faktoren gegeben ist. Der Schwerpunkt liegt dabei auf den Faktoren, die für einen Pilotversuch von Windows-Upgrades und -Updates am wichtigsten sind. Indem Sie eine erfolgreichere Durchführung des Pilotversuchs sicherstellen, können Sie schneller und zuverlässiger zu umfassenden Produktionsbereitstellungen wechseln.

-    **Identifizieren von Problemen**: Anhand von aggregierten Marktdaten und Daten aus Ihrer Umgebung prognostiziert der Dienst potenzielle Probleme bei der laufenden Aktualisierung von Windows. Anschließend werden potenzielle Maßnahmen zur Risikominderung vorgeschlagen.

-    **Configuration Manager-Integration**: Ihre vorhandene lokale Infrastruktur wird mit Cloudunterstützung versehen. Verwenden Sie diese Daten und Analysen, um Windows auf Ihren Geräten bereitzustellen und zu verwalten.

### <a name="what-does-the-ready-for-windows-status-mean-in-desktop-analytics"></a>Was bedeutet der Status *Ready for Windows* in Desktop Analytics?

Der **Einführungsstatus** basiert auf Informationen von kommerziellen Geräten, die Daten an Microsoft weitergeben. Der Status ist in Supporthinweise von Softwareanbietern integriert.

Desktop Analytics gibt den Einführungsstatus für jede Version eines Objekts an, das auf kommerziellen Geräten gefunden wurde. Dieser Status enthält keine Daten von Endanwendergeräten oder Geräten, die keine Daten übermitteln. Der Status ist möglicherweise nicht repräsentativ für die Einführungsrate auf allen Windows 10-Geräten.

Weitere Informationen finden Sie unter [Bewertung der Kompatibilität](compat-assessment.md).

### <a name="what-assets-get-the-ready-for-windows-status-in-desktop-analytics"></a>Welche Objekte erhalten den Status *Ready for Windows* in Desktop Analytics? 

Objekte erhalten den Status *Ready for Windows* in Desktop Analytics unter folgenden Umständen:

-    Der Softwareanbieter erklärt, dass die Lösung unterstützt wird.
-    Kunden haben diese auf einer großen Anzahl kommerzieller Windows 10-Geräte bereitgestellt, die Informationen an Microsoft weitergeben.
-    Das Objekt ist für kommerzielle Benutzer relevant.

### <a name="what-additional-insights-do-i-get-in-desktop-analytics"></a>Welche zusätzlichen Einblicke erhalte ich in Desktop Analytics?

Desktop Analytics bietet eine Inventur der [Geräte und der installierten Apps](about-assets.md)sowie [erweiterte Einblicke](compat-assessment.md#advanced-insights) für branchenspezifische Apps. 

## <a name="software-providers"></a>Softwareanbieter

### <a name="can-i-still-list-my-software-solution-in-desktop-analytics"></a>Kann ich meine Softwarelösung weiterhin in Desktop Analytics aufnehmen lassen?

Veröffentlichen Sie einen Supporthinweis, der besagt, dass Ihr Produkt mit 32-Bit- oder 64-Bit-Windows 10 oder Office 365 ProPlus funktioniert. Um Ihre Lösungen in Desktop Analytics vorzustellen, wenden Sie sich an Ihre Microsoft-Kontaktperson.

### <a name="how-can-listing-my-solutions-benefit-me"></a>Welche Vorteile bietet ein Eintrag für meine Lösung?

Tausende von IT-Administratoren verwalten Millionen von Geräten mit Configuration Manager und Desktop Analytics. Mit diesen Tools können sie ihre Organisationen zuverlässig auf die neueste Version von Windows 10 und Office 365 ProPlus aktualisieren. Sie werden auch verwendet, um Kaufentscheidungen für Softwarelösungen zu treffen.

Microsoft integriert Supporthinweise von Softwareanbietern mit den Einführungsinformationen, die Sie von kommerziellen Geräten erhalten. Organisationen auf der ganzen Welt verwenden diese Daten dann in den Tools Desktop Analytics und Office Readiness. 

Wenn Ihr Supporthinweis nicht ordnungsgemäß mit Objekten verknüpft sind, wenden Sie sich an Ihre Microsoft-Kontaktperson.

### <a name="can-i-see-detailed-performance-metrics-on-my-assets"></a>Lassen sich ausführliche Leistungsmetriken für meine Objekte anzeigen?

Evaluieren Sie die Leistung Ihrer Lösungen mit Integritäts- und Metrikberichten über das Developer Center: 

- [Windows Store](/windows/uwp/publish/health-report)
- [Desktop](/windows/desktop/appxpkg/windows-desktop-application-program)
- [Office-Add-Ins](/office/dev/store/update-unpublish-and-view-metrics) 

### <a name="how-can-i-develop-compatible-assets-for-windows-10-and-office-365-proplus"></a>Wie kann ich kompatible Objekte für Windows 10 und Office 365 ProPlus entwickeln?

Stellen Sie sicher, dass Ihre Desktopanwendungen jetzt und in Zukunft mit Windows 10 kompatibel sind. Weitere Informationen finden Sie unter [Anwendungskompatibilität für Entwickler](https://developer.microsoft.com/windows/desktop/app-compatibility).

Wenn Sie Lösungen für Office 365 ProPlus entwickeln, lesen Sie [Bewährte Methoden für die Entwicklung von com-, VSTO-und VBA-Add-Ins in Office](/visualstudio/vsto/development-best-practices-for-com-vsto-and-vba-add-ins-in-office).