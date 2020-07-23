---
title: Konfigurieren des Clientstatus
titleSuffix: Configuration Manager
description: Hier finden Sie Informationen zu Clientstatuseinstellungen in Configuration Manager.
ms.date: 07/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a2275ba2-c83d-43e7-90ed-418963a707fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a352e53a672f7fb47416214884fe7adf0fb829cc
ms.sourcegitcommit: 488db8a6ab272f5d639525d70718145c63d0de8f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/14/2020
ms.locfileid: "86384909"
---
# <a name="how-to-configure-client-status-in-configuration-manager"></a>Konfigurieren des Clientstatus in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Bevor Sie Configuration Manager-Clients überwachen und Probleme lösen können, konfigurieren Sie die Einstellungen für den Clientstatus des Standorts. Diese Einstellungen geben die Parameter an, die der Standort verwendet, um den Client als inaktiv zu markieren. Es werden ebenfalls Optionen konfiguriert, um Sie zu warnen, wenn die Clientaktivität unter einen angegebenen Schwellenwert sinkt.

## <a name="configure-client-status"></a>Konfigurieren des Clientstatus

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**, und wählen Sie den Knoten **Clientstatus** aus. Klicken Sie auf der Registerkarte **Home** (Start) des Menübands auf die Gruppe **Clientstatus** und dann auf **Client-Statuseinstellungen**.

1. Konfigurieren Sie die folgenden Einstellungen:

    > [!NOTE]
    > Wenn ein Client die Einstellungen nicht erfüllt, wird er vom Standort als inaktiv markiert.

    - **Clientrichtlinienanforderungen innerhalb der folgenden Tage:** Geben Sie die Anzahl der Tage seit der letzten Richtlinienanforderung des Standorts durch einen Client an. Der Standardwert ist `7` Tage.

      Vergleichen Sie diesen Wert mit der Einstellung zum **Clientrichtlinien-Abrufintervall** in der Gruppe **Clientrichtlinie** der Clienteinstellungen. Die Standardeinstellung beträgt 60 Minuten. Anders ausgedrückt: Ein Client sollte der Standort stündlich nach Richtlinien abfragen. Wenn nach einer Woche keine Richtlinie angefordert wurde, wird der Client vom Standort als inaktiv markiert.

    - **Taktermittlung innerhalb der folgenden Tage:** Geben Sie die Anzahl der Tage seit der letzten Übermittlung eines Frequenzermittlungsdatensatzes an den Standort durch den Client an. Der Standardwert ist `7` Tage.

      Vergleichen Sie den Wert mit dem Zeitplan für die [Frequenzermittlungsmethode](../../servers/deploy/configure/about-discovery-methods.md). Standardmäßig führt der Standort die Frequenzermittlung einmal pro Woche aus.

    - **Hardwareinventur innerhalb der folgenden Tage:** Geben Sie die Anzahl der Tage seit der letzten Übermittlung eines Hardwareinventurdatensatzes an den Standort durch den Client an. Der Standardwert ist `7` Tage.

      Vergleichen Sie diesen Wert mit der Einstellung **Hardwareinventur-Zeitplan** in der Gruppe **Hardwareinventur** der Clienteinstellungen. Der Standardwert beträgt sieben Tage.

    - **Softwareinventur innerhalb der folgenden Tage:** Geben Sie die Anzahl der Tage seit der letzten Übermittlung eines Softwareinventurdatensatzes an den Standort durch den Client an. Der Standardwert ist `7` Tage.

      Vergleichen Sie diesen Wert mit der Einstellung **Softwareinventur- und Dateisammlung planen** in der Gruppe **Softwareinventur** der Clienteinstellungen. Der Standardwert beträgt sieben Tage.

    - **Statusmeldungen innerhalb der folgenden Tage:** Geben Sie die Anzahl der Tage seit der letzten Übermittlung von Statusmeldungen an den Standort durch den Client an. Der Standardwert ist `7` Tage. Der Client kann Statusmeldungen für unterschiedliche Aktivitäten senden, zum Beispiel das Ausführen einer Tasksequenz. Der Standort löscht alte Statusmeldungen als Teil des Wartungstasks **Veraltete Statusmeldungen löschen**.

