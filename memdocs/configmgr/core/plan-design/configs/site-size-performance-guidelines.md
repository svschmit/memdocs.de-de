---
title: Richtlinien zu Größe und Leistung von Standorten
titleSuffix: Configuration Manager
description: Auf die Standortgröße bezogene Leistungstestergebnisse, Methodik und Anleitungen.
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.topic: conceptual
ms.date: 04/23/2019
ms.openlocfilehash: 9e5cc21e4fef60f64576a7b578b3616a7e37756d
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82073499"
---
# <a name="configuration-manager-site-size-and-performance-guidelines"></a>Configuration Manager: Anleitungen zu Größe und Leistung von Standorten

*Gilt für: Configuration Manager (Current Branch)*

Configuration Manager ist branchenweit führend in Skalierbarkeit und Leistung. Weitere Dokumentation umfasst [maximal unterstützte Skalierbarkeitsgrenzen](size-and-scale-numbers.md) und [Hardwareempfehlungen](recommended-hardware.md) für den Betrieb von Standorten in den größten Umgebungen. Dieser Artikel enthält ergänzende Leistungsanleitungen für Umgebungen jeder Größe. Mit diesen Anleitungen können Sie genauer einschätzen, welche Hardware Sie benötigen, um den Configuration Manager bereitzustellen.

Dieser Artikel konzentriert sich auf die Komponente, auf die Configuration Manager-Leistungsengpässe vorwiegend zurückzuführen sind: das Ein-/Ausgabesubsystem des Datenträgers oder IOPS. Der Artikel:

- enthält nähere Informationen und Testergebnisse zu IOPS
- dokumentiert das Reproduzieren der Tests mit Ihren eigenen Umgebungen und Ihrer Hardware
- schlägt Datenträger-IOPS-Anforderungen für Umgebungen verschiedener Größe vor 

## <a name="performance-test-methodology"></a>Leistungstestmethodik

Sie können Configuration Manager in vielen individuellen Varianten bereitstellen, aber Sie müssen einige Variablen kennen, die in allen Diskussionen zur Größenanpassung von Bedeutung sind. Eine Variable ist das *Featureintervall*, z.B. ein Inventurzyklus. Andere Variablen sind die Anzahl von Benutzern, Softwarebereitstellungen oder anderen *Objekten*, auf die das System verweist, oder die es bereitstellt. Das Testen der Leistung wendet diese Variablen als Teil einer *Last* an. Die Last generiert mithilfe von Produktionsbereitstellungen in Umgebungen unterschiedlicher Größe Objekte mit einer typischen Rate für Enterprisekunden.

> [!NOTE] 
> Telemetriedaten von Kunden ermöglichen das Testen aktueller Branchbuilds mit den häufigsten Szenarien, Konfigurationen und Einstellungen für die meisten Kunden. Die Empfehlungen in diesem Artikel basieren auf diesen Durchschnittswerten. Ihre Erfahrungen können je nach der Größe Ihrer Umgebung und Ihrer Konfiguration variieren. Im Allgemeinen setzt Configuration Manager beim Umgang mit Objekten und Intervallen gesunden Menschenverstand voraus. Nur weil Sie jede Datei auf einem System erfassen oder das Intervall für einen Zyklus auf die Minute genau festlegen können, bedeutet dies nicht, dass Sie es auch tun sollten.

In den folgenden Abschnitten werden einige wichtige Einstellungen und Konfigurationen hervorgehoben, die Sie beim Testen und Modellieren von Verarbeitungsanforderungen für große Unternehmen verwenden können. Diese Richtlinien unterstützen die Festlegung grundlegender Systemleistungserwartungen für die empfohlenen Hardwaregrößen.

### <a name="feature-intervals-settings"></a>Featureintervalleinstellungen 
Bei den meisten Tests sollten Sie Standardintervalle für die wichtigsten Zyklen im System verwenden. Hardwareinventurtests sollten z.B. einmal pro Woche mit einer *MOF*-Datei durchgeführt werden, deren Größe über dem Standard liegt. Einige periodisch auftretende Featureintervalle, insbesondere Hardware- und Softwareinventurzyklen, können bedeutenden Einfluss auf die Leistungsmerkmale einer Umgebung haben. In Umgebungen, die aggressive Standardintervalle für die Datensammlung aktivieren, muss die Hardware direkt proportional zum Aktivitätsanstieg überdimensioniert sein. Stellen Sie sich z.B. vor, Sie verfügen über 25.000 Desktopclients und möchten die Hardwareinventur zwei Mal schneller als mit dem Standardintervall durchführen. Sie sollten zunächst die Hardware Ihres Standorts so dimensionieren, als hätten Sie 50.000 Clients.

