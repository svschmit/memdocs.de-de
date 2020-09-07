---
title: Verwalten von Microsoft Teams für iOS und Android mit Intune
titleSuffix: ''
description: Nutzen Sie die Intune-App-Schutz- und Konfigurationsrichtlinien mit Microsoft Teams für iOS und Android, um sicherzustellen, dass der Zugriff auf Funktionen für die Zusammenarbeit im Team stets mit entsprechenden Sicherheitsvorkehrungen erfolgt.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/13/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: smithre4
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b1531de9ceab57b26bc9af5faac08673b8b758b0
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88993101"
---
# <a name="manage-team-collaboration-access-by-using-teams-for-ios-and-android-with-microsoft-intune"></a>Verwalten der Zusammenarbeit mithilfe von Microsoft Teams für iOS und Android mit Microsoft Intune

Microsoft Teams ist der Hub für die Zusammenarbeit von Teams in Microsoft 365, der die Personen, Inhalte und Tools verbindet, die Ihr Team für die effiziente Zusammenarbeit benötigt.

Die vielfältigsten und umfangreichsten Schutzfunktionen für Microsoft 365-Daten sind verfügbar, wenn Sie die Enterprise Mobility + Security-Suite abonnieren, die Microsoft Intune und Azure Active Directory Premium-Features wie bedingten Zugriff bietet. Sie sollten mindestens eine Richtlinie für bedingten Zugriff bereitstellen, die nur die Konnektivität mit Teams für iOS und Android auf mobilen Geräten zulässt, sowie eine Intune-App-Schutzrichtlinie, die gewährleistet, dass die Funktionen für die Zusammenarbeit geschützt sind.

## <a name="apply-conditional-access"></a>Aktivieren des bedingten Zugriff
Organisationen können Richtlinien für bedingten Zugriff von Azure AD nutzen, um sicherzustellen, dass Benutzer nur mit Teams für iOS und Android auf Geschäfts-, Schul- oder Uni-Inhalte zugreifen können. Dazu benötigen Sie eine Richtlinie für bedingten Zugriff, die für alle potenziellen Benutzer gilt. Einzelheiten zur Erstellung dieser Richtlinie finden Sie unter [Erzwingen einer App-Schutzrichtlinie für den Cloud-App-Zugriff mit bedingtem Zugriff](/azure/active-directory/conditional-access/app-protection-based-conditional-access).

1. Befolgen Sie „Schritt 1: Konfigurieren einer Azure AD-Richtlinie für bedingten Zugriff für Office 365“ unter [Szenario 1: Office 365-Apps erfordern genehmigte Apps mit App-Schutzrichtlinien.](/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies) So wird Teams für iOS und Android zugelassen, OAuth-fähige Clients von Drittanbietern für mobile Geräte werden jedoch daran gehindert, eine Verbindung zu Office 365-Endpunkten herzustellen.

   >[!NOTE]
   > Diese Richtlinie sorgt dafür, dass Benutzer mobiler Geräte über die entsprechenden Apps auf alle Office-Endpunkte zugreifen können.

## <a name="create-intune-app-protection-policies"></a>Erstellen von Intune-App-Schutzrichtlinien

App-Schutzrichtlinien legen fest, welche Apps zulässig sind und welche Aktionen sie auf die Daten Ihres Unternehmens anwenden dürfen. Die in den App-Schutzrichtlinien verfügbaren Optionen ermöglichen Organisationen, den Schutz an ihre speziellen Anforderungen anzupassen. In einigen Situationen ist es jedoch möglicherweise nicht offensichtlich, welche Richtlinieneinstellungen genau erforderlich sind, um ein vollständiges Szenario zu implementieren. Um Unternehmen bei der Priorisierung der Absicherung mobiler Clientendpunkte zu unterstützen, hat Microsoft für die Verwaltung mobiler iOS- und Android-Apps eine Taxonomie für sein Datenschutzframework für App-Schutzrichtlinien eingeführt.

