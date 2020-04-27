---
title: Erstellen von Linux- und UNIX-Serveranwendungen
titleSuffix: Configuration Manager
description: Hier erfahren Sie, was Sie beim Erstellen und Bereitstellen von Anwendungen für Linux- und Unix-Geräte berücksichtigen müssen.
ms.date: 03/27/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 79cd131a-1a24-4751-87c8-7f275e45d847
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 3f5d0cfb930e6d1b8cf4cd6dfb0eabfa38ddab16
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075777"
---
# <a name="create-linux-and-unix-server-applications-with-configuration-manager"></a>Erstellen von Linux- und UNIX-Serveranwendungen mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

> [!Important]  
> Ab Version 1902 unterstützt Configuration Manager keine Linux- oder UNIX-Clients mehr. 
> 
> Ziehen Sie deshalb Microsoft Azure Management zum Verwalten von Linux-Servern in Betracht. Azure-Lösungen verfügen über umfangreiche Linux-Unterstützung, die i.d.R. über die Funktionen von Configuration Manager hinausgeht (einschließlich der End-to-End-Patchverwaltung für Linux).

Berücksichtigen Sie beim Erstellen und Bereitstellen von Anwendungen für Computer, auf denen Linux und UNIX ausgeführt wird, die folgenden Aspekte.  

## <a name="general-considerations"></a>Allgemeine Aspekte  
 Der Configuration Manager-Client für Linux und UNIX unterstützt **Softwarebereitstellungen, von denen Pakete und Programme verwendet werden**. Configuration Manager-Anwendungen können nicht auf Computern bereitgestellt werden, auf denen Linux und UNIX ausgeführt werden.  

 Eine Linux- und UNIX-Softwarebereitstellung unterstützt Folgendes:  

-   Installation von Software für Linux- und UNIX-Server, einschließlich der folgenden Funktionen:  

    -   Neue Softwarebereitstellung  

    -   Softwareupdates für bereits auf einem Computer installierte Programme  

    -   Betriebssystempatches  

-   Native Linux- und UNIX-Befehle sowie auf Linux- und UNIX-Servern gespeicherte Skripts  

-   Bereitstellungen, die auf die Betriebssysteme beschränkt sind, die Sie beim Auswählen der Programmoption **Nur auf angegebenen Clientplattformen** angegeben haben

-   Wartungsfenster zum Steuern, wann die Software installiert wird

-   Bereitstellungsstatusmeldungen zum Überwachen von Bereitstellungen  

-   Option für den Client zum Drosseln der Netzwerkauslastung beim Herunterladen von Software von einem Verteilungspunkt  

### <a name="differences-between-deploying-to-linux-and-unix-computers-and-deploying-to-windows-devices"></a>Unterschiede zwischen der Bereitstellung für Linux- und UNIX-Computer und der Bereitstellung für Windows-Geräte
Zwischen dem Bereitstellen von Paketen und Programmen für Linux- und UNIX-Computer und dem Bereitstellen von Paketen und Programmen für Windows-Geräte bestehen die folgenden Hauptunterschiede:  

