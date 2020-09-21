---
title: Verwenden von Zertifikaten mit privaten und öffentlichen Schlüsseln in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Verwenden Sie PKCS-Zertifikate (Public Key Cryptography Standards) mit Intune, arbeiten Sie mit Stammzertifikaten und Zertifikatvorlagen, installieren Sie den Microsoft Intune-Connector (NDES), und verwenden Sie Gerätekonfigurationsprofile für ein PKCS-Zertifikat.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/03/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 28ca32bc65ee0c4647c22b10b6b5d47a25efa202
ms.sourcegitcommit: d4ed7b4369389fd8ab07d28a7fa507797b6c6e57
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89643622"
---
# <a name="configure-and-use-pkcs-certificates-with-intune"></a>Konfigurieren und Verwenden Ihrer PKCS-Zertifikate mit Intune

Intune unterstützt die Verwendung von (PKCS-)Zertifikaten für private und öffentliche Schlüssel. In diesem Artikel erfahren Sie, wie Sie erforderliche Infrastrukturelemente wie lokale Zertifikatconnectors konfigurieren, ein PKCS-Zertifikat exportieren und dieses anschließend zu einem Intune-Gerätekonfigurationsprofil hinzufügen.

Mit den in Microsoft Intune integrierten Einstellungen lassen sich PKCS-Zertifikate für die Authentifizierung bei und den Zugriff auf Unternehmensressourcen verwenden. Mit Zertifikaten wird der Zugriff auf Unternehmensressourcen (z. B. ein VPN- oder ein WLAN-Netzwerk) authentifiziert und gesichert. Stellen Sie diese Einstellungen in Intune über Gerätekonfigurationsprofile bereit.

Informationen zur Verwendung importierter PKCS-Zertifikate finden Sie unter [Importierte PFX-Zertifikate](certificates-imported-pfx-configure.md).


## <a name="requirements"></a>Anforderungen

Wenn Sie PKCS-Zertifikate mit Intune verwenden möchten, müssen Sie über folgende Infrastruktur verfügen:

- **Active Directory-Domäne**:  
  Alle in diesem Abschnitt aufgeführten Server müssen der Active Directory-Domäne angehören.

  Informationen zum Installieren und Konfigurieren von Active Directory Domain Services (AD DS) finden Sie unter [AD DS Design and Planning (AD DS-Entwurf und -Planung)](/windows-server/identity/ad-ds/plan/ad-ds-design-and-planning).

- **Zertifizierungsstelle:**  
   Eine Unternehmenszertifizierungsstelle

  Informationen zum Installieren und Konfigurieren von Active Directory-Zertifikatdiensten finden Sie unter [Active Directory Certificate Services Step-by-Step Guide (Ausführliche Anleitung zu den Active Directory-Zertifikatdiensten)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc772393(v=ws.10)).

  > [!WARNING]  
  > Für Intune müssen AD CS mit einer Unternehmenszertifizierungsstelle, nicht mit einer eigenständigen Zertifizierungsstelle ausgeführt werden.

- **Einen Client**  
  Zum Herstellen einer Verbindung mit der Unternehmenszertifizierungsstelle.

- **Ein Stammzertifikat:**  
  Eine exportierte Kopie Ihres Stammzertifikats aus Ihrer Unternehmenszertifizierungsstelle.

- **PFX-Zertifikatconnector für Microsoft Intune:**

  Informationen über den PFX-Connector, einschließlich der Anforderungen und Releaseversionen finden Sie unter [Zertifikatconnectors](certificate-connectors.md).

  > [!IMPORTANT]
  > Mit dem Release von Version 6.2008.60.607 des PFX-Zertifikatconnectors ist der Microsoft Intune-Connector nicht mehr für PKCS-Zertifikatprofile erforderlich. 
  
## <a name="export-the-root-certificate-from-the-enterprise-ca"></a>Exportieren des Stammzertifikats aus der Unternehmenszertifizierungsstelle

Jedes Gerät benötigt ein Zertifikat einer Stamm- oder Zwischenzertifizierungsstelle für die Geräteauthentifizierung über VPN, WLAN oder andere Ressourcen. Die folgenden Schritte erläutern, wie das erforderliche Zertifikat von Ihrer Unternehmenszertifizierungsstelle abgerufen wird.

**Verwenden der Befehlszeile:**  

1. Melden Sie sich bei dem Server für Ihre Stammzertifizierungsstelle mit einem Administratorkonto an.

