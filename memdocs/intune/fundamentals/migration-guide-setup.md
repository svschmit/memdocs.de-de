---
title: Grundlegende Einrichtung von Microsoft Intune
description: Dieser Artikel enthält die notwendigen Schritte zum Einrichten von Microsoft Intune.
keywords: ''
author: dougeby
ms.author: dougeby
manager: dougeby
ms.date: 03/04/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 60cfa440-0723-4ea0-bacf-3c5d26f9a1d3
ms.reviewer: dagerrit
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: c39174dded9fae0055786b6132b3f964f187b1b1
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88992707"
---
# <a name="basic-setup"></a>Grundlegende Einrichtung

Nachdem Sie Ihre Umgebung analysiert haben, können Sie mit dem Einrichten von Microsoft Intune beginnen.

## <a name="external-dependencies-for-an-intune-deployment"></a>Externe Abhängigkeiten für eine Bereitstellung mit Intune

### <a name="identity"></a>Identität

Intune erfordert Azure Active Directory (Azure AD) als Identitäts- und Benutzergruppierungsanbieter. Weitere Informationen:

- [Identitätsanforderungen](/azure/active-directory/active-directory-hybrid-identity-design-considerations-overview#design-considerations-overview)

- [Anforderungen für die Verzeichnissynchronisierung](/azure/active-directory/active-directory-hybrid-identity-design-considerations-directory-sync-requirements)

- [So funktioniert's: Azure Multi-Factor Authentication](/azure/active-directory/authentication/concept-mfa-howitworks)

- [Planen von Benutzer- und Gerätegruppen](users-add.md)

- [Erstellen von Benutzer- und Gerätegruppen](groups-get-started.md)

Wenn in Ihrer Organisation bereits Microsoft 365 verwendet wird, muss Intune dieselbe Azure Active Directory-Umgebung verwenden.

### <a name="pki-optional"></a>PKI (optional)

Wenn Sie die zertifikatbasierte Authentifizierung für VPN-, WLAN- oder E-Mail-Profile von Intune verwenden möchten, müssen Sie sicherstellen, dass eine [unterstützte PKI-Infrastruktur](../protect/certificates-configure.md) vorhanden ist, in der Zertifikatprofile erstellt und bereitgestellt werden können. Weitere Informationen zum Konfigurieren von Zertifikaten in Intune:

- [Konfigurieren der Zertifikatinfrastruktur für SCEP](/intune/certificates-scep-configure)

- [Konfigurieren der Zertifikatinfrastruktur für PFX](/intune/certficates-pfx-configure)

## <a name="task-list-for-an-intune-setup"></a>Aufgabenliste für die Einrichtung von Intune

### <a name="task-1-intune-subscription"></a>Aufgabe 1: Intune-Abonnement

Bevor Sie zu Intune migrieren können, brauchen Sie ein [Intune-Abonnement](account-sign-up.md).

### <a name="task-2-assign-intune-user-licenses"></a>Aufgabe 2: Zuweisen von Intune-Benutzerlizenzen

- Erfahren Sie, wie Sie [Intune-Benutzerlizenzen zuweisen](licenses-assign.md) können.

- Wenn Sie bereits einen neuen AAD-Mandanten erstellt haben, erfahren Sie, wie Sie [neue Benutzer erstellen oder Benutzer aus Ihrem lokalen Active Directory (AD) synchronisieren](/azure/active-directory/connect/active-directory-aadconnect) können.

### <a name="task-3-set-your-mdm-authority-to-intune"></a>Aufgabe 3: Stellen Sie die MDM-Autorität auf Intune um

Es wird empfohlen, Intune über das [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) zu verwalten.

Legen Sie Ihre MDM-Autorität auf **Intune** fest. Wenn Sie eine andere MDM-Autorität verwenden, ist es Intune möglich, die MDM-Verwaltung auf andere Verwaltungskonsolen von Microsoft zu übertragen. Das geschieht jedoch selten.

> [!IMPORTANT]
> Wenn Sie Ihr MDM zum ersten Mal an Intune übertragen, sollten Sie die MDM-Autorität auf Intune festlegen.

Erfahren Sie, wie Sie die [Autorität für die Verwaltung mobiler Geräte einrichten](mdm-authority-set.md) können.

## <a name="next-step"></a>Nächste Schritte

Konfigurieren Sie [Richtlinien für die Verwaltung von Apps und Geräten](migration-guide-configure-policies.md).