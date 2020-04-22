---
title: Sicherheit und Datenschutz für die Betriebssystembereitstellung
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über bewährte Methoden für Sicherheit und Datenschutz bei der Betriebssystembereitstellung in Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 5ee5928f-3d72-4b00-8156-1e0d1030a96c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 53256889b8bbd6a9608748a57de33b38be77cfd8
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709328"
---
# <a name="security-and-privacy-for-os-deployment-in-configuration-manager"></a>Sicherheit und Datenschutz bei der Betriebssystembereitstellung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Dieser Artikel enthält Sicherheits- und Datenschutzinformationen für die Betriebssystembereitstellung in Configuration Manager.  



##  <a name="security-best-practices-for-os-deployment"></a><a name="bkmk_security"></a> Bewährte Sicherheitsmethoden bei der Betriebssystembereitstellung  

Wenden Sie die folgenden bewährten Sicherheitsmethoden für die Bereitstellung von Betriebssystemen mit Configuration Manager an:  


### <a name="implement-access-controls-to-protect-bootable-media"></a>Implementieren Sie Zugriffssteuerungen zum Schutz startbarer Medien.

Wenn Sie startbare Medien erstellen, weisen Sie zum Schutz der Medien immer ein Kennwort zu. Selbst mit einem Kennwort werden nur Dateien verschlüsselt, die vertrauliche Informationen enthalten, und alle Dateien können überschrieben werden.  

Kontrollieren Sie den physischen Zugriff auf die Medien, um zu verhindern, dass ein Angreifer mithilfe kryptografischer Angriffe Zugang zum Clientauthentifizierungszertifikat erhält.  

Auf den Inhalt wird ein Hashwert angewendet, und der Inhalt muss mit der Originalrichtlinie verwendet werden, um zu verhindern, dass von einem Client Inhalt oder eine Clientrichtlinie installiert wird, der bzw. die manipuliert wurde. Wenn für den Inhaltshash ein Fehler auftritt oder die Überprüfung der Übereinstimmung des Inhalts mit der Richtlinie nicht erfolgreich ist, werden die startbaren Medien vom Client nicht verwendet. Nur der Inhalt wird hashcodiert. Die Richtlinie ist nicht hashcodiert, aber verschlüsselt und geschützt, wenn Sie ein Kennwort angeben. Dadurch wird es Angreifern erschwert, die Richtlinie zu ändern.  


### <a name="use-a-secure-location-when-you-create-media-for-os-images"></a>Verwenden eines sicheren Speicherorts beim Erstellen von Medien für Betriebssystemimages

Wenn nicht autorisierte Benutzer auf den Speicherort zugreifen können, können diese die von Ihnen erstellten Dateien manipulieren. Diese Benutzer können zudem den gesamten verfügbaren Speicherplatz auf der Festplatte verwenden, sodass die Erstellung von Medien fehlschlägt.  


### <a name="protect-certificate-files"></a>Schützen von Zertifikatdateien 

Schützen Sie Zertifikatdateien (PFX-Dateien) mit einem sicheren Kennwort. Wenn Sie diese im Netzwerk speichern, verwenden Sie beim Importieren in Configuration Manager einen sicheren Netzwerkkanal.

Wenn für das Importieren des Clientauthentifizierungszertifikats, das Sie für startbare Medien verwenden, ein Kennwort erforderlich ist, ist das Zertifikat durch diese Konfiguration vor Angriffen geschützt.  

Verwenden Sie SMB-Signaturen oder IPsec zwischen Netzwerkspeicherort und Standortserver, um einen Angreifer an der Manipulation der Zertifikatdatei zu hindern.  


### <a name="block-or-revoke-any-compromised-certificates"></a>Sperren oder Widerrufen von kompromittierten Zertifikaten 

Sperren Sie ein Clientzertifikat in Configuration Manager, falls es kompromittiert wurde. Wenn es sich um ein PKI-Zertifikat handelt, sollten Sie dieses widerrufen.  

Zum Bereitstellen eines Betriebssystems mithilfe startbarer Medien und PXE-Start benötigen Sie ein Clientauthentifizierungszertifikat mit einem privaten Schlüssel. Sollte das Zertifikat gefährdet sein, blockieren Sie es im Arbeitsbereich **Verwaltung** über die Knoten **Zertifikate** und **Sicherheit** .  


