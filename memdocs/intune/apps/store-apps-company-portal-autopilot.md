---
title: Hinzufügen und Zuweisen der Unternehmensportal-App für Windows 10 auf vom Autopilot bereitgestellten Geräten
titleSuffix: Microsoft Intune
description: In diesem Artikel erfahren Sie, wie Sie die Unternehmensportal-App für Windows 10 auf vom Autopilot bereitgestellten Geräten hinzufügen und zuweisen.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/17/2020
ms.topic: how-to
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
ms.openlocfilehash: 4d45d73f9c10c9bf7562def73b005c0dd63c7613
ms.sourcegitcommit: 91519f811b58a3e9fd116a4c28e39341ad8af11a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/18/2020
ms.locfileid: "88559520"
---
# <a name="add-and-assign-the-windows-10-company-portal-app-for-autopilot-provisioned-devices"></a>Hinzufügen und Zuweisen der Unternehmensportal-App für Windows 10 auf vom Autopilot bereitgestellten Geräten

Ihre Benutzer können die Unternehmensportal-App verwenden, um Geräte zu verwalten und Apps zu installieren. Sie können die Unternehmensportal-App für Windows 10 direkt in Intune zuweisen. 

## <a name="prerequisites"></a>Voraussetzungen

Auf vom Autopilot bereitgestellten Geräten mit Windows 10 sollten Sie Ihr Microsoft Store für Unternehmen-Konto mit Intune verknüpfen. Weitere Informationen finden Sie unter [Verwalten von VPP-Apps (Apple Volume Purchase Program) aus Microsoft Store für Unternehmen mit Microsoft Intune](windows-store-for-business.md).

Mithilfe der folgenden Schritte können Sie die App **Unternehmensportal (offline)** installieren. Die Unternehmensportal-App wird im Gerätekontext installiert, wenn sie der Autopilot-Gruppe zugewiesen ist, und wird auf dem Gerät installiert, bevor sich der Benutzer anmeldet.

## <a name="configure-the-store-settings-to-show-the-offline-app"></a>Konfigurieren der Storeeinstellungen zum Anzeigen der Offline-App

1. Melden Sie sich beim [Microsoft Store für Unternehmen](https://www.microsoft.com/business-store) mit Ihrem Administratorkonto an.
2. Klicken Sie auf die Registerkarte **Verwalten** am oberen Rand des Fensters.
3. Klicken Sie im linken Bereich auf **Settings** (Einstellungen).
4. Legen Sie unter **Shopping experience** (Einkaufserlebnis) die Option **Show offline apps** (Offline-Apps anzeigen) auf **On** (Aktiv) fest.  
   Dadurch werden die lizenzierten Offline-Apps angezeigt.

## <a name="get-the-offline-company-portal-app-from-the-store"></a>Abrufen der Offline-Unternehmensportal-App im Store

1. Suchen Sie die **Unternehmensportal**-App, und wählen Sie diese aus.
2. Legen Sie den **Lizenztyp** auf **Offline** fest.
3. Klicken Sie auf **App nutzen**, um die Offline-Unternehmensportal-App Ihrem Inventar hinzuzufügen.
   Damit die App in Intune aufgelistet wird, müssen Sie entweder warten, bis der Synchronisierungszeitplan abgeschlossen ist, oder eine manuelle Synchronisierung im Microsoft Endpoint Manager Admin Center durchführen.

## <a name="manually-sync-company-portal-app-with-intune"></a>Manuelles Synchronisieren der Unternehmensportal-App mit Intune

1. Melden Sie sich im  [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) ( ) mit Ihrem Administratorkonto an.
2. Wählen Sie **Mandantenverwaltung** > **Connectors und Token** > **Microsoft Store für Unternehmen** aus.
3. Klicken Sie auf **Aktivieren**.
4. Klicken Sie auf den Link zur Registrierung für den Microsoft Store für Unternehmen, falls Sie dies noch nicht getan haben, und weisen Sie Ihr Konto wie oben beschrieben zu.
5. Wählen Sie in der Dropdownliste **Sprache** die Sprache aus, in der Apps aus dem Microsoft Store für Unternehmen im Azure-Portal angezeigt werden sollen. Die Installation der Apps erfolgt unabhängig von der Anzeigesprache in der Sprache des Endbenutzers, sofern verfügbar.
6. Klicken Sie auf **Synchronisieren**, um die im Microsoft Store erworbenen Apps in Intune abzurufen.

## <a name="assign-the-company-portal-app"></a>Verknüpfen der Unternehmensportal-App

1. Melden Sie sich im  [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) ( ) mit Ihrem Administratorkonto an.
2. Wählen Sie **Apps** > **Windows**aus.
3. Wählen Sie in der Liste der Windows-Apps **Unternehmensportal (offline)** aus.
4. [Weisen](apps-deploy.md) Sie den Autopilot-Gerätegruppen die Unternehmensportal-App als erforderliche App zu.

## <a name="next-steps"></a>Nächste Schritte

- Weitere Informationen zum Zuweisen von Apps finden Sie unter [Zuweisen von Apps zu Gruppen mit Microsoft Intune](apps-deploy.md).

