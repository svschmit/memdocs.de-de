---
title: Installieren von Power BI-Beispielberichten
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie die Power BI-Beispielberichte in Configuration Manager installieren
ms.date: 08/18/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 7e9bc22c-67ac-4a86-b613-944a4928e583
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 025788a4ed4a26123f24ec667348eae97821295e
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88699686"
---
# <a name="install-power-bi-sample-reports"></a>Installieren von Power BI-Beispielberichten
<!--5679791-->
*Gilt für: Configuration Manager (Current Branch)*

Sie können den [Power BI-Berichtsserver](/power-bi/report-server/get-started) ab Version 2002 mit der Configuration Manager-Berichterstellung integrieren. Zum Herunterladen stehen Beispielberichte zur Verfügung, die Sie in Configuration Manager installieren können. In diesem Artikel wird beschrieben, wie Sie die Power BI-Beispielberichte in Configuration Manager installieren.

## <a name="prerequisites"></a>Voraussetzungen

- Configuration Manager-Reporting Services-Punkt in [Power BI-Berichtsserver integriert](powerbi-report-server.md)

- [Microsoft Power BI Desktop (optimiert für Power BI-Berichtsserver, Version vom September 2019)](https://www.microsoft.com/download/details.aspx?id=57271) oder höher

- Das [Updaterollup (4560496) für Version 2002](https://support.microsoft.com/help/4560496) wird empfohlen, ist jedoch nicht erforderlich.

    > [!IMPORTANT]
    > Verwenden Sie nur Power BI Desktop-Versionen aus dem [Microsoft Download Center](https://www.microsoft.com/download/). Nutzen Sie keine Version aus dem Microsoft Store.
    >
    > Verwenden Sie nur eine Version von Power BI Desktop, die [für Power BI-Berichtsserver optimiert](/power-bi/report-server/install-powerbi-desktop) ist.

## <a name="download-the-sample-reports"></a>Herunterladen der Beispielberichte

So laden Sie die Beispielberichte herunter:

1. Laden Sie die Power BI-Beispielberichte aus dem [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=101452) herunter.

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

    :::image type="content" source="media/sample-report-database.png" alt-text="Angeben von Datenbank- und Datenbankserver-Name" lightbox="media/sample-report-database.png":::

    > [!NOTE]
    > Wenn Sie das Datenmodell laden oder anwenden, ignorieren Sie alle Fehlermeldungen, die Sie ggf. erhalten. Wenn z. B. die folgende Fehlermeldung angezeigt wird: „Das Herstellen von Verbindungen mit Tabellen aus mehr als einer Datenbank wird im DirectQuery-Modus nicht unterstützt“, wählen Sie **Schließen** aus. Aktualisieren Sie dann die Datenquelleneinstellungen:
    >
    > 1. Wählen Sie in Power BI Desktop im Menüband **Abfragen bearbeiten** und dann **Datenquelleneinstellungen** aus.
    > 1. Wählen Sie **Quelle ändern** aus, bestätigen Sie Ihre Server- und Datenbanknamen, und wählen Sie **OK** aus.
    > 1. Schließen Sie das Fenster mit den Datenquelleneinstellungen, und wählen Sie dann **Änderungen übernehmen** aus.

1. Wenn die Berichtsdaten geladen sind, wählen Sie **Datei** > **Speichern unter** und dann **Power BI-Berichtsserver** aus.

    :::image type="content" source="media/save-powerbi-report-server.png" alt-text="Speichern unter „Power BI-Berichtsserver“" lightbox="media/save-powerbi-report-server.png":::

1. Speichern Sie den Bericht im `Sample Reports`-Ordner, den Sie auf dem Berichterstattungspunkt erstellt haben.

    :::image type="content" source="media/save-sample-report.png" alt-text="Speichern im Ordner „Beispielberichte“" lightbox="media/save-sample-report.png":::

1. Wiederholen Sie die Schritte für alle anderen Beispielberichte. Schließen Sie anschließend Microsoft Power BI Desktop (optimiert für Power BI-Berichtsserver).

1. Wechseln Sie in der Configuration Manager-Konsole zu **Überwachung** > **Power BI-Berichte** > **Beispielberichte**.

1. Klicken Sie mit der rechten Maustaste auf einen der Berichte, und wählen Sie **Im Browser ausführen** aus, um den Bericht zu starten.

    :::image type="content" source="media/view-powerbi-report.png" alt-text="Ausführen des Beispielberichts über die Configuration Manager-Konsole" lightbox="media/view-powerbi-report.png":::