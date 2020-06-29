---
title: Konfigurieren von Endpoint Protection auf macOS-Geräten mit Microsoft Intune | Microsoft-Dokumentation
description: Verwenden Sie Intune zum Konfigurieren von macOS-Geräten, und verwenden Sie die integrierte Firewall, um spezifische Apps zuzulassen oder zu blockieren, um den geschützten Modus zu verwenden, um Gatekeeper zum Bestimmen des Installationspfads von Apps zu bestimmen und um die FileVault-Datenträgerverschlüsselung zu verwenden.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/19/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 506bb4672b84423204df5fce1401748ffbce0484
ms.sourcegitcommit: 3217778ebe7fd0318810696e8931e427a85da897
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/19/2020
ms.locfileid: "85107500"
---
# <a name="macos-endpoint-protection-settings-in-intune"></a>Endpoint Protection-Einstellungen in Intune unter macOS

In diesem Artikel werden die Endpoint Protection-Einstellungen beschrieben, die Sie für Ihre macOS-Geräte konfigurieren können. Sie konfigurieren diese Einstellungen mithilfe eines macOS-Gerätekonfigurationsprofils für [Endpoint Protection](endpoint-protection-configure.md) in Intune.

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen eines Endpoint Protection-Profils für macOS](endpoint-protection-configure.md)

## <a name="firewall"></a>Firewall

Verwenden Sie die Firewall, um Verbindungen pro Anwendung statt pro Port zu steuern. Wenn Sie die Einstellung „Pro Anwendung“ verwenden, können Sie die Vorteile des Schutzes durch die Firewall besser nutzen. Dadurch wird ebenfalls verhindert, dass unerwünschte Apps die Netzwerkports steuern, die für zulässige Apps geöffnet sind.

- **Firewall aktivieren**

  Aktivieren Sie die Firewall unter macOS, und konfigurieren Sie dann, wie eingehende Verbindungen in Ihrer Umgebung verarbeitet werden.

  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Ja**

