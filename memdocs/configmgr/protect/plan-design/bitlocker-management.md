---
title: Plan für die BitLocker-Verwaltung
titleSuffix: Configuration Manager
description: Planung der Verwaltung der BitLocker-Laufwerkverschlüsselung mit Configuration Manager
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a4d8cda2-bc9b-4fb4-aa0d-23c31b4fc60b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 2523d06034f4a7effe769235cb5a4ede4df7e167
ms.sourcegitcommit: 9a700a72735f9a316bdb51c44f86f9cc3bfb7be2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/21/2020
ms.locfileid: "83764117"
---
# <a name="plan-for-bitlocker-management"></a>Plan für die BitLocker-Verwaltung

*Gilt für: Configuration Manager (Current Branch)*

<!-- 3601034 -->

Ab Version 1910 können Sie die BitLocker-Laufwerkverschlüsselung (BitLocker Drive Encryption, BDE) von Configuration Manager für lokale Windows-Clients verwalten. Configuration Manager bietet eine vollständige Lebenszyklusverwaltung für BitLocker, die die Microsoft BitLocker-Verwaltung und -Überwachung (Microsoft BitLocker Administration and Monitoring, MBAM) ersetzen kann.

> [!Note]  
> Configuration Manager aktiviert dieses optionale Feature nicht automatisch. Sie müssen dieses Feature aktivieren, bevor Sie es verwenden. Weitere Informationen finden Sie unter [Enable optional features from updates (Aktivieren optionaler Features von Updates)](../../core/servers/manage/install-in-console-updates.md#bkmk_options).  

Weitere Informationen finden Sie unter [BitLocker (Übersicht)](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-overview).

> [!TIP]
> Stellen Sie die [**Endpoint Protection**-Workload](../../comanage/workloads.md#endpoint-protection) auf Intune um, damit Sie die Verschlüsselung auf gemeinsam verwalteten Windows 10-Geräten mit dem Clouddienst „Microsoft Endpoint Manager“ verwalten können. Weitere Informationen zur Verwendung von Intune finden Sie unter [Windows-Verschlüsselung](/intune/protect/endpoint-protection-windows-10#windows-encryption).

## <a name="features"></a>Features

Configuration Manager bietet die folgenden Verwaltungsfunktionen für die BitLocker-Laufwerkverschlüsselung:

### <a name="client-deployment"></a>Clientbereitstellung

Stellen Sie den BitLocker-Client auf verwalteten Windows-Geräten mit Windows 10 oder Windows 8.1 bereit.

### <a name="manage-encryption-policies"></a>Verwalten von Verschlüsselungsrichtlinien

- Beispiel: Wählen Sie die Laufwerkverschlüsselung und Verschlüsselungsstärke aus, und konfigurieren Sie die Ausnahmerichtlinie für Benutzer, die Verschlüsselungseinstellungen für das Festplattenlaufwerk.

- Bestimmen Sie die Algorithmen, mit denen das Gerät verschlüsselt werden soll, und die Datenträger, die verschlüsselt werden sollen.

- Erzwingen Sie, dass Benutzer vor der Verwendung des Geräts die neuen Sicherheitsrichtlinien erfüllen.

- Passen Sie das Sicherheitsprofil ihrer Organisation für jedes Gerät an.

- Wenn ein Benutzer das Betriebssystemlaufwerk entsperrt, geben Sie an, ob nur ein Betriebssystemlaufwerk oder alle angefügten Laufwerke entsperrt werden sollen.

### <a name="compliance-reports"></a>Konformitätsberichte

Integrierte Berichte für:

- Den Verschlüsselungsstatus pro Volume oder pro Gerät
- Der primäre Benutzer des Geräts
- Konformitätsstatus
- Gründe für Nichtkonformität

### <a name="administration-and-monitoring-website"></a>Administration and Monitoring-Website

Lassen Sie zu, dass andere Personen in Ihrer Organisation außerhalb der Configuration Manager-Konsole bei der Schlüsselwiederherstellung helfen können, z. B. durch Schlüsselrotation und anderen BitLocker-spezifischen Support. Helpdeskadministratoren können Benutzern z. B. bei der Schlüsselwiederherstellung behilflich sein.

### <a name="user-self-service-portal"></a>Self-Service-Portal für Benutzer

Ermöglichen Sie es Benutzern, ein mit BitLocker verschlüsseltes Gerät mit einem Single Use Key selbst zu entsperren. Sobald dieser Schlüssel verwendet wird, wird ein neuer Schlüssel für das Gerät generiert.

## <a name="prerequisites"></a>Voraussetzungen

- Wenn Sie eine BitLocker-Verwaltungsrichtlinie erstellen möchten, benötigen Sie in Configuration Manager die Rolle **Hauptadministrator**.

- Der BitLocker-Wiederherstellungsdienst benötigt HTTPS, um die Wiederherstellungsschlüssel im Netzwerk zwischen dem Configuration Manager-Client und dem Verwaltungspunkt zu verschlüsseln. Es stehen zwei Optionen zur Verfügung:

  - HTTPS wird für die IIS-Website auf dem Verwaltungspunkt, auf dem der Wiederherstellungsdienst gehostet wird, aktiviert. Diese Option gilt nur für Version 2002 von Configuration Manager.<!-- 5925660 -->

  - Konfigurieren des Verwaltungspunkts für HTTPS. Diese Option gilt nur für die Versionen 1910 und 2002 von Configuration Manager.

  Weitere Informationen finden Sie unter [Verschlüsseln von Wiederherstellungsdaten](../deploy-use/bitlocker/encrypt-recovery-data.md).

- Wenn Sie BitLocker-Verwaltungsberichte verwenden möchten, installieren Sie die Standortsystemrolle „Reporting Services-Punkt“. Weitere Informationen finden Sie unter [Konfigurieren der Berichterstellung](../../core/servers/manage/configuring-reporting.md).

    > [!NOTE]
    > Damit der **Bericht zur Wiederherstellungsüberwachung** über die Verwaltungs- und Überwachungswebsite funktioniert, dürfen Sie nur am primären Standort einen Reporting Services-Punkt verwenden.

- Für das Self-Service-Portal oder die Verwaltungs- und Überwachungswebsite benötigen Sie einen Windows-Server, auf dem die Internetinformationsdienste ausgeführt werden. Sie können ein Configuration Manager-Standortsystem wieder verwenden oder einen eigenständigen Webserver nutzen, der über eine Verbindung mit dem Standortdatenbankserver verfügt. Verwenden Sie eine [unterstützte Betriebssystemversion für Standortsystemserver](../../core/plan-design/configs/supported-operating-systems-for-site-system-servers.md).

    > [!NOTE]
    > Installieren Sie das Self-Service-Portal und die Verwaltungs- und Überwachungswebsite nur mit einer Datenbank für den primären Standort. Installieren Sie diese Websites in einer Hierarchie für jeden primären Standort.

- Installieren Sie [Microsoft ASP.NET MVC 4.0](https://docs.microsoft.com/aspnet/mvc/mvc4) auf dem Webserver, auf dem das Self-Service-Portal gehostet wird.

- Das Benutzerkonto zur Ausführung des Portalinstallationsskripts benötigt auf dem Standortdatenbankserver **sysadmin**-Rechte für SQL. Während des Setupvorgangs legt das Skript die Anmeldung, den Benutzer und die SQL-Rollenberechtigungen für das Computerkonto des Webservers fest. Sie können dieses Benutzerkonto aus der Rolle „sysadmin“ entfernen, nachdem Sie das Setup für das Self-Service-Portal und die Verwaltungs- und Überwachungswebsite abgeschlossen haben.

- Die BitLocker-Verwaltung wird auf virtuellen Computern (VMs) oder Serverbetriebssystemen nicht unterstützt. Aus diesem Grund funktionieren einige Features auf virtuellen Computern oder Serverbetriebssystemen möglicherweise nicht wie erwartet. Beispielsweise startet die BitLocker-Verwaltung auf virtuellen Computern die Verschlüsselung nicht auf festen Laufwerken der virtuellen Computer. Zudem können sich feste Laufwerke in virtuellen Computern als konform erweisen, obwohl sie nicht verschlüsselt sind.

> [!TIP]
> Der Tasksequenzschritt **BitLocker aktivieren** verschlüsselt standardmäßig nur den *verwendeten Speicherplatz* auf dem Laufwerk. Die BitLocker-Verwaltung verwendet die *vollständige* Datenträgerverschlüsselung. Konfigurieren Sie diesen Tasksequenzschritt, um die Option **Vollständige Datenträgerverschlüsselung verwenden** zu aktivieren. Weitere Informationen finden Sie unter [Tasksequenzschritte – Aktivieren von BitLocker](../../osd/understand/task-sequence-steps.md#BKMK_EnableBitLocker).

## <a name="next-steps"></a>Nächste Schritte

[Verschlüsseln von Wiederherstellungsdaten](../deploy-use/bitlocker/encrypt-recovery-data.md) (optionale Voraussetzung vor dem erstmaligen Bereitstellen der Richtlinie)

[Bereitstellen der BitLocker-Verwaltung](../deploy-use/bitlocker/deploy-management-agent.md)
