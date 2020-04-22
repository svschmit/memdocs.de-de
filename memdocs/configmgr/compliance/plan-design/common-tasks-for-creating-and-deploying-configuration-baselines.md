---
title: 'Allgemeine Aufgaben für Konfigurationsbaselines '
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Configuration Manager-Konfigurationsbaselines erstellen und bereitstellen.
ms.date: 07/12/2017
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 4bb6afeb-d267-4f9b-ade2-26e5400c223b
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 52e83639029db9eeb4ef64657e70e3dc11aab8f2
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692258"
---
# <a name="common-tasks-for-creating-and-deploying-configuration-baselines-with-configuration-manager"></a>Allgemeine Aufgaben zum Erstellen und Bereitstellen von Konfigurationsbaselines mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Dieses Thema enthält häufige Szenarios, mit deren Hilfe Sie mehr über das Erstellen und Bereitstellen von Configuration Manager-Konfigurationsbaselines erfahren.  

 Wenn Sie bereits mit Konformitätseinstellungen vertraut sind, finden Sie eine ausführliche Dokumentation zu allen verwendbaren Funktionen in den Themen [Erstellen von Konfigurationsbaselines](../../compliance/deploy-use/create-configuration-baselines.md) und [Bereitstellen von Konfigurationsbaselines](../../compliance/deploy-use/deploy-configuration-baselines.md).  

 Bevor Sie beginnen, lesen Sie [Erste Schritte mit Kompatibilitätseinstellungen](../../compliance/get-started/get-started-with-compliance-settings.md), um einige Grundlagen der Kompatibilitätseinstellungen zu erfahren, und lesen Sie zudem [Planen und Konfigurieren von Kompatibilitätseinstellungen](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md), um jegliche notwendigen Voraussetzungen zu implementieren.  

## <a name="create-a-configuration-baseline"></a>Erstellen einer Konfigurationsbaseline  
 In diesem Beispiel haben Sie ein Konfigurationselement ausschließlich für Windows 10-PCs erstellt, auf denen der Configuration Manager-Client ausgeführt wird.  

 Dieses Konfigurationselement erzwingt ein erforderliches Kennwort mit mindestens 6 Zeichen auf Windows 10-PCs. Das Konfigurationselement hat den Namen **Windows 10 Password Enforcement**.  

Mit dem folgenden Verfahren fügen Sie dieses Konfigurationselement zu einer Konfigurationsbaseline hinzu, um es für die Bereitstellung vorzubereiten.  

1. Klicken Sie in der Configuration Manager-Konsole auf **Assets und Konformität** > **Konformitätseinstellungen** > **Konfigurationsbaselines**.  

2. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Konfigurationsbaseline erstellen**.  

3. Konfigurieren Sie im Dialogfeld **Konfigurationsbaseline erstellen** die folgenden Einstellungen:  

   -   **Name** : Geben Sie **Windows 10 Passwords** (oder einen anderen Namen Ihrer Wahl) ein.  

4. Klicken Sie auf **Hinzufügen** > **Konfigurationselemente**.  

5. Wählen Sie im Dialogfeld **Konfigurationselemente hinzufügen** das zuvor erstellte Konfigurationselement **Windows 10 Password Enforcement** aus, und klicken Sie dann auf **Hinzufügen**.  

6. Klicken Sie auf „OK“, um das Dialogfeld **Konfigurationselemente hinzufügen** zu schließen und zum Dialogfeld **Konfigurationsbaseline erstellen** zurückzukehren.

7. Klicken Sie auf **OK** , um das Dialogfeld **Konfigurationsbaseline erstellen** zu schließen.  

   Sie sehen die Konfigurationsbaseline jetzt im Knoten **Konfigurationsbaselines** der Configuration Manager-Konsole.  

## <a name="deploy-the-configuration-baseline"></a>Bereitstellen der Konfigurationsbaseline  
 In diesem Beispiel stellen Sie die im vorherigen Verfahren erstellte Konfigurationsbaseline für eine Sammlung von Computern bereit.  

1. Klicken Sie in der Configuration Manager-Konsole auf **Assets und Konformität** > **Konformitätseinstellungen** > **Konfigurationsbaselines**.  

2. Wählen Sie aus der Liste der Konfigurationsbaselines **Windows 10 Passwords**aus.  

3. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Bereitstellung** auf **Bereitstellen**.  

4. Konfigurieren Sie im Dialogfeld **Konfigurationsbaselines bereitstellen** die folgenden Einstellungen:  

   -   **Ausgewählte Konfigurationsbaselines** : Stellen Sie sicher, dass die Konfigurationsbaseline **Windows 10 Passwords** automatisch dieser Liste hinzugefügt wurde.  

   -   **Nicht konforme Regeln wiederherstellen, falls dies unterstützt wird**: Aktivieren Sie dieses Kontrollkästchen, um sicherzustellen, dass die Einstellungen von Configuration Manager wiederhergestellt werden, falls auf Zielgeräten nicht die richtigen Einstellungen vorhanden sind.  

   -   **Sammlung**: Klicken Sie auf **Durchsuchen**, um die Sammlung von Computern auszuwählen, auf denen die Konfigurationsbaseline ausgewertet und die Konformität wiederhergestellt wird. In diesem Beispiel wurde die Konfigurationsbaseline für die integrierte Sammlung **Alle Desktop- und Serverclients** bereitgestellt.  

       > [!TIP]  
       >  Es ist unerheblich, ob die ausgewählte Sammlung Computer oder Geräte enthält, auf denen nicht Windows 10 ausgeführt wird. Solange Sie im erstellten Konfigurationselement unterstützte Plattformen konfiguriert haben, wird nur die Konformität von Windows 10-PCs ausgewertet.  

   -   Konfigurieren Sie bei Bedarf den Zeitplan, nach dem die Konfigurationsbaseline ausgewertet wird. Andernfalls behalten Sie die Standardeinstellung **7 Tage**bei.  

5. Klicken Sie auf **OK** , um das Dialogfeld **Konfigurationsbaselines bereitstellen** zu schließen und die Bereitstellung zu erstellen.  

   Um einen kurzen Blick auf die Kompatibilitätsstatistik für diese Bereitstellung zu werfen, klicken Sie im Arbeitsbereich **Überwachung** auf **Bereitstellungen**. Am unteren Bildschirmrand wird ein Diagramm zur **Konformitätsstatistik** angezeigt.  

## <a name="next-steps"></a>Nächste Schritte 

Ausführlichere Informationen zum Überwachen von Konfigurationsbaselines finden Sie unter [Überwachen von Konformitätseinstellungen](../../compliance/deploy-use/monitor-compliance-settings.md).  
