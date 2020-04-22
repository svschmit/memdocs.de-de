---
title: Konfigurieren des Clientstatus
titleSuffix: Configuration Manager
description: Hier finden Sie Informationen zu Clientstatuseinstellungen in Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a2275ba2-c83d-43e7-90ed-418963a707fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5bb77e1e9f55919a03368d549946ee4dd1cda58a
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81694218"
---
# <a name="how-to-configure-client-status-in-configuration-manager"></a>Konfigurieren des Clientstatus in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Sie müssen zunächst für Ihren Standort die Parameter einrichten, anhand derer Clients als inaktiv gekennzeichnet werden, und Benachrichtigungsoptionen für den Fall konfigurieren, dass ein angegebener Schwellenwert von einer Clientaktivität unterschritten wird, damit Sie den Configuration Manager-Clientstatus überwachen und aufgetretene Probleme beheben können. Sie können außerdem Computer daran hindern, Clientstatusprobleme automatisch zu beheben.  

##  <a name="to-configure-client-status"></a><a name="BKMK_1"></a> So konfigurieren Sie den Clientstatus  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Klicken Sie im Arbeitsbereich **Überwachung** auf **Clientstatus**und dann auf der Registerkarte **Startseite** in der Gruppe **Clientstatus** auf **Client-Statuseinstellungen**.  

3.  Geben Sie im Dialogfeld **Eigenschaften der Clientstatuseinstellungen** die folgenden Werte zum Bestimmen der Clientaktivität an:  

    > [!NOTE]  
    >  Wenn keine dieser Einstellungen zutrifft, wird der Client als inaktiv gekennzeichnet.  

    -   **Clientrichtlinienanforderungen innerhalb der folgenden Tage:** Geben Sie die Anzahl der Tage seit der letzten Richtlinienanforderung durch einen Client an. Der Standardwert ist **7** Tage.  

    -   **Taktermittlung innerhalb der folgenden Tage:** Geben Sie die Anzahl der Tage seit der letzten Übermittlung eines Frequenzermittlungsdatensatzes an die Standortdatenbank durch den Clientcomputer an. Der Standardwert ist **7** Tage.  

    -   **Hardwareinventur innerhalb der folgenden Tage:** Geben Sie die Anzahl der Tage seit der letzten Übermittlung eines Hardwareinventurdatensatzes an die Standortdatenbank durch den Clientcomputer an. Der Standardwert ist **7** Tage.  

    -   **Softwareinventur innerhalb der folgenden Tage:** Geben Sie die Anzahl der Tage seit der letzten Übermittlung eines Softwareinventurdatensatzes an die Standortdatenbank durch den Clientcomputer an. Der Standardwert ist **7** Tage.  

    -   **Statusmeldungen innerhalb der folgenden Tage:** Geben Sie die Anzahl der Tage seit der letzten Übermittlung von Statusmeldungen an die Standortdatenbank durch den Clientcomputer an. Der Standardwert ist **7** Tage.  

4.  Geben Sie im Dialogfeld **Eigenschaften der Clientstatuseinstellungen** die folgenden Werte an, um festzulegen, wie lange Verlaufsdaten für den Clientstatus beibehalten werden:  

    -   **Beibehalten des Clientstatusverlaufs für die folgende Anzahl von Tagen:** Geben Sie an, wie lange der Clientstatusverlauf in der Standortdatenbank gespeichert werden soll. Der Standardwert ist **31** Tage.  

5.  Klicken Sie auf **OK** , um die Eigenschaften zu speichern und das Dialogfeld **Eigenschaften der Clientstatuseinstellungen** zu schließen.  

##  <a name="to-configure-the-schedule-for-client-status"></a><a name="BKMK_Schedule"></a> So konfigurieren Sie den Zeitplan für den Clientstatus  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Klicken Sie im Arbeitsbereich **Überwachung** auf **Clientstatus**und dann auf der Registerkarte **Startseite** in der Gruppe **Clientstatus** auf **Aktualisierung des Clientstatus planen**.  

