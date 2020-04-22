---
title: Zuweisen von Clients zu einem Standort
titleSuffix: Configuration Manager
description: Weisen Sie Clients einem Standort in Configuration Manager zu.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: ba9b623f-6e86-4006-93f2-83d563de0cd0
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 32944157759e537c5b01061ab8648f242cfdac57
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693568"
---
# <a name="how-to-assign-clients-to-a-site-in-configuration-manager"></a>Zuweisen von Clients zu einem Standort in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Nachdem ein Configuration Manager-Client installiert wurde, muss er einem primären Configuration Manager-Standort beitreten, bevor er verwaltet werden kann. Der Standort, mit dem ein Client verbunden wird, wird als sein *zugewiesener Standort* bezeichnet. Clients können weder einem Standort der zentralen Verwaltung noch einem sekundären Standort zugewiesen werden.  

Die Zuweisung erfolgt nach der erfolgreichen Installation des Clients. Durch sie wird bestimmt, von welchem Standort der Clientcomputer verwaltet wird. Sie können den Client entweder direkt einem Standort zuweisen oder die automatische Standortzuweisung verwenden, bei der automatisch ein geeigneter Standort für den Client basierend auf seinem aktuellen Netzwerkspeicherort oder ein für die Hierarchie konfigurierter Fallbackstandort ermittelt wird.

Wenn Sie den Client des mobilen Geräts während der Configuration Manager-Anmeldung installieren, wird das Gerät stets automatisch einem Standort zugewiesen. Wenn Sie den Client auf einem Computer installieren, können Sie auswählen, ob der Client einem Standort zugewiesen werden soll oder nicht. Wenn der Client jedoch installiert aber nicht zugewiesen ist, kann der Client nicht verwaltet werden, bis die Standortzuweisung erfolgreich vorgenommen wurde.  
 

> [!NOTE]  
>  Weisen Sie Clients stets Standorten zu, auf denen dieselbe Version von Configuration Manager ausgeführt wird. Weisen Sie einem Standort eines älteren Releases keinen Configuration Manager-Client eines neueren Releases zu.   Aktualisieren Sie gegebenenfalls den primären Standort auf dieselbe Configuration Manager-Version, die Sie für die Clients verwenden.  

Nachdem der Client einem Standort zugewiesen wurde, bleibt er auch dann diesem Standort zugewiesen, wenn seine IP-Adresse geändert wird und er zu einem anderen Standort wechselt. Nur ein Administrator kann den Client manuell einem anderen Standort zuweisen oder die Clientzuweisung entfernen.  

> [!WARNING]  
>  Eine Ausnahme zu einem dem Standort zugewiesenen Client ist die Zuweisung des Clients zu einem Windows Embedded-Gerät bei aktivierten Schreibfiltern. Wenn Sie nicht zuerst die Schreibfilter deaktivieren, bevor Sie den Client zuordnen, dann wechselt der Standortzuweisungsstatus des Clients beim nächsten Neustart des Geräts in seinen ursprünglichen Zustand zurück.  
>   
>  Wenn der Client beispielsweise für die automatische Standortzuweisung konfiguriert ist, wird er beim Start neu zugewiesen und möglicherweise zu einem anderen Standort zugewiesen. Wenn der Client nicht für die automatische Standortzuweisung konfiguriert ist, sondern eine manuelle Standortzuweisung erfordert, müssen Sie den Client nach dem Start manuell erneut zuweisen, bevor Sie diesen Client mit Configuration Manager erneut verwalten können.  
>   
>  Deaktivieren Sie zum Vermeiden dieses Verhaltens die Schreibfilter, bevor Sie den Client auf Embedded-Geräten zuweisen, und aktivieren Sie die Filter, nachdem Sie sichergestellt haben, dass die Standortzuweisung erfolgreich war.  

Tritt bei der Zuweisung des Clients ein Fehler auf, bleibt die Clientsoftware weiterhin installiert, der Client wird allerdings nicht verwaltet. Ein Client wird als nicht verwaltet betrachtet, wenn er installiert, aber keinem Standort zugewiesen ist, oder wenn er einem Standort zugewiesen ist, aber die Kommunikation mit einem Verwaltungspunkt nicht möglich ist.  

##  <a name="using-manual-site-assignment-for-computers"></a>Verwenden der manuellen Standortzuweisung für Computer  
 Die manuelle Zuweisung von Clientcomputern zu einem Standort kann über folgenden zwei Methoden erfolgen:  

