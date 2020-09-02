---
title: Behandeln häufig auftretender Probleme in Bezug auf den Intune Exchange Connector
titleSuffix: Microsoft Intune
description: Behandeln und Lösen häufig auftretender Probleme in Bezug auf den lokalen Microsoft Intune Exchange Connector
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/02/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: cea8981b9fdd16e0d8da9dd36445b8fbdfe3d53f
ms.sourcegitcommit: 94e86320b9340507becc9e6ce4b6eb744f09fcd8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193945"
---
# <a name="resolve-common-errors-for-the-intune-exchange-connector"></a>Lösen häufig auftretender Probleme in Bezug auf den Intune Exchange Connector

In diesem Artikel erfahren Intune-Administratoren, wie sie bestimmte Fehler lösen können, die beim Ausführen des Intune Exchange Connectors auftreten können. Zudem werden die entsprechenden Meldungen erläutert.  

## <a name="configuration-failed-and-returned-error-code-0x0000001"></a>Fehler bei der Konfiguration: Fehlercode 0x0000001

**Problem:**  
Beim Konfigurieren des Microsoft Intune Exchange Connectors erhalten Sie die folgende Fehlermeldung:

```
   The Microsoft Intune Exchange Connector cannot connect to the Microsoft Exchange server.  
   The following Microsoft Exchange Server address could not be reached <Exchange server Name FQDN>  
   Verify that the FQDN of the exchange server address and credentials that you entered is correct and the server is running. The Microsoft Intune Exchange Connector does not support Exchange server arrays.  
   Error code: 0x0000001  
```

Dieses Problem kann auftreten, wenn die Internetproxyeinstellungen falsch konfiguriert sind.

**Lösung**:  
Konfigurieren von Proxyeinstellungen:
1. Wenden Sie sich an den Administrator des lokalen Netzwerks, um sicherzustellen, dass die Proxyeinstellungen ordnungsgemäß konfiguriert sind. 
2. Verwenden Sie den **Netsh winhttp**-Befehl, um den Proxyserver zu konfigurieren und die erforderliche Ausschlussliste hinzuzufügen. Beispiel:  

   ```
   Netsh winhttp set proxy proxy-server="http=proxy.corp.domain.com" bypass-list"34*.*;134.132.*.*;10.*.*;localhost;*.corp.domain.com;*.staging.domain.com"
   ```

## <a name="configuration-failed-and-returned-error-code-0x000000b"></a>Fehler bei der Konfiguration: Fehlercode 0x000000b   

**Problem:**  
Beim Konfigurieren des Microsoft Intune Exchange Connectors erhalten Sie die folgende Fehlermeldung:  

```
   The Microsoft Intune Exchange Connector experienced an error:  
   CertEnroll::CX509PrivateKey::Create: The system cannot find the file specified. 0x80070002 (WIN32: 2  
   ERROR_FILE_NOT_FOUND  
   Error code: 0x000000b  
```
Dieses Problem kann auftreten, wenn das Konto, das Sie für die Anmeldung bei Intune verwendet haben, kein globales Intune-Administratorkonto ist.

**Lösung**:  
Melden Sie sich bei Intune mit einem Konto an, das ein globales Administratorkonto ist, oder fügen Sie Ihr Konto der Gruppe „Globaler Administrator“ hinzu. Weitere Informationen finden Sie unter [Rollenbasierte Zugriffssteuerung (RBAC) mit Microsoft Intune](../fundamentals/role-based-access-control.md).

## <a name="configuration-failed-and-returned-error-code-0x0000006"></a>Fehler bei der Konfiguration: Fehlercode 0x0000006

**Problem:**  
Beim Konfigurieren des Microsoft Intune Exchange Connectors erhalten Sie die folgende Fehlermeldung:  

```  
   The Microsoft Intune Exchange Connector cannot connect to Microsoft Intune  
   Verify that you are connected to the Internet, check the Microsoft Intune Service Status, and try to connect again.  
   Error code: 0x00000006  
```  
Dieser Fehler kann auftreten, wenn ein Proxyserver zum Herstellen einer Verbindung zum Internet verwendet wird und den Datenverkehr zum Intune-Dienst blockiert. Um zu ermitteln, ob ein Proxyserver verwendet wird, navigieren Sie zu **Systemsteuerung\Netzwerk und Internet** > **Internetoptionen**, öffnen Sie die Registerkarte **Verbindungen**, und klicken Sie dann auf **LAN-Einstellungen**.

