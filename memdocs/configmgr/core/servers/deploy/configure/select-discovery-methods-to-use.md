---
title: Auswählen von Ermittlungsmethoden
titleSuffix: Configuration Manager
description: Prüfen Sie die Überlegungen dazu, welche Methoden verwendet werden sollen und an welchen Standorten sie angewendet werden sollen.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 127ce713-d085-430f-ac7b-2701637fe126
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2f08ab44a11b48b4446a372c4f6065ea0d7c63e0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81700958"
---
# <a name="select-discovery-methods-to-use-for-configuration-manager"></a>Auswählen von Ermittlungsmethoden zur Verwendung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Damit Sie die Ermittlung für Configuration Manager erfolgreich und effizient nutzen können, müssen Sie überlegen, welche Methoden verwendet werden sollen und an welchen Standorten sie angewendet werden sollen.  

 Bei der Ermittlung kann hoher Netzwerkdatenverkehr entstehen, und bei der Verarbeitung der resultierenden Discovery Data Records (DDRs) werden möglicherweise erhebliche CPU-Ressourcen in Anspruch genommen. Sie sollten sich daher auf die Ermittlungsmethoden beschränken, die zur Erreichung Ihrer Ziele erforderlich sind. Möglicherweise genügen ein oder zwei Ermittlungsmethoden für Ihre Zwecke. Später können Sie weitere Methoden Schritt für Schritt hinzufügen, um die Ermittlung in Ihrer Umgebung auszuweiten. Anhand der Informationen in diesem Thema können Sie fundierte Entscheidungen treffen.  

 Informationen zu den einzelnen Ermittlungsmethoden finden Sie unter [Ermittlungsmethoden für Configuration Manager](../../../../core/servers/deploy/configure/about-discovery-methods.md).  

## <a name="select-methods-to-discover-different-things"></a>Auswählen von Methoden zum Ermitteln unterschiedlicher Dinge  
 Sie müssen geeignete Ermittlungsmethoden aktivieren, damit potenzielle Configuration Manager-Clientcomputer oder Benutzerressourcen ermittelt werden können. Sie können verschiedene Ermittlungsmethoden miteinander kombinieren, um verschiedene Ressourcen zu finden und zusätzliche Informationen zu diesen Ressourcen zu ermitteln. Durch die verwendeten Ermittlungsmethoden wird bestimmt, welcher Ressourcentyp ermittelt wird und welche Configuration Manager-Dienste und -Agents im Ermittlungsprozess eingesetzt werden. Auch die Art von Informationen, die Sie für Ressourcen ermitteln können, wird durch die Ermittlungsmethoden bestimmt.  

### <a name="discover-computers"></a>Computer ermitteln   
Zur Ermittlung von Computern können Sie die **Active Directory-Systemermittlung** oder die **Netzwerkermittlung** verwenden.  

 Wenn Sie beispielsweise Ressourcen ermitteln möchten, mit denen der Configuration Manager-Client vor dem Ausführen der Clientpushinstallation installiert werden kann, können Sie die Active Directory-Systemermittlung ausführen. Mit dieser Methode ermitteln Sie nicht nur die Ressource, sondern auch grundlegende Informationen. Über die Active Directory-Domänendienste können Sie sogar erweiterte Informationen ermitteln. Diese Informationen können sich beim Erstellen komplexer Abfragen und Sammlungen, mit denen Clienteinstellungen zugewiesen oder Inhalte bereitgestellt werden, als nützlich erweisen.

Alternativ können Sie die Netzwerkermittlung ausführen und mithilfe ihrer Optionen das Betriebssystem der Ressourcen ermitteln (für die spätere Clientpushinstallation erforderlich). Über die Netzwerkermittlung erhalten Sie Informationen über die Netzwerktopologie, die Ihnen andere Ermittlungsmethoden nicht liefern. Diese Methode liefert jedoch keine Informationen über die Active Directory-Umgebung.

 Es gibt auch eine Methode namens **Frequenzermittlung**. Es ist möglich, nur die Frequenzermittlung zu verwenden, um die Ermittlung von Clients zu erzwingen, die Sie mit anderen Methoden als der Clientpushinstallation installiert haben. Im Gegensatz zu anderen Ermittlungsmethoden können bei der Frequenzermittlung jedoch nur Computer mit einem aktiven Configuration Manager-Client ermittelt werden. Es wird eine begrenzte Anzahl von Informationen zurückgegeben. Dies dient der Wartung eines vorhandenen Datenbankdatensatzes, und nicht als Grundlage für diesen Datensatz. Die von der Frequenzermittlung bereitgestellten Informationen reichen möglicherweise nicht aus, um komplexe Abfragen oder Sammlungen zu erstellen.  

 Wenn Sie mithilfe der **Active Directory-Gruppenermittlung** die Mitgliedschaft einer bestimmten Gruppe ermitteln, können Sie beschränkte System- oder Computerinformationen ermitteln. Dies stellt zwar keinen Ersatz für eine vollständige Ermittlung von Computern dar, kann aber grundlegende Informationen liefern. Diese Informationen sind für die Clientpushinstallation unzureichend.  

