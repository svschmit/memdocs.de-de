---
title: Richtlinien für die Android Enterprise-Sicherheitskonfiguration
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
ms.openlocfilehash: 3735a37d4572454968638d29ab2646d6fda943ad
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546585"
---
# <a name="android-enterprise-security-configuration-framework-app-configuration-policies"></a>App-Konfigurationsrichtlinien im Framework für die Android Enterprise-Sicherheitskonfiguration

Im Rahmen des [Frameworks für die Android Enterprise-Sicherheitskonfiguration](android-configuration-framework.md) müssen Sie App-Konfigurationsrichtlinien für Android Enterprise-Geräte ordnungsgemäß festlegen.

Geräte mit Android Enterprise-Arbeitsprofil sind so konzipiert, dass geschäftliche und private Daten voneinander isoliert werden können. Vollständig verwaltete Android Enterprise-Geräte sind nur auf Geschäfts-, Schul- und Unidaten ausgelegt. Daher müssen Microsoft-Apps, die auf diesen Geräten bereitgestellt werden, so konfiguriert werden, dass sie keine persönlichen Konten zulassen.

## <a name="disallow-personal-accounts-for-microsoft-apps-on-android-enterprise-devices"></a>Verhindern persönlicher Konten für Microsoft-Apps auf Android Enterprise-Geräten

1. Fügen Sie die Apps zu Managed Google Play hinzu. Weitere Informationen finden Sie unter [Hinzufügen von verwalteten Google Play-Apps für Android Enterprise-Geräte mit Intune](../apps/apps-add-android-for-work.md).
2. Erstellen Sie gemäß den Anweisungen unter [Hinzufügen von App-Konfigurationsrichtlinien für verwaltete Android Enterprise-Geräte]() eine Richtlinie für jede Managed Google Play-App.
3. Erstellen Sie in jeder Richtlinie den folgenden Einzelschlüssel:

    | Schlüssel | Werte |
    | --- | --- |
    | com.microsoft.intune.mam.AllowedAccountUPNs | Ein oder mehrere durch ; getrennte UPNs.<br>Die einzigen zulässigen Konten sind die von diesem Schlüssel definierten, verwalteten Benutzerkonten.<br>Für bei Intune registrierte Geräte kann das Token {{userprincipalname}} verwendet werden, um das registrierte Benutzerkonto darzustellen. |


## <a name="next-steps"></a>Nächste Schritte
Wenden Sie [Android Enterprise-Sicherheitseinstellungen für das Arbeitsprofil](android-work-profile-security-settings.md) oder [vollständig verwaltete Android Enterprise-Sicherheitseinstellungen](android-fully-managed-security-settings.md) an.