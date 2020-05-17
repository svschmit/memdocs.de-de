---
title: Bewertung der Kompatibilität
titleSuffix: Configuration Manager
description: In diesem Artikel wird die Bewertung der Kompatibilität für Windows-Apps und -Treiber in Desktop Analytics erläutert.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: ea78f726-b1b3-49b0-8141-d916be48c458
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 7b2bff4f8365693c86540c9b0578307340f13a49
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268894"
---
# <a name="compatibility-assessment-in-desktop-analytics"></a>Kompatibilitätsbewertung in Desktop Analytics

Bei vorherigen Lösungen war die Upgradebewertung generisch. Beispiele: „Eingreifen erforderlich“ oder „Korrektur verfügbar“. Sie bieten keinerlei visuelle Indikatoren dazu, wie Apps oder Treiber mit Problemen oder Upgrade-Erkenntnisse zu priorisieren sind. In Desktop Analytics wird dieses Feature durch **Kompatibilitätsrisiko** ersetzt. In Desktop Analytics wird die Bewertung für Apps nur in der Bereitstellungsansicht für ein Vor-Upgrade-Szenario angezeigt. Die Apps werden auf der Grundlage von Erkenntnissen kategorisiert, die Microsoft anhand der Computer in einem aktuellen Bereitstellungsplan gewinnt.

Desktop Analytics verwendet die folgenden Kategorien zur Kompatibilitätsbewertung:

- **Niedrig:** Der Dienst hat keine Anzeichen gefunden, die auf ein Risiko für die App bei einem Windows-Upgrade hindeuten. Es ist wahrscheinlich, dass sie im Zielbetriebssystem unverändert funktioniert.

- **Mittel**: Analytics gibt an, dass der Funktionsumfang der Anwendung möglicherweise beeinträchtigt wird, obgleich Gegenmaßnahmen wahrscheinlich möglich sind.

- **Hoch**: Die Anwendung kann während des Upgrades oder danach mit hoher Wahrscheinlichkeit nicht ausgeführt werden. Eine Gegenmaßnahme ist möglicherweise erforderlich.

- **Unbekannt**: Die App wurde nicht bewertet. Es gibt keine sonstigen Erkenntnisse wie z. B. *MS bekannte Probleme* oder *Ready for Windows*.

In der Liste der App- oder Treiberobjekte in einem Bereitstellungsplan sehen Sie diesen Wert für jedes Objekt in der Spalte **Kompatibilitätsrisiko**.

## <a name="app-risk-assessment"></a>Risikobewertung für Apps

![Diagramm der Quellen für die App-Risikobewertung](media/app-risk-assessment-sources.png)

Es gibt eine Reihe von Quellen, anhand derer Desktop Analytics die Bewertung für Anwendungen generiert:

- [MS bekannte Probleme](#microsoft-known-issues)
- [Ready for Windows](#ready-for-windows)
- [Umfassendere Erkenntnisse](#advanced-insights)

Die Bewertung für die einzelnen Quellen zur App wird in Desktop Analytics angegeben. Wählen Sie in der Liste der App-Objekte in einem Bereitstellungsplan eine einzelne App aus, um ihren Flyout-Eigenschaftenbereich zu öffnen. Eine Gesamtempfehlungs- und Bewertungsebene wird angezeigt. Im Abschnitt **Kompatibilitätsrisikofaktoren** werden die Details für diese Bewertungen angezeigt.

> [!TIP]
> Wenn im App-Detailbereich die Kompatibilitätsbewertung nicht angezeigt wird, liegt dies möglicherweise daran, dass die Einstellung **Details zu App-Versionen** deaktiviert ist. Diese Einstellung ist standardmäßig deaktiviert und fasst alle Versionen von Apps mit dem gleichen Namen und Herausgeber zusammen. Der Dienst führt weiterhin Kompatibilitätsrisikobewertungen für jede Version durch. Aktivieren Sie **Details zu App-Versionen**, um die Kompatibilitätsrisikobewertung für eine bestimmte App-Version anzuzeigen. Weitere Informationen finden Sie unter [Planobjekte](about-deployment-plans.md#plan-assets).

## <a name="microsoft-known-issues"></a>MS bekannte Probleme

Desktop Analytics durchsucht die Microsoft-Datenbank zur App-Kompatibilität nach bekannten Problemen. Anhand dieser Datenbank werden etwaige vorhandene Kompatibilitätsblöcke für allgemein erhältliche Anwendungen von Microsoft oder anderen Herausgebern bestimmt. Diese Prüfung bezieht sich nur auf das Zielbetriebssystem für den ausgewählten Bereitstellungsplan.

Die folgenden Probleme werden im App-Eigenschaftenbereich als **MS bekannte Probleme** angezeigt:

### <a name="asset-is-removed-during-upgrade"></a>Das Objekt wird während des Upgrades entfernt.

Windows hat Kompatibilitätsprobleme mit einer Anwendung oder einem Treiber festgestellt. Das Objekt wird nicht zur neuen Betriebssystemversion migriert. Es ist keine Aktion erforderlich, damit das Upgrade fortgesetzt werden kann. Installieren Sie eine kompatible Version der Anwendung oder des Treibers unter der neuen Betriebssystemversion.

<!-- 3594545 -->
Windows kann die folgenden Objekte teilweise oder vollständig entfernen:

- Vollständiges Entfernen: Die App bzw. der Treiber wird vom Windows Setup beim Upgrade vollständig vom Gerät entfernt.
- Teilweises Entfernen: Die App bzw. der Treiber wird vom Windows Setup teilweise vom Gerät entfernt. Sie müssen die App bzw. den Treiber nach dem Upgrade von Windows manuell deinstallieren.

In beiden Fällen kann der Benutzer nach dem Windows-Upgrade die App oder die zum Treiber gehörende Hardware nicht verwenden.

So zeigen Sie diese Empfehlung im Desktop Analytics-Portal an:

1. Wählen Sie in einem Bereitstellungsplan **Piloten vorbereiten** aus.
1. Klicken Sie auf die Registerkarte **Apps**.
1. Wählen Sie eine App aus, und rufen Sie die Kompatibilitätsrisikofaktoren sowie die Empfehlungen im Seitenbereich auf.

[![Screenshot der Objektempfehlung im Desktop Analytics-Portal](media/3594545-app-removed.png)](media/3594545-app-removed.png#lightbox)

### <a name="blocking-upgrade"></a>Blockiert Upgrade

Windows hat Blockierungsprobleme erkannt, und die Anwendung kann während des Upgrades nicht entfernt werden. Sie funktioniert möglicherweise nicht in der neuen Betriebssystemversion. Entfernen Sie die Anwendung vor dem Upgrade. Installieren Sie sie unter der neuen Betriebssystemversion, und testen Sie sie.

### <a name="blocking-upgrade-but-can-be-reinstalled-after-upgrading"></a>Blockiert Upgrade, kann aber nach dem Upgrade neu installiert werden

Die Anwendung ist mit der neuen Version des Betriebssystems kompatibel, sie wird jedoch nicht migriert. Entfernen Sie die Anwendung vor dem Windows-Upgrade. Installieren Sie sie unter der neuen Betriebssystemversion neu.

### <a name="blocking-upgrade-update-application-to-newest-version"></a>Blockiert Upgrade. Aktualisieren Sie die Anwendung auf die neueste Version

Die vorhandene Version der Anwendung ist nicht mit der neuen Betriebssystemversion kompatibel, und sie wird nicht migriert. Es ist eine kompatible Version der Anwendung verfügbar. Aktualisieren Sie die Anwendung vor dem Upgrade.

### <a name="disk-encryption-blocking-upgrade"></a>Datenträgerverschlüsselung blockiert das Upgrade

Die Verschlüsselungsfunktionen der Anwendung blockieren das Upgrade. Deaktivieren Sie die Verschlüsselungsfunktion vor dem Windows-Upgrade, und aktivieren Sie sie nach dem Upgrade.

### <a name="does-not-work-with-new-os-but-wont-block-upgrade"></a>Funktioniert nicht mit neuem BS, wird das Upgrade aber nicht blockieren

Die Anwendung ist mit der neuen Version des Betriebssystems nicht kompatibel, sie blockiert jedoch nicht das Upgrade. Es ist keine Aktion erforderlich, damit das Upgrade fortgesetzt werden kann. Installieren Sie eine kompatible Version der Anwendung unter der neuen Betriebssystemversion.

### <a name="does-not-work-with-new-os-and-will-block-upgrade"></a>Funktioniert nicht mit neuem BS und wird das Upgrade blockieren

Die Anwendung ist mit der neuen Version des Betriebssystems nicht kompatibel, und sie blockiert das Upgrade. Entfernen Sie die Anwendung vor dem Upgrade. Eine kompatible Version der Anwendung ist möglicherweise verfügbar.

### <a name="evaluate-application-on-new-os"></a>Anwendung unter neuem BS evaluieren

Die Anwendung wird von Windows migriert, es wurden jedoch Probleme erkannt, welche die Leistung der App unter der neuen Betriebssystemversion beeinträchtigen können. Es ist keine Aktion erforderlich, damit das Upgrade fortgesetzt werden kann. Testen Sie die Anwendung unter der neuen Betriebssystemversion.

### <a name="may-block-upgrade-test-application"></a>Könnte Upgrade blockieren. Anwendung testen

Windows hat Probleme festgestellt, die das Upgrade möglicherweise beeinträchtigen, weitere Untersuchungen sind jedoch erforderlich. Testen Sie das Verhalten der Anwendung während des Upgrades. Sollte sie das Upgrade blockieren, entfernen Sie sie vor dem Upgrade. Installieren Sie sie unter der neuen Betriebssystemversion neu, und testen Sie sie.

### <a name="multiple"></a>Mehrere

Mehrere Probleme wirken sich auf die Anwendung aus. Wählen Sie **Abfrage** aus, um Details zu den von Windows festgestellten Problemen anzuzeigen.

### <a name="reinstall-application-after-upgrading"></a>Anwendung nach dem Upgrade neu installieren

Die Anwendung ist mit der neuen Betriebssystemversion kompatibel, Sie müssen sie jedoch nach dem Windows-Upgrade neu installieren. Die Anwendung wird durch den Upgradeprozess entfernt. Es ist keine Aktion erforderlich, damit das Upgrade fortgesetzt werden kann. Installieren Sie die Anwendung unter der neuen Betriebssystemversion neu.

### <a name="safeguards"></a>Safeguard-Tags

<!-- 5746559 -->

In den Windows-Kompatibilitätsdaten sind einige Apps und Treiber mit *Safeguard*-Tags klassifiziert, aufgrund derer beim Update auf Windows 10 möglicherweise ein Fehler auftritt oder ein Rollback durchgeführt wird. Es ist auch möglich, dass das Windows-Update durchgeführt, die App oder der Treiber jedoch entfernt wird. In Desktop Analytics können diese Tags jetzt vorab ermittelt werden, damit Sie ein Objekt entsprechend korrigieren können, bevor Sie das Update bereitstellen.

1. Wählen Sie im Desktop Analytics-Portal einen Bereitstellungsplan aus.

1. Wählen Sie im Menü die Option **Planobjekte** aus, und wechseln Sie zur Registerkarte **Apps**.

1. Filtern Sie die Namensspalte, um Elemente mit Werten anzuzeigen, die den Begriff `Safeguard` enthalten. Wählen Sie das Ergebnis aus, um weitere Informationen anzuzeigen.

    > [!NOTE]
    > Dieser Eintrag ist keine echte App, die auf Ihren Geräten installiert ist. Es handelt sich um einen Platzhalter, mit dem Sie Apps oder Treiber in Ihrer Umgebung ermitteln können, die mit einem Safeguard-Tag aufgrund von Kompatibilitätsproblemen gekennzeichnet sind.

1. Wählen Sie im Abschnitt mit den Empfehlungen den Link *Weitere Informationen* aus. Mit diesem Link wird die Windows-Website mit der aktuellen Liste der Apps oder Treiber geöffnet, die mit Safeguard-Tags gekennzeichnet sind.

1. Vergleichen Sie die aktuelle veröffentlichte Liste mit der Liste der Objekte in Ihrer Umgebung. Behandeln Sie alle potenziell problematischen Apps oder Treiber, indem Sie ein Update auf eine kompatible Version durchführen.

[![Screenshot der Safeguard-App in Desktop Analytics](media/5746559-safeguards.png)](media/5746559-safeguards.png#lightbox)

## <a name="ready-for-windows"></a>Ready for Windows

Der Einführungsstatus basiert auf Informationen von kommerziellen Geräten, die Daten an Microsoft weitergeben. Der Status ist in Supporthinweise von Softwareanbietern integriert.

Desktop Analytics gibt den Einführungsstatus für jede Version eines Objekts an, das auf kommerziellen Geräten gefunden wurde. Dieser Status enthält keine Daten von Endanwendergeräten oder Geräten, die keine Daten übermitteln. Der Status ist möglicherweise nicht repräsentativ für die Einführungsrate auf allen Windows 10-Geräten.

Mögliche Kategorien:

- **Umfassend eingeführt**: Diese App wurde auf mindestens 100.000 kommerziellen Windows 10-Geräten installiert.

- **Eingeführt**: Diese App wurde auf mindestens 10.000 kommerziellen Windows 10-Geräten installiert.

- **Unzureichende Daten**: Zu wenige kommerzielle Windows 10-Geräte teilen Informationen zu dieser App mit Microsoft, sodass die Einführung nicht kategorisiert werden kann.

- **Entwickler kontaktieren**: Möglicherweise treten Kompatibilitätsprobleme mit dieser Version der App auf. Microsoft empfiehlt, den Softwareanbieter zu kontaktieren, um weitere Informationen einzuholen.

- **Unbekannt**: Für diese Version der Anwendung sind keine Informationen verfügbar. Eventuell sind Informationen zu anderen Versionen der Anwendung vorhanden.

### <a name="support-statement"></a>Supporthinweis

Wenn der Softwareanbieter eine oder mehrere Versionen dieser Anwendung unter Windows 10 unterstützt, wird diese Bestimmung im App-Eigenschaftenbereich angezeigt. Sehen Sie im Abschnitt „Kompatibilitätsrisikofaktoren“ den **Supporthinweis** ein.

## <a name="advanced-insights"></a>Umfassendere Erkenntnisse

Desktop Analytics kann Probleme auch anhand der folgenden umfassenderen Erkenntnisse erkennen:

### <a name="adopted-version-available"></a>Verbreitete Version verfügbar

Es gibt eine andere Version dieser App, die starke Akzeptanz unter anderen Kunden hat. Dieses Signal verwendet Übernahmedaten aus dem Windows-Ökosystem. Sollten andere das Update blockierende Faktoren in der aktuellen Version vorhanden sein, erwägen Sie, stattdessen die alternative Version bereitzustellen. Wie Sie weitere von der Anwendung übernommene Versionen finden, erfahren Sie unter „Vorbereiten der Produktion“ in den Informationen zur Anwendungsintegrität.

### <a name="driver-dependency"></a>Driver dependency (Treiberabhängigkeit)

Die App ist von einem Treiber abhängig. Desktop Analytics empfiehlt, die App Pilotversuchen zu unterziehen, um mögliche Regressionen zu erkennen. Wenn Probleme auftreten, fordern Sie beim Herausgeber eine Version an, die mit Windows 10 kompatibel ist.

### <a name="additional-insights"></a>Zusätzliche Erkenntnisse

<!-- 4021225 -->
Wenn Sie den Configuration Manager-Standort und die Clients auf Version 1906 aktualisieren, melden Clients außerdem diese zusätzlichen Erkenntnisse, wenn die Diagnosedatenebene auf „Erweitert (begrenzt)“ festgelegt ist:

> [!Important]  
> Wenn Sie die neuen Configuration Manager-Features nach der Aktualisierung des Standorts vollständig nutzen möchten, müssen Sie auch Clients auf die neueste Version aktualisieren. Dieses Szenario funktioniert erst, wenn auch die Clientversion aktuell ist.

#### <a name="16-bit-apps"></a>16-Bit-Apps

Entfernen Sie alle 16-Bit-Komponenten aus Anwendungen, und ersetzen Sie Sie durch entsprechende 32-Bit-oder 64-Bit-Komponenten. Weitere Informationen finden Sie unter [The Windows Vista and Windows Server 2008 Developer Story: Application Compatibility Cookbook](https://docs.microsoft.com/previous-versions/aa480152\(v=msdn.10\)) (Die Windows Vista- und Windows Server 2008-Entwicklerstory: Cookbook zur Anwendungskompatibilität).

Die andere Möglichkeit besteht darin, NT Virtual DOS Machine (NTVDM) für die Unterstützung unter Windows 10 zu aktivieren.

#### <a name="requires-admin-privileges"></a>Erfordert Administratorberechtigungen

Die App erfordert, dass der Benutzer mit Administratorberechtigungen auf das Gerät zugreift. Verwenden Sie ein App-Manifest für diese Apps, die Administratorberechtigungen erfordern. Weitere Informationen finden Sie unter [Create and embed an application manifest](https://docs.microsoft.com/previous-versions/bb756929\(v=msdn.10\)) (Erstellen und Einbetten eines Anwendungsmanifests).

Desktop Analytics empfiehlt, die App Pilotversuchen zu unterziehen, um mögliche Regressionen zu erkennen.

#### <a name="java-dependency"></a>Java-Abhängigkeit

Viele Java-Anwendungen hängen von einer separat installierten JRE (Java Runtime Environment) ab. Ältere JRE-Versionen funktionieren möglicherweise weiterhin unter Windows 10, Oracle hingegen unterstützt ausschließlich die neuesten JRE-Versionen. Die Verwendung einer älteren, nicht unterstützten JRE kann Sicherheitslücken bewirken. Überprüfen Sie, ob Ihre Anwendung mit den neuesten JRE-Versionen ausgeführt wird.

#### <a name="not-dpi-aware"></a>Nicht mit DPI-Werten kompatibel

In der App treten möglicherweise Anzeigeprobleme mit höheren Bildschirmauflösungen unter Windows 10 auf. Verwenden Sie ein App-Manifest, um Probleme mit hoher DPI-Auflösung zu vermeiden. Weitere Informationen finden Sie unter [Anwendungsmanifeste](https://docs.microsoft.com/windows/desktop/SbsCs/application-manifests).

Desktop Analytics empfiehlt, die App Pilotversuchen zu unterziehen, um mögliche Regressionen zu erkennen.

#### <a name="silverlight-framework"></a>Silverlight-Framework

Microsoft empfiehlt, Silverlight nicht mit nicht-browserbasierten Apps zu verwenden. Das Supportenddatum für Silverlight 5 ist der Oktober 2021.

Silverlight wird von den meisten aktuellen Webbrowsern nicht unterstützt.

| Browser | Unterstützung |
|---------|---------|
| Google Chrome | Ende der Unterstützung: September 2015 |
| Firefox | Ende der Unterstützung: März 2017 |
| Microsoft Edge | Kein Plug-in verfügbar |

Desktop Analytics empfiehlt, die App Pilotversuchen zu unterziehen, um mögliche Regressionen zu erkennen.

#### <a name="net-framework-1011"></a>.NET Framework 1.0/1.1

Die .NET Framework-Version 1.0 wird von Windows 10 nicht unterstützt. Version 1.1 ist nicht kompatibel mit Windows 10. Wenn die App von einem Drittherausgeber stammt, wenden Sie sich an den Anbieter, um eine Version anzufordern, die mit Windows 10 kompatibel ist. Andernfalls müssen Sie die Anwendung so neu entwickeln, sodass eine unterstützte Version von .NET verwendet wird.

#### <a name="net-framework-2030"></a>.NET Framework 2.0/3.0

.NET Framework 2.0 und .NET Framework 3.5 werden unter Windows 10 unterstützt. Möglicherweise müssen Sie das Windows-Feature aktivieren. Weitere Informationen finden Sie unter [Installieren von .NET Framework 3.5 unter Windows 10](https://docs.microsoft.com/dotnet/framework/install/dotnet-35-windows-10).

#### <a name="ui-access"></a>UI-Zugriff

Anwendungen mit UI-Zugriff können die UI-Steuerelementebenen umgehen, um Eingaben in Fenstern mit höheren Berechtigungen auf dem Desktop vorzunehmen. Verwenden Sie diese Einstellung nur für Anwendungen mit Benutzeroberflächen-Hilfstechnologien.

Wenn Sie keine Barrierefreiheitsfunktionen in Ihrer App verwenden, legen Sie das Flag für den UI-Zugriff im App-Manifest auf „false“ fest. Weitere Informationen finden Sie unter [Create and embed an application manifest](https://docs.microsoft.com/previous-versions/bb756929\(v=msdn.10\)) (Erstellen und Einbetten eines Anwendungsmanifests).

Desktop Analytics empfiehlt, die App Pilotversuchen zu unterziehen, um mögliche Regressionen zu erkennen.

## <a name="driver-risk-assessment"></a>Risikobewertung für Treiber

Von Desktop Analytics werden auch alle Treiber nach Verfügbarkeit aufgelistet und gruppiert, die nicht zur Betriebssystemversion migriert werden.

Die Bewertung für den Treiber wird in Desktop Analytics angegeben. Wählen Sie in der Liste der Treiberobjekte in einem Bereitstellungsplan einen einzelnen Treiber aus, um seinen Flyout-Eigenschaftenbereich zu öffnen. Eine Gesamtempfehlungs- und Bewertungsebene wird angezeigt. Im Abschnitt **Kompatibilitätsrisikofaktoren** werden die Details für diese Bewertungen angezeigt.

| Treiberverfügbarkeit | Aktion erforderlich? | Bedeutung | Empfehlung |
|---------------------|------------------|---------------|----------|
| Über den Handel verfügbar | Nein, nur zur Information | Die derzeit installierte Version einer Anwendung oder eines Treibers wird nicht zur neuen Betriebssystemversion migriert. Eine kompatible Version wird mit der neuen Version des Betriebssystems installiert. | Es ist keine Aktion erforderlich, damit das Upgrade fortgesetzt werden kann. |
| Von Windows Update importieren | Ja | Die derzeit installierte Version eines Treibers wird nicht zur neuen Betriebssystemversion migriert. Eine kompatible Version ist über Windows Update verfügbar. | Wenn der Computer automatisch Updates von Windows Update empfängt, ist keine Aktion erforderlich. Importieren Sie andernfalls nach dem Windows-Upgrade einen neuen Treiber aus Windows Update. |
| Über den Handel und über Windows Update verfügbar | Ja | Die derzeit installierte Version eines Treibers wird nicht zur neuen Betriebssystemversion migriert. Während des Upgrades wird zwar ein neuer Treiber installiert, es ist jedoch eine neuere Version von Windows Update verfügbar. | Wenn der Computer automatisch Updates von Windows Update empfängt, ist keine Aktion erforderlich. Importieren Sie andernfalls nach dem Windows-Upgrade einen neuen Treiber aus Windows Update. |
| Beim Hersteller nachfragen | Ja | Der Treiber wird nicht zur neuen Betriebssystemversion migriert, und Desktop Analytics kann keine kompatible Version finden. | Wenden Sie sich wegen einer Lösung an den unabhängigen Hardwarehersteller (IHV), der den Treiber herstellt, oder an den Originalgerätehersteller (OEM), der das Gerät bereitgestellt hat. |

## <a name="see-also"></a>Weitere Informationen:

Der FastTrack Center-Vorteil für Windows 10 bietet Zugriff auf **Desktop App Assure**. Dieser Vorteil ist ein neuer Dienst zum Beheben von Kompatibilitätsproblemen mit Windows 10- und Microsoft 365 Apps for Enterprise. Weitere Informationen finden Sie unter [Desktop App Assure](https://docs.microsoft.com/fasttrack/win-10-desktop-app-assure).