2. Navigieren Sie zu **Starten** > **Ausführen**, und geben Sie **Cmd** ein, um die Eingabeaufforderung zu öffnen.

3. Geben Sie **certutil -ca.cert ca_name.cer** an, um das Stammzertifikat als Datei mit dem Namen *ca_name.cer* zu exportieren.

## <a name="configure-certificate-templates-on-the-ca"></a>Konfigurieren von Zertifikatvorlagen für die Zertifizierungsstelle

1. Melden Sie sich bei Ihrer Unternehmenszertifizierungsstelle mit einem Konto an, das über Administratorrechte verfügt.
2. Öffnen Sie die Konsole **Zertifizierungsstelle**, klicken Sie mit der rechten Maustaste auf **Zertifikatvorlagen**, und klicken Sie dann auf **Verwalten**.
3. Suchen Sie die Zertifikatvorlage **Benutzer**, klicken Sie mit der rechten Maustaste darauf, und wählen Sie **Vorlage duplizieren** aus, um **Eigenschaften der neuen Vorlage** zu öffnen.

    > [!NOTE]
    > Zur Signierung und Verschlüsselung von E-Mails mit S/MIME nutzen viele Administratoren für die jeweiligen Schritte unterschiedliche Zertifikate. Wenn Sie Microsoft Active Directory-Zertifikatdienste verwenden, können Sie die Vorlage **Nur Exchange-Signatur** für Zertifikate zum Signieren von E-Mails mit S/MIME verwenden. Die Vorlage **Exchange-Benutzer** können Sie für Zertifikate zur Verschlüsselung mit S/MIME nutzen.  Wenn Sie auf eine Drittanbieter-Zertifizierungsstelle zurückgreifen, sollten Sie sich mit deren Leitfaden zum Einrichten von Signatur- und Verschlüsselungsvorlagen vertraut machen.

4. Gehen Sie auf der Registerkarte **Konformität** wie folgt vor:

    - Legen Sie **Zertifizierungsstelle** auf **Windows Server 2008 R2** fest.
    - Legen Sie **Zertifizierungsstelle** auf **Windows 7/Server 2008 R2** fest.

5. Legen Sie auf der Registerkarte **Allgemein** für **Vorlagenanzeigename** einen für Sie aussagekräftigen Namen fest.

    > [!WARNING]
    > **Vorlagenname** entspricht standardmäßig dem **Vorlagenanzeigenamen** *ohne Leerzeichen*. Notieren Sie sich den Namen der Vorlage, da Sie diesen später brauchen werden.

6. Klicken Sie unter **Anforderungsverarbeitung** auf **Exportieren von privatem Schlüssel zulassen**.

    > [!NOTE]
    > Anders als beim SCEP wird bei den PKCS der private Schlüssel des Zertifikats auf dem Server generiert, auf dem der Connector installiert ist, und nicht auf dem Gerät. Die Zertifikatvorlage muss das Exportieren des privaten Schlüssels erlauben, sodass der Zertifikatconnector das PFX-Zertifikat exportieren und an das Gerät senden kann. 
    >
    > Beachten Sie jedoch, dass die Zertifikate auf dem Gerät selbst installiert sind und der private Schlüssel als nicht exportierbar markiert ist.

7. Bestätigen Sie unter **Kryptografie**, dass die **Minimale Schlüsselgröße** auf 2048 festgelegt ist.
8. Klicken Sie unter **Antragstellername** auf **Supply in the request** (Informationen werden in der Anforderung angegeben).
9. Überprüfen Sie unter **Erweiterungen**, ob „Verschlüsselndes Dateisystem“, „Sichere E-Mail“ und „Clientauthentifizierung“ unter **Anwendungsrichtlinien** angezeigt werden.

    > [!IMPORTANT]
    > Wechseln Sie für iOS/iPadOS-Zertifikatvorlagen auf die Registerkarte **Erweiterungen**, aktualisieren Sie die Option **Schlüsselverwendung**, und stellen Sie sicher, dass die Option **Signatur ist Ursprungsnachweis** nicht aktiviert ist.

