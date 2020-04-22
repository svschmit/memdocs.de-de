---
title: Windows-Firewall- und -Porteinstellungen für Clients
titleSuffix: Configuration Manager
description: Wählen Sie Windows-Firewall- und -Porteinstellungen für Clients in Configuration Manager aus.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: dce4b640-c92f-401a-9873-ce9aa9262014
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2290899c0159221c5f45ce6c34332b766984e4c1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694778"
---
# <a name="windows-firewall-and-port-settings-for-clients-in-configuration-manager"></a>Windows-Firewall- und -Porteinstellungen für Clients in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Für Clientcomputer in Configuration Manager, auf denen die Windows-Firewall ausgeführt wird, müssen häufig Ausnahmen definiert werden, damit die Kommunikation mit deren Standort möglich ist. Welche Ausnahmen konfiguriert werden müssen, ist abhängig von den mit dem Configuration Manager-Client verwendeten Verwaltungsfeatures.  

 In den folgenden Abschnitten werden diese Verwaltungsfunktionen und die Konfiguration der erforderlichen Ausnahmen in der Windows-Firewall beschrieben.  

##  <a name="modifying-the-ports-and-programs-permitted-by-windows-firewall"></a><a name="BKMK_ModifyingWindowsFirewall"></a> Ändern der von der Windows-Firewall zugelassenen Ports und Programme  
 Gehen Sie wie folgt vor, um die Ports und Programme in der Windows-Firewall für den Configuration Manager-Client zu ändern.  

#### <a name="to-modify-the-ports-and-programs-permitted-by-windows-firewall"></a>So ändern Sie die von der Windows-Firewall zugelassenen Ports und Programme  

1.  Öffnen Sie auf dem Computer, auf dem die Windows-Firewall ausgeführt wird, die Systemsteuerung.  

2.  Klicken Sie mit der rechten Maustaste auf **Windows-Firewall**, und klicken Sie dann auf **Öffnen**.  

3.  Konfigurieren Sie alle erforderlichen Ausnahmen und benutzerdefinierten Programme und Ports.  

## <a name="programs-and-ports-that-configuration-manager-requires"></a>Für Configuration Manager erforderliche Programme und Ports  
 Für die folgenden Configuration Manager-Features müssen Ausnahmen für die Windows-Firewall eingerichtet werden:  

### <a name="queries"></a>Abfragen  
 Wenn Sie die Configuration Manager-Konsole auf einem Computer ausführen, auf dem die Windows-Firewall ausgeführt wird, tritt bei der ersten Ausführung von Abfragen ein Fehler auf. Sie werden über ein Dialogfeld gefragt, ob die Blockierung der Datei „statview.exe“ aufgehoben werden soll. Wenn Sie die Blockierung von "statview.exe" aufheben, werden künftige Abfragen fehlerfrei ausgeführt. Sie können "Statview.exe" vor dem Ausführen einer Abfrage der Liste der Programme und Dienste auf der Registerkarte **Ausnahmen** der Windows-Firewall auch manuell hinzufügen.  

### <a name="client-push-installation"></a>Clientpushinstallation  
 Fügen Sie der Windows-Firewall folgende Ausnahmen hinzu, um Configuration Manager-Clients mithilfe von Clientpush installieren zu können:  

-   Eingehend und ausgehend: **Datei- und Druckerfreigabe**  

-   Eingehend: **Windows-Verwaltungsinstrumentation (WMI)**  

### <a name="client-installation-by-using-group-policy"></a>Installieren von Clients mithilfe von Gruppenrichtlinien  
 Sie müssen der Windows-Firewall die Funktion **Datei- und Druckerfreigabe** als Ausnahme hinzufügen, um Configuration Manager-Clients mithilfe von Gruppenrichtlinien installieren zu können.  

### <a name="client-requests"></a>Clientanfragen  
 Damit die Kommunikation zwischen Clientcomputern und Configuration Manager-Standortsystemen möglich ist, müssen der Windows-Firewall folgende Ausnahmen hinzugefügt werden:  

 Ausgehend: TCP-Port **80** (für die HTTP-Kommunikation)  

 Ausgehend: TCP-Port **443** (für die HTTPS-Kommunikation)  

> [!IMPORTANT]  
>  Es handelt sich dabei um Standardportnummern, die in Configuration Manager geändert werden können. Weitere Informationen finden Sie unter [Konfigurieren von Clientkommunikationsports](../../../core/clients/deploy/configure-client-communication-ports.md). Wurden diese Ports geändert, müssen Sie außerdem entsprechende Ausnahmen in der Windows-Firewall konfigurieren.  

