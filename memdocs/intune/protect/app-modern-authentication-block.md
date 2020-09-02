---
title: Blockieren von Apps ohne moderne Authentifizierung in Intune
titleSuffix: Microsoft Intune
description: Erfahren Sie mehr über Apps und moderne Authentifizierung (ADAL) mit Microsoft Intune.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/22/2020
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.topic: conceptual
ms.technology: ''
ms.assetid: 73db3070-d033-40fb-a8f1-58b9d198021e
ms.reviewer: chrisgre
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure, has-adal-ref
ms.collection: M365-identity-device-management
ms.openlocfilehash: 4703288faac219b40fae08c6551425d6f0d5e4f3
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909413"
---
# <a name="block-apps-that-dont-use-modern-authentication-adal"></a>Blockieren von Apps, die keine moderne Authentifizierung verwenden (ADAL)

> [!NOTE]
> Azure Active Directory (Azure AD), Active Directory-Authentifizierungsbibliothek (ADAL) und die Azure AD Graph-API werden als veraltet gekennzeichnet. Weitere Informationen finden Sie unter [Updaten Ihrer Anwendung zur Verwendung von Microsoft-Authentifizierungsbibliothek (MSAL) und Microsoft Graph-API](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363).

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Der App-basierte bedingte Zugriff mit App-Schutzrichtlinien hängt von Anwendungen ab, die die [moderne Authentifizierung](https://support.office.com/article/Using-Office-365-modern-authentication-with-Office-clients-776c0036-66fd-41cb-8928-5495c0f9168a) nutzen, bei der es sich um eine Implementierung von OAuth2 handelt. Die meisten aktuellen mobilen und desktopbasierten Office-Anwendungen nutzen die moderne Authentifizierung. Es gibt jedoch Apps von Drittanbietern oder ältere Office-Apps, die andere Authentifizierungsmethoden wie die Standardauthentifizierung und die formularbasierte Authentifizierung nutzen.

## <a name="block-access-to-apps"></a>Blockieren des App-Zugriffs

Verwenden Sie zum Blockieren des Zugriffs auf Apps, die keine moderne Authentifizierung verwenden, die App-Schutzrichtlinien von Intune, um den bedingten Zugriff zu implementieren. Weitere Informationen finden Sie unter [App-basierter bedingter Zugriff mit Intune](app-based-conditional-access-intune.md).

## <a name="additional-information"></a>Zusätzliche Informationen

Weitere Informationen zum bedingten Zugriff in Azure AD finden Sie in den folgenden Artikeln:
- [Was ist der bedingte Zugriff in Azure Active Directory?](/azure/active-directory/conditional-access/overview)
- [Funktionsweise des App-basierten bedingten Zugriffs](app-based-conditional-access-intune.md#how-app-based-conditional-access-works)
- [Einrichten von SharePoint Online und Exchange Online für bedingten Zugriff mit Azure Active Directory](/azure/active-directory/conditional-access/conditional-access-for-exo-and-spo)

## <a name="next-steps"></a>Nächste Schritte

- [App-basierter bedingter Zugriff mit Intune](app-based-conditional-access-intune.md)