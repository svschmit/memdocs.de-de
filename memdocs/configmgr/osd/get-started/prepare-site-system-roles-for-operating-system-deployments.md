---
title: Vorbereiten von Standortsystemrollen für die Betriebssystembereitstellung
titleSuffix: Configuration Manager
description: Konfigurieren Sie die Standortsystemrollen vor der Bereitstellung von Betriebssystemen in Configuration Manager.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 0ef5f3ce-b0e4-4775-b5c2-b245e45b4194
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1beec2f5ef7b6da9f1f093300ec6c2b239e7396e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81708798"
---
# <a name="prepare-site-system-roles-for-os-deployments-with-configuration-manager"></a>Vorbereiten von Standortsystemrollen für Betriebssystembereitstellungen mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Zum Bereitstellen von Betriebssystemen in Configuration Manager müssen Sie zuerst die unten stehenden Standortsystemrollen vorbereiten. Für diese sind besondere Konfigurationen und Überlegungen erforderlich.



##  <a name="distribution-points"></a><a name="BKMK_DistributionPoints"></a> Verteilungspunkte  

Die Standortsystemrolle des Verteilungspunkts hostet Quelldateien, die von Clients heruntergeladen werden können. Dieser Inhalt ist für Anwendungen, Softwareupdates, Betriebssystemimages, Startimages und Treiberpakete vorgesehen. Sie können die Inhaltsverteilung mithilfe der Optionen für die Bandbreite, Bandbreiteneinschränkung und Zeitplanung steuern.  

Sie benötigen unbedingt genügend Verteilungspunkte, um die Bereitstellung von Betriebssystemen auf Computern zu unterstützen. Außerdem ist es wichtig, die Platzierung dieser Verteilungspunkte in Ihrer Hierarchie zu planen. Weitere Informationen finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md). Dieser Artikel enthält einige zusätzliche Überlegungen zur Planung von Verteilungspunkten, die sich auf die Betriebssystembereitstellung beziehen.  


###  <a name="additional-planning-considerations-for-distribution-points"></a><a name="BKMK_AdditionalPlanning"></a> Zusätzliche Überlegungen zur Planung von Verteilungspunkten  

Im Folgenden sind weitere Aspekte aufgeführt, die bei der Planung von Verteilungspunkten berücksichtigt werden sollten:  

#### <a name="how-can-i-prevent-unwanted-os-deployments"></a>Wie lassen sich unerwünschte Betriebssystembereitstellungen verhindern?  
Configuration Manager unterscheidet nicht zwischen Standortservern von anderen Zielcomputern in einer Sammlung. Wenn Sie eine erforderliche Tasksequenz für eine Sammlung bereitstellen, die einen Standortserver enthält, wird die Tasksequenz genauso wie auf allen anderen Computern in der Sammlung ausgeführt. Stellen Sie sicher, dass Ihre Betriebssystembereitstellung eine Sammlung verwendet, die die vorgesehenen Clients enthält.  

Verwalten Sie das Verhalten für Tasksequenzbereitstellungen mit hohem Risiko. Eine Bereitstellung mit hohem Risiko wird automatisch auf einem Client installiert und kann zu unerwünschten Ergebnissen führen. Ein Beispiel ist eine Tasksequenz, die als Zweck „Erforderlich“ aufweist und ein Betriebssystem bereitstellt. Konfigurieren Sie Einstellungen zur Bereitstellungsüberprüfung, um das Risiko einer unbeabsichtigten Bereitstellung mit hohem Risiko zu reduzieren. Weitere Informationen finden Sie unter [Settings to manage high-risk deployments (Einstellungen zum Verwalten risikoreicher Bereitstellungen)](../../core/servers/manage/settings-to-manage-high-risk-deployments.md).  

#### <a name="how-many-computers-can-receive-an-os-image-at-one-time-from-a-single-distribution-point"></a>Wie viele Computer können gleichzeitig ein Betriebssystemimage von einem einzelnen Verteilungspunkt empfangen?  
Um einschätzen zu können, wie viele Verteilungspunkte Sie benötigen, berücksichtigen Sie die folgenden Variablen:  
- Die Prozessorgeschwindigkeit des Verteilungspunkts
- Die Datenträgergeschwindigkeit des Verteilungspunkts
- Die verfügbare Bandbreite auf dem Netzwerk
- Der Größe des Imagepakets   
  
Wenn Sie beispielsweise keine anderen Serverressourcenfaktoren berücksichtigen, können maximal elf Computer ein Imagepaket mit der Größe von 4 GB in einem Ethernet-Netzwerk mit 100 MBit/s in einer Stunde verarbeiten.  

