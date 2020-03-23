---
title: Problembehandlung bei der Integration von Jamf Pro mit Microsoft Intune
titleSuffix: Microsoft Intune
description: Vorschläge zur Behandlung einiger der am häufigsten auftretenden Probleme bei der Integration von Jamf Pro für Mac-Geräte mit Microsoft Intune
keywords: ''
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
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 335841a8642429e36c277673fd8a238d486366c9
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79350615"
---
# <a name="troubleshoot-integration-of-jamf-pro-with-microsoft-intune"></a>Problembehandlung bei der Integration von Jamf Pro mit Microsoft Intune

In diesem Artikel finden Intune-Administratoren Informationen zur Behandlung von Problemen bei der Integration von Jamf Pro für macOS mit Intune.

> [!TIP]  
> Viele der Informationen in diesem Artikel waren ursprünglich in [Problembehandlung bei der Integration von Jamf Pro mit Microsoft Intune](https://support.microsoft.com/help/4519171/troubleshoot-problems-when-integrating-jamf-with-microsoft-intune) auf support.microsoft.com enthalten.

## <a name="prerequisites"></a>Voraussetzungen

Bevor Sie mit der Problembehandlung beginnen, sollten Sie grundlegende Informationen sammeln, um das Problem zu verdeutlichen und die Zeit für die Suche nach einer Lösung zu verkürzen. Wenn beispielsweise ein Problem mit der Jamf-Intune-Integration auftritt, sollten Sie immer zuerst überprüfen, ob alle Voraussetzungen erfüllt sind. Überprüfen Sie vor Beginn der Problembehandlung die folgenden Punkte:

- Überprüfen Sie, ob die Voraussetzungen unter [Integrieren von Jamf Pro in Intune zu Konformitätszwecken](conditional-access-integrate-jamf.md#prerequisites) erfüllt werden.
- Alle Benutzer müssen über Microsoft Intune- und Microsoft AAD Premium P1-Lizenzen verfügen. 
- Sie müssen über ein Benutzerkonto verfügen, das in der Jamf Pro-Konsole die Berechtigung zur Integration mit Microsoft Intune besitzt.
- Sie müssen über ein Benutzerkonto verfügen, das globale Administratorberechtigungen in Azure besitzt.


Beachten Sie die Folgendes, wenn Sie Probleme mit der Jamf Pro-Integration in Intune untersuchen: 
- Wie lautet die genaue Fehlermeldung?
- Wo tritt die Fehlermeldung auf?
- Wann fing das Problem an?  Hat die Jamf Pro-Integration in Intune zuvor funktioniert?
- Wie viele Benutzer sind betroffen? Sind alle oder nur einige Benutzer betroffen?
- Wie viele Geräte sind betroffen? Sind alle oder nur einige Geräte betroffen?
 

## <a name="common-problems"></a>Häufige Probleme 

Die folgenden Informationen können Ihnen helfen, häufige Probleme für Geräte zu identifizieren und zu beheben, nachdem Sie die Integration von Intune und Jamf Pro eingerichtet haben.  

| Problem   | Weitere Informationen                  |
|-----------------|--------------------------|
| **Geräte werden in Jamf Pro als nicht reagierend markiert**  | [Geräte können nicht mit Jamf Pro oder Azure AD einchecken](#devices-are-marked-as-unresponsive-in-jamf-pro) |
| **Mac-Geräte fordern zur Schlüsselbundanmeldung auf, wenn eine App geöffnet wird, Geräte können nicht registriert werden**  | [Benutzer werden aufgefordert, Ihr Kennwort einzugeben, damit Apps sich bei Azure AD registrieren können.](#mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app) |
| **Geräte können nicht registriert werden**  | Folgende Ursachen können vorliegen: <br> **-** [***Ursache 1:*** Die Jamf Pro-App in Azure besitzt die falschen Berechtigungen.](#cause-1) <br> **-** [***Ursache 2:*** Es gibt ein Problem für den *nativen Jamf-Connector für macOS* in Azure AD.](#cause-2) <br> **-** [***Ursache 3:*** Der Benutzer besitzt keine eine gültige Intune- oder Jamf-Lizenz.](#cause-3) <br> **-** [***Ursache 4:*** Der Benutzer hat den Jamf-Self-Service nicht zum Starten der Unternehmensportal-App verwendet.](#cause-4) <br> **-** [***Ursache 5:*** Die Intune-Integration ist deaktiviert.](#cause-5) <br> **-** [***Ursache 6:*** Das Gerät wurde zuvor bei Intune registriert, oder der Benutzer hat versucht, das Gerät mehrfach zu registrieren.](#cause-6) <br> **-** [***Ursache 7:*** JamfAAD fordert Zugriff auf einen Microsoft Workplace Join-Schlüssel aus dem Schlüsselbund des Benutzers an.](#cause-7) |
|  **Mac-Gerät wird in Intune als konform, aber in Azure als nicht konform angezeigt** | [Fehler bei der Geräteregistrierung](#mac-device-shows-compliant-in-intune-but-noncompliant-in-azure) |
| **Doppelte Einträge werden in der Intune-Konsole für Mac-Geräte angezeigt, die mit Jamf registriert wurden** | [Mehrere Registrierungen für dasselbe Gerät](#duplicate-entries-appear-in-the-intune-console-for-mac-devices-enrolled-by-using-jamf) |
| **Die Konformitätsrichtlinie kann das Gerät nicht auswerten** | [Richtlinie ist auf Gerätegruppen ausgerichtet](#compliance-policy-fails-to-evaluate-the-device) |
| **Das Zugriffstoken für Microsoft Graph-API konnte nicht abgerufen werden** | Folgende Ursachen können vorliegen: <br> -[Berechtigungen für die Jamf Pro-App in Azure](#theres-a-permission-issue-with-the-jamf-pro-application-in-azure) <br> - [Abgelaufene Lizenz für Jamf oder Intune](#a-license-required-for-jamf-intune-integration-has-expired) <br> **-** [Ports sind nicht geöffnet](#the-required-ports-arent-open-on-your-network)|
 

### <a name="devices-are-marked-as-unresponsive-in-jamf-pro"></a>Geräte werden in Jamf Pro als nicht reagierend markiert  

**Ursache:** Im Folgenden werden häufige Gründe dafür aufgeführt, dass Geräte von Jamf Pro als *nicht reagierend* gekennzeichnet werden:

- Das Gerät kann nicht mit Jamf Pro einchecken.  
  Jamf Pro erwartet, dass Geräte alle 15 Minuten einchecken. Geräte werden durch Jamf als nicht reagierend gekennzeichnet, wenn sie über einen Zeitraum von 24 Stunden nicht eingecheckt werden können.  

- Das Gerät kann nicht mit Azure AD einchecken.  
  Bei erfolgreicher Registrierung bei Azure AD erhalten macOS-Geräte ein Azure-Token:
  - Dieses Token wird alle 12 Stunden aktualisiert.   
  - Wenn die Tokenaktualisierung für 24 Stunden oder länger fehlschlägt, kennzeichnet Jamf Pro das Gerät als nicht reagierend.  
  - Wenn das Azure-Token abläuft, werden Benutzer aufgefordert, sich bei Azure anzumelden, um ein neues Token abzurufen. Ein Aktualisierungstoken für den Azure-Zugriff wird alle sieben Tage generiert.

**Lösung**  
Nachdem ein Gerät von Jamf Pro als *nicht reagierend* gekennzeichnet wurde, muss sich der registrierte Benutzer des Geräts anmelden, um den nicht reagierenden Zustand zu korrigieren. Dabei muss es sich um den Benutzer handeln, der das Konto mit dem Arbeitsbereich verknüpft hat, da dieser die Intune-Identität im Schlüsselbund für die Anmeldung hat.



### <a name="mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app"></a>Mac-Geräte fordern zur Schlüsselbundanmeldung auf, wenn eine App geöffnet wird  

Nachdem Sie die Integration von Intune und Jamf Pro konfiguriert und Richtlinien für den bedingten Zugriff bereitgestellt haben, werden Benutzer von Geräten, die mit Jamf Pro verwaltet werden, beim Öffnen Microsoft Office 365-Anwendungen wie Teams oder Outlook, für die eine Azure AD-Authentifizierung erforderlich ist, zur Eingabe eines Kennworts aufgefordert. 

Beim Öffnen von Microsoft Teams wird z. B. eine Eingabeaufforderung angezeigt, die dem folgenden Beispiel ähnelt:

``` 
  Microsoft Teams wants to sign using key “Microsoft Workplace Join Key” in your keychain.  
  To allow this, enter the “login” keychain password 
```

**Ursache:** Diese Eingabeaufforderungen werden von Jamf Pro für jede kompatible App generiert, für die eine Azure AD Registrierung erforderlich ist. 

**Lösung**   
In der Eingabeaufforderung muss der Benutzer sein Gerätekennwort angeben, um sich bei Azure AD anzumelden. Zu den Optionen gehören:
- **Verweigern**: Keine Anmeldung und keine Nutzung der App
- **Zulassen**: Ermöglicht eine einmalige Anmeldung, und wenn die App das nächste Mal geöffnet wird, werden Sie zur erneuten Anmeldung aufgefordert.
- **Immer zulassen**: Die Anmeldeinformationen werden für diese Anwendung zwischengespeichert. Wenn Sie die App das nächste Mal öffnen, werden Sie nicht zur erneuten Anmeldung aufgefordert.  

Wenn Sie *Immer zulassen* für eine App auswählen, gilt die Einstellung ausschließlich für diese App. Andere Apps fordern Sie zur Authentifizierung auf, bis diese auch auf *Immer zulassen* eingestellt sind. Zwischengespeicherte Anmeldeinformationen für eine App können nicht von einer anderen App verwendet werden.  

### <a name="devices-fail-to-register"></a>Geräte können nicht registriert werden  

Es gibt verschiedene gängige Ursachen, wenn Mac-Geräte nicht registriert werden können.  

#### <a name="cause-1"></a>Ursache 1  

**Die Jamf Pro-Unternehmensanwendung in Azure hat die falsche Berechtigung oder mehr als eine Berechtigung.**  

  Wenn Sie die App in Azure erstellen, müssen Sie alle standardmäßig festgelegten API-Berechtigungen entfernen und Intune dann nur die Berechtigung *update_device_attributes* zuweisen. 

  **Lösung**  
  Überprüfen Sie die Berechtigungen für die Jamf-App, die Sie in Azure AD erstellt haben, und korrigieren Sie diese gegebenenfalls. Weitere Informationen finden Sie im Verfahren zum [Erstellen einer Anwendung für Jamf in Azure AD](conditional-access-integrate-jamf.md#create-an-application-in-azure-active-directory). 

#### <a name="cause-2"></a>Ursache 2  

**Der native macOS-Connector von **Jamf** wurde nicht in Ihrem Azure AD Mandanten erstellt, oder die Einwilligung für den Connector wurde von einem Konto signiert, das keine globalen Administratorrechte hat.**  

  **Lösung**  
  Weitere Informationen finden Sie im Abschnitt *Konfigurieren der Intune-Integration unter macOS* unter [Integration mit Microsoft Intune](https://docs.jamf.com/10.13.0/jamf-pro/administrator-guide/Integrating_with_Microsoft_Intune.html) auf docs.jamf.com. 

#### <a name="cause-3"></a>Ursache 3

**Der Benutzer besitzt keine eine gültige Intune- oder Jamf-Lizenz.**  

  Wenn keine gültige Lizenz vorliegt, kann der folgende Fehler auftreten, der darauf hindeutet, dass die Jamf-Lizenz abgelaufen ist:  
  ```
    Unable to connect to Microsoft Intune.  
    
    Check your Microsoft Intune Integration configuration.
  ```  

  **Lösung**
  - Jamf-Lizenz: Wenden Sie sich an Jamf, wenn Sie eine neue Lizenz für Jamf benötigen.  
  - Intune-Lizenz: Weisen Sie dem Benutzer eine gültige Lizenz zu, oder wenden Sie sich an Microsoft oder Ihren Partner, um Informationen zu erhalten, wie Sie an eine aktuelle Lizenz gelangen können.

#### <a name="cause-4"></a>Ursache 4  

**Der Benutzer hat den *Jamf-Self-Service* nicht zum Starten der Unternehmensportal-App verwendet.**

Damit ein Gerät erfolgreich bei Intune über Jamf registriert werden kann, muss der Benutzer den Jamf-Self-Service verwenden, um das Intune-Unternehmensportal zu öffnen. Wenn der Benutzer das Unternehmensportal manuell öffnet, wird das Gerät ohne Verbindung mit Jamf registriert.  

Überprüfen Sie die Unternehmensportal-App auf dem Gerät, um zu bestimmen, für welchen Dienst das Gerät registriert wurde. Wenn es über Jamf registriert wurde, sollten Sie eine Benachrichtigung erhalten, um die Self-Service-App zu öffnen und Änderungen vorzunehmen.

In der Unternehmensportal-App wird dem Benutzer **`Not registered`** angezeigt, und ein Eintrag ähnlich dem folgenden Beispiel ist möglicherweise in den Unternehmensportal-Protokollen vorhanden:  

```
   Line 7783: <DATE> <IP ADDRESS> INFO com.microsoft.ssp.application TID=1  
 
   WelcomeViewController.swift: 253 (startLogin()) Portal launched without WPJ only arg while account is under partner management
```

**Lösung**  
So ändern Sie die Registrierungsquelle von Intune in Jamf:
1. [Aufheben der Registrierung Ihres macOS-Geräts bei Intune](https://docs.microsoft.com/user-help/unenroll-your-device-from-intune-macos). Informationen zu weiteren Komplikationen mit Geräten, die nicht vollständig aus Intune entfernt werden, finden Sie unter [*Ursache 6*](#cause-6) in dieser Liste.  

2. Verwenden Sie auf dem Gerät den Jamf-Self-Service, um die Unternehmensportal-App zu öffnen, und registrieren Sie das Gerät anschließend bei Intune. Hierfür müssen Sie [Jamf verwendet haben, um die Unternehmensportal-App für macOS](conditional-access-assign-jamf.md#deploy-the-company-portal-app-for-macos-in-jamf-pro) bereitzustellen, und [eine Richtlinie in Jamf Pro erstellt haben, die das Gerät des Benutzers bei Azure AD](conditional-access-assign-jamf.md#create-a-policy-in-jamf-pro-to-have-users-register-their-devices-with-azure-active-directory) registriert.  

3. Wenn das Portal geöffnet wird, werden Sie auf dem ersten angezeigten Bildschirm aufgefordert, sich anzumelden. Verwenden Sie Ihr Geschäfts-, Schul- oder Unikonto.  

4. Das Unternehmensportal bestätigt Ihre Kontoinformationen und zeigt Ihnen Ihren Status zur Geräteregistrierung und Gerätekompatibilität an. Gelbe Dreiecke heben die Aktionen hervor, die Sie ergreifen müssen, um Ihr macOS-Gerät für die Schule, die Uni oder die Arbeit zu sichern. Klicken Sie auf „Begin“ (Starten), um die Registrierung zu starten.  

5. Geben Sie die Anmeldeinformationen für Ihren Computer ein, wenn Sie dazu aufgefordert werden.  
     
Das Registrieren Ihres Geräts für die Verwaltung kann einige Minuten beanspruchen. Während dieser Zeit können Sie auf dem Gerät andere Vorgänge ausführen. Sobald das Setup des Unternehmenszugriffs abgeschlossen ist, wird Ihnen eine Meldung angezeigt, die Sie darüber informiert.

#### <a name="cause-5"></a>Ursache 5  

**Die Intune-Integration ist deaktiviert.**

Wenn die Intune-Integration deaktiviert ist, wird Benutzern ein Popupfenster im Unternehmensportal mit der folgenden Meldung angezeigt, wenn sie versuchen, ein Gerät zu registrieren:  

```
   Invalid command line input
   
   Registration-only command line flag (-r) can only be used when partner management is enabled in Intune. Please contact your IT admin.
```  

Der Jamf Pro-Server sendet bei deaktivierter Integration einen Impuls an die Intune-Server, der Intune mitteilt, dass die Integration deaktiviert ist. 

**Lösung**  
Aktivieren Sie die Intune-Integration in Jamf Pro erneut. Weitere Informationen finden Sie unter [Konfigurieren der Microsoft Intune-Integration in Jamf Pro](conditional-access-integrate-jamf.md#enable-intune-to-integrate-with-jamf-pro).


#### <a name="cause-6"></a><a name="cause-6"></a>Ursache 6  

**Das Gerät wurde zuvor bei Intune registriert, oder der Benutzer hat versucht, das Gerät mehrfach zu registrieren.**

Wenn die Registrierung eines Geräts bei Jamf aufgehoben, aber nicht ordnungsgemäß aus Intune entfernt wird oder mehrere Registrierungsversuche vorgenommen werden, werden möglicherweise mehrere Instanzen desselben Geräts im Portal angezeigt. Dadurch schlägt die Jamf-Registrierung fehl.

**Lösung**  
1. Starten Sie auf dem Mac das **Terminal**.
2. Führen Sie **sudo JAMF removemdmprofile** aus.
3. Führen Sie **sudo JAMF removeframework** aus.
4. Löschen Sie auf dem Jamf Pro-Server den Inventurdatensatz des Computers.
5. Löschen Sie das Gerät aus Azure AD.
6. Löschen Sie die folgenden Dateien vom Gerät, sofern diese vorhanden sind:
   - /Library/Application Support/com.microsoft.CompanyPortal.usercontext.info
   - /Library/Application Support/com.microsoft.CompanyPortal
   - /Library/Application Support/com.jamfsoftware.selfservice.mac
   - /Library/Saved Application
   - State/com.jamfsoftware.selfservice.mac.savedState
   - /Library/Saved Application State/com.microsoft.CompanyPortal.savedState
   - /Library/Preferences/com.microsoft.CompanyPortal.plist
   - /Library/Preferences/com.jamfsoftware.selfservice.mac.plist
   - /Library/Preferences/com.jamfsoftware.management.jamfAAD.plist
   - /Users/<username>/Library/Cookies/com.microsoft.CompanyPortal.binarycookies
   - /Users/<username>/Library/Cookies/com.jamf.management.jamfAAD.binarycookies
   - com.microsoft.CompanyPortal
   - com.microsoft.CompanyPortal.HockeySDK
   - enterpriseregistration.windows.net
   - https://device.login.microsoftonline.com
   - https://device.login.microsoftonline.com/
   - Microsoft-Sitzungstransportschlüssel (öffentliche und private Schlüssel)
   - Microsoft Workplace Join-Schlüssel (öffentliche und private Schlüssel)
7. Entfernen Sie alle Einträge aus dem Schlüsselbund auf dem Gerät, das auf *Microsoft*, *Intune*oder das *Unternehmensportal* verweist, einschließlich DeviceLogin.Microsoft.com-Zertifikaten. Entfernen Sie *Jamf-* Verweise mit Ausnahme des öffentlichen und privaten Jamf-Schlüssels. 
   > [!IMPORTANT]  
   > Durch das Entfernen des öffentlichen und privaten Schlüssels wird die Geräteregistrierung ungültig.

8. Löschen Sie alle zutreffenden Einträge, die folgender Liste entsprechen:  
   - Art: Anwendungskennwort, Konto: com.microsoft.workplacejoin.thumbprint
   - Art: Anwendungskennwort, Konto: com.microsoft.workplacejoin.registeredUserPrincipalName
   - Art: Zertifikat, ausgestellt von: MS-Organization-Access
   - Art: Bevorzugte Identität, Name (ADFS-STS-URL, falls vorhanden): https://adfs\<DNSName>.com/adfs/ls
   - Art: Bevorzugte Identität, Name: https://enterpriseregistration.windows.net
   - Art: Bevorzugte Identität, Name: https://enterpriseregistration.windows.net/  
9. Starten Sie das Mac-Gerät neu.
10. Deinstallieren Sie das Unternehmensportal vom Gerät.
11. Wechseln Sie zu portal.manage.microsoft.com, und löschen Sie alle Instanzen des Mac-Geräts. Warten Sie mindestens 30 Minuten, bevor Sie mit dem nächsten Schritt fortfahren.
12. Registrieren Sie das Gerät erneut bei Jamf Pro.
13. Öffnen Sie Self-Service erneut, starten Sie die und Registrierungsrichtlinie.


#### <a name="cause-7"></a>Ursache 7  

**JamfAAD fordert Zugriff auf einen Microsoft Workplace Join-Schlüssel aus dem Schlüsselbund des Benutzers an.**

Während der Registrierung wird dem Benutzer eines macOS-Geräts die folgende Eingabeaufforderung angezeigt, um den JamfAAD-Zugriff auf einen Schlüssel aus dem Schlüsselbund zu gestatten: 

```
   JamfAAD wants to access key “Microsoft Workplace Join Key" in your keychain. 
    
   To allow this, enter the “login” keychain password
```

**Lösung**  
Damit das Gerät erfolgreich bei Azure AD registriert werden kann, muss der Benutzer sein Kontokennwort angeben und **Zulassen** festlegen.

Diese Anforderung ähnelt der Anforderung [Mac-Geräte fordern zur Schlüsselbundanmeldung auf, wenn eine App geöffnet wird](#mac-devices-prompt-for-keychain-sign-in-when-you-open-an-app) weiter oben in diesem Artikel.  

 
### <a name="mac-device-shows-compliant-in-intune-but-noncompliant-in-azure"></a>Mac-Gerät wird in Intune als konform, aber in Azure als nicht konform angezeigt  

**Ursache:** Die folgenden Bedingungen können dazu führen, dass ein Gerät in Intune als konform angezeigt wird, aber in Azure als nicht konform:  
- Das Gerät ist nicht ordnungsgemäß registriert.  
- Das Gerät wurde mehrfach registriert, ohne dass die notwendige Bereinigung durchgeführt wurde.

**Lösung**  
Sie können dieses Problem beheben, indem Sie die Lösung unter [*Ursache 6*](#cause-6) für *Geräte können nicht registriert werden* weiter oben in diesem Artikel befolgen. 


### <a name="duplicate-entries-appear-in-the-intune-console-for-mac-devices-enrolled-by-using-jamf"></a>Doppelte Einträge werden in der Intune-Konsole für Mac-Geräte angezeigt, die mit Jamf registriert wurden  
 
**Ursache:** Ein Gerät wird bei Intune in der Regel deshalb mehrfach registriert, weil es nach dem Entfernen aus Intune erneut registriert wurde.  

Wenn ein Gerät aus der Intune- und Jamf Pro-Integration entfernt wird, können Daten zurückbleiben. Das kann dazu führen, dass bei nachfolgenden Registrierungen doppelte Einträge erstellt werden.  

**Lösung**  
Sie können dieses Problem beheben, indem Sie die Lösung unter [*Ursache 6*](#cause-6) für *Geräte können nicht registriert werden* weiter oben in diesem Artikel befolgen. 

### <a name="compliance-policy-fails-to-evaluate-the-device"></a>Die Konformitätsrichtlinie kann das Gerät nicht auswerten  

**Ursache:** Die Jamf-Integration mit Intune unterstützt keine Konformitätsrichtlinien für Gerätegruppen. 

**Lösung**  
Ändern Sie die Konformitätsrichtlinie für macOS-Geräte, die Benutzergruppen zugewiesen werden sollen. 


### <a name="could-not-retrieve-the-access-token-for-microsoft-graph-api"></a>Das Zugriffstoken für Microsoft Graph-API konnte nicht abgerufen werden

Sie erhalten die folgende Fehlermeldung:

```
   Could not retrieve the access token for Microsoft Graph API. Check the configuration for Microsoft Intune Integration.
```   

Diesem Fehler kann eine der folgenden Ursachen zugrunde liegen: 

#### <a name="theres-a-permission-issue-with-the-jamf-pro-application-in-azure"></a>Bei der Jamf Pro-Anwendung in Azure liegt ein Berechtigungsproblem vor.

Beim Registrieren der Jamf Pro-App in Azure wurde eine der folgenden Bedingungen erfüllt:  
- Die App hat mehr als eine Berechtigung erhalten.
- Die Option **Administratorzustimmung für *\<Ihr Unternehmen>* erteilen** wurde nicht ausgewählt.  

**Lösung**  
Die Lösung für dieses Problem finden Sie unter Ursache 1 für [Geräte können nicht registriert werden](#devices-fail-to-register) weiter oben in diesem Artikel.

#### <a name="a-license-required-for-jamf-intune-integration-has-expired"></a>Eine für die Jamf-Intune-Integration erforderliche Lizenz ist abgelaufen

**Lösung**: Die Lösung für dieses Problem finden Sie unter Ursache 3 für [Geräte können nicht registriert werden](#devices-fail-to-register). 

#### <a name="the-required-ports-arent-open-on-your-network"></a>Die erforderlichen Ports in Ihrem Netzwerk sind nicht geöffnet

**Lösung**: Überprüfen Sie die Informationen für Netzwerkports unter [Voraussetzungen](conditional-access-integrate-jamf.md#prerequisites) für die Integration von Jamf Pro mit Intune.


## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen finden Sie unter [Integrieren von Jamf Pro in Intune zu Konformitätszwecken](conditional-access-integrate-jamf.md).