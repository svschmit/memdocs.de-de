---
title: Endpoint Protection-Malwaredefinitionen von WSUS
titleSuffix: Configuration Manager
ms.date: 02/14/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: a34d9401-83e4-471d-8e23-b8042fc11c90
author: mestew
ms.author: mstewart
description: Erfahren Sie, wie Sie Windows Server Updates Services konfigurieren müssen, damit Definitionsupdates automatisch genehmigt werden.
manager: dougeby
ms.openlocfilehash: 301a3f318e836f2501a25ae65ebb61173b8e6231
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697208"
---
# <a name="enable-endpoint-protection-malware-definitions-to-download-from-windows-server-update-services-wsus-for-configuration-manager"></a>Aktivieren der Endpoint Protection-Schadsoftwaredefinitionen zum Herunterladen von Windows Server Update Services (WSUS) für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

 Wenn Sie WSUS verwenden, um die Antischadsoftwaredefinitionen auf dem neuesten Stand zu halten, können Sie eine Konfiguration zur automatischen Genehmigung von Definitionsupdates vornehmen. Obwohl die Verwendung von Configuration Manager-Softwareupdates die empfohlene Methode ist, um Definitionen auf dem neuesten Stand zu halten, können Sie auch WSUS konfigurieren, um Benutzern das manuelle Einleiten von Definitionsupdates zu ermöglichen. Verwenden Sie die folgenden Verfahren, um WSUS als eine Definitionsupdatequelle zu konfigurieren.

## <a name="to-synchronize-endpoint-protection-definition-updates-in-configuration-manager-software-updates"></a>So synchronisieren Sie Endpoint Protection-Definitionsupdates in den Configuration Manager-Softwareupdates

1. Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.

2. Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Standortkonfiguration**, und klicken Sie dann auf **Standorte**.

3. Wählen Sie den Standort mit dem Softwareupdatepunkt aus. Klicken Sie in der Gruppe **Einstellungen** auf **Standortkomponenten konfigurieren**und dann auf **Softwareupdatepunkt**.

4. Aktivieren Sie im Dialogfeld **Eigenschaften der Softwareupdatepunktkomponente** auf der Registerkarte **Klassifizierungen** das Kontrollkästchen **Definitionsupdates** .

5. Geben Sie die mit WSUS aktualisierten **Produkte** an:

   -   Für Windows 8.1 und frühere Versionen aktivieren Sie im Dialogfeld **Eigenschaften der Softwareupdatepunktkomponente** auf der Registerkarte **Produkte** das Kontrollkästchen **Forefront Endpoint Protection 2010** .

   -   Für Windows 10 und höhere Versionen aktivieren Sie auf der Registerkarte **Produkte** im Dialogfeld **Eigenschaften der Softwareupdatepunktkomponente** das Kontrollkästchen **Windows Defender**.

6. Klicken Sie auf **OK** , um das Dialogfeld **Eigenschaften von Softwareupdatepunkt-Komponente** zu schließen.

   Verwenden Sie das folgende Verfahren, um Endpoint Protection-Updates zu konfigurieren, wenn Ihr WSUS-Server nicht in Ihre Configuration Manager-Umgebung integriert ist.

## <a name="to-synchronize-endpoint-protection-definition-updates-in-standalone-wsus"></a>So synchronisieren Sie Endpoint Protection-Definitionsupdates in eigenständigem WSUS

1.  Erweitern Sie in der WSUS-Verwaltungskonsole den Bereich **Computer**, klicken Sie auf **Optionen**, und klicken Sie dann auf **Produkte und Klassifizierungen**.

2.  Geben Sie die mit WSUS aktualisierten **Produkte** an:

    -   Für Windows 8.1 und frühere Versionen aktivieren Sie im Dialogfeld **Eigenschaften der Softwareupdatepunktkomponente** auf der Registerkarte **Produkte** das Kontrollkästchen **Forefront Endpoint Protection 2010** .

    -   Für Windows 10 und höhere Versionen aktivieren Sie auf der Registerkarte **Produkte** im Dialogfeld **Eigenschaften der Softwareupdatepunktkomponente** das Kontrollkästchen **Windows Defender**.

