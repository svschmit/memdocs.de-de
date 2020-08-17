---
title: Behandeln von Problemen bei der Verwendung von PKCS-Zertifikatprofilen zum Bereitstellen von Zertifikaten mit Microsoft Intune | Microsoft-Dokumentation
description: Informationen zum Behandeln von Problemen bei der Verwendung von PKCS-Profilen (Paaren mit privatem und öffentlichem Schlüssel) von Geräten zum Anfordern von Zertifikaten für die Verwendung mit Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/11/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 2c6f2eb7d6174c706cdd8a3910df1d0ddc2e6ef0
ms.sourcegitcommit: 532a06163f462527254d23e7dc505b18c0c4f938
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/11/2020
ms.locfileid: "88110680"
---
# <a name="troubleshoot-pkcs-certificate-deployment-in-microsoft-intune"></a>Problembehandlung bei der Bereitstellung eines PKCS-Zertifikats in Microsoft Intune

Die Informationen in diesem Artikel können Ihnen helfen, mehrere gängige Probleme bei der Bereitstellung von PKCS-Zertifikaten (Paaren mit privatem und öffentlichem Schlüssel) in Microsoft Intune zu beheben. Stellen Sie vor der Problembehandlung sicher, dass Sie die folgenden in [Konfigurieren und Verwenden Ihrer PKCS-Zertifikate mit Intune](../protect/certficates-pfx-configure.md#export-the-root-certificate-from-the-enterprise-ca) beschriebenen Aufgaben erledigt haben:

- Überprüfen der [Anforderungen für die Verwendung von PKCS-Zertifikatprofilen](../protect/certficates-pfx-configure.md#requirements)
- Exportieren des Stammzertifikats aus der Unternehmenszertifizierungsstelle
- Konfigurieren von Zertifikatvorlagen für die Zertifizierungsstelle
- Installieren und Konfigurieren des Intune Certificate Connectors
- Erstellen und Bereitstellen eines vertrauenswürdigen Zertifikatprofils zum Bereitstellen des Stammzertifikats
- Erstellen und Bereitstellen eines PKCS-Zertifikatprofils

Die häufigste Problemursache bei PKCS-Zertifikatsprofilen war bisher deren Konfiguration. Überprüfen Sie die Profilkonfiguration, achten Sie auf Tippfehler in Server- oder vollqualifizierten Domänennamen (FQDNs), und bestätigen Sie, dass **Zertifizierungsstelle** und **Zertifizierungsstellenname** stimmen.

- **Zertifizierungsstelle:** Der interne FQDN des Computers mit der Zertifizierungsstelle. Beispiel: server1.domain.local.
- **Name der Zertifizierungsstelle**: Der Name der Zertifizierungsstelle, der in der MMC „Zertifizierungsstelle“ angezeigt wird. Sehen Sie unter **Zertifizierungsstelle (Lokal)** nach.

Sie können das [Befehlszeilenprogramm certutil](https://docs.microsoft.com/windows-server/administration/windows-commands/certutil) auf die Zertifizierungsstelle anwenden, um zu bestätigen, dass der Name für „Zertifizierungsstelle“ und „Name der Zertifizierungsstelle“ richtige Angaben enthalten.

## <a name="pkcs-communication-overview"></a>Übersicht über die PKCS-Kommunikation

Die folgende Abbildung bietet einen grundlegenden Überblick über den Prozess der Bereitstellung von PKCS-Zertifikaten in Intune.

> [!div class="mx-imgBorder"]
> ![Ablauf des Bereitstellungsprozesses von PKCS-Zertifikaten](./media/troubleshoot-pkcs-certificate-profiles/pkcs-overview-graphic.png)

1. Ein Administrator erstellt in Intune ein PKCS-Zertifikatprofil.
2. Der Intune-Dienst fordert den lokalen Intune Certificate Connector auf, ein neues Zertifikat für den Benutzer zu erstellen.
3. Der Intune Certificate Connector sendet ein PFX-Blob und eine Anforderung an Ihre Microsoft-Zertifizierungsstelle.
4. Die Zertifizierungsstelle stellt das PFX-Benutzerzertifikat aus und sendet es zurück an den Intune Certificate Connector.
5. Der Intune Certificate Connector lädt das verschlüsselte PFX-Benutzerzertifikat in Intune hoch.
6. Intune entschlüsselt das PFX-Benutzerzertifikat und verschlüsselt das Gerät mit dem Geräteverwaltungszertifikat neu.  Intune sendet dann das PFX-Benutzerzertifikat an das Gerät.
7. Das Gerät meldet Intune den Zertifikatsstatus.

## <a name="data-and-log-files"></a>Daten- und Protokolldateien

Um Probleme mit dem Workflow für Kommunikation und Zertifikatbereitstellung zu identifizieren, überprüfen Sie sowohl die Protokolldateien aus der Serverinfrastruktur als auch von den Geräten. Spätere Abschnitte zur Problembehandlung bei PKCS-Zertifikatprofilen beziehen sich auf Protokolldateien, auf die in diesem Abschnitt verwiesen wird.

- [Infrastruktur- und Serverprotokolle](#logs-for-on-premises-infrastructure)

Geräteprotokolle sind von der Geräteplattform abhängig:

- [iOS und iPadOS](#logs-for-ios-and-ipados-devices)
- [Android](#logs-for-android-devices)
- [Windows](#logs-for-windows-devices)

### <a name="logs-for-on-premises-infrastructure"></a>Protokolle für die lokale Infrastruktur
  
Die lokale Infrastruktur, die die Verwendung von PKCS-Zertifikatprofilen für Zertifikatbereitstellungen unterstützt, umfasst den Microsoft Intune Certificate Connector, den NDES, der auf einem Windows-Server ausgeführt wird, und die Zertifizierungsstelle.

Zu den Protokolldateien für diese Rollen zählen Windows-Ereignisanzeige, Zertifikatkonsolen und verschiedene Protokolldateien für Intune Certificate Connector, NDES oder andere Rollen und Vorgänge, die Teil der lokalen Infrastruktur sind.

- **NDESConnector_date_time.svclog**:

  Dieses Protokoll zeigt die Kommunikation des Microsoft Intune Certificate Connector mit dem Intune-Clouddienst. Um diese Protokolldatei anzuzeigen, können Sie das [Service Trace Viewer-Tool](https://docs.microsoft.com/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe) verwenden.

  Zugehöriger Registrierungsschlüssel: *HKLM\SW\Microsoft\MicrosoftIntune\NDESConnector\ConnectionStatus*

  Speicherort: Auf dem Server, der NDES auf *%program_files%\Microsoft intune\ndesconnectorisvc\logs\logs* hostet

- **CertificateRegistrationPoint_date_time.svclog**:

  Dieses Protokoll zeigt das NDES-Richtlinienmodul, das Zertifikatanforderungen empfängt und überprüft. Um diese Protokolldatei anzuzeigen, können Sie das [Service Trace Viewer-Tool](https://docs.microsoft.com/dotnet/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe) verwenden.

  Speicherort: Auf dem Server, der NDES auf *%program_files%\Microsoft intune\ndesconnectorisvc\logs\logs* hostet

- **NDESPlugin.log**:

  Dieses Protokoll zeigt das Übergeben von Zertifikatanforderungen an den Zertifikatregistrierungspunkt und die resultierende Überprüfung dieser Anforderungen.

  Speicherort: Auf dem Server, der NDES auf *% program_files%\Microsoft intune\NDESPolicyModule\logs* hostet

- **Windows-Anwendungsprotokoll**:

  Speicherort: Auf dem Server, der NDES hostet: Führen Sie **eventvwr.msc** aus, um die Windows-Ereignisanzeige zu öffnen.

### <a name="logs-for-android-devices"></a>Protokolle für Android-Geräte

Bei Geräten, auf denen Android ausgeführt wird, verwenden Sie die App-Protokolldatei des **Android-Unternehmensportals**, **OMADM.log**. Stellen Sie vor dem Erfassen und Überprüfen von Protokollen sicher, dass [ausführliche Protokollierung](../user-help/use-verbose-logging-to-help-your-it-administrator-fix-device-issues-android.md) aktiviert ist, und reproduzieren Sie dann das Problem.

Informationen zum Erfassen von OMADM-Protokollen von einem Gerät finden Sie unter [Hochladen und E-Mail-Versand von Protokollen mithilfe eines USB-Kabels](../user-help/send-logs-to-your-it-admin-using-cable-android.md).

Unterstützung finden Sie auch unter [Hochladen und E-Mail-Versand von Protokollen aus der Microsoft Intune-App](../user-help/send-logs-to-your-it-admin-by-email-android.md#upload-and-email-logs-from-microsoft-intune-app).

### <a name="logs-for-ios-and-ipados-devices"></a>Protokolle für iOS- und iPadOS-Geräte

Bei Geräten, auf denen iOS/iPadOS ausgeführt wird, verwenden Sie Debugprotokolle und **Xcode**, der auf einem Macintosh-Computer ausgeführt wird:

1. Verbinden Sie das iOS/iPadOS-Gerät mit dem Mac, und wechseln Sie dann zu **Anwendungen** > **Hilfsprogramme**, um die Konsolen-App zu öffnen.

2. Wählen Sie unter **Aktion** die Option **Include Info Messages** (Informationsmeldungen einschließen) und **Include Debug Messages** (Debugmeldungen einschließen) aus.

   ![Auswählen von Protokolloptionen](../protect/media/troubleshoot-pkcs-certificate-profiles/message-options.png)

3. Reproduzieren Sie das Problem, und speichern Sie die Protokolle in einer Textdatei:
   1. Wählen Sie **Bearbeiten** > **Alle auswählen** aus, um alle Nachrichten auf dem aktuellen Bildschirm auszuwählen, und wählen Sie dann **Bearbeiten** > **Kopieren** aus, um die Nachrichten in die Zwischenablage zu kopieren.
   2. Öffnen Sie die TextEdit-Anwendung, fügen Sie die kopierten Protokolle in eine neue Textdatei ein, und speichern Sie die Datei.

Das Unternehmensportalprotokoll für iOS- und iPadOS-Geräte enthält keine Informationen zu PKCS-Zertifikatprofilen.

### <a name="logs-for-windows-devices"></a>Protokolle für Windows-Geräte

Verwenden Sie für Geräte unter Windows die Windows-Ereignisprotokolle, um Probleme mit der Registrierung oder der Geräteverwaltung für Geräte zu diagnostizieren, die Sie mit Intune verwalten.

Öffnen Sie auf dem Gerät **Ereignisanzeige** > **Anwendungs- und Dienstprotokolle** > **Microsoft** > **Windows** > **DeviceManagement-Enterprise-Diagnostics-Provider**.

![Windows-Ereignisprotokolle](../protect/media/troubleshoot-pkcs-certificate-profiles/windows-event-log.png)

## <a name="antivirus-exclusions"></a>Antivirenausschlüsse

Unter folgenden Umständen sollte Sie auf Servern, die NDES oder den Certificate Connector hosten, ggf. Ausnahmen für die Antivirensoftware hinzufügen:

- Zertifikatanforderungen erreichen den Server oder den Microsoft Intune Certificate Connector, werden jedoch nicht erfolgreich verarbeitet. 
- Zertifikate werden langsam ausgegeben.

Nachstehend finden Sie einige Beispiele für Speicherorte, die ausgeschlossen werden können:

- *%program_files%* \Microsoft Intune\PfxRequest
- *%program_files%* \Microsoft Intune\CertificateRequestStatus
- *%program_files%* \Microsoft Intune\CertificateRevocationStatus

## <a name="common-errors"></a>Häufige Fehler

Die folgenden gängigen Fehler werden in einem der folgenden Abschnitte angesprochen:

- [Der RPC-Server ist nicht verfügbar: 0x800706ba](#the-rpc-server-is-unavailable-0x800706ba)
- [Ein Registrierungsrichtlinienserver wurde nicht gefunden: 0x80094015](#an-enrollment-policy-server-cannot-be-located-0x80094015)
- [Die Übermittlung steht aus](#the-submission-is-pending)
- [Falscher Parameter: 0x80070057](#the-parameter-is-incorrect-0x80070057)
- [Vom Richtlinienmodul verweigert](#denied-by-policy-module)
- [Zertifikatprofil hängt als „Ausstehend“](#certificate-profile-stuck-as-pending)
- [Fehler: 2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED](#error--2146875374-certsrv_e_subject_email_required)

### <a name="the-rpc-server-is-unavailable-0x800706ba"></a>Der RPC-Server ist nicht verfügbar: 0x800706ba

Während der PFX-Bereitstellung wird zwar das vertrauenswürdige Stammzertifikat auf dem Gerät angezeigt, aber das PFX-Zertifikat ist nicht auf dem Gerät vorhanden. Die NDESConnector-Protokolldatei enthält die Zeichenfolge **Der RPC-Server nicht verfügbar ist. 0x800706ba**, wie in der ersten Zeile im folgenden Beispiel gezeigt:

```
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x800706BA): CCertRequest::Submit: The RPC server is unavailable. 0x800706ba (WIN32: 1722 RPC_S_SERVER_UNAVAILABLE)
IssuePfx -Generic Exception: System.ArgumentException: CCertRequest::Submit: The parameter is incorrect. 0x80070057 (WIN32: 87 ERROR_INVALID_PARAMETER)
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x80094800): The requested certificate template is not supported by this CA. (Exception from HRESULT: 0x80094800)
```

#### <a name="cause-1---incorrect-configuration-of-the-ca-in-intune"></a>Ursache 1: Falsche Konfiguration der Zertifizierungsstelle in Intune

Dieses Problem kann auftreten, wenn das PKCS-Zertifikatsprofil den falschen Server angibt oder Rechtschreibfehler im Namen oder FQDN der Zertifizierungsstelle aufweist. Die Zertifizierungsstelle wird in den folgenden Eigenschaften des Profils angegeben:

- Zertifizierungsstelle
- Name der Zertifizierungsstelle

**Lösung**:

Überprüfen Sie die folgenden Einstellungen, und korrigieren Sie sie, sofern sie nicht stimmen:

- Die Eigenschaft **Zertifizierungsstelle** zeigt den internen FQDN Ihres Zertifizierungsstellenservers an.
- Die Eigenschaft **Name der Zertifizierungsstelle** zeigt den Namen Ihrer Zertifizierungsstelle an.

#### <a name="cause-2---ca-doesnt-support-certificate-renewal-for-requests-signed-by-previous-ca-certificates"></a>Ursache 2: Die Zertifizierungsstelle unterstützt keine Zertifikatverlängerung für Anforderungen, die von früheren Zertifizierungsstellenzertifikaten signiert wurden.

Wenn der FQDN und Name der Zertifizierungsstelle im PKCS-Zertifikatsprofil stimmen, überprüfen Sie das Windows-Protokoll „Anwendung“, das sich auf dem Zertifizierungsstellenserver befindet. Suchen Sie nach der **Ereignis-ID 128**, die dem folgenden Beispiel ähnelt:

```
Log Name: Application:
Source: Microsoft-Windows-CertificationAuthority
Event ID: 128
Level: Warning
Details:
An Authority Key Identifier was passed as part of the certificate request 2268. This feature has not been enabled. To enable specifying a CA key for certificate signing, run: "certutil -setreg ca\UseDefinedCACertInRequest 1" and then restart the service.
```

Wenn das Zertifizierungsstellenzertifikat verlängert wird, muss es das OCSP-Antwortsignaturzertifikat (Online Certificate Status Protocol) signieren. Durch das Signieren wird das OCSP-Antwortsignaturzertifikat aktiviert, um andere Zertifikate zu validieren, indem ihr Sperrstatus überprüft wird. Diese Signierung ist standardmäßig nicht aktiviert.

**Lösung**:

Erzwingen Sie die Signierung des Zertifikats manuell:

1. Öffnen Sie auf dem Zertifizierungsstellenserver eine Eingabeaufforderung mit erhöhten Berechtigungen, und führen Sie den folgenden Befehl aus: **certutil -setreg ca\UseDefinedCACertInRequest 1**
2. Starten Sie den Dienst „Zertifikatdienste“ neu.

Nachdem der Dienst „Zertifikatdienste“ neu gestartet wurde, können Geräte Zertifikate empfangen.

### <a name="an-enrollment-policy-server-cannot-be-located-0x80094015"></a>Ein Registrierungsrichtlinienserver wurde nicht gefunden: 0x80094015

**Ein Registrierungsrichtlinienserver wurde nicht gefunden** und **0x80094015** wie im folgenden Beispiel gezeigt:

```
IssuePfx - COMException: System.Runtime.InteropServices.COMException (0x80094015): An enrollment policy server cannot be located. (Exception from HRESULT: 0x80094015)
```

#### <a name="cause---certificate-enrollment-policy-server-name"></a>Ursache: Name des Registrierungsrichtlinienservers für das Zertifikat

Dieses Problem tritt auf, wenn der Computer, der den NDES-Connector von Intune hostet, keinen Registrierungsrichtlinienserver für das Zertifikat finden kann.

**Lösung**:

Konfigurieren Sie den Namen des Registrierungsrichtlinienservers für das Zertifikat manuell auf dem Computer, der den NDES-Connector hostet. Um den Namen zu konfigurieren, verwenden Sie das PowerShell-Cmdlet [Add-CertificateEnrollmentPolicyServer](https://docs.microsoft.com/powershell/module/pkiclient/add-certificateenrollmentpolicyserver?view=win10-ps).

### <a name="the-submission-is-pending"></a>Die Übermittlung steht aus

Nachdem Sie ein PKCS-Zertifikatsprofil auf mobilen Geräten bereitgestellt haben, werden die Zertifikate nicht bezogen, und das NDESConnector-Protokoll enthält die Zeichenfolge **The submission is pending** (Die Übermittlung ist ausstehend), wie im folgenden Beispiel zu sehen:

```
IssuePfx - The submission is pending: Taken Under Submission
IssuePfx -Generic Exception: System.InvalidOperationException: IssuePfx - The submission is pending
```

Darüber hinaus können Sie auf dem Zertifizierungsstellenserver die PFX-Anforderung im Ordner **Ausstehende Anforderungen** sehen:

> [!div class="mx-imgBorder"]
> ![Screenshot des Ordners „Ausstehende Anforderungen“ der Zertifizierungsstelle](./media/troubleshoot-pkcs-certificate-profiles/pending-requests.png)

#### <a name="cause---incorrect-configuration-for-request-handling"></a>Ursache: falsche Konfiguration der Anforderungsverarbeitung

Dieser Fehler tritt auf, wenn die Option **Status der Zertifikatanforderung auf Ausstehend festlegen. Der Administrator muss das Zertifikat explizit ausstellen** in der Zertifizierungsstelle im Dialogfeld **Eigenschaften** > **Richtlinienmodul** > **Eigenschaften** aktiviert ist.

> [!div class="mx-imgBorder"]
> ![Screenshot der Eigenschaften des Richtlinienmoduls](./media/troubleshoot-pkcs-certificate-profiles/policy-module-properties.png)

**Lösung**:

Bearbeiten Sie Eigenschaften des Richtlinienmoduls so, dass Folgendes festgelegt wird: **Den Einstellungen der Zertifikatvorlage folgen, falls zutreffend. Zertifikat ansonsten automatisch ausstellen.**

### <a name="the-parameter-is-incorrect-0x80070057"></a>Falscher Parameter: 0x80070057

Nachdem der Intune Certificate Connector erfolgreich installiert und konfiguriert wurde, empfangen Geräte keine PKCS-Zertifikate, und das NDESConnector-Protokoll enthält die Zeichenfolge **Der Parameter ist falsch. 0x80070057**, wie im folgenden Beispiel gezeigt:

```
CCertRequest::Submit: The parameter is incorrect. 0x80070057 (WIN32: 87 ERROR_INVALID_PARAMETER)
```

#### <a name="cause---configuration-of-the-pkcs-profile"></a>Ursache: Konfiguration des PKCS-Profils

Dieses Problem tritt auf, wenn das PKCS-Profil in Intune falsch konfiguriert ist. Es folgen häufige Konfigurationsfehler:

- Das Profil enthält einen falschen Namen für die Zertifizierungsstelle.
- Der alternative Antragstellername (Subject Alternative Name, SAN) ist für eine E-Mail-Adresse konfiguriert, aber der Zielbenutzer hat noch keine gültige E-Mail-Adresse. Diese Kombination führt zu einem NULL-Wert für den SAN, was unzulässig ist.

**Lösung**:

Überprüfen Sie die folgenden Konfigurationen für das PKCS-Profil, und warten Sie dann, bis die Richtlinie auf dem Gerät aktualisiert wird:

- Mit dem Namen der Zertifizierungsstelle konfiguriert
- Der richtigen Benutzergruppe zugewiesen
- Benutzer in der Gruppe mit gültigen E-Mail-Adressen

Weitere Informationen finden Sie unter [Konfigurieren und Verwenden von PKCS-Zertifikaten mit Intune](../protect/certficates-pfx-configure.md).

### <a name="denied-by-policy-module"></a>Vom Richtlinienmodul verweigert

Wenn Geräte das vertrauenswürdige Stammzertifikat empfangen, aber das PFX-Zertifikat nicht, und das NDESConnector-Protokoll die Zeichenfolge **Übermittlung fehlgeschlagen: Verweigert vom Richtlinienmodul** enthält, wie im folgenden Beispiel gezeigt:

```
IssuePfx - The submission failed: Denied by Policy Module
IssuePfx -Generic Exception: System.InvalidOperationException: IssuePfx - The submission failed
   at Microsoft.Management.Services.NdesConnector.MicrosoftCA.GetCertificate(PfxRequestDataStorage pfxRequestData, String containerName, String& certificate, String& password)
Issuing Pfx certificate for Device ID <Device ID> failed  
```

#### <a name="cause--computer-account-permissions-to-the-certificate-template"></a>Ursache: Berechtigungen des Computerkontos für die Zertifikatvorlage

Dieses Problem tritt auf, wenn das Computerkonto des Servers, der den Intune Certificate Connector hostet, keine Berechtigungen für die Zertifikatvorlage hat.

**Lösung**:

1. Melden Sie sich bei Ihrer Unternehmenszertifizierungsstelle mit einem Konto an, das über Administratorrechte verfügt.
2. Öffnen Sie die Konsole **Zertifizierungsstelle**, klicken Sie mit der rechten Maustaste auf **Zertifikatvorlagen**, und wählen Sie dann „Verwalten“ aus.
3. Navigieren Sie zur Zertifikatvorlage, und öffnen Sie das Dialogfeld **Eigenschaften** der Vorlage.
4. Wählen Sie die Registerkarte **Sicherheit** aus, und fügen Sie das Computerkonto des Servers hinzu, auf dem Sie den Microsoft Intune Certificate Connector installiert haben. Weisen Sie diesem Konto die Berechtigungen **Lesen** und **Registrieren** zu.
5. Wählen Sie **Übernehmen** > **OK** aus, um die Zertifikatvorlage zu speichern. Schließen Sie anschließend die Konsole **Zertifikatvorlagen**.
6. Klicken Sie in der Konsole **Zertifizierungsstelle** mit der rechten Maustaste auf **Zertifikatvorlagen** > **Neu** > **Auszustellende Zertifikatvorlage**.
7. Wählen Sie die geänderte Zertifikatvorlage aus, und klicken Sie dann auf **OK**.

Weitere Informationen finden Sie unter [Konfigurieren von Zertifikatvorlagen in der Zertifizierungsstelle](../protect/certficates-pfx-configure.md#configure-certificate-templates-on-the-ca).

### <a name="certificate-profile-stuck-as-pending"></a>Zertifikatprofil hängt als „Ausstehend“

Im Microsoft Endpoint Manager Admin Center schlägt die Bereitstellung von PKCS-Zertifikatprofilen mit dem Status **Ausstehend** fehl. In der Protokolldatei von NDESConnector finden sich keine offensichtlichen Fehler.
Da die Ursache dieses Problems in den Protokollen nicht eindeutig bestimmt werden kann, gehen Sie die folgenden Ursachen durch.

#### <a name="cause-1---unprocessed-request-files"></a>Ursache 1: Nicht verarbeitete Anforderungsdateien

Überprüfen Sie die Anforderungsdateien auf Fehler, die angeben, warum sie nicht verarbeitet wurden.

1. Navigieren Sie auf dem Computer, auf dem sich der NDES-Connector befindet, im Datei-Explorer zu **%programfiles%\Microsoft Intune\PfxRequest**.
2. Überprüfen Sie mit Ihrem bevorzugten Text-Editor Dateien in den Ordnern **Failed** und **Processing**.

   > [!div class="mx-imgBorder"]
   > ![Überprüfen des Ordners PfxRequest](./media/troubleshoot-pkcs-certificate-profiles/pfxrequest-folder.png)

3. Suchen Sie in diesen Dateien nach Einträgen, die auf Fehler oder Probleme hinweisen. Schlagen Sie mithilfe einer webbasierten Suche die Fehlermeldungen nach, um Hinweise darauf zu erhalten, warum die Anforderung fehlgeschlagen ist, und um Lösungen für diese Probleme zu finden.

#### <a name="cause-2---misconfiguration-for-the-pkcs-certificate-profile"></a>Ursache 2: Falsche Konfiguration des PKCS-Zertifikatprofils

Wenn Sie Anforderungsdateien in den Ordnern **Failed**, **Processing** oder **Succeed** nicht finden, kann die Ursache sein, dass das falsche Zertifikat mit dem PKCS-Zertifikatprofil verknüpft ist. Beispielsweise ist dem Profil eine untergeordnete Zertifizierungsstelle zugeordnet, oder es wird das falsche Stammzertifikat verwendet.

**Lösung**:

1. Überprüfen Sie Ihr vertrauenswürdiges Zertifikatprofil, um sicherzustellen, dass Sie das Stammzertifikat Ihrer Unternehmenszertifizierungsstelle für Geräte bereitgestellt haben.
2. Überprüfen Sie Ihr PKCS-Zertifikatprofil, um sicherzustellen, dass es auf die richtige Zertifizierungsstelle, den richtigen Zertifikatstyp und das vertrauenswürdige Zertifikatprofil verweist, das das Stammzertifikat für Geräte bereitstellt.

Weitere Informationen finden Sie unter [Verwenden von Zertifikaten zur Authentifizierung](../protect/certificates-configure.md) in Microsoft Intune.

### <a name="error--2146875374-certsrv_e_subject_email_required"></a>Fehler: 2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED

PKCS-Zertifikate werden nicht bereitgestellt, und die Zertifikatkonsole der ausstellenden Zertifizierungsstelle zeigt eine Meldung mit der Zeichenfolge **-2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED** an, wie im folgenden Beispiel dargestellt:

```
Active Directory Certificate Services denied request abc123 because The Email name is unavailable and cannot be added to the Subject or Subject Alternate name. 0x80094812 (-2146875374 CERTSRV_E_SUBJECT_EMAIL_REQUIRED). The request was for CN=” Common Name”.  Additional information: Denied by Policy Module”.
```

#### <a name="cause---supply-in-the-request-is-miscongifured"></a>Ursache: „Informationen werden in der Anforderung angegeben“ falsch konfiguriert

Dieses Problem tritt auf, wenn im Dialogfeld **Eigenschaften** der Zertifikatvorlage auf der Registerkarte **Antragstellername** die Option **Informationen werden in der Anforderung angegeben** nicht aktiviert ist.

> [!div class="mx-imgBorder"]
> ![Konfigurieren der NDES-Eigenschaften](./media/troubleshoot-pkcs-certificate-profiles/supply-in-the-request.png)

**Lösung**:

Bearbeiten Sie die Vorlage, um das Konfigurationsproblem zu beheben:

1. Melden Sie sich bei Ihrer Unternehmenszertifizierungsstelle mit einem Konto an, das über Administratorrechte verfügt.
2. Öffnen Sie die Konsole **Zertifizierungsstelle**, klicken Sie mit der rechten Maustaste auf **Zertifikatvorlagen**, und klicken Sie dann auf **Verwalten**.
3. Öffnen Sie das Dialogfeld „Eigenschaften“ der Zertifikatvorlage.
4. Wählen Sie auf der Registerkarte **Antragstellername** die Option **Informationen werden in der Anforderung angegeben**.
5. Wählen Sie **OK** aus, um die Zertifikatvorlage zu speichern. Schließen Sie anschließend die Konsole **Zertifikatvorlagen**.
6. Klicken Sie in der Konsole **Zertifizierungsstelle** mit der rechten Maustaste auf **Vorlagen** > **Neu** > **Auszustellende Zertifikatvorlage**.
7. Wählen Sie die geänderte Zertifikatvorlage und dann **OK** aus.

## <a name="next-steps"></a>Nächste Schritte

Wenn Sie weiterhin eine Lösung benötigen oder weitere Informationen zu Intune suchen, stellen Sie eine Frage in unserem [Microsoft Intune-Forum](https://social.technet.microsoft.com/Forums/home?category=microsoftintune&filter=alltypes&sort=lastpostdesc). Viele Supporttechniker, MVPs und Mitglieder unseres Entwicklungsteams suchen die Foren häufig auf, sodass eine gute Chance auf Hilfe gibt.

Informationen zum Öffnen einer Supportanfrage beim Microsoft Intune-Produktsupportteam finden Sie unter [Anfordern von Support für Microsoft Intune](../fundamentals/get-support.md).
Weitere Informationen zur Bereitstellung von PKCS-Zertifikaten finden Sie in den folgenden Artikeln:

- [Konfigurieren und Verwenden Ihrer PKCS-Zertifikate mit Intune](../protect/certficates-pfx-configure.md)
- [Konfigurieren eines Zertifikatprofils für Ihre Geräte in Microsoft Intune](../protect/certificates-configure.md)
- [Entfernen von SCEP- und PKCS-Zertifikaten in Microsoft Intune](../protect/remove-certificates.md)
