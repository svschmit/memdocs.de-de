---
title: Bewährte Methoden zur Clientbereitstellung
titleSuffix: Configuration Manager
description: Hier finden Sie bewährte Methoden für die Clientbereitstellung in Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a933d69c-5feb-4b2b-84e8-56b3b64d5947
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 28f8bfb2ef012fcd4f19835190b7c042d38fd9e0
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693878"
---
# <a name="best-practices-for-client-deployment-in-configuration-manager"></a>Bewährte Methoden für die Clientbereitstellung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*


## <a name="use-software-update-based-client-installation-for-active-directory-computers"></a>Verwenden einer auf Softwareupdate basierenden Clientinstallation für Active Directory-Computer  
 Diese Clientbereitstellungsmethode verwendet vorhandene Windows-Technologien, ist in Ihre Active Directory-Infrastruktur integriert, erfordert nur geringfügige Konfigurationen in Configuration Manager, ist am einfachsten für Firewalls zu konfigurieren und ist außerdem die sicherste Methode. Durch die Verwendung von Sicherheitsgruppen und der WMI-Filterung für die Gruppenrichtlinienkonfiguration sind Sie außerdem sehr flexibel bei der Steuerung, auf welchen Computern der Configuration Manager-Client installiert wird.  

 Weitere Informationen finden Sie unter [Installieren von Configuration Manager-Clients mithilfe von auf Softwareupdate basierender Installation](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientSUP).  

