---
title: Autopilot-Profile konfigurieren
description: Erfahren Sie, wie Sie Geräteprofile beim Ausführen einer Windows Autopilot-Bereitstellung konfigurieren.
keywords: MDM, Setup, Windows, Windows 10, OOBE, Manage, Bereitstellung, Autopilot, ZTD, Zero-Touchscreen, Partner, msfb, InTune
ms.reviewer: mniehaus
manager: laurawi
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
ms.openlocfilehash: 0a18eb4020a32e752c9d3fa7988e411dc72be98e
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756614"
---
# <a name="configure-autopilot-profiles"></a>Autopilot-Profile konfigurieren

**Zielgruppe**

-   Windows 10

Für jedes Gerät, das für den Windows Autopilot-Bereitstellungs Dienst definiert wurde, muss ein Profil mit Einstellungen angewendet werden, das das genaue Verhalten dieses Geräts bei der Bereitstellung angibt. Ausführliche Verfahren zum Konfigurieren von Profileinstellungen und zum Registrieren von Geräten finden Sie unter [Registrieren von Geräten](add-devices.md#registering-devices).

## <a name="profile-settings"></a>Profileinstellungen

Die folgenden Profileinstellungen sind verfügbar:

-   Überspringen Sie die **Setup Seiten für Cortana, onedrive und OEM-Registrierung**. Bei allen mit Autopilot registrierten Geräten werden diese Seiten im zur Windows-Willkommensseite gehörigen Prozess automatisch übersprungen.

-   **Automatische Einrichtung für Arbeit oder Schule**. Alle Geräte, die bei Autopilot registriert sind, werden automatisch als Geschäfts-, Schul-oder unigeräte angesehen, sodass diese Frage während des OOBE-Prozesses nicht angezeigt wird

-   **Anmeldevorgang mit Unternehmens Branding**. Anstatt eine generische Azure Active Directory Anmeldeseite darzustellen, stellen alle Geräte, die bei Autopilot registriert sind, eine angepasste Anmeldeseite mit dem Namen, Logo und zusätzlichen Hilfe Text der Organisation dar, die in Azure Active Directory konfiguriert ist. Informationen zum Anpassen dieser Einstellungen finden Sie [unter Hinzufügen von Unternehmens Branding zu Ihrem Verzeichnis](https://docs.microsoft.com/azure/active-directory/customize-branding#add-company-branding-to-your-directory) .

-   Über **springen der Datenschutzeinstellungen**. Diese optionale Einstellung im Autopilot-Profil ermöglicht Organisationen, auf Fragen zu Datenschutzeinstellungen auf der Windows-Willkommensseite zu verzichten. Dies ist in der Regel wünschenswert, damit die Organisation diese Einstellungen über InTune oder ein anderes Verwaltungs Tool konfigurieren kann.

-   **Deaktivieren Sie die lokale Administrator Kontoerstellung auf dem Gerät**. Organisationen können entscheiden, ob der Benutzer, der das Gerät einrichtet, nach Abschluss des Vorgangs Administratorrechte erhalten soll.

-   **Endbenutzer-Lizenzvertrag (EULA) überspringen**. In Windows 10, Version 1709 und höher, können Organisationen entscheiden, die während des OOBE-Prozesses dargestellten EULA-Seite zu überspringen. Dies bedeutet, dass Organisationen die Lizenzbedingungen im Namen Ihrer Benutzer akzeptieren.

-   **Deaktivieren Sie die Windows-consumerfeatures**. In Windows 10, Version 1803 und höher, können Organisationen Windows-consumerfeatures deaktivieren, sodass das Gerät nicht automatisch zusätzliche Microsoft Store-Apps installiert, wenn sich der Benutzer zum ersten Mal beim Gerät anmeldet. Weitere Informationen finden Sie in der [MDM-Dokumentation](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsconsumerfeatures).

## <a name="related-topics"></a>Zugehörige Themen

[Profil Download](troubleshooting.md#profile-download)<br>
[Registrieren von Geräten](add-devices.md)
