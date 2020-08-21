---
title: Windows Hello for Business-Einstellungen
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Windows Hello for Business in Configuration Manager integrieren.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a95bc292-af10-4beb-ab56-2a815fc69304
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 4c8029cdda80d327cbed2a4c60c71ff1811e4723
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88698696"
---
# <a name="windows-hello-for-business-settings-in-configuration-manager"></a>Windows Hello for Business-Einstellungen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

<!--1245704-->
Configuration Manager kann in Windows Hello for Business integriert werden. (Dieses Feature war früher als Microsoft Passport for Work bekannt.) Windows Hello for Business ist eine alternative Anmeldemethode für Windows 10-Geräte. Hello for Business verwendet Active Directory oder ein Azure Active Directory-Konto, um ein Kennwort, eine Smartcard oder eine virtuelle Smartcard zu ersetzen. Mit Hello for Business können Sie anstelle eines Kennworts eine *Benutzeraktion* zur Anmeldung verwenden. Eine Benutzeraktion kann eine PIN, eine biometrische Authentifizierung oder ein externes Gerät wie ein Fingerabdruckscanner sein.

> [!Important]  
> Ab Version 1910 wird die zertifikatbasierte Authentifizierung mit Windows Hello for Business-Einstellungen in Configuration Manager nicht unterstützt. Weitere Informationen finden Sie unter [Veraltete Features](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md). Die schlüsselbasierte Authentifizierung ist nach wie vor gültig.
>
> Die Bereitstellung einer Registrierungsstelle für Azure Directory-Verbunddienste (Active Directory Federation Services Registration Authority, ADFS RA) ist einfacher und bietet eine höhere Benutzerfreundlichkeit sowie eine deterministischere Oberfläche für die Zertifikatregistrierung. Verwenden Sie ADFS RA für die zertifikatbasierte Authentifizierung mit Windows Hello for Business.
>
> Ziehen Sie bei gemeinsam verwalteten Geräten in Betracht, die [**Ressourcenzugriffsrichtlinien** nach Intune zu verschieben](../../comanage/workloads.md#resource-access-policies). Verwenden Sie dann Intune-Richtlinien, um diese Zertifikate zu verwalten. Weitere Informationen finden Sie unter [Verschieben von Workloads](../../comanage/how-to-switch-workloads.md).

Weitere Informationen finden Sie unter [Windows Hello for Business](/windows/security/identity-protection/hello-for-business/hello-identity-verification).

> [!Note]  
> Configuration Manager aktiviert dieses optionale Feature nicht automatisch. Sie müssen dieses Feature aktivieren, bevor Sie es verwenden. Weitere Informationen finden Sie unter [Enable optional features from updates (Aktivieren optionaler Features von Updates)](../../core/servers/manage/install-in-console-updates.md#bkmk_options).<!--505213-->  

Configuration Manager kann auf folgende Art und Weise in Windows Hello for Business integriert werden:  

- Steuern der Gesten, die Benutzer zur Anmeldung verwenden können.  

- Speichern von Authentifizierungszertifikaten im Windows Hello for Business-Schlüsselspeicheranbieter (Key Storage Provider, KSP). Weitere Informationen finden Sie unter [Zertifikatprofile](introduction-to-certificate-profiles.md).  

- Erstellen Sie ein Windows Hello for Business-Profil, um seine Einstellungen auf Windows 10-Geräten zu steuern, die in Domänen eingebunden sind und auf denen der Configuration Manager-Client ausgeführt wird, und stellen Sie das Profil bereit. Ab Version 1910 können Sie die zertifikatbasierte Authentifizierung nicht mehr verwenden. Beim Verwenden der schlüsselbasierten Authentifizierung müssen Sie kein Zertifikatprofil bereitstellen.

## <a name="configure-a-profile"></a>Konfigurieren eines Profils  

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**. Erweitern Sie **Konformitätseinstellungen**, dann **Zugriff auf Unternehmensressourcen**, und wählen Sie den Knoten **Windows Hello for Business-Profile** aus.

1. Wählen Sie im Menüband **Windows Hello for Business-Profil erstellen** aus, um den Profil-Assistenten zu starten.

1. Geben Sie auf der Seite **Allgemein** einen Namen und optional eine Beschreibung für dieses Profil an.

1. Wählen Sie auf der Seite **Unterstützte Plattformen** die Betriebssystemversionen aus, für die dieses Profil gelten soll.

1. Konfigurieren Sie auf der Seite **Einstellungen** die folgenden Einstellungen:

    - **Konfigurieren Sie Windows Hello for Business**: Geben Sie an, ob dieses Profil Hello for Business aktiviert, deaktiviert oder nicht konfiguriert.

    - **Trusted Platform Module (TPM) verwenden**: Ein TPM bietet zusätzliche Sicherheit für Daten. Wählen Sie einen der folgenden Werte aus:  

      - **Erforderlich**: Nur Geräte mit verfügbarem TPM können Windows Hello for Business bereitstellen.  

      - **Bevorzugt**: Geräte versuchen zunächst, ein TPM zu verwenden. Wenn diese Option nicht verfügbar ist, können sie die Softwareverschlüsselung verwenden.

    - **Authentifizierungsmethode**: Legen Sie diese Option auf **Nicht konfiguriert** oder **Schlüsselbasiert** fest.

        > [!NOTE]
        > Ab Version 1910 wird die zertifikatbasierte Authentifizierung mit Windows Hello for Business-Einstellungen in Configuration Manager nicht unterstützt.

    - **PIN-Mindestlänge konfigurieren**: Wenn Sie eine Mindestlänge für die PIN des Benutzers erfordern möchten, aktivieren Sie diese Option, und geben Sie einen Wert an. Wenn sie aktiviert ist, lautet der Standardwert `4`.

    - **Maximale PIN-Länge konfigurieren**: Wenn Sie eine maximale Länge für die PIN des Benutzers erfordern möchten, aktivieren Sie diese Option, und geben Sie einen Wert an. Wenn sie aktiviert ist, lautet der Standardwert `127`.

    - **PIN-Ablauf (in Tagen) erforderlich**: Gibt an, nach wie vielen Tagen der Benutzer die Geräte-PIN ändern muss.

    - **Wiederverwendung vorheriger PINs verhindern**: Erlauben Sie Benutzern nicht, PINs zu verwenden, die sie zuvor bereits verwendet haben.

    - **Großbuchstaben in PIN anfordern**: Gibt an, ob Benutzer in der Windows Hello for Business-PIN Großbuchstaben verwenden müssen. Es stehen die folgenden Optionen zur Auswahl:  

      - **Zulässig**: Benutzer können Großbuchstaben in ihrer PIN verwenden, müssen dies aber nicht tun.

      - **Erforderlich**: Benutzer müssen mindestens einen Großbuchstaben in ihrer PIN verwenden.  

      - **Nicht zulässig**: Benutzer dürfen keine Großbuchstaben in ihrer PIN verwenden.  

    - **Kleinbuchstaben in PIN anfordern**: Gibt an, ob Benutzer in der Windows Hello for Business-PIN Kleinbuchstaben verwenden müssen. Es stehen die folgenden Optionen zur Auswahl:  

      - **Zulässig**: Benutzer können Kleinbuchstaben in ihrer PIN verwenden, müssen dies aber nicht tun.

      - **Erforderlich**: Benutzer müssen mindestens einen Kleinbuchstaben in ihrer PIN verwenden.  

      - **Nicht zulässig**: Benutzer dürfen keine Kleinbuchstaben in ihrer PIN verwenden.  

    - **Sonderzeichen konfigurieren**: Gibt die Verwendung von Sonderzeichen in der PIN an. Es stehen die folgenden Optionen zur Auswahl:  

        > [!NOTE]
        > Zu den Sonderzeichen zählt der folgende Satz:
        >
        > ``` characters
        > ! " # $ % & ' ( ) * + , - . / : ; < = > ? @ [ \ ] ^ _ ` { | } ~
        > ```

      - **Zulässig**: Benutzer können Sonderzeichen in ihrer PIN verwenden, müssen dies aber nicht tun.  

      - **Erforderlich**: Benutzer müssen mindestens ein Sonderzeichen in ihrer PIN verwenden.  

      - **Nicht zulässig**: Benutzer dürfen keine Sonderzeichen in ihrer PIN verwenden. Dieses Verhalten gilt auch, wenn die Einstellung **Nicht konfiguriert** ist.  

    - **Verwendung von Ziffern in PIN konfigurieren**: Gibt die Verwendung von Zahlen in der PIN an. Es stehen die folgenden Optionen zur Auswahl:

      - **Zulässig**: Benutzer können Zahlen in ihrer PIN verwenden, müssen es aber nicht.  

      - **Erforderlich**: Benutzer müssen mindestens eine Zahl in ihrer PIN angeben.  

      - **Nicht zulässig**: Benutzer dürfen keine Zahlen in ihrer PIN verwenden.

    - **Biometrische Gesten aktivieren**: Verwenden Sie eine biometrische Authentifizierung wie Gesichts- oder Fingerabdruckerkennung. Diese Modi sind eine Alternative zu einer PIN für Windows Hello for Business. Benutzer konfigurieren für den Fall, dass die biometrische Authentifizierung fehlschlägt. dennoch eine PIN.  

      Wenn diese Option auf **Ja** festgelegt ist, lässt Windows Hello for Business die biometrische Authentifizierung zu. Wenn diese Option auf **Nein** festgelegt ist, verhindert Windows Hello for Business die biometrische Authentifizierung für alle Kontotypen.  

    - **Erweitertes Antispoofing verwenden**: Konfiguriert das erweiterte Antispoofing auf Geräten, die diese Option unterstützen. Wenn diese Option auf **Ja** festgelegt ist, fordert Windows von allen Benutzern die Verwendung von Antispoofing für Gesichtsmerkmale, sofern dies unterstützt wird.  

    - **Anmeldung per Telefon verwenden**: Konfiguriert die zweistufige Authentifizierung mit einem Mobiltelefon.

1. Schließen Sie den Assistenten ab.

Der folgende Screenshot zeigt ein Beispiel für Profileinstellungen für Windows Hello for Business:  

![Der Assistent für die Windows Hello for Business-Richtlinie, der die Liste verfügbarer Einstellungen anzeigt.](../media/hello-for-business-settings.png)

## <a name="configure-permissions"></a>Berechtigungen konfigurieren

1. Melden Sie sich als Domänenadministrator oder mit gleichwertigen Anmeldeinformationen an einer sicheren, administrativen Arbeitsstation an, auf der das folgende optionale Feature installiert ist: RSAT: Active Directory Domain Services- und Lightweight Directory Services-Tools.

1. Öffnen Sie die Konsole **Active Directory-Benutzer und -Computer**.

1. Wählen Sie die Domäne aus, wechseln Sie zum Menü **Aktion** und wählen Sie **Eigenschaften** aus.

1. Wechseln Sie zur Registerkarte **Sicherheit**, und wählen Sie **Erweitert** aus.

    > [!TIP]
    > Wenn die Registerkarte **Sicherheit** nicht angezeigt wird, schließen Sie das Eigenschaftenfenster. Wechseln Sie zum Menü **Ansicht**, und wählen Sie **Erweiterte Features** aus.

1. Klicken Sie auf **Hinzufügen**.

1. Wählen Sie **Prinzipal auswählen** aus, und geben Sie `Key Admins` ein.

1. Wählen Sie aus der Liste **Gilt für** **Descendant User objects (Nachfolgerbenutzerobjekte)** aus.

1. Wählen Sie unten auf der Seite **Alle löschen** aus.

1. Wählen Sie im Bereich **Eigenschaften** **Read msDS-KeyCredentialLink (msDS-KeyCredentialLink lesen)** aus.

1. Klicken Sie auf **OK**, um die Änderungen zu speichern und alle Fenster zu schließen.

## <a name="next-steps"></a>Nächste Schritte

[Zertifikatprofile](introduction-to-certificate-profiles.md)