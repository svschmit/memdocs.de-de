---
title: Windows Autopilot-Registrierungs Status (Seite)
ms.reviewer: ''
manager: laurawi
description: Bietet einen Überblick über die Funktionen der Registrierungs Status Seite, Konfiguration
keywords: Autopilot-Plug-and-Forget, Windows 10
ms.technology: windows
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
ms.openlocfilehash: a7d368aef0b10fbe78e2c4ca141a39aa4ed6d803
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89606605"
---
# <a name="windows-autopilot-enrollment-status-page"></a>Windows Autopilot-Registrierungs Status (Seite)

**Zielgruppe**

-  Windows 10, Version 1803 und höher 

Wenn ein Benutzer sich zum ersten Mal bei einem Gerät anmeldet, wird auf der Seite Anmeldungs Status (ESP) der Konfigurations Status des Geräts angezeigt. Das ESP stellt außerdem sicher, dass sich das Gerät im erwarteten Zustand befindet, bevor der Benutzer zum ersten Mal auf den Desktop zugreifen kann.

ESP verfolgt die Installation von Anwendungen, Sicherheitsrichtlinien, Zertifikaten und Netzwerkverbindungen. Ein Administrator kann ESP-Profile für einen lizenzierten InTune-Benutzer bereitstellen und bestimmte Einstellungen im ESP-Profil konfigurieren. Einige dieser Einstellungen lauten:
- Erzwingen der Installation von angegebenen Anwendungen.
- Ermöglicht Benutzern das Erfassen von Problem Behandlungsprotokollen.
- Angeben, wie ein Benutzer vorgehen kann, wenn die Geräteeinrichtung fehlschlägt.

Weitere Informationen finden Sie unter Einrichten der Seite "Registrierungs [Status" in InTune](/intune/windows-enrollment-status).  
 
![Seite zum Registrierungsstatus](images/enrollment-status-page.png)
 

## <a name="more-information"></a>Weitere Informationen

Weitere Informationen zum Konfigurieren der Seite Anmeldungs Status finden Sie in der [Microsoft InTune-Dokumentation](/intune/windows-enrollment-status).<br>
Ausführliche Informationen zur zugrunde liegenden Implementierung finden Sie [in den firstsyncstatus-Details in der dmclient-CSP-Dokumentation](/windows/client-management/mdm/dmclient-csp).<br>
Weitere Informationen zum Blockieren der App-Installation:
- [Blockieren der App-Installation mithilfe der Seite](/archive/blogs/mniehaus/blocking-for-app-installation-using-enrollment-status-page)"Registrierungs Status".
- [Support Tipp: die Office C2R-Installation wird jetzt bei ESP nachverfolgt](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Office-C2R-installation-is-now-tracked-during-ESP/ba-p/295514).