### <a name="secure-the-communication-channel-between-the-site-server-and-the-sms-provider"></a>Sichern des Kommunikationskanals zwischen dem Standortserver und dem SMS-Anbieter

Wenn der SMS-Anbieter sich nicht auf dem Standortserver befindet, sollten Sie den Kommunikationskanal sichern, um Startimages zu schützen.

Wenn Sie Startimages ändern und der SMS-Anbieter auf einem anderen Server als dem Standortserver ausgeführt wird, sind diese anfällig für Angriffe. Schützen Sie den Netzwerkkanal zwischen diesen Computern mithilfe von SMB-Signaturen oder IPsec.  


### <a name="enable-distribution-points-for-pxe-client-communication-only-on-secure-network-segments"></a>Aktivieren Sie Verteilungspunkte für die PXE-Client-Kommunikation nur in sicheren Netzwerksegmenten.

Wenn von einem Client eine PXE-Startanforderung gesendet wird, können Sie nicht sicherstellen, dass die Anforderung von einem gültigen PXE-fähigen Verteilungspunkt bearbeitet wird. In diesem Szenario bestehen die folgenden Sicherheitsrisiken:  

- Von einem nicht autorisierten Verteilungspunkt, von dem PXE-Anforderungen beantwortet werden, könnte ein manipuliertes Abbild an Clients bereitgestellt werden.  

- Ein Angreifer könnte einen Man-in-the-Middle-Angriff auf das Trivial File Transfer Protocol starten, das von PXE verwendet wird. Bei diesem Angriff könnte schädlicher Code mit den Betriebssystemdateien gesendet werden. Der Angreifer könnte ebenfalls einen nicht autorisierten Client erstellen, um TFTP-Anforderungen direkt vom Verteilungspunkt aus auszuführen.  

- Ein Angreifer könnte einen schädlichen Client verwenden, um einen DoS-Angriff gegen den Verteilungspunkt zu starten.  

Verwenden Sie einen umfassenden Schutz für die Netzwerksegmente, in denen Clients auf PXE-Verteilungspunkte zugreifen.  

> [!WARNING]  
>  Wegen dieser Sicherheitsrisiken wird von der Aktivierung eines Verteilungspunkts für die PXE-Kommunikation abgeraten, wenn er sich in einem nicht vertrauenswürdigen Netzwerk (z.B. ein Umkreisnetzwerk) befindet.  


### <a name="configure-pxe-enabled-distribution-points-to-respond-to-pxe-requests-only-on-specified-network-interfaces"></a>Konfigurieren Sie PXE-fähige Verteilungspunkte so, dass von ihnen nur an bestimmten Netzwerkschnittstellen auf PXE-Anforderungen reagiert wird.  

Wenn Sie zulassen, dass die Reaktion des Verteilungspunkts auf PXE-Anforderungen an allen Netzwerkschnittstellen möglich ist, wird der PXE-Dienst möglicherweise für nicht vertrauenswürdige Netzwerke verfügbar.  


### <a name="require-a-password-to-pxe-boot"></a>Erfordern Sie zum PXE-Start ein Kennwort.

Wenn Sie festlegen, dass für den PXE-Start ein Kennwort erforderlich ist, wird die Sicherheit des PXE-Startprozesses verbessert. Durch diese Konfiguration kann verhindert werden, dass nicht autorisierte Clients der Configuration Manager-Hierarchie beitreten.  


### <a name="restrict-content-in-os-images-used-for-pxe-boot-or-multicast"></a>Einschränken des Inhalts in Betriebssystemimages, die für den PXE-Start oder Multicast verwendet werden

Schließen Sie in ein Image, das für den PXE-Start oder Multicast verwendet wird, keine Branchenanwendungen oder Software mit vertraulichen Daten ein.  

Mit dem PXE-Start und Multicast sind grundsätzlich Sicherheitsrisiken verbunden. Verringern Sie daher das Risiko für den Fall, dass das Betriebssystemimage von einem nicht autorisierten Computer heruntergeladen wird.  


### <a name="restrict-content-installed-by-task-sequence-variables"></a>Einschränken von Inhalten, die über Tasksequenzvariablen installiert wurden

Schließen Sie in Anwendungspakete, die mithilfe von Tasksequenzvariablen installiert werden, keine Branchenanwendungen oder Software mit vertraulichen Daten ein.  