Dieses Datenschutzframework ist in drei Konfigurationsebenen unterteilt, wobei jede Ebene auf der vorherigen Ebene aufbaut:

- **Einfacher Datenschutz für Unternehmen** (Ebene 1): Diese Ebene stellt sicher, dass Apps mit einer PIN geschützt und verschlüsselt sind, und dient zum Durchführen selektiver Löschvorgänge. Bei Android-Geräten überprüft diese Ebene den Android-Gerätenachweis. Dabei handelt es sich um eine Konfiguration auf Einstiegsebene, die ähnliche Datenschutzkontrolle in Exchange Online-Postfachrichtlinien bereitstellt und der IT sowie dem Benutzerstamm eine Einführung in App-Schutzrichtlinien bietet.
- **Erweiterter Datenschutz für Unternehmen** (Ebene 2): Diese Ebene führt Mechanismen für App-Schutzrichtlinien zur Verhinderung von Datenlecks sowie die mindestens zu erfüllenden Betriebssystemanforderungen ein. Dies ist die Konfiguration, die für die meisten mobilen Benutzer gilt, die auf Geschäfts-, Schul- oder Unidaten zugreifen.
- **Hoher Datenschutz für Unternehmen** (Ebene 3): Auf dieser Ebene werden Mechanismen zum erweiterten Datenschutz, eine verbesserte PIN-Konfiguration sowie Mobile Threat Defense für App-Schutzrichtlinien eingeführt. Diese Konfiguration ist für Benutzer vorgesehen, die auf Hochrisikodaten zugreifen.

Die spezifischen Empfehlungen für jede Konfigurationsebene sowie die zumindest zu schützenden Apps finden Sie unter [Datenschutzframework mithilfe von App-Schutzrichtlinien](app-protection-framework.md).

Unabhängig davon, ob das Gerät in einer UEM-Lösung (Unified Endpoint Management) registriert ist, muss eine Intune-App-Schutzrichtlinie sowohl für iOS- als auch für Android-Apps erstellt werden, indem die Schritte unter [Erstellen und Zuweisen von App-Schutzrichtlinien](app-protection-policies.md) ausgeführt werden. Diese Richtlinien müssen mindestens die folgenden Bedingungen erfüllen:

1. Sie umfassen alle mobilen Microsoft 365-Anwendungen wie Microsoft Edge, Outlook, OneDrive, Office oder Teams. Damit wird sichergestellt, dass Benutzer in jeder Microsoft-App sicher auf Geschäfts-, Schul- oder Unidaten zugreifen und diese bearbeiten können.

2. Sie werden allen Benutzern zugewiesen. Dadurch wird sichergestellt, dass alle Benutzer unabhängig davon, ob sie Teams für iOS oder Android nutzen, geschützt sind.

3. Bestimmen Sie, welche Frameworkebene Ihre Anforderungen erfüllt. Die meisten Organisationen sollten die Einstellungen, die unter **Erweiterter Datenschutz für Unternehmen** (Ebene 2) festgelegt wurden, implementieren, da dadurch Datenschutz und Zugriffsanforderungskontrollen ermöglicht werden.

Weitere Informationen zu den verfügbaren Einstellungen finden Sie unter [Einstellungen für App-Schutzrichtlinien für Android](app-protection-policy-settings-android.md) und [Einstellungen für App-Schutzrichtlinien für iOS](app-protection-policy-settings-ios.md).

> [!IMPORTANT]
> Um Intune-App-Schutzrichtlinien auf Apps auf Android-Geräten anzuwenden, die nicht bei Intune registriert sind, muss der Benutzer auch das Intune-Unternehmensportal installieren. Weitere Informationen finden Sie unter [Was Sie erwartet, wenn Ihre Android-App von App-Schutzrichtlinien verwaltet wird](../fundamentals/end-user-mam-apps-android.md).

## <a name="utilize-app-configuration"></a>Verwenden der App-Konfiguration

