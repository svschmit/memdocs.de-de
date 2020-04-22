---
title: Freigeben von Anwendungen im Softwarecenter
titleSuffix: Configuration Manager
description: Teilen Sie einen Link zu einer Anwendung im Software Center in Configuration Manager.
ms.date: 07/31/2017
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: be2e930e3f59bc5a4d7db9e27ce2f875814fd358
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689238"
---
# <a name="share-an-application-from-software-center"></a>Teilen einer Anwendung aus dem Software Center

*Gilt für: Configuration Manager (Current Branch)* <!-- 1706 -->

Sie können einen Hyperlink zu einer Anwendung in Software Center kopieren, indem Sie in der Ansicht „Anwendungsdetails“ auf ![Freigeben](media/share15.png) **Freigeben** klicken. Sie können nur Hyperlinks für Anwendungen freigeben. Wenn eine Anwendung nicht verfügbar ist, führt der Hyperlink zu einem Fenster mit einer Meldung, in der darauf hingewiesen wird.

1. Klicken Sie auf **Anwendungen**, und wählen Sie dann die Anwendung aus.
2. Klicken Sie auf die Schaltfläche ![Freigeben](media/share15.png) **Freigeben**.
3. Klicken Sie im Fenster auf **Kopieren**.
4. Fügen Sie die URL in eine E-Mail ein, um die Anwendung freizugeben.  

> [!TIP]  
>  Wenn Sie in einer über Outlook gesendeten E-Mail einen Link erstellen möchten, drücken Sie **STRG** + **K**, und fügen Sie die URL ein.  
>  
> Standardmäßig zeigt Outlook eine Sicherheitswarnung für das Softwarecenter-Protokoll an, wenn der Empfänger auf den Link klickt. Vermeiden Sie dies in Ihrer Umgebung, indem Sie einen vertrauenswürdigen Protokollschlüssel zur Registrierung hinzufügen. Beispiel: `HKCU\Software\Policies\Microsoft\Office\16.0\Common\Security\Trusted Protocols\All Applications\softwarecenter:`  
