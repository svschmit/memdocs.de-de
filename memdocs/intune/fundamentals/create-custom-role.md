---
title: Erstellen einer benutzerdefinierten Rolle in Intune
description: Erfahren Sie, wie Sie eine benutzerdefinierte Rolle in Microsoft Intune erstellen.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/26/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: pjain
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 51c8ce62d27efa72b6c974f10364e33fb7e6da76
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988018"
---
# <a name="create-a-custom-role-in-intune"></a>Erstellen einer benutzerdefinierten Rolle in Intune

Sie können eine benutzerdefinierte Intune-Rolle erstellen, die alle für einen bestimmten Aufgabenbereich erforderlichen Berechtigungen enthält. Wenn beispielsweise eine IT-Abteilungsgruppe Anwendungen, Richtlinien und Konfigurationsprofile verwaltet, können Sie alle diese Berechtigungen gemeinsam einer benutzerdefinierten Rolle hinzufügen. Nachdem Sie eine benutzerdefinierte Rolle erstellt haben, können Sie sie allen Benutzern [zuweisen](assign-role.md), die diese Berechtigungen benötigen.

Für das Erstellen, Bearbeiten oder Zuweisen von Rollen muss das Konto in Azure AD über eine der folgenden Berechtigungen verfügen:
- **Globaler Administrator**
- **Intune-Dienstadministrator**

## <a name="to-create-a-custom-role"></a>So erstellen Sie eine benutzerdefinierte Rolle

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Mandantenverwaltung** > **Rollen** > **Alle Rollen** > **Erstellen**.

2. Geben Sie auf der Seite **Grundeinstellungen** einen Namen und eine Beschreibung für die neue Rolle ein, und klicken Sie dann auf **Weiter**.

3. Klicken Sie auf der Seite **Berechtigungen** auf die Berechtigungen, die Sie mit dieser Rolle verwenden möchten.

4. Wählen Sie auf der Seite **Bereich (Markierungen)** die Tags für diese Rolle aus. Wenn diese Rolle einem Benutzer zugewiesen wird, kann dieser Benutzer auf Ressourcen zugreifen, die ebenfalls über diese Tags verfügen. Wählen Sie **Weiter** aus.

5. Klicken Sie, wenn Sie fertig sind, auf der Seite **Bewerten + erstellen** auf **Erstellen**. Die neue Rolle wird in der Liste auf dem Blatt **Intune-Rollen – Alle Rollen** angezeigt.

## <a name="copy-a-role"></a>Kopieren einer Rolle

Sie können auch eine vorhandene Rolle kopieren.

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Mandantenverwaltung** > **Rollen** > **Alle Rollen**, klicken Sie auf das Kästchen neben einer Rolle in der Liste und dann auf **Duplizieren**.

2. Geben Sie auf der Seite **Grundeinstellungen** einen Namen ein. Stellen Sie sicher, dass Sie einen eindeutigen Namen verwenden.

3. Alle Berechtigungen und Bereichstags der ursprünglichen Rolle werden bereits ausgewählt. Anschließend können Sie **Name**, **Beschreibung** **Berechtigungen** und **Scope (Tags)** (Bereich (Tags)) der duplizierten Rolle ändern.

4. Nachdem Sie alle gewünschten Änderungen vorgenommen haben, klicken Sie auf **Weiter**, um auf die Seite **Bewerten + erstellen** weitergeleitet zu werden. Wählen Sie **Erstellen** aus. 

## <a name="next-steps"></a>Nächste Schritte
- [Zuweisen einer Rolle an einen Benutzer](assign-role.md)
- [Erfahren Sie mehr über die rollenbasierte Zugriffssteuerung in Intune](role-based-access-control.md)