Wenn Sie Software mithilfe von Tasksequenzvariablen bereitstellen, ist eine Installation der Software auf Geräten und für Benutzer möglich, die für den Empfang dieser Software nicht autorisiert sind.  


### <a name="secure-the-network-channel-when-migrating-user-state"></a>Sichern des Netzwerkkanals bei der Migration von Benutzerzuständen

Sichern Sie beim Migrieren von Benutzerzuständen den Netzwerkkanal zwischen dem Client und dem Statusmigrationspunkt mithilfe von SMB-Signaturen oder IPsec.  

Nachdem die erste Verbindung über HTTP hergestellt wurde, werden die Migrationsdaten für den Benutzerzustand mithilfe von SMB übertragen. Wenn Sie den Netzwerkkanal nicht sichern, können diese Daten von einem Angreifer gelesen und geändert werden.  


### <a name="use-the-latest-version-of-usmt"></a>Verwenden der aktuellen Version von USMT

Verwenden Sie die aktuelle Version des Migrationstools für den Benutzerstatus (USMT), die von Configuration Manager unterstützt wird.  

Die aktuelle Version von Windows-EasyTransfer umfasst Sicherheitsverbesserungen und bessere Steuerungsmöglichkeiten für die Migration von Benutzerzustandsdaten.  


### <a name="manually-delete-folders-on-state-migration-points-when-you-decommission-them"></a>Manuelles Löschen von Ordnern auf Zustandsmigrationspunkten, wenn diese außer Betrieb gesetzt werden  

Wenn Sie einen Ordner für einen Zustandsmigrationspunkt in der Configuration Manager-Konsole aus den Eigenschaften des Zustandsmigrationspunkts entfernen, löscht der Standort den physischen Ordner nicht. Entfernen Sie die Netzwerkfreigabe manuell, und löschen Sie den Ordner, um zu verhindern, dass die Migrationsdaten für den Benutzerzustand offengelegt werden.  


### <a name="dont-configure-the-deletion-policy-to-immediately-delete-user-state"></a>Konfigurieren der Löschrichtlinie für das nicht sofortige Löschen des Benutzerzustands  

Wenn Sie die Löschrichtlinie auf dem Zustandsmigrationspunkt so konfigurieren, dass zum Löschen markierte Daten sofort gelöscht werden, und es einem Angreifer vor dem gültigen Computer gelingt, die Benutzerzustandsdaten abzurufen, löscht der Standort die Benutzerzustandsdaten sofort. Legen Sie das Intervall **Löschen nach** auf eine Dauer fest, die dafür ausreicht, die erfolgreiche Wiederherstellung der Benutzerzustandsdaten zu überprüfen.  


### <a name="manually-delete-computer-associations"></a>Manuelles Löschen von Computerzuordnungen 

Löschen Sie Computerzuordnungen manuell, wenn die Wiederherstellung der Migrationsdaten für den Benutzerstatus abgeschlossen ist und überprüft wurde.

Computerzuordnungen werden von Configuration Manager nicht automatisch entfernt. Schützen Sie die Identität von Benutzerzustandsdaten, indem Sie Computerzuordnungen, die nicht mehr benötigt werden, manuell löschen.  


### <a name="manually-back-up-the-user-state-migration-data-on-the-state-migration-point"></a>Sichern Sie die Migrationsdaten für den Benutzerzustand auf dem Zustandsmigrationspunkt manuell.  

Die Migrationsdaten für den Benutzerzustand in der Standortsicherung werden bei der Sicherung in Configuration Manager nicht berücksichtigt.  


### <a name="implement-access-controls-to-protect-the-prestaged-media"></a>Implementieren Sie Zugriffssteuerungen zum Schutz der vorab bereitgestellten Medien.  

Kontrollieren Sie den physischen Zugriff auf die Medien, um zu verhindern, dass ein Angreifer mithilfe kryptografischer Angriffe Zugang zum Clientauthentifizierungszertifikat und zu sensiblen Daten erhält.  


### <a name="implement-access-controls-to-protect-the-reference-computer-imaging-process"></a>Implementieren Sie Zugriffssteuerungen zum Schutz des Abbilderstellungsprozesses auf dem Referenzcomputer.  

