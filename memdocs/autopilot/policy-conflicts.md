---
title: Konflikte bei Windows Autopilot-Richtlinien
ms.reviewer: ''
manager: laurawi
description: Informieren Sie sich über bekannte Probleme, die während der Bereitstellung von Windows Autopilot auftreten können.
keywords: MDM, Setup, Windows, Windows 10, OOBE, Manage, Bereitstellung, Autopilot, ZTD, Zero-Touchscreen, Partner, msfb, InTune
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
ms.openlocfilehash: 23c5c9c0fd025279f1c97b6f19673f9e8b527adb
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88907978"
---
# <a name="windows-autopilot---policy-conflicts"></a>Windows Autopilot-Richtlinien Konflikte

**Zielgruppe**

- Windows 10

Für Windows 10 stehen eine beträchtliche Anzahl von Richtlinien Einstellungen zur Verfügung, sowohl als systemeigene MDM-Richtlinien als auch als Einstellungen für Gruppenrichtlinien (ADMX-gestützt). Einige davon können Probleme in bestimmten Windows Autopilot-Szenarien verursachen, weil Sie das Verhalten von Windows 10 ändern. Wenn diese Probleme auftreten, entfernen Sie die betreffende Richtlinie, um das Problem zu beheben.

<table>
<th>Richtlinie<th>Weitere Informationen

<tr><td width="50%">Geräte Einschränkung/Kenn <a href="https://docs.microsoft.com/windows/client-management/mdm/devicelock-csp">Wort Richtlinie</a></td>
<td>Wenn bestimmte <a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-devicelock">DeviceLock-Richtlinien</a>, z. b. minimale Kenn Wort Länge und Kenn Wort Komplexität, oder ähnliche Gruppenrichtlinien Einstellungen (einschließlich der automatischen Deaktivierung) auf ein Gerät angewendet werden und das Gerät auf der Seite Geräte Registrierungs Status (ESP) neu gestartet wird, kann die Out-of-Box-Umgebung (OOBE) oder die Benutzer Desktop-Authentifizierung nicht erwartungsgemäß ausfallen.  Dies gilt insbesondere für Kiosk Szenarios, in denen Kenn Wörter automatisch generiert werden.</td>

<tr><td width="50%">Windows 10-Sicherheitsbaseline/Eingabe Aufforderungs <a href="/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions">Verhalten für Administrator</a> Rechte
<br>Windows 10-Sicherheitsbaseline/ <a href="https://docs.microsoft.com/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions">Administrator Genehmigungs Modus für Administratoren erforderlich</a></td>
<td>Wenn Sie die Einstellungen für die Benutzerkontensteuerung (User Account Control, UAC) während der Verwendung der Seite Geräte Registrierungs Status (ESP) ändern, können zusätzliche UAC-Eingabe Aufforderungen entstehen, insbesondere dann, wenn das Gerät neu gestartet wird, nachdem diese Richtlinien angewendet wurden, sodass Sie wirksam werden können.  Um dieses Problem zu umgehen, können die Richtlinien für Benutzer anstelle von Geräten bestimmt werden, damit Sie später im Prozess angewendet werden.</td>

<tr><td width="50%">Geräte Einschränkungen/Cloud und Storage/ <a href="https://docs.microsoft.com/mem/intune/configuration/device-restrictions-windows-10#cloud-and-storage">Anmelde-Assistent für Microsoft-Konten</a></td>
<td>Wenn diese Richtlinie auf "deaktiviert" festgelegt wird, wird der Microsoft Sign-in Assistant Service (wlidsvc) deaktiviert.  Dieser Dienst wird von Windows Autopilot zum Abrufen des Windows Autopilot-Profils benötigt.</td>

</table>

## <a name="related-topics"></a>Zugehörige Themen

[Problembehandlung bei Windows Autopilot](troubleshooting.md)