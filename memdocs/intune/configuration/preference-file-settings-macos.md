---
title: 'Hinzufügen von Einstellungsdatei-Einstellungen für macOS-Geräte in Microsoft Intune: Azure | Microsoft-Dokumentation'
titleSuffix: ''
description: Fügen Sie eine XML- oder PLIST-Datei hinzu, die Schlüsselinformationen zu Ihrer App enthält. Verwenden Sie ein Einstellungsdatei-Gerätekonfigurationsprofil, um Schlüsselinformationen in der Eigenschaftenlistendatei zu ändern, und weisen Sie diese Ihren macOS-Geräten zu.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 01/09/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: d226888c3d710a7b80357ebb92130b34ab2fef94
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79360755"
---
# <a name="add-a-property-list-file-to-macos-devices-using-microsoft-intune"></a>Hinzufügen einer Eigenschaftenlistendatei zu macOS-Geräten mit Microsoft Intune

Mit Microsoft Intune können Sie eine Eigenschaftenlistendatei (.plist) für macOS-Geräte oder Apps auf macOS-Geräten hinzufügen.

Diese Funktion gilt für:

- macOS-Geräte mit Version 10.7 und höher

Eigenschaftenlistendateien beinhalten üblicherweise Informationen zu macOS-Anwendungen. Weitere Informationen finden Sie unter [Informationen zu Informationseigenschaftenlisten-Dateien](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html) (Website von Apple) und [Eigene Payload-Einstellungen](https://support.apple.com/guide/mdm/custom-mdm9abbdbe7/1/web/1).

In diesem Artikel werden die verschiedenen Einstellungen für Eigenschaftenlistendateien aufgeführt und beschrieben, die Sie für macOS-Geräte hinzufügen können. Verwenden Sie diese Einstellungen als Bestandteil Ihrer Lösung für die mobile Geräteverwaltung (Mobile Device Management, MDM), um die App-Bundle-ID (`com.company.application`) hinzuzufügen, und fügen Sie die entsprechende PLIST-Datei hinzu.

Diese Einstellungen werden einem Gerätekonfigurationsprofil in Intune hinzugefügt und dann Ihren macOS-Geräten zugewiesen oder bereitgestellt.

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen Sie das Profil.](device-profile-create.md)

## <a name="what-you-need-to-know"></a>Was Sie wissen müssen

- Diese Einstellungen werden nicht überprüft. Stellen Sie sicher, dass Sie Ihre Änderungen testen, bevor Sie das Profil Ihren Geräten zuweisen.
- Wenn Sie nicht sicher sind, wie Sie einen App-Schlüssel eingeben, ändern Sie die Einstellungen in der App. Überprüfen Sie anschließend die Einstellungsdatei der App mit [Xcode](https://developer.apple.com/xcode/), um zu sehen, wie die Einstellung konfiguriert ist. Apple empfiehlt, nicht verwaltbare Einstellungen mit Xcode vor dem Importieren der Datei zu entfernen.
- Nur manche Apps arbeiten mit verwalteten Einstellungen, und selbst bei diesen Apps können Sie möglicherweise nicht alle Einstellungen verwalten.
- Stellen Sie sicher, dass Sie Eigenschaftenlistendateien hochladen, die die Gerätekanaleinstellungen und nicht die Benutzerkanaleinstellungen konfigurieren. Eigenschaftenlistendateien beziehen sich auf das gesamte Gerät.

## <a name="preference-file"></a>Einstellungsdatei

- **Name der bevorzugten Domäne:** Eigenschaftenlistendateien werden üblicherweise für Webbrowser (Microsoft Edge), [Microsoft Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) und benutzerdefinierte Apps verwendet. Wenn Sie eine bevorzugte Domäne erstellen, wird auch eine Bundle-ID erstellt. Geben Sie die Bundle-ID ein, z. B. `com.company.application`. Geben Sie beispielsweise `com.Contoso.applicationName`, `com.Microsoft.Edge` oder `com.microsoft.wdav` ein.
- **Datei mit Eigenschaftenliste:** Wählen Sie die mit Ihrer App verknüpfte Eigenschaftenlistendatei aus. Stellen Sie sicher, dass es sich dabei um eine `.plist`- oder `.xml`-Datei handelt. Laden Sie z. B. eine Datei mit dem Namen `YourApp-Manifest.plist` oder `YourApp-Manifest.xml` hoch.
- **Dateiinhalte**: Die Schlüsselinformationen in der Eigenschaftenlistendatei werden angezeigt. Wenn Sie die Schlüsselinformationen ändern müssen, öffnen Sie die Listendatei in einem anderen Editor, und laden Sie die Datei noch mal in Intune hoch.

Stellen Sie sicher, dass Ihre Datei richtig formatiert ist. Die Datei sollte nur Schlüssel-Wert-Paare enthalten und nicht in `<dict>`-, `<plist>`- oder `<xml>`-Tags eingeschlossen sein. Ihre Eigenschaftenlistendatei sollte z. B. ähnlich aussehen wie die folgende Datei:

```xml
<key>SomeKey</key>
<string>someString</string>
<key>AnotherKey</key>
<false/>
...
```

Wählen Sie **OK** > **Erstellen** aus, um die Änderungen zu speichern. Das Profil wird erstellt und in der Profilliste angezeigt.

## <a name="next-steps"></a>Nächste Schritte

Das Profil ist nun erstellt, führt aber noch keine Aktionen durch. Die nächsten Schritte sind das [Zuweisen von Benutzer- und Geräteprofilen in Microsoft Intune](device-profile-assign.md) und das [Überwachen von Geräteprofilen in Microsoft Intune](device-profile-monitor.md).

Weitere Informationen zu Einstellungsdateien für Microsoft Edge finden Sie unter [Konfigurieren der Microsoft Edge-Richtlinieneinstellungen für macOS mithilfe einer Eigenschaftsliste (.plist)](https://docs.microsoft.com/deployedge/configure-microsoft-edge-on-mac).