`100 megabits/sec = 12.5 megabytes/sec = 750 megabytes/min = 45 gigabytes/hour = 11 images @ 4 GB per image`  

Falls die Bereitstellung eines Betriebssystems also innerhalb eines bestimmten Zeitrahmens auf einer bestimmten Anzahl von Computern erfolgen muss, verteilen Sie das Image auf eine geeignete Anzahl von Verteilungspunkten.  

#### <a name="can-i-deploy-an-os-to-a-distribution-point"></a>Kann ein Betriebssystem auf einem Verteilungspunkt bereitgestellt werden?  
Sie können ein Betriebssystem auf einem Verteilungspunkt bereitstellen, allerdings muss das Betriebssystemimage von einem anderen Verteilungspunkt empfangen werden.  


###  <a name="configuring-distribution-points-to-accept-pxe-requests"></a><a name="BKMK_PXEDistributionPoint"></a> Konfigurieren von Verteilungspunkten zum Akzeptieren von PXE-Anforderungen  

Zum Bereitstellen von Betriebssystemen für Konfigurations-Manager-Clients, die PXE-Startanforderungen senden, müssen Sie mindestens einen Verteilungspunkt so konfigurieren, dass er PXE-Anforderungen akzeptiert. Sobald der Verteilungspunkt konfiguriert ist, reagiert er auf PXE-Startanforderungen und ermittelt die geeigneten Bereitstellungsaktionen. Weitere Informationen finden Sie unter [Installieren oder Modifizieren eines Verteilungspunkts](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-pxe).  


###  <a name="customize-the-ramdisk-tftp-block-and-window-sizes-on-pxe-enabled-distribution-points"></a><a name="BKMK_RamDiskTFTP"></a> Anpassen der RamDisk-TFTP-Blockgröße und der Fenstergröße auf PXE-fähigen Verteilungspunkten  

Sie können die Größe des RamDisk-TFTP-Blocks und des Fensters für PXE-fähige Verteilungspunkte anpassen. Wenn Sie Ihr Netzwerk angepasst haben, kann eine übermäßige Block- oder Fenstergröße zu einem Timeout beim Herunterladen des Startimages führen. Durch Anpassen der Größe des RamDisk-TFTP-Blocks und des Fensters können Sie den TFTP-Datenverkehr bei Verwendung von PXE für Ihre spezifischen Netzwerkanforderungen optimieren. Um die effizienteste Einstellung zu ermitteln, müssen Sie die benutzerdefinierten Einstellungen in Ihrer Umgebung testen.  

-   **TFTP-Blockgröße:** Die Blockgröße ist die Größe der Datenpakete, die vom Server an den Client gesendet werden, der die Datei herunterlädt. Mit einer größeren Blockgröße kann der Server weniger Pakete senden, sodass weniger Roundtripverzögerungen zwischen dem Server und dem Client auftreten. Große Blöcke führen jedoch zu fragmentierten Paketen, die von den meisten PXE-Clientimplementierungen nicht unterstützt werden.  

-   **TFTP-Fenstergröße:** TFTP erfordert ein Bestätigungspaket (acknowledgment packet; ACK) für jeden gesendeten Datenblock. Der Server sendet den nächsten Block in der Sequenz erst, wenn er das ACK-Paket für den vorherigen Block empfangen hat. Mithilfe von TFTP-Fenstern können Sie definieren, wie viele Datenblöcke Sie zum Füllen eines Fensters benötigen. Der Server sendet die Datenblöcke nach dem Back-to-Back-Prinzip, bis das Fenster gefüllt ist. Anschließend sendet der Client ein ACK-Paket. Durch Erhöhen diese Fenstergröße reduzieren Sie die Anzahl von Roundtripverzögerungen zwischen Client und Server und verringern die Gesamtzeit, die zum Herunterladen eines Startimages erforderlich ist.  
  

#### <a name="modify-the-ramdisk-tftp-window-size"></a>Ändern der RamDisk-TFTP-Fenstergröße  
Fügen Sie auf PXE-fähigen Verteilungspunkten den folgenden Registrierungsschlüssel hinzu, um die RamDisk-TFTP-Fenstergröße anzupassen:  

- **Speicherort**: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP`  
- **Name:** RamDiskTFTPWindowSize  
- **Typ:** REG_DWORD  
- **Wert**: (angepasste Fenstergröße)  
    - Der Standardwert ist **1** (ein Datenblock füllt das Fenster aus).  

#### <a name="modify-the-ramdisk-tftp-block-size"></a>Ändern der RamDisk-TFTP-Blockgröße  
Fügen Sie auf PXE-fähigen Verteilungspunkten den folgenden Registrierungsschlüssel hinzu, um die RamDisk-TFTP-Fenstergröße anzupassen:  

- **Speicherort**: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SMS\DP`  
- **Name:** RamDiskTFTPBlockSize  
- **Typ:** REG_DWORD  
- **Wert**: (angepasste Blockgröße)  
    - Der Standardwert lautet **4096**.  

