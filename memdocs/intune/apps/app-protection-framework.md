---
title: Datenschutzframework mithilfe von App-Schutzrichtlinien
titleSuffix: Microsoft Intune
description: Hier erfahren Sie, wie App-Schutzrichtlinien (App Protection Policies, APP) dafür sorgen, dass die Daten eines Unternehmens geschützt bleiben oder innerhalb einer verwalteten App verbleiben, unabhängig davon, ob das Gerät registriert ist.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/03/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: smithre4
ms.suite: ems
search.appverid: MET150
ms.custom: ''
ms.collection: M365-identity-device-management
ms.openlocfilehash: cfb0012dfc2cedb72c64a54c16b567dffff84c9e
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79342295"
---
# <a name="data-protection-framework-using-app-protection-policies"></a>Datenschutzframework mithilfe von App-Schutzrichtlinien 

Da immer mehr Unternehmen Strategien für Mobilgeräte für den Zugriff auf Daten im Zusammenhang mit Unternehmen oder Bildungseinrichtungen implementieren, ist es sehr wichtig, Schutzmaßnahmen gegen Datenlecks zu implementieren. Die Lösung für mobile Anwendungsverwaltung von Intune für das Verhindern von Datenlecks sind App-Schutzrichtlinien (App Protection Policies, APP). Bei App-Schutzrichtlinien handelt es sich um Regeln, die dafür sorgen, dass die Daten eines Unternehmens geschützt bleiben oder innerhalb einer verwalteten App verbleiben, unabhängig davon, ob das Gerät registriert ist. Weitere Informationen finden Sie unter [Übersicht über App-Schutzrichtlinien](app-protection-policy.md).

