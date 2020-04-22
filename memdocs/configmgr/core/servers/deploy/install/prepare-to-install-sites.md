---
title: Prepare to install System Center Configuration Manager sites (Vorbereitung zur Installation von Standorten für System Center Configuration Manager)
titleSuffix: Configuration Manager
description: Wenn Sie beabsichtigen, mehrere Configuration Manager-Standorte zu installieren, lesen Sie diese Informationen, um Zeit zu sparen und Fehler zu vermeiden.
ms.date: 09/18/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 9089e1b5-cba4-42bd-a2de-126ef882a3af
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 87c1713f9903cf704e484c49f7e720e6f0bd3e4a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700718"
---
# <a name="prepare-to-install-configuration-manager-sites"></a>Vorbereiten auf die Installation von Configuration Manager-Standorten

*Gilt für: Configuration Manager (Current Branch)*

Zur Vorbereitung auf eine erfolgreiche Bereitstellung von Configuration Manager-Standorten machen Sie sich mit den Details in diesem Artikel vertraut. Durch diese Schritte können Sie während der Installation von mehreren Standorten Zeit sparen und Fehler vermeiden, nach denen möglicherweise einer oder mehrere Standorte neu installiert werden müssen.

> [!TIP]
> Beim Verwalten des Configuration Manager-Standorts und der Hierarchieinfrastruktur werden die Begriffe *Upgrade*, *Update* und *Installation* verwendet, um drei verschiedene Konzepte zu beschreiben. Erfahren Sie mehr über die Verwendung der Begriffe unter [Informationen zu Upgrade, Update und Installation für einen Standort und eine Hierarchieinfrastruktur](../../../understand/upgrade-update-install.md).

## <a name="options-for-installing-different-types-of-sites"></a><a name="bkmk_options"></a> Optionen für die Installation verschiedener Standorttypen
Wenn Sie einen neuen Configuration Manager-Standort installieren, hängt die Version der Quelldateien, die Sie verwenden können, von der Version der Standorte ab, die sich bereits in der Hierarchie befinden (falls vorhanden). Die verfügbaren Installationsmethoden hängen vom jeweiligen Standorttyp ab, den Sie installieren möchten.  

Stellen Sie vor der Installation eines Standorts sicher, dass Sie Ihre Hierarchie geplant haben und den Standorttyp kennen, den Sie installieren möchten. Weitere Informationen finden Sie unter [Entwerfen einer Hierarchie von Standorten](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).


### <a name="first-site"></a>Erster Standort
Der erste Standort, den Sie in einer Hierarchie installieren, ist entweder ein eigenständiger primärer Standort oder ein Standort der zentralen Verwaltung.

