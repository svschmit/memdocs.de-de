---
title: Vorbereiten der Bereitstellung des Clients für Mac-Computer
titleSuffix: Configuration Manager
description: Konfigurationsaufgaben vor dem Bereitstellen des Configuration Manager-Clients auf Mac-Computern.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 2285a953-6a86-4ed5-97dd-cd57b02bc1ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2b5bcbce659601e10f44f06af94eb939767a389a
ms.sourcegitcommit: 214fb11771b61008271c6f21e17ef4d45353788f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/07/2020
ms.locfileid: "82906621"
---
# <a name="prepare-to-deploy-client-software-to-macs"></a>Vorbereiten der Bereitstellung von Clientsoftware auf Macs

*Gilt für: Configuration Manager (Current Branch)*

Führen Sie die folgenden Schritte aus, um sicherzustellen, dass Sie zum [Bereitstellen des Configuration Manager-Clients auf Mac-Computern](deploy-clients-to-macs.md) bereit sind.



## <a name="mac-prerequisites"></a>Voraussetzungen für Mac-Computer

Das Mac-Clientinstallationspaket wird nicht mit den Configuration Manager-Medien geliefert. Laden Sie die **Clients für weitere Betriebssysteme** aus dem [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=47719) herunter.  

Eine Liste der unterstützten Versionen finden Sie unter [Unterstützte Betriebssysteme für Clients und Geräte](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md#mac-computers).



## <a name="certificate-requirements"></a>Zertifikatanforderungen

Die Clientinstallation und -verwaltung für Macintosh-Computer erfordert PKI-Zertifikate (Public Key-Infrastruktur). Durch PKI-Zertifikate wird die Kommunikation zwischen den Macintosh-Computern und dem Configuration Manager-Standort mithilfe gegenseitiger Authentifizierung und verschlüsselter Datenübertragungen gesichert. Configuration Manager kann ein Benutzerclientzertifikat anfordern und installieren. Dabei werden Zertifikatdienste mit einer Unternehmenszertifizierungsstelle und der Anmeldungspunkt sowie der Anmeldungsproxypunkt von Configuration Manager verwendet. Sie können ein Computerzertifikat auch unabhängig von Configuration Manager anfordern und installieren. Dieses Zertifikat muss die Configuration Manager-Zertifikatanforderungen erfüllen.  

Configuration Manager-Clients für Mac prüfen stets auf Zertifikatsperren. Sie können diese Funktion nicht deaktivieren.  

Wenn Mac-Clients die Zertifikatsperrliste nicht finden können, können sie keine Verbindung mit den Configuration Manager-Standortsystemen herstellen. Vor allem bei Mac-Clients in einer anderen Gesamtstruktur als die ausstellende Zertifizierungsstelle müssen Sie den Entwurf Ihrer Zertifikatsperrliste prüfen. Stellen Sie sicher, dass Mac-Clients eine Zertifikatsperrliste finden und herunterladen können.  

Legen Sie vor dem Installieren des Configuration Manager-Clients auf einem Macintosh-Computer fest, wie das Clientzertifikat installiert werden soll:  

-   Verwenden der Configuration Manager-Registrierung mithilfe des Tools [CMEnroll](deploy-clients-to-macs.md#client-and-certificate-automation-with-cmenroll). Der Registrierungsprozess unterstützt die automatische Zertifikaterneuerung nicht. Registrieren Sie Mac-Computer erneut, bevor das Zertifikat abläuft.  

-   [Verwenden einer von Configuration Manager unabhängigen Zertifikatanforderungs- und -installationsmethode](deploy-clients-to-macs.md#bkmk_external).  

Weitere Informationen zu den Zertifikatanforderungen für Mac-Clients finden Sie unter [PKI-Zertifikatanforderungen für Configuration Manager](../../plan-design/network/pki-certificate-requirements.md).  

Macintosh-Clients werden automatisch dem Configuration Manager-Standort zugewiesen, von dem aus sie verwaltet werden. Mac-Clients werden als reine Internetclients installiert, selbst wenn die Kommunikation auf das Intranet beschränkt ist. Das heißt, dass sie mit internetfähigen Verwaltungspunkten und Verteilungspunkten am ihnen zugewiesenen Standort kommunizieren. Mac-Computer kommunizieren nicht mit Standortsystemen außerhalb ihres zugewiesenen Standorts.  

> [!IMPORTANT]  
>  Der Configuration Manager-Client für macOS kann nicht zum Herstellen der Verbindung mit einem Verwaltungspunkt verwendet werden, der für die Verwendung eines [Datenbankreplikats](../../servers/deploy/configure/database-replicas-for-management-points.md) konfiguriert ist.  



## <a name="deploy-a-web-server-certificate-to-site-system-servers"></a>Bereitstellen eines Webserverzertifikats für Standortsystemserver  

Wenn diese Standortsysteme nicht darüber verfügen, stellen Sie ein Webserverzertifikat für die Computer mit diesen Standortsystemrollen bereit:  

-   Verwaltungspunkt  

-   Verteilungspunkt  

-   Anmeldungspunkt  

-   Anmeldungsproxypunkt  

Im Webserverzertifikat muss der Internet-FQDN (vollqualifizierter Domänenname), der in den Eigenschaften des Standortsystems angegeben ist, enthalten sein. Auf den Server muss kein Zugriff über das Internet möglich sein, um Mac-Computer zu unterstützen. Wenn Sie keine internetbasierte Clientverwaltung benötigen, können Sie den Wert des Intranet-FQDN für den Internet-FQDN angeben.  

Geben Sie den Wert des Internet-FQDN für das Standortsystem im Webserverzertifikat für den Verwaltungspunkt, den Verteilungspunkt und den Anmeldungsproxypunkt an.

Weitere Informationen über eine Beispielbereitstellung finden Sie unter [Deploying the web server certificate for site systems that run IIS (Bereitstellen des Webserverzertifikats für Standortsysteme mit IIS)](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  



## <a name="deploy-a-client-authentication-certificate-to-site-system-servers"></a>Bereitstellen eines Clientauthentifizierungszertifikat für Standortsystemserver  

Wenn diese Standortsysteme nicht darüber verfügen, stellen Sie ein Clientauthentifizierungszertifikat für die Computer mit diesen Standortsystemrollen bereit:  

-   Verwaltungspunkt  

-   Verteilungspunkt  

Eine Beispielbereitstellung, bei der das Clientzertifikat für Verwaltungspunkte erstellt und installiert wird, finden Sie unter [Deploying the client certificate for Windows computers (Bereitstellen des Clientzertifikats für Windows-Computer)](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_client2008_cm2012).  

Eine Beispielbereitstellung, bei der das Clientzertifikat für Verteilungspunkte erstellt und installiert wird, finden Sie unter [Deploying the client certificate for distribution points (Bereitstellen des Clientzertifikats für Verteilungspunkte)](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012).  

> [!IMPORTANT]  
>  Zum Bereitstellen des Clients auf Geräten mit macOS Sierra muss der Antragstellername des Verwaltungspunktzertifikats ordnungsgemäß konfiguriert werden. Verwenden Sie beispielsweise den FQDN des Verwaltungspunktservers.  



## <a name="prepare-the-client-certificate-template-for-macs"></a>Vorbereiten der Clientzertifikatvorlage für Mac-Computer  

Die Zertifikatvorlage muss über die Berechtigungen **Lesen** und **Anmelden** für das Benutzerkonto verfügen, mit dem das Zertifikat auf dem Mac-Computer angemeldet wird.  

Weitere Informationen finden Sie unter [Deploying the client certificate for Mac computers (Bereitstellen des Clientzertifikats für Mac-Computer)](../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_MacClient_SP1).  



## <a name="configure-the-management-point-and-distribution-point"></a>Konfigurieren des Verwaltungspunkts und Verteilungspunkts  

Konfigurieren Sie Verwaltungspunkte für die folgenden Optionen:  

-   HTTPS  

-   Clientverbindungen aus dem Internet zulassen. Dieser Konfigurationswert wird benötigt, um Macintosh-Computer zu verwalten. Dies bedeutet jedoch nicht, dass der Zugriff auf Standortsystemserver über das Internet möglich sein muss.  

-   Verwendung dieses Verwaltungspunkts durch mobile Geräte und Macintosh-Computer zulassen  

Verteilungspunkte sind zum Installieren des Clients für Mac nicht erforderlich. Konfigurieren Sie Verteilungspunkte, um Clientverbindungen über das Internet zuzulassen, wenn Sie Software auf diesen Computern bereitstellen möchten, nachdem Sie den Client installiert haben.  


### <a name="to-configure-management-points-and-distribution-points-to-support-macs"></a>So konfigurieren Sie Verwaltungspunkte und Verteilungspunkte für die Unterstützung von Macintosh-Computern  

Stellen Sie sicher, dass der Verwaltungspunkt und der Verteilungspunkt mit einem Internet-FQDN konfiguriert sind, bevor Sie dieses Verfahren anwenden. Wenn diese Server die internetbasierte Clientverwaltung nicht unterstützen, geben Sie den Intranet-FQDN für den Internet-FQDN an.

Die Standortsystemrollen müssen sich an einem primären Standort befinden.  

1.  Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Server und Standortsystemrollen** aus. Wählen Sie dann den Server aus, der über die entsprechenden Standortsystemrollen verfügt.  

2.  Wählen Sie im Detailbereich die Rolle **Verwaltungspunkt** aus, und klicken Sie anschließend im Menüband auf **Eigenschaften**. Konfigurieren Sie folgende Optionen im Fenster **Eigenschaften des Verwaltungspunkts**:  

    1.  Wählen Sie **HTTPS** aus.  

    2.  Wählen Sie **Nur Internetclientverbindungen zulassen** oder **Allow intranet and internet client connections** (Intranet- und Internetclientverbindungen zulassen) aus. Für diese Optionen ist ein Internet- oder Intranet-FQDN erforderlich.  

    3.  Aktivieren Sie **Verwendung dieses Verwaltungspunkts durch mobile Geräte und Macintosh-Computer zulassen**.  

    4. Klicken Sie auf **OK**, um diese Konfiguration zu speichern.  

3.  Wählen Sie im Detailbereich des Knotens „Server- und Standortsystemrollen“ die Rolle **Verteilungspunkt** aus, und klicken Sie im Menüband auf **Eigenschaften**. Konfigurieren Sie folgende Optionen im Fenster **Verteilungspunkteigenschaften**:  

    -   Wählen Sie **HTTPS** aus.  

    -   Wählen Sie **Nur Internetclientverbindungen zulassen** oder **Allow intranet and internet client connections** (Intranet- und Internetclientverbindungen zulassen) aus. Für diese Optionen ist ein Internet- oder Intranet-FQDN erforderlich.  

    -   Klicken Sie auf **Zertifikat importieren**, suchen Sie die exportierte Clientzertifikatdatei für den Verteilungspunkt, und geben Sie das Kennwort an.  

4.  Wiederholen Sie dieses Verfahren für alle Verwaltungspunkte und Verteilungspunkte an primären Standorten, die Mac-Computer verwalten.  



## <a name="configure-the-enrollment-proxy-point-and-the-enrollment-point"></a>Konfigurieren des Anmeldungsproxypunkts und Anmeldungspunkts  

Installieren Sie beide Rollen am gleichen Standort. Sie müssen sie nicht auf dem gleichen Standortsystemserver oder der gleichen Active Directory-Gesamtstruktur installieren.  

Weitere Informationen zu Überlegungen und Platzierung von Standortsystemrollen finden Sie unter [Standortsystemrollen](../../plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md#bkmk_planroles).  

Informationen zum Hinzufügen der Standortsystemrollen zur Unterstützung von Mac-Computern finden Sie unter [Installieren von Standortsystemrollen](../../servers/deploy/configure/install-site-system-roles.md).

Wählen Sie auf der Seite **Systemrollenauswahl** in der Liste der verfügbaren Rollen **Anmeldungsproxypunkt** und **Anmeldungspunkt** aus.  



## <a name="install-the-reporting-services-point"></a>Installieren Sie den Reporting Services-Punkt.  

Weitere Informationen finden Sie unter [Installieren des Reporting Services-Punkts](../../servers/manage/configuring-reporting.md).  



## <a name="next-steps"></a>Nächste Schritte

[Deploy the Configuration Manager client to Mac computers (Bereitstellen des Configuration Manager-Clients für Mac-Computer)](deploy-clients-to-macs.md)  
