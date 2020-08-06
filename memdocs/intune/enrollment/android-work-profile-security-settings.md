---
title: Arbeitsprofil für Android Enterprise-Sicherheitskonfigurationen
titleSuffix: Microsoft Intune
description: Erfahren Sie, welche Einschränkungen und Einstellungen für die Sicherheitsstufen „Standard“ und „Hoch“ für Android Enterprise-Geräte vorgesehen sind.
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
ms.openlocfilehash: 4283caf8f21e87736b09a3d6c7b31f8daf1f6075
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546825"
---
# <a name="android-enterprise-work-profile-security-configurations"></a>Sicherheitskonfigurationen für Android Enterprise-Arbeitsprofile

Übernehmen Sie im Rahmen des [Frameworks für die Android Enterprise-Sicherheitskonfiguration](android-configuration-framework.md) die folgenden Einstellungen für mobile Benutzer mit Android Enterprise-Arbeitsprofil. Weitere Informationen zu den einzelnen Richtlinieneinstellungen finden Sie unter [Android Enterprise-Einstellungen, um Geräte mit Intune als konform oder nicht konform zu kennzeichnen](../protect/compliance-policy-create-android-for-work.md#work-profile) und [Android Enterprise-Geräteeinstellungen zum Zulassen oder Einschränken von Features mit Intune](../configuration/device-restrictions-android-for-work.md#work-profile-only).

Wenn Sie Ihre Einstellungen wählen, prüfen und kategorisieren Sie Nutzungsszenarien. Konfigurieren Sie anschließend Benutzer entsprechend der Anleitung für die gewählte Sicherheitsstufe. Sie können die vorgeschlagenen Einstellungen je nach den Bedürfnissen Ihrer Organisation festlegen. Achten Sie darauf, dass Ihr Sicherheitsteam die Bedrohungsumgebung, die Risikobereitschaft und die Auswirkungen auf die Nutzbarkeit beurteilt.

Für Arbeitsprofile auf benutzereigenen Geräten gibt es zwei empfohlene Frameworks für die Sicherheitskonfiguration:

- [Arbeitsprofilsicherheit „Standard“ (Stufe 1)](#work-profile-basic-security) 
- [Arbeitsprofilsicherheit „Hoch“ (Stufe 3)](#work-profile-high-security) 

> [!Note]
> Aufgrund der für Geräte mit Android Enterprise-Arbeitsprofil verfügbaren Einstellungen wird keine erhöhte Sicherheit (Stufe 2) geboten. Die verfügbaren Einstellungen begründen keinen Unterschied zwischen Stufe 1 und 2.

## <a name="work-profile-basic-security"></a>Arbeitsprofilsicherheit „Standard“

Stufe 1 ist die empfohlene Mindestsicherheitskonfiguration für persönliche Geräte, auf denen Benutzer auf Geschäfts-, Schul- oder Unidaten zugreifen. Diese Konfiguration eignet sich für die meisten mobilen Benutzer. Einige Steuerungsmöglichkeiten können sich auf die Servicequalität für Benutzer auswirken.

### <a name="device-compliance"></a>Gerätekonformität

| Abschnitt | Einstellung | Wert | Hinweise |
| ----- | ----- | ----- | ----- |
| Microsoft Defender ATP | Anfordern, dass das Gerät höchstens das angegebene Computerrisiko aufweist | Nicht konfiguriert ||
| Geräteintegrität | Gerät mit Rootzugriff | Blockieren ||
| Geräteintegrität | Anfordern, dass das Gerät höchstens der angegebenen Gerätebedrohungsstufe entspricht | Nicht konfiguriert||
| Geräteintegrität | Google Play Services ist konfiguriert | Erforderlich ||
| Geräteintegrität | Aktueller Sicherheitsanbieter | Erforderlich ||
| Geräteintegrität | SafetyNet-Gerätenachweis | Grundlegende Integrität und zertifizierte Geräte prüfen | Diese Einstellung konfiguriert SafetyNet Attestation von Google auf Endbenutzergeräten. Die Basisintegrität überprüft die Integrität des Geräts. Für gerootete Geräte, Emulatoren, virtuelle Geräte und Geräte, die Anzeichen von Manipulationen aufweisen, schlägt die Überprüfung der grundlegenden Integrität fehl.<p>Die Option „Basisintegrität und zertifizierte Geräte“ überprüft die Kompatibilität des Geräts mit Google-Diensten. Nur unveränderte Geräte, die von Google zertifiziert wurden, bestehen diese Überprüfung. |
| Geräteeigenschaften | Minimale Version des Betriebssystems | Format: Hauptversion.Nebenversion<br>Beispiel: 5.0| Microsoft empfiehlt das Konfigurieren der Mindesthauptversion für das Android-Betriebssystem, um übereinstimmende unterstützte Android-Versionen für Microsoft-Apps verwenden zu können. OEMs und Geräte, für die von Android Enterprise empfohlene Anforderungen gelten, müssen die aktuelle Versandversion und ein Upgrade auf die nächste Version unterstützen. Aktuell empfiehlt Android für Wissensarbeiter Android 8.0 und höher. Unter [Anforderungen für „Android Enterprise Recommended“](https://www.android.com/enterprise/recommended/requirements/) finden Sie die aktuellen Empfehlungen von Android. |
| Geräteeigenschaften | Maximale Version des Betriebssystems | Nicht konfiguriert ||
| Systemsicherheit | Anfordern eines Kennworts zum Entsperren mobiler Geräte | Erforderlich ||
| Systemsicherheit | Erforderlicher Kennworttyp | Numerisch, komplex | Organisationen müssen diese Festlegung möglicherweise entsprechend ihrer Kennwortrichtlinien aktualisieren. |
| Systemsicherheit | Minimale Kennwortlänge | 6 | Organisationen müssen diese Festlegung möglicherweise entsprechend ihrer Kennwortrichtlinien aktualisieren. |
| Systemsicherheit | Maximaler Zeitraum der Inaktivität (in Minuten) bis zur Anforderung eines Kennworts| 5 | Organisationen müssen diese Festlegung möglicherweise entsprechend ihrer Kennwortrichtlinien aktualisieren.|
| Systemsicherheit | Anzahl von Tagen bis zum Kennwortablauf| Nicht konfiguriert | Organisationen müssen diese Festlegung möglicherweise entsprechend ihrer Kennwortrichtlinien aktualisieren. |
| Systemsicherheit | Anzahl vorheriger Kennwörter, deren Wiederverwendung verhindert wird | Nicht konfiguriert | Organisationen müssen diese Festlegung möglicherweise entsprechend ihrer Kennwortrichtlinien aktualisieren. |
| Systemsicherheit | Verschlüsselung des Datenspeichers auf dem Gerät | Erforderlich ||
| Systemsicherheit | Apps von unbekannten Quellen blockieren | Blockieren ||
| Systemsicherheit | Laufzeitintegrität der Unternehmensportal-App | Erforderlich ||
| Systemsicherheit | USB-Debugging auf Gerät blockieren | Blockieren | Diese Festlegung blockiert zwar das Debuggen mit einem USB-Gerät, unterbindet aber auch die Möglichkeit, Protokolle zu erfassen, die bei der Problembehandlung nützlich sein können. |
| Systemsicherheit | Mindestens erforderliche Sicherheitspatchebene | Nicht konfiguriert | Android-Geräte können monatliche Sicherheitsupdates erhalten, aber das Release hängt von den OEMs und/oder Netzbetreibern ab. Unternehmen sollten dafür sorgen, dass bereitgestellte Android-Geräte Sicherheitsupdates erhalten, bevor diese Einstellung implementiert wird. Unter [Android-Sicherheitsbulletins](https://source.android.com/security/bulletin/) finden Sie die aktuellen Patchreleases. |
| Aktionen bei Nichtkonformität | Gerät als nicht konform markieren | Sofort | Standardmäßig ist die Richtlinie so konfiguriert, dass das Gerät als nicht konform markiert wird. Weitere Aktionen sind verfügbar. Weitere Informationen finden Sie unter [Konfigurieren von Aktionen für nicht konforme Geräte in Intune](../protect/actions-for-noncompliance.md).|

### <a name="device-restrictions"></a>Geräteeinschränkungen

| Abschnitt | Einstellung | Wert | Hinweise |
| ----- | ----- | ----- | ----- |
| Arbeitsprofileinstellungen | Kopieren und Einfügen zwischen Arbeitsprofilen und persönlichen Profilen | Blockieren ||
| Arbeitsprofileinstellungen | Datenaustausch zwischen Arbeitsprofilen und persönlichen Profilen | Apps im Arbeitsprofil können Freigabeanforderungen vom persönlichen Profil verarbeiten ||
| Arbeitsprofileinstellungen | Arbeitsprofilbenachrichtigungen bei Gerätesperre | Nicht konfiguriert | Das Sperren dieser Einstellung stellt sicher, dass sensible Daten in den Arbeitsprofilbenachrichtigungen nicht verfügbar gemacht werden, was die Nutzbarkeit beeinträchtigen könnte. |
| Arbeitsprofileinstellungen | Standardmäßige App-Berechtigungen | Gerätestandard | Administratoren müssen die Berechtigungen überprüfen und anpassen, die von Apps gewährt werden, die sie bereitstellen. |
| Arbeitsprofileinstellungen | Konten hinzufügen und entfernen | Blockieren ||
| Arbeitsprofileinstellungen | Kontaktfreigabe über Bluetooth | Aktivieren | Standardmäßig ist der Zugriff auf Geschäftskontakte auf anderen Geräten, wie z. B. im Auto, über die Bluetooth-Integration nicht möglich. Durch Aktivieren dieser Einstellung werden die Freisprechfunktionen für Benutzer verbessert. Das Bluetooth-Gerät kann die Kontakte jedoch bei der ersten Verbindung zwischenspeichern. Organisationen müssen bei der Implementierung dieser Einstellung die Nutzbarkeitsszenarien mit Datenschutzbedenken abwägen. |
| Arbeitsprofileinstellungen | Bildschirmaufnahme | Blockieren ||
| Arbeitsprofileinstellungen | Anrufer-ID des Arbeitskontakts im persönlichen Profil anzeigen | Nicht konfiguriert ||
| Arbeitsprofileinstellungen | Im persönlichen Profil nach Geschäftskontakten suchen | Nicht konfiguriert | Das Blockieren des Zugriffs von Benutzern auf Geschäftskontakte im persönlichen Profil kann sich auf bestimmte Nutzbarkeitsszenarien wie SMS und Wählverbindungen innerhalb des persönlichen Profils auswirken. Organisationen müssen bei der Implementierung dieser Einstellung die Nutzbarkeitsszenarien mit Datenschutzbedenken abwägen. |
| Arbeitsprofileinstellungen | Kamera | Nicht konfiguriert ||
| Arbeitsprofileinstellungen | Widgets aus Arbeitsprofil-Apps zulassen | Aktivieren ||
| Arbeitsprofileinstellungen | Arbeitsprofilkennwort erforderlich | Erforderlich ||
| Arbeitsprofileinstellungen | Minimale Kennwortlänge | 6 | Organisationen müssen diese Festlegung möglicherweise entsprechend ihrer Kennwortrichtlinien aktualisieren. |
| Arbeitsprofileinstellungen | Maximaler Zeitraum der Inaktivität (in Minuten) bis zur Sperrung des Arbeitsprofils| 5 | Organisationen müssen diese Festlegung möglicherweise entsprechend ihrer Kennwortrichtlinien aktualisieren. |
| Arbeitsprofileinstellungen | Anzahl von Anmeldefehlern, bevor das Arbeitsprofil zurückgesetzt wird| 10 | Organisationen müssen diese Festlegung möglicherweise entsprechend ihrer Kennwortrichtlinien aktualisieren. |
| Arbeitsprofileinstellungen | Kennwortablauf (Tage) | Nicht konfiguriert | Organisationen müssen diese Festlegung möglicherweise entsprechend ihrer Kennwortrichtlinien aktualisieren. |
| Arbeitsprofileinstellungen | Erforderlicher Kennworttyp | Numerisch, komplex ||
| Arbeitsprofileinstellungen | Wiederverwendung vorheriger Kennwörter verhindern | Nicht konfiguriert | Organisationen müssen diese Festlegung möglicherweise entsprechend ihrer Kennwortrichtlinien aktualisieren.|
| Arbeitsprofileinstellungen | Entsperrung durch Fingerabdruck | Nicht konfiguriert ||
| Arbeitsprofileinstellungen | Smart Lock und andere Vertrauens-Agents | Nicht konfiguriert |||
| Gerätekennwort | Minimale Kennwortlänge | 6 | Organisationen müssen diese Festlegung möglicherweise entsprechend ihrer Kennwortrichtlinien aktualisieren. |
| Gerätekennwort | Maximaler Zeitraum der Inaktivität (in Minuten) bis zur Bildschirmsperrung | 5 | Organisationen müssen diese Festlegung möglicherweise entsprechend ihrer Kennwortrichtlinien aktualisieren. |
| Gerätekennwort | Anzahl von fehlgeschlagenen Anmeldungen, bevor das Gerät zurückgesetzt wird | 10 | Mit dieser Festlegung wird ein Löschen des Arbeitsprofils und nicht ein Zurücksetzen des Geräts ausgelöst. |
| Gerätekennwort | Kennwortablauf (Tage) | Nicht konfiguriert | Organisationen müssen diese Festlegung möglicherweise entsprechend ihrer Kennwortrichtlinien aktualisieren. |
| Gerätekennwort | Erforderlicher Kennworttyp | Numerisch, komplex ||
| Gerätekennwort | Wiederverwendung vorheriger Kennwörter verhindern | Nicht konfiguriert | Organisationen müssen diese Festlegung möglicherweise entsprechend ihrer Kennwortrichtlinien aktualisieren. |
| Gerätekennwort | Entsperrung durch Fingerabdruck | Nicht konfiguriert ||
| Gerätekennwort | Smart Lock und andere Vertrauens-Agents | Nicht konfiguriert ||
| Systemsicherheit | Bedrohungsüberprüfung für Apps | Erforderlich | Diese Einstellung sorgt dafür, dass die Verify Apps-Überprüfung von Google für Endbenutzergeräte aktiviert ist. Wenn diese Einstellung konfiguriert ist, wird der Zugriff für den Endbenutzer so lange gesperrt, bis er auf seinem Android-Gerät die App-Überprüfung von Google aktiviert. |
| Systemsicherheit | App-Installationen aus unbekannten Quellen im persönlichen Profil verhindern | Blockieren ||

> [!Note]
> Wenn das Android Enterprise-Arbeitsprofil aktiviert wird, ist One Lock standardmäßig konfiguriert, um Passcodes von Gerät und Arbeitsprofil zu kombinieren. One Lock kann deaktiviert werden, um unter den Arbeitsprofileinstellungen bei Bedarf Passcodes von Arbeitsprofil und Gerät zu trennen.

## <a name="work-profile-high-security"></a>Arbeitsprofilsicherheit „Hoch“

Stufe 3 ist die empfohlene Konfiguration für Geräte, die von Benutzern oder Gruppen mit besonders hohem Risiko verwendet werden. Beispielsweise Benutzer, die mit äußerst sensiblen Daten umgehen, bei denen eine unbefugte Preisgabe erhebliche materielle Verluste verursacht. Eine Organisation, die wahrscheinlich von finanzkräftigen und raffinierten Gegnern ins Visier genommen wird, benötigt die nachstehend beschriebenen zusätzlichen Einschränkungen. Diese Konfiguration erweitert die Konfiguration der Stufe 1 um Folgendes:
- Implementieren von Mobile Threat Defense oder Microsoft Defender ATP
- Einschränken von Szenarien für Arbeitsprofildaten
- Erzwingen strengerer Kennwortrichtlinien

Die auf Stufe 3 erzwungenen Richtlinieneinstellungen umfassen alle für Stufe 1 empfohlenen Richtlinieneinstellungen. Die nachstehend aufgeführten Einstellungen sind jedoch nur diejenigen, die hinzugefügt oder geändert wurden. Diese Einstellungen haben möglicherweise eine etwas größere Auswirkung auf Benutzer oder Anwendungen. Sie erzwingen ein Sicherheitsniveau, das besser den Risiken entspricht, denen Benutzer mit Zugriff auf sensible Daten auf mobilen Geräten ausgesetzt sind.

### <a name="device-compliance"></a>Gerätekonformität

| Abschnitt | Einstellung | Wert | Hinweise |
| ----- | ----- | ----- | ----- |
| Microsoft Defender ATP | Anfordern, dass das Gerät höchstens das angegebene Computerrisiko aufweist | Löschen | Diese Einstellung erfordert Microsoft Defender ATP. Weitere Informationen finden Sie unter [Erzwingen der Konformität für Microsoft Defender ATP mit bedingtem Zugriff in Intune](../protect/advanced-threat-protection.md).<p>Kunden sollten die Implementierung von Microsoft Defender ATP oder einer Mobile Threat Defense-Lösung in Betracht ziehen. Es ist nicht notwendig, beide Lösungen bereitzustellen. |
| Geräteintegrität | Anfordern, dass das Gerät höchstens der angegebenen Gerätebedrohungsstufe entspricht | Geschützt | Diese Einstellung erfordert ein Mobile Threat Defense-Produkt. Weitere Informationen finden Sie unter [Mobile Threat Defense für registrierte Geräte](../protect/mtd-device-compliance-policy-create.md).<p>Kunden sollten die Implementierung von Microsoft Defender ATP oder einer Mobile Threat Defense-Lösung in Betracht ziehen. Es ist nicht notwendig, beide Lösungen bereitzustellen.|
| Geräteeigenschaften | Minimale Version des Betriebssystems | Format: Hauptversion.Nebenversion<br>Beispiel: 8.0| Microsoft empfiehlt das Konfigurieren der Mindesthauptversion für das Android-Betriebssystem, um übereinstimmende unterstützte Android-Versionen für Microsoft-Apps verwenden zu können. OEMs und Geräte, für die von Android Enterprise empfohlene Anforderungen gelten, müssen die aktuelle Versandversion und ein Upgrade auf die nächste Version unterstützen. Aktuell empfiehlt Android für Wissensarbeiter Android 8.0 und höher. Unter „Anforderungen für Android Enterprise Recommended“ finden Sie die aktuellen Empfehlungen von Android. |
| Systemsicherheit | Anzahl von Tagen bis zum Kennwortablauf | 365 | Organisationen müssen diese Festlegung möglicherweise entsprechend ihrer Kennwortrichtlinien aktualisieren. |
| Systemsicherheit | Anzahl vorheriger Kennwörter, deren Wiederverwendung verhindert wird | 5 | Organisationen müssen diese Festlegung möglicherweise entsprechend ihrer Kennwortrichtlinien aktualisieren. |


### <a name="device-restrictions"></a>Geräteeinschränkungen

| Abschnitt | Einstellung | Wert | Hinweise |
| ----- | ----- | ----- | ----- |
| Arbeitsprofileinstellungen | Arbeitsprofilbenachrichtigungen bei Gerätesperre | Blockieren | Das Sperren dieser Einstellung stellt sicher, dass sensible Daten in den Arbeitsprofilbenachrichtigungen nicht verfügbar gemacht werden, was die Nutzbarkeit beeinträchtigen könnte. |
| Arbeitsprofileinstellungen | Kontaktfreigabe über Bluetooth | Nicht konfiguriert | Standardmäßig ist der Zugriff auf Geschäftskontakte auf anderen Geräten, wie z. B. im Auto, über die Bluetooth-Integration nicht möglich. Durch Aktivieren dieser Einstellung werden die Freisprechfunktionen für Benutzer verbessert. Das Bluetooth-Gerät kann die Kontakte jedoch bei der ersten Verbindung zwischenspeichern. Organisationen müssen bei der Implementierung dieser Einstellung die Nutzbarkeitsszenarien mit Datenschutzbedenken abwägen. |
| Arbeitsprofileinstellungen | Im persönlichen Profil nach Geschäftskontakten suchen | Blockieren | Das Blockieren des Zugriffs von Benutzern auf Geschäftskontakte im persönlichen Profil kann sich auf bestimmte Nutzbarkeitsszenarien wie SMS und Wählverbindungen innerhalb des persönlichen Profils auswirken. Organisationen müssen bei der Implementierung dieser Einstellung die Nutzbarkeitsszenarien mit Datenschutzbedenken abwägen. |
| Arbeitsprofileinstellungen | Widgets aus Arbeitsprofil-Apps zulassen | Nicht konfiguriert ||
| Arbeitsprofileinstellungen | Anzahl von Anmeldefehlern, bevor das Arbeitsprofil zurückgesetzt wird | 5 | Organisationen müssen diese Festlegung möglicherweise entsprechend ihrer Kennwortrichtlinien aktualisieren. |
| Arbeitsprofileinstellungen | Kennwortablauf (Tage) | 365 | Organisationen müssen diese Festlegung möglicherweise entsprechend ihrer Kennwortrichtlinien aktualisieren. |
| Arbeitsprofileinstellungen | Wiederverwendung vorheriger Kennwörter verhindern | 5 | Organisationen müssen diese Festlegung möglicherweise entsprechend ihrer Kennwortrichtlinien aktualisieren. |
| Arbeitsprofileinstellungen | Smart Lock und andere Vertrauens-Agents | Blockieren ||
| Gerätekennwort | Anzahl von fehlgeschlagenen Anmeldungen, bevor das Gerät zurückgesetzt wird | 5 | Mit dieser Festlegung wird ein Löschen des Arbeitsprofils und nicht ein Zurücksetzen des Geräts ausgelöst. |
| Gerätekennwort | Kennwortablauf (Tage) | 365 | Organisationen müssen diese Festlegung möglicherweise entsprechend ihrer Kennwortrichtlinien aktualisieren. |
| Gerätekennwort | Wiederverwendung vorheriger Kennwörter verhindern | 5 | Organisationen müssen diese Festlegung möglicherweise entsprechend ihrer Kennwortrichtlinien aktualisieren. |

## <a name="next-steps"></a>Nächste Schritte

Administratoren können die oben erläuterten Konfigurationsstufen in ihrer Ringbereitstellungsmethododik für Test- und Produktionszwecke implementieren, indem das Beispiel für [JSON-Vorlagen für das Framework für die Android Enterprise-Sicherheitskonfiguration](https://github.com/microsoft/Intune-Config-Frameworks/tree/master/AndroidEnterprise) mit [PowerShell-Skripts von Intune](https://github.com/microsoftgraph/powershell-intune-samples) importiert wird.
