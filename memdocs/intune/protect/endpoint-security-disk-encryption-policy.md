---
title: Verwalten der Datenträgerverschlüsselung mit Endpunktsicherheitsrichtlinien in Microsoft Intune | Microsoft-Dokumentation
description: Konfigurieren und Bereitstellen von Richtlinien für Geräte, die Sie mithilfe von Richtlinien für die Datenträgerverschlüsselung für Endpunktsicherheit in Microsoft Endpoint Manager verwalten.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: a8eeb8263e337fa7427818c05f183fdea3c9dbea
ms.sourcegitcommit: 22e1095a41213372c52d85c58b18cbabaf2300ac
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/25/2020
ms.locfileid: "85353631"
---
# <a name="disk-encryption-policy-for-endpoint-security-in-intune"></a>Einstellungen der Richtlinie für die Datenträgerverschlüsselung für Endpunktsicherheit in Intune

Die Datenträgerverschlüsselungsprofile für die Endpunktsicherheit konzentrieren sich ausschließlich auf die Einstellungen, die für eine integrierte Verschlüsselungsmethode für Geräte relevant sind, zum Beispiel FileVault oder BitLocker. Dieser Schwerpunkt vereinfacht Sicherheitsadministratoren die Verwaltung der Datenträgerverschlüsselungseinstellungen, ohne in einem Host mit nicht verknüpften Einstellungen navigieren zu müssen.

Obwohl Sie die gleichen Geräteeinstellungen mithilfe von *Endpoint Protection*-Profilen für die Gerätekonfiguration konfigurieren können, enthalten die Gerätekonfigurationsprofile zusätzliche Einstellungskategorien. Diese zusätzlichen Einstellungen stehen nicht im Zusammenhang mit der Datenträgerverschlüsselung und können die Konfiguration einer reinen Datenträgerverschlüsselung erschweren.

Die Endpunktsicherheitsrichtlinien für die Datenträgerverschlüsselung finden Sie unter *Verwalten* im Knoten **Endpunktsicherheit** des [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).

## <a name="prerequisites-for-disk-encryption-policy"></a>Voraussetzungen für die Richtlinie zur Datenträgerverschlüsselung

- **macOS:** macOS 10.13 oder höher
- **Windows:** Windows 10 oder höher

## <a name="disk-encryption-profiles"></a>Datenträgerverschlüsselungsprofile

**macOS-Profile:**

- **FileVault:** FileVault bietet integrierte vollständige Datenträgerverschlüsselung für macOS-Geräte.

  Verwalten von [FileVault-Einstellungen](../protect/endpoint-security-disk-encryption-profile-settings.md#filevault) für macOS

  Unter [Verwenden der FileVault-Datenträgerverschlüsselung für macOS](../protect/encrypt-devices-filevault.md) finden Sie Informationen zum Erstellen eines FileVault-Profils.

**Windows 10-Profile:**

- **BitLocker:** Die BitLocker-Laufwerkverschlüsselung ist ein Datenschutzfeature, das in das Betriebssystem integriert wird und die Bedrohungen des Diebstahls oder der Offenlegung von Daten auf verlorenen, gestohlenen oder nicht ordnungsgemäß außer Betrieb gesetzten Computern beseitigt.

  Verwalten von [Einstellungen für BitLocker](../protect/endpoint-security-disk-encryption-profile-settings.md#bitlocker) für Windows 10

  Im Artikel zum [Verwalten der BitLocker-Datenträgerverschlüsselung für Windows 10](../protect/encrypt-devices.md) finden Sie Informationen zum Erstellen eines BitLocker-Profils.

## <a name="manage-device-encryption"></a>Verwalten der Geräteverschlüsselung

Nach der Bereitstellung einer Richtlinie zum Verschlüsseln eines Gerätedatenträgers finden Sie in den folgenden Artikeln Informationen zum Verwalten der Verschlüsselung:

- [Verwalten von BitLocker](../protect/encrypt-devices.md#manage-bitlocker)
- [Verwalten von FileVault](../protect/encrypt-devices-filevault.md#manage-filevault)
- [Überwachen der Geräteverschlüsselung](../protect/encryption-monitor.md)

## <a name="next-steps"></a>Nächste Schritte

- [Erstellen eines FileVault-Profils](../protect/encrypt-devices-filevault.md#create-endpoint-security-policy-for-filevault)
- [Erstellen eines BitLocker-Profils](../protect/encrypt-devices.md#create-an-endpoint-security-policy-for-bitlocker)