|Konfiguration|Details|  
|-------------------|-------------|  
|Verwenden Sie ausschließlich Konfigurationen für Computer und nicht die Konfigurationen für Benutzer.|Konfigurationen für Benutzer werden vom Configuration Manager-Client für Linux und UNIX nicht unterstützt.|  
|Konfigurieren Sie die Programme so, dass Software vom Verteilungspunkt heruntergeladen wird und die Programme vom lokalen Clientcache ausgeführt werden.|Das Ausführen der Software am Verteilungspunkt wird vom Configuration Manager-Client für Linux und UNIX nicht unterstützt. Stattdessen müssen Sie die Software so konfigurieren, dass sie auf den Client heruntergeladen und dann installiert wird.<br /><br /> Standardmäßig wird die Software aus dem Clientcache gelöscht, nachdem sie vom Client für Linux und UNIX installiert wurde. Allerdings werden Pakete, für die **Inhalt dauerhaft in Clientcache speichern** konfiguriert wurde, nicht vom Client entfernt. Sie verbleiben nach der Installation der Software im Cache des Clients.<br /><br /> Vom Client für Linux und UNIX werden keine Konfigurationen für den Clientcache unterstützt. Die maximale Cachegröße ist lediglich durch den freien Speicherplatz auf dem Clientcomputer beschränkt.|  
|Konfigurieren des Netzwerkzugriffskontos für den Zugriff über Verteilungspunkte|Linux- und UNIX-Computer wurden als Arbeitsgruppencomputer entwickelt. Das Netzwerkzugriffskonto muss für den Standort konfiguriert sein, um über den Verteilungspunkt in der Configuration Manager-Standortserverdomäne auf Pakete zugreifen zu können. Sie müssen dieses Konto als Eigenschaft der Softwareverteilungskomponente angeben und es vor dem Bereitstellen von Software konfigurieren.<br /><br /> An einem Standort können jeweils mehrere Netzwerkzugriffskonten konfiguriert werden. Auf dem Client für Linux und UNIX können alle die von Ihnen konfigurierten Konten als Netzwerkzugriffskonto verwendet werden.<br /><br /> Weitere Informationen finden Sie unter [Standortkomponenten für Configuration Manager](../../core/servers/deploy/configure/site-components.md).|  

 Sie können Pakete und Programme für Sammlungen bereitstellen, die ausschließlich Linux- oder UNIX-Clients enthalten, oder für Sammlungen, die verschiedene Clienttypen enthalten, beispielsweise die Sammlung **Alle Systeme**. Die Software wird jedoch auf Nicht-Linux- und Nicht-UNIX-Clients nicht installiert, oder diese Clients melden einen Fehler.  

 Wenn der Configuration Manager-Client für Linux und UNIX eine Bereitstellung empfängt und ausführt, werden Statusmeldungen generiert. Sie können diese Statusmeldungen in der Configuration Manager-Konsole anzeigen oder den Bereitstellungsstatus mithilfe von Berichten überwachen.  

 Weitere Informationen zum Verwenden von Paketen und Programmen finden Sie unter [Pakete und Programme](../../apps/deploy-use/packages-and-programs.md).  

##  <a name="configure-packages-programs-and-deployments-for-linux-and-unix-servers"></a>Konfigurieren von Paketen, Programmen und Bereitstellungen für Linux- und UNIX-Server  
 Pakete und Programme können mit den in der Configuration Manager-Konsole verfügbaren Standardoptionen erstellt und bereitgestellt werden. Für den Client sind keine eindeutigen Konfigurationen erforderlich.  

 Verwenden Sie die Informationen in den folgenden Abschnitten, um Pakete, Programme und Bereitstellungen zu konfigurieren.  

### <a name="packages-and-programs"></a>Pakete und Programme  
 Verwenden Sie in der Configuration Manager-Konsole den **Assistenten zum Erstellen von Paketen und Programmen**, um ein Paket und Programm für einen Linux- oder UNIX-Server zu erstellen. Die meisten Einstellungen für Pakete und Programme werden vom Client für Linux und UNIX unterstützt. Einige Einstellungen werden jedoch nicht unterstützt. Beachten Sie die folgenden Punkte, wenn Sie Pakete und Programme erstellen oder konfigurieren:  

-   Schließen Sie die Dateitypen ein, die von den Zielcomputern unterstützt werden.  

-   Definieren Sie die Befehlszeilen, die für die Verwendung auf dem Zielcomputer geeignet sind.  

-   Denken Sie daran, dass keine Einstellungen unterstützt werden, bei denen eine Interaktion mit Benutzern erfolgt.  

In der folgenden Tabelle sind die Eigenschaften für Pakete und Programme aufgeführt, die nicht unterstützt werden:  

