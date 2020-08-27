---
title: Dfci-Verwaltung
ms.reviewer: ''
manager: laurawi
description: Mit der Windows Autopilot-Bereitstellung und InTune können Sie UEFI-Einstellungen (BIOS) verwalten, nachdem Sie mithilfe der Device Firmware Configuration Interface (dfci) registriert wurden.
keywords: Autopilot, dfci, UEFI, Windows 10
ms.prod: w10
ms.mktglfcycl: deploy
ms.sitesec: library
ms.pagetype: deploy
ms.localizationpriority: medium
audience: itpro
author: greg-lindsay
ms.author: greglin
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: df49fb939b709c15f2b01b3577f7fc7ced60140d
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908345"
---
# <a name="dfci-management"></a>Dfci-Verwaltung

**Zielgruppe**

-   Windows 10

Mit der Windows Autopilot-Bereitstellung und InTune können Sie die Einstellungen für Unified Extensible Firmware Interface (UEFI) verwalten, nachdem Sie mithilfe der Device Firmware Configuration Interface (dfci) registriert wurden.  Dfci [ermöglicht Windows das Übergeben von Verwaltungs Befehlen](/windows/client-management/mdm/uefi-csp) von InTune an UEFI an von Autopilot bereitgestellte Geräte. Dies ermöglicht es Ihnen, die Kontrolle über die BIOS-Einstellungen des Endbenutzers einzuschränken. Beispielsweise können Sie die Startoptionen sperren, um zu verhindern, dass Benutzer ein anderes Betriebssystem starten, z. b. eine, die nicht über die gleichen Sicherheitsfeatures verfügt.

Wenn ein Benutzer eine frühere Windows-Version neu installiert, ein separates Betriebssystem installiert oder die Festplatte formatiert, kann die dfci-Verwaltung nicht außer Kraft gesetzt werden. Diese Funktion kann auch verhindern, dass Schadsoftware mit Betriebssystem Prozessen kommuniziert, einschließlich erhöhter Betriebssystem Prozesse. Die Vertrauenskette von dfci verwendet die Kryptografie mit öffentlichem Schlüssel und ist nicht von der lokalen UEFI-Kenn Wort Sicherheit abhängig. Diese Sicherheitsebene blockiert lokale Benutzer am Zugriff auf verwaltete Einstellungen aus den UEFI-Menüs des Geräts.

Eine Übersicht über die Vorteile von dfci, Szenarien und Voraussetzungen finden Sie unter Einführung in die [dfci (Device Firmware Configuration Interface)](https://microsoft.github.io/mu/dyn/mu_plus/DfciPkg/Docs/Dfci_Feature/).

## <a name="dfci-management-lifecycle"></a>Dfci-Verwaltungs Lebenszyklus

Der dfci-Verwaltungs Lebenszyklus kann als UEFI-Integration, Geräteregistrierung, Profilerstellung, Registrierung, Verwaltung, Deaktivierung und Wiederherstellung angezeigt werden. Dies wird in der folgenden Abbildung veranschaulicht.

   ![Lebenszyklus](images/dfci.png)

## <a name="requirements"></a>Requirements (Anforderungen)

- Windows 10, Version 1809 oder höher, und eine unterstützte UEFI-Version ist erforderlich.
- Der Gerätehersteller muss dfci der UEFI-Firmware im Fertigungsprozess oder als Firmwareupdate hinzugefügt haben, das Sie installieren. Arbeiten Sie mit ihren Geräte Anbietern zusammen, um die Hersteller zu ermitteln, die [dfci unterstützen](#oems-that-support-dfci), oder die Firmwareversion für die Verwendung von dfci.
- Das Gerät muss mit Microsoft InTune verwaltet werden. Weitere Informationen finden Sie unter [Registrieren von Windows-Geräten in InTune mithilfe von Windows Autopilot](/intune/enrollment/enrollment-autopilot).
- Das Gerät muss von einem [CSP-Partner (Microsoft Cloud Solution Provider)](https://partner.microsoft.com/membership/cloud-solution-provider) oder direkt vom OEM für Windows Autopilot registriert werden. 

>[!IMPORTANT]
>Geräte, die manuell für Autopilot registriert sind (z. b. durch den [Import aus einer CSV-Datei](/intune/enrollment/enrollment-autopilot#add-devices)), dürfen dfci nicht verwenden. Die DFCI-Verwaltung erfordert standardmäßig den externen Nachweis der kommerziellen Beschaffung des Geräts über eine OEM- oder CSP-Partnerregistrierung bei Windows Autopilot. Wenn Ihr Gerät registriert ist, wird seine Seriennummer in der Liste der Windows Autopilot-Geräte angezeigt.

## <a name="managing-dfci-profile-with-windows-autopilot"></a>Verwalten des dfci-Profils mit Windows Autopilot

Bei der Verwaltung des dfci-Profils mit Windows Autopilot sind vier grundlegende Schritte erforderlich:

1. Erstellen eines Autopilot-Profils
2. Erstellen eines Seitenprofils für den Registrierungsstatus
3. Erstellen eines dfci-Profils
4. Zuweisen der profile

Weitere Informationen finden Sie unter [Erstellen der Profile](/intune/configuration/device-firmware-configuration-interface-windows#create-the-profiles) und [Zuweisen der Profile und Neustarten](/intune/configuration/device-firmware-configuration-interface-windows#assign-the-profiles-and-reboot) .

Sie können auch [vorhandene dfci-Einstellungen](/intune/configuration/device-firmware-configuration-interface-windows#update-existing-dfci-settings) auf Geräten ändern, die verwendet werden. Ändern Sie in Ihrem vorhandenen dfci-Profil die Einstellungen, und speichern Sie die Änderungen. Da das Profil bereits zugewiesen ist, werden die neuen dfci-Einstellungen wirksam, wenn das Gerät das nächste Mal neu gestartet wird oder das Gerät neu gestartet wird.

## <a name="oems-that-support-dfci"></a>OEMs, die dfci unterstützen

- [Microsoft Surface](/surface/surface-manage-dfci-guide)

Weitere OEMs sind ausstehend.

## <a name="see-also"></a>Weitere Informationen

[Microsoft dfci-Szenarios](https://microsoft.github.io/mu/dyn/mu_plus/DfciPkg/Docs/Scenarios/DfciScenarios/)<br>
[Windows Autopilot-und Surface-Geräte](/surface/windows-autopilot-and-surface-devices)<br>