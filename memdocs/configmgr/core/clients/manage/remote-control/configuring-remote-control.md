---
title: Konfigurieren der Remotesteuerung
titleSuffix: Configuration Manager
description: Hier erhalten Sie Informationen zum Einrichten der Remotesteuerung in Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 45affc27-aa11-4249-9493-082ac23a3a3d
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 78f74a9659a011defd50e6ab0e9e1cfe85eec16b
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82076729"
---
# <a name="configuring-remote-control-in-configuration-manager"></a>Konfigurieren der Remotesteuerung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

 In diesem Verfahren wird die Konfiguration der Clientstandardeinstellungen für die Remotesteuerung beschrieben. Diese Einstellungen gelten für alle Computer in der Hierarchie. Wenn diese Einstellungen nur auf manche Computer angewendet werden sollen, weisen Sie eine benutzerdefinierte Geräteclienteinstellung einer Sammlung mit diesen Computern zu. Weitere Informationen finden Sie unter [Konfigurieren von Clienteinstellungen](../../../../core/clients/deploy/configure-client-settings.md). 

Für die Verwendung der Remoteunterstützung oder des Remotedesktops müssen sie auf dem Computer, auf dem die Configuration Manager-Konsole ausgeführt wird, installiert und konfiguriert sein. Weitere Informationen zum Installieren und Konfigurieren der Remoteunterstützung oder des Remotedesktops finden Sie in der Windows-Dokumentation.  

#### <a name="to-enable-remote-control-and-configure-client-settings"></a>So aktivieren Sie die Remotesteuerung und konfigurieren die Clienteinstellungen  

1. Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** > **Clienteinstellungen** > **Clientstandardeinstellungen** aus.  

2. Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.  

3. Wählen Sie im Dialogfeld **Standard** die Option **Remotetools** aus.  

4. Konfigurieren Sie die Remotesteuerungs-, Remoteunterstützungs- und Remotedesktop-Clienteinstellungen. Eine Liste der Remotetools-Clienteinstellungen, die Sie konfigurieren können, finden Sie unter [Remotetools](../../../../core/clients/deploy/about-client-settings.md#remote-tools).  

   Sie können den Firmennamen ändern, der im Dialogfeld **ConfigMgr-Remotesteuerung** angezeigt wird, indem Sie in den Clienteinstellungen **Computer-Agent** einen Wert für **Im Softwarecenter angezeigter Organisationsname** konfigurieren.  

   Die Clientcomputer werden beim nächsten Download der Clientrichtlinien mit diesen Einstellungen konfiguriert. Informationen zum Initiieren des Richtlinienabrufs für einen einzelnen Client finden Sie unter [How to manage Clients (Verwalten von Clients)](../../../../core/clients/manage/manage-clients.md).  

#### <a name="enable-keyboard-translation"></a>Aktivieren der Tastaturübersetzung

Standardmäßig überträgt Configuration Manager die Schlüsselposition vom Standort des anzeigenden Benutzers an den Standort des freigebenden Benutzers. Dies kann zu Problemen führen, wenn die Tastaturkonfiguration des anzeigenden Benutzers von der des freigebenden Benutzers abweicht. Beispielsweise würde ein anzeigender Benutzer mit einer englischen Tastatur ein „A“ eingeben, die französische Tastatur des freigebenden Benutzers würde jedoch ein „Q“ bereitstellen. Sie haben jetzt die Möglichkeit, die Remotesteuerung so zu konfigurieren, dass das Zeichen selbst von der Tastatur des anzeigenden Benutzers an den freigebenden Benutzer übertragen wird. Beim freigebenden Benutzer kommt das an, was der anzeigende Benutzer einzugeben beabsichtigt.

Wählen Sie zum Aktivieren der Tastaturübersetzung in **Configuration Manager-Remotesteuerung** **Aktion** und **Enable keyboard translation** (Tastaturübersetzung aktivieren) aus, um die Schlüsselposition zu übertragen.

> [!NOTE]
>
> Spezielle Schlüssel wie z.B. ~!#@$% werden nicht richtig übersetzt.


## <a name="keyboard-shortcuts-for-the-remote-control-viewer"></a>Tastenkombinationen für den Remotesteuerungsviewer

|Tastenkombination|Beschreibung|  
|-----------------------|-----------------|  
|ALT+BILD-AUF|Wechselt zwischen gerade ausgeführten Programmen von links nach rechts.|  
|ALT+BILD-AB|Wechselt zwischen gerade ausgeführten Programmen von rechts nach links.|  
|ALT+EINFG|Wechselt zwischen gerade ausgeführten Programmen in der Reihenfolge, in der sie geöffnet wurden.|  
|ALT+POS1|Zeigt das Menü **Start** an.|  
|STRG+ALT+ENDE|Zeigt das Dialogfeld "Windows-Sicherheit" an (STRG+ALT+ENTF).|  
|ALT+ENTF|Zeigt das Windows-Menü an.|  
|STRG+ALT+Minuszeichen (auf der Zehnertastatur)|Kopiert das aktive Fenster des lokalen Computers in die Zwischenablage des Remotecomputers.|  
|STRG+ALT+Pluszeichen (auf der Zehnertastatur)|Kopiert den gesamten Fensterbereich des lokalen Computers in die Zwischenablage des Remotecomputers.|  
