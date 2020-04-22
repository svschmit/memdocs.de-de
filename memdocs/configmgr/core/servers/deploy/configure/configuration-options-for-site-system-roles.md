---
title: Optionen für Standortsystemrollen
titleSuffix: Configuration Manager
description: In diesem Artikel finden Sie Informationen über Configuration Manager-Standortsystemrollen, die nicht unbedingt selbsterklärend sind.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 0e9f0fbd-e442-4509-a021-bfdedf2d04dd
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 9dfe9e0cb2ecefc636c67cf127e596fd1ad2bfa4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704808"
---
# <a name="configuration-options-for-site-system-roles-in-configuration-manager"></a>Konfigurationsoptionen für Standortsystemrollen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Die meisten Konfigurationsoptionen für Configuration Manager-Standortsystemrollen sind selbsterklärend oder werden bei der Installation im Assistenten bzw. in den Dialogfeldern erklärt. In den folgenden Abschnitten werden Standortsystemrollen erläutert, für deren Einstellungen möglicherweise zusätzliche Informationen erforderlich sind.  


## <a name="application-catalog-website-point"></a><a name="BKMK_ApplicationCatalog_Website"></a> Anwendungskatalog-Websitepunkt  

> [!Important]
> Die Silverlight-Benutzeroberfläche für den Anwendungskatalog wird ab Current Branch-Version 1806 nicht unterstützt. Ab Version 1906 verwenden aktualisierte Clients automatisch den Verwaltungspunkt für Anwendungsbereitstellungen, die Benutzern zur Verfügung stehen. Zudem können Sie keine neuen Anwendungskatalogrollen installieren. Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910.  
>
> Weitere Informationen finden Sie in den folgenden Artikeln:
>
> - [Konfigurieren des Softwarecenters](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Entfernte und veraltete Features](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Weitere Informationen zum Einrichten des Anwendungskatalog-Websitepunkts finden Sie unter [Planen und Konfigurieren der Anwendungsverwaltung](../../../../apps/plan-design/plan-for-and-configure-application-management.md).  


## <a name="application-catalog-web-service-point"></a><a name="BKMK_ApplicationCatalog_WebService"></a> Anwendungskatalog-Webdienstpunkt  

> [!Important]
> Die Silverlight-Benutzeroberfläche für den Anwendungskatalog wird ab Current Branch-Version 1806 nicht unterstützt. Ab Version 1906 verwenden aktualisierte Clients automatisch den Verwaltungspunkt für Anwendungsbereitstellungen, die Benutzern zur Verfügung stehen. Zudem können Sie keine neuen Anwendungskatalogrollen installieren. Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910.  
>
> Weitere Informationen finden Sie in den folgenden Artikeln:
>
> - [Konfigurieren des Softwarecenters](../../../../apps/plan-design/plan-for-software-center.md#bkmk_userex)
> - [Entfernte und veraltete Features](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

Weitere Informationen zum Einrichten des Anwendungskatalog-Webdienstpunkts finden Sie unter [Planen und Konfigurieren der Anwendungsverwaltung](../../../../apps/plan-design/plan-for-and-configure-application-management.md).  


## <a name="certificate-registration-point"></a><a name="BKMK_CertificateRegistrationPoint"></a> Zertifikatregistrierungspunkt  

Weitere Informationen zum Einrichten des Zertifikatregistrierungspunkts finden Sie unter [Einführung in Zertifikatprofile in System Center Configuration Manager](../../../../protect/deploy-use/introduction-to-certificate-profiles.md).  


## <a name="distribution-point"></a><a name="BKMK_Distribution_Point"></a> Verteilungspunkt  

Weitere Informationen zum Einrichten des Verteilungspunkts für die Inhaltsbereitstellung finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur](manage-content-and-content-infrastructure.md).  

Weitere Informationen zum Einrichten des Verteilungspunkts für PXE-Bereitstellungen finden Sie unter [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).  

Weitere Informationen zum Einrichten des Verteilungspunkts für Multicastbereitstellungen finden Sie unter [Verwenden von Multicast zum Bereitstellen von Windows über das Netzwerk](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).  

### <a name="install-and-configure-iis-if-required-by-configuration-manager"></a>Installieren und Konfigurieren von IIS (falls für Configuration Manager erforderlich)

Aktivieren Sie diese Option, damit Configuration Manager IIS auf dem Standortsystem installieren und einrichten kann, sofern nicht bereits geschehen. IIS müssen auf allen Verteilungspunkten installiert sein, und Sie müssen diese Einstellung auswählen, um mit dem Assistenten fortzufahren.  

### <a name="site-system-installation-account"></a>Standortsystem-Installationskonto

Bei Verteilungspunkten, die auf einem Standortserver installiert sind, wird nur die Verwendung des Computerkontos des Standortservers als Standortsystem-Installationskonto unterstützt. Weitere Informationen finden Sie unter [Konten](../../../plan-design/hierarchy/accounts.md#site-system-installation-account).  


## <a name="enrollment-point"></a><a name="BKMK_Enrollment_Point"></a> Anmeldungspunkt  

Anmeldungspunkte werden zur Installation von macOS-Computern und zur Registrierung von Geräten verwendet, die lokal über die Geräteverwaltung verwaltet werden. Weitere Informationen finden Sie in den folgenden Artikeln:  

- [Bereitstellen von Clients auf Macintosh-Computern](../../../clients/deploy/deploy-clients-to-macs.md)  

- [Lokales Registrieren von Geräten mit der mobilen Geräteverwaltung](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md)  

### <a name="allowed-connections"></a>Zulässige Verbindungen

Die HTTPS-Einstellung wird automatisch verwendet. Für diese ist ein PKI-Zertifikat für den Server zur Serverauthentifizierung beim Anmeldungsproxypunkt und zur SSL-Datenverschlüsselung erforderlich. Weitere Informationen zu PKI-Zertifikatanforderungen finden Sie unter [PKI-Zertifikatanforderungen](../../../plan-design/network/pki-certificate-requirements.md).  

Eine Beispielbereitstellung des Serverzertifikats sowie Informationen zum Konfigurieren des Zertifikats in IIS (Internetinformationsdienste) finden Sie unter [Bereitstellen des Webserverzertifikats für Standortsysteme, von denen IIS ausgeführt wird](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  


## <a name="enrollment-proxy-point"></a><a name="BKMK_Enrollment_Proxy_Point"></a> Anmeldungsproxypunkt  

Weitere Informationen zum Einrichten eines Anmeldungsproxypunkts für mobile Geräte finden Sie unter [Lokales Registrieren von Geräten mit der mobilen Geräteverwaltung](../../../../mdm/deploy-use/user-enroll-devices-on-premises-mdm.md).  

### <a name="client-connections"></a>Clientverbindungen

Die HTTPS-Einstellung wird automatisch ausgewählt. Sie erfordert die folgenden PKI-Zertifikate auf dem Server:

- Für die Serverauthentifizierung auf mobilen Geräten und Mac-Computern, die Sie mit Configuration Manager registrieren
- Für die Datenverschlüsselung über SSL (Secure Sockets Layer)

Weitere Informationen zu den Zertifikatanforderungen finden Sie unter [PKI-Zertifikatanforderungen](../../../plan-design/network/pki-certificate-requirements.md).  

Eine Beispielbereitstellung des Serverzertifikats sowie Informationen zum Konfigurieren des Zertifikats in IIS (Internetinformationsdienste) finden Sie unter [Bereitstellen des Webserverzertifikats für Standortsysteme, von denen IIS ausgeführt wird](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_webserver2008_cm2012).  


## <a name="fallback-status-point"></a><a name="BKMK_Fallback_Status_Point"></a> Fallbackstatuspunkt  

### <a name="number-of-state-messages-and-throttle-interval-in-seconds"></a>Anzahl von Zustandsmeldungen und Drosselungsintervall (in Sekunden)

Die Standardeinstellungen für diese Optionen sind 10.000 Zustandsmeldungen und 3.600 Sekunden für das Drosselungsintervall. Obwohl diese Einstellungen i.d.R. ausreichend sind, müssen Sie sie ggf. ändern, wenn die beiden folgenden Bedingungen erfüllt sind:  

- Vom Fallbackstatuspunkt werden Verbindungen nur aus dem Intranet akzeptiert.  

- Sie verwenden den Fallbackstatuspunkt während der Einführung einer Clientbereitstellung für zahlreiche Computer.  

In diesem Szenario kann ein kontinuierlicher Strom von Zustandsmeldungen einen Rückstand von Zustandsmeldungen erzeugen, wodurch eine hohe Prozessorauslastung auf dem Standortserver für einen längeren Zeitraum verursacht wird. Außerdem sehen Sie in der Configuration Manager-Konsole und in den Clientbereitstellungsberichten möglicherweise keine aktuellen Informationen über die Clientbereitstellung.  

Diese Einstellungen für Fallbackstatuspunkte sollen für Zustandsmeldungen eingerichtet werden, die während der Clientbereitstellung generiert werden. Sie sind nicht für Probleme bei der Clientkommunikation gedacht, beispielsweise wenn Clients im Internet keine Verbindung mit dem internetbasierten Verwaltungspunkt herstellen können. Da diese Einstellungen von dem Fallbackstatuspunkt nicht nur auf die Zustandsmeldungen angewendet werden können, die bei der Clientbereitstellung generiert werden, konfigurieren Sie die Einstellungen nicht, wenn der Fallbackstatuspunkt Verbindungen aus dem Internet akzeptiert.  

Jeder Computer, auf dem der Konfigurations-Manager-Client installiert ist, sendet die folgenden vier Zustandsmeldungen an den Fallbackstatuspunkt:  

- Clientbereitstellung wurde gestartet  

- Clientbereitstellung war erfolgreich  

- Clientzuweisung wurde gestartet  

- Clientzuweisung war erfolgreich  

Computer, die nicht installiert werden können oder den Konfigurations-Manager-Client zuweisen, senden zusätzliche Zustandsmeldungen.  

Wenn Sie den Configuration Manager-Client beispielsweise für 20.000 Computer bereitstellen, werden möglicherweise 80.000 Zustandsmeldungen von der Bereitstellung an den Fallbackstatuspunkt gesendet. Da aufgrund der Standardkonfiguration der Einschränkung alle 3.600 Sekunden (1 Stunde) 10.000 Zustandsmeldungen an den Fallbackstatuspunkt gesendet werden können, kann dies beim Fallbackstatuspunkt zu einem Rückstand bei der Verarbeitung der Zustandsmeldungen führen. Berücksichtigen Sie auch die verfügbare Netzwerkbandbreite zwischen dem Fallbackstatuspunkt und dem Standortserver sowie die Verarbeitungsleistung des Standortservers, um viele Zustandsmeldungen zu verarbeiten.  

Um solche Probleme zu vermeiden, sollten Sie erwägen, die Anzahl von Zustandsmeldungen zu erhöhen und das Drosselungsintervall zu verkürzen.  

Setzen Sie die Einschränkungswerte für den Fallbackstatuspunkt zurück, wenn eine der folgenden Bedingungen zutrifft:  

- Ihren Berechnungen nach sind die aktuellen Einschränkungswerte höher, als dies für die Verarbeitung von Zustandsmeldungen vom Fallbackstatuspunkt erforderlich ist.  

- Die aktuellen Drosselungseinstellungen verursachen eine hohe Prozessorauslastung auf dem Standortserver.  

Ändern Sie die Drosselungseinstellungen für den Fallbackstatuspunkt nur dann, wenn Sie sich über die Konsequenzen im Klaren sind. Wenn Sie beispielsweise die Drosselungseinstellungen stark erhöhen, kann dadurch die Prozessorauslastung auf dem Standortserver so steigen, dass alle Standortvorgänge verlangsamt werden.  
