---
title: Erstellen eines Images für ein OEM-Vorinstallations- oder lokales Depot
titleSuffix: Configuration Manager
description: Verwenden Sie vorab bereitgestellte Medienbereitstellungen zum Reduzieren des Netzwerkverkehrs, während Sie ein Betriebssystem für Computer bereitstellen, die nicht vollständig bereitgestellt sind.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: a7d3df90-062d-4d57-9e9d-e137d3e7cd7f
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5c4d445d18b9e239ace673199f6a7d0f26d10a42
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707288"
---
# <a name="create-an-image-for-an-oem-in-factory-or-a-local-depot-with-configuration-manager"></a>Erstellen eines Images für ein OEM-Vorinstallations- oder lokales Depot mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Bei Bereitstellungen mit vorab bereitgestellten Medien in Configuration Manager können Sie ein Betriebssystem für Computer bereitstellen, die nicht vollständig bereitgestellt sind. Bei vorab bereitgestellten Medien handelt es sich um eine WIM-Datei (Windows Imaging Format), die vom Hersteller (OEM) auf einem Computer ohne Betriebssystem oder im Staging Center eines Unternehmens ohne Verbindung zur Configuration Manager-Umgebung installiert werden kann. Später wird der Computer in der Configuration Manager-Umgebung mithilfe des auf den Medien bereitgestellten Startimages gestartet, auf den vorab bereitgestellten Medien wird eine Hashüberprüfung ausgeführt, um die Gültigkeit sicherzustellen, und wird der Computer mit dem Verwaltungspunkt des Standorts verbunden und der Downloadvorgang mithilfe der dort verfügbaren Tasksequenzen abgeschlossen.


Durch diese Bereitstellungsmethode wird der Netzwerkdatenverkehr reduziert, da das Startabbild und Betriebssystemabbild bereits auf dem Zielcomputer vorhanden sind. Sie können auch Anwendungen, Pakete und Treiberpakete als vorab bereitgestellte Medien angeben. Nachdem das Betriebssystem auf dem Computer installiert wurde, wird der Cache der Tasksequenz zunächst auf Anwendungen, Pakete oder Treiberpakete geprüft. Wenn kein Inhalt gefunden oder der Inhalt geprüft wurde, wird er von einem Verteilungspunkt heruntergeladen, der in dem vorab bereitgestellten Medium konfiguriert wurde, und anschließend installiert.  

 Sie können vorab bereitgestellte Medien in den folgenden Szenarios für die Betriebssystembereitstellung verwenden:  

- [Installieren einer neuen Version von Windows auf einem neuen Computer (Bare-Metal)](install-new-windows-version-new-computer-bare-metal.md)  

- [Ersetzen eines vorhandenen Computers und Übertragen von Einstellungen](replace-an-existing-computer-and-transfer-settings.md)  

  Führen Sie die Schritte in einem der Betriebssystembereitstellungsszenarien aus, und verwenden Sie dann die folgenden Abschnitte, um die vorab bereitgestellten Medien vorzubereiten und zu erstellen.  

## <a name="configure-deployment-settings"></a>Konfigurieren von Bereitstellungseinstellungen  
 Wenn Sie vorab bereitgestellte Medien verwenden, um den Bereitstellungsprozess für das Betriebssystem zu starten, müssen Sie die Bereitstellung konfigurieren, um das Betriebssystem für die Medien zur Verfügung zu stellen. Sie können dies auf der Seite der **Bereitstellungseinstellungen** des Assistenten oder der Registerkarte für die **Bereitstellungseinstellungen** in den Eigenschaften für die Bereitstellung konfigurieren.  Konfigurieren Sie eine der folgenden Optionen für die Einstellung **Verfügbar machen für** :  

-   **Configuration Manager-Clients, Medien und PXE**  

-   **Nur Medien und PXE**  

-   **Nur Medien und PXE (ausgeblendet)**  

## <a name="create-the-prestaged-media"></a>Erstellen der vorab bereitgestellten Medien  
 Erstellen der vorab bereitgestellten Mediendatei zum Versand an den OEM oder Ihr lokales Depot. Weitere Informationen finden Sie unter [Erstellen von vorab bereitgestellten Medien](create-prestaged-media.md).  

## <a name="send-the-prestaged-media-file-to-the-oem-or-local-depot"></a>Senden der vorab bereitgestellten Mediendatei an den OEM oder Ihr lokales Depot  
 Senden Sie die Medien an den OEM oder Ihr lokales Depot, um die Computer vorab bereitzustellen. Die vorab bereitgestellte Mediendatei wird auf einer formatierten Festplatte auf dem Computer installiert.  

## <a name="start-the-computer-to-install-the-operating-system"></a>Starten des Computers, um das Betriebssystem zu installieren  
 Die vorab bereitgestellte Mediendatei wird auf Computern installiert. Beim erstmaligen Starten des Computers wird die Betriebssysteminstallation gestartet.  
