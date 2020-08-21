---
title: Konfigurieren der Zertifikatinfrastruktur
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie die Zertifikatregistrierung in Configuration Manager konfigurieren.
ms.date: 07/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 29ae59b7-2695-4a0f-a9ff-4f29222f28b3
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 656cc80c929eb7e829dd06b642a83cb174d3b0c8
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697244"
---
# <a name="configure-certificate-infrastructure"></a>Konfigurieren der Zertifikatinfrastruktur

*Gilt für: Configuration Manager (Current Branch)*

Erfahren Sie, wie Sie die Zertifikatinfrastruktur in Configuration Manager konfigurieren. Bevor Sie beginnen, überprüfen Sie die unter [Voraussetzungen für Zertifikatprofile](../../protect/plan-design/prerequisites-for-certificate-profiles.md) aufgeführten Voraussetzungen.  

Folgen Sie diesen Schritten, um Ihre Infrastruktur für SCEP- oder PFX-Zertifikate zu konfigurieren.

## <a name="step-1---install-and-configure-the-network-device-enrollment-service-and-dependencies-for-scep-certificates-only"></a>Schritt 1: Installieren und Konfigurieren des Registrierungsdiensts für Netzwerkgeräte und der Abhängigkeiten (nur für SCEP-Zertifikate)

 Sie müssen den Rollendienst „Registrierungsdienst für Netzwerkgeräte“ für Active Directory-Zertifikatdienste (AD CS) installieren und konfigurieren, die Sicherheitsberechtigungen für die Zertifikatvorlagen ändern, ein PKI-Zertifikat (Public Key Infrastructure) zur Clientauthentifizierung bereitstellen und die Registrierung bearbeiten, um das standardmäßige URL-Größenlimit für IIS anzuheben. Bei Bedarf müssen Sie zudem die ausstellende Zertifizierungsstelle so konfigurieren, dass ein benutzerdefinierter Gültigkeitszeitraum zulässig ist.  

> [!IMPORTANT]  
>  Überprüfen Sie die Installation und Konfiguration des Registrierungsdiensts für Netzwerkgeräte (Network Device Enrollment Service, NDES), bevor Sie Configuration Manager für den Registrierungsdienst für Netzwerkgeräte konfigurieren. Wenn diese Abhängigkeiten nicht ordnungsgemäß funktionieren, wird die Problembehandlung bei der Zertifikatregistrierung mit Configuration Manager erschwert.  

### <a name="to-install-and-configure-the-network-device-enrollment-service-and-dependencies"></a>So installieren und konfigurieren Sie den Registrierungsdienst für Netzwerkgeräte und die Abhängigkeiten  

1. Installieren und konfigurieren Sie auf einem Server unter Windows Server 2012 R2 den Rollendienst „Registrierungsdienst für Netzwerkgeräte“ für die Serverrolle „Active Directory-Zertifikatdienste“. Weitere Informationen finden Sie im [Leitfaden zum Registrierungsdienst für Netzwerkgeräte](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498\(v=ws.11\)).

