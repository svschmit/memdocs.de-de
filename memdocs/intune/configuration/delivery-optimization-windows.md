---
title: Übermittlungsoptimierungseinstellungen für Windows 10 in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Konfigurieren Sie, wie von Ihnen mit Intune verwaltete Windows 10-Geräte die Übermittlungsoptimierung verwenden sollen. Erstellen Sie in Intune ein Gerätekonfigurationsprofil zum Installieren von Updates über das Internet. Erfahren Sie auch, wie vorhandene Updateringe durch ein Übermittlungsoptimierungsprofil ersetzt werden.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: kerimh
ms.openlocfilehash: 4d491a3210229d5dd6c74ccaed7f44c4ae4eb83c
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990061"
---
# <a name="delivery-optimization-settings-in-microsoft-intune"></a>Übermittlungsoptimierungseinstellungen in Microsoft Intune

Verwenden Sie mithilfe von Intune die Übermittlungsoptimierungseinstellungen für Ihre Windows 10-Geräte, um die Auslastung der Bandbreite zu verringern, wenn diese Geräte Anwendungen und Updates herunterladen. Konfigurieren Sie die Übermittlungsoptimierung im Rahmen Ihrer Gerätekonfigurationsprofile.  

In diesem Artikel wird beschrieben, wie Sie Übermittlungsoptimierungseinstellungen als Teil eines Gerätekonfigurationsprofils konfigurieren können. Nachdem Sie ein Profil erstellt haben, sollten Sie dieses Ihren Windows 10-Geräten zuweisen oder für diese bereitstellen.

Eine Liste der von Intune unterstützten Übermittlungsoptimierungseinstellungen finden Sie unter [Übermittlungsoptimierungseinstellungen für Intune](delivery-optimization-settings.md).  

Weitere Informationen zur Übermittlungsoptimierung unter Windows 10 finden Sie in der Windows-Dokumentation unter [Delivery Optimization updates (Updates für die Übermittlungsoptimierung)](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization).  

## <a name="create-the-profile"></a>Erstellen des Profils

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.

3. Geben Sie die folgenden Eigenschaften ein:

   - **Plattform**: Wählen Sie **Windows 10 und höher** aus.
   - **Profil**: Wählen Sie **Übermittlungsoptimierung** aus.

4. Wählen Sie **Erstellen** aus.

5. Geben Sie in **Grundlagen** die folgenden Eigenschaften ein:

   - **Name:** Geben Sie einen aussagekräftigen Namen für das neue Profil ein.
   - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.

6. Wählen Sie **Weiter** aus.

7. Legen Sie auf der Seite **Konfigurationseinstellungen** fest, wie Updates und Apps heruntergeladen werden sollen. Weitere Informationen zu verfügbaren Einstellungen finden Sie unter [Übermittlungsoptimierungseinstellungen für Intune](delivery-optimization-settings.md).

   Wenn Sie fertig sind mit dem Konfigurieren der Einstellungen, klicken Sie auf **Weiter**.

8. Klicken Sie auf der Seite **Bereich (Markierungen)** auf **Bereichstags auswählen**, um den Bereich *Markierungen auswählen* zu öffnen, in dem Sie dem Profil Bereichstags zuweisen.
  
   Wählen Sie **Weiter** aus, um den Vorgang fortzusetzen.

9. Wählen Sie auf der Seite **Zuweisungen** die Gruppen aus, die dieses Profil erhalten sollen. Weitere Informationen zum Zuweisen von Profilen finden Sie unter [Zuweisen von Benutzer- und Geräteprofilen](../configuration/device-profile-assign.md).

   Wählen Sie **Weiter** aus.

10. Verwenden Sie auf der Seite **Anwendbarkeitsregeln** die Optionen **Regel**, **Eigenschaft**und **Wert**, um zu definieren, wie dieses Profil in zugewiesenen Gruppen angewendet wird.

