---
title: Integrieren mit dem Power BI-Berichtsserver
titleSuffix: Configuration Manager
description: Durch die Integration von Power BI-Berichtsserver mit der Configuration Manager-Berichterstellung stellen Sie moderne Visualisierung und eine höhere Leistung sicher.
ms.date: 04/08/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 315e2613-dc71-46b1-80cb-26161d08103a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dc8aa57bda5f5a29d72af854be9a18e4f32760f8
ms.sourcegitcommit: 7b656712cc9340d18211c7754cb99bcaae91b0ca
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/03/2020
ms.locfileid: "89432539"
---
# <a name="integrate-with-power-bi-report-server"></a>Integrieren mit dem Power BI-Berichtsserver

*Gilt für: Configuration Manager (Current Branch)*

<!--3721603-->

Sie können den [Power BI-Berichtsserver](/power-bi/report-server/get-started) ab Version 2002 mit der Configuration Manager-Berichterstellung integrieren. So lässt sich die Visualisierung modernisieren und die Leistung verbessern. Durch die Integration werden Power BI-Berichte in der Konsole unterstützt. Dieses Feature ähnelt dem bereits für SQL Server Reporting Services verfügbaren Angebot.

Außerdem lassen sich Power BI Desktop-Berichtsdateien (.pbix) speichern und auf dem Power BI-Berichtsserver bereitstellen. Dieser Prozess ist bei allen SQL Server Reporting Services-Berichtsdateien (.rdl) ähnlich. Sie können die Berichte auch über die Configuration Manager-Konsole direkt im Browser starten.

## <a name="prerequisites"></a>Voraussetzungen

