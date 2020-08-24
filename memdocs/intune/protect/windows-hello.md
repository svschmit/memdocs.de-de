---
title: Integrieren von Windows Hello for Business in Microsoft Intune
titleSuffix: Microsoft Intune
description: Hier erfahren Sie, wie Sie während der Geräteregistrierung eine Richtlinie zum Steuern der Verwendung von Windows Hello for Business auf verwalteten Geräten erstellen.
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
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: shpate
ms.openlocfilehash: 7088bfd5b27d986e12a175de1bdea0bf060c3ad3
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252519"
---
# <a name="integrate-windows-hello-for-business-with-microsoft-intune"></a>Integrieren von Windows Hello for Business in Microsoft Intune  

Sie können Windows Hello for Business (früher Microsoft Passport for Work) während der Geräteregistrierung in Microsoft Intune integrieren.

Hello for Business ist eine alternative Anmeldemethode, die Active Directory oder ein Azure Active Directory-Konto verwendet, um ein Kennwort, eine Smartcard oder eine virtuelle Smartcard zu ersetzen. Damit können Sie anstelle eines Kennworts eine *Benutzergeste* zur Anmeldung verwenden. Eine Benutzeraktion kann eine PIN, eine biometrische Authentifizierung wie Windows Hello oder ein externes Gerät wie z. B. ein Fingerabdruckleser sein.

Intune integriert Hello for Business auf zwei Arten:

- **Mandantenweit** (*dieser Artikel)* : Sie können unter *Geräteregistrierung* eine Intune-Richtlinie erstellen. Diese Richtlinie gilt für die gesamte Organisation (mandantenweit). Sie unterstützt die Windows-Willkommensseite von Windows Autopilot und wird angewendet, wenn ein Gerät registriert wird.
- **Diskrete Gruppen:** Verwenden Sie für Geräte, die bereits in Intune registriert sind, das Gerätekonfigurationsprofil [**Identitätsschutz**](../protect/identity-protection-configure.md), um Geräte für Windows Hello for Business zu konfigurieren. Identitätsschutzprofile können für zugewiesene Benutzer oder Geräte gelten und werden beim Check-In angewendet.

Darüber hinaus unterstützt Intune die folgenden Richtlinientypen zur Verwaltung einiger Einstellungen für Windows Hello for Business:

