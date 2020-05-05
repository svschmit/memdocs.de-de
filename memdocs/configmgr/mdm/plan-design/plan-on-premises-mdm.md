---
title: Planen von lokalem MDM
titleSuffix: Configuration Manager
description: Planen der lokalen Verwaltung mobiler Geräte zur Verwaltung mobiler Geräte in Configuration Manager
ms.date: 01/09/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: 02979fb8-ea7e-4ec6-b7e0-ecbfda73e52d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5690e4fe003939d00dee1185e6f6551813c346e5
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724694"
---
# <a name="plan-for-on-premises-mdm-in-configuration-manager"></a>Planen der lokalen Verwaltung mobiler Geräte (MDM) in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Wenn Sie planen, die lokale Verwaltung mobiler Geräte (Mobile Device Management, MDM) in Configuration Manager zu implementieren, können Sie verschiedene wichtige Bereiche überprüfen:

- Unterstützte Geräte und Betriebssystemversionen
- Erforderliche Standortsystemrollen
- Sichere Kommunikation
- Geräteregistrierung

> [!IMPORTANT]
> Während der Standort oder jedes mobile Gerät keine Verbindung mit Microsoft InTune herstellt, benötigt Ihre Organisation weiterhin InTune-Lizenzen, um dieses Feature zu verwenden. Weitere Informationen finden Sie unter [Microsoft InTune-Lizenzierung](https://docs.microsoft.com/intune/fundamentals/licenses).

Berücksichtigen Sie die folgenden Anforderungen, bevor Sie die Configuration Manager-Infrastruktur für die lokale Verwaltung mobiler Geräte (MDM) vorbereiten.

## <a name="supported-devices"></a><a name="bkmk_devices"></a> Unterstützte Geräte  

Der Current Branch von Configuration Manager unterstützt die Registrierung bei der lokalen Verwaltung mobiler Geräte für Windows 10-Geräte. Diese Gerätetypen umfassen hauptsächlich Laptops, IOT und Surface Hub. Weitere Informationen und die Liste der spezifischen Editionen finden Sie [unter Unterstützte Betriebssystemversionen für Clients und Geräte](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS).

## <a name="site-system-roles"></a><a name="bkmk_roles"></a> Standortsystemrollen

Lokale MDM erfordert mindestens eine der folgenden Standortsystem Rollen:

- **Anmeldungsproxypunkt** zur Unterstützung von Anmeldungsanforderungen.

- **Anmeldungspunkt** zur Unterstützung der Geräteanmeldung.

- **Geräteverwaltungspunkt** für die Bereitstellung von Richtlinien. Diese Rolle ist eine Variante des Verwaltungs Punkts, ermöglicht aber die Verwaltung mobiler Geräte.

- **Verteilungspunkt** für die Inhaltsübermittlung.

Abhängig von den Anforderungen Ihrer Organisation können Sie diese Rollen auf dem einzelnen Server oder separat auf verschiedenen Servern installieren.

> [!NOTE]
> Sie müssen jede Rolle, die für die lokale MDM verwendet wird, als HTTPS-Endpunkt für die Kommunikation mit vertrauenswürdigen Geräten konfigurieren. Weitere Informationen finden Sie unter [Erforderliche vertrauenswürdige Kommunikation](#bkmk_trustedComs).

Weitere allgemeine Informationen finden Sie unter [Planen für Standortsystem Server und-Rollen](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).

## <a name="trusted-communications"></a><a name="bkmk_trustedComs"></a>Vertrauenswürdige Kommunikation

Lokale MDM erfordert, dass Sie Standortsystem Rollen für die HTTPS-Kommunikation aktivieren. Abhängig von Ihren Anforderungen können Sie die Zertifizierungsstelle (ca) Ihrer Organisation verwenden, um die vertrauenswürdigen Verbindungen zwischen Servern und Geräten herzustellen. Sie können auch eine öffentlich verfügbare Zertifizierungsstelle als vertrauenswürdige Zertifizierungsstelle verwenden. In jedem Fall müssen Sie die folgenden Zertifikate konfigurieren:

- Ein **Webserver Zertifikat** in IIS auf den Servern, auf denen die erforderlichen Standortsystem Rollen gehostet werden. Wenn ein Server mehrere Standortsystem Rollen hostet, benötigen Sie nur ein Zertifikat für diesen Server. Wenn sich jede Rolle auf einem separaten Server befindet, benötigt jeder Server ein separates Zertifikat.

- Das **Vertrauenswürdige Stamm Zertifikat der Zertifizierungs** Stelle, von der die Webserver Zertifikate ausgestellt werden. Installieren Sie dieses Stamm Zertifikat auf allen Geräten, von denen eine Verbindung mit den Standortsystem Rollen hergestellt werden muss.

Weitere Informationen finden Sie unter [Einrichten von Zertifikaten für vertrauenswürdige Verbindungen in der](../get-started/set-up-certificates-on-premises-mdm.md)lokalen Verwaltung mobiler Geräte (MDM).

## <a name="device-enrollment"></a><a name="bkmk_enrollment"></a>Geräteregistrierung

So aktivieren Sie die Geräteregistrierung für die lokale Verwaltung mobiler Geräte:

- Erteilen der Berechtigung zum Registrieren über Client Einstellungen für Benutzer

- Konfigurieren von Geräten für die vertrauenswürdige Kommunikation mit den Standortsystem Servern, die die erforderlichen Rollen hosten

Als Alternative zur Benutzer initiierten Registrierung können Sie ein Massen Registrierungspaket einrichten. Mit diesem Paket kann das Gerät ohne Benutzereingriff registriert werden. Übermitteln Sie das Paket an das Gerät, bevor es für die Verwendung bereitgestellt wird oder nachdem es den OOBE-Prozess durchlaufen hat.

Weitere Informationen finden Sie unter [Einrichten der Geräteregistrierung für die lokale Verwaltung mobiler Geräte (MDM](../get-started/set-up-device-enrollment-on-premises-mdm.md)).

## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Installieren von Standortsystemrollen](../get-started/install-site-system-roles-for-on-premises-mdm.md)
