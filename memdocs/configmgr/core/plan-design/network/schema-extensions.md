---
title: Schemaerweiterungen
titleSuffix: Configuration Manager
description: Erweitern Sie das Active Directory-Schema zur Unterstützung von Configuration Manager.
ms.date: 02/7/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 95c13c00-909f-4fbb-bbaa-1eba9d54d8c5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 1ace560130e43fd5675b51b6d507e84043c01407
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82904070"
---
# <a name="schema-extensions-for-configuration-manager"></a>Schemaerweiterungen für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Sie können das Active Directory-Schema so erweitern, dass es Configuration Manager unterstützt. Hierdurch wird das Active Directory-Schema einer Gesamtstruktur so bearbeitet, dass ein neuer Container und mehrere Attribute hinzugefügt werden. Diese werden von Configuration Manager-Standorten dazu verwendet, wichtige Informationen in Active Directory zu veröffentlichen, wo Clients sicher darauf zugreifen können. Diese Informationen können die Bereitstellung und Konfiguration von Clients vereinfachen und versetzen Clients in die Lage, Standortressourcen, etwa Server mit bereitgestellten Inhalten, oder Standortressourcen zu finden, die verschiedene Dienste für Clients bereitstellen.  

-   Es ist ratsam, das Active Directory-Schema zu erweitern, aber es ist nicht erforderlich.  

