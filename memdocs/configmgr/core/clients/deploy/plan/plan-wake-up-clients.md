---
title: Reaktivieren von Clients
titleSuffix: Configuration Manager
description: Planen Sie das Reaktivieren von Clients in Configuration Manager mit Wake-On-LAN (WOL).
ms.date: 04/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 52ee82b2-0b91-4829-89df-80a6abc0e63a
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: feea1cdea52b76b900497e84eea210444535fcd8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693768"
---
# <a name="plan-how-to-wake-up-clients-in-configuration-manager"></a>Planen des Reaktivierens von Clients in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

 Configuration Manager unterstützt herkömmliche Aktivierungspakete, um Computer im Energiesparmodus zu reaktivieren, wenn Sie erforderliche Software wie Softwareupdates und Anwendungen installieren möchten.

> [!NOTE]
> In diesem Artikel wird die Funktionsweise einer älteren Version von Wake-On-LAN beschrieben. Diese Funktion ist in Version 1810 von Configuration Manager noch vorhanden, die zudem eine neuere Version von Wake-On-LAN enthält. Beide Versionen von Wake-On-LAN können gleichzeitig aktiviert werden und werden auch oft gleichzeitig aktiviert. Weitere Informationen zur Funktionsweise der neuen Version von Wake-On-LAN ab Version 1810 sowie zum Aktivieren einer oder beider Versionen finden Sie unter [Konfigurieren von Wake-On-LAN in System Center Configuration Manager](../configure-wake-on-lan.md).  

## <a name="how-to-wake-up-clients-in-configuration-manager"></a>Reaktivieren von Clients in Configuration Manager

 Configuration Manager unterstützt herkömmliche Aktivierungspakete, um Computer im Energiesparmodus zu reaktivieren, wenn Sie erforderliche Software wie Softwareupdates und Anwendungen installieren möchten.  

Sie können die auf herkömmlichen Aktivierungspaketen beruhende Methode durch die Clienteinstellungen für den Aktivierungsproxy ergänzen. Vom Aktivierungsproxy wird mithilfe eines Peer-zu-Peer-Protokolls und ausgewählten Computern überprüft, ob andere Computer im Subnetz aktiv sind. Diese werden bei Bedarf dann aktiviert. Wenn der Standort für Wake-On-LAN konfiguriert ist und gleichzeitig Clients für den Aktivierungsproxy konfiguriert sind, gilt Folgendes:  

1. Von Computern, auf denen der Configuration Manager-Client installiert ist und die im Subnetz aktiv sind, wird geprüft, ob andere Computer im Subnetz aktiv sind. Diese Überprüfung wird durchgeführt, indem sich die Computer alle fünf Sekunden einen TCP/IP-Pingbefehl senden.  

2. Wenn keine Antwort von anderen Computern eingeht, wird davon ausgegangen, dass sie inaktiv sind. Die aktiven Computer werden als *Manager-Computer* des Subnetzes eingesetzt.  

    Nicht alle Computer, von denen keine Antwort eingeht, sind inaktiv. Manche wurden möglicherweise ausgeschaltet, aus dem Netzwerk entfernt oder die Clienteinstellung für den Aktivierungsproxy wird nicht mehr angewendet. Aus diesem Grund wird täglich ein Aktivierungspaket an die Computer gesendet, und zwar um 14:00 Uhr. lokale Zeit. Computer, von denen keine Antwort eingeht, werden nicht mehr als inaktiv eingestuft und nicht durch den Aktivierungsproxy aktiviert.  

    Zur Unterstützung des Aktivierungsproxys müssen in jedem Subnetz mindestens drei Computer aktiv sein. Um diese Anforderung zu erreichen, werden drei Computer auf nicht deterministische Weise als *Wächter-Computer* für das Subnetz ausgewählt. Dieser Zustand bedeutet, dass sie unabhängig von einer konfigurierten Energierichtlinie aktiv bleiben und nicht nach einer gewissen Zeit der Inaktivität in den Energiespar- oder Ruhemodus umgeschaltet werden. Befehle zum Herunterfahren oder Neustarten, die mit Wartungstasks zusammenhängen, werden von Wächter-Computern beachtet. Wenn diese Aktion eintritt, wird von den verbleibenden Wächter-Computern ein weiterer Computer im Subnetz aktiviert, damit das Subnetz weiterhin drei Wächter-Computer aufweist.  

