---
title: Installieren von Clients mit Azure AD
titleSuffix: Configuration Manager
description: Installieren und Zuweisen von Configuration Manager-Clients auf Windows 10-Geräten mithilfe von Azure Active Directory zur Authentifizierung
ms.date: 03/20/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9a55440e7ba61ec62d9f0c91c0a23b98bab5884c
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694108"
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>Installieren und Zuweisen von Configuration Manager-Windows 10-Clients über das Internet mit Authentifizierung über Azure AD

Wenn Sie Configuration Manager-Clients auf Windows 10-Geräten mit Azure AD zur Authentifizierung installieren möchten, müssen Sie Configuration Manager in Azure Active Directory (Azure AD) integrieren. Clients können im Intranet direkt mit einem HTTPS-fähigen Verwaltungspunkt oder einem beliebigen Verwaltungspunkt kommunizieren, an dem die Nutzung von erweitertem HTTP möglich ist. Des Weiteren können sie auch internetbasiert sein und über das CMG (cloud management gateway, Cloudverwaltungsgateway) oder mit einem internetbasierten Verwaltungspunkt kommunizieren. Für diesen Prozess wird Azure AD zur Authentifizierung von Clients bei dem Configuration Manager-Standort verwendet. Dadurch müssen Sie keine Clientauthentifizierungszertifikate mehr konfigurieren.

Die Einrichtung von Azure AD kann für einige Kunden einfacher sein als die Einrichtung einer Public Key-Infrastruktur für zertifikatsbasierte Authentifizierung. Es gibt Funktionen, für die Sie die Website bei Azure AD integrieren müssen, aber es nicht unbedingt notwendig ist, dass die Clients mit Azure AD verbunden sind.<!-- SCCMDocs issue 1259 --> Weitere Informationen finden Sie in den folgenden Artikeln:

