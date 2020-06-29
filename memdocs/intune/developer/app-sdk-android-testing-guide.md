---
title: Testleitfaden für Entwickler zum Microsoft Intune App SDK für Android
description: Der Testleitfaden zum Microsoft Intune App SDK für Android unterstützt Sie beim Testen Ihrer mit Intune verwalteten Android-App.
keywords: SDK
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/18/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: 4ef8f421-9610-4d34-a464-cc02eb1578a9
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: dd4ece62215d48f3481923e099feecc992d7aa6d
ms.sourcegitcommit: 387706b2304451e548d6d9c68f18e4764a466a2b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85093364"
---
# <a name="microsoft-intune-app-sdk-for-android-developers-testing-guide"></a>Testleitfaden für Entwickler zum Microsoft Intune App SDK für Android

Der Testleitfaden zum Microsoft Intune App SDK für Android wurde dazu entworfen, Sie beim Testen Ihrer mit Intune verwalteten Android-App zu unterstützen.

## <a name="demo-tenant-setup"></a>Einrichtung des Demomandanten
Wenn Sie in Ihrem Unternehmen nicht bereits über einen Mandanten verfügen, können Sie einen Demomandanten mit oder ohne vorab generierten Daten erstellen. Sie müssen sich als [Microsoft-Partner](https://partner.microsoft.com/en-us/business-opportunities/why-microsoft) registrieren, um auf Microsoft CDX zuzugreifen. Gehen Sie folgendermaßen vor, um ein neues Konto zu erstellen:
1. Navigieren Sie zur [Website für die Erstellung eines Microsoft CDX-Mandanten](https://cdx.transform.microsoft.com/my-tenants/create-tenant), und erstellen Sie einen Microsoft 365 Enterprise-Mandanten.
2. [Richten Sie Intune ein](../fundamentals/setup-steps.md), um die mobile Geräteverwaltung (MDM) zu aktivieren.
3. [Erstellen Sie Benutzer](../fundamentals/users-add.md).
4. [Erstellen Sie Gruppen](../fundamentals/groups-add.md).
5. [Weisen Sie Lizenzen je nach Bedarf für Ihre Tests zu](../fundamentals/licenses-assign.md).


## <a name="azure-portal-policy-configuration"></a>Richtlinienkonfiguration des Azure-Portals
[Erstellen Sie App-Schutzrichtlinien](../apps/app-protection-policies.md) über das [Intune-Blatt des Azure-Portals](https://portal.azure.com/?feature.customportal=false#blade/Microsoft_Intune_Apps/MainMenu/14/selectedMenuItem/Overview), und weisen Sie sie zu. Außerdem können Sie eine [App-Konfigurationsrichtlinie](../apps/app-configuration-policies-overview.md) über das Intune-Blatt erstellen und zuweisen.

> [!NOTE]
> Wenn Ihre App nicht im Azure-Portal aufgeführt wird, können Sie eine Richtlinie auf die App anwenden, indem Sie auf **Weitere Apps** klicken und den Paketnamen in das Textfeld eingeben.

## <a name="test-cases"></a>Testfälle

In den folgenden Testfällen werden Konfigurations- und Bestätigungsschritte veranschaulicht. Verwenden Sie diese Tests, um Ihre neu integrierte Android-App zu überprüfen.

### <a name="required-pin-and-corporate-credentials"></a>Erforderliche PIN und Unternehmensanmeldeinformationen

Sie können eine PIN für den Zugriff auf Unternehmensressourcen anfordern. Außerdem können Sie Unternehmensauthentifizierung erzwingen, bevor Benutzer verwaltete Apps verwenden können. Gehen Sie wie folgt vor:

1. Legen Sie die Optionen **PIN für Zugriff erforderlich** und **Unternehmensanmeldeinformationen für Zugriff erforderlich** auf **Ja** fest. Weitere Informationen finden Sie unter [Einstellungen für App-Schutzrichtlinien für Android in Microsoft Intune](../apps/app-protection-policy-settings-android.md#access-requirements).
2. Überprüfen Sie die folgenden Bedingungen:
    - Beim App-Start sollte eine Eingabeaufforderung für die Angabe einer PIN oder eines Produktionsbenutzers angezeigt werden, der bei der Registrierung im Unternehmensportal verwendet wurde.
    - Wenn keine gültige Anmeldeaufforderung angezeigt wird, kann dies an einem fehlerhaft konfigurierten Android-Manifest und insbesondere an den Werten („SkipBroker“, „ClientID“ und „Authority“) für die ADAL-Integration (Azure Active Directory-Authentifizierungsbibliothek) liegen.
    - Wenn keinerlei Eingabeaufforderung angezeigt wird, liegt dies möglicherweise an einem fehlerhaft integrierten `MAMActivity`-Wert. Weitere Informationen zu `MAMActivity` finden Sie im [Entwicklerhandbuch zum Microsoft Intune App SDK für Android](app-sdk-android.md).

> [!NOTE] 
> Wenn der oben genannte Test nicht funktioniert, werden die folgenden Tests wahrscheinlich ebenfalls fehlschlagen. Überprüfen Sie das [SDK](app-sdk-android.md#sdk-integration) und die [ADAL](app-sdk-android.md#configure-azure-active-directory-authentication-library-adal)-Integration.

### <a name="restrict-transferring-and-receiving-data-with-other-apps"></a>Einschränken der Übertragung von Daten von und zu anderen Apps
Sie können die Datenübertragung zwischen vom Unternehmen verwalteten Anwendungen wie folgt steuern:

1. Legen Sie **Zulassen, dass die App Daten an andere Apps überträgt** auf **Richtlinienverwaltete Apps** fest.
2. Legen Sie die Option **Zulassen, dass die App Daten von anderen Apps empfängt** auf **Alle Apps** fest. 

Diese Richtlinien wirken sich auf die Verwendung von Absichten und Inhaltsanbietern aus.
3. Überprüfen Sie die folgenden Bedingungen:
    - Das Öffnen Ihrer App-Funktionen über eine nicht verwaltete App funktioniert.
    - Das Freigeben von Inhalten zwischen Ihrer App und verwalteten Apps ist zulässig.
    - Die Freigabe über Ihre App an nicht verwaltete Apps (z. B. Chrome) wird blockiert.


#### <a name="restrict-receiving-data-from-other-apps"></a>Einschränken des Datenempfangs von anderen Apps

1. Wählen Sie für **Organisationsdaten an andere Apps senden** die Option **Alle Apps** aus.
2. Legen Sie die Option **Daten von anderen Apps empfangen** auf **Richtlinienverwaltete Apps** fest. 
3. Überprüfen Sie die folgenden Bedingungen:
    - Das Senden von Daten an eine nicht verwaltete App von Ihrer App aus funktioniert ordnungsgemäß.
    - Das Freigeben von Inhalten zwischen Ihrer App und verwalteten Apps ist zulässig.
    - Die Freigabe von einer nicht verwalteten App (z. B. Chrome) für Ihre App wird blockiert.

Wenn Ihre App [integrierte Steuerelemente für „Öffnen aus“](app-sdk-android.md#opening-data-from-a-local-or-cloud-storage-location) benötigt, können Sie die Funktion **Öffnen aus** folgendermaßen steuern:

1. Legen Sie die Option **Daten von anderen Apps empfangen** auf **Richtlinienverwaltete Apps** fest. 
2. Legen Sie die Option **Daten in Organisationsdokumenten öffnen** auf **Blockieren** fest. 
3. Überprüfen Sie die folgenden Bedingungen:
    - Das Öffnen ist auf entsprechende verwaltete Speicherorte beschränkt.

### <a name="restrict-cut-copy-and-paste"></a>Einschränken von Ausschneiden, Kopieren und Einfügen
Sie können die Zwischenablage wie folgt auf verwaltete Apps einschränken:

1. Legen Sie für **Ausschneiden, Kopieren und Einfügen mit anderen Apps einschränken** die Option **Richtlinienverwaltete Apps mit Einfügen** fest.
2. Überprüfen Sie die folgenden Bedingungen:
    - Das Kopieren von Text aus Ihrer App in eine nicht verwaltete App (z. B. eine Nachrichten-App) wird blockiert.

### <a name="prevent-save"></a>Verhindern der Speicherung
Wenn Ihre App [integrierte Steuerelemente für „Speichern als“](app-sdk-android.md#example-data-transfer-between-apps-and-device-or-cloud-storage-locations) benötigt, können Sie die Funktion **Speichern als** folgendermaßen steuern:

1. Legen Sie die Option **„Speichern unter“ verhindern** auf **Ja** fest.
2. Überprüfen Sie die folgenden Bedingungen:
    - Das Speichern ist auf entsprechende verwaltete Speicherorte eingeschränkt.

### <a name="file-encryption"></a>Dateiverschlüsselung
Sie können Daten auf dem Gerät wie folgt verschlüsseln:

1. Legen Sie **App-Daten verschlüsseln** auf **Ja** fest.
2. Überprüfen Sie die folgenden Bedingungen:
    - Das normale Anwendungsverhalten wird nicht beeinträchtigt.

### <a name="prevent-android-backups"></a>Verhindern von Android-Sicherungen
Sie können die App-Sicherung wie folgt steuern:

1. Wenn Sie [integrierte Sicherungseinschränkungen](app-sdk-android.md#protecting-backup-data) festgelegt haben, legen Sie **Android-Sicherungen verhindern** auf **Ja** fest.
2. Überprüfen Sie die folgenden Bedingungen:
    - Sicherungen sind eingeschränkt.

### <a name="wipe"></a>Zurücksetzen
Sie könnten Remotelöschvorgänge für verwaltete Apps ausführen, die Unternehmens-E-Mails und -Dokumente enthalten. Personenbezogene Daten werden entschlüsselt, wenn sich nicht mehr verwaltet werden. Gehen Sie wie folgt vor:

1. [Veranlassen Sie eine Zurücksetzung](../apps/apps-selective-wipe.md) über das Azure-Portal.
2. Wenn Ihre App keine Zurücksetzungshandler registriert, überprüfen Sie die folgenden Bedingungen:
    - Eine vollständige Zurücksetzung wird durchgeführt.
3. Wenn Ihre App für `WIPE_USER_DATA` oder `WIPE_USER_AUXILARY_DATA` registriert ist, überprüfen Sie die folgenden Bedingungen:
    - Der verwaltete Inhalt wird aus der App entfernt. Weitere Informationen finden Sie im [Entwicklerhandbuch zum Intune App SDK für Android im Abschnitt „Selektives Zurücksetzen“](app-sdk-android.md#selective-wipe).

### <a name="multi-identity-support"></a>Unterstützung mehrerer Identitäten
Die Integration von [Unterstützung mehrerer Identitäten](app-sdk-android.md#multi-identity-optional) ist eine Änderung mit hohem Risiko, die gründlich getestet werden muss. Die am häufigsten auftretenden Probleme werden von fehlerhaft festgelegten aktiven Identitäten (`Context` in Relation zur Bedrohungsstufe) oder fehlerhaftem Überwachen von Dateiidentitäten (`MAMFileProtectionManager`) ausgelöst.

Stellen Sie zumindest Folgendes sicher:

- Die Richtlinie für **Speichern unter** funktioniert für verwaltete Identitäten ordnungsgemäß.
- Die Einschränkungen beim Kopieren und Einfügen von Inhalten aus verwalteten Identitäten in persönliche Konten werden ordnungsgemäß erzwungen.
- Nur Daten, die zur verwalteten Identität gehören, werden verschlüsselt. Personenbezogene Dateien werden nicht geändert.
- Das selektive Zurücksetzen während der Aufhebung der Registrierung entfernt nur die Daten der verwalteten Identität.
- Der Endbenutzer wird zum bedingten Start aufgefordert, wenn er zum ersten Mal von einem nicht verwalteten Konto zu einem verwalteten wechselt.

### <a name="app-configuration-optional"></a>App-Konfiguration (Optional)
Sie können das Verhalten von verwalteten Apps konfigurieren. Wenn Ihre App App-Konfigurationseinstellungen nutzt, sollten Sie testen, ob Ihre App alle Werte ordnungsgemäß verarbeitet, die Sie (als Administrator) festlegen können. Sie können [App-Konfigurationsrichtlinien](../apps/app-configuration-policies-overview.md) in Intune erstellen und zuweisen.


