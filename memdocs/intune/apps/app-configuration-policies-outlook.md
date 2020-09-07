---
title: Verwalten von Outlook für iOS und Android mit Intune
description: Nutzen Sie die Intune-App-Schutz- und Konfigurationsrichtlinien mit Outlook für iOS und Android, um sicherzustellen, dass der Zugriff auf Funktionen für die Zusammenarbeit im Team stets mit entsprechenden Sicherheitsvorkehrungen erfolgt.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/11/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: smithre4
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ac2133455d4440e8048e7b9aba8f9f9b13d98a53
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996536"
---
# <a name="manage-messaging-collaboration-access-by-using-outlook-for-ios-and-android-with-microsoft-intune"></a>Verwalten des Zugriffs für Nachrichten und Zusammenarbeit mithilfe von Outlook für iOS und Android mit Microsoft Intune

Die App „Outlook für iOS und Android“ ist so entworfen, dass Benutzer Ihrer Organisation mehr Möglichkeiten auf ihrem mobilen Geräten haben, indem E-Mails, Kalender, Kontakte und andere Dateien zusammengeführt werden.

Die vielfältigsten und umfangreichsten Schutzfunktionen für Microsoft 365-Daten sind verfügbar, wenn Sie die Enterprise Mobility + Security-Suite abonnieren, die Microsoft Intune und Azure Active Directory Premium-Features wie bedingten Zugriff bietet. Sie sollten mindestens eine Richtlinie für bedingten Zugriff bereitstellen, die nur die Konnektivität mit Outlook für iOS und Android auf mobilen Geräten zulässt, sowie eine Intune-App-Schutzrichtlinie, die gewährleistet, dass die Funktionen für die Zusammenarbeit geschützt sind.

## <a name="apply-conditional-access"></a>Aktivieren des bedingten Zugriff
Organisationen können Richtlinien für bedingten Zugriff von Azure AD nutzen, um sicherzustellen, dass Benutzer nur mit Outlook für iOS und Android auf Geschäfts-, Schul- oder Uni-Inhalte zugreifen können. Dazu benötigen Sie eine Richtlinie für bedingten Zugriff, die für alle potenziellen Benutzer gilt. Einzelheiten zur Erstellung dieser Richtlinie finden Sie unter [Erzwingen einer App-Schutzrichtlinie für den Cloud-App-Zugriff mit bedingtem Zugriff](/azure/active-directory/conditional-access/app-protection-based-conditional-access).

1. Befolgen Sie „Schritt 1: Konfigurieren einer Azure AD-Richtlinie für bedingten Zugriff für Office 365“ unter [Szenario 1: Office 365-Apps erfordern genehmigte Apps mit App-Schutzrichtlinien](/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies). Dadurch wird Outlook für iOS und Android zugelassen, die OAuth-fähigen Exchange ActiveSync-Clients werden jedoch daran gehindert, eine Verbindung zu Exchange Online herzustellen.

   > [!NOTE]
   > Diese Richtlinie sorgt dafür, dass Benutzer mobiler Geräte über die entsprechenden Apps auf alle Office-Endpunkte zugreifen können.

