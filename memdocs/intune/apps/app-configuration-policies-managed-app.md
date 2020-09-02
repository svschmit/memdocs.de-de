---
title: Konfigurationsrichtlinien für verwaltete Apps ohne Geräteregistrierung
titleSuffix: Microsoft Intune
description: Erfahren Sie, wie Sie Richtlinien für verwaltete Apps ohne Geräteregistrierung konfigurieren.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 07/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: E61C1618-79D0-41A1-B61F-4123FB6672FC
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 20b5b3de16023ac475cc41a633e5d3ab915a1bd0
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88910722"
---
# <a name="add-app-configuration-policies-for-managed-apps-without-device-enrollment"></a>Hinzufügen von App-Konfigurationsrichtlinien für verwaltete Apps ohne Geräteregistrierung

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Sie können App-Konfigurationsrichtlinien mit verwalteten Apps, die das Intune App-SDK unterstützen, sogar auf nicht registrierten Geräten verwenden. 

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Apps** > **App-Konfigurationsrichtlinien** > **Hinzufügen** > **Verwaltete Apps** aus.
3. Nehmen Sie auf der Seite **Basics** folgende Einstellungen vor:
    - **Name:** Der Name des Profils, das im Azure-Portal angezeigt wird
    - **Beschreibung:** Die Beschreibung des Profils, das im Azure-Portal angezeigt wird
    - **Geräteregistrierungstyp**: „Verwaltete Apps“ ist ausgewählt.
4. Wählen Sie über **Öffentliche Apps auswählen** oder **Benutzerdefinierte Apps auswählen** die App aus, die Sie konfigurieren möchten. Wählen Sie die App aus der Liste der Apps aus, die Sie genehmigt und mit Intune synchronisiert haben.
5. Klicken Sie auf **Weiter**, um die Seite **Einstellungen** anzuzeigen.
6. Auf der Seite **Einstellungen** finden Sie Optionen, die auf der App basieren, die Sie konfigurieren:

    - **Allgemeine Konfigurationseinstellungen:** Geben Sie für jede von der App unterstützte allgemeine Konfigurationseinstellung den **Namen** und den **Wert** ein. 
 
        Für das Intune App SDK aktivierte Apps unterstützen Konfigurationen in Schlüssel-Wert-Paaren. Weitere Informationen zu den unterstützten Schlüssel-Wert-Konfigurationen finden Sie in der Dokumentation zu den einzelnen Apps. Beachten Sie, dass Sie Tokens verwenden können, die dynamisch mit den von der Anwendung generierten Daten aufgefüllt werden. Klicken Sie zum Löschen einer allgemeinen Konfigurationseinstellung auf die Auslassungspunkte ( **...** ), und wählen Sie dann **Löschen** aus. Weitere Informationen finden Sie unter [Konfigurationswerte für das Verwenden von Token](app-configuration-policies-managed-app.md#configuration-values-for-using-tokens). 

    - **Outlook-Konfigurationseinstellungen:** Outlook für iOS und Android bietet Administratoren die Möglichkeit, die Standardkonfiguration für mehrere In-App-Einstellungen anzupassen. Weitere Informationen finden Sie unter [Outlook für iOS und Android: allgemeine App-Konfigurationsszenarios](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune#general-app-configuration-scenarios).
   
    - **S/MIME:** Secure Multipurpose Internet Mail Extensions (S/MIME) ist eine Spezifikation, die es Benutzern ermöglicht, digital signierte und verschlüsselte E-Mails zu senden und zu empfangen.
        - **S/MIME aktivieren:** Mit dieser Option geben Sie an, ob S/MIME-Steuerelemente beim Verfassen einer E-Mail aktiviert werden. Standardwert: **Nicht konfiguriert**.
        - **Benutzer das Ändern der Einstellung erlauben:** Mit dieser Option legen Sie fest, ob der Benutzer die Einstellung ändern darf. Hierzu muss S/MIME aktiviert sein. Standardwert: **Ja**.
        
    Informationen über Outlook-Einstellungen für App-Konfigurationsrichtlinien finden Sie unter [Bereitstellen von Outlook für iOS und Android: App-Konfigurationseinstellungen](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune).

7. Klicken Sie auf **Weiter**, um die Seite **Zuweisungen** anzuzeigen.
8. Klicken Sie auf **Wählen Sie die Gruppen aus, die eingeschlossen werden sollen**.
9. Wählen Sie im Bereich **Wählen Sie die Gruppen aus, die eingeschlossen werden sollen** eine Gruppe aus, und klicken Sie auf **Auswählen**.
10. Klicken Sie auf **Select groups to exclude** (Auszuschließende Gruppen auswählen), um den zugehörigen Bereich anzuzeigen.
11. Wählen Sie die Gruppen aus, die Sie ausschließen möchten, und klicken Sie dann auf **Auswählen**.

    >[!NOTE]
    >Beachten Sie beim Hinzufügen einer Gruppe Folgendes: Wenn eine Gruppe bereits für einen bestimmten Zuweisungstyp eingeschlossen wurde, ist diese vorausgewählt und kann für andere Einschlusszuweisungstypen nicht mehr geändert werden. Darum kann die Gruppe, die verwendet wurde, nicht als ausgeschlossene Gruppe verwendet werden.

12. Klicken Sie auf **Weiter**, um die Seite **Überprüfen + erstellen** anzuzeigen.
13. Klicken Sie auf **Erstellen**, um Intune die App-Konfigurationsrichtlinie hinzuzufügen.

## <a name="configuration-values-for-using-tokens"></a>Konfigurationswerte für das Verwenden von Token

Intune kann bestimmte Token generieren und sie an die verwaltete Anwendung senden. Wenn Ihre App-Konfiguration beispielsweise eine E-Mail-Einstellung verwenden kann, können Sie mithilfe eines Tokens dynamische E-Mail hinzufügen. Geben Sie den Namen, der von der App erwartet wird, in das Feld **Name** und anschließend `{{mail}}` in das Feld **Wert** ein.

Intune unterstützt folgende Tokentypen in den Konfigurationseinstellungen. Andere benutzerdefinierte Schlüssel-Wert-Paare werden nicht unterstützt.

- \{\{userPrincipalName\}\}: z.B.John@contoso.com
- \{\{mail\}\}: z.B.John@contoso.com
- \{\{partialupn\}\}: z.B. John
- \{\{accountid\}\}: z.B. fc0dc142-71d8-4b12-bbea-bae2a8514c81
- \{\{userid\}\}: z.B. 3ec2c00f-b125-4519-acf0-302ac3761822
- \{\{username\}\}: z.B. John Doe
- \{\{PrimarySMTPAddress\}\}. z.B.testuser@ad.domain.com

> [!Note]  
> Die Zeichen \{\{ und \}\} werden nur von Tokentypen verwendet und dürfen nicht für andere Zwecke verwendet werden.

## <a name="next-steps"></a>Nächste Schritte

Fahren Sie wie gewöhnlich mit dem [Zuweisen](apps-deploy.md) und [Überwachen](apps-monitor.md) der App fort.