---
title: Clientbenachrichtigung
titleSuffix: Configuration Manager
description: Verwalten Sie Clients, indem Sie über die zentrale Configuration Manager-Konsole sofortige Maßnahmen ergreifen.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: deb8aac8-2bd9-4980-a25b-5f8d93051226
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8a00f77a5a902728a7c41905314511cffcfa81a5
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694958"
---
# <a name="client-notification-in-configuration-manager"></a>Clientbenachrichtigung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Um sofortige Maßnahmen über Remoteclients zu ergreifen, senden Sie eine Clientbenachrichtigung mithilfe der Configuration Manager-Konsole. Starten Sie diese Aktionen auf einem einzelnen Gerät oder für eine Gerätesammlung.

## <a name="actions"></a>Aktionen

Die folgenden Aktionen finden Sie im Menüband auf der Registerkarte „Start“ in den Gruppen „Gerät“ oder „Sammlung“.

### <a name="install-client"></a>Client installieren

Öffnet den **Assistenten zur Clientinstallation**. Dieser Assistent installiert einen Configuration Manager-Client mithilfe einer Clientpushinstallation. Weitere Informationen finden Sie unter [Clientpushinstallation](../deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).

#### <a name="permissions---install-client"></a>Berechtigungen: Client installieren

Für diese Aktion sind die Berechtigungen **Ressource ändern** und **Lesen** für das Objekt **Sammlung** erforderlich.

Die folgenden integrierten Rollen verfügen standardmäßig über diese Berechtigungen:

- Anwendungsadministrator  
- Hauptadministrator  
- Infrastrukturadministrator  
- Betriebsadministrator  
- Manager der Betriebssystembereitstellung  

Fügen Sie diese Berechtigungen benutzerdefinierten Rollen hinzu, die den Client pushen müssen.

### <a name="run-script"></a>Skript ausführen

Öffnet den **Assistenten zur Skriptausführung**, um ein PowerShell-Skript auf allen Clients in der Sammlung auszuführen. Weitere Informationen finden Sie unter [Erstellen und Ausführen von PowerShell-Skripts](../../../apps/deploy-use/create-deploy-scripts.md).

#### <a name="permissions---run-script"></a>Berechtigungen: Skript ausführen

Diese Aktion erfordert die Berechtigung **Skript ausführen** für das Objekt **Sammlung**.

Die folgenden integrierten Rollen verfügen standardmäßig über diese Berechtigung:

- Hauptadministrator  
- Infrastrukturadministrator  
- Betriebsadministrator  

Fügen Sie diese Berechtigung benutzerdefinierten Rollen hinzu, die Skripts ausführen müssen.

### <a name="start-cmpivot"></a>Starten von CMPivot

Startet **CMPivot**, das Abfragen für die Zielgeräte in Echtzeit ausführt. Weitere Informationen finden Sie unter [CMPivot](../../servers/manage/cmpivot.md).

#### <a name="permissions---start-cmpivot"></a>Berechtigungen: CMPivot starten