> [!Note]  
> Sowohl Windows-Bereitstellungsdienste als auch der Configuration Manager-PXE-Antwortdienst unterstützen diese TFTP-Konfigurationen.  


###  <a name="configure-distribution-points-to-support-multicast"></a><a name="BKMK_DPMulticast"></a> Konfigurieren von Verteilungspunkten für die Multicastunterstützung  

Multicast ist eine Methode zur Netzwerkoptimierung. Sie können sie auf Verteilungspunkten verwenden, wenn mehrere Clients mit hoher Wahrscheinlichkeit gleichzeitig dasselbe Betriebssystemimage herunterladen. Wenn Sie Multicast verwenden, können mehrere Computer gleichzeitig das Betriebssystemimage herunterladen, da es vom Verteilungspunkt über Multicast gesendet wird. Ohne Multicast sendet der Verteilungspunkt eine Kopie der Daten an jeden Client über eine separate Verbindung. Weitere Informationen finden Sie unter [Verwenden von Multicast zum Bereitstellen von Windows über das Netzwerk](../deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

Sie müssen einen Verteilungspunkt für die Multicastunterstützung konfigurieren, bevor Sie das Betriebssystem bereitstellen. Weitere Informationen finden Sie unter [Installieren und Konfigurieren von Verteilungspunkten](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_config-multicast).



##  <a name="state-migration-point"></a><a name="BKMK_StateMigrationPoints"></a> Zustandsmigrationspunkt  

Vom Zustandsmigrationspunkt werden die vom Migrationstool für den Benutzerstatus (USMT) auf einem Computer erfassten Benutzerdaten gespeichert und anschließend auf einem anderen Computer wiederhergestellt. Wenn Sie jedoch Benutzereinstellungen für eine Betriebssystembereitstellung auf dem gleichen Computer erfassen, z.B. zur Aktualisierung von Windows auf dem Zielcomputer, können Sie die Daten auf dem gleichen Computer unter Verwendung von festen Links oder auf dem Zustandsmigrationspunkt speichern. Wenn Sie den Statusspeicher erstellen, wird von Configuration Manager bei einigen Computerbereitstellungen automatisch eine Zuordnung zwischen Statusspeicher und Zielcomputer erstellt. Berücksichtigen Sie bei der Planung des Zustandsmigrationspunkts die folgenden Faktoren:    


### <a name="user-state-size"></a>Größe des Benutzerzustands  

Die Größe des Benutzerzustands hat direkte Auswirkungen auf den Speicherplatz auf dem Zustandsmigrationspunkt und die Netzwerkleistung während der Migration. Berücksichtigen Sie die Größe des Benutzerzustands und die Anzahl der zu migrierenden Computer. Überlegen Sie genau, welche Einstellungen vom Computer migriert werden müssen. Wenn beispielsweise bereits eine Sicherungskopie des Ordners **Eigene Dateien** auf einem Server erstellt wurde, braucht dieser Ordner im Rahmen der Imagebereitstellung möglicherweise nicht migriert zu werden. Durch Vermeidung unnötiger Migrationen wird die Gesamtgröße des Benutzerzustands kleiner gehalten, und die Auswirkung auf die Netzwerkleistung und den Speicherplatz auf dem Zustandsmigrationspunkt wird verringert.  


### <a name="user-state-migration-tool"></a>Windows-EasyTransfer (früher USMT)  

Sie müssen ein USMT-Paket (Windows-Migrationstool für den Benutzerstatus) verwenden, in dem auf USMT-Quelldateien verwiesen wird, um den Benutzerzustand während der Betriebssystembereitstellung erfassen und wiederherstellen zu können. Configuration Manager erstellt dieses Paket in der Configuration Manager-Konsole unter **Softwarebibliothek** > **Anwendungsverwaltung** > **Pakete**. Configuration Manager verwendet USMT 10, um den Benutzerzustand von einem Betriebssystem zu erfassen und auf einem anderen Betriebssystem wiederherzustellen. Das Windows Assessment and Deployment Kit (Windows ADK) für Windows 10 enthält USMT 10.

Eine Beschreibung verschiedener Migrationsszenarios für USMT 10 finden Sie unter [Häufige Migrationsszenarios](https://docs.microsoft.com/windows/deployment/usmt/usmt-common-migration-scenarios) in der Windows-Dokumentation.  


### <a name="retention-policy"></a>Aufbewahrungsrichtlinie  

Geben Sie beim Konfigurieren des Zustandsmigrationspunkts an, wie lange die auf dem Statusmigrationspunkt gespeicherten Benutzerzustandsdaten beibehalten werden sollen. Die Beibehaltungsdauer der auf dem Zustandsmigrationspunkt gespeicherten Daten hängt von zwei Faktoren ab:  

-   Auswirkung der gespeicherten Daten auf den Speicherplatz  

-   Mögliche Anforderung zur längeren Beibehaltung der Daten für den Fall, dass diese erneut migriert werden müssen  
  
  
Die Zustandsmigration erfolgt in zwei Phasen: Erfassen der Daten und Wiederherstellen der Daten. Wenn Sie Daten erfassen, werden die Benutzerzustandsdaten gesammelt und auf dem Zustandsmigrationspunkt gespeichert. Wenn Sie die Daten wiederherstellen, werden die Benutzerzustandsdaten vom Zustandsmigrationspunkt abgerufen und auf den Zielcomputer geschrieben. Anschließend werden die gespeicherten Daten mithilfe des Tasksequenzschritts **Zustandsspeicher freigeben** freigegeben. Sobald die Daten freigegeben sind, wird der Beibehaltungszeitgeber gestartet. Wenn Sie die Option zum sofortigen Löschen der migrierten Daten ausgewählt haben, werden die Benutzerzustandsdaten sofort nach der Freigabe gelöscht. Wenn Sie die Option zum zeitlich begrenzten Beibehalten der Daten ausgewählt haben, werden die freigegebenen Daten nach Ablauf des festgelegten Zeitraums gelöscht. Je länger der festgelegte Beibehaltungszeitraum ist, desto mehr Speicherplatz wird voraussichtlich benötigt.  


### <a name="select-drive-to-store-user-state-migration-data"></a>Auswählen des Laufwerks zum Speichern von Daten zur Benutzerzustandsmigration  

Wenn Sie den Zustandsmigrationspunkt konfigurieren, müssen Sie das Laufwerk auf dem Server angeben, auf dem die Benutzerzustands-Migrationsdaten gespeichert werden. Die Auswahl des Laufwerks erfolgt über eine vorgegebene Liste von Laufwerken. Einige dieser Laufwerke sind jedoch möglicherweise schreibgeschützte Laufwerke (z. B. CD-Laufwerke) oder Laufwerke ohne Netzwerkfreigabe. Einige der Laufwerkbuchstaben sind möglicherweise überhaupt keinem Laufwerk auf dem Computer zugeordnet. Wenn Sie den Zustandsmigrationspunkt konfigurieren, geben Sie ein beschreibbares, freigegebenes Laufwerk an.  


### <a name="configure-a-state-migration-point"></a>Konfigurieren eines Zustandsmigrationspunkts  

Mithilfe der folgenden Methoden können Sie einen Zustandsmigrationspunkt zum Speichern der Benutzerzustandsdaten konfigurieren:  

-   Verwenden Sie den **Assistenten zum Erstellen von Standortsystemservern**, um einen neuen Standortsystemserver für den Zustandsmigrationspunkt zu erstellen.  

-   Verwenden Sie den **Assistenten zum Hinzufügen von Standortsystemrollen**, um einem vorhandenen Server einen Zustandsmigrationspunkt hinzuzufügen.  

Wenn Sie diese Assistenten verwenden, werden Sie aufgefordert, die folgenden Angaben zum Zustandsmigrationspunkt zu machen:  

-   Die Ordner, in denen die Benutzerzustandsdaten gespeichert werden  

-   Die maximale Anzahl von Clients, von denen Daten auf dem Zustandsmigrationspunkt gespeichert werden können  

-   Der für einen Zustandsmigrationspunkt zum Speichern der Benutzerzustandsdaten mindestens erforderliche freie Speicherplatz  

-   Die Löschrichtlinie für die Rolle. Sie können angeben, ob die Benutzerzustandsdaten nach deren Wiederherstellung auf einem Computer entweder unmittelbar danach oder erst nach einer bestimmten Anzahl von Tagen gelöscht werden sollen.  

-   Ob vom Zustandsmigrationspunkt nur Anforderungen zum Wiederherstellen von Benutzerzustandsdaten beantwortet werden. Wenn Sie diese Option aktivieren, können Sie den Zustandsmigrationspunkt nicht zum Speichern von Benutzerzustandsdaten verwenden.  

Die Schritte zum Installieren einer Standortsystemrolle finden Sie unter [Hinzufügen von Standortsystemrollen](../../core/servers/deploy/configure/add-site-system-roles.md).  
