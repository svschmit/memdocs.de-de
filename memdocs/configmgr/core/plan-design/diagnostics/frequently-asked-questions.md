---
title: Häufig gestellte Fragen zu Diagnose- und Nutzungsdaten
titleSuffix: Configuration Manager
description: Häufig gestellte Fragen zu Diagnose- und Nutzungsdaten für Configuration Manager
ms.date: 01/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 3fe32aa2-d594-4ad0-a291-b8f5395ac50b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.collection: M365-identity-device-management
ms.openlocfilehash: 60634ed8e275ff8496a08969054aa912a81b9d07
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81688478"
---
# <a name="frequently-asked-questions-about-diagnostics-and-usage-data"></a>Häufig gestellte Fragen zu Diagnose- und Verwendungsdaten

*Gilt für: Configuration Manager (Current Branch)*

In diesem Artikel erhalten Sie Antworten zu häufig gestellten Fragen zu Diagnose- und Nutzungsdaten in Configuration Manager.

## <a name="can-i-turn-off-diagnostic-and-usage-data"></a><a name="bkmk_off"></a> Kann ich Diagnose- und Nutzungsdaten deaktivieren?

Verwenden Sie den Dienstverbindungspunkt im Offlinemodus, um zu verwalten, wann der Standort Daten sendet. Verwenden Sie dann das Dienstverbindungstool, um Daten manuell zu senden. Weitere Informationen finden Sie in den folgenden Artikeln:

- [Informationen zum Dienstverbindungspunkt](../../servers/deploy/configure/about-the-service-connection-point.md)
- [Verwenden des Dienstverbindungstools](../../servers/manage/use-the-service-connection-tool.md)

Der aktuelle Branch von Configuration Manager muss in regelmäßigen Abständen aktualisiert werden, um neue Versionen von Windows 10 und Clouddiensten wie Microsoft Intune zu unterstützen. Für Microsoft ist zumindest ein grundlegendes Verständnis von Diagnose- und Nutzungsdaten erforderlich. Diese Daten werden verwendet, um das Produkt auf dem neuesten Stand zu halten, den Updateprozess zu optimieren und die Qualität und Sicherheit des Produkts zu verbessern.

Wenn sich der Dienstverbindungspunkt im Offlinemodus befindet, werden keine Daten an den Dienst gesendet. Wenn Sie in den Onlinemodus wechseln oder das Dienstverbindungstool verwenden, werden Daten an den Dienst gesendet, um nach Updates zu suchen.

Sie können auch die Ebene der von Configuration Manager gesammelten Daten einstellen. Weitere Informationen finden Sie unter [Ebenen von Nutzungsdaten zu Diagnosezwecken](levels-overview.md).

## <a name="what-is-the-data-retention-period"></a><a name="bkmk_retention"></a> Wie lange ist der Datenaufbewahrungszeitraum?

Microsoft speichert Diagnose- und Nutzungsdaten in Bezug auf Configuration Manager für ein Jahr.

## <a name="is-diagnostics-and-usage-data-sent-when-setup-runs"></a><a name="bkmk_update"></a> Werden beim Setup Diagnose- und Nutzungsdaten gesendet?

Nein. Diagnose- und Verwendungsdaten erst nur gesendet, sobald der Standort installiert wurde und betriebsbereit ist.

## <a name="how-frequently-is-the-data-sent"></a><a name="bkmk_frequency"></a> Wie oft werden die Daten gesendet?

Die gespeicherten SQL-Prozeduren werden alle sieben Tage (ab dem Datum der Installation des Standorts) ausgeführt.

- Im Onlinemodus lädt der Dienstverbindungspunkt die Daten nach dem Ausführen der Abfragen hoch.

- Im Offlinemodus werden die Daten mit dem Dienstverbindungstool hochgeladen. (Die Daten sind erst sieben Tage nach der Installation des Standorts für die Offlineverwendung verfügbar.)  

