---
title: Überwachen von Anwendungen in der Konsole
titleSuffix: Configuration Manager
description: Überwachen Sie die Bereitstellung von Software, einschließlich Updates, Konformitätseinstellungen und Anwendungen, mithilfe des Arbeitsbereichs „Überwachung“ in Configuration Manager.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 784c295c-b8b8-4202-ab9f-665908d49d6d
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 892a55ad4f3518794bef017f1d4e3a7a4de14e13
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689208"
---
# <a name="monitor-applications-from-the-configuration-manager-console"></a>Überwachen von Anwendungen aus der Configuration Manager-Konsole

*Gilt für: Configuration Manager (Current Branch)*


Sie können in Configuration Manager die Bereitstellung der gesamten Software überwachen, z. B. Softwareupdates, Konformitätseinstellungen, Anwendungen, Tasksequenzen sowie Pakete und Programme. Sie können Bereitstellungen über den Arbeitsbereich **Überwachung** in der Configuration Manager-Konsole oder mithilfe von Berichten überwachen.  

 Für Anwendungen in Configuration Manager wird eine zustandsbasierte Überwachung unterstützt, womit Sie den letzten Anwendungsbereitstellungszustand für Benutzer und Geräte nachverfolgen können. In diesen Zustandsmeldungen werden Informationen über einzelne Geräte angegeben. Wenn beispielsweise eine Anwendung für eine Sammlung von Benutzern bereitgestellt wird, können Sie den Kompatibilitätszustand und den Zweck der Bereitstellung in der Configuration Manager-Konsole anzeigen.  

## <a name="learn-about-compliance-states"></a>Weitere Informationen zu Konformitätszuständen
 Für einen Anwendungsbereitstellungszustand wird einer der folgenden Konformitätszustände angezeigt:  

-   **Erfolg** : Die Anwendung wurde erfolgreich bereitgestellt oder war bereits installiert.  

-   **In Bearbeitung** : Die Anwendungsbereitstellung wird ausgeführt.  

-   **Unbekannt** : Der Zustand der Anwendungsbereitstellung konnte nicht ermittelt werden. Dieser Zustand gilt nicht für Bereitstellungen mit dem Zweck **Verfügbar**. Dieser Zustand wird in der Regel angezeigt, wenn noch keine Zustandsmeldungen vom Client eingegangen sind.  

-   **Anforderungen nicht erfüllt** : Die Anwendung wurde nicht bereitgestellt, weil sie mit einer Abhängigkeit oder einer Anforderungsregel nicht kompatibel war oder weil das Zielbetriebssystem für die Bereitstellung ungültig war.  

-   **Fehler** : Bei der Bereitstellung der Anwendung ist ein Fehler aufgetreten.  

Sie können für jeden Konformitätszustand zusätzliche Informationen anzeigen, wie zum Beispiel Unterkategorien im Konformitätszustand oder die Anzahl der Benutzer und Geräte in dieser Kategorie. Der Konformitätszustand **Fehler** enthält beispielsweise die folgenden Unterkategorien:  

- Fehler beim Auswerten von Anforderungen  

- Inhaltsfehler  

- Installationsfehler  

  Wenn auf eine Anwendungsbereitstellung mehrere Kompatibilitätszustände zutreffen, wird der aggregierte Zustand mit der geringsten Kompatibilität angezeigt. Beispiel:  

  -   Wenn ein Benutzer sich auf zwei Geräten anmeldet und die Anwendung auf einem Gerät erfolgreich ist, auf dem anderen dagegen ein Fehler auftritt, wird für diesen Benutzer der Aggregatzustand **Fehler**für die Anwendungsbereitstellung angezeigt.  

  -   Wenn eine Anwendung für alle Benutzer bereitgestellt wird, die sich auf einem Computer anmelden, werden für diesen Computer mehrere Bereitstellungsergebnisse angezeigt. Wenn bei einer Bereitstellung ein Fehler auftritt, wird für den Computer der Aggregatbereitstellungszustand **Fehler**angezeigt.  

