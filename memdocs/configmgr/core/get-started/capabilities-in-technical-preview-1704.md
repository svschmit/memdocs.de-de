---
title: Funktionen in Technical Preview 1704
titleSuffix: Configuration Manager
description: Erfahren Sie mehr zu Features, die in Technical Preview für Configuration Manager-Version 1704 zur Verfügung stehen.
ms.date: 04/21/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: e318e705-20f2-417d-8cde-7dfe661b2fa7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: c24b9a6e4f6f123e0456b9f1337a7c3b19ab6962
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705268"
---
# <a name="capabilities-in-technical-preview-1704-for-configuration-manager"></a>Funktionen in der Technical Preview 1704 für Configuration Manager

*Gilt für: Configuration Manager (Technical Preview-Branch)*

In diesem Artikel werden die Features vorgestellt, die in der Technical Preview-Version 1704 für Configuration Manager verfügbar sind. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen. Bevor Sie diese Version der Technical Preview installieren, lesen Sie das einführende Thema [Technical Preview für Configuration Manager](../../core/get-started/technical-preview.md), um sich mit den allgemeinen Anforderungen und Einschränkungen bei der Verwendung einer Technical Preview vertraut zu machen und um zu erfahren, wie Sie Updates für Versionen durchführen und Feedback zu den Features in einer Technical Preview geben können.    


**Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  

## <a name="configure-android-apps-with-app-configuration-policies"></a>Konfigurieren von Android-Apps mit Konfigurationsrichtlinien für Apps
Sie können Konfigurationsrichtlinien für Apps in Configuration Manager verwenden, um Einstellungen bereitzustellen, die beim Ausführen einer App durch den Benutzer auf Android for Work-Geräten erforderlich sein können. Konfigurationsrichtlinien für Android-Apps stehen nur auf Geräten zur Verfügung, die Android for Work ausführen, und gelten für genehmigte Apps aus dem Play for Work-Store.

### <a name="try-it-out"></a>Probieren Sie es aus                 

Wählen Sie in der Configuration Manager-Konsole **Softwarebibliothek** > **Anwendungsverwaltung** > **App-Konfigurationsrichtlinien** aus, und wählen Sie **Richtlinie für die App-Konfiguration erstellen**. Auf der Seite **Allgemein** des Assistenten können Sie jetzt einen **Konfigurationsrichtlinientyp auswählen:** . Geben Sie die Plattform an, auf die die App-Konfigurationsrichtlinie ausgerichtet ist: **Konfigurationsrichtlinie für Android for Work-Apps**. Sie können dann zwischen zwei Optionen wählen: **Name/Wert-Paare angeben** oder **Zu Eigenschaftenlisten-JSON-Datei wechseln**. Die neue App-Konfigurationsrichtlinie wird im Knoten **App-Konfigurationsrichtlinien** des Arbeitsbereichs **Softwarebibliothek** angezeigt. Um eine App-Konfigurationsrichtlinie mit der Bereitstellung einer Android for Work-App zuzuordnen, stellen Sie die Anwendung wie gewohnt bereit, indem Sie die Vorgehensweise im Thema [Bereitstellen von Anwendungen](../../apps/deploy-use/deploy-applications.md) durchführen.

## <a name="hardware-inventory-collects-secure-boot-information"></a>Die Hardwareinventur sammelt Sicherer Start-Informationen
Die Hardwareinventur sammelt jetzt Informationen darüber, ob Sicherer Start auf Clients aktiviert ist. Diese Informationen werden in der **SMS_Firmware**-Klasse (eingeführt in Version 1702) gespeichert und standardmäßig in der Hardwareinventur aktiviert. Weitere Informationen zur Hardwareinventur finden Sie unter [How to configure hardware inventory (Konfigurieren der Hardwareinventur)](../clients/manage/inventory/configure-hardware-inventory.md).

## <a name="add-child-task-sequences-to-a-task-sequence"></a>Hinzufügen von untergeordneten Tasksequenzen zu einer Tasksequenz
In dieser Version können Sie einen neuen Tasksequenzschritt hinzufügen, der eine andere Tasksequenz ausführt, die eine Beziehung zwischen übergeordnetem/untergeordnetem Objekt zwischen den Tasksequenzen erstellt. Dadurch können Sie modularere Tasksequenzen erstellen, die Sie wiederverwenden können.  

Berücksichtigen Sie Folgendes, wenn Sie eine untergeordnete Tasksequenz einer Tasksequenz hinzufügen:

