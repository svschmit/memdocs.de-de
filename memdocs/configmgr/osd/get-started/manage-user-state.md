---
title: Verwalten des Benutzerzustands
titleSuffix: Configuration Manager
description: Configuration Manager verwendet das Migrationstool für den Benutzerstatus, um in Szenarios für die Betriebssystembereitstellung den Benutzerstatus zu erfassen und wiederherzustellen.
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: d8d5c345-1e91-410b-b8a9-0170dcfa846e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 0a720c68fc705187dedb6ff04fc3898a8b0b21c8
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88124362"
---
# <a name="manage-user-state-in-configuration-manager"></a>Verwalten des Benutzerstatus in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Mit Configuration Manager-Tasksequenzen können Sie bei der Betriebssystembereitstellung die Benutzerstatusdaten erfassen und wiederherstellen, wenn Sie den Benutzerstatus des aktuellen Betriebssystems beibehalten möchten. Beispiel:  

- Bereitstellungen, bei denen Sie den Benutzerzustand auf einem Computer erfassen und auf einem anderen Computer wiederherstellen möchten  

- Updatebereitstellungen, bei denen Sie den Benutzerzustand auf dem gleichen Computer erfassen und wiederherstellen möchten  

Configuration Manager verwendet das Migrationstool für den Benutzerstatus (USMT 10.0), um nach Abschluss der Installation des Betriebssystems die Migration von Benutzerstatusdaten von einem Quellcomputer zu einem Zielcomputer zu verwalten. Weitere Informationen zu häufigen Migrationsszenarien für USMT 10.0 finden Sie unter  [Häufige Migrationsszenarien](https://docs.microsoft.com/windows/deployment/usmt/usmt-common-migration-scenarios).

Mithilfe der folgenden Abschnitte können Sie Benutzerdaten erfassen und wiederherstellen.

## <a name="store-user-state-data"></a><a name="BKMK_StoringUserData"></a> Speichern von Benutzerzustandsdaten

 Wenn Sie den Benutzerzustand erfassen, können Sie die Benutzerzustandsdaten auf dem Zielcomputer oder auf einem Zustandsmigrationspunkt speichern. Sie müssen einen Configuration Manager-Standortsystemserver verwenden, auf dem die Standortsystemrolle „Statusmigrationspunkt“ gehostet wird, um den Benutzerstatus auf einem Migrationspunkt für den Benutzerstatus zu speichern. Wenn Sie den Benutzerzustand auf dem Zielcomputer speichern möchten, müssen Sie die Tasksequenz so konfigurieren, dass die Daten lokal mithilfe von Links gespeichert werden.

> [!NOTE]
> Die Links, mit deren Hilfe der Benutzerzustand lokal gespeichert wird, werden als feste Links bezeichnet. Feste Links sind eine Funktion von USMT 10.0. Diese Funktion dient dazu, den Computer auf Benutzerdateien und -einstellungen zu durchsuchen und dann die festen Links zu diesen Dateien in einem Verzeichnis zu erfassen. Mithilfe der festen Links werden dann die Benutzerdaten wiederhergestellt, nachdem das neue Betriebssystem bereitgestellt wurde.

> [!IMPORTANT]
> Es ist nicht möglich, zum Speichern der Benutzerzustandsdaten sowohl einen Zustandsmigrationspunkt als auch feste Links zu verwenden.

Wenn die Benutzerzustandsinformationen erfasst sind, können sie auf folgende Arten gespeichert werden:  

- Sie können die Benutzerzustandsdaten remote speichern, indem Sie einen Zustandsmigrationspunkt konfigurieren. Die Daten werden von der Tasksequenz **Erfassen** an den Zustandsmigrationspunkt gesendet. Nach der Bereitstellung des Betriebssystems werden die Daten von der Tasksequenz **Wiederherstellen** abgerufen, und der Benutzerzustand wird auf dem Zielcomputer wiederhergestellt.  

- Sie können die Benutzerzustandsdaten lokal an einem bestimmten Speicherort speichern. In diesem Szenario werden die Benutzerdaten von der Tasksequenz **Erfassen** an einen bestimmten Speicherort auf dem Zielcomputer kopiert. Nach der Bereitstellung des Betriebssystems werden die Daten durch die Tasksequenz **Wiederherstellen** von diesem Speicherort abgerufen.  

- Sie können Hardlinks angeben, die verwendet werden können, um die Benutzerdaten am ursprünglichen Speicherort wiederherzustellen. In diesem Szenario verbleiben die Benutzerdaten auf dem Laufwerk, wenn das alte Betriebssystem entfernt wird. Nach der Bereitstellung des neuen Betriebssystems werden die Benutzerzustandsdaten von der Tasksequenz **Wiederherstellen** mithilfe der festen Links am ursprünglichen Speicherort wiederhergestellt.  

### <a name="store-user-data-on-a-state-migration-point"></a><a name="BKMK_UserDataSMP"></a> Speichern von Benutzerdaten auf einem Zustandsmigrationspunkt

 Sie müssen die folgenden Schritte ausführen, um die Benutzerzustandsdaten auf einem Zustandsmigrationspunkt zu speichern:  

1. [Configure a state migration point](#BKMK_StateMigrationPoint) , um die die Benutzerzustandsdaten zu speichern.  

1. [Create a computer association](#BKMK_ComputerAssociation) zwischen dem Quellcomputer und dem Zielcomputer. Sie müssen diese Zuordnung erstellen, bevor Sie den Benutzerzustand auf dem Quellcomputer erfassen.  

1. [Tasksequenz erstellen](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md), um den Benutzerstatus zu erfassen und wiederherzustellen. Insbesondere müssen Sie die folgenden Schritte der Tasksequenz ausführen, um Benutzerdaten von einem Computer zu erfassen, die Benutzerdaten auf einem Statusmigrationspunkt zu speichern und anschließend auf einem Computer wiederherzustellen:  

    - [Statusspeicher anfordern](../understand/task-sequence-steps.md#BKMK_RequestStateStore), um den Zugriff auf einen Statusmigrationspunkt anzufordern, wenn der Computerstatus erfasst oder auf einem Computer wiederhergestellt werden soll.  

    - [Benutzerstatus erfassen](../understand/task-sequence-steps.md#BKMK_CaptureUserState), um die Benutzerstatusdaten zu erfassen und auf dem Statusmigrationspunkt zu speichern.  

    - [Benutzerstatus wiederherstellen](../understand/task-sequence-steps.md#BKMK_RestoreUserState), um den Benutzerstatus durch Abrufen der Daten von einem Migrationspunkt für den Benutzerstatus auf dem Zielcomputer wiederherzustellen.  

    - [Statusspeicher freigeben](../understand/task-sequence-steps.md#BKMK_ReleaseStateStore), um den Statusmigrationspunkt darüber zu benachrichtigen, dass die Erfassungs- oder Wiederherstellungsaktion abgeschlossen ist.  

### <a name="store-user-data-locally"></a><a name="BKMK_UserDataDestination"></a> Speichern von Benutzerdaten auf einem lokalen Computer

 Um die Benutzerdaten lokal zu speichern, gehen Sie folgendermaßen vor:  

- [Tasksequenz erstellen](../deploy-use/create-a-task-sequence-to-capture-and-restore-user-state.md), um den Benutzerstatus zu erfassen und wiederherzustellen. Insbesondere müssen Sie die folgenden Tasksequenzschritte hinzufügen, um Benutzerdaten von einem Computer zu erfassen und anschließend auf einem Computer unter Verwendung von festen Links wiederherzustellen:

  - [Benutzerstatus erfassen](../understand/task-sequence-steps.md#BKMK_CaptureUserState), um die Benutzerdaten zu erfassen und unter Verwendung von festen Links in einen lokalen Ordner zu speichern.  

  - [Benutzerstatus wiederherstellen](../understand/task-sequence-steps.md#BKMK_RestoreUserState), um den Benutzerstatus durch Abrufen der Daten unter Verwendung von festen Links auf dem Zielcomputer wiederherzustellen.  

    > [!NOTE]
    > Die Benutzerzustandsdaten, auf die von den festen Links verwiesen wird, verbleiben auf dem Computer, nachdem das alte Betriebssystem von der Tasksequenz entfernt wurde. Dies sind die Daten, mit deren Hilfe die Benutzerdaten wiederhergestellt werden, wenn das neue Betriebssystem bereitgestellt wird.  

## <a name="configure-a-state-migration-point"></a><a name="BKMK_StateMigrationPoint"></a> Configure a state migration point

Vom Zustandsmigrationspunkt werden die auf einem Computer erfassten Benutzerdaten gespeichert und anschließend auf einem anderen Computer wiederhergestellt. Wenn Sie jedoch Benutzereinstellungen für eine Betriebssystembereitstellung auf dem gleichen Computer erfassen, z. B. zur Aktualisierung des Betriebssystems auf dem Zielcomputer, können Sie die Daten auf dem gleichen Computer unter Verwendung von festen Links oder auf dem Zustandsmigrationspunkt speichern. Wenn Sie den Statusspeicher erstellen, wird von Configuration Manager bei einigen Computerbereitstellungen automatisch eine Zuordnung zwischen Statusspeicher und Zielcomputer erstellt. Mithilfe der folgenden Methoden können Sie einen Zustandsmigrationspunkt zum Speichern der Benutzerzustandsdaten konfigurieren:  

- Verwenden Sie den **Assistenten zum Erstellen von Standortsystemservern**, um einen neuen Standortsystemserver für den Zustandsmigrationspunkt zu erstellen.  

- Verwenden Sie den **Assistenten zum Hinzufügen von Standortsystemrollen**, um einem vorhandenen Server einen Zustandsmigrationspunkt hinzuzufügen.  

  Wenn Sie diese Assistenten verwenden, werden Sie aufgefordert, die folgenden Angaben zum Zustandsmigrationspunkt zu machen:  

- Die Ordner, in denen die Benutzerzustandsdaten gespeichert werden  

- Die maximale Anzahl von Clients, von denen Daten auf dem Zustandsmigrationspunkt gespeichert werden können  

- Der für einen Zustandsmigrationspunkt zum Speichern der Benutzerzustandsdaten mindestens erforderliche freie Speicherplatz  

- Die Löschrichtlinie für die Rolle. Sie können angeben, ob die Benutzerzustandsdaten sofort oder erst nach Ablauf einer bestimmten Anzahl von Tagen nach ihrer Wiederherstellung auf einem Computer gelöscht werden.  

- Ob vom Zustandsmigrationspunkt nur Anforderungen zum Wiederherstellen von Benutzerzustandsdaten beantwortet werden. Wenn Sie diese Option aktivieren, können Sie den Zustandsmigrationspunkt nicht zum Speichern von Benutzerzustandsdaten verwenden.  

  Weitere Informationen zum Statusmigrationspunkt und den entsprechenden Konfigurationsschritten finden Sie unter [Statusmigrationspunkt](prepare-site-system-roles-for-operating-system-deployments.md#BKMK_StateMigrationPoints).  

## <a name="create-a-computer-association"></a><a name="BKMK_ComputerAssociation"></a> Create a computer association

Erstellen Sie eine Computerzuordnung, um eine Beziehung zwischen einem Quellcomputer und einem Zielcomputer zu definieren, wenn Sie ein Betriebssystem auf neuer Hardware installieren und Benutzereinstellungen erfassen und wiederherstellen möchten. Der Quellcomputer ist ein vorhandener Computer, der von Configuration Manager verwaltet wird. Wenn Sie das neue Betriebssystem auf dem Zielcomputer bereitstellen, enthält der Quellcomputer den Benutzerzustand, der zum Zielcomputer migriert wird.  

> [!NOTE]  
> Das Erstellen einer Computerzuordnung zwischen Computern an einem übergeordneten Configuration Manager-Standort und Computern an einem untergeordneten Standort wird nicht unterstützt. Computerzuordnungen sind standortspezifisch und werden nicht repliziert.  

### <a name="to-create-a-computer-association"></a>So erstellen Sie eine Computerzuordnung

1. Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

1. Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Benutzerzustandsmigration**.  

1. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Computerzuordnung erstellen**.  

1. Geben Sie im Dialogfeld **Eigenschaften der Computerzuordnung** auf der Registerkarte **Computerzuordnung** den Quellcomputer an, auf dem der Benutzerzustand erfasst wird, sowie den Zielcomputer, auf dem die Benutzerzustandsdaten wiederhergestellt werden.  

1. Geben Sie auf der Registerkarte **Benutzerkonten** die Benutzerkonten an, die zum Zielcomputer migriert werden sollen. Geben Sie eine der folgenden Einstellungen an:  

    - **Alle Benutzerkonten erfassen und wiederherstellen:** Bei dieser Einstellung werden alle Benutzerkonten erfasst und wiederhergestellt. Verwenden Sie diese Einstellung, um mehrere Zuordnungen zum gleichen Quellcomputer zu erstellen.  

    - **Alle Benutzerkonten erfassen und bestimmte Konten wiederherstellen:** Bei dieser Einstellung werden alle Benutzerkonten auf dem Quellcomputer erfasst und nur die von Ihnen angegebenen Konten auf dem Zielcomputer wiederhergestellt. Sie können mit dieser Einstellung auch mehrere Zuordnungen zum gleichen Quellcomputer erstellen.  

    - **Bestimmte Benutzerkonten erfassen und wiederherstellen:** Bei dieser Einstellung werden nur die von Ihnen angegebenen Konten erfasst und wiederhergestellt. Wenn diese Einstellung ausgewählt ist, ist es nicht möglich, mehrere Zuordnungen zum gleichen Quellcomputer zu erstellen.  

## <a name="restore-user-state-data-when-an-operating-system-deployment-fails"></a><a name="BKMK_MigrationFails"></a> Wiederherstellen von Benutzerzustandsdaten, wenn bei einer Betriebssystembereitstellung ein Fehler auftritt

Wenn bei der Bereitstellung des Betriebssystems ein Fehler auftritt, können Sie die LoadState-Funktion von USMT 10.0 verwenden, um die während des Bereitstellungsvorgangs erfassten Benutzerzustandsdaten abzurufen. Dazu gehören auch Daten, die auf einem Zustandsmigrationspunkt oder lokal auf dem Zielcomputer gespeichert sind. Weitere Informationen zu dieser USMT-Funktion finden Sie unter [LoadState-Syntax](https://docs.microsoft.com/windows/deployment/usmt/usmt-loadstate-syntax).
