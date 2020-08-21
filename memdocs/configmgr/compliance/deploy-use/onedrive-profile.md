---
title: OneDrive for Business-Profile
titleSuffix: Configuration Manager
description: Leiten Sie bekannte Windows-Ordner mithilfe eines OneDrive for Business-Profils in Configuration Manager an OneDrive for Business um.
ms.date: 04/11/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: e217699a-28b2-471a-b421-8fbd1d1fd638
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: ca7d81ba112c9eb79fb8bcfff96fb213b87b44c3
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694813"
---
# <a name="onedrive-for-business-profiles"></a>OneDrive for Business-Profile

Ab der Configuration Manager-Version 1902 können Sie OneDrive for Business-Profile erstellen, um bekannte Windows-Ordner nach OneDrive for Business zu verschieben. Zu diesen Ordnern gehören Desktop, Dokumente und Bilder. In jedem Profil können Sie Einstellungen zum Verschieben der bekannten Windows-Ordner angeben. Weitere Informationen zu OneDrive for Business finden Sie unter [Umleiten und Verschieben von bekannten Windows-Ordnern nach OneDrive](/onedrive/redirect-known-folders). <!--3556021-->

## <a name="prerequisites"></a>Voraussetzungen

- [Suchen Ihrer Microsoft 365-Mandanten-ID](/onedrive/find-your-office-365-tenant-id)  

- Stellen Sie die Clientversion 18.111.0603.0004 oder höher für die OneDrive-Synchronisierung bereit. Weitere Informationen finden Sie unter [Bereitstellen von OneDrive-Apps mit Configuration Manager](/onedrive/deploy-on-windows).  

## <a name="move-windows-known-folders-to-onedrive"></a><a name="bkmk_odfb"></a> Verschieben von bekannten Windows-Ordnern nach OneDrive
<!--3556021-->
Verwenden Sie Configuration Manager, um bekannte Windows-Ordner in OneDrive for Business zu verschieben. Zu diesen Ordnern gehören Desktop, Dokumente und Bilder. Stellen Sie diese Einstellungen für Windows 7-Clients bereit, bevor Sie eine Tasksequenz bereitstellen, um so Ihre Windows 10-Upgrades zu vereinfachen. 

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**, erweitern Sie **Konformitätseinstellungen**, und wählen Sie den Knoten **OneDrive for Business-Profile** aus.  

   ![Knoten „OneDrive for Business-Profile“](media/onedrive-for-business-profiles-node.png)
2. Klicken Sie im Menüband auf **OneDrive for Business-Profil erstellen**.  

3. Geben Sie einen Namen an, um diese Richtlinie zu identifizieren, und klicken Sie auf **Weiter**.  

4. Wählen Sie die Plattformen aus, die mit dem OneDrive for Business-Profil bereitgestellt werden sollen. Wenn Sie die gewünschten Plattformen ausgewählt haben, klicken Sie auf **Weiter**.

    ![Auswählen von Plattformen für das OneDrive for Business-Profil](media/onedrive-for-business-profile-select-platforms.png) 

5. Führen Sie auf der Seite **Einstellungen** die folgenden Schritte aus:

    1. Geben Sie Ihre Microsoft 365-Mandanten-ID an.  

    2. Wählen Sie eine der folgenden Optionen aus, um die bekannten Ordner in OneDrive zu verschieben:  

        - **Benutzer zum Verschieben bekannter Windows-Ordner nach OneDrive auffordern**: Bei dieser Option wird dem Benutzer ein Assistent zum Verschieben seiner Dateien angezeigt. Wenn Benutzer das Verschieben der Ordner später durchführen möchten oder ablehnen, werden sie in regelmäßigen Abständen von OneDrive daran erinnert.  

        - **Bekannte Windows-Ordner im Hintergrund nach OneDrive verschieben**: Wenn diese Richtlinie für das Gerät gilt, leitet der OneDrive-Client die bekannten Ordner automatisch an OneDrive um.  

            - **Nach dem Umleiten von Ordnern Benutzerbenachrichtigung anzeigen**: Wenn Sie diese Option aktivieren, benachrichtigt der OneDrive-Client den Benutzer, nachdem er dessen Ordner verschoben hat.  

    3. **Benutzer an der Umleitung bekannter Windows-Ordner zurück an ihren PC hindern**: Dadurch wird die Option in OneDrive for Business auf dem Client deaktiviert, mit der Benutzer diese Ordner zurück auf ihr Gerät verschieben können.  

       ![OneDrive for Business-Einstellungen zum Verschieben bekannter Ordner](media/onedrive-for-business-profile-move-folder-settings.png)

6. Schließen Sie den Assistenten ab, und stellen Sie anschließend die Richtlinie bereit.  


## <a name="deploy-the-onedrive-for-business-profile"></a>Bereitstellen des OneDrive for Business-Profils

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**, erweitern Sie **Konformitätseinstellungen**, und wählen Sie den Knoten **OneDrive for Business-Profile** aus.  


2. Wählen Sie das Profil und dann im Menüband **Bereitstellen** aus.

3. Geben Sie die folgenden Einstellungen für Ihre Bereitstellung an:

   1. **Sammlung**: Klicken Sie auf **Durchsuchen**, und wählen Sie die Sammlung aus, für die Sie das Profil bereitstellen möchten.  
   1. **Warnung generieren:**

      - **Wenn die Konformität geringer ist als**: Mindestprozentsatz der Clientkonformität, der eingehalten werden muss. Andernfalls wird eine Warnung generiert.
      -  **Datum und Uhrzeit**: Das Datum, an dem Warnungen zum ersten Mal anhand der Konformität des Profils generiert werden.
      - **System Center Operations Manager-Warnung generieren**: Eine Konformitätswarnung an System Center Operations Manager senden.
   1. **Zeitplan:**

      - **Einfacher Zeitplan**: Diese Einstellung verwendet standardmäßig einen einfachen Zeitplan, um die Konformitätsauswertung alle sieben Tage zu starten.
      - **Benutzerdefinierter Zeitplan**: Definieren Sie, wann die Konformitätsauswertung ausgeführt werden soll. Die Startzeit basiert auf der zum Zeitpunkt der Zeitplanerstellung geltenden lokalen Zeit des Computers, auf dem die Configuration Manager-Konsole ausgeführt wird. Alternativ können Sie UTC verwenden.
 
      ![Bereitstellen des OneDrive for Business-Profils](media/onedrive-for-business-deploy-profile.png)

4. Klicken Sie auf **OK**, um das OneDrive for Business-Profil bereitzustellen.


## <a name="next-steps"></a>Nächste Schritte

[Erstellen von Remoteverbindungsprofilen](create-remote-connection-profiles.md)