---
title: Konfigurieren von Klassifizierungen und Produkten
titleSuffix: Configuration Manager
description: Führen Sie diese Schritte zum Konfigurieren von Softwareupdateklassifizierungen und Produkten in der Configuration Manager-Konsole durch.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 05/13/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 5ddde4e6-d553-4182-b752-6bc8b4a26745
ms.openlocfilehash: 7dc3ef2ceb22f1c15c96127c593965ea31bdd7eb
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88696819"
---
# <a name="configure-classifications-and-products-to-synchronize"></a>Konfigurieren der zu synchronisierenden Klassifizierungen und Produkte  

*Gilt für: Configuration Manager (Current Branch)*

Die Metadaten von Softwareupdates werden während des Synchronisierungsprozesses in Configuration Manager abgerufen. Diese basieren auf den Einstellungen, die Sie in den Komponenteneigenschaften des Softwareupdatepunkts angeben. Nachdem Sie Softwareupdates zum ersten Mal synchronisiert haben oder neue Produkte und Klassifikationen freigegeben werden, müssen Sie in den Eigenschaften die neuen Elemente auswählen. Gehen Sie wie folgt vor, um die zu synchronisierenden Klassifizierungen und Produkte zu konfigurieren.  

> [!NOTE]  
> Führen Sie das in diesem Abschnitt beschriebene Verfahren nur am Standort der obersten Ebene aus.  

## <a name="to-configure-classifications-and-products-to-synchronize"></a>So konfigurieren Sie die zu synchronisierenden Klassifizierungen und Produkte  

1. Wechseln Sie in der **Configuration Manager**-Konsole zu **Verwaltung** > **Standortkonfiguration** > **Standorte**.

2. Wählen Sie entweder den Standort der zentralen Verwaltung oder den eigenständigen primären Standort aus.  

3. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** auf **Standortkomponenten konfigurieren**, und klicken Sie dann auf **Softwareupdatepunkt**.

