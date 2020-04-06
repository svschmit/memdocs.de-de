---
title: Verwenden von rollenbasierter Zugriffssteuerung und Bereichstags für verteilte IT-Systeme in Intune | Microsoft-Dokumentation
description: Verwenden Sie Bereichsmarkierungen, um Konfigurationsprofile nach bestimmten Rollen zu filtern.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/06/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.technology: ''
ms.assetid: a21d3039-f2ed-4f43-b6fa-d00c071edbc4
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: eea973ec936ce41578754cb1a68d1b9128895b76
ms.sourcegitcommit: e2567b5beaf6c5bf45a2d493b8ac05d996774cac
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/27/2020
ms.locfileid: "80326685"
---
# <a name="use-role-based-access-control-rbac-and-scope-tags-for-distributed-it"></a>Verwenden der rollenbasierten Zugriffssteuerung und Bereichsmarkierungen für verteilte IT

Sie können die rollenbasierte Zugriffssteuerung und Bereichsmarkierungen verwenden, um sicherzustellen, dass die richtigen Administratoren über die korrekten Zugriffsrechte und Sichtbarkeit für die entsprechenden Intune-Objekte verfügen. Mit Rollen wird bestimmt, über welchen Zugriff Administratoren auf welche Objekte verfügen. Mit Bereichsmarkierungen wird bestimmt, welche Objekte Administratoren sehen können.

Angenommen, ein Administrator der Bezirksdirektion von Seattle hat die Rolle „Richtlinien- und Profil-Manager“. Sie möchten, dass dieser Administrator nur die Profile und Richtlinien sieht und verwalten kann, die für Geräte in Seattle gelten. Zum Einrichten dieses Zugriffs gehen Sie wie folgt vor:

1. Erstellen Sie eine Bereichsmarkierung namens „Seattle“.
2. Erstellen Sie eine Rollenzuweisung für die Rolle „Richtlinien- und Profil-Manager“ mit: 
    - Mitglieder (Gruppen): Eine Sicherheitsgruppe namens „Seattle-IT-Administratoren“. Alle Administratoren in dieser Gruppe verfügen über die Berechtigung zum Verwalten von Richtlinien und Profilen für Benutzer/Geräte im Bereich (Gruppen).
    - Mitglieder (Gruppen): Eine Sicherheitsgruppe namens „Seattle-Benutzer“. Alle Benutzer/Geräte in dieser Gruppe können über ihre eigenen Profile und Richtlinien verfügen, die von den Administratoren in Mitglieder (Gruppen) verwaltet werden. 
    - Bereich (Markierungen): Seattle. Die Administratoren in Mitglieder (Gruppen) können Intune-Objekte sehen, die ebenfalls über die Bereichsmarkierung „Seattle“ verfügen.
3. Fügen Sie die Seattle-Bereichsmarkierung Richtlinien und Profilen hinzu, auf die Administratoren in Mitglieder (Gruppen) zugreifen können sollen.
4. Fügen Sie die Seattle-Bereichsmarkierung zu Geräten hinzu, die für Administratoren in Mitglieder (Gruppen) sichtbar sein sollen. 

## <a name="default-scope-tag"></a>Standardbereichsmarkierung
Das Standardbereichstag wird automatisch allen ungetaggten Objekten hinzugefügt, die Bereichstags unterstützen.

Das Feature Standardbereichsmarkierung ähnelt dem Feature für Sicherheitsbereiche in Microsoft Endpoint Configuration Manager. 

## <a name="to-create-a-scope-tag"></a>So erstellen Sie eine Bereichsmarkierung

1. Navigieren Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) zu **Mandantenverwaltung** > **Rollen** > **Bereich (Markierungen)**  > **Erstellen**.
2. Geben Sie auf der Seite **Grundlagen** eine optionale **Beschreibung** sowie unter **Name** einen Wert an. Wählen Sie **Weiter** aus.
3. Wählen Sie auf der Seite **Zuweisungen** die Gruppen aus, die die Geräte enthalten, denen Sie das Bereichstag zuweisen möchten. Wählen Sie **Weiter** aus.
4. Klicken Sie auf der Seite **Review + create** (Prüfen + erstellen) auf **Erstellen**.

## <a name="to-assign-a-scope-tag-to-a-role"></a>So weisen Sie einer Rolle eine Bereichsmarkierung zu

1. Navigieren Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) zu **Mandantenverwaltung** > **Rollen** > **Alle Rollen**, wählen Sie eine Rolle aus, und klicken Sie auf **Zuweisungen** > **Zuweisen**.
2. Geben Sie auf der Seite **Grundlagen** eine **Beschreibung** sowie unter **Zuweisungsname** einen Wert an. Wählen Sie **Weiter** aus.
3. Klicken Sie auf der Seite **Admin Groups** (Verwaltungsgruppen) auf **Wählen Sie die Gruppen aus, die eingeschlossen werden sollen**, und wählen Sie die für diese Zuweisung gewünschten Gruppen aus. Die Benutzer in dieser Gruppe verfügen über die Berechtigungen, die Benutzer/Geräte unter „Bereich (Gruppen)“ zu verwalten. Wählen Sie **Weiter** aus.

    ![Screenshot: Benutzergruppen auswählen](./media/scope-tags/select-member-groups.png)