3.  Aktivieren Sie im Dialogfeld **Produkte und Klassifizierungen** auf der Registerkarte **Klassifizierungen** die Kontrollkästchen **Definitionsupdates** und **Updates** .

## <a name="approving-definition-updates"></a>Genehmigen von Definitionsupdates
 Endpoint Protection-Definitionsupdates müssen genehmigt und auf den WSUS-Server heruntergeladen werden, bevor sie Clients, die die Liste der verfügbaren Updates anfordern, angeboten werden. Clients stellen eine Verbindung mit dem WSUS-Server her, um nach anwendbaren Updates zu suchen, und fordern dann die neuesten genehmigten Definitionsupdates an.

### <a name="to-approve-definitions-and-updates-in-wsus"></a>So genehmigen Sie Definitionen und Updates in WSUS

1. Klicken Sie in der WSUS-Verwaltungskonsole auf **Updates**, und klicken Sie dann auf **Alle Updates** oder auf die Klassifizierung der Updates, die Sie genehmigen möchten.

2. Klicken Sie in der Liste der Updates mit der rechten Maustaste auf die Updates, die Sie zur Installation genehmigen möchten, und klicken Sie dann auf **Genehmigen**.

3. Wählen Sie im Dialogfeld **Updates genehmigen** die Computergruppe aus, für die Sie die Updates genehmigen möchten, und klicken Sie dann auf **Für die Installation genehmigt**.

   Neben der manuellen Genehmigung können Sie auch eine Regel zur automatischen Genehmigung für Definitionsupdates und Endpoint Protection-Updates festlegen. Dadurch wird WSUS für die automatische Genehmigung von Endpoint Protection-Definitionsupdates konfiguriert, die von WSUS heruntergeladen wurden.

### <a name="to-configure-an-automatic-approval-rule"></a>So konfigurieren Sie eine Regel zur automatischen Genehmigung

1.  Klicken Sie in der WSUS-Verwaltungskonsole auf **Optionen**und dann auf **Automatische Genehmigungen**.

2.  Klicken Sie auf der Registerkarte **Updateregeln** auf **Neue Regel**.

3.  Aktivieren Sie im Dialogfeld **Regel hinzufügen** unter **Schritt 1: Eigenschaften auswählen** das Kontrollkästchen **Wenn ein Update in einer bestimmten Klassifizierung enthalten ist**.

4.  Klicken Sie unter **Schritt 2: Eigenschaften bearbeiten**auf **beliebige Klassifizierung**.

5.  Deaktivieren Sie alle Kontrollkästchen außer **Definitionsupdates**, und klicken Sie dann auf **OK**.

6.  Aktivieren Sie im Dialogfeld **Regel hinzufügen** unter **Schritt 1: Eigenschaften auswählen** das Kontrollkästchen **Wenn ein Update in einem bestimmten Produkt enthalten ist**.

7.  Klicken Sie unter **Schritt 2: Eigenschaften bearbeiten**auf **beliebiges Produkt**.

8.  Deaktivieren Sie alle Kontrollkästchen außer **Forefront Endpoint Protection** für Windows 8.1 und frühere Versionen bzw. **Windows Defender** für Windows 10 und höhere Versionen, und klicken Sie dann auf **OK**.

9. Geben Sie unter **Schritt 3: Namen angeben** einen Namen für die Regel ein, und klicken Sie dann auf **OK**.

10. Aktivieren Sie im Dialogfeld **Automatische Genehmigungen** das Kontrollkästchen für die neu erstellte Regel, und klicken Sie dann auf **Regel ausführen**.

> [!NOTE]
>  Um die Leistung auf dem WSUS-Server und den Clientcomputern zu maximieren, lehnen Sie alte Definitionsupdates ab. Zu diesem Zweck können Sie die automatische Genehmigung für Revisionen und automatische Ablehnung abgelaufener Updates konfigurieren. Weitere Informationen finden Sie im [Microsoft Knowledge Base-Artikel 938947](https://go.microsoft.com/fwlink/p/?LinkId=204078).
> 
> [!div class="button"]
> [Nächster Schritt >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Zurück >](endpoint-configure-alerts.md)
