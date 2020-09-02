---
title: Verwenden der Windows Defender-Anwendungssteuerung auf HoloLens 2-Geräten in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Konfigurieren Sie den WDAC-CSP (Windows Defender Application Control, Windows Defender-Anwendungssteuerung), um das Öffnen von Apps auf HoloLens 2-Geräten in Microsoft Intune zu erlauben oder zu blockieren. Verwenden Sie PowerShell und ein benutzerdefiniertes Konfigurationsprofil.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/20/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f4a1929749c5921714078ec54ac687f4cefe1474
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915873"
---
# <a name="use-wdac-and-windows-powershell-to-allow-or-blocks-apps-on-hololens-2-devices-with-microsoft-intune"></a>Verwenden von WDAC und Windows PowerShell, um Apps auf HoloLens 2-Geräten mit Microsoft Intune zuzulassen oder zu blockieren

Microsoft HoloLens 2-Geräte unterstützen den [WDAC-CSP (Windows Defender Application Control, Windows Defender-Anwendungssteuerung)](/windows/client-management/mdm/applicationcontrol-csp), der den [AppLocker CSP](/windows/client-management/mdm/applocker-csp) ersetzt.

Mithilfe von Windows PowerShell und Microsoft Intune können Sie mithilfe den WDAC-CSP verwenden, um zuzulassen oder zu blockieren, dass bestimmte Apps auf Microsoft HoloLens 2-Geräten geöffnet werden. Beispielsweise möchten Sie möglicherweise zulassen oder verhindern, dass die Cortana-App auf HoloLens 2-Geräten in Ihrer Organisation geöffnet wird.

Diese Funktion gilt für:

- HoloLens 2-Geräte, auf denen Windows Holographic for Business ausgeführt wird

Der WDAC-CSP basiert auf der [WDAC-Funktion (Windows Defender Application Control, Windows Defender-Anwendungssteuerung)](/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control). Sie können auch [mehrere WDAC-Richtlinien verwenden](/windows/security/threat-protection/windows-defender-application-control/deploy-multiple-windows-defender-application-control-policies).

In diesem Artikel erfahren Sie, wie Sie Folgendes durchführen:

1. Verwenden von Windows PowerShell, um WDAC-Richtlinien zu erstellen.
2. Verwenden von Windows PowerShell zum Konvertieren der WDAC-Richtlinienregeln in XML, Aktualisieren des XML-Codes und anschließendes Konvertieren des XML-Codes in eine Binärdatei.
3. Erstellen eines [benutzerdefinierten Gerätekonfigurationsprofils](custom-settings-windows-holographic.md) in Microsoft Intune, Hinzufügen dieser WDAC-Richtlinienbinärdatei und Anwenden der Richtlinie auf Ihre HoloLens 2-Geräte.

In Intune müssen Sie ein benutzerdefiniertes Konfigurationsprofil erstellen, um den WDAC-CSP (Windows Defender Application Control, Windows Defender-Anwendungssteuerung) zu verwenden. 

Verwenden Sie die Schritte in diesem Artikel als Vorlage, um das Öffnen bestimmter Anwendungen auf HoloLens 2-Geräten zuzulassen oder zu verweigern.

## <a name="prerequisites"></a>Voraussetzungen

- Vertrautheit mit Windows PowerShell.
- Melden Sie sich bei Intune als Mitglied einer der folgenden Rollen an:

  - Intune-Rolle **Richtlinien- und Profil-Manager** oder **Intune-Rollenadministrator**

    ODER

  - Azure AD-Rolle **Globaler Administrator** oder **Intune-Dienstadministrator**

  Weitere Informationen finden Sie unter [Rollenbasierte Zugriffssteuerung (RBAC) mit Intune](../fundamentals/role-based-access-control.md).

