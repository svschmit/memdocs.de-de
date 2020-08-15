---
title: Übersicht über Windows Autopilot
description: Bei Windows Autopilot handelt es sich um eine Sammlung von Technologien, die zum Einrichten und vorkonfigurieren neuer Geräte verwendet werden, um Sie für den produktiven Einsatz vorzubereiten.
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
ms.openlocfilehash: da15ea9ceae46c9c54858a6be0f724c5d67d22ce
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252173"
---
# <a name="overview-of-windows-autopilot"></a>Übersicht über Windows Autopilot

**Zielgruppe**

-  Windows 10

Bei Windows Autopilot handelt es sich um eine Sammlung von Technologien, die zum Einrichten und vorkonfigurieren neuer Geräte verwendet werden, um Sie für den produktiven Einsatz vorzubereiten. Sie können Windows Autopilot auch zum Zurücksetzen, wieder verwenden und Wiederherstellen von Geräten verwenden. Diese Lösung ermöglicht es einer IT-Abteilung, das oben genannte zu erreichen, ohne dass eine Infrastruktur verwaltet werden muss, die einfach und einfach zu verwalten ist.

Windows Autopilot vereinfacht den Lebenszyklus von Windows-Geräten für IT-und Endbenutzer von der ersten Bereitstellung bis zum Ende der Lebensdauer. Mit cloudbasierten Diensten, Windows Autopilot:
- verringert die Zeit, die für die Bereitstellung, Verwaltung und Außerbetriebnahme von Geräten benötigt wird.
- verringert die Infrastruktur, die zum Warten der Geräte erforderlich ist.
- maximiert die Benutzerfreundlichkeit für alle Arten von Endbenutzern.

Sehen Sie sich das folgende Video und Diagramm an:

&nbsp;

> [!video https://www.microsoft.com/videoplayer/embed/RE4C7G9?autoplay=false]

![Übersicht über den Prozess](images/image1.png)

Bei der anfänglichen Bereitstellung neuer Windows-Geräte verwendet Windows Autopilot die OEM-optimierte Version von Windows 10. Diese Version ist auf dem Gerät vorinstalliert, sodass Sie keine benutzerdefinierten Images und Treiber für jedes Gerätemodell verwalten müssen. Anstatt das Gerät neu zu erstellen, kann die vorhandene Windows 10-Installation in einen "Business-Ready"-Zustand transformiert werden, in dem Folgendes möglich ist:
- Anwenden von Einstellungen und Richtlinien
- Installieren von apps
- Ändern Sie die verwendete Edition von Windows 10 (z. b. von Windows 10 pro zu Windows 10 Enterprise), um erweiterte Funktionen zu unterstützen.

Nach der Bereitstellung können Sie Windows 10-Geräte wie folgt verwalten:
- Microsoft Intune
- Windows Update for Business
- Microsoft Endpoint Configuration Manager
- oder andere ähnliche Tools.

Mit Windows Autopilot können Sie schnell ein Gerät für einen neuen Benutzer mit Windows Autopilot Reset vorbereiten. Sie können auch in Break/Fix-Szenarien zurücksetzen verwenden, um ein Gerät schnell wieder in den Status "bereit" zu bringen.

Windows Autopilot ermöglicht Folgendes:
* Automatisches Hinzufügen von Geräten zu Azure Active Directory (Azure AD) oder Active Directory (über Azure AD Hybrid Join). Weitere Informationen zu den Unterschieden zwischen diesen beiden joinoptionen finden Sie unter Einführung in die [Geräteverwaltung in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-introduction).
* Automatisches Registrieren von Geräten bei MDM-Diensten, wie z. b. Microsoft InTune ([*erfordert ein Azure AD Premium Abonnement für die Konfiguration*](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Windows-10-Azure-AD-and-Microsoft-Intune-Automatic-MDM/ba-p/244067)).
* Beschränken Sie die Erstellung des Administrator Kontos.
* Erstellen und automatisches Zuweisen von Geräten zu Konfigurations Gruppen basierend auf dem Profil eines Geräts.
* Anpassen von OOBE-Inhalten, die für die Organisation spezifisch sind.

## <a name="benefits-of-windows-autopilot"></a>Vorteile von Windows Autopilot

In der Vergangenheit haben IT-Experten beträchtliche Zeit damit verbracht, Images zu entwickeln und anzupassen, die später auf Geräten bereitgestellt werden. Windows Autopilot führt einen neuen Ansatz ein.

Aus Sicht des Benutzers werden nur einige einfache Vorgänge benötigt, damit das Gerät einsatzbereit ist.

Aus der Perspektive von IT-Experten besteht die einzige vom Endbenutzer benötigte Interaktion darin, eine Verbindung mit einem Netzwerk herzustellen und deren Anmelde Informationen zu überprüfen. Alles, was darüber hinausgeht, ist automatisiert.

## <a name="requirements"></a>Anforderungen

Eine [unterstützte Version](https://docs.microsoft.com/windows/release-information/) des halbjährlichen Kanals von Windows 10 ist erforderlich, um Windows Autopilot zu verwenden. Windows 10 Enterprise LTSC 2019 wird ebenfalls unterstützt. Weitere Informationen finden Sie unter [Windows Autopilot Software](software-requirements.md), [Networking](networking-requirements.md), [Configuration](configuration-requirements.md)und [Licensing](licensing-requirements.md) Requirements.

## <a name="related-topics"></a>Zugehörige Themen

[Registrieren von Windows-Geräten in InTune mithilfe von Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot)<br>
[Windows Autopilot-Szenarios und-Funktionen](windows-autopilot-scenarios.md)
