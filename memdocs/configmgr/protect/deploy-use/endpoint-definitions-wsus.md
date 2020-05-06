---
title: Endpoint Protection-Malwaredefinitionen von WSUS
titleSuffix: Configuration Manager
ms.date: 04/23/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a34d9401-83e4-471d-8e23-b8042fc11c90
author: mestew
ms.author: mstewart
description: Erfahren Sie, wie Sie Windows Server Updates Services konfigurieren müssen, damit Definitionsupdates automatisch genehmigt werden.
manager: dougeby
ms.openlocfilehash: 235caff52b877177b92792bf8d9fb3a2007127a5
ms.sourcegitcommit: 2871a17e43b2625a5850a41a9aff447c8ca44820
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/24/2020
ms.locfileid: "82126020"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-wsus-for-configuration-manager"></a>Ermöglichen des Herunterladens aus WSUS für Configuration Manager durch Endpoint Protection-Schadsoftwaredefinitionen

*Gilt für: Configuration Manager (Current Branch)*

Wenn Sie WSUS verwenden, um die Antischadsoftwaredefinitionen auf dem neuesten Stand zu halten, können Sie eine Konfiguration zur automatischen Genehmigung von Definitionsupdates vornehmen. Obwohl die Verwendung von Configuration Manager-Softwareupdates die empfohlene Methode ist, um Definitionen auf dem neuesten Stand zu halten, können Sie auch WSUS als Methode konfigurieren, Benutzern das manuelle Updaten von Definitionen zu ermöglichen. Verwenden Sie die folgenden Verfahren, um WSUS als eine Definitionsupdatequelle zu konfigurieren.

## <a name="synchronize-definition-updates-for-configuration-manager"></a>Synchronisieren von Definitionsupdates für Configuration Manager

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und klicken Sie dann auf **Standorte**.

1. Wählen Sie den Standort mit dem Softwareupdatepunkt aus. Klicken Sie in der Gruppe **Einstellungen** des Menübands auf **Standortkomponenten konfigurieren** und dann auf **Softwareupdatepunkt**.

1. Wechseln Sie im Fenster **Eigenschaften der Softwareupdatepunktkomponente** zur Registerkarte **Klassifizierungen**. Klicken Sie auf **Definitionsupdates**.

1. Wechseln Sie zur Registerkarte **Produkte**, um die mit WSUS aktualisierten **Produkte** anzugeben.

    - Windows 10 und höher: Wählen Sie **Windows Defender** unter „Microsoft“ > „Windows“ aus.

    - Windows 8.1 und früher: Wählen Sie **System Center Endpoint Protection** unter „Microsoft“ > „Forefront“ aus.

1. Klicken Sie auf **OK**, um das Fenster **Eigenschaften der Softwareupdatepunktkomponente** zu schließen.

## <a name="synchronize-definition-updates-for-standalone-wsus"></a>Synchronisieren von Definitionsupdates für eigenständige WSUS-Server

Verwenden Sie das folgende Verfahren, um Endpoint Protection-Updates zu konfigurieren, wenn Ihr WSUS-Server nicht in Ihre Configuration Manager-Umgebung integriert ist.

1. Erweitern Sie in der WSUS-Verwaltungskonsole den Bereich **Computer**, klicken Sie auf **Optionen** und dann auf **Produkte und Klassifizierungen**.

1. Wechseln Sie zur Registerkarte **Produkte**, um die mit WSUS aktualisierten **Produkte** anzugeben.

    - Windows 10 und höher: Wählen Sie **Windows Defender** unter „Microsoft“ > „Windows“ aus.

    - Windows 8.1 und früher: Wählen Sie **System Center Endpoint Protection** unter „Microsoft“ > „Forefront“ aus.

1. Wechseln Sie zur Registerkarte **Klassifizierungen**. Klicken Sie auf **Definitionsupdates** und **Updates**.

## <a name="approve-definition-updates"></a>Genehmigen von Definitionsupdates

Endpoint Protection-Definitionsupdates müssen genehmigt und auf den WSUS-Server heruntergeladen werden, bevor sie Clients angeboten werden, die die Liste der verfügbaren Updates anfordern. Clients stellen eine Verbindung mit dem WSUS-Server her, um nach anwendbaren Updates zu suchen, und fordern dann die neuesten genehmigten Definitionsupdates an.

### <a name="approve-definitions-and-updates-in-wsus"></a>Genehmigen von Definitionen und Updates in WSUS

1. Klicken Sie in der WSUS-Verwaltungskonsole auf **Updates**. Klicken Sie dann auf **Alle Updates** oder auf die Klassifizierung der Updates, die Sie genehmigen möchten.

1. Klicken Sie in der Liste der Updates mit der rechten Maustaste auf die Updates, deren Installation Sie genehmigen möchten, und klicken Sie dann auf **Genehmigen**.

1. Wählen Sie im Fenster **Updates genehmigen** die Computergruppe aus, für die Sie die Updates genehmigen möchten, und klicken Sie dann auf **Für die Installation genehmigt**.

### <a name="configure-an-automatic-approval-rule"></a>Konfigurieren einer Regel zur automatischen Genehmigung

Sie können auch eine Regel zur automatischen Genehmigung für Definitionsupdates und Endpoint Protection-Updates festlegen. Dadurch wird WSUS für die automatische Genehmigung von Endpoint Protection-Definitionsupdates konfiguriert, die von WSUS heruntergeladen wurden.

1. Klicken Sie in der WSUS-Verwaltungskonsole auf **Optionen** und dann auf **Automatische Genehmigungen**.

1. Klicken Sie auf der Registerkarte **Updateregeln** auf **Neue Regel**.

1. Wählen Sie im Fenster **Regel hinzufügen** unter **Schritt 1: Eigenschaften auswählen** folgende Option aus: **Wenn ein Update in einer bestimmten Klassifizierung enthalten ist**.

    1. Klicken Sie unter **Schritt 2: Eigenschaften bearbeiten** auf **Beliebige Klassifizierung**.

    1. Deaktivieren Sie alle Optionen außer **Definitionsupdates**, und klicken Sie dann auf **OK**.

1. Wählen Sie im Fenster **Regel hinzufügen** unter **Schritt 1: Eigenschaften auswählen** folgende Option aus: **Wenn ein Update in einem bestimmten Produkt enthalten ist**.

    1. Klicken Sie unter **Schritt 2: Eigenschaften bearbeiten** auf **Beliebiges Produkt**.

    1. Deaktivieren Sie alle Optionen außer **System Center Endpoint Protection** für Windows 8.1 und frühere Versionen bzw. **Windows Defender** für Windows 10 und höhere Versionen. Klicken Sie dann auf **OK**.

1. Geben Sie unter **Schritt 3: Namen angeben** einen Namen für die Regel ein, und klicken Sie dann auf **OK**.

1. Wählen Sie im Dialogfeld **Automatische Genehmigungen** die neu erstellte Regel aus, und klicken Sie dann auf **Regel ausführen**.

> [!NOTE]
> Um die Leistung auf dem WSUS-Server und den Clientcomputern zu maximieren, lehnen Sie alte Definitionsupdates ab. Zu diesem Zweck können Sie die automatische Genehmigung für Revisionen und automatische Ablehnung abgelaufener Updates konfigurieren. Weitere Informationen finden Sie im [Microsoft-Support-Artikel 938947](https://support.microsoft.com/kb/938947).

> [!div class="nextstepaction"]
> [Erstellen und Bereitstellen von Richtlinien für Antischadsoftware für Endpoint Protection in Configuration Manager](endpoint-antimalware-policies.md)