2. Überprüfen Sie die Sicherheitsberechtigungen für die Zertifikatvorlagen, die vom Registrierungsdienst für Netzwerkgeräte verwendet werden, und ändern Sie sie bei Bedarf:  

   -   Für das Konto, mit dem die Configuration Manager-Konsole ausgeführt wird: Berechtigung **Lesen**.  

        Diese Berechtigung ist erforderlich, damit Sie während der Ausführung des Assistenten zum Erstellen von Zertifikatprofilen die Zertifikatvorlage suchen und auswählen können, die Sie bei der Erstellung eines SCEP-Einstellungsprofils verwenden möchten. Durch die Auswahl einer Zertifikatvorlage werden einige Einstellungen im Assistenten automatisch festgelegt. Sie müssen also weniger Einstellungen konfigurieren, und die Gefahr, dass Sie Einstellungen auswählen, die mit den vom Registrierungsdienst für Netzwerkgeräte verwendeten Zertifikatvorlagen nicht kompatibel sind, wird verringert.  

   -   Für das SCEP-Dienstkonto (Simple Certificate Enrollment-Protokoll), das vom Anwendungspool des Registrierungsdiensts für Netzwerkgeräte verwendet wird: die Berechtigungen **Lesen** und **Anmelden**.  

        Diese Anforderung gilt nicht nur für Configuration Manager, sondern ist Bestandteil der Konfiguration des Registrierungsdiensts für Netzwerkgeräte. Weitere Informationen finden Sie im [Leitfaden zum Registrierungsdienst für Netzwerkgeräte](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831498\(v=ws.11\)).  

   > [!TIP]  
   >  Die vom Registrierungsdienst für Netzwerkgeräte verwendeten Zertifikatvorlagen sind unter dem folgenden Registrierungsschlüssel auf dem Server angegeben, auf dem der Registrierungsdienst für Netzwerkgeräte ausgeführt wird: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP.  

   > [!NOTE]  
   >  Dies sind die standardmäßigen Sicherheitsberechtigungen, die für die meisten Umgebungen geeignet sind. Sie können auch eine alternative Sicherheitskonfiguration verwenden. Weitere Informationen finden Sie unter [Planen der Berechtigungen von Zertifikatvorlagen für Zertifikatprofile](../../protect/plan-design/planning-for-certificate-template-permissions.md).  

3. Stellen Sie auf diesem Server ein PKI-Zertifikat bereit, das die Clientauthentifizierung unterstützt. Es ist möglich, dass bereits ein geeignetes Zertifikat auf dem Computer installiert ist, das Sie verwenden können. Möglicherweise müssen (oder möchten) Sie aber auch ein Zertifikat speziell für diesen Zweck bereitstellen. Weitere Informationen zu den Anforderungen für dieses Zertifikat finden Sie im Thema [PKI-Zertifikatanforderungen für Configuration Manager](../../core/plan-design/network/pki-certificate-requirements.md) im Abschnitt **PKI-Zertifikate für Server**. Lesen Sie dort die Details zu Servern, auf denen das Configuration Manager-Richtlinienmodul mit dem Rollendienst „Registrierungsdienst für Netzwerkgeräte“ ausgeführt wird.  

   > [!TIP]
   >  Falls Sie Hilfe bei der Bereitstellung dieses Zertifikats benötigen, können Sie die Anweisungen unter [Bereitstellen des Clientzertifikats für Verteilungspunkte](../../core/plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012) verwenden, da die Zertifikatanforderungen mit einer einzigen Ausnahme identisch sind:  
   > 
   > - Aktivieren Sie nicht das Kontrollkästchen **Exportieren von privatem Schlüssel zulassen** auf der Registerkarte **Anforderungsverarbeitung** der Eigenschaften der Zertifikatvorlage.  
   > 
   >   Sie müssen dieses Zertifikat nicht mit dem privaten Schlüssel exportieren, weil Sie im lokalen Computerspeicher danach suchen und es auswählen können, wenn Sie das Configuration Manager-Richtlinienmodul konfigurieren.  

4. Suchen Sie das Stammzertifikat, mit dem das Clientauthentifizierungszertifikat verkettet ist. Exportieren Sie dann dieses Zertifikat der Stammzertifizierungsstelle in eine CER-Zertifikatdatei. Speichern Sie diese Datei an einem sicheren Speicherort, auf den Sie sicher zugreifen können, wenn Sie zu einem späteren Zeitpunkt den Standortsystemserver für den Zertifikatregistrierungspunkt installieren und konfigurieren.  