-   Durch Angabe des Standortcodes mithilfe einer Clientinstallationseigenschaft  

-   Durch Angabe des Standortcodes über die Systemsteuerung im Modul **Configuration Manager**  

> [!NOTE]  
>  Wird ein Clientcomputer manuell einem nicht vorhandenen Configuration Manager-Standortcode zugewiesen, tritt bei der Standortzuweisung ein Fehler auf.   

##  <a name="using-automatic-site-assignment-for-computers"></a><a name="BKMK_AutomaticAssignment"></a> Verwenden der automatischen Standortzuweisung für Computer  
 Die automatische Standortzuweisung kann im Rahmen der Clientbereitstellung stattfinden oder, indem Sie in der Systemsteuerung in **Configuration Manager-Eigenschaften** auf der Registerkarte **Erweitert** auf **Standortsuche** klicken. Der Netzwerkpfad des Configuration Manager-Clients wird mit den in der Configuration Manager-Hierarchie konfigurierten Grenzen verglichen. Fällt der Netzwerkpfad des Clients in eine Begrenzungsgruppe, die für die Standortzuweisung aktiviert ist, oder ist die Hierarchie für einen Fallbackstandort konfiguriert, dann wird der Client automatisch diesem Standort zugewiesen, ohne dass Sie einen Standortcode angeben müssen.  

 Sie können Grenzen über die folgenden Elemente konfigurieren:  

-   IP-Subnetz  

-   Active Directory-Standort  

-   IPv6-Präfix  

-   IP-Adressbereich  

> [!NOTE]  
>  Wenn ein Configuration Manager-Client über mehrere Netzwerkadapter und somit über mehrere IP-Adressen verfügt, wird die IP-Adresse, die zum Auswerten der Clientstandortzuweisung verwendet wird, nach dem Zufallsprinzip zugewiesen.  

 Informationen dazu, wie Sie Begrenzungsgruppen für die Standortzuweisung konfigurieren und wie Sie einen Fallbackstandort für die automatische Standortzuweisung konfigurieren, finden Sie unter [Definieren von Standortgrenzen und Begrenzungsgruppen für Configuration Manager](../../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).  

 Configuration Manager-Clients, die die automatische Zuweisung verwenden, versuchen, Standortbegrenzungsgruppen zu finden, die in Active Directory Domain Services veröffentlicht wurden. Tritt hierbei ein Fehler auf (z.B., wenn das Active Directory-Schema nicht für Configuration Manager erweitert ist oder es sich bei Clients um Arbeitsgruppencomputer handelt), können die Informationen zu Begrenzungsgruppen für Clients über einen Verwaltungspunkt gesucht werden.  

 Sie können einen Verwaltungspunkt zur Verwendung durch installierte Clientcomputer angeben, oder Clients die Suche eines Verwaltungspunkts mithilfe von DNS-Veröffentlichung oder WINS ermöglichen.  

 Wenn die Suche nach einem Standort, der einer Begrenzungsgruppe zugeordnet ist, die den Netzwerkpfad des Clients enthält, erfolglos ist und die Hierarchie nicht über einen Fallbackstandort verfügt, wird die Suche vom Client alle zehn Minuten wiederholt, bis er einem Standort zugewiesen werden kann.  

 Falls eine der folgenden Bedingungen zutrifft, können Configuration Manager-Clientcomputer nicht automatisch einem Standort zugewiesen werden, sondern sie müssen dann manuell zugewiesen werden:  

-   Sie sind momentan einem Standort zugewiesen.  

-   Sie befinden sich im Internet oder sind nur für Internetverbindungen konfiguriert.  

-   Ihr Netzwerkpfad liegt nicht innerhalb einer der konfigurierten Begrenzungsgruppen in der Configuration Manager-Hierarchie, und es ist kein Fallbackstandort für die Hierarchie definiert.  