### <a name="client-notification"></a>Clientbenachrichtigung  
 Fügen Sie der Windows-Firewall Folgendes als Ausnahme hinzu, damit der Verwaltungspunkt Clientcomputer über Aktionen informiert, die ausgeführt werden müssen, wenn ein Administrator eine Clientaktion in der Configuration Manager-Konsole auswählt, z.B. das Herunterladen einer Computerrichtlinie oder das Initiieren einer Überprüfung auf Schadsoftware:  

 Ausgehend: TCP-Port **10123**  

 Wenn diese Art der Kommunikation nicht erfolgreich ist, greift Configuration Manager automatisch auf den vorhandenen HTTP- oder HTTPS-Port für die Kommunikation zwischen Client und Verwaltungspunkt zurück:  

 Ausgehend: TCP-Port **80** (für die HTTP-Kommunikation)  

 Ausgehend: TCP-Port **443** (für die HTTPS-Kommunikation)  

> [!IMPORTANT]  
>  Es handelt sich dabei um Standardportnummern, die in Configuration Manager geändert werden können. Weitere Informationen finden Sie unter [Konfigurieren von Clientkommunikationsports](../../../core/clients/deploy/configure-client-communication-ports.md). Wurden diese Ports geändert, müssen Sie außerdem entsprechende Ausnahmen in der Windows-Firewall konfigurieren.  

### <a name="remote-control"></a>Remotesteuerung  
 Damit Sie die Configuration Manager-Remotesteuerung verwenden können, lassen Sie folgenden Port zu:  

-   Eingehend: TCP-Port **2701**  

### <a name="remote-assistance-and-remote-desktop"></a>Remoteunterstützung und Remotedesktop  
 Damit Sie Remoteunterstützung von der Configuration Manager-Konsole aus initiieren können, fügen Sie auf dem Clientcomputer in der Windows-Firewall der Liste zugelassener Programme und Dienste das benutzerdefinierte Programm **Helpsvc.exe** und den benutzerdefinierten eingehenden Port TCP **135** hinzu. Sie müssen außerdem **Remoteunterstützung** und **Remotedesktop**zulassen. Wenn Sie Remoteunterstützung vom Clientcomputer aus initiieren, werden **Remoteunterstützung** und **Remotedesktop**von der Windows-Firewall automatisch konfiguriert.  

### <a name="wake-up-proxy"></a>Aktivierungsproxy  
 Wenn Sie die Clienteinstellung für den Aktivierungsproxy aktivieren, wird von einem neuen Dienst mit dem Namen „ConfigMgr-Aktivierungsproxy“ mithilfe eines Peer-zu-Peer-Protokolls überprüft, ob andere Computer im Subnetz aktiv sind. Diese werden dann bei Bedarf aktiviert. Für diese Kommunikation werden die folgenden Ports verwendet:  

 Ausgehend: UDP-Port **25536**  

 Ausgehend: UDP-Port **9**  

 Dies sind die Standardportnummern, die in Configuration Manager unter **Energieverwaltung** über die Clienteinstellungen **Portnummer für Aktivierungsproxy (UDP)** und **Wake-on-LAN-Portnummer (UDP)** geändert werden können. Wenn Sie die Clienteinstellung **Energieverwaltung**: **Windows-Firewall-Ausnahme für Aktivierungsproxy** angeben, werden diese Ports in der Windows-Firewall für Clients automatisch konfiguriert. Falls auf Clients eine andere Firewall ausgeführt wird, müssen Sie die Ausnahmen für diese Portnummern jedoch manuell konfigurieren.  

 Zusätzlich zu diesen Ports nutzt der Aktivierungsproxy auch ICMP-Echoanforderungsmeldungen (Internet Control Message Protocol) von einem Clientcomputer zu einem anderen Clientcomputer. Diese Kommunikation wird verwendet, um zu überprüfen, ob der andere Clientcomputer im Netzwerk aktiviert ist. ICMP (Internet Control Message Protocol) wird gelegentlich als „TCP/IP-Ping-Befehle“ bezeichnet.  

 Weitere Informationen zum Aktivierungsproxy finden Sie unter [Planen der Clientaktivierung](../../../core/clients/deploy/plan/plan-wake-up-clients.md).  

