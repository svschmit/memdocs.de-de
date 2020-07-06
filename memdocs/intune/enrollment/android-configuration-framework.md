---
title: Framework für die Android Enterprise-Sicherheitskonfiguration
titleSuffix: Microsoft Intune
description: Erfahren Sie, welche Einschränkungen und Einstellungen für die Sicherheitsstufen „Standard“ und „Hoch“ für Android Enterprise-Geräte vorgesehen sind.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: rosssmi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6f0e4452f5209d569e11a782528582f4d5a76045
ms.sourcegitcommit: b4b75876839e86357ef5804e5a0cf7a16c8a0414
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85502977"
---
# <a name="android-enterprise-security-configuration-framework"></a>Framework für die Android Enterprise-Sicherheitskonfiguration

Das Framework für die Android Enterprise-Sicherheitskonfiguration besteht aus einer Reihe von Empfehlungen zur Konformität von Geräten und Richtlinieneinstellungen für die Konfiguration. Diese Empfehlungen helfen Ihnen, den Sicherheitsschutz Ihrer Organisation für mobile Geräte auf Ihre speziellen Bedürfnisse zuzuschneiden.

Sicherheitsbewusste Organisationen suchen nach Möglichkeiten sicherzustellen, dass Unternehmensdaten auf mobilen Geräten geschützt sind. Eine Methode zum Schutz dieser Daten ist die Geräteregistrierung. Die Geräteregistrierung hilft Organisationen bei folgenden Aufgaben:
- Bereitstellen von Konformitätsrichtlinien (z. B. PIN-Sicherheit, Jailbreak-/Root-Validierung usw.)
- Bereitstellen von Konfigurationsrichtlinien (für WLAN, Zertifikate, VPN)
- Verwalten des App-Lebenszyklus

Um Ihnen zu helfen, ein vollständiges Sicherheitsszenario einzurichten, hat Microsoft eine neue Taxonomie für [Sicherheitskonfigurationen unter Windows 10](https://aka.ms/secconframework) eingeführt. Intune nutzt eine ähnliche Taxonomie für sein Framework für die Android Enterprise-Sicherheitskonfiguration. Sie enthalten für Standard-, erhöhte und hohe Sicherheit empfohlene Einstellungen für Gerätekonformität und -einschränkungen. Diese Taxonomie wird in den folgenden Artikeln erläutert:

1. [Methodik zur Android Enterprise-Frameworkbereitstellung](framework-deployment-methodology.md): Eine empfohlene Methode für die Bereitstellung des Frameworks für die Sicherheitskonfiguration.
2. [Einschränkungen bei der Registrierung von Android-Geräten](device-enrollment-restrictions.md): Einschränkungen für Geräte vor der Registrierung für Android Enterprise-Geräte.
3. [Festlegen von App-Konfigurationsrichtlinien für Android Enterprise-Geräte](android-app-configuration-policies.md): Konfigurieren Sie Apps auf den Geräten so, dass persönliche Konten nicht zugelassen werden.
4. [Sicherheitseinstellungen für Android Enterprise-Arbeitsprofile](android-work-profile-security-settings.md): Spezifische Konfigurationseinstellungen für Standard- und hohe Sicherheit auf Geräten mit Arbeitsprofil.
5. [Sicherheitseinstellungen für vollständig verwaltete Android Enterprise-Geräte](android-fully-managed-security-settings.md): Spezifische Konfigurationseinstellungen für Standard-, erhöhte und hohe Sicherheit auf vollständig verwalteten Geräten.

## <a name="android-enterprise-enrollment-modes"></a>Registrierungsmodi von Android Enterprise

In Android 5.0 wurde Android Enterprise von Google eingeführt, das zwei Registrierungsmodi bietet. Das Framework für die Android Enterprise-Sicherheitskonfiguration enthält Empfehlungen für beide Modi.
- [Vollständig verwaltet (Gerätebesitzer)](android-fully-managed-enroll.md): Für unternehmenseigene Geräte, die einem einzelnen Benutzer zugeordnet sind. Solche Geräte sind ausschließlich für die Arbeit und nicht für persönliche Zwecke gedacht.
- [Arbeitsprofil (Profilbesitzer)](android-work-profile-enroll.md): Typisch für benutzereigene Geräte, bei denen die IT-Abteilung eine klare Abgrenzung zwischen Arbeits- und persönlichen Daten wünscht. Von der IT-Abteilung gesteuerte Richtlinien stellen sicher, dass Arbeitsdaten nicht in das persönliche Profil übertragen werden können.


## <a name="next-steps"></a>Nächste Schritte

[Methodik zur Android Enterprise-Frameworkbereitstellung](framework-deployment-methodology.md)