### <a name="objects"></a>Objects 
In Tests sollte der *obere Durchschnitt* der Objekte verwendet werden, die große Unternehmen in der Regel mit dem System verwenden. Typische Werte sind Tausende von Sammlungen und Anwendungen, die für Hunderte oder Tausende von Benutzern oder Systemen bereitgestellt werden. Tests sollten gleichzeitig auf *allen* Objekten im System mit diesen Grenzwerten ausgeführt werden. Viele Kunden nutzen mehrere Features, aber verwenden Sie nicht generell alle Features des Produkts mit diesen Obergrenzen. Tests mit allen Features des Produkts bieten Gewähr für die bestmögliche systemweite Leistung und schaffen einen Puffer für Features, die vielleicht von einigen Kunden überdurchschnittlich verwendet werden. 

### <a name="loads"></a>Lasten 
Tests sollten außerdem mit über dem Standard liegenden *durchschnittlichen Tageslasten* ausgeführt werden, indem Simulationen durchgeführt werden, die Spitzennutzungsanforderungen auf dem System generieren. Ein Beispiel ist das Simulieren von Patch-Dienstag-Rollouts, um sicherzustellen, dass das System Updatekonformitätsdaten während dieser Tage mit Spitzenauslastung schnell zurückgeben kann. Ein weiteres Beispiel ist das Simulieren der Standortaktivität während eines großflächigen Schadsoftwareausbruchs, um sicherzustellen, dass rechtzeitige Benachrichtigung und Antwort möglich sind. Bereitgestellte Computer der empfohlenen Größe sind vielleicht an manchen Tagen nicht ausgelastet, aber extremere Situationen erfordern einen Verarbeitungspuffer.

### <a name="configurations"></a>Konfigurationen
Führen Sie Tests mit einer Reihe von physischen, Hyper-V- und Azure-Hardwarekomponenten mit einer Mischung der unterstützten Betriebssysteme und SQL Server-Versionen durch. Überprüfen Sie immer die schlimmsten Fälle für die unterstützte Konfiguration. Im Allgemeinen liefern Hyper-V und Azure mit äquivalenter physischer Hardware bei ähnlicher Konfiguration vergleichbare Leistungsergebnisse. Neuere Serverbetriebssysteme bieten tendenziell mindestens die gleiche Leistung wie ältere unterstützte Serverbetriebssysteme. Während alle unterstützten Plattformen die Mindestanforderungen erfüllen, bieten die neuesten Versionen der unterstützenden Produkte wie Windows und SQL sogar in der Regel noch mehr Leistung. 