- [Erstellen von Plänen für Azure Active Directory](../../plan-design/security/plan-for-security.md#bkmk_planazuread)
- [Verwenden von Azure AD für die Co-Verwaltung](../../../comanage/quickstart-hybrid-aad.md)

## <a name="before-you-begin"></a>Vorbereitung

- Voraussetzung ist ein Azure AD-Mandant.  

- Geräteanforderungen:  

  - Windows 10  

  - Einbindung in Azure AD (einfache Einbindung in Clouddomäne oder Einbindung in Hybrid-Azure AD)  

- Benutzeranforderungen:  

  - Der angemeldete Benutzer muss eine Azure AD-Identität sein.

  - Wenn der Benutzer eine Verbundsidentität oder synchronisierte Identität ist, müssen Sie in Configuration Manager die [Active Directory-Benutzerermittlung](../../servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser) und die [Azure AD-Benutzerermittlung](../../servers/deploy/configure/about-discovery-methods.md#azureaddisc) verwenden. Weitere Informationen zu Hybrididentitäten finden Sie unter [Definieren einer Strategie zur Hybrididentitätsübernahme](https://docs.microsoft.com/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->  

- Zusätzlich zu den [erforderlichen Komponenten](../../plan-design/configs/site-and-site-system-prerequisites.md#bkmk_2012MPpreq) für die Standortsystemrolle des Verwaltungspunkts müssen Sie auch **ASP.NET 4.5** auf diesem Server installieren. Bei der Aktivierung von ASP.NET 4.5 werden weitere Optionen automatisch ausgewählt, die Sie ebenfalls verwenden müssen.  

- Bestimmen Sie, ob Ihr Verwaltungspunkt HTTPS erfordert. Weitere Informationen finden Sie unter [Verwaltungspunkt für HTTPS aktivieren](../manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

- Richten Sie optional ein [CMG](../manage/cmg/plan-cloud-management-gateway.md) ein, um internetbasierte Clients bereitzustellen. Für lokale Clients, die sich bei Azure AD authentifizieren, ist kein CMG erforderlich.  

> [!TIP]
> Ab Version 2002 gilt Folgendes:<!--5686290--> Configuration Manager weitet seine Unterstützung auf internetbasierte Geräte aus, die nur selten eine Verbindung mit dem internen Netzwerk herstellen, die mit Azure Active Directory (Azure AD) nicht verknüpft werden können und die über keine Methode zum Installieren eines von der PKI ausgestellten Zertifikats verfügen. Weitere Informationen finden Sie unter [Tokenbasierte Authentifizierung für CMG](deploy-clients-cmg-token.md).

## <a name="configure-azure-services-for-cloud-management"></a>Konfigurieren von Azure-Diensten für die Cloudverwaltung

Verbinden Sie zuerst Ihren Configuration Manager-Standort mit Azure AD. Weiter Informationen hierzu finden Sie unter [Konfigurieren von Azure-Diensten](../../servers/deploy/configure/azure-services-wizard.md). Stellen Sie eine Verbindung mit dem **Cloudverwaltungsdienst** her.

Aktivieren Sie die [Azure AD-Benutzerermittlung](../../servers/deploy/configure/configure-discovery-methods.md#azureaadisc) während des Onboardings für die **Cloudverwaltung**.

Nachdem Sie diese Aktionen ausgeführt haben, wird Ihr Configuration Manager-Standort mit Azure AD verbunden.

## <a name="configure-client-settings"></a>Konfigurieren von Clienteinstellungen

Die folgenden Clienteinstellungen unterstützen das Einbinden von Windows 10-Geräten in Azure AD. Außerdem können damit internetbasierte Clients das CMG und den Cloudverteilungspunkt verwenden.

1. Konfigurieren Sie die folgenden Clienteinstellungen im Abschnitt **Clouddienste** anhand der Informationen in [Konfigurieren von Clienteinstellungen](configure-client-settings.md).  

    - **Zugriff auf Cloudverteilungspunkt zulassen**: Aktivieren Sie diese Einstellung, um internetbasierte Geräte beim Abrufen des zur Installation des Konfigurations-Manager-Clients erforderlichen Inhalts zu unterstützen. Wenn am Cloudverteilungspunkt der Inhalt nicht verfügbar ist, können Geräte diesen über das CMG abrufen. Der Bootstrap für die Clientinstallation sendet vier Stunden lang wiederholt Anforderungen an den Cloudverteilungspunkt, bevor das CMG als Ausweichlösung verwendet wird.<!--495533-->  

    - **Automatische Registrierung neuer, in die Domäne eingebundener Windows 10-Geräte bei Azure Active Directory**: Legen Sie diese Option auf **Ja** oder **Nein** fest. Der Standardwert für diese Einstellung ist **Ja**. Dieses Verhalten ist auch die Standardeinstellung in Version 1709 von Windows 10.

    - **Ermöglichen Sie Clients die Verwendung eines Cloudverwaltungsgateways**: Legen Sie **Ja** (Standardeinstellung) oder **Nein** fest.  

2. Stellen Sie die Clienteinstellungen in der gewünschten Sammlung von Geräten bereit. Stellen Sie diese Einstellungen nicht für Benutzersammlungen bereit.

Um zu bestätigen, dass das Gerät in Azure AD eingebunden wurde, müssen Sie `dsregcmd.exe /status` mit der Eingabeaufforderung ausführen. Im Feld **AzureAdjoined** wird in den Ergebnissen **JA** angezeigt, wenn das Gerät in Azure AD eingebunden ist.

## <a name="install-and-register-the-client-using-azure-ad-identity"></a>Installieren und Registrieren des Clients mithilfe einer Azure AD-Identität

Wenn Sie den Client mithilfe einer Azure AD-Identität manuell installieren möchten, ist es zuerst erforderlich, dass Sie sich mit der allgemeinen Vorgehensweise unter [Manuelles Installieren von Clients](deploy-clients-to-windows-computers.md#BKMK_Manual) vertraut machen.

 > [!Note]  
 > Das Gerät benötigt zwar Zugriff auf das Internet, um Azure AD kontaktieren zu können, muss aber nicht internetbasiert sein.

Im folgenden Beispiel wird die allgemeine Syntax für den Befehl demonstriert, der mit der Befehlszeile ausgeführt wird: `ccmsetup.exe /mp:<source management point> CCMHOSTNAME=<internet-based management point> SMSSiteCode=<site code> SMSMP=<initial management point> AADTENANTID=<Azure AD tenant identifier> AADCLIENTAPPID=<Azure AD client app identifier> AADRESOURCEURI=<Azure AD server app identifier>`

Weitere Informationen finden Sie unter [Informationen zu Clientinstallationseigenschaften](about-client-installation-properties.md).

Der Parameter **/mp** und die Eigenschaft **CCMHOSTNAME** legen je nach Szenario Folgendes fest:

- Lokaler Verwaltungspunkt: Geben Sie nur den Parameter **/mp** an. Die Eigenschaft **CCMHOSTNAME** ist nicht erforderlich.
- Cloudverwaltungsgateway
- Internetbasierter Verwaltungspunkt

Die Eigenschaft **SMSMP** legt entweder den lokalen oder internetbasierten Verwaltungspunkt fest.

Im folgenden Beispiel wird ein Cloudverwaltungsgateway verwendet. Darin werden die Beispielwerte ersetzt: `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com AADTENANTID=daf4a1c2-3a0c-401b-966f-0b855d3abd1a AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver`

Auf der Website werden zusätzliche Azure AD-Informationen für Cloud Management Gateway (CMG) veröffentlicht. Ein in Azure AD eingebundener Client ruft diese Informationen beim ccmsetup-Prozess von Cloud Management Gateway ab und verwendet dabei den gleichen Mandanten, mit dem er verknüpft ist. Dieses Verhalten vereinfacht die Installation des Clients in einer Umgebung mit mehreren Azure AD-Mandanten. Die einzigen beiden erforderlichen ccmsetup-Eigenschaften sind **CCMHOSTNAME** und **SMSSiteCode**.<!--3607731-->

Wenn Sie die Clientinstallation mithilfe einer Azure AD-Identität über Microsoft Intune automatisieren möchten, finden Sie unter [Vorbereiten internetbasierter Geräte für die Co-Verwaltung](../../../comanage/how-to-prepare-Win10.md#install-the-configuration-manager-client) weitere Informationen.

## <a name="next-steps"></a>Nächste Schritte

Lesen Sie nach dem Abschluss dieser Schritte den Artikel [Überwachen von Clients in System Center Configuration Manager](../manage/monitor-clients.md).
