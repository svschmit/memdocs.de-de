---
title: Verwalten der Endpunktsicherheitsrichtlinien in Microsoft Intune | Microsoft-Dokumentation
description: Erfahren Sie, wie Sicherheitsadministratoren die Richtlinien und Profile für Endgerätesicherheit verwenden können, um sich auf die Sicherheitskonfiguration von Geräten in Microsoft Endpoint Manager zu konzentrieren.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/15/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 071cab69b652193b835282603e187e4f3d0c7b0d
ms.sourcegitcommit: 97f150f8ba8be8746aa32ebc9b909bb47e22121c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2020
ms.locfileid: "84879728"
---
# <a name="manage-device-security-with-endpoint-security-policies-in-microsoft-intune"></a>Verwalten der Gerätesicherheit mit Endgerätesicherheitsrichtlinien in Microsoft Intune

Verwenden Sie als Sicherheitsadministrator die Sicherheitsrichtlinien der *Endpunktsicherheit* von Intune, um die Gerätesicherheit zu konfigurieren, ohne dazu die Vielzahl von Einstellungen in den Gerätekonfigurationsprofilen und Sicherheitsbaselines bearbeiten zu müssen.

Jeder Richtlinientyp unterstützt mindestens ein Profil. In Profilen konfigurieren Sie Einstellungen und können Einstellungen für verschiedene Plattformen oder für verschiedene Schwerpunktbereiche im größeren Richtlinienbereich gruppieren.

Diese Richtlinien finden Sie unter *Verwalten* im Knoten **Endpunktsicherheit** im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).

![Verwalten von Richtlinien](./media/endpoint-security-policy/endpoint-security-policies.png)

Im Folgenden finden Sie kurze Beschreibungen der einzelnen Typen von Endpunktsicherheitsrichtlinien. Um mehr über die einzelnen Typen zu erfahren, einschließlich der verfügbaren Profile, folgen Sie den Links zu den Inhalten der jeweiligen Richtlinientypen:

- [Antivirus](../protect/endpoint-security-antivirus-policy.md): Antivirenrichtlinien unterstützen Sicherheitsadministratoren dabei, sich auf die Verwaltung der einzelnen Gruppen von Antivireneinstellungen für verwaltete Geräte zu konzentrieren. Integrieren Sie Intune mit Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) als Mobile Threat Defense-Lösung, um die Antivirenrichtlinie zu verwenden.

- [Datenträgerverschlüsselung](../protect/endpoint-security-disk-encryption-policy.md): Die Datenträgerverschlüsselungsprofile für die Endpunktsicherheit konzentrieren sich ausschließlich auf die Einstellungen, die für eine integrierte Verschlüsselungsmethode für Geräte relevant sind, zum Beispiel FileVault oder BitLocker. Dieser Schwerpunkt vereinfacht Sicherheitsadministratoren die Verwaltung der Datenträgerverschlüsselungseinstellungen, ohne in einem Host mit nicht verknüpften Einstellungen navigieren zu müssen.

- [Firewall](../protect/endpoint-security-firewall-policy.md): Verwenden Sie die Firewallrichtlinie für Endpunktsicherheit in Intune, um eine integrierte Firewall für Geräte zu konfigurieren, die unter macOS und Windows 10 ausgeführt werden. 

- [Endpunkterkennung und -antwort](../protect/endpoint-security-edr-policy.md): Wenn Sie Microsoft Defender ATP mit Intune integrieren, verwenden Sie die Endpunktsicherheitsrichtlinien für die Endpunkterkennung und -antwort (EDR), um die EDR-Einstellungen zu verwalten und das Onboarding von Geräten für Microsoft Defender ATP durchzuführen.

- [Verringerung der Angriffsfläche](../protect/endpoint-security-asr-policy.md) Wenn Defender Antivirus auf Ihren Windows 10-Geräten verwendet wird, können Sie Endpunktsicherheitsrichtlinien von Intune für die Verringerung der Angriffsfläche verwenden, um diese Einstellungen für Ihre Geräte zu verwalten.

