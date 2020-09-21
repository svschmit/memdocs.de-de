---
title: Win32-App-Verwaltung in Microsoft Intune
titleSuffix: ''
description: Erfahren Sie, wie Sie Win32-Apps mit Microsoft Intune verwalten. Dieses Thema bietet eine Übersicht über die Intune-Funktionen zum Bereitstellen und Verwalten von Win32-Apps.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: efdc196b-38f3-4678-ae16-cdec4303f8d2
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: contperfq1
ms.collection: M365-identity-device-management
ms.openlocfilehash: db28653207d7bf4341d614aeecb769dcc145caaa
ms.sourcegitcommit: 4b8c317c71535c2d464f336c03b5bebdd2c6d4c9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/15/2020
ms.locfileid: "90083929"
---
# <a name="win32-app-management-in-microsoft-intune"></a>Win32-App-Verwaltung in Microsoft Intune

Microsoft Intune bietet Funktionen für die Verwaltung von Win32-Apps. Kunden mit Cloudverbindung können zwar Microsoft Endpoint Configuration Manager für die Verwaltung von Win32-Anwendungen verwenden. Allerdings stehen Kunden, die ausschließlich Intune verwenden, umfangreichere Verwaltungsfunktionen für ihre Win32-Branchen-Apps (LOB, Line-of-Business) zur Verfügung. Dieses Thema bietet eine Übersicht über die Intune-Features zur Verwaltung von Win32-Apps sowie weitere Informationen.

> [!NOTE]
> Für Windows-Anwendungen unterstützt dieses App-Verwaltungsfeature sowohl eine 32-Bit- als auch 64-Bit-Betriebssystemarchitektur.

> [!IMPORTANT]
> Bei der Bereitstellung von Win32-Apps sollten Sie ausschließlich die Methode der [Intune-Verwaltungserweiterung](../apps/intune-management-extension.md) nutzen. Dies gilt insbesondere dann, wenn Sie ein Win32-App-Installationsprogramm mit mehreren Dateien verwenden. Wenn Sie während der Autopilot-Registrierung die Installation von Win32- und branchenspezifischen Apps kombinieren, funktioniert die App-Installation möglicherweise nicht. Die Intune-Verwaltungserweiterung wird automatisch installiert, wenn ein PowerShell-Skript oder eine Win32-App dem Benutzer oder Gerät zugewiesen ist.

## <a name="prerequisites"></a>Voraussetzungen

Stellen Sie sicher, dass die folgenden Kriterien erfüllt sind, wenn Sie die Win32-App-Verwaltung verwenden wollen:

- Verwenden Sie Windows 10 Version 1607 oder höher (Enterprise-, Pro- und Education-Editionen).
- Geräte müssen Azure Active Directory (Azure AD) beigetreten und automatisch registriert sein. Die Intune-Verwaltungserweiterung unterstützt Geräte, die Azure AD und der hybriden Domäne beigetreten und per Gruppenrichtlinie registriert sind. 
  > [!NOTE]
  > Im Szenario der Registrierung per Gruppenrichtlinie verwenden Endbenutzer das lokale Benutzerkonto zum Einbinden ihrer Windows 10-Geräte in Azure AD. Benutzer müssen sich mit ihrem Azure AD-Benutzerkonto beim Gerät anmelden und sich bei Intune registrieren. Intune installiert die Intune-Verwaltungserweiterung auf dem Gerät, wenn ein PowerShell-Skript oder eine Win32-App auf einen Benutzer oder ein Gerät ausgerichtet sind.
- Die Größe der Windows-Anwendung ist auf 8 GB pro App begrenzt.

## <a name="prepare-the-win32-app-content-for-upload"></a>Vorbereiten des Inhalts der Win32-App für den Upload

Bevor Sie Microsoft Intune eine Win32-App hinzufügen können, müssen Sie die App mit dem Microsoft Win32 Content Prep Tool vorbereiten. Verwenden Sie das Microsoft Win32-Inhaltsvorbereitungstool zum Vorverarbeiten von klassischen Windows-Apps (Win32). Das Tool konvertiert Anwendungsinstallationsdateien in das *INTUNEWIN*-Format. Weitere Informationen und Schritte finden Sie unter [Vorbereiten des Inhalts der Win32-App für den Upload](apps-win32-prepare.md). 

## <a name="add-assign-and-monitor-a-win32-app"></a>Hinzufügen, Zuweisen und Überwachen einer Win32-App

Nachdem Sie mit dem Microsoft Win32 Content Prep Tool die [Win32-App für den Upload in Intune vorbereitet haben](apps-win32-prepare.md), können Sie die App zu Intune hinzufügen. Weitere Informationen und Schritte finden Sie unter [Hinzufügen, Zuweisen und Überwachen einer Win32-App in Microsoft Intune](apps-win32-add.md).

