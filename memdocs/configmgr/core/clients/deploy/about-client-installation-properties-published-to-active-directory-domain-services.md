---
title: Clientinstallationseigenschaften in Active Directory
titleSuffix: Configuration Manager
description: Veröffentlichen von Installationseigenschaften des Configuration Manager-Clients in Active Directory Domain Services
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 101d7d4d-92db-419d-b2ae-3c1c1dea68e9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 49b2edf7234e53c3fc03542f803933463190e8c1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692068"
---
# <a name="about-client-installation-properties-published-to-active-directory-domain-services"></a>Informationen zu Clientinstallationseigenschaften, die in Active Directory-Domänendiensten veröffentlicht wurden

*Gilt für: Configuration Manager (Current Branch)*

Wenn Sie das Active Directory-Schema für Configuration Manager erweitern, und der Standort in Active Directory Domain Services veröffentlicht wird, werden viele Clientinstallationseigenschaften in Active Directory Domain Services veröffentlicht. Wenn diese Clientinstallationseigenschaften von einem Computer gefunden werden können, kann er sie im Rahmen der Configuration Manager-Clientbereitstellung verwenden.  

 Die Verwendung von Active Directory-Domänendiensten zum Veröffentlichen von Clientinstallationseigenschaften hat u. a. folgende Vorteile:  

-   Bei Clientinstallationen, die auf einem Softwareupdatepunkt oder auf Gruppenrichtlinien basieren, müssen nicht auf jedem Computer Setupparameter eingerichtet werden.  

-   Da diese Informationen automatisch generiert werden, wird das Risiko eines Fehlers durch manuelle Eingabe der Installationseigenschaften beseitigt.  

> [!NOTE]  
>  Weitere Informationen zum Erweitern des Active Directory-Schemas für Configuration Manager und zum Veröffentlichen einer Website finden Sie unter [Schemaerweiterungen für Configuration Manager](../../plan-design/network/schema-extensions.md).  

## <a name="client-installation-properties-published-to-active-directory-domain-services"></a>Clientinstallationseigenschaften, die in Active Directory Domain Services veröffentlicht wurden  
Im folgenden finden Sie eine Liste der Clientinstallationseigenschaften. Weitere Informationen zu den einzelnen Elementen finden Sie unter [Informationen zu Parametern und Eigenschaften für die Clientinstallation](../../../core/clients/deploy/about-client-installation-properties.md).  

- Der Configuration Manager-Standortcode.  

- Das Signaturzertifikat des Standortservers  

- Der vertrauenswürdige Stammschlüssel  

- Die Clientkommunikationsports für HTTP und HTTPS  

- Der Fallbackstatuspunkt. Wenn der Standort mehrere Fallbackstatuspunkte aufweist, wird in Active Directory-Domänendiensten nur der zuerst installierte veröffentlicht.  

- Eine Einstellung, um anzugeben, dass der Client nur über HTTPS kommunizieren darf  

- Einstellungen im Zusammenhang mit PKI-Zertifikaten:  

  -   Angabe, ob ein PKI-Zertifikat verwendet werden soll  

  -   Die Auswahlkriterien für die Zertifikatauswahl. Diese werden möglicherweise benötigt, weil der Client mehr als ein gültiges PKI-Zertifikat aufweist, das für Configuration Manager verwendet werden kann.  

  -   Eine Einstellung, um zu bestimmen, welches Zertifikat zu verwenden ist, wenn der Client nach der Auswahl des Zertifikats über mehrere gültige Zertifikate verfügt  

  -   Die Liste der Zertifikataussteller, die eine Liste vertrauenswürdiger Stamm-Zertifizierungsstellenzertifikate enthält  

- Clientinstallationseigenschaften für "client.msi", die im Dialogfeld **Eigenschaften von Clientpushinstallation** auf der Registerkarte **Client** angegeben werden.

In Active Directory-Domänendiensten veröffentlichte Eigenschaften werden nur dann von der Clientinstallation (CCMSetup) verwendet, wenn keine anderen Eigenschaften mithilfe einer der folgenden Methoden angegeben werden:  

-   Der manuellen Installationsmethode (weiter unten in diesem Artikel beschrieben)

-   Der manuellen Gruppenrichtlinieninstallationsmethode (weiter unten in diesem Artikel beschrieben)

> [!NOTE]  
>  Die Clientinstallationseigenschaften werden zur Installation des Clients verwendet. Diese Eigenschaften können durch neue Einstellungen vom zugewiesenen Standort außer Kraft gesetzt werden, nachdem der Client installiert und erfolgreich einem Configuration Manager-Standort zugewiesen wurde.  

 Verwenden Sie die Details in den folgenden Abschnitten, um zu bestimmen, welche Configuration Manager-Clientinstallationsmethoden Active Directory Domain Services verwenden, um Clientinstallationseigenschaften abzurufen.  

