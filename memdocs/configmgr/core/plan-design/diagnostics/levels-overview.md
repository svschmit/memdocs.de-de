---
title: Ebenen von Nutzungsdaten zu Diagnosezwecken
titleSuffix: Configuration Manager
description: Hier erfahren Sie mehr über die Ebenen der Diagnose- und Nutzungsdaten, die Configuration Manager sammelt.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: 3c46bdb2-5bda-47c8-b5f4-9365a4b3521c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0d27e4a2f82de75cde853f3ce95c98ea8a12c465
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126504"
---
# <a name="levels-of-diagnostic-usage-data"></a>Ebenen von Nutzungsdaten zu Diagnosezwecken

*Gilt für: Configuration Manager (Current Branch)*

Configuration Manager sammelt drei Arten von Diagnose- und Nutzungsdaten: **Einfach**, **Erweitert** und **Vollständig**. Standardmäßig ist dieses Feature auf die Ebene „Erweitert“ festgelegt.

> [!IMPORTANT]
> Configuration Manager sammelt auf den Ebenen „Einfach“ und „Erweitert“ keine Standortcodes, Standortnamen, IP-Adressen, Benutzer- oder Computernamen, physischen Adressen oder E-Mail-Adressen. Eine Erfassung dieser Informationen auf der Ebene „Vollständig“ ist nicht zielführend. Erst in erweiterten Diagnoseinformationen wie Protokolldateien oder Arbeitsspeichermomentaufnahmen sind diese Informationen möglicherweise enthalten. Microsoft nutzt diese Informationen weder, um Sie zu identifizieren oder zu kontaktieren, noch zu Werbezwecken.

## <a name="levels"></a>Ebenen

### <a name="basic"></a>Einfach

Die Ebene „Einfach“ umfasst Daten zu Ihrer Hierarchie. Sie ist zur Verbesserung der Installation oder des Upgrades erforderlich. Mithilfe dieser Daten können außerdem die Configuration Manager-Updates ermittelt werden, die für Ihre Hierarchie infrage kommen.

### <a name="enhanced"></a>Erweitert

Die Ebene „Erweitert“ ist die Standardeinstellung nach dem Setup. Diese Ebene umfasst Daten, die von der Ebene „Einfach“ gesammelt werden, sowie featurespezifische Daten. Sie zeigt die Häufigkeit und Dauer der Verwendung verschiedener Features an. Außerdem werden Daten zu den folgenden Configuration Manager-Clienteinstellungen gesammelt: Komponentenname, Zustand und spezifische Einstellungen wie Abrufintervalle. Informationen zu Softwareupdates sind bei der Verwendung von Features grundlegend. Sie enthalten keine Daten zur Updatekonformität auf dieser Ebene.

Diese Ebene wird von Microsoft empfohlen, da sie die mindestens erforderlichen Daten erhalten, um Produkte und Dienste zu verbessern.

Einige Beispiele für Daten, die auf dieser Ebene nicht erfasst werden, sind folgende:

- Namen von Websites, Benutzern, Computern oder anderen Objekten

- Details zu sicherheitsbezogenen Objekten

- Sicherheitsrisiken wie die Anzahl der Systeme, die Softwareupdates erfordern

### <a name="full"></a>Vollständig

Die Ebene „Vollständig“ umfasst alle Daten der Ebenen „Basis“ und „Erweitert“. Darüber hinaus werden zusätzliche Informationen zu Endpoint Protection, die Prozentsätze zur Updatekompatibilität sowie Informationen zu Softwareupdates erfasst. Diese Ebene kann auch erweiterte Diagnoseinformationen wie Systemdateien und Arbeitsspeichermomentaufnahmen enthalten. Zu diesen erweiterten Daten können personenbezogene Daten gehören, die zum Zeitpunkt der Erfassung im Arbeitsspeicher oder in Protokolldateien enthalten sind.

## <a name="how-to-change-the-level"></a><a name="bkmk_change"></a> Ändern der Ebene

Zum Ändern der Datensammlungsebene benötigen Sie Berechtigungen zum **Ändern** der **Site**-Objektklasse.

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Standorte** aus.
1. Klicken Sie im Menüband auf **Hierarchieeinstellungen**.
1. Wechseln Sie zur Registerkarte **Diagnose- und Nutzungsdaten**, und wählen Sie dann die Datenebene aus.

## <a name="version-specific-details"></a><a name="bkmk_versions"></a> Versionsspezifische Details

In den folgenden Artikeln werden die spezifischen Daten beschrieben, die Configuration Manager auf jeder Ebene mit jeder unterstützten Version sammelt:

- [Diagnose- und Nutzungsdaten für Version 2006](levels-of-diagnostic-usage-data-collection-2006.md)
- [Diagnose- und Nutzungsdaten für Version 2002](levels-of-diagnostic-usage-data-collection-2002.md)
- [Diagnose- und Nutzungsdaten für Version 1910](levels-of-diagnostic-usage-data-collection-1910.md)
- [Diagnose- und Nutzungsdaten für Version 1906](levels-of-diagnostic-usage-data-collection-1906.md)
- [Diagnose- und Nutzungsdaten für Version 1902](levels-of-diagnostic-usage-data-collection-1902.md)

## <a name="next-steps"></a>Nächste Schritte

> [!div class="nextstepaction"]
> [Häufig gestellte Fragen](frequently-asked-questions.md)