Diese Aktion erfordert die gleichen Berechtigungen wie die Aktion [Skript ausführen](#run-script).

Ab Version 1906 können Sie die Berechtigung **CMPivot ausführen** im Objekt **Sammlung** verwenden.

## <a name="client-notification"></a>Clientbenachrichtigung

Diese Aktionen sind im Menü **Clientbenachrichtigung** im Menüband auf der Registerkarte „Start“ in den Gruppen „Gerät“ oder „Sammlung“ zu finden.

Bis Version 1806 einschließlich stand die Option **Clientbenachrichtigung** nur über den Knoten „Gerätesammlung“ oder durch Anzeige der Mitgliedschaft einer Gerätesammlung zur Verfügung. Ab Version 1810 können Sie eine **Clientbenachrichtigung** direkt vom Knoten **Geräte** aus starten. Sie müssen sich nicht mehr in einer Ansicht der Sammlungsmitgliedschaft befinden. <!--SCCMDocs-pr issue 2972-->

#### <a name="permissions---client-notification"></a>Benachrichtigungen: Clientbenachrichtigung

<!--SCCMDocs-pr issue #2972-->
Ab Version 1810 ist für Clientbenachrichtigungsaktionen die Berechtigung **Ressource benachrichtigen** im Sammlungsobjekt erforderlich. Diese Berechtigung gilt für alle Aktionen im Menü **Clientbenachrichtigung**.

Die folgenden integrierten Rollen verfügen standardmäßig über diese Berechtigung:

- Hauptadministrator  
- Betriebsadministrator  

Fügen Sie diese Berechtigung benutzerdefinierten Rollen hinzu, die Clientbenachrichtigungsaktionen verwenden müssen.

### <a name="download-computer-policy"></a>Computerrichtlinie herunterladen

Aktualisieren Sie die Geräterichtlinie. Weitere Informationen finden Sie unter [Initiieren des Richtlinienabrufs für einen Konfigurations-Manager-Client](manage-clients.md#BKMK_PolicyRetrieval).  

### <a name="download-user-policy"></a>Benutzerrichtlinie herunterladen

Aktualisieren Sie die Benutzerrichtlinie.  

### <a name="collect-discovery-data"></a>Ermittlungsdaten sammeln

Senden Sie Clients zum Senden eines Discovery Data Records (DDR) an. Weitere Informationen finden Sie unter [Frequenzermittlung](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutHeartbeat).  

### <a name="collect-software-inventory"></a>Softwareinventurdaten sammeln

Weisen Sie Clients zum Ausführen eines Softwareinventurzyklus an. Weitere Informationen finden Sie unter [Einführung in die Softwareinventur](inventory/introduction-to-software-inventory.md).  

### <a name="collect-hardware-inventory"></a>Erfassen der Hardwareinventur

Weisen Sie Clients zum Ausführen eines Hardwareinventurzyklus an. Weitere Informationen finden Sie unter [Einführung in die Hardwareinventur](inventory/introduction-to-hardware-inventory.md).  

### <a name="evaluate-application-deployments"></a>Anwendungsbereitstellungen auswerten

Weisen Sie Clients zum Ausführen eines Evaluationszyklus für die Anwendungsbereitstellung an. Weitere Informationen finden Sie unter [Erneute Auswertung für Bereitstellungen planen](../deploy/about-client-settings.md#schedule-re-evaluation-for-deployments).  

### <a name="evaluate-software-update-deployments"></a>Bereitstellungen von Softwareupdates auswerten

Weisen Sie Clients zum Ausführen eines Evaluationszyklus für die Bereitstellung von Softwareupdates an. Weitere Informationen finden Sie unter [Einführung in Softwareupdates](../../../sum/understand/software-updates-introduction.md).  

### <a name="switch-to-the-next-software-update-point"></a>Zum nächsten Softwareupdatepunkt wechseln

Weisen Sie Clients an, zum nächsten verfügbaren Softwareupdatepunkt zu wechseln. Weitere Informationen finden Sie unter [Wechseln des Softwareupdatepunkts](../../../sum/plan-design/plan-for-software-updates.md#BKMK_SUPSwitching).  

### <a name="evaluate-device-health-attestation"></a>Integritätsnachweis für Geräte auswerten

Weisen Sie Windows 10-Clients zum Überprüfen und Senden ihres aktuellen Geräteintegritätsstatus an. Weitere Informationen finden Sie unter [Integritätsnachweis](../../servers/manage/health-attestation.md).  

### <a name="wake-up"></a>Reaktivieren

Weisen Sie ab Version 1810 Geräte, die zur Unterstützung von Wake-On-LAN zum Reaktivieren mithilfe von anderen Geräten in demselben Subnetz konfiguriert wurden, zum Senden des Wake-On-LAN-Pakets an. Weitere Informationen finden Sie unter [Konfigurieren von Wake-On-LAN](../deploy/configure-wake-on-lan.md).

### <a name="restart"></a>Neu starten

Lösen Sie den Neustart der ausgewählten Geräte aus. Weitere Informationen finden Sie unter [Restart clients](manage-clients.md#restart-clients) (Clients neu starten).

## <a name="client-diagnostics"></a>Clientdiagnose
<!--4433455-->

Ab Version 1910 gibt es in der Configuration Manager-Konsole neue Geräteaktionen für die **Clientdiagnose**. Die folgenden Aktionen wurden hinzugefügt:

- **Aktivieren ausführlicher Protokollierung**: Ändern Sie die globale Protokollebene für die CCM-Komponente in „Ausführlich“, und aktivieren Sie Debugprotokollierung.
- **Deaktivieren ausführlicher Protokollierung**: Ändern Sie die globale Protokollebene in „Standard“, und deaktivieren Sie Debugprotokollierung.
- **Clientprotokolle erfassen** (ab 2002): Eine Clientbenachrichtigung wird an die ausgewählten Clients gesendet, um die CCM-Protokolle zu erfassen. Die Protokolle werden mithilfe der Dateisammlungen der Softwareinventur zurückgegeben. <!--4226618-->
   - Die Größenbeschränkung für die komprimierten Clientprotokolle beträgt 100 MB. <!--6366098-->
   - Sie können diese Dateien mit dem [Ressourcen-Explorer](inventory/use-resource-explorer-to-view-software-inventory.md#bkmk_diag) verwalten und anzeigen.

   [![Sammeln von Clientprotokolle über die Konsole](./media/4226618-collect-client-logs.png)](./media/4226618-collect-client-logs.png#lightbox)

> [!IMPORTANT]
> - Diese Aktionen ändern nur die Ausführlichkeit des Protokolls, nicht die Größe oder den Verlauf. Durch ausführlichere Protokollierung können umfangreichere Protokollinhalte generiert werden.
> - Die Verwaltungspunktrolle verwendet ebenfalls die CCM-Komponente. Wenn das Zielgerät ebenfalls ein Verwaltungspunkt ist, gilt diese Aktion auch für diese Rolle.

Weitere Informationen zu diesen Einstellungen finden Sie unter [Informationen zu Protokolldateien](../../plan-design/hierarchy/about-log-files.md#bkmk_reg-client).

Verfolgen Sie den Status der Aufgabe in der Datei **diagnostics.log** auf dem Client nach. Beim Erfassen von Clientprotokollen werden zusätzliche Informationen in der Datei **MP_SinvCollFile.log** auf dem Verwaltungspunkt und in der Datei **sinvproc.log** auf dem Standortserver gesammelt.

### <a name="prerequisites---client-diagnostics"></a>Voraussetzungen: Clientdiagnose

- Aktualisieren Sie den Zielclient auf die neueste Version.

- Der Configuration Manager-Administratorbenutzer benötigt die Berechtigung **Ressource benachrichtigen**.

  Die folgenden integrierten Rollen verfügen standardmäßig über diese Berechtigung:

  - Hauptadministrator  
  - Infrastrukturadministrator  

  Fügen Sie diese Berechtigung benutzerdefinierten Rollen hinzu, die Clientbenachrichtigungsaktionen verwenden müssen.


## <a name="endpoint-protection"></a>Endpoint Protection

Die folgenden Aktionen sind im Menü **Endpoint Protection** zu finden. Diese Menü befindet sich im Menüband auf der Registerkarte „Start“ in der Gruppe „Sammlung“. Wenn Sie eines oder mehrere Geräte auswählen, befinden sich diese Aktionen auf der Registerkarte **Ausgewähltes Objekt** des Menübands.

Weitere Informationen finden Sie unter [Endpoint Protection in Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).

### <a name="permissions---endpoint-protection"></a>Berechtigungen: Endpoint Protection

Diese Aktion erfordert die Berechtigung **Sicherheit erzwingen** für das Objekt **Sammlung**.

Die folgenden integrierten Rollen verfügen standardmäßig über diese Berechtigung:

- Hauptadministrator  
- Endpoint Protection-Manager  
- Betriebsadministrator  

Fügen Sie diese Berechtigung benutzerdefinierten Rollen hinzu, die Endpoint Protection-Aktionen auslösen müssen.

### <a name="full-scan"></a>Vollständige Überprüfung

Lösen Sie Endpoint Protection oder Windows Defender aus, um eine *vollständige* Antischadsoftwareüberprüfung auszuführen.  

### <a name="quick-scan"></a>Schnellüberprüfung

Lösen Sie Endpoint Protection oder Windows Defender aus, um eine *schnelle* Antischadsoftwareüberprüfung auszuführen.  

### <a name="download-definition"></a>Definition herunterladen

Lösen Sie Endpoint Protection oder Windows Defender aus, um die neuesten Antischadsoftwaredefinitionen herunterzuladen.  

## <a name="see-also"></a>Weitere Informationen:

- [Verwalten von Clients](manage-clients.md)
- [Verwalten von Sammlungen](collections/manage-collections.md)
