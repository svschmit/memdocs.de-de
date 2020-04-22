---
title: Automatisches Kategorisieren von Geräten in Sammlungen
titleSuffix: Configuration Manager
description: Kategorisieren Sie Geräte automatisch in Sammlungen.
ms.date: 04/23/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 98b038b4-1a13-4228-bdb8-a12194e32b0e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: f91f150a095838484c516226da0d3e44e1f5b331
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695268"
---
# <a name="automatically-categorize-devices-into-collections"></a>Automatisches Kategorisieren von Geräten in Sammlungen

*Gilt für: Configuration Manager (Current Branch)*

Sie können Gerätekategorien erstellen, mit denen Geräte automatisch in Gerätesammlungen platziert werden, wenn Sie Configuration Manager mit Microsoft Intune verwenden. Benutzer müssen eine Gerätekategorie auswählen, wenn sie ein Gerät in Intune registrieren. Sie können außerdem eine Gerätekategorie in der Configuration Manager-Konsole ändern.

> [!IMPORTANT]
>  Diese Funktion wird vom Microsoft Intune-Release vom **Juni 2016** und später unterstützt. Stellen Sie sicher, dass Sie auf dieses Release aktualisiert haben, bevor Sie die Verfahren ausprobieren.

## <a name="create-device-categories"></a>Gerätekategorien erstellen

1.  Wechseln Sie zu **Bestand und Konformität** > **Übersicht** >  **Gerätesammlungen**.
2.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Gerätesammlungen** die Option **Gerätekategorien verwalten** aus.
3.  Erstellen, bearbeiten oder entfernen Sie Kategorien.

## <a name="associate-a-collection-with-a-device-category"></a>Ordnen Sie eine Sammlung einer Gerätekategorie zu

Wenn Sie eine Sammlung einer Gerätekategorie zuordnen, werden alle Geräte in der Kategorie der Sammlung hinzugefügt. Sie können keine Gerätekategorieregel zu einer integrierten Sammlung wie **Alle Systeme** hinzufügen.

1.  Wählen Sie auf der Registerkarte **Mitgliedschaftsregeln** des Dialogfelds **Eigenschaften** einer Gerätesammlung **Regel hinzufügen** > **Device Category Rule** (Gerätekategorieregel) aus.
2.  Wählen Sie im Dialogfeld **Gerätekategorien auswählen** eine oder mehrere Gerätekategorien aus, die auf allen Geräte in der Sammlung angewendet werden.

## <a name="change-the-category-of-a-device"></a>Ändern der Gerätekategorie

1.  Wählen Sie unter **Bestand und Konformität** > **Übersicht** > **Geräte** ein Gerät in der Liste **Geräte** aus.
2.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Gerät** dann **Kategorie ändern** aus.
3.  Wählen Sie eine Kategorie und anschließend **OK** aus.

## <a name="view-which-category-a-device-belongs-to"></a>Anzeigen der Kategorie eines Geräts

Unter **Bestand und Konformität** > **Übersicht** > **Geräte** wird in der Liste **Geräte** die Kategorie in der Spalte **Gerätekategorie** angezeigt.

Klicken Sie mit der rechten Maustaste auf die Überschrift einer der Spalten in der Liste **Geräte** (wie **Name**), und wählen Sie dann **Gerätekategorie** aus, wenn die Spalte **Gerätekategorie** nicht angezeigt wird.

Wenn Sie ein Gerät zu einer Kategorie zuweisen, und die Kategorie anschließend löschen, zeigt der Bericht **Liste der pro Benutzer in Microsoft Intune registrierten Geräte** eine GUID in der Spalte **Gerätekategorie** statt eines Kategorienamens an.
