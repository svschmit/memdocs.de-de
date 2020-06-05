---
title: Konfigurieren von Endpoint Protection-Einstellungen in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Erstellen Sie Endpoint Protection-Einstellungen, wenn Sie in Microsoft Intune ein macOS- oder Windows 10-Geräteprofil erstellen.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/24/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
mr.reviewer: karthib
ms.openlocfilehash: cb51d5f73edbc28572ee01d49ba4bd5a62cf6393
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989636"
---
# <a name="add-endpoint-protection-settings-in-intune"></a>Hinzufügen der Endpoint Protection-Einstellungen in Intune

Mit Intune können Sie Gerätekonfigurationsprofile verwenden, um allgemeine Sicherheitsfunktionen für den Endpunktschutz auf Geräten zu verwalten, einschließlich:

- Firewall
- BitLocker
- Zulassen und Sperren von Apps
- Microsoft Defender und Verschlüsselung

Beispielsweise können Sie ein Endpoint Protection-Profil erstellen, über das nur macOS-Benutzer Apps aus dem Mac App Store installieren können. Stattdessen können Sie auch Windows SmartScreen aktivieren, wenn Sie Apps auf Windows 10-Geräten ausführen.

Bevor Sie ein Profil erstellen, lesen Sie die folgenden Artikel, in denen die Einstellungen für den Endpunktschutz dargelegt werden, die Intune für die jeweilige unterstützte Plattform verwalten kann:

- [Einstellungen für macOS](endpoint-protection-macos.md)
- [Einstellungen für Windows 10](endpoint-protection-windows-10.md)

## <a name="create-a-device-profile-containing-endpoint-protection-settings"></a>Erstellen von Geräteprofilen mit Endpoint Protection-Einstellungen

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.

3. Geben Sie die folgenden Eigenschaften ein:

    - **Plattform**: Wählen Sie die Plattform Ihrer Geräte aus. Folgende Optionen sind verfügbar:

        - **macOS**
        - **Windows 10 und höher**

    - **Profil**: Wählen Sie **Endpoint Protection** aus.

4. Wählen Sie **Erstellen** aus.
5. Geben Sie in **Grundlagen** die folgenden Eigenschaften ein:

   - **Name:** Geben Sie einen aussagekräftigen Namen für die Richtlinie ein. Benennen Sie Ihre Richtlinien so, dass Sie diese später leicht wiedererkennen. Ein guter Richtlinienname enthält beispielsweise den Profiltyp und die Plattform.

   - **Beschreibung:** Geben Sie eine Beschreibung für die Richtlinie ein. Diese Einstellung ist optional, wird jedoch empfohlen.

6. Wählen Sie **Weiter** aus.

7. Die verfügbaren **Konfigurationseinstellungen** variieren je nach ausgewählter Plattform. Wählen Sie Ihre Plattform für detaillierte Einstellungen aus:

   - [Einstellungen für macOS](endpoint-protection-macos.md)
   - [Einstellungen für Windows 10](endpoint-protection-windows-10.md)

8. Wählen Sie **Weiter** aus.
9. Weisen Sie in **Bereichstags** (optional) ein Tag zu, um das Profil nach bestimmten IT-Gruppen wie `US-NC IT Team` oder `JohnGlenn_ITDepartment` zu filtern. Weitere Informationen zu Bereichstags finden Sie unter [Verwenden der RBAC und von Bereichstags für verteilte IT](../fundamentals/scope-tags.md).

    Wählen Sie **Weiter** aus.

10. Wählen Sie unter **Zuweisungen** die Benutzer oder Gruppen aus, denen Ihr Profil zugewiesen werden soll. Weitere Informationen zum Zuweisen von Profilen finden Sie unter [Zuweisen von Benutzer- und Geräteprofilen](../configuration/device-profile-assign.md).

    Wählen Sie **Weiter** aus.

11. Überprüfen Sie die Einstellungen unter **Überprüfen + erstellen**. Wenn Sie auf **Erstellen** klicken, werden die Änderungen gespeichert, und das Profil wird zugewiesen. Die Richtlinie wird auch in der Profilliste angezeigt.

## <a name="add-custom-firewall-rules-for-windows-10-devices"></a>Hinzufügen benutzerdefinierter Firewallregeln für Windows 10-Geräte

