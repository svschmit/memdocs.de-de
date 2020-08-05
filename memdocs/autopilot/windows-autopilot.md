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
ms.openlocfilehash: 171070e1560796763f3c3851afe239237098f756
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756491"
---
# <a name="overview-of-windows-autopilot"></a>Übersicht über Windows Autopilot

**Zielgruppe**

-   Windows 10

Bei Windows Autopilot handelt es sich um eine Sammlung von Technologien, die zum Einrichten und vorkonfigurieren neuer Geräte verwendet werden, um Sie für den produktiven Einsatz vorzubereiten. Sie können Windows Autopilot auch zum Zurücksetzen, wieder verwenden und Wiederherstellen von Geräten verwenden. Diese Lösung ermöglicht es einer IT-Abteilung, das oben genannte zu erreichen, ohne dass eine Infrastruktur verwaltet werden muss, die einfach und einfach zu verwalten ist.

Windows Autopilot ist so konzipiert, dass alle Teile des Lebenszyklus von Windows-Geräten für IT-und Endbenutzer von der anfänglichen Bereitstellung bis zum Ende der Lebensdauer vereinfacht werden. Mithilfe von cloudbasierten Diensten können IT-Administratoren die Gesamtkosten für die Bereitstellung, Verwaltung und Außerbetriebnahme von Geräten verringern, indem Sie die Zeit verkürzen, die für diese Prozesse aufgewendet werden muss, sowie die Menge der Infrastruktur, die Sie verwalten müssen, und gleichzeitig die Benutzerfreundlichkeit für alle Arten von Endbenutzern sicherstellen. Sehen Sie sich das folgende Video und Diagramm an:

&nbsp;

> [!video https://www.microsoft.com/videoplayer/embed/RE4C7G9?autoplay=false]

![Übersicht über den Prozess](images/image1.png)

Wenn Sie neue Windows-Geräte anfänglich bereitstellen, nutzt Windows Autopilot die OEM-optimierte Version von Windows 10, die auf dem Gerät vorinstalliert ist. so werden Organisationen daran gewöhnt, benutzerdefinierte Images und Treiber für jedes verwendete Gerätemodell zu verwalten. Anstatt das Gerät neu zu erstellen, können Sie Ihre vorhandene Windows 10-Installation in den Status "geschäftlich bereit" umwandeln, Einstellungen und Richtlinien anwenden, Apps installieren und sogar die verwendete Edition von Windows 10 (z. b. von Windows 10 pro zu Windows 10 Enterprise) ändern, um erweiterte Funktionen zu unterstützen.

Nach der Bereitstellung können Windows 10-Geräte mithilfe von Tools wie Microsoft InTune, Windows Update for Business, Microsoft Endpoint Configuration Manager und anderen ähnlichen Tools verwaltet werden. Windows Autopilot kann auch verwendet werden, um ein Gerät zu verwenden, indem Windows Autopilot Reset verwendet wird, um schnell ein Gerät für einen neuen Benutzer vorzubereiten, oder in Break/Fix-Szenarien, damit ein Gerät schnell wieder in einen Zustand versetzt wird, der für den Betrieb bereit ist.

Windows Autopilot ermöglicht Folgendes:
* Automatisches Hinzufügen von Geräten zu Azure Active Directory (Azure AD) oder Active Directory (über Azure AD Hybrid Join).  Weitere Informationen zu den Unterschieden zwischen diesen beiden joinoptionen finden Sie unter Einführung in die [Geräteverwaltung in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-introduction) .
* Automatisches Registrieren von Geräten bei MDM-Diensten, wie z. b. Microsoft InTune ([*erfordert ein Azure AD Premium Abonnement für die Konfiguration*](https://techcommunity.microsoft.com/t5/Azure-Active-Directory-Identity/Windows-10-Azure-AD-and-Microsoft-Intune-Automatic-MDM/ba-p/244067)).
* Beschränken Sie die Erstellung des Administrator Kontos.
* Erstellen und automatisches Zuweisen von Geräten zu Konfigurations Gruppen basierend auf dem Profil eines Geräts.
* Anpassen von OOBE-Inhalten, die für die Organisation spezifisch sind.

## <a name="benefits-of-windows-autopilot"></a>Vorteile von Windows Autopilot

Normalerweise haben IT-Experten viel Zeit damit verbracht, Images zu entwickeln und anzupassen, die später auf Geräten bereitgestellt werden. Windows Autopilot führt einen neuen Ansatz ein.

Aus Sicht des Benutzers werden nur einige einfache Vorgänge benötigt, damit das Gerät einsatzbereit ist.

Aus der Perspektive von IT-Experten besteht die einzige vom Endbenutzer benötigte Interaktion darin, eine Verbindung mit einem Netzwerk herzustellen und deren Anmelde Informationen zu überprüfen. Alles, was darüber hinausgeht, ist automatisiert.

## <a name="requirements"></a>Requirements (Anforderungen)

Eine [unterstützte Version](https://docs.microsoft.com/windows/release-information/) des halbjährlichen Kanals von Windows 10 ist erforderlich, um Windows Autopilot zu verwenden. Windows 10 Enterprise LTSC 2019 wird ebenfalls unterstützt. Ausführliche Informationen zu Software-, Konfigurations-, Netzwerk-und Lizenzierungsanforderungen finden Sie unter [Windows Autopilot Requirements](windows-autopilot-requirements.md) .

## <a name="related-topics"></a>Zugehörige Themen

[Registrieren von Windows-Geräten in InTune mithilfe von Windows Autopilot](https://docs.microsoft.com/intune/enrollment-autopilot)<br>
[Windows Autopilot-Szenarios und-Funktionen](windows-autopilot-scenarios.md)