1. Geben Sie den folgenden Wert an, um zu bestimmen, wie lange der Standort die Verlaufsdaten des Clientstatus speichert.

    - **Beibehalten des Clientstatusverlaufs für die folgende Anzahl von Tagen:** Standardmäßig speichert der Standort die Clientstatusinformationen für `31` Tage. Diese Einstellung hat keinen Einfluss auf das Verhalten des Clients oder des Standorts. Dies ähnelt einem Wartungstask für den Clientstatusverlauf.

## <a name="configure-the-schedule"></a>Konfigurieren des Zeitplans

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**, und wählen Sie den Knoten **Clientstatus** aus. Klicken Sie auf der Registerkarte **Home** (Start) des Menübands in der Gruppe **Clientstatus** auf **Aktualisierung des Clientstatus planen**.

1. Konfigurieren Sie das Intervall, in dem der Clientstatus aktualisiert werden soll.

    > [!NOTE]
    > Wenn Sie den Zeitplan für Clientstatusaktualisierungen ändern, treten die Änderungen erst mit der nächsten geplanten Clientstatusaktualisierung (nach dem zuvor konfigurierten Zeitplan) in Kraft.

## <a name="configure-alerts"></a>Konfigurieren von Warnungen

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Bestand und Konformität**, und wählen Sie den Knoten **Gerätesammlungen** aus.

1. Wählen Sie die Sammlung aus, für die Sie Warnungen konfigurieren möchten. Klicken Sie auf dem Menüband auf der Registerkarte **Start** in der Gruppe **Eigenschaften** auf **Eigenschaften**.

    > [!NOTE]
    > Für Benutzersammlungen können keine Warnungen konfiguriert werden.

1. Wechseln Sie zur Registerkarte **Warnungen**, und klicken Sie auf **Hinzufügen**.

   > [!TIP]
   > Sie können die Registerkarte **Warnungen** nur anzeigen, wenn Ihre Sicherheitsrolle über Berechtigungen für Warnungen verfügt.

    Wählen Sie die Warnungen aus, die der Standort für die Clientstatusschwellenwerte generieren soll, und klicken Sie auf **OK**.

1. Wählen Sie auf der Registerkarte **Warnungen** in der Liste **Bedingungen** die einzelnen Clientstatuswarnungen aus, und geben Sie für jede Warnung die folgenden Informationen an:

    - **Warnungsname:** Übernehmen Sie den Standardnamen, oder geben Sie einen neuen Namen für die Warnung ein.

    - **Warnungsschweregrad:** Wählen Sie die Warnungsstufe aus, die in der Configuration Manager-Konsole angezeigt wird.

    - **Warnung auslösen:** Geben Sie den Schwellenwert für die Warnung in Prozent an.

## <a name="automatic-remediation-exclusion"></a>Ausschluss aus der automatischen Korrektur

1. Öffnen Sie auf dem Clientcomputer, für den die automatische Wiederherstellung deaktiviert werden soll, den Registrierungs-Editor.

    > [!WARNING]
    > Durch unsachgemäße Verwendung des Registrierungs-Editors können schwerwiegende Fehler auftreten, die möglicherweise eine Neuinstallation von Windows erforderlich machen. Microsoft kann nicht garantieren, dass Probleme, die aufgrund unsachgemäßer Verwendung des Registrierungs-Editors entstehen, behoben werden können. Verwenden Sie diese Option auf eigene Gefahr.

1. Navigieren Sie im Registrierungsschlüssel zu **HKEY_LOCAL_MACHINE\Software\Microsoft\CCM\CcmEval**.

1. Ändern Sie den Wert für den Eintrag **NotifyOnly**.

    - `TRUE`: Der Client stellt gefundene Probleme nicht automatisch wieder her. Sie werden aber auch weiterhin im Arbeitsbereich **Überwachung** über Probleme bei diesem Client informiert.

    - `FALSE`: Dies ist die Standardeinstellung. Der Client stellt Probleme automatisch wieder her, wenn er sie findet, und Sie werden vom Standort über den Arbeitsbereich **Überwachung** benachrichtigt.

Wenn Sie Clients installieren, können Sie diese aus der automatischen Wiederherstellung mithilfe der Installationseigenschaft **NotifyOnly** ausschließen. Weitere Informationen finden Sie unter [Informationen zu Clientinstallationseigenschaften](about-client-installation-properties.md).

## <a name="next-steps"></a>Nächste Schritte

[Überwachen von Clients](../manage/monitor-clients.md)
