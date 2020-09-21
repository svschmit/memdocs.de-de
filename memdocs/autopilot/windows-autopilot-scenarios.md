---
title: Windows Autopilot-Szenarios und-Funktionen
description: Befolgen Sie einige typische Windows Autopilot-Bereitstellungs Szenarien, wie z. b. das erneute Bereitstellen eines Geräts in einem betriebsbereiten Zustand.
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
ms.openlocfilehash: 1755399ad67cd073c71f2a26ef4305bec5a53f51
ms.sourcegitcommit: 7037d2cd6b4e3d3e75471db33f22d475dfd89f5e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/19/2020
ms.locfileid: "90814872"
---
# <a name="windows-autopilot-scenarios-and-capabilities"></a>Windows Autopilot-Szenarios und-Funktionen

**Gilt für: Windows 10**

## <a name="scenarios"></a>Szenarien

Windows Autopilot unterstützt eine wachsende Liste der Szenarien, die Organisationen häufig benötigen. Diese Anforderungen variieren je nach den folgenden:
- Organisationsart.
- Fortschritt bei der Umstellung auf Windows 10.
- Wie weit Sie [zur modernen Verwaltung übergehen](/windows/client-management/manage-windows-10-in-your-organization-modern-management).

Die folgenden Windows Autopilot-Szenarien werden in diesem Handbuch beschrieben:

| Szenario | Weitere Informationen |
| --- | --- |
| Bereitstellen und Konfigurieren von Geräten, damit ein Endbenutzer diese für sich selbst einrichten kann | [Benutzergesteuerter Modus von Windows Autopilot](user-driven.md) |
| Stellen Sie Geräte bereit, die automatisch für die freigegebene Verwendung, als Kiosk oder als digitales Geräte Gerät konfiguriert werden sollen.| [Selbstbereitstellungs Modus von Windows Autopilot](self-deploying.md) |
| Erneutes Bereitstellen eines Geräts in einem betriebsbereiten Zustand.| [Windows Autopilot Reset](windows-autopilot-reset.md) |
| Vorab Bereitstellung eines Geräts mit aktuellen Anwendungen, Richtlinien und Einstellungen.| [Intensive Benutzerunterstützung](white-glove.md) |
| Bereitstellen von Windows 10 auf einem vorhandenen Windows 7-oder 8,1-Gerät | [Windows Autopilot für vorhandene Geräte](existing-devices.md) |

Diese Szenarien werden im folgenden Video zusammengefasst.

&nbsp;

> [!video https://www.microsoft.com/videoplayer/embed/RE4Ci1b?autoplay=false]

## <a name="windows-autopilot-capabilities"></a>Windows Autopilot-Funktionen

### <a name="windows-autopilot-is-self-updating-during-oobe"></a>Windows Autopilot ist während des OOBE-Updates selbst Aktualisier.

Bei Geräten unter Windows 10, Version 1903 und höher, werden bei der Verwendung von Autopilot-funktionalen Updates und kritischen Updates während der Erstellung automatisch heruntergeladen:
- Das Gerät ist mit einem Netzwerk verbunden.
- Die [Updates kritischer Treiber und Windows Zero-Day Patch (ZDP)](/windows-hardware/customize/desktop/windows-updates-during-oobe) sind fertiggestellt.

Diese Autopilot-Updates können nicht deaktiviert werden, da Sie für die Windows Autopilot-Bereitstellung erforderlich sind. Windows benachrichtigt den Benutzer, dass das Gerät die Updates überprüft, herunterlädt und installiert.

Weitere Informationen finden Sie unter [Windows Autopilot Update](autopilot-update.md).

### <a name="cortana-voiceover-and-speech-recognition-during-oobe"></a>Cortana VoiceOver und Spracherkennung während OOBE

In Windows 10, Version 1903 und höher, ist Cortana VoiceOver und die Spracherkennung während OOBE standardmäßig deaktiviert. Diese Standardeinstellung gilt für alle Windows 10 pro-, Education-und Enterprise-SKUs.

Sie können auch Cortana VoiceOver und die Spracherkennung während der OOBE aktivieren, indem Sie den folgenden Registrierungsschlüssel erstellen. Dieser Schlüssel ist standardmäßig nicht vorhanden:

Hklm\software\microsoft\windows\currentversion\oobe\enablevoiceforalleditions

Der Schlüsselwert ist ein DWORD-Wert, bei dem **0** = deaktiviert und **1** = aktiviert ist.

| Wert | Beschreibung |
| --- | --- |
| 0 | Cortana VoiceOver ist deaktiviert. |
| 1 | Cortana VoiceOver ist aktiviert |
| Kein Wert | Das Gerät wird auf das Standardverhalten der Edition zurückgreifen. |

Um diesen Schlüsselwert zu ändern, verwenden Sie das WCD-Tool zum Erstellen von As ppkg, wie [hier](/windows/configuration/wcd/wcd-oobe#nforce)dokumentiert.

### <a name="bitlocker-encryption"></a>BitLocker-Verschlüsselung

Mit Windows Autopilot können Sie die BitLocker-Verschlüsselungseinstellungen so konfigurieren, dass Sie vor dem Start der automatischen Verschlüsselung angewendet werden. Weitere Informationen finden Sie unter [Festlegen des BitLocker-Verschlüsselungsalgorithmus für Autopilot-Geräte](bitlocker.md) .

## <a name="related-topics"></a>Zugehörige Themen

[Windows Autopilot: Neuerungen](windows-autopilot-whats-new.md)