---
title: Planen und Konfigurieren von Konformitätseinstellungen
titleSuffix: Configuration Manager
description: Erfahren Sie mehr zu den Voraussetzungen und Konfigurationsaufgaben für die Arbeit mit Konformitätseinstellungen in Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9ea20b01-676a-4cc2-b328-0098a41b202e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 73ccec4ca318b522c0714bc8e5cc89f6c8899edd
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692188"
---
# <a name="plan-for-and-configure-compliance-settings-in-configuration-manager"></a>Planen und Konfigurieren von Kompatibilitätseinstellungen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Bevor Sie beginnen, mit Configuration Manager-Kompatibilitätseinstellungen zu arbeiten, gibt es einige Voraussetzungen, die Sie kennen sollten, und einige Konfigurationsaufgaben, die Sie ausführen müssen.  

## <a name="prerequisites-for-compliance-settings"></a>Voraussetzungen für Konformitätseinstellungen  

|Voraussetzung|Weitere Informationen|  
|------------------|----------------------|  
|Windows Configuration Manager-Clients müssen für die Kompatibilitätsauswertung aktiviert und konfiguriert werden.|Informationen hierzu finden Sie weiter unten.|  
|Wenn Sie Berichte ausführen möchten, müssen Sie die Berichterstellung für Ihren Standort konfigurieren.|[Introduction to reporting (Einführung in die Berichterstellung)](../../core/servers/manage/introduction-to-reporting.md)|  
|Erforderliche Sicherheitsberechtigungen|Die Sicherheitsrolle **Kompatibilitätseinstellungs-Manager** beinhaltet die erforderlichen Berechtigungen, um Kompatibilitätseinstellungen, Konfigurationselemente für Benutzerdaten und -profile sowie Remoteverbindungsprofile verwalten zu können.<br /><br /> [Configure role-based administration (Konfigurieren der rollenbasierten Verwaltung)](../../core/servers/deploy/configure/configure-role-based-administration.md)|  

##  <a name="enable-and-configure-compliance-settings-for-windows-pcs-only"></a>Aktivieren und Konfigurieren von Kompatibilitätseinstellungen (nur für Windows-PCs)  

In dieser Vorgehensweise werden die Standardclienteinstellungen für Konformitätseinstellungen konfiguriert und auf alle Computer in Ihrer Hierarchie angewendet. Wenn Sie diese Einstellungen nur auf manche Computer anwenden möchten, erstellen Sie eine benutzerdefinierte Geräteclienteinstellung, und weisen Sie diese einer Sammlung zu, die die Computer enthält, für die Sie die Kompatibilitätseinstellungen anwenden möchten. Weitere Informationen zum Erstellen von benutzerdefinierten Geräteeinstellungen finden Sie unter [How to configure client settings (Konfigurieren von Clienteinstellungen)](../../core/clients/deploy/configure-client-settings.md).  

> [!TIP]  
>  Andere Gerätetypen erfordern keine besondere Konfiguration für die Auswertung von Kompatibilitätseinstellungen.  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Clienteinstellungen** > **Standardeinstellungen**.  
2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  
3.  Klicken Sie im Dialogfeld **Standardeinstellungen** auf **Kompatibilitätseinstellungen**.  
4.  Konfigurieren Sie die folgenden Clienteinstellungen für Kompatibilitätseinstellungen:
    - **Kompatibilitätsauswertung auf Clients aktivieren:** Legen Sie diese Einstellung auf **TRUE** fest, wenn Sie die Kompatibilität auf Clientgeräten auswerten möchten.
    - **Kompatibilitätsauswertung planen:** Klicken Sie auf **Zeitplan**, wenn Sie den Standardzeitplan der Kompatibilitätsauswertung auf Clientgeräten ändern möchten.
    - **Benutzerdaten und -profile aktivieren:** Aktivieren Sie diese Option, wenn Sie Konfigurationselemente für Benutzerdaten und -profile auf Windows-Computern erstellen und bereitstellen möchten. Ausführlichere Informationen finden Sie unter [Erstellen von Konfigurationselementen für Benutzerdaten und -profile](../deploy-use/create-remote-connection-profiles.md).
5. Klicken Sie auf **OK** , um das Dialogfeld **Standardeinstellungen** zu schließen.  

Die Clientcomputer werden beim nächsten Download der Clientrichtlinien mit diesen Einstellungen konfiguriert.  
