---
title: Importieren von PFX-Zertifikatprofilen
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie PFX-Dateien in Configuration Manager verwenden, um benutzerspezifische Zertifikate zu generieren, die den verschlüsselten Datenaustausch unterstützen.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e3bb3e13-3037-4122-93bc-504bfd080a4d
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: df5dfdeab010012a258fe59612a348c269081c45
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700496"
---
# <a name="import-pfx-certificate-profiles"></a>Importieren von PFX-Zertifikatprofilen

*Gilt für: Configuration Manager (Current Branch)*

Erfahren Sie, wie Sie ein Zertifikat Profil erstellen, indem Sie Anmelde Informationen aus externen Zertifikaten importieren. In diesem Artikel werden bestimmte Informationen zu PFX-Zertifikat Profilen (Personal Information Exchange) hervorgehoben. Weitere Informationen zum Erstellen und Konfigurieren dieser Profile finden Sie unter [Zertifikat profile](../../protect/deploy-use/introduction-to-certificate-profiles.md).

Configuration Manager unterstützt verschiedene Arten von Zertifikat speichern für verschiedene Geräte und Betriebssystemversionen. Beispielsweise Windows 10 und Windows 10 Mobile. Weitere Informationen finden Sie unter [Voraussetzungen für Zertifikat profile](../../protect/plan-design/prerequisites-for-certificate-profiles.md).

Verwenden Sie Configuration Manager, um Zertifikat Anmelde Informationen zu importieren und dann PFX-Dateien auf Geräten bereitzustellen. Sie können diese Dateien verwenden, um benutzerspezifische Zertifikate zur Unterstützung von verschlüsseltem Datenaustausch zu generieren.

> [!TIP]  
> Eine schrittweise exemplarische Vorgehensweise für diesen Prozess finden Sie im Blogbeitrag Erstellen und Bereitstellen von [PFX-Zertifikat Profilen in Configuration Manager](/archive/blogs/karanrustagi/how-to-create-and-deploy-pfx-certificate-profiles-in-configuration-manager).  

## <a name="create-a-profile"></a>Ein Profil erstellen

1. Wechseln Sie in der Configuration Manager Konsole zum Arbeitsbereich bestand **und** Kompatibilität, erweitern **Sie Konformitäts Einstellungen**, erweitern Sie **Zugriff auf Unternehmensressourcen**, und wählen Sie dann **Zertifikat profile**aus.

1. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Erstellen** die Option **Zertifikatsprofil erstellen** aus.

1. Geben Sie auf der Seite **Allgemein** des **Assistenten zum Erstellen von Zertifikat Profilen**die folgenden Informationen an:  

    - **Name**: Geben Sie einen eindeutigen Namen für das Zertifikatprofil ein. Sie können maximal 256 Zeichen verwenden.  

    - **Beschreibung**: Geben Sie eine Beschreibung mit einem Überblick über das Zertifikat Profil ein, mit dessen Hilfe Sie es in der Configuration Manager-Konsole identifizieren können. Sie können maximal 256 Zeichen verwenden.  

1. Wählen Sie **Einstellungen für persönlichen Informationsaustausch-PKCS-#12 (PFX)-importieren**aus. Diese Option importiert Informationen aus einem vorhandenen Zertifikat, um ein Zertifikat Profil zu erstellen.

    > [!NOTE]
    > Mit der Option **Erstellen** wird ein Zertifikat im Namen eines Benutzers von einer verbundenen lokalen Zertifizierungsstelle (ca) angefordert. Bei diesem Vorgang wird das Zertifikat auf sichere Weise als PFX-Dateien an Clients übermittelt. Weitere Informationen finden Sie unter [Erstellen von pfx-Zertifikat Profilen mit einer Zertifizierungs](create-pfx-certificate-profiles.md)Stelle.

1. Geben Sie auf der Seite **PFX-Zertifikat** des **Assistenten zum Erstellen von Zertifikat Profilen**den Geräte Schlüsselspeicher Anbieter (KSP) an:

    - **In Trusted Platform Module (TPM) installieren (sofern vorhanden)**  
    - **In Trusted Platform Module (TPM) installieren, andernfalls Fehler**
    - **In Windows Hello for Business installieren, andernfalls Fehler**
    - **In Softwareschlüsselspeicher-Anbieter installieren**

1. Wählen Sie auf der Seite **Unterstützte Plattformen** die unterstützten Geräte Plattformen aus.

1. Schließen Sie den Assistenten ab.

## <a name="deploy-the-profile"></a>Bereitstellen des Profils

Nachdem Sie ein Zertifikat Profil erstellt und bereitgestellt haben, ist es jetzt im Knoten **Zertifikat profile** verfügbar. Weitere Informationen zur Bereitstellung finden Sie unter Bereitstellen von [Ressourcen Zugriffs Profilen](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md).

## <a name="assign-primary-users"></a>Primäre Benutzer zuweisen

Weisen Sie die Ziel Benutzer als primäre Benutzer auf den Windows 10-Geräten zu, auf denen Sie die PFX-Zertifikate installieren müssen. Weitere Informationen finden Sie unter [Affinität zwischen Benutzer und Gerät](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

## <a name="provision-a-create-pfx-script"></a>Bereitstellen eines PFX-Skripts

Verwenden Sie zum Importieren eines PFX-Zertifikats die folgenden Configuration Manager PowerShell-Cmdlets, um ein PFX-Erstellungs Skript bereitzustellen:

- [Get-cmclientcertifi-epfx](/powershell/module/configurationmanager/get-cmclientcertificatepfx?view=sccm-ps)
- [Import-cmclientcertifialisiepfx](/powershell/module/configurationmanager/import-cmclientcertificatepfx?view=sccm-ps)
- [Remove-cmclientcertifialisiepfx](/powershell/module/configurationmanager/remove-cmclientcertificatepfx?view=sccm-ps)

### <a name="example-script"></a>Beispielskript

Öffnen Sie PowerShell auf einem Computer mit der Configuration Manager Konsole, um eine PFX-Datei in einem Zertifikat Profil für einen Benutzer bereitzustellen. Ändern Sie die Variablen mit Werten aus Ihrer Umgebung.

``` PowerShell
# The display name of your PFX Import certificate profile
$PfxProfileDisplayName = "ImportPFX"

# The password you used to protect/encrypt the external PFX file that was created/exported from your certificate storage provider
# If you omit this password, PowerShell will securely prompt you for it. You can specify it as a parameter for process automation.
$password = ""

# The username of the user who will receive this PFX certificate on their device
$user = "Melissa"

# The full path to the PFX file you exported from the certificate store
$pfxfile = "c:\p1.pfx"

# If the target user isn't in the same domain as the user running this script, specify a different domain
Import-CMClientCertificatePfx -UserName "$env:USERDOMAIN\$user" -Password (ConvertTo-SecureString -String $password -AsPlainText -Force) -CertificateProfilePfx (Get-CMCertificateProfilePfx -Fast -Name $PfxProfileDisplayName) -Path $pfxfile
```

## <a name="see-also"></a>Weitere Informationen

[Erstellen eines neuen Zertifikat Profils](../../protect/deploy-use/create-certificate-profiles.md)

[Erstellen von PFX-Zertifikatprofilen mit einer Zertifizierungsstelle](create-pfx-certificate-profiles.md)

[Bereitstellen von WLAN-, VPN-, E-Mail- und Zertifikatprofilen](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)