##  <a name="completing-site-assignment-by-checking-site-compatibility"></a>Abschließen der Standortzuweisung durch Überprüfen der Standortkompatibilität  
 Nachdem der zugewiesene Standort für einen Client gefunden wurde, werden Version und Betriebssystem des Clients überprüft, um sicherzustellen, dass er von einem Configuration Manager-Standort verwaltet werden kann. Configuration Manager kann z.B. keine Configuration Manager 2007-Clients, System Center 2012 Configuration Manager-Clients oder Clients, auf denen Windows 2000 ausgeführt wird, verwalten.  

 Die Standortzuweisung schlägt fehl, wenn Sie einen Client, auf dem Windows 2000 ausgeführt wird, einem Configuration Manager-Standort zuweisen. Wenn Sie einen Configuration Manager 2007-Client oder einen System Center 2012 Configuration Manager-Client zu einem Configuration Manager-Standort (Current Branch) zuweisen, unterstützt die Standortzuweisung automatische Clientupgrades. Bis für Clients der älteren Generation jedoch ein Upgrade auf den Configuration Manager-Client (Current Branch) ausgeführt wird, kann dieser Client von Configuration Manager nicht über Clienteinstellungen, Anwendungen oder Softwareupdates verwaltet werden.  

> [!NOTE]  
>  Um die Standortzuweisung eines Configuration Manager 2007- oder eines System Center 2012 Configuration Manager-Clients zu einem Configuration Manager-Standort (Current Branch) zu unterstützen, müssen Sie das automatische Clientupgrade für die Hierarchie konfigurieren. Weitere Informationen finden Sie unter [Aktualisieren von Clients für Windows-Computer](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md).  

Configuration Manager prüft darüber hinaus, ob der Configuration Manager-Client (Current Branch) einem Standort zugewiesen wurde, der den Client unterstützt. Die folgenden Szenarios können bei einer Migration von früheren Versionen von Configuration Manager auftreten.  

- Szenario: Sie haben die automatische Standortzuweisung verwendet, und die Grenzen überschneiden sich mit den in einer vorherigen Version von Configuration Manager definierten Grenzen.  

   In diesem Fall versucht der Client automatisch, einen Configuration Manager-Standort (Current Branch) zu finden.  

   Zunächst wird Active Directory Domain Services vom Client überprüft, und wenn ein veröffentlichter Configuration Manager-Standort (Current Branch) gefunden wird, wird die Standortzuweisung erfolgreich durchgeführt. Schlägt dies fehl (der Configuration Manager-Standort wird beispielsweise nicht veröffentlicht, oder der Computer ist ein Arbeitsgruppenclient), wird vom Client nach Standortinformationen von seinem zugewiesenen Verwaltungspunkt gesucht.  

  > [!NOTE]  
  >  Während der Clientinstallation können Sie dem Client einen Verwaltungspunkt zuordnen, indem Sie die Client.msi-Eigenschaft **SMSMP=&lt;server_name>** verwenden.  

   Wenn beide Methoden fehlschlagen, dann schlägt auch die Standortzuweisung fehl und Sie müssen den Client manuell zuweisen.  

- Szenario: Sie haben den Configuration Manager-Client (Current Branch) mithilfe eines spezifischen Standortcodes anstelle der automatischen Standortzuweisung zugewiesen und versehentlich einen Standortcode für eine Configuration Manager-Version vor System Center 2012 R2 Configuration Manager angegeben.  

   In diesem Fall ist die Standortzuweisung nicht erfolgreich, und Sie müssen den Client manuell einem Configuration Manager-Standort (Current Branch) neu zuweisen.  

  Zur Überprüfung der Standortkompatibilität muss eine der folgenden Bedingungen erfüllt sein:  

- Der Client kann auf Standortinformationen zugreifen, die in Active Directory-Domänendiensten veröffentlicht sind.  

- Der Client kann mit einem Verwaltungspunkt auf dem Standort kommunizieren.  

  Wenn die Überprüfung der Standortkompatibilität nicht vollständig abgeschlossen werden kann, schlägt die Standortzuweisung fehl, und der Client wird so lange nicht verwaltet, bis die Überprüfung der Standortkompatibilität wiederholt und erfolgreich abgeschlossen wurde.  

  Eine Ausnahme bei der Durchführung dieser Standortkompatibilitätsprüfung tritt dann ein, wenn ein Client für einen internetbasierten Verwaltungspunkt konfiguriert wird. In diesem Fall findet keine Standortkompatibilitätsprüfung statt. Wenn Sie Clients einem Standort mit internetbasierten Standortsystemen zuweisen und einen internetbasierten Verwaltungspunkt angeben, achten Sie darauf, dass Sie den Client dem richtigen Standort zuweisen. Wenn Sie den Client fälschlicherweise einem Configuration Manager 2007-Standort, einem System Center 2012 Configuration Manager-Standort oder einem Configuration Manager-Standort zuweisen, der keine internetbasierten Standortsystemrollen aufweist, wird der Client nicht verwaltet.  

