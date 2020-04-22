---
title: Verwenden von Azure AD für die Co-Verwaltung
titleSuffix: Configuration Manager
description: Mit Azure AD können Sie die Vorteile von verbesserter Produktivität für Ihre Benutzer und von Sicherheit für Ihre Ressourcen nutzen, und zwar sowohl in Cloud- als auch in lokalen Umgebungen.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 2af37410-d04c-4059-801c-9edb8bf72d89
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a84247482ddece88208e83fec545afc5e953a070
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691288"
---
# <a name="use-azure-ad-for-co-management"></a>Verwenden von Azure AD für die Co-Verwaltung

In der Cloud ist Identität die neue Steuerungsebene. Azure Active Directory (Azure AD) ermöglicht es Ihnen, Ihre Benutzer, Geräte und Anwendungen sowohl in Cloud- als auch in lokalen Umgebungen zu verbinden. Die Registrierung Ihrer Geräte bei Azure AD ermöglicht es Ihnen, die Produktivität Ihrer Benutzer und die Sicherheit Ihrer Ressourcen zu verbessern. Der Einsatz von Geräten in Azure AD ist die Grundlage für die Co-Verwaltung und den gerätebasierten bedingten Zugriff.

Weitere Informationen zum gerätebasierten bedingten Zugriff finden Sie unter [Vorgehensweise: Erfordern verwalteter Geräte für den Cloud-App-Zugriff mit bedingtem Zugriff](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices).

Im folgenden Video erläutern und zeigen Senior Program Manager Sandeep Deo und Product Marketing Manager Adam Harbour Azure AD für Co-Verwaltung:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Embedding-Co-management-With-Azure-Active-Directory/player]

Azure AD bietet zwei Optionen für firmeneigene Geräte, die den Anforderungen Ihres Unternehmens entsprechen:  

- **In Azure AD eingebundenes Gerät**: Binden Sie Ihre Windows 10-Geräte in Azure AD ein, ohne dass Sie sie in Ihr lokales Active Directory einbinden müssen.  

  - Unterstützt Windows 10

  - Einrichtung ohne zusätzliche Konfiguration für Ihre lokalen Umgebungen.  

  - Durch Aktivieren einiger Einstellungen in Azure AD können Sie Ihren Benutzern ermöglichen, Geräte über die Windows-Setupbenutzeroberfläche (OOBE) in Azure AD einzubinden.  

  - Weitere Informationen finden Sie unter [Gewusst wie: Planen der Implementierung der Azure AD-Einbindung](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan).  

- **In Hybrid-Azure AD eingebundenes Gerät**: Einbinden vorhandener, in die Domäne eingebundener Geräte in Azure AD  

  - Unterstützt Windows 10, Windows 8.1 und Windows 7

  - Einrichtung mithilfe von AD FS-Ansprüchen oder Azure AD Connect  

  - Für Windows 10 erfolgt die Einbindung im Computerkontext, sodass Benutzer keine zusätzliche Schritte ausführen müssen.  

  - Weitere Informationen finden Sie unter [Planen der Azure Active Directory-Hybrideinbindung](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan).  

