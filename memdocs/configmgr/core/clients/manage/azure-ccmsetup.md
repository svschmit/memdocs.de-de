---
title: Workflow für die Azure AD-Authentifizierung
titleSuffix: Configuration Manager
description: Details zum Installationsprozess des Konfigurations-Manager-Clients auf einem Windows 10-Gerät mit der Azure Active Directory-Authentifizierung
ms.date: 07/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9aaf466a-3f40-4468-b3cd-f0010f21f05a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9215688104b1a929cad7c172126387961851760b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694998"
---
# <a name="azure-ad-authentication-workflow"></a>Workflow für die Azure AD-Authentifizierung

*Gilt für: Configuration Manager (Current Branch)*

Bei diesem Artikel handelt es sich um eine technische Referenz für den Installationsprozess des Konfigurations-Manager-Clients auf einem Windows 10-Gerät, das mit Azure Active Directory (Azure AD) verknüpft ist. Darin wird der Workflowprozess für die Geräteauthentifizierung und die Clientinstallation erläutert.  
 

## <a name="azure-ad-token-request-workflow"></a>Workflow zur Tokenanforderung in Azure AD

![Ccmsetup-Workflow in Azure AD (Diagramm)](media/azure-ad-install-workflow.png)  

### <a name="1-azure-ad-token-request"></a>1. Tokenanforderung in Azure AD

Ein Client, der in Windows 10 in einer Azure AD-Domäne eingebunden ist, verwendet Azure AD-Parameter, um ein Token anzufordern. Die folgenden Einträge werden in **ccmsetup.log** protokolliert:

- Anfordern eines Azure AD-Gerätetokens:

    ``` Log
    Getting AAD (device) token with: ClientId = 22ed38d9-XXXX-4036-XXXX-a98452fda4fc, ResourceUrl = https://ConfigMgrService, AccountId = https://login.microsoftonline.com/common/oauth2/token
    ```

- Wenn kein Gerätetoken abgerufen werden kann, fordert der Client ein Azure AD-Benutzertoken an:

    ``` Log
    Getting AAD (user) token with: ClientId = f1f9b14e-XXXX-4f17-XXXX-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = X49FC29A-ECE3-XXX-A3C1-XXXXXXF035A6E
    ```

> [!NOTE]
> Ein Client sollte ein WPJ-Zertifikat (Arbeitsplatz beitreten, workplace join) erhalten, wenn er Azure AD beitritt. Wenn ein solches WPJ-Zertifikat nicht gefunden wird, versucht der Client nicht, die Anforderung mithilfe des Kommunikationskanals des Sicherheitstokendiensts (CCM_STS) zu erstellen. Dieses Verhalten ist darauf zurückzuführen, dass der Client der Anforderung keine Azure AD-Token hinzufügen kann. Wenn der Client nicht ordnungsgemäß mit Azure AD verknüpft ist, verfügt das Gerät in der Regel nicht über dieses Zertifikat.
>
> Wenn das Token nicht gültig ist, leitet das Cloud Management Gateway (CMG) außerdem die Anforderung nicht an die internen Standortrollen weiter. Das Token kann ungültig sein, wenn der Mandant nicht als Cloudverwaltungsdienst in Configuration Manager registriert ist.


### <a name="2-configuration-manager-client-token-request"></a>2. Tokenanforderung des Konfigurations-Manager-Clients

Sobald der Client über ein Azure AD-Token verfügt, fordert er ein CCM-Token (Konfigurations-Manager-Client) an.

Die folgenden Einträge werden in der **ccmsetup.log**-Datei des virtuellen CMG-Computers protokolliert:

``` Log
Getting CCM Token from STS server 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216'
Getting CCM Token from https://CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216/CCM_STS
```

#### <a name="21-cmg-gets-request"></a>2.1 Das CMG empfängt eine Anforderung

Die folgenden Einträge werden in der **IIS.log**-Datei protokolliert:

``` Log
RD0003FF74XX2 10.0.0.4 GET /CCM_STS - 443 - HTTP/1.1 python-requests/2.20.0 - - 13.95.234.44 404 0 2 1477 154 15
```

#### <a name="22-cmg-forwards-request-to-cmg-connection-point"></a>2.2 Das CMG leitet die Anforderung an den CMG-Verbindungspunkt weiter

Die folgenden Einträge werden in der **CMGService.log**-Datei protokolliert:

``` Log
RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
```

