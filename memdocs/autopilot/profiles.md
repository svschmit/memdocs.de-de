---
title: Autopilot-Profile konfigurieren
description: Erfahren Sie, wie Sie Geräteprofile für die Windows Autopilot-Bereitstellung konfigurieren.
keywords: MDM, Setup, Windows, Windows 10, OOBE, Manage, Bereitstellung, Autopilot, ZTD, Zero-Touchscreen, Partner, msfb, InTune
ms.reviewer: mniehaus
manager: laurawi
ms.technology: windows
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: dddabd1408a3f00c472ae787f201f3998c323482
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606567"
---
# <a name="configure-autopilot-profiles"></a>Autopilot-Profile konfigurieren

**Zielgruppe**

-  Windows 10

Sie müssen für jedes Gerät, das den Windows Autopilot-Bereitstellungs Dienst verwendet, ein Einstellungs Profil anwenden. Das Profil muss das genaue Bereitstellungs Verhalten des Geräts angeben. Ausführliche Verfahren zum Konfigurieren von Profileinstellungen und zum Registrieren von Geräten finden Sie unter [Registrieren von Geräten](add-devices.md#registering-devices).

## <a name="profile-settings"></a>Profileinstellungen

Die folgenden Profileinstellungen sind verfügbar:

-  Überspringen Sie die **Setup Seiten für Cortana, onedrive und OEM-Registrierung**. Bei allen mit Autopilot registrierten Geräten werden diese Seiten im zur Windows-Willkommensseite gehörigen Prozess automatisch übersprungen.

-  **Automatische Einrichtung für Arbeit oder Schule**. Alle Geräte, die bei Autopilot registriert sind, werden automatisch als Geschäfts-, Schul-oder unigeräte angesehen, sodass diese Frage während des OOBE-Prozesses nicht angezeigt

-  **Anmeldevorgang mit Unternehmens Branding**. Anstatt eine generische Azure AD Anmeldeseite darzustellen, stellen alle von Autopilot registrierten Geräten eine angepasste Anmeldeseite zur Verfügung. Auf dieser Seite werden der Name, das Logo und der zusätzliche Hilfe Text der Organisation angezeigt, wie in Azure AD konfiguriert. Informationen zum Anpassen dieser Einstellungen finden Sie [unter Hinzufügen von Unternehmens Branding zu Ihrem Verzeichnis](/azure/active-directory/customize-branding#add-company-branding-to-your-directory) .

-  Über **springen der Datenschutzeinstellungen**. Diese optionale Einstellung im Autopilot-Profil ermöglicht Organisationen, auf Fragen zu Datenschutzeinstellungen auf der Windows-Willkommensseite zu verzichten. Diese Einstellung ist in der Regel wünschenswert, damit die Organisation diese Einstellungen über InTune oder ein anderes Verwaltungs Tool konfigurieren kann.

-  **Deaktivieren Sie die lokale Administrator Kontoerstellung auf dem Gerät**. Organisationen können entscheiden, ob der Benutzer, der das Gerät einrichtet, nach Abschluss des Vorgangs Administratorrechte erhalten soll.

-  **Endbenutzer-Lizenzvertrag (EULA) überspringen**. In Windows 10, Version 1709 und höher, können Organisationen entscheiden, die während des OOBE-Prozesses dargestellten EULA-Seite zu überspringen. Das Überspringen der EULA-Seite bedeutet, dass Organisationen die Lizenzbedingungen für Ihre Benutzer akzeptieren.

-  **Deaktivieren Sie die Windows-consumerfeatures**. In Windows 10, Version 1803 und höher, können Unternehmen Windows-consumerfeatures deaktivieren. Wenn die Windows-consumerfeatures deaktiviert sind, werden vom Gerät nicht automatisch zusätzliche Microsoft Store-Apps installiert, wenn sich der Benutzer zum ersten Mal beim Gerät anmeldet. Weitere Informationen finden Sie in der [MDM-Dokumentation](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsconsumerfeatures).

## <a name="related-topics"></a>Verwandte Themen

[Profil Download](troubleshooting.md#profile-download)<br>
[Registrieren von Geräten](add-devices.md)
