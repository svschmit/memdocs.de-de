---
title: Verwalten von Updates für den Surface-Treiber
titleSuffix: Configuration Manager
description: Configuration Manager synchronisiert Surface-Treiberupdates für die Bereitstellung auf Surface-Geräten.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 06/18/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: e9f9f4e6-5b4f-4b8f-94d6-db9b2b239113
ms.openlocfilehash: f276db618a2e67832ffa5575622e00eea02c7422
ms.sourcegitcommit: 8a4a86ee8044f273dcece26155132a801f3d8f9a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/30/2020
ms.locfileid: "87438630"
---
# <a name="manage-surface-drivers-with-configuration-manager"></a>Verwalten von Surface-Treibern mit Configuration Manager

*Gilt für: System Center Configuration Manager (Current Branch)*

Mit System Center Configuration Manager können Sie Treiber für Surface-Geräte synchronisieren und wie ein Softwareupdate bereitstellen. Mit dieser Funktion können Sie sicherstellen, dass auf Ihren Surface-Geräten die neuesten verfügbaren Treiber ausgeführt werden. Diese Synchronisierung wurde erstmals in Version 1706 als Vorabversionsfeature eingeführt und wurde in 1710 zu einem Feature. <!--3684621, 3608197, 1098490-->

## <a name="prerequisites-for-synchronizing-surface-drivers"></a>Voraussetzungen für die Synchronisierung von Surface-Treibern

