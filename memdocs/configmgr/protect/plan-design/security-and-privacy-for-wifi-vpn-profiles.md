---
title: Sicherheit und Datenschutz für WLAN- und VPN-Profile
titleSuffix: Configuration Manager
description: In diesem Artikel lernen Sie die Sicherheitsempfehlungen bei der Verwaltung von WLAN- und VPN-Profilen für Geräte in Configuration Manager kennen.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: ef3ab519-9cf7-47fc-8831-d400e0e96df8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: a6f444e35e16a3b42414fdc6fbee50687cf76f2f
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705978"
---
# <a name="security-and-privacy-for-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Sicherheit und Datenschutz bei WLAN-Profilen und VPN-Profilen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

## <a name="security-recommendations"></a>Empfehlungen zur Sicherheit

Verwenden Sie die folgenden bewährten Sicherheitsmethoden bei der Verwaltung von WLAN- und VPN-Profilen für Geräte.

### <a name="choose-the-most-secure-options-that-your-wi-fi-and-vpn-infrastructure-and-client-operating-systems-can-support"></a>Wählen Sie die sichersten Optionen aus, die von der WLAN- und VPN-Infrastruktur sowie den Clientbetriebssystemen unterstützt werden.

WLAN- und VPN-Profile stellen eine praktische Methode dar, um von Ihren Geräten bereits unterstützte WLAN- und VPN-Einstellungen zentral zu verteilen und zu verwalten. Configuration Manager bietet keine zusätzlichen WLAN- oder VPN-Funktionen. Ermitteln, implementieren und befolgen Sie alle Sicherheitsempfehlungen für Ihre Geräte und Infrastruktur.

## <a name="privacy-information"></a>Datenschutzinformationen

Sie können WLAN- und VPN-Profile verwenden, um Clientgeräte für die Verbindung mit WLAN- und VPN-Servern zu konfigurieren. Verwenden Sie dann Configuration Manager, um zu ermitteln, ob diese Geräte nach der Anwendung der Profile konform sein werden. Vom Verwaltungspunkt werden Kompatibilitätsinformationen an den Standortserver gesendet, die dann in der Standortdatenbank gespeichert werden. Die Informationen werden verschlüsselt, wenn sie von Geräten an den Verwaltungspunkt gesendet werden, sie werden aber nicht in einem verschlüsselten Format in der Standortdatenbank gespeichert. Die Informationen verbleiben in der Datenbank, bis sie mit dem Standortwartungstask **Veraltete Konfigurationsverwaltungsdaten löschen** gelöscht werden. Das Löschintervall beträgt standardmäßig 90 Tage, kann aber geändert werden. Die Konformitätsinformationen werden nicht an Microsoft gesendet.

Standardmäßig werden WLAN- und VPN-Profile nicht von Geräten ausgewertet. Darüber hinaus müssen Sie die Profile konfigurieren und sie dann für Benutzer bereitstellen.  

Berücksichtigen Sie vor dem Konfigurieren der WLAN- und VPN-Profile Ihre Datenschutzanforderungen.  
