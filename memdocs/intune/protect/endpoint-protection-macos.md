---
title: Hinzufügen von Endpoint Protection unter macOS in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Verwenden Sie auf macOS-Geräten den Gatekeeper, um zu bestimmen, wo Apps, einschließlich der Mac App Store, installiert werden können. Aktivieren oder Konfigurieren Sie ebenfalls eine Firewall, um bestimmte Apps zuzulassen, zu blockieren, den geschützten Modus zu verwenden oder bestimmte Arten von eingehenden Verbindungen mithilfe von Microsoft Intune zu blockieren.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5e857cdd7028851f14f607739ba7e37c744fa2f1
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "80359466"
---
# <a name="macos-endpoint-protection-settings-in-intune"></a>Endpoint Protection-Einstellungen in Intune unter macOS  

In diesem Artikel werden die Endpoint Protection-Einstellungen beschrieben, die Sie für Ihre macOS-Geräte konfigurieren können. Sie konfigurieren diese Einstellungen mithilfe eines macOS-Gerätekonfigurationsprofils für [Endpoint Protection](endpoint-protection-configure.md) in Intune.  

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen eines Endpoint Protection-Profils für macOS](endpoint-protection-configure.md)

## <a name="gatekeeper"></a>Gatekeeper  

- **Apps aus den folgenden Downloadquellen zulassen**  
  Schränken Sie die Apps ein, die auf einem Gerät gestartet werden können, je nach Herkunft ein. Dadurch sollen Geräte vor Schadsoftware geschützt werden, außerdem werden nur Apps von vertrauenswürdigen Quellen zugelassen.  

  - **Nicht konfiguriert**  
  - **Mac App Store**  
  - **Mac App Store und verifizierte Entwickler**  
  - **Anywhere** (Beliebig)  

  **Standardeinstellung:** Nicht konfiguriert  

- **Benutzer kann Gatekeeper außer Kraft setzen**  
  Hindert Benutzer am Außerkraftsetzen der Gatekeeper-Einstellungen und vom Installieren von Apps durch STRG+Klick. Wenn diese Einstellung aktiviert ist, kann der Benutzer eine beliebige App mithilfe von STRG+Klick installieren.  
 
  - **Nicht konfiguriert**: Benutzer können Apps per STRG+Klick installieren.  
  - **Blockieren**: Verhindert, dass Benutzer Apps per STRG+Klick installieren können  

  **Standardeinstellung:** Nicht konfiguriert  

## <a name="firewall"></a>Firewall  

Verwenden Sie die Firewall, um Verbindungen pro Anwendung statt pro Port zu steuern. Wenn Sie die Einstellung „Pro Anwendung“ verwenden, können Sie die Vorteile des Schutzes durch die Firewall besser nutzen. Dadurch wird ebenfalls verhindert, dass unerwünschte Apps die Netzwerkports steuern, die für zulässige Apps geöffnet sind.  

**Allgemein**
- **Firewall**  
  Aktivieren Sie die Firewall, um zu konfigurieren, wie eingehende Verbindung in Ihrer Umgebung behandelt werden.  
  - **Nicht konfiguriert**  
  - **Aktivieren**  

  **Standardeinstellung:** Nicht konfiguriert  

- **Eingehende Verbindungen**  
  Blockiert alle eingehenden Verbindungen außer denen, die für grundlegende Internetdienste erforderlich sind, z.B. DHCP, Bonjour und IPSec. Durch dieses Feature werden alle Freigabedienste blockiert, z.B. die Dateifreigabe und die Bildschirmfreigabe. Wenn Sie Freigabedienste verwenden, behalten Sie *Nicht konfiguriert* für diese Einstellung bei.  
  - **Nicht konfiguriert**  
  - **Blockieren**  

  **Standardeinstellung:** Nicht konfiguriert  

**Zulassen oder Blockieren eingehender Verbindungen für bestimmte Apps.**  

  - **Zugelassene Apps**  
    Wählen Sie die Apps aus, die explizit für eingehende Verbindungen zugelassen sind.  

  - **Blockierte Apps**  
    Wählen Sie die Apps aus, für die eingehende Verbindungen blockiert werden sollen.  

  - **Geschützter Modus**  
    Hindern Sie den Computer daran, auf Suchanforderungen zu antworten, indem Sie den geschützten Modus aktivieren. Das Gerät antwortet weiterhin auf eingehende Anforderungen für autorisierte Apps. Unerwartete Anforderungen, wie z.B. ICMP (Ping), werden ignoriert.  
    - **Nicht konfiguriert**  
    - **Aktivieren**  

    **Standardeinstellung:** Nicht konfiguriert  