5. Verwenden Sie auf dem gleichen Server den Registrierungs-Editor, um das standardmäßige URL-Größenlimit für IIS anzuheben. Hierzu legen Sie die DWORD-Werte des folgenden Registrierungsschlüssels unter HKEY_LOCAL_MACHINE\System\CurrentControlSet\Services\HTTP\Parameters fest:  

   - Legen Sie den Schlüssel **MaxFieldLength** auf **65534**fest.  

   - Legen Sie den Schlüssel **MaxRequestBytes** auf **16777216**fest.  

     Weitere Informationen finden Sie im Microsoft-Support-Artikel [820129: Http.sys-Registrierungseinstellungen für Windows](https://support.microsoft.com/help/820129).

6. Ändern Sie auf dem gleichen Server im IIS-Manager (Internet Information Services, Internetinformationsdienste) die Einstellungen für die Anforderungsfilterung für die Anwendung /certsrv/mscep. Starten Sie dann den Server neu. Im Dialogfeld **Einstellungen für die Anforderungsfilterung bearbeiten** sollten die Einstellungen unter **Anforderungslimits** wie folgt lauten:  

   - **Maximal zulässige Inhaltslänge (Bytes)** : **30000000**  

   - **Maximale URL-Länge (Bytes)** : **65534**  

   - **Maximale Länge einer Abfragezeichenfolge (Bytes)** : **65534**  

     Weitere Informationen zu diesen Einstellungen und deren Konfiguration finden Sie unter [Anforderungslimits](/iis/configuration/system.webServer/security/requestFiltering/requestLimits/).

7. Wenn Sie ein Zertifikat mit einem kürzeren Gültigkeitszeitraum als dem der verwendeten Zertifikatvorlage anfordern möchten, gilt: Diese Konfiguration ist für eine Unternehmenszertifizierungsstelle standardmäßig deaktiviert. Sie können diese Option für eine Unternehmenszertifizierungsstelle mit dem Befehlszeilentool „Certutil“ aktivieren. Verwenden Sie dann die folgenden Befehle, um den Zertifikatdienst zu beenden und neu zu starten:  

   1. **certutil ‒ setreg Richtlinie\EditFlags +EDITF_ATTRIBUTEENDDATE**  

   2. **net stop certsvc**  

   3. **net start certsvc**  

      Weitere Informationen finden Sie unter [Tools und Einstellungen der Zertifikatdienste](/previous-versions/windows/it-pro/windows-server-2003/cc780742\(v=ws.10\)).

8. Verwenden Sie den folgenden Link als Beispiel, um zu überprüfen, ob der Registrierungsdienst für Netzwerkgeräte funktioniert: `https://server.contoso.com/certsrv/mscep/mscep.dll`. Es sollte die integrierte Webseite „Registrierungsdienst für Netzwerkgeräte“ angezeigt werden. Auf dieser Webseite wird der Dienst erläutert, und Sie erfahren, dass Netzwerkdienste die URL zum Übermitteln von Zertifikatanforderungen verwenden.  

   Nachdem Sie den Registrierungsdienst für Netzwerkgeräte und die Abhängigkeiten konfiguriert haben, können Sie den Zertifikatregistrierungspunkt installieren und konfigurieren.


## <a name="step-2---install-and-configure-the-certificate-registration-point"></a>Schritt 2: Installieren und Konfigurieren des Zertifikatregistrierungspunkts.

Sie müssen mindestens einen Zertifikatregistrierungspunkt in der Configuration Manager-Hierarchie installieren und konfigurieren. Dann können Sie diese Standortsystemrolle am Standort der zentralen Verwaltung oder an einem primären Standort installieren.  

> [!IMPORTANT]  
>  Lesen Sie vor der Installation des Zertifikatregistrierungspunkts die Informationen zu Betriebssystemanforderungen und -abhängigkeiten für den Zertifikatregistrierungspunkt im Abschnitt **Anforderungen an das Standortsystem** des Themas [Unterstützte Konfigurationen für Configuration Manager](../../core/plan-design/configs/supported-configurations.md).  

##### <a name="to-install-and-configure-the-certificate-registration-point"></a>So installieren und konfigurieren Sie den Zertifikatregistrierungspunkt  

1. Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2. Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standortkonfiguration**, klicken Sie auf **Server und Standortsystemrollen**, und wählen Sie dann den Server aus, den Sie als Zertifikatregistrierungspunkt verwenden möchten.  

3. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Server** auf **Standortsystemrollen hinzufügen**.  

4. Geben Sie auf der Seite **Allgemein** die allgemeinen Einstellungen für den Standortsystemserver an, und klicken Sie dann auf **Weiter**.  

5. Klicken Sie auf der Seite **Proxy** auf **Weiter**. Für den Zertifikatregistrierungspunkt werden keine Internetproxyeinstellungen verwendet.  

6. Wählen Sie auf der Seite **Systemrollenauswahl** in der Liste der verfügbaren Rollen **Zertifikatregistrierungspunkt** aus, und klicken Sie dann auf **Weiter**. 

7. Legen Sie auf der Seite **Zertifikatregistrierungsmodus** fest, ob der Zertifikatregistrierungspunkt **SCEP-Zertifikatanforderungen verarbeiten** oder **PFX-Zertifikatanforderungen verarbeiten** soll. Ein Zertifikatregistrierungspunkt kann nicht beide Arten von Anforderungen verarbeiten, aber Sie können mehrere Zertifikatregistrierungspunkte erstellen, wenn Sie mit beiden Zertifikattypen arbeiten.

   Wenn Sie PFX-Zertifikate verarbeiten, müssen Sie als Zertifizierungsstelle entweder Microsoft oder Entrust auswählen.

8. Die Seite **Einstellungen für den Zertifikatregistrierungspunkt** ist je nach Zertifikatstyp unterschiedlich aufgebaut:
   - Wenn Sie **SCEP-Zertifikatanforderungen verarbeiten** ausgewählt haben, nehmen Sie folgende Konfiguration vor:
     -   **Websitename**, **HTTPS-Portnummer** und **Name der virtuellen Anwendung** für den Zertifikatregistrierungspunkt. Diese Felder werden automatisch mit Standardwerten ausgefüllt. 
     -   **URL für Registrierungsdienst für Netzwerkgeräte und Zertifikat der Stammzertifizierungsstelle**: Klicken Sie auf **Hinzufügen**, und geben Sie anschließend im Dialogfeld **URL und Zertifikat der Stammzertifizierungsstelle hinzufügen** Folgendes an:
         - **URL für den Registrierungsdienst für Netzwerkgeräte**: Geben Sie die URL im folgenden Format an: https:// *<Server_FQDN>* /certsrv/mscep/mscep.dll. Beispiel: Wenn der FQDN des Servers, der den Registrierungsdienst für Netzwerkgeräte ausführt, „server1.contoso.com“ lautet, geben Sie `https://server1.contoso.com/certsrv/mscep/mscep.dll` ein.
         - **Zertifikat der Stammzertifizierungsstelle**: Navigieren Sie zu der CER-Zertifikatdatei, die Sie in **Schritt 1: Installieren und Konfigurieren des Registrierungsdiensts für Netzwerkgeräte und der Abhängigkeiten** erstellt und gespeichert haben, und wählen Sie sie aus. Mit diesem Zertifikat der Stammzertifizierungsstelle kann das Clientauthentifizierungszertifikat, das vom Configuration Manager-Richtlinienmodul verwendet wird, durch den Zertifikatregistrierungspunkt überprüft werden.  

   - Wenn Sie **PFX-Zertifikatanforderungen verarbeiten** ausgewählt haben, konfigurieren Sie die Verbindungsdetails und die Anmeldeinformationen für die ausgewählte Zertifizierungsstelle.

     - Um Microsoft als Zertifizierungsstelle zu verwenden, klicken Sie auf **Hinzufügen**, und geben Sie anschließend im Dialogfeld **Zertifizierungsstelle und Konto hinzufügen** Folgendes an:
         - **Name des Zertifizierungsstellenservers**: Geben Sie den Namen Ihres Zertifizierungsstellenservers ein.
         - **Konto der Zertifizierungsstelle**: Klicken Sie auf **Festlegen**, um das Konto auszuwählen oder zu erstellen, das Berechtigungen für die Registrierung in Vorlagen an der Zertifizierungsstelle hat.
         - **Verbindungskonto für Zertifikatregistrierungspunkt**: Wählen Sie das Konto aus, das den Zertifikatregistrierungspunkt mit der Configuration Manager-Datenbank verbindet, oder erstellen Sie dieses. Alternativ können Sie auch das lokale Computerkonto des Computers verwenden, auf dem der Zertifikatregistrierungspunkt gehostet wird.
         - **Konto für Active Directory-Zertifikatveröffentlichung**: Wählen Sie ein Konto aus, das zur Veröffentlichung von Zertifikaten für Benutzerobjekte in Active Directory verwendet werden soll, oder erstellen Sie ein neues Konto.

         - Geben Sie im Dialogfeld **URL for the Network Device Enrollment and root CA certificate (URL für Registrierung für Netzwerkdienste und Zertifikat der Stammzertifizierungsstelle)** Folgendes an, und klicken Sie anschließend auf **OK**:  

     - Um Entrust als Zertifizierungsstelle zu verwenden, geben Sie Folgendes an:

       - die **MDM-Webdienst-URL**
       - den Benutzernamen und das Kennwort für die URL.

         Wenn Sie bei der Angabe der Entrust-Webdienst-URL die MDM-API benutzen, müssen Sie mindestens Version 9 der API verwenden, wie im folgenden Beispiel gezeigt wird:

         `https://entrust.contoso.com:19443/mdmws/services/AdminServiceV9`

         Entrust wird nicht von früheren Versionen der API unterstützt.

9. Klicken Sie auf **Weiter** , und schließen Sie den Assistenten ab.  

10. Warten Sie einige Minuten, bis die Installation abgeschlossen ist. Überprüfen Sie dann mit einer der folgenden Methoden, ob der Zertifikatregistrierungspunkt erfolgreich installiert wurde:  

    -   Erweitern Sie im Arbeitsbereich **Überwachung** die Option **Systemstatus**, klicken Sie auf **Komponentenstatus**, und suchen Sie nach Statusmeldungen der Komponente **SMS_CERTIFICATE_REGISTRATION_POINT** .  

    -   Verwenden Sie auf dem Standortsystemserver die Datei „ *<Configuration Manager-Installationspfad\>* \Logs\crpsetup.log“ und die Datei „ *<Configuration Manager-Installationspfad\>* \Logs\crpmsi.log“. Bei einer erfolgreichen Installation wird der Exitcode 0 zurückgegeben.  

    -   Überprüfen Sie mithilfe eines Browsers, ob Sie eine Verbindung mit der URL des Zertifikatregistrierungspunkts herstellen können. Beispiel: `https://server1.contoso.com/CMCertificateRegistration`. Es sollte eine Seite mit einem **Serverfehler** für den Anwendungsnamen mit einer HTTP 404-Beschreibung angezeigt werden.  

11. Suchen Sie nach der exportierten Zertifikatdatei für die Stammzertifizierungsstelle, die vom Zertifikatregistrierungspunkt automatisch im folgenden Ordner auf dem primären Standortservercomputer erstellt wurde: *<Configuration Manager-Installationspfad\>* \inboxes\certmgr.box. Speichern Sie diese Datei an einem sicheren Speicherort, auf den Sie zu einem späteren Zeitpunkt während der Installation des Configuration Manager-Richtlinienmoduls auf dem Server mit dem Registrierungsdienst für Netzwerkgeräte sicher zugreifen können.  

    > [!TIP]  
    >  Dieses Zertifikat steht nicht sofort in diesem Ordner zur Verfügung. Möglicherweise müssen Sie eine Weile warten (beispielsweise eine halbe Stunde), bis Configuration Manager die Datei in diesen Speicherort kopiert.  


## <a name="step-3----install-the-configuration-manager-policy-module-for-scep-certificates-only"></a>Schritt 3: Installieren des Configuration Manager-Richtlinienmoduls (nur für SCEP-Zertifikate).

Sie müssen das Configuration Manager-Richtlinienmodul auf jedem Server installieren und konfigurieren, den Sie in **Schritt 2: Installieren und Konfigurieren des Zertifikatregistrierungspunkts** als **URL für den Registrierungsdienst für Netzwerkgeräte** in den Eigenschaften des Zertifikatregistrierungspunkts angegeben haben.  

##### <a name="to-install-the-policy-module"></a>So installieren Sie das Richtlinienmodul  

1. Melden Sie sich auf dem Server mit dem Registrierungsdienst für Netzwerkgeräte als Domänenadministrator an, und kopieren Sie die folgenden Dateien aus dem Ordner „<Configuration Manager-Installationsmedium\>\SMSSETUP\POLICYMODULE\X64“ auf dem Configuration Manager-Installationsmedium in einen temporären Ordner:  

   -   PolicyModule.msi  

   -   PolicyModuleSetup.exe  

   Wenn das Installationsmedium den Ordner LanguagePack enthält, kopieren Sie auch diesen Ordner und seinen Inhalt.  

2. Führen Sie „PolicyModuleSetup.exe“ im temporären Ordner aus, um den Setup-Assistenten für das Configuration Manager-Richtlinienmodul zu starten.  

3. Klicken Sie auf der ersten Seite des Assistenten auf **Weiter**, nehmen Sie die Lizenzbedingungen an, und klicken Sie dann auf **Weiter**.  

4. Übernehmen Sie auf der Seite **Installationsordner** den standardmäßigen Installationsordner für das Richtlinienmodul, oder geben Sie einen anderen Ordner an, und klicken Sie dann auf **Weiter**.  

5. Geben Sie auf der Seite **Zertifikatregistrierungspunkt** die URL des Zertifikatregistrierungspunkts an, indem Sie den FQDN des Standortsystemservers und den Namen der virtuellen Anwendung verwenden, der in den Eigenschaften des Zertifikatregistrierungspunkts aufgeführt ist. Der Standardname der virtuellen Anwendung lautet „CMCertificateRegistration“. Beispiel: Wenn der Standortsystemserver den FQDN „server1.contoso.com“ aufweist und Sie den Standardnamen der virtuellen Anwendung verwendet haben, geben Sie `https://server1.contoso.com/CMCertificateRegistration` an.

6. Übernehmen Sie den Standardport **443** , oder geben Sie die alternative Portnummer an, die vom Zertifikatregistrierungspunkt verwendet wird. Klicken Sie dann auf **Weiter**.  

7. Navigieren Sie auf der Seite **Clientzertifikat für das Richtlinienmodul** zum Clientauthentifizierungszertifikat, das Sie in **Schritt 1: Installieren und Konfigurieren des Registrierungsdiensts für Netzwerkgeräte und der Abhängigkeiten** bereitgestellt haben, und geben Sie es an. Klicken Sie dann auf **Weiter**.  

8. Klicken Sie auf der Seite **Zertifikat für Zertifikatregistrierungspunkt** auf **Durchsuchen**, um die exportierte Zertifikatdatei für die Stammzertifizierungsstelle auszuwählen, die Sie am Ende von **Schritt 2: Installieren und Konfigurieren des Zertifikatregistrierungspunkts** gesucht und gespeichert haben.  

   > [!NOTE]  
   >  Wenn Sie diese Zertifikatdatei zuvor nicht gespeichert haben, befindet sie sich im Ordner „<Configuration Manager-Installationspfad\>\inboxes\certmgr.box“ auf dem Standortservercomputer.  

9. Klicken Sie auf **Weiter** , und schließen Sie den Assistenten ab.  

   Wenn Sie das Configuration Manager-Richtlinienmodul deinstallieren möchten, verwenden Sie hierzu die Option **Programme und Features** in der Systemsteuerung. 

 
Nachdem Sie die Konfigurationsschritte abgeschlossen haben, sind Sie für die Bereitstellung von Zertifikaten für Benutzer und Geräte mit dem Erstellen und Bereitstellen von Zertifikatprofilen bereit. Weitere Informationen zum Erstellen von Zertifikatprofilen finden Sie unter [Erstellen von Zertifikatprofilen in Configuration Manager](../../protect/deploy-use/create-certificate-profiles.md).