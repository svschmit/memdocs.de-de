---
title: macOS-Erweiterungseinstellungen in Microsoft Intune – Azure | Microsoft-Dokumentation
titleSuffix: ''
description: Hinzufügen, Konfigurieren oder Erstellen von Einstellungen auf macOS-Geräten, um System- und Kernelerweiterungen zu verwenden. Außerdem wird beschrieben, wie Sie in Microsoft Intune Benutzern das Überschreiben genehmigter Erweiterungen ermöglichen und alle Erweiterungen einer Team-ID, bestimmte Erweiterungen oder bestimmte Apps zulassen.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/12/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 8b716a7e85f817e95a9f1fec992458e052570d81
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83429512"
---
# <a name="macos-device-settings-to-configure-and-use-kernel-and-system-extensions-in-intune"></a>macOS-Geräteeinstellungen zum Konfigurieren und Verwenden von Kernel- und Systemerweiterungen in Intune

> [!NOTE]
> macOS-Kernelerweiterungen werden durch Systemerweiterungen ersetzt. Weitere Informationen finden Sie unter [Tipp zur Unterstützung: Verwenden von Systemerweiterungen anstelle von Kernelerweiterungen für macOS Catalina 10.15 in Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/support-tip-using-system-extensions-instead-of-kernel-extensions/ba-p/1191413).

In diesem Artikel werden die verschiedenen Einstellungen für Kernel- und Systemerweiterungen aufgeführt und beschrieben, die Sie auf macOS-Geräten steuern können. Mit diesen Einstellungen Ihrer Lösung für die mobile Geräteverwaltung (Mobile Device Management, MDM) können Sie Erweiterungen auf Ihren Geräten hinzufügen und verwalten.

Weitere Informationen zu Erweiterungen in Intune und deren Anforderungen finden Sie unter [Hinzufügen von macOS-Erweiterungen in Intune](kernel-extensions-overview-macos.md).

Diese Einstellungen werden einem Gerätekonfigurationsprofil in Intune hinzugefügt und dann Ihren macOS-Geräten zugewiesen oder bereitgestellt.

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen Sie ein macOS- Erweiterungskonfigurationsprofil.](kernel-extensions-overview-macos.md)

> [!NOTE]
> Diese Einstellungen gelten für verschiedene Registrierungstypen. Weitere Informationen zu den verschiedenen Registrierungstypen finden Sie unter [macOS-Registrierung](../enrollment/macos-enroll.md).

## <a name="kernel-extensions"></a>Kernelerweiterungen

Diese Funktion gilt für:

- macOS 10.13.2 und höher
- Vom Benutzer genehmigte Geräteregistrierung ist erforderlich 

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment"></a>Die Einstellungen gelten für: Vom Benutzer genehmigte Geräteregistrierung, automatisierte Geräteregistrierung