4. Geben Sie auf der Registerkarte **Klassifizierungen** die Softwareupdateklassifizierungen an, für die Sie Softwareupdates synchronisieren möchten.  

    Jedes Softwareupdate ist mit einer Updateklassifizierung definiert, die bei der Einteilung in verschiedene Updatearten behilflich ist. Bei der Synchronisierung werden die Metadaten für Softwareupdates für die angegebenen Klassifizierungen synchronisiert. Configuration Manager kann Softwareupdates mit folgenden Updateklassifizierungen synchronisieren:  

     - **Wichtige Updates:** Gibt eine im großen Umfang freigegebene Behebung für ein bestimmtes Problem an, mit dem ein wichtiger, nicht sicherheitsrelevanter Fehler behoben wird.  
     - **Definitionsupdates:** Gibt ein im großen Umfang freigegebenes Softwareupdate an, das Zusätze zur Definitionsdatenbank eines Produkts hinzufügt.  
     - **Feature Packs:** Hierbei handelt es sich um neue Produktfunktionen, die zunächst außerhalb einer Produktversion verteilt werden und in der Regel in der nächsten vollständigen Produktversion enthalten sind.  
     - **Sicherheitsupdates**: Gibt eine im großen Umfang freigegebene Behebung für ein produktspezifisches, sicherheitsrelevantes Sicherheitsrisiko an.  
     - **Service Packs:** Gibt eine getestete, kumulative Menge aller Hotfixes, Sicherheitsupdates, wichtiger Updates und Updates an, die auf ein Produkt angewendet werden. Zusätzlich können Service Packs zusätzliche Behebungen für Probleme enthalten, die intern nach dem Release des Produkts gefunden wurden.  
     - **Tools:** Gibt ein Dienstprogramm oder Feature an, das bei der Durchführung einer oder mehrerer Aufgaben hilft.  
     - **Updaterollups:** Gibt eine getestete, kumulative Menge aller Hotfixes, Sicherheitsupdates, kritischer Updates und Updates an, die zur Erleichterung der Bereitstellung zusammengefasst sind. Ein Updaterollup betrifft in der Regel einen bestimmten Bereich, z.B. Sicherheit oder eine Produktkomponente.  
     - **Updates:** Gibt eine im großen Rahmen freigegebene Behebung für ein bestimmtes Problem an. Ein Update betrifft einen nicht schwerwiegenden, nicht sicherheitsrelevanten Fehler.  
     - **Upgrade:** Hierbei handelt es sich um ein Upgrade für Windows 10-Features und -Funktionalität. Ihre Softwareupdatepunkte und Standorte müssen mindestens WSUS 6.2 mit dem [Hotfix 3095113](https://support.microsoft.com/kb/3095113) ausführen, um die Klassifizierung **Upgrade** zu erhalten. Weitere Informationen zum Installieren dieses Updates sowie zu anderen Updates für **Aktualisierungen** finden Sie unter [Voraussetzungen für Softwareupdates in Configuration Manager – Welche Updates sind in WSUS 6.2 und 6.3 erforderlich?](../plan-design/prerequisites-for-software-updates.md#BKMK_wsus2012).
    
    > [!NOTE]
    > Sie können das Kontrollkästchen **Microsoft Surface-Treiber und Firmwareupdates einbeziehen** aktivieren, um Microsoft Surface-Treiber zu synchronisieren.<!--1098490--> Voraussetzung hierfür ist die Installation von mindestens Windows Server 2016 auf allen Softwareupdatepunkten. Wenn Sie einen Softwareupdatepunkt auf einem Computer mit Windows Server 2012 aktivieren, nachdem Sie Surface-Treiber aktiviert haben, sind die Suchergebnisse für die Treiberupdates ungenau. Dies führt zu fehlerhaften Konformitätsdaten, die in der Configuration Manager-Konsole und in Configuration Manager-Berichten angezeigt werden. Weitere Informationen finden Sie unter [Verwalten von Surface-Treibern mit Configuration Manager](../deploy-use/surface-drivers.md).

5. Geben Sie auf der Seite **Produkte** die Produkte an, für die Sie Softwareupdates synchronisieren möchten. Klicken Sie dann auf **Schließen**.  

    - Configuration Manager speichert eine Liste der Produkte und Produktfamilien, aus denen Sie bei der Erstinstallation des Softwareupdatepunkts auswählen können. Produkte und Produktfamilien, die nach der Veröffentlichung von Configuration Manager freigegeben werden, können möglicherweise erst ausgewählt werden, nachdem Sie die Softwareupdatesynchronisierung abgeschlossen haben. Dabei wird die Liste der verfügbaren Produkte und Produktfamilien, aus denen Sie auswählen können, aktualisiert.  

    - Die Produkte, für die ein Update gilt, werden anhand der Metadaten für die einzelnen Softwareupdates definiert. Ein Produkt ist eine bestimmte Edition eines Betriebssystems oder einer Anwendung, z. B. Microsoft Windows Server 2012. Eine Produktfamilie ist das Basisbetriebssystem bzw. die Basisanwendung, von dem bzw. der die einzelnen Produkte abgeleitet sind. Ein Beispiel für eine Produktfamilie ist Windows. Windows Server 2012 ist ein Mitglied dieser Produktfamilie. Sie können eine Produktfamilie oder einzelne Produkte innerhalb einer Produktfamilie angeben. Je mehr Produkte Sie auswählen, desto länger dauert die Synchronisierung von Softwareupdates.  

    - Wenn Softwareupdates auf mehrere Produkte anwendbar sind und mindestens eines der Produkte für die Synchronisierung ausgewählt wurde, werden sämtliche Produkte in der Configuration Manager-Konsole angezeigt, auch wenn einige Produkte nicht ausgewählt wurden. Wenn z. B. Windows Server 2012 das einzige Betriebssystem ist, das Sie ausgewählt haben, und ein Softwareupdate auf Windows 8 und auf Windows Server 2012 anwendbar ist, werden beide Produkte in der Configuration Manager-Konsole angezeigt.  

    > [!NOTE]  
    > **Windows 10, Version 1903 und höher** wurde Microsoft Update als eigenes Produkt hinzugefügt, anstatt wie frühere Versionen Teil des Produkts **Windows 10** zu sein. Aufgrund dieser Änderung mussten Sie eine Reihe von manuellen Schritten ausführen, um sicherzustellen, dass Ihre Clients diese Updates sehen. Nun wurde die Anzahl der manuellen Schritte, die Sie für das neue Produkt in Configuration Manager, Version 1906 ausführen müssen, erfolgreich verringert. <!--4682946-->
    >
    > Wenn Sie ein Update auf Configuration Manager, Version 1906 ausführen und das Produkt **Windows 10** für die Synchronisierung ausgewählt haben, werden die folgenden Aktionen automatisch ausgeführt:
    > - Das Produkt **Windows 10, Version 1903 und höher** wird für die Synchronisierung hinzugefügt.
    > - [Automatische Bereitstellungsregeln](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process), die das Produkt **Windows 10** enthalten, werden aktualisiert, sodass sie **Windows 10, Version 1903 und höher** enthalten.
    > - [Wartungspläne](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow) werden aktualisiert, sodass sie das Produkt **Windows 10, Version 1903 und höher** enthalten.


## <a name="configuring-products-for-versions-of-windows-10"></a>Konfigurieren von Produkten für Windows 10-Versionen

### <a name="windows-10-version-1909"></a>Windows 10, Version 1909

Windows 10, Version 1909 verfügt über dasselbe zugrunde liegende Betriebssystem wie Windows 10, Version 1903. Beide Versionen erhalten dieselben kumulativen Updates. Weitere Informationen zu Windows 10, Version 1909 finden Sie im Blogbeitrag [Auslieferungsoptionen für Windows 10, Version 1909](https://aka.ms/1909mechanics).

Damit sichergestellt ist, dass die Windows 10-Versionen 1909 und 1903 Updates über Configuration Manager installieren:

- Genehmigen Sie Updates für die Windows 10-Versionen 1909 und 1903.
  - Die Updates verfügen je nach Betriebssystemversion über unterschiedliche Namen und Anwendbarkeitsregeln.
  - Wenn Sie jedes Update versionsweise und pro Betriebssystemarchitektur genehmigen, wird der normale Genehmigungsprozess für Administratoren aufrechterhalten.
- Müssen die Installationsdateien für die kumulativen Updates für die Windows 10-Versionen 1909 und 1903 identisch sein.
  - Configuration Manager lädt die Updatequelldateien nur einmal herunter.

#### <a name="feature-updates-for-windows-10-version-1909"></a>Funktionsupdates für Windows 10, Version 1909

Wenn Sie Funktionsupdates für Windows 10, Version 1909 genehmigen, stehen Ihnen verschiedene Optionen zur Auswahl:

- Windows 10-Clients mit Version 1903 wird ein [Enablement Package](https://support.microsoft.com/en-us/help/4517245/feature-update-via-windows-10-version-1909-enablement-package) angeboten, das am 12. November 2019 veröffentlicht wurde.
  - Das Enablement Package ist eine kleine, schnell installierbare Datei, die die Features von Windows 10, Version 1909 aktiviert und das Gerät neu startet.
  - Die Voraussetzungen für das Enablement Package sind:
    - Ein minimal kumulatives Update von [KB4517389](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4517389), veröffentlicht am 8. Oktober 2019
    - Ein minimales Update des Wartungsstapels von [KB4520390](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4520390), veröffentlicht am 24. September 2019
  - Dieses Update ist wie jedes andere Funktionsupdate nicht für den Import aus `https:\\catalog.update.microsoft.com` verfügbar.
  - Das Update wird automatisch mit Windows Server Update Services (WSUS) synchronisiert, wenn Sie über das Produkt **Windows 10, Version 1903 und höher** verfügen und die Klassifizierung **Aktualisierungen** ausgewählt haben.
  - Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie **Windows 10-Wartung**, und wählen Sie dann den Knoten **Alle Windows 10-Updates** aus. Suchen Sie nach den Suchbegriffen „Enablement“ oder „4517245“.

    > [!TIP]
    > Da es sich hierbei um Funktionsupdates handelt, sind sie nicht im Knoten **Alle Softwareupdates** verfügbar.

- Windows 10-Clients mit Version 1809 und früher werden mit einem einzelnen direkten Funktionsupdate aktualisiert.
  - Dies entspricht allen anderen früheren Installationen für Funktionsupdates, die Sie für Windows 10 durchgeführt haben.

> [!NOTE]
> Sowohl das Enablement Package als auch das herkömmliche Funktionsupdate für Windows 10, Version 1909 werden bei der Berichterstellung als „Installiert“ angezeigt, unabhängig davon, welcher Pfad zur Installation verwendet wurde.

### <a name="windows-10-version-1903-and-later"></a>Windows 10, Version 1903 und höher

**Windows 10, Version 1903 und höher** wurde Microsoft Update als eigenes Produkt hinzugefügt, anstatt wie frühere Versionen Teil des Produkts **Windows 10** zu sein. Aufgrund dieser Änderung mussten Sie eine Reihe von manuellen Schritten ausführen, um sicherzustellen, dass Ihre Clients diese Updates sehen. Nun wurde die Anzahl der manuellen Schritte, die Sie für das neue Produkt in Configuration Manager, Version 1906 ausführen müssen, erfolgreich verringert. <!--4682946-->

#### <a name="windows-10-version-1903-and-later-with-configuration-manager-version-1906"></a>Windows 10, Version 1903 und höher mit Configuration Manager, Version 1906
Wenn Sie ein Update auf Configuration Manager, Version 1906 ausführen und das Produkt **Windows 10** für die Synchronisierung ausgewählt haben, werden die folgenden Aktionen automatisch ausgeführt:
- Das Produkt **Windows 10, Version 1903 und höher** wird für die Synchronisierung hinzugefügt.
- [Automatische Bereitstellungsregeln](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process), die das Produkt **Windows 10** enthalten, werden aktualisiert, sodass sie **Windows 10, Version 1903 und höher** enthalten.
- [Wartungspläne](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow) werden aktualisiert, sodass sie das Produkt **Windows 10, Version 1903 und höher** enthalten.

#### <a name="windows-10-version-1903-and-later-with-configuration-manager-version-1902"></a>Windows 10, Version 1903 und höher mit Configuration Manager, Version 1902
Wenn Sie Configuration Manager 1902 mit Windows 10-Clients mit Version 1903 verwenden:
- Wählen Sie das Produkt **Windows 10, Version 1903 und höher** für die Synchronisierung aus.
- Aktualisieren Sie alle [automatischen Bereitstellungsregeln](../deploy-use/automatically-deploy-software-updates.md#bkmk_adr-process) für Windows 10-Clients mit Version 1903.
- Aktualisieren Sie die [Wartungspläne](../../osd/deploy-use/manage-windows-as-a-service.md#servicing-plan-workflow) für Windows 10-Clients mit Version 1903.

## <a name="windows-insider-program"></a><a name="bkmk_WIfB"></a> Windows-Insider-Programm
<!--3556023-->
Ab September 2019 können Sie Geräte mit Configuration Manager warten und aktualisieren, auf denen Windows Insider Preview-Builds ausgeführt werden. Diese Änderung bedeutet, dass Sie diese Geräte verwalten können, ohne Ihre regulären Prozesse zu ändern oder Windows Update for Business zu aktivieren. Sie können Feature- und kumulative Updates für Windows Insider Preview-Builds in Configuration Manager genau wie jedes andere Windows 10-Update oder -Upgrade herunterladen. Weitere Informationen finden Sie im Blogbeitrag [Veröffentlichen der Vorabversion von Windows 10-Funktionsupdates für WSUS](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/Publishing-pre-release-Windows-10-feature-updates-to-WSUS/ba-p/845054).

Weitere Informationen zur Unterstützung für Windows-Insider in Configuration Manager finden Sie unter [Unterstützung für Windows-Insider](../../core/plan-design/configs/support-for-windows-10.md#bkmk_WIfB-support).

### <a name="prerequisites"></a>Voraussetzungen

- Configuration Manager, Version 1906 oder höher, die für die [Verwaltung von Softwareupdates](../plan-design/plan-for-software-updates.md) konfiguriert ist
- Windows 10-Geräte, auf denen der [Windows Insider Preview-Build](/windows-insider/at-work-pro/wip-4-biz-get-started) ausgeführt wird
- Eine Sammlung, die die Windows-Insider-Geräte enthält

### <a name="enable-windows-insider-upgrades-and-updates"></a>Aktivieren der Windows-Insider-Upgrades und -Updates

Sie müssen die Produkte und Klassifizierungen für Windows-Insider-Upgrades und -Updates aktivieren. Funktionsupdates, kumulative Updates und andere Updates für Windows-Insider befinden sich in der Produktkategorie **Windows Insider Pre-Release** (Windows-Insider-Vorabversion).

1. Wechseln Sie in der **Configuration Manager**-Konsole zu **Verwaltung** > **Standortkonfiguration** > **Standorte**.
2. Wählen Sie entweder den Standort der zentralen Verwaltung oder den eigenständigen primären Standort aus.  
3. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** auf **Standortkomponenten konfigurieren**, und klicken Sie dann auf **Softwareupdatepunkt**.
4. Vergewissern Sie sich, dass auf der Registerkarte **Produkte** die folgenden Produkte für die Synchronisierung ausgewählt sind:
    - Windows-Insider-Vorabversion
    - Windows 10, Version 1903 und höher
5. Stellen Sie auf der Registerkarte **Klassifizierungen** sicher, dass die folgenden Klassifizierungen für die Synchronisierung ausgewählt sind:
    - Upgrades
    - Sicherheitsupdates
    - Updates (optional)
6. Klicken Sie auf **OK**, um die **Eigenschaften der Softwareupdatepunkt-Komponente** zu schließen.

### <a name="upgrading-windows-insider-devices"></a>Upgraden von Windows-Insider-Geräten

Nachdem die Upgrades für Windows-Insider synchronisiert wurden, werden sie unter **Softwarebibliothek** > **Windows 10-Wartung** > **Alle Windows 10-Updates** angezeigt.

![Windows-Insider-Funktionsupdates für die Windows 10-Wartung](media/3556023-windows-insiders-pre-release-feature-update.png)

Stellen Sie für Ihre Zielsammlung Funktionsupdates für Windows-Insider so bereit, wie Sie auch jedes andere Upgrade bereitstellen würden. Sie sollten dabei jedoch die folgenden Punkte berücksichtigen:

- Diese Upgrades gelten für alle Windows 10-Clients mit Version 1903 oder früher und der entsprechenden Architektur, Edition und Sprache.
- Es gibt Lizenzbedingungen, die akzeptiert werden müssen, damit Ihre Bereitstellung installiert werden kann.
- Möglicherweise sollten Sie die [Threadpriorität in den Clienteinstellungen](../../core/clients/deploy/about-client-settings.md#bkmk_thread-priority) verwenden.
- Beim dynamischen Update werden wichtige Updates, einschließlich des aktuellen kumulativen Updates, direkt aus Microsoft Update installiert. Dieses Verhalten begann mit den Funktionsupdates für Windows 10, Version 1903. 
  - Sie können das dynamische Update [in den Clienteinstellungen](../../core/clients/deploy/about-client-settings.md#bkmk_du) oder mit der [Datei „setupconfig.ini“](/windows-hardware/manufacture/desktop/windows-setup-command-line-options) explizit deaktivieren. 
  - Weitere Informationen finden Sie im Blogbeitrag [Vorteile des dynamischen Updates für Windows 10](https://techcommunity.microsoft.com/t5/Windows-IT-Pro-Blog/The-benefits-of-Windows-10-Dynamic-Update/ba-p/467847).

Weitere Informationen zum Bereitstellen von Upgrades finden Sie unter [Verwalten von Windows-as-a-Service mit Configuration Manager](../../osd/deploy-use/manage-windows-as-a-service.md).


### <a name="keeping-insider-devices-up-to-date"></a>Auf-dem-neuesten-Stand-Halten von Insider-Geräten

Kumulative Updates für Windows-Insider sind für WSUS und damit auch für Configuration Manager verfügbar. Diese kumulativen Updates werden in einer ähnlichen Häufigkeit wie die kumulativen Updates für Windows 10, Version 1903 freigegeben. Die kumulativen Windows-Insider-Updates befinden sich in der Produktkategorie **Windows Insider Pre-Release** (Windows-Insider-Vorabversion) und sind entweder als **Sicherheitsupdates** oder **Updates** klassifiziert. Sie können die kumulativen Updates für Windows-Insider mithilfe ihres regulären Softwareupdateprozesses bereitstellen, z. B. über [automatische Bereitstellungsregeln](../deploy-use/automatically-deploy-software-updates.md) oder [graduelle Bereitstellungen](../../osd/deploy-use/create-phased-deployment-for-task-sequence.md?toc=/mem/configmgr/sum/toc.json&bc=/mem/configmgr/sum/breadcrumb/toc.json).

## <a name="extended-security-updates-and-configuration-manager"></a><a name="bkmk_ESU"></a> Erweiterte Sicherheitsupdates und Configuration Manager

Das Programm [Extended Security Updates (ESU)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) ist ein letzter Ausweg für Kunden, die bestimmte ältere Microsoft-Produkte über das Supportende hinaus ausführen müssen. Es umfasst kritische und/oder wichtige Sicherheitsupdates (wie durch das [Microsoft Security Response Center](https://www.microsoft.com/msrc) definiert), die für maximal drei Jahre nach dem Ende des erweiterten Supports für das Produkt bereitgehalten werden.

Produkte, deren Supportlebenszyklus abgelaufen ist, werden nicht mehr für die Verwendung mit Configuration Manager unterstützt. Hierzu gehören alle Produkte im ESU-Programm. Beispiel: Windows 7. Sicherheitsupdates, die im Rahmen des ESU-Programms zur Verfügung gestellt werden, werden in den Windows Server Update Services (WSUS) veröffentlicht. Diese Updates werden in der Configuration Manager-Konsole angezeigt. Während Produkte, die durch das ESU-Programm abgedeckt sind, nicht mehr für die Verwendung mit Configuration Manager unterstützt werden, kann die [letzte veröffentlichte Version des aktuellen Configuration Manager-Branchs](../../core/servers/manage/updates.md#version-details) zum Bereitstellen und Installieren von im Rahmen des Programms veröffentlichten Windows-Sicherheitsupdates verwendet werden. Mit der neuesten veröffentlichten Version kann auch Windows 10 auf Geräten mit Windows 7 bereitgestellt werden.

Clientverwaltungsfeatures, die nicht im Zusammenhang mit der Verwaltung von Windows-Softwareupdates oder der Betriebssystembereitstellung stehen, werden unter Betriebssystemen, die durch das ESU-Programm abgedeckt werden, nicht mehr getestet, und wir garantieren nicht, dass diese weiterhin funktionsfähig sind. Es wird dringend empfohlen, so schnell wie möglich ein Upgrade oder eine Migration zu einer aktuellen Version der Betriebssysteme durchzuführen, um Unterstützung für die Clientverwaltung zu erhalten.


## <a name="next-steps"></a>Nächste Schritte

Starten Sie die Synchronisierung von Softwareupdates, um Softwareupdates auf der Grundlage der neuen Kriterien abzurufen. Weitere Informationen finden Sie unter [Synchronisieren von Softwareupdates](synchronize-software-updates.md).