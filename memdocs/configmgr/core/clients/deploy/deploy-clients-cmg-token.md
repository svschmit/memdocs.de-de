---
title: Tokenbasierte Authentifizierung für CMG
titleSuffix: Configuration Manager
description: Registrieren Sie einen Client im internen Netzwerk für ein eindeutiges Token, oder erstellen Sie ein Token für die Massenregistrierung internetbasierter Geräte.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: f0703475-85a4-450d-a4e8-7a18a01e2c47
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: ae92fa2f8e3ee3270de4777fd889bc5fc16a6de4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694138"
---
# <a name="token-based-authentication-for-cloud-management-gateway"></a>Tokenbasierte Authentifizierung für Cloud Management Gateway

*Gilt für: Configuration Manager (Current Branch)*

<!--5686290-->

Cloud Management Gateway (CMG) unterstützt zwar viele Clienttypen, aber auch mit [Erweitertem HTTP](../../plan-design/hierarchy/enhanced-http.md) erfordern diese Clients ein [Clientauthentifizierungszertifikat](../manage/cmg/certificates-for-cloud-management-gateway.md#for-internet-based-clients-communicating-with-the-cloud-management-gateway). Diese Zertifikatanforderung kann beim Bereitstellen auf internetbasierten Clients Probleme bereiten, die nicht häufig eine Verbindung mit dem internen Netzwerk herstellen, mit Azure Active Directory (Azure AD) verknüpft werden können und über keine Methode zum Installieren eines von der PKI ausgestellten Zertifikats verfügen.

Ab Version 2002 erweitert Configuration Manager die Geräteunterstützung um die folgenden Methoden:

- Registrieren im internen Netzwerk für ein eindeutiges Token

- Erstellen eines Tokens für die Massenregistrierung von internetbasierten Geräten

Wenn Sie dieses Feature nach der Aktualisierung des Standorts voll nutzen möchten, müssen Sie auch Clients auf die neueste Version aktualisieren. Das gesamte Szenario funktioniert erst, wenn auch die Clientversion aktuell ist. Stellen Sie ggf. sicher, dass Sie [die neue Clientversion zur Produktion heraufstufen](../manage/upgrade/test-client-upgrades.md#to-promote-the-new-client-to-production).

Der Configuration Manager-Client verwaltet dieses Token zusammen mit dem Verwaltungspunkt, daher besteht keine Abhängigkeit von der Betriebssystemversion. Dieses Feature ist für alle [unterstützten Versionen von Clientbetriebssystemen](../../plan-design/configs/supported-operating-systems-for-clients-and-devices.md) verfügbar.

> [!NOTE]
> Diese Methoden unterstützen nur geräteorientierte Verwaltungsszenarios.
>
> Microsoft empfiehlt, Geräte zu Azure AD hinzuzufügen. Internetbasierte Geräte können Azure AD verwenden, um sich mit Configuration Manager zu authentifizieren. Außerdem werden sowohl Geräte- als auch Benutzerszenarios ermöglicht, unabhängig davon, ob das Gerät mit dem Internet oder dem internen Netzwerk verbunden ist. Weitere Informationen finden Sie unter [Installieren und Registrieren des Clients mithilfe einer Azure AD-Identität](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity).

## <a name="register-on-the-internal-network"></a>Registrieren im internen Netzwerk

Diese Methode erfordert, dass der Client zuerst beim Verwaltungspunkt im internen Netzwerk registriert wird. Die Clientregistrierung erfolgt in der Regel direkt nach der Installation. Der Verwaltungspunkt gibt dem Client ein eindeutiges Token, das anzeigt, dass es ein selbst signiertes Zertifikat verwendet. Wenn der Client mit dem Internet verbunden ist, wird für die Kommunikation mit dem CMG das selbst signierte Zertifikat mit dem vom Verwaltungspunkt ausgestellten Token verknüpft. Der Client erneuert das Token einmal im Monat und ist 90 Tage gültig.

Dieses Verhalten wird von der Website standardmäßig aktiviert.

## <a name="create-a-bulk-registration-token"></a>Erstellen eines Massenregistrierungstokens

Wenn Sie Clients im internen Netzwerk nicht installieren und registrieren können, erstellen Sie jetzt ein Token für die Massenregistrierung. Verwenden Sie dieses Token, wenn der Client auf einem internetbasierten Gerät installiert und über das CMG registriert wird. Das Token für die Massenregistrierung hat eine kurze Gültigkeitsdauer und ist nicht auf dem Client oder der Website gespeichert. Es ermöglicht es dem Client, ein eindeutiges Token zu generieren, das mit dem selbst signierten Zertifikat gekoppelt ist, damit es sich beim CMG authentifizieren kann.

1. Melden Sie sich am Standortserver der obersten Ebene in der Hierarchie mit lokalen Administratorrechten an.

1. Öffnen Sie eine Eingabeaufforderung als Administrator.

1. Führen Sie das Tool aus dem Ordner `\bin\X64` des Configuration Manager-Installationsverzeichnisses auf dem Standortserver aus: `BulkRegistrationTokenTool.exe`. Erstellen Sie ein neues Token mit dem Parameter `/new`. Beispiel: `BulkRegistrationTokenTool.exe /new`. Weitere Informationen finden Sie unter [Nutzung des Massenregistrierungstokens](#bulk-registration-token-tool-usage).

1. Kopieren Sie das Token, und speichern Sie es an einem sicheren Ort.

1. Installieren Sie den Konfigurations-Manager-Client auf einem internetbasierten Gerät. Fügen Sie den Clientinstallationsparameter [ **/regtoken**](about-client-installation-properties.md#regtoken) ein. Die folgende Beispielbefehlszeile enthält die anderen erforderlichen Setupparameter und -eigenschaften:

    `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com /regtoken:eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik9Tbzh2Tmd5VldRUjlDYVh5T2lacHFlMDlXNCJ9.eyJTQ0NNVG9rZW5DYXRlZ29yeSI6IlN7Q01QcmVBdXRoVG9rZW4iLCJBdXRob3JpdHkiOiJTQ0NNIiwiTGljZW5zZSI6IlNDQ00iLCJUeXBlIjoiQnVsa1JlZ2lzdHJhdGlvbiIsIlRlbmFudElkIjoiQ0RDQzVFOTEtMEFERi00QTI0LTgyRDAtMTk2NjY3RjFDMDgxIiwiVW5pcXVlSWQiOiJkYjU5MWUzMy1wNmZkLTRjNWItODJmMy1iZjY3M2U1YmQwYTIiLCJpc3MiOiJ1cm46c2NjbTpvYXV0aDI6Y2RjYzVlOTEtMGFkZi00YTI0LTgyZDAtMTk2NjY3ZjFjMDgxIiwiYXVkIjoidXJuOnNjY206c2VydmljZSIsImV4cCI6MTU4MDQxNbUwNSwibmJmIjoxNTgwMTU2MzA1fQ.ZUJkxCX6lxHUZhMH_WhYXFm_tbXenEdpgnbIqI1h8hYIJw7xDk3wv625SCfNfsqxhAwRwJByfkXdVGgIpAcFshzArXUVPPvmiUGaxlbB83etUTQjrLIk-gvQQZiE5NSgJ63LCp5KtqFCZe8vlZxnOloErFIrebjFikxqAgwOO4i5ukJdl3KQ07YPRhwpuXmwxRf1vsiawXBvTMhy40SOeZ3mAyCRypQpQNa7NM3adCBwUtYKwHqiX3r1jQU0y57LvU_brBfLUL6JUpk3ri-LSpwPFarRXzZPJUu4-mQFIgrMmKCYbFk3AaEvvrJienfWSvFYLpIYA7lg-6EVYRcCAA`

    > [!TIP]
    > Weitere Informationen zu dieser Befehlszeile finden Sie unter [Installieren und Registrieren des Clients mithilfe einer Azure AD-Identität](deploy-clients-cmg-azure.md#install-and-register-the-client-using-azure-ad-identity). Dieser Prozess ist ähnlich, und es werden nur die Azure AD-Eigenschaften nicht verwendet.

### <a name="known-issues"></a>Bekannte Probleme

Sie können kein Massenregistrierungstoken an einem Standort erstellen, der über einen Standortserver im passiven Modus verfügt.<!-- 6399087 -->

### <a name="bulk-registration-token-tool-usage"></a>Nutzung des Massenregistrierungstokens

Das Tool `BulkRegistrationTokenTool.exe` befindet sich im Ordner `\bin\X64` des Configuration Manager-Installationsverzeichnisses auf dem Standortserver. Melden Sie sich beim Standortserver an, und führen Sie es als Administrator aus. Es unterstützt die folgenden Befehlszeilenparameter:

- `/?`
- `/new`
- `/lifetime`

#### <a name=""></a>/?

Diese Informationen zur Verwendung anzeigen.

Beispiel: `BulkRegistrationTokenTool.exe /?`

#### <a name="new"></a>/new

Erstellen eines neuen Massenregistrierungstokens.

Beispiel: `BulkRegistrationTokenTool.exe /new`

In dem Tool werden die folgenden Informationen angezeigt:
  
- eine GUID, die die Website zum Nachverfolgen von ausgestellten Tokens verwendet
- Der Gültigkeitszeitraum des Tokens, der standardmäßig drei Tage beträgt.
- Das Massenregistrierungstoken.

Das Token wird nicht auf dem Client oder am Standort gespeichert. Kopieren Sie das Token unbedingt von der Eingabeaufforderung, und speichern Sie es an einem sicheren Speicherort.

#### <a name="lifetime"></a>/lifetime

Verwenden Sie dies mit dem `/new`-Parameter, um den Gültigkeitszeitraum des Tokens anzugeben. Geben Sie einen ganzzahligen Wert in Minuten ein. Der Standardwert beträgt 4.320 (drei Tage).

Beispiel: `BulkRegistrationTokenTool.exe /lifetime:4320`

## <a name="see-also"></a>Weitere Informationen:

- [Planen des Cloudverwaltungsgateways](../manage/cmg/plan-cloud-management-gateway.md)

- [Installieren und Zuweisen von Windows 10-Clients in Configuration Manager mit Authentifizierung über Azure AD](deploy-clients-cmg-azure.md)