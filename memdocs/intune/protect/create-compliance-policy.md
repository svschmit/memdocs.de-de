---
title: Erstellen von Gerätekonformitätsrichtlinien in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Erstellen von Gerätekonformitätsrichtlinien, Übersicht über den Status und die Sicherheitsebenen, Verwendung des InGracePeriod-Status, Arbeiten mit bedingtem Zugriff, Handhabung von Geräten ohne zugewiesene Richtlinie und die Unterschiede bei der Konformität im Azure-Portal und im klassischen Portal in Microsoft Intune
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: b437a72a2380fea215746aa76b35898c6fc60b16
ms.sourcegitcommit: 0ad7cd842719887184510c6acd9cdfa290a3ca91
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/02/2020
ms.locfileid: "80551384"
---
# <a name="create-a-compliance-policy-in-microsoft-intune"></a>Erstellen einer Konformitätsrichtlinie in Microsoft Intune

Konformitätsrichtlinien für Geräte sind ein wichtiges Feature bei der Verwendung von Intune, um die Ressourcen Ihrer Organisation zu schützen. Sie können in Intune Regeln und Einstellungen erstellen, die Geräte erfüllen müssen, um als konform angesehen zu werden, z. B. die mindestens erforderliche Betriebssystemversion. Wenn das Gerät nicht konform ist, können Sie dann den Zugriff auf Daten und Ressourcen mit [bedingtem Zugriff](conditional-access.md) blockieren.

Sie können auch Maßnahmen ergreifen, sollte das Gerät nicht konform sein, z. B. eine Benachrichtigungs-E-Mail an den Benutzer senden. Eine Übersicht der Funktionsweise von Konformitätsrichtlinie und wie Sie diese verwenden können, finden Sie unter [Erste Schritte mit den Gerätekonformitätsrichtlinien in Intune](device-compliance-get-started.md).

Inhalt dieses Artikels

- Liste der Voraussetzungen und Schritte zum Erstellen einer Konformitätsrichtlinie.
- Zuweisen der Richtlinie an einen Benutzer und an eine Gerätegruppe.
- Beschreibung zusätzlicher Funktionen, u. a. Bereichstags zum „Filtern“ Ihrer Richtlinien, und möglicher Maßnahmen für Geräte, die nicht konform sind.
- Liste der Check-In-Aktualisierungszykluszeiten, wenn Geräte Richtlinienaktualisierungen erhalten.

## <a name="before-you-begin"></a>Vorbereitung

Stellen Sie zum Verwenden von Konformitätsrichtlinien folgendes sicher:

