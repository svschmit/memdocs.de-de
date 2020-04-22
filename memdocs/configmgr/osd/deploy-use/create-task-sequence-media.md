---
title: Tasksequenzmedien erstellen
titleSuffix: Configuration Manager
description: Erstellen von Tasksequenzmedien zum Bereitstellen eines Betriebssystems auf einem Zielcomputer in Ihrer Configuration Manager-Umgebung
ms.date: 05/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 90498b4b-6a9b-43cd-b465-1d6c9a52df1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 87d5df6edee2adba32f1a49b8e867e930386b4df
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690598"
---
# <a name="create-task-sequence-media"></a>Tasksequenzmedien erstellen

*Gilt für: Configuration Manager (Current Branch)*

Mithilfe von Medien können Sie ein Betriebssystemimage von einem Referenzcomputer erfassen oder ein Betriebssystem auf einem Zielcomputer in Ihrer Configuration Manager-Umgebung bereitstellen. Sie können eine CD, einen DVD-Satz oder einen USB-Speicherstick als Medien erstellen.  

Medien werden überwiegend zur Betriebssystembereitstellung auf Zielcomputern ohne Netzwerkverbindung oder auf Zielcomputern verwendet, deren Verbindung mit dem Configuration Manager-Standort eine geringe Bandbreite aufweist. Sie können Medien jedoch auch zum Starten einer Betriebssystembereitstellung außerhalb eines vorhandenen Windows-Betriebssystems verwenden. Diese Methode ist nützlich, wenn kein Betriebssystem vorhanden ist, das Betriebssystem nicht funktioniert oder Sie die Festplatte neu partitionieren möchten.  

Zu den Bereitstellungsmedien gehören startbare Medien, eigenständige Medien und vorab bereitgestellte Medien. Der Inhalt der Medien ist unterschiedlich und hängt von dem verwendeten Medientyp ab. Eigenständige Medien enthalten beispielsweise die Tasksequenz, die das Betriebssystem bereitstellt. Andere Medientypen rufen Tasksequenzen aus dem Verwaltungspunkt ab.  

> [!IMPORTANT]  
> Zum Erstellen von Tasksequenzmedien müssen Sie ein Administrator auf dem Computer sein, auf dem Sie die Configuration Manager-Konsole ausführen. Wenn Sie kein Administrator sind, werden Sie zur Eingabe von Administratoranmeldeinformationen aufgefordert, wenn Sie den Assistenten zum Erstellen von Tasksequenzmedien starten.  


## <a name="capture-media"></a><a name="BKMK_PlanCaptureMedia"></a> Erfassungsmedien

Mithilfe von Erfassungsmedien können Sie ein Betriebssystemimage von einem Referenzcomputer erfassen. Die Erfassungsmedien enthalten das Startimage zum Starten des Referenzcomputers und die Tasksequenz zum Erfassen des Betriebssystemimages.

Weitere Informationen zum Erstellen von Erfassungsmedien finden Sie unter [Erstellen von Erfassungsmedien mit System Center Configuration Manager](create-capture-media.md).  


## <a name="bootable-media"></a><a name="BKMK_PlanBootableMedia"></a> Startbare Medien

Startbare Medien enthalten die folgenden Komponenten:

- Das Startimage
- Optionale [Prestart-Befehle](../understand/prestart-commands-for-task-sequence-media.md) und ihre erforderlichen Dateien
- Configuration Manager-Binärdateien

Beim Starten des Zielcomputers wird eine Verbindung mit dem Netzwerk hergestellt. Die Tasksequenz, das Betriebssystemimage sowie sämtlicher anderer erforderlicher Inhalt werden dann aus dem Netzwerk abgerufen. Da sich die Tasksequenz nicht auf den Medien befindet, brauchen Sie die Medien nicht neu zu erstellen, wenn Sie die Tasksequenz oder den Inhalt ändern.  

> [!IMPORTANT]  
> Die Pakete auf startbaren Medien sind nicht verschlüsselt. Schützen Sie den Paketinhalt mithilfe geeigneter Sicherheitsmaßnahmen vor dem Zugriff Unbefugter, etwa durch Hinzufügen eines Kennworts für die Medien.  

