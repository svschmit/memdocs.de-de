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
ms.openlocfilehash: eb591206ad61878bc2637bf1a10c2a1cec17ddba
ms.sourcegitcommit: 41e6e6b7f5c2a87aaf7f23d90d0f175dd63c0579
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2020
ms.locfileid: "89057362"
---
# <a name="windows-autopilot-device-guidelines"></a>Windows Autopilot-Geräte Richtlinien

**Zielgruppe**

- Windows 10

## <a name="hardware-and-firmware-best-practice-guidelines-for-windows-autopilot"></a>Best Practices-Richtlinien für Hardware und Firmware für Windows Autopilot

Alle Geräte mit Windows Autopilot müssen die [Mindesthardwareanforderungen](/windows-hardware/design/minimum/minimum-hardware-requirements-overview) für Windows 10 erfüllen.  

Mit den folgenden bewährten Methoden wird sichergestellt, dass Geräte im Rahmen des Windows Autopilot-Bereitstellungs Prozesses problemlos bereitgestellt werden können: 
- TPM 2,0 ist aktiviert und in einem ordnungsgemäßen Zustand (nicht im **Modus mit eingeschränkter Funktionalität**) auf Geräten vorgesehen, die für den selbst Bereitstellungs Modus von Windows Autopilot vorgesehen sind.
- Der OEM sollte eine der folgenden Informationen in den [SMBIOS-Feldern](/windows-hardware/drivers/bringup/smbios)bereitstellen. Die Informationen sollten den Microsoft-Spezifikationen entsprechen (Hersteller, Produkt Name und Seriennummer, die im SMBIOS-Typ 1 04h gespeichert sind, Typ 1 05h und Type 1 07h).
    - Eindeutige tupelinformationen (smbiossystemhersteller, smbiossystemproductname, smbiossystemserialnumber)
    - Pkid + smbiossystemserialnumber
- Bevor Geräte an einen Autopilot-Kunden oder-Kanalpartner versendet werden, sollte der OEM mithilfe des CBR-Berichts 4K-hardwarehashes an Microsoft hochladen. Die Hashes sollten mithilfe des OA3-Tools RS3 + im Überwachungsmodus im vollständigen Betriebssystem ausgeführt werden.
- Microsoft verlangt, dass OEM-Versand Treiber innerhalb von 30 Tagen nach dem CBR-Übermittlungs Datum in Windows Update veröffentlicht werden. System Firmware-und Treiber Updates werden innerhalb von 14 Tagen Windows Update veröffentlicht.
- Der OEM stellt sicher, dass das im SMBIOS bereitgestellte pkid an den Kanal übergeben wird.

## <a name="software-best-practice-guidelines-for-windows-autopilot"></a>Best Practices-Richtlinien für Windows Autopilot

- Das Windows Autopilot-Gerät sollte nur mit einem Windows 10-Basis Image Plus Treibern vorinstalliert werden.
- Sie können Ihre lizenzierte Version von Office vorinstallieren, z. b. [Microsoft 365 Apps für Unternehmen](/deployoffice/about-office-365-proplus-in-the-enterprise).
- Sofern nicht explizit vom Kunden angefordert, sollte keine andere vorinstallierte Software eingeschlossen werden.
  - Gemäß der OEM-Richtlinie sollten Windows 10-Features, einschließlich integrierter apps, nicht deaktiviert oder entfernt werden.

## <a name="next-steps"></a>Nächste Schritte

[Windows Autopilot-Kunden Zustimmung](registration-auth.md)<br>
[Leitfaden zum Austauschen von Austausch Szenarios](autopilot-mbr.md)<br>