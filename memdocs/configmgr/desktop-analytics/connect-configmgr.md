---
title: Herstellen einer Verbindung mit Configuration Manager
titleSuffix: Configuration Manager
description: Dieser Artikel bietet eine Anleitung zum Verbinden von Configuration Manager mit Desktop Analytics.
ms.date: 03/12/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 7ed389c3-a9ab-48ce-a5eb-27d52ee4fb94
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 7015ab4c180ed56b00149ffbff99c9e5a8112e95
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88126000"
---
# <a name="how-to-connect-configuration-manager-with-desktop-analytics"></a>Herstellen einer Verbindung von Configuration Manager mit Desktop Analytics

Desktop Analytics ist eng in Configuration Manager integriert. Vergewissern Sie sich zunächst, ob der Standort auf dem neuesten Stand ist, sodass die neuesten Features unterstützt werden. Erstellen Sie anschließend die Desktop Analytics-Verbindung in Configuration Manager. Überwachen Sie schließlich die Integrität der Verbindung.

## <a name="update-the-site"></a><a name="bkmk_hotfix"></a> Aktualisieren des Standorts

Stellen Sie zuerst sicher, dass an Ihrem Configuration Manager-Standort mindestens Version 1902 ausgeführt wird. Weitere Informationen finden Sie unter [Installieren konsoleninterner Updates](../core/servers/manage/install-in-console-updates.md).

