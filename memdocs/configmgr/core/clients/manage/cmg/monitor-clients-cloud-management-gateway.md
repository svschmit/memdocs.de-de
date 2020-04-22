---
title: Überwachen des Cloudverwaltungsgateways
titleSuffix: Configuration Manager
description: Überwachen Sie Clients und Netzwerkdatenverkehr mit Cloud Management Gateway.
ms.date: 06/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 15f72f80-9850-40ce-9c3a-443ba04b6a03
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b3233dc2f6bd13e56f7555536c95d42a34e01d5e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695148"
---
# <a name="monitor-cloud-management-gateway"></a>Überwachen des Cloudverwaltungsgateways

*Gilt für: Configuration Manager (Current Branch)*

Wenn CMG (Cloud Management Gateway) ausgeführt wird und Clients über diesen Dienst eine Verbindung herstellen, können Sie Clients und den Netzwerkdatenverkehr überwachen, um sich über die Leistung des Diensts zu informieren.


## <a name="monitor-clients"></a>Überwachen von Clients

Clients, die über CMG verbunden sind, werden genauso wie lokale Clients in der Configuration Manager-Konsole angezeigt. Weitere Informationen finden Sie unter [Überwachen von Clients in System Center Configuration Manager](../monitor-clients.md).


## <a name="monitor-traffic-in-the-console"></a>Überwachen von Datenverkehr in der Konsole

Sie können Datenverkehr über CMG mithilfe der Configuration Manager-Konsole wie folgt überwachen:

1. Navigieren Sie zum Arbeitsbereich **Verwaltung**, erweitern Sie den Eintrag **Cloud Services**, und wählen Sie den Knoten **Cloud Management Gateway** aus.  

2. Wählen Sie im Listenbereich das CMG aus.  

3. Sehen Sie sich die Informationen zum Datenverkehr im Detailbereich für den CMG-Verbindungspunkt und die Standortsystemrollen an, mit denen eine Verbindung hergestellt wird. Diese Statistiken zeigen die Clientanforderungen, die für diese Rollen eingehen. Die Anforderungen umfassen Benachrichtigungen zu Richtlinien, Standorten, Registrierung, Inhalten, Inventar und Clients.<!-- SCCMDocs#1208 -->

## <a name="set-up-outbound-traffic-alerts"></a>Einrichten von Warnungen für ausgehenden Datenverkehr

Durch Warnungen für ausgehenden Datenverkehr erfahren Sie, wann der für den Zeitraum von 14 Tagen festgelegte Schwellenwert für den Netzwerkdatenverkehr erreicht wird. Wenn Sie CMG hinzufügen, können Sie Warnungen für den Datenverkehr einrichten. Wenn Sie diesen Teil übersprungen haben, können Sie noch immer die Warnungen einrichten, wenn der Dienst ausgeführt wird. Die Warnungseinstellungen lassen sich jederzeit anpassen.

1. Navigieren Sie zum Arbeitsbereich **Verwaltung**, erweitern Sie den Eintrag **Cloud Services**, und wählen Sie den Knoten **Cloud Management Gateway** aus.  

2. Wählen Sie im Listenbereich CMG und anschließend auf dem Menüband **Eigenschaften** aus.  

3. Wechseln Sie zur Registerkarte **Warnungen**, um den Schwellenwert und die Warnungen zu aktivieren. Geben Sie den Datenschwellenwert in Gigabyte (GB) für den Zeitraum von 14 Tagen an. Legen Sie außerdem für den Schwellenwert eine Prozentzahl fest, mit der die Auslösung unterschiedlicher Warnstufen gesteuert wird.  

4. Klicken Sie auf **OK**, wenn Sie fertig sind.  


## <a name="monitor-logs"></a>Überwachungsprotokolle