## <a name="client-push-installation"></a>Clientpushinstallation  
 Bei der Clientpushinstallation werden Installationseigenschaften nicht mithilfe der Active Directory-Domänendienste abgerufen.  

 Stattdessen können Sie Clientinstallationseigenschaften im Dialogfeld **Eigenschaften von Clientpushinstallation** auf der Registerkarte **Installationseigenschaften** angeben. Diese Optionen und clientrelevanten Standorteinstellungen werden in einer Datei gespeichert, die während der Clientinstallation vom Client gelesen wird.  

> [!NOTE]  
>  Für die Clientpushinstallation müssen Sie weder CCMSetup-Eigenschaften noch den Fallbackstatuspunkt oder den vertrauenswürdigen Stammschlüssel auf der Registerkarte **Installationseigenschaften** angeben. Diese Einstellungen werden den Clients bei ihrer Installation mithilfe der Clientpushinstallation automatisch bereitgestellt.
CCMSetup unterstützt zusätzlich zu den Client.msi-Eigenschaften die folgenden Parameter: /forcereboot, /skipprereq, /logon, /BITSPriority, /downloadtimeout, /forceinstall

 Alle Eigenschaften, die Sie auf der Registerkarte **Installationseigenschaften** angeben, werden in Active Directory-Domänendiensten veröffentlicht, wenn der Standort in Active Directory-Domänendiensten veröffentlicht wird. Diese Einstellungen werden bei der Clientinstallation gelesen, wenn CCMSetup ohne Installationseigenschaften ausgeführt wird.  

## <a name="software-update-point-based-installation"></a>Auf einem Softwareupdatepunkt basierende Installation  
 Die auf einem Softwareupdatepunkt basierende Installationsmethode unterstützt das Hinzufügen von Installationseigenschaften zur CCMSetup-Befehlszeile nicht.  

 Wurden keine Befehlszeileneigenschaften mithilfe von Gruppenrichtlinien auf dem Clientcomputer bereitgestellt, werden die Active Directory-Domänendienste von CCMSetup nach Installationseigenschaften durchsucht.  

## <a name="group-policy-installation"></a>Gruppenrichtlinieninstallation  
 Bei der auf einer Gruppenrichtlinie basierenden Installation wird das Hinzufügen von Installationseigenschaften zur CCMSetup-Befehlszeile nicht unterstützt.  

 Wurden keine Befehlszeileneigenschaften auf dem Clientcomputer bereitgestellt, werden die Active Directory-Domänendienste von CCMSetup nach Installationseigenschaften durchsucht.  

## <a name="manual-installation"></a>Manuelle Installation  
 Die Active Directory-Domänendienste werden unter den folgenden Umständen von CCMSetup nach Installationseigenschaften durchsucht:  

-   Es sind keine Befehlszeileneigenschaften nach dem Befehl CCMSetup.exe angegeben.  

-   Es wurden keine Installationseigenschaften über Gruppenrichtlinien auf dem Computer bereitgestellt.  

## <a name="logon-script-installation"></a>Anmeldeskriptinstallation  
 Die Active Directory-Domänendienste werden unter den folgenden Umständen von CCMSetup nach Installationseigenschaften durchsucht:  

-   Es sind keine Befehlszeileneigenschaften nach dem Befehl CCMSetup.exe angegeben.  

-   Es wurden keine Installationseigenschaften über Gruppenrichtlinien auf dem Computer bereitgestellt.  

## <a name="software-distribution-installation"></a>Softwareverteilungsinstallation  
 Die Active Directory-Domänendienste werden unter den folgenden Umständen von CCMSetup nach Installationseigenschaften durchsucht:  

-   Es sind keine Befehlszeileneigenschaften nach dem Befehl CCMSetup.exe angegeben.  

-   Es wurden keine Installationseigenschaften über Gruppenrichtlinien auf dem Computer bereitgestellt.  

## <a name="installations-for-clients-that-cannot-access-active-directory-domain-services"></a>Installationen für Clients, die nicht auf Active Directory-Domänendienste zugreifen können  
Diese Clientcomputer können die veröffentlichten Installationseigenschaften in Active Directory-Domänendiensten nicht lesen und nicht darauf zugreifen.

 Zu diesen Clients gehören:  

-   Arbeitsgruppencomputer  

-   Clients, die einem Configuration Manager-Standort zugewiesen sind, der nicht in Active Directory-Domänendiensten veröffentlicht wurde  

-   Clients, die sich bei der Installation im Internet befinden  