- Die über- und untergeordneten Tasksequenzen werden effektiv in einer einzigen Richtlinie kombiniert, die der Client ausführt.
- Es wird nicht unterstützt, eine untergeordnete Tasksequenz hinzuzufügen, die einer anderen Tasksequenz übergeordnet ist.
- Die Umgebung ist global. Wenn eine Variable beispielsweise von der übergeordneten Tasksequenz festgelegt und dann von der untergeordneten Tasksequenz geändert wird, bleibt die Änderung der Variablen im weiteren Verlauf bestehen. Wenn die untergeordnete Tasksequenz eine neue Variable erstellt, ist die Variable ebenso für die restlichen Schritte in der übergeordneten Tasksequenz verfügbar.
- Statusmeldungen werden in der Regel für einen einzelnen Tasksequenzvorgang gesendet.
- Die Tasksequenzen schreiben Einträge in die Datei „smsts.log“, mit neuen Protokolleinträgen, die den Start einer untergeordneten Tasksequenz deutlich machen.
- Wenn untergeordnete Tasksequenzen in Technical Preview für Configuration Manager, Version 1704, auf ein Paket verweisen, und Sie die übergeordnete Tasksequenz vom Software Center aus ausführen, findet der Client den Paketinhalt nicht, wenn die untergeordnete Tasksequenz ausgeführt wird. In diesem Szenario müssen Sie die Tasksequenz von Medien aus ausführen (Startmedien, PXE usw.).  

    Wenn die untergeordnete Tasksequenz Schritte wie **Befehlszeile ausführen** (ohne Paketreferenz), **Format**, **BitLocker** usw. verwendet, wird die Tasksequenz erfolgreich vom Software Center aus ausgeführt.

### <a name="to-add-a-child-task-sequence-to-a-task-sequence"></a>So fügen Sie eine untergeordnete Tasksequenz einer Tasksequenz hinzu
1. Klicken Sie im Tasksequenz-Editor auf **Hinzufügen**, wählen Sie **Allgemein** aus, und klicken Sie auf **Tasksequenz ausführen**.
2. Klicken Sie auf **Durchsuchen**, um die untergeordnete Tasksequenz auszuwählen.  

## <a name="reload-boot-images-with-current-windows-pe-version"></a>Neuladen von Startimages mit der aktuellen Version von Windows PE
Beim Ausführen von **Verteilungspunkte aktualisieren** auf einem ausgewählten Startimage können Sie jetzt wahlweise die neueste Version von Windows PE neu in das Startimage laden (aus dem Installationsverzeichnis von Windows ADK). Die Seite **Allgemein** des Assistenten enthält Informationen über die auf dem Standortserver installierte Windows ADK-Version, die Windows ADK-Version, von der aus Windows PE im Startimage verwendet wurde, und die Version des Configuration Manager-Clients. Anhand dieser Informationen können Sie entscheiden, ob Sie das Startimage erneut laden möchten. Darüber hinaus wurde eine neue Spalte hinzugefügt (**Clientversion**), die angezeigt wird, wenn Sie Startimages im Knoten **Startimages** anzeigen, damit Sie wissen, welche Version des Configuration Manager-Clients jedes Startimage verwendet.

### <a name="to-reload-a-boot-image-with-the-current-windows-pe-version"></a>So laden Sie ein Startimage mit der aktuellen Version von Windows PE neu

1. Navigieren Sie in der Configuration Manager-Konsole zu **Softwarebibliothek** > **Betriebssysteme** > **Startimages**.
2. Wählen Sie ein Startimage aus, und klicken Sie auf **Verteilungspunkte aktualisieren**.
3. Wählen Sie auf der Seite **Allgemein** des Assistenten die Option **Reload boot image using the current version of Windows PE from the installed Windows ADK** (Startimage mit der aktuellen Version von Windows PE aus dem installierten Windows ADK neu laden).

## <a name="improvements-to-operating-system-deployment"></a>Verbesserungen bei der Betriebssystembereitstellung
Basierend auf dem Feedback von Benutzern haben wir die folgenden Verbesserungen an der Betriebssystembereitstellung vorgenommen.

- [Neue Spalte **Betriebssystemversion** für Betriebssystemimages:](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/17558407-add-a-column-to-the-operating-system-images-node-f) Wir haben eine neue Spalte namens **Betriebssystemversion** hinzugefügt, um die Version des Betriebssystems für das Image anzuzeigen, wenn Sie Informationen in den Knoten **Betriebssystemabbilder** und **Betriebssystemaktualisierungspakete** abrufen. Nur die Version des ersten Indexes in der WIM-Datei wird angezeigt. Wechseln Sie zur Registerkarte **Details** für das Image, um Betriebssystemversionen für andere Indizes zu überprüfen.

- [Effizientere Protokollierung in „Smsts.log“:](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/16791919-stop-filling-smsts-log-with-useless) Ab dieser Version schreiben wir keine Einträge zu „CCM_CIVersionInfo.PolicyID“-Informationen mehr in die Datei „smsts.log“. Vor dieser Version konnte es viele Einträge mit diesen Informationen geben, wodurch es schwierig war, relevantere Informationen in der Protokolldatei zu finden.
