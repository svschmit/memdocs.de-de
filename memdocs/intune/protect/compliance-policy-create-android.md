---
title: Konformitätseinstellungen für Android-Geräte in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Dieser Artikel enthält eine Liste aller Einstellungen, die Sie verwenden können, um Konformität für Ihre Android-Geräte in Microsoft Intune festzulegen. Sie können Kennwortregeln festlegen, eine minimale oder maximale Betriebssystemversion auswählen, bestimmte Anwendungen einschränken, die Wiederverwendung von Kennwörtern verhindern und vieles mehr.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/01/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: e1258fe4-0b5c-4485-8bd1-152090df6345
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3f8cb75907befaa747ebae1718815d9722ff7085
ms.sourcegitcommit: 56bb5419c41c2e150ffed0564350123135ea4592
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/02/2020
ms.locfileid: "82729231"
---
# <a name="android-settings-to-mark-devices-as-compliant-or-not-compliant-using-intune"></a>Android-Einstellungen, um Geräte mit Intune als konform oder nicht konform zu kennzeichnen

In diesem Artikel werden die verschiedenen Konformitätseinstellungen aufgeführt und beschrieben, die Sie in Intune für Android-Geräte festlegen können. Im Rahmen Ihrer MDM-Lösung (Mobile Device Management, Verwaltung mobiler Geräte) verwenden Sie diese Einstellungen, um Geräte des Typs „Rooted“ (mit Jailbreak) als nicht konform zu markieren, eine zulässige Bedrohungsstufe festzulegen, Google Play Protect zu aktivieren und vieles mehr.

Diese Funktion gilt für:

- Android-Geräteadministrator

Als Intune-Administrator verwenden Sie diese Konformitätseinstellungen, um die Ressourcen Ihrer Organisation zu schützen. Weitere Informationen zu Konformitätsrichtlinien und ihren Aufgaben finden Sie unter [Erste Schritte bei der Gerätekonformität](device-compliance-get-started.md).

## <a name="before-you-begin"></a>Vorbereitung