## <a name="can-the-data-be-used-to-form-a-network-map"></a><a name="bkmk_network"></a> Können die Daten zum Erstellen einer Netzwerkübersicht verwendet werden?

Nein. In diesen Daten sind keine Netzwerkdetails wie IP-Adressen oder detaillierte geografische Informationen enthalten. Weitere Informationen hierzu für die von Ihnen verwendete Version finden Sie unter [Ebenen von Nutzungsdaten zu Diagnosezwecken](levels-overview.md#bkmk_versions).

Die Daten enthalten allerdings Informationen zur Zeitzone des jeweiligen Standorts. So erhalten Sie Einblicke in die allgemeine geografische und globale Verteilung von Standorten in einer Hierarchie.

## <a name="can-you-see-data-in-custom-sql-tables"></a><a name="bkmk_tables"></a> Kann Microsoft Daten in benutzerdefinierten SQL-Tabellen sehen?

Nein. Configuration Manager erfasst Diagnose- und Nutzungsdaten über in SQL gespeicherte Prozeduren. Diese gespeicherten Prozeduren werden für die Standardprodukttabellen in der Datenbank ausgeführt. Diese gesamten SQL-Tabellen werden mit dem Präfix **TEL_** versehen. Als Teil der SQL-Abfrage zur Erkennung des Schemas werden alle Tabellennamen für den Vergleich mit bekannten Standardwerten hashcodiert. Durch dieses Verhalten wird festgelegt, dass benutzerdefinierte Tabellen in der Datenbank vorhanden sind. Wenn benutzerdefinierte Tabellen vorhanden sind, wird Microsoft darüber informiert, dass das Datenbankschema abweichend vom Standard erweitert wurde. Es enthält keine Daten, die in diesen Tabellen gespeichert sind.

## <a name="can-you-see-other-databases"></a><a name="bkmk_databases"></a> Kann Microsoft andere Datenbanken sehen?

Nein. Die gespeicherten Prozeduren zum Sammeln von Daten sind auf die Configuration Manager-Standortdatenbank beschränkt. Microsoft kann weder die Namen anderer Datenbanken noch Daten in diesen Datenbanken sehen.

## <a name="is-any-data-sent-to-other-integrated-cloud-services"></a><a name="bkmk_cloud"></a> Werden Daten an andere integrierte Clouddienste gesendet?

Ja, wenn Sie diese Dienste mit Configuration Manager integrieren. Im Rahmen der Interaktion mit Clouddiensten sendet Configuration Manager Daten an diese Dienste. Diese Daten sind spezifisch für den jeweiligen Clouddienst und getrennt von Diagnose- und Nutzungsdaten in Bezug auf Configuration Manager. Weitere Informationen zu den spezifischen Daten, die bei der Interaktion mit anderen Clouddiensten verwendet werden, finden Sie in der Dokumentation für den jeweiligen Dienst.

Die folgenden Clouddienste sind beispielsweise Teil von Microsoft Endpoint Manager:

- [Desktop Analytics – Datenschutz](../../../desktop-analytics/privacy.md)
- [Datenschutz und personenbezogene Daten in Intune](https://docs.microsoft.com/intune/protect/privacy-personal-data)
- [Anforderungen für Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot-requirements)

## <a name="does-configuration-manager-collect-any-personal-data"></a><a name="bkmk_personal"></a> Sammelt Configuration Manager personenbezogene Daten?

Nein. Personenbezogene Daten und Kundendaten werden von Configuration Manager weder gesammelt noch übertragen. Es handelt sich um ein lokales Produkt, das direkt von Ihnen bereitgestellt, verwaltet und ausgeführt wird. Die Diagnose- und Nutzungsdaten, die von Microsoft gesammelt werden, verbessern die Anwendungsinstallation, Qualität sowie die Sicherheit zukünftiger Releases.

Weitere Informationen zu Configuration Manager-Daten finden Sie unter [Ebenen von Nutzungsdaten zu Diagnosezwecken](levels-overview.md).