Teams für iOS und Android unterstützt App-Einstellungen, die eine einheitliche Endpunktverwaltung ermöglichen, wie z. B. Microsoft Endpoint Manager. Administratoren können das Verhalten der App anpassen.

Die App-Konfiguration kann entweder über den Kanal „MDM (Mobile Device Management, Verwaltung mobiler Geräte)“ des Betriebssystems auf registrierten Geräten (Kanal [Managed App Configuration](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) für iOS oder [Android in the Enterprise ](https://developer.android.com/work/managed-configurations) für Android) oder über den Kanal „Intune-App-Schutzrichtlinie“ bereitgestellt werden. Teams für iOS und Android unterstützt die folgenden Konfigurationsszenarios:

- Nur Geschäfts-, Schul- oder Unikonten zulassen

> [!IMPORTANT]
> Für Konfigurationsszenarios, die eine Geräteregistrierung unter Android erfordern, müssen die Geräte in Android Enterprise registriert werden, und Teams für Android muss über den Managed Google Play Store bereitgestellt werden. Weitere Informationen finden Sie unter [Einrichten der Registrierung von Android Enterprise-Arbeitsprofilgeräten](../enrollment/android-work-profile-enroll.md) und [Hinzufügen von App-Konfigurationsrichtlinien für verwaltete Android Enterprise-Geräte](app-configuration-policies-use-android.md).

Für jedes Konfigurationsszenario werden die spezifischen Anforderungen hervorgehoben. Zum Beispiel, ob das Konfigurationsszenario die Registrierung von Geräten verlangt und somit mit jedem UEM-Anbieter funktioniert oder ob Intune-App-Schutzrichtlinien erforderlich sind.

> [!NOTE]
> Bei Microsoft Endpoint Manager wird die App-Konfiguration, die über den MDM-OS-Kanal bereitgestellt wird, als App-Konfigurationsrichtlinie für **verwaltete Geräte** bezeichnet. Eine App-Konfiguration, die über den Kanal „App-Schutzrichtlinie“ bereitgestellt wird, wird als App-Konfigurationsrichtlinie für **verwaltete Apps** bezeichnet.

## <a name="only-allow-work-or-school-accounts"></a>Nur Geschäfts-, Schul- oder Unikonten zulassen

Die Einhaltung der Datensicherheits- und Compliancerichtlinien unserer größten und hoch regulierten Kunden ist eine tragende Säule des Werts von Microsoft 365. In einigen Unternehmen müssen alle Kommunikationsinformationen in der Unternehmensumgebung aufgezeichnet werden, und ebenso muss sichergestellt werden, dass die Geräte nur für die Unternehmenskommunikation verwendet werden. Teams für iOS und Android kann auf registrierten Geräten so konfiguriert werden, dass nur ein einziges Firmenkonto innerhalb der App bereitgestellt werden darf, um diese Anforderungen zu unterstützen.

Hier erfahren Sie mehr über das Konfigurieren der Einstellung des Modus für zulässige Organisationskonten:

- [Einstellungen für Android](app-configuration-policies-use-android.md#allow-only-configured-organization-accounts-in-multi-identity-apps)
- [Einstellungen für iOS](app-configuration-policies-use-ios.md#allow-only-configured-organization-accounts-in-multi-identity-apps)

Dieses Konfigurationsszenario funktioniert nur mit registrierten Geräten. Allerdings werden beliebige UEM-Anbieter unterstützt. Wenn Sie Microsoft Endpoint Manager nicht nutzen, müssen Sie in Ihrer UEM-Dokumentation nachschlagen, wie Sie diese Konfigurationsschlüssel bereitstellen können.

## <a name="next-steps"></a>Nächste Schritte

- [Was sind App-Schutzrichtlinien?](app-protection-policy.md) 
- [App-Konfigurationsrichtlinien für Microsoft Intune](app-configuration-policies-overview.md)