|Eigenschaft des Pakets und Programms|Verhalten|Weitere Informationen|  
|----------------------------------|--------------|----------------------|  
|Einstellungen für die Paketfreigabe:<br /><br /> - Alle Optionen|Ein Fehler wird generiert, und bei der Softwareinstallation tritt ein Fehler auf.|Der Client unterstützt diese Konfiguration nicht. Die Software muss vom Client über HTTP oder HTTPS heruntergeladen werden. Die Befehlszeile muss anschließend aus dem lokalen Cache ausgeführt werden.|  
|Einstellungen für die Paketaktualisierung:<br /><br /> - Verbindungen zwischen Benutzern und Verteilungspunkten trennen|Die Einstellungen werden ignoriert.|Der Client unterstützt diese Konfiguration nicht.|  
|Betriebssystembereitstellungseinstellungen:<br /><br /> - Alle Optionen|Die Einstellungen werden ignoriert.|Der Client unterstützt diese Konfiguration nicht.|  
|Berichterstattung:<br /><br /> - Paketeigenschaften für MIF-Statusabstimmung verwenden<br /><br /> - Folgende Felder für MIF-Statusabstimmung verwenden|Die Einstellungen werden ignoriert.|Die Verwendung von Status-MIF-Dateien wird vom Client nicht unterstützt.|  
|**Run**:<br /><br /> - Alle Optionen|Die Einstellungen werden ignoriert.|Pakete ohne Benutzeroberfläche werden immer vom Client ausgeführt.<br /><br /> Alle Konfigurationsoptionen für Ausführen werden vom Client ausgeführt.|  
|Nach der Ausführung:<br /><br />- Der Computer wird von Configuration Manager neu gestartet.<br /><br /> - Neustart wird durch das Programm gesteuert<br /><br /> - Der Benutzer wird von Configuration Manager abgemeldet.|Ein Fehler wird generiert, und bei der Softwareinstallation tritt ein Fehler auf.|Die Einstellung für einen Neustart des Systems und die benutzerspezifischen Einstellungen werden nicht unterstützt.<br /><br /> Wird eine andere Einstellung als **Keine Aktion erforderlich** verwendet, wird vom Client ein Fehler generiert, und die Installation der Software wird ohne weitere Maßnahmen fortgesetzt.|  
|Programm kann ausgeführt werden:<br /><br /> - Nur wenn ein Benutzer angemeldet ist|Ein Fehler wird generiert, und bei der Softwareinstallation tritt ein Fehler auf.|Benutzerspezifische Einstellungen werden nicht unterstützt.<br /><br /> Wenn diese Option konfiguriert wurde, wird vom Client ein Fehler generiert, und bei der Softwareinstallation tritt ein Fehler auf.<br /><br /> Andere Optionen werden ignoriert, und die Softwareinstallation wird fortgesetzt.|  
|Ausführmodus:<br /><br /> - Mit Benutzerrechten ausführen|Die Einstellungen werden ignoriert.|Benutzerspezifische Einstellungen werden nicht unterstützt.<br /><br /> Allerdings wird die Konfiguration zur Ausführung mit Administratorrechten vom Client unterstützt.<br /><br /> Wenn Sie die Option **Mit Administratorrechten ausführen** festlegen, werden vom Configuration Manager-Client die Stammanmeldedaten verwendet.<br /><br /> Mit dieser Einstellung wird kein Fehler oder Protokolleintrag generiert. Stattdessen tritt bei der Softwareinstallation ein Fehler auf, wenn vom Client für die Konfiguration **Programm kann ausgeführt werden** = **Nur wenn ein Benutzer angemeldet ist** ein Fehler generiert wird.|  
|Benutzern gestatten, die Programminstallation anzuzeigen und mit ihr zu interagieren|Die Einstellungen werden ignoriert.|Benutzerspezifische Einstellungen werden nicht unterstützt.<br /><br /> Diese Konfiguration wird ignoriert, und die Softwareinstallation wird fortgesetzt.|  
|Laufwerkmodus:<br /><br /> - Alle Optionen|Die Einstellungen werden ignoriert.|Diese Einstellung wird nicht unterstützt, da der Inhalt immer auf den Client heruntergeladen und lokal ausgeführt wird.|  
|Ein anderes Programm zuerst ausführen|Ein Fehler wird generiert, und bei der Softwareinstallation tritt ein Fehler auf.|Die rekursive Programminstallation wird nicht unterstützt.<br /><br /> Wurde ein Programm so konfiguriert, dass ein anderes Programm zuerst ausgeführt wird, tritt bei der Softwareinstallation ein Fehler auf, und die Installation des anderen Programms wird nicht gestartet.|  
|Wenn dieses Programm einem Computer zugewiesen ist:<br /><br /> - Einmal ausführen für jeden Benutzer, der sich anmeldet|Die Einstellungen werden ignoriert.|Benutzerspezifische Einstellungen werden nicht unterstützt.<br /><br /> Allerdings wird die Konfiguration zur einmaligen Ausführung für den Computer vom Client unterstützt.<br /><br /> Mit dieser Einstellung wird kein Fehler oder Protokolleintrag generiert, da für die Konfiguration **Programm kann ausgeführt werden** = **Nur wenn ein Benutzer angemeldet ist**.|  
|Programmbenachrichtigungen unterdrücken|Die Einstellungen werden ignoriert.|Vom Client wird keine Benutzeroberfläche implementiert.<br /><br /> Bei Auswahl dieser Konfiguration wird die Einstellung ignoriert, und die Softwareinstallation wird fortgesetzt.|  
|Dieses Programm auf Computern deaktivieren, auf denen es bereitgestellt ist|Die Einstellungen werden ignoriert.|Diese Einstellung wird nicht unterstützt und hat keinen Einfluss auf die Installation der Software.|  
|Installation dieses Programms aus der Tasksequenz „Paket installieren“ ohne Bereitstellung zulassen||Vom Client werden keine Tasksequenzen unterstützt.<br /><br /> Diese Einstellung wird nicht unterstützt und hat keinen Einfluss auf die Installation der Software.|  
|Windows Installer:<br /><br /> - Alle Optionen|Die Einstellungen werden ignoriert.|Vom Client werden keine Windows Installer-Dateien oder -Einstellungen unterstützt.|  
|OpsMgr-Wartungsmodus:<br /><br /> - Alle Optionen|Die Einstellungen werden ignoriert.|Der Client unterstützt diese Konfiguration nicht.|  

