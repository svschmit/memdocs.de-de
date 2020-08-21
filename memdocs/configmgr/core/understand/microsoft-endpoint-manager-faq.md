---
title: Häufig gestellte Fragen zu Microsoft Endpoint Configuration Manager
titleSuffix: Configuration Manager
description: Häufig gestellte Fragen zu Microsoft Endpoint Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: be276b34-e283-4386-8b45-5629e431c50d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e0b59ffa73bb2c7524f2eed29326f238d856adef
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699312"
---
# <a name="microsoft-endpoint-configuration-manager-faq"></a>Häufig gestellte Fragen zu Microsoft Endpoint Configuration Manager

*Gilt für: Configuration Manager (Current Branch, Technical Preview-Branch)*

Ab Version 1910 ist Configuration Manager Bestandteil von Microsoft Endpoint Manager. Dieser Artikel beinhaltet Antworten auf häufig gestellte Fragen.

## <a name="summary"></a>Zusammenfassung

Schauen Sie zunächst das zweiminütige Video von Brad Anderson, Microsoft Corporate Vice President für Microsoft 365:

> [!VIDEO https://www.youtube.com/embed/GS7oNPInFuw]

## <a name="faqs"></a>Häufig gestellte Fragen

### <a name="what-is-microsoft-endpoint-manager"></a>Was ist Microsoft Endpoint Manager?

Microsoft Endpoint Manager ist eine integrierte Lösung für die Verwaltung all Ihrer Geräte. Microsoft vereint Configuration Manager und Intune mit vereinfachter Lizenzierung. Nutzen Sie weiterhin ihre bestehenden Investitionen in Configuration Manager, und profitieren Sie von der Leistungsfähigkeit der Microsoft-Cloud nach Ihren Vorgaben.

Die folgenden Microsoft-Verwaltungslösungen sind nun unter dem Namen **Microsoft Endpoint Manager** vereint:

- [Configuration Manager](/configmgr)
- [Intune](/intune)
- [Desktop Analytics](../../desktop-analytics/overview.md)
- [Autopilot](/intune/enrollment/enrollment-autopilot)
- Weitere Features in der [Verwaltungskonsole für die Geräteverwaltung](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/microsoft-intune-rolls-out-an-improved-streamlined-endpoint/ba-p/937760)

Weitere Informationen finden Sie in den folgenden Beiträgen von Brad Anderson, Microsoft Corporate Vice President für Microsoft 365:

- [Ankündigungs-Blogbeitrag](https://aka.ms/cmannounce)
- [Artikel zur Vision](https://aka.ms/MEMVisionPaper)

### <a name="what-things-change-in-configuration-manager-with-microsoft-endpoint-manager"></a>Welche Änderungen gibt es in Configuration Manager mit Microsoft Endpoint Manager?

Abgesehen von der Namensänderung funktioniert Configuration Manager in Version 1910 weiterhin gleich.

In den meisten Fällen wurden die Ordnernamen für allgemeine Komponenten im Startmenü geändert. Beispiele hierfür sind [Configuration Manager-Konsole](../servers/manage/admin-console.md#bkmk_open) und [Softwarecenter](software-center.md#bkmk_open).

### <a name="how-do-we-refer-to-the-product-now"></a>Wie soll jetzt auf das Produkt verwiesen werden?

- Beim Verweisen auf die gesamte Lösung, die alle Komponenten umfasst: **Microsoft Endpoint Manager**

- Beim Verweisen auf die lokale Komponente:
  - Verwenden Sie bei der ersten Erwähnung den vollständigen Markennamen: **Microsoft Endpoint Configuration Manager**
  - Zur allgemeinen Verwendung: **Configuration Manager**
  - Bei Verwendung mit eingeschränktem Platz: **ConfigMgr** (nur in Fällen, in denen der allgemeine Verwendungsname nicht passt)

### <a name="are-there-any-licensing-changes"></a>Gibt es Änderungen hinsichtlich der Lizenzierung?

Ja! Wie auf der Microsoft Ignite 2019 angekündigt verfügen Sie jetzt bei gültiger Lizenz für Configuration Manager auch über die Lizenz für Intune zur [gemeinsamen Verwaltung](../../comanage/overview.md) Ihrer Windows-PCs. Weitere Informationen finden Sie unter [Häufig gestellte Fragen zum Produkt und zur Lizenzierung](product-and-licensing-faq.md#bkmk_mem).

### <a name="why-do-i-still-see-system-center-configuration-manager-some-places"></a>Warum wird an manchen Stellen weiterhin „System Center Configuration Manager“ angezeigt?

Es dauert eine Weile, bis alle Produkte, Dienste und unterstützenden Materialien wie Dokumentationen geändert werden.

Es gibt auch einige grundlegende Komponenten, die sich möglicherweise nie ändern. **SMS_Executive** ist auf Standortservern weiterhin der wichtigste Windows-Dienst. **SCCMDocs** ist weiterhin das GitHub-Repository, das diese Dokumentation unterstützt.

## <a name="next-steps"></a>Nächste Schritte

[Neuigkeiten zu inkrementellen Versionen von Configuration Manager](../plan-design/changes/whats-new-incremental-versions.md)