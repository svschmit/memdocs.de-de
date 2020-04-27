---
title: Remoteaktionen mit Co-Verwaltung
titleSuffix: Configuration Manager
description: Ausführen von Remoteaktionen aus Intune für gemeinsam verwaltete Geräte
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 4a877bed-f6c4-4048-9421-507dc848af5c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0ca37a4e15f5da63ed743b541eeabc43708b0be1
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075318"
---
# <a name="remote-actions-with-co-management"></a>Remoteaktionen mit Co-Verwaltung

Sie müssen sicherstellen, dass jedes von Ihnen verwaltete Gerät erreichbar ist (egal wo es sich befindet), wenn es eine Verbindung herstellt. Außerdem müssen Sie jedem Benutzer alles zur Verfügung stellen, was er benötigt, um produktiv zu bleiben, und gleichzeitig die Anwendungen und Daten schützen. Mit den von Intune unterstützten Geräteaktionen können Sie diese wichtigen Funktionen remote ausführen.

Im folgenden Video erläutern und zeigen Principal Program Manager Heidi Cheng und Senior Program Manager Danny Guillory Remoteaktionen mit Co-Verwaltung:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Co-Management-to-Execute-Remote-Actions/player]



## <a name="benefits"></a>Vorteile

Durch Remotegeräteaktionen erhalten Sie Verwaltungskontrolle auf dem Gerät, ohne die personenbezogenen Daten zu beeinträchtigen. Diese Remotegeräteaktionen ermöglichen Folgendes: 
- Löschen von Unternehmensdaten auf verlorenen oder gestohlenen Geräten  
- Umbenennen eines Geräts  
- Neustarten eines Geräts  
- Überprüfen des Gerätebestands  
- Remotesteuern eines Geräts  
- Löschen vorinstallierter OEM-Apps mit einem sauberen Neustart  
- Zurücksetzung auf die Werkseinstellungen auf einem beliebigen Windows 10-Gerät  

Diese Funktionen sind eine wichtige und einfache Möglichkeit, die auf diesen Geräten gespeicherten Unternehmensdaten zu schützen, sei es in E-Mails oder OneDrive.

