---
title: Voraussetzungen für WLAN- und VPN-Profile
titleSuffix: Configuration Manager
description: In diesem Artikel erfahren Sie mehr über die Voraussetzungen für die Verwaltung von WLAN- und VPN-Profilen in Configuration Manager.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d2dacb2d-ab3b-42a2-8dc8-94da31f993c2
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9e7a557bab6b41be6e6335e3aa2744e8627d285b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706068"
---
# <a name="prerequisites-for-wi-fi-and-vpn-profiles-in-configuration-manager"></a>Voraussetzungen für WLAN- und VPN-Profile in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

WLAN- und VPN-Profile in Configuration Manager weisen nur Abhängigkeiten innerhalb des Produkts auf.

Sie müssen über die folgenden Sicherheitsberechtigungen verfügen, um Einstellungen für den Zugriff auf Unternehmensressourcen wie Zertifikatprofile, WLAN- und VPN-Profile zu verwalten:  

- Anzeigen und Verwalten von Warnungen und Berichten für WLAN- und VPN-Profile: **Erstellen**, **Löschen**, **Ändern**, **Bericht ändern**, **Lesen** und **Bericht ausführen** für das Objekt **Warnungen**  

- So erstellen und verwalten Sie Zertifikatprofile: **Richtlinie erstellen**, **Bericht ändern**, **Lesen** und **Bericht ausführen** für das Objekt **Zertifikatprofil**  

- So verwalten Sie Bereitstellungen von WLAN-, VPN- und Zertifikatprofilen: **Konfigurationsrichtlinien bereitstellen**, **Warnung zu Clientstatus ändern**, **Lesen** und **Ressource lesen** für das Objekt **Sammlung**  

- So verwalten Sie alle Konfigurationsrichtlinien: **Erstellen**, **Löschen**, **Ändern**, **Lesen** und **Sicherheitsbereich festlegen** für das Objekt **Konfigurationsrichtlinie**  

- Ausführen von Abfragen zu WLAN- und VPN-Profilen: Berechtigung **Lesen** für das Objekt **Abfrage**  

- So zeigen Sie Informationen zu WLAN- und VPN-Profilen in der Configuration Manager-Konsole an: Berechtigung **Lesen** für das Objekt **Standort**.  

- Anzeigen von Statusmeldungen für WLAN- und VPN-Profile: Berechtigung **Lesen** für das Objekt **Statusmeldungen**  

- So erstellen und ändern Sie das Profil des vertrauenswürdigen Zertifizierungsstellenzertifikats: **Richtlinie erstellen**, **Bericht ändern**, **Lesen** und **Bericht ausführen** für das Objekt **Profil des vertrauenswürdigen Zertifizierungsstellenzertifikats**  

- So erstellen und verwalten Sie VPN-Profile: **Richtlinie erstellen**, **Bericht ändern**, **Lesen** und **Bericht ausführen** für das Objekt **VPN-Profil**  

- So erstellen und verwalten Sie WLAN-Profile: **Richtlinie erstellen**, **Bericht ändern**, **Lesen** und **Bericht ausführen** für das Objekt **WLAN-Profil**  

In der Sicherheitsrolle **Zugriffs-Manager für Unternehmensressourcen** sind die Berechtigungen enthalten, die beim Verwalten von WLAN-Profilen in Configuration Manager benötigt werden. Weitere Informationen finden Sie unter [Konfigurieren der Sicherheit in Configuration Manager](../../core/plan-design/security/configure-security.md).