Die größte Abweichung resultiert aus den verwendeten SQL Server-Versionen. Weitere Informationen zu SQL Server-Versionen finden Sie unter [Welche Version von SQL sollte ich ausführen?](../../understand/site-size-performance-faq.md#what-version-of-sql-should-i-run). 

## <a name="key-performance-determinants"></a>Maßgebliche Leistungsfaktoren

Sie können die Configuration Manager-Leistung mit einer Vielzahl von Einstellungen, auf unterschiedliche Weise und mit verschiedenen Standortgrößen testen und messen. Die folgenden Einstellungen und Objekte können die Leistung erheblich beeinflussen. Beachten Sie diese unbedingt beim Testen und Modellieren der Leistung in Ihrer Umgebung.

> [!CAUTION]
> Für einige Aspekte von Configuration Manager sind offizielle Höchstwerte oder Benutzeroberflächenlimits festgelegt, die eine übermäßige Nutzung verhindern, und das Ignorieren dieser Richtlinien kann erhebliche negative Auswirkungen auf die Leistung eines Standorts haben. Die Überschreitung empfohlener Grenzen oder das Ignorieren einer Anleitung zur Größenanpassung erfordert in der Regel umfangreichere Hardware und kann die Wartung Ihrer Umgebung unmöglich machen, bis Sie Häufigkeit oder Anzahl bestimmter Objekte reduzieren.

### <a name="hardware-inventory"></a>Hardwareinventur
Führen Sie zum Testen der Basisleistung die Hardwareinventursammlung einmal pro Woche mit der standardmäßigen *MOF*-Dateigröße plus ungefähr 20% zusätzlicher Eigenschaften durch. Aktivieren Sie nicht alle Eigenschaften, und erfassen Sie nur Eigenschaften, die Sie tatsächlich benötigen. Widmen Sie dem Erfassen von Eigenschaften, die sich *immer* mit *jedem* Inventurzyklus ändern, wie z.B. verfügbarer virtueller Speicher, besondere Beachtung. Das Erfassen dieser Eigenschaften kann bei jedem Inventurzyklus jedes Clients zu einer übermäßigen Änderung führen.

### <a name="software-inventory"></a>Softwareinventur
Führen Sie zum Testen der Basisleistung die Softwareinventursammlung einmal pro Woche mit *ausschließlichen Produktdetails* durch. Das Erfassen vieler Dateien kann das Inventursubsystem erheblich belasten. Vermeiden Sie es, Filter anzugeben, die das Erfassen Tausender von Dateien vieler Clients zur Folge haben könnten, z.B. *\*EXE* oder *\*DLL*.

### <a name="collections"></a>Sammlungen
Das Testen der Basisleistung kann mehrere Tausend Sammlungen mit einer Vielzahl von Bereichs-, Größen- Komplexitäts- und Aktualisierungseinstellungen beinhalten. Die Standortleistung ist keine direkte Funktion der bloßen Anzahl von Sammlungen an einem Standort. Die Leistung ist auch ein Kreuzprodukt der Komplexität der Abfrage von Sammlungen, von vollständigen und inkrementellen Updates und Änderungshäufigkeit, von Abhängigkeiten der Sammlungen untereinander und der Anzahl von Clients in den Sammlungen.

Wenn möglich, minimieren Sie Sammlungen mit aufwändigen oder komplizierten dynamischen Regelabfragen. Legen Sie für Sammlungen, die diese Typen von Regeln benötigen, entsprechende Updateintervalle und Updatezeiten fest, um die Auswirkungen der erneuten Auswertung von Sammlungen auf dem System zu minimieren. Aktualisieren Sie beispielsweise um Mitternacht statt um 8:00 Uhr morgens.

Das Aktivieren inkrementeller Updates für Sammlungen stellt schnelle und rechtzeitige Updates der Sammlungsmitgliedschaft sicher. Aber obwohl inkrementelle Updates effizient sind, belasten sie dennoch das System. Wägen Sie die erwartete Änderungshäufigkeit gegen die Notwendigkeit nahezu in Echtzeit durchgeführter Updates der Mitgliedschaft ab. Stellen Sie sich z.B. vor, dass Sie eine gravierende Änderung bei Sammlungsmitgliedern erwarten, aber keine nahezu in Echtzeit durchgeführten Updates der Mitgliedschaft erforderlich sind. Es ist effizienter und für das System weniger belastend, die Sammlung in einem bestimmten Intervall mit einem geplanten vollständigen Update zu aktualisieren, als inkrementelle Updates zu aktivieren. 

Wenn Sie inkrementelle Updates aktivieren, reduzieren Sie alle geplanten vollständigen Updates der gleichen Sammlungen. Sie sind nur eine Sicherungsmethode der Auswertung, da inkrementelle Updates Ihre Sammlungsmitgliedschaft nahezu in Echtzeit aktualisiert halten sollten. Unter [Verwenden Sie keine inkrementellen Updates bei einer größeren Anzahl von Sammlungen](../../clients/manage/collections/best-practices-for-collections.md#bkmk_incremental) wird eine maximale Anzahl der gesamten Sammlungen für inkrementelle Updates empfohlen, aber der Artikel betont, dass Ihre Erfahrung basierend auf vielen Faktoren variieren kann.

Sammlungen, auf die ausschließlich Regeln für direkte Mitgliedschaft angewandt werden, und zu denen eine begrenzende Sammlung gehört, die keine inkrementellen Updates ausführt, benötigen keine geplanten vollständigen Updates. Deaktivieren Sie Updatepläne für diese Typen von Sammlungen, um eine unnötige Belastung des Systems zu verhindern. Wenn die begrenzende Sammlung inkrementelle Updates verwendet, spiegeln Sammlungen, auf die ausschließlich Regeln für direkte Mitgliedschaft angewandt werden, Mitgliedschaftsupdates möglicherweise bis zu 24 Stunden lang oder bis eine geplante Aktualisierung stattfindet nicht wider.

Es ist zwar keine bewährte Methode, aber einige Organisationen erstellen Hunderte oder sogar Tausende von Sammlungen als Teil der verschiedenen Geschäftsprozesse. Wenn Sie Sammlungen automatisch erstellen, müssen Sie ggf. benötigte inkrementelle Updates ordnungsgemäß aktivieren. Minimieren und verteilen Sie Pläne vollständiger Updates, um Hotspots der Sammlungsauswertung während eines einzelnen Zeitraums zu vermeiden. Richten Sie einen regulären Bereinigungsprozess zum Löschen nicht verwendeter Sammlungen ein, insbesondere dann, wenn Sie Sammlungen automatisch erstellen, die Sie nach einiger Zeit nicht mehr benötigen.

Denken Sie daran, dass Configuration Manager Richtlinien für alle Objekte in Ihren Sammlungen erstellt, wenn Sie Aufgaben wie Bereitstellungen auf sie anwenden. Änderungen der Gruppenmitgliedschaft mittels geplanter oder inkrementeller Updates können einen großen Aufwand für das gesamte System bedeuten. Die neuesten aktuellen Branchbuilds verfügen über spezielle Richtlinienoptimierungen für „Alle Systeme“- und „Alle Benutzer“-Sammlungen. Wenn Sie auf Ihr gesamtes Unternehmen abzielen, verwenden Sie die integrierten Sammlungen statt eines Klons dieser integrierten Sammlungen.

Um die Sammlungsleistung noch gründlicher zu untersuchen, können Sie den Collection Evaluation Viewer (CEViewer) im [Configuration Manager-Toolkit](https://www.microsoft.com/download/details.aspx?id=50012) verwenden.

### <a name="discovery-methods"></a>Ermittlungsmethoden
Führen Sie für die Basisleistungstests einmal pro Woche serverbasierte Ermittlungsmethoden durch, wobei Sie die Deltaermittlung in angemessener Weise aktivieren, um die Daten während der Woche aktuell zu halten. Die Tests sollten eine zur simulierten Unternehmensgröße proportionale Objektmenge ermitteln. Der Basisleistungstest für die Taktermittlung sollte ebenfalls einmal pro Woche ausgeführt.

Ermittlungsdaten sind globale Daten. Ein häufiges leistungsbezogenes Problem ist die fehlerhafte Konfiguration serverbasierter Ermittlungsmethoden in einer Hierarchie, wodurch die doppelte Ermittlung derselben Ressourcen auf mehreren primären Standorten verursacht wird. Konfigurieren Sie die Ermittlungsmethoden sorgfältig, um die Kommunikation mit dem Zieldienst, wie Active Directory-Domänencontrollern, zu optimieren und dabei eine Duplizierung desselben Ermittlungsbereichs auf mehreren primären Standorten zu vermeiden.

## <a name="general-sizing-guidelines"></a>Allgemeine Richtlinien zur Größenanpassung 

Basierend auf der vorherigen [Leistungstestmethodik](#performance-test-methodology) enthält die folgende Tabelle allgemeine Richtlinien für *minimale* Hardwareanforderungen für jeweils eine bestimmte Anzahl von verwalteten Clients. Mit diesen Werten sollten die meisten Kunden mit der angegebenen Anzahl von Clients Objekte schnell genug verarbeiten können, um den angegebenen Standort zu verwalten. Der Preis der Rechenleistung sinkt weiterhin von Jahr zu Jahr, und einige der unten aufgeführten Anforderungen sind im Hinblick auf moderne Serverhardwarekonfigurationen gering. Hardware, die die folgenden Richtlinien überschreitet, erhöht die Leistung für Standorte proportional, die zusätzliche Rechenleistung erfordern oder spezielle Produktverwendungsmuster haben. 

| Desktopclients  | Standorttyp/-rolle  | Kerne<sup>1</sup>   | Arbeitsspeicher (GB)   | SQL-Speicherreservierung  | IOPS:  Eingangsboxen<sup>2</sup>  | IOPS: SQL<sup>2</sup>   | Benötigter Speicherplatz (GB)<sup>3</sup>   |
|------|-------------------------------------------------------------|-----|-----|-----|------|------|------|
| 25KB  | Primär oder CAS mit Datenbankstandortrolle auf dem gleichen Server   | 6   | 24  | 65% | 600  | 1\.700 | 350  |
| 25.000  | Primär oder CAS                                              | 4   | 8   |     | 600  |      | 100  |
|      | Remote-SQL                                                  | 4   | 16  | 70% |      | 1\.700 | 250  |
|      |                                                             |     |     |     |      |      |      |
| 50.000  | Primär oder CAS mit Datenbankstandortrolle auf dem gleichen Server   | 8   | 32  | 70% | 1\.200 | 2\.800 | 600  |
| 50.000  | Primär oder CAS                                              | 4   | 8   |     | 1\.200 |      | 200  |
|      | Remote-SQL                                                  | 8   | 24  | 70% |      | 2\.800 | 400  |
|      |                                                             |     |     |     |      |      |      |
| 100.000 | Primär oder CAS mit Datenbankstandortrolle auf dem gleichen Server   | 12  | 64  | 70% | 1\.200 | 5000 | 1\.100 |
| 100.000 | Primär oder CAS                                              | 6   | 12  |     | 1\.200 |      | 300  |
|      | Remote-SQL                                                  | 12  | 48  | 80% |      | 5000 | 800  |
|      |                                                             |     |     |     |      |      |      |
| 150.000 | Primär oder CAS mit Datenbankstandortrolle auf dem gleichen Server   | 16  | 96  | 70% | 1\.800 | 7\.400 | 1\.600 |
| 150.000 | Primär oder CAS                                   | 8   | 16   |     | 1\.800  |         | 400   |
|      | Remote-SQL                                       | 16  | 72   | 90% |       | 7\.400    | 1\.200  |
|      |                                                             |     |     |     |      |      |      |
| 700.000 | CAS mit Datenbankstandortrolle auf dem gleichen Server   | 20+ | 128+ | 80% | 1\.800+ | 9\.000+   | 5\.000+ |
| 700.000 | CAS                                              | 8+  | 16+  |     | 1\.800+ |         | 500+  |
|      | Remote-SQL                                       | 16+ | 96+  | 90% |       | 9\.000+   | 4\.500+ |
|      |                                                             |     |     |     |      |      |      |
| 5\.000   | Sekundärer Standort                                   | 4   | 8    |     | 500   | -       | 200   |
| 15.000  | Sekundärer Standort                                   | 8   | 16   |     | 500   | -       | 300   |

**Hinweise**

1. **Kerne**: Configuration Manager führt viele gleichzeitige Prozesse durch und benötigt daher eine bestimmte minimale Anzahl von CPU-Kernen für die verschiedenen Standortgrößen. Während die Kerne jedes Jahr schneller werden, ist es wichtig, sicherzustellen, dass eine bestimmte Mindestanzahl von Kernen parallel eingesetzt wird. Im Allgemeinen erfüllt jede nach 2015 hergestellte CPU auf Serverebene die grundlegenden Leistungsanforderungen für die in der Tabelle angegebenen Kerne. Configuration Manager nutzt zwar die Vorteile zusätzlicher Kerne, die die empfohlene Anzahl übertreffen, aber sobald Sie über die empfohlene Mindestanzahl von Kernen verfügen, sollten Sie im Allgemeinen die CPU-Ressourceninvestitionen priorisieren, um die Geschwindigkeit vorhandener Kerne zu erhöhen, anstatt weitere, langsamere Kerne hinzuzufügen. Beispielsweise bietet Configuration Manager bei wichtigen Verarbeitungsaufgaben mit 16 schnellen Kernen eine bessere Leistung als mit 24 langsameren Kernen, vorausgesetzt, dass genügend andere Systemressourcen wie Datenträger-IOPS verfügbar sind.
   
   Die Beziehung zwischen Kernen und Arbeitsspeicher ist auch wichtig. Im Allgemeinen reduzieren weniger als 3-4GB RAM pro Kern die gesamte Verarbeitungskapazität auf Ihren SQL-Servern. Sie benötigen mehr RAM pro Kern, wenn SQL mit den Komponenten des Standortservers zusammengestellt wird.
   
   > [!NOTE]
   > Bei allen Tests werden Computerenergiesparpläne festgelegt, die maximalen Energieverbrauch und maximale Leistung der CPU bestimmen.
   
2. **„IOPS: Eingangsboxen“ und „IOPS: SQL“** beziehen sich auf die IOPS-Anforderungen für Configuration Manager und logische SQL-Laufwerke. Die Spalte **IOPS: Eingangsboxen** zeigt die IOPS-Anforderungen für das logische Laufwerk, auf dem sich die Eingangsboxenverzeichnisse von Configuration Manager befinden. Die Spalte **IOPS: SQL** zeigt die gesamten IOPS-Anforderungen für die logischen Laufwerke, die verschiedene SQL-Dateien verwenden. Diese Spalten unterscheiden sich, da die beiden Laufwerke unterschiedlich formatiert sein sollten. Weitere Informationen und Beispiele zu empfohlenen SQL-Datenträgerkonfigurationen und bewährten Dateimethoden einschließlich des Aufteilens von Dateien auf mehrere Volumes finden Sie unter [Häufig gestellte Fragen zu Größe und Leistung von Standorten](../../understand/site-size-performance-faq.md).
   
   Beide IOPS-Spalten verwenden Daten vom Branchenstandardtool *Diskspd*. Unter [Messen der Datenträgerleistung](#how-to-measure-disk-performance) finden Sie Anweisungen zum Duplizieren dieser Messungen. Sobald Sie grundlegende CPU- und Speicheranforderungen erfüllen, hat das Speichersubsystem im Allgemeinen den größten Einfluss auf die Standortleistung, und Verbesserungen rentieren sich hier am ehesten.
   
3.  **Benötigter Speicherplatz:** Diese Praxiswerte können von anderen dokumentierten Empfehlungen abweichen. Diese Zahlen dienen nur als allgemeine Richtlinie; einzelne Anforderungen können stark abweichen. Planen Sie den Datenträgerspeicherbedarf sorgfältig vor der Installation des Standorts. Berücksichtigen Sie, dass ein gewisses Maß dieses Speichers die meiste Zeit als freier Datenträgerspeicherplatz verfügbar bleibt. Sie können diesen Pufferspeicher in einem Wiederherstellungsszenario verwenden, oder für Upgradeszenarien, die freien Speicherplatz für eine Setuppaketerweiterung benötigen. Möglicherweise erfordert Ihr Standort zusätzlichen Speicher für große Mengen von Datensammlungen, längere Perioden der Datenaufbewahrung und große Mengen an Softwareverteilungsinhalt. Sie können diese Elemente auch auf separaten Volumes mit niedrigerem Durchsatz speichern.

## <a name="how-to-measure-disk-performance"></a>Messen der Datenträgerleistung 

Sie können mit dem Branchenstandardtool *Diskspd* standardisierte Vorschläge für den IOPS angeben, die Configuration Manager-Umgebungen in verschiedener Größe erfordern. Die folgenden Befehlszeilen und Testschritte sind zwar nicht vollständig, stellen aber eine einfache und reproduzierbare Möglichkeit dar, den Durchsatz des Datenträgersubsystems Ihres Servers zu schätzen. Sie können Ihre Ergebnisse mit dem empfohlenen Mindest-IOPS in der Tabelle [Allgemeine Richtlinien zur Größenanpassung](#general-sizing-guidelines) vergleichen. 

Unter [Beispiel für Datenträgerkonfigurationen](#example-disk-configurations) finden Sie Testergebnisse aus einer Vielzahl von Hardwarekonfigurationen in Laborumgebungen. Sie können die Daten als groben Ausgangspunkt nutzen, wenn Sie das Speichersubsystem für eine neue Umgebung von Grund auf neu entwerfen.

### <a name="to-test-disk-iops"></a>So testen Sie den Datenträger-IOPS  
1. Laden Sie das *Diskspd*-Hilfsprogramm hier herunter: [https://gallery.technet.microsoft.com/DiskSpd-A-Robust-Storage-6ef84e62](https://gallery.technet.microsoft.com/DiskSpd-A-Robust-Storage-6ef84e62).
   
1. Stellen Sie sicher, dass Sie über mindestens 100GB freien Speicherplatz verfügen. Deaktivieren Sie alle Apps, die stören oder eine zusätzliche Last auf dem Datenträger sein könnten, z.B. aktive Überprüfungen des Verzeichnisses auf Viren, SQL oder SMSExec.
   
1. Starten Sie *Diskspd* in einem Eingabeaufforderungsfenster mit erhöhten Rechten neu. 
   
   Führen Sie das Tool zweimal nacheinander für das Volume aus, das Sie testen möchten. Der erste Test führt eine Minute lang zufällige Schreibvorgänge in der Größe von 64 KB aus. Dieser Test stellt sicher, dass der Controllercache geladen und Datenträgerspeicherplatz zugeordnet wird, falls das Volume dynamisch erweitert wird. Verwerfen Sie die Ergebnisse des ersten Tests. Der zweite Test sollte *sofort* nach dem ersten Test ausgeführt werden und die gleiche Last fünf Minuten lang ausführen.
   
   Verwenden Sie beispielsweise die folgenden spezifischen Befehlszeilen zum Testen des G:\\-Volumes.
   
   `DiskSpd.exe -r -w100 -t8 -o8 -b64K -c100G -d60 -h -L G:\\test\testfile.dat` 
   
   `del G:\\test\testfile.dat`
   
   `DiskSpd.exe -r -w100 -t8 -o8 -b64K -c100G -d300 -h -L G:\\test\testfile.dat`
   
1. Überprüfen Sie die Ausgabe des zweiten Tests, um den Gesamt-IOPS der Spalte **I/O per s** (E/A pro Sekunde) zu entnehmen. Im folgenden Beispiel beträgt der Gesamt-IOPS **3929,18**.

   ``` Output
   Total IO
   | thread |  bytes      |  I/Os   |  MB/s  | I/O per s | AvgLat | LatStdDev |
   |--------|-------------|---------|--------|-----------|--------|-----------|
   |   1    |  9651814400 |  147275 |  30.68 |    490.92 | 16.294 | 10.210    |
   |   2    |  9676652544 |  147654 |  30.76 |    492.18 | 16.252 |  9.998    |
   |   3    |  9638248448 |  147068 |  30.64 |    490.23 | 16.317 | 10.295    |
   |   4    |  9686089728 |  147798 |  30.79 |    492.66 | 16.236 | 10.072    |
   |   5    |  9590931456 |  146346 |  30.49 |    487.82 | 16.398 | 10.384    |
   |   6    |  9677242368 |  147663 |  30.76 |    492.21 | 16.251 | 10.067    |
   |   7    |  9637330944 |  147054 |  30.64 |    490.18 | 16.319 | 10.249    |
   |   8    |  9692577792 |  147897 |  30.81 |    492.99 | 16.225 | 10.125    |
   | Total: | 77250887680 | 1178755 | 245.57 |   3929.18 | 16.286 | 10.176    |
   ```

## <a name="example-disk-configurations"></a>Beispiele für Datenträgerkonfigurationen

Die folgenden Tabellen zeigen die Ergebnisse der Testschritte in [Messen der Datenträgerleistung](#how-to-measure-disk-performance) mit verschiedenen Testlaborkonfigurationen. Nutzen Sie diese Daten als *groben* Ausgangspunkt, wenn Sie das Speichersubsystem für eine neue Umgebung von Grund auf neu entwerfen. 

### <a name="physical-machines-and-hyper-v"></a>Physische Computer und Hyper-V 
Hardware wird ständig verbessert. Gehen Sie davon aus, dass neuere Hardwaregenerationen und andere Hardwarekombinationen, z.B. SSDs und SANs, die im Folgenden erwähnte Leistung überschreiten. Diese Ergebnisse sind ein einfacher Ausgangspunkt für die Überlegungen beim Entwerfen eines Servers oder für Diskussionen mit Ihrem Hardwarehersteller.

Die folgende Tabelle zeigt die Ergebnisse in verschiedenen Datenträgersubsystemen einschließlich Spindel und SSD-basierter Festplatten in verschiedenen Testlaborkonfigurationen. Alle Konfigurationen formatieren die Datenträger mit 64-KB-Clustern und fügen sie einem Datenträgercontroller der Unternehmensklasse an. Zusätzlich zur Anzahl der RAID-Arraydatenträger verfügen sie jeweils über mindestens einen Ersatzdatenträger.

| Datenträgertyp   | Anzahl der Datenträger, 1 Ersatzdatenträger nicht eingeschlossen | RAID     | Gemessener IOPS  |
|------------------|----------------------------------------------------|---------------|---------------|
| 15K SAS          | 2                                                  |           1   | 620           |
| 15K SAS          | 4                                                  |           10  | 1\.206          |
| 15K SAS          | 6                                                  |           10  | 1\.751          |
| 15K SAS          | 8                                                  |           10  | 2\.322          |
| 15K SAS          | 10                                                 |           10  | 2\.882          |
| 15K SAS          | 12                                                 |           10  | 3\.476          |
| 15K SAS          | 16                                                 |           10  | 4\.236          |
| 15K SAS          | 20                                                 |           10  | 5\.148          |
| 15K SAS          | 30                                                 |           10  | 7\.398          |
| 15K SAS          | 40                                                 |           10  | 9\.913          |
| SSD SATA         | 2                                                  |           1   | 3\.300          |
| SSD SATA         | 4                                                  |           10  | 5\.542          |
| SSD SATA         | 6                                                  |           10  | 7201          |
| SSD SAS          | 2                                                  |           1   | 7\.539          |
| SSD SAS          | 4                                                  |           10  | 14346         |
| SSD SAS          | 6                                                  |           10  | 15.607         |

Hierbei handelt es sich um die Geräte, die im Beispiel verwendet werden. Diese Informationen sind keine Empfehlung für bestimmte Hardwaremodelle oder -hersteller. 

| Datenträgertyp    | Modell      | RAID-Controller | Cachespeicher und -konfiguration |
|-------------------|-----------------|----------------------|-------------------------------------|
| 15K U/Min SAS HD    | HP EH0300JDYTH  | Smart Array P822     | 2GB, 20% lesen / 80% schreiben           |
| SSD SATA          | ATA MK0200GCTYV | Smart Array P420i    | 1GB, 20% lesen / 80% schreiben           |
| SSD SAS           | HP MO0800 JEFPB | Smart Array P420i    | 1GB, 20% lesen / 80% schreiben           |

### <a name="azure-machine-and-disk-performance"></a>Azure-Computer und Datenträgerleistung 
Die Azure-Datenträgerleistung hängt von verschiedenen Faktoren wie z.B. der Größe der Azure-VM sowie der Anzahl und dem Typ des verwendeten Datenträgers ab. Azure fügt auch ständig neue Computertypen und Datenträgergeschwindigkeiten hinzu, die sich vom folgenden Diagramm unterscheiden. Weitere Informationen zur Ausführung von Configuration Manager in Azure und zum Verständnis der Datenträger-E/A in Azure finden Sie unter [Configuration Manager in Azure – Häufig gestellte Fragen](../../understand/configuration-manager-on-azure.md).

Alle Datenträger werden mit einer Clustergröße von 64KB im NTFS-Format formatiert, und Reihen mit mehreren Datenträgern werden mithilfe des Windows-Hilfsprogramms zur Datenträgerverwaltung als Stripesetvolumes konfiguriert.

| Azure-VM| Azure-Datenträger| Anzahl von Datenträgern | Verfügbarer Speicherplatz | Gemessener IOPS   | Begrenzungsfaktor   |
|--------------------------------------------|-------------------------|---------------------|---------------------------|-------|-----------------|
| **DS2/DS11**                              | P20                     | 1                   | 512 MB                    | 965   | Azure-VM-Größe   |
| **DS2/DS11**                              | P20                     | 2                   | 1\.024MB                   | 996   | Azure-VM-Größe   |
| **DS2/DS11**                              | P30                     | 1                   | 1\.024MB                   | 996   | Azure-VM-Größe   |
| **DS2/DS11**                              | P30                     | 2                   | 2\.048MB                   | 996   | Azure-VM-Größe   |
| **DS3/DS12/F4S**                          | P20                     | 1                   | 512 MB                    | 1\.994  | Azure-VM-Größe   |
| **DS3/DS12/F4S**                          | P20                     | 2                   | 1\.024MB                   | 1\.992  | Azure-VM-Größe   |
| **DS3/DS12/F4S**                          | P30                     | 1                   | 1\.024MB                   | 1\.993  | Azure-VM-Größe   |
| **DS3/DS12/F4S**                          | P30                     | 2                   | 2\.048MB                   | 1\.992  | Azure-VM-Größe   |
| **DS4/DS13/F8S**                          | P20                     | 1                   | 512 MB                    | 2\.334  | P20-Datenträger        |
| **DS4/DS13/F8S**                          | P20                     | 2                   | 1\.024MB                   | 3\.984  | Azure-VM-Größe   |
| **DS4/DS13/F8S**                          | P20                     | 3                   | 1\.536MB                   | 3\.984  | Azure-VM-Größe   |
| **DS4/DS13/F8S**                          | P30                     | 1                   | 1\.024MB                   | 3\.112  | P30-Datenträger        |
| **DS4/DS13/F8S**                          | P30                     | 2                   | 2\.048MB                   | 3\.984  | Azure-VM-Größe   |
| **DS4/DS13/F8S**                          | P30                     | 3                   | 3\.072 MB                   | 3\.996  | Azure-VM-Größe   |
| **DS5/DS14/F16S**                         | P20                     | 1                   | 512 MB                    | 2\.335  | P20-Datenträger        |
| **DS5/DS14/F16S**                         | P20                     | 2                   | 1\.024MB                   | 4\.639  | P20-Datenträger        |
| **DS5/DS14/F16S**                         | P20                     | 3                   | 1\.536MB                   | 6\.913  | P20-Datenträger        |
| **DS5/DS14/F16S**                         | P20                     | 4                   | 2\.048MB                   | 7\.966  | Azure-VM-Größe   |
| **DS5/DS14/F16S**                         | P30                     | 1                   | 1\.024MB                   | 3\.112  | P30-Datenträger        |
| **DS5/DS14/F16S**                         | P30                     | 2                   | 2\.048MB                   | 6\.182  | P30-Datenträger        |
| **DS5/DS14/F16S**                         | P30                     | 3                   | 3\.072 MB                   | 7\.963  | Azure-VM-Größe   |
| **DS5/DS14/F16S**                         | P30                     | 4                   | 4\.096MB                   | 7\.968  | Azure-VM-Größe   |
| **DS15**                                  | P30                     | 1                   | 1\.024MB                   | 3\.113  | P30-Datenträger        |
| **DS15**                                  | P30                     | 2                   | 2\.048MB                   | 6\.184  | P30-Datenträger        |
| **DS15**                                  | P30                     | 3                   | 3\.072 MB                   | 9225  | P30-Datenträger        |
| **DS15**                                  | P30                     | 4                   | 4\.096MB                   | 10.200 | Azure-VM-Größe   |

## <a name="see-also"></a>Weitere Informationen:

- [Häufig gestellte Fragen zu Größe und Leistung von Standorten](../../understand/site-size-performance-faq.md)
- [Configuration Manager in Azure – Häufig gestellte Fragen](../../understand/configuration-manager-on-azure.md)
- [Size and scale numbers (Anpassen und Skalieren von Zahlen)](size-and-scale-numbers.md)
- [Empfohlene Hardware](recommended-hardware.md)

