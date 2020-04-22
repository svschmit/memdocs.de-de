---
title: Einführung zu Softwareupdates
titleSuffix: Configuration Manager
description: Hier erhalten Sie grundlegende Informationen zu Softwareupdates in Configuration Manager.
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 10/30/2017
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: e9778b13-c8a3-40eb-8655-34ac8ce9cdaa
ms.openlocfilehash: c857997bdbeed51286e874dcbecf00b414dfe6a0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81699958"
---
# <a name="introduction-to-software-updates-in-configuration-manager"></a>Einführung in Softwareupdates in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Softwareupdates in Configuration Manager stellen eine Reihe von Tools und Ressourcen bereit, die die komplexe Aufgabe der Nachverfolgung und Anwendung von Softwareupdates auf Clientcomputern im Unternehmen vereinfachen. Ein effektiver Softwareupdate-Verwaltungsprozess ist erforderlich, um die Betriebseffektivität aufrechtzuerhalten, Sicherheitsprobleme zu beheben und die Stabilität der Netzwerkinfrastruktur zu gewährleisten. Da die Technologie sich kontinuierlich wandelt und immer wieder neue Sicherheitsrisiken auftreten, gebührt der effektiven Verwaltung von Softwareupdates besonderes Augenmerk.  

Ein Beispielszenario für die Bereitstellung von Softwareupdates in Ihrer Umgebung finden Sie unter [Example scenario for using System Center Configuration Manager to deploy and monitor the security software updates released monthly by Microsoft (Beispielszenario für die Verwendung von Configuration Manager zum Bereitstellen und Überwachen der monatlichen Sicherheitsupdates von Microsoft)](../deploy-use/example-scenario-deploy-monitor-monthly-security-updates.md).  

##  <a name="software-updates-synchronization"></a><a name="BKMK_Synchronization"></a> Softwareupdatesynchronisierung  
 Bei der Softwareupdatesynchronisierung in Configuration Manager werden Metadaten für Softwareupdates über eine Verbindung zu Microsoft Update abgerufen. Der Standort der obersten Ebene (Standort der zentralen Verwaltung oder eigenständiger primärer Standort) wird nach einem Zeitplan mit Microsoft Update synchronisiert. Über die Configuration Manager-Konsole können Sie die Synchronisierung auch manuell starten. Nachdem die Softwareupdatesynchronisierung am Standort der obersten Ebene abgeschlossen ist, wird sie von Configuration Manager ggf. an untergeordneten Standorten gestartet. Wenn die Synchronisierung an allen primären bzw. sekundären Standorten abgeschlossen ist, wird eine standortweite Richtlinie erstellt. Mit dieser Richtlinie werden Clientcomputer darüber informiert, wo die Softwareupdatepunkte sich befinden.  

