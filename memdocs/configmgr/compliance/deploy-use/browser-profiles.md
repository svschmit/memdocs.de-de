---
title: Konfigurieren von Microsoft Edge-Einstellungen
titleSuffix: Configuration Manager
description: Konfigurieren von Einstellungen für den Webbrowser Microsoft Edge Legacy auf Windows 10-Clients
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 06/02/2020
ms.topic: how-to
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.openlocfilehash: deededfe18275837ae93859c4075837eac870c35
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694779"
---
# <a name="configure-microsoft-edge-legacy-settings-in-configuration-manager"></a>Konfigurieren von Microsoft Edge Legacy-Einstellungen in Configuration Manager

> [!IMPORTANT]
> Wenn Sie Microsoft Edge ab Version 77 verwenden und versuchen, den Einstellungsbereich zu öffnen, geben Sie `edge://settings/profiles` in die Adressleiste des Browsers statt in die Suchfunktion ein. Weitere Informationen finden Sie unter [Kennenlernen von Microsoft Edge](https://support.microsoft.com/help/17171/microsoft-edge-get-to-know).
>
> Dieser Artikel richtet sich an IT-Experten, die Microsoft Edge Legacy-Einstellungen mit Microsoft Endpoint Configuration Manager verwalten.

*Gilt für: Configuration Manager (Current Branch)*

<!-- 1357310 -->
Kunden, die den Webbrowser [Microsoft Edge Legacy](/microsoft-edge/deploy/) auf Windows 10-Clients nutzen, erstellen eine Configuration Manager-Konformitätsrichtlinie, um die Browsereinstellungen zu konfigurieren.

Diese Richtlinie gilt nur für Clients unter Windows 10 ab Version 1703 und Microsoft Edge Legacy ab Version 45. <!--511552-->

Weitere Informationen zum Verwalten von Microsoft Edge ab Version 77 mit Configuration Manager finden Sie unter [Bereitstellen von Microsoft Edge, Version 77 oder höher](../../apps/deploy-use/deploy-edge.md). Weitere Informationen zum Konfigurieren von Richtlinien für Microsoft Edge ab Version 77 finden Sie unter [Microsoft Edge-Richtlinien](/DeployEdge/microsoft-edge-policies).

## <a name="policy-settings"></a>Richtlinieneinstellungen

Diese Richtlinie umfasst derzeit die folgenden Einstellungen:

- **Microsoft Edge-Browser als Standard** festlegen: Konfiguriert die Windows 10-Standard-App-Einstellung für Webbrowser auf Microsoft.

- **Dropdownliste in Adressleiste zulassen:** Erfordert Windows 10, Version 1703 oder höher. Weitere Informationen finden Sie unter der [AllowAddressBarDropdown-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-allowaddressbardropdown).

- **Das Synchronisieren von Favoriten zwischen Microsoft-Browsern zulassen:** Erfordert Windows 10, Version 1703 oder höher. Weitere Informationen finden Sie unter der [SyncFavoritesBetweenIEAndMicrosoftEdge-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-syncfavoritesbetweenieandmicrosoftedge).

- **Das Löschen von Browserdaten beim Beenden zulassen:** Erfordert Windows 10, Version 1703 oder höher. Weitere Informationen finden Sie unter der [ClearBrowsingDataOnExit-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-clearbrowsingdataonexit).

- **DNT-Kopfzeilen zulassen:** Weitere Informationen finden Sie unter [AllowDoNotTrack-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-allowdonottrack).

- **AutoAusfüllen zulassen:** Weitere Informationen finden Sie unter [AllowAutofill-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-allowautofill).

- **Cookies zulassen:** Weitere Informationen finden Sie unter [AllowCookies-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-allowcookies).

- **Popupblocker zulassen:** Weitere Informationen finden Sie unter [AllowPopups-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-allowpopups).

- **Suchvorschläge in Adressleiste zulassen:** Weitere Informationen finden Sie unter [AllowSearchSuggestionsinAddressBar-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-allowsearchsuggestionsinaddressbar).

- **Senden von Intranetdatenverkehr an Internet Explorer zulassen:** Weitere Informationen finden Sie unter [SendIntranetTraffictoInternetExplorer-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-sendintranettraffictointernetexplorer).

- **Kennwort-Manager zulassen:** Weitere Informationen finden Sie unter [AllowPasswordManager-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager).

- **Entwicklertools zulassen:** Weitere Informationen finden Sie unter [AllowDeveloperTools-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-allowdevelopertools).

- **Erweiterungen zulassen:** Weitere Informationen finden Sie unter [AllowExtensions-Browserrichtlinie](/windows/client-management/mdm/policy-csp-browser#browser-allowextensions).

> [!TIP]
> Weitere Informationen zum Konfigurieren dieser und anderer Einstellungen mithilfe von Gruppenrichtlinien finden Sie unter [Microsoft Edge Legacy-Gruppenrichtlinien](/microsoft-edge/deploy/group-policies/).

### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge-legacy"></a>Konfigurieren von Windows Defender SmartScreen-Einstellungen für Microsoft Edge Legacy
<!--1353701-->
Diese Richtlinie fügt drei Einstellungen für [Windows Defender-SmartScreen](/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview) hinzu. Die Richtlinie enthält nun die folgenden zusätzlichen Einstellungen auf der Seite **SmartScreen-Einstellungen**:

- **SmartScreen zulassen:** Gibt an, ob Windows Defender SmartScreen zugelassen wird. Weitere Informationen finden Sie unter [AllowSmartScreen browser policy (Browserrichtlinie „AllowSmartScreen“)](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen).

- **Benutzer können SmartScreen-Aufforderung für Websites außer Kraft setzen:** Gibt an, ob Benutzer die Windows Defender SmartScreen-Filterwarnungen zu potenziell schädlichen Websites außer Kraft setzen können. Weitere Informationen finden Sie unter [PreventSmartScreenPromptOverride browser policy (Browserrichtlinie „PreventSmartScreenPromptOverride“)](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride).

- **Benutzer können SmartScreen-Aufforderung für Dateien außer Kraft setzen:** Gibt an, ob Benutzer die Windows Defender SmartScreen-Filterwarnungen zum Herunterladen nicht überprüfter Dateien außer Kraft setzen können. Weitere Informationen finden Sie unter [PreventSmartScreenPromptOverride browser policy (Browserrichtlinie „PreventSmartScreenPromptOverrideForFiles“)](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles).

## <a name="create-the-browser-profile"></a>Erstellen des Browserprofils

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**. Erweitern Sie die **Konformitätseinstellungen**, und klicken Sie auf den Knoten **Microsoft Edge-Profile**. Wählen Sie auf dem Menüband **Microsoft Edge-Profil erstellen** aus.

2. Geben Sie einen **Namen** für die Richtlinie und optional eine **Beschreibung** ein, und wählen Sie **Weiter** aus.

3. Ändern Sie auf der Seite **Allgemeine Einstellungen** den Wert für die Einstellungen, die in diese Richtlinie einbezogen werden sollen, in **Konfiguriert**. Um im Assistenten fortfahren zu können, muss die Einstellung mit **Microsoft Edge-Browser als Standard festlegen** konfiguriert werden.

4. Konfigurieren Sie Einstellungen auf der Seite **SmartScreen-Einstellungen**.

5. Wählen Sie auf der Seite **Unterstützte Plattformen** die Betriebssystemversionen und -architekturen aus, für die diese Richtlinie gelten soll.

6. Schließen Sie den Assistenten ab.

## <a name="deploy-the-policy"></a>Bereitstellen der Richtlinie

1. Wählen Sie Ihre Richtlinie und dann auf dem Menüband **Bereitstellen** aus.

2. Wählen Sie **Durchsuchen** aus, um die Benutzer- oder Gerätesammlung auszuwählen, für die die Richtlinie bereitgestellt werden soll.

3. Wählen Sie nach Bedarf weitere Optionen aus:

    1. Generieren Sie Warnungen, wenn die Richtlinie nicht konform ist.

    2. Legen Sie den Zeitplan fest, nach dem der Client die Konformität des Geräts mit dieser Richtlinie auswertet.

4. Wählen Sie **OK** aus, um die Bereitstellung zu erstellen.

## <a name="next-steps"></a>Nächste Schritte

Wie bei jeder anderen Richtlinie für Konformitätseinstellungen gleicht der Client die Einstellungen gemäß dem von Ihnen angegebenen Zeitplan ab. In der Configuration Manager-Konsole können Sie die [Gerätekonformität überwachen und Berichte anzeigen](monitor-compliance-settings.md).