**Lösung**:  

- **Option 1:** Entfernen Sie die Proxyeinstellungen, damit der Computer eine Verbindung mit dem Internet herstellen kann, ohne den Proxyserver zu benutzen.  

- **Option 2:** Konfigurieren Sie den Proxyserver für die Kommunikation mit dem Intune-Dienst, wie unter [Anforderungen an den Intune Exchange Connector](exchange-connector-install.md#intune-exchange-connector-requirements) dokumentiert.



## <a name="event-7000-or-7041-microsoft-intune-exchange-connector-service-wont-start"></a>Ereignis 7000 oder 7041: Microsoft Intune Exchange Connector-Dienst wird nicht gestartet

**Problem:**  
Ein iOS-Gerät kann nicht bei Intune registriert werden, woraufhin eine der folgenden Fehlermeldungen angezeigt wird:  

```  
   Log Name:      System
   Source:            Service Control Manager
   Date:               <time>
   Task Category: None
   Level:               Error
   Keywords:        Classic
   User:                N/A
   Computer:      <computer>
   Description:
   The Microsoft Intune Exchange Connector Service service failed to start because of the following error:  
   The service did not start because of a logon failure.
```  

```  
   Log Name:      System
   Source:            Service Control Manager
   Date:               <time>
   Event ID:          7041
   Task Category: None
   Level:               Error   
   Keywords:        Classic
   User:                N/A
   Computer:       <computer>
   Description:
   The WIEC service was unable to log on as .\WIEC_USER with the currently configured password because of the following error:
   Logon failure: the user has not been granted the requested logon type at this computer.
   Service: WIEC
   Domain and account: .\WIEC_USER
   This service account does not have the required user right "Log on as a service."  
```
Dieses Problem kann auftreten, wenn das **WIEC_User**-Konto nicht über das **Anmelden als Dienst**-Benutzerrecht in der lokalen Richtlinie verfügt.

**Lösung**:  
Weisen Sie auf dem Computer, auf dem der Intune Exchange Connector ausgeführt wird, dem **WIEC_User**-Dienstkonto das **Anmelden als Dienst**-Benutzerrecht zu. Wenn es sich bei dem Computer um einen Knoten in einem Cluster handelt, muss dem Clusterdienstkonto auf allen Knoten im Cluster das *Anmelden als Dienst*-Benutzerrecht zugewiesen werden.  

Führen Sie die folgenden Schritte aus, um dem **WIEC_User**-Dienstkonto auf dem Computer das **Anmelden als Dienst**-Benutzerrecht zuzuweisen:

1. Melden Sie sich beim Computer als Administrator oder als Mitglied der Gruppe „Administratoren“ an.
2. Führen Sie **secpol.msc** aus, um die lokale Sicherheitsrichtlinie zu öffnen.
3. Navigieren Sie zu **Sicherheitseinstellungen** > **Lokale Richtlinien**, und klicken Sie dann auf **Zuweisen von Benutzerrechten**.
4. Doppelklicken Sie auf den rechten Bereich **Anmelden als Dienst**.
5. Klicken Sie auf **Benutzer oder Gruppe hinzufügen**, fügen Sie der Richtlinie **WIEC_USER** hinzu, und klicken Sie dann zweimal auf **OK**.

Wenn das **Anmelden als Dienst**-Benutzerrecht dem **WIEC_User**-Dienstkonto zugewiesen wurde, dann jedoch wieder entfernt wurde, wenden Sie sich an den Domänenadministrator, um festzustellen, ob es von einer Gruppenrichtlinieneinstellung überschrieben wird.  

## <a name="next-steps"></a>Nächste Schritte  

Im folgenden Artikel erfahren Sie, wie Sie bestimmte Fehler beheben können:
- [Resolve common problems for the Intune Exchange Connector (Lösen häufig auftretender Probleme in Bezug auf den Intune Exchange Connector)](troubleshoot-exchange-connector-common-problems.md) 

Wenden Sie sich an den Support oder an die Intune-Community.
- Navigieren Sie zu [Support anfordern](../fundamentals/get-support.md), um das Problem mithilfe der Intune-Konsole zu beheben oder eine Supportanfrage bei Microsoft zu stellen. 
- Posten Sie Ihr Problem in den [Microsoft Intune-Foren](/answers/products/mem).