- [Kontoschutz](../protect/endpoint-security-account-protection-policy.md): Mit Kontoschutzrichtlinien können Sie die Identität und die Konten Ihrer Benutzer schützen. Die Kontoschutzrichtlinie konzentriert sich auf Einstellungen für Windows Hello and Credential Guard, die Teil der Windows-Identitäts- und Zugriffsverwaltung sind.

Die folgenden Abschnitte gelten für alle Endpunktsicherheitsrichtlinien.

## <a name="create-an-endpoint-security-policy"></a>Erstellen einer Endpunktsicherheitsrichtlinie

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Endpunktsicherheit**, dann den Typ der Richtlinie, die Sie konfigurieren möchten, und anschließend **Richtlinie erstellen** aus. Wählen Sie aus den folgenden Richtlinientypen aus:
   - Antivirus
   - Datenträgerverschlüsselung
   - Firewall
   - Endpunkterkennung und -antwort
   - Verringerung der Angriffsfläche
   - Kontoschutz

3. Geben Sie die folgenden Eigenschaften ein:
   - **Plattform**: Wählen Sie die Plattform aus, für die Sie die Richtlinie erstellen. Die verfügbaren Optionen hängen vom ausgewählten Richtlinientyp ab:
     - macOS
     - Windows 10 und höher
   - **Profil**: Wählen Sie aus den verfügbaren Profilen für die von Ihnen gewählte Plattform aus. Informationen zu den Profilen finden Sie im entsprechenden Abschnitt in diesem Artikel für den von Ihnen gewählten Richtlinientyp.

4. Wählen Sie **Erstellen** aus.

5. Geben Sie auf der Seite **Grundeinstellungen** einen Namen und eine Beschreibung für das Profil ein, und klicken Sie dann auf **Weiter**.

6. Erweitern Sie auf der Seite **Konfigurationseinstellungen** die einzelnen Gruppen von Einstellungen und konfigurieren Sie die Einstellungen, die Sie mit diesem Profil verwalten möchten.

   Wenn Sie fertig sind mit dem Konfigurieren der Einstellungen, klicken Sie auf **Weiter**.

7. Klicken Sie auf der Seite **Bereichstags** auf **Bereichstags auswählen**, um den Bereich *Tags auswählen* zu öffnen, in dem Sie dem Profil Bereichstags zuweisen.
  
   Wählen Sie **Weiter** aus, um den Vorgang fortzusetzen.

8. Wählen Sie auf der Seite **Zuweisungen** die Gruppen aus, die dieses Profil erhalten sollen. Weitere Informationen zum Zuweisen von Profilen finden Sie unter [Zuweisen von Benutzer- und Geräteprofilen](../configuration/device-profile-assign.md).

   Wählen Sie **Weiter** aus.

9. Klicken Sie, wenn Sie fertig sind, auf der Seite **Bewerten + erstellen** auf **Erstellen**. Das neue Profil wird in der Liste angezeigt, wenn Sie den Richtlinientyp für das Profil auswählen, das Sie erstellt haben.

## <a name="duplicate-a-policy"></a>Duplizieren einer Richtlinie

Endpunktsicherheitsrichtlinien unterstützen die Duplizierung, um eine Kopie der ursprünglichen Richtlinie zu erstellen. Beim Duplizieren einer Richtlinie ist ein Szenario dann sinnvoll, wenn Sie verschiedenen Gruppen ähnliche Richtlinien zuweisen müssen, aber nicht die gesamte Richtlinie manuell neu erstellen möchten. Stattdessen können Sie die ursprüngliche Richtlinie duplizieren und dann nur die Änderungen vornehmen, die für die neue Richtlinie erforderlich sind. Sie können z. B. nur eine bestimmte Einstellung und die Gruppe ändern, der die Richtlinie zugewiesen wird.

