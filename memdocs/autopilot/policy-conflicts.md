---
title: Konflikte bei Windows Autopilot-Richtlinien
ms.reviewer: ''
manager: laurawi
description: Informieren Sie sich über Richtlinien Konflikte, die während der Bereitstellung von Windows Autopilot auftreten können.
keywords: MDM, Setup, Windows, Windows 10, OOBE, Manage, Bereitstellung, Autopilot, ZTD, Zero-Touchscreen, Partner, msfb, InTune
ms.technology: windows
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: medium
ms.sitesec: library
ms.pagetype: deploy
audience: itpro
author: mtniehaus
ms.author: mniehaus
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: 1f839f128dc869f7c9a4619237de0c33a21d66e1
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606583"
---
# <a name="windows-autopilot---policy-conflicts"></a>Windows Autopilot-Richtlinien Konflikte

**Zielgruppe**

- Windows 10

Für Windows 10 stehen eine beträchtliche Anzahl von Richtlinien Einstellungen zur Verfügung, einschließlich:
- Native MDM-Richtlinien
- Gruppenrichtlinien Einstellungen (ADMX-gestützt)

Einige Richtlinien Einstellungen können in einigen Windows Autopilot-Szenarien Probleme verursachen. Diese Probleme können auftreten, wenn die Richtlinien das Verhalten von Windows 10 ändern. Wenn Sie eines dieser Probleme feststellen, entfernen Sie die betreffende Richtlinie, um das Problem zu beheben.

<table>
<th>Policy<th>Weitere Informationen

<tr><td width="50%">Geräte Einschränkung/Kenn <a href="https://docs.microsoft.com/windows/client-management/mdm/devicelock-csp">Wort Richtlinie</a></td>
<td>Die Out-of-Box-Umgebung (OOBE) oder die Benutzer Desktop-Authentifizierung kann fehlschlagen, wenn ein Gerät auf der Seite Geräte Registrierungs Status (ESP) neu gestartet wird. Dieser Fehler kann auftreten, wenn bestimmte <a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock">DeviceLock-Richtlinien</a> auf ein Gerät angewendet werden. Diese Richtlinien können Folgendes umfassen:<ul><li>Minimale Kenn Wort Länge und Kenn Wort Komplexität</li><li>Alle ähnlichen Gruppenrichtlinien Einstellungen (einschließlich aller aktivierenden AutoLogon)</li></ul>
Diese mögliche Fehlermeldung gilt besonders für Kiosk Szenarien, in denen Kenn Wörter automatisch generiert werden.</td>

<tr><td width="50%">Windows 10-Sicherheitsbaseline/Eingabe Aufforderungs <a href="/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions">Verhalten für Administrator</a> Rechte
<br>Windows 10-Sicherheitsbaseline/ <a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions">Administrator Genehmigungs Modus für Administratoren erforderlich</a></td>
<td>Wenn Sie die Einstellungen für die Benutzerkontensteuerung (User Account Control, UAC) auf der Seite OOBE mithilfe der Seite Geräte Registrierungs Status (ESP) ändern, werden weitere Aufforderungen angezeigt. Größere Eingabe Aufforderungen sind wahrscheinlicher, wenn das Gerät neu gestartet wird, nachdem Richtlinien angewendet wurden. Um dieses Problem zu umgehen, können die Richtlinien für Benutzer anstelle von Geräten bestimmt werden, damit Sie später im Prozess angewendet werden.</td>

<tr><td width="50%">Geräte Einschränkungen/Cloud und Storage/ <a href="https://docs.microsoft.com/mem/intune/configuration/device-restrictions-windows-10#cloud-and-storage">Anmelde-Assistent für Microsoft-Konten</a></td>
<td>Wenn diese Richtlinie auf "deaktiviert" festgelegt wird, wird der Microsoft Sign-in Assistant Service (wlidsvc) deaktiviert. Dieser Dienst wird von Windows Autopilot zum Abrufen des Windows Autopilot-Profils benötigt.</td>

</table>

## <a name="related-topics"></a>Verwandte Themen

[Problembehandlung bei Windows Autopilot](troubleshooting.md)
