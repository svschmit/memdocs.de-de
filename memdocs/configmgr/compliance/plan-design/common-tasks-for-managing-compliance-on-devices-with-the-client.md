---
title: Allgemeine Aufgaben der Konformitätsverwaltung
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über Configuration Manager-Konformitätseinstellungen, indem Sie einige gängige Szenarios durcharbeiten.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 4e345791-74db-41ad-b472-024ce6521daf
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 5920229331bca8d2a47b0bf1ab663530ef63c51e
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240659"
---
# <a name="common-tasks-for-managing-compliance-on-devices-with-the-configuration-manager-client"></a>Allgemeine Aufgaben zur Verwaltung von Konformität auf Geräten mit dem Configuration Manager-Client

*Gilt für: Configuration Manager (Current Branch)*

Dieser Artikel bietet eine Einführung in die Verwendung der Konformitätseinstellungen von Configuration Manager, indem er Sie durch einige häufige Szenarien führt, die bei Ihnen auftreten könnten.  

 Wenn Sie bereits mit den Kompatibilitätseinstellungen vertraut sind, finden Sie ausführliche Informationen zu allen verwendbaren Features unter [Konfigurationselemente für Geräte, die mit dem Configuration Manager-Client verwaltet werden](../../compliance/deploy-use/create-configuration-items.md).  

 Bevor Sie beginnen, lesen Sie [Erste Schritte mit Konformitätseinstellungen](../../compliance/get-started/get-started-with-compliance-settings.md), um einige Grundlagen zu Konformitätseinstellungen zu erhalten. Informationen zu den notwendigen Voraussetzungen finden Sie unter [Planen und Konfigurieren von Konformitätseinstellungen](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md).  

## <a name="general-information-for-each-scenario"></a>Allgemeine Informationen für jedes Szenario  
 In jedem Szenario erstellen Sie ein Konfigurationselement, das eine bestimmte Aufgabe ausführt. Führen Sie die folgenden Schritte aus, um den Assistenten zum Erstellen von Konfigurationselementen zu öffnen und zu starten:  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Assets und Konformität** > **Konformitätseinstellungen** > **Konfigurationselemente**.  

1.  Klicken Sie auf der Registerkarte **Start** in der Gruppe **Erstellen** auf **Konfigurationselement erstellen**.  

1.  Geben Sie auf der Seite **Allgemein** des Assistenten zum Erstellen von Konfigurationselementen, wie im folgenden Screenshot gezeigt, einen Namen und eine Beschreibung für das Konfigurationselement an. Wählen Sie dann den geeigneten Konfigurationselementtyp für die einzelnen Szenarien in diesem Artikel aus.  

     ![Seite „Allgemein“ des Assistenten zum Erstellen von Konfigurationselementen](../../mdm/deploy-use/media/Compliance-Settings-Wizard---1.png)  

## <a name="scenario-disable-bluetooth-on-windows-10-devices"></a>Szenario: Deaktivieren von Bluetooth auf Windows 10-Geräten

 In diesem Szenario hat Ihre Sicherheitsabteilung festgestellt, dass die Bluetooth-Funktion auf Geräten dazu genutzt werden kann, vertrauliche Unternehmensdaten an externe Geräte zu übermitteln. Sie haben kürzlich für alle Ihre Computer ein Upgrade auf Windows 10 durchgeführt. Sie beschließen, Bluetooth auf diesen Geräten zu deaktivieren.  

1. Wählen Sie im Assistenten zum Erstellen von Konfigurationselementen auf der Seite **Allgemein** den Konfigurationselementtyp **Windows 10** aus, und klicken Sie dann auf **Weiter**.  

2. Wählen Sie auf der Seite **Unterstützte Plattformen** des Assistenten alle Windows 10-Plattformen aus.  

3. Wählen Sie auf der Seite **Geräteeinstellungen** die Option **Gerät** und dann **Weiter** aus.  

4. Wählen Sie auf der Seite **Sicherheit** die Option **Nicht zulässig** als Einstellung für **Bluetooth**aus.  

5. Wählen Sie **Nicht kompatible Einstellungen wiederherstellen** aus, um sicherzustellen, dass die Änderung auf alle Windows 10-Geräte angewendet wird.  

6. Schließen Sie den Assistenten ab, um das neue Konfigurationselement zu erstellen.  

 Sie können nun die Informationen im Artikel [Allgemeine Aufgaben zum Erstellen und Bereitstellen von Konfigurationsbaselines mit Configuration Manager](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) verwenden, um die von Ihnen erstellte Konfiguration auf Geräten bereitzustellen.  

