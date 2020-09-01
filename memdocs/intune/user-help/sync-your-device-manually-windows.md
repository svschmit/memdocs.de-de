---
title: Manuelles Synchronisieren Ihres Windows-Geräts | Microsoft-Dokumentation
description: ''
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/20/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: ''
searchScope:
- User help
ROBOTS: ''
ms.reviewer: priyar
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: ba2f9d2e3f9e89d37b1dc8361cd80451155a6869
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/25/2020
ms.locfileid: "88820679"
---
# <a name="sync-your-windows-device-manually"></a>Manuelles Synchronisieren des Windows-Geräts

Wenn die Geschwindigkeit der App-Installation nicht optimal ist, können Sie eine manuelle Gerätesynchronisierung initiieren. Bei manuellen Synchronisierungen wird erzwungen, dass Ihr Gerät eine Verbindung mit Intune herstellt, um die neuesten Updates und die aktuelle Kommunikation zu erhalten. Die Installationsgeschwindigkeit kann sich nach Abschluss der Gerätesynchronisierung erhöhen.

Intune unterstützt die manuelle Synchronisierung über die Unternehmensportal-App, die Desktoptaskleiste oder das Startmenü und über die Geräte-App „Einstellungen“. Die Funktionen der Unternehmensportal-App werden auf Windows 10-Geräten unterstützt, auf denen Creators Update (1703) oder höher ausgeführt wird. 

Über die Geräte-App „Einstellungen“ können alle Windows-Geräte synchronisiert werden, einschließlich:

* [Windows 10 Desktop](#windows-10-desktop)  
* [Microsoft HoloLens](#microsoft-hololens)   

## <a name="sync-directly-from-company-portal-app-for-windows"></a>Direktes Synchronisieren über die Unternehmensportal-App für Windows
Führen Sie die folgenden Schritte aus, um Windows 10-Geräte, auf denen das Creators Update (Version 1709) oder höher ausgeführt wird, manuell zu synchronisieren.

1. Öffnen Sie die Unternehmensportal-App auf Ihrem Gerät.

2. Wählen Sie **Einstellungen** > **Synchronisierung** aus.

    ![Screenshot der Startseite der Unternehmensportal-App, „Einstellungen“ hervorgehoben](./media/RS1_homePage_settings_04.png)  
    
    ![Screenshot der Seite „Einstellungen“ der Unternehmensportal-App, Schaltfläche „Synchronisierung“ hervorgehoben](./media/RS1_settingspage_sync05.png)  

## <a name="sync-from-device-taskbar-or-start-menu"></a>Synchronisieren über die Gerätetaskleiste oder das Startmenü   

Sie können über den Desktop Ihres Geräts auch außerhalb der App auf die Synchronisierungssteuerung zugreifen. Dies ist nützlich, wenn Sie die App direkt an Ihre Taskleiste oder das Startmenü angeheftet haben und eine schnelle Synchronisierung durchführen möchten.  

1. Suchen Sie das Symbol der Unternehmensportal-App auf Ihrer Taskleiste oder in Ihrem Startmenü.  
2. Klicken Sie mit der rechten Maustaste auf das Symbol der App, sodass deren Menü (das sogenannte Kontextmenü) angezeigt wird.  

    ![Screenshot der Windows-Taskleiste auf dem Desktop eines Geräts Das Symbol der Unternehmensportal-App wurde ausgewählt und zeigt ein Menü mit den Optionen „An Taskleiste anheften“, „Fenster schließen“ und „Dieses Gerät synchronisieren“ an.](./media/sync-device-from-start-menu-1807.png)  

3. Wählen Sie **Dieses Gerät synchronisieren** aus. Die Unternehmensportal-App wird geöffnet und zeigt die Seite **Einstellungen** an. Außerdem wird die Synchronisierung gestartet.  

## <a name="sync-from-settings-app"></a>Synchronisieren über die App „Einstellungen“ 
Führen Sie die folgenden Schritte aus, um Ihre Microsoft HoloLens- und Windows 10 Desktop-Geräte über die App „Einstellungen“ manuell zu synchronisieren.  

### <a name="windows-10-desktop"></a>Windows 10 Desktop
1. Wählen Sie auf Ihrem Gerät die Optionen **Start** > **Einstellungen** aus.

2. Wählen Sie **Konten** aus.

    ![Auswählen von Konten auf der Seite „Einstellungen“](./media/win10pc-sync-2-settings-accounts.png)  

3. Für Desktops gibt es mehrere Versionen von Windows 10. Vergleichen Sie Ihren Bildschirm mit den nachstehenden Screenshots, um zu bestimmen, welche Schritte Sie ausführen müssen. 

    * Wenn auf Ihrem Bildschirm die Option **Zugriff auf Geschäfts-, Schul- oder Unikonto** angezeigt wird, fahren Sie mit den Schritten unter [Zugriff auf Geschäfts-, Schul- oder Unikonto](#access-work-or-school-steps) fort.

    ![Option „Zugriff auf Geschäfts-, Schul- oder Unikonto“ in der App „Einstellungen“](./media/w10-enroll-rs1-connect-to-work-or-school.png)  

    * Wenn auf Ihrem Bildschirm die Option **Arbeitsplatzzugriff** angezeigt wird, fahren Sie mit den Schritten unter [Arbeitsplatzzugriff](#work-access-steps) fort.  

    ![Auswählen des Arbeitsplatzzugriffs als den Kontotyp](./media/win10pc-sync-3-work-access.png)

### <a name="microsoft-hololens"></a>Microsoft HoloLens  
Diese Anweisungen gelten für HoloLens-Geräte, auf denen das Windows 10 Anniversary Update (auch bekannt als RS1) ausgeführt wird.  

1. Öffnen Sie die App „Einstellungen“ auf Ihrem Gerät.  

2. Wählen Sie **Konten** > **Arbeitsplatzzugriff** aus.  

    ![Screenshot der HoloLens-App „Einstellungen“, Link „Konten“ hervorgehoben](./media/RS1_holoLens_SettingsRS1_Accounts_06.png)  

3. Wählen Sie Ihr verbundenes Konto > **Synchronisierung** aus.  

    ![Screenshot der HoloLens-App „Einstellungen“, Schaltfläche „Synchronisierung“ hervorgehoben](./media/RS1_holoLens_SyncRS1_Sync_08.png)   

#### <a name="access-work-or-school-steps"></a>Auszuführende Schritte bei Anzeige von „Zugriff auf Geschäfts-, Schul- oder Unikonto“  

1. Wählen Sie **Zugriff auf Geschäfts-, Schul- oder Unikonto** aus.

    ![Screenshot mit der Option „Zugriff auf Geschäfts-, Schul- oder Unikonto“](./media/w10-enroll-rs1-connect-to-work-or-school.png)  

2. Wählen Sie das Konto aus, neben dem ein Aktentaschensymbol angezeigt wird. Wenn dieses Konto nicht angezeigt wird, hat Ihr Unternehmen Ihre Einstellungen möglicherweise anders konfiguriert. Wählen Sie in diesem Fall das Konto aus, neben dem ein Microsoft-Logo angezeigt wird.

     ![Auswählen Ihres Kontonamens neben der Aktentasche oder dem Microsoft-Logo](./media/win10pc-rs1-sync-info-button.png)

3. Wählen Sie **Informationen** aus. 

4. Klicken Sie auf **Synchronisieren**. 

#### <a name="work-access-steps"></a>Auszuführende Schritte bei Anzeige von „Arbeitsplatzzugriff“

1. Wählen Sie **Arbeitsplatzzugriff** aus.

    ![Auswählen des Arbeitsplatzzugriffs als den Kontotyp](./media/win10pc-sync-3-work-access.png)

2. Wählen Sie unter **Bei Geräteverwaltung registrieren** den Namen Ihres Unternehmens aus.

    ![Auswählen des Firmennamens für die Geräteverwaltung aus](./media/win10pc-sync-4-tap-com-name.png)

3. Wählen Sie **Synchronisieren** aus. Die Schaltfläche bleibt bis zum Abschluss der Synchronisierung deaktiviert.

    ![Auswählen der Schaltfläche „Synchronisieren“](./media/win10pc-sync-5-tap-sync.png)  
    
## <a name="next-steps"></a>Nächste Schritte  

Benötigen Sie weitere Unterstützung? Kontaktieren Sie den Support Ihres Unternehmens. Die entsprechenden Kontaktinformationen finden Sie auf der [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980).