Weitere Informationen zu diesen Aktionen finden Sie unter [Verfügbare Remoteaktionen](#available-remote-actions). 



## <a name="case-studies"></a>Fallstudien

Das weltweit tätige Beratungsunternehmen Avanade setzt regelmäßig Remoteaktionen ein, um die von seinen 30.000 Mitarbeitern verwendeten Geräte zu verwalten. In einem [kürzlich erschienenen Blogbeitrag](https://www.microsoft.com/microsoft-365/blog/2018/02/07/the-future-is-on-the-other-side-of-this-bridge/) hat der CIO von Avanade Folgendes angemerkt:

> *Unser unmittelbarer Gewinn aus der Intune-Funktionalität war die Möglichkeit, Windows auf einem Computer remote zurückzusetzen. Dies ist wichtig für uns bei verlorenen oder gestohlenen Computern, was bei unseren hochmobilen Mitarbeitern häufiger der Fall ist.* 
> *Dies ist Funktionalität, die wir sonst in einem benutzerdefinierten ConfigMgr-Paket hätten erstellen und verwalten müssen.*

Weitere Informationen dazu, wie diese Remoteaktionen verwendet werden, finden Sie unter [Verfügbare Geräteaktionen](../../intune/remote-actions/device-management.md#available-device-actions).


## <a name="value-proposition"></a>Leistungsversprechen

Wenn ein Configuration Manager-Gerät gemeinsam verwaltet wird, fügt es sofort diese Funktionen hinzu, über die Configuration Manager nicht nativ verfügt. Jetzt können Sie alle Remoteaktion ausführen, die von Intune unterstützt werden. 

Mit Co-Verwaltung verhalten sich die Configuration Manager-Geräte nun wie jedes andere von Intune verwaltete Gerät. Beispielsweise sind sie vollständig in der Cloud präsent und können erreicht werden, sofern sie über Internetzugang verfügen. Sie können alle diese Aktionen durchführen, ohne zusätzliche Schritte über die Aktivierung der Co-Verwaltung hinaus zu unternehmen.

Da der automatische Registrierungsvorgang für den Benutzer transparent ist, besitzt er keinen Einfluss auf seine Produktivität. Der Benutzer muss keine weiteren Maßnahmen ergreifen.


### <a name="available-remote-actions"></a>Verfügbare Remoteaktionen

Verwenden Sie die folgenden Remoteaktionen aus Intune, sobald Sie in Configuration Manager [Co-Verwaltung aktiviert](how-to-enable.md) haben.

#### <a name="remove-devices"></a>Entfernen von Geräten
- **Außer Betrieb nehmen**: Diese Aktion entfernt verwaltete Apps und Daten (falls zutreffend), Einstellungen und E-Mail-Profile, die diesem Gerät zugewiesen wurden. Das Gerät wird anschließend aus der Intune-Verwaltung entfernt. Dieser Prozess findet bei der nächsten Anmeldung des Geräts statt, wenn es die Remoteaktion zur Außerbetriebnahme empfängt. Die Funktion zur Außerbetriebnahme belässt die persönlichen Daten des Benutzers auf dem Gerät.  

- **Zurücksetzen**: Diese Aktion setzt ein Gerät auf die werkseitigen Standardeinstellungen zurück. Wenn Sie die Option **Registrierungszustand und Benutzerkonto beibehalten** auswählen, werden die Benutzerdaten beibehalten. Andernfalls wird das Laufwerk sicher gelöscht.  

- **Löschen** Wenn Sie Geräte aus Intune im Azure-Portal entfernen möchten, löschen Sie sie aus dem jeweiligen Gerätebereich. Das nächste Mal, wenn sich das Gerät anmeldet, werden alle darauf gespeicherten Unternehmensdaten entfernt.  

Weitere Informationen finden Sie unter [Entfernen von Geräten durch Zurücksetzen, Außerbetriebnahme oder manuelles Aufheben der Registrierung des Geräts](../../intune/remote-actions/devices-wipe.md).

#### <a name="selective-wipe"></a>Selektives Zurücksetzen
<!--SCCMDocs issue 973-->
Wenn Sie eine **Selektive App-Zurücksetzung** auswählen, werden App-Unternehmensdaten entfernt, persönliche Daten hingegen nicht. Verwenden Sie diese Aktion, wenn ein Gerät als verloren oder gestohlen gemeldet wird. 

Weitere Informationen finden Sie unter [How to wipe only corporate data from Intune-managed apps](../../intune/apps/apps-selective-wipe.md) (Zurücksetzen nur von Unternehmensdaten aus mit Intune verwalteten Apps).

#### <a name="sync"></a>Sync
Die Geräteaktion **Synchronisieren** zwingt das ausgewählte Gerät, sich sofort bei Intune anzumelden. Wenn sich ein Gerät anmeldet, empfängt es sofort alle ausstehenden Aktionen oder Richtlinien, die Sie ihm zugewiesen haben.

Diese Funktion kann Ihnen dabei helfen, die von Ihnen zugewiesenen Richtlinien sofort zu überprüfen und Probleme zu behandeln, ohne auf die nächste geplante Anmeldung zu warten.

Weitere Informationen finden Sie unter [Synchronisieren von Geräten, um die neuesten Richtlinien und Aktionen mit Intune abzurufen](../../intune/remote-actions/device-sync.md).

#### <a name="restart"></a>Neu starten
Die Geräteaktion **Neu starten** bewirkt, dass das ausgewählte Gerät neu gestartet wird. Diese Aktion ist sinnvoll, wenn ein Neustart aussteht, der Benutzer aber nicht verfügbar ist, um ihn durchzuführen.

Weitere Informationen finden Sie unter [Remoteneustart von Geräten mit Intune](../../intune/remote-actions/device-restart.md).

#### <a name="fresh-start"></a>Sauber starten
Die Geräteaktion **Sauber starten** entfernt alle Apps, die auf einem Gerät mit Windows 10, Version 1703 oder höher, installiert sind. Mit „Sauber starten“ können vorinstallierte Apps (OEM-Apps) entfernt werden, die typischerweise auf einem neuen Gerät installiert werden.

Wenn Sie sich dafür entscheiden, die Benutzerdaten nicht beizubehalten, stellt das Gerät seinen Ausgangszustand wieder her. Es hebt die Registrierung bei Azure AD und MDM auf.

Wenn Sie vorgegebene Standards dafür haben, welche Apps auf dem Gerät installiert werden sollten, dann beseitigt diese Aktion diejenigen Apps, die nicht Ihren Kriterien entsprechen.

Weitere Informationen finden Sie unter [Verwenden von „Sauber starten“ zum Zurücksetzen von Windows 10-Geräten mit Intune](../../intune/remote-actions/device-fresh-start.md). 

#### <a name="remote-control"></a>Remotesteuerung
Von Intune verwaltete Geräte können mit [TeamViewer](https://www.teamviewer.com/) remote verwaltet werden. TeamViewer ist ein Drittanbieterprogramm, das Sie separat erwerben.

Weitere Informationen finden Sie unter [Verwenden von TeamViewer für die Remoteverwaltung von Intune-Geräten](../../intune/remote-actions/teamviewer-support.md).



## <a name="configure"></a>Konfigurieren

Abgesehen von der Remotesteuerung über TeamViewer ist für die Verwendung dieser Remotegeräteaktionen in Intune keine zusätzliche Einrichtung erforderlich, nachdem Sie [Co-Verwaltung](how-to-enable.md) aktiviert haben.

Weitere Informationen zur Verwendung von TeamViewer für die Remotesteuerung finden Sie unter [Verwenden von TeamViewer für die Remoteverwaltung von Intune-Geräten](../../intune/remote-actions/teamviewer-support.md).
