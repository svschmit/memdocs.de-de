---
title: 'macOS: Virenschutzrichtlinien-Einstellungen für Microsoft Defender Antivirus für Intune | Microsoft-Dokumentation'
description: Hier finden Sie eine Liste der Einstellungen im Microsoft Defender Antivirus-Profil für macOS. Dieses Profil gehört zur Virenschutzrichtlinie für Endpunktsicherheit für macOS in Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: samyada
ms.openlocfilehash: a75fe5bac4bb99b30e21ec842dcbbe3be83e9e5b
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88909447"
---
# <a name="settings-for-microsoft-defender-atp-for-mac-in-microsoft-intune"></a>Einstellungen für Microsoft Defender ATP für Mac in Microsoft Intune

Sehen Sie sich die Einstellungen für das *Antivirus*-Profil an, die Sie für Microsoft Defender ATP für Mac in Microsoft Intune konfigurieren können. Weitere Informationen zu diesen Einstellungen finden Sie in der Windows-Dokumentation unter [Microsoft Defender Advanced Threat Protection für Mac](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-atp-mac).

Erfahren Sie mehr über dich Verwendung von [Endpunktsicherheitsrichtlinien](../protect/endpoint-security-policy.md) in Intune.

**Microsoft Defender ATP**

- **Echtzeitschutz**  
  Hiermit fordern Sie an, dass Defender auf macOS-Geräten die Funktion der Echtzeitüberwachung verwenden muss. Die Echtzeitüberwachung sucht nach Schadsoftware und verhindert, dass diese auf dem Gerät installiert oder ausgeführt wird. Sie können diese Einstellung für kurze deaktivieren, bevor sie automatisch wieder aktiviert wird.

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Systemstandardwert wiederhergestellt.
  - **Aktiviert**: Die Verwendung der Echtzeitüberwachung wird erzwungen. Gerätebenutzer können diese Einstellung nicht ändern.
  - **Deaktiviert**: Die Einstellung ist deaktiviert. Gerätebenutzer können diese Einstellung nicht ändern.

- **Schutz über die Cloud**  
  Standardmäßig sendet Defender Informationen zu allen gefundenen Problemen an Microsoft. Microsoft analysiert diese Informationen, um mehr über die Probleme zu erfahren, die Sie und andere Kunden betreffen, und dann verbesserte Lösungen anzubieten. Der Schutz funktioniert am besten, wenn die Einstellung *Automatische Beispielübermittlung* aktiviert ist.

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Systemstandardwert wiederhergestellt.
  - **Aktiviert**: Der von der Cloud bereitgestellte Schutz ist aktiviert. Gerätebenutzer können diese Einstellung nicht ändern.
  - **Deaktiviert**: Die Einstellung ist deaktiviert. Gerätebenutzer können diese Einstellung nicht ändern.

- **Automatische Beispielübermittlung**  
  Mit dieser Einstellung werden Beispieldateien an Microsoft gesendet, um Gerätebenutzer und Ihre Organisation vor potenziellen Bedrohungen zu schützen.

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Systemstandardwert wiederhergestellt.
  - **Aktiviert**: Der von der Cloud bereitgestellte Schutz ist aktiviert.  Gerätebenutzer können diese Einstellung nicht ändern.
  - **Deaktiviert**: Die Einstellung ist deaktiviert. Gerätebenutzer können diese Einstellung nicht ändern.

- **Diagnosedatensammlung**

  Konfigurieren Sie die Freigabe von Diagnose- und Nutzungsdaten für Microsoft.

  - **Nicht konfiguriert** (*Standardeinstellung*): Die Einstellung wird auf den Systemstandardwert wiederhergestellt.
  - **Erforderlich**
  - **Optional**

- **Von der Überprüfung ausgeschlossene Ordner**  
  Wählen Sie **Hinzufügen** aus, und geben Sie dann die Ordner an, die bei einer Überprüfung ignoriert werden sollen.

- **Von der Überprüfung ausgeschlossene Dateien**  
  Wählen Sie **Hinzufügen** aus, und geben Sie dann die Dateien an, die bei einer Überprüfung ignoriert werden sollen.

- **Von der Überprüfung ausgeschlossene Dateitypen**  
  Wählen Sie **Hinzufügen** aus, und geben Sie dann die Dateierweiterungen an, die bei einer Überprüfung ignoriert werden sollen.

- **Von der Überprüfung ausgeschlossene Prozesse**  
  Wählen Sie **Hinzufügen** aus, und geben Sie dann die Prozesse an, die bei einer Überprüfung ignoriert werden sollen.