---
title: Einschränkungen bei der Registrierung von Geräten für das Framework für die Android Enterprise-Sicherheitskonfiguration
titleSuffix: Microsoft Intune
description: Informationen zu Einschränkungen bei der Registrierung von Geräten für das Framework für die Android Enterprise-Sicherheitskonfiguration.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 07/02/2020
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
ms.openlocfilehash: 618be398d963e0a796ad9be7e8810201fc5e12f5
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88995091"
---
# <a name="android-enterprise-device-enrollment-restrictions"></a>Einschränkungen bei der Registrierung von Android Enterprise-Geräten

Bevor Geräte beim [Framework für die Android Enterprise-Sicherheitskonfiguration](android-configuration-framework.md) registriert werden, müssen Organisationen die entsprechenden Einschränkungen konfigurieren. Diese Einschränkungen stellen sicher, dass Benutzer Folgendes registrieren können:

- genehmigte Geräte
- eine angegebene Anzahl von Geräten
- Geräte mit angegebenen Plattformen
- Geräte mit angegebenen Betriebssystemen
- Geräte von angegebenen Herstellern

Weitere Informationen zu Einschränkungen bei der Registrierung finden Sie unter [Festlegen von Registrierungseinschränkungen](enrollment-restrictions-set.md).

## <a name="work-profile-basic-level-1-security-restrictions"></a>Sicherheitseinschränkungen für Arbeitsprofile des Typs „Standard“ (Stufe 1)

Für Android Enterprise-Arbeitsprofile mit Standardsicherheit (Stufe 1) müssen die folgenden Geräteeinschränkungen implementiert werden:

| Typ | Plattform | Version | Persönliche Geräte zulässig |
|--------|--------|--------|--------|
| Android Enterprise | Zulassen | Android 5.0 und höher.<p>Microsoft empfiehlt das Konfigurieren der Mindesthauptversion für das Android-Betriebssystem, um übereinstimmende unterstützte Android-Versionen für Microsoft-Apps verwenden zu können. OEMs und Geräte, für die von Android Enterprise empfohlene Anforderungen gelten, müssen die aktuelle Versandversion und ein Upgrade auf die nächste Version unterstützen.   Aktuell empfiehlt Android für Wissensarbeiter Android 8.0 und höher. Weitere Informationen finden Sie unter [Anforderungen für „Android Enterprise Recommended“](https://www.android.com/enterprise/recommended/requirements/). | Ja |
| Android-Geräteadministrator| Blockieren | Alle Versionen | Ja |

## <a name="work-profile-high-level-3-security-restrictions"></a>Sicherheitseinschränkungen für Arbeitsprofile des Typs „Hoch“ (Stufe 3)
Für Android Enterprise-Arbeitsprofile mit hoher Sicherheit (Stufe 3) müssen die folgenden Geräteeinschränkungen implementiert werden:

| Typ | Plattform | Version | Persönliche Geräte zulässig |
|--------|--------|--------|--------|
| Android Enterprise | Zulassen | Android 8.0 und höher | Ja |
| Android-Geräteadministrator| Blockieren | Alle Versionen | Ja |

## <a name="fully-managed-security-restrictions"></a>Vollständig verwaltete Sicherheitseinschränkungen
Stellen Sie sicher, dass die Organisation die vollständig verwaltete Android Enterprise-Geräteregistrierung unterstützt, indem Sie die Anweisungen zum [Registrieren vollständig verwalteter Geräte](android-fully-managed-enroll.md#enroll-the-fully-managed-devices) überprüfen. 

## <a name="conditional-access-policies"></a>Bedingte Zugriffsrichtlinien
Organisationen können Richtlinien für bedingten Zugriff von Azure AD verwenden, um sicherzustellen, dass Benutzer nur mit registrierten Android-Geräten auf Geschäfts-, Schul- oder Uni-Inhalte zugreifen können. Dazu benötigen Sie eine Richtlinie für bedingten Zugriff, die für alle potenziellen Benutzer gilt. Informationen zum Erstellen dieser Richtlinie finden Sie unter [Vorschreiben der Verwendung verwalteter Geräte für den Zugriff auf Cloud-Apps mithilfe des bedingten Zugriffs](/azure/active-directory/conditional-access/require-managed-devices). 

Führen Sie die unter [Szenario: Erfordern der Geräteregistrierung für iOS- und Android-Geräte](/azure/active-directory/conditional-access/require-managed-devices#scenario-require-device-enrollment-for-ios-and-android-devices) aufgeführten Schritte aus, um sicherzustellen, dass nur registrierte, konforme Mobilgeräte eine Verbindung mit Microsoft 365-Endpunkten herstellen können.

## <a name="next-steps"></a>Nächste Schritte

[Einrichten von App-Konfigurationsrichtlinien](android-app-configuration-policies.md)