Wenn Sie ein Duplikat erstellen, müssen Sie der Kopie einen neuen Namen geben. Die Kopie wird mit denselben Einstellungskonfigurationen und Bereichstags wie das Original erstellt, aber ohne Zuweisungen. Zum Erstellen von Zuweisungen müssen Sie die neue Richtlinie später bearbeiten.  

Die folgenden Richtlinientypen unterstützen eine Duplizierung:

- Antivirus
- Datenträgerverschlüsselung
- Firewall
- Endpunkterkennung und -antwort
- Verringerung der Angriffsfläche
- Kontoschutz

Nach der Erstellung der neuen Richtlinie überprüfen und bearbeiten Sie die Richtlinie, um Änderungen an ihrer Konfiguration vorzunehmen.

### <a name="to-duplicate-a-policy"></a>So duplizieren Sie eine Richtlinie

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie die Richtlinie aus, das Sie kopieren möchten. Wählen Sie dann **Duplizieren** oder die Auslassungspunkte ( **...** ) rechts neben der Richtlinie und anschließend **Duplizieren** aus.
3. Geben Sie einen **neuen Namen** für die Richtlinie an, und wählen Sie dann **Speichern** aus.

### <a name="to-edit-a-policy"></a>So bearbeiten Sie eine Richtlinie

1. Wählen Sie neue Richtlinie aus, und wählen Sie dann **Eigenschaften** aus.
2. Wählen Sie „Einstellungen“ aus, um eine Liste der Konfigurationseinstellungen in der Richtlinie zu erweitern. Sie können die Einstellungen in dieser Ansicht nicht ändern, aber Sie können überprüfen, wie sie konfiguriert sind.
3. Um die Richtlinie zu ändern, wählen Sie **Bearbeiten** für jede Kategorie aus, in der Sie eine Änderung vornehmen möchten:
   - Grundlagen
   - Zuweisungen
   - Festlegen von Tags
   - Konfigurationseinstellungen
4. Nachdem Sie Änderungen vorgenommen haben, wählen Sie **Speichern** aus, um Ihre Änderungen zu speichern.  Sie müssen Änderungen an einer Kategorie speichern, bevor Sie Änderungen an weiteren Kategorien vornehmen können.

## <a name="manage-conflicts"></a>Verwalten von Konflikten

Viele der Geräteeinstellungen, die Sie mit Endgerätesicherheitsrichtlinien (Sicherheitsrichtlinien) verwalten können, können Sie über andere Richtlinientypen in Intune verwalten. Zu diesen anderen Richtlinientypen gehören die *Gerätekonfiguration* und *Sicherheitsbaselines*. Da Sie eine Einstellung mit mehreren verschiedenen Richtlinientypen oder mehreren Instanzen desselben Richtlinientyps verwalten können, sollten Sie Richtlinienkonflikte erkennen und lösen können, falls ein Gerät nicht den von Ihnen erwarteten Konfigurationen entspricht.

- Sicherheitsbaselines können einen nicht standardmäßigen Wert für eine Einstellung festlegen, um der empfohlenen Konfiguration zu entsprechen, auf die die Baseline ausgerichtet ist.
- Andere Richtlinientypen, einschließlich der Endpunktsicherheitsrichtlinien, legen standardmäßig den Wert *Nicht konfiguriert* fest. Für diese anderen Richtlinientypen müssen Sie die Einstellungen in der Richtlinie explizit konfigurieren.

Unabhängig von der Richtlinienmethode kann die Verwaltung derselben Einstellung auf demselben Gerät über mehrere Richtlinientypen oder über mehrere Instanzen desselben Richtlinientyps zu Konflikten führen, die vermieden werden sollten.

Verwenden Sie die Informationen unter den folgenden Links, um Konflikte zu identifizieren und zu beheben:

- [Richtlinien und Profile zur Problembehandlung in Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
- [Überwachen Ihrer Sicherheitsbaselines](../protect/security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## <a name="next-steps"></a>Nächste Schritte

[Verwalten der Endpunktsicherheit in Intune](../protect/endpoint-security.md)
