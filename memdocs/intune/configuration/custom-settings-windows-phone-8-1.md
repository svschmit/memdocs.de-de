---
title: 'Hinzufügen von benutzerdefinierten Einstellungen für Windows Phone 8.1-Geräte in Microsoft Intune: Azure | Microsoft-Dokumentation'
titleSuffix: ''
description: Fügen Sie ein benutzerdefinierten Profils zur Verwendung der OMA-URI-Einstellungen für Windows Phone 8.1-Geräte in Microsoft Intune hinzu, oder erstellen Sie ein solches Profil.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 08/11/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ROBOTS: NOINDEX
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: c0adb573dbb40f00a1b43b9fb356cdc20b97b669
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910076"
---
# <a name="use-custom-settings-for-windows-phone-81-devices-in-intune"></a>Verwenden von benutzerdefinierten Einstellungen für Windows Phone 8.1-Geräte in Intune

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]

Mit Microsoft Intune können Sie benutzerdefinierte Einstellungen für Windows Phone 8.1-Geräte mit einem benutzerdefinierten Profil hinzufügen oder erstellen. Benutzerdefinierte Profile sind ein Feature in Intune. Sie sind dafür da, Geräteeinstellungen und -features hinzuzufügen, die nicht in Intune integriert sind.

Benutzerdefinierte Windows Phone 8.1-Profile verwenden die OMA-URI-Einstellungen (Open Mobile Alliance Uniform Resource Identifier) zum Konfigurieren verschiedener Features. Diese Einstellungen werden in der Regel von den Herstellern der Geräte verwendet, um die Features auf dem Gerät zu steuern. In der [Dokumentation zum Windows Phone 8.1-MDM-Protokoll](/previous-versions/windows/it-pro/windows-phone/dn499787(v=technet.10)) werden die Einstellungen aufgeführt.

In diesem Artikel erfahren Sie, wie Sie ein benutzerdefiniertes Profil für Windows Phone 8.1-Geräte erstellen. 

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen Sie ein benutzerdefiniertes Windows Phone 8.1-Profil](custom-settings-configure.md).

## <a name="custom-oma-uri-settings"></a>Benutzerdefinierte OMA-URI-Einstellungen

- **OMA-URI-Einstellungen**: **Fügen** Sie die folgenden Einstellungen hinzu:

  - **Name:** Geben Sie einen eindeutigen Namen für die OMA-URI-Einstellung ein, damit Sie sie in der Liste der Einstellungen leichter identifizieren können.
  - **Beschreibung:** Geben Sie eine Beschreibung, die eine Übersicht über die Einstellung bietet, und andere relevante Informationen ein, die Ihnen die Suche nach dem Profil erleichtern.
  - **OMA-URI** (Groß-/Kleinschreibung beachten): Geben Sie den OMA-URI ein, für den Sie eine Einstellung bereitstellen möchten.
  - **Datentyp:** Wählen Sie den Datentyp aus, den Sie für diese OMA-URI-Einstellung verwenden möchten. Folgende Optionen sind verfügbar:

    - Zeichenfolge
    - Zeichenfolge (XML-Datei)
    - Datum und Uhrzeit
    - Ganze Zahl
    - Gleitkomma
    - Boolesch
    - Base64 (Datei)

  - **Wert**: Geben Sie den gewünschten Datenwert an, der dem von Ihnen eingegebenen OMA-URI zugeordnet werden soll. Der Wert hängt vom ausgewählten Datentyp ab. Beim Datentyp **Datum und Uhrzeit** wählen Sie den Wert beispielsweise aus einer Datumsauswahl aus.

  Wenn Sie einige Einstellungen hinzugefügt haben, können Sie auf **Exportieren** klicken. Wenn Sie auf **Exportieren** klicken, wird eine Liste aller hinzugefügten Werte in einer Datei mit durch Trennzeichen getrennten Werten (CSV) erstellt.

## <a name="example"></a>Beispiel

Im folgenden Beispiel werden Windows 8.1-Smartphones daran gehindert, Mobilfunknetze zu ändern, wenn der Benutzer außerhalb des Abdeckungsbereichs des Netzbetreibers unterwegs ist.

- **Name:** Roaming für mobile Daten zulassen
- **Beschreibung:** Roaming für mobile Daten zulassen oder verweigern
- **OMA-URI** (case sensitive): ./Vendor/MSFT/PolicyManager/My/Connectivity/AllowCellularDataRoaming
- **Datentyp:** Ganze Zahl
- **Wert:** 0

## <a name="next-steps"></a>Nächste Schritte

[Weisen Sie das Profil zu](device-profile-assign.md), und [überwachen Sie dessen Status](device-profile-monitor.md).

Erstellen eines [benutzerdefinierten Profils auf Windows 10-Geräten](custom-settings-windows-10.md).