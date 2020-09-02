---
title: Windows Hello for Business-Einstellungen in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Hier finden Sie eine Liste aller PIN-, biometrischen und Antispoofing-Einstellungen in einem Identity Protection-Profil zum Verwenden und Konfigurieren von Windows Hello for Business-Geräten auf Windows 10 in Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/20/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: shpate
ms.openlocfilehash: ce4795dd060d29b62887fbf5496b2f2706ba954f
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909107"
---
# <a name="windows-10-device-settings-to-enable-windows-hello-for-business-in-intune"></a>Einstellungen für Windows 10-Geräte zum Aktivieren von Windows Hello for Business in Intune

In diesem Artikel werden die Windows Hello for Business-Einstellungen aufgeführt und beschrieben, die Sie für Windows 10-Geräte in Intune steuern können. Als Intune-Administrator können Sie diese Einstellungen konfigurieren und Windows 10-Geräten als Teil Ihrer Lösung für die mobile Geräteverwaltung (MDM) zuweisen. 

Weitere Informationen zu diesen Einstellungen finden Sie in der Windows Hello-Dokumentation unter [Configure Windows Hello for Business Policy settings](/windows/security/identity-protection/hello-for-business/hello-cert-trust-policy-settings) (Konfigurieren der Richtlinieneinstellungen für Windows Hello for Business).