Bevor Sie [das Active Directory-Schema erweitern](https://docs.microsoft.com/sccm/core/plan-design/network/extend-the-active-directory-schema), sollten Sie mit Active Directory-Domänendienste vertraut sein und wissen, wie ein [Ändern des Active Directory-Schemas](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2003/cc759402(v=ws.10))vorgenommen wird.  

## <a name="considerations-for-extending-the-active-directory-schema-for-configuration-manager"></a>Überlegungen zum Erweitern des Active Directory-Schemas für Configuration Manager  

-   Die Active Directory-Schemaerweiterungen für Configuration Manager sind dieselben, die auch in Configuration Manager 2007 und Configuration Manager 2012 verwendet wurden. Wenn Sie das Schema bereits für eine der Versionen erweitert haben, müssen Sie es nicht erneut erweitern.  

-   Das Erweitern des Schemas ist eine gesamtstrukturweite, einmalige, nicht rückgängig zu machende Aktion.  

-   Das Erweitern des Schemas kann nur von einem Mitglied der Gruppe „Schema-Admins“ oder von einem Benutzer ausgeführt werden, der die erforderlichen Berechtigungen zum Ändern des Schemas besitzt.  

-   Sie können das Schema zwar vor oder nach dem Ausführen von Setup für Configuration Manager erweitern, aber es empfiehlt sich, das Schema zu erweitern, bevor Sie damit beginnen, Ihre Standorte und Hierarchieeinstellungen zu konfigurieren. Dadurch lassen sich viele der späteren Konfigurationsschritte vereinfachen.  

-   Nachdem Sie das Schema erweitert haben, wird der globale Katalog von Active Directory in der Gesamtstruktur repliziert. Daher sollten Sie die Schemaerweiterung vornehmen, wenn der Replikationsdatenverkehr keine negativen Auswirkungen auf andere vom Netzwerk abhängige Prozesse hat:  

    -   In Windows 2000-Gesamtstrukturen führt das Erweitern des Schemas zu einer vollständigen Synchronisierung des gesamten globalen Katalogs.  

    -   Bei Gesamtstrukturen ab Windows 2003 werden nur die neu hinzugefügten Attribute repliziert.  

**Geräte und Clients, die das Active Directory-Schema nicht verwenden:**  

-   Mobile Geräte, die vom Exchange Server-Connector verwaltet werden  

-   Client für Macintosh-Computer  

-   Client für Linux- und UNIX-Server  

-   Von Configuration Manager registrierte mobile Geräte  

-   Durch Microsoft Intune registrierte mobile Geräte  

-   Legacyclients für mobile Geräte  

-   Windows-Clients, die für die rein internetbasierte Clientverwaltung konfiguriert sind  

-   Windows-Clients, die von Configuration Manager im Internet erkannt werden  

## <a name="capabilities-that-benefit-from-extending-the-schema"></a>Funktionen, für die das Erweitern des Schemas vorteilhaft ist  
**Clientcomputerinstallation und Standortzuweisung:** Wenn ein neuer Client auf einem Windows-Computer installiert wird, durchsucht der Client Active Directory Domain Services nach Installationseigenschaften.  

-   **Problemumgehung:** Wenn Sie das Schema nicht erweitern, sollten Sie eine der folgenden Optionen verwenden, um für die Installation auf Computern erforderliche Konfigurationsdaten bereitzustellen:  

    -   **Verwenden Sie die Clientpushinstallation**. Bevor Sie eine Clientinstallationsmethode verwenden, stellen Sie sicher, dass alle Voraussetzungen erfüllt sind. Weitere Informationen finden Sie unter [Voraussetzungen für die Windows-Clientbereitstellung in Configuration Manager](../../clients/deploy/prerequisites-for-deploying-clients-to-windows-computers.md) im Abschnitt „Installationsmethodenabhängigkeiten“.  

    -   **Manuelles Installieren von Clients** und Bereitstellen von Installationseigenschaften über die CCMSetup-Befehlszeileneigenschaften für die Installation. Dies umfasst folgende Aktionen:  

        -   Geben Sie einen Verwaltungspunkt oder Quellpfad an, damit der Computer die Installationsdateien über die CCMSetup-Eigenschaft **/mp:=&lt;Computername des Verwaltungspunkts\>** bzw. **/source:&lt;Pfad für die Clientquelldateien\>** auf der CCMSetup-Befehlszeile während der Clientinstallation herunterladen kann.  

        -   Geben Sie eine Liste von ersten Verwaltungspunkten an, die vom Client verwendet werden, damit eine Zuordnung zum Standort möglich ist und die Clientrichtlinie sowie die Standorteinstellungen heruntergeladen werden können. Zu diesem Zweck verwenden Sie die „CCMSetup Client.msi“-Eigenschaft „SMSMP“.  

    -   **Veröffentlichen des Verwaltungspunkts in DNS oder WINS** und Konfigurieren von Clients für die Verwendung dieser Dienstidentifizierungsmethode.  

**Portkonfiguration für die Kommunikation zwischen Client und Server** – Wenn ein Client installiert wird, wird er mit Portinformationen konfiguriert, die in Active Directory gespeichert sind. Wenn Sie den Port für die Kommunikation zwischen Client und Server für einen Standort später ändern, kann ein Client diesen neuen Port aus en Active Directory-Domänendienste abrufen.  

-   **Problemumgehung:** Wenn Sie das Schema nicht erweitern, verwenden Sie eine der folgenden Optionen, um neue Portkonfigurationen für vorhandene Clients bereitzustellen:  

    -   **Installieren Sie Clients neu** mit Optionen, die den neuen Port konfigurieren.  

    -   **Stellen Sie auf den Clients ein benutzerdefiniertes Skript zum Aktualisieren der Portinformationen bereit**. Können Clients wegen einer Portänderung nicht mit einem Standort kommunizieren, können Sie Configuration Manager nicht für die Skriptbereitstellung verwenden. Sie könnten beispielsweise Gruppenrichtlinien verwenden.  

**Szenarios für die Inhaltsbereitstellung** – Wenn Sie Inhalte an einem Standort erstellen und an einem anderen Standort in der Hierarchie bereitstellen, muss der Zielstandort in der Lage sein, die Signatur der signierten Inhaltsdaten zu überprüfen. Dazu ist der Zugriff auf den öffentlichen Schlüssel des Quellstandorts erforderlich, auf dem die Daten erstellt wurde. Wenn Sie das Active Directory-Schema für Configuration Manager erweitern, steht der öffentliche Schlüssel eines Standorts allen Standorten in der Hierarchie zur Verfügung.  

-   **Problemumgehung**: Wenn Sie das Schema nicht erweitern, verwenden Sie das Hierarchieverwaltungstool **preinst.exe**, um die Informationen zu dem sicheren Schlüssel zwischen Standorten auszutauschen.  

     Wenn Sie beispielsweise planen, Inhalte an einem primären Standort zu erstellen und diese dann an einem sekundären Standort unterhalb eines anderen primären Standorts bereitzustellen, müssen Sie entweder das Active Directory-Schema erweitern, damit der öffentliche Schlüssel des primären Quellstandorts durch den sekundären Standort abgerufen werden kann, oder die Schlüssel mithilfe von „preinst.exe“ direkt zwischen beiden Standorten freigeben.  

## <a name="active-directory-attributes-and-classes"></a>Active Directory-Attribute und -Klassen  
Wenn Sie das Schema für Configuration Manager erweitern, werden dem Schema die folgenden Klassen und Attribute hinzugefügt und für alle Configuration Manager-Standorte in der Active Directory-Gesamtstruktur verfügbar gemacht.  

-   Attribute:  

    -   cn=mS-SMS-Assignment-Site-Code  

    -   cn=mS-SMS-Capabilities  

    -   cn=MS-SMS-Default-MP  

    -   cn=mS-SMS-Device-Management-Point  

    -   cn=mS-SMS-Health-State  

    -   cn=MS-SMS-MP-Address  

    -   cn=MS-SMS-MP-Name  

    -   cn=MS-SMS-Ranged-IP-High  

    -   cn=MS-SMS-Ranged-IP-Low  

    -   cn=MS-SMS-Roaming-Boundaries  
        auf  

    -   cn=MS-SMS-Site-Boundaries  

    -   cn=MS-SMS-Site-Code  

    -   cn=mS-SMS-Source-Forest  

    -   cn=mS-SMS-Version  

-   Klassen:  

    -   cn=MS-SMS-Management-Point  

    -   cn=MS-SMS-Roaming-Boundary-Range  

    -   cn=MS-SMS-Server-Locator-Point  

    -   cn=MS-SMS-Site  

> [!NOTE]
> 
>  Die Schemaerweiterungen können Attribute und Klassen enthalten, die aus vorherigen Versionen des Produkts übernommen wurden, aber von Configuration Manager nicht verwendet werden. Beispiel:  
> 
> 
> - Attribut: cn=MS-SMS-Site-Boundaries  
>   -   Klasse: cn=MS-SMS-Server-Locator-Point  

Sie können sicherstellen, dass die vorangehenden Listen aktuell sind, indem Sie die Datei **ConfigMgr_ad_schema.LDF** aus dem Ordner **\SMSSETUP\BIN\x64** der Configuration Manager-Installationsmedien anzeigen.  
