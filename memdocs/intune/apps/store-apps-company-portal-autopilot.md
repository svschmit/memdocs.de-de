---
title: Hinzufügen und Zuweisen der Unternehmensportal-App für Windows 10 auf vom Autopilot bereitgestellten Geräten
titleSuffix: Microsoft Intune
description: In diesem Artikel erfahren Sie, wie Sie die Unternehmensportal-App für Windows 10 auf vom Autopilot bereitgestellten Geräten hinzufügen und zuweisen.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/21/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ec131df32e06c1c43b8904dde732b4e6a17a91aa
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79334196"
---
# <a name="add-and-assign-the-windows-10-company-portal-app-for-autopilot-provisioned-devices"></a>Hinzufügen und Zuweisen der Unternehmensportal-App für Windows 10 auf vom Autopilot bereitgestellten Geräten

Ihre Benutzer können die Unternehmensportal-App verwenden, um Geräte zu verwalten und Apps zu installieren. Sie können die Unternehmensportal-App für Windows 10 direkt in Intune zuweisen. 

## <a name="prerequisites"></a>Voraussetzungen

Auf vom Autopilot bereitgestellten Geräten mit Windows 10 sollten Sie Ihr Microsoft Store für Unternehmen-Konto mit Intune verknüpfen. Weitere Informationen finden Sie unter [Verwalten von VPP-Apps (Apple Volume Purchase Program) aus Microsoft Store für Unternehmen mit Microsoft Intune](windows-store-for-business.md).

Die Unternehmensportal-App (Offline) kann über die folgenden Schritte installiert werden. Die Unternehmensportal-App wird im Gerätekontext installiert, wenn sie der Autopilot-Gruppe zugewiesen ist, und wird auf dem Gerät installiert, bevor sich der Benutzer anmeldet. 

## <a name="configure-settings-to-show-offline-app"></a>Konfigurieren der Einstellungen zum Anzeigen von Offline-Apps

1. Melden Sie sich beim [Microsoft Store für Unternehmen](https://www.microsoft.com/business-store) mit Ihrem Administratorkonto an.
2. Klicken Sie auf die Registerkarte **Verwalten** am oberen Rand des Fensters.
3. Klicken Sie im linken Bereich auf **Settings** (Einstellungen).
4. Legen Sie unter **Shopping experience** (Einkaufserlebnis) die Option **Show offline apps** (Offline-Apps anzeigen) auf **On** (Aktiv) fest.  
    Dadurch werden die lizenzierten Offline-Apps angezeigt.

## <a name="get-the-offline-company-portal-app"></a>Herunterladen der Offline-Unternehmensportal-App

1. Suchen Sie die **Unternehmensportal**-App, und wählen Sie diese aus.
2. Legen Sie den **Lizenztyp** auf **Offline** fest.
3. Klicken Sie auf **App nutzen**, um die Offline-Unternehmensportal-App Ihrem Inventar hinzuzufügen.

## <a name="assign-the-company-portal-app"></a>Verknüpfen der Unternehmensportal-App

1. Melden Sie sich im  [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) ( ) mit Ihrem Administratorkonto an. 
2. Klicken Sie rechts auf die Registerkarte  **Apps** .
3. Wählen Sie unter  **Nach Plattform** die Option **Windows** aus.
4. Klicken Sie auf  **Unternehmensportal (Offline)** .
5. Sie müssen entweder warten, bis der Synchronisierungszeitplan abgeschlossen ist, oder eine manuelle Synchronisierung im Microsoft Endpoint Manager Admin Center durchführen.
6. Weisen Sie den Autopilot-Gerätegruppen die Unternehmensportal-App als erforderliche App zu.

## <a name="next-steps"></a>Nächste Schritte

- Weitere Informationen zum Zuweisen von Apps finden Sie unter [Zuweisen von Apps zu Gruppen mit Microsoft Intune](apps-deploy.md).