Wenn Sie Microsoft Defender Firewall als Teil eines Profils konfigurieren, das Endpoint Protection-Regeln für Windows 10 umfasst, können Sie benutzerdefinierte Regeln für Firewalls konfigurieren. Benutzerdefinierte Regeln ermöglichen es Ihnen, die vordefinierten Firewallregeln zu erweitern, die für Windows 10 unterstützt werden.

Wenn Sie Profile mit benutzerdefinierten Firewallregeln planen, sollten Sie die folgenden Informationen berücksichtigen, die sich auf das Gruppieren von Firewallregeln in ihren Profilen auswirken können:

- Jedes Profil unterstützt bis zu 150 Firewallregeln. Wenn Sie mehr als 150 Regeln verwenden, sollten Sie zusätzliche Profile erstellen, die jeweils auf 150 Regeln beschränkt sind.

- Wenn eine einzelne Regel nicht angewendet werden kann, schlagen für alle Regeln sämtliche Profile fehl, und keine der Regeln wird auf das Gerät angewendet.

- Wenn eine Regel nicht angewendet werden kann, werden für alle Regeln im Profil ein Fehler gemeldet. Intune kann nicht feststellen, welche Regel fehlgeschlagen ist.  

Die Firewallregeln, die von Intune verwaltet werden können, werden im Artikel [Windows-Firewall-Konfigurationsdienstanbieter](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp) ausführlich beschrieben. Die Liste der benutzerdefinierten Firewalleinstellungen für Windows 10-Geräte, die von Intune unterstützt werden, finden Sie unter [Custom Firewall rules (Benutzerdefinierte Firewallregeln)](endpoint-protection-windows-10.md#firewall-rules).

### <a name="to-add-custom-firewall-rules-to-an-endpoint-protection-profile"></a>So fügen Sie einem Endpoint Protection-Profil benutzerdefinierte Firewallregeln hinzu

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.

3. Klicken Sie unter *Plattform* auf die Option **Windows 10 und höher** und anschließend unter *Profil* auf **Endpoint Protection**.

    Wählen Sie **Erstellen** aus.

4. Geben Sie einen **Namen** für Ihr Profil ein, und klicken Sie auf **Weiter**.
5. Klicken Sie unter **Konfigurationseinstellungen** auf **Microsoft Defender Firewall**. Klicken Sie unter *Firewallregeln* auf **Hinzufügen**, um die Seite **Regel erstellen** zu öffnen.

6. Legen Sie Einstellungen für die Firewallregel fest, und klicken Sie dann auf **OK**, um diese zu speichern. Informationen zu den verfügbaren Optionen für benutzerdefinierte Firewallregeln in der Dokumentation finden Sie unter [Custom Firewall rules (Benutzerdefinierte Firewallregeln)](endpoint-protection-windows-10.md#firewall-rules).

    1. Die Regel wird auf der Seite *Microsoft Defender Firewall* in der Liste mit den Regeln aufgeführt.
    2. Sie können Regeln ändern, indem Sie die gewünschte Regel aus der Liste auswählen, um die Seite **Regel bearbeiten** zu öffnen.
    3. Wenn Sie eine Regel aus einem Profil löschen möchten, klicken Sie erst auf die Auslassungspunkte **(...)** und anschließend auf **Löschen**.
    4. Sie können die Reihenfolge ändern, in der die Regeln angezeigt werden, indem Sie im oberen Bereich der Regelliste auf das Symbol mit den *Pfeilen nach oben und unten* klicken.

7. Klicken Sie auf **Weiter**, bis Sie zu **Überprüfen + erstellen** gelangen. Wenn Sie auf **Erstellen** klicken, werden die Änderungen gespeichert, und das Profil wird zugewiesen. Die Richtlinie wird auch in der Profilliste angezeigt.

## <a name="next-steps"></a>Nächste Schritte

Das Profil ist nun erstellt, führt aber vielleicht noch keine Aktionen durch. Die nächsten Schritte sind das [Zuweisen von Benutzer- und Geräteprofilen in Microsoft Intune](../configuration/device-profile-assign.md) und das [Überwachen von Geräteprofilen in Microsoft Intune](../configuration/device-profile-monitor.md).
