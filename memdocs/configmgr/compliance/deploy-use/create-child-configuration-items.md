---
title: Erstellen von untergeordneten Konfigurationselementen
titleSuffix: Configuration Manager
description: Erstellen von untergeordneten Konfigurationselementen in Configuration Manager
ms.date: 05/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 113984fa-6150-41a1-89ed-d2a83b979732
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 319f673200244d4451b957dcb778ce378f9569fa
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240319"
---
# <a name="how-to-create-child-configuration-items-in-configuration-manager"></a>Erstellen von untergeordneten Konfigurationselementen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Untergeordnete Konfigurationselemente in Configuration Manager sind Kopien von Konfigurationselementen, die eine Beziehung zum ursprünglichen Konfigurationselement beibehalten: Sie erben die ursprüngliche Konfiguration vom übergeordneten Konfigurationselement.  

Wenn Sie in der Configuration Manager-Konsole die Eigenschaften eines untergeordneten Konfigurationselements anzeigen, können Sie die geerbten Objekte und Einstellungen mit den entsprechenden Überprüfungskriterien nicht bearbeiten. Sie können jedoch dem untergeordneten Konfigurationselement zusätzliche Überprüfungskriterien hinzufügen und diese anschließend bearbeiten. Außerdem können Sie dem untergeordneten Konfigurationselement auch neue Objekte und Einstellungen hinzufügen.
Ein Beispiel zum Erstellen und Bearbeiten eines untergeordneten Konfigurationselements ist, das ursprüngliche Konfigurationselement für Ihre Unternehmensanforderungen zu optimieren.  

> [!NOTE]  
>  Sie können untergeordnete Konfigurationselemente nur von Konfigurationselementen des Typs **Windows-Desktops und -Server (benutzerdefiniert)** erstellen.  

## <a name="to-create-a-child-configuration-item"></a>So erstellen Sie ein untergeordnetes Konfigurationselement  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** > **Kompatibilitätseinstellungen** > **Konfigurationselemente**.  

3.  Wählen Sie in der Liste **Konfigurationselemente** das Konfigurationselement aus, für das Sie ein untergeordnetes Konfigurationselement erstellen möchten, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Konfigurationselement** auf **Untergeordnetes Konfigurationselement erstellen**.  

4.  Auf der Seite **Allgemein** des **Assistenten zum Erstellen untergeordneter Konfigurationselemente**können Sie eine spezifische Revision des übergeordneten Konfigurationselements auswählen, aus der das untergeordnete Konfigurationselement erstellt werden soll. Andere Schritte des Assistenten sind identisch mit denen zum Erstellen eines Standardkonfigurationselements. Weitere Informationen finden Sie unter [Erstellen benutzerdefinierter Konfigurationselemente für Windows-Desktop- und -Servercomputer](../../compliance/deploy-use/create-custom-configuration-items-for-windows-desktop-and-server-computers-managed-with-the-client.md).  

5.  Schließen Sie den Assistenten ab. Das neue untergeordnete Konfigurationselement wird in der Liste **Konfigurationselemente** angezeigt.  