3. Der Netzwerkswitch wird von den Manager-Computern angewiesen, den für die inaktiven Computer vorgesehenen Netzwerkverkehr zu den Manager-Computern umzuleiten.  

    Die Umleitung erfolgt durch den Manager-Computer, von dem ein Ethernet-Frame übertragen wird. Von diesem wird die MAC-Adresse des Computers, der sich im Ruhezustand befindet, als Quelladresse verwendet. Durch dieses Verhalten reagiert der Netzwerkswitch so, als ob der inaktive Computer auf den Port verschoben wurde, auf dem sich auch der Manager-Computer befindet. Vom Manager-Computer werden außerdem ARP-Pakete für die inaktiven Computer gesendet, damit der Eintrag im ARP-Cache aktuell bleibt. Darüber hinaus werden vom Manager-Computer im Auftrag des inaktiven Computers Antworten auf ARP-Anforderungen gesendet. Die Antwort erfolgt mit der MAC-Adresse des inaktiven Computers.  

   > [!WARNING]  
   >  Während dieses Vorgangs bleibt die IP-zu-MAC-Zuordnung für den inaktiven Computer bestehen. Der Netzwerkswitch wird über einen Aktivierungsproxy darüber informiert, dass der von einer Netzwerkkarte registrierte Port von einer anderen Netzwerkkarte verwendet wird. Dieses Verhalten wird als MAC-Flapping bezeichnet und ist bei Standardnetzwerkvorgängen nicht üblich. Von einigen Netzwerküberwachungstools wird geprüft, ob dieses Verhalten auftritt. Falls ja, werden Fehler angenommen. Durch diese Überwachungstools können also Warnungen generiert oder Ports heruntergefahren werden, wenn Sie einen Aktivierungsproxy verwenden.  
   >   
   >  Verwenden Sie keinen Aktivierungsproxy, wenn Ihre Netzwerküberwachungstools und -dienste kein MAC-Flapping zulassen.  

4. Wird von einem Manager-Computer eine neue TCP-Verbindungsanforderung für einen Computer erkannt, der sich im Ruhezustand befindet, und die Anforderung erfolgt an einem Port, der vom Computer vor den Wechsel in den Ruhezustand abgehört wurde, wird vom Manager-Computer ein Aktivierungspaket an den inaktiven Computer gesendet. Außerdem wird das Umleiten von Datenverkehr für diesen Computer beendet.  

5. Der inaktive Computer erhält das Aktivierungspaket und wird dadurch aktiviert. Vom sendenden Computer wird automatisch versucht, die Verbindung wiederherzustellen. Der Computer ist nun aktiv und kann antworten.  

   Für Aktivierungsproxys gelten die folgenden Voraussetzungen und Einschränkungen:  

> [!IMPORTANT]  
>  Wenn in Ihrem Unternehmen ein eigenes Team für die Netzwerkstruktur und die Netzwerkdienste verantwortlich ist, sollten Sie dieses Team informieren und während des Testzeitraums einbeziehen. Beispiel: In einem Netzwerk, von dem eine 802.1X-Zugriffssteuerung verwendet wird, funktioniert der Aktivierungsproxy nicht. Der Netzwerkdienst wird möglicherweise unterbrochen. Außerdem kann es durch den Aktivierungsproxy dazu kommen, dass von einigen Netzwerküberwachungstools Warnungen generiert werden, wenn Datenverkehr zur Aktivierung anderer Computer erkannt wird.  

-   Alle Windows-Betriebssysteme, die unter [Unterstützte Betriebssysteme für Clients und Geräte](../../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md) aufgeführt sind, werden für Wake-On-LAN unterstützt.  

-   Es werden keine Gastbetriebssysteme unterstützt, die auf einem virtuellen Computer ausgeführt werden.  

-   Die Clients müssen durch die Verwendung von Clienteinstellungen für den Aktivierungsproxy aktiviert sein. Zwar hängt der Vorgang des Aktivierungsproxys nicht von der Hardwareinventur ab, aber die Installation des Aktivierungsproxydiensts wird von Clients erst dann gemeldet, wenn sie für die Hardwareinventur aktiviert sind und von ihnen mindestens eine Hardwareinventur gesendet wurde.  

-   Für Aktivierungspakete müssen Netzwerkkarten (und möglichst das BIOS) aktiviert und konfiguriert sein. Ist die Netzwerkkarte nicht für Aktivierungspakete konfiguriert bzw. wurde diese Einstellung deaktiviert, wird sie von Configuration Manager automatisch konfiguriert und für einen Computer aktiviert, wenn die Clienteinstellung zum Aktivieren des Aktivierungsproxys empfangen wird.  

-   Verfügt ein Computer über mehrere Netzwerkkarten, können Sie nicht auswählen, welche Karte für den Aktivierungsproxy verwendet werden soll. Die Auswahl ist nicht deterministisch. Die ausgewählte Karte wird in der Datei „SleepAgent_<DOMÄNE\>@SYSTEM_0.log“ aufgezeichnet.  

-   Vom Netzwerk müssen ICMP-Echoanforderungen zugelassen werden, zumindest innerhalb des Subnetzes. Es ist nicht möglich, das Intervall von fünf Minuten zum Senden der ICMP-Pingbefehle zu konfigurieren.  

-   Die Kommunikation ist unverschlüsselt und nicht authentifiziert, und IPsec wird nicht unterstützt.  

-   Die folgenden Netzwerkkonfigurationen werden nicht unterstützt:  

    -   802.1 X mit Portauthentifizierung  

    -   Drahtlosnetzwerke  

    -   Netzwerkswitches, von denen MAC-Adressen an bestimmte Ports gebunden werden  

    -   Netzwerke, die nur IPv6 unterstützen  

    -   DHCP-Lease-Dauer von weniger als 24 Stunden  