## <a name="delivery-optimization"></a>Übermittlungsoptimierung

Clients mit Windows 10, Version 1709 und höher laden Intune-Win32-App-Inhalte mithilfe einer Komponente zur Übermittlungsoptimierung auf den Windows 10-Client herunter. Die Übermittlungsoptimierung bietet Peer-zu-Peer-Funktionen, die standardmäßig aktiviert sind. 

Sie können den Übermittlungsoptimierungs-Agent so konfigurieren, dass Win32-App-Inhalte basierend auf der Zuweisung entweder im Hintergrund- oder im Vordergrundmodus heruntergeladen werden. Die Übermittlungsoptimierung kann per Gruppenrichtlinie und über die Intune-Gerätekonfiguration konfiguriert werden. Weitere Informationen finden Sie unter [Übermittlungsoptimierung für Windows 10](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization). 

> [!NOTE]
> Sie können auch einen Microsoft Connected Cache-Server auf Ihren Configuration Manager-Verteilungspunkten installieren, um Inhalte von Intune Win32-Apps zwischenzuspeichern. Weitere Informationen finden Sie unter [Microsoft Connected Cache in Configuration Manager](https://docs.microsoft.com/configmgr/core/plan-design/hierarchy/microsoft-connected-cache#bkmk_intune).

## <a name="install-required-and-available-apps-on-devices"></a>Installieren erforderlicher und verfügbarer Apps auf Geräten

Benutzer erhalten Windows-Benachrichtigungen zu erforderlichen und verfügbaren App-Installationen. Die folgende Abbildung zeigt eine exemplarische Benachrichtigung. Hierbei ist die App-Installation erst nach einem Neustart des Geräts abgeschlossen. 

![Screenshot der Windows-Benachrichtigungen zu einer App-Installation](./media/apps-win32-app-management/apps-win32-app-08.png)    

Die folgende Abbildung zeigt Benutzern an, dass am Gerät App-Änderungen vorgenommen werden.

![Screenshot mit einer Benachrichtigung an den Benutzer, dass Änderungen an der App vorgenommen werden](./media/apps-win32-app-management/apps-win32-app-09.png)    

In der Unternehmensportal-App werden Benutzern außerdem weitere Statusmeldungen zur App-Installation angezeigt. Bei Win32-Abhängigkeitsfeatures können folgende Szenarios auftreten:
- Die App wurde nicht installiert. Vom Administrator definierte Abhängigkeiten wurden nicht erfüllt.
- Die App wurde erfolgreich installiert, erfordert aber einen Neustart.
- Die App wird gerade installiert, es ist jedoch ein Neustart erforderlich, um den Vorgang fortzusetzen.

## <a name="set-win32-app-availability-and-notifications"></a>Festlegen der Verfügbarkeit und Benachrichtigungen von Win32-Apps
Sie können den Beginn und das Ende der Verfügbarkeit einer Win32-App konfigurieren. Zum Startzeitpunkt startet die Intune-Verwaltungserweiterung den Download der App-Inhalte und speichert sie für die erforderliche Absicht zwischen. Die App wird zu einem bestimmten Endzeitpunkt installiert. 

Für verfügbare Apps wird durch die Startzeit vorgegeben, wann die App im Unternehmensportal sichtbar ist. Inhalte werden heruntergeladen, wenn Benutzer die App vom Unternehmensportal anfordern. Sie können auch einen Kulanzzeitraum für den Neustart festlegen. 

> [!IMPORTANT]
> Der **Kulanzzeitraum für Geräteneustart** im Abschnitt **Zuweisung** ist nur verfügbar, wenn Sie im Abschnitt **Programm** das **Verhalten beim Geräteneustart** auf eine der folgenden Optionen festlegen:
> - **Verhalten auf Grundlage von Rückgabecodes bestimmen**
> - **Intune erzwingt einen verbindlichen Geräteneustart**

Legen Sie die App-Verfügbarkeit basierend auf einem Datum und einer Uhrzeit für eine erforderliche App fest, indem Sie die folgenden Schritte ausführen:

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Apps** > **Alle Apps** aus.
3. Wählen Sie in der Liste **Windows-App (Win32)** eine App aus. 
4. Wählen Sie im App-Bereich neben dem Abschnitt **Zuweisungen** den Eintrag **Eigenschaften** > **Bearbeiten** aus. Wählen Sie dann unterhalb des Zuweisungstyps **Erforderlich** die Option **Gruppe hinzufügen** aus. 
   
   Beachten Sie, dass die App-Verfügbarkeit basierend auf dem Zuweisungstyp festgelegt werden kann. Der **Zuweisungstyp** kann **Erforderlich**, **Für registrierte Geräte verfügbar** oder **Deinstalliert** sein.
5. Wählen Sie im Bereich **Gruppe auswählen** eine Gruppe aus, um anzugeben, welcher Gruppe von Benutzern die App zugewiesen wird. 

    > [!NOTE]
    > Optionen für den **Zuweisungstyp** beinhalten Folgendes:<br>
    > - **Erforderlich**: Sie können die Option **Diese App für alle Benutzer als erforderlich festlegen** und/oder die Option **Diese App auf allen Geräten als erforderlich festlegen** auswählen.<br>
    > - **Für registrierte Geräte verfügbar**: Sie können die Option **Diese App für alle Benutzer mit registrierten Geräten verfügbar machen** auswählen.<br>
    > - **Deinstallieren**: Sie können die Option **Diese App für alle Benutzer deinstallieren** und/oder die Option **Diese App für alle Geräte deinstallieren** auswählen.

6. Um die Optionen für die **Endbenutzerbenachrichtigung** zu ändern, wählen Sie **Alle Popupbenachrichtigungen anzeigen** aus.
7. Legen Sie im Bereich **Zuweisung bearbeiten** die **Endbenutzerbenachrichtigungen** auf **Alle Popupbenachrichtigungen anzeigen** fest. Beachten Sie, dass Sie **Endbenutzerbenachrichtigungen** auf **Alle Popupbenachrichtigungen anzeigen**, **Popupbenachrichtigungen für Computerneustarts anzeigen** oder **Alle Popupbenachrichtigungen ausblenden** festlegen können.
8. Legen Sie die **App-Verfügbarkeit** auf die Option **Bestimmtes Datum und bestimmte Uhrzeit** fest, und wählen Sie Datum und Uhrzeit aus. Dieses Datum und diese Uhrzeit geben an, wann die App auf das Benutzergerät heruntergeladen wird. 
9. Legen Sie den **Stichtag für App-Installation** auf die Option **Bestimmtes Datum und bestimmte Uhrzeit** fest, und wählen Sie Datum und Uhrzeit aus. Dieses Datum und diese Uhrzeit geben an, wann die App auf dem Benutzergerät installiert wird. Wenn für denselben Benutzer oder dasselbe Gerät mehr als eine Zuweisung durchgeführt wird, wird der Stichtag für die App-Installation basierend auf dem frühestmöglichen Zeitpunkt ausgewählt.

10. Klicken Sie neben der Option **Kulanzzeitraum neu starten** auf **Aktiviert**. Der Kulanzzeitraum für den Neustart beginnt, sobald die App-Installation auf dem Gerät abgeschlossen ist. Wenn diese Einstellung deaktiviert ist, kann das Gerät ohne Warnung neu gestartet werden. 

    Sie können die folgenden Optionen anpassen:
    
    - **Kulanzzeitraum für Geräteneustart (Minuten)** : Der Standardwert beträgt 1.440 Minuten (24 Stunden). Dieser Wert kann maximal 2 Wochen betragen.
    - **Wählen Sie aus, wann das Dialogfeld „Minuten bis zum Neustart“ vor der Durchführung des Neustarts angezeigt wird**: Der Standardwert beträgt 15 Minuten.
    - **Dem Benutzer das Aufschieben der Neustartbenachrichtigung gestatten**: Sie können **Ja** oder **Nein** auswählen.
        - **Zeitraum bis zur erneuten Erinnerung auswählen (Minuten)** : Der Standardwert beträgt 240 Minuten (4 Stunden). Der Wert für die erneute Erinnerung darf nicht größer als der Kulanzzeitraum für den Neustart sein.

11. Klicken Sie auf **Überprüfen + speichern**.

## <a name="notifications-for-win32-apps"></a>Benachrichtigungen für Win32-Apps 
Bei Bedarf können Sie die Anzeige von Benachrichtigungen an die Benutzer pro App-Zuweisung unterdrücken. Wählen Sie in Intune **Apps** > **Alle Apps** > *die App* > **Zuweisungen** > **Gruppen einschließen** aus. 

> [!NOTE]
> Win32-Apps, die über die Intune-Verwaltungserweiterung installiert wurden, werden auf Geräten mit aufgehobener Registrierung nicht deinstalliert. Administratoren können Zuweisungsausnahmen verwenden, um Win32-Apps für BYOD-Geräte (Bring Your Own Device) auszuschließen.

## <a name="next-steps"></a>Nächste Schritte

- Weitere Informationen zum Hinzufügen von Apps zu Intune finden Sie unter [Hinzufügen von Apps zu Microsoft Intune](apps-add.md).