Stellen Sie sicher, dass der Referenzcomputer, der für das Erfassen des Betriebssystemimages verwendet wird, sich in einer sicheren Umgebung befindet. Verwenden Sie eine angemessene Zugriffssteuerung, damit unerwartete oder schädliche Software nicht installiert und dadurch versehentlich in das erfasste Image aufgenommen werden kann. Wenn Sie das Image erfassen, sollten Sie sicherstellen, dass die Zielnetzwerkadresse sicher ist. Dadurch können Sie sicherstellen, dass das Image nicht manipuliert werden kann, nachdem Sie es erfasst haben.  


### <a name="always-install-the-most-recent-security-updates-on-the-reference-computer"></a>Installieren Sie immer die neuesten Sicherheitsupdates auf dem Referenzcomputer.  

Wenn die aktuellen Sicherheitsupdates auf dem Referenzcomputer vorhanden sind, werden die Sicherheitsrisiken beim ersten Start neuer Computer reduziert.  


### <a name="implement-access-controls-when-deploying-an-os-to-an-unknown-computer"></a>Implementieren der Zugriffssteuerung beim Bereitstellen eines Betriebssystems auf einem unbekannten Computer

Wenn Sie ein Betriebssystem für einen unbekannten Computer bereitstellen müssen, implementieren Sie Zugriffssteuerungen, um zu verhindern, dass von nicht autorisierten Computern eine Verbindung mit dem Netzwerk hergestellt wird.  

Das Bereitstellen unbekannter Computer stellt eine praktische Methode zum Bereitstellen neuer Computer bei Bedarf dar. Ein Angreifer kann sich dadurch jedoch auch als vertrauenswürdiger Client in Ihr Netzwerk einschleusen. Schränken Sie den physischen Zugriff auf das Netzwerk ein, und überwachen Sie Clients, um nicht autorisierte Computer zu erkennen. 

Auf Computern, die auf eine von PXE initiierte Betriebssystembereitstellung reagieren, können währenddessen alle Daten vernichtet werden. Dadurch sind Systeme, die versehentlich umformatiert werden, möglicherweise nicht mehr verfügbar.  


### <a name="enable-encryption-for-multicast-packages"></a>Aktivieren Sie die Verschlüsselung für Multicastpakete.  

Sie können bei jedem Paket der Betriebssystembereitstellung die Verschlüsselung aktivieren, wenn Configuration Manager das Paket mithilfe von Multicast überträgt. Durch diese Konfiguration kann verhindert werden, dass nicht autorisierte Computer der Multicastsitzung beitreten. Außerdem können Angreifer daran gehindert werden, die Übertragung zu manipulieren.  


### <a name="monitor-for-unauthorized-multicast-enabled-distribution-points"></a>Überwachen Sie das System auf nicht autorisierte, multicastfähige Verteilungspunkte.  

Wenn Angreifer Zugriff auf Ihr Netzwerk erhalten, können sie nicht autorisierte Multicastserver konfigurieren, um die Betriebssystembereitstellung zu spoofen.  


### <a name="when-you-export-task-sequences-to-a-network-location-secure-the-location-and-secure-the-network-channel"></a>Wenn Sie Tasksequenzen an einen Netzwerkspeicherort exportieren, sichern Sie den Speicherort und den Netzwerkkanal.

Schränken Sie die Anzahl der Personen ein, die auf den Netzwerkordner zugreifen können.  

Verwenden Sie SMB-Signaturen oder IPsec zwischen Netzwerkspeicherort und Standortserver, um einen Angreifer an der Manipulation der exportierten Tasksequenz zu hindern.  


### <a name="if-you-use-the-task-sequence-run-as-account-take-additional-security-precautions"></a>Zusätzliche Sicherheitsvorkehrungen beim Verwenden eines ausführenden Kontos für die Tasksequenz