4. Wählen Sie auf der Seite **Scope Groups** (Bereichsgruppen) eine der folgenden Optionen für **Zuweisen zu** aus:
    - **Ausgewählte Gruppen:** Wählen Sie die Gruppen aus, die die Benutzer/Geräte enthalten, die Sie verwalten möchten. Alle Benutzer/Geräte in den ausgewählten Gruppen werden dann von den Benutzern in den Verwaltungsgruppen verwaltet.
    - **Alle Benutzer**: Alle Benutzer können von den Benutzern in den Verwaltungsgruppen verwaltet werden.
    - **Alle Geräte:** Alle Geräte können von den Benutzern in den Verwaltungsgruppen verwaltet werden.
    - **Alle Benutzer und Geräte:** Alle Benutzer und alle Geräte können von den Benutzern in den Verwaltungsgruppen verwaltet werden.

5. Klicken Sie auf **Weiter**.
6. Wählen Sie auf der Seite **Bereichstags** die Tags aus, die Sie zur Rolle hinzufügen möchten. Dadurch erhalten Benutzer, die Mitglieder einer Verwaltungsgruppe sind, Zugriff auf die Intune-Objekte, die dasselbe Bereichstag aufweisen. Sie können einer Rolle maximal 100 Bereichstags zuweisen.
7. Wählen Sie **Weiter** aus, um zur Seite **Review + create** (Prüfen + erstellen) zu wechseln, und klicken Sie dann auf **Erstellen**.

## <a name="assign-scope-tags-to-other-objects"></a>Zuweisen von Bereichstags zu anderen Objekten

Bei Objekten, die Bereichstags unterstützen, werden Bereichstags in der Regel unter **Eigenschaften** angezeigt. Für das Zuweisen eines Bereichstags zu einem Konfigurationsprofil führen Sie beispielsweise die folgenden Schritte aus:

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf **Geräte** > **Konfigurationsprofile**, und wählen Sie ein Profil aus.

2. Klicken Sie auf **Eigenschaften** > **Bereich (Markierungen)**  > **Bearbeiten** > **Bereichstags auswählen**, und wählen Sie die Tags aus, die Sie dem Profil hinzufügen möchten. Sie können einem Objekt maximal 100 Bereichstags zuweisen.
4. Klicken Sie auf **Auswählen** > **Review + save** (Prüfen + speichern).

## <a name="scope-tag-details"></a>Informationen zu Bereichsmarkierungen
Bei der Arbeit mit Bereichsmarkierungen sollten Sie Folgendes beachten: 

- Sie können einem Intune-Objekttyp Bereichstags zuweisen, wenn der Mandant mehrere Versionen desselben Objekts akzeptiert (z. B. als Rollenzuweisung oder als Apps).
  Die folgenden Intune-Objekte sind Ausnahmen zu dieser Regel und unterstützen derzeit keine Bereichstags:
    - Windows ESP-Profile
    - Gerätekategorien
    - Registrierungseinschränkungen
    - Bezeichner von Unternehmensgeräten
    - Autopilotgeräte
    - Konformitätsstandorte von Geräten
    - Jamf-Geräte
- VPP-Apps und E-Books, die dem VPP-Token zugeordnet sind, erben die Bereichstags, die dem VPP-Token zugewiesen sind.
- Für das Programm zur Geräteregistrierung (Device Enrollment Program, DEP) registrierte Geräte und DEP-Profile, die dem DEP-Token zugeordnet sind, erben die Bereichstags, die dem entsprechenden DEP-Token zugewiesen sind.
- Wenn ein Administrator ein Objekt in Intune erstellt, werden alle Bereichsmarkierungen, die diesem Administrator zugewiesen sind, automatisch dem neuen Objekt zugewiesen.
- Die rollenbasierte Zugriffssteuerung von Intune gilt nicht für Azure Active Directory-Rollen. Intune-Dienstadministratoren und globale Administratoren verfügen unabhängig von ihren Bereichsmarkierungen über vollständigen Administratorzugriff auf Intune.
- Wenn eine Rollenzuweisung über kein Bereichstag verfügt, werden dem IT-Administrator gemäß der Einstellungen für IT-Administratoren alle Objekte angezeigt. Administratoren ohne Bereichstags verfügen im Grunde über alle Bereichstags.
- Sie können nur Bereichsmarkierungen zuweisen, die in Ihren Rollenzuweisungen enthalten sind.
- Sie können nur Zielgruppen verwenden, die in Bereich (Gruppen) Ihrer Rollenzuweisung enthalten sind.
- Wenn Ihrer Rolle eine Bereichsmarkierung zugewiesen ist, können Sie nicht alle Bereichsmarkierungen eines Intune-Objekts löschen. Mindestens eine Bereichsmarkierung ist erforderlich.

## <a name="next-steps"></a>Nächste Schritte

Informieren Sie sich zum Verhalten von Bereichstags bei [mehreren Rollenzuweisungen](role-based-access-control.md#multiple-role-assignments).
Verwalten Sie Ihre [Rollen](role-based-access-control.md) und [Profile](../configuration/device-profile-assign.md).


