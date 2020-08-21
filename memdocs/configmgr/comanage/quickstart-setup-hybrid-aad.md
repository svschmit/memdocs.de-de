---
title: Einrichten von Hybrid-Azure AD
titleSuffix: Configuration Manager
description: Wenn Ihre Umgebung derzeit über in Domänen eingebundene Windows 10-Geräte verfügt, richten Sie Hybrid-Azure AD ein, bevor Sie die Co-Verwaltung aktivieren.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 27dd26d1-e99c-4431-b2f8-60406394b6db
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 405303b3988e8c853ba30e8fb6d620d782b0474e
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694898"
---
# <a name="set-up-hybrid-azure-ad-for-co-management"></a>Einrichten von Hybrid-Azure AD für die Co-Verwaltung

Wenn Sie Windows 10-Geräte in das lokale Active Directory eingebunden haben, binden Sie diese Geräte zunächst in Azure Active Directory (Azure AD) ein, bevor Sie die Co-Verwaltung in Configuration Manager aktivieren. Dieser Vorgang wird als Azure AD-Hybrideinbindung bezeichnet. 

Im folgenden Video erläutern und zeigen Senior Program Manager Sandeep Deo und Product Marketing Manager Adam Harbour die Konfiguration von Geräten in Azure AD:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Configuring-Devices-in-Azure-Active-Directory/player]

Der Vorgang der Azure AD-Hybrideinbindung registriert Ihre lokalen, domäneneingebundenen Geräte automatisch bei Azure AD. Weitere Informationen zu diesem Prozess finden Sie in den folgenden Artikeln:
- [Einführung in die Geräteverwaltung in Azure Active Directory](/azure/active-directory/device-management-introduction) 
- [Planen der Azure AD-Hybrideinbindung](/azure/active-directory/devices/hybrid-azuread-join-plan)

Die Azure AD-Hybrideinbindung ist eine der wichtigsten Grundlagen für Co-Verwaltung. Dieser Prozess kann für einige Kunden unter Umständen eine Herausforderung darstellen:
- Ihre Organisation verwendet eine Identitätslösung von einem Drittanbieter 
- Komplexität beim Einrichten von Active Directory-Verbunddiensten (AD FS)

Bei der Bewältigung dieser Herausforderungen kann eine gewisse Orientierungshilfe erforderlich sein. Dieser Artikel hilft dabei, Verzögerungen zu vermeiden.


## <a name="how-to-do-it"></a>Vorgehensweise

Geräte sind ähnlich wie Benutzer, wenn Sie eine Identität erstellen, die Sie schützen möchten. Um die Identität eines Geräts zu jeder Zeit und an jedem Ort zu schützen, müssen Sie die Identität dieses Geräts in Azure AD einbinden.

Je nachdem, welche Art von Domäne Sie verwenden, gibt es zwei grundlegende Möglichkeiten, dies zu erreichen. Konfigurieren Sie die Azure AD-Hybrideinbindung für einen der folgenden Domänentypen:  
- [Verbunddomänen](/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  
- [Verwaltete Domänen](/azure/active-directory/devices/hybrid-azuread-join-managed-domains)  

Die beiden oben genannten Methoden bieten die bestmögliche Erfahrung. Detaillierte Informationen, einschließlich des vollständigen manuellen Vorgangs, finden Sie in den folgenden Artikeln:
- [Manuelles Konfigurieren von Geräten mit Azure AD-Hybrideinbindung](/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)  
- [AD FS-Pass-Through-Authentifizierung für Hybrid-Azure AD](/windows-server/identity/ad-fs/ad-fs-overview), einschließlich Azure AD-Ermittlung  

Anleitungen zur Problembehandlung finden Sie im [Problembehandlungsleitfaden zur Windows 10 Azure AD-Hybrideinbindung](/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).



## <a name="case-study"></a>Fallstudie

Ein großes europäisches Softwareunternehmen mit über 100.000 Benutzern in seinem Netzwerk verfolgte einen genauen und stufenweisen Ansatz, um eine Azure AD-Hybrideinbindung zu ermöglichen.

Da die Azure AD-Hybrideinbindung ein Schlüsselelement zur Unterstützung von Co-Verwaltung ist, arbeiteten die Configuration Manager-Administratoren in der Planungsphase mit dem Identitätsteam zusammen. Dieses Softwareunternehmen verfügte über zahlreiche ADFS-Regeln, von denen einige komplex waren. Um dieser Herausforderung zu begegnen, überprüfte das Identitätsteam die vorhandenen ADFS-Regeln, bevor es die Azure AD-Hybrideinbindung aktivierte. Das IT-Team entschied sich auch für ein Upgrade von Azure AD Connect auf die neueste Version. Azure AD Connect bietet jetzt einen automatisierten Prozessablauf für die Aktivierung der Azure AD-Hybrideinbindung.

Nach erfolgreicher Bereitstellung und Testphase in der Vorproduktionsumgebung aktivierte dieser Kunde die Azure AD-Hybrideinbindung für den gesamten Produktionsbereich. Innerhalb von einer Woche wurde für jedes Windows 10-Gerät Co-Verwaltung eingeführt.



## <a name="contact-fasttrack"></a>Kontaktaufnahme mit FastTrack

Wenn Sie Unterstützung bei der Einrichtung von Azure AD zu irgendeinem Zeitpunkt des Vorgangs benötigen, navigieren Sie zu [Microsoft FastTrack](https://Microsoft.com/FastTrack/), melden Sie sich an, und fordern Sie Unterstützung an. 

Weitere Informationen finden Sie unter [Abrufen von Hilfe aus FastTrack](quickstart-fasttrack.md).