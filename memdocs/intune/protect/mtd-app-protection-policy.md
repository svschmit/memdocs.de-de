---
title: Erstellen einer Mobile Threat Defense-App-Schutzrichtlinie (MTD) mit Intune
titleSuffix: Microsoft Intune
description: Erfahren Sie, wie Sie eine Mobile Threat Defense-App-Schutzrichtlinie (MTD) mit Microsoft Intune erstellen können.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: 0fc25aa915762e0e1df9446c9fb14513bdf20352
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79351564"
---
# <a name="create-mobile-threat-defense-app-protection-policy-with-intune"></a>Erstellen einer Mobile Threat Defense-App-Schutzrichtlinie (MTD) mit Intune

Intune mit Mobile Threat Defense (MTD) hilft Ihnen dabei, Bedrohungen zu erkennen und Risiken auf mobilen Geräten zu bewerten. Sie können eine Intune-App-Schutzrichtlinie erstellen, die eine Risikobewertung durchführt und bestimmt, ob dem Gerät Zugriff auf Unternehmensdaten gewährt wird.

> [!NOTE]
> Dieser Artikel gilt für alle Mobile Threat Defense-Partner, die App-Schutzrichtlinien unterstützen:
>
> - Better Mobile (Android, iOS/iPadOS)
> - Zimperium (Android, iOS/iPadOS)
> - Lookout for Work (Android, iOS/iPadOS)

## <a name="before-you-begin"></a>Vorbereitung

Beim Einrichten von MTD haben Sie in der MTD-Partnerkonsole eine Richtlinie erstellt, die verschiedene Bedrohungen als hoch, mittel und niedrig klassifiziert. Nun müssen Sie die Mobile Threat Defense-Stufe in der Intune-App-Schutzrichtlinie festlegen.

Voraussetzungen für die App-Schutzrichtlinie mit MTD:

- Richten Sie die MTD-Integration in Intune ein. Ohne diese Integration hat die MTD-App-Schutzrichtlinie keine Auswirkung.

## <a name="to-create-an-mtd-app-protection-policy"></a>Erstellen einer MTD-App-Schutzrichtlinie

Verwenden Sie die Prozedur, um [eine iOS-/iPadOS- oder Android-App-Schutzrichtlinie zu erstellen](../apps/app-protection-policies.md#app-protection-policies-for-iosipados-and-android-apps), und verwenden Sie die folgenden Informationen von den Seiten *Apps*, *Bedingter Start* und *Zuweisungen*:

- **Apps**: Wählen Sie die Apps aus, für die die App-Schutzrichtlinien gelten sollen. Für diese Featuregruppe werden diese Apps blockiert oder basierend auf der Geräterisikobewertung des Mobile Threat Defense-Anbieters selektiv zurückgesetzt.
- **Bedingter Start:**  Wählen Sie in der Dropdownliste unter *Gerätebedingungen* **Maximal zulässige Bedrohungsstufe für Gerät** aus.

  Optionen für den **Wert** der Bedrohungsstufe:

  - **Secured** (Geschützt): Diese Stufe ist die sicherste Einstellung. Solange auf einem Gerät Bedrohungen vorhanden sind, ist kein Zugriff auf Unternehmensressourcen möglich. Wenn Bedrohungen gefunden werden, wird das Gerät als nicht kompatibel bewertet.
  - **Niedrig:** Das Gerät ist konform, wenn nur Bedrohungen auf niedriger Stufe vorliegen. Durch Bedrohungen höherer Stufen wird das Gerät in einen nicht kompatiblen Status versetzt.
  - **Mittel**: Das Gerät ist konform, wenn auf dem Gerät Bedrohungen niedriger oder mittlerer Stufe gefunden werden. Wenn auf dem Gerät Bedrohungen hoher Stufen erkannt werden, wird es als nicht kompatibel bewertet.
  - **Hoch**: Diese Stufe bietet die geringste Sicherheit. Es werden alle Bedrohungsstufen zugelassen, und Mobile Threat Defense wird nur zu Berichtszwecken verwendet. Auf Geräten muss mit dieser Einstellung die MTD-App aktiviert sein.

  Optionen für **Aktion**:

  - **Zugriff blockieren**
  - **Daten löschen**

- **Zuweisungen:** Weisen Sie die Richtlinie Benutzergruppen zu.  Die von den Gruppenmitgliedern verwendeten Geräte werden für den Zugriff auf Unternehmensdaten in Ziel-Apps über den Intune-App-Schutz ausgewertet.

## <a name="next-steps"></a>Nächste Schritte

- Erfahren Sie mehr über [Mobile Threat Defense](mobile-threat-defense.md) in Microsoft Intune.
