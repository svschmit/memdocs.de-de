---
title: Konfigurieren von Clientkommunikationsports
titleSuffix: Configuration Manager
description: Hier erhalten Sie Informationen zum Konfigurieren der Clientkommunikationsports in Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 406bbdbf-ab4a-4121-a68b-154f96ea14ec
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 30b553bbe2a68ec97e4d5200644a88d09ee5967d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81693558"
---
# <a name="how-to-configure-client-communication-ports-in-configuration-manager"></a>Konfigurieren der Clientkommunikationsports in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Sie können die Anforderungsportnummern ändern, die von Configuration Manager-Clients zur Kommunikation mit Standortsystemen verwendet werden, bei denen HTTP und HTTPS für die Kommunikation verwendet werden. Auch wenn es wahrscheinlicher ist, dass HTTP oder HTTPS für Firewalls bereits konfiguriert ist, bewirkt eine Clientbenachrichtigung mit Verwendung von HTTP oder HTTPS auf dem Verwaltungspunktcomputer eine höhere CPU- und Arbeitsspeicherauslastung als bei Verwendung einer benutzerdefinierten Portnummer. Sie können darüber hinaus die Standortportnummern für die Clientaktivierung über herkömmliche Aktivierungspakete angeben.  

 Für HTTP- und HTTPS-Anforderungsports können Sie sowohl eine Standardportnummer als auch eine alternative Portnummer angeben. Wenn bei der Kommunikation mit dem Standardport Fehler auftreten, wird automatisch die Kommunikation über den alternativen Port versucht. Sie können Einstellungen für HTTP- und HTTPS-Datenkommunikation angeben.  

 Die Standardwerte für Clientanforderungsports lauten für HTTP-Verkehr **80** und für HTTPS-Verkehr **443** . Sie sollten diese nur ändern, wenn Sie die Standardwerte nicht verwenden möchten. Benutzerdefinierte Ports sind zum Beispiel dann sinnvoll, wenn Sie in IIS anstelle der Standardwebsite eine benutzerdefinierte Website verwenden. Wenn Sie die Standardportnummern für die Standardwebsite in IIS ändern und von anderen Anwendungen ebenfalls auf die Standardwebsite zugegriffen wird, kommt es zu Verbindungsfehlern.  

> [!IMPORTANT]
>  Ändern Sie die Portnummern in Configuration Manager nur, wenn Sie sich der Konsequenzen bewusst sind. Beispiele:  
> 
> - Wenn Sie die Portnummern für die Clientanforderungsdienste in der Standortkonfiguration ändern und vorhandene Clients nicht für die neuen Portnummern umkonfigurieren, sind diese Clients nicht mehr verwaltet.  
>   -   Vergewissern Sie sich vor dem Konfigurieren einer nicht standardmäßigen Portnummer, dass diese Konfiguration von Firewalls und allen beteiligten Netzwerkgeräten unterstützt wird, und ändern Sie ggf. deren Konfiguration. Wenn Sie Clients über das Internet verwalten möchten und die HTTPS-Standardportnummer 443 ändern, wird diese Verbindung von Routern und Firewalls im Internet möglicherweise blockiert.  

 Clients müssen für die neuen Anforderungsportnummern konfiguriert werden, damit diese Clients nach dem Ändern der Anforderungsportnummern weiterhin verwaltet werden können. Wenn Sie die Anforderungsports an einem primären Standort ändern, übernehmen alle damit verbundenen sekundären Standorte automatisch dieselbe Portkonfiguration. Konfigurieren Sie die Ports am primären Standort anhand des in diesem Thema beschriebenen Verfahrens.  

