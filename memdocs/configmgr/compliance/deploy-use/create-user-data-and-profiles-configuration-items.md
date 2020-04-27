---
title: Erstellen von Konfigurationselementen für Benutzerdaten und -profile
titleSuffix: Configuration Manager
description: Verwenden Sie Konfigurationselemente für Benutzerdaten und -profile in Configuration Manager, um Ordnerumleitung, Offlinedateien und servergespeicherte Benutzerprofile zu verwalten.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 9fcbcc81-cd6f-496e-b075-ef1afa2b8ccc
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2a99384772895ff2675ade671076163b74cecee2
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82075301"
---
# <a name="create-user-data-and-profiles-configuration-items-in-configuration-manager"></a>Erstellen von Benutzerdaten und Profile von Konfigurationselementen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Konfigurationselemente für Benutzerdaten und -profile in Configuration Manager enthalten Einstellungen, mit denen die Ordnerumleitung, Offlinedateien und Roamingprofile auf Computern mit Windows 8 und höher für Benutzer in Ihrer Hierarchie verwaltet werden können. Beispielsweise können Sie folgende Aktionen ausführen:  

- Umleiten des Ordners „Dokumente“ eines Benutzers an eine Netzwerkfreigabe  

- Sicherstellen, dass angegebene Dateien, die im Netzwerk gespeichert sind, auf dem Computer eines Benutzers verfügbar sind, wenn keine Netzwerkverbindung besteht  

- Konfigurieren, welche Dateien im servergespeicherten Profil eines Benutzers bei dessen An- und Abmeldung mit einer Netzwerkfreigabe synchronisiert werden  

  Im Unterschied zu anderen Konfigurationselementen in Configuration Manager fügen Sie Konfigurationselemente für Benutzerdaten und -profile keiner Konfigurationsbaseline hinzu, die anschließend bereitgestellt wird. Stattdessen stellen Sie das Konfigurationselement direkt über das Dialogfeld **Konfigurationselemente für Benutzerdaten und Profile bereitstellen** bereit.  

> [!IMPORTANT]  
>  Sie können Konfigurationselemente für Benutzerdaten und Profile nur für Benutzersammlungen bereitstellen.  

## <a name="enable-user-data-and-profiles-for-compliance-settings"></a>Aktivieren von Benutzerdaten und Profilen für Kompatibilitätseinstellungen  
 Verwenden Sie das folgende Verfahren, um die Clientstandardeinstellung für Kompatibilitätseinstellungen der Benutzerdaten und Profile zu konfigurieren, die auf alle Computern in Ihrer Hierarchie angewendet wird. Wenn Sie diese Einstellung nur auf manche Computer anwenden möchten, erstellen Sie eine benutzerdefinierte Geräteclienteinstellung, und weisen Sie sie einer Sammlung mit den Computern zu, für die Sie Konformitätseinstellungen der Benutzerdaten und Profile verwenden möchten. Weitere Informationen zum Erstellen von benutzerdefinierten Geräteeinstellungen finden Sie unter [How to configure client settings (Konfigurieren von Clienteinstellungen)](../../core/clients/deploy/configure-client-settings.md).  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung** > **Clienteinstellungen** > **Standardeinstellungen**.  

4.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

5.  Klicken Sie im Dialogfeld **Standardeinstellungen** auf **Kompatibilitätseinstellungen**.  

6.  Wählen Sie in der Dropdownliste **Benutzerdaten und -profile aktivieren** die Option **Ja**aus.  

7.  Klicken Sie auf **OK** , um das Dialogfeld **Standardeinstellungen** zu schließen.  

## <a name="create-a-user-data-and-profiles-configuration-item"></a>Erstellen von Konfigurationselementen für Benutzerdaten und -profile  

1. Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** > **Kompatibilitätseinstellungen** > **Benutzerdaten und -profile**.  

2. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Konfigurationselement für Benutzerdaten und Profil erstellen**.  

3. Geben Sie auf der Seite **Allgemein** des **Assistenten zum Erstellen von Konfigurationselementen für Benutzerdaten und Profile**die folgenden Informationen an:  

   -   **Name:** Geben Sie einen eindeutigen Namen für das Konfigurationselement ein. Sie können maximal 256 Zeichen verwenden.  

   -   **Beschreibung:** Geben Sie eine Beschreibung des Konfigurationselements sowie weitere relevante Informationen ein, die zur Identifikation des Elements in der Configuration Manager-Konsole dienen. Sie können maximal 256 Zeichen verwenden.  

   -   **Ordnerumleitung:** Aktivieren Sie dieses Kontrollkästchen, wenn Sie Ordnerumleitungseinstellungen für dieses Konfigurationselement festlegen möchten.  

   -   **Offlinedateien:** Aktivieren Sie dieses Kontrollkästchen, wenn Sie Offlinedateieinstellungen für dieses Konfigurationselement festlegen möchten.  

   -   **Roamingbenutzerprofile:** Aktivieren Sie dieses Kontrollkästchen, wenn Sie Einstellungen für Roamingbenutzerprofile für dieses Konfigurationselement festlegen möchten.  

