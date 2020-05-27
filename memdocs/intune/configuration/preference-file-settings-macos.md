---
title: 'Hinzufügen von Einstellungsdatei-Einstellungen für macOS-Geräte in Microsoft Intune: Azure | Microsoft-Dokumentation'
titleSuffix: ''
description: Fügen Sie eine XML- oder PLIST-Datei hinzu, die Schlüsselinformationen zu Ihrer App enthält. Verwenden Sie ein Einstellungsdatei-Gerätekonfigurationsprofil, um Schlüsselinformationen in der Eigenschaftenlistendatei zu ändern, und weisen Sie diese Ihren macOS-Geräten zu.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/05/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: ebf65ecc6dbe5059adbd6fec70833bf2fcab9de7
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83988671"
---
# <a name="add-a-property-list-file-to-macos-devices-using-microsoft-intune"></a>Hinzufügen einer Eigenschaftenlistendatei zu macOS-Geräten mit Microsoft Intune

Mit Microsoft Intune können Sie eine Eigenschaftenlistendatei (.plist) für macOS-Geräte oder Apps auf macOS-Geräten hinzufügen.

Diese Funktion gilt für:

- macOS 10.7 und höher

Eigenschaftenlistendateien beinhalten Informationen zu macOS-Anwendungen. Weitere Informationen finden Sie unter [Informationen zu Informationseigenschaftenlisten-Dateien](https://developer.apple.com/library/archive/documentation/General/Reference/InfoPlistKeyReference/Articles/AboutInformationPropertyListFiles.html) (Website von Apple) und [Eigene Payload-Einstellungen](https://support.apple.com/guide/mdm/custom-mdm9abbdbe7/1/web/1).

In diesem Artikel werden die verschiedenen Einstellungen für Eigenschaftenlistendateien aufgeführt und beschrieben, die Sie für macOS-Geräte hinzufügen können. Verwenden Sie diese Einstellungen als Bestandteil Ihrer Lösung für die mobile Geräteverwaltung (Mobile Device Management, MDM), um die App-Bundle-ID (`com.company.application`) hinzuzufügen, und fügen Sie die PLIST-Datei der App hinzu.

Diese Einstellungen werden einem Gerätekonfigurationsprofil in Intune hinzugefügt und dann Ihren macOS-Geräten zugewiesen oder bereitgestellt.

## <a name="what-you-need-to-know"></a>Was Sie wissen müssen

- Diese Einstellungen werden nicht überprüft. Stellen Sie sicher, dass Sie Ihre Änderungen testen, bevor Sie das Profil Ihren Geräten zuweisen.
- Wenn Sie nicht sicher sind, wie Sie einen App-Schlüssel eingeben, ändern Sie die Einstellungen in der App. Überprüfen Sie anschließend die Einstellungsdatei der App mit [Xcode](https://developer.apple.com/xcode/), um zu sehen, wie die Einstellung konfiguriert ist. Apple empfiehlt, nicht verwaltbare Einstellungen mit Xcode vor dem Importieren der Datei zu entfernen.
- Nur manche Apps arbeiten mit verwalteten Einstellungen, und selbst bei diesen Apps können Sie möglicherweise nicht alle Einstellungen verwalten.
- Stellen Sie sicher, dass Sie Eigenschaftenlistendateien hochladen, die die Gerätekanaleinstellungen und nicht die Benutzerkanaleinstellungen konfigurieren. Eigenschaftenlistendateien beziehen sich auf das gesamte Gerät.

## <a name="create-the-profile"></a>Erstellen des Profils

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.
3. Geben Sie die folgenden Eigenschaften ein:

    - **Plattform**: Wählen Sie **macOS** aus.
    - **Profil**: Klicken Sie auf **Einstellungsdatei**.

4. Wählen Sie **Erstellen** aus.
5. Geben Sie in **Grundlagen** die folgenden Eigenschaften ein:

    - **Name:** Geben Sie einen aussagekräftigen Namen für die Richtlinie ein. Benennen Sie Ihre Richtlinien so, dass Sie diese später leicht wiedererkennen. Ein guter Richtlinienname ist beispielsweise **macOS: Einstellungsdatei zum Konfigurieren von Microsoft Defender ATP auf Geräten hinzufügen**.
    - **Beschreibung:** Geben Sie eine Beschreibung für die Richtlinie ein. Diese Einstellung ist optional, wird jedoch empfohlen.

6. Wählen Sie **Weiter** aus.

7. Konfigurieren Sie Ihre Einstellungen in den **Konfigurationseinstellungen**:

    - **Name der bevorzugten Domäne:** Geben Sie die Bundle-ID ein, z. B. `com.company.application`. Geben Sie beispielsweise `com.Contoso.applicationName`, `com.Microsoft.Edge` oder `com.microsoft.wdav` ein.

      Eigenschaftenlistendateien werden üblicherweise für Webbrowser (Microsoft Edge), [Microsoft Defender Advanced Threat Protection](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac) und benutzerdefinierte Apps verwendet. Wenn Sie eine bevorzugte Domäne erstellen, wird auch eine Bundle-ID erstellt.

    - **Datei mit Eigenschaftenliste:** Wählen Sie die mit Ihrer App verknüpfte Eigenschaftenlistendatei aus. Stellen Sie sicher, dass es sich dabei um eine `.plist`- oder `.xml`-Datei handelt. Laden Sie z. B. eine Datei mit dem Namen `YourApp-Manifest.plist` oder `YourApp-Manifest.xml` hoch.

      Die Schlüsselinformationen in der Eigenschaftenlistendatei werden angezeigt. Wenn Sie die Schlüsselinformationen ändern müssen, öffnen Sie die Listendatei in einem anderen Editor, und laden Sie die Datei noch mal in Intune hoch.

    Stellen Sie sicher, dass Ihre Datei richtig formatiert ist. Die Datei sollte nur Schlüssel-Wert-Paare enthalten und nicht in `<dict>`-, `<plist>`- oder `<xml>`-Tags eingeschlossen sein. Ihre Eigenschaftenlistendatei sollte z. B. ähnlich aussehen wie die folgende Datei:

    ```xml
    <key>SomeKey</key>
    <string>someString</string>
    <key>AnotherKey</key>
    <false/>
    ...
    ```

8. Wählen Sie **Weiter** aus.
9. Weisen Sie in **Bereichstags** (optional) ein Tag zu, um das Profil nach bestimmten IT-Gruppen wie `US-NC IT Team` oder `JohnGlenn_ITDepartment` zu filtern. Weitere Informationen zu Bereichstags finden Sie unter [Verwenden der RBAC und von Bereichstags für verteilte IT](../fundamentals/scope-tags.md).

    Wählen Sie **Weiter** aus.

10. Wählen Sie unter **Zuweisungen** die Benutzer oder Gruppen aus, denen Ihr Profil zugewiesen werden soll. Weitere Informationen zum Zuweisen von Profilen finden Sie unter [Zuweisen von Benutzer- und Geräteprofilen](device-profile-assign.md).

    Wählen Sie **Weiter** aus.

11. Überprüfen Sie die Einstellungen unter **Überprüfen + erstellen**. Wenn Sie auf **Erstellen** klicken, werden die Änderungen gespeichert, und das Profil wird zugewiesen. Die Richtlinie wird auch in der Profilliste angezeigt.

## <a name="next-steps"></a>Nächste Schritte

[Zuweisen von Profilen](device-profile-assign.md) und [Überwachen von Profilen](device-profile-monitor.md)

Weitere Informationen zu Einstellungsdateien für Microsoft Edge finden Sie unter [Konfigurieren der Microsoft Edge-Richtlinieneinstellungen für macOS mithilfe einer Eigenschaftsliste (.plist)](https://docs.microsoft.com/deployedge/configure-microsoft-edge-on-mac).
