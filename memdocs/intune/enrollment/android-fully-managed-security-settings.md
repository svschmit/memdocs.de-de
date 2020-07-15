---
title: Vollständig verwaltete Android Enterprise-Sicherheitskonfigurationen
titleSuffix: Microsoft Intune
description: Lernen Sie die vorgeschlagenen Einstellungen für die vollständig verwaltete Android Enterprise-Sicherheitskonfiguration „Standard“, „Erhöht“ und „Hoch“ kennen.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 06/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: rosssmi
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure;seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 99b17cc165fc8d24fdf1b0f48525f3b23d8cc9b7
ms.sourcegitcommit: d647eefa23c8849f49584442df568284d51d7525
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/09/2020
ms.locfileid: "86195632"
---
# <a name="android-enterprise-fully-managed-security-configurations"></a>Vollständig verwaltete Android Enterprise-Sicherheitskonfigurationen

Übernehmen Sie im Rahmen des [Frameworks für die Android Enterprise-Sicherheitskonfiguration](android-configuration-framework.md) die folgenden Einstellungen für vollständig verwaltete mobile Android Enterprise-Benutzer. Weitere Informationen zu den einzelnen Richtlinieneinstellungen finden Sie unter [Android Enterprise-Einstellungen, um Geräte mit Intune als konform oder nicht konform zu kennzeichnen](../protect/compliance-policy-create-android-for-work.md#device-owner) und [Android Enterprise-Geräteeinstellungen zum Zulassen oder Einschränken von Features mit Intune](../configuration/device-restrictions-android-for-work.md#device-owner-only).

Wenn Sie Ihre Einstellungen wählen, prüfen und kategorisieren Sie Nutzungsszenarien. Konfigurieren Sie anschließend Benutzer entsprechend der Anleitung für die gewählte Sicherheitsstufe. Sie können die vorgeschlagenen Einstellungen je nach den Bedürfnissen Ihrer Organisation festlegen. Achten Sie darauf, dass Ihr Sicherheitsteam die Bedrohungsumgebung, die Risikobereitschaft und die Auswirkungen auf die Nutzbarkeit beurteilt.

Für vollständig verwaltete unternehmenseigene Geräte gibt es drei empfohlene Frameworks für die Sicherheitskonfiguration:

- [Vollständig verwaltete Standardsicherheit (Stufe 1)](#fully-managed-basic-security) 
- [Vollständig verwaltete erhöhte Sicherheit (Stufe 2)](#fully-managed-enhanced-security)
- [Vollständig verwaltete hohe Sicherheit (Stufe 3)](#fully-managed-high-security) 

## <a name="fully-managed-basic-security"></a>Vollständig verwaltete Standardsicherheit

Stufe 1 ist die empfohlene Mindestsicherheitskonfiguration für organisationseigene mobile Geräte.

Die Richtlinien der Stufe 1 erzwingen einen angemessenen Zugriff auf Datenebene bei gleichzeitiger Minimierung der Auswirkungen auf Benutzer. Dies geschieht durch Erzwingen von Kennwortrichtlinien, einer Mindestbetriebssystemversion, einem SafetyNet-Gerätenachweis und der Deaktivierung bestimmter Gerätefunktionen (wie Dateiübertragungen per USB). 

### <a name="device-compliance"></a>Gerätekonformität

| Abschnitt | Einstellung | Wert | Hinweise |
| ----- | ----- | ----- | ----- |
| Microsoft Defender ATP | Anfordern, dass das Gerät höchstens das angegebene Computerrisiko aufweist | Nicht konfiguriert ||
| Geräteintegrität | Anfordern, dass das Gerät höchstens der angegebenen Gerätebedrohungsstufe entspricht | Nicht konfiguriert||
| Geräteintegrität | SafetyNet-Gerätenachweis | Grundlegende Integrität und zertifizierte Geräte prüfen | Diese Einstellung konfiguriert SafetyNet Attestation von Google auf Endbenutzergeräten. Die Basisintegrität überprüft die Integrität des Geräts. Für gerootete Geräte, Emulatoren, virtuelle Geräte und Geräte, die Anzeichen von Manipulationen aufweisen, schlägt die Überprüfung der grundlegenden Integrität fehl.<br>Die Option „Basisintegrität und zertifizierte Geräte“ überprüft die Kompatibilität des Geräts mit Google-Diensten. Nur unveränderte Geräte, die von Google zertifiziert wurden, bestehen diese Überprüfung. |
| Geräteeigenschaften | Minimale Version des Betriebssystems | Format: Hauptversion.Nebenversion<br>Beispiel: 8.0| Microsoft empfiehlt das Konfigurieren der Mindesthauptversion für das Android-Betriebssystem, um übereinstimmende unterstützte Android-Versionen für Microsoft-Apps verwenden zu können. OEMs und Geräte, für die von Android Enterprise empfohlene Anforderungen gelten, müssen die aktuelle Versandversion und ein Upgrade auf die nächste Version unterstützen. Aktuell empfiehlt Android für Wissensarbeiter Android 8.0 und höher. Unter [Anforderungen für „Android Enterprise Recommended“](https://www.android.com/enterprise/recommended/requirements/) finden Sie die aktuellen Empfehlungen von Android. |
| Geräteeigenschaften | Maximale Version des Betriebssystems | Nicht konfiguriert ||
| Geräteeigenschaften | Mindestens erforderliche Sicherheitspatchebene | Nicht konfiguriert | Android-Geräte können monatliche Sicherheitsupdates erhalten, aber das Release hängt von den OEMs und/oder Netzbetreibern ab. Unternehmen sollten dafür sorgen, dass bereitgestellte Android-Geräte Sicherheitsupdates erhalten, bevor diese Einstellung implementiert wird. Unter [Android-Sicherheitsbulletins](https://source.android.com/security/bulletin/) finden Sie die aktuellen Patchreleases. |
| Systemsicherheit | Anfordern eines Kennworts zum Entsperren mobiler Geräte | Erforderlich ||
| Systemsicherheit | Erforderlicher Kennworttyp | Numerisch, komplex | Organisationen müssen diese Festlegung möglicherweise entsprechend ihrer Kennwortrichtlinien aktualisieren. |
| Systemsicherheit | Minimale Kennwortlänge | 6 | Organisationen müssen diese Festlegung möglicherweise entsprechend ihrer Kennwortrichtlinien aktualisieren. |
| Systemsicherheit | Maximaler Zeitraum der Inaktivität (in Minuten) bis zur Anforderung eines Kennworts| 5 | Organisationen müssen diese Festlegung möglicherweise entsprechend ihrer Kennwortrichtlinien aktualisieren.|
| Systemsicherheit | Anzahl von Tagen bis zum Kennwortablauf| Nicht konfiguriert ||
| Systemsicherheit |    Anzahl erforderlicher Kennwörter, bevor ein Benutzer ein Kennwort wiederverwenden kann | Nicht konfiguriert ||
| Systemsicherheit | Verschlüsselung des Datenspeichers auf dem Gerät | Erforderlich ||
| Aktionen bei Nichtkonformität | Gerät als nicht konform markieren | Sofort | Standardmäßig ist die Richtlinie so konfiguriert, dass das Gerät als nicht konform markiert wird. Weitere Aktionen sind verfügbar. Weitere Informationen finden Sie unter [Konfigurieren von Aktionen für nicht konforme Geräte in Intune](../protect/actions-for-noncompliance.md).|

### <a name="device-restrictions"></a>Geräteeinschränkungen

| Abschnitt | Einstellung | Wert | Hinweise |
| ----- | ----- | ----- | ----- |
| Allgemein | Bildschirmaufnahme | Nicht konfiguriert ||
| Allgemein | Kamera | Nicht konfiguriert ||
| Allgemein | Standardberechtigungsrichtlinie | Gerätestandard ||
| Allgemein | Datums- und Uhrzeitänderungen | Nicht konfiguriert ||
| Allgemein | Änderung der Lautstärke | Nicht konfiguriert ||
| Allgemein | Wiederherstellung der Herstellerstandards | Blockieren ||
| Allgemein | Abgesicherter Start | Blockieren ||
| Allgemein | Statusleiste | Nicht konfiguriert ||
| Allgemein | Roamingdatendienste | Nicht konfiguriert ||
| Allgemein | Änderung der WLAN-Einstellungen | Nicht konfiguriert ||
| Allgemein | Bluetooth-Konfiguration | Nicht konfiguriert ||
| Allgemein | Tethering und Zugriff auf Hotspots | Nicht konfiguriert ||
| Allgemein | USB-Speicher | Nicht konfiguriert ||
| Allgemein | USB-Dateiübertragung | Blockieren ||
| Allgemein | Externe Medien | Blockieren ||
| Allgemein | Daten mithilfe von NFC übertragen | Nicht konfiguriert ||
| Allgemein | Debugfunktionen | Nicht konfiguriert ||
| Allgemein | Mikrofonanpassung | Nicht konfiguriert ||
| Allgemein | E-Mail-Adressen für Schutz vor Zurücksetzung auf Werkseinstellungen | Nicht konfiguriert ||
| Allgemein | Notausstieg für Netzwerk | Nicht konfiguriert ||
| Allgemein | Systemupdate | Automatisch ||
| Allgemein | Benachrichtigungsfenster | Nicht konfiguriert ||
| Allgemein | Hinweise zur ersten Verwendung überspringen | Nicht konfiguriert ||
| Systemsicherheit | Bedrohungsüberprüfung für Apps |Erforderlich ||
| Benutzeroberfläche des Geräts | Registrierungsprofiltyp | Vollständig verwaltet ||
| Benutzeroberfläche des Geräts | Über Microsoft Launcher als Standardstartprogramm festlegen | Nicht konfiguriert | Unternehmen können sich für die Implementierung von Microsoft Launcher entscheiden, um eine einheitliche Startbildschirmerfahrung auf vollständig verwalteten Geräten zu gewährleisten. Weitere Informationen finden Sie im Artikel zum [Einrichten von Microsoft Launcher auf vollständig verwalteten Android Enterprise-Geräten mit Intune](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-launcher-on-android-enterprise-fully/ba-p/1482134). |
| Kennwort | Sperrbildschirm deaktivieren | Nicht konfiguriert ||
| Kennwort | Deaktivierte Sperrbildschirmfeatures | 0 ausgewählt ||
| Kennwort | Erforderlicher Kennworttyp | Numerisch, komplex ||
| Kennwort | Minimale Kennwortlänge | 6 ||
| Kennwort | Anzahl von Tagen bis zum Kennwortablauf | Nicht konfiguriert ||
| Kennwort | Anzahl erforderlicher Kennwörter, bevor ein Benutzer ein Kennwort wiederverwenden kann | Nicht konfiguriert ||
| Kennwort | Anzahl von fehlgeschlagenen Anmeldungen, bevor das Gerät zurückgesetzt wird | 10 ||
| Energieeinstellungen | Zeit bis Bildschirmsperre | 5 ||
| Energieeinstellungen | Bildschirm aktiviert, wenn Gerät angeschlossen ist | Nicht konfiguriert ||
| Benutzer und Konten | Neue Benutzer hinzufügen | Nicht konfiguriert ||
| Benutzer und Konten | Entfernen von Benutzern | Nicht konfiguriert ||
| Benutzer und Konten | Kontoänderungen (nur dedizierte Geräte) | Nicht konfiguriert ||
| Benutzer und Konten | Persönliche Google-Konten | Nicht konfiguriert ||
| Benutzer und Konten | Benutzer kann Anmeldeinformationen konfigurieren | Blockieren ||
| Applications | Installation aus unbekannten Quellen zulassen | Nicht konfiguriert ||
| Applications | Zugriff auf alle Apps im Google Play Store zulassen | Nicht konfiguriert | Standardmäßig können Benutzer persönliche Apps aus dem Google Play Store nicht auf vollständig verwalteten Geräten installieren. Wenn Organisationen die Nutzung vollständig verwalteter Geräte für persönliche Zwecke zulassen möchten, erwägen Sie die Änderung dieser Einstellung. |
| Applications | Automatische App-Updates | Nur WLAN | Organisationen sollten diese Einstellung bei Bedarf anpassen, da bei Aktualisierungen von Apps über das Mobilfunknetz Gebühren anfallen können. |

## <a name="fully-managed-enhanced-security"></a>Vollständig verwaltete erhöhte Sicherheit

Stufe 2 ist die empfohlene Konfiguration für unternehmenseigene Geräte, auf denen Benutzer auf sensiblere Informationen zugreifen. Heutzutage sind diese Geräte in Unternehmen oftmals Angriffen ausgesetzt. Diese Einstellungen setzen keinen großen Stab hochqualifizierter Sicherheitsfachleute voraus. Daher sollten sie für die meisten Unternehmensorganisationen zugänglich sein. Diese Konfiguration baut auf der Konfiguration der Stufe 1 dahingehend auf, dass strengere Kennwortrichtlinien gelten und Funktionen für Benutzer/Konten deaktiviert werden.

Die Einstellung auf Stufe 2 umfassen alle für Stufe 1 empfohlenen Richtlinieneinstellungen. Die nachstehend aufgeführten Einstellungen sind jedoch nur diejenigen, die hinzugefügt oder geändert wurden. Diese Einstellungen haben möglicherweise eine etwas größere Auswirkung auf Benutzer oder Anwendungen. Sie erzwingen ein Sicherheitsniveau, das besser den Risiken entspricht, denen Benutzer mit Zugriff auf sensible Daten auf mobilen Geräten ausgesetzt sind.

### <a name="device-compliance"></a>Gerätekonformität

| Abschnitt | Einstellung | Wert | Hinweise |
| ----- | ----- | ----- | ----- |
| Systemsicherheit | Anzahl von Tagen bis zum Kennwortablauf | 365 | Organisationen müssen diese Festlegung möglicherweise entsprechend ihrer Kennwortrichtlinien aktualisieren. |
| Systemsicherheit |    Anzahl erforderlicher Kennwörter, bevor ein Benutzer ein Kennwort wiederverwenden kann | 5 | Organisationen müssen diese Festlegung möglicherweise entsprechend ihrer Kennwortrichtlinien aktualisieren. |

### <a name="device-restrictions"></a>Geräteeinschränkungen

| Abschnitt | Einstellung | Wert | Hinweise |
| ----- | ----- | ----- | ----- |
| Allgemein | E-Mail-Adressen für Schutz vor Zurücksetzung auf Werkseinstellungen | E-Mail-Adressen für Google-Konto ||
| Allgemein | Liste der E-Mail-Adressen (nur Option „E-Mail-Adressen für Google-Konto“) | example@gmail.com | Aktualisieren Sie diese Richtlinie manuell, um die Google-E-Mail-Adressen von Geräteadministratoren anzugeben, die die Geräte nach dem Zurücksetzen entsperren können. |
| Gerätekennwort | Anzahl von Tagen bis zum Kennwortablauf | 365 | Organisationen müssen diese Festlegung möglicherweise entsprechend ihrer Kennwortrichtlinien aktualisieren. |
| Gerätekennwort | Anzahl erforderlicher Kennwörter, bevor ein Benutzer ein Kennwort wiederverwenden kann | 5 | Organisationen müssen diese Festlegung möglicherweise entsprechend ihrer Kennwortrichtlinien aktualisieren. |
| Gerätekennwort | Anzahl von fehlgeschlagenen Anmeldungen, bevor das Gerät zurückgesetzt wird | 5 ||
| Benutzer und Konten | Neue Benutzer hinzufügen | Blockieren ||
| Benutzer und Konten | Entfernen von Benutzern | Blockieren ||
| Benutzer und Konten | Persönliche Google-Konten | Blockieren ||

## <a name="fully-managed-high-security"></a>Vollständig verwaltete hohe Sicherheit

Stufe 3 ist die empfohlene Konfiguration für Folgendes:
- Organisationen mit großen und ausgereiften Sicherheitsabteilungen
- Bestimmte Benutzer und Gruppen, auf die Angreifer besonders abzielen
Auf solche Organisationen wird oft von mit hohen finanziellen Mitteln und umfassenden Know-how ausgestatteten Angreifern abgezielt. Deshalb benötigen die zusätzlichen beschriebenen Einschränkungen und Steuerungsmöglichkeiten.

Diese Konfiguration erweitert die Stufe 2 um Folgendes:
- Erhöhen der Mindestbetriebssystemversion
- Sicherstellen, dass das Gerät konform ist, indem die sichersten Microsoft Defender ATP- oder Mobile Threat Defense-Stufe erzwungen wird
- Erhöhen der Mindestbetriebssystemversion
- Erzwingen zusätzlicher Geräteeinschränkungen (z. B. Deaktivieren unbearbeiteter Benachrichtigungen auf dem Sperrbildschirm)
- Anfordern, dass Apps immer auf dem neuesten Stand sein müssen 

Die auf Stufe 3 erzwungenen Richtlinieneinstellungen umfassen alle für Stufe 2 empfohlenen Richtlinieneinstellungen. Die nachstehend aufgeführten Einstellungen sind nur diejenigen, die hinzugefügt oder geändert wurden. Diese Einstellungen haben möglicherweise eine erhebliche Auswirkung auf Benutzer oder Anwendungen. Sie erzwingen ein Sicherheitsniveau, das eher den Risiken entspricht, denen die anvisierten Organisationen ausgesetzt sind.


### <a name="device-compliance"></a>Gerätekonformität

| Abschnitt | Einstellung | Wert | Hinweise |
| ----- | ----- | ----- | ----- |
| Microsoft Defender ATP | Anfordern, dass das Gerät höchstens das angegebene Computerrisiko aufweist | Löschen | Diese Einstellung erfordert Microsoft Defender ATP. Weitere Informationen finden Sie unter [Erzwingen der Konformität für Microsoft Defender ATP mit bedingtem Zugriff in Intune](../protect/advanced-threat-protection.md).<p> Kunden sollten die Implementierung von Microsoft Defender ATP oder einer Mobile Threat Defense-Lösung in Betracht ziehen. Es ist nicht notwendig, beide Lösungen bereitzustellen. |
| Geräteintegrität | Anfordern, dass das Gerät höchstens der angegebenen Gerätebedrohungsstufe entspricht | Geschützt | Diese Einstellung erfordert ein Mobile Threat Defense-Produkt. Weitere Informationen finden Sie unter [Mobile Threat Defense für registrierte Geräte](../protect/mtd-device-compliance-policy-create.md).<p>Kunden sollten die Implementierung von Microsoft Defender ATP oder einer Mobile Threat Defense-Lösung in Betracht ziehen. Es ist nicht notwendig, beide Lösungen bereitzustellen.|
| Geräteeigenschaften | Minimale Version des Betriebssystems | Format: Hauptversion.Nebenversion<br>Beispiel: 10.0| Microsoft empfiehlt das Konfigurieren der Mindesthauptversion für das Android-Betriebssystem, um übereinstimmende unterstützte Android-Versionen für Microsoft-Apps verwenden zu können. OEMs und Geräte, für die von Android Enterprise empfohlene Anforderungen gelten, müssen die aktuelle Versandversion und ein Upgrade auf die nächste Version unterstützen. Aktuell empfiehlt Android für Wissensarbeiter Android 8.0 und höher. Unter „Anforderungen für Android Enterprise Recommended“ finden Sie die aktuellen Empfehlungen von Android. |

### <a name="device-restrictions"></a>Geräteeinschränkungen

| Abschnitt | Einstellung | Wert | Hinweise |
| ----- | ----- | ----- | ----- |
| Allgemein | Datums- und Uhrzeitänderungen | Blockieren ||
| Allgemein | Tethering und Zugriff auf Hotspots | Blockieren ||
| Allgemein | Daten mithilfe von NFC übertragen | Blockieren ||
| Gerätekennwort | Deaktivierte Sperrbildschirmfeatures | Vertrauens-Agents, Unbearbeitete Benachrichtigungen ||
| Applications | Automatische App-Updates | Immer | Organisationen sollten diese Einstellung bei Bedarf anpassen, da bei Aktualisierungen von Apps über das Mobilfunknetz Gebühren anfallen können. |


## <a name="next-steps"></a>Nächste Schritte

Administratoren können die oben erläuterten Konfigurationsstufen in ihrer Ringbereitstellungsmethododik für Test- und Produktionszwecke implementieren, indem das Beispiel für [JSON-Vorlagen für das Framework für die Android Enterprise-Sicherheitskonfiguration](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AndroidEnterprise) mit [PowerShell-Skripts von Intune](https://github.com/microsoftgraph/powershell-intune-samples) importiert wird.