2. Befolgen Sie „Schritt 2: Konfigurieren einer Azure AD-Richtlinie für bedingten Zugriff für Exchange Online mit ActiveSync (EAS)“ unter [Szenario 1: Office 365-Apps erfordern genehmigte Apps mit App-Schutzrichtlinien](/azure/active-directory/conditional-access/app-protection-based-conditional-access#scenario-1-office-365-apps-require-approved-apps-with-app-protection-policies). Dadurch werden Exchange ActiveSync-Clients, die eine einfache Authentifizierung nutzen, daran gehindert, eine Verbindung zu Exchange Online herzustellen.

   Die oben genannten Richtlinien nutzen die Zuweisungssteuerung [App-Schutzrichtlinie erforderlich](/azure/active-directory/active-directory-conditional-access-technical-reference). So kann dafür gesorgt werden, dass eine Intune-App-Schutz-Richtlinie auf das zugehörige Konto in Outlook für iOS und Android angewendet wird, bevor der Zugriff gewährt wird. Wenn der Benutzer keiner Intune-App-Schutz-Richtlinie zugewiesen ist, keine Lizenz für Intune hat oder die App nicht in der Intune-App-Schutz-Richtlinie eingeschlossen ist, hindert die Richtlinie den Benutzer daran, ein Zugriffstoken abzurufen und Zugriff auf die Nachrichtendaten zu erhalten.

3. Befolgen Sie schließlich noch die Anweisungen unter [Vorgehensweise: Blockieren der Legacyauthentifizierung bei Azure AD mit bedingtem Zugriff](/azure/active-directory/conditional-access/block-legacy-authentication), um Legacyauthentifizierung für andere Exchange-Protokolle auf iOS- und Android-Geräten zu verhindern. Diese Richtlinie sollte nur auf die Microsoft Exchange Online-Cloud-App und auf iOS- und Android-Geräteplattformen angewendet werden. Dies sorgt dafür dass, das mobile Apps, für die Exchange Web Services oder IMAP4- oder POP3-Protokolle mit einer einfachen Authentifizierung verwendet werden, keine Verbindung zu Exchange Online herstellen können.

## <a name="create-intune-app-protection-policies"></a>Erstellen von Intune-App-Schutzrichtlinien

App-Schutzrichtlinien legen fest, welche Apps zulässig sind und welche Aktionen sie auf die Daten Ihres Unternehmens anwenden dürfen. Die in den App-Schutzrichtlinien verfügbaren Optionen ermöglichen Organisationen, den Schutz an ihre speziellen Anforderungen anzupassen. In einigen Situationen ist es jedoch möglicherweise nicht offensichtlich, welche Richtlinieneinstellungen genau erforderlich sind, um ein vollständiges Szenario zu implementieren. Um Unternehmen bei der Priorisierung der Absicherung mobiler Clientendpunkte zu unterstützen, hat Microsoft für die Verwaltung mobiler iOS- und Android-Apps eine Taxonomie für sein Datenschutzframework für App-Schutzrichtlinien eingeführt.

Dieses Datenschutzframework ist in drei Konfigurationsebenen unterteilt, wobei jede Ebene auf der vorherigen Ebene aufbaut:

- **Einfacher Datenschutz für Unternehmen** (Ebene 1): Diese Ebene stellt sicher, dass Apps mit einer PIN geschützt und verschlüsselt sind, und dient zum Durchführen selektiver Löschvorgänge. Bei Android-Geräten überprüft diese Ebene den Android-Gerätenachweis. Dabei handelt es sich um eine Konfiguration auf Einstiegsebene, die ähnliche Datenschutzkontrolle in Exchange Online-Postfachrichtlinien bereitstellt und der IT sowie dem Benutzerstamm eine Einführung in App-Schutzrichtlinien bietet.
- **Erweiterter Datenschutz für Unternehmen** (Ebene 2): Diese Ebene führt Mechanismen für App-Schutzrichtlinien zur Verhinderung von Datenlecks sowie die mindestens zu erfüllenden Betriebssystemanforderungen ein. Dies ist die Konfiguration, die für die meisten mobilen Benutzer gilt, die auf Geschäfts-, Schul- oder Unidaten zugreifen.
- **Hoher Datenschutz für Unternehmen** (Ebene 3): Auf dieser Ebene werden Mechanismen zum erweiterten Datenschutz, eine verbesserte PIN-Konfiguration sowie Mobile Threat Defense für App-Schutzrichtlinien eingeführt. Diese Konfiguration ist für Benutzer vorgesehen, die auf Hochrisikodaten zugreifen.

Die spezifischen Empfehlungen für jede Konfigurationsebene sowie die zumindest zu schützenden Apps finden Sie unter [Datenschutzframework mithilfe von App-Schutzrichtlinien](app-protection-framework.md).

Unabhängig davon, ob das Gerät in einer UEM-Lösung (Unified Endpoint Management) registriert ist, muss eine Intune-App-Schutzrichtlinie sowohl für iOS- als auch für Android-Apps erstellt werden, indem die Schritte unter [Erstellen und Zuweisen von App-Schutzrichtlinien](app-protection-policies.md) ausgeführt werden. Diese Richtlinien müssen mindestens die folgenden Bedingungen erfüllen:

1. Sie umfassen alle mobilen Microsoft 365-Anwendungen wie Microsoft Edge, Outlook, OneDrive, Office oder Teams. Damit wird sichergestellt, dass Benutzer in jeder Microsoft-App sicher auf Geschäfts-, Schul- oder Unidaten zugreifen und diese bearbeiten können.

2. Sie werden allen Benutzern zugewiesen. Dadurch wird sichergestellt, dass alle Benutzer unabhängig davon, ob sie Outlook für iOS oder Android nutzen, geschützt sind.

3. Bestimmen Sie, welche Frameworkebene Ihre Anforderungen erfüllt. Die meisten Organisationen sollten die Einstellungen, die unter **Erweiterter Datenschutz für Unternehmen** (Ebene 2) festgelegt wurden, implementieren, da dadurch Datenschutz und Zugriffsanforderungskontrollen ermöglicht werden.

Weitere Informationen zu den verfügbaren Einstellungen finden Sie unter [Einstellungen für App-Schutzrichtlinien für Android](app-protection-policy-settings-android.md) und [Einstellungen für App-Schutzrichtlinien für iOS](app-protection-policy-settings-ios.md).

> [!IMPORTANT]
> Um Intune-App-Schutzrichtlinien auf Apps auf Android-Geräten anzuwenden, die nicht bei Intune registriert sind, muss der Benutzer auch das Intune-Unternehmensportal installieren. Weitere Informationen finden Sie unter [Was Sie erwartet, wenn Ihre Android-App von App-Schutzrichtlinien verwaltet wird](../fundamentals/end-user-mam-apps-android.md).

## <a name="utilize-app-configuration"></a>Verwenden der App-Konfiguration

Outlook für iOS und Android unterstützt App-Einstellungen, die eine einheitliche Endpunktverwaltung ermöglichen, z. B. Microsoft Endpoint Manager. Administratoren können das Verhalten der App anpassen.

Die App-Konfiguration kann entweder über den Kanal „MDM (Mobile Device Management, Verwaltung mobiler Geräte)“ des Betriebssystems auf registrierten Geräten (Kanal [Managed App Configuration](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) für iOS oder [Android in the Enterprise ](https://developer.android.com/work/managed-configurations) für Android) oder über den Kanal „Intune-App-Schutzrichtlinie“ bereitgestellt werden. Outlook für iOS und Android unterstützt die folgenden Konfigurationsszenarios:

- Nur Geschäfts-, Schul- oder Unikonten zulassen
- Allgemeine App-Konfigurationseinstellungen
- S/MIME-Einstellungen
- Datenschutzeinstellungen

Spezifische Verfahrensschritte und eine ausführliche Dokumentation zu den App-Konfigurationseinstellungen von Outlook für iOS und Android finden Sie unter [Bereitstellen von Outlook für IOS-und Android-App-Konfigurationseinstellungen](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune).

## <a name="next-steps"></a>Nächste Schritte

- [Was sind App-Schutzrichtlinien?](app-protection-policy.md) 
- [App-Konfigurationsrichtlinien für Microsoft Intune](app-configuration-policies-overview.md)