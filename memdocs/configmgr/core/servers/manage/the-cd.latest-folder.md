---
title: Ordner „CD.Latest“
titleSuffix: Configuration Manager
description: Enthält Informationen über den Vorgang, in dem Updates des Produkts aus der Configuration Manager-Konsole heraus bereitstellt werden.
ms.date: 03/07/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8db92d67-5d9c-4e9c-80d0-ae6fa0dd4817
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 577bfd865ad3872c386384c3bba95cb009ef83ec
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704048"
---
# <a name="the-cdlatest-folder-for-configuration-manager"></a>Der Ordner „CD.Latest“ für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Updates des Produkts können aus der Configuration Manager-Konsole heraus bereitgestellt werden. Zur Unterstützung dieser neuen Methode zur Aktualisierung von Configuration Manager ist ein neuer Ordner namens **CD.Latest** erstellt worden. Dieser Ordner enthält eine Kopie der Configuration Manager-Installationsdateien für die aktualisierte Version Ihrer Website.  

Der Ordner „CD.Latest“ enthält einen Ordner namens **Redist**, der die verteilbaren Dateien enthält, die während des Setupvorgangs heruntergeladen und verwendet werden. Diese Dateien sind der Version der Configuration Manager-Dateien zugeordnet, die sich im Ordner „CD.Latest“ befinden. Wenn Sie den Setupvorgang aus einem „CD.Latest“-Ordner ausführen, müssen Sie Dateien verwenden, die zu dieser Setup-Version passen. Sie können Setup entweder anweisen, neue und aktuelle Dateien von Microsoft herunterzuladen, oder die Dateien aus dem „Redist“-Ordner zu verwenden, der sich im „CD.Latest“-Ordner befindet.

Baselinemedien enthalten keinen **Redist**-Ordner. Der Standort erstellt den Ordner „Redist“ erst dann, wenn Sie ein Update von der Konsole aus installieren. Verwenden Sie in der Zwischenzeit den Redist-Ordner, den Sie auch bei der Installation von Standorten mit dem Baselinemedium verwendet haben.  

> [!TIP]  
> Stellen Sie sicher, dass aktuelle verteilbare Dateien verwendet werden. Falls Sie die Dateien noch nicht heruntergeladen haben, weisen Sie das Setupprogramm an, diese von Microsoft herunterzuladen.   

In den folgenden Szenarien wird der Ordner „CD.Latest“ an einem Standort der zentralen Verwaltung oder auf dem primären Standortserver erstellt oder aktualisiert:  

- Wenn Sie ein Update oder Hotfix aus der Configuration Manager-Konsole heraus installieren, erstellt oder aktualisiert der Standort den Ordner im Configuration Manager-Installationsordner.  

- Wenn Sie den integrierten Configuration Manager-Sicherungstask ausführen, erstellt oder aktualisiert der Standort den Ordner unter dem angegebenen Sicherungsordner.  

- Wenn Sie einen neuen Standort mithilfe der Baselinemedien installieren, erstellt der Standort den Ordner „CD.Latest“.


## <a name="supported-scenarios"></a>Unterstützte Szenarien

Die Quelldateien aus dem Ordner „CD.Latest“ werden für folgende Szenarien unterstützt:  

### <a name="backup-and-recovery"></a>Sicherung und Wiederherstellung
Verwenden Sie zum Wiederherstellen eines Standorts die Quelldateien aus einem CD.Latest-Ordner, der zu Ihrem Standort passt. Wenn Sie eine Standortsicherung mithilfe des integrierten Standortsicherungstask ausführen, wird der CD.Latest-Ordner als Teil der Sicherung eingeschlossen.

- Wenn Sie den Standort im Rahmen einer Standortwiederherstellung neu installieren, wird der Standort aus dem Ordner „CD.Latest“ installiert, der in der Sicherung enthalten ist. Diese Aktion installiert den Standort anhand der Dateiversionen, die der Standortsicherung und der Standortdatenbank entsprechen.  

    - Wenn Sie nicht auf die richtige Version des Ordners „CD.Latest“ zugreifen können, rufen Sie den CD.Latest-Ordner mit den richtigen Dateiversionen durch Installation eines Standorts in einer Testumgebung ab. Aktualisieren Sie dann diesen Standort so, das er mit der Version übereinstimmt, die Sie wiederherstellen möchten.  

    - Wenn Sie nicht über den richtigen Ordner „CD.Latest“ und dessen Inhalte verfügen, können Sie einen Standort nicht wiederherstellen. In diesem Fall müssen Sie den Standort neu installieren.  

- Wenn Sie keinen Ordner „CD.Latest“ haben, aber einen funktionierenden untergeordneten primären Standort oder Standort der zentralen Verwaltung, können Sie diesen Standort als Referenzstandort für eine Standortwiederherstellung verwenden.  

### <a name="install-a-child-primary-site"></a>Installieren eines untergeordneten primären Standorts
Wenn Sie einen neuen untergeordneten primären Standort unterhalb eines Standorts der zentralen Verwaltung installieren möchten, auf dem ein oder mehrere In-Console-Updates installiert sind, verwenden Sie Setup und Quelldateien des Ordners „CD.Latest“ vom Standort der zentralen Verwaltung. Dieser Prozess verwendet die Installationsquelldateien, die mit der Version des Standorts der zentralen Verwaltung übereinstimmen. Weitere Informationen finden Sie unter [Verwenden des Setup-Assistenten zum Installieren von Standorten](../deploy/install/use-the-setup-wizard-to-install-sites.md).  

### <a name="expand-a-stand-alone-primary-site"></a>Erweitern eines eigenständigen primären Standorts
Wenn Sie einen eigenständigen primären Standort durch Installation eines neuen Standorts der zentralen Verwaltung erweitern, verwenden Sie das Setup und die Quelldateien des Ordners „CD.Latest“ vom primären Standort. Dieser Prozess verwendet die Installationsquelldateien, die mit der Version des primären Standorts übereinstimmen. Weitere Informationen finden Sie unter [Erweitern eines eigenständigen primären Standorts](../deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand).

### <a name="install-a-secondary-site"></a>Installieren eines sekundären Standorts
<!-- SCCMDocs-pr issue #3164 -->
Wenn Sie einen neuen sekundären Standort unterhalb eines primären Standorts installieren möchten, auf dem ein oder mehrere In-Console-Updates installiert sind, verwenden Sie die Quelldateien des Ordners „CD.Latest“ des primären Standorts. 

Weitere Informationen finden Sie unter [Installieren eines sekundären Standorts](../deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_secondary). 


## <a name="unsupported-scenarios"></a>Nicht unterstützte Szenarien

Die aktualisierten „CD.Latest“-Quelldateien werden nicht unterstützt für:  

- Installieren eines neuen Standorts für eine neue Hierarchie  
- Upgrade eines System Center 2012 Configuration Manager-Standorts auf Configuration Manager (Current Branch)
- Installieren von Configuration Manager-Clients
- Installieren von Configuration Manager-Konsolen