## <a name="extend-the-active-directory-schema-and-publish-the-site-so-that-you-can-run-ccmsetup-without-command-line-options"></a>Erweitern Sie das Active Directory-Schema, und veröffentlichen Sie den Standort, damit Sie CCMSetup ohne Befehlszeilenoptionen ausführen können.  
 Wenn Sie das Active Directory-Schema für Configuration Manager erweitert haben, und der Standort in Active Directory Domain Services veröffentlicht wird, werden viele Clientinstallationseigenschaften in Active Directory Domain Services veröffentlicht. Wenn diese Clientinstallationseigenschaften von einem Computer gefunden werden können, kann er sie im Rahmen der Configuration Manager-Clientbereitstellung verwenden. Da diese Informationen automatisch generiert werden, wird das Risiko eines Fehlers durch manuelle Eingabe der Installationseigenschaften beseitigt.  

 Weitere Informationen finden Sie unter [Informationen zu Clientinstallationseigenschaften, die in Active Directory Domain Services veröffentlicht wurden](../../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

## <a name="use-a-phased-rollout-to-manage-cpu-usage"></a>Verwenden eines Rollouts in Phasen zur Verwaltung der CPU-Nutzung  
 Verringern Sie die Auswirkung auf die Prozessoranforderungen auf dem Standortserver, indem Sie ein Rollout der Clients in mehreren Phasen verwenden. Stellen Sie Clients außerhalb der Geschäftszeiten bereit, sodass den anderen Diensten tagsüber mehr Bandbreite zur Verfügung steht und die Benutzer nicht durch Computer behindert werden, die langsam sind oder neu gestartet werden müssen.  

## <a name="enable-automatic-upgrade-after-your-main-client-deployment-has-finished"></a>Aktivieren von automatischem Upgrade nach Abschluss Ihrer wichtigsten Clientbereitstellung  
 [Automatische Clientupgrades](../../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md) sind nützlich bei einer geringen Anzahl von Clientcomputern, die von Ihrer Hauptmethode für die Clientinstallation nicht erfasst wurden, da sie möglicherweise offline waren. 

> [!NOTE]  
>  Durch Leistungsverbesserungen in Configuration Manager können Sie automatische Upgrades als primäre Upgrademethode für Clients verwenden. Die Leistung hängt jedoch von Ihrer Hierarchieinfrastruktur ab, wie etwa von der Anzahl der Clients.  


## <a name="use-smsmp-and-fsp-if-you-install-the-client-with-clientmsi-properties"></a>Verwenden Sie bei der Installation des Clients mit client.msi-Eigenschaften SMSMP und FSP.  
 Durch die Eigenschaft SMSMP wird der erste Verwaltungspunkt für den Client zur Kommunikation angegeben und die Abhängigkeit von Dienstidentifizierungslösungen wie Active Directory-Domänendiensten, DNS und WINS beseitigt.  

 Verwenden Sie die FSP-Eigenschaft, und installieren Sie einen Fallbackstatuspunkt, sodass Sie die Clientinstallation und -zuordnung überwachen und Kommunikationsprobleme ermitteln können.  

 Weitere Informationen zu diesen Optionen finden Sie unter [Informationen zu Clientinstallationseigenschaften](../../../../core/clients/deploy/about-client-installation-properties.md).  

## <a name="install-client-language-packs-before-you-install-the-clients"></a>Installieren von Clientsprachpaketen vor der Installation der Clients  
Es wird empfohlen, Clientsprachpakete vor dem Bereitstellen des Clients zu installieren. Wenn Sie [Clientsprachpakete](../../../../core/servers/deploy/install/language-packs.md) nach der Installation von Clients an einem Standort installieren (um weitere Sprachen zu aktivieren), müssen Sie die Clients erneut installieren, bevor sie diese Sprachen verwenden können. Für Clients mobiler Geräte bedeutet dies, dass Sie das mobile Gerät zurücksetzen und erneut registrieren müssen.  

## <a name="prepare-required-pki-certificates-in-advance"></a>Vorbereiten erforderlicher PKI-Zertifikate im Voraus  
 Zur Verwaltung von Geräten im Internet, angemeldeten mobilen Geräte und Macintosh-Computern müssen PKI-Zertifikate in den Standortsystemen (Verwaltungspunkte und Verteilungspunkte) sowie auf den Clientgeräten vorhanden sein. In Produktionsnetzwerken benötigen Sie für die Verwendung neuer Zertifikate möglicherweise die Genehmigung des Änderungsmanagements, müssen die Standortsystemserver neu starten, oder die Benutzer müssen sich eventuell für die neue Gruppenmitgliedschaft ab- und wieder anmelden. Außerdem müssen Sie möglicherweise ausreichend Zeit für das Replizieren von Sicherheitsberechtigungen und für sämtliche neuen Zertifikatvorlagen einplanen.  

 Weitere Informationen zu erforderlichen PKI-Zertifikaten finden Sie unter [PKI-Zertifikatanforderungen für Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md).  

## <a name="before-you-install-clients-configure-any-required-client-settings-and-maintenance-windows"></a>Konfigurieren Sie sämtliche erforderlichen Clienteinstellungen und Wartungsfenster, bevor Sie Clients installieren  
 Obwohl Sie [Clienteinstellungen](../../../../core/clients/deploy/configure-client-settings.md) und Wartungsfenster vor oder nach dem Installieren von Clients konfigurieren können, sollten Sie alle erforderlichen Einstellungen vornehmen, bevor Sie Clients installieren, sodass die Einstellungen verwendet werden, sobald der Client installiert ist. 

 Konfigurieren Sie Wartungsfenster für Server und für Windows Embedded-Geräte, um die Geschäftskontinuität für geschäftskritische Geräte sicherzustellen. Durch Wartungsfenster wird sichergestellt, dass die Computer von erforderlichen Softwareupdates und Antischadsoftware nicht innerhalb der Geschäftszeiten neu gestartet werden.  

> [!IMPORTANT]  
>  Bei Windows 10-Computern, die Sie mit UWF (Unified Write Filter) schützen möchten, müssen Sie das Gerät für UWF konfigurieren, bevor Sie den Client installieren. Auf diese Weise kann Configuration Manager den Client mit einem benutzerdefinierten Anmeldeinformationsanbieter installieren, durch den Benutzer mit geringen Rechten von der Anmeldung beim Gerät im Wartungsmodus ausgeschlossen werden.  

## <a name="plan-your-user-enrollment-experience-for-mac-computers-and-mobile-devices"></a>Planen einer benutzerfreundlichen Benutzerregistrierung für Macintosh-Computer und mobile Geräte   
 Wenn Benutzer ihre eigenen Macintosh-Computer und mobilen Geräte über Configuration Manager registrieren, planen Sie einen benutzerfreundlichen Weg. Sie können für den Installations- und Anmeldungsprozess per Webseite beispielsweise ein Skript erstellen, sodass die Benutzer ein Mindestmaß der erforderlichen Informationen eingeben müssen und Sie Anweisungen über einen Link in einer E-Mail senden können.  

## <a name="use-file-based-write-filters-for-windows-embedded-devices"></a>Verwenden von dateibasierten Schreibfiltern für Windows Embedded-Geräte 
 Für Embedded-Geräte, die erweiterte Schreibfilter (EWF) verwenden, treten wahrscheinlich Neusynchronisierungen von Zustandsmeldungen auf. Wenn Sie nur einige Embedded-Geräte mit erweiterten Schreibfiltern verwenden, bemerken Sie dies möglicherweise nicht. Wenn Sie jedoch viele Embedded-Geräte haben, von denen die Informationen neu synchronisiert werden, wie etwa das Versenden des vollständigen Inventars anstelle des Deltainventars, dann kann dies zu einem merkbaren Anstieg an Netzwerkpaketen und einer höheren Prozessorauslastung auf dem Standortserver führen.  

 Wenn Sie die Wahl haben, welche Art von Schreibfilter Sie aktivieren möchten, wählen Sie für die Netzwerk- und Prozessoreffizienz auf dem Configuration Manager-Client die dateibasierten Schreibfilter aus, und konfigurieren Sie Ausnahmen, um den Clientzustand sowie Inventurdaten zwischen den Geräteneustarts beizubehalten. Weitere Informationen zu Schreibfiltern finden Sie unter [Planen der Clientbereitstellung auf Windows Embedded-Geräten](../../../../core/clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).  

 Weitere Informationen zur maximalen Anzahl von Windows Embedded-Clients, die von einem primären Standort unterstützt werden können, finden Sie unter [Supported operating systems for sites and clients for System Center Configuration Manager](../../../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md)(Unterstützte Betriebssysteme für Standorte und Clients für System Center Configuration Manager).  