> [!NOTE]  
>  Softwareupdates sind in Clienteinstellungen standardmäßig aktiviert. Wenn Sie aber für die Clienteinstellung **Softwareupdates auf Clients aktivieren** die Option **Nein** auswählen, um Softwareupdates in einer Sammlung oder in den Standardeinstellungen zu deaktivieren, werden die zugeordneten Clients nicht darüber informiert, wo die Softwareupdatepunkte sich befinden. Ausführlichere Informationen finden Sie im Abschnitt [Software Updates](../../core/clients/deploy/about-client-settings.md#software-updates) (Softwareupdates).  

 Nachdem die Richtlinie beim Client eingegangen ist, wird die Softwareupdatekonformität überprüft. Die Informationen werden vom Client in Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI) geschrieben. Anschließend werden die Konformitätsinformationen an den Verwaltungspunkt und von dort an den Standortserver gesendet. Weitere Informationen zur Compliancebewertung finden Sie im Abschnitt [Software updates compliance assessment](#BKMK_SUMCompliance) dieses Themas.  

 Sie können an einem primären Standort mehrere Softwareupdatepunkte installieren. Der zuerst installierte Softwareupdatepunkt wird als Synchronisierungsquelle konfiguriert. Hiermit erfolgt die Synchronisierung über Microsoft Update oder über einen WSUS-Server, der der Configuration Manager-Hierarchie nicht angehört. Der erste Softwareupdatepunkt wird von den übrigen Softwareupdatepunkten am Standort als Synchronisierungsquelle verwendet.  

> [!NOTE]  
>  Wenn die Softwareupdatesynchronisierung am Standort der obersten Ebene abgeschlossen ist, werden die Metadaten für Softwareupdates mithilfe der Datenbankreplikation an untergeordnete Standorte repliziert. Wenn Sie eine Verbindung zwischen einer Configuration Manager-Konsole und dem untergeordneten Standort herstellen, werden von Configuration Manager die Metadaten für Softwareupdates angezeigt. Allerdings ist es erst nach der Installation und Konfiguration eines Softwareupdatepunkts am Standort möglich, die Kompatibilität von Softwareupdates zu prüfen, Kompatibilitätsinformationen an Configuration Manager zu senden und Softwareupdates bereitzustellen.  

### <a name="synchronization-on-the-top-level-site"></a>Synchronisierung am Standort der obersten Ebene  
 Bei der Softwareupdatesynchronisierung am Standort der obersten Ebene werden von Microsoft Update die Metadaten für Softwareupdates abgerufen, die die in Eigenschaften der Softwareupdatepunktkomponente angegebenen Kriterien erfüllen. Sie konfigurieren die Kriterien nur am Standort der obersten Ebene.  

> [!NOTE]  
>  Sie können anstelle von Microsoft Updates einen vorhandenen WSUS-Server, der nicht der Configuration Manager-Hierarchie angehört, als Synchronisierungsquelle festlegen.  

 In der folgenden Liste werden die grundlegenden Schritte des Synchronisierungsprozesses am Standort der obersten Ebene beschrieben:  

1.  Die Softwareupdatesynchronisierung wird gestartet.  

2.  Vom WSUS-Synchronisierungs-Manager wird die Anforderung, die Synchronisierung mit Microsoft Update zu starten, an WSUS auf dem Softwareupdatepunkt gesendet.  

3.  Die Metadaten für Softwareupdates werden über Microsoft Update synchronisiert, und alle Änderungen werden in die WSUS-Datenbank eingefügt bzw. in dieser aktualisiert.  

4.  Wenn die Synchronisierung von WSUS abgeschlossen ist, werden die Metadaten für Softwareupdates aus der WSUS-Datenbank vom WSUS-Synchronisierungs-Manager mit der Configuration Manager-Datenbank synchronisiert. Alle Änderungen, die seit der letzten Synchronisierung vorgenommen wurden, werden in die Standortdatenbank eingefügt bzw. in dieser aktualisiert. Die Metadaten für Softwareupdates werden in der Standortdatenbank als Konfigurationselement gespeichert.  

5.  Die Konfigurationselemente für Softwareupdates werden mithilfe der Datenbankreplikation an untergeordnete Standorte gesendet.  

6.  Wenn die Synchronisierung erfolgreich abgeschlossen wurde, wird vom WSUS-Synchronisierungs-Manager die Statusmeldung 6702 ausgegeben.  

7.  Vom WSUS-Synchronisierungs-Manager wird eine Synchronisierungsanforderung an alle untergeordneten Standorte gesendet.  

8.  Vom WSUS-Synchronisierungs-Manager werden einzelne Anforderungen an WSUS auf anderen Softwareupdatepunkten des Standorts gesendet. Die WSUS-Server auf den übrigen Softwareupdatepunkten werden als Replikate von WSUS auf dem Standard-Softwareupdatepunkt am Standort konfiguriert.  

### <a name="synchronization-on-child-primary-and-secondary-sites"></a>Synchronisierung an untergeordneten primären Standorten und sekundären Standorten  
 Bei der Softwareupdatesynchronisierung am Standort der obersten Ebene werden die Konfigurationselemente für Softwareupdates mithilfe der Datenbankreplikation an untergeordnete Standorte repliziert. Am Ende des Prozesses wird vom Standort der obersten Ebene eine Synchronisierungsanforderung an den untergeordneten Standort gesendet. Daraufhin wird die WSUS-Synchronisierung vom untergeordneten Standort gestartet. Die folgende Liste enthält die grundlegenden Schritte für den Synchronisierungsprozess an einem untergeordneten primären Standort oder an einem sekundären Standort:  

1.  Beim WSUS-Synchronisierungs-Manager geht eine Synchronisierungsanforderung vom Standort der obersten Ebene ein.  

2.  Die Softwareupdatesynchronisierung wird gestartet.  

3.  Vom WSUS-Synchronisierungs-Manager wird die Anforderung, die Synchronisierung zu starten, an WSUS auf dem Softwareupdatepunkt gesendet.  

4.  Von WSUS auf dem Softwareupdatepunkt am untergeordneten Standort werden die von WSUS auf dem Softwareupdatepunkt am übergeordneten Standort stammenden Metadaten für Softwareupdates synchronisiert.  

5.  Wenn die Synchronisierung erfolgreich abgeschlossen wurde, wird vom WSUS-Synchronisierungs-Manager die Statusmeldung 6702 ausgegeben.  

6.  Vom WSUS-Synchronisierungs-Manager wird von einem primären Standort eine Synchronisierungsanforderung an alle untergeordneten sekundären Standorte gesendet. Am sekundären Standort wird die Softwareupdatesynchronisierung mit dem übergeordneten primären Standort gestartet. Der sekundäre Standort wird als Replikat von WSUS auf dem übergeordneten Standort konfiguriert.  

7.  Vom WSUS-Synchronisierungs-Manager werden einzelne Anforderungen an WSUS auf anderen Softwareupdatepunkten des Standorts gesendet. Die WSUS-Server auf den übrigen Softwareupdatepunkten werden als Replikate von WSUS auf dem Standard-Softwareupdatepunkt am Standort konfiguriert.  

##  <a name="software-updates-compliance-assessment"></a><a name="BKMK_SUMCompliance"></a> Software updates compliance assessment  
 Prüfen Sie vor der Bereitstellung von Softwareupdates auf Clientcomputern in Configuration Manager die Konformität der Clientcomputer mit den Softwareupdates. Für jedes Softwareupdate wird eine Zustandsmeldung mit dem Konformitätszustand für das Update erstellt. Die Zustandsmeldungen werden zusammen an den Verwaltungspunkt gesendet und anschließend an den Standortserver weitergeleitet, wo der Kompatibilitätszustand in die Standortdatenbank aufgenommen wird. Der Kompatibilitätszustand für Softwareupdates wird in der Configuration Manager-Konsole angezeigt. Sie können Softwareupdates auf Computern, auf denen die Updates erforderlich sind, bereitstellen und installieren. Die folgenden Abschnitte enthalten Informationen zu Kompatibilitätszuständen und eine Beschreibung des Überprüfungsprozesses der Softwareupdatekompatibilität.  

### <a name="software-updates-compliance-states"></a>Konformitätszustände von Softwareupdates  
 Im Folgenden finden Sie eine Beschreibung der Kompatibilitätszustände, die in der Configuration Manager-Konsole für Softwareupdates angezeigt werden.  

-   **Erforderlich**  

     Gibt an, dass das Softwareupdate für den Clientcomputer anwendbar und erforderlich ist. Der Softwareupdatezustand ist **Erforderlich**, wenn eine der folgenden Bedingungen erfüllt ist:  

    -   Das Softwareupdate wurde nicht für den Clientcomputer bereitgestellt.  

    -   Das Softwareupdate wurde auf dem Clientcomputer installiert. Allerdings wurde die letzte Zustandsmeldung bisher noch nicht in die Datenbank auf dem Standortserver eingefügt. Nach Abschluss der Installation wird der Clientcomputer erneut auf das Update überprüft. Der aktualisierte Zustand wird vom Client möglicherweise erst nach einer Verzögerung von bis zu zwei Minuten an den Verwaltungspunkt gesendet und von dort an den Standortserver weitergeleitet.  

    -   Das Softwareupdate wurde auf dem Clientcomputer installiert. Allerdings muss die Installation des Softwareupdates mit einem Computerneustart abgeschlossen werden.  

    -   Das Softwareupdate wurde für den Clientcomputer bereitgestellt, jedoch noch nicht installiert.  

-   **Nicht erforderlich**  

     Hiermit wird angegeben, dass das Softwareupdate nicht für den Clientcomputer gilt. Das Softwareupdate ist daher nicht erforderlich.  

-   **Installiert**  

     Gibt an, dass das Softwareupdate auf den Clientcomputer anwendbar ist und bereits installiert wurde.  

-   **Unbekannt**  

     Beim Standortserver ist keine Zustandsmeldung vom Clientcomputer eingegangen. Dies kann unter anderem einen der folgenden Gründe haben:  

    -   Der Clientcomputer konnte die Softwareupdatekompatibilität nicht erfolgreich überprüfen.  

    -   Die Überprüfung wurde auf dem Clientcomputer erfolgreich abgeschlossen. Die Zustandsmeldung wurde jedoch noch nicht auf dem Standortserver verarbeitet, was möglicherweise auf einen Rückstand von Zustandsmeldungen zurückzuführen ist.  

    -   Die Überprüfung auf dem Clientcomputer wurde erfolgreich abgeschlossen, die Zustandsmeldung jedoch noch nicht vom untergeordneten Standort empfangen.  

    -   Die Überprüfung auf dem Clientcomputer wurde erfolgreich abgeschlossen, die Zustandsmeldung ist jedoch in irgendeiner Form beschädigt und konnte nicht verarbeitet werden.  

### <a name="scan-for-software-updates-compliance-process"></a>Überprüfen der Softwareupdatekonformität  
 Wenn der Softwareupdatepunkt installiert und synchronisiert ist, wird eine standortweite Computerrichtlinie erstellt. Mit dieser Richtlinie werden Clientcomputer darüber informiert, dass Configuration Manager-Softwareupdates für den Standort aktiviert wurden. Beim Empfang der Computerrichtlinie durch einen Client wird eine Kompatibilitätsüberprüfung geplant, die innerhalb der nächsten zwei Stunden zufällig gestartet wird. Beim Start der Überprüfung wird der Überprüfungsverlauf vom Softwareupdateclient-Agent gelöscht. Außerdem wird eine Anforderung zum Suchen des WSUS-Servers übermittelt, der für die Überprüfung verwendet werden soll, und anhand des WSUS-Serverspeicherorts wird ein Update der lokalen Gruppenrichtlinie ausgeführt.  

> [!NOTE]  
>  Verbindungen zwischen internetbasierten Clients und dem WSUS-Server müssen mithilfe von SSL hergestellt werden.  

 Eine Überprüfungsanforderung wird an den Windows Update-Agent (WUA) geleitet. Daraufhin wird vom WUA eine Verbindung mit dem in der lokalen Richtlinie genannten Ort des WSUS-Servers hergestellt. Anschließend werden die auf dem WSUS-Server synchronisierten Metadaten für Softwareupdates abgerufen, und der Clientcomputer wird auf diese Updates überprüft. Von einem Prozess des Softwareupdateclient-Agents wird erkannt, dass die Kompatibilitätsüberprüfung abgeschlossen wurde. Für jedes Softwareupdate, dessen Kompatibilitätszustand sich seit der letzten Überprüfung geändert hat, werden Zustandsmeldungen erstellt. Die Zustandsmeldungen werden alle fünfzehn Minuten zusammen an den Verwaltungspunkt gesendet. Der Verwaltungspunkt leitet die Zustandsmeldungen dann an den Standortserver weiter, auf dem die Zustandsmeldungen in der Standortdatenbank gespeichert werden.  

 Nach der ersten Überprüfung der Kompatibilität von Softwareupdates wird die Überprüfung im konfigurierten Überprüfungszeitplan gestartet. Wenn die Kompatibilität von Softwareupdates vom Client jedoch innerhalb des durch die Gültigkeitsdauer (Time-to-Live, TTL) angegebenen Zeitrahmens überprüft wurde, werden vom Client die lokal gespeicherten Metadaten für Softwareupdates verwendet. Erfolgt die letzte Überprüfung außerhalb der Gültigkeitsdauer, muss vom Client eine Verbindung mit WSUS auf dem Softwareupdatepunkt hergestellt werden, und für die auf dem Client gespeicherten Metadaten für Softwareupdates muss ein Update ausgeführt werden.  

 Mithilfe des Überprüfungszeitplans kann die Überprüfung der Kompatibilität von Softwareupdates auf folgende Weise gestartet werden:  

-   **Zeitplan für Softwareupdateprüfung:** Die Überprüfung der Konformität von Softwareupdates beginnt gemäß dem Überprüfungszeitplan, der in den Einstellungen des Softwareupdateclient-Agents konfiguriert ist. Weitere Informationen zum Konfigurieren der Clienteinstellungen für Softwareupdates finden Sie im Abschnitt [Software Updates (Softwareupdates)](../../core/clients/deploy/about-client-settings.md#software-updates) im Thema „About client settings in System Center Configuration Manager“ (Informationen zu Clienteinstellungen in System Center Configuration Manager).  

-   **Aktion in den Configuration Manager-Eigenschaften:** Der Benutzer kann auf dem Clientcomputer im Dialogfeld **Configuration Manager-Eigenschaften** auf der Registerkarte **Aktion** die Aktion **Überprüfungszyklus für Softwareupdates** oder **Auswertungszyklus für Softwareupdatebereitstellung** starten.  

-   **Zeitplan für die erneute Bewertung der Bereitstellung:** Die Auswertung der Bereitstellung und die Überprüfung der Konformität von Softwareupdates beginnen gemäß dem Zeitplan für die erneute Auswertung von Bereitstellungen, der in den Einstellungen des Softwareupdateclient-Agents konfiguriert ist. Weitere Informationen zu den Clienteinstellungen für Softwareupdates finden Sie im Abschnitt „Software Updates“ (Softwareupdates) im Thema [About client settings in System Center Configuration Manager (Informationen zu Clienteinstellungen in Configuration Manager)](../../core/clients/deploy/about-client-settings.md#software-updates).  

-   **Vor dem Herunterladen von Updatedateien:** Wenn ein Clientcomputer eine Zuweisungsrichtlinie für eine neue erforderliche Bereitstellung empfängt, lädt der Softwareupdateclient-Agent die Softwareupdatedateien in den lokalen Clientcache herunter. Vor dem Download der Softwareupdatedatei wird vom Client-Agent im Rahmen einer Überprüfung bestätigt, dass das Softwareupdate noch erforderlich ist.  

-   **Vor der Softwareupdateinstallation:** Unmittelbar vor der Installation der Softwareupdates startet der Softwareupdateclient-Agent eine Überprüfung, um sicherzustellen, dass die Softwareupdates noch erforderlich sind.  

-   **Nach der Softwareupdateinstallation:** Unmittelbar nach dem Abschluss einer Softwareupdateinstallation startet der Softwareupdateclient-Agent eine Überprüfung, um sicherzustellen, dass die Softwareupdates nicht mehr erforderlich sind. Dann erstellt der Agent eine neue Zustandsmeldung, aus der hervorgeht, dass das Softwareupdate installiert ist. Wenn die Installation abgeschlossen ist, aber ein Neustart ausgeführt werden muss, geht aus der Zustandsmeldung hervor, dass auf dem Clientcomputer ein Neustart ansteht.  

-   **Nach dem Neustart des Systems:** Wenn auf das System eines Clientcomputer neu gestartet werden muss, damit die Installation eines Softwareupdates abgeschlossen werden kann, startet der Softwareupdateclient-Agent nach dem Neustart eine Überprüfung, um sicherzustellen, dass das Softwareupdate nicht mehr erforderlich ist. Dann erstellt der Agent eine Zustandsmeldung, aus der hervorgeht, dass das Softwareupdate installiert ist.  

#### <a name="time-to-live-value"></a>Gültigkeitsdauer  
 Die zum Überprüfen der Konformität von Softwareupdates erforderlichen Metadaten für Softwareupdates werden auf dem lokalen Clientcomputer gespeichert und sind standardmäßig bis zu 24 Stunden gültig. Dieser Wert wird als Gültigkeitsdauer (Time to Live, TTL) bezeichnet.  

#### <a name="scan-for-software-updates-compliance-types"></a>Überprüfungstypen für Softwareupdatekompatibilität  
 Die Überprüfung der Konformität von Softwareupdates durch den Client erfolgt entweder online oder offline sowie entweder erzwungenermaßen oder freiwillig. Welcher Überprüfungstyp verwendet wird, hängt davon ab, wie die Überprüfung der Konformität von Softwareupdates gestartet wurde. Im Folgenden wird beschrieben, welche Methoden zum Starten der Überprüfung online oder offline ausgeführt werden und ob die Überprüfung erzwungenermaßen oder freiwillig erfolgt.  

-   **Zeitplan für Softwareupdateprüfung** (freiwillige Onlineüberprüfung)  

     Vom Client wird gemäß konfiguriertem Überprüfungszeitplan nur dann eine Verbindung mit WSUS auf dem Softwareupdatepunkt hergestellt, um die Metadaten für Softwareupdates abzurufen, wenn die letzte Überprüfung außerhalb der Gültigkeitsdauer erfolgt ist.  

-   **Überprüfungszyklus für Softwareupdates** oder **Auswertungszyklus für Softwareupdatebereitstellung** (erzwungene Onlineüberprüfung)  

     Vom Clientcomputer wird vor der Überprüfung der Kompatibilität von Softwareupdates immer eine Verbindung mit WSUS auf dem Softwareupdatepunkt hergestellt, um die Metadaten für Softwareupdates abzurufen. Der Zähler für die Gültigkeitsdauer wird nach Abschluss der Überprüfung zurückgesetzt. Beträgt die Gültigkeitsdauer beispielsweise 24 Stunden, wird sie nach dem Start einer Überprüfung der Kompatibilität von Softwareupdates auf 24 Stunden zurückgesetzt.  

-   **Zeitplan für die erneute Bewertung der Bereitstellung** (freiwillige Onlineüberprüfung)  

     Vom Client wird gemäß konfiguriertem Zeitplan für die erneute Auswertung der Bereitstellungen nur dann eine Verbindung mit WSUS auf dem Softwareupdatepunkt hergestellt, um die Metadaten für Softwareupdates abzurufen, wenn die letzte Überprüfung außerhalb der Gültigkeitsdauer erfolgt ist.  

-   **Vor dem Herunterladen von Updatedateien** (freiwillige Onlineüberprüfung)  

     Vom Client wird bei erforderlichen Bereitstellungen vor dem Herunterladen der Updatedateien nur dann eine Verbindung mit WSUS auf dem Softwareupdatepunkt hergestellt, um die Metadaten für Softwareupdates abzurufen, wenn die letzte Überprüfung außerhalb der Gültigkeitsdauer erfolgt ist.  

-   **Vor der Softwareupdateinstallation** (freiwillige Onlineüberprüfung)  

     Vom Client wird bei erforderlichen Bereitstellungen vor dem Installieren von Softwareupdates nur dann eine Verbindung mit WSUS auf dem Softwareupdatepunkt hergestellt, um die Metadaten für Softwareupdates abzurufen, wenn die letzte Überprüfung außerhalb der Gültigkeitsdauer erfolgt ist.  

-   **Nach der Softwareupdateinstallation** (erzwungene Offlineüberprüfung)  

     Nach der Installation eines Softwareupdates wird vom Softwareupdateclient-Agent anhand der lokalen Metadaten eine Überprüfung gestartet. Vom Client wird keine Verbindung mit WSUS auf dem Softwareupdatepunkt hergestellt, um Metadaten für Softwareupdates abzurufen.  

-   **Nach dem Neustart des Systems** (erzwungene Offlineüberprüfung)  

     Nach der Installation eines Softwareupdates und nach dem Neustart des Computers wird vom Softwareupdateclient-Agent anhand der lokalen Metadaten eine Überprüfung gestartet. Vom Client wird keine Verbindung mit WSUS auf dem Softwareupdatepunkt hergestellt, um Metadaten für Softwareupdates abzurufen.  

##  <a name="software-update-deployment-packages"></a><a name="BKMK_DeploymentPackages"></a> Softwareupdate-Bereitstellungspakete  
 Mithilfe von Bereitstellungspaketen für Softwareupdates werden Softwareupdates in freigegebene Netzwerkordner heruntergeladen. Die Quelldateien des Softwareupdates werden dann in die Inhaltsbibliothek auf Standortservern und an Verteilungspunkten kopiert, die in der Bereitstellung definiert sind. Mit dem Assistenten zum Herunterladen von Updates können Sie Softwareupdates herunterladen und Bereitstellungspaketen hinzufügen, bevor diese bereitgestellt werden. Sie können mit dem Assistenten Softwareupdates an Verteilungspunkten bereitstellen und sich vom Erfolg dieses Teils des Bereitstellungsprozesses überzeugen, bevor Sie die Softwareupdates Clients bereitstellen.  

 Wenn Sie heruntergeladene Softwareupdates mit dem Assistenten zum Bereitstellen von Softwareupdates bereitstellen, wird bei der Bereitstellung automatisch das Bereitstellungspaket verwendet, das die Softwareupdates enthält. Werden Softwareupdates bereitgestellt, die nicht heruntergeladen wurden, müssen Sie im Assistenten zum Bereitstellen von Softwareupdates ein neues oder vorhandenes Bereitstellungspaket angeben. Die Softwareupdates werden dann heruntergeladen, wenn der Assistent abgeschlossen ist.  

> [!IMPORTANT]  
>  Sie müssen den freigegebenen Netzwerkordner für die Quelldateien des Bereitstellungspakets manuell erstellen, bevor Sie ihn im Assistenten angeben. Von jedem Bereitstellungspaket muss ein eigener freigegebener Ordner verwendet werden.  

> [!IMPORTANT]  
>  Sowohl das Computerkonto „SMS-Anbieter“ als auch der Administrator, der die Softwareupdates herunterlädt, muss über die Berechtigung **Schreiben** für die Paketquelle verfügen. Beschränken Sie den Zugriff auf die Paketquelle, um das Risiko zu verringern, dass die Quelldateien der Softwareupdates an der Paketquelle von Angreifern manipuliert werden.  

 Bei der Erstellung eines neuen Bereitstellungspakets wird die Inhaltsversion auf 1 festgesetzt, bevor Softwareupdates heruntergeladen werden. Wenn die Softwareupdatedateien über das Paket heruntergeladen werden, wird die Inhaltsversion auf 2 erhöht. Aus diesem Grund haben alle neuen Bereitstellungspakete anfänglich die Inhaltsversion 2. Bei jeder Änderung des Inhalts eines Bereitstellungspakets wird die Inhaltsversion um 1 erhöht. Weitere Informationen finden Sie unter [Fundamental concepts for content management in System Center Configuration Manager (Grundlegende Konzepte für das Content Management)](../../core/plan-design/hierarchy/fundamental-concepts-for-content-management.md).  

 Clients installieren die in einer Bereitstellung enthaltenen Softwareupdates mithilfe eines beliebigen Verteilungspunkts, auf dem die Softwareupdates verfügbar ist. Dies geschieht unabhängig vom Bereitstellungspaket. Wenn ein Bereitstellungspaket für eine aktive Bereitstellung gelöscht wird, können die Softwareupdates in der Bereitstellung dennoch weiterhin von Clients installiert werden. Dies setzt voraus, dass jedes Update in mindestens ein weiteres Bereitstellungspaket heruntergeladen wurde und auf einem Verteilungspunkt verfügbar ist, auf den der Client Zugriff hat. Wenn das letzte Bereitstellungspaket mit einem Softwareupdate gelöscht wird, kann das Softwareupdate erst wieder von Clientcomputern abgerufen werden, nachdem es erneut in ein Bereitstellungspaket heruntergeladen wurde. In der Configuration Manager-Konsole werden Softwareupdates mit einem roten Pfeil markiert, wenn sich die Updatedateien nicht in Bereitstellungspaketen befinden. Bereitstellungen werden mit einem roten Doppelpfeil angezeigt, wenn sie Updates in diesem Zustand enthalten.  

##  <a name="software-update-deployment-workflows"></a><a name="BKMK_DeploymentWorkflows"></a> Workflows für die Softwareupdatebereitstellung  
 Die Bereitstellung von Softwareupdates in einer Umgebung erfolgt entweder manuell oder automatisch. In der Regel werden Softwareupdates manuell bereitgestellt, um eine Basislinie für die Clientcomputer zu erstellen. Die Verwaltung der Softwareupdates auf Clients erfolgt dann durch die automatische Bereitstellung. Die folgenden Abschnitte enthalten einen Überblick über die Workflows bei der manuellen und automatischen Bereitstellung von Softwareupdates  

###  <a name="manual-deployment-of-software-updates"></a><a name="BKMK_ManualDeployment"></a> Manuelle Bereitstellung von Softwareupdates  
 Bei der manuellen Bereitstellung von Softwareupdates werden Softwareupdates in der Configuration Manager-Konsole ausgewählt, und der Bereitstellungsprozess wird manuell gestartet. Mit dieser Bereitstellungsmethode sorgen Sie in der Regel dafür, dass die aktuell erforderlichen Softwareupdates auf den Clientcomputern vorhanden sind, bevor Sie automatische Bereitstellungsregeln zur Verwaltung der laufenden monatlichen Softwareupdatebereitstellungen erstellen. Diese Methode dient auch dazu, Out-of-Band-Anforderungen für Softwareupdates bereitzustellen. Der allgemeine Workflow für die manuelle Bereitstellung von Softwareupdates umfasst die folgenden Schritte:  

1.  Filtern Sie Softwareupdates mit bestimmten Anforderungen heraus. Beispielsweise könnten Sie anhand geeigneter Kriterien angeben, dass alle Softwareupdates abgerufen werden sollen, die auf mehr als 50 Clientcomputern benötigt werden und deren Klassifizierung Sicherheit oder Kritisch lautet.  

2.  Erstellen Sie eine Softwareupdategruppe, die die Softwareupdates enthält.  

3.  Laden Sie den Inhalt für die Softwareupdates in der Softwareupdategruppe herunter.  

4.  Stellen Sie die Softwareupdategruppe manuell bereit.  

###  <a name="automatic-deployment-of-software-updates"></a><a name="BKMK_AutomaticDeployment"></a> Automatische Bereitstellung von Softwareupdates  
 Die automatische Bereitstellung von Softwareupdates wird mithilfe einer automatischen Bereitstellungsregel (ADR) konfiguriert. Diese Bereitstellungsmethode eignet sich insbesondere für monatliche Softwareupdates („Patch-Dienstag“) und für die Verwaltung von Definitionsupdates. Bei der Ausführung der Regel werden Softwareupdates aus der Softwareupdategruppe entfernt (bei Verwendung einer vorhandenen Gruppe), Softwareupdates, die einem angegebenen Kriterium (z. B. alle in der letzten Woche veröffentlichten Sicherheitsupdates der letzten Woche) entsprechen, zu einer Softwareupdategruppe hinzugefügt, die Inhaltsdateien für die Softwareupdates heruntergeladen und auf Verteilungspunkte kopiert und die Softwareupdates auf Clientcomputern in der Zielsammlung bereitgestellt. Der allgemeine Workflow für die automatische Bereitstellung von Softwareupdates umfasst die folgenden Schritte:  

1. Erstellen Sie eine automatische Bereitstellungsregel, von der unter anderem die folgenden Bereitstellungseinstellungen angegeben werden:  

   -   Zielsammlung  

   -   Aktivierung der Bereitstellung oder Erstellung eines Berichts zur Kompatibilität mit Softwareupdates für die Clientcomputer in der Zielsammlung  

   -   Kriterien für Softwareupdates  

   -   Auswertungs- und Bereitstellungszeitpläne  

   -   Benutzerfreundlichkeit  

   -   Downloadeigenschaften  

2. Die Softwareupdates werden einer Softwareupdategruppe hinzugefügt.  

3. Die Softwareupdategruppe wird auf den Clientcomputern in der Zielsammlung bereitgestellt, sofern diese angegeben ist.  

   Sie müssen eine Bereitstellungsstrategie für Ihre Umgebung auswählen. Beispielsweise könnten Sie eine automatische Bereitstellungsregel erstellen und eine Sammlung mit Testclients als Ziel angeben. Nachdem Sie sich vergewissert haben, dass die Softwareupdates in der Testgruppe installiert werden, können Sie eine neue Bereitstellung zur Regel hinzufügen oder in der vorhandenen Bereitstellung eine andere Zielsammlung angeben, die mehr Clients enthält. Die von den automatischen Bereitstellungsregeln erstellten Softwareupdateobjekte sind interaktiv.  

- Die mithilfe einer automatischen Bereitstellungsregel bereitgestellten Softwareupdates werden neuen Clients, die der Zielsammlung hinzugefügt werden, automatisch bereitgestellt.  

- Neue Softwareupdates, die einer Softwareupdategruppe hinzugefügt werden, werden den Clients in der Zielsammlung automatisch bereitgestellt.  

- Sie können Bereitstellungen für die automatische Bereitstellungsregel jederzeit aktivieren oder deaktivieren.  

  Nach der Erstellung einer automatischen Bereitstellungsregel können Sie zusätzliche Bereitstellungen zur Regel hinzufügen. Dies hilft Ihnen dabei, die Komplexität der Bereitstellung verschiedener Updates für verschiedene Sammlungen zu verwalten. Jede neue Bereitstellung verfügt über sämtliche Funktionen und die Bereitstellungsüberwachungsumgebung, und in jeder neu hinzugefügten Bereitstellung:  

- Werden die gleiche Upgradegruppe und das gleiche Upgradepaket verwendet, die bzw. das bei der ersten Ausführung der ADR erstellt wurde.  

- Kann eine andere Sammlung angegeben werden.  

- Werden eindeutige Bereitstellungseigenschaften unterstützt, einschließlich:  

  -   Aktivierungszeitpunkt  

  -   Stichtag  

  -   Endbenutzeroberfläche ein- oder ausblenden  

  -   Warnungen für diese Bereitstellung trennen  

##  <a name="software-update-deployment-process"></a><a name="BKMK_DeploymentProcess"></a> Vorgang der Softwareupdatebereitstellung  
 Nachdem Sie Softwareupdates bereitgestellt haben oder wenn bei der Ausführung einer automatischen Bereitstellungsregel Softwareupdates bereitgestellt werden, wird der Computerrichtlinie des Standorts eine Bereitstellungszuweisungsrichtlinie hinzugefügt. Die Softwareupdates werden vom Downloadort, aus dem Internet oder aus einem freigegebenen Netzwerkordner in die Paketquelle heruntergeladen. Dann werden die Softwareupdates aus der Paketquelle in die Inhaltsbibliothek auf dem Standortserver und anschließend in die Inhaltsbibliothek am Verteilungspunkt kopiert.  

 Wenn die Computerrichtlinie bei einem Clientcomputer in der Zielsammlung der Bereitstellung eingeht, wird vom Softwareupdateclient-Agent eine Bewertungsüberprüfung gestartet. Der Inhalt für erforderliche Softwareupdates wird vom Client-Agent von einem Verteilungspunkt in den lokalen Clientcache heruntergeladen. Dies erfolgt gemäß der Einstellung **Zeitpunkt der Verfügbarkeit der Software** für die Bereitstellung, zu dem die Softwareupdates für die Installation verfügbar sind. Die Softwareupdates in optionalen Bereitstellungen (d. h. Bereitstellungen ohne Installationsstichtag) werden erst heruntergeladen, wenn ein Benutzer die Installation manuell startet.  

 Wenn der konfigurierte Stichtag verstrichen ist, wird vom Softwareupdateclient-Agent im Rahmen einer Überprüfung bestätigt, dass die Softwareupdates noch erforderlich sind. Anschließend wird im lokalen Cache auf dem Clientcomputer überprüft, ob die Quelldateien für die Softwareupdates noch verfügbar sind. Schließlich werden die Softwareupdates vom Client installiert. Wurde der Inhalt aus dem Clientcache gelöscht, um für eine andere Bereitstellung Platz zu machen, werden die Softwareupdates vom Client erneut vom Verteilungspunkt in den Clientcache heruntergeladen. Softwareupdates werden unabhängig von der konfigurierten maximalen Größe des Clientcaches immer in den Clientcache heruntergeladen. Nach Abschluss der Installation wird vom Client-Agent im Rahmen einer Überprüfung bestätigt, dass die Softwareupdates nicht mehr erforderlich sind. Dann wird an den Verwaltungspunkt eine Zustandsmeldung gesendet, aus der hervorgeht, dass die Softwareupdates jetzt auf dem Client installiert sind.  

### <a name="required-system-restart"></a>Erforderlicher Neustart des Systems  
 Wenn Softwareupdates aus einer erforderlichen Bereitstellung auf einem Clientcomputer installiert werden und zum Abschluss der Installation ein Neustart des Systems erforderlich ist, wird der Systemneustart standardmäßig gestartet. Bei vor dem Stichtag installierten Softwareupdates wird der automatische Systemneustart bis zum Stichtag verschoben, sofern der Computer nicht aus einem anderen Grund vor diesem Zeitpunkt neu gestartet wird. Der Systemneustart kann für Server und Arbeitsstationen unterdrückt werden. Diese Einstellungen werden auf der Seite **Benutzerfreundlichkeit** des Assistenten zum Bereitstellen von Softwareupdates oder des Assistenten zum Erstellen automatischer Bereitstellungsregeln konfiguriert.  

### <a name="deployment-reevaluation-cycle"></a>Zyklus der erneuten Bereitstellungsbewertung  
 Von Clientcomputern wird standardmäßig alle 7 Tage ein Zyklus zur erneuten Auswertung der Bereitstellung gestartet. Während dieses Auswertungszyklus wird vom Clientcomputer nach bereits bereitgestellten und installierten Softwareupdates gesucht. Falls Softwareupdates fehlen, werden diese vom lokalen Cache aus neu installiert. Ist ein Softwareupdate nicht mehr im lokalen Cache verfügbar, wird es von einem Verteilungspunkt heruntergeladen und dann installiert. Sie können den Zeitplan für die erneute Auswertung in den Clienteinstellungen des Standorts auf der Seite **Softwareupdates** konfigurieren.  

##  <a name="support-for-windows-embedded-devices-that-use-write-filters"></a><a name="BKMK_EmbeddedDevices"></a> Unterstützung für Windows Embedded-Geräte mit Schreibfiltern  
 Beim Bereitstellen von Softwareupdates für Windows Embedded-Geräte mit aktivierten Schreibfiltern können Sie angeben, ob der Schreibfilter auf dem Gerät während der Bereitstellung deaktiviert und das Gerät nach der Bereitstellung neu gestartet werden soll. Wenn der Schreibfilter nicht deaktiviert wird, wird die Software auf einem temporären Overlay bereitgestellt und bei einem Neustart des Geräts nicht mehr installiert, es sei denn, die Beibehaltung der Änderungen wird durch eine andere Bereitstellung erzwungen.  

> [!NOTE]  
>  Stellen Sie beim Bereitstellen eines Softwareupdates auf einem Windows Embedded-Gerät sicher, dass das Gerät Mitglied einer Sammlung ist, für die ein Wartungsfenster konfiguriert ist. So können Sie verwalten, wann der Schreibfilter deaktiviert bzw. aktiviert ist und wann das Gerät neu gestartet wird.  

 Das Verhalten der Schreibfilter wird über eine Einstellung der Benutzerfreundlichkeit gesteuert, bei der es sich um das Kontrollkästchen **Änderungen zum Stichtag oder während eines Wartungsfensters ausführen (erfordert Neustart)** handelt.  

 Weitere Informationen dazu, wie Configuration Manager Embedded-Geräte verwaltet, die Schreibfilter verwenden, finden Sie unter [Planning for client deployment to Windows Embedded devices (Planen der Clientbereitstellung auf Windows Embedded-Geräten)](../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

##  <a name="extend-software-updates-in-configuration-manager"></a><a name="BKMK_ExtendSoftwareUpdates"></a> Erweitern von Softwareupdates in Configuration Manager  
 Mit System Center Updates Publisher können Sie Softwareupdates verwalten, die nicht über Microsoft Update verfügbar sind. Nachdem Sie die Softwareupdates auf dem Updateserver veröffentlicht und in Configuration Manager synchronisiert haben, können Sie sie für Configuration Manager-Clients bereitstellen. Weitere Informationen zu Updates Publisher finden Sie unter [Updates Publisher 2011](https://go.microsoft.com/fwlink/p/?LinkId=252947).  

## <a name="next-steps"></a>Nächste Schritte
[Planen von Softwareupdates](../plan-design/plan-for-software-updates.md)