Falls Sie Computer für eine geplante Softwareinstallation aktivieren möchten, müssen Sie jeden primären Standort für die Verwendung von Aktivierungspaketen konfigurieren.  

 Zur Verwendung eines Aktivierungsproxys müssen Sie in der Energieverwaltung die Clienteinstellungen für den Aktivierungsproxy bereitstellen und den primären Standort konfigurieren.  

Entscheiden Sie, ob subnetzgesteuerte Broadcastpakete oder Unicastpakete verwendet werden sollen und welche UDP-Portnummer angegeben werden soll. Herkömmliche Aktivierungspakete werden standardmäßig über UDP-Port 9 übertragen. Zur Steigerung der Sicherheit können Sie aber für den Standort einen anderen Port auswählen, sofern dieser Port von beteiligten Routern und Firewalls unterstützt wird.  

## <a name="choose-between-unicast-and-subnet-directed-broadcast-for-wake-on-lan"></a>Auswahl zwischen Unicast und subnetzgesteuerten Broadcasts für Wake-On-LAN  
 Falls Sie sich für die Aktivierung von Computern mit herkömmlichen Aktivierungspaketen entscheiden, müssen Sie angeben, ob Unicastpakete oder subnetzgesteuerte Broadcastpakete übertragen werden sollen. Wenn Sie einen Aktivierungsproxy nutzen, müssen Sie Unicastpakete verwenden. Orientieren Sie sich andernfalls bei der Auswahl der Übertragungsmethode an der folgenden Tabelle.  

|Übertragungsmethode|Vorteil|Nachteil|  
|-------------------------|---------------|------------------|  
|Unicast|Diese Lösung ist sicherer als subnetzgesteuerte Broadcasts, weil das Paket nicht an alle Computer in einem Subnetz, sondern direkt an einen Computer gesendet wird.<br /><br /> Eine Neukonfiguration der Router ist möglicherweise nicht erforderlich (Sie müssen eventuell den ARP-Cache konfigurieren).<br /><br /> Belegt weniger Netzwerkbandbreite als subnetzgesteuerte Broadcasts.<br /><br /> Unterstützt mit IPv4 und IPv6.|Zielcomputer, deren Subnetzadresse seit der letzten geplanten Hardwareinventur geändert wurde, werden von Aktivierungspaketen nicht gefunden.<br /><br /> Es müssen möglicherweise Switches zum Weiterleiten der UDP-Pakete konfiguriert werden.<br /><br /> Bei manchen Netzwerkadapter ist die Aktivierung durch Aktivierungspakete möglicherweise nicht in allen Ruhezuständen möglich, wenn als Übertragungsmethode Unicast verwendet wird.|  
|Subnetzgesteuerte Broadcasts|Höhere Erfolgsrate als Unicast, wenn die IP-Adressen einiger Computer innerhalb des gleichen Subnetzes sich oft ändern<br /><br /> Keine Switchneukonfiguration erforderlich<br /><br /> Hohe Kompatibilitätsrate mit Computernetzwerkkarten in allen Ruhezuständen, weil subnetzgesteuerte Broadcasts die Originalübertragungsmethode zum Senden von Reaktivierungspaketen sind|Diese Lösung ist weniger sicher als Unicast, da von einem Angreifer kontinuierlich ICMP-Echoanforderungen von einer gefälschten Quelladresse an die gesteuerte Broadcastadresse gesendet werden könnten. Dies führt dazu, dass von allen Hosts Antworten an diese Quelladresse gesendet werden. Wenn Router für die Verwendung subnetzgesteuerter Broadcasts konfiguriert sind, wird die folgende zusätzliche Konfiguration aus Sicherheitsgründen empfohlen:<br /><br /> - Konfigurieren Sie Router so, dass sie nur IP-gesteuerte Broadcasts vom Configuration Manager-Standortserver zulassen. Verwenden Sie hierzu die angegebene UDP-Portnummer.<br />- Konfigurieren Sie Configuration Manager so, dass die angegebene, nicht standardmäßige Portnummer verwendet wird.<br /><br /> Erfordert möglicherweise die Neukonfiguration aller beteiligten Router, damit subnetzgesteuerte Broadcasts möglich werden.<br /><br /> Belegt mehr Netzwerkbandbreite als Unicast-Übertragungen.<br /><br /> Nur mit IPv4 unterstützt, keine Unterstützung für IPv6.|  

> [!WARNING]  
>  Subnetzgesteuerte Broadcasts sind mit Sicherheitsrisiken verbunden: Von einem Angreifer könnten kontinuierlich ICMP-Echoanforderungen (Internet Control Message Protocol) von einer gefälschten Quelladresse an die gesteuerte Broadcastadresse gesendet werden. Dies würde dazu führen, dass von allen Hosts Antworten an diese Quelladresse gesendet werden. Diese Art von DoS-Angriff wird allgemein als „Smurf Attack“ bezeichnet und üblicherweise dadurch verhindert, dass keine subnetzgesteuerten Broadcasts zugelassen werden.
