---
title: Erstellen von Bereitstellungsplänen
titleSuffix: Configuration Manager
description: Dieser Artikel enthält eine Anleitung zum Erstellen von Bereitstellungsplänen in Desktop Analytics.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 8e0e8496-136b-461f-8239-cc19c6b78c3b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: ac9b5ddd85904c90709a9450d6d2a9ffd379ddb9
ms.sourcegitcommit: fddbb6c20cf7e19944944d4f81788adf249c963f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/12/2020
ms.locfileid: "83268758"
---
# <a name="how-to-create-deployment-plans-in-desktop-analytics"></a>Erstellen von Bereitstellungsplänen in Desktop Analytics

In diesem Artikel werden die Schritte zum Erstellen eines Bereitstellungsplans in Desktop Analytics erläutert. Zunächst sollten Sie sich über [Bereitstellungspläne informieren](about-deployment-plans.md).

## <a name="create-a-plan-for-windows-10"></a>Erstellen eines Plans für Windows 10

Führen Sie die Schritte in diesem Abschnitt aus, um mit Desktop Analytics einen Plan für die Bereitstellung von Windows 10 zu erstellen.

1. Öffnen Sie das [Desktop Analytics-Portal](https://aka.ms/desktopanalytics). Geben Sie Anmeldeinformationen ein, die mindestens über die Berechtigungen **Arbeitsbereichsmitwirkende** verfügen.  

2. Wählen Sie in der Gruppe „Verwalten“ die Option **Bereitstellungspläne** aus.  

3. Wählen Sie im Bereich **Bereitstellungspläne** die Option **Erstellen** aus.  

4. Konfigurieren Sie im Bereich **Bereitstellungsplan erstellen** die folgenden Einstellungen:  

    - **Name:** Hier wird ein eindeutiger Name für die Bereitstellung angegeben.  

    - **Produkte und Versionen**: Wählen Sie die bereitzustellende Windows 10-Version aus. Microsoft empfiehlt, Bereitstellungspläne zu erstellen, die die neueste Version verwenden.  

    - **Gerätegruppen**: Wählen Sie eine oder mehrere Gruppen derselben Hierarchie aus. Bei diesen Gruppen handelt es sich um [Gerätesammlungen](connect-configmgr.md#bkmk_Collections), die aus Configuration Manager synchronisiert werden.

        Wenn Sie mehrere Configuration Manager-Hierarchien mit derselben Desktop Analytics-Instanz verbinden, wird dem Sammlungsnamen in der Konfiguration des globalen Piloten ein Anzeigename für die Hierarchie vorangestellt. Dieser Name ist die **Anzeigename**-Eigenschaft der Desktop Analytics-Verbindung in der Configuration Manager-Konsole.<!-- 4814075 -->

        > [!NOTE]
        > Die Unterstützung mehrerer Hierarchien erfordert Configuration Manager-Version 1910 oder höher.
        >
        > Wenn Sie Sammlungen für mehrere Hierarchien auswählen, wird im Portal eine Warnung angezeigt. Der Bereitstellungsplan kann nicht mit Sammlungen aus mehreren Hierarchien erstellt werden.<!-- 4814075 -->

    - **Bereitschaftsregeln**: Anhand dieser Regeln können Sie bestimmen, welche Geräte sich für ein Upgrade qualifizieren. Weitere Informationen finden Sie unter [Bereitschaftsregeln](#readiness-rules).  

    - **Abschlussdatum**: Wählen Sie das Datum aus, an dem Windows vollständig auf sämtlichen Zielgeräten bereitgestellt sein soll.  

5. Wählen Sie **Erstellen** aus. Der neue Plan wird während seiner Verarbeitung in der Liste der Bereitstellungspläne angezeigt. Fordern Sie die bedarfsgesteuerte Datenaktualisierung an, um die Verarbeitung zu beschleunigen. Weitere Informationen finden Sie unter [Desktop Analytics – Häufig gestellte Fragen](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).  

6. Öffnen Sie den Bereitstellungsplan, indem Sie seinen Namen auswählen.  

7. Wählen Sie im Menü des Bereitstellungsplans in der Gruppe **Vorbereiten** die Option **Wichtigkeit angeben** aus.  

    1. Wählen Sie auf der Registerkarte **Apps** aus, dass nur Objekte vom Typ **Nicht überprüft** angezeigt werden sollen.  

    2. Wählen Sie die einzelnen Apps aus, und wählen Sie anschließend **Bearbeiten** aus. Sie können mehrere Apps gleichzeitig für die Bearbeitung auswählen.  

    3. Wählen Sie in der Liste **Wichtigkeit** eine Wichtigkeitsstufe aus. Wenn Desktop Analytics die App während des Pilotversuchs überprüfen soll, wählen Sie **Kritisch** oder **Wichtig** aus. Apps, die als **Nicht wichtig** markiert sind, werden nicht überprüft. Bewerten Sie beim Zuweisen von Wichtigkeitsstufen ihre [Kompatibilität](compat-assessment.md) und andere Planerkenntnisse.  

        Beim Zuweisen von Wichtigkeitsstufen können Sie auch die Upgradeentscheidung auswählen.  

    4. Klicken Sie abschließend auf **Speichern**.  

8. Wählen Sie im Menü des Bereitstellungsplans in der Gruppe **Vorbereiten** die Option **Piloten identifizieren** aus.  

    1. Überprüfen Sie die empfohlenen Geräte für den Pilotversuch.  

    2. Wählen Sie die einzelnen Geräte aus, und wählen Sie **Zu Pilot hinzufügen** aus. Wenn Sie mit der Empfehlung nicht einverstanden sind, wählen Sie **Ersetzen** aus.  

        Wenn Sie Informationen dazu wünschen, wie Desktop Analytics diese Empfehlungen abgibt, wählen Sie oben rechts im Bereich **Piloten identifizieren** das Informationssymbol aus.

## <a name="readiness-rules"></a>Bereitschaftsregeln

Anhand dieser Regeln können Sie bestimmen, welche Geräte sich für ein direktes Upgrade qualifizieren. Sie können diese Regeln beim Erstellen des Bereitstellungsplans festlegen; die Regeln können jedoch auch später bearbeitet werden.

So ändern Sie die Bereitschaftsregeln:

1. Wählen Sie im Desktop Analytics-Portal den Bereitstellungsplan aus.
1. Wählen Sie neben dem Namen die Option **Bearbeiten** aus.
1. Wählen Sie **Bereitschaftsregeln** aus.
1. Wählen Sie **Windows-Betriebssystem** aus.
1. Nehmen Sie die erforderlichen Änderungen vor, und wählen Sie **Speichern** aus.

Für Upgrades des **Windows-Betriebssystems** sind zwei Regeln verfügbar: Gerätetreiber und Windows-Anwendungen.

### <a name="device-drivers"></a>Gerätetreiber

Hiermit wird konfiguriert, ob ihre Geräte Treiber aus Windows Update beziehen. Dieser Wert ist in der Standardeinstellung **Aus**. Aktivieren Sie diese Regel, wenn Sie Updates (einschließlich von Treibern) mithilfe von Windows Update for Business verwalten. Wenn Sie Softwareupdates hingegen mit Configuration Manager verwalten, legen Sie diese Regel auf **Aus** fest.

### <a name="windows-applications"></a>Windows-Anwendungen

Die Apps, die von Desktop Analytics als *Beachtenswert* ausgewiesen werden, basieren auf dem Schwellenwert für eine niedrige Anzahl von Installationen. Legen Sie diesen Schwellenwert in den Bereitschaftsregeln für den Bereitstellungsplan fest. Standardmäßig beträgt dieser Schwellenwert **2,0 %** . Sie können den Wert von `0.0` in `10.0` ändern.


## <a name="next-steps"></a>Nächste Schritte

Fahren Sie mit dem nächsten Artikel fort, um die Bereitstellung auf Geräten in der Pilotphase durchzuführen.
> [!div class="nextstepaction"]  
> [Bereitstellen für die Pilotphase](deploy-pilot.md)  