#### <a name="23-cmg-connection-point-transforms-cmg-client-request-to-management-point-client-request"></a>2.3 Der CMG-Verbindungspunkt transformiert die CMG-Clientanforderung in eine Verwaltungspunkt-Clientanforderung

Die folgenden Einträge werden in der **SMS_Cloud_ProxyConnector.log.log**-Datei protokolliert:

``` Log
MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms
```

#### <a name="24-management-point-verifies-user-token-in-site-database"></a>2.4 Der Verwaltungspunkt überprüft das Benutzertoken in der Standortdatenbank

Die folgenden Einträge werden in der **CCM_STS.log**-Datei protokolliert:

``` Log
Validated AAD token. TokenType: Device TenantId: XXXXe388-XXXX-485c-XXXX-e8e4eb41XXXX UserId: 00000000-0000-0000-0000-000000000000 DeviceId: 0XXXXX80-77XX-4XXa-X63X-67XXXXX64bb7 OnPrem_UserSid:  OnPrem_DeviceSid:

Return token to client, token type: UDA, hierarchyId: XXXX4f9c-XXXX-46a5-XXXX-7612c324XXXX, userId: 00000000-0000-0000-0000-000000000000, deviceId: GUID:XXXXaee9-cXXc-4ccd-XXXX-f1417d81XXX
```


## <a name="content-location-request"></a>Anforderung des Speicherorts des Inhalts

Sobald der Client eine Antwort mit dem CCM-Token erhält, wird dieses zwischengespeichert und mithilfe des CMG zum Anfordern von Standortinformationen und dem Inhaltsspeicherort verwendet. Die folgenden Einträge werden in **ccmsetup.log** protokolliert:

``` Log
Cached encrypted token for 'S-1-5-18'. Will expire at '00/99/2999 00:00:00'
Sending location request to 'CloudManagementGateway.cloudapp.net/CCM_PROXY_MUTUALAUTH/XXXXXX037938216' with payload '< Request >
Appending CCM Token to the header.
```


## <a name="client-installation"></a>Clientinstallation

Das Gerät lädt Clientinhalte herunter und startet die Installation.

### <a name="communication-validation"></a>Kommunikationsüberprüfung

- Das CMG überprüft das Clienttoken über das CMG, den CMG-Verbindungspunkt, HTTP(S) und die Verwaltungspunkt-Datenbankanforderung.
- Der Client überprüft das CMG-Dienstzertifikat oder -Verwaltungszertifikat.
- Public Key-Infrastruktur (PKI) für CMG-Dienstzertifikate: Der Client benötigt die Stammzertifizierungsstelle (CA) des CMG-Zertifikats im lokalen Speicher.
- CMG-Dienstzertifikate von Drittanbietern: Clients überprüfen ein Zertifikat mit dessen Stammzertifizierungsstelle im Internet automatisch.


## <a name="common-issues"></a>Häufige Probleme

- Stammzertifizierungsstelle ist nicht vorhanden
- CRL-Überprüfung (Zertifikatsperrliste, Certificate Revocation List) aktiviert: Veröffentlichen Sie die CRL im Internet, oder verwenden Sie die Option **/NoCRLcheck** in der Befehlszeile.
- WPJ-Zertifikat nicht gefunden: Der Client ist bei Azure AD registriert, aber nicht mit Azure AD verknüpft.

Die Verwendung von „/NoCRLCheck“ eignet sich nur für den ccmsetup-Bootstrap. Damit die Clients voll funktionsfähig sind, sollten Sie die CRL im Internet veröffentlichen. Sie können dieses Problem umgehen, indem Sie die CRL-Überprüfung in der Clientkommunikationskonfiguration der Website deaktivieren. Andernfalls beenden die Clients die Kommunikation mit dem Server, wenn die Sicherheitseinstellungen vom Ortsdienst aktualisiert werden.


## <a name="client-registration"></a>Clientregistrierung

![Diagramm des Azure AD-Registrierungsworkflows](media/azure-ad-registration-workflow.png)  

### <a name="1-configuration-manager-client-request-registration"></a>1. Anforderung der Configuration Manager-Clientregistrierung

Die folgenden Einträge werden in **ClientIDManagerStartup.log** protokolliert:

``` Log
[RegTask] - Client is not registered. Sending registration request for GUID:1XXXXXEF-5XX8-4XX3-XEDX-XXXFBFF78XXX ...
Registering client using AAD auth.
```

### <a name="2-configuration-manager-request-azure-ad-token-to-register-client"></a>2. Configuration Manager fordert für die Registrierung des Clients ein Azure AD-Token an

