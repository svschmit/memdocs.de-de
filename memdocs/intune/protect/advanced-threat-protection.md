---
title: Verwenden von Microsoft Defender ATP in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Verwenden Sie Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) mit Intune, einschließlich Einrichtung und Konfiguration, Onboarding Ihrer Intune-Geräte mit ATP, und verwenden Sie dann eine ATP-Geräterisikobewertung mit Ihren Richtlinien für Intune-Gerätecompliance und bedingten Zugriff zum Schutz von Netzwerkressourcen.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/23/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 9f54bf7f281fca65e01d839e926200bc68c49765
ms.sourcegitcommit: 46d4bc4fa73b22ae2a6a17a2d1cc6ec933a50e89
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88663446"
---
# <a name="enforce-compliance-for-microsoft-defender-atp-with-conditional-access-in-intune"></a>Erzwingen der Konformität für Microsoft Defender ATP mit bedingtem Zugriff in Intune

Sie können Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) als Mobile Threat Defense-Lösung mit Microsoft Intune integrieren. Mit der Integration tragen Sie dazu bei, Sicherheitsverletzungen zu verhindern und deren Auswirkungen innerhalb einer Organisation zu begrenzen.

Microsoft Defender ATP funktioniert mit Geräten, auf denen Windows 10 oder höher ausgeführt wird, sowie mit Android-Geräten.

Für eine erfolgreiche Einrichtung verwenden Sie die folgenden Konfigurationen gemeinsam:

- **Richten Sie eine Dienst-zu-Dienst-Verbindung zwischen Intune und Microsoft Defender ATP ein**. Diese Verbindung ermöglicht Microsoft Defender ATP das Sammeln von Daten zu Computerrisiken von unterstützten Geräten, die Sie mit Intune verwalten.
- **Verwenden Sie ein Gerätekonfigurationsprofil für das Onboarding von Geräten mit Microsoft Defender ATP**. Sie führen das Onboarding von Geräten durch, um sie für die Kommunikation mit Microsoft Defender ATP zu konfigurieren und Daten bereitzustellen, mit deren Hilfe Sie ihre Risikostufe bewerten können.
- **Verwenden Sie eine Gerätekonformitätsrichtlinie, um die Risikostufe festzulegen, die Sie zulassen möchten**. Risikostufen werden von Microsoft Defender ATP gemeldet. Geräte, die die zulässige Risikostufe überschreiten, werden als nicht konform eingestuft.
- **Verwenden Sie eine Richtlinie für bedingten Zugriff**, um den Zugriff von Benutzern auf Unternehmensressourcen mit nicht konformen Geräten zu blockieren.

Wenn Sie Intune mit Microsoft Defender ATP integrieren, können Sie die Bedrohungs- und Sicherheitsrisikenverwaltung von Microsoft Defender ATP (Thread & Vulnerability Management, TVM) nutzen und [Intune verwenden, um mittels TVM identifizierte Schwachstellen von Endpunkten zu beheben](atp-manage-vulnerabilities.md).

## <a name="example-of-using-microsoft-defender-atp-with-intune"></a>Beispiel für die Verwendung von Microsoft Defender ATP mit Intune

Im folgenden Beispiel wird erläutert, wie diese Lösungen zusammenarbeiten, um Ihre Organisation zu schützen. In diesem Beispiel sind Microsoft Defender ATP und Intune bereits integriert.

Stellen Sie sich vor, dass eine Person eine Word-Anlage mit eingebettetem bösartigem Code an einen Benutzer in Ihrer Organisation sendet.

- Der Benutzer öffnet die Anlage und aktiviert den Inhalt.
- Ein Angriff mit erhöhten Rechten beginnt, und ein Angreifer an einem Remotecomputer verfügt über Administratorrechte für das Gerät des Opfers.
- Der Angreifer greift dann remote auf die anderen Geräte des Benutzers zu. Diese Sicherheitsverletzung kann sich auf die gesamte Organisation auswirken.

Microsoft Defender ATP kann Sicherheitsereignisse wie dieses Szenario auflösen.

- In unserem Beispiel erkennt Microsoft Defender ATP, dass das Gerät nicht ordnungsgemäßen Code ausgeführt hat, seine Prozessrechte erhöht wurden, dass es bösartigen Code eingeschleust und eine verdächtige Remoteshell aufgerufen hat.
- Basierend auf diesen Aktionen des Geräts [klassifiziert Microsoft Defender ATP das Gerät als hochriskant](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/alerts-queue#severity) und legt einen detaillierten Bericht über verdächtige Aktivitäten im Microsoft Defender Security Center-Portal ab.

Sie können Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) als Mobile Threat Defense-Lösung mit Microsoft Intune integrieren. Mit der Integration tragen Sie dazu bei, Sicherheitsverletzungen zu verhindern und deren Auswirkungen innerhalb einer Organisation zu begrenzen.

Da Sie über eine Intune-Gerätekonformitätsrichtlinie verfügen, um Geräte mit der Risikostufe *Mittel* oder *Hoch* als nicht konform zu klassifizieren, wird das gefährdete Gerät als nicht konform klassifiziert. Diese Klassifizierung ermöglicht Ihrer Richtlinie für bedingten Zugriff, den Zugriff von diesem Gerät auf Ihre Unternehmensressourcen zu blockieren.

Bei Android-Geräten können Sie die Intune-Richtlinie verwenden, um die Konfiguration von Microsoft Defender ATP unter Android zu ändern. Weitere Informationen finden Sie unter [Webschutz in Microsoft Defender ATP](../protect/advanced-threat-protection-manage-android.md).

## <a name="prerequisites"></a>Voraussetzungen

Um Microsoft Defender ATP mit Intune zu verwenden, stellen Sie sicher, dass Sie Folgendes konfiguriert haben und verwenden können:

- Lizenzierter Mandant für Enterprise Mobility + Security E3 und Windows E5 (oder Microsoft 365 Enterprise E5)
- Microsoft Intune-Umgebung mit [Intune-verwalteten](../enrollment/windows-enroll.md) Windows 10- oder Android-Geräten, die auch mit Azure AD verknüpft sind
- [Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)-Umgebung für den Zugriff auf das Microsoft Defender Security Center (ATP-Portal)

> [!NOTE]
> Microsoft Defender ATP wird für Intune-App-Schutzrichtlinien für iOS/iPadOS und Android nicht unterstützt.

## <a name="next-steps"></a>Nächste Schritte

- Unter [Konfigurieren von Microsoft Defender ATP in Intune](../protect/advanced-threat-protection-configure.md) erfahren Sie, wie Sie Microsoft Defender ATP mit Intune verbinden, das Onboarding von Geräten durchführen und Richtlinien für den bedingten Zugriff konfigurieren.

In der Intune-Dokumentation erhalten Sie weitere Informationen:

- [Verwenden von Intune zum Korrigieren von mit Microsoft Defender ATP identifizierten Sicherheitsrisiken](atp-manage-vulnerabilities.md)
- [Erste Schritte mit den Gerätekonformitätsrichtlinien in Intune](device-compliance-get-started.md)

Weitere Informationen finden Sie in der Dokumentation zu Microsoft Defender ATP:

- [Microsoft Defender ATP – bedingter Zugriff](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Microsoft Defender ATP – Risikodashboard](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)
