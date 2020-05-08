---
title: Übermittlungsoptimierungseinstellungen für Windows 10 in Microsoft Intune – Azure | Microsoft-Dokumentation
description: Konfigurieren Sie, wie von Ihnen mit Intune verwaltete Windows 10-Geräte die Übermittlungsoptimierung verwenden sollen. Erstellen Sie in Intune ein Gerätekonfigurationsprofil zum Installieren von Updates über das Internet. Erfahren Sie auch, wie vorhandene Updateringe mit einem Übermittlungsoptimierungsprofil ersetzt werden.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/28/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: kerimh
ms.openlocfilehash: c37563dee40d776d352dec4e0b8ef11b1dc8f67b
ms.sourcegitcommit: 7b3eed763b394075766ea080968889a8538bfe56
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/29/2020
ms.locfileid: "82506538"
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
   - **Profiltyp**: Wählen Sie **Übermittlungsoptimierung** aus.

4. Wählen Sie **Erstellen** aus.

5. Geben Sie auf der Seite **Grundeinstellungen** einen Namen und eine Beschreibung für das Profil ein, und klicken Sie dann auf **Weiter**.

6. Legen Sie auf der Seite **Konfigurationseinstellungen** fest, wie Updates und Apps heruntergeladen werden sollen. Weitere Informationen zu verfügbaren Einstellungen finden Sie unter [Delivery optimization settings for Intune (Übermittlungsoptimierungseinstellungen für Intune)](delivery-optimization-settings.md).

   Wenn Sie fertig sind mit dem Konfigurieren der Einstellungen, klicken Sie auf **Weiter**.

7. Klicken Sie auf der Seite **Bereich (Markierungen)** auf **Bereichstags auswählen**, um den Bereich *Markierungen auswählen* zu öffnen, in dem Sie dem Profil Bereichstags zuweisen.
  
   Wählen Sie **Weiter** aus, um den Vorgang fortzusetzen.

8. Wählen Sie auf der Seite **Zuweisungen** die Gruppen aus, die dieses Profil erhalten sollen. Weitere Informationen zum Zuweisen von Profilen finden Sie unter [Zuweisen von Benutzer- und Geräteprofilen](../configuration/device-profile-assign.md).

   Wählen Sie **Weiter** aus.

9. Verwenden Sie auf der Seite **Anwendbarkeitsregeln** die Optionen **Regel**, **Eigenschaft**und **Wert**, um zu definieren, wie dieses Profil in zugewiesenen Gruppen angewendet wird.

10. Klicken Sie, wenn Sie fertig sind, auf der Seite **Bewerten + erstellen** auf **Erstellen**. Das Profil wird erstellt und in der Liste angezeigt. [Weisen](device-profile-assign.md) Sie als Nächstes das Profil zu, und [überwachen Sie dessen Status](device-profile-monitor.md).

## <a name="remove-delivery-optimization-from-windows-10-update-rings"></a>Entfernen der Übermittlungsoptimierung aus den Windows 10-Updateringen

Die Übermittlungsoptimierung war zuvor als Teil der Softwareupdateringe konfiguriert. Ab Februar 2019 werden die Einstellungen der Übermittlungsoptimierung jedoch als Teil eines Gerätekonfigurationsprofils für Übermittlungsoptimierungen konfiguriert, das zusätzliche Einstellungen enthält, die mehr Auswirkungen als nur die Softwareupdateübermittlung an Geräte haben. Wenn Sie die Übermittlungsoptimierungseinstellungen noch nicht aus Ihren Updateringen entfernt haben, sollten Sie das jetzt nachholen, indem Sie sie auf *Nicht konfiguriert* festlegen und anschließend ein Übermittlungsoptimierungsprofil verwenden, um den größeren Bereich verfügbarer Optionen zu verwalten.

1. Erstellen Sie ein Gerätekonfigurationsprofil für die Übermittlungsoptimierung:

    1. Wählen Sie im Microsoft Endpoint Manager Admin Center die Option **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.
    2. Geben Sie die folgenden Eigenschaften ein:

        - **Name:** Geben Sie einen aussagekräftigen Namen für das neue Profil ein.
        - **Beschreibung:** Geben Sie eine Beschreibung für das Profil ein. Diese Einstellung ist optional, wird jedoch empfohlen.
        - **Plattform**: Wählen Sie **Windows 10 und höher** aus.
        - **Profiltyp**: Wählen Sie **Übermittlungsoptimierung** aus.
        - **Einstellungen**: Legen Sie für den **Downloadmodus für Übermittlungsoptimierung** den Modus fest, der bereits vom vorhanden Softwareupdatering verwendet wird, wenn Sie die Einstellungen für Ihre Geräte nicht ändern möchten. Folgende Optionen sind verfügbar:
            - **Nicht konfiguriert**
            - **Nur HTTP, kein Peering**
            - **HTTP kombiniert mit Peering hinter derselben NAT**
            - **HTTP kombiniert mit eine Privatgruppe übergreifendem Peering**
            - **HTTP kombiniert mit Internetpeering**
            - **Einfacher Downloadmodus ohne Peering**
            - **Umgehungsmodus**
    3. Konfigurieren Sie jegliche zusätzlichen Einstellungen, die Sie möglicherweise verwalten möchten.

2. Weisen Sie dieses neue Profil den gleichen Geräten und Benutzern zu, die zu dem vorhandenen Softwareupdatering gehören. In [Zuweisen von Benutzer- und Geräteprofilen in Microsoft Intune](device-profile-assign.md) sind die Schritte aufgeführt.

3. Heben Sie die Konfiguration des vorhandenen Softwarerings auf:
    1. Wechseln Sie im Microsoft Endpoint Manager Admin Center zu **Softwareupdates** > Windows 10-Updateringe.
    2. Wählen Sie in der Liste Ihren Updatering aus.
    3. Legen Sie in den Einstellungen für den **Downloadmodus für Bereitstellungsoptimierung** **Nicht konfiguriert** fest.
    4. Wählen Sie zum Speichern der Änderungen **OK** > **Speichern** aus.

## <a name="next-steps"></a>Nächste Schritte

[Weisen Sie das Profil zu](device-profile-assign.md), und [überwachen Sie seinen Status](device-profile-monitor.md).  
Sehen Sie sich die [Übermittlungsoptimierungseinstellungen](delivery-optimization-settings.md) für Intune an.