Weitere Informationen zu Windows Hello for Business-Profilen in Intune finden Sie unter [Konfigurieren von Identity Protection-Einstellungen in Microsoft Intune](identity-protection-configure.md).

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen Sie ein Konfigurationsprofil](identity-protection-configure.md#create-the-device-profile).

## <a name="windows-hello-for-business"></a>Windows Hello for Business
- **Konfigurieren Sie Windows Hello for Business**:
  - **Nicht konfiguriert** – Wählen Sie diese Einstellung aus, wenn Sie Windows Hello for Business-Einstellungen nicht mit Intune steuern möchten. Vorhandene Windows Hello for Business-Einstellungen auf Geräten mit Windows 10 werden nicht geändert. Alle anderen Einstellungen in dem Bereich sind nicht verfügbar.

  - **Deaktiviert** – Wenn Sie Windows Hello for Business nicht verwenden möchten, wählen Sie diese Einstellung aus. In diesem Fall ist keine der anderen Einstellungen auf dem Bildschirm verfügbar.
  - **Aktiviert** – Wählen Sie diese Einstellung aus, wenn Sie Windows Hello for Business-Einstellungen konfigurieren möchten.  
  
  **Standardeinstellung:** Nicht konfiguriert

  Wenn der Wert *Aktiviert* festgelegt wird, sind die folgenden Einstellungen verfügbar:

  - **PIN-Mindestlänge**  
    Geben Sie die minimale PIN-Länge für Geräte an, um eine sichere Anmeldung zu unterstützen. Der Standardwert für Windows-Geräte sind sechs Zeichen. Für diese Einstellung können jedoch 4–127 Zeichen erzwungen werden. 

    **Standardeinstellung:** *Nicht konfiguriert*

  - **Höchstlänge für PIN**  
  Geben Sie die maximale PIN-Länge für Geräte an, um eine sichere Anmeldung zu unterstützen. Der Standardwert für Windows-Geräte sind sechs Zeichen. Für diese Einstellung können jedoch 4–127 Zeichen erzwungen werden.  

    **Standardeinstellung:** *Nicht konfiguriert*  

  - **Kleinbuchstaben in PIN**  
    Sie können eine stärkere PIN erzwingen, indem Sie von Endbenutzern fordern, Kleinbuchstaben einzubeziehen. Folgende Optionen sind verfügbar:

    - **Nicht zulässig** : Hiermit wird die Verwendung von Kleinbuchstaben in der PIN von Benutzern blockiert. Dieses Verhalten tritt auch auf, wenn die Einstellung nicht konfiguriert ist.
    - **Zulässig**: Benutzer können Kleinbuchstaben in der PIN verwenden, aber es ist nicht erforderlich.
    - **Erforderlich**: Benutzer müssen in ihre PIN mindestens einen Kleinbuchstaben einbeziehen. Beispielsweise ist es üblich, die Verwendung mindestens eines Großbuchstabens und eines Sonderzeichens vorzuschreiben.

  - **Großbuchstaben in PIN**  
    Sie können eine stärkere PIN erzwingen, indem Sie von Endbenutzern fordern, Großbuchstaben einzubeziehen. Folgende Optionen sind verfügbar:

    - **Nicht zulässig**: Hiermit wird die Verwendung von Großbuchstaben in der PIN von Benutzern blockiert. Dieses Verhalten tritt auch auf, wenn die Einstellung nicht konfiguriert ist.
    - **Zulässig**: Benutzer können Großbuchstaben in der PIN verwenden, aber es ist nicht erforderlich.
    - **Erforderlich**: Benutzer müssen in ihre PIN mindestens einen Großbuchstaben einbeziehen. Beispielsweise ist es üblich, die Verwendung mindestens eines Großbuchstabens und eines Sonderzeichens vorzuschreiben.

  - **Sonderzeichen in PIN**  
    Sie können eine stärkere PIN erzwingen, indem Sie von Endbenutzern fordern, Sonderzeichen einzubeziehen. Gilt für diese Sonderzeichen: `! " # $ % &amp; ' ( ) &#42; + , - . / : ; &lt; = &gt; ? @ [ \ ] ^ _ &#96; { &#124; } ~`  

    Folgende Optionen sind verfügbar:
    - **Nicht zulässig** : Hiermit wird die Verwendung von Sonderzeichen in der PIN von Benutzern blockiert. Dieses Verhalten tritt auch auf, wenn die Einstellung nicht konfiguriert ist.
    - **Zulässig**: Benutzer können Großbuchstaben in der PIN verwenden, aber es ist nicht erforderlich.
    - **Erforderlich**: Benutzer müssen in ihre PIN mindestens einen Großbuchstaben einbeziehen. Beispielsweise ist es üblich, die Verwendung mindestens eines Großbuchstabens und eines Sonderzeichens vorzuschreiben.

    **Standardeinstellung:** Nicht zulässig

  - **PIN-Ablauf (Tage)**  
    Es wird empfohlen, ein Ablaufdatum für eine PIN anzugeben, nach dem sie vom Benutzer geändert werden muss. Der Standardwert für Windows-Geräte sind 41 Tage.

    **Standardeinstellung:** Nicht konfiguriert

  - **PIN-Verlauf speichern**  
    Schränkt die Wiederverwendung zuvor verwendeter PINs ein. Dies ist der Standardwert, um die Wiederverwendung der letzten fünf PINs zu verhindern.  

    **Standardeinstellung:** Nicht konfiguriert  

  - **PIN-Wiederherstellung aktivieren**   
    Ermöglicht dem Benutzer, den PIN-Wiederherstellungsdienst von Windows Hello for Business zu verwenden. 
    
    - **Aktiviert:** Das Geheimnis für die PIN-Wiederherstellung ist auf dem Gerät gespeichert, und der Benutzer kann seine PIN bei Bedarf ändern.  
    - **Deaktiviert:** Es wird kein Geheimnis für die Wiederherstellung erstellt oder gespeichert.

    **Standardeinstellung:** Nicht konfiguriert

  - **Trusted Platform Module (TPM) verwenden**   
    Ein TPM-Chip bietet eine zusätzliche Sicherheitsebene für Daten.  

    - **Aktiviert**: Nur Geräte mit verfügbarem TPM können Windows Hello for Business bereitstellen.
    - **Nicht konfiguriert**: Geräte versuchen zunächst, ein TPM zu verwenden. Wenn diese Option nicht verfügbar ist, können sie die Softwareverschlüsselung verwenden.
    
    **Standardeinstellung:** Nicht konfiguriert

  - **Biometrische Authentifizierung zulassen**  
     Aktiviert die biometrische Authentifizierung, z. B. die Gesichtserkennung oder Fingerabdrücke, als Alternative zu einer PIN für Windows Hello for Business. Benutzer müssen für den Fall dennoch eine PIN konfigurieren, dass die biometrische Authentifizierung fehlschlägt. Es stehen die folgenden Optionen zur Auswahl:

    - **Aktivieren**: Windows Hello for Business ermöglicht biometrische Authentifizierung.
    - **Nicht konfiguriert**: Windows Hello for Business verhindert die biometrische Authentifizierung (für alle Kontotypen).

    **Standardeinstellung:** Nicht konfiguriert

  - **Erweitertes Antispoofing verwenden, falls verfügbar**  
    Konfiguriert, ob die Antispoofingfeatures von Windows Hello auf Geräten verwendet werden, die diese unterstützen (z. B. Erkennung eines Fotos von einem Gesicht anstelle eines echten Gesichts).  
    - **Aktivieren**: Windows verlangt, dass alle Benutzer Antispoofing für Gesichtsmerkmale einsetzen, sofern dies unterstützt wird.
    - **Nicht konfiguriert**: Antispoofingkonfigurationen auf dem Gerät werden von Windows berücksichtigt.

    **Standardeinstellung:** Nicht konfiguriert

  - **Zertifikat für lokale Ressourcen**  

    - **Aktivieren**: Ermöglicht es Windows Hello for Business, Zertifikate zur Authentifizierung bei lokalen Ressourcen zu verwenden.
    - **Nicht konfiguriert**: Verhindert, dass Windows Hello for Business Zertifikate zur Authentifizierung bei lokalen Ressourcen verwendet. Stattdessen verwenden Geräte das Standardverhalten der *lokalen schlüsselbasierten Authentifizierung*. Weitere Informationen finden Sie unter [User certificate for on-premises authentication (Benutzerzertifikat für lokale Authentifizierung)](/windows/security/identity-protection/hello-for-business/hello-cert-trust-policy-settings#use-certificate-for-on-premises-authentication) in der Windows Hello-Dokumentation.  

  **Standardeinstellung:** Nicht konfiguriert

- **Verwenden von Sicherheitsschlüsseln zur Anmeldung**  
  Diese Einstellung ist für Geräte verfügbar, auf denen Windows 10, Version 1903 oder höher ausgeführt wird. Verwenden Sie sie, um die Unterstützung von Windows Hello-Sicherheitsschlüsseln für die Anmeldung zu verwalten.  

  - **Aktiviert:** Benutzer können einen Windows Hello-Sicherheitsschlüssel als Anmeldeinformation für PCs verwenden, die dieser Richtlinie unterliegen. 
  - **Deaktiviert:** Sicherheitsschlüssel sind deaktiviert, und Benutzer können sich nicht mit ihnen auf PCs anmelden.   

  **Standardeinstellung:** Nicht konfiguriert

## <a name="next-steps"></a>Nächste Schritte

[Zuweisen von Profilen](../configuration/device-profile-assign.md) und [Überwachen von Profilen](../configuration/device-profile-monitor.md)