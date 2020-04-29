---
title: Verknüpfen von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät
titleSuffix: Configuration Manager
description: Verknüpfen Sie Benutzer und Geräte mit Affinität zwischen Benutzer und Gerät, und stellen Sie Apps automatisch auf Geräten bereit, die einem Benutzer zugeordnet sind.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 5b30b0d5-722d-4d4b-9ed7-5a43de315461
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2e74f969016d79254ceb8e8323b6e3914969ecc7
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689268"
---
# <a name="link-users-and-devices-with-user-device-affinity-in-configuration-manager"></a>Verknüpfen von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Durch die Affinität zwischen Benutzer und Gerät in Configuration Manager wird ein Benutzer einem oder mehreren Geräten zugeordnet. Dadurch ist es zum Bereitstellen einer Anwendung für den Benutzer nicht erforderlich, die Namen seiner Geräte zu kennen. Anstatt die Anwendung für jedes einzelne Gerät eines Benutzers bereitzustellen, stellen Sie sie für den Benutzer bereit. Mithilfe der Affinität zwischen Benutzer und Gerät wird dann automatisch sichergestellt, dass die Anwendung auf allen Geräten installiert wird, die dem Benutzer zugeordnet sind.  

Definieren Sie primäre Geräte, die Benutzer täglich für ihre Arbeit verwenden. Durch das Erstellen einer Affinität zwischen einem Benutzer und einem Gerät bieten sich zusätzliche Optionen für die Bereitstellung von Apps. Wenn ein Benutzer beispielsweise Microsoft Visio benötigt, können Sie es mithilfe einer Windows Installer-Bereitstellung auf dem primären Gerät des Benutzers installieren. Auf Geräten, bei denen es sich nicht um ein primäres Gerät handelt, können Sie Visio dagegen als virtuelle Anwendung bereitstellen. Sie können mithilfe der Affinität zwischen Benutzer und Gerät auch Software auf dem Gerät eines Benutzers vorab bereitstellen, während der Benutzer nicht angemeldet ist. Wenn sich der Benutzer dann anmeldet, ist die App bereits installiert und betriebsbereit.  

Sie müssen lediglich die Informationen zur Affinität zwischen Benutzer und Gerät für Computer verwalten. Die Affinitäten zwischen Benutzern und Geräten werden von Configuration Manager bei den von ihm angemeldeten mobilen Geräten automatisch verwaltet.  

## <a name="manually-set-up-user-device-affinity"></a>Manuelles Einrichten der Affinität zwischen Benutzer und Gerät  

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**, und wählen Sie den Knoten **Geräte** aus.  

1. Wählen Sie ein Gerät aus. Wählen Sie auf der Registerkarte **Start** des Menübands in der Gruppe **Gerät** die Option **Primäre Benutzer bearbeiten** aus.  

1. Wählen Sie im Dialogfeld **Primäre Benutzer bearbeiten** die Benutzer aus, die dem ausgewählten Gerät als primäre Benutzer hinzugefügt werden sollen. Wählen Sie dann **Hinzufügen** aus.  

    > [!NOTE]  
    > In der Liste **Primäre Benutzer** sind Benutzer, die bereits primäre Benutzer dieses Geräts sind, mit der jeweils zum Zuweisen der Beziehung zwischen Benutzer und Gerät verwendeten Methode aufgelistet.  

## <a name="set-up-primary-devices-for-a-user"></a>Einrichten primärer Geräte für einen Benutzer  

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**, und wählen Sie den Knoten **Benutzer** aus.  

1. Wählen Sie einen Benutzer aus. Wählen Sie auf der Registerkarte **Gerät** im Menüband die Option **Primäre Geräte bearbeiten** aus.  

1. Wählen Sie im Dialogfeld **Primäre Geräte bearbeiten** die Geräte aus, die dem ausgewählten Benutzer als primäre Geräte hinzugefügt werden sollen. Wählen Sie **Hinzufügen** aus.  

    > [!NOTE]  
    > In der Liste **Primäre Geräte** sind Geräte, die bereits als primäre Geräte für diesen Benutzer eingerichtet sind, mit der jeweils zum Zuweisen der Beziehung zwischen Benutzer und Gerät verwendeten Methode aufgelistet.  

## <a name="automatically-create-user-device-affinities-windows-pcs-only"></a>Automatisches Erstellen von Affinitäten zwischen Benutzern und Geräten (nur Windows-PCs)

Von Configuration Manager werden Daten zu Benutzeranmeldeereignissen aus dem Windows-Ereignisprotokoll ausgelesen. Aktivieren Sie zum automatischen Erstellen von Affinitäten zwischen Benutzer und Gerät die folgenden beiden Einstellungen in der lokalen Sicherheitsrichtlinie auf Clientcomputern, damit Anmeldeereignisse im Windows-Ereignisprotokoll gespeichert werden:  

- **Anmeldeversuche überwachen**  
- **Anmeldeereignisse überwachen**  

Sie können diese Einstellungen mithilfe von Windows-Gruppenrichtlinien konfigurieren.  