### <a name="deploy-software-to-a-linux-or-unix-server"></a>Bereitstellen von Software für einen Linux- oder UNIX-Server
 Sie können in der Configuration Manager-Konsole den **Assistenten zum Bereitstellen von Software** verwenden, um mithilfe eines Pakets und Programms Software auf einem Linux- oder UNIX-Server bereitzustellen. Die meisten Bereitstellungseinstellungen werden vom Client für Linux und UNIX unterstützt. Einige Einstellungen werden jedoch nicht unterstützt. Beim Bereitstellen von Software sind folgende Punkte zu beachten:  

- Stellen Sie das Paket auf mindestens einem Verteilungspunkt bereit, der einer für Inhaltsspeicherorte konfigurierten Begrenzungsgruppe zugeordnet ist.  

- Der Client für Linux und UNIX, von dem diese Bereitstellung empfangen wird, muss über seinen Netzwerkpfad auf diesen Verteilungspunkt zugreifen können.  

- Das Paket wird vom Client für Linux und UNIX vom Verteilungspunkt heruntergeladen, und das Programm wird auf dem lokalen Computer ausgeführt.  

- Vom Client für Linux und UNIX können keine Pakete aus freigegebenen Ordnern heruntergeladen werden. Es werden Pakete von IIS-fähigen Verteilungspunkten heruntergeladen, die HTTP oder HTTPS unterstützen.  

  In der folgenden Tabelle sind Eigenschaften für Bereitstellungen aufgelistet, die nicht unterstützt werden:  

