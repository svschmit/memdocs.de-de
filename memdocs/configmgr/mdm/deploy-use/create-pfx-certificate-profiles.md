---
title: Erstellen von PFX-Zertifikatprofilen
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie PFX-Dateien in Configuration Manager verwenden, um benutzerspezifische Zertifikate zu generieren, die den verschlüsselten Datenaustausch unterstützen.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d240a836-c49b-49ab-a920-784c062d6748
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b45474484629b437f2548fb375075cfe55275ee2
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724574"
---
# <a name="create-pfx-certificate-profiles-using-a-certificate-authority"></a>Erstellen von PFX-Zertifikatprofilen mit einer Zertifizierungsstelle

*Gilt für: Configuration Manager (Current Branch)*

Erfahren Sie, wie Sie ein Zertifikat Profil erstellen, das eine Zertifizierungsstelle für Anmelde Informationen verwendet. In diesem Artikel werden bestimmte Informationen zu PFX-Zertifikat Profilen (Personal Information Exchange) hervorgehoben. Weitere Informationen zum Erstellen und Konfigurieren dieser Profile finden Sie unter [Zertifikat profile](../../protect/deploy-use/introduction-to-certificate-profiles.md).

Mit Configuration Manager können Sie ein pfx-Zertifikat Profil mithilfe von Anmelde Informationen erstellen, die von einer Zertifizierungsstelle ausgestellt wurden. Sie können Microsoft oder Entrust als Zertifizierungsstelle auswählen. Bei der Bereitstellung für Benutzer Geräte generieren PFX-Dateien benutzerspezifische Zertifikate, um den verschlüsselten Datenaustausch zu unterstützen.

Informationen zum Importieren von Zertifikat Anmelde Informationen aus vorhandenen Zertifikat Dateien finden Sie unter [Importieren von pfx-Zertifikat Profilen](import-pfx-certificate-profiles.md).

## <a name="prerequisites"></a>Voraussetzungen

