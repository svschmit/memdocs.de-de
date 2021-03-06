---
title: Verhindern von nicht autorisiertem Zugriff auf Unternehmensdaten
titleSuffix: Microsoft Intune
description: Verhindern Sie mithilfe von Microsoft Intune nicht autorisierten Zugriff auf Ihre Unternehmensdaten, wenn diese außerhalb des Unternehmensnetzwerks freigegeben werden.
keywords: Microsoft 365, M365, Azure Information Protection, Datenschutz außerhalb des Netzwerks, Unternehmensdaten
ms.author: dougeby
author: dougeby
manager: dougeby
ms.date: 01/02/2018
ms.topic: archived
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 6a88573a-aa60-455c-858c-74562798246b
ms.reviewer: pchacon
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 24d0ed7b9111e54c4912cf23cd5b52072253c931
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996145"
---
# <a name="prevent-unauthorized-access-to-company-data-using-microsoft-intune"></a>Verhindern von nicht autorisiertem Zugriff auf Unternehmensdaten mit Microsoft Intune

Sie können Microsoft 365-Dokumente und -E-Mails klassifizieren, bezeichnen und schützen, sodass nur autorisierte Benutzer Zugriff auf die Daten haben. Die Einstellungen werden automatisch verwaltet, nachdem IT-Administratoren oder Benutzer die Regeln und Bedingungen festgelegt haben. Alternativ kann das IT-Team empfohlene Einstellungen bereitstellen, nach denen sich Benutzer richten sollen. Administratoren und Benutzer können auch ohne die Unterstützung einer anderen Autorität den Zugriff auf Daten widerrufen, die bereits für Andere freigegeben wurden. Somit kann gesteuert werden, wer geschützte Daten öffnet und aktualisiert, selbst wenn die Daten das Unternehmensnetzwerk verlassen. 

## <a name="before-you-begin"></a>Vorbereitung

Der folgende Maßnahmenplan kann verwendet werden, wenn Sie die folgenden Anforderungen erfüllen:
* Ihr Unternehmen ist für den sicheren Übergang in die Cloud bereit.
* Ihr Unternehmen verwendet Microsoft 365 Exchange Online, SharePoint Online, OneDrive for Business oder Yammer.
* Ihr Unternehmen verfügt über Lizenzen für Microsoft-365, Enterprise Mobility + Security (EMS) oder Azure Information Protection.
* Ihr Unternehmen arbeitet mit Geräten, auf denen Windows 7 Service Pack 1 oder höher ausgeführt wird.
* Ihr Unternehmen verwendet Microsoft 365-Apps mit 2016-Apps oder 2013-Apps, Office Professional Plus 2016, Office Professional Plus 2013 mit Service Pack 1 oder Office Professional Plus 2010.

## <a name="action-plan"></a>Maßnahmenplan

Schließen Sie das [Schnellstarttutorial für Azure Information Protection](/information-protection/get-started/infoprotect-quick-start-tutorial) ab.  

## <a name="what-to-tell-employees-and-students"></a>Informationen für Mitarbeiter und Studenten

Sie können Informationen dazu teilen, [wie und wann Dokumente und E-Mails geschützt werden sollen, die sensible Informationen enthalten](/information-protection/deploy-use/help-users).

## <a name="next-steps"></a>Nächste Schritte

Im Zuge der nächsten Schritte können Sie mehr über die anderen Möglichkeiten erfahren, den Schutz Ihrer Unternehmensdaten zu erhöhen. Dazu zählt Folgendes: 

* Informationen zur Verwendung von Azure Information Protection für iOS-/iPadOS- und Android-Geräte finden Sie [hier](/information-protection/rms-client/mobile-app-faq).
* Informieren Sie sich über die [Microsoft Rights Management-Freigabeanwendung](/previous-versions/msdn10/dn451248(v=msdn.10)) für Mac-Computer.