##  <a name="locating-management-points"></a>Suchen von Verwaltungspunkten  
 Nachdem ein Client erfolgreich einem Standort zugewiesen wurde, wird von diesem ein Verwaltungspunkt am Standort geortet.  

 Durch Clientcomputer wird eine Liste von Verwaltungspunkten heruntergeladen, mit denen am Standort eine Verbindung hergestellt werden kann. Dies passiert bei jedem Neustart des Clients, alle 25 Stunden oder wenn vom Client eine Netzwerkänderung festgestellt wird (z.B. wenn der Computer die Verbindung zum Netzwerk unterbricht und neu aufbaut oder wenn er eine neue IP-Adresse bezieht). Zur Liste gehören Verwaltungspunkte im Intranet und Informationen dazu, ob von diesen Clientverbindungen über HTTP oder HTTPS akzeptiert werden. Wenn für einen Clientcomputer, der sich im Internet befindet, noch keine Liste von Verwaltungspunkten verfügbar ist, wird eine Verbindung mit dem angegebenen internetbasierten Verwaltungspunkt hergestellt, um eine Liste von Verwaltungspunkten abzurufen. Wenn für den Client eine Liste von Verwaltungspunkten für dessen zugewiesenen Standort verfügbar ist, wird ein Verwaltungspunkt für die Verbindung ausgewählt:  

-   Wenn der Client sich im Intranet befindet und über ein gültiges PKI-Zertifikat verfügt, wird HTTPS-Verwaltungspunkten Vorrang vor HTTP-Verwaltungspunkten gegeben. Dann wird der nächste Verwaltungspunkt basierend auf seiner Gesamtstrukturmitgliedschaft gesucht.  

-   Wenn sich der Client im Internet befindet, wählt er nach dem Zufallsprinzip einen der internetbasierten Verwaltungspunkte aus.  

Von Clients mobiler Geräte, die von Configuration Manager angemeldet wurden, wird nur eine Verbindung mit einem Verwaltungspunkt an ihrem zugewiesenen Standort hergestellt, und niemals mit Verwaltungspunkten an sekundären Standorten. Von diesen Clients wird immer eine Verbindung über HTTPS hergestellt und der Verwaltungspunkt muss so konfiguriert sein, dass Clientverbindungen über das Internet zugelassen werden. Wenn am primären Standort für Clients mobiler Geräte mehrere Verwaltungspunkte zur Verfügung stehen, wird von Configuration Manager während der Zuweisung einer dieser Verwaltungspunkte nach dem Zufallsprinzip ausgewählt, und dieser Verwaltungspunkt wird ab diesem Zeitpunkt vom Client des mobilen Geräts verwendet.  

Wenn der Client die Clientrichtlinie von einem Verwaltungspunkt seines Standorts heruntergeladen hat, ist der Client ein verwalteter Client.  

##  <a name="downloading-site-settings"></a>Herunterladen von Standorteinstellungen  
 Nachdem der Client erfolgreich einem Standort zugewiesen und ein Verwaltungspunkt gefunden wurde, werden von einem Clientcomputer, auf dem Active Directory-Domänendienste für die Standortkompatibilitätsprüfung verwendet werden, clientrelevante Standorteinstellungen für den zugewiesenen Standort heruntergeladen. Zu diesen Einstellungen zählen die Auswahlkriterien für das Clientzertifikat, Informationen dazu, ob eine Zertifikatsperrliste verwendet werden soll, und die Anforderungsportnummern für den Client. Der Client überprüft diese Einstellungen weiterhin regelmäßig.  

 Wenn es Clientcomputern nicht möglich ist, die Standorteinstellungen von den Active Directory-Domänendiensten abzurufen, werden diese von ihren Verwaltungspunkten heruntergeladen. Es ist auch möglich, den Clientcomputern die Standorteinstellungen bei ihrer Installation mithilfe der Clientpushinstallation bereitzustellen oder sie mithilfe von CCMSetup.exe und den Clientinstallationseigenschaften manuell anzugeben. Weitere Informationen zu den Clientinstallationseigenschaften finden Sie unter [Informationen zu Clientinstallationseigenschaften](../../../core/clients/deploy/about-client-installation-properties.md).  