- [**Sicherheitsbaselines**](../protect/security-baselines.md). Die folgenden Baselines enthalten Einstellungen für Windows Hello for Business:
  - [Microsoft Defender Advanced Threat Protection-Baselineeinstellungen](../protect/security-baseline-settings-defender-atp.md#windows-hello-for-business)
  - [Einstellungen der MDM-Sicherheitsbaselines für Windows](../protect/security-baseline-settings-mdm-all.md#windows-hello-for-business)
- [**Kontoschutz**](../protect/endpoint-security-account-protection-policy.md)-Richtlinie für Endpunktsicherheit. Sehen Sie sich die [Kontoschutzeinstellungen](../protect/endpoint-security-account-protection-profile-settings.md#account-protection) an.

In den nächsten Abschnitten dieses Artikels wird die Erstellung einer Windows Hello for Business-Standardrichtlinie für Ihre gesamte Organisation beschrieben.

> [!IMPORTANT]
> Vor dem Anniversary Update konnten Sie zwei unterschiedliche PINS für die Authentifizierung bei Ressourcen festlegen:
>
> - Die **Geräte-PIN** konnte zum Entsperren des Geräts und zur Verbindung mit Cloudressourcen verwendet werden.
> - Die **Arbeits-PIN** wurde für den Zugang zu Azure AD-Ressourcen auf persönlichen Geräten von Benutzern (BYOD) verwendet.
>
> Im Anniversary Update wurden diese beiden PINs in eine einzige Geräte-PIN zusammengeführt.
> Dieser neue PIN-Wert wird jetzt sowohl von allen Intune-Konfigurationsrichtlinien, die Sie zum Steuern der Geräte-PIN festlegen, als auch von allen konfigurierten Windows Hello for Business-Richtlinien festgelegt.
> Wenn Sie beide Richtlinientypen für die PIN-Steuerung eingerichtet haben, wird die Windows Hello for Business-Richtlinie angewendet.
> Um sicherzustellen, dass Richtlinienkonflikte gelöst werden und dass die PIN-Richtlinie korrekt angewendet wird, aktualisieren Sie Ihre Windows Hello for Business-Richtlinie auf die Einstellungen in der Konfigurationsrichtlinie. Fordern Sie auch die Benutzer auf, ihre Geräte in der Unternehmensportal-App zu synchronisieren.

## <a name="create-a-windows-hello-for-business-policy"></a>Erstellen einer Windows Hello for Business-Richtlinie

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Navigieren Sie zu **Geräte** >  **Registrierung** > **Geräte registrieren** > **Windows-Registrierung** > **Windows Hello for Business**. Daraufhin wird der Bereich „Windows Hello for Business“ geöffnet.

3. Wählen Sie aus den folgenden Optionen für **Konfigurieren von Windows Hello for Business**:

   - **Aktiviert**. Wählen Sie diese Einstellung aus, wenn Sie Windows Hello for Business-Einstellungen konfigurieren möchten.  Wenn Sie *Aktivieren* auswählen, werden zusätzliche Einstellungen für Windows Hello angezeigt, die für Geräte konfiguriert werden können.

   - **Deaktiviert**. Wählen Sie diese Option aus, wenn Sie Windows Hello for Business nicht während der Geräteregistrierung aktivieren möchten. Bei Deaktivierung können Geräte Windows Hello for Business nicht bereitstellen. Wenn *Deaktiviert* festgelegt ist, können Sie dennoch die folgenden Einstellungen für Windows Hello for Business konfigurieren, obwohl diese Richtlinie verhindert, dass Windows Hello for Business aktiviert werden kann.

   - **Nicht konfiguriert**. Wählen Sie diese Einstellung aus, wenn Sie Windows Hello for Business-Einstellungen nicht mit Intune steuern möchten. Vorhandene Windows Hello for Business-Einstellungen auf Windows 10-Geräten werden nicht geändert. Alle anderen Einstellungen in dem Bereich sind nicht verfügbar.

4. Wenn Sie im letzten Schritt **Aktiviert** ausgewählt haben, konfigurieren Sie die erforderlichen Einstellungen, die auf alle registrierten Windows 10-Geräte angewendet werden. Nachdem Sie diese Einstellungen konfiguriert haben, wählen Sie **Speichern** aus.

   - **Trusted Platform Module (TPM) verwenden**:

     Ein TPM-Chip bietet eine zusätzliche Sicherheitsebene für Daten. Wählen Sie einen der folgenden Werte aus:

     - **Erforderlich** (Standard). Nur Geräte mit verfügbarem TPM können Windows Hello for Business bereitstellen.
     - **Bevorzugt**. Geräte versuchen zunächst, ein TPM zu verwenden. Wenn diese Option nicht verfügbar ist, können sie die Softwareverschlüsselung verwenden.

   - **PIN-Mindestlänge** und **Maximale PIN-Länge**:

     Konfiguriert Geräte für die Verwendung der von Ihnen angegebenen minimalen und maximalen PIN-Länge, um eine sichere Anmeldung zu gewährleisten. Die Standard-PIN-Länge beträgt 6 Zeichen, aber Sie können eine Mindestlänge von 4 Zeichen erzwingen. Die maximale PIN-Länge ist 127 Zeichen.

   - **Kleinbuchstaben in PIN**, **Großbuchstaben in PIN**, und **Sonderzeichen in PIN**.

     Sie können eine stärkere PIN erzwingen, indem Sie die Nutzung von Großbuchstaben, Kleinbuchstaben und Sonderzeichen in der PIN vorschreiben. Wählen Sie für alle Einstellungen eine der folgenden Optionen aus:

     - **Zulässig**. Benutzer können den Zeichentyp in ihrer PIN verwenden, aber es ist nicht zwingend erforderlich.

     - **Erforderlich**. Benutzer müssen mindestens einen der Zeichentypen in ihrer PIN verwenden. Beispielsweise ist es üblich, die Verwendung mindestens eines Großbuchstabens und eines Sonderzeichens vorzuschreiben.

     - **Nicht zulässig** (Standard). Benutzer dürfen diese Zeichentypen in ihrer PIN nicht verwenden. (Dies trifft auch zu, wenn die Einstellung nicht konfiguriert ist.)

       Gilt für diese Sonderzeichen: **! " # $ % &amp; ' ( ) &#42; + , - . / : ; &lt; = &gt; ? @ [ \ ] ^ _ &#96; { &#124; } ~**

   - **PIN-Ablauf (Tage)** :

     Es wird empfohlen, ein Ablaufdatum für eine PIN anzugeben, nach dem sie vom Benutzer geändert werden muss. Die Standardeinstellung ist 41 Tage.

   - **PIN-Verlauf speichern**:

     Schränkt die Wiederverwendung zuvor verwendeter PINs ein. Standardmäßig können die letzten fünf PINs nicht erneut verwendet werden.

   - **Biometrische Authentifizierung zulassen**:

     Aktiviert die biometrische Authentifizierung, z. B. die Gesichtserkennung oder Fingerabdrücke, als Alternative zu einer PIN für Windows Hello for Business. Benutzer müssen für den Fall dennoch eine PIN konfigurieren, dass die biometrische Authentifizierung fehlschlägt. Es stehen die folgenden Optionen zur Auswahl:

     - **Ja**. Windows Hello for Business ermöglicht biometrische Authentifizierung.
     - **Nein**. Windows Hello for Business verhindert die biometrische Authentifizierung (für alle Arten von Konten).

   - **Erweitertes Antispoofing verwenden, falls verfügbar**:

     Hiermit wird konfiguriert, ob die Antispoofing-Features von Windows Hello auf Geräten verwendet werden, die dies unterstützen. Beispiel: Erkennen eines Fotos eines Gesichts anstelle eines echten Gesichts.

     Wenn diese Option auf **Ja** festgelegt ist, erfordert Windows von allen Benutzern die Verwendung von Antispoofing für Gesichtsmerkmale, sofern dies unterstützt wird.

   - **Anmeldung per Telefon zulassen:**

     Wenn diese Option auf **Ja** festgelegt ist, können die Benutzer einen Remote-Passport als tragbares Begleitgerät für die Authentifizierung von Desktopcomputern verwenden. Der Desktopcomputer muss mit Azure Active Directory verknüpft sein, und das Begleitgerät muss mit einer Windows Hello for Business-PIN konfiguriert werden.

## <a name="windows-holographic-for-business-support"></a>Unterstützung durch Windows Holographic for Business

Windows Holographic for Business unterstützt die folgenden Einstellungen für Windows Hello for Business:

- Trusted Platform Module (TPM) verwenden
- Mindestlänge für PIN
- Höchstlänge für PIN
- Kleinbuchstaben in PIN
- Großbuchstaben in PIN
- Sonderzeichen in PIN
- PIN-Ablauf (Tage)
- PIN-Verlauf speichern

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu Windows Hello for Business finden Sie im [Leitfaden](https://technet.microsoft.com/library/mt589441.aspx) in der Dokumentation zu Windows 10.
