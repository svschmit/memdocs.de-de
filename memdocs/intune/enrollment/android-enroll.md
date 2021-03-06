---
title: Registrieren von Android-Geräten in Intune
titleSuffix: Microsoft Intune
description: Erfahren Sie, wie Sie Android-Geräte in Intune registrieren.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 7/23/2019
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: f276d98c-b077-452a-8835-41919d674db5
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: d8506661c49fa4f9c8481a3caa96883c91e6d8bb
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2020
ms.locfileid: "86461758"
---
# <a name="enroll-android-devices"></a>Registrieren von Android-Geräten

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Als Intune-Administrator können Sie Android-Geräte auf folgende Weisen registrieren:
- Android Enterprise bietet mehrere Registrierungsoptionen, die Benutzer mit den aktuellsten und sichersten Features versorgen:
    - [**Android Enterprise-Arbeitsprofil:** ](android-work-profile-enroll.md) Für persönliche Geräte mit Berechtigung für den Zugriff auf Unternehmensdaten. Administratoren können Arbeitskonten, -Apps und -daten verwalten. Auf dem Gerät gespeicherte persönliche Daten werden von den arbeitsbezogenen Daten getrennt, und Administratoren können weder auf persönliche Einstellungen noch auf persönliche Daten zugreifen. 
    - [**Dediziertes Android Enterprise:** ](android-kiosk-enroll.md) Für unternehmenseigene Geräte für einen einzigen Verwendungszweck, z. B. für die digitale Beschilderung, zum Drucken von Tickets oder für die Bestandsverwaltung. Administratoren beschränken die Verwendung eines Geräts auf eine begrenzte Anzahl von Apps und Weblinks. Außerdem wird verhindert, dass Benutzer andere Apps hinzufügen oder andere Aktionen auf dem Gerät ausführen können.
    - [**Vollständig verwaltetes Android Enterprise:** ](android-fully-managed-enroll.md) Für unternehmenseigene Geräte für einzelne Benutzer, die ausschließlich für die Arbeit verwendet werden, und nicht für persönliche Zwecke. Administratoren können das gesamte Gerät verwalten und Richtlinienkontrollen durchsetzen, die für Arbeitsprofile nicht verfügbar sind.
    - [**Android Enterprise unternehmenseigen mit Arbeitsprofil:** ](android-corporate-owned-work-profile-enroll.md) Dieses Profil ist für unternehmenseigene Einzelbenutzergeräte gedacht, die für die geschäftliche und private Benutzung vorgesehen sind.
- [**Als Android-Geräteadministrator**](android-enroll-device-administrator.md), einschließlich auf Geräten nach dem Samsung Knox Standard- und [Zebra-Geräten](../configuration/android-zebra-mx-overview.md). 

## <a name="prerequisites"></a>Voraussetzungen

Um auf die Verwaltung von mobilen Geräten vorzubereiten, müssen Sie die MDM-Autorität (Mobile Device Management, Verwaltung mobiler Geräte) auf **Microsoft Intune** festlegen. Anweisungen finden Sie unter [Festlegen der MDM-Autorität](../fundamentals/mdm-authority-set.md). Sie legen dieses Element nur einmal fest, wenn Sie die Ersteinrichtung von Intune für die Verwaltung mobiler Geräte durchführen.

Konsultieren Sie den folgenden Supportartikel von Google, um sicherzustellen, dass Android Enterprise in Ihrem Land oder Ihrer Region verfügbar ist: https://support.google.com/work/android/answer/6270910

Für von Zebra Technologies hergestellte Geräte müssen Sie abhängig von den Funktionen des jeweiligen Geräts dem Unternehmensportal möglicherweise zusätzliche Berechtigungen gewähren. Ausführliche Informationen finden Sie im Artikel zur [Erweiterung der Mobilität auf Zebra-Geräten](../configuration/android-zebra-mx-overview.md).

Für Samsung Knox Standard-Geräte gibt es [weitere Voraussetzungen](android-samsung-knox-mobile-enroll.md).

## <a name="next-steps"></a>Nächste Schritte

- [Set up enrollment of Android Enterprise work profile devices (Einrichten der Registrierung von Android Enterprise-Arbeitsprofilgeräten)](android-work-profile-enroll.md)
- [Set up Intune enrollment of Android Enterprise dedicated devices (Einrichten der Intune-Registrierung von dedizierten Android Enterprise-Geräten)](android-kiosk-enroll.md)
- [Set up Intune enrollment of Android Enterprise fully managed devices (Preview) (Einrichten der Intune-Registrierung von vollständig verwalteten Android Enterprise-Geräten (Preview))](android-fully-managed-enroll.md)
- [Einrichten der Android-Geräteadministratorregistrierung](android-enroll-device-administrator.md)

