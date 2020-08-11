---
title: 'Tutorial: Aktivieren der Co-Verwaltung für Internetgeräte'
titleSuffix: Configuration Manager
description: Informationen zum Konfigurieren der Co-Verwaltung für neue internetbasierte Windows 10-Geräte mit Configuration Manager und Microsoft Intune
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 05/14/2020
ms.topic: tutorial
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 7fb02a5c-e286-46b1-a972-6335c858429a
ms.openlocfilehash: 742cd1e86ac0bff6563c0d3ee4edce7324629480
ms.sourcegitcommit: c1afc8abd0d7da48815bd2b0e45147774c72c2df
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/05/2020
ms.locfileid: "87815462"
---
# <a name="tutorial-enable-co-management-for-new-internet-based-devices"></a>Tutorial: Aktivieren der Co-Verwaltung für neue internetbasierte Geräte

Mit der Co-Verwaltung können Sie Ihre bewährten Prozesse für die Verwendung von Configuration Manager zum Verwalten von PCs in Ihrem Unternehmen beibehalten. Gleichzeitig investieren Sie mit der Nutzung von Intune für Sicherheit und moderne Bereitstellung in die Cloud.

In diesem Tutorial richten Sie die Co-Verwaltung von Windows 10-Geräten in einer Umgebung ein, wo Sie sowohl Azure Active Directory (AD) als auch ein lokales AD verwenden, jedoch kein [hybrides Azure Active Directory](/azure/active-directory/devices/concept-azure-ad-join-hybrid) (AD) haben. Die Configuration Manager-Umgebung umfasst einen einzigen primären Standort mit allen Standortsystemrollen, die sich auf dem gleichen Server – dem Standortserver – befinden. Dieses Tutorial beginnt mit der Voraussetzung, dass Ihre Windows 10-Geräte bereits bei Intune registriert sind. 

Wenn Sie über ein hybrides Azure AD verfügen, das Ihr lokales AD mit Azure AD verbindet, sollten Sie unser Begleittutorial [Co-Verwaltung für vorhandene Configuration Manager-Clients aktivieren](tutorial-co-manage-clients.md) lesen.

Verwenden Sie dieses Tutorial in folgenden Fällen:
  
- Sie müssen Windows 10-Geräte in die Co-Verwaltung einbinden. Diese Geräte können über Windows Autopilot oder direkt von Ihrem Hardware-OEM bereitgestellt werden.
- Sie verfügen über zurzeit mit Intune verwaltete Windows 10-Geräte im Internet, denen Sie den Configuration Manager-Client hinzufügen möchten.

**Die Themen dieses Tutorials sind:**  
> [!div class="checklist"]  
> * Überprüfen der Voraussetzungen für Azure und Ihre lokale Umgebung
> * Anfordern eines öffentlichen SSL-Zertifikats für das Cloud Management Gateway (CMG)
> * Aktivieren von Azure-Diensten in Configuration Manager
> * Bereitstellen und Konfigurieren eines Cloud Management Gateways  
> * Konfigurieren von Verwaltungspunkt und Clients zum Verwenden des CMG
> * Aktivieren der Co-Verwaltung in Configuration Manager
> * Konfigurieren von Intune zum Installieren des Configuration Manager-Clients

## <a name="prerequisites"></a>Voraussetzungen  

### <a name="azure-services-and-environment"></a>Azure-Dienste und -Umgebung

