---
title: Anzeigen von BitLocker-Berichten
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über die BitLocker-Verwaltungsberichte in Configuration Manager
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: reference
ms.assetid: 0bae9477-0500-41cf-8aa3-5e6efadd0554
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7c44ec9a9ed91d8543fedbdd5fba191b3989da19
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88129210"
---
# <a name="view-bitlocker-reports"></a>Anzeigen von BitLocker-Berichten

*Gilt für: Configuration Manager (Current Branch)*

<!--3601034-->

Nachdem Sie [die Berichte](setup-websites.md) auf dem Reporting Services-Punkt installiert haben, können Sie die Berichte anzeigen. In den Berichten wird die BitLocker-Richtlinienkonformität des Unternehmens sowie für einzelne Geräte gezeigt. Sie enthalten Tabellen und Diagramme und verfügen über Filter, um Daten aus verschiedenen Perspektiven anzuzeigen.

Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Überwachung** den Knoten **Berichterstellung**, und wählen Sie den Knoten **Berichte** aus. Die folgenden Berichte gehören zur Kategorie **BitLocker-Verwaltung**:

- [BitLocker-Computerkonformität](#bkmk-compliancereport)

- [Dashboard zur BitLocker-Unternehmenskonformität](#bkmk-dashboard)

- [Details zur BitLocker-Unternehmenskonformität](#bkmk-compliancedetails)

- [Zusammenfassung der BitLocker-Unternehmenskonformität](#bkmk-compliancesummary)

- [Bericht zur Wiederherstellungsüberwachung](#bkmk-audit)

Sie können auf all diese Berichte direkt von der Website des Reporting Services-Punkts aus zugreifen.

> [!NOTE]
> Damit diese Berichte vollständige Daten anzeigen:
>
> - Erstellen und Bereitstellen einer BitLocker-Verwaltungsrichtlinie für eine Gerätesammlung
> - Clients in der Zielsammlung müssen Hardwareinventar senden

## <a name="bitlocker-computer-compliance"></a><a name="bkmk-compliancereport"></a> BitLocker-Computerkonformität

Mit diesem Bericht können Sie computerspezifische Informationen sammeln. Er liefert detaillierte Verschlüsselungsinformationen zum Betriebssystemlaufwerk und zu allen Festplattenlaufwerken. Erweitern Sie den Eintrag „Computername“, um die ausführlichen Informationen zu den einzelnen Laufwerken anzuzeigen. Darüber hinaus werden die jeweils geltenden Richtlinien für alle Laufwerke eines Computers angegeben.

:::image type="content" source="media/bitlocker-computer-compliance.png" alt-text="Screenshot des BitLocker-Computer Konformitäts Berichts Beispiel" lightbox="media/bitlocker-computer-compliance.png":::

Sie können diesen Bericht auch verwenden, um den letzten bekannten BitLocker-Verschlüsselungsstatus von verlorenen oder gestohlenen Computern zu ermitteln. Configuration Manager bestimmt die Konformität des Geräts basierend auf den BitLocker-Richtlinien, die Sie bereitstellen. Bevor Sie versuchen, den BitLocker-Verschlüsselungsstatus eines Geräts zu ermitteln, überprüfen Sie die Richtlinien, die Sie für das Gerät bereitgestellt haben.

> [!NOTE]
> Dieser Bericht zeigt nicht den Verschlüsselungsstatus des Wechseldatenträgers an.

### <a name="computer-details"></a>Computerdetails

|Spaltenname&nbsp;|Beschreibung|
|----------------|----|
|Computername|Der vom Benutzer angegebene DNS-Computername.|
|Domänenname|Vollständig qualifizierter Domänennamen des Computers|
|Computertyp|Der Computertyp, gültige Typen sind **Nicht tragbar** und **Tragbar**.|
|Betriebssystem|Betriebssystemtyp des Computers|
|Gesamtkonformität|Der BitLocker-Konformitätsgesamtstatus des Computers. Die gültigen Statuswerte sind: **Richtlinienkonform** und **Nicht richtlinienkonform**. Der [Konformitätsstatus pro Laufwerk](#bkmk_volume) kann verschiedene Konformitätszustände anzeigen. In diesem Feld wird jedoch der Konformitätsstatus gemäß der angegebenen Richtlinie angezeigt.|
|Konformität des Betriebssystems|Der Konformitätsstatus des Betriebssystems auf dem Computer. Die gültigen Statuswerte sind: **Richtlinienkonform** und **Nicht richtlinienkonform**.|
|Konformität des Festplattenlaufwerks|Konformitätsstatus eines Festplattenlaufwerks auf dem Computer. Die gültigen Statuswerte sind: **Richtlinienkonform** und **Nicht richtlinienkonform**.|
|Datum der letzten Aktualisierung|Dieses Feld enthält das Datum und die Uhrzeit der letzten Verbindung, die vom Computer mit dem Server hergestellt wurde, um den Konformitätsstatus zu melden.|
|Ausnahme|Gibt an, ob für den Benutzer eine Ausnahme von der BitLocker-Richtlinie gilt|
|Ausgenommener Benutzer|Der Benutzer, für die eine Ausnahme von der BitLocker-Richtlinie gilt|
|Datum der Ausnahme|Das Datum, an dem die Ausnahme gewährt wurde|
|Details zum Konformitätsstatus|Fehler- und Statusmeldungen zum Status der Computerkonformität entsprechend der angegebenen Richtlinie|
|Richtlinie: Verschlüsselungsstärke|Die Verschlüsselungsstärke, die Sie in der BitLocker-Verwaltungsrichtlinie ausgewählt haben.|
|Richtlinie: Betriebssystemlaufwerk|Gibt an, ob für das Betriebssystem eine Verschlüsselung erforderlich ist, und ggf. wird der geeignete Schutzvorrichtungstyp angezeigt|
|Richtlinie: Festplattenlaufwerk|Gibt an, ob für das Festplattenlaufwerk eine Verschlüsselung erforderlich ist|
|Hersteller|Der Name des Computerherstellers, der im BIOS des Computers angezeigt wird|
|Modell|Der Modellname des Computers, der im BIOS des Computers angezeigt wird|
|Gerätebenutzer|Bekannte Benutzer auf dem Computer.|

### <a name="computer-volume"></a><a name="bkmk_volume"></a> Computervolume

|Spaltenname&nbsp;|Beschreibung|
|----------------|----|
|Laufwerkbuchstabe|Der Laufwerksbuchstabe auf dem Computer.|
|Laufwerkstyp|Typ des Laufwerks Die gültigen Werte sind **Betriebssystemlaufwerk** und **Festplattenlaufwerk**. Bei diesen Einträgen handelt es sich um physische Laufwerke und nicht um logische Volumes.|
|Verschlüsselungsstärke|Die Verschlüsselungsstärke, die Sie in der BitLocker-Verwaltungsrichtlinie ausgewählt haben.|
|Schutzvorrichtungstyp|Der Schutzvorrichtungstyp, den Sie in der Richtlinie zum Verschlüsseln des Laufwerks ausgewählt haben. Die gültigen Schutzvorrichtungstypen für ein Betriebssystemlaufwerk sind: **TPM** oder **TPM+PIN**. Der einzige gültige Schutzvorrichtungstyp für ein Festplattenlaufwerk ist **Kennwort**.|
|Schutzvorrichtungsstatus|In diesem Feld wird angezeigt, ob auf dem Computer der Schutzvorrichtungstyp aktiviert ist, der in der Richtlinie angegeben ist. Die gültigen Statuswerte sind **Aktiviert** oder **Deaktiviert**.|
|Verschlüsselungsstatus|Der Verschlüsselungsstatus des Laufwerks Die gültigen Statuswerte sind **Verschlüsselt**, **Nicht verschlüsselt** oder **Wird verschlüsselt**.|

## <a name="bitlocker-enterprise-compliance-dashboard"></a><a name="bkmk-dashboard"></a> Dashboard zur BitLocker-Unternehmenskonformität

Dieser Bericht enthält die folgenden Diagramme, die den BitLocker-Konformitätsstatus in Ihrer Organisation veranschaulichen:

- Verteilung des Konformitätsstatus

- Verteilung der Konformitätsfehler

- Verteilung des Konformitätsstatus nach Laufwerkstyp

:::image type="content" source="media/bitlocker-enterprise-compliance-dashboard.png" alt-text="Beispielscreenshot des Dashboards für die BitLocker-Unternehmenskonformität" lightbox="media/bitlocker-enterprise-compliance-dashboard.png":::

### <a name="compliance-status-distribution"></a>Verteilung des Konformitätsstatus

In diesem Tortendiagramm wird der Konformitätsstatus für Computer im Unternehmen angezeigt. Außerdem wird die prozentuale Anzahl der Computer, die über den Konformitätsstatus verfügt, im Vergleich zur Gesamtzahl der Computer in der Auswahl angezeigt. Die tatsächliche Anzahl von Computern mit den jeweiligen Konformitätsstatus wird ebenfalls angezeigt.

Im Tortendiagramm werden die folgenden Konformitätsstatus angezeigt:

- Kompatibel

- Nicht kompatibel

- Benutzerausnahme

- Temporäre Benutzerausnahme

- Richtlinie nicht erzwungen

- Unbekannt Diese Computer haben einen Statusfehler gemeldet, oder sie gehören zur Auswahl, aber ihr Konformitätsstatus wurde noch nie gemeldet. Ein fehlender Konformitätsstatus ist möglicherweise darauf zurückzuführen, dass der Computer nicht mit der Organisation verbunden ist.

### <a name="non-compliant---errors-distribution"></a>Verteilung der Konformitätsfehler

Dieses Kreisdiagramm zeigt die Kategorien von Computern in Ihrer Organisation, die nicht mit der BitLocker-Laufwerkverschlüsselungsrichtlinie konform sind. Es zeigt auch die Anzahl der Computer in den einzelnen Kategorien. Der Bericht berechnet jeden Prozentsatz aus der Gesamtzahl der nicht konformen Computer in der Sammlung.

- Verschlüsselung durch Benutzer zurückgestellt

- Kein kompatibles TPM gefunden

- Systempartition nicht verfügbar oder nicht groß genug

- TPM sichtbar, aber nicht initialisiert

- Richtlinienkonflikt

- Warten auf automatische TPM-Bereitstellung

- Unbekannter Fehler

- Keine Informationen Auf diesen Computern ist der BitLocker-Verwaltungs-Agent nicht installiert, oder er ist installiert, aber nicht aktiviert. Der Dienst funktioniert z. B. nicht.

### <a name="compliance-status-distribution-by-drive-type"></a>Verteilung des Konformitätsstatus nach Laufwerkstyp

In diesem Balkendiagramm wird der aktuelle BitLocker-Konformitätsstatus nach Laufwerkstyp dargestellt. Die Status sind **Richtlinienkonform** und **Nicht richtlinienkonform**. Für Festplattenlaufwerke und Betriebssystemlaufwerke werden Balken angezeigt. Der Bericht umfasst Computer ohne Festplattenlaufwerk und zeigt nur einen Wert in der Leiste **Betriebssystemlaufwerk** an. Im Diagramm werden keine Benutzer dargestellt, für die bei der Richtlinie zur BitLocker-Laufwerkverschlüsselung eine Ausnahme bzw. die Kategorie „Keine Richtlinie“ gilt.

## <a name="bitlocker-enterprise-compliance-details"></a><a name="bkmk-compliancedetails"></a> Details zur BitLocker-Unternehmenskonformität

Dieser Bericht zeigt Informationen zur allgemeinen BitLocker-Konformität in Ihrer Organisation für die Sammlung von Computern an, auf denen Sie die BitLocker-Verwaltungsrichtlinie bereitgestellt haben.

:::image type="content" source="media/bitlocker-enterprise-compliance-details.png" alt-text="Screenshot der Details zu BitLocker Enterprise Compliance Beispiel" lightbox="media/bitlocker-enterprise-compliance-details.png":::

|Spaltenname|Beschreibung|
|--- |--- |
|Verwaltete Computer|Anzahl der Computer, auf denen Sie eine BitLocker-Verwaltungsrichtlinie bereitgestellt haben.|
|% Konform|Prozentsatz der richtlinienkonformen Computer in der Organisation|
|% Nicht konform|Prozentsatz der nicht richtlinienkonformen Computer in der Organisation|
|% Konformität unbekannt|Prozentsatz der Computer mit einem unbekannten Konformitätsstatus|
|Ausnahme (%)|Prozentsatz der Computer, für die eine Ausnahme von der BitLocker-Verschlüsselungsanforderung gilt|
|Ohne Ausnahme (%)|Prozentsatz der Computer, für die keine Ausnahme von der BitLocker-Verschlüsselungsanforderung gilt|
|Kompatibel|Anzahl der konformen Computer in der Organisation.|
|Nicht konform|Anzahl der nicht konformen Computer in der Organisation.|
|Konformität unbekannt|Anzahl der Computer mit einem unbekannten Konformitätsstatus.|
|Ausnahme|Anzahl der Computer, für die eine Ausnahme von der BitLocker-Verschlüsselungsanforderung gilt|
|Ohne Ausnahme|Anzahl der Computer, für die keine Ausnahme von der BitLocker-Verschlüsselungsanforderung gilt|

### <a name="computer-details"></a>Computerdetails

|Spaltenname|Beschreibung|
|--- |--- |
|Computername|Der DNS-Computername des verwalteten Geräts.|
|Domänenname|Vollständig qualifizierter Domänennamen des Computers|
|Konformitätsstatus|Der Konformitätsgesamtstatus des Computers Die gültigen Statuswerte sind: **Richtlinienkonform** und **Nicht richtlinienkonform**.|
|Ausnahme|Gibt an, ob für den Benutzer eine Ausnahme von der BitLocker-Richtlinie gilt|
|Gerätebenutzer|Benutzer des Geräts.|
|Details zum Konformitätsstatus|Fehler- und Statusmeldungen zum Status der Computerkonformität entsprechend der angegebenen Richtlinie|
|Letzter Kontakt|Dieses Feld enthält das Datum und die Uhrzeit der letzten Verbindung, die vom Computer mit dem Server hergestellt wurde, um den Konformitätsstatus zu melden.|

## <a name="bitlocker-enterprise-compliance-summary"></a><a name="bkmk-compliancesummary"></a> Zusammenfassung der BitLocker-Unternehmenskonformität

Verwenden Sie diesen Bericht, um die allgemeine BitLocker-Konformität in Ihrer Organisation aufzuzeigen. Er zeigt auch die Konformität für einzelne Computer an, auf denen Sie die BitLocker-Verwaltungsrichtlinie bereitgestellt haben.

:::image type="content" source="media/bitlocker-enterprise-compliance-summary.png" alt-text="Screenshot der BitLocker-Übersicht über die unternehmensweite Konformität Beispiel" lightbox="media/bitlocker-enterprise-compliance-summary.png":::

|Spaltenname|Beschreibung|
|--- |--- |
|Verwaltete Computer|Anzahl der Computer, die Sie mit der BitLocker-Richtlinie verwalten.|
|% Konform|Prozentsatz der konformen Computer in Ihrer Organisation.|
|% Nicht konform|Prozentsatz der nicht konformen Computer in Ihrer Organisation.|
|% Konformität unbekannt|Prozentsatz der Computer mit einem unbekannten Konformitätsstatus|
|Ausnahme (%)|Prozentsatz der Computer, für die eine Ausnahme von der BitLocker-Verschlüsselungsanforderung gilt|
|Ohne Ausnahme (%)|Prozentsatz der Computer, für die keine Ausnahme von der BitLocker-Verschlüsselungsanforderung gilt|
|Kompatibel|Anzahl der konformen Computer in Ihrer Organisation.|
|Nicht kompatibel|Anzahl der nicht konformen Computer in Ihrer Organisation.|
|Konformität unbekannt|Anzahl der Computer mit einem unbekannten Konformitätsstatus.|
|Ausnahme|Anzahl der Computer, für die eine Ausnahme von der BitLocker-Verschlüsselungsanforderung gilt|
|Ohne Ausnahme|Anzahl der Computer, für die keine Ausnahme von der BitLocker-Verschlüsselungsanforderung gilt|

## <a name="recovery-audit-report"></a><a name="bkmk-audit"></a> Bericht zur Wiederherstellungsüberwachung

> [!NOTE]
> Ab Version 2002 ist dieser Bericht nur auf der [Website für die Verwaltung und Überwachung von BitLocker](helpdesk-portal.md#reports) verfügbar.<!-- 7629549 -->

Verwenden Sie diesen Bericht, um Benutzer zu überwachen, die Zugriff auf BitLocker-Wiederherstellungsschlüssel angefordert haben. Sie können nach den folgenden Kriterien filtern:

- Ein bestimmter Typ von Benutzer, z. B. ein Helpdeskbenutzer oder ein Endbenutzer
- Ob die Anforderung erfolglos oder erfolgreich war
- Der bestimmte angeforderte Schlüsseltyp: „Kennwort für den Wiederherstellungsschlüssel“, „Wiederherstellungsschlüssel-ID“ oder „TPM-Kennworthashwert“
- Ein Datumsbereich, in dem der Abruf erfolgt ist

:::image type="content" source="media/bitlocker-recovery-audit-report.png" alt-text="Screenshot der BitLocker-Wiederherstellungs Überwachung Beispiel" lightbox="media/bitlocker-recovery-audit-report.png":::

|Spaltenname&nbsp;|BESCHREIBUNG|
|----------------|----|
|Datum und Uhrzeit der Anforderung|Datum und Uhrzeit, zu der ein Endbenutzer oder Helpdeskbenutzer einen Schlüssel angefordert hat.|
|Quelle der Überwachungsanforderung|Der Standort, von dem die Anforderung stammt. Gültige Werte sind **Self-Service-Portal** oder **Helpdesk**.|
|Ergebnis der Anforderung|Status der Anforderung. Gültige Werte sind **Erfolgreich** oder **Fehler**.|
|Helpdeskbenutzer|Der Administrator, der den Schlüssel angefordert hat. Wenn ein Helpdeskadministrator den Schlüssel ohne Angabe des Benutzernamens wiederherstellt, ist das Feld **Endbenutzer** leer. Ein Standardhelpdeskbenutzer muss den Benutzernamen angeben, der in diesem Feld angezeigt wird. Bei der Wiederherstellung über das Self-Service-Portal wird in diesem Feld und im Feld **Endbenutzer** der Name des Benutzers angezeigt, der die Anforderung gestellt hat.|
|Endbenutzer|Der Name des Benutzers, der den Schlüsselabruf angefordert hat.|
|Computer|Der Name des wiederhergestellten Computers|
|Schlüsseltyp|Der vom Benutzer angeforderte Schlüsseltyp. Die drei Schlüsseltypen lauten wie folgt:<br/><br/>- **Kennwort für den Wiederherstellungsschlüssel**: wird zum Wiederherstellen eines Computers im Wiederherstellungsmodus verwendet<br/>- **Wiederherstellungsschlüssel-ID**: wird zum Wiederherstellen eines Computers im Wiederherstellungsmodus für einen anderen Benutzer verwendet<br/>- **TPM-Kennworthashwert** : wird zum Wiederherstellen eines Computers mit gesperrtem Trusted Platform Module verwendet|
|Beschreibung der Ursache|Gibt an, warum der Benutzer den angegebenen Schlüsseltyp angefordert hat, basierend auf der im Formular ausgewählten Option.|
