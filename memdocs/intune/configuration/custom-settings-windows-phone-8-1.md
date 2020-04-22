---
title: 'Hinzufügen von benutzerdefinierten Einstellungen für Windows Phone 8.1-Geräte in Microsoft Intune: Azure | Microsoft-Dokumentation'
titleSuffix: ''
description: Fügen Sie ein benutzerdefinierten Profils zur Verwendung der OMA-URI-Einstellungen für Windows Phone 8.1-Geräte in Microsoft Intune hinzu, oder erstellen Sie ein solches Profil.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 12/18/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b1bea9047d65faf449c77e1a677000d32e883a76
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "79364525"
---
# <a name="use-custom-settings-for-windows-phone-81-devices-in-intune"></a>Verwenden von benutzerdefinierten Einstellungen für Windows Phone 8.1-Geräte in Intune

Mit Microsoft Intune können Sie benutzerdefinierte Einstellungen für Windows Phone 8.1-Geräte mit einem benutzerdefinierten Profil hinzufügen oder erstellen. Benutzerdefinierte Profile sind ein Feature in Intune. Sie sind dafür da, Geräteeinstellungen und -features hinzuzufügen, die nicht in Intune integriert sind.

Benutzerdefinierte Windows Phone 8.1-Profile verwenden die OMA-URI-Einstellungen (Open Mobile Alliance Uniform Resource Identifier) zum Konfigurieren verschiedener Features. Diese Einstellungen werden in der Regel von den Herstellern der Geräte verwendet, um die Features auf dem Gerät zu steuern. In der [Dokumentation zum Windows Phone 8.1-MDM-Protokoll](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-phone/dn499787(v=technet.10)) werden die Einstellungen aufgeführt.

In diesem Artikel erfahren Sie, wie Sie ein benutzerdefiniertes Profil für Windows Phone 8.1-Geräte erstellen. 

## <a name="create-the-profile"></a>Erstellen des Profils

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.
3. Legen Sie folgende Einstellungen fest:

    - **Name:** Geben Sie einen aussagekräftigen Namen für das Profil ein. Benennen Sie Ihre Profile, damit Sie diese später leicht wiedererkennen. Ein guter Profilname ist beispielsweise **Benutzerdefiniertes Windows Phone-Profil**.
    - **Beschreibung:** Geben Sie eine Beschreibung ein, die einen Überblick über die Einstellung und andere wichtige Details bietet.
    - **Plattform**: Wählen Sie **Windows Phone 8.1** aus.
    - **Profiltyp**: Klicken Sie auf **Benutzerdefiniert**.

4. Klicken Sie unter **Benutzerdefinierte OMA-URI-Einstellungen** auf **Hinzufügen**. Legen Sie folgende Einstellungen fest:

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

5. Klicken Sie auf **OK**, um die Änderungen zu speichern. Fügen Sie nach Bedarf weitere Einstellungen hinzu.
6. Klicken Sie anschließend auf **OK** > **Erstellen**, um das Intune-Profil zu erstellen. Das Profil wird erstellt und in der Liste **Gerätekonfiguration > Konfigurationsprofile** angezeigt.

## <a name="example"></a>Beispiel

Im folgenden Beispiel werden Windows 8.1-Smartphones daran gehindert, Mobilfunknetze zu ändern, wenn der Benutzer außerhalb des Abdeckungsbereichs des Netzbetreibers unterwegs ist.

- **Name:** Roaming für mobile Daten zulassen
- **Beschreibung:** Roaming für mobile Daten zulassen oder verweigern
- **OMA-URI** (case sensitive): ./Vendor/MSFT/PolicyManager/My/Connectivity/AllowCellularDataRoaming
- **Datentyp:** Ganze Zahl
- **Wert:** 0

## <a name="next-steps"></a>Nächste Schritte

Das Profil ist nun erstellt, führt aber noch keine Aktionen durch. Die nächsten Schritte sind das [Zuweisen von Benutzer- und Geräteprofilen in Microsoft Intune](device-profile-assign.md) und das [Überwachen von Geräteprofilen in Microsoft Intune](device-profile-monitor.md).

Erstellen eines [benutzerdefinierten Profils auf Windows 10-Geräten](custom-settings-windows-10.md).