Weitere Informationen zum Erstellen von startbaren Medien finden Sie unter [Erstellen von startbaren Medien](create-bootable-media.md).  


## <a name="prestaged-media"></a><a name="BKMK_PlanPrestagedMedia"></a> Vorab bereitgestellte Medien

Mithilfe von vorab bereitgestellten Medien können Sie startbare Medien und ein Betriebssystemimage vor Beginn des Bereitstellungsprozesses auf einer Festplatte bereitstellen. Die vorab bereitgestellten Medien sind Windows-Imagedateien (WIM). Sie können vom Hersteller auf einem Bare-Metal-Computer oder in Ihrem Stagingzentrum ohne Verbindung mit der Configuration Manager-Produktionsumgebung installiert werden.  

Vorab bereitgestellte Medien enthalten das Startimage, mit dem der Zielcomputer gestartet wird, sowie das Betriebssystemimage, das auf den Zielcomputer angewendet wird. Sie können auch Anwendungen, Pakete und Treiberpakete als Teil der vorab bereitgestellten Medien angeben. Die Tasksequenz zur Bereitstellung des Betriebssystems ist nicht in den Medien enthalten. Wenn Sie eine Tasksequenz mit vorab bereitgestellten Medien bereitstellen, prüft der Client zunächst den lokalen Tasksequenzcache auf gültige Inhalte. Falls keine Inhalte gefunden werden oder die Inhalte geändert wurden, lädt der Client die Inhalte von einem Verteilungspunkt oder von einem Peer herunter.  

Vorab bereitgestellte Medien werden auf die Festplatte eines neuen Computers angewendet, bevor dieser an den Endbenutzer ausgeliefert wird. Wenn der Computer nach Anwendung der vorab bereitgestellten Medien zum ersten Mal gestartet wird, wird Windows PE gestartet. Es wird eine Verbindung mit einem Verwaltungspunkt hergestellt, um nach der Tasksequenz zum Abschließen der Betriebssystembereitstellung zu suchen.  

> [!IMPORTANT]  
> Die Pakete auf vorab bereitgestellte Medien sind nicht verschlüsselt. Schützen Sie den Paketinhalt mithilfe geeigneter Sicherheitsmaßnahmen vor dem Zugriff Unbefugter, etwa durch Hinzufügen eines Kennworts für die Medien.  

Weitere Informationen zum Erstellen von vorab bereitgestellten Medien finden Sie unter [Erstellen von vorab bereitgestellten Medien](create-prestaged-media.md).  


## <a name="stand-alone-media"></a><a name="BKMK_PlanStandaloneMedia"></a> Eigenständige Medien

Eigenständige Medien enthalten alles, was zur Bereitstellung des Betriebssystems erforderlich ist. Dazu gehören die Tasksequenz und sämtlicher anderer erforderlicher Inhalt. Da alle für die Bereitstellung des Betriebssystems erforderlichen Komponenten auf den eigenständigen Medien gespeichert sind, ist der Speicherplatzbedarf für eigenständige Medien größer als für andere Medientypen.  

Weitere Informationen zum Erstellen von eigenständigen Medien finden Sie unter [Erstellen von eigenständigen Medien](create-stand-alone-media.md).  


## <a name="considerations-when-using-https"></a>Überlegungen zur Verwendung von HTTPS

Wenn Sie Ihre Verwaltungs- und Verteilungspunkte für die Verwendung von HTTPS konfigurieren, erstellen Sie Startmedien und vorab bereitgestellte Medien an einem primären Standort und nicht am Standort der zentralen Verwaltung. Berücksichtigen Sie auch den folgenden Punkt, um besser bestimmen zu können, ob die Medien als dynamisch oder als standortbasiert konfiguriert werden müssen:  

- Zum Konfigurieren der Medien als dynamische Medien müssen alle primären Standorte über die Stammzertifizierungsstelle des Standorts verfügen, über den Sie die Medien erstellt haben. Sie können die Stammzertifizierungsstelle in alle primären Standorte der Hierarchie importieren.  

- Wenn primäre Standorte in Ihrer Configuration Manager-Hierarchie unterschiedliche Stammzertifizierungsstellen verwenden, müssen Sie an jedem Standort standortbasierte Medien verwenden.  
