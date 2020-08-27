---
title: Windows Autopilot-Geräte Richtlinien
ms.reviewer: ''
manager: laurawi
description: Erfahren Sie alles über Hardware, Firmware und bewährte Methoden für Software für die Windows Autopilot-Bereitstellung.
keywords: MDM, Setup, Windows, Windows 10, OOBE, Manage, Bereitstellung, Autopilot, ZTD, Zero-Touchscreen, Partner, msfb, InTune
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
ms.openlocfilehash: 326901cef5b337a505d85dc6c5706109ad9cbc1f
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908541"
---
# <a name="windows-autopilot-device-guidelines"></a>Windows Autopilot-Geräte Richtlinien

**Zielgruppe**

- Windows 10

## <a name="hardware-and-firmware-best-practice-guidelines-for-windows-autopilot"></a>Best Practices-Richtlinien für Hardware und Firmware für Windows Autopilot

Alle Geräte, die mit Windows Autopilot verwendet werden, müssen die [Mindesthardwareanforderungen](/windows-hardware/design/minimum/minimum-hardware-requirements-overview) für Windows 10 erfüllen.  

Mit den folgenden bewährten Methoden wird sichergestellt, dass Geräte im Rahmen des Windows Autopilot-Bereitstellungs Prozesses problemlos bereitgestellt werden können: 
- Stellen Sie sicher, dass das TPM 2,0 aktiviert ist und sich in einem ordnungsgemäßen Zustand (nicht im **reduzierten Funktionsmodus**) auf Geräten befindet, die für den selbst Bereitstellungs Modus von Windows Autopilot vorgesehen sind
- Der OEM stellt eindeutige tupelinformationen (smbiossystemhersteller, smbiossystemproductname, smbiossystemnumber) oder pkid + smbiossystemserialnumber in die [SMBIOS-Felder](/windows-hardware/drivers/bringup/smbios) pro Microsoft-Spezifikation (Hersteller, Produkt Name und Seriennummer, die in SMBIOS Type 1 04h gespeichert sind, Typ 1 05h und Type 1 07h)
- Der OEM lädt 4K-hardwarehashes hoch, die mit dem OA3-Tool RS3 + im Überwachungsmodus auf dem vollständigen Betriebssystem für Microsoft über den CBR-Bericht ausgeführt wurden, bevor Geräte an einen Autopilot-Kunden oder einen
- Microsoft verlangt, dass OEM-Versand Treiber innerhalb von 30 Tagen nach der Übermittlung der CBR in Windows Update veröffentlicht werden. System Firmware-und Treiber Updates werden innerhalb von 14 Tagen Windows Update veröffentlicht.
- Der OEM stellt sicher, dass das im SMBIOS bereitgestellte pkid an den Kanal übergeben wird.

## <a name="software-best-practice-guidelines-for-windows-autopilot"></a>Best Practices-Richtlinien für Windows Autopilot

- Das Windows Autopilot-Gerät sollte nur mit einem Windows 10-Basis Image Plus Treibern vorinstalliert werden.
- Sie können Ihre lizenzierte Version von Office vorinstallieren, z. b. [Microsoft 365 Apps für Unternehmen](/deployoffice/about-office-365-proplus-in-the-enterprise).
- Sofern nicht explizit vom Kunden angefordert, sollte keine andere vorinstallierte Software eingeschlossen werden.
  - Gemäß der OEM-Richtlinie sollten Windows 10-Features, einschließlich integrierter apps, nicht deaktiviert oder entfernt werden.

## <a name="related-topics"></a>Zugehörige Themen

[Windows Autopilot-Kunden Zustimmung](registration-auth.md)<br>
[Leitfaden zum Austauschen von Austausch Szenarios](autopilot-mbr.md)<br>