11. Klicken Sie, wenn Sie fertig sind, auf der Seite **Bewerten + erstellen** auf **Erstellen**. Das Profil wird erstellt und in der Liste angezeigt.

Wenn die Geräte das nächste Mal einchecken, wird die Richtlinie angewendet.

## <a name="remove-delivery-optimization-from-windows-10-update-rings"></a>Entfernen der Übermittlungsoptimierung aus den Windows 10-Updateringen

Die Übermittlungsoptimierung war zuvor als Teil der Softwareupdateringe konfiguriert. Ab Februar 2019 werden die Einstellungen der Übermittlungsoptimierung jedoch als Teil eines Gerätekonfigurationsprofils für Übermittlungsoptimierungen konfiguriert, das zusätzliche Einstellungen enthält, die mehr Auswirkungen als nur die Softwareupdateübermittlung an Geräte haben. Wenn Sie die Übermittlungsoptimierungseinstellungen noch nicht aus Ihren Updateringen entfernt haben, sollten Sie das jetzt nachholen, indem Sie sie auf *Nicht konfiguriert* festlegen und anschließend ein Übermittlungsoptimierungsprofil verwenden, um den größeren Bereich verfügbarer Optionen zu verwalten.

1. Erstellen Sie ein Gerätekonfigurationsprofil für die Übermittlungsoptimierung:

    1. Wählen Sie im Microsoft Endpoint Manager Admin Center die Option **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.
    2. Geben Sie die folgenden Eigenschaften ein:

        - **Plattform**: Wählen Sie **Windows 10 und höher** aus.
        - **Profil**: Wählen Sie **Übermittlungsoptimierung** aus.

    3. Wählen Sie **Erstellen** aus.
    4. Geben Sie in **Grundlagen** die folgenden Eigenschaften ein:

        - **Name:** Geben Sie einen aussagekräftigen Namen für das neue Profil ein.
        - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.

    5. Wählen Sie **Weiter** aus.
    6. Legen Sie unter **Konfigurationseinstellungen** > **Downloadmodus** den gleichen Modus fest, der bereits vom vorhanden Softwareupdatering verwendet wird, wenn Sie die Einstellungen für Ihre Geräte *nicht* ändern möchten. Folgende Optionen sind verfügbar:

        - **Nicht konfiguriert**
        - **Nur HTTP, kein Peering**
        - **HTTP kombiniert mit Peering hinter derselben NAT**
        - **HTTP kombiniert mit eine Privatgruppe übergreifendem Peering**
        - **HTTP kombiniert mit Internetpeering**
        - **Einfacher Downloadmodus ohne Peering**
        - **Umgehungsmodus**

    7. Konfigurieren Sie [alle zusätzlichen Einstellungen](delivery-optimization-settings.md) die Sie verwalten möchten, und setzen Sie die Profilerstellung fort.

        Weisen Sie dieses neue Profil unter **Zuweisungen** den gleichen Geräten und Benutzern zu, die zu dem vorhandenen Softwareupdatering gehören. Weitere Informationen finden Sie unter [Zuweisen eines Profils](device-profile-assign.md).

2. Heben Sie die Konfiguration des vorhandenen Softwarerings auf:

    1. Wechseln Sie im Microsoft Endpoint Manager Admin Center zu **Softwareupdates** > Windows 10-Updateringe.
    2. Wählen Sie in der Liste Ihren Updatering aus.
    3. Legen Sie in den Einstellungen für den **Downloadmodus für Bereitstellungsoptimierung** auf **Nicht konfiguriert** fest.
    4. Wählen Sie zum Speichern der Änderungen **OK** > **Speichern** aus.

## <a name="next-steps"></a>Nächste Schritte

Nachdem Sie das [Profil zugewiesen haben](device-profile-assign.md), [überwachen Sie seinen Status](device-profile-monitor.md).

Zeigen Sie die [Übermittlungsoptimierungseinstellungen](delivery-optimization-settings.md) für Intune an.