[Erstellen einer Konformitätsrichtlinie](create-compliance-policy.md#create-the-policy) Wählen Sie für **Plattform** die Option **Android-Geräteadministrator** aus.

## <a name="microsoft-defender-atp"></a>Microsoft Defender ATP

- **Anfordern, dass das Gerät höchstens das angegebene Computerrisiko aufweist**  

  Wählen Sie das maximal zulässige Computerrisiko für Geräte aus, die von Microsoft Defender ATP bewertet wurden. Geräte, die diesen Wert überschreiten, werden als nicht konform gekennzeichnet.
  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Clear** (Deaktiviert)
  - **Niedrig**
  - **Mittel**
  - **Hoch**

## <a name="device-health"></a>Geräteintegrität

- **Durch Geräteadministrator verwaltete Geräte**  
  Die Funktionen des *Geräteadministrators* werden durch Android Enterprise ersetzt.

  - **Nicht konfiguriert** (*Standardeinstellung*)
  - **Blockieren:** Das Blockieren des Geräteadministrators bringt Benutzer dazu, die Android Enterprise-Arbeitsprofilverwaltung zu verwenden, um den Zugriff zurückzuerhalten.

- **Geräte mit entfernten Nutzungsbeschränkungen**  
  Hiermit wird verhindert, dass Geräte mit entfernten Nutzungsbeschränkungen Unternehmenszugriff erhalten. (Diese Konformitätsprüfung wird für Android 4.0 und höher unterstützt.)

  - **Nicht konfiguriert** (*Standardeinstellung*): Diese Einstellung wird nicht für die Konformitätsprüfung ausgewertet.
  - **Blockieren**: Geräte mit Jailbreak oder entfernten Nutzungsbeschränkungen werden als nicht konform gekennzeichnet.

- **Anfordern, dass das Gerät höchstens der angegebenen Gerätebedrohungsstufe entspricht**  
  Verwenden Sie diese Einstellung, um die Risikobewertung eines verbundenen Mobile Threat Defense-Diensts als Bedingung für die Konformität zu nehmen.

  - **Nicht konfiguriert** (*Standardeinstellung*): Diese Einstellung wird nicht für die Konformitätsprüfung ausgewertet.
  - **Gesichert**: Diese Option ist die sicherste, da auf dem Gerät keine Bedrohungen vorhanden sein können. Wenn auf dem Gerät Bedrohungen jeglicher Stufen erkannt werden, wird es als nicht konform bewertet.
  - **Niedrig**: Das Gerät wird als konform bewertet, wenn nur Bedrohungen auf niedrigen Stufen vorliegen. Durch Bedrohungen höherer Stufen wird das Gerät in einen nicht kompatiblen Status versetzt.
  - **Mittel**: Das Gerät wird als kompatibel bewertet, wenn die auf dem Gerät vorhandenen Bedrohungen niedriger oder mittlerer Stufe sind. Wenn auf dem Gerät Bedrohungen hoher Stufen erkannt werden, wird es als nicht konform bewertet.
  - **Hoch**: Dies ist die am wenigsten sichere Option, die alle Bedrohungsebenen zulässt. Es ist möglicherweise hilfreich, diese Lösung nur zu Berichtszwecken zu verwenden.

### <a name="google-play-protect"></a>Google Play Protect

- **Google Play Services ist konfiguriert**  
  Google Play Services ermöglicht Sicherheitsupdates und stellt eine grundlegende Abhängigkeit für viele Sicherheitsfunktionen auf zertifizierten Google-Geräten dar.

  - **Nicht konfiguriert** (*Standardeinstellung*): Diese Einstellung wird nicht für die Konformitätsprüfung ausgewertet.  
  - **Erforderlich**: Erzwingt, dass die Google Play Services-App installiert und aktiviert ist.  

- **Aktueller Sicherheitsanbieter**

  - **Nicht konfiguriert** (*Standardeinstellung*): Diese Einstellung wird nicht für die Konformitätsprüfung ausgewertet.
  - **Erforderlich**: Erzwingt, dass ein aktueller Sicherheitsanbieter ein Gerät vor bekannten Sicherheitslücken schützen kann.

- **Bedrohungsüberprüfung für Apps**

  - **Nicht konfiguriert** (*Standardeinstellung*): Diese Einstellung wird nicht für die Konformitätsprüfung ausgewertet.
  - **Erforderlich**: Erzwingt, dass die Android-Funktion **Apps überprüfen** aktiviert wird.

  > [!NOTE]
  > Auf der älteren Android-Plattform ist diese Funktion eine Konformitätseinstellung. Intune kann nur prüfen, ob diese Einstellung auf Geräteebene aktiviert ist.

- **SafetyNet-Gerätenachweis**  
  Legen Sie die Integritätsstufe des [SafetyNet-Nachweises](https://developer.android.com/training/safetynet/attestation.html) fest, die eingehalten werden muss. Folgende Optionen sind verfügbar:

  - **Nicht konfiguriert** (*Standardeinstellung*): Diese Einstellung wird nicht für die Konformitätsprüfung ausgewertet.
  - **Grundlegende Integrität prüfen**
  - **Grundlegende Integrität und zertifizierte Geräte prüfen**

> [!NOTE]
> Informationen zum Konfigurieren der Google Play Protect-Einstellungen mithilfe von App-Schutzrichtlinien finden Sie unter [Intune App-Schutzrichtlinieneinstellungen](../apps/app-protection-policy-settings-android.md#conditional-launch) für Android.

## <a name="device-properties"></a>Geräteeigenschaften

### <a name="operating-system-version"></a>Version des Betriebssystems

- **Minimales Release des Betriebssystems**  
  Wenn ein Gerät die Anforderung an die Mindestversion des Betriebssystems nicht erfüllt, wird es als nicht konform gemeldet. Ein Link mit Informationen zum Durchführen von Upgrades wird gezeigt. Der Endbenutzer kann ein Upgrade seines Geräts durchführen, und anschließend auf die Unternehmensressourcen zugreifen.

  *Standardmäßig ist keine Version konfiguriert*.

- **Maximales Release des Betriebssystems**  
  Wenn auf einem Gerät eine neuere Betriebssystemversion verwendet wird, als in der Regel angegeben, wird der Zugriff auf Unternehmensressourcen gesperrt. Der Benutzer wird dazu aufgefordert, sich an den zuständigen IT-Administrator zu wenden. Mit diesem Gerät kann solange nicht auf Unternehmensressourcen zugegriffen werden, bis die Regel geändert und die betreffende Betriebssystemversion zugelassen wird.

  *Standardmäßig ist keine Version konfiguriert*.

## <a name="system-security"></a>Systemsicherheit

### <a name="password"></a>Kennwort

- **Anfordern eines Kennworts zum Entsperren mobiler Geräte**  
  *Unter Android 4.0 und höher oder Knox 4.0 und höher unterstützt.*

  Mit dieser Einstellung wird festgelegt, ob Benutzer ein Kennwort eingeben müssen, damit auf die Daten auf ihren mobilen Geräten zugegriffen werden kann. Empfohlener Wert: Erforderlich  

  - **Nicht konfiguriert** (*Standardeinstellung*): Diese Einstellung wird nicht für die Konformitätsprüfung ausgewertet.
  - **Erforderlich**: Benutzer müssen ein Kennwort eingeben, bevor sie auf ihr Gerät zugreifen können.

- **Erforderlicher Kennworttyp**  
  *Unter Android 4.0 und höher oder Knox 4.0 und höher unterstützt.*

  Wählen Sie aus, ob ein Kennwort nur aus numerischen Zeichen oder aus einer Kombination aus Ziffern und anderen Zeichen bestehen soll.

  - **Gerätestandard**: Zur Auswertung der Kennwortkonformität sollten Sie in jedem Fall eine andere Einstellung für die Kennwortstärke als **Gerätestandard** angeben.
  - **Biometrie auf niedriger Sicherheitsstufe**
  - **Mindestens numerisch**
  - **Numerisch, komplex**: Sich wiederholende oder fortlaufende Ziffern wie `1111` oder `1234` sind nicht zulässig.
  - **Mindestens alphabetisch**
  - **Mindestens alphanumerisch**
  - **Mindestens alphanumerisch mit Symbolen**

  Basierend auf der Konfiguration dieser Einstellung stehen eine oder mehrere der folgenden Optionen zur Verfügung:

  - **Minimale Kennwortlänge**  
    *Unter Android 4.0 und höher oder Knox 4.0 und höher unterstützt.*

    Geben Sie die Mindestanzahl von Ziffern oder Zeichen an, die das Benutzerkennwort enthalten muss.

  - **Maximaler Zeitraum der Inaktivität (in Minuten) bis zur Anforderung eines Kennworts**  
    *Unter Android 4.0 und höher oder Knox 4.0 und höher unterstützt.*

    Geben Sie die Leerlaufzeit ein, nach der ein Benutzer sein Kennwort erneut eingeben muss. Wenn Sie **Nicht konfiguriert** (Standardeinstellung) auswählen, wird diese Einstellung nicht für die Konformitätsprüfung ausgewertet.

  - **Anzahl von Tagen bis zum Kennwortablauf**  
  *Unter Android 4.0 und höher oder Knox 4.0 und höher unterstützt.*

  Legen Sie die Anzahl von Tagen fest, bis das Kennwort abläuft und der Benutzer ein neues erstellen muss.

  - **Anzahl vorheriger Kennwörter, deren Wiederverwendung verhindert wird**  
    Geben Sie die Anzahl von vorherigen Kennwörtern ein, die nicht wiederverwendet werden dürfen. Verwenden Sie diese Einstellung, um zu verhindern, dass der Benutzer zuvor verwendete Kennwörter erstellt. (Diese Einstellung wird für Android 4.0 und höher oder KNOX 4.0 und höher unterstützt.)

### <a name="encryption"></a>Verschlüsselung

- **Verschlüsselung des Datenspeichers auf dem Gerät**  
  *Unter Android 4.0 und höher oder Knox 4.0 und höher unterstützt.*

  - **Nicht konfiguriert** (*Standardeinstellung*): Diese Einstellung wird nicht für die Konformitätsprüfung ausgewertet.
  - **Anfordern:** Bei dieser Einstellung wird der Datenspeicher auf Ihren Geräten verschlüsselt. Wenn Sie die Einstellung **Kennwort zum Entsperren mobiler Geräte anfordern** auswählen, werden Geräte verschlüsselt.

### <a name="device-security"></a>Gerätesicherheit

- **Apps von unbekannten Quellen blockieren**  
  *Diese Einstellung wird unter Android 4.0 bis Android 7.x unterstützt, aber nicht unter Android 8.0 und höher.*

  - **Nicht konfiguriert** (*Standardeinstellung*): Diese Einstellung wird nicht für die Konformitätsprüfung ausgewertet.
  - **Blockieren:** Mit dieser Einstellung werden Geräte blockiert, bei denen die Einstellung **Sicherheit > Unbekannte Quellen** aktiviert ist (*wird von Android 4.0 bis Android 7.x, aber nicht von Android 8.0 und höher unterstützt*).

  Für das Sideloading von Apps müssen unbekannte Quellen zugelassen werden. Wenn Sie kein Sideloading von Android-Apps durchführen, legen Sie für dieses Feature **Blockieren** fest, um diese Konformitätsrichtlinie zu aktivieren.

  > [!IMPORTANT]
  > Das Sideloading von Anwendungen erfordert, dass die Einstellung **Apps von unbekannten Quellen blockieren** aktiviert ist. Erzwingen Sie diese Konformitätsrichtlinie nur, wenn Sie kein Sideloading von Android-Apps auf Geräten durchführen.

- **Laufzeitintegrität der Unternehmensportal-App**
  - **Nicht konfiguriert** (*Standardeinstellung*): Diese Einstellung wird nicht für die Konformitätsprüfung ausgewertet.
  - **Erforderlich**: Wählen Sie diese Einstellung aus, um sicherzustellen, dass die Unternehmensportal-App alle folgenden *Anforderungen* erfüllt:

    - Die Standardlaufzeitumgebung ist installiert.
    - Die App ist ordnungsgemäß signiert.
    - Die App befindet sich nicht im Debug-Modus.
    - Die App wurde aus einer bekannten Quelle installiert.

- **USB-Debugging auf Gerät blockieren**  
  *(Unter Android 4.2 oder höher unterstützt)*

  - **Nicht konfiguriert** (*Standardeinstellung*): Diese Einstellung wird nicht für die Konformitätsprüfung ausgewertet.
  - **Blockieren**: Mit dieser Einstellung wird verhindert, dass Geräte das USB-Debuggingfeature verwenden.

- **Mindestens erforderliche Sicherheitspatchebene**  
  *(Unter Android 6.0 oder höher unterstützt)*

  Wählen Sie die älteste Sicherheitspatchebene, die ein Gerät haben darf. Geräte, die nicht mindestens diese Patchebene aufweisen, sind nicht konform. Das Datum muss im Format „`YYYY-MM-DD`“ eingegeben werden.

  *Standardmäßig ist kein Datum konfiguriert*.

- **Eingeschränkte Apps**  
  Geben Sie den **App-Namen** und die **App Bundle-ID** für Apps ein, die eingeschränkt werden sollen, und wählen Sie **Hinzufügen** aus. Geräte mit mindestens einer installierten, eingeschränkten App werden als nicht konform gekennzeichnet.

## <a name="next-steps"></a>Nächste Schritte

- [Hinzufügen von Aktionen für nicht kompatible Geräte](actions-for-noncompliance.md) und [Verwenden von Bereichsmarkierungen zum Filtern von Richtlinien](../fundamentals/scope-tags.md).
- [Überwachen Ihrer Konformitätsrichtlinien](compliance-policy-monitor.md).
- Siehe [Konformitätsrichtlinieneinstellungen für Android Enterprise](compliance-policy-create-android-for-work.md)-Geräte.