- Verwenden Sie folgende Abonnements:

  - Intune
  - Wenn Sie den bedingten Zugriff verwenden, benötigen Sie die Azure Active Directory-Premium-Edition. In der Liste mit den [Preisen für Azure Active Directory](https://azure.microsoft.com/pricing/details/active-directory/) finden Sie Angaben zu den unterschiedlichen Editionen. Für die Intune-Konformität ist Azure Active Directory nicht erforderlich.

- Verwenden Sie eine unterstützte Plattform:

  - Android-Geräteadministrator
  - Android Enterprise
  - iOS
  - macOS
  - Windows 10
  - Windows 8.1
  - Windows Phone 8.1

- Registrieren Sie Geräte in Intune (nur dann können Sie den Konformitätsstatus ermitteln).

- Registrieren Sie Geräte für einen Benutzer oder registrieren Sie ohne einen Hauptbenutzer. Für mehrere Benutzer registrierte Geräte werden nicht unterstützt.

> [!NOTE]
> Die Intune-Benutzeroberfläche (User Interface, UI) wird auf eine Vollbildversion aktualisiert, und dies kann einige Wochen in Anspruch nehmen. Bis Ihr Mandant dieses Update erhält, haben Sie einen etwas anderen Workflow, wenn Sie die in diesem Artikel beschriebenen Einstellungen erstellen oder bearbeiten.

## <a name="create-the-policy"></a>Erstellen der Richtlinie

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Geräte** > **Konformitätsrichtlinien** > **Richtlinien** > **Richtlinie erstellen** aus.

3. Wählen Sie aus den folgenden Optionen eine **Plattform** für diese Richtlinie aus:
   - *Android-Geräteadministrator*
   - *Android Enterprise*
   - *iOS/iPadOS*
   - *macOS*
   - *Windows Phone 8.1*
   - *Windows 8.1 und höher*
   - *Windows 10 und höher*

    Für *Android Enterprise* können Sie auch einen **Richtlinientyp** auswählen:
     - *Konformitätsrichtlinie für Android-Gerätebesitzer*
     - *Konformitätsrichtlinie für Android-Arbeitsprofil*

    Wählen Sie dann **Erstellen** aus, um das Konfigurationsfenster **Richtlinie erstellen** zu öffnen.

4. Geben Sie auf der Registerkarte **Grundlagen** einen **Namen** an, um die Richtlinie später identifizieren zu können. Ein geeigneter Richtlinienname ist z. B. **iOS/iPadOS-Geräte mit Jailbreak als nicht konform markieren**.

   Sie können auch eine **Beschreibung** angeben.
  
5. Erweitern Sie auf der Registerkarte **Konformitätseinstellungen** die verfügbaren Kategorien, und konfigurieren Sie Einstellungen für Ihre Richtlinie.  In den folgenden Artikeln werden die Einstellungen für die einzelnen Plattformen beschrieben:
   - [Android-Geräteadministrator](compliance-policy-create-android.md)
   - [Android Enterprise](compliance-policy-create-android-for-work.md)
   - [iOS/iPadOS](compliance-policy-create-ios.md)
   - [macOS](compliance-policy-create-mac-os.md)
   - [Windows Phone 8.1, Windows 8.1 und höher](compliance-policy-create-windows-8-1.md)
   - [Windows 10 und höher](compliance-policy-create-windows.md)  

6. Auf der Registerkarte **Standorte** können Sie die Konformität basierend auf dem Standort des Geräts erzwingen. Sie können vorhandene Standorte auswählen. Wenn noch kein Standort verfügbar ist, finden Sie weitere Informationen unter [Verwenden von Standorten (Netzwerkfence)](use-network-locations.md).
   > [!TIP]
   > **Standorte** sind nur für die Plattform *Android-Geräteadministrator* verfügbar.

7. Geben Sie auf der Registerkarte **Aktionen bei Nichtkonformität** eine Reihe von Aktionen an, die automatisch auf Geräte angewendet werden, die diese Konformitätsrichtlinie nicht erfüllen.

   Sie können mehrere Aktionen hinzufügen und Zeitpläne sowie weitere Details für einige Aktionen konfigurieren. Sie können beispielsweise den Zeitplan der Standardaktion *Gerät als nicht konform markieren* so ändern, dass die Aktion nach einem Tag ausgeführt wird. Dann können Sie eine Aktion hinzufügen, mit der eine E-Mail mit einer Warnung an den Benutzer gesendet wird, wenn ein Gerät nicht konform ist. Sie können auch Aktionen hinzufügen, die Geräte sperren oder außer Betrieb nehmen, die weiterhin nicht konform sind.

   Informationen zu den Aktionen, die Sie konfigurieren können – z. B. zum Senden von Benachrichtigungs-E-Mails an Ihre Benutzer –, finden Sie unter [Aktionen für nicht konforme Geräte hinzufügen](actions-for-noncompliance.md).

   Ein anderes Beispiel ist die Verwendung von Standorten: Sie können einer Konformitätsrichtlinie mindestens einen Standort hinzufügen. In diesem Fall gilt die Standardaktion für Nichtkonformität, wenn Sie mindestens einen Standort auswählen. Wenn ein Gerät nicht mit einem der ausgewählten Standorte verbunden ist, wird es als nicht konform betrachtet. Sie können den Zeitplan so konfigurieren, dass Ihren Benutzern eine Toleranzperiode eingeräumt wird (z.B. ein Tag).

8. Wählen Sie auf der Registerkarte **Bereich** Tags aus, mit denen die Richtlinien für bestimmte Gruppen gefiltert werden können, wie etwa `US-NC IT Team` oder `JohnGlenn_ITDepartment`. Nachdem Sie die Einstellungen hinzugefügt haben, können Sie Ihrer Konformitätsrichtlinie ebenfalls eine Bereichsmarkierung hinzufügen. 

   Weitere Informationen zur Verwendung von Bereichstags finden Sie unter [Verwenden von Bereichsmarkierungen](../fundamentals/scope-tags.md).

9. Weisen Sie die Richtlinie auf der Registerkarte **Zuweisungen** Ihren Gruppen zu.  

   Klicken Sie auf **+ Einzuschließende Gruppen auswählen**, und weisen Sie die Richtlinie einer oder mehreren Gruppen zu. Die Richtlinie wird auf diese Gruppen angewendet, wenn Sie die Richtlinie nach dem nächsten Schritt speichern. 

10. Überprüfen Sie die Einstellungen auf der Registerkarte **Überprüfen + erstellen**, und klicken Sie auf **Erstellen**, um die Konformitätsrichtlinie zu speichern.  

    Die Benutzer oder Geräte, für die Ihre Richtlinie gilt, werden hinsichtlich der Konformität ausgewertet, wenn sie mit Intune eingecheckt werden.

<!-- Evaluate option  - pending details as to its fate with this new Full Screen UI udpate  

### Evaluate how many users are targeted

When you assign the policy, you can also **Evaluate** how many users are affected. This feature calculates users; it doesn't calculate devices.

1. In Intune, select **Devices** > **Compliance policies** > **Policies**.

2. Select a *policy* > **Assignments** > **Evaluate**. A message shows you how many users are targeted by this policy.

If the **Evaluate** button is grayed out, make sure the policy is assigned to one or more groups.
-->

## <a name="refresh-cycle-times"></a>Aktualisierungszykluszeit

Intune verwendet verschiedene Aktualisierungszyklen, um nach Updates der Konformitätsrichtlinien zu suchen. Wenn das Gerät kürzlich registriert wurde, wird der Check-In häufiger durchgeführt. Unter [Richtlinien- und Profilaktualisierungszyklen](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned) werden die geschätzten Aktualisierungszeiten aufgeführt.

Benutzer können jederzeit die Unternehmensportal-App öffnen und das Gerät synchronisieren, um sofort nach Richtlinienupdates zu suchen.

### <a name="assign-an-ingraceperiod-status"></a>Zuweisung eines InGracePeriod-Status

Der InGracePeriod-Status für eine Konformitätsrichtlinie ist ein Wert. Der Wert wird durch die Kombination der Toleranzperiode eines Geräts und dem tatsächlichen Status eines Geräts in Bezug auf diese Konformitätsrichtlinie ermittelt.

Im Detail bedeutet das: Wenn ein Gerät den Status „NonCompliant“ für eine zugewiesene Richtlinie aufweist und:

- dem Gerät keine Toleranzperiode zugewiesen ist, dann ist der zugewiesene Wert für die Konformitätsrichtlinie „NonCompliant“.
- die Toleranzperiode des Geräts abgelaufen ist, dann lautet der zugewiesene Wert für die Konformitätsrichtlinie „NonCompliant“.
- die Toleranzperiode des Geräts erst in der Zukunft abläuft, lautet der zugewiesene Wert für die Konformitätsrichtlinie „InGracePeriod“.

In der folgenden Tabelle werden diese Punkte zusammengefasst:

|Tatsächlicher Konformitätsstatus|Wert der zugewiesenen Toleranzperiode|Effektiver Konformitätsstatus|
|---------|---------|---------|
|NonCompliant |Keine Toleranzperiode zugewiesen |NonCompliant |
|NonCompliant |Datum des Vortags|NonCompliant|
|NonCompliant |Datum des folgenden Tags|InGracePeriod|

Weitere Informationen zum Überwachen der Richtlinien zur Gerätekonformität finden Sie unter [Überwachen von Intune-Richtlinien zur Gerätekonformität](compliance-policy-monitor.md).

### <a name="assign-a-resulting-compliance-policy-status"></a>Zuweisen eines resultierenden Konformitätsrichtlinienstatus

Wenn ein Gerät mehrere Konfigurationsprofile hat und es über verschiedene Konformitätsstatus für mindestens zwei zugeordnete Konformitätsprofile verfügt, wird genau ein resultierender Konformitätsstaus zugewiesen. Diese Zuweisung basiert auf einem konzeptuellen Schweregrad, der den einzelnen Konformitätsstatus zugewiesen ist. Jeder Konformitätsstatus verfügt über den folgenden Schweregrad:

|Status  |Schweregrad  |
|---------|---------|
|Unbekannt     |1|
|NotApplicable     |2|
|Kompatibel|3|
|InGracePeriod|4|
|NonCompliant|5|
|Fehler|6|

Hat ein Gerät mehrere Konformitätsrichtlinien, so wird dem Gerät der höchste Schweregrad aller Richtlinien zugewiesen.

Angenommen, einem Gerät sind z. B. drei Konformitätsrichtlinien zugewiesen: ein Status „Unknown“ (Unbekannt, Schweregrad = 1), ein Status „Compliant“ (Konform, Schweregrad = 3) und ein Status „InGracePeriod“ (Befristet, Schweregrad = 4). Der Status „InGracePeriod“ (Befristet) hat den höchsten Schweregrad. Deshalb haben alle drei Richtlinien den Konformitätsstatus „InGracePeriod“ (Befristet).

## <a name="next-steps"></a>Nächste Schritte

[Überwachen von Intune-Richtlinien zur Gerätekompatibilität](compliance-policy-monitor.md).
