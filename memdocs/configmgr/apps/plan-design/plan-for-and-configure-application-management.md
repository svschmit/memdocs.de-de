---
title: Planen der Anwendungsverwaltung
titleSuffix: Configuration Manager
description: Implementieren und konfigurieren Sie die erforderlichen Abhängigkeiten zum Bereitstellen von Anwendungen in Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 2be84a1d-ebb9-47ae-8982-c66d5b92a52a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 03fda62774b930a1cc3603415f3b872050b9cb71
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689048"
---
# <a name="plan-for-and-configure-application-management-in-configuration-manager"></a>Planen und Konfigurieren der Anwendungsverwaltung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Implementieren Sie anhand der Informationen in diesem Artikel die erforderlichen Abhängigkeiten zum Bereitstellen von Anwendungen in Configuration Manager.  



## <a name="dependencies-external-to-configuration-manager"></a>Externe Abhängigkeiten von Configuration Manager  


### <a name="internet-information-services-iis"></a>Internetinformationsdienste (IIS)

IIS muss auf den Servern installiert sein, auf denen die folgenden Standortsystemrollen ausgeführt werden:

- Verwaltungspunkt  
- Verteilungspunkt  

Weitere Informationen finden Sie unter [Site and site system prerequisites for System Center Configuration Manager](../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Standort- und Standortsystemanforderungen für System Center Configuration Manager).  