|Bereitstellungseigenschaft|Verhalten|Weitere Informationen|  
|-------------------------|--------------|----------------------|  
|Bereitstellungseinstellungen – Zweck:<br /><br /> - Verfügbar<br /><br /> - Erforderlich|Die Einstellungen werden ignoriert.|Benutzerspezifische Einstellungen werden nicht unterstützt.<br /><br /> Allerdings wird die Einstellung **Erforderlich**vom Client unterstützt, wodurch die geplante Installationszeit erzwungen wird, aber es wird keine manuelle Installation vor dieser geplanten Zeit unterstützt.|  
|Aktivierungspakete senden|Die Einstellungen werden ignoriert.|Der Client unterstützt diese Konfiguration nicht.|  
|Zuweisungszeitplan:<br /><br /> Anmelden<br /><br /> Abmelden|Ein Fehler wird generiert, und bei der Softwareinstallation tritt ein Fehler auf.|Benutzerspezifische Einstellungen werden nicht unterstützt.<br /><br /> Vom Client wird die Einstellung **So bald wie möglich**unterstützt.|  
|Benachrichtigungseinstellungen:<br /><br /> - Benutzern zuweisungsunabhängige Programmausführung erlauben|Die Einstellungen werden ignoriert.|Vom Client wird keine Benutzeroberfläche implementiert.|  
|Wenn die geplante Zuweisungszeit erreicht ist, erlauben Sie die Ausführung folgender Aktivität außerhalb des Wartungsfensters:<br /><br /> Systemneustart (falls dieser zum Abschluss der Installation nötig ist)|Es wird ein Fehler generiert.|Vom Client wird kein Systemneustart unterstützt.|  
|Bereitstellungsoption für schnelle (LAN-)Netzwerke:<br /><br /> - Programm vom Verteilungspunkt ausführen|Ein Fehler wird generiert, und bei der Softwareinstallation tritt ein Fehler auf.|Vom Client kann die Software nicht am Verteilungspunkt ausgeführt werden. Das Programm muss zur Ausführung heruntergeladen werden.|  
|Bereitstellungsoption für eine langsame oder unzuverlässige Netzwerkgrenze oder für einen Fallbackquellpfad für den Inhalt:<br /><br /> - Freigeben von Inhalten für andere Clients im gleichen Subnetz zulassen|Die Einstellungen werden ignoriert.|Vom Client wird das Freigeben von Inhalten zwischen Peers nicht unterstützt.|  

 Weitere Informationen zu Inhaltsorten finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur für Configuration Manager](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

 Weitere Informationen zum Erstellen einer Bereitstellung finden Sie unter [Bereitstellen von Anwendungen](../../apps/deploy-use/deploy-applications.md).  

##  <a name="manage-network-bandwidth-for-software-downloads-from-distribution-points"></a>Verwalten der Netzwerkbandbreite für das Herunterladen von Software von Verteilungspunkten  
 Der Linux- und UNIX-Client unterstützt die Steuerung der Netzwerkbandbreite beim Herunterladen von Software von einem Verteilungspunkt.  

 Hierfür werden die BITS-Einstellungen (Background Intelligent Transfer Service, intelligenter Hintergrundübertragungsdienst) verwendet, die Sie als Clienteinstellungen in Configuration Manager konfigurieren, ohne dass BITS implementiert wird. Stattdessen erfolgt die Drosselung der genutzten Netzwerkbandbreite beim Softwaredownload, indem die die Größe der HTTP-Anforderungsblöcke und die Verzögerung zwischen den Blöcken vom Client gesteuert werden.  

 Soll ein Clients für die Steuerung der Netzwerkbandbreite konfiguriert werden, legen Sie die Clienteinstellungen unter **Intelligente Hintergrundübertragung** fest und wenden diese Einstellungen dann auf den Clientcomputer an. Die Bandbreitensteuerung kann nur von Clients durchgeführt werden, für die die Option **Intelligente Hintergrundübertragung** in den folgenden Clienteinstellungen auf **Ja** festgelegt wurde:  

- **Maximale Netzwerkbandbreite für BITS-Übertragungen im Hintergrund begrenzen**  

  Die folgenden Konfigurationen für intelligente Hintergrundübertragung werden vom Client unterstützt:  

  -   **Beginn des Einschränkungszeitfensters**  

  -   **Ende des Einschränkungszeitfensters**  

  -   **Maximale Übertragungsrate während des Einschränkungszeitfensters (KBit/s)**  

  -   **Maximale Übertragungsrate außerhalb des Einschränkungszeitfensters (KBit/s)**  

Die folgende Konfiguration der intelligente Hintergrundübertragung wird nicht unterstützt und wird vom Client für Linux und UNIX ignoriert:  

- **BITS-Downloads außerhalb des Einschränkungszeitfensters zulassen**  

  Wenn der Softwaredownload von einem Verteilungspunkt auf den Client unterbrochen wird, wird der Ladevorgang vom Client für Linux und UNIX nicht wiederaufgenommen. Stattdessen wird der Download des gesamten Softwarepakets neu gestartet.  

##  <a name="configure-operations-for-software-deployments"></a>Konfigurieren von Vorgängen für Softwarebereitstellungen  
 Ähnlich wie beim Windows-Client werden vom Configuration Manager-Client für Linux und UNIX neue Softwarebereitstellungen ermittelt, wenn die Abfragen und Überprüfungen für neue Richtlinien ausgeführt werden. Die Häufigkeit, mit der die Überprüfung auf neue Richtlinien vom Client ausgeführt wird, hängt von den Einstellungen des Clients ab. Sie können Wartungsfenster konfigurieren, um zu steuern, wann die Softwarebereitstellungen auftreten.  

 Softwarebereitstellungen auf Linux- und UNIX-Servern können Sie mithilfe von Paket-, Programm- und Bereitstellungseigenschaften konfigurieren.  

 Wenn auf dem Client eine Richtlinie für eine Bereitstellung empfangen wird, wird von diesem eine Statusmeldung übermittelt. Außerdem werden Statusmeldungen übermittelt, sobald die Installation der Software gestartet wird und wenn sie beendet wird bzw. ein Fehler auftritt.  

 Programme für Softwarebereitstellungen werden mit den Stammanmeldedaten ausgeführt, mit denen der Configuration Manager-Client für Linux und UNIX ausgeführt wird. Mit dem Exitcode des Programmbefehls wird ermittelt, ob der Vorgang fehlerfrei ausgeführt wurde oder nicht. Der Exitcode 0 (Null) bedeutet „erfolgreich“. Darüber hinaus werden die Einträge **stdout** (Standardausgabestream) und **stderr** (Standardfehlerstream) in die Protokolldatei kopiert, wenn die Protokollebene auf INFO oder TRACE festgelegt wurde.  

> [!TIP]  
>  Wenn sich die bereitzustellende Software auf einer NFS-Freigabe (NFS) befindet, auf die der Linux- oder UNIX-Server Zugriff hat, müssen Sie keinen Verteilungspunkt verwenden, um das Paket herunterzuladen. Stattdessen müssen Sie beim Erstellen des Pakets nur darauf achten, dass das Kontrollkästchen **Dieses Paket enthält Quelldateien**nicht aktiviert ist. Geben Sie dann beim Konfigurieren des Programms die Befehlszeile an, die einen direkten Zugriff auf das Paket auf dem NFS-Bereitstellungspunkt erlaubt.  