- **Außerkraftsetzungen durch Benutzer zulassen:** **Ja** ermöglicht es Benutzern, Kernelerweiterungen zu genehmigen, die nicht im Konfigurationsprofil enthalten sind. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig verhindert das Betriebssystem, dass Benutzer Erweiterungen zulassen, die nicht im Konfigurationsprofil enthalten sind. Dies bedeutet, dass nur im Profil enthaltene Erweiterungen genehmigt sind.

  Weitere Informationen zu diesem Feature finden Sie unter [Vom Benutzer genehmigtes Laden von Kernelerweiterungen](https://developer.apple.com/library/archive/technotes/tn2459/_index.html) (Website von Apple).

- **Zulässige Team-IDs:** Verwenden Sie diese Einstellung, um mindestens eine Team-ID zuzulassen. Jede Kernelerweiterung, die mit den von Ihnen eingegebenen Team-IDs signiert ist, werden zugelassen und gelten als vertrauenswürdig. Mit anderen Worten: Mit dieser Option können Sie alle Kernelerweiterungen mit einer einzelnen Team-ID zulassen. Diese ID kann z. B. einem bestimmten Entwickler oder Partner gehören.

  Mit **Hinzufügen** können Sie eine Team-ID einer gültigen und signierten Kernelerweiterung hinzufügen, die geladen werden soll. Sie können mehrere Team-IDs hinzufügen. Die Team-ID muss alphanumerisch sein (d. h. aus Buchstaben und Zahlen bestehen) und 10 Zeichen haben. Geben Sie beispielsweise `ABCDE12345` ein.

  Nachdem Sie eine Team-ID hinzugefügt haben, kann diese auch gelöscht werden.

  Weitere Informationen finden Sie unter [Ermitteln Ihrer Team-ID](https://help.apple.com/developer-account/#/dev55c3c710c) (Apple-Website).

- **Zulässige Kernelerweiterungen:** Mit dieser Einstellung können Sie bestimmte Kernelerweiterungen zulassen. Nur Kernelerweiterungen, die Sie eingeben, sind zulässig oder vertrauenswürdig.

  Mit der Option **Hinzufügen** können Sie die Bundle-ID und die Team-ID einer Kernelerweiterung hinzufügen, die geladen werden soll. Für unsignierte Legacykernelerweiterungen können Sie eine leere Team-ID verwenden. Sie können mehrere Kernelerweiterungen hinzufügen. Die Team-ID muss alphanumerisch sein (d. h. aus Buchstaben und Zahlen bestehen) und 10 Zeichen haben. Geben Sie beispielweise `com.contoso.appname.macos` für **Bundle-ID** und `ABCDE12345` für **Team-ID** ein.

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

## <a name="system-extensions"></a>Systemerweiterungen

Diese Funktion gilt für:

- macOS 10.15 und neuer
- Vom Benutzer genehmigte Geräteregistrierung ist erforderlich

### <a name="settings-apply-to-user-approved-device-enrollment-automated-device-enrollment"></a>Die Einstellungen gelten für: Vom Benutzer genehmigte Geräteregistrierung, automatisierte Geräteregistrierung

- **Außerkraftsetzungen durch Benutzer blockieren**: **Ja** verhindert, dass Benutzer Systemerweiterungen genehmigen, die nicht in der Zulassungsliste enthalten sind. Wenn die Standardeinstellung **Nicht konfiguriert** festgelegt ist, wird diese Einstellung nicht von Intune geändert oder aktualisiert. Standardmäßig erlaubt das Betriebssystem ggf., dass Benutzer Erweiterungen genehmigen, die nicht im Konfigurationsprofil enthalten sind. Dies bedeutet, dass nicht im Konfigurationsprofil enthaltene Erweiterungen zulässig sind.

- **Zulässige Team-IDs**: Verwenden Sie diese Einstellung, um mindestens eine Team-ID zuzulassen. Jede Systemerweiterung, die mit den von Ihnen eingegebenen Team-IDs signiert ist, wird immer zugelassen und gilt als vertrauenswürdig. Mit anderen Worten: Mit dieser Option können Sie alle Systemerweiterungen mit einer einzelnen Team-ID zulassen. Diese ID kann z. B. einem bestimmten Entwickler oder Partner gehören.

  Mit **Hinzufügen** können Sie eine **Team-ID** einer gültigen und signierten Systemerweiterung hinzufügen, die geladen werden soll. Sie können mehrere Team-IDs hinzufügen. Die Team-ID muss alphanumerisch sein (d. h. aus Buchstaben und Zahlen bestehen) und 10 Zeichen haben. Geben Sie beispielsweise `ABCDE12345` ein.

  Nachdem Sie eine Team-ID hinzugefügt haben, kann diese auch gelöscht werden.

  Weitere Informationen finden Sie unter [Ermitteln Ihrer Team-ID](https://help.apple.com/developer-account/#/dev55c3c710c) (Apple-Website).

- **Zulässige Systemerweiterungen**: Mit dieser Einstellung können Sie bestimmte Systemerweiterungen immer zulassen. Nur Systemerweiterungen, die Sie eingeben, sind zulässig oder vertrauenswürdig.

  Mit der Option **Hinzufügen** können Sie die **Paket-ID** und die **Team-ID** einer Systemerweiterung hinzufügen, die geladen werden soll. Für unsignierte Legacysystemerweiterungen können Sie eine leere Team-ID verwenden. Sie können mehrere Systemerweiterungen hinzufügen. Die Team-ID muss alphanumerisch sein (d. h. aus Buchstaben und Zahlen bestehen) und 10 Zeichen haben. Geben Sie beispielweise `com.contoso.appname.macos` für **Bundle-ID** und `ABCDE12345` für **Team-ID** ein.

- **Zulässige Systemerweiterungstypen**: Geben Sie die Team-ID und die Systemerweiterungstypen ein, die für diese Team-ID zulässig sein sollen:
  - **Team-ID**: Geben Sie die Team-ID einer anderen Systemerweiterung ein, die Sie für bestimmte Erweiterungstypen zulassen möchten. Oder geben Sie eine Team-ID ein, die Sie **Zulässige Systemerweiterungen** hinzugefügt haben.
  - **Zulässige Systemerweiterungstypen**: Wählen Sie die Systemerweiterungstypen aus, die für die einzelnen Team-IDs zulässig sein sollen. Folgende Optionen sind verfügbar:
    - Alles auswählen
    - Treiberweiterungen
    - Netzwerkerweiterungen
    - Endpunktsicherheitserweiterungen

    Weitere Informationen zu diesen Erweiterungstypen finden Sie unter [Systemerweiterungen](https://developer.apple.com/system-extensions/) (Website von Apple).

    Sie können eine Team-ID aus der Liste **Zulässige Systemerweiterungen** hinzufügen und einen bestimmten Erweiterungstyp zulassen. Wenn die Erweiterung ein Typ ist, der unzulässig ist, wird die Erweiterung möglicherweise nicht ausgeführt.

    Um alle Erweiterungstypen für eine Team-ID zuzulassen, fügen Sie die Team-ID der Liste **Zulässige Systemerweiterungen** hinzu. Fügen Sie die Team-ID nicht der Liste **Zulässige Systemerweiterungstypen** hinzu. Anders ausgedrückt: Wenn sich eine Team-ID in der Liste **Zulässige Systemerweiterungen** und nicht in der Liste **Zulässige Systemerweiterungstypen** befindet, sind alle Erweiterungstypen für diese Team-ID zulässig.

> [!NOTE]
> Das Hinzufügen derselben Team-ID für **Zulässige Systemerweiterungen** und **Zulässige Team-IDs** kann zu einem Fehler führen, und das Profil schlägt fehl. Fügen Sie dieselbe Team-ID nicht beiden Einstellungen hinzu. 

## <a name="next-steps"></a>Nächste Schritte

[Zuweisen von Profilen](device-profile-assign.md) und [Überwachen von Profilen](device-profile-monitor.md)