## <a name="scenario-remediate-an-incorrect-registry-value-on-windows-desktop-computers"></a>Szenario: Wiederherstellen eines falschen Registrierungswerts auf Windows-Desktopcomputern

> [!NOTE] 
> Auf Macintosh-Computern mit ausgeführtem Configuration Manager-Client haben Sie zwei Optionen zur Bewertung der Kompatibilität:  
> - Auswerten einer Datei mit Einstellungen für Mac OS X (.plist)
> - Verwenden eines benutzerdefinierten Skripts und Auswerten der vom Skript zurückgegeben Ergebnisse  
>
>Mehr Informationen finden Sie unter [Erstellen von Konfigurationselementen für Mac OS X-Geräte, die mit dem Configuration Manager-Client verwaltet werden](../../compliance/deploy-use/create-configuration-items-for-mac-os-x-devices-managed-with-the-client.md).  

 In diesem Szenario erkennen Sie, dass eine wichtige Sparten-App auf einigen von Ihnen verwalteten Computern mit Windows 8.1. nicht ordnungsgemäß funktioniert. Sie stellen fest, dass der Wert des Registrierungsschlüssels **HKEY_LOCAL_MACHINE\SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1** auf einigen Computern auf den Wert **0** festgelegt ist. Damit die Branchen-App ordnungsgemäß funktioniert, muss dieser Wert auf **1** festgelegt werden.  

 Bei diesem Verfahren erstellen Sie ein Konfigurationselement, das eine Überwachung auf falsche Registrierungsschlüsselwerte durchführt und diese automatisch korrigiert.  

1. Wählen Sie im Assistenten zum Erstellen von Konfigurationselementen auf der Seite **Allgemein** den Konfigurationselementtyp **Windows-Desktop oder -Server (benutzerdefiniert)** aus, und klicken Sie dann auf **Weiter**.  

2. Wählen Sie auf der Seite **Unterstützte Plattformen** des Assistenten **Windows 8.1** aus (um sicherzustellen, dass das Konfigurationselement nur für betroffene Computer gilt).  

3. Klicken Sie auf der Seite **Einstellungen** auf **Neu**, um eine neue Einstellung zu erstellen.  

4. Konfigurieren Sie auf der Registerkarte **Allgemein** des Dialogfelds **Einstellung erstellen** die folgenden Einstellungen:  

   -   **Name** > **Beispieleinstellung**  

   -   **Einstellungstyp** > **Registrierungswert**  

   -   **Datentyp** > **Ganze Zahl** (da der Wert nur eine Zahl enthält)  

   -   **Struktur** > **HKEY_LOCAL_MACHINE**  

   -   **Schlüssel** > **SOFTWARE\Woodgrove\LOB App\Configuration\Configuration1**  

   -   **Wert** > **1** (der erforderliche Wert)  

5. Wählen Sie auf der Registerkarte **Konformitätsregeln** des Dialogfelds **Einstellung erstellen** die Option **Neu** aus. Konfigurieren Sie die folgenden Einstellungen im Dialogfeld **Regel erstellen**:  

   -   **Name** > **Beispielregel**  

   -   **Ausgewählte Einstellung**: Überprüfen Sie, ob die ausgewählte Einstellung **Beispieleinstellung** lautet.

   -   **Regeltyp** > **Wert**  

   -   **Die Einstellung muss folgende Regel erfüllen**: Stellen Sie sicher, dass der Name der Einstellung richtig ist. Konfigurieren Sie die Option, um anzugeben, dass der Einstellungswert **1** lauten muss.  

   -   **Nicht konforme Regeln wiederherstellen, falls dies unterstützt wird**: Aktivieren Sie dieses Kontrollkästchen, um sicherzustellen, dass Configuration Manager den Wert des Registrierungsschlüssels auf den richtigen Wert zurücksetzt, wenn er falsch ist.  

6. Schließen Sie den Assistenten ab, um das neue Konfigurationselement zu erstellen.  

 Sie können nun die Informationen im Artikel [Allgemeine Aufgaben zum Erstellen und Bereitstellen von Konfigurationsbaselines](../../compliance/plan-design/common-tasks-for-creating-and-deploying-configuration-baselines.md) verwenden, um die von Ihnen erstellte Konfiguration auf Geräten bereitzustellen.  

## <a name="next-steps"></a>Nächste Schritte

[Erstellen und Bereitstellen von Konfigurationsbaselines](common-tasks-for-creating-and-deploying-configuration-baselines.md)