##  <a name="downloading-client-settings"></a>Herunterladen von Clienteinstellungen  
 Die standardmäßige Clienteinstellungsrichtlinie sowie jede relevante benutzerdefinierte Clienteinstellungsrichtlinie wird von allen Clients heruntergeladen. Das Softwarecenter ist von diesen Clientkonfigurationsrichtlinien für Windows-Computer abhängig, und Benutzer werden benachrichtigt, dass das Softwarecenter erst erfolgreich ausgeführt werden kann, wenn diese Konfigurationsinformationen heruntergeladen wurden. Je nachdem, welche Clienteinstellungen konfiguriert wurden, kann das erste Herunterladen der Clienteinstellungen einige Zeit in Anspruch nehmen, und möglicherweise können einige Clientverwaltungstasks erst nach Abschluss dieses Prozesses ausgeführt werden.  

##  <a name="verifying-site-assignment"></a>Überprüfen der Standortzuweisung  
 Mithilfe der folgenden Methoden können Sie überprüfen, ob die Standortzuweisung erfolgreich war:  

-   Verwenden Sie für Clients auf Windows-Computern Configuration Manager in der Systemsteuerung und stellen Sie sicher, dass der Standortcode auf der Registerkarte **Standort** korrekt angezeigt wird.  

-   Verwenden Sie für Clientcomputer im Arbeitsbereich **Bestand und Konformität** den Knoten **Geräte**, um sicherzustellen, dass vom Computer für die Spalte **Client** die Option **Ja** und für die Spalte **Standortcode** der korrekte Code des primären Standorts angezeigt wird.  

-   Verwenden Sie für Clients von mobilen Geräten im Arbeitsbereich **Bestand und Kompatibilität** den Knoten **Alle Mobilgeräte** , um sicherzustellen, dass vom Computer für die Spalte **Client** die Option **Ja** sowie der korrekter Code des primären Standorts für die Spalte **Standortcode** angezeigt wird.  

-   Verwenden Sie die Berichte für Clientzuweisung und die Anmeldung von mobilen Geräten.  

-   Verwenden Sie für Clientcomputer die LocationServices.log-Datei auf dem Client.  

##  <a name="roaming-to-other-sites"></a>Roaming an andere Standorte  
 Wenn Clientcomputer im Intranet zu einem primären Standort zugewiesen sind, deren Netzwerkort aber so geändert wird, dass er in einer für einen anderen Standort konfigurierten Begrenzungsgruppe liegt, dann wechseln sie per Roaming an einen anderen Standort. Wenn dieser Standort ein sekundärer Standort für ihren zugewiesenen Standort ist, kann von Clients ein Verwaltungspunkt am sekundären Standort verwendet werden, um eine Clientrichtlinie herunterzuladen und Clientdaten hochzuladen. So wird vermieden, dass die Daten über ein möglicherweise langsames Netzwerk versendet werden. Wenn diese Clients jedoch per Roaming in die Begrenzungen für einen anderen primären Standort gelangen oder an einen sekundären Standort, der kein untergeordneter Standort ihres zugewiesenen Standorts ist, dann wird für diese Clients immer ein Verwaltungspunkt an deren zugewiesenem Standort verwendet, um eine Clientrichtlinie herunterzuladen oder Daten auf ihren Standort hochzuladen.  

 Für diese Clientcomputer, für die per Roaming ein Wechsel an andere Standorte vorgenommen wird (alle primären und alle sekundären Standorte), können immer Verwaltungspunkte an anderen Standorten für Anfragen zum Inhaltsort verwendet werden. Über die Verwaltungspunkte am aktuellen Standort kann Clients eine Liste an Verteilungspunkten zur Verfügung gestellt werden, an denen der von Clients angeforderte Inhalt verfügbar ist.  

 Bei Clientcomputern, die für eine Clientverwaltung ausschließlich über das Internet konfiguriert wurden, sowie bei mobilen Geräten und Macintosh-Computern, die von Configuration Manager angemeldet wurden, können diese Clients nur mit Verwaltungspunkten an ihrem zugewiesenen Standort kommunizieren. Für diese Clients ist keine Verbindung mit Verwaltungspunkten an sekundären Standorten oder an anderen primären Standorten hergestellt werden.  