### <a name="windows-event-viewer-windows-performance-monitor-and-windows-diagnostics"></a>Windows-Ereignisanzeige, Windows-Systemmonitor und Windows-Diagnose  
 Sie müssen die Funktion **Datei- und Druckerfreigabe** als Ausnahme in der Windows-Firewall aktivieren, um den Zugriff auf die Windows-Ereignisanzeige, den Windows-Systemmonitor und die Windows-Diagnose von der Configuration Manager-Konsole aus zu ermöglichen.  

## <a name="ports-used-during-configuration-manager-client-deployment"></a>Bei der Clientbereitstellung von Konfigurations-Manager verwendete Ports  
 In der folgenden Tabelle werden die Ports aufgelistet, die bei der Clientinstallation verwendet werden.  

> [!IMPORTANT]  
>  Wenn sich zwischen den Standortsystemservern und dem Clientcomputer eine Firewall befindet, überprüfen Sie, ob von der Firewall Datenverkehr für die Ports zugelassen wird, die für die ausgewählte Clientinstallationsmethode erforderlich sind. Firewalls verhindern beispielsweise häufig die Clientpushinstallation, da sie Server Message Block (SMB) und Remote Procedure Calls (RPC) blockieren. Verwenden Sie in diesem Szenario eine andere Clientinstallationsmethode, zum Beispiel die manuelle Installation (durch Ausführen von CCMSetup.exe) oder die auf Gruppenrichtlinien basierende Clientinstallation. Für diese alternativen Clientinstallationsmethoden sind weder SMB noch RPC erforderlich.  

 Informationen zum Konfigurieren der Windows-Firewall auf dem Clientcomputer finden Sie unter [Ändern der von der Windows-Firewall zugelassenen Ports und Programme](#BKMK_ModifyingWindowsFirewall).  

### <a name="ports-that-are-used-for-all-installation-methods"></a>Für alle Installationsmethoden verwendete Ports  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP (Hypertext Transfer Protocol) vom Clientcomputer zu einem Fallbackstatuspunkt, wenn dem Client ein Fallbackstatuspunkt zugewiesen wurde.|--|80 (siehe Hinweis 1, **Alternativer Port verfügbar**)|  

### <a name="ports-that-are-used-with-client-push-installation"></a>Mit der Clientpushinstallation verwendete Ports  
 Bei Clientpushinstallation werden nicht nur die in der folgenden Tabelle aufgeführten Ports, sondern auch ICMP-Echoanforderungsmeldungen vom Standortserver zum Clientcomputer verwendet. Mit diesen Meldungen wird überprüft, ob der Clientcomputer im Netzwerk verfügbar ist. ICMP (Internet Control Message Protocol) wird gelegentlich als „TCP/IP-Ping-Befehle“ bezeichnet. ICMP hat keine UDP- oder TCP-Protokollnummer und wird daher in der folgenden Tabelle nicht aufgeführt. Damit bei der Clientpushinstallation kein Fehler auftritt, muss ICMP-Datenverkehr von den beteiligten Netzwerkgeräten wie Firewalls zugelassen werden.  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|SMB-Datenverkehr (Server Message Block) zwischen Standortserver und Clientcomputer.|--|445|  
|RPC-Endpunktzuordnung zwischen Standortserver und Clientcomputer|135|135|  
|Dynamische RPC-Ports zwischen Standortserver und Clientcomputer|--|DYNAMISCH|  
|HTTP-Verbindung (Hypertext Transfer Protocol) vom Clientcomputer zu einem Verwaltungspunkt|--|80 (siehe Hinweis 1, **Alternativer Port verfügbar**)|  
|HTTPS-Verbindung (Secure Hypertext Transfer Protocol) vom Clientcomputer zu einem Verwaltungspunkt|--|443 (siehe Hinweis 1, **Alternativer Port verfügbar**)|  

### <a name="ports-that-are-used-with-software-update-point-based-installation"></a>Ports für die auf einem Softwareupdatepunkt basierende Installation  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP (Hypertext Transfer Protocol) vom Clientcomputer zum Softwareupdatepunkt|--|80 oder 8530 (siehe Hinweis 2, **Windows Server Update Services**)|  
|HTTPS (Secure Hypertext Transfer Protocol) vom Clientcomputer zum Softwareupdatepunkt|--|443 oder 8531 (siehe Hinweis 2, **Windows Server Update Services**)|  
|SMB-Datenverkehr (Server Message Block) zwischen dem Quellserver und dem Clientcomputer, wenn Sie die CCMSetup-Befehlszeileneigenschaft **/source:&lt;Pfad\>** festlegen.|--|445|  

### <a name="ports-that-are-used-with-group-policy-based-installation"></a>Ports für die auf einer Gruppenrichtlinie basierende Installation  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|HTTP-Verbindung (Hypertext Transfer Protocol) vom Clientcomputer zu einem Verwaltungspunkt|--|80 (siehe Hinweis 1, **Alternativer Port verfügbar**)|  
|HTTPS-Verbindung (Secure Hypertext Transfer Protocol) vom Clientcomputer zu einem Verwaltungspunkt|--|443 (siehe Hinweis 1, **Alternativer Port verfügbar**)|  
|SMB-Datenverkehr (Server Message Block) zwischen dem Quellserver und dem Clientcomputer, wenn Sie die CCMSetup-Befehlszeileneigenschaft **/source:&lt;Pfad\>** festlegen.|--|445|  

### <a name="ports-that-are-used-with-manual-installation-and-logon-script-based-installation"></a>Ports für die manuelle Installation oder die auf einem Anmeldeskript basierende Installation  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|SMB-Datenverkehr (Server Message Block) zwischen dem Clientcomputer und einer Netzwerkfreigabe, über die Sie CCMSetup.exe ausführen<br /><br /> Bei der Installation von Configuration Manager werden die Quelldateien für die Clientinstallation kopiert und automatisch im Ordner *&lt;Installationspfad\>* \Client auf Verwaltungspunkten freigegeben. Allerdings können Sie diese Dateien auch kopieren und eine neue Freigabe auf einen beliebigen Computer im Netzwerk erstellen. Sie können diesen Netzwerkverkehr aber auch vermeiden, indem Sie CCMSetup.exe lokal ausführen und z. B. Wechselmedien verwenden.|--|445|  
|HTTP-Verbindung (Hypertext Transfer Protocol) vom Clientcomputer zu einem Verwaltungspunkt, wenn die CCMSetup-Befehlszeileneigenschaft **/source:&lt;Pfad\>** nicht angegeben wird.|--|80 (siehe Hinweis 1, **Alternativer Port verfügbar**)|  
|HTTPS-Verbindung (Secure Hypertext Transfer Protocol) vom Clientcomputer zu einem Verwaltungspunkt, wenn die CCMSetup-Befehlszeileneigenschaft **/source:&lt;Pfad\>** nicht angegeben wird.|--|443 (siehe Hinweis 1, **Alternativer Port verfügbar**)|  
|SMB-Datenverkehr (Server Message Block) zwischen dem Quellserver und dem Clientcomputer, wenn Sie die CCMSetup-Befehlszeileneigenschaft **/source:&lt;Pfad\>** festlegen.|--|445|  

### <a name="ports-that-are-used-with-software-distribution-based-installation"></a>Ports für die auf einer Softwareverteilung basierende Installation  

|Beschreibung|UDP|TCP|  
|-----------------|---------|---------|  
|SMB-Datenverkehr (Server Message Block) zwischen Verteilungspunkt und Clientcomputer|--|445|  
|HTTP-Verbindung (Hypertext Transfer Protocol) vom Clientcomputer zu einem Verteilungspunkt|--|80 (siehe Hinweis 1, **Alternativer Port verfügbar**)|  
|HTTPS-Verbindung (Secure Hypertext Transfer Protocol) vom Clientcomputer zu einem Verteilungspunkt|--|443 (siehe Hinweis 1, **Alternativer Port verfügbar**)|  

## <a name="notes"></a>Hinweise  
 **1 Alternativer Port verfügbar** In Configuration Manager können Sie für diesen Wert einen alternativen Port angeben. Wenn ein benutzerdefinierter Port definiert wurde, ersetzen Sie diesen benutzerdefinierten Port, wenn Sie die IP-Filterinformationen für die IPsec-Richtlinien oder für die Konfiguration von Firewalls definieren.  

 **2 Windows Server Update Services** WSUS kann entweder auf der Standardwebsite (Port 80) oder auf einer benutzerdefinierten Website (Port 8530) installiert werden.  

 Sie können den Port nach der Installation ändern. Es ist nicht erforderlich, in der gesamten Standorthierarchie dieselbe Portnummer zu verwenden.  

 Wenn der HTTP-Port 80 verwendet wird, muss der HTTPS-Port 443 sein.  

 Wenn ein anderer HTTP-Port verwendet wird, muss der HTTPS-Port eine Nummer höher sein. Bei Port 8530 wäre dies z.B. Port 8531.