Beide Optionen bieten eine ähnliche Funktionalität für Benutzer. Dies ist eine flexible Möglichkeit, sich für eine der beiden Varianten nach Ihren Bedürfnissen zu entscheiden. So können Sie beispielsweise [auf Ihre lokalen Ressourcen](https://docs.microsoft.com/azure/active-directory/devices/azuread-join-sso) über in Azure AD eingebundene Computer zugreifen, obwohl diese nicht in Active Directory eingebunden sind.

Sie können Geräte in Azure AD in verschiedenen Umgebungen unabhängig von Ihrer [Authentifizierungsmethode](https://docs.microsoft.com/azure/active-directory/hybrid/choose-ad-authn) einbinden. Beispielsweise Verbundauthentifizierung oder Cloudauthentifizierung.

Wenn Sie bereits über ein lokales Active Directory verfügen, ist die Einrichtung für beide Optionen einfach.

## <a name="benefits"></a>Vorteile

Das Einbinden von Geräten in Azure AD bietet die folgenden Vorteile für Ihre Organisation:

### <a name="single-sign-on-to-cloud-resources"></a>Einmaliges Anmelden bei Cloudressourcen

Auf Geräten, die in Azure AD eingebunden sind, können Sie eine integrierte Umgebung für den Zugriff auf beliebige Cloud- oder lokale Ressourcen nutzen. Sobald Sie sich bei einem Windows-Computer anmelden, der in Azure AD eingebunden ist, können Sie sich ohne zusätzliche Anmeldeaufforderungen einmalig bei allen Anwendungen anmelden.  

### <a name="windows-hello-for-business"></a>Windows Hello for Business

Windows Hello for Business bietet sichere kennwortlose Authentifizierung für Windows 10. Indem Sie Ihre Geräte in Azure AD einbinden, können Sie Windows Hello for Business in Ihrer gesamten Benutzerbasis für Cloud- und lokale Ressourcen aktivieren. Windows Hello for Business verhindert, dass Benutzer sich komplexe Kennwörter merken müssen oder diese versehentlich offenlegen. Der Anmeldeprozess ist einfach und sicher.

Weitere Informationen finden Sie unter [Windows Hello for Business](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification).  

### <a name="device-based-conditional-access"></a>Gerätebasierter bedingter Zugriff

Aktivieren Sie bedingten Zugriff basierend auf dem Gerätestatus, um die Daten Ihrer Organisation besser zu schützen. Für gerätebasierten bedingten Zugriff ist ein verwaltetes Gerät erforderlich. Dieses Gerät muss ein konformes Gerät oder ein in Azure AD eingebundenes Hybridgerät sein. Für in Azure AD eingebundene Geräte muss Intune das jeweilige Gerät als konform kennzeichnen. Bei in Azure AD eingebundenen Hybridgeräten wird jedoch der Gerätezustand selbst verwendet, um bedingten Zugriff auszuwerten. Co-Verwaltung bietet Ihnen den zusätzlichen Vorteil, dass Sie die Compliance für in Azure AD eingebundene Hybridgeräte über Intune auswerten können. Dieses Feature stellt sicher, dass die Gerätekonfiguration intakt ist.

Weitere Informationen zum gerätebasierten bedingten Zugriff finden Sie unter [Vorgehensweise: Erfordern verwalteter Geräte für den Cloud-App-Zugriff mit bedingtem Zugriff](https://docs.microsoft.com/azure/active-directory/conditional-access/require-managed-devices).  

### <a name="automatic-device-licensing"></a>Automatische Gerätelizenzierung.

Alle Windows 10-Geräte, die in Azure AD eingebunden werden, durchlaufen Lizenzüberprüfungen. Diese Überprüfungen ermöglichen ein automatisches Upgrade dieser Geräte von Pro auf Enterprise über die Microsoft-Cloud. Wenn Sie das entsprechende Abonnement des Benutzers entfernen, stuft das Gerät seine Lizenz automatisch herunter. Diese Funktion bietet eine einzige Kontrollebene für die Verwaltung von Windows-Lizenzen ohne komplizierte Prozesse oder lokale Systeme.

### <a name="self-service-functionality"></a>Self-Service-Funktionen

Die Self-Service-Funktionen umfassen die Self-Service-Kennwortzurücksetzung und einen BitLocker-Wiederherstellungsschlüssel. Azure AD bietet Ihnen außerdem direkte Optionen zum Zurücksetzen Ihres Kennworts oder für den Zugriff auf BitLocker-Wiederherstellungsschlüssel. Sie können Azure AD verwenden, um Ihr Kennwort direkt über den Windows-Sperrbildschirm und nicht über einen Webbrowser zurückzusetzen. Diese Funktionen verringern Reibungsverluste für Benutzer und helfen, die Helpdeskkosten für Ihre Organisation zu senken.  

Weitere Informationen finden Sie unter [Tutorial: Ermöglichen der Kontoentsperrung oder Kennwortzurücksetzung für Benutzer mit der Self-Service-Kennwortzurücksetzung von Azure Active Directory](https://docs.microsoft.com/azure/active-directory/authentication/tutorial-enable-sspr).

### <a name="enterprise-state-roaming"></a>Enterprise State Roaming

Alle Geräte, die in Azure AD eingebunden sind, können ihre Einstellungen in der Cloud synchronisieren. Jedes Gerät, bei dem sich ein Benutzer anmeldet, synchronisiert alle seine Einstellungen, um eine produktivere Erfahrung zu ermöglichen.  

## <a name="value-proposition"></a>Leistungsversprechen

Das Einbinden Ihrer Geräte in Azure AD mit einem dieser Verfahren beschleunigt Ihre digitale Transformation. Dadurch werden weitere Funktionen aktiviert, die von Microsoft 365 bereitgestellt werden. Sie erhalten eine bessere Benutzererfahrung und verfügen über größere Sicherheit für Ihre Daten.

Azure AD bietet mehrere Optionen, um Ihre Workload zu erleichtern:

- Verwalten Sie alle Geräteidentitäten in Ihrer Organisation an einem zentralen Ort.  

- Senken Sie die Helpdeskkosten durch Aktivieren von Self-Service-Kennwortzurücksetzung. Dann können Benutzer Ihr Kennwort über den Windows 10-Sperrbildschirm auf dem Gerät jederzeit zurücksetzen.  

## <a name="configure"></a>Konfigurieren

Wenn Sie bereits über eine lokale Active Directory-Umgebung verfügen und Ihre in Domänen eingebundenen Geräte in Azure AD einbinden möchten, konfigurieren Sie in Azure AD eingebundene Hybridgeräte. Weitere Informationen finden Sie unter [Vorgehensweise: Planen der Implementierung Ihrer Azure Active Directory-Hybrideinbindung](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan).

Configuration Manager verfügt über eine Clienteinstellung zum [Automatischen Registrieren neuer, in eine Domäne eingebundener Windows 10-Geräte bei Azure AD](../core/clients/deploy/about-client-settings.md#automatically-register-new-windows-10-domain-joined-devices-with-azure-active-directory). Weitere Informationen zum Konfigurieren dieser Clienteinstellungen finden Sie unter [Konfigurieren von Clienteinstellungen](../core/clients/deploy/configure-client-settings.md).

Wenn Sie die Azure AD-Einbindung für Ihre Geräte konfigurieren möchten, ohne sie auch in Ihre lokale Domäne einzubinden, lesen Sie die Überlegungen zur Azure AD-Einbindung in Ihrer Umgebung. Nachdem Sie sich für die Azure AD-Einbindung entschieden haben, stehen Ihnen viele Optionen für die Bereitstellung basierend auf den Anforderungen Ihrer Organisation zur Verfügung. Weitere Informationen finden Sie in den folgenden Artikeln:

- [How to: Planen der Implementierung der Azure AD-Einbindung](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan).  
- [Grundlegendes zu Ihren Bereitstellungsoptionen](https://docs.microsoft.com/azure/active-directory/devices/azureadjoin-plan#understand-your-provisioning-options)  
