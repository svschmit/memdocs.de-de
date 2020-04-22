---
title: Häufig gestellte Fragen zu Größe und Leistung von Standorten
titleSuffix: Configuration Manager
description: Antworten auf häufig gestellte Fragen zu Configuration Manager im Zusammenhang mit der Größe und Leistung von Standorten.
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: conceptual
ms.date: 04/19/2019
ms.openlocfilehash: 5cd23667eadc7e1caae90a135bc96be89563f883
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706798"
---
# <a name="configuration-manager-site-sizing-and-performance-faq"></a>Configuration Manager: häufig gestellte Fragen zu Größe und Leistung von Standorten

*Gilt für: Configuration Manager (Current Branch)*

In diesem Dokument werden häufig gestellte Fragen zu Configuration Manager in Bezug auf die Größe von Standorten und allgemeine Leistungsprobleme angesprochen.

## <a name="machine-and-disk-configuration-faqs-and-examples"></a>Häufig gestellte Fragen und Beispiele für die Konfiguration von Computern und Datenträgern

### <a name="how-should-i-format-the-disks-on-my-site-server-and-sql-server"></a>Wie soll ich die Datenträger auf meiner Standortserver- und SQL Server-Instanz formatieren?

Verteilen Sie die Eingangsboxen von Configuration Manager und die SQL Server-Dateien auf mindestens zwei getrennte Volumes. Diese Trennung ermöglicht Ihnen, die Clusterzuteilungsgrößen für die verschiedenen Arten von E/A zu optimieren. 

Verwenden Sie für das Volume, das die Eingangsboxen Ihrer Standortserver hostet, NTFS mit Zuteilungseinheiten von 4 KB oder 8 KB. ReFS schreibt 64 KB selbst für kleine Dateien. Configuration Manager weist viele kleine Dateien auf, sodass ReFS unnötigen Speicherbedarf auf den Datenträgern verursachen kann.

Verwenden Sie für Datenträger, die SQL Server-Datenbankdateien enthalten, entweder die NTFS- oder die ReFS-Formatierung mit Zuteilungseinheiten von 64 KB.

### <a name="how-and-where-should-i-lay-out-my-sql-database-files"></a>Wie und wo sollte ich meine SQL Server-Datenbankdateien ablegen?

Moderne Arrays aus SSD-Laufwerken (Solid-State Drives) und Azure Storage Premium können für ein einzelnes Volume mit einige wenigen Datenträgern hohe IOPS-Werte erreichen. In der Regel fügen Sie einem Array weitere Laufwerke für zusätzlichen Speicher, nicht für zusätzlichen Durchsatz hinzu. Wenn Sie physische spindelbasierte Datenträger verwenden, benötigen Sie möglicherweise mehr IOPS, als Sie auf einem einzelnen Volume generieren können. Sie sollten 60 % der insgesamt empfohlenen IOPS und des Speicherplatzes für die *MDF*-Datei, 20 % für die *LDF*-Datei und 20 % für die Protokoll- und temporären Datendateien zuteilen. Die *LDF*- und temporären Dateien können sich alle auf einem einzigen Volume mit 40 % (20 % + 20 %) Ihrer zugeteilten IOPS befinden.

SQL Server-Instanzen vor SQL Server 2016 erstellten standardmäßig nur eine temporäre Datendatei. Sie sollten weitere erstellen, um SQL Server-Sperren und das Warten auf den Zugriff auf eine einzelne Datei zu vermeiden. Die Meinungen in der Community gehen auseinander, was die beste Anzahl der zu erstellenden temporären Datendateien betrifft, von vier bis acht. Bei Tests zeigt sich ein geringer Unterschied zwischen vier und acht, sodass Sie vier *gleich große* temporäre Datendateien erstellen können. Ihre tempdb-Datendateien sollten bis zu 20-25 % der Größe der gesamten Datenbank erreichen.

### <a name="are-there-any-other-recommendations-for-disk-setup"></a>Gibt es Empfehlungen zur Datenträgereinrichtung?

