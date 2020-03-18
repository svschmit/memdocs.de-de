---
title: Zuweisen einer Rolle an einen Intune-Benutzer
description: Erfahren Sie, wie Sie einem Benutzer in Microsoft Intune eine integrierte oder benutzerdefinierte Rolle zuweisen.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 03/26/2019
ms.topic: conceptual
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
ms.openlocfilehash: e4ea84b0b378030a02c73da20b4a59d0b65ca288
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79363147"
---
# <a name="assign-a-role-to-an-intune-user"></a>Zuweisen einer Rolle an einen Intune-Benutzer

Sie können einem Intune-Benutzer eine [integrierte](role-based-access-control.md#built-in-roles) oder [benutzerdefinierte](create-custom-role.md) Rolle zuweisen.

Für das Erstellen, Bearbeiten oder Zuweisen von Rollen muss das Konto in Azure AD über eine der folgenden Berechtigungen verfügen:
- **Globaler Administrator**
- **Intune-Dienstadministrator**

1. Navigieren Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) zu **Mandantenverwaltung** > **Rollen** > **Alle Rollen**.

2. Klicken Sie auf dem Blatt **Intune-Rollen – Alle Rollen** auf die integrierte Rolle, die Sie zuweisen möchten, und dann auf **Zuweisungen** > **Zuweisen**.

5. Geben Sie auf der Seite **Grundlagen** einen **Zuweisungsnamen** und optional eine **Zuweisungsbeschreibung** ein, und klicken Sie dann auf **Weiter**.

6. Wählen Sie auf der Seite **Admin Groups** (Administratorgruppen) die Gruppe aus, die den Benutzer enthält, dem Sie die Berechtigungen erteilen möchten. Klicken Sie auf **Weiter**.

7. Wählen Sie auf der Seite **Bereich (Gruppen)** eine Gruppe aus, die die Benutzer/Geräte enthält, die das oben ausgewählte Mitglied verwalten können soll. Wählen Sie **Weiter** aus.

8. Wählen Sie auf der Seite **Bereich (Markierungen)** die Markierungen aus, bei denen diese Rollenzuweisung angewendet wird. Wählen Sie **Weiter** aus.

9. Klicken Sie, wenn Sie fertig sind, auf der Seite **Überprüfen + erstellen** auf **Erstellen**. Die neue Zuweisung wird in der Liste der Zuweisungen angezeigt.

## <a name="next-steps"></a>Nächste Schritte
- [Erfahren Sie mehr über die rollenbasierte Zugriffssteuerung in Intune](role-based-access-control.md)
- [Erstellen einer benutzerdefinierten Rolle](create-custom-role.md)


