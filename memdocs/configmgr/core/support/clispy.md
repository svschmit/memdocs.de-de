---
title: Client Spy
titleSuffix: Configuration Manager
description: Mit Client Spy können Sie Fehler in der Softwareverteilung, -inventur und der Softwaremessung auf Konfigurations-Manager-Clients beheben.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 60575413-44fe-43bb-bcfb-39ec5ed5055b
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 43c3d0f25cf9a71bf07189315ee5f11eba47de1d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707908"
---
# <a name="client-spy"></a>Client Spy

*Gilt für: Configuration Manager (Current Branch)*

Client Spy ist eines der [Configuration Manager-Tools](tools.md). Mit diesem Tool können Sie Fehler in der Softwareverteilung, -inventur und der Softwaremessung auf Konfigurations-Manager-Clients beheben. 

Der Großteil der Informationen, die von diesem Tool abgerufen werden, bezieht sich auf Softwarebereitstellungen:
- Alle aktuellen Softwarebereitstellungen 
- Softwareverteilung – Verlauf
- Konfigurieren des Clientcaches
- Zwischengespeicherte Elemente
- Ausstehende erforderliche Bereitstellungen
- Verfügbare Bereitstellungen  

Darüber hinaus werden folgende Inventurinformationen angezeigt:
- Das Datum des aktuellen Inventurzyklus
- Das letzte Berichtsdatum
- Haupt- und Nebenversionen der Softwareinventur
- Dateisammlung
- Hardwareinventur
- IDMIF-Sammlung
- DDRs (Discovery Data Records) 

Softwaremessungsregeln werden ebenfalls angezeigt. 

> [!Note]   
> Zur Leistungssteigerung sammelt das Tool nur Informationen für die einzelnen Registerkarten, wenn Sie diese auswählen. Gleichermaßen werden nur die Informationen für die derzeit angezeigte Registerkarte aktualisiert, wenn Sie auf **Aktualisieren** klicken.



## <a name="usage"></a>Verwendung


### <a name="tools-menu"></a>Menü „Extras“

Im Menü **Extras** sind die folgenden Aktionen verfügbar:  

#### <a name="connect"></a>Verbinden
Rufen Sie Informationen von einem anderen Computer ab.  

- Das Tool zeigt standardmäßig Informationen vom aktuellen Computer an. 

- Stellen Sie mit dem Namen des Remotecomputers, dem Benutzernamen und dem Kennwort für das Konto eine Verbindung her. Das Tool stellt eine Verbindung mit der IPC$-Freigabe auf dem Remotecomputer her. Es löscht die Verbindung, wenn das Tool beendet wird oder wenn Sie eine Verbindung mit einem anderen Computer herstellen.  

- Zum Abrufen der Informationen ist ein Konto mit ausreichenden Berechtigungen erforderlich.  

- Wenn Sie keinen Benutzernamen mit zugehörigem Kennwort angeben, versucht Client Spy, die Verbindung mithilfe des Sicherheitskontexts des derzeit angemeldeten Benutzers herzustellen.  

- Wenn Sie eine Verbindung mit einem Remotecomputer herstellen, werden auf allen angezeigten Registerkarten Informationen über den Remotecomputer angezeigt.