Der Bereitstellungszustand für Paket- und Programmbereitstellungen wird nicht aggregiert.  

 Mithilfe dieser Unterkategorien können Sie Probleme bei der Anwendungsbereitstellung schnell identifizieren. Sie können außerdem zusätzliche Informationen zu den Geräten anzeigen, die zu einer bestimmten Unterkategorie eines Konformitätszustands gehören.  

 Die Anwendungsverwaltung in Configuration Manager umfasst mehrere integrierte Berichte, mit deren Hilfe Daten zu Anwendungen und Bereitstellungen überwacht werden können. Die Berichte gehören zur Berichtkategorie **Softwareverteilung – Anwendungsüberwachung**.  

 Weitere Informationen zum Konfigurieren der Berichterstellung in Configuration Manager finden Sie unter [Einführung in die Berichterstellung](../../core/servers/manage/introduction-to-reporting.md).  

## <a name="monitor-the-state-of-an-application-in-the-configuration-manager-console"></a>Überwachen des Zustands einer Anwendung in der Configuration Manager-Konsole  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Überwachung** > **Bereitstellungen** aus.  

3.  Wenn Sie die Bereitstellungsdetails für jeden Konformitätszustand und die Geräte in diesem Zustand überprüfen möchten, wählen Sie eine Bereitstellung aus, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Status anzeigen**, um den Bereich **Bereitstellungsstatus** anzuzeigen. In diesem Bereich können Sie für alle Konformitätszustände anzeigen, welche Bestände den jeweiligen Zustand aufweisen. Wählen Sie einen Bestand aus, um detaillierte Informationen zu dessen Bereitstellungsstatus anzuzeigen.  

    > [!NOTE]  
    >  Im Bereich **Bereitstellungsstatus** können maximal 20.000 Elemente angezeigt werden. Verwenden Sie Configuration Manager-Berichte, um Anwendungsstatusdaten zu einer größeren Anzahl von Elementen anzuzeigen.  
    >   
    >  Der Status von Bereitstellungstypen wird im Bereich **Bereitstellungsstatus** aggregiert. Verwenden Sie den Bericht **Fehler in der Anwendungsinfrastruktur** in der Berichtskategorie **Softwareverteilung – Anwendungsüberwachung**, um ausführlichere Informationen zu Bereitstellungstypen anzuzeigen.  

4.  Wählen Sie eine Bereitstellung aus, und wählen Sie dann im Fenster **Ausgewählte Bereitstellungseigenschaften** die Registerkarte **Zusammenfassung** aus, um allgemeine Statusinformationen zu einer Anwendungsbereitstellung anzuzeigen.  

5.  Wählen Sie eine Bereitstellung aus, und wählen Sie dann im Fenster **Ausgewählte Bereitstellungseigenschaften** die Registerkarte **Bereitstellungstypen** aus, um Informationen zum Anwendungsbereitstellungstyp zu überprüfen.  

Bei den Informationen, die nach der Auswahl von **Status anzeigen** im Bereich **Bereitstellungsstatus** angezeigt werden, handelt es sich um Livedaten aus der Configuration Manager-Datenbank. Bei den Informationen, die auf den Registerkarten **Zusammenfassung** und **Bereitstellungstypen** angezeigt werden, handelt es sich um zusammengefasste Daten.

Wählen Sie **Zusammenfassung ausführen** aus, wenn die auf den Registerkarten **Zusammenfassung** und **Bereitstellungstypen** angezeigten Daten nicht mit den Daten im Bereich **Bereitstellungsstatus** übereinstimmen, um die Daten auf diesen Registerkarten zu aktualisieren. Gehen Sie folgendermaßen vor, um das Standardintervall für die Zusammenfassung von Anwendungsbereitstellungsdaten zu konfigurieren:  

1. Wählen Sie in der Configuration Manager-Konsole **Verwaltung** > **Standortkonfiguration** > **Standorte** aus.

2. Wählen Sie in der Liste **Standorte** den Standort aus, für den Sie das Zusammenfassungsintervall konfigurieren möchten, und wählen Sie dann auf der Registerkarte **Startseite** in der Gruppe **Einstellungen** **Statuszusammenfassungen** aus.

3. Wählen Sie im Dialogfeld **Statuszusammenfassungen** **Anwendungsbereitstellung – Zusammenfassung** aus, und wählen Sie dann **Bearbeiten** aus.  

4. Konfigurieren Sie im Dialogfeld **Anwendungsbereitstellung – Zusammenfassung** die erforderlichen Zusammenfassungsintervalle, und wählen Sie dann **OK** aus.  