> [!NOTE]  
>  Informationen zum Konfigurieren der Anforderungsports für Clients auf Computern, auf denen Linux und UNIX ausgeführt wird, finden Sie unter [Configure Request Ports for the Client for Linux and UNIX (Konfigurieren von Anforderungsports für den Client für Linux und UNIX)](../../../core/clients/deploy/deploy-clients-to-unix-and-linux-servers.md#BKMK_ConfigLnUClientCommuincations).  

 Wenn der Configuration Manager-Standort in den Active Directory-Domänendiensten veröffentlicht wird, werden neue und vorhandene Clients, die auf diese Informationen zugreifen können, automatisch mit den Porteinstellungen ihres Standorts konfiguriert. Sie müssen keine weiteren Maßnahmen ergreifen. Zu den Clients, die nicht auf diese in den Active Directory-Domänendiensten veröffentlichten Informationen zugreifen können, gehören Arbeitsgruppenclients, Clients aus einer anderen Active Directory-Gesamtstruktur, nur für das Internet konfigurierte Clients sowie Clients, die aktuell mit dem Internet verbunden sind. Wenn Sie die Standardportnummer ändern, nachdem diese Clients installiert wurden, installieren Sie sie erneut, und installieren Sie alle neuen Clients anhand einer der folgenden Methoden:  

- Installieren Sie die Clients mithilfe des Clientpushinstallations-Assistenten neu. Bei einer Clientpushinstallation werden Clients automatisch mit der aktuellen Portkonfiguration des Standorts konfiguriert. Weitere Informationen zur Verwendung des Clientpushinstallations-Assistenten finden Sie unter [How to Install Configuration Manager Clients by Using Client Push (Installieren von Configuration Manager-Clients mithilfe von Clientpush)](../../../core/clients/deploy/deploy-clients-to-windows-computers.md#BKMK_ClientPush).  

- Installieren Sie die Clients mithilfe von CCMSetup.exe sowie den client.msi-Installationseigenschaften CCMHTTPPORT und CCMHTTPSPORT neu. Weitere Informationen zu diesen Eigenschaften finden Sie unter [Informationen zu Parametern und Eigenschaften für die Clientinstallation](../../../core/clients/deploy/about-client-installation-properties.md).  

- Installieren Sie die Clients mittels einer Methode neu, bei der die Active Directory-Domänendienste nach Configuration Manager-Clientinstallationseigenschaften durchsucht werden. Weitere Informationen finden Sie unter [Informationen zu Clientinstallationseigenschaften, die in Active Directory Domain Services veröffentlicht wurden](../../../core/clients/deploy/about-client-installation-properties-published-to-active-directory-domain-services.md).  

  Die Portnummern für vorhandene Clients können Sie auch mithilfe des Skripts PORTSWITCH.VBS neu konfigurieren, das zusammen mit den Installationsmedien im Ordner SMSSETUP\Tools\PortConfiguration bereitgestellt wird.  

> [!IMPORTANT]  
>  Für vorhandene und neue Clients, die zurzeit mit dem Internet verbunden sind, müssen Sie die nicht standardmäßigen Portnummern mithilfe der client.msi-Eigenschaften CCMHTTPPORT und CCMHTTPSPORT von CCMSetup.exe konfigurieren.  

 Im Anschluss an die Änderung der Anforderungsports auf dem Standort werden neue Clients, die mithilfe der standortweiten Clientpushinstallations-Methode installiert werden, automatisch mit den aktuellen Portnummern des Standorts konfiguriert.  

#### <a name="to-configure-the-client-communication-port-numbers-for-a-site"></a>So konfigurieren Sie die Portnummern für die Clientkommunikation für einen Standort  

1. Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2. Erweitern Sie im Arbeitsbereich **Verwaltung** den Knoten **Standortkonfiguration**, klicken Sie auf **Standorte**, und wählen Sie den zu konfigurierenden primären Standort aus.  

3. Klicken Sie auf der Registerkarte **Startseite** auf **Eigenschaften**, und klicken Sie dann auf die Registerkarte **Ports** .  

4. Wählen Sie die gewünschten Objekte aus, und klicken Sie auf das Symbol "Eigenschaften", um das Dialogfeld **Portdetail** anzuzeigen.  

5. Geben Sie im Dialogfeld **Portdetail** die Portnummer und die Objektbeschreibung an, und klicken Sie dann auf **OK**.  

6. Wählen Sie **Benutzerdefinierte Website verwenden** aus, wenn Sie planen, den benutzerdefinierten Websitenamen **SMSWeb** für Standortsysteme zu verwenden, auf denen IIS ausgeführt wird.  

7. Klicken Sie auf **OK** , um das Eigenschaftendialogfeld für den Standort zu schließen.  

   Wiederholen Sie diesen Vorgang für alle primären Standorte in der Hierarchie.