- Erstellen Sie eine Benutzergruppe oder eine Gerätegruppe mit Ihren HoloLens 2-Geräten. Weitere Informationen finden Sie unter [Benutzer- und Gerätegruppen im Vergleich](device-profile-assign.md#user-groups-vs-device-groups).

## <a name="example"></a>Beispiel

In diesem Beispiel wird Windows PowerShell verwendet, um eine WDAC-Richtlinie (Windows Defender Application Control, Windows Defender-Anwendungssteuerung) zu erstellen. Die Richtlinie verhindert, dass bestimmte Apps geöffnet werden. Verwenden Sie anschließend Intune, um die Richtlinie für HoloLens 2-Geräte bereitzustellen.

1. Öffnen Sie auf dem Desktopcomputer die App **Windows PowerShell**.
2. Rufen Sie Informationen zum installierten Anwendungspaket auf Ihrem Desktopcomputer ab:

    ```powershell
    $package1 = Get-AppxPackage -name *<applicationname>*
    ```

    Geben Sie z. B. Folgendes ein:

    ```powershell
    $package1 = Get-AppxPackage -name *cortana*
    ```

    Vergewissern Sie sich anschließend, dass das Paket über Anwendungsattribute verfügt:

    ```powershell
    $package1
    ```

    Ihnen werden ähnliche Attribute wie in den folgenden App-Details angezeigt:

    ```powershell
    Name              : Microsoft.Windows.Cortana
    Publisher         : CN=Microsoft Windows, O=Microsoft Corporation, L=Redmond, S=Washington, C=US
    Architecture      : Neutral
    ResourceId        : neutral
    Version           : 1.13.0.18362
    PackageFullName   : Microsoft.Windows.Cortana_1.13.0.18362_neutral_neutral_cw5n1h2txyewy
    InstallLocation   : C:\Windows\SystemApps\Microsoft.Windows.Cortana_cw5n1h2txyewy
    IsFramework       : False
    PackageFamilyName : Microsoft.Windows.Cortana_cw5n1h2txyewy
    PublisherId       : cw5n1h2txyewy
    IsResourcePackage : False
    IsBundle          : False
    IsDevelopmentMode : False
    NonRemovable      : True
    IsPartiallyStaged : False
    SignatureKind     : System
    Status            : Ok
    ```

3. Erstellen Sie eine WDAC-Richtlinie, und fügen Sie das App-Paket der DENY-Regel hinzu:

    ```powershell
    $rule = New-CIPolicyRule -Package $package1 -Deny
    ```

4. Wiederholen Sie die Schritte 2 und 3 für alle anderen Anwendungen, die Sie verweigern möchten:

    ```powershell
    $rule += New-CIPolicyRule -Package $package<2..n> -Deny
    ```

    Geben Sie z. B. Folgendes ein:

    ```powershell
    $package2 = Get-AppxPackage -name *windowsstore*
    $rule += New-CIPolicyRule -Package $package<2..n>  -Deny
    ```

5. Konvertieren Sie die WDAC-Richtlinie in **newPolicy.xml**:

    ```powershell
    New-CIPolicy -rules $rule -f .\newPolicy.xml -UserPEs
    ```

    Um alle Versionen einer App als Ziel zu verwenden, stellen Sie in „newPolicy.xml“ sicher, dass sich `PackageVersion="65535.65535.65535.65535"` im Knoten „Deny“ befindet:

    ```xml
    <Deny ID="ID_DENY_D_1" FriendlyName="Microsoft.WindowsStore_8wekyb3d8bbwe FileRule" PackageFamilyName="Microsoft.WindowsStore_8wekyb3d8bbwe" PackageVersion="65535.65535.65535.65535" />
    ```

    Für `PackageFamilyNameRules` können Sie die folgenden Versionen verwenden:

    - **Zulassen:** Geben Sie `PackageVersion, 0.0.0.0` ein („Diese Version und alle höheren Versionen zulassen“).
    - **Verweigern**: Geben Sie `PackageVersion, 65535.65535.65535.65535` ein („Diese Version und alle früheren Versionen verweigern“).

6. Mergen Sie **newPolicy.xml** mit der Standardrichtlinie auf Ihrem Desktopcomputer. In diesem Schritt wird **mergedPolicy.xml** erstellt. Gestatten Sie z. B. das Ausführen von Windows-Apps, von WHQL-signierten Treibern und vom Store signierten Apps:

    ```powershell
    Merge-CIPolicy -PolicyPaths .\newPolicy.xml,C:\Windows\Schemas\codeintegrity\examplepolicies\DefaultWindows_Audit.xml -o mergedPolicy.xml
    ```

7. Deaktivieren Sie die Regel **Überwachungsmodus** in **mergedPolicy.xml**. Wenn Sie mergen, wird der Überwachungsmodus automatisch aktiviert:

    ```powershell
    Set-RuleOption -o 3 -Delete .\mergedPolicy.xml
    ```

8. Aktivieren Sie die Regel **InvalidateEAs beim Neustart** in **mergedPolicy.xml**:

    ```powershell
    Set-RuleOption -o 15 .\mergedPolicy.xml
    ```

    Weitere Informationen zu diesen Regeln finden Sie unter [Verstehen von WDAC-Richtlinienregeln und -Dateiregeln](/windows/security/threat-protection/windows-defender-application-control/select-types-of-rules-to-create).

9. Konvertieren Sie **mergedPolicy.xml** in das Binärformat. Mit diesem Schritt wird **compiledPolicy.bin** erstellt. Sie fügen diese **compiledPolicy.bin**-Binärdatei Intune hinzu.

    ```powershell
    ConvertFrom-CIPolicy .\mergedPolicy.xml .\compiledPolicy.bin
    ```

10. Erstellen Sie das benutzerdefinierte Gerätekonfigurationsprofil in Intune:

    1. Erstellen Sie in [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) ein benutzerdefiniertes Windows 10-Gerätekonfigurationsprofil.

        Informationen zu den einzelnen Schritten finden Sie unter [Erstellen eines benutzerdefinierten Profils mit dem OMA-URI in Intune](custom-settings-configure.md).

    2. Wenn Sie das Profil erstellen, geben Sie die folgenden Einstellungen ein:

      - **OMA-URI**: Geben Sie `./Vendor/MSFT/ApplicationControl/Policies/<PolicyGUID>` ein. Ersetzen Sie `<PolicyGUID>` durch den Knoten PolicyTypeID in der Datei **mergedPolicy.xml**, die Sie in Schritt 6 erstellt haben.

        Geben Sie in unserem Beispiel `./Vendor/MSFT/ApplicationControl/Policies/A244370E-44C9-4C06-B551-F6016E563076` ein.

        Die Richtlinien-GUID muss mit dem Knoten PolicyTypeID in der Datei **mergedPolicy.xml** **übereinstimmen** (die Sie in Schritt 6 erstellt haben).

      - **Datentyp:** Legen Sie den Typ auf **Base64-Datei** fest. Die Datei wird automatisch aus „bin“ in „base64“ konvertiert.
      - **Zertifikatdatei**: Laden Sie die Binärdatei **compiledPolicy.bin** (erstellt in Schritt 9) hoch.

      Ihre Einstellungen sehen ähnlich aus wie die folgenden:

      :::image type="content" source="./media/custom-profile-hololens/custom-applicationcontrol-omauri.png" alt-text="Fügen Sie einen benutzerdefinierten OMA-URI hinzu, um den ApplicationControl-CSP in Microsoft Intune zu konfigurieren.":::

11. Wenn das Profil der Gruppe HoloLens 2 [zugewiesen](device-profile-assign.md) wird, überprüfen Sie den Profilstatus. Nachdem das Profil erfolgreich angewendet wurde, starten Sie die HoloLens 2-Geräte neu.

## <a name="next-steps"></a>Nächste Schritte

[Weisen Sie das Profil zu](device-profile-assign.md), und [überwachen Sie dessen Status](device-profile-monitor.md).

Weitere Informationen zu [benutzerdefinierten Profilen in Intune](custom-settings-configure.md).