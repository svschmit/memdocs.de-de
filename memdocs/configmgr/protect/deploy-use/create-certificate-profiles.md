---
title: Erstellen von SCEP-Zertifikatprofilen
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie mithilfe von Zertifikatprofilen verwaltete Geräte mit den benötigten Zertifikaten bereitstellen.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 634d612c-92d7-4c03-873a-b2e730c9a72d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 84f1ea48887f89cf06ed4b41d0de0dfc24e9d508
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88697125"
---
# <a name="create-certificate-profiles"></a>Erstellen von Zertifikatprofilen

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie Zertifikatprofile in Configuration Manager, um für verwaltete Geräte die Zertifikate bereitzustellen, die sie für den Zugriff auf Unternehmensressourcen benötigen. Legen Sie vor dem Erstellen von Zertifikatprofilen die Zertifikatinfrastruktur wie unter [Erstellen von Zertifikatprofilen](certificate-infrastructure.md) beschrieben fest.  

> [!TIP]
> Ziehen Sie bei gemeinsam verwalteten Geräten in Betracht, die [**Ressourcenzugriffsrichtlinien** nach Intune zu verschieben](../../comanage/workloads.md#resource-access-policies). Verwenden Sie dann Intune-Richtlinien, um diese Zertifikate zu verwalten. Weitere Informationen finden Sie unter [Verschieben von Workloads](../../comanage/how-to-switch-workloads.md).

In diesem Artikel wird beschrieben, wie Sie vertrauenswürdige Stamm- und SCEP-Zertifikatprofile (Simple Certificate Enrollment-Protokoll) erstellen können. Wenn Sie die PFX-Zertifikatprofile erstellen möchten, sollten Sie den Artikel [Erstellen von PFX-Zertifikatprofilen](../../mdm/deploy-use/create-pfx-certificate-profiles.md) lesen.

Erstellen eines Zertifikatprofils:

1. Starten Sie den Assistenten zum Erstellen von Zertifikatprofilen.
1. Stellen Sie allgemeine Informationen zum Zertifikat bereit.
1. Konfigurieren Sie ein Zertifikat über eine vertrauenswürdige Zertifizierungsstelle (CA).  
1. Konfigurieren Sie die SCEP-Zertifikatinformationen.  
1. Geben Sie die unterstützten Plattformen für das Zertifikatprofil an.

## <a name="start-the-wizard"></a>Starten des Assistenten  

So starten Sie den Assistenten zum Erstellen von Zertifikatprofilen

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**, erweitern Sie **Konformitätseinstellungen** und dann **Zugriff auf Unternehmensressourcen**, und wählen Sie den Knoten **Zertifikatsprofile** aus.  

1. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Erstellen** die Option **Zertifikatsprofil erstellen** aus.  

## <a name="general"></a>Allgemein

Geben Sie auf der Seite **Allgemein** des Assistenten zum Erstellen von Zertifikatprofilen die folgenden Informationen an:  

- **Name:** Geben Sie einen eindeutigen Namen für das Zertifikatprofil ein. Sie können maximal 256 Zeichen verwenden.  

- **Beschreibung:** Stellen Sie eine Beschreibung bereit, die eine Übersicht über das Zertifikatprofil bietet. Fügen Sie auch andere relevante Informationen hinzu, die helfen, sie in der Configuration Manager-Konsole zu identifizieren. Sie können maximal 256 Zeichen verwenden.  

- Geben Sie den Typ des Zertifikatprofils an, das Sie erstellen möchten:

  - **Vertrauenswürdiges Zertifikat der Zertifizierungsstelle**: Wählen Sie diesen Typ aus, wenn Sie ein vertrauenswürdiges Zertifikat der Stamm- oder Zwischenzertifizierungsstelle bereitstellen möchten, um eine Vertrauenskette zu bilden, wenn der Benutzer oder das Gerät sich bei einem anderen Gerät authentifizieren muss. Hierbei könnte es sich etwa um einen RADIUS-Server (Remote Authentication Dial-In User Service) oder einen VPN-Server (Virtual Private Network) handeln.
  
    Konfigurieren Sie darüber hinaus ein Profil mit einem vertrauenswürdigen Zertifikatsprofil der Zertifizierungsstelle, bevor Sie ein SCEP-Zertifikatprofil erstellen. In diesem Fall muss das vertrauenswürdige Zertifizierungsstellenzertifikat für die Zertifizierungsstelle sein, die das Zertifikat für den Benutzer oder das Gerät ausstellt.  

  - **Einstellungen für Simple Certificate Enrollment-Protokoll (SCEP)** : Wählen Sie diesen Typ aus, wenn Sie mit dem Simple Certificate Enrollment-Protokoll und dem Rollendienst „Registrierungsdienst für Netzwerkgeräte“ (Network Device Enrollment Service, NDES) ein Zertifikat für einen Benutzer oder ein Gerät anfordern möchten.

  - **Privater Informationsaustausch – PKCS #12 (PFX)-Einstellungen – Import**: Wählen Sie diese Option aus, um ein PFX-Zertifikat zu importieren. Weitere Informationen finden Sie unter [Importieren von PFX-Zertifikatprofilen](../../mdm/deploy-use/import-pfx-certificate-profiles.md).

  - **Privater Informationsaustausch – PKCS #12 (PFX)-Einstellungen – Erstellen**: Wählen Sie diese Option aus, um PFX-Zertifikate mithilfe einer Zertifizierungsstelle zu verarbeiten. Weitere Informationen finden Sie unter [Erstellen von PFX-Zertifikatprofilen](../../mdm/deploy-use/create-pfx-certificate-profiles.md).

## <a name="trusted-ca-certificate"></a>Vertrauenswürdiges Zertifikat der Zertifizierungsstelle  

> [!IMPORTANT]  
> Bevor Sie ein SCEP-Zertifikatsprofil erstellen, konfigurieren Sie mindestens ein vertrauenswürdiges Zertifikatsprofil der Zertifizierungsstelle.
>
> Wenn Sie nach der Bereitstellung des Zertifikats einen dieser Werte ändern, wird ein neues Zertifikat angefordert:
>
> - Schlüsselspeicheranbieter
> - Name der Zertifikatvorlage
> - Zertifikattyp
> - Format des Antragstellernamens
> - Alternativer Antragstellername
> - Gültigkeitsdauer des Zertifikats
> - Schlüsselverwendung
> - Schlüsselgröße
> - Erweiterte Schlüsselverwendung
> - Zertifikat der Stammzertifizierungsstelle

1. Geben Sie auf der Seite **Vertrauenswürdiges Zertifikat der Zertifizierungsstelle** des Assistenten zum Erstellen von Zertifikatprofilen die folgenden Informationen an:  

    - **Zertifikatdatei**: Wählen Sie **Importieren** aus, und navigieren Sie dann zur Zertifikatdatei.  

    - **Zielspeicher**: Wählen Sie für Geräte, die mehr als einen Zertifikatspeicher haben, den Speicherort des Zertifikats aus. Bei Geräten, die nur einen Speicher haben, wird diese Einstellung ignoriert.  

2. Stellen Sie mit dem Wert **Zertifikatfingerabdruck** sicher, dass Sie das richtige Zertifikat importiert haben.  

## <a name="scep-certificates"></a>SCEP-Zertifikate

### <a name="1-scep-servers"></a>1. SCEP-Server

Geben Sie auf der Seite **SCEP-Server** des Assistenten zum Erstellen von Zertifikatprofilen die URLs für die NDES-Server ein, die über SCEP Zertifikate ausstellen. Sie können eine NDES-URL auf Basis der Konfiguration des Zertifikatregistrierungspunkts automatisch zuweisen oder URLs manuell hinzufügen.  

### <a name="2-scep-enrollment"></a>2. SCEP-Registrierung

Schließen Sie die Seite **SCEP Enrollment** (SCEP-Anmeldung) des Assistenten zum Erstellen von Zertifikatprofilen ab.

- **Wiederholungen**: Geben Sie an, wie oft das Gerät die Zertifikatanforderung automatisch erneut an den NDES-Server sendet. Mit dieser Einstellung wird das Szenario unterstützt, bei dem eine Zertifikatanforderung von einem Zertifizierungsstellen-Manager genehmigt werden muss, bevor sie akzeptiert wird. Sie wird üblicherweise in Umgebungen mit hoher Sicherheit oder in Fällen verwendet, in denen eine eigenständige ausstellende Zertifizierungsstelle statt einer Unternehmenszertifizierungsstelle eingesetzt wird. Sie können diese Einstellung auch für Testzwecke nutzen, sodass Sie die Optionen der Zertifikatanforderung prüfen können, bevor die Zertifikatanforderung von der ausstellenden Zertifizierungsstelle verarbeitet wird. Verwenden Sie diese Einstellung zusammen mit der Einstellung **Wiederholungsverzögerung (Minuten)** .  

- **Wiederholungsverzögerung (Minuten)** : Geben Sie das Intervall in Minuten zwischen den Registrierungsversuchen an, wenn die Genehmigung durch einen Zertifizierungsstellen-Manager benötigt wird, bevor die Zertifikatanforderungen von der ausstellenden Zertifizierungsstelle verarbeitet werden. Wenn Sie die Genehmigung eines Managers zu Testzwecken verwenden, geben Sie einen niedrigen Wert an. Dann müssen Sie nicht lange warten, bis das Gerät die Zertifikatanforderung erneut versucht, nachdem Sie die Anforderung genehmigt haben.

    Wenn Sie die Genehmigung eines Managers in einem Produktionsnetzwerk verwenden, geben Sie einen höheren Wert an. Dieses Verhalten lässt dem Administrator der Zertifizierungsstelle genügend Zeit, ausstehende Genehmigungen zu erteilen oder zu verweigern.  

- **Verlängerungsschwellenwert (%)** : Geben Sie den Prozentsatz der Zertifikatgültigkeitsdauer an, die verbleibt, bevor das Gerät eine Erneuerung des Zertifikats anfordert.  

- **Schlüsselspeicheranbieter**: Geben Sie an, wo der Schlüssel für das Zertifikat gespeichert wird. Wählen Sie einen der folgenden Werte aus:  

  - **In Trusted Platform Module (TPM) installieren (sofern vorhanden)** : Installiert den Schlüssel im TPM. Wenn das TPM nicht vorhanden ist, wird der Schlüssel im Speicheranbieter für den Softwareschlüssel installiert.  

  - **In Trusted Platform Module (TPM) installieren (andernfalls Fehler)** : Installiert den Schlüssel im TPM. Wenn das TPM-Modul nicht vorhanden ist, tritt bei der Installation ein Fehler auf.  

  - **In Windows Hello for Business installieren, andernfalls Fehler**: Diese Option ist für Windows 10-Geräte verfügbar. Sie ermöglicht es Ihnen, das Zertifikat im Windows Hello for Business-Speicher zu speichern, der durch Multi-Factor Authentication geschützt ist. Weitere Informationen finden Sie unter [Windows Hello for Business](/windows/security/identity-protection/hello-for-business/hello-identity-verification).

    > [!NOTE]  
    > Diese Option unterstützt nicht die Smartcard-Anmeldung für die erweiterte Schlüsselverwendung auf der Seite „Zertifikateigenschaften“.

  - **In Softwareschlüsselspeicher-Anbieter installieren**: Installiert den Schlüssel im Speicheranbieter für den Softwareschlüssel.  

- **Geräte für die Zertifikatregistrierung**: Wenn Sie das Zertifikatprofil für eine Benutzersammlung bereitstellen, erlauben Sie die Zertifikatregistrierung nur auf dem primären Gerät des Benutzers oder auf jedem Gerät, auf dem sich der Benutzer anmeldet.

    Wenn Sie das Zertifikatprofil in einer Gerätesammlung bereitstellen, erlauben Sie die Zertifikatregistrierung nur für den primären Benutzer des Geräts oder für alle Benutzer, die sich auf dem Gerät anmelden.  

### <a name="3-certificate-properties"></a>3. Zertifikateigenschaften

Geben Sie auf der Seite **Zertifikateigenschaften** des Assistenten zum Erstellen von Zertifikatprofilen die folgenden Informationen an:  

- **Name der Zertifikatvorlage**: Wählen Sie den Namen einer Zertifikatvorlage aus, die Sie in NDES konfiguriert und zu einer ausstellenden Zertifizierungsstelle hinzugefügt haben. Ihr Benutzerkonto benötigt zum erfolgreichen Browsen zu Zertifikatvorlagen die Berechtigung **Lesen** für die Zertifikatvorlage. Wenn Sie nicht nach dem Zertifikat **suchen** können, geben Sie seinen Namen ein.  

  > [!IMPORTANT]
  > Wenn der Name der Zertifikatvorlage Nicht-ASCII-Zeichen enthält, wird das Zertifikat nicht bereitgestellt. (Ein Beispiel für diese Zeichen stammt aus dem chinesischen Alphabet.) Erstellen Sie zunächst eine Kopie der Zertifikatvorlage bei der Zertifizierungsstelle, um sicherzustellen, dass das Zertifikat bereitgestellt wird. Benennen Sie dann die Kopie unter Verwendung von ASCII-Zeichen um.  

  - Wenn Sie zur Auswahl des Zertifikatvorlagennamens zur Zertifikatvorlage *navigieren*, werden einige Felder auf der Seite automatisch aus der Zertifikatvorlage aufgefüllt. In einigen Fällen können Sie diese Werte erst ändern, wenn Sie eine andere Zertifikatvorlage auswählen.  

  - Wenn Sie den Namen der Zertifikatvorlage *eingeben*, stellen Sie sicher, dass der Name genau mit einer der Zertifikatvorlagen übereinstimmt. Er muss mit den Namen übereinstimmen, die in der Registrierung des NDES-Servers aufgeführt sind. Achten Sie darauf, dass Sie den Namen der Zertifikatvorlage und nicht den Anzeigenamen der Zertifikatvorlage angeben.  

    Navigieren Sie zum folgenden Registrierungsschlüssel, um die Namen der Zertifikatvorlagen zu suchen: `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography\MSCEP`. Die Zertifikatvorlagen werden als Werte für **EncryptionTemplate**, **GeneralPurposeTemplate** und **SignatureTemplate** aufgeführt. Standardmäßig ist der Wert für die drei Zertifikatvorlagen **IPSECIntermediateOffline**. Dieser Wert entspricht dem Anzeigenamen **IPSec (Offlineanforderung)** .  

    > [!WARNING]  
    > Wenn Sie den Namen der Zertifikatvorlage eingeben, kann Configuration Manager den Inhalt der Zertifikatvorlage nicht überprüfen. Möglicherweise können Sie Optionen auswählen, die von der Zertifikatvorlage nicht unterstützt werden, was zu einer fehlgeschlagenen Zertifikatanforderung führen kann. Wenn dieses Verhalten auftritt, wird in der Datei CPR.log eine Fehlermeldung für w3wp.exe angezeigt, die darauf hinweist, dass der Vorlagenname in der Zertifikatsignieranforderung (CSR) und die Abfrage nicht übereinstimmen.  
    >
    > Wenn Sie den Namen der Zertifikatvorlage eingeben, der für den Wert **GeneralPurposeTemplate** angegeben ist, wählen Sie für dieses Zertifikatprofil die Optionen **Schlüsselverschlüsselung** und **Digitale Signatur** aus. Wenn Sie in diesem Zertifikatprofil nur die Option **Schlüsselverschlüsselung** aktivieren möchten, geben Sie den Namen der Zertifikatvorlage für den Schlüssel **EncryptionTemplate** an. Wenn Sie in diesem Zertifikatprofil dagegen nur die Option **Digitale Signatur** aktivieren möchten, geben Sie den Namen der Zertifikatvorlage für den Schlüssel **SignatureTemplate** an.  

- **Zertifikattyp**: Wählen Sie aus, ob Sie das Zertifikat für ein Gerät oder einen Benutzer bereitstellen möchten.  

- **Format des Antragstellernamens**: Wählen Sie aus, wie Configuration Manager den Antragstellernamen in der Zertifikatanforderung automatisch erstellen soll. Wenn das Zertifikat für einen Benutzer bestimmt ist, können Sie auch die E-Mail-Adresse des Benutzers im Antragstellernamen einschließen.

    > [!NOTE]  
    > Wenn Sie **IMEI-Nummer** oder **Seriennummer** auswählen, können Sie zwischen verschiedenen Geräten unterscheiden, die dem gleichen Benutzer gehören. Bei diesen Geräten kann z.B. der allgemeine Name identisch sein, nicht aber die IMEI-Nummer oder Seriennummer. Wenn das Gerät keine IMEI- oder Seriennummer meldet, wird das Zertifikat mit dem allgemeinen Namen ausgegeben.

- **Alternativer Antragstellername**: Geben Sie an, wie Configuration Manager die Werte für den alternativen Antragstellernamen (Subject Alternative Name, SAN) in der Zertifikatanforderung automatisch erstellen soll. Beispiel: Wenn Sie einen Benutzerzertifikattyp ausgewählt haben, könnten Sie in den alternativen Antragstellernamen den Benutzerprinzipalnamen (User Principal Name, UPN) aufnehmen. Wenn das Clientzertifikat einen Netzwerkrichtlinienserver authentifizieren soll, legen Sie den alternativen Antragstellernamen auf den Benutzerprinzipalnamen fest.  

- **Gültigkeitsdauer des Zertifikats**: Wenn Sie für die ausstellende Zertifizierungsstelle eine benutzerdefinierte Gültigkeitsdauer festlegen, geben Sie die verbleibende Zeit bis zum Ablauf des Zertifikats an.

    > [!TIP]
    > Legen Sie mit der folgenden Befehlszeile eine benutzerdefinierte Gültigkeitsdauer fest: `certutil -setreg Policy\EditFlags +EDITF_ATTRIBUTEENDDATE`
    > Weitere Informationen zu diesem Befehl finden Sie unter [Zertifikatinfrastruktur](certificate-infrastructure.md).  

    Sie können einen niedrigeren Wert als den für die Gültigkeitsdauer in der angegebenen Zertifikatvorlage angeben, aber keinen höheren. Beispiel: Wenn die Gültigkeitsdauer des Zertifikats in der Zertifikatvorlage zwei Jahre beträgt, können Sie als Wert ein Jahr angeben, aber nicht fünf Jahre. Zudem muss der Wert niedriger als die verbleibende Gültigkeitsdauer des Zertifikats der ausstellenden Zertifizierungsstelle sein.  

- **Schlüsselverwendung**: Geben Sie Schlüsselverwendungsoptionen für das Zertifikat an. Wählen Sie aus den folgenden Optionen:  

  - **Schlüsselverschlüsselung**: Der Schlüsselaustausch wird nur gestattet, wenn der Schlüssel verschlüsselt ist.  

  - **Digitale Signatur**: Der Schlüsselaustausch wird nur gestattet, wenn der Schutz des Schlüssels durch eine digitale Signatur unterstützt wird.  

  Wenn Sie nach einer Zertifikatvorlage gesucht haben, können Sie diese Einstellungen nicht ändern, es sei denn, Sie wählen eine andere Zertifikatvorlage aus.  

  Konfigurieren Sie die ausgewählte Zertifikatvorlage mit einer oder beiden der beiden oben genannten Optionen zur Schlüsselverwendung. Andernfalls wird die folgende Meldung in der Protokolldatei **Crp.log** für den Zertifikatregistrierungspunkt angezeigt: **Schlüsselverwendung in CSR und Abfrage stimmen nicht überein**.  

- **Schlüsselgröße (Bits)** : Wählen Sie die Größe des Schlüssels in Bits aus.  

- **Erweiterte Schlüsselverwendung**: Fügen Sie Werte für den beabsichtigten Zweck des Zertifikats hinzu. In den meisten Fällen erfordert das Zertifikat **Clientauthentifizierung**, damit der Benutzer bzw. das Gerät auf einem Server authentifiziert werden kann. Sie können nach Bedarf weitere Schlüsselverwendungen hinzufügen.  

- **Hashalgorithmus**: Wählen Sie einen der verfügbaren Hashalgorithmustypen, der für dieses Zertifikat verwendet werden soll. Wählen Sie die höchste Sicherheitsebene aus, die die verbundenen Geräten unterstützen.  

  > [!NOTE]  
  > **SHA-2** unterstützt SHA-256, SHA-384 und SHA-512. **SHA-3** unterstützt nur SHA-3.  

- **Zertifikat der Stammzertifizierungsstelle**: Wählen Sie ein Profil für ein Zertifikat der Stammzertifizierungsstelle aus, das Sie zuvor konfiguriert und für den Benutzer oder das Gerät bereitgestellt haben. Dieses Zertifizierungsstellenzertifikat muss das Stammzertifikat für die Zertifizierungsstelle sein, die das Zertifikat ausstellt, das Sie in diesem Zertifikatprofil konfigurieren.  

  > [!IMPORTANT]  
  > Wenn Sie ein Zertifikat der Stammzertifizierungsstelle angeben, das dem Benutzer oder Gerät nicht bereitgestellt wurde, wird die Anforderung des Zertifikats, das Sie in diesem Zertifikatprofil konfigurieren, von Configuration Manager nicht eingeleitet.  

## <a name="supported-platforms"></a>Unterstützte Plattformen  

Wählen Sie auf der Seite **Unterstützte Plattformen** des Assistenten zum Erstellen von Zertifikatprofilen die Betriebssystemversionen aus, unter denen das Zertifikatprofil installiert werden soll. Wählen Sie **Alle auswählen** aus, um das Zertifikatprofil unter allen verfügbaren Betriebssystemen zu installieren.

## <a name="next-steps"></a>Nächste Schritte

Das neue Zertifikatprofil wird im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Zertifikatprofile** angezeigt. Es ist bereit für die Bereitstellung für Benutzer oder Geräte. Weitere Informationen finden Sie unter [Bereitstellen von Profilen](deploy-wifi-vpn-email-cert-profiles.md).