---
title: Intune-Onboardingprozess
titleSuffix: Microsoft Intune
description: Dieser Artikel hilft Ihnen bei allem, was beim Onboarding einer reinen Microsoft Intune-Cloudlösung in Ihrer Umgebung berücksichtigt werden muss.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ac7bd764-5365-4920-8fd0-ea57d5ebe039
ms.reviewer: jeffbu, cgerth
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0b479f770053051e580a68aa810a60c35d745ac5
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996349"
---
# <a name="implement-your-microsoft-intune-plan"></a>Implementieren Ihres Microsoft Intune-Plans

Während der Onboarding-Phase stellen Sie Intune in Ihrer Produktionsumgebung bereit. Der Implementierungsprozess besteht aus dem Einrichten und Konfigurieren von Intune und externen Abhängigkeiten (falls erforderlich), basierend auf den [Anforderungen Ihres Anwendungsfalls](planning-guide-requirements.md).

Der folgende Abschnitt enthält eine Übersicht über den Intune-Implementierungsprozess, der Anforderungen und allgemeine Aufgaben umfasst.

## <a name="intune-requirements"></a>Intune-Anforderungen

Die wichtigsten Anforderungen der eigenständigen Intune-Version lauten wie folgt:

- Enterprise Mobility + Security (EMS)/Intune-Abonnement

- Microsoft 365-Abonnement (für Office-Apps und über die durch die App-Schutzrichtlinie verwalteten Apps)

- APNs-Zertifikat (zum Aktivieren der Verwaltung der iOS-/iPadOS-Geräteplattform)

- Azure AD Connect (zur Verzeichnissynchronisierung)

- Intune-Connector für lokale Exchange-Umgebungen (für den bedingten Zugriff für Exchange lokal, falls erforderlich)

- Intune Certificate Connector (für die SCEP-Zertifikatbereitstellung, falls erforderlich)

>[!TIP]
> Die Liste [Unterstützte Geräte](supported-devices-browsers.md) umfasst eine vollständige Auflistung der Geräte, die mit Intune verwaltet werden können.

## <a name="intune-implementation-process"></a>Intune-Implementierungsprozess

Es wurden 13 diskrete Aufgaben für die Implementierung einer Intune-Bereitstellung identifiziert. Abhängig von Ihren Geschäftsanforderungen, der vorhandenen Infrastruktur und der Verwaltungsstrategie für Geräte sind einige dieser Aufgaben möglicherweise bereits abgeschlossen worden. Andere finden möglicherweise keine Anwendung auf Ihren Plan.

### <a name="task-1-get-an-intune-subscription"></a>Aufgabe 1: Abschließen eines Intune-Abonnements

Wie oben im Abschnitt „Intune-Anforderungen“ angegeben, benötigen Sie ein EMS- oder Intune-Abonnement. Wenn Ihre Organisation nicht über ein solches Abonnement verfügt, wenden Sie sich an Microsoft oder das Microsoft-Konto-Team, und teilen Sie Ihr Interesse am Kauf von Enterprise Mobility + Security (EMS) oder Intune mit.