CMG generiert Einträge in einer Reihe von Protokolldateien. Weitere Informationen finden Sie unter [Protokolldateien in System Center Configuration Manager](../../../plan-design/hierarchy/log-files.md#cloud-management-gateway).


## <a name="cloud-management-dashboard"></a>Dashboard für die Cloudverwaltung

<!--1358461-->
Ab Version 1806 stellt das Dashboard für die Cloudverwaltung eine zentrale Ansicht für die Nutzung von CMG bereit. Wenn der Standort in [Azure-Diensten](../../../servers/deploy/configure/azure-services-wizard.md) für die Cloudverwaltung integriert ist, werden auch Daten zu Cloudbenutzern und -geräten angezeigt.  

Der folgende Screenshot zeigt einen Teil des Dashboards für die Cloudverwaltung mit zwei der verfügbaren Kacheln:  
![Kacheln des Dashboards für die Cloudverwaltung mit CMG-Datenverkehr und aktuellen Onlineclients](media/1358461-cmg-dashboard.png)

Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**. Wählen Sie den Knoten **Cloudverwaltung** aus, und zeigen Sie die Dashboardkacheln an.  


## <a name="connection-analyzer"></a>Verbindungsanalyse

Verwenden Sie ab Version 1806 die CMG-Verbindungsanalyse für die Echtzeitüberprüfung zur Unterstützung der Problembehandlung. Das Hilfsprogramm in der Konsole überprüft den aktuellen Status des Diensts und den Kommunikationskanal über den CMG-Verbindungspunkt zu Verwaltungspunkten, die CMG-Datenverkehr zulassen.

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**. Erweitern Sie **Clouddienste**, und wählen Sie den Knoten **Cloud Management Gateway** aus.  

2. Wählen Sie die CMG-Zielinstanz und dann **Verbindungsanalyse** im Menüband aus.  

3. Wählen Sie im CMG-Verbindungsanalysefenster eine der folgenden Optionen aus, um sich bei dem Dienst zu authentifizieren:  

     1. **Azure AD-Benutzer:** Simulieren Sie mit dieser Option die Kommunikation einer cloudbasierten Benutzeridentität, die bei einem in Azure AD eingebundenen Windows 10-Gerät angemeldet ist. Klicken Sie auf **Anmelden**, um sicher die Anmeldeinformationen für das Azure AD-Benutzerkonto einzugeben.  

     2. **Clientzertifikat**: Simulieren Sie mit dieser Option die Kommunikation eines Configuration Manager-Clients mit einem [Clientauthentifizierungszertifikat](certificates-for-cloud-management-gateway.md#bkmk_clientauth).  

4. Klicken Sie auf **Starten**, um die Analyse zu starten. Im Fenster des Analysetools werden die Ergebnisse angezeigt. Wählen Sie einen Eintrag aus, um weitere Informationen im Feld „Beschreibung“ anzuzeigen.  


## <a name="stop-cmg-when-it-exceeds-threshold"></a><a name="bkmk_stop"></a> Beenden von CMG beim Überschreiten des Schwellenwerts

<!--3735092-->
Ab Version 1902 kann Configuration Manager einen CMG-Dienst beenden, wenn die Gesamtmenge der übertragenen Daten Ihr Limit überschreitet. Verwenden Sie [Warnungen](#set-up-outbound-traffic-alerts), um Benachrichtigungen auszulösen, wenn bei der Nutzung Warnstufen oder kritische Werte erreicht werden. Um unerwartete Azure-Kosten aufgrund einer Nutzungsspitze zu reduzieren, deaktiviert diese Option den Clouddienst.

> [!Important]  
> Mit dem Clouddienst sind auch dann Kosten verbunden, wenn der Dienst nicht ausgeführt wird. Durch Beenden des Diensts werden nicht alle mit Azure verbunden Kosten eingespart. Wenn Sie alle Kosten für den Clouddienst einsparen möchten, [entfernen Sie den CMG-Dienst](setup-cloud-management-gateway.md#modify-a-cmg).  
>
> Wenn der CMG-Dienst beendet wird, können internetbasierte Clients nicht mehr mit Configuration Manager kommunizieren.  

Zur Gesamtmenge übertragener Daten (ausgehend) gehören Daten vom Clouddienst und Speicherkonto. Diese Daten stammen aus folgenden Datenflüssen:

- CMG zu Client  
- CMG zu Standort, darunter auch CMG-Protokolldateien  
- Wenn Sie CMG für Inhalte aktivieren, Speicherkonto zu Client  

Weitere Informationen zu diesen Datenflüssen finden Sie unter [Ports und Datenflüsse](plan-cloud-management-gateway.md#ports-and-data-flow).

Der Schwellenwert für die Speicherwarnung ist hiervon getrennt zu sehen. Mit dieser Warnung wird die Kapazität der Azure Storage-Instanz überwacht.

Wenn Sie in der Konsole im Knoten **Cloudverwaltungsgateway** die CMG-Instanz auswählen, wird im Detailbereich die Gesamtmenge der übertragenen Daten angezeigt.

Der Schwellenwert wird von Configuration Manager alle sechs Minuten überprüft. Wenn eine plötzliche Nutzungsspitze auftritt, kann es daher bis zu sechs Minuten dauern, bis Configuration Manager eine Überschreitung des Schwellenwerts erkennt und den Dienst beendet.

### <a name="process-to-stop-the-cloud-service-when-it-exceeds-threshold"></a>Prozess zum Beenden eines Clouddiensts beim Überschreiten des Schwellenwerts

1. [Richten Sie Warnungen für ausgehenden Datenverkehr ein](#set-up-outbound-traffic-alerts).  

2. Aktivieren Sie im Eigenschaftenfenster von CMG auf der Registerkarte **Warnungen** die Option **Diesen Dienst anhalten, wenn der kritische Schwellenwert überschritten wird**.  

Geben Sie zum Testen dieses Features für folgende Einstellungen vorübergehend einen niedrigeren Wert ein:  

- **14-Tage-Schwellenwert für ausgehende Datenübertragung (GB)** . Der Standardwert lautet `10000`.  

- **Prozentsatz des Schwellenwerts für Auslösung einer kritischen Warnung**. Der Standardwert lautet `90`.  