3.  Konfigurieren Sie im Dialogfeld **Aktualisierung des Clientstatus planen** das Intervall für die Aktualisierung des Clientstatus, und klicken Sie dann auf "OK".  

    > [!NOTE]  
    >  Wenn Sie den Zeitplan für Clientstatusaktualisierungen ändern, treten die Änderungen erst mit der nächsten geplanten Clientstatusaktualisierung (nach dem zuvor konfigurierten Zeitplan) in Kraft.  

##  <a name="to-configure-alerts-for-client-status"></a><a name="BKMK_2"></a> So konfigurieren Sie Warnungen für den Clientstatus  

1. Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2. Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Gerätesammlungen**.  

3. Wählen Sie in der Liste **Gerätesammlungen** die Sammlung aus, für die Sie Warnungen konfigurieren möchten, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

   > [!NOTE]  
   >  Es können keine Benachrichtigungen für Benutzersammlungen konfiguriert werden.  

4. Klicken Sie auf der Registerkarte **Warnungen** des Dialogfelds **Eigenschaften** von <em>&lt;Sammlungsname\></em> auf **Hinzufügen**.  

   > [!NOTE]  
   >  Die Registerkarte **Warnungen** wird nur angezeigt, wenn die Ihnen zugewiesene Sicherheitsrolle über Berechtigungen für Warnungen verfügt.  

5. Wählen Sie im Dialogfeld **Neue Sammlungswarnungen hinzufügen** die Warnungen aus, die beim Unterschreiten bestimmter Clientstatuswerte generiert werden sollen, und klicken Sie dann auf **OK**.  

6. Wählen Sie auf der Registerkarte **Warnungen** in der Liste **Bedingungen** die einzelnen Clientstatuswarnungen aus, und geben Sie für jede Warnung die folgenden Informationen an:  

   -   **Warnungsname** – Übernehmen Sie den Standardnamen, oder geben Sie einen neuen Namen für die Warnung ein.  

   -   **Warnungsschweregrad** – Wählen Sie in der Dropdownliste den Schweregrad aus, der in der Configuration Manager-Konsole angezeigt werden soll.  

   -   **Warnung auslösen** – Geben Sie den Schwellenwert für die Warnung in Prozent an.  

7. Klicken Sie auf **OK**, um das Dialogfeld **Eigenschaften** von <em>&lt;Sammlungsname\></em> zu schließen.  

##  <a name="to-exclude-computers-from-automatic-remediation"></a><a name="BKMK_3"></a> So schließen Sie Computer von der automatischen Wiederherstellung aus  

1. Öffnen Sie auf dem Clientcomputer, für den die automatische Wiederherstellung deaktiviert werden soll, den Registrierungs-Editor.  

   > [!WARNING]  
   >  Durch eine unsachgemäße Verwendung des Registrierungs-Editors können schwerwiegende Fehler auftreten, die möglicherweise eine Neuinstallation des Betriebssystems erforderlich machen. Microsoft kann nicht garantieren, dass Sie Probleme, die durch die fehlerhafte Verwendung des Registrierungs-Editors entstehen, beheben können. Die Verwendung des Registrierungs-Editors erfolgt auf Ihr eigenes Risiko.  

2. Wechseln Sie zu **HKEY_LOCAL_MACHINE\Software\Microsoft\CCM\CcmEval\NotifyOnly**.  

3. Geben Sie einen der folgenden Werte für diesen Registrierungsschlüssel an:  

   -   **True** – Auf dem Clientcomputer aufgetretene Probleme werden nicht automatisch behoben. Sie werden aber auch weiterhin im Arbeitsbereich **Überwachung** über Probleme bei diesem Client informiert.  

   -   **False** – Auf dem Clientcomputer aufgetretene Probleme werden automatisch behoben, und Sie werden im Arbeitsbereich **Überwachung** darüber informiert. Dies ist die Standardeinstellung.  

4. Schließen Sie den Registrierungs-Editor.  

   Sie können Clients auch mithilfe der CCMSetup-Installationseigenschaft **NotifyOnly** installieren, um sie von der automatischen Wiederherstellung auszuschließen. Weitere Informationen zu dieser Clientinstallationseigenschaft finden Sie unter [Informationen zu Parametern und Eigenschaften für die Clientinstallation](../../../core/clients/deploy/about-client-installation-properties.md).  
