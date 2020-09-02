---
title: Verstehen der Einschränkungen zum Gerätelimit in Intune und Azure
titleSuffix: ''
description: Informieren Sie sich über die Unterschiede zwischen den Einschränkungen zum Gerätelimit von Intune und den Einschränkungen von Azure AD.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 04/12/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 63c9d9e4752e4b0d317667162255e368fc5a099c
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88908553"
---
# <a name="understand-intune-and-azure-ads-device-limit-restrictions"></a>Verstehen der Einschränkungen zum Gerätelimit in Intune und Azure AD

Einschränkungen zum Gerätelimit können auf zwei Arten konfiguriert werden:
- Intune-Registrierung
- In Azure Active Directory (AD) eingebunden oder in Azure AD registriert

In diesem Artikel wird erläutert, wann diese Limits basierend auf Ihrer Konfiguration angewendet werden.

## <a name="intune-device-limit-restrictions"></a>Einschränkungen zum Gerätelimit von Intune

Die Einschränkungen zum Gerätelimit von Intune legen die maximale Anzahl von Geräten fest, die ein Benutzer steuern kann (der maximale Wert ist 15). Um dieses **Gerätelimit** festzulegen, navigieren Sie zu [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Geräte** > **Registrierungseinschränkungen**. Weitere Informationen finden Sie unter [Erstellen einer Einschränkungen zum Gerätelimit](enrollment-restrictions-set.md#create-a-device-limit-restriction).

## <a name="azure-device-limit-restriction"></a>Einschränkung zum Gerätelimit in Azure

Einschränkungen zum Gerätelimit in Azure legen die maximale Anzahl von Geräten fest, die in Azure AD eingebunden oder registriert werden können. Um die **maximale Anzahl von Geräten pro Benutzer** festzulegen, navigieren Sie zum Azure-Portal und dann zu **Azure Active Directory** > **Geräte**. Weitere Informationen finden Sie unter [Konfigurieren von Geräteeinstellungen](/azure/active-directory/devices/device-management-azure-portal).

## <a name="settings-applied-based-on-user-affinity"></a>Auf Grundlage von Benutzeraffinität angewendete Einstellungen

Wenn Sie Einschränkungen zum Gerätelimit für Intune und für Azure festgelegt haben, können Sie der folgenden Tabelle entnehmen, was auf Grundlage ihrer Benutzeraffinitätseinstellung angewendet wird.

| Geräteplattform | Benutzeraffinität | Von Azure angewendet | Von Intune angewendet |
| ----- | ----- | ----- | ----- | ----- |
| Android Enterprise-Arbeitsprofil | Ja | Ja | Ja|
| Dediziertes Android Enterprise-Gerät | Nein | Nein | Nein |
| Vollständig verwaltetes Android Enterprise | Ja | Ja | Ja |
| Android-Geräteadministrator | Ja | Ja | Ja |
| Android-Geräteadministrator-DEM | Nein | | Nein | 
| iOS/macOS BYOD | Ja | Ja | Ja |
| Automatische Geräteregistrierung (Automated Device Enrollment, ADE) von iOS/macOS | Ja | Ja | Ja |
| iOS/macOS ADE | Nein | Ja | Nein |
| Windows BYOD | Ja | Ja | Ja |
| Nur Windows-MD | | Ja | Ja |
| In Windows Azure AD eingebunden| Ja | Ja | Nein |
| Windows Autopilot | Ja | Ja | Nein |
| In Windows-Hybrid-Azure AD eingebunden | Nein | Nein | Ja |
| Windows Co-Verwaltung | Nein | Ja | Nein |
| Windows DEM | Nein | Ja | Nein |
| Windows-Massenregistrierung | Nein | Ja | Nein |


## <a name="android-and-ios-devices"></a>Android- und iOS-Geräte

### <a name="ios-or-android-devices-example-1"></a>iOS- oder Android-Gerätebeispiel 1

- Die Azure-Einstellung **Maximale Anzahl von Geräten pro Benutzer** ist auf 3 festgelegt.
- Die Einstellung **Gerätelimit** von Intune ist auf 5 festgelegt.
 
**Ergebnis**: Die maximale Anzahl wird pro Benutzer angegeben. Wenn Sie z. B. drei Intune-Geräte registrieren, schlägt die Azure-Registrierung für das vierte Gerät aufgrund der Einstellungen zum Begrenzen der Anzahl von Registrierungen für Geräte fehl.

### <a name="ios-or-android-devices-example-2"></a>iOS- oder Android-Gerätebeispiel 2

- Die Azure-Einstellung **Maximale Anzahl von Geräten pro Benutzer** ist auf 20 festgelegt.
- Die Einstellung **Gerätelimit** von Intune ist auf 2 festgelegt.

**Ergebnis**: Sie können zwei Geräte erfolgreich registrieren. Die Intune-Registrierung wird für alle weiteren Geräte blockiert. ADE ohne Benutzeraffinität wird durch die Begrenzung der Anzahl von Registrierungen für Azure-Geräte eingeschränkt, obwohl sie nicht mit einem Benutzer verknüpft ist.

## <a name="windows-devices"></a>Windows-Geräte

Einschränkungen des Gerätelimits in Intune gelten nicht für die folgenden Windows-Registrierungstypen:
- Gemeinsam verwaltete Registrierungen
- GPO-Registrierungen (Gruppenrichtlinienobjekt)
- Eingebundene Azure AD-Registrierungen
- Eingebundene Azure AD-Massenregistrierungen
- Autopilot-Registrierungen
- Registrierungen über den Geräteregistrierungs-Manager

Sie können Gerätelimiteinschränkungen für diese Registrierungstypen nicht erzwingen, da diese als Szenarien mit gemeinsam genutzten Geräten gelten. Sie können für diese Registrierungstypen harte Grenzwerte in Azure Active Directory festlegen.

Für die Einschränkungen des Gerätelimits in Azure gilt die Einstellung **Maximale Anzahl von Geräten pro Benutzer** für Geräte, die entweder in Azure AD eingebunden oder in Azure AD registriert sind. Diese Einstellung gilt nicht für eingebundene Azure AD-Hybridgeräte.

### <a name="windows-10-example-1"></a>Windows 10: Beispiel 1

- Die Azure-Einstellung **Maximale Anzahl von Geräten pro Benutzer** ist auf 5 festgelegt.
- Die Einstellung **Gerätelimit** von Intune ist auf 3 festgelegt.
- Die Geräte sind in Azure AD eingebundene Hybridgeräte und werden automatisch registriert (durch GPO konfiguriert).

**Ergebnis**: Da die Registrierung über ein GPO gepusht wird, gilt die Begrenzung der Anzahl von Registrierungen für Azure-Geräte nicht.  Die Einschränkungen des Gerätelimits in Intune gilt ebenfalls nicht.

### <a name="windows-10-example-2"></a>Windows 10: Beispiel 2

- Die Azure-Einstellung **Maximale Anzahl von Geräten pro Benutzer** ist auf 5 festgelegt.
- Die Einstellung **Gerätelimit** von Intune ist auf 2 festgelegt.
- Die Geräte sind in eine lokale Domäne eingebunden und werden über **Einstellungen** > **Zugriff auf Geschäft, Schule oder Uni** > **Verbinden** registriert.

**Ergebnis**: Sie können nur zwei Geräte registrieren, bevor eine Blockierung erfolgt. Sie können bis zu fünf Geräte registrieren.


## <a name="next-steps"></a>Nächste Schritte

- [Erstellen einer Gerätelimiteinschränkung in Azure.](/azure/active-directory/devices/device-management-azure-portal#configure-device-settings)
- [Konfigurieren von Geräteeinstellungen in Azure.](enrollment-restrictions-set.md#create-a-device-limit-restriction)
- [Weitere Informationen zur Registrierung und zum Domänenbeitritt.](/azure/active-directory/devices/overview#getting-devices-in-azure-ad)