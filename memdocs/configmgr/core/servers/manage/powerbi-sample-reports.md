---
title: Installieren von Power BI-Beispielberichten
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie die Power BI-Beispielberichte in Configuration Manager installieren
ms.date: 06/25/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7e9bc22c-67ac-4a86-b613-944a4928e583
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 39bec7e8b01b35a8411400399a74eb352406c023
ms.sourcegitcommit: e2ef7231d3abaf3c925b0e5ee9f66156260e3c71
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/26/2020
ms.locfileid: "85383188"
---
# <a name="install-power-bi-sample-reports"></a>Installieren von Power BI-Beispielberichten
<!--5679791-->
*Gilt für: Configuration Manager (Current Branch)*

Sie können den [Power BI-Berichtsserver](https://docs.microsoft.com/power-bi/report-server/get-started) ab Version 2002 mit der Configuration Manager-Berichterstellung integrieren. Zum Herunterladen stehen Beispielberichte zur Verfügung, die Sie in Configuration Manager installieren können. In diesem Artikel wird beschrieben, wie Sie die Power BI-Beispielberichte in Configuration Manager installieren.

## <a name="prerequisites"></a>Voraussetzungen

- Configuration Manager-Reporting Services-Punkt in [Power BI-Berichtsserver integriert](powerbi-report-server.md)
- [Microsoft Power BI Desktop (optimiert für Power BI-Berichtsserver, Version vom September 2019)](https://www.microsoft.com/download/details.aspx?id=57271) oder höher

    > [!IMPORTANT]
    > - Verwenden Sie nur Power BI Desktop-Versionen aus dem [Microsoft Download Center](https://www.microsoft.com/download/), keine Versionen aus dem Microsoft Store.
    > - Verwenden Sie nur eine Version von [Power BI Desktop, die **für Power BI-Berichtsserver optimiert ist**](https://docs.microsoft.com/power-bi/report-server/install-powerbi-desktop).

## <a name="download-the-sample-reports"></a>Herunterladen der Beispielberichte

> [!IMPORTANT]
> Die Beispielberichte sind zurzeit nicht zum Download verfügbar. Sie wurden vorübergehend entfernt, um gemeldete Probleme zu beheben.

So laden Sie die Beispielberichte herunter:

1. Herunterladen von Power BI-Beispielberichten<!-- from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=101452)-->.
1. Speichern Sie die Datei `ConfigMgrSamplePowerBIReports.exe`. 
1. Verschieben Sie die Datei auf einen Computer, auf dem Microsoft Power BI Desktop (optimiert für Power BI-Berichtsserver) installiert ist, wenn Sie sie von einem anderen Gerät heruntergeladen haben.
1. Führen Sie die Datei `ConfigMgrSamplePowerBIReports.exe` aus, um die PBIT-Dateien zu extrahieren.

## <a name="install-the-sample-reports"></a>Installieren der Beispielberichte

So installieren Sie die Beispielberichte:

1. Erstellen Sie auf dem Power BI-Berichtsserver einen neuen Ordner mit dem Namen `Sample Reports` im Configuration Manager-Stammberichtsordner.
   
   :::image type="content" source="media/create-sample-reports-folder.png" alt-text="Erstellen des Beispielberichtsordners im Configuration Manager-Stammberichtsordner" lightbox="media/create-sample-reports-folder.png":::


1. Starten Sie Microsoft Power BI Desktop (optimiert für Power BI-Berichtsserver).
1. Wählen Sie **Datei** und dann **Öffnen** aus, und navigieren Sie zum Speicherort der extrahierten PBIT-Dateien.
1. Wählen Sie eine der PBIT-Dateien aus, die Sie aus der Datei `ConfigMgrSamplePowerBIReports.exe` extrahiert haben.
1. Geben Sie den Namen der Configuration Manager-Datenbank und den Namen des Datenbankservers an, wenn Sie dazu aufgefordert werden, und wählen Sie **Laden**.
   - Wenn Sie das Datenmodell laden oder anwenden, ignorieren Sie alle Fehlermeldungen, die Sie ggf. erhalten.
   
    :::image type="content" source="media/sample-report-database.png" alt-text="Angeben von Datenbank- und Datenbankserver-Name" lightbox="media/sample-report-database.png":::

1. Wenn die Berichtsdaten geladen sind, wählen Sie **Datei** > **Speichern unter** und dann **Power BI-Berichtsserver** aus.
   
   :::image type="content" source="media/save-powerbi-report-server.png" alt-text="Speichern unter „Power BI-Berichtsserver“" lightbox="media/save-powerbi-report-server.png":::

1. Speichern Sie den Bericht im `Sample Reports`-Ordner, den Sie auf dem Berichterstattungspunkt erstellt haben.
     
   :::image type="content" source="media/save-sample-report.png" alt-text="Speichern im Ordner „Beispielberichte“" lightbox="media/save-sample-report.png":::

1. Wiederholen Sie die Schritte für alle anderen Beispielberichte. Schließen Sie anschließend Microsoft Power BI Desktop (optimiert für Power BI-Berichtsserver).
1. Wechseln Sie in der Configuration Manager-Konsole zu **Überwachung** > **Power BI-Berichte** > **Beispielberichte**.
1. Klicken Sie mit der rechten Maustaste auf einen der Berichte, und wählen Sie **Im Browser ausführen** aus, um den Bericht zu starten.

   :::image type="content" source="media/view-powerbi-report.png" alt-text="Ausführen des Beispielberichts über die Configuration Manager-Konsole" lightbox="media/view-powerbi-report.png":::

## <a name="next-steps"></a>Nächste Schritte

[Integrieren mit dem Power BI-Berichtsserver](powerbi-report-server.md)