Treffen Sie die folgenden Sicherheitsvorkehrungen, wenn Sie das [ausführende Konto für die Tasksequenz](../../core/plan-design/hierarchy/accounts.md#task-sequence-run-as-account) verwenden:  

- Verwenden Sie ein Konto mit geringstmöglichen Berechtigungen.  

- Verwenden Sie für dieses Konto nicht das Netzwerkzugriffskonto.  

- Versehen Sie das Konto niemals mit Domänenadministratorrechten.  

- Konfigurieren Sie niemals servergespeicherte Profile für dieses Konto. Wenn die Tasksequenz ausgeführt wird, lädt diese das Roamingprofil für das Konto herunter, sodass es anfällig für einen Zugriff auf den lokalen Computer wird.  

- Beschränken Sie den Kontoumfang. Erstellen Sie beispielsweise unterschiedliche ausführende Konten für jede Tasksequenz. Wenn ein Konto gefährdet ist, sind nur die Clientcomputer gefährdet, auf die dieses Konto Zugriff hat. Wenn für die Befehlszeile Administratorrechte auf dem Computer erforderlich sind, erwägen Sie die Erstellung eines lokalen Administratorkontos lediglich für das ausführende Konto für die Tasksequenz. Erstellen Sie dieses lokale Konto auf allen Computern, die die Tasksequenz ausführen, und löschen Sie das Konto, sobald es nicht mehr benötigt wird.  


### <a name="restrict-and-monitor-the-administrative-users-who-are-granted-the-os-deployment-manager-security-role"></a>Überwachen und Einschränken der Administratoren mit der Sicherheitsrolle „Betriebssystembereitstellungs-Manager“

Administratoren mit der Sicherheitsrolle **Betriebssystembereitstellungs-Manager** können selbstsignierte Zertifikate erstellen. Diese Zertifikate können anschließend verwendet werden, um die Identität eines Clients anzunehmen und eine Clientrichtlinie von Configuration Manager abzurufen.  


### <a name="use-enhanced-http-to-reduce-the-need-for-a-network-access-account"></a>Verwenden von erweitertem HTTP zum Reduzieren der Notwendigkeit eines Netzwerkzugriffskontos

Wenn Sie [Erweitertes HTTP](../../core/plan-design/hierarchy/enhanced-http.md) ab Version 1806 aktivieren, ist bei mehreren Szenarios für die Betriebssystembereitstellung kein Netzwerkzugriffskonto erforderlich, um Inhalt von einem Verteilungspunkt herunterzuladen. Weitere Informationen finden Sie unter [Tasksequenzen und das Netzwerkzugriffskonto](planning-considerations-for-automating-tasks.md#BKMK_TSNetworkAccessAccount).<!--1358278--> 



## <a name="security-issues-for-os-deployment"></a>Sicherheitsprobleme bei der Betriebssystembereitstellung  

Obwohl die Betriebssystembereitstellung eine bequeme Methode zur Bereitstellung der sichersten Betriebssysteme und Konfigurationen für die Computer in Ihrem Netzwerk darstellt, ist sie mit den folgenden Sicherheitsrisiken verbunden:  


### <a name="information-disclosure-and-denial-of-service"></a>Offenlegung von Informationen und Denial-of-Service  

Wenn ein Angreifer die Kontrolle über Ihre Configuration Manager-Infrastruktur erlangen kann, kann dieser jede Tasksequenz ausführen. Dadurch ist unter anderem die Formatierung aller Festplatten auf allen Clientcomputern möglich. Tasksequenzen können so konfiguriert werden, dass sie vertrauliche Informationen wie Konten mit Berechtigungen zum Domänenbeitritt und Volumenlizenzschlüssel enthalten.  


### <a name="impersonation-and-elevation-of-privileges"></a>Identitätsvortäuschung und Rechteerweiterungen  

Mit Tasksequenzen kann der Beitritt eines Computers zu einer Domäne bewirkt werden, und hierdurch kann ein nicht autorisierter Computer möglicherweise einen authentifizierten Netzwerkzugriff erhalten. 

Schützen Sie das Clientauthentifizierungszertifikat, das für startbare Tasksequenzmedien und für die Bereitstellung mit PXE-Start verwendet wird. Wenn Sie ein Clientauthentifizierungszertifikat erfassen, kann ein Angreifer den privaten Schlüssel im Zertifikat abrufen. Durch dieses Zertifikat kann der Angreifer die Identität eines gültigen Clients im Netzwerk annehmen. In diesem Fall kann von dem nicht autorisierten Computer die Richtlinie, die möglicherweise sensible Daten enthält, heruntergeladen werden.  

Wenn Clients das Netzwerkzugriffskonto verwenden, um auf Daten zuzugreifen, die im Zustandsmigrationspunkt gespeichert sind, besitzen diese Clients im Prinzip die gleiche Identität. Sie könnten somit auf Zustandsmigrationsdaten von einem anderen Client aus zugreifen, der das Netzwerkzugriffskonto verwendet. Die Daten werden verschlüsselt, damit sie nur vom ursprünglichen Client gelesen werden können. Es ist jedoch möglich, die Daten zu manipulieren oder zu löschen.  


### <a name="client-authentication-to-the-state-migration-point-is-achieved-by-using-a-configuration-manager-token-that-is-issued-by-the-management-point"></a>Die Clientauthentifizierung für den Statusmigrationspunkt wird mithilfe eines Configuration Manager-Tokens durchgeführt, das vom Verwaltungspunkt ausgegeben wird.  

Configuration Manager schränkt die Menge der Daten, die auf dem Zustandsmigrationspunkt gespeichert wird, nicht ein oder verwaltet diese. Ein Angreifer könnte den verfügbarer Speicherplatz auf der Festplatte belegen und somit einen Denial-of-Service-Angriff ausführen.  


### <a name="if-you-use-collection-variables-local-administrators-can-read-potentially-sensitive-information"></a>Wenn Sie Sammlungsvariablen verwenden, können lokale Administratoren potenziell vertrauliche Informationen lesen.  

Obwohl Sammlungsvariablen ein flexibles Verfahren zum Bereitstellen von Betriebssystemen darstellen, kann dieses Feature zur Offenlegung von Informationen führen.  



##  <a name="privacy-information-for-os-deployment"></a><a name="bkmk_privacy"></a> Datenschutzinformationen für die Betriebssystembereitstellung  

Neben dem Bereitstellen von Betriebssystemen für Computer ohne Betriebssystem können mit Configuration Manager Benutzerdateien und -einstellungen von einem Computer zu einem anderen migriert werden. Der Administrator konfiguriert, welche Informationen übertragen werden. Dies umfasst persönliche Datendateien, Konfigurationseinstellungen und Browsercookies.  

Configuration Manager speichert die Informationen in einem Zustandsmigrationspunkt und verschlüsselt diese während der Übertragung und Speicherung. Nur die neuen Computer, die den Zustandsinformationen zugeordnet sind, können die gespeicherten Informationen abrufen. Verliert der neue Computer den Schlüssel zum Abrufen der Informationen, kann ein Configuration Manager-Administrator mit dem Recht **Wiederherstellungsinformationen anzeigen** für Computerzuordnungsinstanzobjekte auf die Informationen zugreifen und diese einem neuen Computer zuordnen. Nachdem der neue Computer die Zustandsinformationen wiederhergestellt hat, werden die Daten standardmäßig nach einem Tag gelöscht. Sie können konfigurieren, wann der Zustandsmigrationspunkt zum Löschen markierte Daten entfernt. Configuration Manager speichert die Zustandsmigrationsinformationen nicht in der Standortdatenbank und sendet diese nicht an Microsoft.  

Wenn Sie Startmedien für die Bereitstellung von Betriebssystemimages verwenden, achten Sie darauf, immer die Standardoption für den Kennwortschutz der Startmedien zu verwenden. Mit dem Kennwort werden alle in der Tasksequenz gespeicherten Variablen verschlüsselt. Alle nicht in einer Variablen gespeicherten Informationen können aber Sicherheitsrisiken ausgesetzt sein.  

Bei der Betriebssystembereitstellung können mithilfe von Tasksequenzen viele verschiedene Tasks wie die Installation von Anwendungen und Softwareupdates ausgeführt werden. Wenn Sie Tasksequenzen konfigurieren, berücksichtigen Sie auch die mit der Installation von Software verbundenen Auswirkungen auf den Datenschutz.  

Configuration Manager implementiert standardmäßig keine Betriebssystembereitstellung. Es müssen mehrere Konfigurationsschritte ausgeführt werden, bevor Sie Benutzerzustandsdaten sammeln oder Tasksequenzen bzw. Startimages erstellen können.  

Berücksichtigen Sie vor dem Konfigurieren der Betriebssystembereitstellung Ihre Datenschutzanforderungen.  



## <a name="see-also"></a>Weitere Informationen:

[Diagnose- und Verwendungsdaten](../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)

[Sicherheit und Datenschutz für Configuration Manager](../../core/plan-design/security/security-and-privacy.md)
