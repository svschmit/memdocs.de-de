---
title: Konfigurieren der Hardwareinventur
titleSuffix: Configuration Manager
description: Richten Sie die Hardwareinventur für alle Clients oder für eine Sammlung in Configuration Manager ein.
ms.date: 02/22/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 0e45290e-f8f7-4335-801e-570225d12c2b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ee40a6c58e3d3a4c85eb5cc8cb19c2a834fbfd0e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695448"
---
# <a name="how-to-configure-hardware-inventory-in-configuration-manager"></a>Konfigurieren der Hardwareinventur in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Mithilfe dieses Verfahrens werden die Clientstandardeinstellungen für die Hardwareinventur konfiguriert. Sie gilt für alle Clients in der Hierarchie. Wenn Sie diese Einstellungen nur auf manche Clients anwenden möchten, erstellen Sie eine benutzerdefinierte Geräteclienteinstellung und weisen diese einer Sammlung mit den Geräten zu, auf denen Sie die Hardwareinventur verwenden möchten. Weitere Informationen finden Sie unter [Konfigurieren von Clienteinstellungen](../../../../core/clients/deploy/configure-client-settings.md).  

> [!NOTE]  
>  Wenn ein Clientgerät Hardwareinventureinstellungen von mehreren Clienteinstellungssätzen erhält, werden die Hardwareinventurklassen aus jedem Einstellungssatz zusammengeführt, sobald vom Client eine Hardwareinventur gemeldet wird. Wenn außerdem das Kontrollkästchen für eine Klasse nicht in einer benutzerdefinierten Clienteinstellung mit höherer Priorität aktiviert wird, kann der Client trotzdem eine Inventur der Klasse erstellen. 

Damit eine bestimmte Klasse für die Hardwareinventur auf beinahe allen Systemen deaktiviert werden kann, muss das Kontrollkästchen für diese in den Standardclienteinstellungen deaktiviert sein. Erstellen Sie anschließend eine benutzerdefinierte Clienteinstellung, um die Klasse zu aktivieren und auf den Zielsystemen bereitzustellen.


### <a name="to-configure-hardware-inventory"></a>So konfigurieren Sie die Hardwareinventur  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** > **Clienteinstellungen** > **Clientstandardeinstellungen** aus.  

4.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.  

5.  Wählen Sie im Dialogfeld **Standardeinstellungen** die Option **Hardwareinventur** aus.  

6.  Konfigurieren Sie in der Liste **Geräteeinstellungen** die folgenden Optionen:  

    -   **Hardwareinventur auf Clients aktivieren**: Wählen Sie **Ja** aus.  

    -   **Hardwareinventur-Zeitplan**: Klicken Sie auf **Zeitplan**, um das Intervall anzugeben, in dem Clients eine Hardwareinventur sammeln.  

7.  Konfigurieren Sie andere [Hardwareinventurclient-Einstellungen](../../../../core/clients/deploy/about-client-settings.md#hardware-inventory), die Sie benötigen.  

Die Clientgeräte werden beim nächsten Clientrichtliniendownload mit diesen Einstellungen konfiguriert. Informationen zum Initiieren des Richtlinienabrufs für einen einzelnen Client finden Sie unter [How to manage Clients (Verwalten von Clients)](../../../../core/clients/manage/manage-clients.md).  
