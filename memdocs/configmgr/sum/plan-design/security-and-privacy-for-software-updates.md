---
title: Sicherheit und Datenschutz für die Softwareupdates
titleSuffix: Configuration Manager
description: Befolgen Sie diese bewährten Methoden für die Sicherheit von Softwareupdates, und erfahren Sie mehr über die Behandlung von Informationen zum Datenschutz in Configuration Manager.
manager: dougeby
ms.date: 09/16/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 41d6d5d8-ba84-4efb-b105-4d1eed239824
author: mestew
ms.author: mstewart
ms.openlocfilehash: 0838f43abf7ff972ac3f6ca2cdf44dcafda323ca
ms.sourcegitcommit: 6176a7825d6c663faa318a6818b7764bc70f08fc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/17/2020
ms.locfileid: "90718721"
---
# <a name="security-and-privacy-for-software-updates-in-configuration-manager"></a>Sicherheit und Datenschutz für Softwareupdates in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Dieses Thema enthält Sicherheits- und Datenschutzinformationen für Softwareupdates in Configuration Manager.  

##  <a name="security-best-practices-for-software-updates"></a><a name="BKMK_Security_HardwareInventory"></a> Bewährte Sicherheitsmethoden für Softwareupdates  
 Wenden Sie die folgenden bewährten Sicherheitsmethoden beim Bereitstellen von Softwareupdates auf Clients an:  

-   Behalten Sie die Standardberechtigungen von Softwareupdatepaketen bei.  

     Administratoren verfügen standardmäßig über **Vollzugriff** und Benutzer über **Lesezugriff** auf die Softwareupdatepakete. Wenn Sie diese Berechtigungen ändern, könnte dies einem Angreifer ermöglichen, Softwareupdates hinzuzufügen, zu entfernen oder zu löschen.  

-   Beschränken Sie den Zugriff auf den Downloadspeicherort für Softwareupdates.  

     Das SMS-Anbietercomputerkonto, der Standortserver und der Administrator, der die Softwareupdates in den Downloadspeicherort herunterlädt, benötigen **Schreibzugriff** auf den Downloadpfad. Beschränken Sie den Zugriff auf den Downloadpfad, um das Risiko zu verringern, dass Angreifer die Quelldatei der Softwareupdates am Downloadspeicherort manipulieren.  

     Wenn Sie darüber hinaus einen UNC-Freigabepfad als Downloadspeicherort verwenden, schützen Sie den Netzwerkkanal mithilfe von IPsec oder SMB-Signaturen, um die Manipulation der Softwareupdatequelldateien beim Übermitteln über das Netzwerk zu verhindern.  

-   Verwenden Sie für die Bewertung der Bereitstellungszeiten UTC.  

     Wenn Sie Ortszeit anstelle von UTC verwenden, können Benutzer die Installation von Softwareupdates verzögern, indem sie die Zeitzone auf ihren Computern ändern.  

-   Aktivieren Sie SSL für WSUS, und befolgen Sie die bewährten Methoden zum Schützen von Windows Server Update Services (WSUS).  

     Identifizieren und befolgen Sie die bewährten Sicherheitsmethoden für die Version von WSUS, die Sie mit Configuration Manager verwenden. 

     Weitere Informationen zum Aktivieren von SSL finden Sie im Tutorial [Konfigurieren eines Softwareupdatepunkts für die Verwendung von TLS/SSL mit einem PKI-Zertifikat](../get-started/software-update-point-ssl.md). 

    > [!IMPORTANT]  
    >  Wenn Sie den Softwareupdatepunkt für SSL-Verbindungen mit dem WSUS-Server konfigurieren, müssen Sie virtuelle Stammverzeichnisse für SSL auf dem WSUS-Server konfigurieren.  

-   Aktivieren Sie die Überprüfung der Zertifikatsperrlisten.  

     Standardmäßig wird in Configuration Manager die Zertifikatsperrliste (Certificate Revocation List, CRL) nicht geprüft, um die Signatur von Softwareupdates vor deren Bereitstellung auf Computern zu überprüfen. Das Prüfen der CRL bei jeder Verwendung eines Zertifikats bietet einen höheren Schutz vor gesperrten Zertifikaten, führt jedoch zu einer Verbindungsverzögerung und zusätzlichem Verarbeitungsaufwand auf dem Computer, der die CRL-Prüfung ausführt.  

     Weitere Informationen zum Aktivieren der Überprüfung der Zertifikatsperrlisten für Softwareupdates finden Sie unter [Aktivieren der CRL-Prüfung für Softwareupdates](../get-started/manage-settings-for-software-updates.md#crl-checking-for-software-updates).  

-   Konfigurieren Sie WSUS für die Verwendung einer benutzerdefinierten Website.  

     Beim Installieren von WSUS auf einem Softwareupdatepunkt haben Sie die Möglichkeit, die vorhandene IIS-Standardwebsite oder eine benutzerdefinierte WSUS-Website zu erstellen. Erstellen Sie eine benutzerdefinierte Website für WSUS, sodass die WSUS-Dienste von IIS in einer dedizierten virtuellen Website gehostet werden, statt die gleiche Website zu verwenden wie die Configuration Manager-Standortsysteme oder anderen Anwendungen.  

     Weitere Informationen finden Sie unter [Configure WSUS to use a custom web site](plan-for-software-updates.md#BKMK_CustomWebSite).  

##  <a name="privacy-information-for-software-updates"></a><a name="BKMK_Privacy_HardwareInventory"></a> Informationen zum Datenschutz für Softwareupdates  
 Die Softwareupdatefunktion überprüft Ihre Clientcomputer, um zu bestimmen, welche Softwareupdates Sie benötigen. Diese Informationen werden dann zur Standortdatenbank zurückgesendet. Beim Softwareupdateprozess überträgt Configuration Manager möglicherweise Informationen zwischen Clients und Servern, die die Computer- und Anmeldekonten identifizieren.  

 In Configuration Manager werden Zustandsinformationen zum Softwarebereitstellungsprozess verwaltet. Zustandsinformationen werden während der Übertragung oder Speicherung nicht verschlüsselt. Zustandsinformationen werden in der Configuration Manager-Datenbank gespeichert und von den Datenbankwartungstasks gelöscht. Die Zustandsinformationen werden nicht an Microsoft gesendet.  

 Das Verwenden der Softwareupdatefunktion von Configuration Manager zur Installation von Softwareupdates auf Clientcomputern kann Softwarelizenzbedingungen für diese Updates unterliegen, die sich von den Softwarelizenzbedingungen für Configuration Manager unterscheiden. Bevor Sie die Softwareupdates mit Configuration Manager installieren, sollten Sie stets die Softwarelizenzbedingungen lesen und akzeptieren.  

 Configuration Manager implementiert die Softwareupdatefunktion nicht standardmäßig, und es sind mehrere Konfigurationsschritte erforderlich, bevor Informationen gesammelt werden.  

 Berücksichtigen Sie beim Konfigurieren der Softwareupdates Ihre Datenschutzanforderungen.  
