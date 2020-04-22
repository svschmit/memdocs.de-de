---
title: Bereitstellen von virtuellen App-V-Anwendungen
titleSuffix: Configuration Manager
description: Hier erfahren Sie, was Sie beim Erstellen und Bereitstellen von virtuellen Anwendungen beachten müssen.
ms.date: 03/12/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: ddcad9f2-a542-4079-83ca-007d7cb44995
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bea7c2ef5c3d77932fcd91ca8d4d2b8baa62edd2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689808"
---
# <a name="deploy-app-v-virtual-applications-with-configuration-manager"></a>Bereitstellen von virtuellen App-V-Anwendungen mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Die Verwaltung von virtuellen Anwendungen mithilfe von Configuration Manager bietet die folgenden Vorteile:  

-   Eine einzige Verwaltungsinfrastruktur  

-   Skalierbarkeits-, Bereitstellungs- und Inhaltsverteilungsfunktionen wie Sammlungen und Affinität zwischen Benutzer und Gerät  

-   Erweiterte Funktionen zur Anwendungsverwaltung  

-   Betriebssystembereitstellung, Software- und Hardwareinventur, Softwaremessung und Asset Intelligence zur Unterstützung virtueller Anwendungen  

Weitere Informationen zum Erstellen und Sequenzieren von Anwendungen mit Microsoft Application Virtualization (App-V) finden Sie unter [Application Virtualization](https://technet.microsoft.com/library/cc843848.aspx) in der TechNet-Bibliothek.  

Zusätzlich zu den anderen Configuration Manager-Anforderungen und -Verfahren zum Erstellen einer Anwendung müssen beim Erstellen und Bereitstellen von virtuellen Anwendungen die folgenden Aspekte berücksichtigt werden:

-   Auf den Computern, auf denen virtuelle Anwendungen bereitgestellt werden sollen, müssen der Configuration Manager-Client und der App-V-Client installiert sein. Die Clientgeräte können Desktop- und tragbare Computer sowie VDI-Clients (Virtual Desktop Infrastructure) umfassen. Virtuelle Anwendungspakete werden von Configuration Manager- und der App-V-Clientsoftware gemeinsam übermittelt, gesucht und gestartet. Die Übermittlung virtueller Anwendungspakete an den App-V-Client wird vom Configuration Manager-Client verwaltet. Die virtuelle Anwendung wird vom App-V-Client auf dem Client ausgeführt.  

-   Zum Bereitstellen einer virtuellen Anwendung müssen Sie diese zunächst mithilfe von App-V Application Virtualization Sequencer erstellen. Vom Sequencer werden die Installation und Einrichtung einer Anwendung überwacht und die für das Ausführen der Anwendung in einer virtuellen Umgebung erforderlichen Informationen aufgezeichnet. Sie können mithilfe des Sequencers auch festlegen, welche Dateien und Konfigurationen für alle Benutzer gelten und welche Konfigurationen von Benutzern angepasst werden können.  

-   Wenn Sie eine Anwendung sequenzieren, müssen Sie das Paket an einem Speicherort speichern, auf den Configuration Manager zugreifen kann. Sie können dann eine Anwendungsbereitstellung erstellen, die diese virtuelle Anwendung enthält.  

-   Die Verwendung des App-V 4.6-Features für freigegebenen, schreibgeschützten Cache wird von Configuration Manager nicht unterstützt.  

-   Configuration Manager unterstützt die SCS-Funktion (Shared Content Store) in App-V 5.  

-   Bei der Erstellung eines Bereitstellungstyps für eine virtuelle Anwendung wird von Configuration Manager der Bereitstellungstyp anhand der Inhalte der Manifestdatei der Anwendung erstellt. Dabei handelt es sich um eine XML-Datei, die Informationen über die virtuelle Anwendung enthält. Darüber hinaus werden von Configuration Manager Anforderungen für den Bereitstellungstyp auf Basis der Inhalte der OSD-Datei von App-V erstellt, in der Informationen zu unterstützten Betriebssystemen für die virtuelle Anwendung enthalten sind.  

-   Zum Bereitstellen von virtuellen Anwendungen in Configuration Manager muss auf den Clientcomputern mindestens App-V 4.6 SP1 oder eine höhere Version des Clients installiert sein.  

-   Sie müssen für den App-V-Client ein Update mit dem im Knowledge Base-Artikel [2645225](https://support.microsoft.com/kb/2645225) beschriebenen Hotfix durchführen, damit Sie virtuelle Anwendungen erfolgreich bereitstellen können.  

-   Bei Verwendung von Verbindungsgruppen in App-V 5.0 können in den von Ihnen bereitgestellten virtuellen Anwendungen auf Clientcomputern das gleiche Dateisystem und die gleiche Registrierung verwendet werden. Im Gegensatz zu virtuellen Standard-Anwendungen können diese Anwendungen Daten gemeinsam verwenden. Darüber hinaus werden für Verbindungsgruppen Benutzereinstellungen für die Anwendungen beibehalten, die sie enthalten. Virtuelle App-V-Umgebungen in Configuration Manager werden zum Einrichten von Verbindungsgruppen auf Clientcomputern verwendet. Virtuelle Umgebungen werden bei der Installation der Anwendung bzw. bei der nächsten Auswertung der auf den Clients installierten Anwendungen auf Clientcomputern erstellt oder geändert. Sie können diese Anwendungen priorisieren. Falls dann mehrere Anwendungen versuchen, ein Dateisystem oder einen Registrierungswert zu ändern, hat die Anwendung mit der höchsten Priorität Vorrang. Weitere Informationen finden Sie unter [Erstellen von virtuellen App-V-Umgebungen](../../apps/deploy-use/create-app-v-virtual-environments.md).  

##  <a name="supported-app-v-versions"></a>Unterstützte App-V-Versionen  
 Configuration Manager unterstützt die folgenden App-V-Versionen:  

-   **App-V 4.6:** Zum Verwenden von virtuellen Anwendungen in Configuration Manager muss auf den Clientcomputern der App-V 4.6 SP1-, App-V 4.6 SP2- oder App-V 4.6 SP3-Client installiert sein.  

     Sie müssen für den App-V 4.6 SP1-Client außerdem ein Update mit dem im Knowledge Base-Artikel [2645225](https://go.microsoft.com/fwlink/p/?LinkId=237322) beschriebenen Hotfix durchführen, damit Sie virtuelle Anwendungen erfolgreich bereitstellen können.  

-   **App-V 5, App-V 5.0 SP1, App-V 5.0 SP2 App-V 5.0 SP3 und App-V 5.1:** Für App-V 5.0 SP2 müssen Sie das [Hotfixpaket 5](https://support.microsoft.com/en-us/kb/2963211) installieren oder App-V 5.0 SP3 verwenden.  
-   **App-V 5.2:** Diese Version ist in Windows 10 Education (1607 und höher), Windows 10 Enterprise (1607 und höher) und Windows Server 2016 integriert.

Weitere Informationen zu App-V in Windows 10 finden Sie in den folgenden Themen:

- [Neuheiten in App-V](https://technet.microsoft.com/itpro/windows/manage/appv-about-appv)
- [Erste Schritte mit App-V für Windows 10](https://technet.microsoft.com/itpro/windows/manage/appv-getting-started)
- [Upgrade auf App-V für Windows 10 aus einer vorhandenen Installation](https://technet.microsoft.com/itpro/windows/manage/appv-upgrading-to-app-v-for-windows-10-from-an-existing-installation)

##  <a name="steps-to-manage-app-v-virtual-applications"></a>Schritte zur Verwaltung virtueller App-V-Anwendungen  
 Führen Sie zum Verwalten von virtuellen App-V-Anwendungen folgende Schritte aus:  

1.   **Sequenzieren:** Beim Sequenzieren wird eine Anwendung mithilfe von App-V Sequencer in eine virtuelle Anwendung konvertiert.

2.   **Erstellen:** Importieren Sie die sequenzierte Anwendung mit dem Assistenten zum Erstellen neuer Bereitstellungstypen in einen Configuration Manager-Bereitstellungstyp, den Sie dann einer Anwendung hinzufügen können. Sie können auch virtuelle Umgebungen erstellen, in denen es mehreren virtuellen Anwendungen möglich ist, Einstellungen freizugeben.

3.   **Verteilen:** Bei der Verteilung werden App-V-Anwendungen auf Configuration Manager-Verteilungspunkten verfügbar gemacht.

4.   **Bereitstellen:** Bei der Bereitstellung wird die Anwendung auf Clientcomputern verfügbar gemacht. Dies wird in einer vollständigen App-V-Infrastruktur als „Publishing and Streaming“ (Veröffentlichen und Streamen) bezeichnet.  

##  <a name="configuration-manager-virtual-application-delivery-methods"></a>Methoden zur Übermittlung virtueller Anwendungen mit Configuration Manager  
In Configuration Manager werden zwei Methoden zur Übermittlung virtueller Anwendungen an Clients unterstützt: Übermittlung durch Streaming und lokale Übermittlung (herunterladen und ausführen).

Bei der Entscheidung für eine Übermittlungsmethode müssen Sie die geringere Speicherplatzanforderung bei der Übermittlung per Streaming und die garantierte Verfügbarkeit von App-V-Anwendungen bei der lokalen Übermittlung sorgfältig abwägen. Möglicherweise ist der größere Clientspeicherplatz, der für die lokale Übermittlung erforderlich ist, einer Übermittlung per Streaming vorzuziehen, damit die Anwendung den Benutzern an jedem Standort stets zur Verfügung steht.  

###  <a name="streaming-delivery"></a>Übermittlung durch Streaming
Bei Verwendung von Configuration Manager zum Verwalten des App-V-Clients wird das Streaming virtueller Anwendungen über HTTP oder HTTPS von einem Verteilungspunkt unterstützt. Streaming über HTTP oder HTTPS ist standardmäßig aktiviert und wird im Dialogfeld für die Verteilungspunkteigenschaften eingerichtet. Wenn Sie eine virtuelle Anwendung für Clientcomputer bereitstellen und ein Benutzer diese Anwendung ausführt, wird vom Configuration Manager-Client eine Verbindung mit einem Verwaltungspunkt hergestellt, um festzustellen, welcher Verteilungspunkt zu verwenden ist. Anschließend wird die Anwendung vom Verteilungspunkt gestreamt.  

Anhand der Informationen in der folgenden Tabelle können Sie feststellen, ob die Übermittlung durch Streaming die für Sie am besten geeignete Übermittlungsmethode ist:

|Vorteile|Nachteile|  
|----------------|-------------------|  
|Bei dieser Methode wird der Paketinhalt mithilfe von Standardnetzwerkprotokollen von Verteilungspunkten gestreamt.<br /><br /> Über Programmverknüpfungen für virtuelle Anwendungen wird eine Verbindung mit dem Verteilungspunkt aufgerufen, damit die virtuelle Anwendung bei Bedarf übermittelt werden kann.<br /><br /> Diese Methode eignet sich insbesondere für Clients, deren Verbindungen mit den Verteilungspunkten eine hohe Bandbreite aufweisen.<br /><br /> Updates für die im gesamten Unternehmen verteilten virtuellen Anwendungen sind verfügbar, wenn Clients über eine Richtlinie darüber informiert werden, dass die aktuelle Version abgelöst wurde. Nur die Änderungen gegenüber der vorherigen Version werden von den Clients heruntergeladen.<br /><br /> Am Verteilungspunkt werden Zugriffsberechtigungen definiert, um den Zugriff Unbefugter auf Anwendungen oder Pakete zu verhindern.|Virtuelle Anwendungen werden erst gestreamt, wenn der Benutzer die Anwendung zum ersten Mal ausführt. Angenommen, ein Benutzer erhält Programmverknüpfungen für virtuelle Anwendungen und trennt dann die Verbindung mit dem Netzwerk, bevor er die virtuellen Anwendungen zum ersten Mal ausführt. Wenn der Benutzer nun versucht, die virtuelle Anwendung auszuführen, während der Client offline ist, wird ein Fehler angezeigt. Die virtuelle Anwendung kann nicht ausgeführt werden, da kein Configuration Manager-Verteilungspunkt zum Streamen der Anwendung verfügbar ist. Die Anwendung wird erst verfügbar, wenn der Benutzer die Verbindung mit dem Netzwerk wiederherstellt und die Anwendung ausführt.<br /><br /> Um dies zu vermeiden, können Sie virtuelle Anwendungen mithilfe der lokalen Übermittlungsmethode an Clients übermitteln. Alternativ können Sie die internetbasierte Clientverwaltung für die Übermittlung per Streaming aktivieren.|  

###  <a name="local-delivery-download-and-execute"></a>Lokale Übermittlung (herunterladen und ausführen)  
Das Herunterladen und Ausführen ist die gängigste Methode bei der Verwendung von Configuration Manager, da diese imitiert, wie andere Anwendungsformate mit Configuration Manager dargestellt werden. Bei Verwendung der lokalen Übermittlungsmethode wird auf dem Configuration Manager-Client zunächst das gesamte virtuelle Anwendungspaket in den Configuration Manager-Clientcache heruntergeladen. In Configuration Manager wird der App-V-Client anschließend angewiesen, die Anwendung aus dem Configuration Manager-Cache in den App-V-Cache zu streamen. Wenn Sie eine virtuelle Anwendung für Clientcomputer bereitstellen und der Inhalt sich nicht im App-V-Cache befindet, wird der Anwendungsinhalt vom App-V-Client aus dem Configuration Manager-Clientcache in den App-V-Cache gestreamt und anschließend ausgeführt. Wenn die Anwendung erfolgreich ausgeführt wird, können Sie den Configuration Manager-Client so einrichten, dass ältere Versionen des Pakets beim nächsten Löschzyklus gelöscht oder dauerhaft im Configuration Manager-Clientcache gespeichert werden. Die dauerhafte lokale Beibehaltung kann die Vorteile der Methoden für die Optimierung von Paketinhaltslieferungen, z.B. BranchCache und PeerCache, nutzen.

Anhand der Informationen in der folgenden Tabelle können Sie feststellen, ob die lokale Übermittlung die für Sie am besten geeignete Übermittlungsmethode ist:   

|Vorteile|Nachteile|  
|----------------|-------------------|  
|Das Paket wird mithilfe der intelligenten Hintergrundübertragung (Background Intelligent Transfer Service, BITS), einer Standardfunktionalität von Verteilungspunkten, heruntergeladen.<br /><br /> Die Inhalte des virtuellen Anwendungspakets werden lokal an den Client übermittelt. Das bedeutet, dass Benutzer sie ausführen können, wenn ihr Computer nicht mit dem Netzwerk verbunden ist.<br /><br /> Diese Methode eignet sich für langsame oder unzuverlässige Netzwerkverbindungen sowie für Computer, die nur gelegentlich mit dem Netzwerk verbunden werden.<br /><br /> Mithilfe der Remotedifferenzialkomprimierung (Remote Differential Compression, RDC) werden von Configuration Manager nur die Byte in den Dateien an Clients gesendet, die sich bei der Aktualisierung des Inhalts des virtuellen Anwendungspakets geändert haben. Vom Configuration Manager-Client wird mithilfe von RDC eine neue Version eines virtuellen Anwendungspakets erstellt, das auf der aktuellen Paketversion und auf den an den Client gesendeten Änderungen basiert.<br /><br /> Diese Methode bietet Anwendungsresilienz für mobile oder nicht verbundene Benutzer. Administratoren können festlegen, dass das Paket nach der Übermittlung dauerhaft im Configuration Manager-Cache gespeichert wird, sofern die virtuelle Anwendung über einen Installationsvorgang bereitgestellt wurde. Das Paket im Configuration Manager-Clientcache dient als lokale, zuverlässige Streamingquelle, über die der App-V-Client das Paket mithilfe von Pull in seinen Cache übertragen kann.|Wenn die virtuelle Anwendung dauerhaft im Configuration Manager-Cache gespeichert wird, muss der auf dem Client verfügbare Speicherplatz ungefähr doppelt so groß wie das virtuelle Anwendungspaket sein.|  

###  <a name="deployment-from-an-image"></a>Bereitstellung über ein Image

Sie können virtuelle Anwendungen auch im Voraus auf einem Computer installieren und dann ein Abbild dieses Computers zur Bereitstellung auf anderen Computern erstellen. Wenn das virtuelle Anwendungspaket jedoch an einem anderen Standort erstellt wurde, erfolgt der Download von Anwendungsupdates nicht über die binäre Deltareplikation. Diese Option kann sich in einer virtuellen Desktopinfrastruktur als nützlich erweisen, wenn Anwendungen sofort verfügbar sein und nicht erst nach der Benutzeranmeldung heruntergeladen werden sollen.    

##  <a name="migrating-from-an-app-v-infrastructure-to-a-configuration-manager-and-app-v-infrastructure"></a>Migrieren von einer App-V-Infrastruktur zu einer Configuration Manager- und App-V-Infrastruktur  
Wenn Sie eine Migration aus einer vorhandenen App-V-Infrastruktur zu einer virtuellen Anwendungsverwaltung mit Configuration Manager beabsichtigen, beachten Sie bei der Planung die in der folgenden Tabelle genannten Punkte.  

|Schritt|Weitere Informationen|  
|----------|----------------------|  
|Wählen Sie unter den aktuellen virtuellen Anwendungen die Anwendungen aus, die Sie in die Configuration Manager-Infrastruktur migrieren möchten.|Keine zusätzlichen Informationen|  
|Bewerten Sie die Benutzer und Geräte, für die die virtuellen Anwendungen bereitgestellt werden.|Erstellen Sie Configuration Manager-Sammlungen, um die Benutzer und Geräte zu gruppieren, für die Sie die virtuellen Anwendungen bereitstellen möchten. Siehe [Einführung in Sammlungen](../../core/clients/manage/collections/introduction-to-collections.md).|  
|Migrieren Sie App-V 5-Verbindungsgruppen in virtuelle Umgebungen von Configuration Manager.|Siehe den Abschnitt [Migrieren von App-V 5-Verbindungsgruppen zu virtuellen Umgebungen in Configuration Manager](deploying-app-v-virtual-applications.md#migrating-app-v-5-connection-groups-to-configuration-manager-virtual-environments) in diesem Thema.|  
|Stellen Sie fest, ob eine der virtuellen Anwendungen in der Configuration Manager-Infrastruktur als vollständige Anwendung vorhanden ist.|Zur einfacheren Verwaltung können Sie die virtuelle Anwendung der vorhandenen vollständigen Anwendung als neuen Bereitstellungstyp hinzufügen. Siehe [Erstellen von Anwendungen](../../apps/deploy-use/create-applications.md).|  
|Erstellen Sie Anwendungen, durch die die vorhandenen App-V-Pakete ersetzt werden.|Siehe [Einführung in die Anwendungsverwaltung](../understand/introduction-to-application-management.md) und [Erstellen von Anwendungen](../../apps/deploy-use/create-applications.md).|  
|Die Verwaltung virtueller Anwendungen auf einem Client durch Configuration Manager beginnt nach der ersten Bereitstellung einer virtuellen Anwendung. Danach müssen alle App-V-Anwendungen auf dem Computer in Configuration Manager verwaltet werden.|Keine zusätzlichen Informationen|  
|Verteilen Sie den Inhalt an die entsprechenden Verteilungspunkte, um die lokale Übermittlung von Anwendungen zu ermöglichen.|Siehe [Verwalten von Inhalt und Inhaltsinfrastruktur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|Stellen Sie die Anwendung für Configuration Manager-Clients bereit.<br /><br /> Wenn die App-V-Anwendung mit einer früheren Sequencer-Version erstellt wurde, von der keine Manifestdatei im XML-Format erstellt wird, können Sie die Anwendung öffnen und in einer neueren Sequencer-Version speichern, um die Datei zu erstellen. Diese Datei ist bei der Bereitstellung virtueller Anwendungen mit Configuration Manager erforderlich.<br /><br /> Die in der Sequencer-Version SoftGrid 4.1 SP1 oder 4.2 erstellten virtuellen Anwendungspakete werden von App-V unterstützt.<br /><br /> Wenn die Anwendungen zuvor lokal installiert waren, müssen Sie sie deinstallieren, bevor Sie eine virtuelle Version der Anwendung bereitstellen.|Siehe [Bereitstellen von Anwendungen](../../apps/deploy-use/deploy-applications.md).|  
|In Configuration Manager werden Pakete und Programme, die virtuelle Anwendungen enthalten, nicht mehr unterstützt. Bei der Migration von Configuration Manager 2007 zu Configuration Manager werden diese Pakete von Configuration Manager in Anwendungen konvertiert.<br /><br /> Configuration Manager 2007-Ankündigungen werden in die folgenden Bereitstellungstypen konvertiert:<br /><br /> - Migrieren von App-V-Paketen ohne Ankündigung:  Ein Bereitstellungstyp, bei dem die Standardeinstellungen verwendet werden.<br /><br /> - Migrieren von App-V-Paketen mit einer Ankündigung: Ein Bereitstellungstyp, der die gleichen Einstellungen wie die <br />                Configuration Manager 2007-Ankündigung verwendet.<br /><br /> - Migrieren von App-V-Paketen mit mehreren Ankündigungen: Ein Bereitstellungstyp für jede <br />                Configuration Manager 2007-Ankündigung. Es werden die Einstellungen für diese Ankündigung verwendet.|Weitere Informationen finden Sie unter [Planen der Migration von Objekten zu Configuration Manager (Current Branch)](../../core/migration/planning-for-the-migration-of-objects.md).|  

##  <a name="migrating-app-v-5-connection-groups-to-configuration-manager-virtual-environments"></a>Migrieren von App-V 5-Verbindungsgruppen zu virtuellen Umgebungen in Configuration Manager  
Mithilfe von virtuellen App-V-Umgebungen in Configuration Manager wird es den von Ihnen bereitgestellten virtuellen Anwendungen ermöglicht, auf Clientcomputern das gleiche Dateisystem und die gleiche Registrierung zu nutzen. Dies bedeutet, dass diese Anwendungen im Gegensatz zu virtuellen Standardanwendungen Daten freigeben können. Virtuelle Umgebungen werden bei der Installation der Anwendung bzw. bei der nächsten Auswertung der auf den Clients installierten Anwendungen auf Clientcomputern erstellt oder geändert. Virtuelle Umgebungen ähneln Verbindungsgruppen in der eigenständigen App-V-Version 5.  

Beim Migrieren von Verbindungsgruppen aus der eigenständigen App-V 5, zu virtuellen Configuration Manager-Umgebungen müssen Sie sicherstellen, dass die auf Clientcomputern bereits vorhandenen Verbindungsgruppen von Configuration Manager ordnungsgemäß verwaltet werden. Achten Sie auch darauf, dass die Umgebung des Benutzers innerhalb dieser Verbindungsgruppen beibehalten wird.  

So wandeln Sie App-V 5-Verbindungsgruppen in virtuelle Configuration Manager-Umgebungen um:  

1.  Erstellen Sie für alle Anwendungen, die in App-V vorhanden waren, Configuration Manager-Anwendungen.  

2.  Stellen Sie die Anwendungen für Benutzer oder Geräte mit dem Bereitstellungszweck **Erforderlich**bereit. Bereitstellungen für Benutzer müssen für dieselben Benutzer bereitgestellt werden, die die Anwendung in App-V verwendet haben. Bereitstellungen für Computer müssen auf denselben Computern bereitgestellt werden, die über die Anwendung in App-V verfügten.  

3.  Erstellen Sie nach Abschluss der Bereitstellung virtuelle Umgebungen, die den Verbindungsgruppen entsprechen, die in der eigenständigen Anwendung App-V veröffentlicht werden. In der virtuellen Umgebung müssen genau die gleichen Pakete (d.h. App-V 5-Bereitstellungstypen) in der gleichen Reihenfolge vorliegen.  

Informationen zur Erstellung einer virtuellen App-V-Umgebung finden Sie unter [Erstellen von virtuellen App-V-Umgebungen](../../apps/deploy-use/create-app-v-virtual-environments.md).  

Alternativ können Sie alle Verbindungsgruppen aus dem App-V-Client löschen, bevor Sie mit der Bereitstellung von Anwendungen mit Configuration Manager beginnen. Dadurch gehen jedoch sämtliche Einstellungen verloren, die Benutzer möglicherweise in App-V-Verbindungsgruppen gespeichert haben.  

##  <a name="dynamic-suite-composition-in-app-v-46"></a>Dynamic Suite Composition in App-V 4.6  
Dynamic Suite Composition ist eine Funktion, mit der Sie ein virtuelles Anwendungspaket so definieren können, dass es eine Abhängigkeit zu einem anderen virtuellen Anwendungspaket aufweist. Wenn die Anwendung ausgeführt wird, hostet der App-V-Client das Primärpaket sowie das abhängige Paket in derselben virtuellen Umgebung für die Anwendung.  

Damit diese Funktion in Configuration Manager verwendet werden kann, müssen beide Pakete bereitgestellt und im App-V-Client registriert sein. Um sicherzustellen, dass der Inhalt abhängiger Pakete lokal auf dem Clientcomputer gehostet wird, müssen Sie die Anwendungsbereitstellung für eine lokale Übermittlung (herunterladen und ausführen) einrichten.  

Weitere Informationen zu Dynamic Suite Composition in App-V finden Sie in der App-V-Dokumentation.  

##  <a name="converting-app-v-46-applications-to-app-v-5-applications"></a>Konvertieren von App-V-Anwendungen von Version 4.6 in Version 5  
Das Format des Anwendungspakets wurde zwischen App-V 4.6 und App-V 5 geändert. Anwendungen, die mit App-V 4.6 sequenziert wurden, werden nicht mehr unterstützt. App-V 5 verfügt jedoch über ein Paketkonvertierungstool, mit dem Anwendungen umgewandelt werden können. Weitere Informationen finden Sie in der [App-V 5-Dokumentation](https://technet.microsoft.com/library/jj713472.aspx).  

Gehen Sie wie folgt vor, um App-V 4.6-Anwendungen in App-V 5-Anwendungen zu konvertieren:  

1.  Konvertieren Sie die App-V 4.6-Pakete in das App-V 5-Format, oder sequenzieren Sie sie entsprechend neu.  

2.  Stellen Sie den App-V 5-Client für Computer in der Hierarchie bereit.  

3.  Erstellen Sie neue Anwendungen mit Bereitstellungstypen für die App-V 5-Anwendungen sowie Ablösungsregeln, um die App-V 4.6-Anwendungen abzulösen.  

4.  Erstellen Sie ggf. virtuelle Umgebungen.  

5.  Stellen Sie die neuen App-V 5-Anwendungen für Computer bereit.  

##  <a name="user-and-deployment-configuration-files"></a>Benutzer- und Bereitstellungskonfigurationsdateien  
Benutzer- und Bereitstellungskonfigurationsdateien enthalten Einstellungen, mit denen das Verhalten einer Anwendung gesteuert wird. Mithilfe dieser Dateien können Sie Anwendungseinstellungen ändern, ohne die Anwendung erneut sequenzieren zu müssen.  

Eine typische App-V 5-Anwendung enthält möglicherweise die folgenden Dateien:  

-   Eine Anwendungspaketdatei (APPV)  

-   Eine Benutzerkonfigurationsdatei  

-   Eine Bereitstellungskonfigurationsdatei  

Die Benutzerkonfigurationsdatei enthält Einstellungen, die nur für den angemeldeten Benutzer gelten. Sie können beispielsweise die Konfigurationsdateien ändern, um die Informationen zur Anwendungsverknüpfung zu ändern, die für die Benutzer bereitgestellt wird. Sie können auch eine Configuration Manager-Anwendung mit mehreren Bereitstellungstypen erstellen. Jeder Bereitstellungstyp kann eine andere Benutzerkonfigurationsdatei enthalten und Anforderungsregeln verwenden, um sicherzustellen, dass diese für die entsprechenden Benutzer installiert werden.  

In der Bereitstellungskonfigurationsdatei sind Einstellungen enthalten, die für den Computer gelten, z.B. Registrierungseinstellungen. Die Datei kann auch Benutzereinstellungen enthalten, die für alle Benutzer gelten.  

Wenn Sie virtuelle App-V 5-Anwendungen mit Configuration Manager bereitstellen möchten, müssen alle drei Dateien im selben Ordner vorliegen, wenn Sie den Bereitstellungstyp für App-V 5 erstellen. Wenn in einem Ordner mehrere Dateien vorhanden sind, werden von Configuration Manager die jüngsten ausgewählt.  

Weitere Informationen finden Sie in der [App-V 5-Dokumentation](https://technet.microsoft.com/library/jj713466.aspx).  

##  <a name="app-v-local-interaction"></a>Lokale Interaktion bei App-V  
In einigen Anwendungsbereitstellungsszenarios werden Anwendungen lokal auf Clientcomputern installiert und andere Anwendungen als virtuelle Anwendungen für denselben Clientcomputer bereitgestellt. Standardmäßig können die lokal installierten Anwendungen nicht direkt mit virtuellen Anwendungen kommunizieren und diese auch nicht „erkennen“. Dieses Verhalten ist beabsichtigt und Teil der Anwendungsisolation von App-V. Die lokale Interaktion ist eine Funktion des App-V-Clients, die Sie für jede Anwendung aktivieren können, damit lokal installierte Anwendungen, die auf einem Clientcomputer ausgeführt werden, mit virtuellen Anwendungen kommunizieren und diese erkennen können. Die lokale Interaktion wird vollständig von Configuration Manager und App-V unterstützt.  

Weitere Informationen zur lokalen Interaktion bei App-V finden Sie in der App-V-Dokumentation.  

##  <a name="app-v-5-shared-content-store"></a>SCS-Modus (Shared Content Store) von App-V 5  
Configuration Manager unterstützt die SCS-Funktion (Shared Content Store) in App-V 5. Weitere Informationen finden Sie unter [Planen des App-V 5.0-Sequencer und der Clientbereitstellung](https://technet.microsoft.com/library/jj713431.aspx).  

##  <a name="monitoring-virtual-applications"></a>Überwachen virtueller Anwendungen  

### <a name="virtual-application-reports"></a>Berichte zu virtuellen Anwendungen  
Mithilfe der folgenden Berichte können Sie App-V in der Configuration Manager-Umgebung überwachen:  

|Berichtsname|Beschreibung|  
|-----------------|-----------------|  
|Ergebnisse zur virtuellen App-V-Umgebung|Zeigt Informationen zu einer ausgewählten virtuellen Umgebung mit einem angegebenen Zustand für eine ausgewählte Sammlung an (nur App-V 5).|  
|Ergebnisse zur virtuellen App-V-Umgebung für Bestand|Zeigt Informationen zu einer ausgewählten virtuellen Umgebung für ein angegebenes Asset sowie sämtliche Bereitstellungstypen für die ausgewählte virtuelle Umgebung an (nur App-V 5).|  
|Status der virtuellen App-V-Umgebung|Zeigt Kompatibilitätsinformationen für eine ausgewählte virtuelle Umgebung für eine ausgewählte Sammlung an. In der Spalte **Beibehalten** dieses Berichts werden die Assets angezeigt, in denen eine zuvor eingerichtete virtuelle Umgebung nicht mehr gültig ist, aber dennoch beibehalten wird, um Benutzereinstellungen in Anwendungen zu bewahren, die in der virtuellen Umgebung ausgeführt werden (nur App-V 5).|  
|Computer mit einer bestimmten virtuellen Anwendung|Zeigt eine Zusammenfassung der Computer mit der angegebenen App-V-Verknüpfung an, die von Application Virtualization Management Sequencer erstellt wurde (nur App-V 4.6).|  
|Computer mit einem bestimmten virtuellen Anwendungspaket|Zeigt eine Liste der Computer an, auf denen das angegebene App-V-Anwendungspaket installiert ist (nur App-V 4.6).|  
|Anzahl aller Instanzen von virtuellen Anwendungspaketen|Zeigt die Anzahl aller erkannten App-V-Anwendungspakete an (nur App-V 4.6).|  
|Anzahl aller Instanzen virtueller Anwendungen|Zeigt die Anzahl aller erkannten App-V-Anwendungen an (nur App-V 4.6).|  

### <a name="log-files"></a>Protokolldateien  
Von Configuration Manager werden Informationen zu Bereitstellungen virtueller Anwendungen in Protokolldateien aufgezeichnet. Informationen über die Protokolldateien, die von virtuellen Anwendungen und von der Configuration Manager-Anwendungsverwaltung verwendet werden, finden Sie unter [Protokolldateien](../../core/plan-design/hierarchy/log-files.md).  

Unter Windows 8.1 finden Sie die Protokolle für den App-V-Client unter C:\ProgramData\Microsoft\Application Virtualization Client.  
