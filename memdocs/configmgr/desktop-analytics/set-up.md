---
title: Einrichten von Desktop Analytics
titleSuffix: Configuration Manager
description: Dieser Artikel enthält eine Anleitung zum Einrichten von und Onboarding in Desktop Analytics.
ms.date: 02/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 7ff8d453-f24d-4230-a116-585190a663fc
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 91a65f240a20e30af1610670c79182dee744e77b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696118"
---
# <a name="how-to-set-up-desktop-analytics"></a>Einrichten von Desktop Analytics

Melden Sie sich mit diesem Verfahren bei Desktop Analytics an, und konfigurieren Sie den Dienst in Ihrem Abonnement. Dieses Verfahren muss einmalig ausgeführt werden, um Desktop Analytics für Ihre Organisation einzurichten.  

> [!Important]  
> Informationen zu den allgemeinen Voraussetzungen für Desktop Analytics mit Configuration Manager finden Sie unter [Voraussetzungen](overview.md#prerequisites).  

## <a name="initial-onboarding"></a>Anfängliches Onboarding

1. Öffnen Sie das [Desktop Analytics-Portal](https://aka.ms/desktopanalytics) in der Microsoft 365-Geräteverwaltung als Benutzer mit der Rolle **Globaler Administrator**. Wählen Sie **Starten** aus. Sie können auch in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek** wechseln, den Knoten **Desktop Analytics-Wartung** auswählen und anschließend **Bereitstellungen planen** auswählen.

2. Lesen Sie auf der Seite **Servicevertrag annehmen** den Servicevertrag durch, und wählen Sie **Annehmen** aus.  

3. Überprüfen Sie auf der Seite **Ihr Abonnement bestätigen** die Liste der erforderlichen qualifizierenden Lizenzen. Legen Sie neben **Haben Sie eins der unterstützten oder höheren Abonnements?** die Einstellung auf **Ja** fest, und wählen Sie **Weiter** aus.  

4. Auf der Seite **Benutzern Zugriff erteilen**:

    - **Desktop Analytics das Verwalten von Verzeichnisrollen in Ihrem Auftrag gestatten**: Desktop Analytics weist **Workspace-Besitzern** automatisch die Rolle **Desktop Analytics-Administrator** zu. Wenn diese Gruppen bereits über **globale Administratorberechtigungen** verfügen, wird keine Änderung vorgenommen.

        Wenn Sie diese Option nicht auswählen, fügt Desktop Analytics dennoch Benutzer als Mitglieder der Sicherheitsgruppe hinzu. Ein **globaler Administrator** muss für die Benutzer die Rolle **Desktop Analytics-Administrator** manuell zuweisen.

        Weitere Informationen zum Zuweisen von Berechtigungen der Administratorrolle in Azure Active Directory und den **Desktop Analytics-Administratoren** zugewiesenen Berechtigungen finden Sie unter [Berechtigungen der Administratorrolle in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles).  

    - Desktop Analytics konfiguriert die Sicherheitsgruppe **Arbeitsbereichsbesitzer** in Azure Active Directory vorab für das Erstellen und Verwalten von Arbeitsbereichen und Bereitstellungsplänen.

        Wenn Sie der Gruppe einen Benutzer hinzufügen möchten, geben Sie seinen Namen oder seine E-Mail-Adresse im Bereich **Namen oder E-Mail-Adresse eingeben** ein. Wählen Sie anschließend **Weiter** aus.

5. Auf der Seite **Ihren Arbeitsbereich einrichten**:  

    > [!NOTE]  
    > Zum Abschließen dieses Schritts benötigt der Benutzer Berechtigungen des **Arbeitsbereichsbesitzers** und zusätzlichen Zugriff auf das Azure-Abonnement und die Ressourcengruppe. Weitere Informationen finden Sie unter [Voraussetzungen](overview.md#prerequisites).  

    - Wenn Sie einen vorhandenen Arbeitsbereich für Desktop Analytics verwenden möchten, wählen Sie ihn aus, und fahren Sie mit dem nächsten Schritt fort.  

        > [!TIP]  
        > Pro Azure AD-Mandant kann nur ein Desktop Analytics-Arbeitsbereich vorhanden sein. Geräte können Diagnosedaten nur an einen Arbeitsbereich senden.  

    - Wählen Sie zum Erstellen eines Arbeitsbereichs für Desktop Analytics die Option **Arbeitsbereich hinzufügen** aus.  

        1. Geben Sie in **Arbeitsbereichsname** einen global eindeutigen Namen ein.

        2. Wählen Sie die Dropdownliste **Das Azure-Abonnement für diesen Arbeitsbereich auswählen** aus, und wählen Sie das Azure-Abonnement für den Arbeitsbereich aus.  

        3. Wählen Sie für die Ressourcengruppe **Neu erstellen** oder **Vorhandene verwenden** aus.

        4. Wählen Sie in der Liste die **Region** aus, und wählen Sie anschließend **Hinzufügen** aus.  

6. Wählen Sie einen neuen oder vorhandenen Arbeitsbereich aus, und wählen Sie dann die Option **Als Desktop Analytics-Arbeitsbereich einrichten** aus.  Wählen Sie im Dialogfeld **Zugriff bestätigen und erteilen** die Option **Weiter** aus.  

7. Wählen Sie auf der neuen Browserregisterkarte ein Konto für die Anmeldung aus. Wählen Sie die Option **Zustimmung im Namen Ihrer Organisation** und anschließend **Zustimmen** aus.  

    > [!Note]  
    > Mit dieser Zustimmung wird der Anwendung MALogAnalyticsReader die Rolle „Log Analytics-Leser“ für den Arbeitsbereich zugewiesen. Diese Anwendungsrolle ist für Desktop Analytics erforderlich. Weitere Informationen erhalten Sie unter [Anwendungsrolle MALogAnalyticsReader](troubleshooting.md#bkmk_MALogAnalyticsReader).  

8. Wählen Sie auf der Seite **Ihren Arbeitsbereich einrichten** die Option **Weiter** aus.  

9. Wählen Sie auf der Seite **Letzte Schritte** die Option **Zu Desktop Analytics wechseln** aus.

Im Azure-Portal wird die **Startseite** von Desktop Analytics angezeigt.

## <a name="next-steps"></a>Nächste Schritte

Fahren Sie mit dem nächsten Artikel fort. Dort erfahren Sie, wie Sie Configuration Manager mit Desktop Analytics verbinden.
> [!div class="nextstepaction"]  
> [Herstellen einer Verbindung mit Configuration Manager](connect-configmgr.md)  