10. Fügen Sie unter **Sicherheit** das Computerkonto für den Server hinzu, auf dem Sie den Microsoft Intune-Connector installieren. Weisen Sie diesem Konto die Berechtigungen **Lesen** und **Registrieren** zu.
11. Wählen Sie **Anwenden** > **OK** aus, um die Zertifikatvorlage zu speichern. Schließen Sie die **Zertifikatvorlagenkonsole**.
12. Klicken Sie in der Konsole **Zertifizierungsstelle** mit der rechten Maustaste auf **Zertifikatvorlagen** > **Neu** > **Auszustellende Zertifikatvorlage**. Wählen Sie die Vorlage aus, die Sie in den vorherigen Schritten erstellt haben. Klicken Sie auf **OK**.
13. Gehen Sie folgendermaßen vor, damit der Server Zertifikate für registrierte Geräte und Benutzer verwaltet:

    1. Klicken Sie mit der rechten Maustaste auf die Zertifizierungsstelle, und wählen Sie **Eigenschaften**.
    2. Fügen Sie auf der Registerkarte „Sicherheit“ das Computerkonto des Servers hinzu, auf dem Sie die Connectors (entweder den **Microsoft Intune-Connector** oder den **PFX-Zertifikatconnector für Microsoft Intune**) ausführen. 
    3. Erteilen Sie dem Computerkonto die Zulassungsberechtigungen **Zertifikate ausstellen und verwalten** und **Zertifikate anfordern**.

14. Melden Sie sich von der Unternehmenszertifizierungsstelle ab.

## <a name="download-install-and-configure-the-pfx-certificate-connector"></a>Herunterladen, Installieren und Konfigurieren des PFX-Zertifikatconnectors

[Überprüfen Sie die Anforderungen an den Connector](certificate-connectors.md), und stellen Sie sicher, dass Ihre Umgebung und Ihr Windows-Server bereit sind, den Connector zu unterstützen, bevor Sie beginnen.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Mandantenverwaltung** > **Connectors und Token** > **Zertifikatconnectors** >  **+ Hinzufügen** aus.

3. Klicken Sie für den Connector für PKCS #12 auf *Zertifikatconnector-Software herunterladen*, und speichern Sie die Datei an einem Speicherort, auf den Sie über den Server zugreifen, auf dem Sie den Connector installieren werden.

   ![Herunterladen des Microsoft Intune-Connectors](./media/certficates-pfx-configure/download-connector.png)

4. Melden Sie sich nach Abschluss des Downloads beim Server an, und führen Sie das Installationsprogramm aus (PfxCertificateConnectorBootstrapper.exe).  
   - Wenn Sie den Standardspeicherort für die Installation übernehmen, wird der Connector in `Program Files\Microsoft Intune\PFXCertificateConnector` installiert.
   - Der Connectordienst wird auf dem lokalen Systemkonto ausgeführt. Wenn für den Internetzugriff ein Proxy erforderlich ist, müssen Sie sicherstellen, dass das lokale Dienstkonto auf die Proxyeinstellungen auf dem Server zugreifen kann.

5. Nach der Installation wird die Registerkarte **Registrierung** vom PFX Certificate Connector für Microsoft Intune geöffnet. Klicken Sie auf **Anmelden**, und geben Sie anschließend ein Konto mit Berechtigungen eines globalen Administrators oder Intune-Administrators an, um die Verbindung mit Intune zu aktivieren.

   > [!WARNING]
   > Standardmäßig ist **Verstärkte Sicherheitskonfiguration für IE** in Windows Server auf **Ein** festgelegt. Dies kann zu Problemen bei der Office 365-Anmeldung führen.

6. Wählen Sie die Registerkarte **Zertifizierungsstellenkonto** aus, und geben Sie die Anmeldeinformationen für ein Konto ein, das über die Berechtigung „Zertifikate ausstellen und verwalten“ für die ausstellende Zertifizierungsstelle verfügt. Diese Anmeldeinformationen werden für die Zertifikatsperrung in der Zertifizierungsstelle verwendet. 

    **Übernehmen** Sie Ihre Änderungen.

7. Schließen Sie das Fenster.

8. Wechseln Sie im Microsoft Endpoint Manager Admin Center zurück zu **Mandantenverwaltung** > **Connectors und Token** > **Zertifikatconnectors**. Nach wenigen Augenblicken wird ein grünes Häkchen angezeigt, und der Verbindungsstatus wird aktualisiert. Der Connectorserver kann jetzt mit Intune kommunizieren.

## <a name="create-a-trusted-certificate-profile"></a>Erstellen eines vertrauenswürdigen Zertifikatprofils

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.