- Lizenz für einen Power BI-Berichtsserver (weitere Informationen unter [Lizenzieren von Power BI-Berichtsserver](/power-bi/report-server/get-started#licensing-power-bi-report-server))

- Laden Sie die Version des [Microsoft Power BI-Berichtsservers vom September 2019](https://www.microsoft.com/download/details.aspx?id=57270) oder höher herunter.

    > [!NOTE]
    > Installieren Sie den Power BI-Berichtsserver nicht sofort. Informationen zur ordnungsgemäßen Vorgehensweise entsprechend Ihrer jeweiligen Umgebung finden Sie unter [Konfigurieren des Reporting Services-Punkts](#configure-the-reporting-services-point).

- Laden Sie [Microsoft Power BI Desktop (optimiert für Power BI-Berichtsserver, Version vom September 2019)](https://www.microsoft.com/download/details.aspx?id=57271) oder höher herunter.

    > [!IMPORTANT]
    > - Verwenden Sie nur Power BI Desktop-Versionen aus dem [Microsoft Download Center](https://www.microsoft.com/download/), keine Versionen aus dem Microsoft Store.
    > - Verwenden Sie nur eine Version von [Power BI Desktop, die **für Power BI-Berichtsserver optimiert ist**](/power-bi/report-server/install-powerbi-desktop).

- Bei der Power BI-Integration wird die gleiche rollenbasierte Verwaltung für die Berichterstellung verwendet.
    > [!NOTE]
    > Power BI-Berichtsserver unterstützt keine RBAC-fähigen Berichte. Daher werden allen Betrachtern der Berichte unabhängig von der zugewiesenen Berechtigung die gleichen Ergebnisse angezeigt.

## <a name="configure-the-reporting-services-point"></a>Konfigurieren des Reporting Services-Punkts

Der Ablauf dieses Vorgangs hängt davon ab, ob diese Rolle bereits am Standort vorhanden ist.

### <a name="you-have-a-reporting-services-point"></a>Sie verfügen über einen Reporting Services-Punkt

Führen Sie diesen Prozess nur dann aus, wenn Sie bereits über einen Reporting Services-Punkt am Standort verfügen. Führen Sie alle Schritte dieses Vorgangs auf demselben Server aus:

1. Sichern Sie im **Konfigurations-Manager für Reporting Services** die **Verschlüsselungsschlüssel**. Weitere Informationen finden Sie unter [SSRS-Verschlüsselungsschlüssel – Sichern und Wiederherstellen von Verschlüsselungsschlüsseln](/sql/reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys).

    > [!WARNING]
    > Wenn Sie diesen Schritt überspringen, können Sie nicht mehr auf die benutzerdefinierten Berichte in SQL Server Reporting Services zugreifen.

1. Entfernen Sie die Rolle „Reporting Services-Punkt“ für den Standort.

1. Deinstallieren Sie SQL Server Reporting Services, aber behalten Sie die Datenbank bei.

1. Installieren Sie den Power BI-Berichtsserver.

1. Konfigurieren Sie den Power BI-Berichtsserver.

    1. Verwenden Sie dazu die Datenbank des vorherigen Berichtsservers.

    1. Verwenden Sie den **Konfigurations-Manager für Reporting Services** zum Wiederherstellen der **Verschlüsselungsschlüssel**.

1. Fügen Sie die Rolle „Reporting Services-Punkt“ in Configuration Manager hinzu.

### <a name="you-dont-have-a-reporting-services-point"></a>Sie verfügen über noch keinen Reporting Services-Punkt

Führen Sie diesen Prozess nur dann aus, wenn Sie am Standort noch über keinen Reporting Services-Punkt verfügen. Führen Sie alle Schritte dieses Vorgangs auf demselben Server aus:

1. Installieren Sie den Power BI-Berichtsserver.

2. Fügen Sie die Rolle „Reporting Services-Punkt“ in Configuration Manager hinzu. Weitere Informationen finden Sie unter [Konfigurieren der Berichterstellung](configuring-reporting.md).

## <a name="configure-the-configuration-manager-console"></a>Konfigurieren der Configuration Manager-Konsole

1. Aktualisieren Sie die Configuration Manager-Konsole auf dem Computer, auf dem sie ausgeführt wird, auf die neueste Version.

1. Installieren Sie Power BI Desktop. Achten Sie darauf, dass die Sprache dieselbe ist.

1. Starten Sie Power BI Desktop nach der Installation mindestens einmal, bevor Sie die Configuration Manager-Konsole öffnen.

## <a name="create-power-bi-reports"></a>Erstellen von Power BI-Berichten

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**, erweitern Sie **Berichterstellung**, und klicken Sie auf den neuen Knoten **Power BI-Berichte**.

1. Klicken Sie im Menüband auf **Create Report** (Bericht erstellen). Dadurch wird Power BI Desktop geöffnet.

1. Erstellen Sie einen Bericht in Power BI Desktop.

    - Wenn Sie in Power BI Desktop eine Verbindung mit einer Datenquelle herstellen, wählen Sie für die Verbindungseinstellungen **DirectQuery** aus.

    - Verwenden Sie in diesen Berichten nur unterstützte SQL-Ansichten. Weitere Informationen finden Sie unter [Erstellen von benutzerdefinierten Berichten mithilfe von SQL Server-Ansichten](../../../develop/core/understand/sqlviews/create-custom-reports-using-sql-server-views.md).

1. Wenn der Bericht gespeichert werden kann, klicken Sie im Menü **Datei** auf **Speichern als**, und wählen Sie dann **Power BI-Berichtsserver** aus.

1. Geben Sie im Fenster **Power BI Report Server Selection** (Ausgewählter Power BI-Berichtsserver) die URL für den Reporting Services-Punkt als **Neue Berichtsserveradresse** ein. Beispiel: `https://rsp.contoso.com/Reports`. Klicken Sie auf **OK**.

1. Doppelklicken Sie im Fenster **Bericht speichern** auf den Ordner `ConfigMgr_<SiteCode>`. Beispiel: `ConfigMgr_PS1`, wobei `PS1` der Code des ConfigMgr-Standorts ist. Sie können optional einen Unterordner für die Speicherung auswählen oder erstellen (vom Berichtsserver aus).
    > [!TIP]
    > Berichte und Berichtsordner mit Power BI-Berichten müssen sich im Ordner `ConfigMgr_<SiteCode>` auf dem Berichtsserver befinden, sonst werden sie nicht in der Configuration Manager-Konsole angezeigt.

1. Geben Sie in **Dateiname** einen Namen für den Bericht ein.

In der Configuration Manager-Konsole wird der neue Bericht in der Liste der Power BI-Berichte angezeigt. Wenn Ihre Berichte nicht angezeigt werden, überprüfen Sie, ob Sie die Berichte im Ordner `ConfigMgr_<SiteCode>` gespeichert haben.

## <a name="next-steps"></a>Nächste Schritte

Führen Sie nach dem Erstellen eines Berichts die folgenden Aktionen in der Configuration Manager-Konsole aus:

- **Run in Browser** (Im Browser ausführen): Dadurch wird der Power BI-Bericht im Webbrowser geöffnet. Geben Sie diese URL für andere frei, z. B.: `https://rsp.contoso.com/Reports/POWERBI/ConfigMgr_ABC/Windows%2010/Windows10%20Dashboard?rs:embed=true`

    > [!TIP]
    > Diese Berichte können nur im Webbrowser angezeigt werden.

- **Bearbeiten:** Nehmen Sie in Power BI Desktop Änderungen am Bericht vor. Bei einem vorhandenen Bericht speichern Sie Änderungen mit der Option **Speichern** auf dem Berichtsserver.

Weitere Informationen zu Protokolldateien, die für die Berichterstellung verwendet werden, finden Sie unter [Protokolldateireferenz: Berichterstellung](../../plan-design/hierarchy/log-files.md#BKMK_ReportLog).
