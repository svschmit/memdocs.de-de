---
title: Konfigurieren von Microsoft Edge-Einstellungen
titleSuffix: Configuration Manager
description: Konfigurieren von Einstellungen für den Microsoft Edge-Webbrowser auf Windows 10-Clients
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.assetid: 76477b4d-df41-4b25-8318-7d18d46ca2c6
ms.openlocfilehash: 4ed49ed3623b34bfb51fd66fafa858ae3951a5af
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906357"
---
# <a name="configure-microsoft-edge-settings-in-configuration-manager"></a>Konfigurieren von Microsoft Edge-Einstellungen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

<!-- 1357310 -->
Kunden, die den [Microsoft Edge](https://www.microsoft.com/itpro/microsoft-edge)-Webbrowser auf Windows 10-Clients verwenden, erstellen ab der Version 1802 eine Richtlinie für Configuration Manager-Konformitätseinstellungen, um verschiedene Microsoft Edge-Einstellungen zu konfigurieren. 

Diese Richtlinie gilt nur für Clients unter Windows 10 ab Version 1703. <!--511552-->


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


### <a name="configure-windows-defender-smartscreen-settings-for-microsoft-edge"></a>Konfigurieren von Windows Defender SmartScreen-Einstellungen für Microsoft Edge
<!--1353701-->
Ab Version 1806 fügt diese Richtlinie drei Einstellungen für [Windows Defender-SmartScreen](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-smartscreen/microsoft-defender-smartscreen-overview) hinzu. Die Richtlinie enthält nun die folgenden zusätzlichen Einstellungen auf der Seite **SmartScreen-Einstellungen**:

- **SmartScreen zulassen:** Gibt an, ob Windows Defender SmartScreen zugelassen wird. Weitere Informationen finden Sie unter [AllowSmartScreen browser policy (Browserrichtlinie „AllowSmartScreen“)](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen).
- **Benutzer können SmartScreen-Aufforderung für Websites außer Kraft setzen:** Gibt an, ob Benutzer die Windows Defender SmartScreen-Filterwarnungen zu potenziell schädlichen Websites außer Kraft setzen können. Weitere Informationen finden Sie unter [PreventSmartScreenPromptOverride browser policy (Browserrichtlinie „PreventSmartScreenPromptOverride“)](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride).
- **Benutzer können SmartScreen-Aufforderung für Dateien außer Kraft setzen:** Gibt an, ob Benutzer die Windows Defender SmartScreen-Filterwarnungen zum Herunterladen nicht überprüfter Dateien außer Kraft setzen können. Weitere Informationen finden Sie unter [PreventSmartScreenPromptOverride browser policy (Browserrichtlinie „PreventSmartScreenPromptOverrideForFiles“)](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles).



## <a name="create-the-microsoft-edge-browser-profile"></a>Erstellen des Microsoft Edge-Browserprofils

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**. Erweitern Sie die **Konformitätseinstellungen**, und klicken Sie auf den Knoten **Microsoft Edge-Profile**. Klicken Sie auf die Menübandoption **Microsoft Edge-Profil erstellen**.
2. Geben Sie einen **Namen** für die Richtlinie ein, geben Sie optional eine **Beschreibung** ein, und klicken Sie auf **Weiter**.
3. Ändern Sie auf der Seite **Allgemeine Einstellungen** den Wert für die Einstellungen, die in diese Richtlinie einbezogen werden sollen, zu **Konfiguriert**, und klicken Sie auf **Weiter**. Die Einstellung **Set Edge Browser as default** (Microsoft Edge als Standardbrowser festlegen) muss konfiguriert werden, damit Sie fortfahren können.
4. Konfigurieren Sie in Version 1806 die Einstellung auf der Seite **SmartScreen-Einstellungen**, und klicken Sie auf **Weiter**. 
5. Wählen Sie auf der Seite **Unterstützte Plattformen** die Betriebssystemversionen und -architekturen aus, für die diese Richtlinie gelten soll, und klicken Sie auf **Weiter**. 
6. Schließen Sie den Assistenten ab.



## <a name="deploy-the-policy"></a>Bereitstellen der Richtlinie

1. Wählen Sie Ihre Richtlinie aus, und klicken Sie auf die Menübandoption **Bereitstellen**.
2. Klicken Sie auf **Durchsuchen**, um die Benutzer- oder Gerätesammlung auszuwählen, in der die Richtlinie bereitgestellt werden soll. 
3. Wählen Sie nach Bedarf weitere Optionen aus.  
     a. Generieren Sie Warnungen, wenn die Richtlinie nicht konform ist.  
     b. Legen Sie den Zeitplan fest, nach dem der Client die Konformität des Geräts mit dieser Richtlinie auswertet. 
4. Klicken Sie auf **OK**, um die Bereitstellung zu erstellen.



## <a name="next-steps"></a>Nächste Schritte

Wie bei jeder anderen Richtlinie für Konformitätseinstellungen gleicht der Client die Einstellungen gemäß dem von Ihnen angegebenen Zeitplan ab. In der Configuration Manager-Konsole können Sie die [Gerätekonformität überwachen und Berichte anzeigen](monitor-compliance-settings.md).