> [!Note]  
> Für den Anwendungskatalog ist IIS ebenfalls erforderlich. Die Silverlight-Benutzeroberfläche wird jedoch ab Current Branch-Version 1806 nicht unterstützt. Ab Version 1906 verwenden aktualisierte Clients automatisch den Verwaltungspunkt für Anwendungsbereitstellungen, die Benutzern zur Verfügung stehen. Zudem können Sie keine neuen Anwendungskatalogrollen installieren. Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910.  
>
> Weitere Informationen finden Sie in den folgenden Artikeln:
>
> - [Konfigurieren des Softwarecenters](plan-for-software-center.md#bkmk_userex)
> - [Entfernte und veraltete Features](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  


### <a name="certificates-on-code-signed-applications-for-mobile-devices"></a>Zertifikate für codesignierte Anwendungen für mobile Geräte

Wenn Sie Anwendungen codesignieren, um sie auf mobilen Geräten bereitzustellen, verwenden Sie kein Zertifikat, das mithilfe einer Vorlage der Version 3 (**Windows Server 2008 Enterprise Edition**) generiert wurde. Bei Verwendung dieser Zertifikatvorlage wird ein Zertifikat generiert, das nicht mit Configuration Manager-Anwendungen für mobile Geräte kompatibel ist.

Wenn Sie Active Directory-Zertifikatdienste für die Codesignierung von Anwendungen für mobile Geräte nutzen, verwenden Sie keine Zertifikatvorlage der Version 3.


### <a name="audit-sign-in-events-for-user-device-affinity"></a>Überwachen von Anmeldeereignissen für Affinität zwischen Benutzer und Gerät  

Wenn Sie die Affinität zwischen Benutzer und Gerät automatisch erstellen möchten, konfigurieren Sie Clients zum Überwachen von Anmeldeereignissen.

Um die Affinität zwischen Benutzer und Gerät automatisch zu bestimmen, liest der Konfigurations-Manager-Client Anmeldeereignisse vom Typ **Erfolg** aus dem Windows-Sicherheitsereignisprotokoll. Aktivieren Sie diese Ereignisse mit diesen beiden Überwachungsrichtlinien:

- **Anmeldeversuche überwachen**
- **Anmeldeereignisse überwachen**

Für die automatische Erstellung von Beziehungen zwischen Benutzern und Geräten müssen Sie sicherstellen, dass diese beiden Einstellungen auf Clientcomputern aktiviert sind. Sie können diese Einstellungen mithilfe von Windows-Gruppenrichtlinien konfigurieren.

Weitere Informationen zur Affinität zwischen Benutzer und Gerät finden Sie unter [Verknüpfen von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät](../deploy-use/link-users-and-devices-with-user-device-affinity.md).  



## <a name="configuration-manager-dependencies"></a>Abhängigkeiten in Configuration Manager


### <a name="management-point"></a>Verwaltungspunkt

Von Clients wird eine Verbindung mit einem Verwaltungspunkt hergestellt, um eine Clientrichtlinie herunterzuladen und nach Inhalten zu suchen.

Ab Version 1906 verwenden aktualisierte Clients automatisch den Verwaltungspunkt für Anwendungsbereitstellungen, die Benutzern zur Verfügung stehen.

Bis Version 1902 verwenden Clients den Verwaltungspunkt, um eine Verbindung mit dem Anwendungskatalog herzustellen. Ohne Zugriff auf einen Verwaltungspunkt können Clients den Anwendungskatalog nicht nutzen.

> [!Note]  
> Ab Version 1806 werden keine Anwendungskatalogrollen mehr benötigt, um für Benutzer verfügbare Anwendungen im Softwarecenter anzuzeigen. Weitere Informationen finden Sie unter [Konfigurieren des Softwarecenters](plan-for-software-center.md#bkmk_userex).<!--1358309-->  
>
> Ab Version 1906 können Sie keine neuen Anwendungskatalogrollen installieren. Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910.  
  

### <a name="distribution-point"></a>Verteilungspunkt

Bevor Sie Anwendungen auf Clients bereitstellen können, benötigen Sie mindestens einen Verteilungspunkt in der Hierarchie. Standardmäßig wird auf dem Standortserver während einer Standardinstallation eine Verteilungspunkt-Standortrolle aktiviert. Anzahl und Standort von Verteilungspunkten richten sich nach den jeweiligen Anforderungen Ihrer Umgebung.

Weitere Informationen zum Installieren von Verteilungspunkten und Verwalten von Inhalt finden Sie unter [Verwalten von Inhalt und Inhaltsinfrastruktur](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  


### <a name="reporting-services-point"></a>Reporting Services-Punkt

Installieren und konfigurieren Sie einen Reporting Services-Punkt, um Configuration Manager-Berichte für die Anwendungsverwaltung zu verwenden.

Weitere Informationen finden Sie unter [Einführung in die Berichterstellung](../../core/servers/manage/introduction-to-reporting.md).  


### <a name="client-settings"></a>Clienteinstellungen

Viele Clienteinstellungen steuern, wie der Client auf dem Gerät Anwendungen installiert und wie die Benutzeroberfläche aussieht. Diese Clienteinstellungen umfassen die folgenden Gruppen:

- Computer-Agent  
- Computerneustart  
- Software Center  
- Softwarebereitstellung  
- Affinität zwischen Benutzer und Gerät  

Weitere Informationen finden Sie in den folgenden Artikeln:

- [Informationen zu Clienteinstellungen](../../core/clients/deploy/about-client-settings.md)  
- [Konfigurieren von Clienteinstellungen](../../core/clients/deploy/configure-client-settings.md)  


### <a name="security-permissions-for-application-management"></a>Sicherheitsberechtigungen für die Anwendungsverwaltung

- Die Sicherheitsrolle **Anwendungsautor** umfasst die erforderlichen Berechtigungen zum Erstellen, Ändern und Außerkraftsetzen von Anwendungen.  

- Die Sicherheitsrolle **Anwendungsbereitstellungs-Manager** enthält die erforderlichen Berechtigungen zum Bereitstellen von Anwendungen.  

- In der Sicherheitsrolle **Anwendungsadministrator** sind alle Berechtigungen der Sicherheitsrollen **Anwendungsautor** und **Anwendungsbereitstellungs-Manager** enthalten.  

Weitere Informationen finden Sie unter [Konfigurieren der rollenbasierten Verwaltung](../../core/servers/deploy/configure/configure-role-based-administration.md).  


### <a name="app-v-46-sp1-or-later-client-to-run-virtual-applications"></a>App-V 4.6 SP1-Client oder höher zum Ausführen von virtuellen Anwendungen

Wenn Sie virtuelle Anwendungen in Configuration Manager erstellen möchten, installieren Sie auf dem entsprechenden Gerät App-V 4.6 SP1 oder höher.

Aktualisieren Sie vor dem Bereitstellen virtueller Anwendungen auch den App-V-Client mit dem im [Microsoft-Supportartikel 2645225](https://support.microsoft.com/help/2645225) beschriebenen Hotfix.  


### <a name="application-catalog"></a>Anwendungskatalog

> [!Important]  
> Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910. Weitere Informationen finden Sie unter [Entfernen des Anwendungskatalogs](#bkmk_remove-appcat).  

#### <a name="application-catalog-web-service-point"></a>Anwendungskatalog-Webdienstpunkt

Der Anwendungskatalog-Webdienstpunkt ist eine Standortsystemrolle, die Informationen über verfügbare Software aus der Softwarebibliothek für die Anwendungskatalog-Website bereitstellt und auf die Benutzer zugreifen können.

Weitere Informationen zum Konfigurieren dieser Standortsystemrolle finden Sie unter [Installieren und Konfigurieren des Anwendungskatalogs](#bkmk_appcat).  

#### <a name="application-catalog-website-point"></a>Anwendungskatalog-Websitepunkt

Der Anwendungskatalog-Websitepunkt ist eine Standortsystemrolle, über die Benutzern eine Liste der verfügbaren Software bereitgestellt wird.

Weitere Informationen zum Konfigurieren dieser Standortsystemrolle finden Sie unter [Installieren und Konfigurieren des Anwendungskatalogs](#bkmk_appcat).

#### <a name="discovered-user-accounts-for-application-catalog"></a>Ermittelte Benutzerkonten für den Anwendungskatalog

Benutzerkonten müssen zunächst von Configuration Manager ermittelt werden, bevor Benutzer Anwendungen anzeigen und aus dem Anwendungskatalog anfordern können. Weitere Informationen finden Sie unter [Run discovery (Ausführen der Ermittlung)](../../core/servers/deploy/configure/run-discovery.md).  



## <a name="configure-software-center"></a><a name="bkmk_userex"></a> Konfigurieren des Softwarecenters  

Weitere Informationen zur Konfiguration und zum Branding des Softwarecenters finden Sie unter [Planen für Software Center](plan-for-software-center.md).


## <a name="remove-the-application-catalog"></a><a name="bkmk_remove-appcat"></a> Entfernen des Anwendungskatalogs

<!-- SCCMDocs-pr issue 3051 -->

Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910. Weitere Informationen finden Sie unter [Entfernte und veraltete Features](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md). In der folgende Liste sind die Änderungen zusammengefasst:

- Ab Version 1806 wird die **Silverlight-Benutzeroberfläche** für den Anwendungskatalog-Websitepunkt nicht mehr unterstützt.<!--1358309--> Die Rolle „Anwendungskatalog-Webdienstpunkt“wird *nicht mehr benötigt*, allerdings weiterhin *unterstützt*.

- Ab Version 1906 verwenden aktualisierte Clients automatisch den Verwaltungspunkt für Anwendungsbereitstellungen, die Benutzern zur Verfügung stehen. Zudem können Sie keine neuen Anwendungskatalogrollen installieren.

- Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910.  

Diese iterativen Verbesserungen an Software Center und Verwaltungspunkt zielen darauf ab, Ihre Infrastruktur zu vereinfachen und die Notwendigkeit des Anwendungskatalogs für Bereitstellungen zu erübrigen, die für Benutzer verfügbar sind. Software Center kann alle App-Bereitstellungen ohne den Anwendungskatalog übermitteln. Wenn Sie zudem TLS 1.2 aktivieren und HTTP mit dem Anwendungskatalog verwenden, können Benutzer keine benutzerbezogenen, verfügbaren Bereitstellungen sehen. Aktualisieren Sie Configuration Manager auf Version 1906 oder höher, um von diesen Verbesserungen zu profitieren.

1. Aktualisieren Sie alle Clients auf Version 1806 oder höher. Version 1906 wird empfohlen.  

1. Legen Sie das Branding für Software Center stattdessen in den Eigenschaften der Websiterolle „Anwendungskatalog“ fest. Weitere Informationen finden Sie unter [Softwarecenter-Clienteinstellungen](../../core/clients/deploy/about-client-settings.md#software-center).  

1. Überprüfen Sie die Standard- und alle benutzerdefinierten Clienteinstellungen. Vergewissern Sie sich in der Gruppe **Computer-Agent** das **Websitepunkt des Standardanwendungskatalogs** auf `(none)` festgelegt ist.  

    In Version 1902 und früheren Versionen wechselt der Client nur dann zur Verwendung des Verwaltungspunkts, wenn es in der Hierarchie keine Anwendungskatalogrollen gibt. Andernfalls verwenden Clients weiterhin eine der Anwendungskataloginstanzen in der Hierarchie. Dieses Verhalten gilt für separate primäre Standorte.  

1. Entfernen Sie die Standortsystemrollen **Anwendungskatalog-Website** und **Anwendungskatalog-Webdienst** aus allen primären Standorten.

Nachdem Sie die Anwendungskatalogrollen entfernt haben, beginnt Software Center, den Verwaltungspunkt für benutzerbezogene, verfügbare Bereitstellungen zu verwenden. Bis Version 1902 kann es bis zu 65 Minuten dauern, bis diese Änderung erfolgt. Um dieses Verhalten für einen bestimmten Client zu prüfen, überprüfen Sie `SCClient_<username>.log`, und suchen Sie nach einem Eintrag ähnlich der folgenden Zeile:

`Using endpoint Url: https://mp.contoso.com/CMUserService_WindowsAuth, Windows authentication`


## <a name="install-and-configure-the-application-catalog"></a><a name="bkmk_appcat"></a> Installieren und Konfigurieren des Anwendungskatalogs  

> [!Important]  
> Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910. Weitere Informationen finden Sie unter [Entfernen des Anwendungskatalogs](#bkmk_remove-appcat).  

### <a name="step-1-web-server-certificate-for-https"></a>Schritt 1: Webserverzertifikat für HTTPS

Wenn Sie HTTPS-Verbindungen verwenden, stellen Sie ein Webserverzertifikat auf den Standortsystemservern für den Anwendungskatalog-Websitepunkt und den Anwendungskatalog-Webdienstpunkt bereit.

Wenn Sie möchten, dass Clients den Anwendungskatalog im Internet verwenden, stellen Sie auf mindestens einem Verwaltungspunkt ein Webserverzertifikat bereit. Konfigurieren Sie es für Clientverbindungen aus dem Internet.

Weitere Informationen zu den Zertifikatanforderungen finden Sie unter [PKI-Zertifikatanforderungen für System Center Configuration Manager](../../core/plan-design/network/pki-certificate-requirements.md).  


### <a name="step-2-client-authentication-certificate-for-https"></a>Schritt 2: Clientauthentifizierungszertifikat für HTTPS

Wenn Sie ein PKI-Clientzertifikat für Verbindungen mit Verwaltungspunkten verwenden, stellen Sie ein Clientauthentifizierungszertifikat auf den Clientcomputern bereit. Obwohl Clients kein PKI-Clientzertifikat für die Verbindung mit dem Anwendungskatalog benötigen, müssen sie sich mit einem Verwaltungspunkt verbinden, bevor sie den Anwendungskatalog nutzen können.

Stellen Sie in den folgenden Situationen ein Clientauthentifizierungszertifikat auf Clientcomputern bereit:

- Von allen Verwaltungspunkten im Intranet werden nur HTTPS-Clientverbindungen akzeptiert.
- Die Verbindung von Clients mit dem Anwendungskatalog wird über das Internet hergestellt.

Weitere Informationen zu den Zertifikatanforderungen finden Sie unter [PKI-Zertifikatanforderungen für System Center Configuration Manager](../../core/plan-design/network/pki-certificate-requirements.md).  


### <a name="step-3-install-and-configure-the-application-catalog-roles"></a>Schritt 3: Installieren und Konfigurieren der Anwendungskatalogrollen

Installieren Sie die beiden Rollen „Anwendungskatalog-Webdienstpunkt“ und „Anwendungskatalog-Websitepunkt“ am gleichen Standort. Die Installation auf demselben Server oder in derselben Active Directory-Gesamtstruktur ist nicht erforderlich. Allerdings müssen sich der Anwendungskatalog-Webdienstpunkt und die Standortdatenbank in der gleichen Gesamtstruktur befinden.

Weitere Informationen zum Platzieren von Servern finden Sie unter [Planen der Standortsystemserver und Standortsystemrollen](../../core/plan-design/hierarchy/plan-for-site-system-servers-and-site-system-roles.md).

> [!NOTE]  
> Installieren Sie den Anwendungskatalog an einem primären Standort. Sie können ihn nicht an einem sekundären Standort oder am Standort der zentralen Verwaltung installieren.  

Installieren Sie den Anwendungskatalog auf einem neuen Standortsystemserver oder auf einem am Standort vorhandenen Server. Weitere Informationen zum allgemeinen Vorgehen finden Sie unter [Installieren von Standortsystemrollen](../../core/servers/deploy/configure/install-site-system-roles.md). Wählen Sie im Assistenten zum Hinzufügen einer Standortsystemrolle oder zum Erstellen eines Standortsystemservers die folgenden Rollen aus der Liste aus:  

- **Anwendungskatalog-Webdienstpunkt**  
- **Anwendungskatalog-Websitepunkt**  

> [!TIP]  
> Wenn Clientcomputer den Anwendungskatalog über das Internet verwenden sollen, geben Sie den Internet-FQDN (vollqualifizierten Domänennamen) an.  

#### <a name="verify-the-installation-of-these-site-system-roles"></a>Überprüfen der Installation dieser Standortsystemrollen  

- Statusmeldungen: Verwenden Sie die Komponenten **SMS_PORTALWEB_CONTROL_MANAGER** und **SMS_AWEBSVC_CONTROL_MANAGER**.  

    Zum Beispiel wird durch die Status-ID **1015** für **SMS_PORTALWEB_CONTROL_MANAGER** bestätigt, dass der Anwendungskatalog-Websitepunkt von Standortkomponenten-Manager erfolgreich installiert wurde.  

- Protokolldateien: Suchen Sie nach **SMSAWEBSVCSetup.log** und **SMSPORTALWEBSetup.log**.  

    Suchen Sie nach den Protokolldateien **awebsvcMSI.log** und **portlwebMSI.log**, um weitere Informationen zu erhalten.  


### <a name="step-4-configure-client-settings"></a>Schritt 4: Konfigurieren von Clienteinstellungen

Konfigurieren Sie die Clientstandardeinstellungen, wenn alle Benutzer über die gleichen Einstellungen verfügen sollen. Andernfalls können Sie auch benutzerdefinierte Clienteinstellungen für bestimmte Sammlungen konfigurieren.

Weitere Informationen finden Sie in den folgenden Artikeln:

- [Informationen zu Clienteinstellungen](../../core/clients/deploy/about-client-settings.md)  
    - Computer-Agent  
    - Computerneustart  
    - Software Center  
    - Softwarebereitstellung  
    - Affinität zwischen Benutzer und Gerät  
- [Konfigurieren von Clienteinstellungen](../../core/clients/deploy/configure-client-settings.md)  

Der Konfigurations-Manager-Client konfiguriert Geräte mit diesen Einstellungen beim nächsten Download der Clientrichtlinie. Informationen zum Auslösen des Richtlinienabrufs für einen einzelnen Client finden Sie unter [Verwalten von Clients](../../core/clients/manage/manage-clients.md).


### <a name="step-5-verify-that-the-application-catalog-is-operational"></a>Schritt 5: Überprüfen, ob der Anwendungskatalog betriebsbereit ist

Verwenden Sie die folgenden Verfahren, um zu überprüfen, ob der Anwendungskatalog betriebsbereit ist.

> [!NOTE]  
> Die Benutzeroberfläche des Anwendungskatalogs erfordert Microsoft Silverlight. Wenn Sie den Anwendungskatalog direkt in einem Browser verwenden, überprüfen Sie zunächst, ob Microsoft Silverlight auf dem Computer installiert ist.  

> [!TIP]  
> Fehlende Voraussetzungen sind einer der häufigsten Gründe dafür, dass der Anwendungskatalog nach der Installation nicht ordnungsgemäß funktioniert. Stellen Sie sicher, dass die Voraussetzungen für die Standortsystemrollen des Anwendungskatalogs erfüllt sind. Weitere Informationen finden Sie unter [Site and site system prerequisites for System Center Configuration Manager](../../core/plan-design/configs/site-and-site-system-prerequisites.md) (Standort- und Standortsystemanforderungen für System Center Configuration Manager).  

Geben Sie in einem Browser die Websiteadresse des Anwendungskatalogs ein. Achten Sie darauf, dass auf der Webseite die folgenden drei Registerkarten angezeigt werden: **Anwendungskatalog**, **Eigene Anwendungsanforderungen** und **Eigene Geräte**.  

Verwenden Sie die entsprechende Adresse für den Anwendungskatalog in der folgenden Liste, wobei `<server>` der Computername, Intranet-FQDN oder Internet-FQDN ist:  

- HTTPS-Clientverbindungen und Standardeinstellungen für die Standortsystemrolle: `https://<server>/CMApplicationCatalog`  

- HTTP-Clientverbindungen und Standardeinstellungen für die Standortsystemrolle: `http://<server>/CMApplicationCatalog`  

- HTTPS-Clientverbindungen und benutzerdefinierte Einstellungen für die Standortsystemrolle: `https://<server>:<port>/<web application name>`  

- HTTPS-Clientverbindungen und benutzerdefinierte Einstellungen für die Standortsystemrolle: `http://<server>:<port>/<web application name>`  

> [!NOTE]  
> Wenn Sie sich mit einem Domänenadministratorkonto auf dem Gerät angemeldet haben, zeigt der Konfigurations-Manager-Client keine Benachrichtigungen an. Dazu gehören auch Meldungen, die darauf hinweisen, dass neue Software verfügbar ist.  