- **Alle eingehenden Verbindungen sperren**

  Blockiert alle eingehenden Verbindungen außer denen, die für grundlegende Internetdienste erforderlich sind, z.B. DHCP, Bonjour und IPSec. Durch dieses Feature werden alle Freigabedienste blockiert, z.B. die Dateifreigabe und die Bildschirmfreigabe. Wenn Sie Freigabedienste verwenden, behalten Sie *Nicht konfiguriert* für diese Einstellung bei.

  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Ja**

  Wenn Sie *Alle eingehenden Verbindungen sperren* auf *Nicht konfiguriert* festlegen, können Sie konfigurieren, welche Apps eingehende Verbindungen empfangen können und welche nicht.

  **Zugelassene Apps:** Konfigurieren Sie eine Liste von Apps, die eingehende Verbindungen empfangen dürfen.

  - **Apps nach Paket-ID hinzufügen**: Geben Sie die [Paket-ID](../configuration/bundle-ids-built-in-ios-apps.md) der App ein. Eine Liste der integrierten Apple-Apps finden Sie auf [dieser Apple-Website](https://support.apple.com/HT208094).
  - **Store-App hinzufügen:** Wählen Sie eine Store-App aus, die Sie zuvor in Intune hinzugefügt haben. Weitere Informationen finden Sie unter [Hinzufügen von Apps zu Microsoft Intune](../apps/apps-add.md).

  **Blockierte Apps:** Konfigurieren Sie eine Liste von Apps, für die eingehende Verbindungen blockiert werden.

  - **Apps nach Paket-ID hinzufügen**: Geben Sie die [Paket-ID](../configuration/bundle-ids-built-in-ios-apps.md) der App ein. Eine Liste der integrierten Apple-Apps finden Sie auf [dieser Apple-Website](https://support.apple.com/HT208094).
  - **Store-App hinzufügen:** Wählen Sie eine Store-App aus, die Sie zuvor in Intune hinzugefügt haben. Weitere Informationen finden Sie unter [Hinzufügen von Apps zu Microsoft Intune](../apps/apps-add.md).

- **Geschützten Modus aktivieren**

  Hindern Sie den Computer daran, auf Suchanforderungen zu antworten, indem Sie den geschützten Modus aktivieren. Das Gerät antwortet weiterhin auf eingehende Anforderungen für autorisierte Apps. Unerwartete Anforderungen, wie z.B. ICMP (Ping), werden ignoriert.

  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Ja**

## <a name="gatekeeper"></a>Gatekeeper

- **Apps aus den folgenden Downloadquellen zulassen**

  Schränken Sie die Apps ein, die auf einem Gerät gestartet werden können, je nach Herkunft ein. Dadurch sollen Geräte vor Schadsoftware geschützt werden, außerdem werden nur Apps von vertrauenswürdigen Quellen zugelassen.

  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Mac App Store**
  - **Mac App Store und verifizierte Entwickler**
  - **Anywhere** (Beliebig)

- **Dem Benutzer das Außerkraftsetzen von Gatekeeper nicht gestatten**

  Hindert Benutzer am Außerkraftsetzen der Gatekeeper-Einstellungen und vom Installieren von Apps durch STRG+Klick. Wenn diese Einstellung aktiviert ist, kann der Benutzer eine beliebige App mithilfe von STRG+Klick installieren.

  - **Nicht konfiguriert** (*Standard*): Benutzer können Apps per STRG+Klick installieren.
  - **Ja**: Verhindert, dass Benutzer Apps per STRG+KLICK installieren können.

## <a name="filevault"></a>FileVault

Weitere Informationen zu den Einstellungen von Apple FileVault finden Sie unter [FDEFileVault](https://developer.apple.com/documentation/devicemanagement/fdefilevault) in den Ressourcen für Apple-Entwickler.

> [!IMPORTANT]
> Ab macOS 10.15 muss die MDM-Registrierung vom Benutzer genehmigt werden.

- **FileVault aktivieren**  

  Sie können die vollständige Datenträgerverschlüsselung mithilfe von XTS-AES 128 mit FileVault auf Geräten *aktivieren*, auf denen macOS 10.13 und höher ausgeführt wird.

  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Ja**

  Wenn *FileVault aktivieren* auf *Ja* festgelegt ist, können Sie die folgenden Einstellungen konfigurieren:

  - **Art des Wiederherstellungsschlüssels**

    *Persönliche Schlüssel*: Wiederherstellungsschlüssel werden für Geräte erstellt. Konfigurieren Sie die folgenden Einstellungen für den persönlichen Schlüssel.

  - **Beschreibung des Hinterlegungsstandorts für den persönlichen Wiederherstellungsschlüssel**

    Legen Sie eine kurze Nachricht an den Benutzer fest, die erklärt, wie und wo dieser den persönlichen Wiederherstellungsschlüssel abrufen kann. Dieser Text wird in die Meldung eingefügt, die dem Benutzer auf dem Anmeldebildschirm angezeigt wird, wenn dieser sein Kennwort vergessen hat und zur Eingabe des persönlichen Wiederherstellungsschlüssels aufgefordert wird.

  - **Rotation für persönlichen Wiederherstellungsschlüssel**

    Geben Sie an, wie häufig der persönliche Wiederherstellungsschlüssel für ein Gerät rotiert werden soll. Sie können die Standardeinstellung **Nicht konfiguriert** oder einen Wert von **1** bis **12** Monaten festlegen.

  - **Wiederherstellungsschlüssel ausblenden**

    Hiermit können Sie den persönlichen Schlüssel für einen Gerätebenutzer während der FileVault 2-Verschlüsselung ausblenden.

    - **Nicht konfiguriert** (*Standard*): Bei dieser Einstellung wird der persönliche Schlüssel dem Gerätebenutzer während der Verschlüsselung angezeigt.
    - **Ja:** Bei dieser Einstellung wird der persönliche Schlüssel für den Gerätebenutzer während der Verschlüsselung ausgeblendet.

    Nach der Verschlüsselung können Gerätebenutzer ihre persönlichen Wiederherstellungsschlüssel für ein verschlüsseltes macOS-Gerät über die folgenden Orte anzeigen:
    - Unternehmensportal-App für iOS/iPadOS
    - Intune-App
    - Unternehmensportal-Website
    - Android-Unternehmensportal-App

    Rufen Sie die Gerätedetails des verschlüsselten macOS-Geräts auf, und klicken Sie auf *Wiederherstellungsschlüssel abrufen*, um den Schlüssel über die App oder Website abzurufen.

  - **Aufforderung bei Abmeldung deaktivieren**

    Mit dieser Option wird verhindert, dass die Aufforderung dem Benutzer bei der Abmeldung angezeigt wird, der die Aktivierung von FileVault anfordert.  Wenn diese Option deaktiviert ist, wird die Eingabeaufforderung bei der Abmeldung deaktiviert, und der Benutzer wird stattdessen aufgefordert, wenn er sich anmeldet.

    - **Nicht konfiguriert** (*Standardeinstellung*)
    - **Ja**: Deaktiviert die Eingabeaufforderung bei der Abmeldung.

  - **Zulässige Anzahl von Umgehungen**

    Hiermit wird festgelegt, wie häufig ein Benutzer Aufforderungen zum Aktivieren von FileVault ignorieren kann, bevor FileVault für die Benutzeranmeldung als erforderlich festgelegt wird.

    - **Nicht konfiguriert**: Die Verschlüsselung auf dem Gerät ist erforderlich, bevor die nächste Anmeldung zugelassen wird.
    - **0:** Bei dieser Einstellung müssen Geräte das nächste Mal verschlüsselt werden, wenn ein Benutzer sich anmeldet.
    - **1** bis **10**: Benutzern das Ignorieren der Eingabeaufforderung ein- bis zehnmal gestatten, bevor die Verschlüsselung auf dem Gerät erforderlich ist.
    - **Kein Limit, immer auffordern**: Der Benutzer wird aufgefordert, FileVault zu aktivieren, aber die Verschlüsselung ist nicht erforderlich.

    Der Standardwert dieser Einstellung hängt von der Konfiguration der Einstellung *Aufforderung bei Abmeldung deaktivieren* ab. Wenn *Aufforderung bei Abmeldung deaktivieren* auf **Nicht konfiguriert** festgelegt ist, lautet die Standardeinstellung **Nicht konfiguriert**. Wenn *Aufforderung bei Abmeldung deaktivieren* auf **Ja** festgelegt ist, ist diese Einstellung standardmäßig auf **1** festgelegt, und der Wert **Nicht konfiguriert** steht nicht zur Auswahl.

## <a name="next-steps"></a>Nächste Schritte

[Zuweisen von Profilen](../configuration/device-profile-assign.md) und [Überwachen von Profilen](../configuration/device-profile-monitor.md)

Sie können Endpoint Protection auch auf [Geräten mit Windows 10 und höher](endpoint-protection-windows-10.md) konfigurieren.
