---
title: Synchronisieren von Geräten mit Microsoft Intune – Azure | Microsoft-Dokumentation
description: Synchronisieren von Geräten, die bei Microsoft Intune registriert sind und dort verwaltet werden, um die neuesten Richtlinien und Aktionen zu erhalten. In diesem Artikel werden die Schritte erläutert, die zur Synchronisierung mithilfe des Azure-Portals erfordelrich sind. Außerdem werden die wiederholbaren Fehlercodes aufgeführt.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/27/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 02ad249e-f098-421f-861f-6b2ff733ac7c
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: de0c6694f046d9df61f136e830d220ab0b688d28
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252689"
---
# <a name="sync-devices-to-get-the-latest-policies-and-actions-with-intune"></a>Synchronisieren von Geräten mit Intune, um die neuesten Richtlinien und Aktionen zu erhalten


Die Geräteaktion **Synchronisieren** zwingt das ausgewählte Gerät, sich sofort bei Intune anzumelden. Checkt ein Gerät ein, empfängt es sofort alle ihm zugewiesenen ausstehenden Aktionen oder Richtlinien. Diese Funktion kann Ihnen dabei helfen, die von Ihnen zugewiesenen Richtlinien sofort zu überprüfen und Probleme zu behandeln, ohne auf die nächste geplante Anmeldung zu warten.

## <a name="supported-platforms"></a>Unterstützte Plattformen

- Windows
- iOS
- macOS
- Android

## <a name="sync-a-device"></a>Gerät synchronisieren

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an. 
3. Klicken Sie auf **Geräte** > **Alle Geräte**.
4. Wählen Sie in der Liste der von Ihnen verwalteten Geräte ein Gerät aus, öffnen Sie seinen *Übersichtsbereich*, und wählen Sie dann **Synchronisieren** aus.
5. Klicken Sie zum Bestätigen auf **Ja**.

Klicken Sie auf **Geräte**  >  **Überwachen**  >  **Geräteaktionen**, um den Status der Synchronisierung anzuzeigen.

Sie finden die standardmäßige Intune-Richtlinie zu Check-In-Frequenzen in der [Übersicht über die Gerätekonfiguration](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

## <a name="retryable-error-codes"></a>Wiederholbare Fehlercodes

Wenn ein Administrator die Geräteaktion **Synchronisieren** ausführt, sind iOS-/iPadOS- und Android-Apps, für die die Synchronisierung nicht ausgeführt werden konnte und die einen wiederholbaren Fehlercode ausgelöst haben, auf dem Gerät weiterhin verfügbar. Allerdings dauert es sieben Tage, bis Apps, die einen nicht wiederholbaren Fehlercode ausgelöst haben, auf dem Gerät wieder verfügbar sind.


| Fehlercode  | Vorgeschlagene Beschreibung | Wiederholbar |
|---|---|---|
| 2016330898 | Unbekannter Fehler aufgetreten. | Nein |
| 2016330897 | Ihre Verbindung zu Intune wurde aufgrund einer Zeitüberschreitung abgebrochen. Setzen Sie Ihre Verbindung zurück. | Ja |
| 2016330896 | Ihre Internetverbindung wurde getrennt. Setzen Sie Ihre Verbindung zurück. | Ja |
| 2016330895 | Ihre Internetverbindung wurde getrennt. Setzen Sie Ihre Verbindung zurück. | Ja |
| 2016330894 | Ihre Internetverbindung wurde getrennt. Setzen Sie Ihre Verbindung zurück. | Ja |
| 2016330893 | Ihre Internetverbindung wurde getrennt. Setzen Sie Ihre Verbindung zurück. | Ja|
| 2016330892 | Internationales Roaming ist deaktiviert. | Nein|
| 2016330891 | Während eines Anrufs kann für dieses Gerät nicht auf die Mobilfunkverbindung zugegriffen werden. Warten Sie, bis der Anruf beendet wird. | Ja|
| 2016330890 | Das Mobilfunknetz für dieses Gerät: Diese Geräte konnten zu diesem Zeitpunkt nicht verwendet werden. | Nein|
| 2016330889 | Fehler bei der sicheren Verbindung: Setzen Sie Ihre Verbindung zurück. | Ja|
| 2016330888 | Fehler bei der Auswertung der Serververtrauensstellung | Nein|

## <a name="next-steps"></a>Nächste Schritte

Sie können sich [die Details](device-inventory.md) des Geräts anschauen.
 
