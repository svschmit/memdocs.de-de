---
title: 'Verwenden von SCEP-Zertifikatprofilen mit Microsoft Intune: Azure | Microsoft-Dokumentation'
description: Erstellen und Zuweisen von SCEP-Zertifikatprofilen (Simple Certificate Enrollment Protocol) mit Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/14/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5126f2e5cc145e864fb4f56e472dba7a5179540f
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915584"
---
# <a name="create-and-assign-scep-certificate-profiles-in-intune"></a>Erstellen und Zuweisen eines SCEP-Zertifikatprofils in Intune

Nachdem Sie [Ihre Infrastruktur für die Unterstützung von SCEP-Zertifikaten (Simple Certificate Enrollment Protocol) konfiguriert haben](certificates-scep-configure.md), können Sie SCEP-Zertifikatprofile erstellen und Benutzern und Geräten in Intune zuweisen.

> [!IMPORTANT]
> Damit Geräte ein SCEP-Zertifikatprofil verwenden können, müssen sie Ihrer vertrauenswürdigen Stammzertifizierungsstelle vertrauen. Die Vertrauensstellung der Stammzertifizierungsstelle wird am besten durch Bereitstellen eines [vertrauenswürdigen Zertifikatprofils](../protect/certificates-configure.md#create-trusted-certificate-profiles) erreicht, und zwar in derselben Gruppe, die das SCEP-Zertifikatprofil empfängt. Vertrauenswürdige Zertifikatprofile stellen das Zertifikat der vertrauenswürdigen Stammzertifizierungsstelle bereit.

## <a name="create-a-scep-certificate-profile"></a>Erstellen eines SCEP-Zertifikatprofils

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.

3. Geben Sie die folgenden Eigenschaften ein:
   - **Plattform**: Wählen Sie die Plattform Ihrer Geräte aus.
   - **Profil**: Wählen Sie das **SCEP-Zertifikat** aus.

     Für die Plattform **Android Enterprise** ist der *Profiltyp* in zwei Kategorien unterteilt: *Fully Managed, Dedicated, and Corporate-Owned Work Profile* (Vollständig verwaltet, dediziert und unternehmenseigen mit einem Arbeitsprofil) und *Nur Arbeitsprofil*. Stellen Sie sicher, dass Sie das richtige SCEP-Zertifikatprofil für die von Ihnen verwalteten Geräte auswählen.  

     SCEP-Zertifikatprofile für das Profil *Fully Managed, Dedicated, and Corporate-Owned Work Profile* (Vollständig verwaltet, dediziert und unternehmenseigen mit einem Arbeitsprofil) weisen die folgenden Einschränkungen auf:

      1. Unter „Überwachung“ ist die Zertifikatberichterstellung für SCEP-Zertifikatprofile für Gerätebesitzer nicht verfügbar.

      2. Sie können Intune nicht verwenden, um Zertifikate zu widerrufen, die von SCEP-Zertifikatsprofilen für Gerätebesitzer bereitgestellt wurden. Sie können den Widerruf über einen externen Prozess oder direkt mit der Zertifizierungsstelle verwalten.

      3. Für dedizierte Android Enterprise-Geräte werden SCEP-Zertifikatprofile nur für die WLAN-Netzwerkkonfiguration, VPNs und die Authentifizierung unterstützt. SCEP-Zertifikatprofile auf dedizierten Android Enterprise-Geräten werden nicht für die App-Authentifizierung unterstützt.

4. Wählen Sie **Erstellen** aus.

5. Geben Sie in **Grundlagen** die folgenden Eigenschaften ein:
   - **Name:** Geben Sie einen aussagekräftigen Namen für das Profil ein. Benennen Sie Ihre Profile, damit Sie diese später leicht wiedererkennen. Ein geeigneter Profilname ist beispielsweise *SCEP-Profil für das gesamte Unternehmen*.
   - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.

6. Wählen Sie **Weiter** aus.

7. Nehmen Sie in den **Konfigurationseinstellungen** die folgenden Konfigurationen vor:

   - **Zertifikattyp**:

     *(Gilt für:  Android, Android Enterprise, iOS/iPadOS, macOS, Windows 8.1 und höher sowie Windows 10 und höher)*

     Wählen Sie je nach Verwendung des Zertifikatprofils einen Typ aus:

     - **Benutzer:** Bei *Benutzerzertifikaten* können sowohl Benutzer- als auch Geräteattribute im Betreff und im alternativen Antragstellernamen des Zertifikats enthalten sein.  
     - **Gerät:**  Beim Zertifikattyp *Gerät* können nur Geräteattribute im Betreff und im alternativen Antragstellernamen des Zertifikats enthalten sein.

       Benutzen Sie **Gerät** für Szenarios mit benutzerlosen Geräten (wie Kioske) oder Windows-Geräten. Auf Windows-Geräten wird das Zertifikat in den Zertifikatspeicher des lokalen Computers eingefügt.

     > [!NOTE]
     > Unter macOS werden Zertifikate, die Sie mit SCEP bereitstellen, immer in der Systemkeychain (Systemspeicher) des Geräts gespeichert.
 
   - **Format des Antragstellernamens**:

     Wählen Sie aus, auf welche Weise Intune den Antragstellernamen in der Zertifikatanforderung automatisch erstellen soll. Die Optionen für das Format des Antragstellernamens sind abhängig vom ausgewählten Zertifikattyp (**Benutzer** oder **Gerät**).

     > [!NOTE]
     > Es gibt ein [bekanntes Problem](#avoid-certificate-signing-requests-with-escaped-special-characters) bei der Verwendung von SCEP zum Abrufen von Zertifikaten, wenn der Antragstellername in der resultierenden Zertifikatsignieranforderung (Certificate Signing Request, CSR) eines der folgenden Zeichen als Escapezeichen enthält (mit vorangestelltem Schrägstrich\\):
     > - \+
     > - ;
     > - ,
     > - =

     - **Benutzerzertifikattyp**

       Formatoptionen für das *Format des Antragstellernamens*:

       - **Nicht konfiguriert**
       - **Allgemeiner Name**
       - **Allgemeiner Name einschließlich E-Mail-Adresse**
       - **Allgemeiner Name als E-Mail-Adresse**
       - **IMEI (International Mobile Equipment Identity)**
       - **Seriennummer**
       - **Benutzerdefiniert**: Bei Auswahl dieser Option wird auch ein **benutzerdefiniertes** Textfeld angezeigt. In dieses Feld können Sie ein benutzerdefiniertes Format für den Antragstellernamen, einschließlich Variablen, eingeben. Das benutzerdefinierte Format unterstützt zwei Variablen: **Common Name (CN)** (Allgemeiner Name) und **Email (E)** (E-Mail-Adresse). **Allgemeiner Name (CN)** kann auf eine der folgenden Variablen festgelegt werden:

         - **CN={{UserName}}** : Der Benutzername des Benutzers (z. B. janedoe).
         - **CN={{UserPrincipalName}}** : Der Benutzerprinzipalname des Benutzers (z. B. janedoe@contoso.com).\*
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
         
         \* Für Profile vom Typ „Fully Managed, Dedicated, and Corporate-Owned Work Profile“ (Vollständig verwaltet, dediziert und unternehmenseigen mit einem Arbeitsprofil) für Android funktioniert die Einstellung **CN={{UserPrincipalName}}** nicht. Solche Profile können für Geräte ohne Benutzer verwendet werden. Daher können sie den Benutzerprinzipalnamen des Benutzers nicht abrufen. Wenn Sie diese Option für Geräte mit Benutzern wirklich benötigen, können Sie eine Problemumgehung wie die folgende verwenden: **CN={{UserName}}\@contoso.com** Es werden der Benutzername und die Domäne angegeben, die Sie manuell hinzugefügt haben, z. B. janedoe@contoso.com

      - **Gerätzertifikattyp**

        Formatoptionen für das Format des Antragstellernamens umfassen die folgenden Variablen:

        - **{{AAD_Device_ID}}** oder **{{AzureADDeviceId}}** : Beide Variablen können zum Identifizieren eines Geräts über die zugehörige Azure AD-ID verwendet werden.
        - **{{Device_Serial}}**
        - **{{Device_IMEI}}**
        - **{{SerialNumber}}**
        - **{{IMEINumber}}**
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

   - **Alternativer Antragstellername**: Wählen Sie aus, auf welche Weise Intune den alternativen Antragstellernamen (Subject Alternative Name, SAN) in der Zertifikatanforderung automatisch erstellen soll. Die Optionen für den alternativen Antragstellernamen sind abhängig vom ausgewählten Zertifikattyp (**Benutzer** oder **Gerät**).

      - **Benutzerzertifikattyp**

        Wählen Sie aus den verfügbaren Attributen aus:

        - **E-Mail-Adresse**
        - **Benutzerprinzipalname (UPN)**

        Benutzerzertifikattypen können beispielsweise den Benutzerprinzipalnamen (User Principal Name, UPN) in den alternativen Antragstellernamen aufnehmen. Wenn ein Clientzertifikat für die Authentifizierung bei einem Netzwerkrichtlinienserver verwendet wird, legen Sie den alternativen Antragstellernamen auf den Benutzerprinzipalnamen fest.

      - **Gerätzertifikattyp**

        Verwenden Sie die Dropdownoption **Attribut**, wählen Sie ein Attribut aus, weisen Sie einen **Wert** zu, und klicken Sie auf **Hinzufügen**, um diesen hinzuzufügen. Sie können mehrere Werte hinzufügen, indem Sie zusätzliche Attribute auswählen.

        Zu den verfügbaren Attributen zählen:

        - **E-Mail-Adresse**
        - **Benutzerprinzipalname (UPN)**
        - **DNS**

        Mit dem Zertifikattyp *Gerät* können Sie die folgenden Gerätzertifikatvariablen für den Wert verwenden:

        - **{{AAD_Device_ID}}** oder **{{AzureADDeviceId}}** : Beide Variablen können zum Identifizieren eines Geräts über die zugehörige Azure AD-ID verwendet werden.
        - **{{Device_Serial}}**
        - **{{Device_IMEI}}**
        - **{{SerialNumber}}**
        - **{{IMEINumber}}**
        - **{{WiFiMacAddress}}**
        - **{{IMEI}}**
        - **{{DeviceName}}**
        - **{{FullyQualifiedDomainName}}**
        - **{{MEID}}**

        Schließen Sie den Variablennamen in geschweifte Klammern ein („{ }“), und fügen Sie den Text für diese Variable hinzu, um einen Wert für ein Attribut anzugeben. Beispielsweise kann mit **{{AzureADDeviceId}}.domain.com** ein Wert für das DNS-Attribut hinzugefügt werden, wobei *.domain.com* der Text ist. Einem Benutzer namens *User1* wird eine E-Mail-Adresse möglicherweise als {{FullyQualifiedDomainName}}User1@Contoso.com angezeigt.

        > [!IMPORTANT]
        > - Wenn Sie eine Gerätezertifikatvariable verwenden, schließen Sie den Variablennamen in geschweifte Klammern ein („{ }“).
        > - Verwenden Sie für den Text nach der Variable keine geschweiften Klammern **{ }** , senkrechten Striche **|** und Semikolons **;** .
        > - Geräteeigenschaften, die im *Betreff* oder *alternativen Antragstellernamen* eines Gerätezertifikats wie **IMEI**, **SerialNumber** oder **FullyQualifiedDomainName** verwendet werden, sind Eigenschaften, die von einer Person mit Zugriff auf das Gerät gespooft sein könnten.
        > - Ein Gerät muss alle in einem Zertifikatprofil für dieses Profil angegebenen Variablen unterstützen, um auf diesem Gerät installiert werden zu können.  Wenn **{{IMEI}}** beispielsweise im alternativen Antragstellernamen eines SCEP-Profils verwendet wird und einem Gerät ohne IMEI-Nummer zugewiesen ist, tritt bei der Profilinstallation ein Fehler auf.

   - **Gültigkeitsdauer des Zertifikats**:

     Sie können einen niedrigeren Wert als den für die Gültigkeitsdauer in der Zertifikatvorlage eingeben, aber keinen höheren. Wenn Sie die Zertifikatvorlage so konfiguriert haben, dass [ein benutzerdefinierter Wert unterstützt wird, der in der Intune-Konsole festgelegt werden kann](certificates-scep-configure.md#modify-the-validity-period-of-the-certificate-template), geben Sie mit dieser Einstellung die verbleibende Zeit bis zum Ablauf des Zertifikats an.

     Wenn die Gültigkeitsdauer des Zertifikats in der Zertifikatvorlage beispielsweise zwei Jahre beträgt, können Sie als Wert „ein Jahr“ eingeben, aber nicht „fünf Jahre“. Zudem muss der Wert niedriger als die verbleibende Gültigkeitsdauer des Zertifikats der ausstellenden Zertifizierungsstelle sein.

   - **Schlüsselspeicheranbieter (KSP)** :

     *(Gilt für:  Windows 8.1 und höher sowie Windows 10 und höher)*

     Geben Sie an, wo der Schlüssel für das Zertifikat gespeichert wird. Wählen Sie aus den folgenden Werten aus:

     - **Bei TPM-KSP (Trusted Platform Module) registrieren, falls vorhanden, andernfalls Software-KSP**
     - **Bei TPM-KSP (Trusted Platform Module) registrieren, andernfalls Fehler**
     - **Bei Passport registrieren, andernfalls Fehler (Windows 10 und höher)**
     - **Bei Software-KSP registrieren**

   - **Schlüsselverwendung**:

     Wählen Sie Schlüsselverwendungsoptionen für das Zertifikat aus:

     - **Digitale Signatur**: Der Schlüsselaustausch wird nur gestattet, wenn der Schutz des Schlüssels durch eine digitale Signatur unterstützt wird.
     - **Schlüsselverschlüsselung**: Der Schlüsselaustausch wird nur gestattet, wenn der Schlüssel verschlüsselt ist.

   - **Schlüsselgröße (Bits)** :

     Wählen Sie die Anzahl der Bits aus, die im Schlüssel enthalten sein sollen.

   - **Hashalgorithmus**:

     *(Gilt für Android, Android Enterprise, Windows 8.1 und höher sowie Windows 10 und höher)*

     Wählen Sie einen der verfügbaren Hashalgorithmustypen, der für dieses Zertifikat verwendet werden soll. Wählen Sie die höchste Sicherheitsebene aus, die die verbundenen Geräten unterstützen.

   - **Stammzertifikat**:

     Wählen Sie das *vertrauenswürdige Zertifikatprofil* aus, das Sie zuvor konfiguriert und den entsprechenden Benutzern und Geräten für dieses SCEP-Zertifikatprofil zugewiesen haben. Das vertrauenswürdige Zertifikatprofil wird zum Bereitstellen von Benutzern und Geräten mit dem Zertifikat der vertrauenswürdigen Stammzertifizierungsstelle verwendet. Weitere Informationen zum vertrauenswürdigen Zertifikatprofil finden Sie unter [Exportieren des Zertifikats der vertrauenswürdigen Stammzertifizierungsstelle](certificates-configure.md#export-the-trusted-root-ca-certificate) und [Erstellen vertrauenswürdiger Zertifikatprofile](certificates-configure.md#create-trusted-certificate-profiles) in *Verwenden von Zertifikaten für die Authentifizierung in Intune*. Wenn Sie über eine Stammzertifizierungsstelle und eine ausstellende Zertifizierungsstelle verfügen, wählen Sie das vertrauenswürdige Stammzertifikatprofil aus, das die ausstellende Zertifizierungsstelle überprüft.
     > [!NOTE]
     > Wenn Sie auf iOS/iPadOS-Geräten über eine Stammzertifizierungsstelle und eine ausstellende Zertifizierungsstelle verfügen, wählen Sie das vertrauenswürdige Stammzertifikatprofil aus, das die Stammzertifizierungsstelle überprüft. 

   - **Erweiterte Schlüsselverwendung**:

     Fügen Sie Werte für den beabsichtigten Zweck des Zertifikats hinzu. In den meisten Fällen erfordert das Zertifikat *Clientauthentifizierung*, damit der Benutzer bzw. das Gerät auf einem Server authentifiziert werden kann. Sie können ggf. weitere Schlüsselverwendungen hinzufügen.

   - **Verlängerungsschwellenwert (%)** :

     Geben Sie den Prozentsatz der Zertifikatgültigkeitsdauer an, die verbleibt, bevor das Gerät eine Verlängerung des Zertifikats anfordert. Wenn Sie beispielsweise „20“ eingeben, wird versucht, das Zertifikat zu erneuern, wenn das Zertifikat bereits zu 80 % abgelaufen ist. Die Erneuerungsversuche werden fortgesetzt, bis die Erneuerung erfolgreich ist. Bei der Erneuerung wird ein neues Zertifikat generiert, das zu einem neuen öffentlichen/privaten Schlüsselpaar führt.

   - **SCEP-Server-URLs**:

     Geben Sie mindestens eine URL für die NDES-Server ein, die Zertifikate über SCEP ausstellen. Geben Sie zum Beispiel `https://ndes.contoso.com/certsrv/mscep/mscep.dll` ein.

     Sie können bei Bedarf zusätzliche SCEP-URLs für Lastenausgleiche hinzufügen. Geräte führen drei separate Aufrufe an den NDES-Server aus, um die Serverfunktionen und einen öffentlichen Schlüssel abzurufen und anschließend eine Anforderung zur Signierung zu übermitteln. Wenn Sie mehrere URLs verwenden ist es möglich, dass der Lastenausgleich zur Verwendung einer anderen URL für nachfolgende Aufrufe an einen NDES-Server führt. Wenn innerhalb derselben Anforderung ein anderer Server für einen nachfolgenden Aufruf kontaktiert wird, ist die Anforderung nicht erfolgreich.

     Das Verhalten zur Verwaltung der NDES-Server-URL ist für jede Geräteplattform spezifisch:

     - **Android**: Das Gerät randomisiert die Liste der URLs, die in der SCEP-Richtlinie empfangen werden, und durchläuft dann die Liste, bis ein zugänglicher NDES-Server ermittelt wird. Das Gerät verwendet dann weiterhin dieselbe URL und denselben Server für den gesamten Prozess. Wenn das Gerät auf keinen der NDES-Server zugreifen kann, wird der Prozess nicht erfolgreich ausgeführt.
     - **iOS/iPadOS:** Intune randomisiert die URLs und stellt eine einzelne URL für ein Gerät bereit. Wenn das Gerät nicht auf den NDES-Server zugreifen kann, wird die SCEP-Anforderung nicht erfolgreich ausgeführt.
     - **Windows**: Die Liste der NDES-URLs wird randomisiert und an das Windows-Gerät übergeben, das diese dann in der empfangenen Reihenfolge testet, bis eine verfügbare URL gefunden wird. Wenn das Gerät auf keinen der NDES-Server zugreifen kann, wird der Prozess nicht erfolgreich ausgeführt.

     Wenn ein Gerät den NDES-Server in diesen drei Aufrufen nicht erreicht, wird die SCEP-Anforderung nicht erfolgreich ausgeführt. Dies kann beispielsweise der Fall sein, wenn eine Lastenausgleichslösung eine andere URL für den zweiten oder dritten Aufruf des NDES-Servers bereitstellt oder einen anderen tatsächlichen NDES-Server anhand einer virtualisierten URL für NDES zurückgibt. Nach einer nicht erfolgreichen Anforderung versucht ein Gerät, den Prozess im nächsten Richtlinienzyklus beginnend mit der randomisierten Liste der NDES-URLs (oder mit einer einzelnen URL für iOS/iPadOS) noch mal auszuführen.  

8. Wählen Sie **Weiter** aus.

9. Weisen Sie in **Bereichstags** (optional) ein Tag zu, um das Profil nach bestimmten IT-Gruppen wie `US-NC IT Team` oder `JohnGlenn_ITDepartment` zu filtern. Weitere Informationen zu Bereichstags finden Sie unter [Verwenden der RBAC und von Bereichstags für verteilte IT](../fundamentals/scope-tags.md).

   Wählen Sie **Weiter** aus.

10. Wählen Sie unter **Zuweisungen** die Benutzer oder Gruppen aus, denen das Profil zugewiesen werden soll. Weitere Informationen zum Zuweisen von Profilen finden Sie unter [Zuweisen von Benutzer- und Geräteprofilen](../configuration/device-profile-assign.md).

    Wählen Sie **Weiter** aus.

11. (*Gilt nur für Windows 10*) Geben Sie unter **Anwendbarkeitsregeln** einige Anwendbarkeitsregeln an, um die Zuweisung dieses Profils genauer zu spezifizieren. Sie können auswählen, dass das Profil basierend auf der Betriebssystemedition oder der Version eines Geräts zugewiesen oder nicht zugewiesen wird.

   Weitere Informationen finden Sie im Artikel *Erstellen eines Geräteprofils in Microsoft Intune* im Abschnitt [Anwendbarkeitsregeln](../configuration/device-profile-create.md#applicability-rules).

12. Überprüfen Sie die Einstellungen unter **Überprüfen + erstellen**. Wenn Sie auf „Erstellen“ klicken, werden die Änderungen gespeichert, und das Profil wird zugewiesen. Die Richtlinie wird auch in der Profilliste angezeigt.

### <a name="avoid-certificate-signing-requests-with-escaped-special-characters"></a>Vermeiden von Zertifikatsignieranforderungen mit Sonderzeichen als Escapezeichen

Es gibt ein bekanntes Problem bei SCEP- und PKCS-Zertifikatanforderungen, die einen Antragstellernamen (CN) mit einem oder mehreren der folgenden Sonderzeichen als Escapezeichen enthalten. Antragstellernamen, die eines der Sonderzeichen als Escapezeichen enthalten, führen zu einer CSR mit einem falschen Antragstellernamen. Ein falscher Antragstellername führt dazu, dass die SCEP-Challenge-Validierung fehlschlägt und kein Zertifikat ausgestellt wird.

Die Sonderzeichen sind:
- \+
- ,
- ;
- =

Wenn Ihr Antragstellername eines der Sonderzeichen enthält, verwenden Sie eine der folgenden Optionen, um diese Einschränkung zu umgehen:

- Kapseln Sie den CN-Wert, der das Sonderzeichen enthält, mit Anführungszeichen.  
- Entfernen Sie das Sonderzeichen aus dem CN-Wert.

**Beispielsweise** haben Sie einen Antragstellernamen, der als *Test user (TestCompany, LLC)* angezeigt wird.  Eine CSR, die einen CN mit dem Komma zwischen *TestCompany* und *LLC* umfasst, stellt ein Problem dar.  Das Problem kann vermieden werden, indem Sie den gesamten CN in Anführungszeichen setzen oder das Komma zwischen *TestCompany* und *LLC* entfernen:

- **Fügen Sie Anführungszeichen hinzu**: *CN="Test User (TestCompany, LLC)",OU=UserAccounts,DC=corp,DC=contoso,DC=com*
- **Entfernen Sie das Komma**: *CN=Test User (TestCompany LLC),OU=UserAccounts,DC=corp,DC=contoso,DC=com*

 Allerdings tritt bei Versuchen, das Komma mithilfe eines umgekehrten Schrägstrichs mit einem Escapezeichen zu versehen, ein Fehler in den CRP-Protokollen auf:
 
- **Mit Escapezeichen versehenes Komma**: *CN=Test User (TestCompany\\, LLC),OU=UserAccounts,DC=corp,DC=contoso,DC=com*

Der Fehler ähnelt dem folgenden:

```
Subject Name in CSR CN="Test User (TESTCOMPANY\, LLC),OU=UserAccounts,DC=corp,DC=contoso,DC=com" and challenge CN=Test User (TESTCOMPANY\, LLC),OU=UserAccounts,DC=corp,DC=contoso,DC=com do not match  

  Exception: System.ArgumentException: Subject Name in CSR and challenge do not match

   at Microsoft.ConfigurationManager.CertRegPoint.ChallengeValidation.ValidationPhase3(PKCSDecodedObject pkcsObj, CertEnrollChallenge challenge, String templateName, Int32 skipSANCheck)

Exception:    at Microsoft.ConfigurationManager.CertRegPoint.ChallengeValidation.ValidationPhase3(PKCSDecodedObject pkcsObj, CertEnrollChallenge challenge, String templateName, Int32 skipSANCheck)

   at Microsoft.ConfigurationManager.CertRegPoint.Controllers.CertificateController.VerifyRequest(VerifyChallengeParams value
```

## <a name="assign-the-certificate-profile"></a>Zuweisen des Zertifikatprofils

Weisen Sie SCEP-Zertifikatprofile auf die gleiche Weise zu, wie Sie [Geräteprofile für andere Zwecke bereitstellen](../configuration/device-profile-assign.md).

Um ein SCEP-Zertifikatprofil zu verwalten, muss ein Gerät auch das vertrauenswürdige Zertifikatprofil erhalten haben, das es mit Ihrem vertrauenswürdigen Zertifikat der Stammzertifizierungsstelle bereitstellt. Es wird empfohlen, jeweils das Profil des vertrauenswürdigen Stammzertifikats sowie das Profil des SCEP-Zertifikats in den gleichen Gruppen bereitzustellen.

Beachten Sie jedoch Folgendes, bevor Sie fortfahren:

- Wenn Sie Gruppen SCEP-Zertifikatprofile zuweisen, wird die vertrauenswürdige Zertifikatsdatei der Stammzertifizierungsstelle (wie im *vertrauenswürdigen Zertifikatprofil* angegeben) auf dem Gerät installiert. Das Gerät verwendet das SCEP-Zertifikatprofil, um eine Zertifikatanforderung für das vertrauenswürdige Zertifikat der Stammzertifizierungsstelle zu erstellen.

- Das SCEP-Zertifikatprofil wird nur auf Geräten installiert, auf denen die Plattform ausgeführt wird, die Sie beim Erstellen des Zertifikatprofils angegeben haben.

- Sie können Zertifikatprofile zu Benutzer- oder Gerätesammlungen zuweisen.

- Damit Zertifikate möglichst schnell nach der Geräteregistrierung auf Geräten veröffentlicht werden können, weisen Sie das Zertifikatprofil besser einer Benutzergruppe zu (nicht einer Gerätegruppe). Wenn Sie es einer Gerätegruppe zuweisen, muss eine vollständige Geräteregistrierung stattfinden, bevor das Gerät Richtlinien empfängt.

- Wenn Sie die Co-Verwaltung für Intune und Configuration Manager verwenden, bewegen Sie in Configuration Manager den [Schieberegler für Workloads](/configmgr/comanage/how-to-switch-workloads) für die Ressourcenzugriffsrichtlinie auf **Intune** oder **Intune-Pilot**. Diese Einstellung ermöglicht es Windows 10-Clients, den Prozess zur Anforderung des Zertifikats zu starten.

> [!NOTE]
> - Wenn auf iOS/iPadOS-Geräten ein SCEP-Zertifikatprofil oder ein PKCS-Zertifikatsprofil einem zusätzlichen Profil (z.B. einem WLAN- oder VPN-Profil) zugeordnet ist, erhält das Gerät ein Zertifikat für jedes der zusätzlichen Profile. Dadurch werden für das iOS/iPadOS-Gerät mehrere Zertifikate über die SCEP- oder PKCS-Zertifikatanforderung bereitgestellt. 
> 
>   Über das SCEP bereitgestellte Zertifikate sind eindeutig. Bei über PKCS bereitgestellten Zertifikaten handelt es sich um dasselbe Zertifikat. Sie scheinen nur unterschiedlich, da jede Profilinstanz im Verwaltungsprofil durch eine separate Zeile dargestellt wird.
> - Auf iOS 13 und macOS 10.15 gibt es einige [zusätzliche Sicherheitsanforderungen, die von Apple dokumentiert sind](https://support.apple.com/HT210176) und berücksichtigt werden müssen.  


## <a name="next-steps"></a>Nächste Schritte

[Zuweisen von Profilen](../configuration/device-profile-assign.md)

[Problembehandlung bei der Bereitstellung von SCEP-Zertifikatprofilen](../protect/troubleshoot-scep-certificate-profiles.md)