> [!IMPORTANT]  
> Wenn ein Fehler bewirkt, dass im Windows-Ereignisprotokoll eine große Anzahl von Einträgen generiert wird, kann dies dazu führen, dass ein neues Ereignisprotokoll erstellt wird. In diesem Fall sind vorhandene Anmeldeereignisse möglicherweise nicht für Configuration Manager verfügbar.  

### <a name="set-up-the-site-to-automatically-create-user-device-affinities"></a>Einrichten des Standorts für das automatische Erstellen von Affinitäten zwischen Benutzer und Gerät  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, und wählen Sie den Knoten **Clienteinstellungen** aus.  

1. Wählen Sie zum Ändern der Clientstandardeinstellungen **Clientstandardeinstellungen** aus. Wählen Sie auf der Registerkarte **Start** des Menübands in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.

    Um benutzerdefinierte Client-Agent-Einstellungen zu erstellen, wählen Sie auf der Registerkarte **Start** im Menüband in der Gruppe **Erstellen** die Option **Benutzerdefinierte Geräteclienteinstellungen erstellen** aus.

    > [!NOTE]  
    > Wenn Sie die Clientstandardeinstellungen ändern, werden sie auf allen Computern in der Hierarchie bereitgestellt. Weitere Informationen finden Sie unter [Konfigurieren von Clienteinstellungen](../../core/clients/deploy/configure-client-settings.md).  

1. Legen Sie in der Gruppe **Affinität zwischen Benutzer und Gerät** die folgenden Einstellungen fest:  

    - **Schwellenwert (Minuten) für Affinität zwischen Benutzer und Gerät**: Legen Sie die Anzahl von Minuten der Gerätenutzung fest, bevor die Site eine Affinität zwischen Benutzer und Gerät erstellt.  

    - **Schwellenwert für Affinität zwischen Benutzer und Gerät (Tage)** : Geben Sie die Anzahl von Tagen an, über die die Site den Schwellenwert für die Affinität zwischen Benutzer und Gerät misst.  

    - **Affinität zwischen Benutzer und Gerät automatisch aus Verwendungsdaten konfigurieren**: Wählen Sie **Wahr** (True) aus, wenn die Site automatisch Affinitäten zwischen Benutzer und Gerät erstellen soll. Wenn Sie **Falsch** auswählen, müssen Sie alle Zuweisungen der Affinität zwischen Benutzer und Gerät manuell genehmigen.  

    > [!TIP]  
    > Beispiel: Wenn Sie **Nutzungsschwellenwert (Minuten) für Affinität zwischen Benutzer und Gerät** auf **60** Minuten und **Nutzungsschwellenwert (Tage) für Affinität zwischen Benutzer und Gerät** auf **5** Tage festlegen, muss der Benutzer das Gerät über einen Zeitraum von 5 Tagen insgesamt mindestens 60 Minuten lang nutzen, damit eine Affinität zwischen Benutzer und Gerät automatisch erstellt wird.  

Nachdem von Configuration Manager eine Affinität zwischen Benutzer und Gerät automatisch erstellt wurde, werden die Schwellenwerte für die Affinität zwischen Benutzer und Gerät weiterhin überwacht. Wenn die Aktivität des Benutzers auf dem Gerät die festgelegten Schwellenwerte unterschreitet, wird die Affinität zwischen Benutzer und Gerät entfernt. Legen Sie **Schwellenwert für Affinität zwischen Benutzer und Gerät (Tage)** auf einen Wert von mindestens sieben Tagen fest. Diese Konfiguration vermeidet Situationen, in denen eine automatisch konfigurierte Affinität zwischen Benutzer und Gerät verloren gehen könnte, während der Benutzer z. B. am Wochenende nicht angemeldet ist.  


## <a name="import-user-device-affinities-from-a-file"></a>Importieren von Affinitäten zwischen Benutzer und Gerät aus einer Datei

Importieren Sie eine Datei, die Affinitäten zwischen Benutzern und Geräten enthält, um viele Beziehungen gleichzeitig zu erstellen. Stellen Sie sicher, dass die Zielgeräte bereits von der Site erkannt wurden und als Ressourcen in der Configuration Manager-Datenbank vorhanden sind.  

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**, und wählen Sie den Knoten **Benutzer** oder den Knoten **Geräte** aus.  

1. Wählen Sie auf der Registerkarte **Start** des Menübands in der Gruppe **Erstellen** die Option **Affinität zwischen Benutzer und Gerät importieren** aus.  

1. Geben Sie im Assistenten zum Importieren von Affinität zwischen Benutzer und Gerät auf der Seite **Zuordnung wählen** die folgenden Informationen an:  

    - **Dateiname**. Geben Sie eine CSV-Datei (kommagetrennte Werte) an, die eine Liste mit Benutzern und Geräten enthält, zwischen denen eine Affinität erstellt werden soll. In der Datei muss jedes Paar aus Benutzer und Gerät in einer separaten Zeile stehen, und die Werte müssen durch ein Komma getrennt sein. Verwenden Sie folgendes Format: `<domain>\<username>,<device NetBIOS name>`  

    - **Diese Datei enthält zu Referenzzwecken Spaltenüberschriften**. Wenn die CSV-Datei eine Kopfzeile in der obersten Zeile aufweist, wählen Sie diese Option aus. Die Kopfzeile wird während des Imports von der Site ignoriert.  