Sie müssen außerdem das Updaterollup (4500571), Version 1902 installieren, um die Integration mit Desktop Analytics zu unterstützen. Weitere Informationen zu diesem Update finden Sie unter [Updaterollup für den aktuellen Branch von Configuration Manager, Version 1902](https://support.microsoft.com/help/4500571).

1. Aktualisieren Sie den Standort mit dem Updaterollup für Version 1902. Weitere Informationen finden Sie unter [Installieren konsoleninterner Updates](../core/servers/manage/install-in-console-updates.md).

2. Aktualisieren der Clients Um diesen Prozess zu vereinfachen, sollten Sie automatische Clientupgrades in Betracht ziehen. Weitere Informationen finden Sie unter [Upgrade clients (Aktualisieren von Clients)](../core/clients/manage/upgrade/upgrade-clients.md#automatic-client-upgrade).

## <a name="connect-to-the-service"></a><a name="bkmk_connect"></a> Herstellen einer Verbindung mit dem Dienst

> [!TIP]
> Erstellen Sie vor dem Starten des Assistenten die in Schritt 8 erwähnte Zielsammlung, da Sie nach dem Start des Assistenten keine Auswahl außerhalb des Programms vornehmen können.

Führen Sie dieses Verfahren aus, um Configuration Manager mit Desktop Analytics zu verbinden und Geräteeinstellungen zu konfigurieren. Dieses Verfahren ist ein einmaliger Prozess, in dem Ihre Hierarchie an den Clouddienst angefügt wird.

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie den Eintrag **Clouddienste**, und wählen Sie anschließend den Knoten **Azure-Dienste** aus. Wählen Sie im Menüband **Azure-Dienste konfigurieren** aus.

    > [!TIP]
    > Stellen Sie die Verbindung mit dem Dienst direkt über den Knoten **Desktop Analytics-Wartung** her. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, und wählen Sie den Knoten **Desktop Analytics-Wartung** aus. Wählen Sie im Feld *Neu bei Desktop Analytics?* den zweiten Link aus, um *Configuration Manager mit dem Desktop Analytics-Dienst zu verbinden*.

2. Konfigurieren Sie auf der Seite **Azure-Dienste** des Assistenten für Azure-Dienste die folgenden Einstellungen:

    - Geben Sie einen **Namen** für das Objekt in Configuration Manager an.

    - Geben Sie eine optionale **Beschreibung** an, mit der Sie den Dienst identifizieren können.

    - Wählen Sie in der Liste der verfügbaren Dienste **Desktop Analytics** aus.

   Wählen Sie **Weiter** aus.

3. Wählen Sie auf der Seite **App** die geeignete **Azure-Umgebung** aus. Wählen Sie anschließend für die Web-App **Durchsuchen** aus.

4. Wenn Sie eine vorhandene App für diesen Dienst wiederverwenden möchten, wählen Sie sie in der Liste aus, und wählen Sie **OK**aus.

5. In den meisten Fällen können Sie mit diesem Assistenten eine App für die Desktop Analytics-Verbindung erstellen. Wählen Sie **Erstellen** aus.<!-- 3572123 -->

    > [!TIP]
    > Wenn Sie die App nicht mit dem Assistenten erstellen können, erstellen Sie die App in Azure AD, und importieren Sie sie dann in Configuration Manager. Weitere Informationen finden Sie unter [Erstellen und Importieren von Apps für Configuration Manager](troubleshooting.md#create-and-import-app-for-configuration-manager).

6. Konfigurieren Sie im Fenster **Serveranwendung erstellen** die folgenden Einstellungen:

    - **Anwendungsname**: Ein Anzeigename für die App in Azure AD.

    - **URL für Startseite**: Dieser Wert wird nicht von Configuration Manager verwendet, ist jedoch für Azure AD erforderlich. Der Standardwert beträgt `https://ConfigMgrService`.

    - **App-ID-URI**: Dieser Wert muss bei Ihrem Azure AD-Mandanten eindeutig sein. Es handelt sich dabei um das Zugriffstoken, mit dem der Konfigurations-Manager-Client Zugriff auf den Dienst anfordert. Der Standardwert beträgt `https://ConfigMgrService`.

    - **Gültigkeitsdauer des geheimen Schlüssels:** Wählen Sie entweder **1 Jahr** oder **2 Jahre** aus der Dropdownliste aus. Ein Jahr ist der Standardwert.

    Wählen Sie **Anmelden** aus. Nach einer erfolgreichen Authentifizierung in Azure, wird zu Referenzzwecken der **Name des Azure AD-Mandanten** auf der Seite angezeigt.

    > [!NOTE]
    > Führen Sie diesen Schritt als **globaler Administrator** aus. Diese Anmeldeinformationen werden nicht in Configuration Manager gespeichert. Für diese Persona sind keine Berechtigungen in Configuration Manager erforderlich. Zudem muss das Konto nicht mit dem Konto identisch sein, auf dem der Assistent für Azure-Dienste ausgeführt wird.

    Klicken Sie auf **OK**, um die Web-App in Azure AD zu erstellen und das Dialogfeld „Serveranwendung erstellen“ zu schließen. Wählen Sie im Dialogfeld „Server-App“ **OK** aus. Wählen Sie anschließend auf der Seite „App“ des Assistenten für Azure-Dienste **Weiter** aus.

7. Konfigurieren Sie auf der Seite **Diagnosedaten** die folgenden Einstellungen:

    - **Kommerzielle ID**: Dieser Wert wird automatisch mit der ID Ihrer Organisation aufgefüllt. Wenn dies nicht der Fall ist, vergewissern Sie sich vor dem Fortfahren, dass der Proxyserver so konfiguriert ist, dass alle erforderlichen [Endpunkte](enable-data-sharing.md#endpoints) zulässig sind. Sie können Ihre kommerzielle ID auch manuell aus dem [Desktop Analytics-Portal](monitor-connection-health.md#bkmk_ViewCommercialID) abrufen.

    - **Windows 10-Diagnosedatenebene**: Wählen Sie mindestens **Erforderlich** aus. Weitere Informationen finden Sie unter [Diagnosedatenebenen](enable-data-sharing.md#diagnostic-data-levels).

        > [!TIP]
        > In Configuration Manager Version 2002 und früher wurde dieser Wert mit **Basic** bezeichnet.<!-- 7363467 -->

    - **Gerätenamen in Diagnosedaten zulassen**: Wählen Sie **Aktivieren** aus.

        > [!NOTE]
        > Ab Windows 10, Version 1803, wird der Gerätename nicht mehr standardmäßig an Microsoft gesendet. Wenn Sie den Gerätenamen nicht senden, wird dieser in Desktop Analytics als „Unbekannt“ angezeigt. Dieses Verhalten kann das Identifizieren und Bewerten von Geräten erschweren.

   Wählen Sie **Weiter** aus. Auf der Seite **Verfügbare Funktionalität** werden die Desktop Analytics-Funktionen angezeigt, die mit den Einstellungen für Diagnosedaten von der vorherigen Seite verfügbar sind. Wählen Sie **Weiter** aus, um fortzufahren, oder wählen Sie **Zurück** aus, um Änderungen vorzunehmen.

    ![Beispielseite „Verfügbare Funktionalität“ im Assistenten für Azure-Dienste](media/available-functionality.png)

<a name="bkmk_Collections"></a>

8. Konfigurieren Sie auf der Seite **Sammlungen** die folgenden Einstellungen:

    - **Anzeigename:** Im Desktop Analytics-Portal wird die Configuration Manager-Verbindung mit diesem Namen angezeigt. Anhand dieses Namens können Sie zwischen verschiedenen Hierarchien unterscheiden und Sammlungen aus unterschiedlichen Hierarchien ermitteln. Verwenden Sie Begriffe, anhand derer Sie die Hierarchien in Ihrer Umgebung problemlos voneinander unterscheiden können, wie z.B.: *Testlab* oder *Produktion*.

    - **Zielsammlung**: Diese Sammlung enthält alle Geräte, die von Configuration Manager mit den Einstellungen für kommerzielle ID und Diagnosedaten konfiguriert werden. Dabei handelt es sich um sämtliche Geräte, die Configuration Manager mit dem Desktop Analytics-Dienst verbindet.

    - **Geräte in der Zielsammlung verwenden einen vom Benutzer authentifizierten Proxy für die ausgehende Kommunikation**: In der Standardeinstellung ist dieser Wert **Nein**. Sollte Ihre Umgebung etwas anderes erfordern, legen Sie ihn auf **Ja** fest.

    - **Wählen Sie bestimmte Sammlungen zur Synchronisierung mit Desktop Analytics aus**: Wählen Sie **Hinzufügen** aus, um weitere Sammlungen aus Ihrer Hierarchie **Zielsammlung** einzuschließen. Diese Sammlungen können im Desktop Analytics-Portal mit Bereitstellungsplänen gruppiert werden. Sie müssen Pilotsammlungen und Pilotausschlusssammlungen einschließen.  <!-- 4097528 -->

        > [!TIP]
        > Im Fenster „Sammlungen auswählen“ werden nur die Sammlungen angezeigt, die durch die **Zielsammlung** beschränkt werden.
        >
        > Im folgenden Beispiel wählen Sie CollectionA als Zielsammlung aus. Wenn Sie dann weitere Sammlungen hinzufügen, werden CollectionA, CollectionB und CollectionC angezeigt. CollectionD kann nicht hinzugefügt werden.
        >
        > - CollectionA: Beschränkt durch die Sammlung **Alle Systeme**
        >     - CollectionB: Beschränkt durch CollectionA
        >         - CollectionC: Beschränkt durch CollectionB
        > - CollectionD: Beschränkt durch die Sammlung **Alle Systeme**
        >
        > Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Clouddienste**, und klicken Sie auf den Knoten **Azure-Dienste**, um die Sammlungen zu verwalten, die sich im Desktop Analytics-Portal mit Bereitstellungsplänen gruppieren lassen. Wählen Sie den mit dem Azure-Dienst **Desktop Analytics** verknüpften Eintrag aus, und aktualisieren Sie Ihre Einstellungen auf der Seite **Desktop Analytics Collection** (Desktop Analytics-Sammlung).

        > [!IMPORTANT]
        > Diese Sammlungen werden auch nach Ändern ihrer Mitgliedschaft weiterhin synchronisiert. Ihre Zielsammlung verwendet beispielsweise eine Sammlung mit einer Windows 7-Mitgliedschaftsregel. Wird für diese Geräte ein Upgrade auf Windows 10 durchgeführt, und Configuration Manager wertet die Sammlungsmitgliedschaft aus, werden diese Geräte aus der Sammlung und Desktop Analytics entfernt.

9. Schließen Sie den Assistenten ab.

Configuration Manager erstellt eine Richtlinie für Einstellungen, um Geräte in der Zielsammlung zu konfigurieren. Diese Richtlinie enthält die Einstellungen für Diagnosedaten, um Geräten das Senden von Daten an Microsoft zu ermöglichen. In der Standardeinstellung wird die Richtlinie von den Clients stündlich aktualisiert. Nach dem Empfang der neuen Einstellungen kann es einige Stunden dauern, bis die Daten in Desktop Analytics verfügbar sind.

## <a name="monitor-connection-health"></a><a name="bkmk_monitor"></a> Überwachen der Verbindungsintegrität

Überwachen Sie die Konfiguration Ihrer Geräte für Desktop Analytics. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Softwarebibliothek**, erweitern Sie den Knoten **Desktop Analytics-Wartung**, und wählen Sie das Dashboard **Verbindungsintegrität** aus.

Weitere Informationen finden Sie unter [Überwachen der Verbindungsintegrität](monitor-connection-health.md).

Configuration Manager synchronisiert Ihre Sammlungen innerhalb von 60 Minuten nach dem Erstellen der Verbindung. Navigieren Sie im Desktop Analytics-Portal zu **Globaler Pilot**, und prüfen Sie Ihre Configuration Manager-Gerätesammlungen.

> [!NOTE]
> Die Configuration Manager-Verbindung mit Desktop Analytics basiert auf dem Dienstverbindungspunkt. Wenn Änderungen an dieser Standortsystemrolle vorgenommen werden, kann dies Auswirkungen auf die Synchronisierung mit dem Clouddienst haben. Weitere Informationen finden Sie unter [About the service connection point (Informationen zum Dienstverbindungspunkt)](../core/servers/deploy/configure/about-the-service-connection-point.md#bkmk_move).

## <a name="next-steps"></a>Nächste Schritte

Fahren Sie mit dem nächsten Artikel fort, und erfahren Sie, wie Sie Geräte für Desktop Analytics registrieren.
> [!div class="nextstepaction"]
> [Registrieren von Geräten](enroll-devices.md)