3. Geben Sie die folgenden Eigenschaften ein:
   - **Plattform**: Wählen Sie die Plattform der Geräte aus, denen dieses Profil zugewiesen werden soll.
   - **Profil**: Wählen Sie **Vertrauenswürdiges Zertifikat** aus.
  
4. Wählen Sie **Erstellen** aus.

5. Geben Sie in **Grundlagen** die folgenden Eigenschaften ein:
   - **Name:** Geben Sie einen aussagekräftigen Namen für das Profil ein. Benennen Sie Ihre Profile, damit Sie diese später leicht wiedererkennen. Ein geeigneter Profilname ist beispielsweise *Profil für vertrauenswürdiges Zertifikat für das gesamte Unternehmen* .
   - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.

6. Wählen Sie **Weiter** aus.

7. Geben Sie in den **Konfigurationseinstellungen** die zuvor exportierte CER-Datei mit dem Zertifikat der Stammzertifizierungsstelle an.

   > [!NOTE]
   > Abhängig von der in **Schritt 3** ausgewählten Plattform besitzen Sie möglicherweise die Option zum Auswählen des **Zielspeichers** für das Zertifikat.

   ![Profil erstellen und ein vertrauenswürdiges Zertifikat hochladen](./media/certficates-pfx-configure/certificates-pfx-configure-profile-fill.png)

8. Wählen Sie **Weiter** aus.

9. Weisen Sie in **Bereichstags** (optional) ein Tag zu, um das Profil nach bestimmten IT-Gruppen wie `US-NC IT Team` oder `JohnGlenn_ITDepartment` zu filtern. Weitere Informationen zu Bereichstags finden Sie unter [Verwenden der RBAC und von Bereichstags für verteilte IT](../fundamentals/scope-tags.md).

   Wählen Sie **Weiter** aus.

10. Wählen Sie unter **Zuweisungen** die Benutzer oder Gruppen aus, denen das Profil zugewiesen werden soll. Planen Sie, dieses Zertifikatprofil für die Gruppen bereitzustellen, die auch das PKCS-Zertifikatprofil erhalten. Weitere Informationen zum Zuweisen von Profilen finden Sie unter [Zuweisen von Benutzer- und Geräteprofilen](../configuration/device-profile-assign.md).

    Wählen Sie **Weiter** aus.