1. Wenn die zu importierende Datei mehr als zwei Elemente pro Zeile enthält, geben Sie mithilfe der Optionen **Spalte** und **Zuweisen** an, welche Spalten Benutzer und Geräte enthalten und welche Spalten beim Importieren ignoriert werden sollen.  

1. Schließen Sie den Assistenten ab.  


## <a name="let-users-create-their-own-device-affinities"></a>Benutzern ermöglichen, eigene Geräteaffinitäten zu erstellen

Einrichten eines Benutzers, um seine eigene Affinität zwischen Benutzer und Gerät im Softwarecenter zu erstellen.

### <a name="set-up-the-site-to-allow-user-created-user-device-affinity-requests"></a>Einrichten des Standorts, um von Benutzern erstellte Affinitätsanforderungen zwischen Benutzer und Gerät zu gestatten  

1  Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, und wählen Sie den Knoten **Clienteinstellungen** aus.  

1. Wählen Sie zum Ändern der Clientstandardeinstellungen **Clientstandardeinstellungen** aus. Wählen Sie auf der Registerkarte **Start** des Menübands in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.

    Um benutzerdefinierte Client-Agent-Einstellungen zu erstellen, wählen Sie auf der Registerkarte **Start** im Menüband in der Gruppe **Erstellen** die Option **Benutzerdefinierte Benutzerclienteinstellungen erstellen** aus.

    > [!NOTE]  
    > Wenn Sie die Clientstandardeinstellungen ändern, werden sie auf allen Computern in der Hierarchie bereitgestellt. Weitere Informationen finden Sie unter [Konfigurieren von Clienteinstellungen](../../core/clients/deploy/configure-client-settings.md).  

1. Aktivieren Sie in der Gruppe **Affinität zwischen Benutzer und Gerät** die Einstellung **Benutzer das Festlegen primärer Geräte gestatten**.  

### <a name="set-up-a-user-device-affinity-in-software-center"></a>Einrichten der Affinität zwischen Benutzer und Gerät im Softwarecenter

Ab Version 1902 verwenden Sie das Softwarecenter, um die Affinität festzulegen.

1. Wechseln Sie im Softwarecenter zur Registerkarte **Optionen**.

1. Wählen Sie im Abschnitt **Arbeitsinformationen** die Option **I regularly use this computer to do my work** (Ich nutze diesen Computer regelmäßig für meine Arbeit) aus.

### <a name="set-up-a-user-device-affinity-in-the-application-catalog"></a>Einrichten einer Affinität zwischen Benutzer und Gerät im Anwendungskatalog

> [!Important]
> Die Silverlight-Benutzeroberfläche für den Anwendungskatalog wird ab Current Branch-Version 1806 nicht unterstützt. Ab Version 1906 verwenden aktualisierte Clients automatisch den Verwaltungspunkt für Anwendungsbereitstellungen, die Benutzern zur Verfügung stehen. Zudem können Sie keine neuen Anwendungskatalogrollen installieren. Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910.  
>
> Weitere Informationen finden Sie in den folgenden Artikeln:
>
> - [Konfigurieren des Softwarecenters](../plan-design/plan-for-software-center.md#bkmk_userex)
> - [Entfernte und veraltete Features](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md)  

1. Wählen Sie im Anwendungskatalog **Eigene Systeme** aus.  

1. Wählen Sie die Option **Ich nutze diesen Computer regelmäßig für meine Arbeit** aus.  


## <a name="manage-user-device-affinity-requests-from-users"></a>Verwalten von Affinitätsanforderungen zwischen Benutzer und Gerät

Wenn Sie die Clienteinstellung **Affinität zwischen Benutzer und Gerät automatisch aus Verwendungsdaten konfigurieren** deaktivieren, müssen Sie alle Affinitätszuweisungen zwischen Benutzer und Gerät manuell genehmigen.  

### <a name="approve-or-reject-a-user-device-affinity-request"></a>Genehmigen oder Ablehnen einer Affinitätsanforderung zwischen Benutzer und Gerät  

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**.  

1. Wählen Sie die Benutzer- oder Gerätesammlung aus, für die Sie Affinitätsanforderungen verwalten möchten.  

1. Wählen Sie auf der Registerkarte **Start** des Menübands in der Gruppe **Sammlung** die Option **Affinitätsanforderungen verwalten** aus.  

1. Wählen Sie im Dialogfeld **Affinitätsanforderungen zwischen Benutzer und Gerät verwalten** eine Affinitätsanforderungen und anschließend **Genehmigen** oder **Ablehnen** aus.  


## <a name="next-steps"></a>Nächste Schritte

Sie können auch Microsoft Intune verwenden, um die primäre Verwendung eines registrierten Geräts zu ermitteln. Weitere Informationen finden Sie unter [Suchen des primären Benutzers eines Intune-Geräts](https://docs.microsoft.com/intune/find-primary-user) in der Intune-Dokumentation.
