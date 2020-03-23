---
title: macOS-Einstellungen für Kernelerweiterungen in Microsoft Intune – Azure | Microsoft-Dokumentation
titleSuffix: ''
description: Hier erfahren Sie, wie Sie Einstellungen auf macOS-Geräten hinzufügen, konfigurieren oder erstellen, um Kernelerweiterungen zu verwenden. Außerdem wird beschrieben, wie Sie in Microsoft Intune Benutzern das Überschreiben genehmigter Erweiterungen ermöglichen und alle Erweiterungen einer Team-ID, bestimmte Erweiterungen oder bestimmte Apps zulassen.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/10/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: aa471beb5929a6c5b39267871518f560fe6978f6
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79343426"
---
# <a name="macos-device-settings-to-configure-and-use-kernel-extensions-in-intune"></a>macOS-Geräteeinstellungen zum Konfigurieren und Verwenden von Kernelerweiterungen in Intune



In diesem Artikel werden die verschiedenen Einstellungen für Kernelerweiterungen aufgeführt und beschrieben, die Sie auf macOS-Geräten steuern können. Mit diesen Einstellungen Ihrer Lösung für die mobile Geräteverwaltung (Mobile Device Management, MDM) können Sie Kernelerweiterungen auf Ihren Geräten hinzufügen und verwalten.

Weitere Informationen zu Kernelerweiterungen in Intune und deren Anforderungen finden Sie unter [Hinzufügen von macOS-Kernelerweiterungen in Intune](kernel-extensions-overview-macos.md).

Diese Einstellungen werden einem Gerätekonfigurationsprofil in Intune hinzugefügt und dann Ihren macOS-Geräten zugewiesen oder bereitgestellt.

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen Sie ein Konfigurationsprofil für Kernelerweiterungen.](kernel-extensions-overview-macos.md)

> [!NOTE]
> Diese Einstellungen gelten für verschiedene Registrierungstypen. Weitere Informationen zu den verschiedenen Registrierungstypen finden Sie unter [macOS-Registrierung](../enrollment/macos-enroll.md).

## <a name="kernel-extensions"></a>Kernelerweiterungen

### <a name="settings-apply-to-user-approved-automated-device-enrollment"></a>Die Einstellungen gelten für: Vom Benutzer genehmigte und automatische Geräteregistrierung

- **Außerkraftsetzungen durch Benutzer zulassen:** Die Einstellung **Zulassen** ermöglicht es Benutzern, Kernelerweiterungen zu genehmigen, die nicht im Konfigurationsprofil enthalten sind. Die Einstellung **Nicht konfiguriert** (Standardeinstellung) verhindert, dass Benutzer Erweiterungen zulassen, die nicht im Konfigurationsprofil enthalten sind. Dies bedeutet, dass nur im Profil enthaltene Erweiterungen genehmigt sind.

  Weitere Informationen zu diesem Feature finden Sie unter [Vom Benutzer genehmigtes Laden von Kernelerweiterungen](https://developer.apple.com/library/archive/technotes/tn2459/_index.html) (Apple-Website).

- **Zulässige Team-IDs:** Verwenden Sie diese Einstellung, um mindestens eine Team-ID zuzulassen. Jede Kernelerweiterung, die mit den von Ihnen eingegebenen Team-IDs signiert ist, werden zugelassen und gelten als vertrauenswürdig. Mit anderen Worten: Mit dieser Option können Sie alle Kernelerweiterungen mit einer einzelnen Team-ID zulassen. Diese ID kann z. B. einem bestimmten Entwickler oder Partner gehören.

  Mit **Hinzufügen** können Sie eine Team-ID einer gültigen und signierten Kernelerweiterung hinzufügen, die Sie laden möchten. Sie können mehrere Team-IDs hinzufügen. Die Team-ID muss alphanumerisch sein (d. h. aus Buchstaben und Zahlen bestehen) und 10 Zeichen haben. Geben Sie beispielsweise `ABCDE12345` ein.

  Nachdem Sie eine Team-ID hinzugefügt haben, kann diese auch gelöscht werden.

  Weitere Informationen finden Sie unter [Ermitteln Ihrer Team-ID](https://help.apple.com/developer-account/#/dev55c3c710c) (Apple-Website).

- **Zulässige Kernelerweiterungen:** Mit dieser Einstellung können Sie bestimmte Kernelerweiterungen zulassen. Nur Kernelerweiterungen, die Sie eingeben, sind zulässig oder vertrauenswürdig.

  Mit der Option **Hinzufügen** können Sie die Bundle-ID und die Team-ID einer Kernelerweiterung hinzufügen, die Sie laden möchten. Für unsignierte Legacykernelerweiterungen können Sie eine leere Team-ID verwenden. Sie können mehrere Kernelerweiterungen hinzufügen. Die Team-ID muss alphanumerisch sein (d. h. aus Buchstaben und Zahlen bestehen) und 10 Zeichen haben. Geben Sie beispielweise `com.contoso.appname.macos` für **Bundle-ID** und `ABCDE12345` für **Team-ID** ein.

  > [!TIP]
  > Zum Abrufen der Bundle-ID einer Kernelerweiterung (Kext) auf einem macOS-Gerät können Sie wie folgt vorgehen:
  >
  > 1. Führen Sie im Terminal `kextstat | grep -v com.apple` aus, und notieren Sie sich die Ausgabe. Installieren Sie die gewünschte Software oder Kernelerweiterung (Kext). Führen Sie noch einmal `kextstat | grep -v com.apple` aus, und suchen Sie nach Änderungen.
  >
  >    Mit `kextstat` werden im Terminal alle unter dem Betriebssystem vorhandenen Kernelerweiterungen aufgelistet. 
  >
  > 2. Öffnen Sie auf dem Gerät die Datei „Information Property List“ (Info.plist) für eine Kernelerweiterung. Die Bundle-ID wird angezeigt. In jeder Kernelerweiterung ist eine Info.plist-Datei gespeichert.

> [!NOTE]
> Sie müssen nicht Team-IDs und Kernelerweiterungen hinzufügen. Es genügt, wenn Sie eines von beiden konfigurieren.

## <a name="next-steps"></a>Nächste Schritte

[Zuweisen von Profilen](device-profile-assign.md) und [Überwachen von Profilen](device-profile-monitor.md)
