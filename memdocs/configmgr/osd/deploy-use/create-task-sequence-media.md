---
title: Tasksequenzmedien erstellen
titleSuffix: Configuration Manager
description: Erstellen von Tasksequenzmedien zum Bereitstellen eines Betriebssystems auf einem Zielcomputer in Ihrer Configuration Manager-Umgebung
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: 90498b4b-6a9b-43cd-b465-1d6c9a52df1c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: bf7ce32ed9e126b5526c68b7da03cf44d9b5062d
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125167"
---
# <a name="create-task-sequence-media"></a>Tasksequenzmedien erstellen

*Gilt für: Configuration Manager (Current Branch)*

Mithilfe von Medien können Sie ein Betriebssystemimage von einem Referenzcomputer erfassen oder ein Betriebssystem auf einem Zielcomputer in Ihrer Configuration Manager-Umgebung bereitstellen. Sie können eine CD, einen DVD-Satz oder einen USB-Speicherstick als Medien erstellen.

Medien werden überwiegend zur Betriebssystembereitstellung auf Computern ohne Netzwerkverbindung verwendet oder auf Computern, deren Verbindung mit der Site eine geringe Bandbreite aufweist. Sie können Medien jedoch auch zum Starten einer Betriebssystembereitstellung außerhalb eines vorhandenen Windows-Betriebssystems verwenden. Diese Methode ist nützlich, wenn kein Betriebssystem vorhanden ist, das Betriebssystem nicht funktioniert oder Sie den Datenträger neu partitionieren möchten.

Zu den Bereitstellungsmedien gehören startbare Medien, eigenständige Medien und vorab bereitgestellte Medien. Der Inhalt der Medien ist unterschiedlich und hängt von dem verwendeten Medientyp ab. Eigenständige Medien enthalten beispielsweise die Tasksequenz, die das Betriebssystem bereitstellt. Andere Medientypen rufen Tasksequenzen aus dem Verwaltungspunkt ab.

> [!IMPORTANT]
> Zum Erstellen von Tasksequenzmedien müssen Sie ein Administrator auf dem Computer sein, auf dem Sie die Configuration Manager-Konsole ausführen. Wenn Sie kein Administrator sind, werden Sie zur Eingabe von Administratoranmeldeinformationen aufgefordert, wenn Sie den Assistenten zum Erstellen von Tasksequenzmedien starten.

## <a name="capture-media"></a><a name="BKMK_PlanCaptureMedia"></a> Erfassungsmedien

Mithilfe von Erfassungsmedien können Sie ein Betriebssystemimage von einem Referenzcomputer erfassen. Die Erfassungsmedien enthalten das Startimage zum Starten des Referenzcomputers und die Tasksequenz zum Erfassen des Betriebssystemimages.

## <a name="bootable-media"></a><a name="BKMK_PlanBootableMedia"></a> Startbare Medien

Startbare Medien enthalten die folgenden Komponenten:

- Das Startimage
- Optionale [Prestart-Befehle](../understand/prestart-commands-for-task-sequence-media.md) und ihre erforderlichen Dateien
- Configuration Manager-Binärdateien

Beim Starten des Zielcomputers wird eine Verbindung mit dem Netzwerk hergestellt. Die Tasksequenz, das Betriebssystemimage sowie sämtlicher anderer erforderlicher Inhalt werden dann aus dem Netzwerk abgerufen. Da sich die Tasksequenz nicht auf den Medien befindet, brauchen Sie die Medien nicht neu zu erstellen, wenn Sie die Tasksequenz oder den Inhalt ändern.  

> [!IMPORTANT]  
> Die Pakete auf startbaren Medien sind nicht verschlüsselt. Schützen Sie den Paketinhalt mithilfe geeigneter Sicherheitsmaßnahmen vor dem Zugriff Unbefugter, etwa durch Hinzufügen eines Kennworts für die Medien.  