11. (*Gilt nur für Windows 10*) Geben Sie unter **Anwendbarkeitsregeln** einige Anwendbarkeitsregeln an, um die Zuweisung dieses Profils genauer zu spezifizieren. Sie können auswählen, dass das Profil basierend auf der Betriebssystemedition oder der Version eines Geräts zugewiesen oder nicht zugewiesen wird.

  Weitere Informationen finden Sie im Artikel *Erstellen eines Geräteprofils in Microsoft Intune* im Abschnitt [Anwendbarkeitsregeln](../configuration/device-profile-create.md#applicability-rules).

12. Überprüfen Sie die Einstellungen unter **Überprüfen + erstellen**. Wenn Sie auf „Erstellen“ klicken, werden die Änderungen gespeichert, und das Profil wird zugewiesen. Die Richtlinie wird auch in der Profilliste angezeigt.

## <a name="create-a-pkcs-certificate-profile"></a>Erstellen eines PKCS-Zertifikatprofils

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.

3. Geben Sie die folgenden Eigenschaften ein:
   - **Plattform**: Wählen Sie die Plattform Ihrer Geräte aus. Folgende Optionen sind verfügbar:
     - Android-Geräteadministrator
     - Android Enterprise > Fully Managed, Dedicated, and Corporate-Owned Work Profile (Android Enterprise > Vollständig verwaltet, dediziert und unternehmenseigen mit einem Arbeitsprofil)
     - Android Enterprise > Nur Arbeitsprofil
     - iOS/iPadOS
     - macOS
     - Windows 10 und höher
   - **Profil**: Wählen Sie das **PKCS-Zertifikat** aus.

   > [!NOTE]
   > Auf Geräten mit einem Android Enterprise-Profil sind Zertifikate, die über ein PKCS-Zertifikatprofil installiert wurden, nicht sichtbar. Um die erfolgreiche Zertifikatbereitstellung zu bestätigen, überprüfen Sie den Status des Profils in der Intune-Konsole.
4. Wählen Sie **Erstellen** aus.

5. Geben Sie in **Grundlagen** die folgenden Eigenschaften ein:
   - **Name:** Geben Sie einen aussagekräftigen Namen für das Profil ein. Benennen Sie Ihre Profile, damit Sie diese später leicht wiedererkennen. Ein geeigneter Profilname ist beispielsweise *PKCS-Profil für das gesamte Unternehmen*.
   - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.

6. Wählen Sie **Weiter** aus.
7. Die verfügbaren **Konfigurationseinstellungen** variieren je nach ausgewählter Plattform. Wählen Sie Ihre Plattform aus, um auf die einzelnen Einstellungen zuzugreifen: Android-Geräteadministrator, Android Enterprise, iOS/iPadOS, Windows 10
   
   |Einstellung     | Plattform     | Details   |
   |------------|------------|------------|
   |**Verlängerungsschwellenwert (%)**        |<ul><li>Alle         |Empfohlen sind 20 %.  | 
   |**Gültigkeitsdauer des Zertifikats**  |<ul><li>Alle         |Wenn Sie die Zertifikatvorlage nicht geändert haben, kann diese Option auf ein Jahr festgelegt werden. |
   |**Schlüsselspeicheranbieter (KSP)**   |<ul><li>Windows 10  |Wählen Sie für Windows den Schlüsselspeicherort auf dem Gerät aus. |
   |**Zertifizierungsstelle**      |<ul><li>Alle         |Zeigt den internen vollqualifizierten Domänennamen (FQDN) Ihrer Unternehmenszertifizierungsstelle an.  |
   |**Name der Zertifizierungsstelle** |<ul><li>Alle         |Zeigt den Namen der Unternehmenszertifizierungsstelle an (z.B. „Contoso-Zertifizierungsstelle“). |
   |**Name der Zertifikatvorlage**    |<ul><li>Alle         |Führt den Namen Ihrer Zertifikatsvorlage auf |
   |**Zertifikattyp**             |<ul><li>Android Enterprise (*Arbeitsprofil*)</li><li>iOS</li><li>macOS</li><li>Windows 10 und höher|Wählen Sie einen Typ aus: <ul><li> Bei **Benutzerzertifikaten** können sowohl Benutzer- als auch Geräteattribute im Betreff und im alternativen Antragstellernamen des Zertifikats enthalten sein. </il><li>Beim Zertifikattyp **Gerät** können nur Geräteattribute im Betreff und im alternativen Antragstellernamen des Zertifikats enthalten sein. Versenden Sie „Gerät“ für Szenarios mit benutzerlosen Geräten (wie Kioske) oder geteilten Geräten.  <br><br> Diese Auswahl wirkt sich auf das Format des Antragstellernamens aus. |
   |**Format des Antragstellernamens**          |<ul><li>Alle         |Weitere Informationen zum Konfigurieren des Formats des Antragstellernamens finden Sie weiter unten in diesem Artikel im Abschnitt [Format des Antragstellernamens](#subject-name-format).  <br><br> Legen Sie für die meisten Plattformen diese Option auf **Allgemeiner Name** fest, falls kein anderes Format erforderlich ist. <br><br>Für die folgenden Plattformen wird das Format des Antragstellernamens durch den Zertifikattyp bestimmt: <ul><li>Android Enterprise (*Arbeitsprofil*)</li><li>iOS</li><li>macOS</li><li>Windows 10 und höher</li></ul>  <p>  |
   |**Alternativer Antragstellername**     |<ul><li>Alle         |Wählen Sie für *Attribut* die Option **Benutzerprinzipalname (UPN)** aus, falls keine andere Option erforderlich ist, konfigurieren Sie einen entsprechenden *Wert*, und klicken Sie dann auf **Hinzufügen**. <br><br>Weitere Informationen zum Konfigurieren des Formats des Antragstellernamens finden Sie weiter unten in diesem Artikel im Abschnitt [Format des Antragstellernamens](#subject-name-format).|
   |**Erweiterte Schlüsselverwendung**           |<ul><li> Android-Geräteadministrator </li><li>Android Enterprise (*Gerätebesitzer*, *Arbeitsprofil*) </li><li>Windows 10 |Zertifikate erfordern in der Regel *Clientauthentifizierung*, damit der Benutzer bzw. das Gerät auf einem Server authentifiziert werden kann. |
   |**Allen Apps Zugriff auf den privaten Schlüssel gewähren** |<ul><li>macOS  |Stellen Sie **Aktiviert** ein, um Apps, die für das zugeordnete Mac-Gerät konfiguriert sind, Zugriff auf den privaten Schlüssel des PKCS-Zertifikats zu gewähren. <br><br> Weitere Informationen zu dieser Einstellung finden Sie unter *AllowAllAppsAccess* im Abschnitt zur Zertifikatnutzlast der [Referenz zum Konfigurationsprofil](https://developer.apple.com/business/documentation/Configuration-Profile-Reference.pdf) in der Apple-Entwicklerdokumentation. |
   |**Stammzertifikat**             |<ul><li>Android-Geräteadministrator </li><li>Android Enterprise (*Gerätebesitzer*, *Arbeitsprofil*) |Wählen Sie ein Stammprofil für das ZS-Zertifikat aus, das zuvor zugewiesen wurde. |

8. Wählen Sie **Weiter** aus.

9. Weisen Sie in **Bereichstags** (optional) ein Tag zu, um das Profil nach bestimmten IT-Gruppen wie `US-NC IT Team` oder `JohnGlenn_ITDepartment` zu filtern. Weitere Informationen zu Bereichstags finden Sie unter [Verwenden der RBAC und von Bereichstags für verteilte IT](../fundamentals/scope-tags.md).

   Wählen Sie **Weiter** aus.

10. Wählen Sie unter **Zuweisungen** die Benutzer oder Gruppen aus, denen das Profil zugewiesen werden soll. Planen Sie die Bereitstellung dieses Zertifikatprofils für die Gruppen, die auch das vertrauenswürdige Zertifikatprofil erhalten. Weitere Informationen zum Zuweisen von Profilen finden Sie unter [Zuweisen von Benutzer- und Geräteprofilen](../configuration/device-profile-assign.md).

    Wählen Sie **Weiter** aus.

11. Überprüfen Sie die Einstellungen unter **Überprüfen + erstellen**. Wenn Sie auf „Erstellen“ klicken, werden die Änderungen gespeichert, und das Profil wird zugewiesen. Die Richtlinie wird auch in der Profilliste angezeigt.


### <a name="subject-name-format"></a>Format des Antragstellernamens

Wenn Sie ein PKCS-Zertifikatsprofil für die folgenden Plattformen erstellen, sind die Optionen für das Format des Antragstellernamens abhängig vom ausgewählten Zertifikattyp und lauten entweder **Benutzer** oder **Gerät**.  

Plattformen:

- Android Enterprise (*Arbeitsprofil*)
- iOS
- macOS
- Windows 10 und höher

> [!NOTE]
> Es gibt ein bekanntes Problem bei der Verwendung von PKCS zum Abrufen von Zertifikaten, [welches das gleiche Problem ist wie bei SCEP](certificates-profile-scep.md#avoid-certificate-signing-requests-with-escaped-special-characters), wenn der Antragstellername in der resultierenden Zertifikatsignieranforderung (Certificate Signing Request, CSR) eines der folgenden Zeichen als Escapezeichen enthält (mit vorangestelltem Schrägstrich\\):
> - \+
> - ;
> - ,
> - =

- **Benutzerzertifikattyp**  
  Formatoptionen für das *Format des Antragstellernamens* enthalten zwei Variablen: **Common Name (CN)** (Allgemeiner Name) und **Email (E)** (E-Mail-Adresse). **Allgemeiner Name (CN)** kann auf eine der folgenden Variablen festgelegt werden:

  - **CN={{UserName}}** : Der Benutzerprinzipalname des Benutzers (z. B. janedoe@contoso.com)
  - **CN={{AAD_Device_ID}}** : Eine ID, die zugewiesen wird, wenn Sie ein Gerät in Azure Active Directory (AD) registrieren. Diese ID wird in der Regel für die Authentifizierung bei Azure Active Directory verwendet.
  - **CN={{SERIALNUMBER}}** : Die eindeutige Seriennummer (SN), die in der Regel vom Hersteller zum Identifizieren eines Geräts verwendet wird.
  - **CN={{IMEINumber}}** : Die eindeutige IMEI-Nummer (International Mobile Equipment Identity), die verwendet wird, um ein Mobiltelefon zu identifizieren.
  - **CN={{OnPrem_Distinguished_Name}}** : Eine Sequenz von durch Kommas getrennte relative definierte Namen wie *CN=Jane Doe, OU=UserAccounts, DC=corp, DC=contoso, DC=com*.

    Stellen Sie sicher, dass Sie das Benutzerattribut *onpremisesdistinguishedname* mithilfe von [Azure AD Connect](/azure/active-directory/connect/active-directory-aadconnect) mit Azure AD synchronisieren, um die Variable *{{OnPrem_Distinguished_Name}}* zu verwenden.

  - **CN={{onPremisesSamAccountName}}** : Administratoren können das Attribut „samAccountName“ aus Active Directory mithilfe von Azure AD Connect in einem Attribut mit dem Namen *onPremisesSamAccountName* mit Azure AD synchronisieren. Intune kann diese Variable als Teil einer Zertifikatsausstellungsanforderung im Antragsteller eines Zertifikats ersetzen. Das Attribut „samAccountName“ ist der zur Unterstützung von Clients und Servern aus einer früheren Version von Windows (vor Windows 2000) verwendete Benutzeranmeldename. Das Format des Benutzeranmeldenamens lautet wie folgt: *DomainName\testUser*oder nur *testUser*.

    Stellen Sie sicher, dass Sie das Benutzerattribut *onPremisesSamAccountName* mithilfe von [Azure AD Connect](/azure/active-directory/connect/active-directory-aadconnect) mit Azure AD synchronisieren, um die Variable *{{onPremisesSamAccountName}}* zu verwenden.

  Durch eine Kombination einer oder vieler dieser Variablen mit statischen Zeichenfolgen können Sie ein benutzerdefiniertes Format wie dieses für den Antragstellernamen erstellen:  
  - **CN={{UserName}},E={{EmailAddress}},OU=Mobile,O=Finance Group,L=Redmond,ST=Washington,C=US**
  
  Dieses Beispiel enthält das Format des Antragstellernamens, das die Variablen „CN“ und „E“ und Zeichenfolgen für die Werte „Organisationseinheit“, „Organisation“, „Standort“, „Bundesland/Kanton“ und „Land/Region“ verwendet. Die Funktion [CertStrToName](/windows/win32/api/wincrypt/nf-wincrypt-certstrtonamea) beschreibt diese Funktion und die unterstützten Zeichenfolgen.

- **Gerätzertifikattyp**  
  Formatoptionen für das Format des Antragstellernamens umfassen die folgenden Variablen: 
  - **{{AAD_Device_ID}}**
  - **{{Device_Serial}}**
  - **{{Device_IMEI}}**
  - **{{SerialNumber}}**
  - **{{IMEINumber}}**
  - **{{AzureADDeviceId}}**
  - **{{WiFiMacAddress}}**
  - **{{IMEI}}**
  - **{{DeviceName}}**
  - **{{FullyQualifiedDomainName}}** *(Gilt nur für Windows-Geräte und in Domänen eingebundene Geräte)*
  - **{{MEID}}**

  Sie können diese Variablen, gefolgt vom Text für die Variablen, im Textfeld angeben. Beispielsweise kann der allgemeine Name für ein Gerät namens *Device1* als **CN={{DeviceName}}Device1** hinzugefügt werden.

  > [!IMPORTANT]  
  > - Schließen Sie den Variablennamen beim Angeben einer Variable wie im Beispiel veranschaulicht in geschweifte Klammern („{ }“) ein, um einen Fehler zu vermeiden.  
  > - Geräteeigenschaften, die im *Betreff* oder *alternativen Antragstellernamen* eines Gerätezertifikats wie **IMEI**, **SerialNumber** oder **FullyQualifiedDomainName** verwendet werden, sind Eigenschaften, die von einer Person mit Zugriff auf das Gerät gespooft sein könnten.
  > - Ein Gerät muss alle in einem Zertifikatprofil für dieses Profil angegebenen Variablen unterstützen, um auf diesem Gerät installiert werden zu können.  Wenn **{{IMEI}}** beispielsweise im Antragstellernamen eines SCEP-Profils verwendet wird und einem Gerät ohne IMEI-Nummer zugewiesen ist, tritt bei der Profilinstallation ein Fehler auf.

## <a name="next-steps"></a>Nächste Schritte

Lesen Sie auch die Artikel [Konfigurieren der Infrastruktur zur Unterstützung von SCEP in Intune](certificates-scep-configure.md) oder [Einrichten des Intune Certificate Connectors für den Symantec PKI-Manager-Webdienst](certificates-digicert-configure.md).

[Problembehandlung bei PKCS-Zertifikatprofilen](../protect/troubleshoot-pkcs-certificate-profiles.md)
