---
title: Importieren und Exportieren von Anwendungen
titleSuffix: Configuration Manager
description: Hier erfahren Sie, wie Sie Anwendungen in Configuration Manager für die Freigabe zwischen separaten Hierarchien importieren und exportieren.
ms.date: 05/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: dba00e54-9d5b-4f6b-916d-ead48c66e288
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b4ed1c10e23b75dc4478a0409d197015c98aff8b
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689438"
---
# <a name="import-and-export-applications"></a>Importieren und Exportieren von Anwendungen

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie Configuration Manager zum Importieren und Exportieren von Anwendungen zwischen zwei Hierarchien. Kopieren Sie beispielsweise eine Anwendung aus einer Testumgebung in eine Produktionsumgebung.

## <a name="export"></a>Exportieren

1. Wählen Sie in der Configuration Manager-Konsole den Knoten **Anwendungen** aus. Klicken Sie in der Menübandgruppe „Erstellen“ auf **Anwendung exportieren**.
1. Geben Sie auf der Anzeige **Allgemein** einen Pfad zu einer neuen ZIP-Datei an, in die die Anwendung exportiert werden soll. Legen Sie optional fest, ob *Abhängigkeiten, Ablösungsbeziehungen, Bedingungen und virtuelle Umgebungen* exportiert werden sollen, und wählen Sie aus, *welche Inhalte der ausgewählten Anwendungen und Abhängigkeiten exportiert werden sollen*.  Geben Sie bei Bedarf Administratorkommentare ein, und klicken Sie dann auf **Weiter**.
1. Überprüfen Sie, ob die Anwendungen und Abhängigkeiten auf der Seite **Zugehörige Objekte** aufgeführt werden, und klicken Sie auf **Weiter**.
1. Klicken Sie auf der Seite „Zusammenfassung“ auf **Weiter**.
1. Sobald der Prozess abgeschlossen ist, wird die ZIP-Datei erstellt, und Sie können den Assistenten schließen.

> [!IMPORTANT]
> Wenn Sie diese Anwendung in eine andere Umgebung kopieren möchten, kopieren Sie sowohl die ZIP-Datei als auch den Ordner, der diese enthält. Die ZIP-Datei muss sich im gleichen Verzeichnis wie der erstellte Ordner befinden.

## <a name="import"></a>Importieren

> [!NOTE]
> Sie können nur Anwendungen aus UNC-Pfaden importieren. Sie können Anwendungen nicht direkt von Ihrem Datenträger importieren.

1. Wählen Sie in der Configuration Manager-Konsole den Knoten **Anwendungen** aus. Klicken Sie in der Menübandgruppe „Erstellen“ auf **Anwendung importieren**.
1. Wählen Sie die ZIP-Datei aus, die Sie importieren möchten, und klicken Sie auf **Weiter**.
1. Im Fenster „Dateiinhalt“ wird gezeigt, was geschieht, wenn Sie die Anwendung importieren. Wählen Sie **Weiter** aus.
1. Überprüfen Sie die Anzeige „Zusammenfassung“, und klicken Sie auf **Weiter**.
1. Schließen Sie den Assistenten. Die Anwendung ist jetzt am Standort verfügbar.

## <a name="see-also"></a>Weitere Informationen:
 
Automatisieren Sie den Import und Export von Anwendungen mithilfe von PowerShell.

* [Import-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/import-cmapplication)
* [Export-CMApplication](https://docs.microsoft.com/powershell/module/configurationmanager/export-cmapplication)