Die folgenden Einträge werden in **ADALOperationProvider.log** protokolliert:

``` Log
Getting AAD (user) token with: ClientId = f1f9b14e-XXXX-4f17-XXXX-2593f6eee91e, ResourceUrl = https://ConfigMgrService, AccountId = X49FC29A-ECE3-XXX-A3C1-XXXXXXF035A6E
Retrieved AAD token for AAD user '00000000-0000-0000-0000-000000000000'
```

#### <a name="21-configuration-manager-client-is-registered"></a>2.1 Configuration Manager-Client ist registriert  

Die folgenden Einträge werden in **ClientIDManagerStartup.log** protokolliert:

``` Log
[RegTask] - Client is registered. Server assigned ClientID is GUID:1XXXXXEF-5XX8-4XX3-XEDX-XXXFBFF78XXX. Approval status 3
```

> [!NOTE]  
> Während der Clientregistrierung erfolgt stets die Zertifikatsvalidierung. Dies gilt auch dann, wenn Sie die Azure AD-Authentifizierungsmethode verwenden, um den Client zu registrieren.


### <a name="3-configuration-manager-client-token-request"></a>3. Tokenanforderung des Konfigurations-Manager-Clients

Sobald der Standort den Client registriert hat, fordert der Client ein CCM-Token an. Der CCM-Token wird für das lokale Systemkonto (S-1-5-18) verschlüsselt und für acht Stunden im Cache zwischengespeichert. Nach acht Stunden läuft das Token ab, woraufhin der Client die Verlängerung des Tokens anfordert.

Die folgenden Einträge werden in **ClientIDManagerStartup.log** protokolliert:

``` Log
Getting CCM Token from STS server 'MP.MYCORP.COM'
Getting CCM Token from https://MP.MYCORP.COM/CCM_STS
...
Cached encrypted token for 'S-1-5-18'. Will expire at 'XX/XX/XX XX:XX:XX'
```

#### <a name="31-cmg-gets-request"></a>3.1 CMG empfängt Anforderung

Die folgenden Einträge werden in der **IIS.log**-Datei protokolliert:

``` Log
RD0003FF74XX2 10.0.0.4 GET /CCM_STS - 443 - HTTP/1.1 python-requests/2.20.0 - - 13.95.234.44 404 0 2 1477 154 15
```

#### <a name="32-cmg-forwards-request-to-cmg-connection-point"></a>3.2 CMG leitet Anforderung an CMG-Verbindungspunkt weiter

Die folgenden Einträge werden in der **CMGService.log**-Datei protokolliert:

``` Log
RequestUri: /CCM_PROXY_SERVERAUTH/XXXXXX037938216/CCM_STS  RequestCount: 769  RequestSize: 1081595 Bytes  ResponseCount: 769     ResponseSize: 36143 Bytes  AverageElapsedTime: 3945 ms
```

#### <a name="33-cmg-connection-point-transforms-cmg-client-request-to-management-point-client-request"></a>3.3 CMG-Verbindungspunkt transformiert CMG-Clientanforderung in eine Verwaltungspunkt-Clientanforderung

Die folgenden Einträge werden in der **SMS_Cloud_ProxyConnector.log.log**-Datei protokolliert:

``` Log
MessageID: 3087bd34-b82c-4950-b972-e82bb0fb8385 RequestURI: https://MP.MYCORP.COM/CCM_STS EndpointName: CCM_STS ResponseHeader: HTTP/1.1 200 OK ~~ ResponseBodySize: 0 ElapsedTime: 2 ms
```

#### <a name="34-management-point-verifies-user-token-in-site-database"></a>3.4 Verwaltungspunkt überprüft das Benutzertoken in Standortdatenbank

Die folgenden Einträge werden in der **CCM_STS.log**-Datei protokolliert:

``` Log
Validated AAD token. TokenType: Device TenantId: XXXXe388-XXXX-485c-XXXX-e8e4eb41XXXX UserId: 00000000-0000-0000-0000-000000000000 DeviceId: 0XXXXX80-77XX-4XXa-X63X-67XXXXX64bb7 OnPrem_UserSid:  OnPrem_DeviceSid:

Return token to client, token type: UDA, hierarchyId: XXXX4f9c-XXXX-46a5-XXXX-7612c324XXXX, userId: 00000000-0000-0000-0000-000000000000, deviceId: GUID:XXXXaee9-cXXc-4ccd-XXXX-f1417d81XXX
```
