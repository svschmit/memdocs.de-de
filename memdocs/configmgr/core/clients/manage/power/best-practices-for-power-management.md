---
title: Empfehlungen für die Energieverwaltung
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über die Empfehlungen von Microsoft für die Energieverwaltung in Configuration Manager.
ms.date: 09/10/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 9f7142e1-c972-4384-853b-2da1568cb3e3
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 02cfb32f9187ca5a0ae0ad70ffcb4b85db8afb1b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696628"
---
# <a name="recommendations-for-power-management-in-configuration-manager"></a>Empfehlungen von Microsoft für die Energieverwaltung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie die folgenden Empfehlungen von Microsoft für die Energieverwaltung in Configuration Manager.  

## <a name="monitor-at-a-representative-time"></a>Überwachen zu einem repräsentativen Zeitpunkt

Die Überwachungsphase der Energieverwaltung bietet Ihnen die folgenden Informationen von Computern in Ihrem Unternehmen:

- Stromverbrauch
- Aktivität
- Energieverwaltungsfunktionen
- Umweltbelastung

Wählen Sie einen repräsentativen Zeitpunkt für die Überwachung der Geräte aus. Wenn Sie für die Überwachungsphase beispielsweise einen Feiertag wählen, kann kein realistischer Bericht zum Energieverbrauch erstellt werden.

## <a name="create-a-control-collection"></a>Erstellen einer Steuerelementsammlung

Erstellen Sie zwei Sammlungen von Computern, mit denen Sie überwachen, wie sich die Anwendung von Energiesparplänen auf Computer auswirkt. Die erste Sammlung muss die Mehrzahl der Computer enthalten, auf die Energieeinstellungen angewendet werden sollen. Die *Steuerelementsammlung* sollte die restlichen Computer enthalten. Wenden Sie den erforderlichen Energieverwaltungsplan auf die erste Sammlung an. Führen Sie dann Berichte aus, um die Auswirkungen der beiden Sammlungen zu vergleichen.  

## <a name="run-reports-before-you-apply-a-plan"></a>Ausführen von Berichten vor dem Anwenden eines Plans

Bevor Sie einen Energieverwaltungsplan auf eine Sammlung von Computern anwenden, führen Sie den Bericht **Energieeinstellungen** aus. Verwenden Sie diesen Bericht, um sich mit den Energieverwaltungseinstellungen vertraut zu machen, die auf den Computern in der Sammlung bereits konfiguriert sind. Wenn Sie neue Energieverwaltungseinstellungen auf Computer anwenden, ohne die bestehenden Einstellungen zu untersuchen, könnte dies zu einem Anstieg im Energieverbrauch führen.  

## <a name="exclude-servers"></a>Ausschließen von Servern

Die Energieverwaltung für Computer mit Windows-Server wird nicht unterstützt. Fügen Sie einer Sammlung Server hinzu, und schließen Sie diese aus der Energieverwaltung aus.  

> [!NOTE]
> Obwohl Configuration Manager die Energieverwaltung von Windows-Server nicht unterstützt, sammelt die Software weiterhin Energieverbrauchsdaten für Analysen und Berichte.

## <a name="exclude-other-computers"></a>Ausschließen anderer Computer

Wenn Sie über Computer verfügen, die Sie nicht mit der Energieverwaltung verwalten wollen, fügen Sie diese Computer einer Ausnahmesammlung hinzu.  

Sie sollten die folgenden Computertypen aus der Energieverwaltung ausschließen:

- Computer, die eingeschaltet bleiben müssen.  

- Computer, mit denen Benutzer eine Remoteverbindung herstellen müssen  

- Computer, auf denen die Energieverwaltung nicht verwendet werden kann  

- Computer mit der Standortsystemrolle "Verteilungspunkt"  

- Öffentliche Computer wie Kioskcomputer, Informationsanzeigen oder Überwachungskonsolen, bei denen Computer und Monitor stets eingeschaltet bleiben müssen  

Weitere Informationen finden Sie unter [Configuring power management (Konfigurieren der Energieverwaltung)](configuring-power-management.md).  

## <a name="apply-power-plans-to-a-test-collection"></a>Anwenden von Energiesparplänen auf eine Testsammlung

Testen Sie die Auswirkungen von Energieverwaltungsplänen stets zuerst an einer Testsammlung von Computern, bevor sie die Energieverwaltungspläne auf größere Computersammlungen anwenden.  

Wenn ein Computer aus der Energieverwaltung ausgeschlossen wird, werden sämtliche Energieeinstellungen auf ihre ursprünglichen Werte zurückgesetzt. Es können keine einzelnen Energieeinstellungen auf ihre ursprünglichen Werte zurückgesetzt werden.  

## <a name="apply-power-plan-settings-individually"></a>Anwenden von Energiesparplaneinstellungen auf einzelne Computer

Überwachen Sie die Auswirkungen jeder Energieeinstellung, bevor Sie die nächste anwenden. Dadurch wird sichergestellt, dass jede Einstellung die erforderliche Auswirkung hat. Weitere Informationen zu Einstellungen des Energiesparplans finden Sie unter [Verfügbare Einstellungen des Energieverwaltungsplans](create-and-apply-power-plans.md#BKMK_Plans).  

## <a name="regularly-monitor-computers-for-multiple-power-plans"></a>Regelmäßiges Überwachen von Computern auf mehrere Energiesparpläne

Die Energieverwaltung umfasst einen Bericht, der Computer anzeigt, auf die mehr als ein Energiesparplan angewendet wird: **Computer mit mehreren Energiesparplänen**.

Wenn ein Computer mehreren Sammlungen angehört, für die unterschiedliche Energiesparpläne verwendet werden, gelten die folgenden Verhaltensweisen:  

- **Energiesparplan**: Wenn auf einen Computer mehrere Werte für Energieeinstellungen angewendet werden, wird der am wenigsten restriktive Wert verwendet.  

- **Aktivierungszeit**: Wenn auf einen Desktopcomputer mehrere Aktivierungszeiten angewendet werden, wird die Zeit verwendet, die Mitternacht am nächsten liegt.  

Weitere Informationen finden Sie unter [Computer mit mehreren Energiesparplänen](monitor-and-plan-for-power-management.md#BKMK_Multiple).  

## <a name="save-or-export-power-management-information"></a>Speichern oder Exportieren von Energieverwaltungsinformationen

Wenn Sie während der Überwachungs- und Kompatibilitätsphase Berichte ausführen, speichern oder exportieren Sie die Ergebnisse. Bewahren Sie die Daten für einen späteren Vergleich auf, falls Configuration Manager die Daten später entfernt.  

Configuration Manager speichert in der Standortdatenbank die folgenden Informationen zur Energieverwaltung:

- Energieverwaltungsinformationen, die von täglichen Berichten verwendet werden: 31 Tage

- Energieverwaltungsinformationen, die von monatlichen Berichten verwendet werden: 13 Monate