- Ein mit dem Internet verbundener Softwareupdatepunkt auf oberster Ebene.
- Auf allen Softwareupdatepunkten muss Windows Server 2016 mit dem kumulativen Update KB4025339 oder höher installiert werden.
- Configuration Manager aktiviert dieses optionale Feature nicht automatisch. Aktivieren Sie diese Funktion, bevor Sie sie verwenden. Weitere Informationen finden Sie unter [Enable optional features from updates (Aktivieren optionaler Features von Updates)](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

## <a name="enable-sync-for-surface-drivers"></a>Aktivieren der Synchronisierung für Surface-Treiber

Gehen Sie folgendermaßen vor, um die Synchronisierung von Surface-Treibern zu aktivieren:

1. Verbinden Sie die Configuration Manager-Konsole mit dem Standortserver der obersten Ebene.
1. Wechseln Sie zu **Verwaltung** > **Standortkonfiguration** > **Standorte**, und klicken Sie dann auf den Standort der obersten Ebene.
1. Wählen Sie im Menüband **Einstellungen** > **Standortkomponenten konfigurieren** > **Softwareupdatepunkt** aus.
1. Klicken Sie auf die Registerkarte **Klassifizierungen**, dann auf das Kontrollkästchen **Microsoft Surface-Treiber und Firmwareupdates einbeziehen** und dann auf **Anwenden**.

     ![Aktivieren von Surface-Treibern in den Eigenschaften des Softwareupdatepunkts](media/enable-surface-driver-sync.png)

1. Klicken Sie in den „Eigenschaften der Softwareupdatepunkt-Komponente“ auf **Produkte**. Weitere Informationen finden Sie in den Abschnitten [Produkte für Surface-Treiber](#bkmk_prod) und [Surface-Modelle](#bkmk_models).
1. Wählen Sie die Produkte für jede Windows 10-Version aus, für die Sie Surface-Treiber unterstützen möchten. Sie werden feststellen, dass es zwei unterschiedliche Versionen der einzelnen Produkte für Treiber gibt:

   - Windows 10-*Versions*-**Update und höher – Wartungstreiber**
   - Windows 10-*Versions*-**Update und höher – Upgrade- und Wartungstreiber**.

     ![Produktliste der Treiber für Windows 10-Versionen](media/surface-driver-products-sup.png)

1. Wenn Sie die Produkte ausgewählt haben, klicken Sie auf **OK**.
1. [Synchronisieren Sie Ihren Softwareupdatepunkt](../get-started/synchronize-software-updates.md), um die Surface-Treiber in Configuration Manager einzubringen.
1. Sobald die Surface-Treiber synchronisiert sind, stellen Sie sie auf die gleiche Weise bereit wie andere Updates.

## <a name="products-for-surface-drivers"></a><a name="bkmk_prod"></a> Produkte für Surface-Treiber

Die meisten Treiber gehören zu den folgenden Produktgruppen:

- Treiber für Windows 10 und spätere Versionen
- Windows 10 und höher – Upgrade- und Wartungstreiber
- Windows 10 Anniversary Update und höher – Wartungstreiber
- Windows 10 Anniversary Update und höher – Upgrade- und Wartungstreiber
- Windows 10 Creators Update und höher – Wartungstreiber
- Windows 10 Creators Update und höher – Upgrade- und Wartungstreiber
- Windows 10 Fall Creators Update und höher – Wartungstreiber
- Windows 10 Fall Creators Update und höher – Upgrade- und Wartungstreiber
- Windows 10 S und höher – Wartungstreiber
- Windows 10 S Version 1709 und höher – Wartungstreiber für Tests
- Windows 10 S Version 1709 und höher – Upgrade- und Wartungstreiber für Tests
- Windows 10 S Version 1803 und höher – Wartungstreiber
- Windows 10 S Version 1803 und höher – Upgrade- und Wartungstreiber
- Windows 10 S Version 1809 und höher – Wartungstreiber
- Windows 10 S Version 1809 und höher – Upgrade- und Wartungstreiber
- Windows 10 S Version 1903 und höher – Wartungstreiber
- Windows 10 S Version 1903 und höher – Upgrade- und Wartungstreiber
- Windows 10 S Version 1803 und höher – Wartungstreiber
- Windows 10 S Version 1803 und höher – Upgrade- und Wartungstreiber
- Windows 10 S Version 1809 und höher – Wartungstreiber
- Windows 10 S Version 1809 und höher – Upgrade- und Wartungstreiber
- Windows 10 S Version 1903 und höher – Wartungstreiber
- Windows 10 S Version 1903 und höher – Upgrade- und Wartungstreiber

> [!NOTE]
> Die meisten Surface-Treiber gehören mehreren Windows 10-Produktgruppen an. Sie müssen möglicherweise nicht alle Produkte auswählen, die hier aufgeführt sind. Um die Anzahl der Produkte zu reduzieren, die ihren Updatekatalog füllen, sollten Sie nur die Produkte auszuwählen, die Ihre Umgebung für die Synchronisierung benötigt.

## <a name="surface-models"></a><a name="bkmk_models"></a> Surface-Modelle

Die folgende Tabelle enthält die Surface-Modelle und Windows 10-Versionen, auf denen Configuration Manager Treiber installieren kann. Surface-Treiberupdates sind im Configuration Manager nicht an demselben Tag verfügbar, an dem sie im Updatekatalog von Microsoft veröffentlicht werden. Configuration Manager verwaltet eine eigene Liste der Surface-Treiber, die importiert werden. Geräte, die Windows 10 S-Produkte benötigen, werden vermerkt. Microsoft strebt an, die Surface-Treiber, die am zweiten Dienstag jedes Monats der Zulassungsliste hinzugefügt werden, für die Synchronisierung mit Configuration Manager verfügbar zu machen. Weitere Informationen finden Sie unter [Häufig gestellte Fragen](#bkmk_faq).

</br>

|Surface-Modell|Windows 10 1709| Windows 10 1803|Windows 10 1809|Windows 10 1903|Windows 10 1909|
|----|----|----|----|----|----|
|Surface Pro 3|Ja| Ja| Ja |Ja|Ja|
|Surface Pro 4|Ja| Ja| Ja |Ja|Ja|
|Surface Pro 6|N/V| Ja| Ja |Ja|Ja|
|Surface Pro 7|N/V| N/V| N/V |Ja|Ja|
|Surface Pro X|N/V| N/V| N/V |Ja|Ja|
|Surface Book|Ja| Ja| Ja |Ja|Ja|
|Surface Book 2|Ja| Ja| Ja |Ja|Ja|
|Surface Book 3|N/V| N/V| N/V |Ja|Ja|
|Surface Laptop|Ja, mit Auswahl des Produkts „Windows 10 S Version 1709 und höher – Wartungstreiber“| Ja, mit Auswahl des Produkts „Windows 10 S Version 1803 und höher – Wartungstreiber“|Ja, mit Auswahl des Produkts „Windows 10 S Version 1809 und höher – Upgrade- und Wartungstreiber“|Ja, mit Auswahl des Produkts „Windows 10 S Version 1903 und höher – Upgrade- und Wartungstreiber“|Ja, mit Auswahl des Produkts „Windows 10 S Version 1903 und höher – Upgrade- und Wartungstreiber“|
|Surface Laptop 2|N/V| Ja |Ja|Ja|Ja|
|Surface Laptop 3|N/V| N/V|N/V|Ja |Ja|
|Surface Go|N/V| Ja, mit Auswahl des Produkts „Windows 10 S Version 1803 und höher – Wartungstreiber“|Ja, mit Auswahl des Produkts „Windows 10 S Version 1809 und höher – Upgrade- und Wartungstreiber“|Ja, mit Auswahl des Produkts „Windows 10 S Version 1903 und höher – Upgrade- und Wartungstreiber“|Ja, mit Auswahl des Produkts „Windows 10 S Version 1903 und höher – Upgrade- und Wartungstreiber“|
|Surface Go 2|N/V| N/V| Ja |Ja|Ja, mit Auswahl des Produkts „Windows 10 S Version 1903 und höher – Upgrade- und Wartungstreiber“|
|Surface Studio|Ja| Ja| Ja |Ja|Ja|
|Surface Studio 2|N/V| Ja| Ja |Ja|Ja|

## <a name="verify-the-configuration"></a>Überprüfen der Konfiguration

Um zu überprüfen, ob der Softwareupdatepunkt ordnungsgemäß konfiguriert ist, verwenden Sie **WsyncMgr.log** und **WCM.log**.

1. Öffnen Sie die Datei „WsyncMgr.log“, und überprüfen Sie den folgenden Protokolleintrag:

    ```text
    Surface Drivers can be supported in this hierarchy since all software update points are on Windows Server 2016, WCM SCF property Sync Catalog Drivers is set. 
    …
    Sync Catalog Drivers SCF value is set to : 1
    ```

1. Wenn einer der folgenden Einträge in **WsyncMgr.log** protokolliert wird, überprüfen Sie, ob Sie die Option **Microsoft Surface-Treiber und Firmwareupdates einbeziehen** in den Eigenschaften des Softwareupdatepunkts ausgewählt haben:
   - `Sync Surface Drivers option is not set`
   - `Sync Catalog Drivers SCF value is set to : 0`

1. Öffnen Sie **WCM.log**, und suchen Sie nach Elementen, die den folgenden Einträgen ähneln:
   ```text
   <Categories>
   <Category Id="Product:05eebf61-148b-43cf-80da-1c99ab0b8699"><![CDATA[Windows 10 and later drivers]]></Category>
   <Category Id="Product:06da2f0c-7937-4e28-b46c-a37317eade73"><![CDATA[Windows 10 Creators Update and Later Upgrade & Servicing Drivers]]></Category>
   <Category Id="Product:c1006636-eab4-4b0b-b1b0-d50282c0377e"><![CDATA[Windows 10 S and Later Servicing Drivers]]></Category>
   … …
   </Categories>
   ```

   Dieser Eintrag ist ein XML-Element, das alle Produktgruppen und Klassifizierungen auflistet, die derzeit von Ihrem Softwareupdatepunkt-Server synchronisiert werden. Wenn Sie die Produkte, die Sie ausgewählt haben, nicht finden können, überprüfen Sie, ob die Produkte für den Softwareupdatepunkt gespeichert wurden.
1. Sie können auch warten, bis die nächste Synchronisierung abgeschlossen ist. Überprüfen Sie dann, ob die Surface-Treiber- und Firmwareupdates in der Configuration Manager-Konsole unter Software Updates aufgeführt sind. Beispielsweise werden in der Konsole möglicherweise folgende Informationen angezeigt: ![Synchronisierte Surface-Treiber in der Configuration Manager-Konsole](media/synchronized-surface-drivers.png)

##  <a name="frequently-asked-questions-faq"></a><a name="bkmk_faq"></a> Häufig gestellte Fragen (FAQ)

### <a name="after-i-follow-the-steps-in-this-article-my-surface-drivers-are-still-not-synchronized-why"></a>Nachdem ich die Schritte in diesem Artikel befolgt habe, werden die Surface-Treiber immer noch nicht synchronisiert. Warum?

Wenn Sie eine Synchronisierung von einem Upstream-WSUS-Server (Windows Server Update Services) statt Microsoft Update ausführen, stellen Sie sicher, dass der Upstream-WSUS-Server für die Unterstützung und Synchronisierung von Surface-Treiberupdates konfiguriert ist. Alle Downstreamserver sind auf Updates beschränkt, die in der Upstream-WSUS-Serverdatenbank vorhanden sind.

Es gibt mehr als 68.000 Updates, die in WSUS als Treiber klassifiziert werden. Um zu verhindern, dass Nicht-Surface-Treiber mit Configuration Manager synchronisiert werden, filtert Microsoft die Treibersynchronisierung anhand einer Zulassungsliste. Sobald die neue Zulassungsliste veröffentlicht und in Configuration Manager integriert ist, werden die neuen Treiber nach der nächsten Synchronisierung der Konsole hinzugefügt. Microsoft strebt an, die Surface-Treiber, die am zweiten Dienstag jedes Monats der Zulassungsliste hinzugefügt werden, für die Synchronisierung mit Configuration Manager verfügbar zu machen.

Wenn die Configuration Manager-Umgebung offline ist, wird jedes Mal eine neue Zulassungsliste importiert, wenn Sie [Wartungsupdates](../../core/servers/manage/use-the-service-connection-tool.md) in Configuration Manager importieren. Außerdem müssen Sie einen [neuen WSUS-Katalog](../get-started/synchronize-software-updates-disconnected.md) importieren, der die Treiber enthält, bevor die Updates in der Configuration Manager-Konsole angezeigt werden. Da eine eigenständige WSUS-Umgebung mehr Treiber als eine Configuration Manager-SUP enthält, empfiehlt es sich, eine Configuration Manager-Umgebung einzurichten, die über Onlinefunktionen verfügt, und die Sie für die Synchronisierung von Surface-Treibern konfigurieren. Dies bietet einen kleineren WSUS-Export, der der Offlineumgebung sehr ähnlich ist.

Wenn Ihre Configuration Manager-Umgebung online ist und neue Updates erkennen kann, erhalten Sie automatisch Updates der Liste. Wenn die erwarteten Treiber nicht angezeigt werden, überprüfen Sie die Dateien „WCM.log“ und „WsyncMgr.log“ auf Synchronisierungsfehler.

### <a name="my-configuration-manager-environment-is-offline-can-i-manually-import-surface-drivers-into-wsus"></a>Meine Configuration Manager-Umgebung ist offline. Kann ich Surface-Treiber manuell in WSUS importieren?

Nein. Auch wenn das Update in WSUS importiert wird, wird das Update nicht für die Bereitstellung in die Configuration Manager-Konsole importiert, wenn es nicht in der Zulassungsliste aufgeführt ist. Sie müssen das [Dienstverbindungstool](../../core/servers/manage/use-the-service-connection-tool.md) verwenden, um zur Aktualisierung der Zulassungsliste Wartungsupdates in Configuration Manager zu importieren.

### <a name="what-alternative-methods-do-i-have-to-deploy-surface-driver-and-firmware-updates"></a>Mit welchen alternativen Methoden kann ich Surface-Treiber und Firmwareupdates bereitstellen?

Informationen zum Bereitstellen von Surface-Treiber- und Firmwareupdates über alternative Kanäle finden Sie unter [Verwalten von Surface-Treiber- und Firmwareupdates](https://docs.microsoft.com/surface/manage-surface-driver-and-firmware-updates). Wenn Sie die MSI- oder EXE-Datei herunterladen und dann über herkömmliche Softwarebereitstellungskanäle bereitstellen möchten, finden Sie weitere Informationen unter [Surface-Firmware mit Configuration Manager auf dem neuesten Stand halten](https://docs.microsoft.com/archive/blogs/thejoncallahan/keeping-surface-firmware-updated-with-configuration-manager).

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen über Surface-Treiber finden Sie in den folgenden Artikeln:

- [Überlegungen zu Surface und System Center Configuration Manager](https://docs.microsoft.com/surface/considerations-for-surface-and-system-center-configuration-manager#deploy-surface-app-with-configuration-manager)
- [Surface – Updateverlauf](https://support.microsoft.com/help/4036283/surface-surface-update-history)
- [Herunterladen der neuesten Firmware und Treiber für Surface-Geräte](/surface/manage-surface-driver-and-firmware-updates)
