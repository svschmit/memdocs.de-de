---
title: Neues in Windows Autopilot
ms.reviewer: ''
manager: laurawi
description: Lesen Sie Neuigkeiten und Ressourcen zu den neuesten Updates und früheren Versionen von Windows Autopilot.
keywords: MDM, Setup, Windows, Windows 10, OOBE, Manage, Bereitstellung, Autopilot, ZTD, Zero-Touchscreen, Partner, msfb, InTune
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
ms.openlocfilehash: 736e01696cf503b63762c32a9acee3cb68c1e241
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606564"
---
# <a name="windows-autopilot-whats-new"></a>Windows Autopilot: Neuerungen

**Zielgruppe**

- Windows 10

## <a name="windows-autopilot-update-history"></a>Windows Autopilot Update-Verlauf

Die folgenden [Windows Autopilot-Updates](autopilot-update.md) sind verfügbar. **Hinweis**: Updates werden während des Windows Autopilot-Bereitstellungs Prozesses automatisch heruntergeladen und angewendet. 

Es sind noch keine Updates verfügbar. Weitere Informationen finden Sie später hier.

## <a name="new-in-windows-10-version-2004"></a>Neu in Windows 10, Version 2004

Mit dieser Version können Sie den Windows Autopilot [-benutzergesteuerten](user-driven.md) Hybrid Azure Active Directory Join mit VPN-Unterstützung konfigurieren. Diese Unterstützung wird auch auf Windows 10, Version 1909 und 1903, Rück portiert.

Wenn Sie die Spracheinstellungen im Autopilot-Profil konfigurieren und das Gerät mit Ethernet verbunden ist, überspringen alle Szenarios nun die Sprache, das Gebiets Schema und die Tastatur Seiten. In früheren Versionen wurde dies nur bei selbst Bereitstellungs Profilen unterstützt.

## <a name="new-in-windows-10-version-1903"></a>Neu in Windows 10, Version 1903

Die [Windows Autopilot for White Glove-Bereitstellung](white-glove.md) ist neu in Windows 10, Version 1903. Sehen Sie sich das folgende Video an:

<br>

> [!VIDEO https://www.youtube.com/embed/nE5XSOBV0rI]

Auch in dieser Windows-Version neu:
- Auf der InTune-Seite zum Registrierungsstatus (ESP) werden nun InTune-Verwaltungs Erweiterungen nachverfolgt.
- [Cortana VoiceOver und die Spracherkennung während OOBE](windows-autopilot-scenarios.md#cortana-voiceover-and-speech-recognition-during-oobe) sind für alle Windows 10 pro Education-und Enterprise-SKUs standardmäßig deaktiviert.
- [Windows Autopilot ist während des OOBE-Updates selbst Aktualisier](windows-autopilot-scenarios.md#windows-autopilot-is-self-updating-during-oobe). Ab Windows 10 werden die funktionalen und kritischen Updates der Version 1903 automatisch während des OOBE-Vorgangs heruntergeladen.
- Windows Autopilot legt die Diagnosedaten Ebene während des OOBE-Betriebs auf Geräten mit Windows 10, Version 1903 oder höher, auf Full fest. 

## <a name="new-in-windows-10-version-1809"></a>Neu in Windows 10, Version 1809

Der [Self-Bereitstellung-Modus](self-deploying.md) von Windows Autopilot ist ein Geräte Bereitstellungs Prozess mit Zero-Note. Schalten Sie einfach das Gerät ein, stellen Sie eine Verbindung mit Ethernet her, und Autopilot konfiguriert das Gerät automatisch. Endbenutzer müssen während des Bereitstellungs Vorgangs nicht auf die Schaltfläche "weiter" klicken. 

Sie können den Windows Autopilot-Modus für die selbst Bereitstellung verwenden, um das Gerät bei einem Aad-Mandanten zu registrieren, den MDM-Anbieter Ihrer Organisation zu registrieren und Richtlinien und Anwendungen bereitzustellen. Es ist keine Benutzerauthentifizierung oder Benutzerinteraktion erforderlich.

>[!NOTE]
>Windows 10, Version 1903 oder höher, ist erforderlich, um den Modus für die selbst Bereitstellung aufgrund von Problemen mit dem TPM-Geräte Nachweis in Windows 10, Version 1809, zu verwenden.

## <a name="related-topics"></a>Verwandte Themen

[Neues in Microsoft InTune](/intune/whats-new)<br>
[Neuerungen in Windows 10](/windows/whats-new/)