Bevor Sie mit dem Erstellen eines Zertifikat Profils beginnen, stellen Sie sicher, dass die erforderlichen Voraussetzungen erfüllt sind. Weitere Informationen finden Sie unter [Voraussetzungen für Zertifikat profile](../../protect/plan-design/prerequisites-for-certificate-profiles.md). Für pfx-Zertifikat profile benötigen Sie z. b. eine Standortsystem Rolle für den [Zertifikat Registrierungspunkt](../../protect/deploy-use/certificate-infrastructure.md#step-2---install-and-configure-the-certificate-registration-point) .

## <a name="create-a-profile"></a>Erstellen eines Profils  

1. Wechseln Sie in der Configuration Manager Konsole zum Arbeitsbereich bestand **und** Kompatibilität, erweitern **Sie Konformitäts Einstellungen**, erweitern Sie **Zugriff auf Unternehmensressourcen**, und wählen Sie dann **Zertifikat profile**aus.

1. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Erstellen** die Option **Zertifikatsprofil erstellen** aus.

1. Geben Sie auf der Seite **Allgemein** des **Assistenten zum Erstellen von Zertifikat Profilen**die folgenden Informationen an:  

    - **Name**: Geben Sie einen eindeutigen Namen für das Zertifikatprofil ein. Sie können maximal 256 Zeichen verwenden.  

    - **Beschreibung**: Geben Sie eine Beschreibung mit einem Überblick über das Zertifikat Profil ein, mit dessen Hilfe Sie es in der Configuration Manager-Konsole identifizieren können. Sie können maximal 256 Zeichen verwenden.  

1. Wählen Sie die Option privater **Informationsaustausch-PKCS-#12 (PFX)-Einstellungen-erstellen**. Mit dieser Option wird ein Zertifikat im Auftrag eines Benutzers von einer verbundenen lokalen Zertifizierungsstelle (ca) angefordert. Wählen Sie Ihre Zertifizierungsstelle aus: **Microsoft** oder **Entrust Datacard**.

    > [!NOTE]
    > Die **Import** Option Ruft Informationen aus einem vorhandenen Zertifikat ab, um ein Zertifikat Profil zu erstellen. Weitere Informationen finden Sie unter [Importieren von PFX-Zertifikatprofilen](import-pfx-certificate-profiles.md).

1. Wählen Sie auf der Seite **Unterstützte Plattformen** die Betriebssystemversionen aus, die dieses Zertifikat Profil unterstützt. Weitere Informationen zu unterstützten Betriebssystemversionen für Ihre Version von Configuration Manager finden Sie [unter Unterstützte Betriebssystemversionen für Clients und Geräte](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md).

1. Wählen Sie auf der Seite **Zertifizierungs** stellen den Zertifikat Registrierungspunkt aus, um die PFX-Zertifikate zu verarbeiten:

    1. **Primärer Standort**: Wählen Sie den Server aus, der die CRP-Rolle für die Zertifizierungsstelle enthält.
    1. **Zertifizierungs**stellen: Wählen Sie die relevante Zertifizierungsstelle aus.

    Weitere Informationen finden Sie unter [Zertifikatinfrastruktur](../../protect/deploy-use/certificate-infrastructure.md).

Die Einstellungen auf der Seite **PFX-Zertifikat** variieren abhängig von der ausgewählten Zertifizierungsstelle auf der Seite **Allgemein** :

- [Microsoft-Zertifizierungsstelle](#bkmk_microsoft)
- [Entrust Datacard Zertifizierungsstelle](#bkmk_entrust)

### <a name="configure-pfx-certificate-settings-for-microsoft-ca"></a><a name="bkmk_microsoft"></a>Konfigurieren der **PFX-Zertifikat** Einstellungen für Microsoft ca

1. Wählen Sie als **Name der Zertifikat Vorlage**die Zertifikat Vorlage aus.

1. Aktivieren Sie die **Zertifikat Verwendung**, um das Zertifikat Profil für die S/MIME-Signierung oder-Verschlüsselung zu verwenden.

    Wenn Sie diese Option aktivieren, werden alle PFX-Zertifikate, die dem Ziel Benutzer zugeordnet sind, allen Geräten übermittelt. Wenn Sie diese Option nicht aktivieren, erhält jedes Gerät ein eindeutiges Zertifikat.  

1. Legen Sie für **Format des Antragstellernamens** entweder die Option **Allgemeiner Name** oder **Vollständiger definierter Name** fest. Wenn Sie nicht sicher sind, welche Verwendung Sie verwenden, wenden Sie sich an Ihren Zertifizierungsstellen Administrator.

1. Aktivieren Sie für den alternativen Antragsteller **Namen**die **e-Mail-Adresse** und den Benutzer Prinzipal **Namen (UPN)** entsprechend Ihrer Zertifizierungsstelle.

1. **Erneuerungs Schwellenwert**: legt fest, wann Zertifikate automatisch erneuert werden, basierend auf dem Prozentsatz der verbleibenden Zeit vor dem Ablauf.

1. Geben Sie mit der Option **Gültigkeitsdauer des Zertifikats** den Zeitraum an, in dem das Zertifikats gültig ist.

1. Wenn der Zertifikat Registrierungspunkt Active Directory Anmelde Informationen angibt, aktivieren Sie **Active Directory Veröffentlichung**.

1. Wenn Sie eine oder mehrere unterstützte Windows 10-Plattformen ausgewählt haben:

    1. Legen Sie den **Windows-Zertifikat Speicher** auf **Benutzer**fest. (Die Option **lokaler Computer** stellt keine Zertifikate bereit, wählen Sie Sie nicht aus.)

    1. Wählen Sie einen der folgenden **Schlüsselspeicher Anbieter (Key Storage Provider, KSP)** aus:

        - **In Trusted Platform Module (TPM) installieren (sofern vorhanden)**  
        - **In Trusted Platform Module (TPM) installieren, andernfalls Fehler**
        - **In Windows Hello for Business installieren, andernfalls Fehler**
        - **In Softwareschlüsselspeicher-Anbieter installieren**

1. Schließen Sie den Assistenten ab.

### <a name="configure-pfx-certificate-settings-for-entrust-datacard-ca"></a><a name="bkmk_entrust"></a>Konfigurieren der **PFX-Zertifikat** Einstellungen für Entrust Datacard Zertifizierungsstelle

1. Wählen Sie für die **Konfiguration der digitalen ID**das Konfigurations Profil aus. Der Entrust-Administrator erstellt die Konfigurationsoptionen für die digitale ID.

1. Aktivieren Sie die **Zertifikat Verwendung**, um das Zertifikat Profil für die S/MIME-Signierung oder-Verschlüsselung zu verwenden.

    Wenn Sie diese Option aktivieren, werden alle PFX-Zertifikate, die dem Ziel Benutzer zugeordnet sind, allen Geräten übermittelt. Wenn Sie diese Option nicht aktivieren, erhält jedes Gerät ein eindeutiges Zertifikat.  

1. Wählen Sie **Format**aus, um Configuration Manager Feldern Entrust-Format Token für den Antragsteller **Namen** zuzuordnen.

    Im Dialog **Certificate Name Formatting (Zertifikatsnamenformatierung)** werden alle Entrust-Variablen aufgeführt, die mit der Konfiguration der digitalen ID in Verbindung stehen. Wählen Sie für jede Entrust-Variable die entsprechenden Configuration Manager Felder aus.

1. Um den unterstützten LDAP-Variablen Entrust **Subject Alternative Name** Tokens zuzuordnen, wählen Sie **Format**aus.

    Im Dialog **Certificate Name Formatting (Zertifikatsnamenformatierung)** werden alle Entrust-Variablen aufgeführt, die mit der Konfiguration der digitalen ID in Verbindung stehen. Wählen Sie für jede Entrust-Variable die entsprechende LDAP-Variable aus.

1. **Erneuerungs Schwellenwert**: legt fest, wann Zertifikate automatisch erneuert werden, basierend auf dem Prozentsatz der verbleibenden Zeit vor dem Ablauf.

1. Geben Sie mit der Option **Gültigkeitsdauer des Zertifikats** den Zeitraum an, in dem das Zertifikats gültig ist.

1. Wenn der Zertifikat Registrierungspunkt Active Directory Anmelde Informationen angibt, aktivieren Sie **Active Directory Veröffentlichung**.

1. Wenn Sie eine oder mehrere unterstützte Windows 10-Plattformen ausgewählt haben:

    1. Legen Sie den **Windows-Zertifikat Speicher** auf **Benutzer**fest. (Die Option **lokaler Computer** stellt keine Zertifikate bereit, wählen Sie Sie nicht aus.)

    1. Wählen Sie einen der folgenden **Schlüsselspeicher Anbieter (Key Storage Provider, KSP)** aus:

        - **In Trusted Platform Module (TPM) installieren (sofern vorhanden)**  
        - **In Trusted Platform Module (TPM) installieren, andernfalls Fehler**
        - **In Windows Hello for Business installieren, andernfalls Fehler**
        - **In Softwareschlüsselspeicher-Anbieter installieren**

1. Schließen Sie den Assistenten ab.

## <a name="deploy-the-profile"></a>Bereitstellen des Profils

Nachdem Sie ein Zertifikat Profil erstellt haben, ist es jetzt im Knoten **Zertifikat profile** verfügbar. Weitere Informationen zur Bereitstellung finden Sie unter Bereitstellen von [Ressourcen Zugriffs Profilen](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).

## <a name="see-also"></a>Weitere Informationen:

[Erstellen eines neuen Zertifikat Profils](../../protect/deploy-use/create-certificate-profiles.md)

[Importieren von PFX-Zertifikatprofilen](import-pfx-certificate-profiles.md)

[Bereitstellen von WLAN-, VPN-, E-Mail- und Zertifikatprofilen](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)
