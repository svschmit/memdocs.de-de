---
title: Supportcenter-Schnellstart
titleSuffix: Configuration Manager
description: In diesem Artikel erfahren Sie, wie Sie für die Problembehandlung schnell den Status eines Konfigurations-Manager-Clients erfassen.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 5cb41e2b-4c79-4da9-a432-ff869c0870f8
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: c8c43fe1dbca9155bf9b554a2554c652b1482583
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707458"
---
# <a name="support-center-quickstart-guide"></a>Schnellstartanleitung für das Supportcenter

*Gilt für: Configuration Manager (Current Branch)*

Das Supportcenter verfügt über leistungsstarke Funktionen wie die Problembehebung und die Protokollanzeige in Echtzeit. Damit können Sie außerdem in nur wenigen Minuten den Status eines Konfigurations-Manager-Clientcomputers erfassen. Diese Fähigkeit umfasst auch den Zugriff auf Remoteclients.

Erstellen Sie eine vollständige *Paketdatei für die Problembehandlung* (.zip), in der der Clientstatus erfasst wird. Das Paket enthält nicht nur Protokolldateien, sondern auch andere Datentypen wie z. B. Registrierungseinstellungen und Clientkonfigurationen. Stellen Sie dieses Paket anschließend für einen Supportmitarbeiter bereit, der die Supportcenteranzeige nutzt.



## <a name="prerequisites"></a>Voraussetzungen

- Lokale Administratorrechte für einen Konfigurations-Manager-Client  

- Der Support-Center-Installer. Die Datei befindet sich auf dem Standortserver unter `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`. Weitere Informationen finden Sie im Abschnitt [Install (Installieren)](support-center.md#install) im Artikel „Support Center for Configuration Manager (Supportcenter für Configuration Manager)“.  



## <a name="step-1-create-a-data-bundle-on-a-local-client"></a>Schritt 1: Erstellen eines Datenpakets auf einem lokalen Client

1.  Installieren Sie das Supportcenter auf dem Konfigurations-Manager-Client.  

2.  Wechseln Sie in der Gruppe **Microsoft System Center** in das **Startmenü**, und klicken Sie auf **Supportcenter**.  

3.  Klicken Sie auf dem Tab „Start“ auf **Ausgewählte Daten sammeln**. Im Supportcenter wird standardmäßig nur das minimale Dataset erfasst: Protokolldateien, die Clientkonfiguration und das Betriebssystem.  

4.  Speichern Sie die Paketdatei für die Problembehebung (.zip) in einem Ordner auf dem Computer. Der Dateiname ähnelt standardmäßig dem im folgenden Beispiel: `Support_c885cdfed3c7482bba4f9e662978ec07.zip`.  



## <a name="step-2-view-the-data-bundle-using-support-center-viewer"></a>Schritt 2: Anzeigen des Datenpakets mithilfe der Supportcenteranzeige

1.  Starten Sie **Supportcenteranzeige**. Sie können diese Aktion auf jedem Computer ausführen, auf dem das Supportcenter installiert ist.  

2.  Klicken Sie auf **Open bundle** (Paket öffnen), navigieren Sie zu der Paketdatei, und wählen Sie **Öffnen** aus.  

3.  Nachdem die Supportcenteranzeige die Datei verarbeitet hat, wechseln Sie zu jeder verfügbaren Registerkarte. Zeigen Sie die Datentypen an, die im Supportcenter standardmäßig erfasst werden:  

    - **Konfiguration**  

        - Configuration Manager-Clientkonfiguration  

        - Betriebssystem  

        - Computer  

        - Dienste  

        - Netzwerkadapter  

    - **Protokolle:** Wählen Sie mindestens einen Eintrag aus der Liste aus, und klicken Sie auf **Öffnen**. Mit dieser Aktion werden die ausgewählten Protokolldateien in der Protokollanzeige geöffnet. Mit diesem Feature können Sie Fehlercodes nachschlagen. Mit erweiterten Filtern lässt sich die Analyse von Protokolldateien beschleunigen.  



## <a name="collect-more-data"></a>Erfassen weiterer Daten

Neben diesen grundlegenden Funktionen kann mit Supportcenter eine Vielzahl anderer Clientstatusinformationen gesammelt werden. Öffnen Sie das **Supportcenter**, und klicken Sie auf **Collect All Data** (Alle Daten erfassen). Dieser Prozess dauert normalerweise einige Minuten, sogar auf neueren Computern. Im Supportcenter werden die folgenden zusätzlichen Daten gesammelt:

- **Richtlinie:** Configuration Manager-Richtlinieneinstellungen, einschließlich der angeforderten Richtlinienkonfiguration und der tatsächlichen Richtlinienkonfiguration.  

- **Zertifikate:** Informationen zu öffentlichen Schlüsseln für Clientzertifikate. Das Supportcenter sammelt keine privaten Zertifikatschlüssel.  

- **Clientregistrierung:** Sammelt Informationen zur Clientkonfiguration aus der Registrierung. Das Supportcenter sammelt nur Informationen zur Configuration Manager-Registrierung.  

- **Client-WMI:** Informationen zur Clientkonfiguration aus der Windows-Verwaltungsinstrumentation (WMI). Das Supportcenter sammelt keine Clientrichtlinien.  

- **Problembehandlung:** Echtzeit-Problembehandlungsdaten für die Diagnose von üblichen Clientproblemen mit Active Directory, Verwaltungspunkten, Netzwerken, Richtlinienzuweisungen und der Registrierung.  

- **Debugdumps:** Führt einen Debugdump für den Client und die verwandten Prozesse durch. Debugdumps können sehr groß sein. Aktivieren Sie diese Option nur, wenn Sie Probleme mit der Leistung des Clients beheben müssen.  