**Installationsmedium:** Zur Installation eines Standorts der zentralen Verwaltung oder eines eigenständigen primären Standorts als erster Standort in einer neuen Hierarchie benötigen Sie eine [Baselineversion](../../../../core/servers/manage/updates.md#bkmk_Baselines) von Configuration Manager. Installieren Sie den ersten Standort einer neuen Hierarchie nicht mit aktualisierten Quelldateien aus dem [Ordner CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) eines beliebigen Standorts.

**Installationsmethode:** Sie können beide Standorttypen mithilfe des [Configuration Manager-Setup-Assistenten](../../../../core/servers/deploy/install/use-the-setup-wizard-to-install-sites.md) installieren, oder Sie können ein Skript für eine [Installation über die Befehlszeile mithilfe von Skripts](../../../../core/servers/deploy/install/use-a-command-line-to-install-sites.md) konfigurieren.


### <a name="additional-sites"></a>Zusätzliche Standorte
Nachdem der erste Standort installiert ist, können Sie weitere Standorte zu einem beliebigen Zeitpunkt hinzufügen. Sie haben folgende Optionen, um Standorte hinzuzufügen (bis zu den [unterstützten Höchstgrenzen](../../../../core/plan-design/configs/size-and-scale-numbers.md)):

|Vorhandener Standort|Zusätzliche Standorttypen, die Sie installieren können|
|---|---|
|Standort der zentralen Verwaltung|Untergeordneter primärer Standort|
|Untergeordneter primärer Standort|Sekundärer Standort|
|Eigenständiger primärer Standort|Sekundärer Standort (Sie können den primären Standort erweitern, wodurch der eigenständige primäre Standort in einen untergeordneten primären Standort konvertiert wird)|

**Installationsmedium:** Wenn Sie einen Standort der zentralen Verwaltung installieren, um einen eigenständigen primären Standort zu erweitern, oder einen neuen untergeordneten primären Standort in einer vorhandenen Hierarchie installieren, benötigen Sie Installationsmedien (die Quelldateien enthalten), die mit der Version der/des vorhandenen Standorte/s übereinstimmen.

> [!IMPORTANT]
> Wenn Sie konsoleninterne Aktualisierungen installiert haben, die die Versionen der zuvor installierten Standorte geändert haben, verwenden Sie nicht die Originalinstallationsmedien. Verwenden Sie in diesem Szenario stattdessen Quelldateien aus dem [Ordner CD.Latest](../../../../core/servers/manage/the-cd.latest-folder.md) eines aktualisierten Standorts. Configuration Manager erfordert die Verwendung von Quelldateien, die mit der Version des bestehenden Standorts übereinstimmen, mit dem der neue Standort eine Verbindung herstellt.

Ein sekundärer Standort muss mithilfe der Configuration Manager-Konsole installiert werden. Auf diese Weise werden sekundäre Standorte immer mithilfe von Quelldateien aus dem übergeordneten primären Standort installiert.

**Installationsmethode:** Die Methode, die Sie zum Installieren zusätzlicher Standorte verwenden, hängt vom Typ des Standorts ab, den Sie installieren möchten.
- **Für einen Standort der zentralen Verwaltung:**  Sie können den Configuration Manager-Setup-Assistenten oder eine skriptgesteuerte Befehlszeile verwenden, um den neuen Standort der zentralen Verwaltung als übergeordneten Standort für Ihren vorhandenen eigenständigen primären Standort zu installieren. Weitere Informationen finden Sie unter [Erweitern eines eigenständigen primären Standorts](../../../../core/servers/deploy/install/prerequisites-for-installing-sites.md#bkmk_expand).
- **Für einen untergeordneten primären Standort:**  Sie können den Configuration Manager-Setup-Assistenten oder eine Befehlszeileninstallation verwenden, um einen untergeordneten primären Standort unterhalb eines Standorts der zentralen Verwaltung hinzuzufügen.
- **Für einen sekundären Standort:**  Verwenden Sie die Configuration Manager-Konsole zur Installation eines sekundären Standorts als untergeordneten Standort unter einem primären Standort. Andere Methoden werden für das Hinzufügen sekundärer Standorte nicht unterstützt.

## <a name="common-tasks-to-complete-before-starting-an-installation"></a><a name="bkmk_tasks"></a> Gängige vor dem Starten einer Installation auszuführende Tasks
- **Vertrautmachen mit der Topologie der Hierarchie, die Sie für Ihre Bereitstellung verwenden**    
Weitere Informationen finden Sie unter [Entwerfen einer Hierarchie von Standorten für Configuration Manager](../../../../core/plan-design/hierarchy/design-a-hierarchy-of-sites.md).  

- **Vorbereiten und Konfigurieren von einzelnen Servern zum Erfüllen der Voraussetzungen und unterstützte Konfigurationen für die Verwendung mit Configuration Manager**         
Weitere Informationen finden Sie unter [Site and site system prerequisites for System Center Configuration Manager](../../../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Standort- und Standortsystemanforderungen für System Center Configuration Manager).  

- **Installation und Konfiguration von SQL Server zum Hosten der Standortdatenbank**     
Weitere Informationen finden Sie unter [Unterstützte SQL Server-Versionen für Configuration Manager](../../../../core/plan-design/configs/support-for-sql-server-versions.md).  

- **Vorbereiten der Netzwerkumgebung zur Unterstützung von Configuration Manager**      
Weitere Informationen finden Sie unter [Configure firewalls, ports, and domains to prepare for Configuration Manager (Konfigurieren von Firewalls, Ports und Domänen als Vorbereitung für Configuration Manager)](../../../../core/plan-design/network/configure-firewalls-ports-domains.md).  

- **Wenn Sie eine Public Key-Infrastruktur (PKI) verwenden möchten, bereiten Sie Ihre Infrastruktur und Zertifikate vor**      
Weitere Informationen finden Sie unter [PKI-Zertifikatanforderungen für Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).

- **Installieren Sie die neuesten Sicherheitsupdates auf Computern, die Sie als Standortserver oder Standortsystemserver verwenden, und starten Sie diese wenn nötig neu**

## <a name="about-site-names-and-site-codes"></a><a name="bkmk_sitecodes"></a> Informationen zu Standortnamen und Standortcodes
Mithilfe von Standortcodes und Standortnamen werden die Standorte einer Configuration Manager-Hierarchie identifiziert und verwaltet. In der Configuration Manager-Konsole werden Standortcode und Standortname im Format &lt;*Standortcode*\> - &lt;*Standortname*\> angezeigt. Jeder in Ihrer Hierarchie verwendete Standortcode muss eindeutig sein. Wenn Active Directory für Configuration Manager erweitert wurde und Daten an Ihren Standorten veröffentlicht werden, müssen die Standortcodes innerhalb der Active Directory-Gesamtstruktur eindeutig sein. Dies gilt auch dann, wenn sie in einer anderen Configuration Manager-Hierarchie verwendet werden oder in früheren Configuration Manager-Installationen verwendet wurden. Planen Sie die Standortcodes und Standortnamen sorgfältig, bevor Sie die Hierarchie bereitstellen.

### <a name="specify-a-site-code-and-site-name"></a>Angeben eines Standortcodes und Standortnamens
Während des Configuration Manager-Setups werden Sie dazu aufgefordert, einen Standortcode und einen Standortnamen für den Standort der zentralen Verwaltung sowie für jede primäre und sekundäre Standortinstallation anzugeben. Ein Standortcode muss jeden Standort in der Hierarchie eindeutig identifizieren. Da der Standortcode in Ordnernamen verwendet wird, dürfen keine der folgenden Namen für den Standortcode verwendet werden. Dazu zählen für Configuration Manager und Windows reservierte Namen wie:
- AUX
- CON
- NUL
- PRN
- SMS
- ENV <!--SCCMDocs-1871 and 5399453-->

> [!NOTE]
> Das Configuration Manager-Setup überprüft nicht, ob ein Standortcode bereits verwendet wird.

Zum Eingeben des Standortcodes für einen Standort während des Configuration Manager-Setups müssen Sie drei alphanumerische Zeichen eingeben. Nur die Buchstaben *A* bis *Z* und die Ziffern *0* bis *9* sind in beliebiger Kombination in Standortcodes zulässig. Die Reihenfolge der Buchstaben oder Ziffern hat keine Auswirkungen auf die Kommunikation zwischen Standorten. Es ist beispielsweise nicht notwendig, den primären Standort mit *ABC* und den sekundären Standort mit *DEF* zu benennen.

Der Standortname dient als Anzeigename für den Standort. Sie können in Standortnamen nur die Zeichen *A* bis *Z*, *a* bis *z*, *0* bis *9* und den Bindestrich ( *-* ) verwenden.

> [!IMPORTANT]
> Eine Änderung des Standortcodes oder des Standortnamens nach der Installation des Standorts wird nicht unterstützt.

### <a name="reuse-a-site-code"></a>Wiederverwenden eines Standortcodes
Standortcodes können nur einmal in einer Configuration Manager-Hierarchie für einen zentralen Verwaltungsstandort oder einen primären Standort verwendet werden, auch wenn der ursprüngliche Standort und Standortcode deinstalliert wurden. Wenn Sie einen bereits vorhandenen Standortcode verwenden, besteht die Gefahr, dass es in Ihrer Hierarchie zu Konflikten zwischen Objekt-IDs kommt. Sie können den Standortcode für einen sekundären Standort wiederverwenden, wenn diese in Ihrer Configuration Manager-Hierarchie oder in der Active Directory-Gesamtstruktur nicht mehr verwendet werden.

## <a name="limits-and-restrictions-for-installed-sites"></a>Limits und Einschränkungen für installierte Standorte
Beachten Sie vor der Installation eines Standorts unbedingt die für Standorte und Standorthierarchien geltenden folgenden Einschränkungen:
- Nachdem Setup abgeschlossen ist, können Sie die folgenden Standorteigenschaften nicht ändern, ohne den Standort zu deinstallieren und anschließend mit den neuen Werten erneut zu installieren:  
  - Installationsverzeichnis für Programmdateien  
  - Standortcode  
  - Standortbeschreibung  
- Falls Ihre Hierarchie einen Standort der zentralen Verwaltung aufweist:  
  - Configuration Manager unterstützt nicht das Verschieben eines untergeordneten primären Standorts aus einer Hierarchie zum Erstellen eines eigenständigen primären Standorts oder zum Hinzufügen des Standorts zu einer anderen Hierarchie. Stattdessen müssen Sie den untergeordneten primären Standort deinstallieren und dann erneut als neuen eigenständigen primären Standort oder untergeordneten Standort des Standorts der zentralen Verwaltung von einer anderen Hierarchie installieren.  


## <a name="optional-steps-before-running-setup"></a><a name="bkmk_optionalsteps"></a> Optionale Schritte vor dem Ausführen des Setups
**Führen Sie das [Setup-Downloadprogramm](../../../../core/servers/deploy/install/setup-downloader.md) manuell aus**

Sie können das Setup-Downloadprogramm ausführen, um die aktualisierten Setupdateien für Configuration Manager herunterzuladen. Wenn der Computer, auf dem Sie Setup ausführen möchten, nicht mit dem Internet verbunden ist oder Sie die Installation mehrerer Standortserver erwarten, erwägen Sie den Einsatz des Setup-Downloadprogramms zum Herunterladen der erforderlichen Updates in Setup. Zusätzliche Informationen:
- Standardmäßig verbindet sich Setup mit dem Internet, um aktualisierte Setupdateien herunterzuladen.
- Standardmäßig werden die Dateien im Ordner „Redist“ gespeichert.
- Sie können Setup an einen Speicherort im Netzwerk verweisen, an dem Sie zuvor eine Kopie dieser Dateien gespeichert haben.

**Führen Sie die [Voraussetzungsprüfung](../../../../core/servers/deploy/install/prerequisite-checker.md)** manuell aus

Sie können die Voraussetzungsprüfung ausführen, um Probleme zu erkennen und zu beheben, bevor Sie mit dem Setup einen Standort und eine Standortsystemrolle auf einem Server installieren. Die Voraussetzungsprüfung trägt dazu bei, dass der Computer die Voraussetzungen zum Hosten des Standorts oder der Standortsystemrolle erfüllt. Zusätzliche Informationen:
- Setup führt die Voraussetzungsprüfung standardmäßig aus.
- Bei etwaigen Fehlern wird Setup angehalten, bis das Problem behoben ist.

**Bestimmen optionaler Ports**

Sie können optionale Ports bestimmen, die von Standortsystemen und Clients verwendet werden können. Zusätzliche Informationen:
- Standardmäßig verwenden Standortsysteme und Clients vordefinierte Ports zur Kommunikation.
- Während der Installation können Sie alternative Ports konfigurieren.

Weitere Informationen finden Sie unter [Verwendete Ports](../../../../core/plan-design/hierarchy/ports.md).