- Azure-Abonnement ([kostenlose Testversion](https://azure.microsoft.com/free))
- Azure Active Directory Premium
- Microsoft Intune-Abonnement
  > [!TIP]  
  > Ein Enterprise Mobility + Security-Abonnement (EMS) umfasst Azure Active Directory Premium und Microsoft Intune. EMS-Abonnement ([kostenlose Testversion](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)).  

- Intune ist für das [automatische Registrieren von Geräten](tutorial-co-manage-clients.md#configure-auto-enrollment-of-devices-to-intune) konfiguriert.  

> [!TIP]
> Sie müssen nicht mehr einzelne Intune- oder EMS-Lizenzen kaufen und Ihren Benutzern zuweisen. Weitere Informationen finden Sie unter [Häufig gestellte Fragen zum Produkt und zur Lizenzierung](../core/understand/product-and-licensing-faq.md#bkmk_mem).

### <a name="on-premises-infrastructure"></a>Lokale Infrastruktur

- Configuration Manager Current Branch, Version 1810 oder höher.
  
  Version 1810 führt [Erweitertes HTTP](../core/plan-design/hierarchy/enhanced-http.md) ein, was in diesem Tutorial verwendet wird, um komplexere PKI-Anforderungen zu vermeiden. Mit erweitertem HTTP muss der primäre Standort, mit dem Sie Clients verwalten, zur Verwendung von Zertifikaten, die in Configuration Manager generiert wurden, für HTTP-Standortsysteme konfiguriert werden.  

  Version 1810 führt außerdem eine einfachere Befehlszeile für die internetbasierte Installation der Configuration Manager-Clients ein.

- Die MDM-Autorität muss auf Intune festgelegt sein.  

### <a name="external-certificates"></a>Externe Zertifikate

- CMG-Serverauthentifizierungszertifikat. Dieses Zertifikat ist ein SSL-Zertifikat eines öffentlichen und global vertrauenswürdigen Zertifikatanbieters. Hierbei kann es sich beispielsweise um DigiCert, Thawte oder VeriSign handeln. Sie müssen dieses Zertifikat als PFX-Datei mit privatem Schlüssel exportieren.  

- Weiter unten in diesem Tutorial finden Sie eine Anleitung zum Konfigurieren der Anforderung für dieses Zertifikat.

### <a name="permissions"></a>Berechtigungen

Verwenden Sie in diesem Tutorial durchgehend die folgenden Berechtigungen, um Aufgaben auszuführen:

- Ein Konto, das ein *globaler Administrator* für Azure Active Directory (Azure AD) ist
- Ein Konto, das *Domänenadministrator* in Ihrer lokalen Infrastruktur ist  
- Ein Konto, das *Hauptadministrator* für *alle* Bereiche in Configuration Manager ist

## <a name="request-a-public-certificate-for-the-cloud-management-gateway"></a>Anfordern eines öffentlichen Zertifikats für das Cloud Management Gateway

Wenn Ihre Geräte im Internet sind, setzt Co-Verwaltung das Configuration Manager Cloud Management Gateway (CMG) voraus. CMG ermöglicht Ihren internetbasierten Windows 10-Geräten die Kommunikation mit Ihrer lokalen Configuration Manager-Bereitstellung. Um eine Vertrauensstellung zwischen Geräten und Ihrer Configuration Manager-Umgebung einzurichten, setzt das CMG ein SSL-Zertifikat voraus.

In diesem Tutorial wird ein öffentliches Zertifikat namens **CMG-Serverauthentifizierungszertifikat** verwendet, das die Autorität von einem global vertrauenswürdigen Zertifikatanbieter ableitet. Sie können die Co-Verwaltung zwar mit Zertifikaten konfigurieren, die Autorität von Ihrer lokalen Microsoft-Zertifizierungsstelle ableiten, aber die Verwendung von selbstsignierten Zertifikaten liegt nicht im Rahmen dieses Tutorials.

Das **CMG-Serverauthentifizierungszertifikat** dient zum Verschlüsseln des Kommunikationsdatenverkehrs zwischen Configuration Manager-Client und CMG. Das Zertifikat führt die Verfolgung zu einem vertrauenswürdigen Stamm zurück durch, um die Identität des Servers für den Client zu überprüfen. Das öffentliche Zertifikat enthält einen vertrauenswürdigen Stamm, dem Windows-Clients bereits vertrauen.

Informationen zu diesem Zertifikat: 

- Sie identifizieren einen eindeutigen Namen für Ihren CMG-Dienst in Azure und geben diesen Namen dann in Ihrer Zertifikatanforderung an.  
- Sie generieren Ihre Zertifikatanforderung auf einem bestimmten Server und senden dann die Anforderung an einen öffentlichen Zertifikatanbieter, um das erforderliche SSL-Zertifikat zu erhalten.  
- Sie importieren in das System, das die Anforderung des Zertifikats generiert hat, das Sie vom Anbieter zurückerhalten. Sie verwenden denselben Computer wie zum Exportieren des zu verwendenden Zertifikats, wenn Sie später das CMG zu Azure bereitstellen.  
- Wenn das CMG installiert wird, erstellt es einen CMG-Dienst in Azure mit dem Namen, den Sie im Zertifikat angegeben haben.  

### <a name="identify-a-unique-name-for-your-cloud-management-gateway-in-azure"></a>Identifizieren eines eindeutigen Namens für Ihr Cloud Management Gateway in Azure

Wenn Sie das CMG-Serverauthentifizierungszertifikat anfordern, geben Sie an, was ein eindeutiger Name sein muss, um Ihren *Clouddienst (klassisch)* in Azure zu identifizieren. Standardmäßig verwendet die öffentliche Azure-Cloud *cloudapp.net*, und das CMG wird in der Domäne „cloudapp.net“ als *\<YourUniqueDnsName>.cloudapp.net* gehostet.  

> [!TIP]  
> In diesem Tutorial verwendet das **CMG-Serverauthentifizierungszertifikat** einen FQDN, der mit *contoso.com* endet.  Nach dem Erstellen des CMG konfigurieren wir einen kanonischen Namenseintrag (CNAME) im öffentlichen DNS unserer Organisation. Hierdurch wird für das CMG ein Alias erstellt, der dem Namen zugeordnet wird, den wir im öffentlichen Zertifikat verwenden.  

Bevor Sie Ihr öffentliches Zertifikat anfordern, bestätigen Sie, dass der Name, den Sie verwenden möchten, in Azure verfügbar ist. Sie erstellen den Dienst nicht direkt in Azure. Stattdessen verwendet Configuration Manager den Namen, der im öffentlichen Zertifikat angegeben wird, das Sie anfordern, um den Cloud-Dienst zu erstellen, wenn Sie das CMG installieren.  

1. Melden Sie sich zuerst beim [Microsoft Azure-Portal](https://portal.azure.com/) an.  

2. Wählen Sie anschließend **Ressource erstellen** und dann die Kategorie **Compute** aus. Klicken Sie dann auf **Clouddienst**. Die Seite „Clouddienst (klassisch)“ wird geöffnet.

3. Geben Sie für **DNS-Name** den Präfixnamen für den Clouddienst an, den Sie verwenden. Dieses Präfix muss mit dem identisch sein, das Sie später bei der Anforderung eines öffentlichen Zertifikats für das CMG-Serverauthentifizierungszertifikat verwenden. Wir verwenden *MyCSG*, wodurch der Namespace von *MyCSG.cloudapp.net* erstellt wird. Auf der Benutzeroberfläche wird bestätigt, ob der Name verfügbar ist oder bereits von einem anderen Dienst verwendet wird.  
 Nachdem Sie bestätigt haben, dass der Name, den Sie verwenden möchten, verfügbar ist, können Sie die Zertifikatsignieranforderungsdatei (Certificate Signing Request, CSR) übermitteln.

### <a name="request-the-certificate"></a>Anfordern des Zertifikats

Verwenden Sie die folgenden Informationen, um eine Zertifikatsignieranforderung für Ihr CMG an den Anbieter öffentlicher Zertifikate zu übermitteln. Ändern Sie die folgenden Werte Ihrer Umgebung gemäß.  

- *MyCMG* zum Identifizieren des Dienstnamens des Cloud Management Gateway
- *Contoso* als Name des Unternehmens
- *Contoso.com* als öffentliche Domäne

Sie sollten Ihren primären Standortserver verwenden, um die Zertifikatsignieranforderungen (CSR) zu generieren. Wenn Sie das Zertifikat erhalten, müssen Sie es auf dem gleichen Server registrieren, der die CSR generiert hat, oder Sie können den privaten Schlüssel der Zertifikate nicht exportieren, was erforderlich ist.  

Fordern Sie Version 2 des Schlüsselanbietertyps an, wenn Sie eine Zertifikatsignieranforderung generieren. Es werden nur Version 2-Zertifikate unterstützt.  

> [!TIP]  
> Wenn wir das CMG bereitstellen, installieren wir zur gleichen Zeit auch einen Cloudverteilungspunkt (Cloud Distribution Point, CDP). Wenn Sie ein CMG bereitstellen, ist standardmäßig die Option **Verwendung dieses Diensts als Cloudverteilungspunkt und zum Verarbeiten von Inhalt aus Azure Storage zulassen** ausgewählt. Wenn Sie den CDP zusammen mit dem CMG auf dem Server platzieren, sind keine separaten Zertifikate und Konfigurationen zur Unterstützung des CDP notwendig. Obwohl der CDP nicht notwendig ist, um die Co-Verwaltung zu verwenden, ist er in den meisten Umgebungen hilfreich.  
>
> Wenn Sie zusätzliche, separate CDPs verwenden, müssen Sie für jeden weiteren CDP separate Anforderungen anfordern. Verwenden Sie zum Anfordern eines öffentlichen Zertifikats für ein CDP die gleichen Details wie für die Zertifikatsignieranforderung für das Cloudverwaltungsgateway. Sie müssen nur den allgemeinen Namen ändern, damit er für jeden CDP eindeutig ist.
>
> Die Verwendung eines zusätzlichen, separaten CDP ist veraltet und wird nicht mehr empfohlen. Weitere Informationen finden Sie unter [Veraltete Features](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features).

#### <a name="details-for-the-cloud-management-gateway-csr"></a>Details für den Cloud Management Gateway-CSR

- **Allgemeiner Name**: CloudServiceNameCMG.YourCompanyPubilcDomainName.com  
Beispiel: MyCSG.contoso.com  
- **Alternativer Antragstellername**: Identisch mit dem allgemeinen Namen (Common Name, CN)  
- **Organisation**:  Der Name Ihrer Organisation  
- **Abteilung**: Ihrer Organisation gemäß  
- **Ort**: Ihrer Organisation gemäß  
- **Zustand**: Ihrer Organisation gemäß  
- **Land oder Region**: Ihrer Organisation gemäß  
- **Schlüsselgröße: 2048**  
- **Anbieter: Microsoft RSA SChannel Cryptographic Provider**  

### <a name="import-the-certificate"></a>Importieren des Zertifikats

Nachdem Sie das öffentliche Zertifikat erhalten haben, importieren Sie es in den lokalen Zertifikatspeicher des Computers, der den CSR erstellt hat. Exportieren Sie das Zertifikat dann als PFX-Datei, damit Sie es für Ihr CMG in Azure verwenden können.  

Anbieter öffentlicher Zertifikate geben in der Regel die Anweisungen für den Import des Zertifikats an. Der Prozess zum Importieren des Zertifikats sollte in etwa der folgenden Anleitung entsprechen:  

1. Suchen Sie auf dem Computer, zu dem das Zertifikat importiert werden soll, die Zertifikat-PFX-Datei.  

2. Klicken Sie mit der rechten Maustaste auf die Datei, und wählen Sie dann **PFX installieren** aus.  

3. Wenn der Zertifikatimport-Assistent gestartet wird, wählen Sie **Weiter** aus.  

4. Wählen Sie auf der Seite **Zu importierende Datei** die Option **Weiter** aus.

5. Geben Sie auf der Seite **Kennwort** das Kennwort für den privaten Schlüssel in das Feld „Kennwort“ ein, und wählen Sie dann **Weiter** aus.  
  
   Wählen Sie die Option aus, damit der Schlüssel exportiert werden kann.

6. Wählen Sie auf der Seite **Zertifikatspeicher** die Option **Zertifikatspeicher automatisch auswählen (auf dem Zertifikattyp basierend).** und dann **Weiter** aus.  

7. Wählen Sie **Fertig stellen** aus.

### <a name="export-the-certificate"></a>Exportieren des Zertifikats

Exportieren Sie das *CMG-Serverauthentifizierungszertifikat* von Ihrem Server. Nach erneutem Exportieren kann das Zertifikat für Ihr Cloud Management Gateway in Azure genutzt werden.  

1. Führen Sie auf dem Server, zu dem Sie das öffentliche SSL-Zertifikat importiert haben, **certlm.msc** zum Öffnen der Zertifikat-Manager-Konsole aus.  

2. Wählen Sie in der Zertifikat-Manager-Konsole **Persönlich > Zertifikate** aus. Klicken Sie dann mit der rechten Maustaste auf das *CMG-Serverauthentifizierungszertifikat*, das Sie im vorherigen Verfahren registriert haben, und wählen Sie dann **Alle Aufgaben > Exportieren** aus.  

3. Wählen Sie im Assistenten zum Exportieren von Zertifikaten **Weiter**, **Ja, privaten Schlüssel exportieren** und dann **Weiter** aus.  

4. Wählen Sie auf der Seite „Exportdateiformat“ **Privater Informationsaustausch – PKCS #12 (.PFX)** und **Weiter** aus, und geben Sie ein Kennwort an. Geben Sie als Dateinamen einen Namen wie **C:\ConfigMgrCloudMGServer** an. Sie müssen bei der Erstellung des CMG in Azure auf diese Datei verweisen.  

5. Wählen Sie **Weiter** aus, und bestätigen Sie die folgenden Einstellungen vor der Auswahl von **Fertig stellen**, um den Export abzuschließen:  

   - Schlüssel exportieren = Ja  
   - Alle Zertifikate im Zertifizierungspfad einbeziehen = Ja  
   - Dateiformat = Privater Informationsaustausch (*.pfx)  

6. Legen Sie nach Abschluss des Exports eine Kopie der PFX-Datei in **C:\Certs** auf dem primären Configuration Manager-Standortserver ab, der internetbasierte Clients verwaltet. Der Ordner „Certs“ ist ein temporärer Ordner, der beim Verschieben von Zertifikaten zwischen Servern verwendet wird. Sie greifen vom primären Standortserver aus auf die Zertifikatdatei zu, wenn Sie das Cloud Management Gateway zu Azure bereitstellen.  

Nachdem Sie das Zertifikat auf den primären Standortserver kopiert haben, können Sie das Zertifikat aus dem Speicher für persönliche Zertifikate auf dem Mitgliedsserver löschen.

## <a name="enable-azure-cloud-services-in-configuration-manager"></a>Aktivieren von Azure-Clouddiensten in Configuration Manager

Um Azure-Dienste in der Configuration Manager-Konsole konfigurieren zu können, verwenden Sie den Assistenten zum Konfigurieren von Azure-Diensten und erstellen zwei Azure Active Directory-Apps (Azure AD).  

- **Server-App** – eine *Web-App* in Azure AD  
- **Client-App** – eine *Native Client*-App in Azure AD  

Führen Sie das folgende Verfahren auf dem primären Standortserver aus.  

1. Öffnen Sie auf dem primären Standortserver die Configuration Manager-Konsole, wechseln Sie zu **Verwaltung > Clouddienste > Azure-Dienste**, und wählen Sie **Azure-Dienste konfigurieren** aus.  

   Geben Sie auf der Seite „Azure-Dienst konfigurieren“ einen Anzeigenamen für den Cloudverwaltungsdienst ein, den Sie konfigurieren. Beispiel: *Mein Cloudverwaltungsdienst*.

   Wählen Sie dann **Cloudverwaltung** und **Weiter** aus.  

   > [!TIP]  
   > Weitere Informationen zu den Konfigurationen, die Sie im Assistenten vornehmen, finden Sie unter [Starten des Assistenten für Azure-Dienste](../core/servers/deploy/configure/Azure-services-wizard.md#start-the-azure-services-wizard)

2. Wählen Sie auf der Seite **App-Eigenschaften** für **Web-App** die Option **Durchsuchen**, um das Dialogfeld **Server-App** zu öffnen, und dann **Erstellen** aus. Konfigurieren Sie die folgenden Felder:

   - **Anwendungsname**: Geben Sie einen Anzeigenamen für die App an, wie z.B. *Web-App zur Cloudverwaltung*.  

   - **URL für Startseite**: Dieser Wert wird nicht von Configuration Manager verwendet, ist jedoch für Azure AD erforderlich. Der Standardwert ist `https://ConfigMgrService`.  

   - **App-ID-URI**: Dieser Wert muss bei Ihrem Azure AD-Mandanten eindeutig sein. Es handelt sich dabei um das Zugriffstoken, das der Configuration Manager-Client verwendet, um Zugriff auf den Dienst anzufordern. Der Standardwert ist `https://ConfigMgrService`.  

   Wählen Sie als Nächstes **Anmelden** aus, und geben Sie ein Konto für einen globalen Azure AD-Administrator an. Diese Anmeldeinformationen werden nicht in Configuration Manager gespeichert. Für diese Persona sind keine Berechtigungen in Configuration Manager erforderlich. Zudem muss das Konto nicht mit dem Konto identisch sein, auf dem der Assistent für Azure-Dienste ausgeführt wird.

   Nachdem Sie sich angemeldet haben, werden die Ergebnisse angezeigt. Wählen Sie **OK** aus, um das Dialogfeld „Serveranwendung erstellen“ zu schließen, und kehren Sie zur Seite „App-Eigenschaften“ zurück.

3. Wählen Sie für **Native Client-App** die Option **Durchsuchen** zum Öffnen des **Client-App**-Dialogfelds aus.

4. Wählen Sie **Erstellen** zum Öffnen des **Clientanwendung erstellen**-Dialogfelds aus, und konfigurieren Sie dann die folgenden Felder:  

   - **Anwendungsname**: Geben Sie einen Anzeigenamen für die App an, wie z.B. *Native Client-App zur Cloudverwaltung*.

   - **Antwort-URL**: Dieser Wert wird nicht von Configuration Manager verwendet, ist jedoch für Azure AD erforderlich. Der Standardwert ist `https://ConfigMgrClient`.
   Wählen Sie als Nächstes **Anmelden** aus, und geben Sie ein Konto für einen globalen Azure AD-Administrator an. Wie bei der Web-App werden diese Anmeldeinformationen nicht gespeichert und erfordern keine Berechtigungen in Configuration Manager.

   Nachdem Sie sich angemeldet haben, werden die Ergebnisse angezeigt. Wählen Sie **OK** aus, um das Dialogfeld „Clientanwendung erstellen“ zu schließen, und kehren Sie zur Seite „App-Eigenschaften“ zurück. Wählen Sie dann **Weiter** aus, um den Vorgang fortzusetzen.

5. Aktivieren Sie auf der Seite **Ermittlungseinstellungen konfigurieren** das Kontrollkästchen für **Azure Active Directory-Benutzerermittlung aktivieren**, wählen Sie **Weiter** aus, und stellen Sie dann die Konfiguration der Ermittlungsdialogfelder für Ihre Umgebung fertig.  

6. Fahren Sie mit den Seiten „Zusammenfassung“, „Fortschritt“ und „Fertigstellung“ fort, und schließen Sie dann den Assistenten.  

   Azure-Dienste für die Azure AD-Benutzerermittlung sind jetzt in Configuration Manager aktiviert.  Lassen Sie die Konsole jetzt geöffnet.  

7. Öffnen Sie einen Browser, und melden Sie sich beim [Azure-Portal](https://portal.azure.com/) an.  

8. Wählen Sie **Alle Dienste > Azure Active Directory > App-Registrierungen** aus, und tun Sie dann Folgendes:

   1. Wählen Sie die Web-App aus, die Sie erstellt haben.

   2. Navigieren Sie zu **API-Berechtigungen**. Klicken Sie auf die Option **Administratorzustimmung für <your tenant> erteilen** und dann auf **Ja**.  

   3. Wählen Sie die Native Client-App aus, die Sie erstellt haben.

   4. Navigieren Sie zu **API-Berechtigungen**. Klicken Sie auf die Option **Administratorzustimmung für <your tenant> erteilen** und dann auf **Ja**.

9. Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung > Übersicht > Clouddienste > Azure-Dienste**, und wählen Sie Ihren Azure-Dienst aus. Klicken Sie dann mit der rechten Maustaste auf **Azure Active Directory-Benutzerermittlung**, und wählen Sie **Vollständige Ermittlung jetzt ausführen** aus. Wählen Sie zum Bestätigen der Aktion **Ja** aus.  

10. Öffnen Sie auf dem primären Standortserver **SMS_AZUREAD_DISCOVERY_AGENT.log** von Configuration Manager, und suchen Sie nach dem folgenden Eintrag, um zu bestätigen, dass die Ermittlung funktioniert:  *UDX für Azure Active Directory-Benutzer erfolgreich veröffentlicht*  

    Die Protokolldatei liegt standardmäßig in *%Program_Files%\Microsoft Configuration Manager\Logs*.  

## <a name="create-the-cloud-services-in-azure"></a>Erstellen von Clouddiensten in Azure

**In diesem Abschnitt des Tutorials führen Sie Folgendes durch**:

- Erstellen des CMG-Clouddiensts  
- Erstellen der DNS CNAME-Einträge für beide Dienste  

### <a name="create-the-cmg"></a>Erstellen des CMG

Verwenden Sie dieses Verfahren zum Installieren eines Cloud Management Gateway als Dienst in Azure. Das CMG wird auf dem Standort auf der obersten Ebene der Hierarchie installiert. In diesem Tutorial verwenden wir weiterhin den primären Standort, wo Zertifikate registriert und exportiert wurden.

1. Öffnen Sie auf dem primären Standortserver die Configuration Manager-Konsole, gehen Sie zu **Verwaltung > Übersicht > Clouddienste > Cloud Management Gateway**, und wählen Sie dann **Cloud Management Gateway erstellen** aus.  

2. Gehen Sie auf der Seite **Allgemein** wie folgt vor:  

   1. Wählen Sie Ihre Cloudumgebung für **Azure-Umgebung** aus. Dieses Tutorial verwendet **AzurePublicCloud**.  

   2. Wählen Sie **Azure Resource Manager-Bereitstellung** aus.  
  
   3. **Melden** Sie sich bei Ihrem Azure-Abonnement an. Configuration Manager trägt anhand der Informationen, die Sie beim Aktivieren der Azure-Clouddienste für Configuration Manager konfiguriert haben, zusätzliche Informationen ein.  

   Wählen Sie **Weiter** aus, um den Vorgang fortzusetzen.  

3. Navigieren Sie auf der Seite **Einstellungen** zu der Datei mit dem Namen **ConfigMgrCloudMGServer.pfx**, und wählen Sie sie aus; dies ist die Datei, die Sie nach dem Importieren des CMG-Serverauthentifizierungszertifikats exportiert haben. Nachdem Sie das Kennwort angeben haben, werden **Dienstname** und **Bereitstellungsname** basierend auf den Details in der PFX-Datei automatisch ausgefüllt.

4. Legen Sie Ihre **Region** fest.

5. Verwenden Sie für **Ressourcengruppe** eine vorhandene Ressourcengruppe, oder erstellen Sie eine Gruppe mit einem Anzeigenamen ohne Leerzeichen, z.B. **CofigMgrCloudServices**. Wenn Sie eine Gruppe erstellen möchten, wird die Gruppe als Ressourcengruppe in Azure hinzugefügt.  

6. Sofern Sie beim Konfigurieren nicht skalieren, verwenden Sie eins (1) für die Anzahl der **VM-Instanzen**. Über die Anzahl der VM-Instanzen kann ein einzelner Cloud Management Gateway-Clouddienst (CMG) aufskalieren, um weitere Clientverbindungen zu unterstützen. Später können Sie in der Configuration Manager-Konsole zurückkehren und die Anzahl der VM-Instanzen bearbeiten, die Sie verwenden.  

7. Aktivieren Sie das Kontrollkästchen **Clientzertifikatsperre überprüfen**.

8. Aktivieren Sie das Kontrollkästchen **Verwendung dieses Diensts als Cloudverteilungspunkt und zum Verarbeiten von Inhalt aus Azure Storage zulassen**, wenn Sie einen Cloudverteilungspunkt mit dem CMG bereitstellen möchten.

9. Wählen Sie **Weiter** aus, um den Vorgang fortzusetzen.

10. Überprüfen Sie die Werte auf der Seite **Warnung**, und wählen Sie dann **Weiter** aus.

11. Überprüfen Sie die Seite **Zusammenfassung**, und klicken Sie auf **Weiter**, um den Cloud Management Gateway-Clouddienst zu erstellen. Wählen Sie **Schließen** aus, um den Assistenten abzuschließen.  

12. Im Cloud Management Gateway-Knoten der Configuration Manager-Konsole wird jetzt der neue Dienst angezeigt.  

### <a name="create-dns-cname-records"></a>Erstellen von DNS-CNAME-Einträgen

Wenn Sie einen DNS-Eintrag für das CMG erstellen, können Sie Ihren Windows 10-Geräten ermöglichen, sowohl innerhalb als auch außerhalb des Unternehmensnetzwerks mit der Namensauflösung den CMG-Clouddienst in Azure zu finden.

Unser CNAME-Eintragsbeispiel verwendet die folgenden Details:  

- Der Unternehmensname ist **Contoso** mit dem öffentlichen DNS-Namespace ***Contoso.com***.  

- Der CMG-Dienstname ist **MyCMG**, der in Azure zu ***MyCMG.CloudApp.Net*** wird.  

CNAME-Eintragsbeispiel: *MyCMG.contoso.com => My.cloudapp.net*

## <a name="configure-the-management-point-and-clients-to-use-the-cmg"></a>Konfigurieren von Verwaltungspunkt und Clients zum Verwenden des CMG

Konfigurieren Sie Einstellungen, die lokalen Verwaltungspunkten und Clients die Verwendung von Cloud Management Gateway ermöglichen.

Da wir erweitertes HTTP für die Clientkommunikation verwenden, ist es nicht erforderlich, einen HTTPS-Verwaltungspunkt zu verwenden.  

### <a name="create-the-cmg-connection-point"></a>Erstellen des CMG-Verbindungspunkts

Konfigurieren Sie den Standort für die Unterstützung von erweitertem HTTP.  

1. Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung > Übersicht > Standortkonfiguration > Standorte**, und öffnen Sie die Eigenschaften des primären Standorts.  

2. Wählen Sie auf der Registerkarte **Clientcomputerkommunikation** die Option *HTTPS oder HTTP* für **Verwenden von vom Configuration Manager generierten Zertifikaten für HTTP-Standortsysteme** aus, und wählen Sie dann **OK** aus, um die Konfiguration zu speichern.

    > [!Note]
    > Ab Version 1906 heißt diese Registerkarte **Sichere Kommunikation**.<!-- SCCMDocs#1645 -->  

3. Wechseln Sie nun zu **Verwaltung > Übersicht > Standortkonfiguration > Server und Standortsystemrollen**, und wählen Sie den Server mit einem Verwaltungspunkt aus, wo Sie den Verbindungspunkt zum Cloud Management Gateway installieren möchten.  

4. Wählen Sie **Standortsystemrollen hinzufügen** und dann **Weiter**> **Weiter** aus.  

5. Wählen Sie den **Verbindungspunkt für Cloudverwaltungsgateway** und dann **Weiter** aus, um den Vorgang fortzusetzen.  

6. Überprüfen Sie die Standardeinstellungen auf der Seite **Verbindungspunkt für Cloudverwaltungsgateway**, und stellen Sie sicher, dass das richtige CMG aktiviert ist. Wenn Sie über mehrere Cloud Management Gateways verfügen, können Sie mit der Dropdownliste ein anderes CMG angeben. Sie können das verwendete CMG auch nach der Installation ändern. Wählen Sie **Weiter** aus, um den Vorgang fortzusetzen.

7. Wählen Sie **Weiter** aus, um die Installation zu starten und dann die Ergebnisse auf der Seite „Fertigstellung“ anzuzeigen.  Wählen Sie **Schließen** zum Fertigstellen der Installation des Verbindungspunkts aus.

8. Wechseln Sie nun zu **Verwaltung > Übersicht > Standortkonfiguration > Server und Standortsystemrollen**, und öffnen Sie die **Eigenschaften** des Verwaltungspunkts, wo Sie den Verbindungspunkt installiert haben. Aktivieren Sie auf der Registerkarte **Allgemein** das Kontrollkästchen für **Datenverkehr über Configuration Manager-Cloudverwaltungsgateway zulassen**, und wählen Sie dann **OK** zum Speichern der Konfiguration aus.
   > [!TIP]  
   > Obwohl es zum Aktivieren der Co-Verwaltung nicht erforderlich ist, sollten Sie dieselbe Bearbeitung für alle Softwareupdatepunkte durchführen.

### <a name="configure-client-settings-to-direct-clients-to-use-the-cmg"></a>Konfigurieren von Clienteinstellungen zur Weiterleitung von Clients zur Verwendung des CMG

Verwenden Sie Clienteinstellungen, um Configuration Manager-Clients für die Kommunikation mit dem CMG zu konfigurieren.  

1. Öffnen Sie **Configuration Manager-Konsole > Verwaltung > Übersicht > Clienteinstellungen**, und bearbeiten Sie dann die **Clientstandardeinstellungen**.  

2. Wählen Sie **Clouddienste** aus.

3. Legen Sie auf der Seite **Standardeinstellungen** für die folgenden Einstellungen **Ja** fest.  

   - **Registrieren Sie neue, in die Domäne eingebundene Windows 10-Geräte automatisch bei Azure Active Directory.**  

   - **Ermöglichen Sie Clients die Verwendung eines Cloudverwaltungsgateways.**

   - **Zugriff auf Cloudverteilungspunkt zulassen**

4. Legen Sie auf der Seite **Clientrichtlinie** die Option **Benutzerrichtlinienanforderungen von Internetclients aktivieren** auf  = **Ja** fest.

5. Klicken Sie auf **OK**, um diese Konfiguration zu speichern.

## <a name="enable-co-management-in-configuration-manager"></a>Aktivieren der Co-Verwaltung in Configuration Manager

Mit den vorhandenen Azure-Konfigurationen, Standortsystemrollen und Clienteinstellungen können Sie Configuration Manager zum Aktivieren der Co-Verwaltung konfigurieren. Allerdings müssen Sie immer noch einige Konfigurationen in Intune vornehmen, nachdem Sie die Co-Verwaltung aktiviert haben, bevor dieses Tutorial abgeschlossen ist. Eine dieser Aufgaben ist das Konfigurieren von Intune zum Bereitstellen des Configuration Manager-Clients. Diese Aufgabe wird durch das Speichern der Befehlszeile für die Clientbereitstellung vereinfacht, die im Assistenten zur Konfiguration der Co-Verwaltung verfügbar ist. Darum aktivieren wir die Co-Verwaltung jetzt, bevor wir die Konfigurationen für Intune fertig stellen.

> [!TIP]
> - Wenn Sie die Co-Verwaltung aktivieren, weisen Sie eine Sammlung als *Pilotgruppe*zu. Dies ist eine Gruppe, die eine kleine Anzahl von Clients enthält, um Ihre Co-Verwaltungskonfigurationen zu testen. Wir empfehlen Ihnen, vor Beginn des Verfahrens eine geeignete Sammlung anzulegen. Dann können Sie diese Sammlung auswählen, ohne das Verfahren zu beenden.
> - Ab Configuration Manager, Version 1906 benötigen Sie u. U. mehrere Sammlungen, da Sie für jede Workload eine andere *Pilotgruppe* zuweisen können.

### <a name="enable-co-management-starting-in-version-1906"></a>Aktivieren von Co-Verwaltung ab Version 1906

Befolgen Sie zum Aktivieren von Co-Verwaltung ab Configuration Manager, Version 1906 die unten stehenden Anweisungen:

[!INCLUDE [Enable Co-management in version 1906 and later](includes/enable-co-management-1906-and-higher.md)]

### <a name="enable-co-management-in-version-1902-and-earlier"></a>Aktivieren von Co-Verwaltung in Version 1902 und früher

Befolgen Sie zum Aktivieren von Co-Verwaltung für Configuration Manager, Version 1902 und früher die unten stehenden Anweisungen:

[!INCLUDE [Enable Co-management in version 1902 and earlier](includes/enable-co-management-1902-and-earlier.md)]

## <a name="use-intune-to-deploy-the-configuration-manager-client"></a>Verwenden von Intune zum Bereitstellen des Configuration Manager-Clients

Sie können Intune verwenden, um den Configuration Manager-Client auf Windows 10-Geräten zu installieren, die derzeit nur mit Intune verwaltet werden.  

Wenn dann ein zuvor nicht verwaltetes Windows 10-Gerät bei Intune registriert wird, installiert es automatisch den Configuration Manager-Client.

### <a name="create-an-intune-app-to-install-the-configuration-manager-client"></a>Erstellen einer Intune-App zum Installieren des Configuration Manager-Clients

1. Melden Sie sich auf dem primären Standortserver im [Microsoft Endpoint Manager Admin Center](https://endpoint.microsoft.com) an, und navigieren Sie zu **Anwendungen** > **Alle Apps** > **Hinzufügen**.

2. Wählen Sie unter **Sonstige** für den App-Typ die Option **Branchenspezifische App** aus.

3. Navigieren Sie zum Speicherort der Configuration Manager-Datei **ccmsetup.msi**, und klicken Sie dann auf **Öffnen > OK**, um zur **App-Paketdatei** zu gelangen.
Beispiel: *C:\Programme\Microsoft Configuration Manager\bin\i386\ccmsetup.msi*.

4. Wählen Sie **App-Informationen** aus, und geben Sie dann die folgenden Details an:
   - **Beschreibung:** Configuration Manager-Client  

   - **Herausgeber**: Microsoft  

   - **Befehlszeilenargumente**: *\<Specify the **CCMSETUPCMD** command line. You can use the command line you saved from the* Enablement *page of the Co-management Configuration Wizard. This command line includes the names of your cloud service and additional values that enable devices to install the Configuration Manager client software.>*  

     Die Befehlszeilenstruktur sollte diesem Beispiel entsprechen und nur die Parameter CCMSETUPCMD und SMSSiteCode verwenden:  

     ``` Command
     CCMSETUPCMD="CCMHOSTNAME=<ServiceName.CLOUDAPP.NET/CCM_Proxy_MutualAuth/<GUID>" SMSSiteCode="<YourSiteCode>"  
     ```

     > [!TIP]  
     > Wenn Sie nicht über die Befehlszeile verfügen, können Sie die Eigenschaften von *CoMgmtSettingsProd* in der Configuration Manager-Konsole anzeigen, um eine Kopie der Befehlszeile zu erhalten.

5. Klicken Sie auf **OK > Hinzufügen**.  Die App wird erstellt und in der Intune-Konsole zur Verfügung gestellt. Nachdem die App verfügbar ist, können Sie Intune im folgenden Abschnitt für die Zuweisung zu Windows 10-Geräten konfigurieren.

### <a name="assign-the-intune-app-to-install-the-configuration-manager-client"></a>Zuweisen der Intune-App zum Installieren des Configuration Manager-Clients

Im folgenden Verfahren wird die App für die Installation des Configuration Manager-Clients bereitgestellt, den Sie im vorherigen Verfahren erstellt haben.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://endpoint.microsoft.com) an. Klicken Sie auf **Anwendungen** > **Alle Apps**, und wählen Sie **ConfigMgr Client Setup Bootstrap** aus. Dabei handelt es sich um die App, die Sie erstellt haben, um den Configuration Manager-Client bereitzustellen.  

2. Wählen Sie **Eigenschaften**, dann bei **Zuweisungen** die Option **Bearbeiten** aus. Klicken Sie bei den Zuweisungen des Typs **Erforderlich** auf **Gruppe hinzufügen**, um die Azure Active Directory-Gruppen (AD) festzulegen, die Benutzer und Geräte enthalten, die Sie in die Co-Verwaltung einbeziehen möchten.  

3. Klicken Sie auf **Überprüfen und speichern**, und **speichern** Sie die Konfiguration.
Die App wird jetzt von Benutzern und Geräten benötigt, denen Sie sie zugewiesen haben. Nachdem die App den Configuration Manager-Client auf einem Gerät installiert hat, wird es mit der Co-Verwaltung verwaltet.

## <a name="summary"></a>Zusammenfassung

Wenn Sie die Konfigurationsschritte in diesem Tutorial abgeschlossen haben, können Sie mit der Verwendung der Co-Verwaltung für Ihre Geräte beginnen.

## <a name="next-steps"></a>Nächste Schritte

- Überprüfen des Status von Geräten, für die eine Co-Verwaltung durchgeführt wird, über das [Dashboard für die Co-Verwaltung](how-to-monitor.md)
- Verwendung von [Windows Autopilot](quickstart-autopilot.md) zum Bereitstellen neuer Geräte
- Verwenden von Regeln für den [bedingten Zugriff](quickstart-conditional-access.md) und Intune Compliance zum Verwalten des Benutzerzugriffs auf Unternehmensressourcen
