---
title: Windows Autopilot-Registrierungs Status (Seite)
ms.reviewer: ''
manager: laurawi
description: Bietet einen Überblick über die Funktionen der Registrierungs Status Seite, Konfiguration
keywords: Autopilot-Plug-and-Forget, Windows 10
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
ms.openlocfilehash: 129023d73f7a0ed458c351e8b2bcfd482a201c23
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756653"
---
# <a name="windows-autopilot-enrollment-status-page"></a>Windows Autopilot-Registrierungs Status (Seite)

**Zielgruppe**

-   Windows 10, Version 1803 und höher 

Auf der Seite Anmeldungs Status (ESP) wird der Status des Vorgangs zur gesamten Gerätekonfiguration angezeigt, wenn ein MDM-verwalteter Benutzer sich zum ersten Mal bei einem Gerät anmeldet.  Mit dem ESP können Benutzer den Fortschritt der Geräte Bereitstellung verstehen und sicherstellen, dass das Gerät den gewünschten Zustand der Organisation erreicht hat, bevor der Benutzer zum ersten Mal auf den Desktop zugreifen kann.

Mit dem ESP werden die Installation von Anwendungen, Sicherheitsrichtlinien, Zertifikaten und Netzwerkverbindungen nachverfolgt.  Mit InTune kann ein Administrator ESP-Profile für einen lizenzierten InTune-Benutzer bereitstellen und bestimmte Einstellungen im ESP-Profil konfigurieren. Dies sind einige dieser Einstellungen: Erzwingen der Installation von angegebenen Anwendungen, zulassen der Erfassung von Problem Behandlungsprotokollen durch Benutzer, angeben der Aktionen, die ein Benutzer ausführen kann, wenn die Geräte Einrichtung fehlschlägt.  Weitere Informationen finden Sie unter Einrichten der Seite "Registrierungs [Status" in InTune](https://docs.microsoft.com/intune/windows-enrollment-status).   
 
 ![Seite zum Registrierungsstatus](images/enrollment-status-page.png)
 

## <a name="more-information"></a>Weitere Informationen

Weitere Informationen zum Konfigurieren der Seite Anmeldungs Status finden Sie in der [Microsoft InTune-Dokumentation](https://docs.microsoft.com/intune/windows-enrollment-status).<br>
Ausführliche Informationen zur zugrunde liegenden Implementierung finden Sie [in den firstsyncstatus-Details in der dmclient-CSP-Dokumentation](https://docs.microsoft.com/windows/client-management/mdm/dmclient-csp).<br>
Weitere Informationen zum Blockieren der App-Installation:
- [Blockieren der App-Installation mithilfe der Seite](https://blogs.technet.microsoft.com/mniehaus/2018/12/06/blocking-for-app-installation-using-enrollment-status-page/)"Registrierungs Status".
- [Support Tipp: die Office C2R-Installation wird jetzt bei ESP nachverfolgt](https://techcommunity.microsoft.com/t5/Intune-Customer-Success/Support-Tip-Office-C2R-installation-is-now-tracked-during-ESP/ba-p/295514).