- Informationen zum [Kauf von Microsoft Intune](https://www.microsoft.com/cloud-platform/microsoft-intune-pricing).

### <a name="task-2-add-microsoft-365-subscription"></a>Aufgabe 2: Hinzufügen eines Microsoft 365-Abonnements

Dieser Schritt ist optional. Sie benötigen ein Microsoft 365-Abonnement, wenn Sie planen, Exchange Online zu verwenden und mobile Office-Apps mit App-Schutzrichtlinien zu verwalten. Wenn Ihre Organisation nicht über ein Microsoft 365-Abonnement verfügt, wenden Sie sich an Microsoft oder das Microsoft-Konto-Team, und teilen Sie Ihr Interesse am Kauf von Microsoft 365 mit.

- Informationen zum [Kauf von Microsoft 365](https://products.office.com/business/compare-office-365-for-business-plans).

### <a name="task-3-add-users-groups-in-azure-ad"></a>Aufgabe 3: Hinzufügen von Benutzergruppen in Azure AD

Möglicherweise müssen Sie je nach den Anwendungsszenarios und Anforderungen Ihrer Intune-Bereitstellung Benutzer oder Sicherheitsgruppen in Active Directory oder Azure Active Directory hinzufügen. Überprüfen Sie Ihre aktuellen Benutzer und Sicherheitsgruppen in Active Directory oder Azure Active Directory, und ermitteln Sie, ob diese vollständig Ihren Anforderungen entsprechen. Wenn Sie neue Benutzer und Sicherheitsgruppen hinzufügen, wird empfohlen, diese in Active Directory hinzuzufügen und sie über Azure AD Connect mit Azure Active Directory zu synchronisieren.

- Weitere Informationen zum [Hinzufügen von Benutzern/Gruppen in Intune](users-add.md).
<!---why not send them to the AAD connect topic? Question out to Andre: https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect--->


### <a name="task-4-assign-intune-and-microsoft-365-user-licenses"></a>Aufgabe 4: Zuweisen von Benutzerlizenzen für Intune und Microsoft 365

Allen Zielbenutzern für das EMS/Intune- und Microsoft 365-Rollout muss eine Lizenz zugewiesen sein. Sie können im Microsoft 365 Admin Center EMS-/Intune- und Microsoft 365-Lizenzen zuweisen.

- Weitere Informationen zum [Zuweisen von Intune-Lizenzen](licenses-assign.md).

### <a name="task-5-set-mobile-device-management-authority-to-intune"></a>Aufgabe 5: Festlegen der Autorität für die Verwaltung mobiler Geräte auf Intune

Bevor Sie mit dem Einrichten, Konfigurieren, Verwalten und Registrieren von Geräten mit Intune beginnen können, müssen Sie die Autorität für die Geräteverwaltung in Intune festlegen.

- Weitere Informationen zum [Festlegen der Autorität für die Geräteverwaltung](mdm-authority-set.md).

### <a name="task-6-enable-device-platforms"></a>Aufgabe 6: Aktivieren von Geräteplattformen

Die meisten Geräteplattformen sind standardmäßig aktiviert, mit Ausnahme von Apple-Geräten (iOS/iPadOS und Mac). Damit iOS-/iPadOS-Geräte registriert und in Intune verwaltet werden können, muss die Geräteplattform aktiviert sein. Zu diesem Zweck müssen Sie ein MDM-Push-Zertifikat erstellen und zu Intune hinzufügen.

- Weitere Informationen zum [Aktivieren von Apple-Geräten für die Registrierung](../enrollment/apple-mdm-push-certificate-get.md).

### <a name="task-7-add-and-deploy-terms-and-conditions-policies"></a>Aufgabe 7: Hinzufügen und Bereitstellen von Richtlinien für Geschäftsbedingungen

Intune unterstützt Richtlinien für Geschäftsbedingungen. Fügen Sie Richtlinien für Geschäftsbedingungen nach Bedarf hinzu, und stellen Sie sie basierend auf den Anwendungsfällen und Anforderungen Ihrer Intune-Bereitstellung für Zielgruppen bereit.

- Weitere Informationen zum [Hinzufügen und Bereitstellen von Richtlinien für Geschäftsbedingungen](../enrollment/terms-and-conditions-create.md).

### <a name="task-8-add-and-deploy-configuration-policies"></a>Aufgabe 8: Hinzufügen und Bereitstellen von Konfigurationsrichtlinien

Intune unterstützt zwei Arten von Konfigurationsrichtlinien: allgemeine und benutzerdefinierte. Fügen Sie Konfigurationsrichtlinien nach Bedarf hinzu, und stellen Sie sie basierend auf den Anwendungsfällen und Anforderungen Ihrer Intune-Bereitstellung für Zielgruppen bereit.

- Weitere Informationen zum [Hinzufügen und Bereitstellen von Konfigurationsrichtlinien](../configuration/device-profiles.md).

### <a name="task-9-add-and-deploy-resource-profiles"></a>Aufgabe 9: Hinzufügen und Bereitstellen von Ressourcenprofilen

Intune unterstützt E-Mail-, WLAN- und VPN-Profile. Fügen Sie diese Profile nach Bedarf hinzu, und stellen Sie sie basierend auf den Anwendungsfällen und Anforderungen Ihrer Intune-Bereitstellung für Zielgruppen bereit.

- Weitere Informationen zum [Aktivieren des Zugriffs auf Unternehmensressourcen mit Intune](../configuration/device-profiles.md).

### <a name="task-10-add-and-deploy-apps"></a>Aufgabe 10: Hinzufügen und Bereitstellen von Apps

Intune unterstützt die Bereitstellung von Web-Apps, branchenspezifischen Apps und Apps aus öffentlichen Stores. Sie können auch Apps mit integriertem Intune SDK verwalten, indem Sie ihnen App-Schutzrichtlinien zuordnen. Fügen Sie Apps nach Bedarf hinzu, und stellen Sie sie basierend auf den Anwendungsfällen und Anforderungen Ihrer Intune-Bereitstellung für Zielgruppen bereit.

- Weitere Informationen zum [Hinzufügen und Bereitstellen von Apps](../apps/app-management.md).

### <a name="task-11-add-and-deploy-compliance-policies"></a>Aufgabe 11: Hinzufügen und Bereitstellen von Konformitätsrichtlinien

Intune unterstützt Kompatibilitätsrichtlinien. Fügen Sie Kompatibilitätsrichtlinien nach Bedarf hinzu, und stellen Sie sie basierend auf den Anwendungsfällen und Anforderungen Ihrer Intune-Bereitstellung für Zielgruppen bereit.

- Weitere Informationen zu [Konformitätsrichtlinien](../protect/device-compliance-get-started.md).

### <a name="task-12-enable-conditional-access-policies"></a>Aufgabe 12: Aktivieren von Richtlinien für bedingten Zugriff

Intune unterstützt den bedingten Zugriff für Exchange Online und lokal, SharePoint Online, Skype for Business Online und Dynamics CRM Online. Aktivieren und konfigurieren Sie den bedingten Zugriff nach Bedarf basierend auf den Anwendungsfällen und Anforderungen Ihrer Intune-Bereitstellung.

- Weitere Informationen zum [bedingten Zugriff](../protect/conditional-access.md).

### <a name="task-13-enroll-devices"></a>Aufgabe 13: Registrieren von Geräten

Intune unterstützt die Geräteplattformen iOS/iPadOS, macOS, Android und Windows Desktop. Registrieren Sie Mobilgeräteplattformen nach Bedarf basierend auf den Anwendungsfällen und Anforderungen Ihrer Intune-Bereitstellung.

- Weitere Informationen zum [Registrieren von Geräten](../enrollment/device-enrollment.md).


## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen finden Sie im Leitfaden zum [Testen und Überprüfen Ihrer Intune-Bereitstellung](planning-guide-test-validation.md).