## <a name="filevault"></a>FileVault  
Weitere Informationen zu den Einstellungen von Apple FileVault finden Sie unter [FDEFileVault](https://developer.apple.com/documentation/devicemanagement/fdefilevault) in den Ressourcen für Apple-Entwickler. 

> [!IMPORTANT]  
> Ab macOS 10.15 muss die MDM-Registrierung vom Benutzer genehmigt werden. 

- **FileVault**  
  Sie können die vollständige Datenträgerverschlüsselung mithilfe von XTS-AES 128 mit FileVault auf Geräten *aktivieren*, auf denen macOS 10.13 und höher ausgeführt wird.  
  - **Nicht konfiguriert**  
  - **Aktivieren**  

  **Standardeinstellung:** Nicht konfiguriert  

  - **Art des Wiederherstellungsschlüssels**  
    *Persönliche Schlüssel*: Wiederherstellungsschlüssel werden für Geräte erstellt. Konfigurieren Sie die folgenden Einstellungen für den persönlichen Schlüssel.  

    - **Speicherort des persönlichen Wiederherstellungsschlüssels**: Legen Sie eine kurze Nachricht an den Benutzer fest, die erklärt, wie und wo dieser den persönlichen Wiederherstellungsschlüssel abrufen kann. Dieser Text wird in die Meldung eingefügt, die dem Benutzer auf dem Anmeldebildschirm angezeigt wird, wenn dieser sein Kennwort vergessen hat und zur Eingabe des persönlichen Wiederherstellungsschlüssels aufgefordert wird.  

    - **Rotation für persönlichen Wiederherstellungsschlüssel**: Geben Sie an, wie häufig der persönliche Wiederherstellungsschlüssel für ein Gerät rotiert werden soll. Sie können die Standardeinstellung **Nicht konfiguriert** oder einen Wert von **1** bis **12** Monaten festlegen.  

  - **Aufforderung bei Abmeldung deaktivieren**  
    Mit dieser Option wird verhindert, dass die Aufforderung dem Benutzer bei der Abmeldung angezeigt wird, der die Aktivierung von FileVault anfordert.  Wenn diese Option deaktiviert ist, wird die Eingabeaufforderung bei der Abmeldung deaktiviert, und der Benutzer wird stattdessen aufgefordert, wenn er sich anmeldet.  
    - **Nicht konfiguriert**  
    - **Deaktivieren**: Deaktiviert die Eingabeaufforderung bei der Abmeldung

    **Standardeinstellung:** Nicht konfiguriert  

  - **Zulässige Anzahl von Umgehungen**  
  Hiermit wird festgelegt, wie häufig ein Benutzer Aufforderungen zum Aktivieren von FileVault ignorieren kann, bevor FileVault für die Benutzeranmeldung als erforderlich festgelegt wird. 

    - **Nicht konfiguriert**: Die Verschlüsselung auf dem Gerät ist erforderlich, bevor die nächste Anmeldung zugelassen wird.  
    - **1** bis **10**: Benutzern das Ignorieren der Eingabeaufforderung ein- bis zehnmal gestatten, bevor die Verschlüsselung auf dem Gerät erforderlich ist.  
    - **Kein Limit, immer auffordern**: Der Benutzer wird aufgefordert, FileVault zu aktivieren, aber die Verschlüsselung ist nicht erforderlich.  
 
    **Standardeinstellung:** *Variiert*: Wenn die Einstellung *Aufforderung bei Abmeldung deaktivieren* auf **Nicht konfiguriert** festgelegt ist, wird diese Einstellung standardmäßig auf **Nicht konfiguriert** festgelegt. Wenn *Aufforderung bei Abmeldung deaktivieren* auf **Deaktivieren** festgelegt ist, ist diese Einstellung standardmäßig auf **1** festgelegt, und der Wert **Nicht konfiguriert** steht nicht zur Auswahl.

Weitere Informationen zu FileVault mit Intune finden Sie unter [FileVault-Wiederherstellungsschlüssel](encryption-monitor.md#filevault-recovery-keys).

## <a name="next-steps"></a>Nächste Schritte

[Zuweisen von Profilen](../configuration/device-profile-assign.md) und [Überwachen von Profilen](../configuration/device-profile-monitor.md)

Sie können Endpoint Protection auch auf [Geräten mit Windows 10 und höher](endpoint-protection-windows-10.md) konfigurieren.