### <a name="discover-users"></a>Ermitteln von Benutzern   
Zur Ermittlung von Informationen über Benutzer können Sie die **Active Directory-Benutzerermittlung** verwenden. Ähnlich wie bei der Active Directory-Systemermittlung ermittelt diese Methode Benutzer aus Active Directory. Sie enthält grundlegende Informationen sowie erweiterte Active Directory-Informationen. Mithilfe dieser Informationen können Sie ähnlich wie für Computer komplexe Abfragen und Sammlungen erstellen.  

### <a name="discover-group-information"></a>Ermitteln von Gruppeninformationen   
Zur Ermittlung von Informationen über Gruppen und Gruppenmitgliedschaften können Sie die **Active Directory-Gruppenermittlung** verwenden. Bei dieser Ermittlungsmethode werden Ressourceneinträge für Sicherheitsgruppen erstellt.  

 Mit dieser Methode können Sie eine bestimmte Active Directory-Gruppe durchsuchen, um die Mitglieder dieser Gruppe sowie alle in dieser Gruppe geschachtelten Gruppen zu identifizieren. Außerdem eignet sich diese Methode zum Durchsuchen eines Active Directory-Orts nach Gruppen sowie zum rekursiven Durchsuchen aller untergeordneten Container dieses Orts in den Active Directory-Domänendiensten.  

 Mit dieser Ermittlungsmethode kann auch die Mitgliedschaft von Verteilergruppen durchsucht werden. Dabei können die Gruppenbeziehungen von Benutzern und Computern identifiziert werden.  

 Beim Ermitteln einer Gruppe können Sie auch in begrenztem Umfang Informationen über die Mitglieder dieser Gruppe in Erfahrung bringen. Dies ersetzt jedoch nicht die Methoden der Active Directory-Systemermittlung oder -Benutzerermittlung. Es ist in der Regel nicht ausreichend, komplexe Abfragen und Sammlungen zu erstellen, oder als Grundlage für eine Clientpushinstallation zu dienen.  

### <a name="discover-infrastructure"></a>Ermitteln der Infrastruktur   
Für die Ermittlung der Netzwerkinfrastruktur stehen zwei Methoden zur Auswahl: die **Active Directory-Gesamtstrukturermittlung** und die **Netzwerkermittlung**.  

 Verwenden Sie die Active Directory-Gesamtstrukturermittlung, um eine Active Directory-Gesamtstruktur nach Informationen über Subnetze und Active Directory-Standortkonfigurationen zu durchsuchen. Diese Konfigurationen können dann automatisch in Configuration Manager als Grenzpositionen eingegeben werden.  

 Soll die Netzwerktopologie ermittelt werden, verwenden Sie die Netzwerkermittlung. Von anderen Ermittlungsmethoden werden zwar Informationen in Bezug auf die Active Directory-Domänendienste zurückgegeben, und der aktuelle Netzwerkort eines Clients kann identifiziert werden, aber es werden keine Infrastrukturinformationen auf Basis der Subnetze und der Routertopologie eines Netzwerks bereitgestellt.  

##  <a name="discovery-data-is-shared-among-sites"></a><a name="bkmk_shared"></a> Gemeinsame Nutzung von Ermittlungsdaten durch verschiedene Standorte  
 Nachdem in Configuration Manager Ermittlungsdaten einer Datenbank hinzugefügt wurden, werden diese Daten direkt für alle Standorte in der Hierarchie freigegeben. Da es in der Regel nicht sinnvoll ist, identische Informationen von mehreren Standorten in Ihrer Hierarchie zu ermitteln, empfiehlt es sich, für jede verwendete Ermittlungsmethode eine einzige Instanz auf einem einzigen Standort einzurichten. Dies ist besser, als mehrere Instanzen einer Methode auf verschiedenen Standorten auszuführen.  

 Allerdings kann es in manchen Umgebungen hilfreich sein, die gleiche Ermittlungsmethode mit einer separaten Konfiguration und einem eigenen Zeitplan auf mehreren Standorten ausführen zu lassen. Dies ist beispielsweise häufig nützlich, wenn nicht versucht wird, alle Netzwerkadressen in einem WAN zu ermitteln, sondern mit der Netzwerkermittlung jeder Standort angewiesen wird, sein lokales Netzwerk zu ermitteln.