Beim Konfigurieren der App-Schutzrichtlinien ermöglicht es die Vielzahl verschiedener Einstellungen und Optionen Unternehmen, den Schutz den eigenen Anforderungen anzupassen. Aufgrund dieser Flexibilität ist es jedoch möglicherweise nicht offensichtlich, welche Richtlinieneinstellungen genau erforderlich sind, um ein vollständiges Szenario zu implementieren. Microsoft hat eine neue Taxonomie für [Sicherheitskonfigurationen unter Windows 10](https://aka.ms/secconframework) eingeführt, um Unternehmen dabei zu unterstützen, den Schutz für Clientendpunkte zu priorisieren, und Intune nutzt eine ähnliche Taxonomie für das APP-Datenschutzframework im Rahmen der Verwaltung mobiler Apps.  

Das APP-Datenschutzkonfigurationsframework kann in drei einzelne Konfigurationsszenarios unterteilt werden:

- Stufe 1: Einfacher Datenschutz für Unternehmen: Microsoft empfiehlt diese Konfiguration als minimale Datenschutzkonfiguration für Unternehmensgeräte.

- Stufe 2: Erweiterter Datenschutz für Unternehmen: Microsoft empfiehlt diese Konfiguration für Geräte, deren Benutzer auf vertrauliche Daten zugreifen. Diese Konfiguration sollte auf die meisten Mobilgerätebenutzer angewendet werden, die auf Unternehmensdaten oder Daten einer Bildungseinrichtung zugreifen. Einige Steuerungsmöglichkeiten können sich auf die Servicequalität für Benutzer auswirken.

- Stufe 3: Hoher Datenschutz für Unternehmen: Microsoft empfiehlt diese Konfiguration für Geräte, die von einem Unternehmen mit einem größeren oder erweiterten Sicherheitsteam ausgeführt werden, oder für bestimmte Benutzer oder Gruppen, die einem besonders hohen Risiko ausgesetzt sind. Ein Beispiel wären Benutzer in einem Unternehmen, die mit Daten arbeiten, deren Diebstahl sich direkt und schwerwiegend auf den Aktienkurs auswirken würde. Unternehmen, die sehr wahrscheinlich als Ziel für mit hohen finanziellen Mitteln und gutem Know-how ausgestatteten Kontrahenten in Frage kommen würden, sollten diese Konfiguration in Erwägung ziehen.

## <a name="app-data-protection-framework-deployment-methodology"></a>Methodologie für die Bereitstellung des APP-Datenschutzframeworks

Wie bei jeder Bereitstellung neuer Software, neuer Features oder Einstellungen empfiehlt Microsoft, in eine Ringmethodologie zu investieren, um die Prüfung vor der Bereitstellung des APP-Datenschutzframeworks zu testen. Das Definieren von Bereitstellungsringen ist in der Regel ein einmaliges Ereignis (oder trifft zumindest nur selten auf), aber das IT-Team sollte diese Gruppen nochmals ansehen, um sicherzustellen, dass die Reihenfolge noch korrekt ist.

Microsoft empfiehlt den folgenden Ansatz für einen Bereitstellungsring für das APP-Datenschutzframework:

| Bereitstellungsring  | Mandant  | Bewertungsteams  | Ausgabe  | Zeitachse  |
|--------------------|------------------------|-------------------------------------------------------------------|----------------------------------------------------------|----------------------------------------|
| Qualitätssicherung  | Präproduktionsmandant  | Inhaber mobiler Funktionen, Sicherheit, Risikobewertung, Datenschutz, Servicequalität  | Funktionelle Szenarioüberprüfung, Entwurfsdokumentation  | 0-30 Tage  |
| Vorschau  | Produktionsmandant  | Inhaber mobiler Funktionen, Servicequalität  | Überprüfung von Endbenutzerszenarios, Dokumentation für Benutzer  | 7-14 Tage, nach der Qualitätssicherung  |
| Produktion  | Produktionsmandant  | Inhaber mobiler Funktionen, IT-Helpdesk  | N/V  | 7 Tage bis zu mehreren Wochen, nach der Vorschauphase  |

Wie Sie in der obigen Tabelle sehen, sollten alle Änderungen an den App-Schutzrichtlinien zunächst in einer Präproduktionsumgebung ausgeführt werden, um die Auswirkungen der Richtlinieneinstellung zu verstehen. Sobald die Testphase abgeschlossen ist, können die Änderungen in die Produktion übertragen werden, und auf eine Teilmenge der Produktionsbenutzer angewendet werden, wobei es sich in der Regel um die IT-Abteilung und andere geeignete Gruppen handelt. Abschließend kann die Einführung abgeschlossen werden, indem die Änderungen auf die verbleibende Community der Benutzer mobiler Geräte ausgeweitet werden. Die Einführung in der Produktion kann etwas länger dauern, je nach Grad der Auswirkung einer entsprechenden Änderung. Wenn keine Benutzer von der Änderung betroffen sind, sollte die Einführung schnell abgeschlossen werden können, während die Einführung bei Auswirkungen auf Benutzer langsamer ausgeführt werden sollte, da die Änderungen zuerst für die Benutzer kommuniziert werden müssen.

Beim Testen der APP-Änderungen sollten Sie die [zeitliche Planung der Implementierung](app-protection-policy-delivery.md) berücksichtigen. Der Status der APP-Implementierung für einen Benutzer kann überwacht werden. Weitere Informationen finden Sie unter [Überwachen von App-Schutzrichtlinien](app-protection-policies-monitor.md).

Mithilfe von Edge und der URL *about:Intunehelp* können Sie einzelne APP-Einstellungen für einzelne Apps auf Geräten überprüfen. Weitere Informationen finden Sie unter [Überprüfen der Protokolle für Client-App-Schutz](app-protection-policy-settings-log.md) und [Einstellungen für das APP-Datenschutzframework](manage-microsoft-edge.md#use-microsoft-edge-on-ios-to-access-managed-app-logs).

## <a name="app-data-protection-framework-settings"></a>Einstellungen für das APP-Datenschutzframework

Die folgenden App-Schutzrichtlinieneinstellungen sollten für geeignete Apps aktiviert und allen Benutzer von mobilen Geräten zugewiesen werden. Weitere Informationen finden Sie unter [Einstellungen für App-Schutzrichtlinien für iOS](app-protection-policy-settings-ios.md) und [Einstellungen für App-Schutzrichtlinien für Android in Microsoft Intune](app-protection-policy-settings-android.md).

Microsoft empfiehlt, Nutzungsszenarios zu überprüfen und zu kategorisieren, und dann mithilfe von Anleitungen Benutzer für eine entsprechende Stufe zu konfigurieren. Wie bei jedem Framework müssen die Einstellungen in einer entsprechenden Stufe möglicherweise je nach Anforderungen eines Unternehmens angepasst werden, da für den Datenschutz die Bedrohungsumgebung, Risikobereitschaft und der Einfluss auf die Verwendbarkeit ausgewertet werden müssen.  

### <a name="apps-to-include-in-the-app-protection-policies"></a>Für die App-Schutzrichtlinien empfohlene Apps  

Bei jeder App-Schutzrichtlinie sollten die folgenden wichtigen Microsoft-Apps eingeschlossen werden:

- Edge
- Excel
- Office
- OneDrive
- OneNote
- Outlook
- PowerPoint
- Microsoft Teams
- Microsoft To-Do
- Word
- Microsoft SharePoint

Diese Richtlinien sollten auch weitere Microsoft-Apps einschließen, je nach Anforderungen Ihres Unternehmens, sowie öffentliche Apps von Drittanbietern, die das Intune-SDK integrieren, das im Unternehmen verwendet wird, und branchenspezifische App, für die das [Intune-SDK](../developer/app-sdk.md) integriert ist, oder die eingeschlossen wurden.

### <a name="level-1-enterprise-basic-data-protection"></a>Stufe 1: Einfacher Datenschutz für Unternehmen

Bei Stufe 1 handelt es sich um die minimale Datenschutzkonfiguration für ein mobiles Gerät eines Unternehmens. Wenn Sie diese Konfiguration verwenden, müssen keine einfachen Exchange Online-Gerätezugriffsrichtlinien festgelegt werden, indem stattdessen eine PIN angefordert wird, um auf Daten eines Unternehmens oder einer Bildungseinrichtung zuzugreifen, indem die Geschäfts-, Schul- oder Unikontodaten verschlüsselt werden, und indem die Funktion zur Verfügung gestellt wird, die entsprechenden Daten selektiv von einem Gerät entfernen zu können. Im Gegensatz zu Exchange Online-Gerätezugriffsrichtlinien gelten die unten stehenden App-Schutzrichtlinieneinstellungen jedoch für alle Apps, die in der Richtlinie ausgewählt wurden, und sorgen damit dafür, dass der Datenzugriff über das Szenario von Messaging auf mobilen Geräten hinaus geschützt ist.

Die Richtlinien der Stufe 1 erzwingen eine solide Datenzugriffsebene und minimieren dabei die Beeinträchtigungen für Benutzer. Sie imitieren den Standarddatenschutz und die Zugriffsanforderungseinstellungen beim Erstellen einer App-Schutzrichtlinie im Microsoft Endpoint Manager.  

#### <a name="data-protection"></a>Datenschutz

| Einstellung | Beschreibung der Einstellung |             Wert  |             Plattform        |
|-----------------|--------------------------------------------------------|-----------------------|----------------------------------------|
| Datenübertragung |             Organisationsdaten sichern in…  |             Zulassen  |             iOS/iPadOS, Android        |
| Datenübertragung |       Organisationsdaten an andere Apps senden  |             Alle Apps  |             iOS/iPadOS, Android        |
| Datenübertragung |       Daten von anderen Apps empfangen  |             Alle Apps  |             iOS/iPadOS, Android        |
| Datenübertragung |       Ausschneiden, Kopieren und Einfügen zwischen Apps einschränken  |             Jede App  |             iOS/iPadOS, Android        |
| Datenübertragung |       Tastaturen von Drittanbietern  |             Zulassen  |             iOS/iPadOS        |
| Datenübertragung |       Genehmigte Tastaturen  |             Nicht erforderlich  |             Android        |
| Datenübertragung |       Bildschirmaufnahme und Google Assistant  |             Zulassen  |             Android        |
| Verschlüsselung |             Organisationsdaten verschlüsseln  |             Erforderlich  |             iOS/iPadOS, Android        |
| Verschlüsselung |       Organisationsdaten auf registrierten Geräten verschlüsseln  |             Erforderlich  |             Android        |
| Funktionalität  |             App mit App für native Kontakte synchronisieren  |             Zulassen  |             iOS/iPadOS, Android        |
| Funktionalität  |       Organisationsdaten drucken  |             Zulassen  |             iOS/iPadOS, Android        |
| Funktionalität  |       Übertragung von Webinhalten mit anderen Apps einschränken  |             Jede App  |             iOS/iPadOS, Android        |
| Funktionalität  |       Benachrichtigungen zu Organisationsdaten  |             Zulassen  |             iOS/iPadOS, Android        |

#### <a name="access-requirements"></a>Erforderliche Zugriffsberechtigungen 

| Einstellung  | Wert  | Plattform  | Hinweise  |
|----------------------------------------------------------------|---------------|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| PIN für Zugriff  | Erforderlich  | iOS/iPadOS, Android  |   |
| PIN-Typ  | Numerisch  | iOS/iPadOS, Android  |   |
| Einfache PIN  | Zulassen  | iOS/iPadOS, Android  |   |
| PIN-Mindestlänge auswählen  | 4  | iOS/iPadOS, Android  |   |
| Biometric instead of PIN for access (Biometrische Anmeldung anstelle von PIN für den Zugriff)  | Zulassen  | iOS/iPadOS, Android  |   |
| Override biometric instead of PIN for access (Biometrische Anmeldung anstelle von PIN für den Zugriff überschreiben)  | Erforderlich  | iOS/iPadOS, Android  |   |
| Timeout (Minuten der Inaktivität)  | 720  | iOS/iPadOS, Android  |   |
| Face ID anstelle von PIN für Zugriff  | Zulassen  | iOS/iPadOS  |   |
| Anzahl von Tagen für PIN-Zurücksetzung  | Nein  | iOS/iPadOS, Android  |   |
| App-PIN, wenn Geräte-PIN festgelegt ist  | Erforderlich  | iOS/iPadOS, Android  | Wenn das Gerät in Intune registriert ist, können Administratoren in Erwägung ziehen, diese Einstellung auf „Nicht erforderliche“ festzulegen, wenn sie eine starke Geräte-PIN über eine Gerätekonformitätsrichtlinie erzwingen.  |
| Anmeldeinformationen für Geschäfts-, Schul- oder Unikonto für Zugriff  | Nicht erforderlich  | iOS/iPadOS, Android  |   |
| Erneutes Prüfen der Zugriffsanforderungen nach (Minuten der Inaktivität)  | 30  | iOS/iPadOS, Android  |   |

#### <a name="conditional-launch"></a>Bedingter Start 

| Einstellung | Beschreibung der Einstellung |          Wert / Aktion  |          Plattform        | Hinweise |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| App-Bedingungen |       Maximal zulässige PIN-Versuche  |          5 / PIN zurücksetzen  |          iOS/iPadOS, Android  |                  |
| App-Bedingungen |       Offline-Toleranzperiode  |          720 / Zugriff blockieren (Minuten)  |          iOS/iPadOS, Android  |                  |
| App-Bedingungen |       Offline-Toleranzperiode  |          90 / Daten löschen (Tage)  |          iOS/iPadOS, Android  |                  |
| Gerätebedingungen  |       Geräte mit Jailbreak/entfernten Nutzungsbeschränkungen  |        Nicht verfügbar / Zugriff blockieren  |          iOS/iPadOS, Android  |                  |
| Gerätebedingungen  |       SafetyNet-Gerätenachweis  |          Basisintegrität und zertifizierte Geräte / Zugriff blockieren  |          Android  |          <p>Diese Einstellung konfiguriert „SafetyNet Attestation“ von Google auf Endbenutzergeräten. Die Basisintegrität überprüft die Integrität des Geräts. Für Geräte mit Rootzugriff, Emulatoren, virtuelle Geräte und Geräte, die Anzeichen von Manipulationen aufweisen, schlägt die Überprüfung der Basisintegrität fehl. </p><p> Die Option „Basisintegrität und zertifizierte Geräte“ überprüft die Kompatibilität des Geräts mit Google-Diensten. Nur unveränderte Geräte, die von Google zertifiziert wurden, bestehen diese Überprüfung.</p>  |
| Gerätebedingungen  |       Bedrohungsüberprüfung für Apps erzwingen  |        Nicht verfügbar / Zugriff blockieren  |          Android  |          Diese Einstellung sorgt dafür, dass die Verify Apps-Überprüfung von Google für Endbenutzergeräte aktiviert ist. Wenn diese Einstellung konfiguriert ist, wird der Zugriff für den Endbenutzer so lange gesperrt, bis er auf seinem Android-Gerät die App-Überprüfung von Google aktiviert.        |

#### <a name="level-2-enterprise-enhanced-data-protection"></a>Stufe 2: Erweiterter Datenschutz für Unternehmen

Bei Stufe 2 handelt es sich um die Datenschutzkonfiguration, die als Standard für Geräte empfohlen wird, deren Benutzer Zugriff auf vertraulichere Daten haben. Heutzutage sind diese Geräte in Unternehmen oftmals Angriffen ausgesetzt. Für diese Empfehlungen wird keine große Menge an Personal oder Sicherheitsexperten mit viel Erfahrung angenommen, und deshalb sollte sich diese Stufe für die meisten Unternehmen eignen. Bei dieser Konfiguration wird die Konfiguration der Stufe 1 ausgeweitet, indem Datenübertragungsszenarios eingeschränkt werden und eine minimale Betriebssystemversion erzwungen wird.

Die in Stufe 2 erzwungenen Richtlinieneinstellungen umfassen alle für Stufe 1 empfohlenen Richtlinieneinstellungen. Dazu kommen die untenstehenden Richtlinieneinstellungen bzw. sie werden aktualisiert, um weitere Steuerungsmöglichkeiten zu implementieren, was Stufe 2 zu einer erweiterten Konfiguration im Vergleich zu Stufe 1 macht. Diese Einstellungen können eine etwas höhere Auswirkung auf Benutzer oder Anwendungen haben. Sie erzwingen aber auch eine Datenschutzebene, die geeigneter für die Risiken ist, denen Benutzer ausgesetzt sind, die Zugriff auf vertrauliche Daten auf mobilen Geräten haben.

#### <a name="data-protection"></a>Datenschutz

| Einstellung | Beschreibung der Einstellung |             Wert  |             Plattform        | Hinweise |
|---------------|----------------------------------------------------------|-----------------------------------------------|---------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Datenübertragung |       Organisationsdaten sichern in…  |          Blockieren  |          iOS/iPadOS, Android  |                  |
| Datenübertragung |       Organisationsdaten an andere Apps senden  |          Richtlinienverwaltete Apps  |          iOS/iPadOS, Android  |          <p>Unter iOS/iPadOS können Administratoren diesen Wert als „Richtlinienverwaltete Apps“, „Per Richtlinie verwaltete Apps mit Betriebssystemfreigabe“ oder „Per Richtlinie verwaltete Apps mit Filterung für ‚Öffnen in‘/‘Freigeben‘“ konfigurieren. </p><p>„Richtlinienverwaltete Apps mit Betriebssystemfreigabe“ ist eine verfügbare Konfiguration, wenn das Gerät auch für Intune registriert wurde. Diese Einstellung ermöglicht die Datenübertragung auf andere richtlinienverwaltete Apps, sowie Dateiübertragungen auf andere Apps, die von Intune verwaltet werden. </p><p>Bei „Per Richtlinie verwaltete Apps mit Filterung für ‚Öffnen in‘/‘Freigeben‘“ werden die „Öffnen in“-/„Freigeben“-Dialogfelder so gefiltert, dass nur richtlinienverwaltete Apps angezeigt werden. </p><p> Weitere Informationen finden Sie unter [Richtlinieneinstellungen für App-Schutz unter iOS](app-protection-policy-settings-ios.md).</p> |
| Datenübertragung |       Kopien von Organisationsdaten speichern  |          Blockieren  |          iOS/iPadOS, Android  |                  |
| Datenübertragung |       Allow users to save copies to selected services (Benutzern das Speichern von Kopien in den ausgewählten Diensten ermöglichen)  |          OneDrive for Business, SharePoint Online |          iOS/iPadOS, Android  |                  |
| Datenübertragung |       Ausschneiden, Kopieren und Einfügen zwischen Apps einschränken  |          Richtlinienverwaltete Apps mit Einfügen in  |          iOS/iPadOS, Android  |                  |
| Datenübertragung |       Bildschirmaufnahme und Google Assistant  |          Blockieren  |          Android  |                  |
| Funktionalität |       Übertragung von Webinhalten mit anderen Apps einschränken  |          Microsoft Edge  |          iOS/iPadOS, Android  |                  |
| Funktionalität |       Benachrichtigungen zu Organisationsdaten  |          Organisationsdaten blockieren  |          iOS/iPadOS, Android  |          Eine Liste der Apps, die diese Einstellung unterstützen, finden Sie unter [Richtlinieneinstellungen für App-Schutz unter iOS](app-protection-policy-settings-ios.md) und [Einstellungen für App-Schutzrichtlinien für Android in Microsoft Intune](app-protection-policy-settings-android.md).       |

#### <a name="conditional-launch"></a>Bedingter Start

| Einstellung | Beschreibung der Einstellung |          Wert / Aktion  |          Plattform        | Hinweise |
|--------------------|----------------------------|-----------------------------------------------------------|----------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Gerätebedingungen  |       Mindestversion für Betriebssystem  |          *Format: Hauptversion.Nebenversion.Buildversion <br>Beispiel:   12.4.4* / Zugriff blockieren |          iOS/iPadOS        | Microsoft empfiehlt das Konfigurieren der Mindesthauptversion für das iOS-Betriebssystem, um übereinstimmende unterstützte iOS-Versionen für Microsoft-Apps verwenden zu können.   Microsoft-Apps unterstützen einen N-1-Ansatz, wobei N für die aktuelle iOS-Hauptversion steht. Als Werte für Neben- und Buildversionen empfiehlt Microsoft, dafür zu sorgen, dass die Geräte über die aktuellen entsprechenden Sicherheitsupdates verfügen. Unter [Apple-Sicherheitsupdates](https://support.apple.com/en-us/HT201222) finden Sie die aktuellen Empfehlungen von Apple. |
| Gerätebedingungen  |       Mindestversion für Betriebssystem  |          *Format: Hauptversion.Nebenversion<br> Beispiel: 8.0* / Zugriff blockieren   |          Android        | Microsoft empfiehlt das Konfigurieren der Mindesthauptversion für das Android-Betriebssystem, um übereinstimmende unterstützte Android-Versionen für Microsoft-Apps verwenden zu können. OEMs und Geräte, für die von Android Enterprise empfohlene Anforderungen gelten, müssen die aktuelle Versandversion und ein Upgrade auf die nächste Version unterstützen.   Aktuell empfiehlt Android für Wissensarbeiter Android 8.0 und höher.   Unter [Anforderungen für „Android Enterprise Recommended“](https://www.android.com/enterprise/recommended/requirements/) finden Sie Informationen zu den aktuellen Empfehlungen von Android. |
| Gerätebedingungen  |       Mindestversion für Patch  |          *Format:   JJJJ-MM-TT <br> Beispiel: 2020-01-01* / Zugriff blockieren  |          Android        | Android-Geräte können monatliche Sicherheitsupdates erhalten, aber das Release hängt von den OEMs und/oder Netzbetreibern ab. Unternehmen sollten dafür sorgen, dass bereitgestellte Android-Geräte Sicherheitsupdates erhalten, bevor diese Einstellung implementiert wird. Unter [Android-Sicherheitsbulletins](https://source.android.com/security/bulletin/) finden Sie die aktuellen Updates.  |

#### <a name="level-3-enterprise-high-data-protection"></a>Stufe 3: Hoher Datenschutz für Unternehmen 

Bei Stufe 3 handelt es sich um die Datenschutzkonfiguration, die als Standard für Organisationen empfohlen wird, die über ein großes und gut ausgebildetes Sicherheitsteam verfügen, oder für bestimmte Benutzer und Gruppen, auf die von Kontrahenten besonders abgezielt werden könnte. Auf solche Organisationen wird oft von mit hohen finanziellen Mitteln und gutem Know-how ausgestatteten Kontrahenten abgezielt. Deshalb sind die zusätzlichen beschriebenen Einschränkungen und Steuerungsmöglichkeiten erforderlich. Bei dieser Konfiguration wird die Konfiguration der Stufe 2 ausgeweitet, indem zusätzliche Datenübertragungsszenarios eingeschränkt werden, die Komplexität der PIN-Konfiguration erhöht und Bedrohungserkennung auf Mobilgeräten hinzugefügt wird.  

Die in Stufe 3 erzwungenen Richtlinieneinstellungen umfassen alle für Stufe 2 und Stufe 1 empfohlenen Richtlinieneinstellungen. Dazu werden die untenstehenden Richtlinieneinstellungen hinzugefügt bzw. sie werden aktualisiert, um eine striktere Datenschutzkonfiguration und Steuerungsmöglichkeiten zu implementieren. Diese Richtlinieneinstellungen können sich stark auf Benutzer oder Anwendungen auswirken, indem eine Sicherheitsebene erzwungen wird, die den Risiken angemessen ist, denen sich die betroffenen Organisationen ausgesetzt sehen.  

#### <a name="data-protection"></a>Datenschutz

| Einstellung | Beschreibung der Einstellung |             Wert  |             Plattform        | Hinweise |
|---------------|---------------------------------------|----------------------------------------|--------------------------------------|---------------------------------------------------------------------------------------------------------|
| Datenübertragung |       Daten von anderen Apps empfangen  |          Richtlinienverwaltete Apps  |          iOS/iPadOS, Android         |  |
| Datenübertragung |       Tastaturen von Drittanbietern  |          Blockieren  |          iOS/iPadOS        | Unter iOS werde hier alle Tastaturen von Drittanbietern blockiert und können nicht mit der App verwendet werden.  |
| Datenübertragung |       Genehmigte Tastaturen  |          Erforderlich  |          Android        | Bei Android-Geräten müssen Tastaturen ausgewählt werden, damit sie auf Ihren bereitgestellten Android-Geräten verwendet werden können.  |
| Datenübertragung |       Zu genehmigende Tastaturen auswählen  |          *add/remove keyboards* (Tastaturen hinzufügen/entfernen)  |          Android        | Bei Android-Geräten müssen Tastaturen ausgewählt werden, damit sie auf Ihren bereitgestellten Android-Geräten verwendet werden können.  |
| Funktionalität |       Drucken der Organisationsdaten  |          Blockieren  |          iOS/iPadOS, Android         |  |

#### <a name="access-requirements"></a>Erforderliche Zugriffsberechtigungen

|       Einstellung  |          Wert  |          Plattform  |
|-----------------------------------------------------------|--------------------|---------------------------------|
|       Einfache PIN  |          Blockieren  |          iOS/iPadOS, Android  |
|       Auswählen der PIN-Mindestlänge  |          6  |          iOS/iPadOS, Android  |
|       Anzahl von Tagen für PIN-Zurücksetzung  |          Ja  |          iOS/iPadOS, Android  |
|       Anzahl von Tagen  |          365  |          iOS/iPadOS, Android  |

#### <a name="conditional-launch"></a>Bedingter Start

| Einstellung | Beschreibung der Einstellung |          Wert / Aktion  |          Plattform        | Hinweise |
|----------------------------|--------------------------------------|-------------------|---------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       Gerätebedingungen  |          Geräte mit Jailbreak/entfernten Nutzungsbeschränkungen  |        Nicht verfügbar / Daten löschen  |          iOS/iPadOS, Android        |  |
|       Gerätebedingungen  |          Maximal zulässige Bedrohungsstufe  |          Gesichert / Zugriff blockieren  |          iOS/iPadOS, Android        | <p>Nicht registrierte Geräte können mithilfe der Mobile Threat Defense auf Bedrohungen untersucht werden. Weitere Informationen finden Sie unter [Aktivieren des Mobile Threat Defense-Connectors in Intune für nicht registrierte Geräte](https://aka.ms/mtdmamdocs).      </p><p>     Wenn das Gerät registriert ist, kann diese Einstellung übersprungen und stattdessen die Mobile Threat Defense für registrierte Geräte bereitgestellt werden. Weitere Informationen finden Sie unter [Erstellen einer Mobile Threat Defense-Gerätekompatibilitätsrichtlinie (MTD) mit Intune](../protect/mtd-device-compliance-policy-create.md).</p> |

## <a name="next-steps"></a>Nächste Schritte

Administratoren können die oben erläuterten Konfigurationsstufen in ihrer Ringbereitstellungsmethodologie für Testzwecke und zur Verwendung in der Produktion implementieren, indem das Beispiel für [JSON-Vorlagen für das Intune-App-Schutz-Richtlinienkonfigurationsframework](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AppProtectionPolicies) mit [PowerShell-Skripts von Intune](https://github.com/microsoftgraph/powershell-intune-samples) importiert wird.

## <a name="see-also"></a>Weitere Informationen:

- [Erstellen und Bereitstellen von App-Schutzrichtlinien mit Microsoft Intune](app-protection-policies.md)
- [Verfügbare Einstellungen für Schutzrichtlinien für Android-Apps mit Microsoft Intune](app-protection-policy-settings-android.md)
- [Einstellungen für App-Schutzrichtlinien für iOS](app-protection-policy-settings-ios.md)
- Apps von Drittanbietern wie beispielsweise die mobile Salesforce-App arbeiten auf eine bestimmte Weise mit Intune zusammen, um die Unternehmensdaten zu schützen. Weitere Informationen zur speziellen Zusammenarbeit der Salesforce-App mit Intune (einschließlich Konfigurationseinstellungen für die MDM-App) finden Sie unter [Salesforce-App und Microsoft Intune](https://gallery.technet.microsoft.com/Salesforce-App-and-Intune-c47d44ee/file/188000/1/Salesforce%20App%20and%20Intune%20for%20external.pdf).