Ab Version 2006 können startbare Medien cloudbasierte Inhalte herunterladen. Das Gerät benötigt weiterhin eine Intranetverbindung mit dem Verwaltungspunkt. Der Inhalt kann von einem inhaltsfähigen Cloudverwaltungsgateway (Cloud Management Gateway, CMG) oder einem Cloudverteilungspunkt stammen.<!--6209223--> Weitere Informationen finden Sie unter [Unterstützung für cloudbasierten Inhalt](use-bootable-media-to-deploy-windows-over-the-network.md#support-for-cloud-based-content).

## <a name="prestaged-media"></a><a name="BKMK_PlanPrestagedMedia"></a> Vorab bereitgestellte Medien

Mithilfe von vorab bereitgestellten Medien können Sie startbare Medien und ein Betriebssystemimage vor Beginn des Bereitstellungsprozesses auf einer Festplatte bereitstellen. Die vorab bereitgestellten Medien sind Windows-Imagedateien (WIM). Der Hersteller kann sie während des Buildprozesses auf dem Bare-Metal-Computer installieren. Sie können sie auch in einem Staging Center verwenden, das nicht mit der Configuration Manager-Produktionsumgebung verbunden ist.

Vorab bereitgestellte Medien enthalten das Startimage, mit dem der Zielcomputer gestartet wird, sowie das Betriebssystemimage, das auf den Zielcomputer angewendet wird. Sie können auch Anwendungen, Pakete und Treiberpakete als Teil der vorab bereitgestellten Medien angeben. Die Tasksequenz zur Bereitstellung des Betriebssystems ist nicht in den Medien enthalten. Wenn Sie eine Tasksequenz mit vorab bereitgestellten Medien bereitstellen, prüft der Client zunächst den lokalen Tasksequenzcache auf gültige Inhalte. Falls keine Inhalte gefunden werden oder die Inhalte geändert wurden, lädt der Client die Inhalte von einem Verteilungspunkt oder von einem Peer herunter.  

Sie wenden vorab bereitgestellte Medien auf die Festplatte eines neuen Computers an, bevor Sie den Computer an den Benutzer ausliefern. Wenn der Computer nach Anwendung der vorab bereitgestellten Medien zum ersten Mal gestartet wird, wird Windows PE gestartet. Es wird eine Verbindung mit einem Verwaltungspunkt hergestellt, um nach der Tasksequenz zum Abschließen der Betriebssystembereitstellung zu suchen.  

> [!IMPORTANT]
> Die Pakete auf vorab bereitgestellte Medien sind nicht verschlüsselt. Schützen Sie den Paketinhalt mithilfe geeigneter Sicherheitsmaßnahmen vor dem Zugriff Unbefugter, etwa durch Hinzufügen eines Kennworts für die Medien.

## <a name="standalone-media"></a><a name="BKMK_PlanStandaloneMedia"></a> Eigenständige Medien

Eigenständige Medien enthalten alles, was zur Bereitstellung des Betriebssystems erforderlich ist. Dazu gehören die Tasksequenz und sämtlicher anderer erforderlicher Inhalt. Da sich alles auf den Medien befindet, ist der erforderliche Speicherplatz größer als für andere Medientypen.

## <a name="considerations-when-using-https"></a>Überlegungen zur Verwendung von HTTPS

Wenn Sie Ihre Verwaltungs- und Verteilungspunkte für die Verwendung von HTTPS konfigurieren, erstellen Sie Startmedien und vorab bereitgestellte Medien an einem primären Standort und nicht am Standort der zentralen Verwaltung. Berücksichtigen Sie auch den folgenden Punkt, um besser bestimmen zu können, ob die Medien als dynamisch oder als standortbasiert konfiguriert werden müssen:  

- Zum Konfigurieren der Medien als dynamische Medien müssen alle primären Standorte über die Stammzertifizierungsstelle des Standorts verfügen, über den Sie die Medien erstellt haben. Sie können die Stammzertifizierungsstelle in alle primären Standorte der Hierarchie importieren.  

- Wenn primäre Standorte in Ihrer Configuration Manager-Hierarchie unterschiedliche Stammzertifizierungsstellen verwenden, müssen Sie an jedem Standort standortbasierte Medien verwenden.  

## <a name="next-steps"></a>Nächste Schritte

- [Erstellen von Erfassungsmedien](create-capture-media.md)

- [Erstellen startbarer Medien](create-bootable-media.md)

- [Erstellen von vorab bereitgestellten Medien](create-prestaged-media.md)

- [Erstellen eigenständiger Medien](create-stand-alone-media.md)