Sofern konfigurierbar, legen Sie den RAID-Controllerspeicher auf 70 % Zuteilung für Schreibvorgänge und 30 % für Lesevorgänge fest. Verwenden Sie im Allgemeinen für die Standortdatenbank eine RAID-10-Arraykonfiguration. RAID 1 ist bei kleinen Standorten mit geringen E/A-Anforderungen oder bei Verwendung schneller SSD-Laufwerke ebenfalls akzeptabel. Konfigurieren Sie bei größeren Datenträgerarrays Ersatzdatenträger, um ausgefallene Datenträger automatisch zu ersetzen.

**Beispiel: Physischer Computer mit physischen Datenträgern** 

[Leitlinien für die Größe](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines), wenn Standortserver- und SQL Server-Instanz zusammengestellt sind, mit **100.000** Clients sehen 1.200 IOPS für die Eingangsboxen des Standortservers und 5.000 IOPS für SQL Server-Dateien vor.

Die resultierende Datenträgerkonfiguration könnte so aussehen:

| Laufwerke<sup>1</sup> | RAID | Format | Volume-Inhalt | Mindestens benötigte IOPS| Ca. bereitgestellte IOPS<sup>2</sup>  |
|----------------|-----------|-------------|----------------------|---------------------|------------------|
| 2 x 10.000          | 1         | -           | Windows              |                     | -                |
| 6 x 15.000          | 10        | NTFS 8 KB     | ConfigMgr-Eingangsboxen    |     1\.700            | 1\.751             |
| 12 x 15.000         | 10        | ReFS 64 KB    | SQL, MDF-Datei             | 60 % x 5.000 = 3.000     | 3\.476             |
| 8 x 15.000          | 10        | ReFS 64 KB    | SQL, LDF- und temporäre Dateien | 40 % x 5.000 = 2.000     | 2\.322             |

1. Empfohlene Ersatzdatenträger nicht inbegriffen. 
2. Dieser Wert stammt aus [Beispielhafte Datenträgerkonfigurationen](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). 

### <a name="i-use-hyper-v-on-windows-server-how-should-i-configure-the-disks-for-my-configuration-manager-vms-for-best-performance"></a>Ich nutze Hyper-V unter Windows Server. Wie sollte ich für optimale Leistung die Datenträger meiner Configuration Manager-VMs konfigurieren?

Hyper-V bietet eine ähnliche Leistung wie ein physischer Server, wenn die Hardwareressourcen (CPU-Kerne und Pass-Through-Speicher) zu 100 % dem virtuellen Computer (VM) zugeteilt sind. Die Verwendung von Datenträgerdateien des Typs *.vhd* oder *.vhdx* mit fester Größe hat eine minimale Auswirkung von 1-5 % auf die E/A-Leistung. Die Verwendung dynamisch erweiterbarer Datenträgerdateien des Typs *.vhd* oder *.vhdx* verursacht für die Configuration Manager-Workload E/A-Leistungseinbußen von bis zu 25 %. Wenn Sie dynamisch erweiterbare Datenträger benötigen, können Sie dies durch Hinzufügen einer zusätzlichen IOPS-Leistung von 25 % zum Array ausgleichen.

Wenn Sie Ihren Configuration Manager-Standortserver oder SQL Server in einer VM ausführen, isolieren Sie die Betriebssystemlaufwerke des Hyper-V-Hosts vom Betriebssystem- und den Datenlaufwerken der VM.

Weitere Informationen zum Optimieren von VMs finden Sie unter [Optimieren der Leistung von Hyper-V-Servern](/windows-server/administration/performance-tuning/role/hyper-v-server/).

**Beispiel: Hyper-V-VM-basierter Standortserver** 

[Leitlinien für die Größe](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines), wenn Standortserver- und SQL Server-Instanz zusammengestellt sind, mit **150.000** Clients sehen 1.800 IOPS für die Eingangsboxen des Standortservers und 7.400 IOPS für SQL Server-Dateien vor.

Die resultierende Datenträgerkonfiguration könnte so aussehen:

| Laufwerke<sup>1</sup> | RAID | Format<sup>2</sup> | Volume-Inhalt | Mindestens benötigte IOPS| Ca. bereitgestellte IOPS<sup>3</sup>  |
|----------------|-----------|----------------|---------------------------|----------------------|------------------|
| 2 x 10.000          | 1         | -              | Betriebssystem des Hyper-V-Hosts           | -                    | -                |
| 2 x 10.000          | 1         | -              | (VM) Betriebssystem des Standortservers       | -                    | -                |
| 2 x SSD SAS      | 1         | NTFS 8 KB        | (VM) ConfigMgr-Eingangsboxen    | 1\.800                 | 7\.539             |
| 4 x SSD SAS      | 10        | ReFS 64 KB       | (VM) SQL Server auf Host (alle Dateien) | 7\.400                 | 14346            |

1. Empfohlene Ersatzdatenträger nicht inbegriffen. 
2. Pass-Through-fähige *VHDX*-Datei fester Größe für das VM-Laufwerk, das dem zugrunde liegenden Volume zugeordnet ist. 
3. Dieser Wert stammt aus [Beispielhafte Datenträgerkonfigurationen](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). 

### <a name="are-there-any-suggestions-for-configuration-manager-environments-in-microsoft-azure"></a>Gibt es Vorschläge für Configuration Manager-Umgebungen in Microsoft Azure?

Beginnen Sie mit der Lektüre von [Configuration Manager in Azure – Häufig gestellte Fragen](configuration-manager-on-azure.md).

IaaS-VMs (Infrastructure-as-a-Service) mit Nutzung von Azure Storage Premium-Datenträgern können hohe IOPS bieten. Konfigurieren Sie auf diesen VMs zusätzliche Datenträger für den erwarteten Speicherplatzbedarf und nicht für zusätzliche IOPS.

Speicher in Azure ist grundsätzlich überreichlich und erfordert keine zusätzlichen Datenträger, um verfügbar zu sein. In der Datenträgerverwaltung oder im Feature „Speicherplätze“ können Sie Datenträger in Stripesets anordnen, um mehr Speicherplatz und Leistung bereitzustellen.

Weitere Informationen und Empfehlungen zur Maximierung der Storage Premium-Leistung und zum Ausführen von SQL Server-Instanzen in Azure IaaS-VMs finden Sie unter:

- [Optimieren der Anwendungsleistung](/azure/storage/storage-premium-storage-performance#optimize-application-performance)
 
- [Leitfaden für Datenträger](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance)

**Beispiel: Azure-basierte Standortserver** 

[Leitlinien für die Größe](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines), wenn Standortserver- und SQL Server-Instanz zusammengestellt sind, mit **50.000** Clients sehen acht Kerne, 32 GB und 1.200 IOPS für die Eingangsboxen des Standortservers und 2.800 IOPS für SQL Server-Dateien vor.

Ihre resultierende Azure-VM könnte den Typ DS13v2 (acht Kerne, 56 GB) mit der folgenden Datenträgerkonfiguration aufweisen:

| Laufwerke | Format | Enthält | Mindestens benötigte IOPS| Ca. bereitgestellte IOPS<sup>1</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;Standard&gt; | -             | Betriebssystem des Standortservers     | -                    | -                |
| 1 x P20 (512 GB)    | NTFS 8 KB       | ConfigMgr-Eingangsboxen  | 1\.200                 | 2\.334             |
| 1 x P30 (1.024 GB)   | ReFS 64 KB      | SQL Server (alle Dateien<sup>2</sup>) | 2\.800                 | 3\.112             |

1. Dieser Wert stammt aus [Beispielhafte Datenträgerkonfigurationen](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations).
2. Die [Leitlinien für Azure](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) gestatten es, die TempDB auf dem lokalen, SSD-basierten Laufwerk *D:* abzulegen, da sie den verfügbaren Speicherplatz nicht überschreitet und eine zusätzliche Verteilung von Datenträger-E/A ermöglicht.

**Beispiel: Azure-basierter Standortserver (für sofortige Leistungssteigerung)** 

Der Durchsatz von Azure-Datenträgern wird durch die Größe der VM beschränkt. Die Konfiguration im vorherigen Azure-Beispiel kann künftige Erweiterungen oder Leistungssteigerungen einschränken. Wenn Sie bei der Erstbereitstellung Ihrer Azure-VM zusätzliche Datenträger hinzufügen, können Sie Ihre Azure-VM bei minimalen Vorabinvestitionen für eine höhere Rechenleistung in der Zukunft rüsten. Es ist wesentlich einfacher, im Voraus zu planen, um die Leistung des Standortservers bei sich ändernden Anforderungen zu steigern, als später eine kompliziertere Migration durchführen zu müssen.

Ändern Sie die Datenträger im vorherigen Azure-Beispiel, um zu prüfen, wie sich die IOPS ändern.

**DS13v2** 

| Laufwerke<sup>1</sup> | Format | Enthält | Mindestens benötigte IOPS| Ca. bereitgestellte IOPS<sup>2</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;Standard&gt; | -             | Betriebssystem des Standortservers     | -                    | -                |
| 2 x P20 (1.024 GB)   | NTFS 8 KB       | ConfigMgr-Eingangsboxen  | 1\.200                 | 3\.984             |
| 2 x P30 (2.048 GB)   | ReFS 64 KB      | SQL Server (alle Dateien<sup>3</sup>) | 2\.800                 | 3\.984             |

1. Datenträger werden mithilfe des Features „Speicherplätze“ in Stripesets angeordnet.
2. Dieser Wert stammt aus [Beispielhafte Datenträgerkonfigurationen](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). Die VM-Größe begrenzt die Leistung.
3. Die [Leitlinien für Azure](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) gestatten es, die TempDB auf dem lokalen, SSD-basierten Laufwerk *D:* abzulegen, da sie den verfügbaren Speicherplatz nicht überschreitet und eine zusätzliche Verteilung von Datenträger-E/A ermöglicht.

Wenn Sie in Zukunft mehr Leistung benötigen, können Sie Ihre VM auf den Typ DS14v2 hochstufen, wodurch sich CPU und Arbeitsspeicher verdoppeln. Die zusätzliche Datenträger-Bandbreite, die durch diese VM-Größe ermöglicht wird, erhöht auch sofort die verfügbaren Datenträger-IOPS auf Ihren bereits konfigurierten Datenträgern.

**DS14v2**

| Laufwerke<sup>1</sup> | RAID | Format | Enthält | Mindestens benötigte IOPS| Ca. bereitgestellte IOPS<sup>2</sup>  |
|------------------|---------------|--------------------|----------------------|------------------|
| &lt;Standard&gt; | -             | Betriebssystem des Standortservers     | -                    | -                |
| 2 x P20 (1.024 GB)   | NTFS 8 KB       | ConfigMgr-Eingangsboxen  | 1\.200                 | 4\.639             |
| 2 x P30 (2.048 GB)   | ReFS 64 KB      | SQL Server (alle Dateien<sup>3</sup>) | 2\.800                 | 6\.182             |

1. Datenträger werden mithilfe des Features „Speicherplätze“ in Stripesets angeordnet.
2. Dieser Wert stammt aus [Beispielhafte Datenträgerkonfigurationen](../plan-design/configs/site-size-performance-guidelines.md#example-disk-configurations). Die VM-Größe begrenzt die Leistung.
3. Die [Leitlinien für Azure](/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance#disks-guidance) gestatten es, die TempDB auf dem lokalen, SSD-basierten Laufwerk *D:* abzulegen, da sie den verfügbaren Speicherplatz nicht überschreitet und eine zusätzliche Verteilung von Datenträger-E/A ermöglicht.

## <a name="other-common-sql-server-related-performance-questions"></a>Andere allgemeine auf die Leistung von SQL Server bezogene Fragen 

### <a name="is-it-better-to-run-with-sql-colocated-with-the-site-server-or-run-it-on-a-remote-server"></a>Ist die Ausführung von SQL Server zusammengestellt mit dem Standortserver oder auf einem Remoteserver besser?

Beide Varianten können eine angemessene Leistung bieten, vorausgesetzt, der einzelne Server ist entsprechend dimensioniert, oder die Netzwerkverbindung zwischen den beiden Servern ist angemessen.

SQL Server auf einem Remoteserver verursacht die Vorab- und Betriebskosten eines zusätzlichen Servers, ist aber typisch für die Mehrheit der Großunternehmen. Diese Konfiguration bietet folgende Vorteile:

- Optionen für höhere Verfügbarkeit am Standort, z.B. SQL Server Always On
- Möglichkeit der Erstellung umfangreicher Berichte mit weniger Verarbeitungsaufwand am Standort
- Einfachere Notfallwiederherstellung in bestimmten Situationen
- Einfachere Sicherheitsverwaltung
- Trennung der Aufgaben bei der SQL Server-Verwaltung, z.B. in einem separaten DBA-Team

SQL Server und Standortserver zusammengestellt auf einem einzelnen Servercomputer ist für kleinere Unternehmen typisch. Diese Konfiguration bietet folgende Vorteile:

- Geringere Kosten für Computer, Lizenzen und Wartung
- Weniger Fehlerquellen am Standort
- Bessere Steuerung der Planung von Downtime

### <a name="how-much-ram-should-i-allocate-for-sql"></a>Wie viel RAM sollte ich SQL Server zuteilen?

Standardmäßig nutzt SQL Server den gesamten verfügbaren Arbeitsspeicher Ihres Servers, worunter Betriebssystem und andere Prozesse auf dem Computer möglicherweise leiden. Um mögliche Leistungsprobleme zu vermeiden, ist es wichtig, SQL Server Arbeitsspeicher explizit zuzuteilen. Wenn Standortserver- und SQL Server-Instanz zusammengestellt sind, muss das Betriebssystem ausreichend RAM für das Zwischenspeichern von Dateien und andere Vorgänge haben. Stellen Sie sicher, dass ausreichend Arbeitsspeicher für SMSExec- und andere Configuration Manager-Prozessen verbleibt. Wenn Sie SQL Server auf einem Remoteserver ausführen, können Sie SQL Server den *Großteil* des Arbeitsspeichers, nicht aber den gesamten zuweisen. Die [Leitlinien für die Größe](../plan-design/configs/site-size-performance-guidelines.md#general-sizing-guidelines) bieten eine erste Orientierung. 

Die Arbeitsspeicherzuteilung für SQL Server muss auf ganze GB gerundet werden. Wenn der Arbeitsspeicher auf große Mengen ansteigt, können Sie SQL Server einen höheren Prozentsatz zuteilen. Wenn beispielsweise 256 GB oder mehr RAM verfügbar ist, können Sie SQL Server bis zu 95 % zuteilen, da dadurch immer noch viel Arbeitsspeicher für das Betriebssystem erhalten bleibt. Das Überwachen der Auslagerungsdatei ist eine gute Möglichkeit, sicherzustellen, dass genügend Arbeitsspeicher für das Betriebssystem und jegliche Configuration Manager-Prozesse vorhanden ist.

### <a name="cores-are-cheap-these-days-should-i-just-add-a-bunch-of-them-to-my-sql-server"></a>Kerne sind mittlerweile kostengünstig. Sollte ich meiner SQL Server-Instanz einfache weitere Kerne hinzufügen?

Es kann zu Arbeitsspeicherkonflikten kommen, wenn in Ihrer SQL Server-Instanz mehr als 16 physische Kerne bei zu wenig RAM vorhanden sind. Die Configuration Manager-Workload zeigt eine bessere Leistung, wenn für SQL Server mindestens 3-4 GB RAM pro Kern zur Verfügung stehen. Wenn Sie Ihren SQL Server-Instanzen Kerne hinzufügen, stellen Sie sicher, dass Sie den Arbeitsspeicher im richtigen Verhältnis vergrößern.

### <a name="will-sql-always-on-impact-my-performance"></a>Wirkt sich SQL Server Always On auf die Leistung aus?

Im Allgemeinen hat SQL Server Always On einen vernachlässigbaren Einfluss auf die Leistung des Systems, wenn die Netzwerkverbindung zwischen den Replikatservern für SQL Server gewährleistet ist. In einer aktiven SQL Server Always On-Umgebung kann die Größe der Datenbank-Protokolldatei ( *.ldf*) schnell zunehmen. Nach erfolgter Datenbanksicherung wird der Speicherplatz der Protokolldatei jedoch automatisch freigegeben. Fügen Sie der Configuration Manager-Datenbank einen SQL Server-Auftrag zur Ausführung einer Sicherung, z.B. alle 24 Stunden, und einer Sicherung der *.ldf*-Datei alle sechs Stunden hinzu. Weitere Informationen zu SQL Server Always On und Configuration Manager, z.B. zu SQL Server-Sicherungsstrategien, finden Sie unter [SQL Server Always On für eine hochverfügbare Standortdatenbank](../servers/deploy/configure/sql-server-alwayson-for-a-highly-available-site-database.md).

### <a name="should-i-enable-sql-compression-on-my-database"></a>Soll ich für meine Datenbank die SQL Server-Komprimierung aktivieren?

Die SQL Server-Komprimierung wird für die Configuration Manager-Datenbank nicht empfohlen. Zwar gibt es keine Funktionsbeeinträchtigungen bei Aktivierung der Komprimierung für eine Configuration Manager-Datenbank, aber die Testergebnisse zeigen keine nennenswerten Größeneinsparungen im Vergleich zu den möglichen erheblichen Auswirkungen auf die Leistung des Systems.

### <a name="should-i-enable-sql-encryption-on-my-database"></a>Soll ich für meine Datenbank die SQL Server-Verschlüsselung aktivieren?

Alle Geheimnisse in der Configuration Manager-Datenbank werden bereits sicher gespeichert, aber das Hinzufügen der SQL Server-Verschlüsselung kann zu noch mehr Sicherheit führen. Zwar gibt es keine Funktionsbeeinträchtigungen bei der Aktivierung der Verschlüsselung für Ihre Datenbank, aber es kann zu einem Leistungsabfall von bis zu 25 % kommen. Dies hängt von den Tabellen, die Sie verschlüsseln möchten, und der verwendeten Version von SQL Server ab. Setzen Sie daher die Verschlüsselung mit Bedacht ein, insbesondere in großen Umgebungen. Denken Sie auch daran, Ihre Sicherungs- und Wiederherstellungspläne zu aktualisieren, um sicherzustellen, dass Sie die verschlüsselten Daten erfolgreich wiederherstellen können.

### <a name="what-version-of-sql-should-i-run"></a>Welche Version von SQL Server sollte ich ausführen?

Unterstützte Versionen von SQL Server finden Sie unter [Unterstützung für SQL Server-Versionen](../plan-design/configs/support-for-sql-server-versions.md). Aus Leistungssicht erfüllen alle unterstützten Versionen von SQL Server die geforderten Leistungskriterien. SQL Server 2012 und SQL Server 2016 oder höher bieten jedoch bei einigen Aspekten der Configuration Manager-Workload eine bessere Leistung als SQL Server 2014. Außerdem verbessert die Ausführung von SQL Server 2014 mit dem Kompatibilitätsgrad SQL Server 2012 (110) die Leistung generell. Bei der Installation werden Configuration Manager-Datenbanken, die in SQL Server 2012 und SQL Server 2014 ausgeführt werden, auf Kompatibilitätsgrad 110 festgelegt. SQL Server 2016 oder höher ist auf den Standardkompatibilitätsgrad der jeweiligen SQL Server-Version festgelegt, z.B. 130 für SQL Server 2016. Bei einem direkten Upgrade von SQL Server werden die Kompatibilitätsgrade erst dann aktualisiert, nachdem Sie die nächste Hauptversion von Configuration Manager (Current Branch) installiert haben. 

Wenn Sie bei bestimmten SQL-Abfragen in SQL Server 2016 oder höher ungewöhnliche Timeouts oder Verzögerungen feststellen, z.B. bei der Verwendung der rollenbasierten Zugriffssteuerung (RBAC) in der Verwaltungskonsole, ändern Sie den SQL Server-Kompatibilitätsgrad für die Configuration Manager-Datenbank auf 110. Die Ausführung mit SQL Server-Kompatibilitätsgrad 110 für SQL Server 2014 und höhere Versionen wird vollständig unterstützt. Weitere Informationen finden Sie im Supportartikel zum Thema [SQL-Abfrage wird abgebrochen oder die Konsole verlangsamt bei bestimmten Configuration Manager-Datenbankabfragen](https://support.microsoft.com/help/3196320/sql-query-times-out-or-console-slow-on-certain-configuration-manager-d).

Ab Januar 2018 sollten Sie die folgenden SQL Server-Versionen *vermeiden*, da verschiedene bekannte leistungsbezogene oder andere potenzielle Probleme vorliegen:

- SQL 2012 SP3 CU1 bis CU5
- SQL 2014 SP1 CU6 bis SP2 CU2
- SQL 2016 RTM bis CU3, SP1 CU3 bis CU5

### <a name="should-i-implement-any-additional-sql-indexing-tasks"></a>Sollte ich zusätzliche SQL Server-Indizierungsaufgaben implementieren?

Ja, aktualisieren Sie Indizes mindestens einmal pro Woche und Statistiken mindestens einmal pro Tag, um die SQL Server-Leistung zu verbessern. Mithilfe von Skripts von Drittanbietern und ergänzenden Informationen aus der Configuration Manager- und SQL Server-Community können diese Aufgaben optimiert werden.

An großen Standorten können einige SQL Server-Tabellen, z.B. CI\_CurrentComplianceStatusDetails und HinvChangeLog, je nach Nutzungsverhalten groß sein. Möglicherweise müssen Sie Ihren Wartungsansatz dafür Schritt für Schritt reduzieren oder ändern.

### <a name="when-should-i-use-full-sql-server-instead-of-sql-express-on-my-secondary-sites"></a>Wann sollte ich an meinen sekundären Standorten die Vollversion SQL Server anstelle von SQL Server Express verwenden?

SQL Server Express hat keine signifikanten Auswirkungen auf die Leistung sekundärer Standorte und ist für die meisten Kunden ausreichend. SQL Server Express ist außerdem einfach zu implementieren und zu verwalten und wird für fast alle Kunden jeder Größe empfohlen.

Es gibt jedoch eine Situation, in der eine Installation der Vollversion von SQL Server erforderlich sein kann. Wenn Sie eine große Anzahl von Verteilungspunkten und Paketen oder Quellen in Ihrer Umgebung haben, kann die Größenbeschränkung von SQL Server Express von 10 GB überschritten werden. Wenn die Anzahl der Pakete multipliziert mit der Anzahl der Verteilungspunkte mehr als 4.000.000 beträgt, z.B. 2.000 Verteilungspunkte mit 2.000 Inhaltselementen, sollten Sie den Einsatz der Vollversion von SQL Server an Ihren sekundären Standorten in Betracht ziehen. 

### <a name="should-i-change-maxdop-settings-on-my-database"></a>Sollte ich die MaxDOP-Einstellungen für meine Datenbank ändern?

Wenn Sie Ihre Einstellung auf 0 belassen (alle verfügbaren Prozessoren verwenden), ist dies in den meisten Fällen für die gesamte Verarbeitungsleistung optimal.

Viele Configuration Manager-Administratoren befolgen die Leitlinien unter [Empfehlungen und Richtlinien für die Konfigurationsoption „Maximaler Grad an Parallelität“ in SQL Server](https://support.microsoft.com/help/2806535/recommendations-and-guidelines-for-the-max-degree-of-parallelism-confi). Auf modernster großer Hardware führt diese Empfehlung zu acht als vorgeschlagene maximale Einstellung. Wenn Sie jedoch viele kleinere Abfragen im Vergleich zur Anzahl Ihrer Prozessoren ausführen, kann es hilfreich sein, einen höheren Wert zu wählen. Die Beschränkung auf acht ist nicht unbedingt die beste Einstellung für größere Standorte, an denen mehr Kerne zur Verfügung stehen. 

Beginnen Sie bei SQL Server-Instanzen mit mehr als acht Kernen mit der Einstellung 0, und nehmen Sie Änderungen nur dann vor, wenn Sie Leistungsprobleme oder übermäßige Sperren feststellen. Wenn Sie MaxDOP ändern müssen, weil bei 0 Leistungsprobleme auftreten, beginnen Sie mit einem neuen Wert, der mindestens größer oder gleich der empfohlenen Mindestanzahl von Kernen für die SQL Server-Größe dieses Standorts ist. Ein Unterschreiten dieses Werts hat nahezu immer negative Auswirkungen auf die Leistung. Eine Remoteserver mit SQL Server für einen Standort mit 100.000 Clients benötigt beispielsweise mindestens 12 Kerne. Wenn Ihre SQL Server-Instanz 16 Kerne hat, starten Sie den Test Ihrer MaxDOP-Einstellung mit dem Wert 12.

## <a name="other-common-performance-related-questions"></a>Andere übliche Fragen zur Leistung

### <a name="which-folders-on-the-site-server-or-other-roles-should-i-exclude-for-antivirus-software"></a>Welche Ordner auf dem Standortserver (oder anderer Rollen) sollte ich von Antivirensoftware ausschließen?

Gehen Sie mit Bedacht vor, wenn Sie den Antivirenschutz auf einem beliebigen System deaktivieren. In sehr umfangreichen und sicheren Umgebungen empfehlen wir, für eine optimale Leistung die *aktive Überwachung* zu deaktivieren.

Weitere Informationen zu empfohlenen Ausnahmen beim Antivirenschutz finden Sie im Artikel zum Thema [Empfohlene Ausnahmen für Antivirenschutz für Configuration Manager 2012 und Current Branch-Standortserver, Standortsysteme und Clients](https://support.microsoft.com/help/327453/recommended-antivirus-exclusions-for-configuration-manager-2012-and-cu).

### <a name="what-can-i-do-to-make-wsus-perform-better-when-its-used-with-configuration-manager"></a>Was kann ich tun, um die Leistung von WSUS bei Verwendung mit Configuration Manager zu verbessern?

Das Ändern einiger wichtiger IIS-Einstellungen, wie z.B. „WsusPool Queue Length“ und „WsusPool Private Memory Limit“, kann die WSUS-Leistung auch bei kleineren Installationen verbessern. Weitere Informationen finden Sie unter [Empfohlene Hardware](../plan-design/configs/recommended-hardware.md).

Vergewissern Sie sich außerdem, dass die neuesten Updates für das Betriebssystem mit WSUS installiert sind:

- Windows Server 2012: Alle nicht rein sicherheitsbezogenen kumulativen Updates, die seit Oktober 2017 veröffentlicht wurden. ([KB4041690](https://support.microsoft.com/help/4041690/windows-server-2012-update-kb4041690))
- Windows Server 2012 R2: Alle nicht rein sicherheitsbezogenen kumulativen Updates, die seit August 2017 veröffentlicht wurden. ([KB4039871](https://support.microsoft.com/help/4039871/windows-8-1-windows-server-2012-r2-update-kb4039871))
- Windows Server 2016: Alle nicht rein sicherheitsbezogenen kumulativen Updates, die seit August 2017 veröffentlicht wurden. ([KB4039396](https://support.microsoft.com/help/4039396/windows-10-update-kb4039396))

### <a name="what-type-of-maintenance-should-i-run-on-my-wsus-servers"></a>Welche Art von Wartung sollte auf meinem Servern mit WSUS ausgeführt werden?

Siehe den Artikel zum Thema [Vollständige Anleitung für die Wartung von WSUS und Configuration Manager-SUP](https://support.microsoft.com/help/4490644/complete-guide-to-microsoft-wsus-and-configuration-manager-sup-maint).

### <a name="i-want-to-set-up-basic-performance-monitoring-for-my-site-what-should-i-watch"></a>Ich möchte für meinen Standort eine grundlegende Leistungsüberwachung einrichten. Was sollte ich überwachen?

Die herkömmliche Überwachung der Serverleistung funktioniert für Configuration Manager im Allgemeinen effektiv. Sie können auch die verschiedenen Management Packs für System Center Operations Manager für Configuration Manager, SQL Server und Windows Server zur Überwachung der grundlegenden Integrität Ihrer Server nutzen. Darüber hinaus können Sie die von Configuration Manager bereitgestellten Zähler des Windows-Systemmonitors (PerfMon) direkt überwachen. Überwachen Sie die Backlogs in den verschiedenen Eingangsboxen auf frühzeitige Warnzeichen für mögliche Probleme mit der Standortleistung oder Backlogs.

## <a name="see-also"></a>Weitere Informationen:

- [Richtlinien zu Größe und Leistung von Standorten](../plan-design/configs/site-size-performance-guidelines.md)
- [Configuration Manager in Azure – Häufig gestellte Fragen](configuration-manager-on-azure.md)
