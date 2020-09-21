---
title: Nicht lizenzierte Administratoren in Microsoft Intune
description: Hier erfahren Sie, wie Sie nicht lizenzierten Administratoren die Zugriffsberechtigungen für Intune gewähren.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 01/02/2018
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: a5f479dcad0c293c547edec24f0f835a4fc987e1
ms.sourcegitcommit: cba06c182646cb6dceef304b35230bf728d5133e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/15/2020
ms.locfileid: "90574829"
---
# <a name="unlicensed-admins"></a>Nicht lizenzierte Administratoren

> [!Important]
> Diese Option bedeutet nur, dass ein Administrator für den Zugriff auf Microsoft Endpoint Manager nicht über eine Lizenz verfügen muss. Für die Nutzung anderer Features oder Dienste wie etwa Azure Active Directory Premium ist möglicherweise weiterhin eine Lizenz für den Administrator erforderlich.

Sie können Administratoren ohne Intune-Lizenzen den Zugriff auf Intune/Microsoft Endpoint Manager Admin Center gewähren.

1. Melden Sie sich an, und navigieren Sie zu [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Mandantenverwaltung** > **Rollen** > **Administratorlizenzierung**.
2. Klicken Sie auf **Zugriff für Administratoren ohne Lizenz zulassen** > **Ja**.
    >[!WARNING]
    >Sie können diese Einstellung nicht mehr rückgängig machen, nachdem Sie auf **Ja** geklickt haben.

3. Ab jetzt ist keine Intune-Lizenz für Benutzer erforderlich, die sich bei Microsoft Endpoint Manager Admin Center anmelden. Ihr Zugriffsumfang wird von den zugewiesenen Rollen definiert.

Intune unterstützt bis zu 350 Administratoren ohne Lizenz pro Sicherheitsgruppe und gilt nur für direkte Mitglieder. Wenn diese Anzahl der Administratoren überschritten wird, kann unerwartetes Verhalten auftreten.