#### <a name="software-distribution"></a>Softwareverteilung
Zeigt die Registerkarte [Softwareverteilung](#software-distribution) an und blendet die anderen Registerkarten aus. Client Spy zeigt standardmäßig die Registerkarten für die Softwareverteilung an.

#### <a name="inventory"></a>Inventarisierung
Zeigt die Registerkarte „Inventur“ an und blendet die anderen Registerkarten aus.

#### <a name="software-metering"></a>Softwaremessung
Zeigt die Registerkarte „Softwaremessung“ an und blendet die anderen Registerkarten aus.

#### <a name="save-current-tab-to-file"></a>Aktuelle Registerkarte in Datei speichern
Speichert die Informationen auf der aktuell angezeigten Registerkarte in einer von Ihnen angegebenen Textdatei. 

#### <a name="save-all-tabs-to-file"></a>Alle Registerkarten in Datei speichern
Speichert die Informationen auf allen Registerkarten in einer von Ihnen angegebenen Textdatei. Es werden nur Informationen gespeichert, die in Ihrem Konto angezeigt werden können.



## <a name="software-distribution-tab"></a>Registerkarte „Softwareverteilung“

Konfigurieren Sie Einstellungen auf den folgenden vier Registerkarten:
- [Software Distribution Execution Requests](#bkmk_exec-requests) (Anforderungen zur Ausführung der Softwareverteilung)
- [Software Distribution History](#bkmk_history) (Softwareverteilungsverlauf)
- [Software Distribution Cache Information](#bkmk_cache-info) (Informationen zum Softwareverteilungscache)
- [Software Distribution Pending Executions](#bkmk_pending-exec) (Ausstehende Ausführungen der Softwareverteilung)


### <a name="software-distribution-execution-requests"></a><a name="bkmk_exec-requests"></a> Anforderungen zur Ausführung der Softwareverteilung

Auf dieser Registerkarte werden sämtliche vorhandenen Bereitstellungen angezeigt, einschließlich der beiden geräte- und benutzerorientierten Bereitstellungen.

Jedes Strukturelement auf der Registerkarte „Software Distribution Execution Requests“ (Anforderungen zur Ausführung der Softwareverteilung) enthält folgende vier Attribute:
- Ankündigungs-ID (Dieser Wert ist möglicherweise leer, wenn es sich um eine verfügbare Bereitstellung handelt.) 
- Paketkennung 
- Programmname 
- Benutzer (Dies ist möglicherweise die benutzerorientierte SID oder die SID des Benutzers, der die Anforderung initiiert hat. Wenn es sich bei beiden Anforderungen um Systemanforderungen handelt, ist „System“ der angezeigte Benutzer.) 

Bei jeder ausgeführten Anforderung werden die folgenden Informationen zudem in einer Unterstruktur angezeigt:
- Programmname 
- Paketkennung 
- Paketname 
- Erstellungszeit der Anforderung 
- Zustand 
- Ausführungsstatus, wenn der Status „Wird ausgeführt“ lautet 
- Ausführungskontext (Benutzer oder Administrator) 
- Verlaufszustand („Erfolg“, „Fehler“ oder „Nicht ausgeführt“) 
- Letzte Laufzeit („Nie“, wenn das Programm vorher noch nicht ausgeführt wurde) 
- Wiederholungsanzahl, wenn der Status „Warten auf Neuversuch“ lautet 
- Zugriff auf Inhalt (Wiederholungsanzahl, wenn der Status „Warten auf Neuversuch“ lautet) 
- Fehlercode, wenn der Status „Warten auf Neuversuch“ lautet 
- Fehlerursache, wenn der Status „Warten auf Neuversuch“ lautet 

Wenn Inhalte für die Anforderung erforderlich sind, lautet der Status „Warten auf Inhalt“. Auf der Registerkarte „Software Distribution Cache Information“ (Informationen zum Softwareverteilungscache) werden die Details zu dieser Downloadanforderung angezeigt.

Wenn es sich bei der Ausführungsanforderung um eine Downloadanforderung handelt, wird auch die Anzahl der heruntergeladenen Bytes angezeigt.

> [!Note]   
> Für die verschiedenen Status einer Ausführungsanforderung werden unterschiedliche Symbole verwendet.


### <a name="software-distribution-history"></a><a name="bkmk_history"></a> Softwareverteilungsverlauf

Diese Registerkarte enthält Informationen zu allen zuvor ausgeführten Programmen. Diese Informationen werden bei der Registrierung gespeichert.

Die Hauptverzweigungen dieser Struktur sind die anderen Benutzerverläufe, einschließlich „System“. Es wird eine Unterstruktur mit der Liste der Pakete angezeigt, aus denen für die einzelnen Benutzer Programme ausgeführt wurden. 

Die Paket-ID und der Paketname der einzelnen Paketunterstrukturen zeigen eine Liste der Programme an, die ausgeführt wurden. Es werden jeweils die folgenden Attribute angezeigt: 
- Programmname
- Ausführungsstatus
- Letzte Ausführungszeit
- Fehlercode
- Fehlerursache  

Der Fehlercode und die Fehlerursache sind leer, wenn ein Programm erfolgreich ausgeführt wurde.


### <a name="software-distribution-cache-information"></a><a name="bkmk_cache-info"></a> Informationen zum Softwareverteilungscache

#### <a name="cache-config"></a>Cachekonfiguration
Enthält Informationen zum Cache des Konfigurations-Manager-Clients. Diese Informationen umfassen den Cachespeicherort, die Cachegröße und die Angabe, ob der Cache derzeit verwendet wird. 

#### <a name="cached-items"></a>Zwischengespeicherte Elemente
Enthält eine Unterstruktur sämtlicher Elemente, die sich derzeit im Cache befinden. Jedes Strukturelement umfasst folgende Informationen zu den einzelnen Elementen: 
- Speicherort (Ordner) des Elements im Cache
- Aktueller Zustand
- Paketkennung
- Paketname
- Paketversion
- Paketgröße
- Aktuelle Referenzanzahl
- Zeitpunkt (UTC) der letzten Referenzierung  

#### <a name="downloading-items"></a>Elemente werden heruntergeladen
Dies sind die Elemente, die aktuell vom Client heruntergeladen werden. Jedes der Elemente zeigt die gleichen Informationen an, die von den zwischengespeicherten Elementen angezeigt werden, sowie die Anzahl der heruntergeladenen Kilobytes. 


### <a name="software-distribution-pending-executions"></a><a name="bkmk_pending-exec"></a> Ausstehende Ausführungen der Softwareverteilung

Diese Registerkarte enthält detaillierte Informationen zu vergangenen und zukünftigen erforderlichen Bereitstellungen sowie eine Liste der verfügbaren Bereitstellungen.

Die einzelnen Strukturverzweigungen sind für die jeweiligen Benutzerkonten mit Bereitstellungen verfügbar, einschließlich „System“.

Eine Unterstruktur enthält für jeden Benutzer die folgenden drei Elemente:  

#### <a name="mandatory-advertisements-with-future-executions"></a>Obligatorische Ankündigungen mit zukünftigen Ausführungen
Hierbei handelt es sich um obligatorische Ankündigungen, die noch auszuführende Programme beinhalten. Die Ankündigungen für Zeitpläne können periodisch, einmalig oder mehrmals erfolgen. Bei den einzelnen Ankündigungen werden die Ankündigungs-ID, die nächste Laufzeit und der Zeitplan angezeigt, für den die Ankündigungen ausgeführt werden. 

#### <a name="optional-advertisements"></a>Optionale Ankündigungen
Zeigt eine Liste sämtlicher veröffentlichten Ankündigungen an. Darüber hinaus werden jeweils Details wie Ankündigungs-ID, Programmname und Paketname angezeigt. 

#### <a name="past-mandatory-advertisements-with-no-future-scheduled-executions"></a>Vergangene obligatorische Ankündigungen ohne zukünftig geplante Ausführungen
Hierbei handelt es sich um eine Liste mit Ankündigungen, die auf dem Client vorhanden sind und keine zukünftig geplanten Programmausführungen beinhalten. Die Ankündigungs-ID, der Paketname und der Programmname werden angezeigt. Für alle optionalen Ankündigungen wird ein Unterstrukturelement angezeigt.

> [!Note]  
> Informationen zum Paketnamen sind nur für Pakete verfügbar, denen auf dem angezeigten Computer angekündigte Richtlinien zugeordnet wurden. Bei Paketen, denen keine verfügbaren Richtlinien mehr zugeordnet sind, wird die Nachricht „Der Paketname ist nicht mehr verfügbar“ angezeigt.  



## <a name="inventory-tab"></a>Registerkarte „Inventur“

Es gibt nur eine Registerkarte mit Inventurinformationen. Die Hauptstruktur enthält die folgenden fünf Elemente:  

- **Softwareinventur:** enthält das Datum, an dem der letzte Zyklus gestartet wurde, das Datum des letzten Berichts und die Neben- und Hauptversionen des letzten Berichts.  

- **Dateisammlung:** enthält das Datum, an dem der letzte Zyklus gestartet wurde, das Datum des letzten Berichts und die Neben- und Hauptversionen des letzten Berichts.  

- **Hardwareinventur:** enthält das Datum, an dem der letzte Zyklus gestartet wurde, das Datum des letzten Berichts und die Neben- und Hauptversionen des letzten Berichts.  

- **IDMIF-Sammlung:** enthält das Datum, an dem der letzte Zyklus gestartet wurde, das Datum des letzten Berichts und die Neben- und Hauptversionen des letzten Berichts.  

- **DDR:** enthält das Datum, an dem der letzte Zyklus gestartet wurde, das Datum des letzten Berichts und die Neben- und Hauptversionen des letzten Berichts. Die DDR-Informationen werden auch in einer Unterstruktur angezeigt.



## <a name="software-metering-tab"></a>Registerkarte „Softwaremessung“

Auf dieser Registerkarte werden Informationen als Unterstruktur angezeigt. Sie enthält sämtliche Softwaremessungsregeln. Jede Regel wird als Knoten angezeigt, der durch den Dateinamen und die Regel-ID identifiziert werden kann. Erweitern Sie die einzelnen Knoten in der Struktur, und zeigen Sie die folgenden Informationen an:
- Dateiname für Explorer 
- Ursprünglicher Dateiname
- Regel-ID
- Dateiversion
- Sprache


