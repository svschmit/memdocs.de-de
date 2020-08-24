---
title: Gerätekonformitätsrichtlinien in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Beginnen Sie mit der Verwendung von Konformitätsrichtlinien, einschließlich den Einstellungen für Konformitätsrichtlinien und den Gerätekonformitätsrichtlinien für Microsoft Intune.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/14/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6bb3397432f1c171418ea99510cb04f1bdefc639
ms.sourcegitcommit: cb12dd341792c0379bebe9fd5f844600638c668a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252791"
---
# <a name="use-compliance-policies-to-set-rules-for-devices-you-manage-with-intune"></a>Verwenden von Konformitätsrichtlinien zum Festlegen von Regeln für Geräte, die Sie mit Intune verwalten

MDM-Lösungen (Mobile Device Management) wie Intune tragen zum Schutz von Unternehmensdaten bei, da Benutzer und Geräte bestimmte Anforderungen erfüllen müssen. In Intune wird dieses Feature *Konformitätsrichtlinien* genannt.

Konformitätsrichtlinien in Intune:

- Konformitätsrichtlinien definieren Regeln und Einstellungen, die Benutzer und Geräte erfüllen müssen, um als „konform“ zu gelten.
- Schließen Sie Aktionen ein, die auf nicht konforme Geräte angewendet werden. Diese Aktionen bei Nichtkonformität können Benutzer an die Gründe der Nichtkonformität warnen und Daten auf nicht konformen Geräten schützen.
- Sie können [in Kombination mit dem bedingten Zugriff](#integrate-with-conditional-access) verwendet werden, wodurch Benutzer und Geräte blockiert werden, die nicht den Regeln entsprechen.

Die Konformitätsrichtlinien in Intune haben zwei Teile:

- **Einstellungen für Konformitätsrichtlinien** – Mandantenweite Einstellungen, die einer integrierten Konformitätsrichtlinie entsprechen, die jedes Gerät erhält. Die Einstellungen für Konformitätsrichtlinien legen eine Baseline für die Funktionsweise von Konformitätsrichtlinien in ihrer Intune-Umgebung fest. Dazu zählt, ob Geräte, die keine Gerätekonformitätsrichtlinien erhalten haben, als konform oder nicht konform gelten.

- **Gerätekonformitätsrichtlinie** – Plattformspezifische Regeln, die Sie konfigurieren und für Gruppen von Benutzern oder Geräten bereitstellen.  Diese Regeln definieren die Anforderungen für Geräte, z. B. die minimalen Betriebssysteme oder die Verwendung der Datenträgerverschlüsselung. Geräte müssen diese Regeln erfüllen, um als konform eingestuft zu werden.

Wie bei anderen Intune-Richtlinien sind die Auswertungen der Konformitätsrichtlinie für ein Gerät davon abhängig, wann das Gerät bei Intune eingecheckt wird, und von den [Richtlinien- und Profilaktualisierungszyklen](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned).

## <a name="compliance-policy-settings"></a>Einstellungen für Kompatibilitätsrichtlinie

Die *Einstellungen für Konformitätsrichtlinien* sind mandantenweite Einstellungen, die bestimmen, wie der Intune-Konformitätsdienst mit Ihren Geräten interagiert. Diese Einstellungen unterscheiden sich von den Einstellungen, die Sie in einer Gerätekonformitätsrichtlinie konfigurieren.

Um die Einstellungen für Konformitätsrichtlinien zu verwalten, melden Sie sich bei [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an, und wechseln Sie zu **Endpoint Security** > **Gerätekonformität** > **Einstellungen für Gerätekonformität**.

Die Einstellungen für Konformitätsrichtlinien umfassen die folgenden Einstellungen:

- **Geräte ohne zugewiesene Konformitätsrichtlinie kennzeichnen als**

  Mit dieser Einstellung wird festgelegt, wie Intune Geräte behandelt, denen keine Gerätekonformitätsrichtlinie zugewiesen wurde. Diese Einstellung verfügt über zwei Optionen:
  - **Konform** (*Standard*): Diese Sicherheitsfunktion ist deaktiviert. Geräte, denen keine Gerätekonformitätsrichtlinie gesendet wurde, werden als *konform* betrachtet.
  - **Nicht konform**: Diese Sicherheitsfunktion ist aktiviert. Geräte, die keine Gerätekonformitätsrichtlinie erhalten haben, werden als nicht konform betrachtet.

  Wenn Sie den bedingten Zugriff mit Ihren Gerätekonformitätsrichtlinien verwenden, empfiehlt es sich, diese Einstellung in **Nicht konform** zu ändern, um sicherzustellen, dass nur Geräte, die als konform bestätigt werden, auf Ihre Ressourcen zugreifen können.

  Wenn ein Endbenutzer nicht konform ist, weil ihm keine Richtlinie zugewiesen ist, wird in der [Unternehmensportal-App](../apps/company-portal-app.md) angezeigt, dass keine Konformitätsrichtlinien zugewiesen wurden.

- **Verbesserte Erkennung von Jailbreaks** (*gilt nur für iOS/iPadOS*)

  Diese Einstellung funktioniert nur mit Geräten, auf die Sie eine Gerätekompatibilitätsrichtlinie ausgerichtet haben, mit der Geräte mit Jailbreaks blockiert werden.  (Weitere Informationen finden Sie unter [Integrität für Geräte](compliance-policy-create-ios.md#device-health) Einstellungen für iOS/iPadOS).

  Diese Einstellung verfügt über zwei Optionen:

  - **Deaktiviert** (*Standard*) Diese Sicherheitsfunktion ist deaktiviert. Diese Einstellung wirkt sich nicht auf Ihre Geräte aus, die Gerätekonformitätsrichtlinien empfangen, mit denen Geräte mit Jailbreaks blockiert werden.
  - **Aktiviert**: Diese Sicherheitsfunktion ist aktiviert. Geräte, die Gerätekonformitätsrichtlinien zum Blockieren von Geräten mit Jailbreaks erhalten, verwenden die erweiterte Jailbreak-Erkennung.

  Bei Aktivierung auf einem anwendbaren iOS/iPadOS-Gerät gilt für das Gerät Folgendes:

  - Es aktiviert Standortdienste auf Betriebssystemebene.
  - Es erlaubt dem Unternehmensportal immer, die Standortdienste zu nutzen.
  - Es verwendet seine Standortdienste, um die Jailbreak-Erkennung häufiger im Hintergrund auszulösen. Die Standortdaten des Benutzers werden nicht in Intune gespeichert.

  In folgenden Situationen führt die verbesserte Jailbreak-Erkennung Auswertung durch:

  - Die Unternehmensportal-App wird geöffnet.
  - Das Gerät wird über eine beträchtliche Entfernung physisch bewegt, was etwa 500 Meter oder mehr beträgt. Intune kann nicht garantieren, dass durch jede bedeutende Standortänderung eine Jailbreak-Erkennungsprüfung ausgelöst wird, da dies von der Netzwerkverbindung des Geräts zum gegebenen Zeitpunkt abhängt.

  Unter iOS 13 und höher müssen Benutzer aufgrund dieses Features immer auf *Immer zulassen* klicken, wenn das Gerät sie dazu auffordert, dem Unternehmensportal weiterhin zu gestatten, ihren Standort im Hintergrund zu verwenden. Wenn Benutzer nicht jedes Mal den Standortzugriff genehmigen und eine Richtlinie mit dieser Einstellung konfiguriert haben, wird ihr Gerät als nicht konform gekennzeichnet.

- **Gültigkeitszeitraum des Konformitätsstatus (Tage)** :

  Geben Sie einen Zeitraum an, in dem Geräte erfolgreich Berichte zu allen empfangenen Konformitätsrichtlinien melden müssen. Wenn ein Gerät vor Ablauf der Gültigkeitsdauer keinen Konformitätsstatus für eine Richtlinie meldet, wird das Gerät als nicht konform behandelt.

  Der Zeitraum ist standardmäßig auf 30 Tage festgelegt. Sie können einen Zeitraum zwischen 1 und 120 Tagen konfigurieren.

  Details zur Gerätekonformität finden Sie in der Einstellung für die Gültigkeitsdauer. Melden Sie sich bei [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an und wechseln Sie zu **Geräte** > **Überwachen** > **Einstellungskonformität**. Diese Einstellung hat den Namen **Ist aktiv** in der Spalte *Einstellung*.  Weitere Informationen zu diesen und zugehörigen Konformitätsstatusansichten finden Sie unter [Überwachen der Gerätekonformtät](compliance-policy-monitor.md).

## <a name="device-compliance-policies"></a>Konformitätsrichtlinien für Geräte

Intune-Gerätekonformitätsrichtlinien:

- Definieren Regeln und Einstellungen, die Benutzer und verwaltete Geräte erfüllen müssen, um als „konform“ zu gelten. Beispiele für Regeln sind u. a. die Notwendigkeit, dass Geräte eine minimale Betriebssystemversion ausführen, nicht durch Jailbreak oder Rooting manipuliert wurden und maximal die *Bedrohungsstufe* aufweisen, die von der Bedrohungsmanagementsoftware festgelegt wurde, die Sie in Intune integriert haben.
- Unterstützen Aktionen, die für Geräte gelten, die Ihre Konformitätsrichtlinie nicht erfüllen. Beispiele für Aktionen sind das Fernsperren oder das Senden einer E-Mail-Nachricht an den Gerätebenutzer zum Gerätestatus, damit dieser die Probleme beheben kann.
- Werden für Benutzer in Benutzergruppen oder Geräten in Gerätegruppen bereitgestellt. Wenn eine Konformitätsrichtlinie für einen Benutzer bereitgestellt wird, werden alle Geräte des Benutzers auf Konformität überprüft. Die Verwendung von Gerätegruppen in diesem Szenario hilft beim Erstellen von Konformitätsberichten.

Wenn Sie den bedingten Zugriff verwenden, können Ihre Richtlinien für den bedingten Zugriff Ihre Gerätekonformitätsergebnisse verwenden, um den Zugriff auf Ressourcen von nicht konformen Geräten zu blockieren.

Welche Einstellungen verfügbar sind, die Sie in einer Gerätekonformitätsrichtlinie festlegen können, hängt vom Plattformtyp ab, den Sie beim Erstellen einer Richtlinie auswählen. Verschiedene Geräteplattformen unterstützen verschiedene Einstellungen, und jeder Plattformtyp erfordert eine separate Richtlinie.  

Die folgenden Themen sind mit dedizierten Artikeln für verschiedene Aspekte der Gerätekonfigurationsrichtlinie verknüpft.

- [**Aktionen bei Nichtkonformität**](actions-for-noncompliance.md) – Jede Gerätekonformitätsrichtlinie umfasst mindestens eine Aktion bei Nichtkonformität. Diese Aktionen sind Regeln, die auf Geräte angewendet werden, die die Bedingungen nicht erfüllen, die Sie in der Richtlinie festgelegt haben.

  Standardmäßig umfasst jede Gerätekonformitätsrichtlinie die Aktion, um ein Gerät als nicht konform zu kennzeichnen, wenn eine Richtlinienregel nicht erfüllt wird. Die Richtlinie wendet dann auf das Gerät alle zusätzlichen Aktionen bei Nichtkonformität an, die Sie konfiguriert haben, basierend auf den Zeitplänen, die Sie für diese Aktionen festgelegt haben.

  Aktionen bei Nichtkonformität können Benutzer warnen, wenn ihr Gerät nicht konform ist, oder Daten schützen, die möglicherweise auf einem Gerät vorliegen. Beispiele für Aktionen:

  - **Senden von E-Mail-Benachrichtigungen** an Benutzer und Gruppen mit Details zum nicht konformen Gerät. Sie können die Richtlinie so konfigurieren, dass sie sofort eine E-Mail sendet, wenn das Gerät als nicht konform gekennzeichnet wird, und danach regelmäßig, bis das Gerät wieder konform ist.
  - **Fernsperren von Geräten**, die seit einiger Zeit nicht konform sind.
  - **Außerbetriebnahme von Geräten**, nachdem sie einige Zeit nicht konform waren. Diese Aktion entfernt das Gerät aus der Intune-Verwaltung und entfernt alle Unternehmensdaten von dem Gerät.

- [**Konfigurieren von Netzwerkstandorten** – Unterstützt von Android-Geräten können Sie ](use-network-locations.md) können Sie *Netzwerkstandorte* konfigurieren, und diese Standorte dann als Regel für die Gerätekonformität verwenden. Bei diesem Regeltyp kann ein Gerät als nicht konform gekennzeichnet werden, wenn es ein bestimmtes Netzwerk verlässt oder sich außerhalb von diesem befindet. Bevor Sie eine Standortregel festlegen können, müssen Sie die Netzwerkstandorte konfigurieren.

- [**Erstellen einer Richtlinie**](create-compliance-policy.md) – Mit den Informationen in diesem Artikel können Sie die Voraussetzungen überprüfen, die Optionen zum Konfigurieren von Regeln erkunden, Aktionen bei Nichtkonformität festlegen und die Richtlinie Gruppen zuweisen. Dieser Artikel enthält auch Informationen zu den Aktualisierungszeiten für Richtlinien.

  In den Konformitätseinstellungen für die unterschiedlichen Geräteplattformen finden Sie weitere Informationen:

  - [Android](compliance-policy-create-android.md)
  - [Android Enterprise](compliance-policy-create-android-for-work.md)
  - [iOS](compliance-policy-create-ios.md)
  - [macOS](compliance-policy-create-mac-os.md)
  - [Windows Holographic for Business](compliance-policy-create-windows.md#windows-holographic-for-business)
  - [Windows 8.1 und höher](compliance-policy-create-windows-8-1.md)
  - [Windows 10 und höher](compliance-policy-create-windows.md)

## <a name="monitor-compliance-status"></a>Überwachen des Konformitätsstatus

Intune enthält ein Dashboard für die Gerätekonformität, mit dem Sie den Konformitätsstatus von Geräten überwachen und einen Drilldown zu Richtlinien und Geräten durchführen können, um weitere Informationen zu erhalten. Weitere Informationen zu diesem Dashboard finden Sie unter [Überwachen der Gerätekonformität](compliance-policy-monitor.md).

## <a name="integrate-with-conditional-access"></a>Integration mit bedingtem Zugriff

Wenn Sie den bedingten Zugriff verwenden, können Sie Ihre Richtlinien für den bedingten Zugriff so konfigurieren, dass anhand der Ergebnisse Ihrer Gerätekonformitätsrichtlinien bestimmt wird, welche Geräte auf Ihre Unternehmensressourcen zugreifen können. Diese Zugriffssteuerung erfolgt zusätzlich zu und unabhängig von den Aktionen bei Nichtkonformität, die Sie in Ihre Gerätekonformitätsrichtlinien integrieren.

Wenn ein Gerät in Intune registriert wird, wird es auch in Azure AD registriert. Der Konformitätsstatus für Geräte wird an Azure AD gemeldet. Wenn in Ihren Richtlinien für den bedingten Zugriff für die Zugriffsteuerung festgelegt ist, dass *das Gerät als konform gekennzeichnet sein muss*, verwendet der bedingte Zugriff diesen Konformitätsstatus, um zu bestimmen, ob der Zugriff auf E-Mails und andere Unternehmensressourcen gewährt oder blockiert wird.

Wenn Sie den Gerätekonformitätsstatus mit Richtlinien für den bedingten Zugriff verwenden, müssen Sie überprüfen, wie Ihr Mandant die Einstellung *Geräte ohne zugewiesene Konformitätsrichtlinie kennzeichnen als* konfiguriert hat, was Sie unter [Einstellungen für Konformitätsrichtlinien](#compliance-policy-settings) verwalten können.

Weitere Informationen zur Verwendung des bedingten Zugriffs mit ihren Gerätekonformitätsrichtlinien finden Sie unter [Gerätebasierter bedingter Zugriff.](conditional-access-intune-common-ways-use.md#device-based-conditional-access)

Weitere Informationen zum bedingten Zugriff finden Sie in der Azure AD-Dokumentation:

- [Was ist bedingter Zugriff?](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [Was ist eine Geräteidentität?](https://docs.microsoft.com/azure/active-directory/device-management-introduction)

### <a name="reference-for-non-compliance-and-conditional-access-on-the-different-platforms"></a>Verweis auf Nichtkonformität und bedingten Zugriff auf den unterschiedlichen Plattformen

In der folgenden Tabelle wird beschrieben, wie nicht konforme Einstellungen verwaltet werden, wenn eine Konformitätsrichtlinie mit einer Richtlinie für bedingten Zugriff verwendet wird.

- **Bereinigt:** Das Betriebssystem des Geräts erzwingt die Konformität. Es ist z.B. erforderlich, dass der Benutzer eine PIN festlegt.

- **In Quarantäne:** Das Betriebssystem des Geräts erzwingt keine Konformität. Android- und Android Enterprise-Geräte zwingen den Benutzer z. B. nicht dazu, das Gerät zu verschlüsseln. Wenn das Gerät nicht kompatibel ist, erfolgen die folgenden Aktionen:
  - Wenn eine Richtlinie für bedingten Zugriff für den Benutzer gilt, wird das Gerät blockiert.
  - Die Unternehmensportal-App benachrichtigt den Benutzer über Konformitätsprobleme.

---------------------------

|**Richtlinieneinstellung**| **Plattform** |
| --- | ----|
| **PIN- oder Kennwortkonfiguration** | - **Android 4.0 und höher:** Isoliert<br>- **Samsung Knox Standard 4.0 und höher:** Isoliert<br>- **Android Enterprise:** Isoliert  <br>  <br>- **iOS 8.0 oder höher:** Wiederhergestellt<br>- **macOS 10.11 und höher:** Wiederhergestellt  <br>  <br>- **Windows 8.1 und höher:** Wiederhergestellt|
| **Geräteverschlüsselung** | - **Android 4.0 und höher:** Isoliert<br>- **Samsung Knox Standard 4.0 und höher:** Isoliert<br>- **Android Enterprise:** Isoliert<br><br>- **iOS 8.0 oder höher:** Wiederhergestellt (durch Festlegen der PIN)<br>- **macOS 10.11 und höher:** Wiederhergestellt (durch Festlegen der PIN)<br><br>- **Windows 8.1 und höher:** Nicht zutreffend|
| **Per Jailbreak oder Rootzugriff manipuliertes Gerät** | - **Android 4.0 und höher:** Unter Quarantäne gestellt (keine Einstellung)<br>- **Samsung Knox Standard 4.0 und höher:** Unter Quarantäne gestellt (keine Einstellung)<br>- **Android Enterprise:** Unter Quarantäne gestellt (keine Einstellung)<br><br>- **iOS 8.0 oder höher:** Unter Quarantäne gestellt (keine Einstellung)<br>- **macOS 10.11 und höher:** Nicht zutreffend<br><br>- **Windows 8.1 und höher:** Nicht zutreffend |
| **E-Mail-Profil** | - **Android 4.0 und höher:** Nicht zutreffend<br>- **Samsung Knox Standard 4.0 und höher:** Nicht zutreffend<br>- **Android Enterprise:** Nicht zutreffend<br><br>- **iOS 8.0 oder höher:** Isoliert<br>- **macOS 10.11 und höher:** Isoliert<br><br>- **Windows 8.1 und höher:** Nicht zutreffend |
| **Minimales Release des Betriebssystems** | - **Android 4.0 und höher:** Isoliert<br>- **Samsung Knox Standard 4.0 und höher:** Isoliert<br>- **Android Enterprise:** Isoliert<br><br>- **iOS 8.0 oder höher:** Isoliert<br>- **macOS 10.11 und höher:** Isoliert<br><br>- **Windows 8.1 und höher:** Isoliert|
| **Maximales Release des Betriebssystems** | - **Android 4.0 und höher:** Isoliert<br>- **Samsung Knox Standard 4.0 und höher:** Isoliert<br>- **Android Enterprise:** Isoliert<br><br>- **iOS 8.0 oder höher:** Isoliert<br>- **macOS 10.11 und höher:** Isoliert<br><br>- **Windows 8.1 und höher:** Isoliert |
| **Windows-Integritätsnachweis** | - **Android 4.0 und höher:** Nicht zutreffend<br>- **Samsung Knox Standard 4.0 und höher:** Nicht zutreffend<br>- **Android Enterprise:** Nicht zutreffend<br><br>- **iOS 8.0 oder höher:** Nicht zutreffend<br>- **macOS 10.11 und höher:** Nicht zutreffend<br><br>- **Windows 10**: Isoliert<br>- **Windows 8.1 und höher:** Isoliert |

---------------------------

## <a name="next-steps"></a>Nächste Schritte

- [Standorte konfigurieren](../protect/use-network-locations.md) zur Verwendung mit Android-Geräten
- [Erstellen und Bereitstellen einer Richtlinie](../protect/create-compliance-policy.md) und Voraussetzungen prüfen
- [Überwachen der Gerätekonformität](../protect/compliance-policy-monitor.md)
- [Häufige Fragen, Probleme und entsprechende Behebungen mit Geräterichtlinien und -profilen in Microsoft Intune](../configuration/device-profile-troubleshoot.md)
- Weitere Informationen zu den Intune-Richtlinienentitäten für Data Warehouses finden Sie unter [Referenz für Richtlinienentitäten](../developer/reports-ref-policy.md).