Wenn Sie mehrere Instanzen der gleichen Ermittlungsmethoden zur Ausführung an verschiedenen Standorten einrichten, sollten Sie das Einrichten jedes Standorts sorgfältig planen. Sie sollten vermeiden, dass zwei oder mehr Standorte dieselben Ressourcen aus Ihrem Netzwerk oder Active Directory ermitteln. Dies kann zusätzliche Netzwerkbandbreite beanspruchen und Duplikate von DDRs erstellen.

In der folgenden Tabelle wird beschrieben, auf welchen Standorten Sie die verschiedenen Ermittlungsmethoden einrichten können.  

|Ermittlungsmethode|Unterstützte Standorte|  
|----------------------|-------------------------|  
|Active Directory-Gesamtstrukturermittlung|Standort der zentralen Verwaltung<br /><br /> Primärer Standort|  
|Active Directory-Gruppenermittlung|Primärer Standort|  
|Active Directory-Systemermittlung|Primärer Standort|  
|Active Directory-Benutzerermittlung|Primärer Standort|  
|Frequenzermittlung<sup>1</sup>|Primärer Standort|  
|Netzwerkermittlung|Primärer Standort<br /><br /> Sekundärer Standort|  

 <sup>1</sup> Auf sekundären Standorten kann die Frequenzermittlung nicht konfiguriert werden, jedoch ist es möglich, den Frequenz-DDR von einem Client zu empfangen.  

 Wenn auf sekundären Standorten die Netzwerkermittlung ausgeführt wird oder Frequenzermittlungs-DDRs empfangen werden, wird der DDR mithilfe von dateibasierter Replikation an deren übergeordneten primären Standort übertragen. Der Grund hierfür besteht darin, dass DDRs nur von primären Standorten und Standorten der zentralen Verwaltung verarbeitet werden können. Weitere Informationen zur Verarbeitung von DDRs finden Sie unter [About Discovery Data Records (Informationen zu Discovery Data Records)](../../../../core/servers/deploy/configure/run-discovery.md#BKMK_DDRs).  

## <a name="considerations-for-different-discovery-methods"></a>Überlegungen zu den verschiedenen Ermittlungsmethoden  
 Da jeder Standortserver und jede Netzwerkumgebung unterschiedlich ist, wird empfohlen, die anfänglichen Konfigurationen für die Ermittlung zu beschränken. Überwachen Sie dann bei jedem Standortserver genau, ob er die generierten Ermittlungsdaten verarbeiten kann.  

Wenn Sie eine **Active Directory**-Ermittlungsmethode für Systeme, Benutzer oder Gruppen verwenden:  

-   Führen Sie die Ermittlung auf einem Standort aus, der über eine schnelle Netzwerkverbindung mit Ihren Domänencontrollern verfügt.  

-   Beachten Sie die Active Directory-Replikationstopologie, um sicherzustellen, dass bei der Ermittlung Zugriff auf die neuesten Informationen besteht.  

-   Beachten Sie den Bereich der Ermittlungskonfiguration und beschränken Sie die Ermittlung auf diejenigen Active Directory-Orte und -Gruppen, die ermittelt werden müssen.  

Wenn Sie die **Netzwerkermittlung** verwenden:  

-   Verwenden Sie eine eingeschränkte Erstkonfiguration, um Ihre Netzwerktopografie zu identifizieren.  

-   Nachdem Sie Ihre Netzwerktopografie identifiziert haben, konfigurieren Sie die Netzwerkermittlung für die Ausführung auf bestimmten Standorten, die für diejenigen Netzwerkbereiche maßgeblich sind, die umfassender ermittelt werden sollen.  

Da die **Frequenzermittlung** nicht auf einem bestimmten Standort ausgeführt wird, müssen Sie diese Methode bei der allgemeinen Planung der Ermittlungsausführung nicht berücksichtigen.  

##  <a name="best-practices-for-discovery"></a><a name="bkmk_best"></a> Bewährte Methoden für die Ermittlung  
Für optimale Ergebnisse bei der Ermittlung wird Folgendes empfohlen:

- **Ausführen der Active Directory-Systemermittlung und Active Directory-Benutzerermittlung vor der Active Directory-Gruppenermittlung.**  

  Wenn bei der Active Directory-Gruppenermittlung ein bisher nicht ermittelter Computer als Mitglied einer Gruppe identifiziert wird, wird versucht, grundlegende Details für den Benutzer oder Computer zu ermitteln. Da die Active Directory-Gruppenermittlung für diese Art der Ermittlung nicht optimiert ist, kann dieser Prozess dazu führen, dass sich ihre Ausführung verlangsamt. Außerdem werden bei der Active Directory-Gruppenermittlung nur die grundlegenden Details zu den ermittelten Benutzern und Computern identifiziert, und es wird kein vollständiger Benutzer- oder Computerermittlungsdatensatz erstellt. Beim Ausführen der Active Directory-Systemermittlung und Active Directory-Benutzerermittlung sind die zusätzlichen Active Directory-Attribute für jeden Objekttyp verfügbar. Dadurch kann die Active Directory-Gruppenermittlung effizienter ausgeführt werden.  

- **Ausschließliches Angeben von Gruppen, die Sie mit Configuration Manager verwenden, beim Konfigurieren der Active Directory-Gruppenermittlung.**  

  Geben Sie nur die Gruppen an, die Sie mit Configuration Manager verwenden, um die Ressourcennutzung der Active Directory-Gruppenermittlung besser steuern zu können. Dies liegt daran, dass bei der Active Directory-Gruppenermittlung jede ermittelte Gruppe rekursiv nach Benutzern, Computern und verschachtelten Gruppen durchsucht wird. Das Durchsuchen aller verschachtelten Gruppen kann dazu führen, dass sich der Umfang der Active Directory-Gruppenermittlung vergrößert und die Leistung beeinträchtigt wird. Wenn Sie die Deltaermittlung für die Active Directory-Gruppenermittlung konfigurieren, wird zudem von der Ermittlungsmethode jede Gruppe auf Änderungen überwacht. Dadurch wird die Leistung noch stärker beeinträchtigt, da nicht erforderliche Gruppen durchsucht werden müssen.  

- **Konfigurieren von Ermittlungsmethoden mit einem längeren Intervall zwischen der vollständigen Ermittlung und häufigeren Zeiträumen für die Deltaermittlung.**  

  Da bei der Deltaermittlung weniger Ressourcen als bei einem vollständigen Ermittlungszyklus genutzt werden und neue oder geänderte Ressourcen in Active Directory identifiziert werden können, können Sie die Häufigkeit der vollständigen Ermittlungszyklen auf einmal pro Woche (oder weniger) reduzieren. Bei der Deltaermittlung für die Active Directory-Systemermittlung, Active Directory-Benutzerermittlung und Active Directory-Gruppenermittlung werden nahezu alle Änderungen von Active Directory-Objekten identifiziert, und für Ressourcen können genaue Ermittlungsdaten vorgehalten werden.  

- **Ausführen von Active Directory-Ermittlungsmethoden an einem primären Standort mit einem Netzwerkspeicherort, der über die geringste Entfernung zum Active Directory-Domänencontroller verfügt.**  

  Zur Verbesserung der Leistung einer Active Directory-Ermittlung wird empfohlen, die Ermittlung an einem primären Standort auszuführen, der über eine schnelle Netzwerkverbindung zu den Domänencontrollern verfügt. Wenn Sie die gleiche Active Directory-Ermittlungsmethode an mehreren Standorten ausführen, wird empfohlen, zum Vermeiden einer Überlappung jede Ermittlungsmethode separat zu konfigurieren. Im Gegensatz zu den vorherigen Versionen von Configuration Manager sind die Ermittlungsdaten für die Nutzung durch andere Standorte freigegeben. Daher ist es nicht erforderlich, an mehreren Standorten die gleichen Informationen zu ermitteln. Weitere Informationen finden Sie unter [Gemeinsame Nutzung von Ermittlungsdaten durch verschiedene Standorte](../../../../core/servers/deploy/configure/select-discovery-methods-to-use.md#bkmk_shared).  

- **Ausführen der Active Directory-Gesamtstrukturermittlung an nur einem Standort, wenn Sie die automatische Erstellung von Grenzen aus den Ermittlungsdaten planen.**  

  Wenn Sie die Active Directory-Gesamtstrukturermittlung in einer Hierarchie an mehr als einem Standort ausführen, wird empfohlen, Optionen zum automatischen Erstellen von Grenzen an nur einem einzelnen Standort zu aktivieren. Der Grund ist, dass Grenzen von Configuration Manager nicht zu einem einzelnen Grenzobjekt zusammengeführt werden können, wenn die Active Directory-Gesamtstrukturermittlung an jedem Standort ausgeführt wird und Grenzen erstellt werden. Wenn Sie die Active Directory-Gesamtstrukturermittlung so konfigurieren, dass Grenzen an mehreren Standorten automatisch erstellt werden, können sich in der Configuration Manager-Konsole doppelte Grenzobjekte ergeben.  
