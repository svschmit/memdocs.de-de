---
title: Geräteverwaltung mit Exchange
titleSuffix: Configuration Manager
description: Verwalten Sie mobile Geräte mit dem Exchange Server-Connector in Configuration Manager.
ms.date: 12/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: aba688d9-fd5b-4c42-8cb4-f7e1b161ef50
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 08d92d5c09331d675dc679a374e1bbf81633748e
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724804"
---
# <a name="device-management-with-exchange-and-configuration-manager"></a>Geräteverwaltung mit Exchange und Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Wenn Sie über mobile Geräte verfügen, die über das ActiveSync-Protokoll mit Exchange Server verbunden sind, können Sie den Exchange Server-Connector in Configuration Manager verwenden, um diese Geräte zu verwalten. Der Connector funktioniert sowohl mit lokalem Exchange Server als auch mit Exchange Online. Verwenden Sie die Configuration Manager Konsole, um die Exchange-Verwaltungsfunktionen für mobile Geräte zu konfigurieren. Beispielsweise die Remote Geräte Löschung und die Einstellungs Steuerung für mehrere Exchange-Server.

![Logisches Diagramm von Exchange Server-Connector mit Configuration Manager](media/configmgr-with-exchange.png)  

Wenn Sie mobile Geräte mit diesem Connector verwalten, wird der Configuration Manager-Client nicht installiert, oder Sie registrieren die Geräte über MDM. Die Verwaltungsfunktionen von Exchange Server sind im Vergleich zu diesen anderen Optionen eingeschränkt. Beispielsweise können Sie keine Software installieren oder Konfigurationselemente verwenden, um diese Geräte zu konfigurieren. Weitere Informationen finden Sie unter [Auswählen einer Geräte Verwaltungs Lösung für Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md).  

## <a name="policies"></a>Richtlinien

Wenn Sie den Connector verwenden, konfiguriert Configuration Manager Einstellungen auf den mobilen Geräten. Die standardmäßigen Exchange ActiveSync-Post Fach Richtlinien werden von den Geräten nicht verwendet. Definieren Sie die Einstellungen, die Sie in den folgenden Gruppen verwenden möchten:

- **Allgemein**
- **Kennwort**
- **E-Mail Verwaltung**
- **Sicherheit**
- **Anwendung**

In der Gruppe **Kennwort** können Sie z. b. die folgenden Einstellungen konfigurieren:

- Ob für mobile Geräte ein Kennwort erforderlich ist
- Die minimale Kenn Wort Länge
- Kennwortkomplexität
- Ob eine Kenn Wort Wiederherstellung zulässig ist

Wenn Sie in der Gruppe mindestens eine Einstellung konfigurieren, werden alle Einstellungen in der Gruppe für mobile Geräte von Configuration Manager verwaltet. Wenn Sie in einer Gruppe keine Einstellung konfigurieren, werden diese Einstellungen von Exchange weiterhin für die mobilen Geräte verwaltet. Alle Exchange ActiveSync-Post Fach Richtlinien, die Sie auf dem Exchange-Server konfigurieren und Benutzern zuweisen, werden weiterhin angewendet.

## <a name="access-rules-and-remote-actions"></a>Zugriffsregeln und Remote Aktionen

Sie können auch den Exchange Server-Connector konfigurieren, um die Exchange-Zugriffsregeln zu verwalten. Zu diesen Zugriffsregeln gehören das zulassen, blockieren oder unter Quarantäne mobiler Geräte. Sie können mobile Geräte über die Configuration Manager-Konsole Remote löschen, und Benutzer können Ihre mobilen Geräte mithilfe des Anwendungs Katalogs Remote löschen.

Das Mobile Gerät eines Benutzers wird automatisch im Anwendungs Katalog angezeigt, wenn Sie es verwalten und der Exchange-Server lokal ist. Damit das Mobile Gerät im Anwendungs Katalog angezeigt wird, wenn Sie Exchange Online verwenden, konfigurieren Sie die Affinität zwischen Benutzer und Gerät manuell. Weitere Informationen finden Sie unter [Verknüpfen von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

> [!TIP]  
> Wenn ein mobiles Gerät an einen anderen Benutzer übertragen wird, bevor der neue Besitzer das Exchange-Konto auf dem Gerät konfiguriert, löschen Sie das Mobile Gerät aus der Configuration Manager-Konsole.

## <a name="prerequisites"></a>Voraussetzungen

> [!IMPORTANT]  
> Vergewissern Sie sich, dass Configuration Manager Ihre Exchange-Version unterstützt, bevor Sie diesen Connector installieren. Weitere Informationen finden Sie [unter Unterstützte Konfigurationen-Exchange Server-Connector](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_ExSrvConOS).  

### <a name="permissions-to-configure-the-connector"></a>Berechtigungen zum Konfigurieren des Verbindungs-Connector

Sie benötigen die folgenden Sicherheits Berechtigungen, um den Exchange Server-Connector in Configuration Manager zu konfigurieren:

- Die Berechtigung **Ändern** für das Objekt **Standort** , um den Exchange Server-Connector hinzufügen, ändern und löschen zu können  

- Die Berechtigung **ModifyConnectorPolicy** für das Objekt **Standort** , um die Einstellungen mobiler Geräte konfigurieren zu können  

Beispielsweise enthält die integrierte Rolle **Vollständiger Administrator** diese erforderlichen Berechtigungen.  

### <a name="permissions-to-manage-mobile-devices"></a>Berechtigungen zum Verwalten mobiler Geräte

Sie benötigen die folgenden Sicherheits Berechtigungen, um mobile Geräte zu verwalten:  

- Die Berechtigung **Ressource löschen** für das Objekt **Sammlung** , um ein mobiles Gerät zurücksetzen zu können  

- Die Berechtigung **Ressource ändern** für das Objekt **Sammlung** , um einen Befehl zum Zurücksetzen abbrechen zu können  

- Berechtigung **Ressource ändern** für das Objekt **Sammlung** , um mobile Geräte zulassen und blockieren zu können  

Die integrierte Rolle " **Operations Administrator** " enthält z. b. die erforderlichen Berechtigungen.

Weitere Informationen finden Sie unter [Konfigurieren der rollenbasierten Verwaltung](../../core/servers/deploy/configure/configure-role-based-administration.md).

## <a name="next-steps"></a>Nächste Schritte

> [!div class="nextstepaction"]
> [Installieren und Konfigurieren von Exchange Connector](install-configure-exchange-connector.md)