4. Geben Sie auf der Seite **Ordnerumleitung** des **Assistenten zum Erstellen von Konfigurationselementen für Benutzerdaten und Profile**an, wie die Ordnerumleitung von Benutzerclientcomputern, die dieses Konfigurationselement erhalten, verwaltet werden soll. Sie können die Einstellungen für jedes Gerät konfigurieren, bei dem sich der Benutzer anmeldet, oder nur für die primären Geräte des Benutzers. Weitere Informationen zur Ordnerumleitung finden Sie in der Windows Server-Dokumentation.  

   > [!NOTE]  
   >  Diese Seite wird nur angezeigt, wenn Sie auf der Seite **Allgemein** des Assistenten die Option **Ordnerumleitung** aktiviert haben.  

5. Auf der Seite **Offlinedateien** des **Assistenten zum Erstellen von Konfigurationselementen für Benutzerdaten und Profile**können Sie die Nutzung von Offlinedateien für Benutzer, die dieses Konfigurationselement erhalten, aktivieren oder deaktivieren und Einstellungen für das Verhalten der Offlinedateien konfigurieren. Darüber hinaus können Sie Offlinedateien angeben, die immer auf jedem Computer verfügbar sind, bei dem sich der Benutzer anmeldet. Weitere Informationen zu Offlinedateien finden Sie in der Windows Server-Dokumentation.  

   > [!NOTE]  
   >  Diese Seite wird nur angezeigt, wenn Sie auf der Seite **Allgemein** des Assistenten das Kontrollkästchen **Offlinedateien** aktiviert haben.  

6. Auf der Seite **Servergespeicherte Profile** des **Assistenten zum Erstellen von Konfigurationselementen für Benutzerdaten und Profile**können Sie konfigurieren, ob servergespeicherte Profile auf den Computern verfügbar sind, bei denen sich der Benutzer anmeldet, und darüber hinaus das Verhalten dieser Profile genauer festlegen. Weitere Informationen zu servergespeicherten Profilen finden Sie in der Windows Server-Dokumentation.  

   > [!NOTE]  
   >  Diese Seite wird nur angezeigt, wenn Sie auf der Seite **Allgemein** des Assistenten das Kontrollkästchen **Servergespeicherte Benutzerprofile** aktiviert haben.  

7. Schließen Sie den Assistenten ab.  

   Das neue Konfigurationselement für Benutzerdaten und Profile wird im Knoten **Benutzerdaten und Profile** des Arbeitsbereichs **Bestand und Kompatibilität** angezeigt.  

## <a name="deploy-a-user-data-and-profiles-configuration-item"></a>Bereitstellen von Konfigurationselementen für Benutzerdaten und -profile  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität** > **Kompatibilitätseinstellungen** > **Benutzerdaten und -profile**.  

3.  Wählen Sie das Konfigurationselement für Benutzerdaten und Profile aus, das Sie bereitstellen möchten, und klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Bereitstellen**.  

4.  Geben Sie im Dialogfeld **Konfigurationselemente für Benutzerdaten und Profile bereitstellen** die folgenden Informationen an.  

    -   **Sammlung:** Klicken Sie auf **Durchsuchen** , um die Benutzersammlung auszuwählen, in der Sie das Konfigurationselement bereitstellen möchten.  

        > [!IMPORTANT]  
        >  Sie können Konfigurationselemente für Benutzerdaten und Profile nur für Benutzersammlungen bereitstellen.  

    -   **Nicht kompatible Regeln wiederherstellen, falls dies unterstützt wird:** Aktivieren Sie diese Option, um automatisch Regeln wiederherzustellen, die auf Clientcomputern als nicht kompatibel ausgewertet werden.  

    -   **Wiederherstellung außerhalb des Wartungsfensters zulassen:** Wenn ein Wartungsfenster für die Sammlung konfiguriert wurde, für die Sie das Konfigurationselement bereitstellen, aktivieren Sie diese Option, um Kompatibilitätseinstellungen zum Wiederherstellen des Werts außerhalb des Wartungsfensters zuzulassen. Weitere Informationen zu Wartungsfenstern finden Sie unter [Verwenden von Wartungsfenstern](../../core/clients/manage/collections/use-maintenance-windows.md).  

    -   **Warnung generieren:** Aktivieren Sie diese Option zum Konfigurieren einer Warnung, die generiert wird, sobald die Kompatibilität eines Konfigurationselements zu einem bestimmten Datum und einer bestimmten Uhrzeit unterhalb eines angegebenen Prozentsatzes liegt. Sie können außerdem angeben, ob eine Warnung an System Center Operations Manager gesendet werden soll.  

    -   **Geben Sie den Zeitplan für die Kompatibilitätsauswertung dieses Konfigurationselements an:** Gibt den Zeitplan an, nach dem das bereitgestellte Konfigurationselement auf Clientcomputern ausgewertet wird. Dabei kann es sich um einen einfachen oder benutzerdefinierten Zeitplan handeln.  

5.  Klicken Sie auf **OK** , um das Dialogfeld **Konfigurationselemente für Benutzerdaten und Profile bereitstellen** zu schließen und die Bereitstellung zu erstellen.  

## <a name="monitor-a-user-data-and-profiles-configuration-item"></a>So überwachen Sie ein Konfigurationselement für Benutzerdaten und Profile  
 Sie überwachen diesen Konfigurationselementtyp auf die gleiche Weise wie andere Kompatibilitätseinstellungen.  

 Weitere Informationen finden Sie unter [How to monitor compliance settings (Überwachen von Kompatibilitätseinstellungen)](../../compliance/deploy-use/monitor-compliance-settings.md).  
