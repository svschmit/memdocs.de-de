---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.date: 06/29/2020
ms.openlocfilehash: 26bfbe7b7cabef8c8dee56077b924b69c4c5886a
ms.sourcegitcommit: f3f2632df123cccd0e36b2eacaf096a447022b9d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/01/2020
ms.locfileid: "85590530"
---
### <a name="azure-ad-authentication-doesnt-work"></a><a name="ki_auth"></a> Azure AD-Authentifizierung funktioniert nicht
<!--7569264-->
Configuration Manager kann den Sicherheitstokendienst von Azure Active Directory (Azure AD) nicht verwenden. Die Datei **CCM_STS.log** auf dem Verwaltungspunkt enthält einen Eintrag, der folgendem Fehler ähnelt: `ProcessRequest - Exception: System.IO.FileLoadException: Could not load file or assembly 'System.IdentityModel.Tokens.JWT.` Er enthält zudem den Fehlercode HRESULT 0x80131040.

Zudem treten Probleme mit einem Cloudverwaltungsgateway (Cloud Management Gateway, CMG) auf. Wenn die CMG-Verbindungsanalyse ausgeführt wird, tritt beim Testen des CMG-Kanals für den Verwaltungspunkt folgender Fehler auf: `Failed to get ConfigMgr token with Azure AD token. Status code is '500' and status description is 'CMGConnector_InternalServerError'.`

Dieses Problem wird durch eine Versionsabweichung mit einer unterstützenden Bibliothek verursacht.

Kopieren Sie **System.IdentityModel.Tokens.JWT.dll** aus dem Ordner \bin\x64 des Installationsverzeichnisses auf dem Standortserver in den Ordner SMS_CCM\CCM_STS\bin auf dem Verwaltungspunkt.
