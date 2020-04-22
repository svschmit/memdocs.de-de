---
title: Installieren von Updates Publisher
titleSuffix: Configuration Manager
description: Installieren von System Center Updates Publisher in der Umgebung
ms.date: 08/22/2019
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.topic: conceptual
ms.assetid: ab5cda93-b67c-4aa5-904d-7b63ce790aa0
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 2f83e7207207496d69342a2322909e972ada5676
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81703848"
---
# <a name="install-updates-publisher"></a>Installieren von Updates Publisher

*Gilt für: System Center Updates Publisher*

Die Informationen in diesen Artikeln unterstützen Sie beim Herunterladen, Installieren und Einrichten von Updates Publisher zur Verwendung in Ihrer Configuration Manager-Umgebung.

## <a name="prerequisites-and-limitations"></a>Voraussetzungen und Einschränkungen
System Center Updates Publisher kann nur mit Configuration Manager verwendet werden. Dieses Tool ist nicht für die Verwendung mit eigenständigen WSUS-Hierarchien vorgesehen.

Die folgenden Abschnitte enthalten Informationen über die Anforderungen zur Installation und Verwendung von Updates Publisher sowie Einschränkungen und bekannte Probleme für die Verwendung.  

### <a name="operating-systems"></a>Betriebssysteme
Installieren Sie Updates Publisher auf einer 64-Bit-Version von folgenden Betriebssystemen und führen Sie es aus. Es gibt keine Mindestanforderungen in Bezug auf kumulative Updates oder Service Packs.

-   Windows Server 2016 (Standard, Datacenter)
-   Windows Server 2012 R2 (Standard, Datacenter)
-   Windows 10 (Pro, Education, Pro Education, Enterprise)
-   Windows 8.1 (Professional, Enterprise)

### <a name="prerequisites"></a>Voraussetzungen
Die folgenden Voraussetzungen gelten für Computer, auf denen Updates Publisher ausgeführt wird.

-   **64-Bit-Betriebssystem**: Auf dem Computer, auf dem Sie Updates Publisher installieren, muss ein 64-Bit-Betriebssystem ausgeführt werden.
-   **WSUS 6.2 oder höher:**
    -   Installieren Sie auf Windows Server die standardmäßige Verwaltungskonsole, um diese Anforderung zu erfüllen.
    -   Installieren Sie für Windows 10 und Windows 8.1 die [Remoteserver-Verwaltungstools (Remote Server Administration Tools, RSAT) für Windows-Betriebssysteme](https://support.microsoft.com/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems). Hierdurch werden die benötigten Supportdateien für die Verwendung von Updates Publisher (*API und PowerShell-Cmdlets* sowie *Benutzeroberfläche der Verwaltungskonsole*) installiert.
-   **Berechtigungen**:
    -   Installation: Lokaler Administrator
    -   Großteil der Vorgänge: Lokaler Benutzer
    -   Veröffentlichung oder Vorgänge mit WSUS: Mitglied der WSUS-Administratorengruppe auf dem WSUS-Server.

### <a name="supported-languages"></a>Unterstützte Sprachen
Updates Publisher ist nur in Englisch verfügbar, kann jedoch Updates für andere Sprachen verwalten. Die Sprachunterstützung hängt von der Aufgabe ab, z.B. Veröffentlichen, Erstellen oder Bearbeiten von Updates.

Beim Exportieren oder Veröffentlichen von Updates zeigt Updates Publisher den Titel und die Beschreibung des Softwareupdates basierend auf dem Gebietsschema des Computers an, auf dem Updates Publisher installiert ist.

Beispiel: Sie erstellen ein Softwareupdate mit einem englisch- und spanischsprachigen Titel.

-   Wenn Sie das Update auf einem Computer erstellen, dessen Gebietsschema Englisch ist, sehen Sie den Titel und die Beschreibung standardmäßig in englischer Sprache.
-   Wenn Sie das Update anschließend auf einen Computer exportieren oder auf einem Computer veröffentlichen, dessen Gebietsschema Spanisch ist, würde Sie auf diesem Computer Titel und Beschreibung in spanischer Sprache sehen.

### <a name="publishing"></a>Veröffentlichung
Bei der Veröffentlichung von Softwareupdates können Sie die Sprache der Softwareupdate-Binärdatei angeben. Sie können auch angeben, dass die Binärdatei sprachneutral ist. Folgende Sprachen werden unterstützt:

-   Arabisch
-   Chinesisch (Hongkong SAR)
-   und SharePoint 2010 angezeigten Optionen
-   Chinesisch (vereinfacht)
-   Tschechisch
-   Dänisch
-   Niederländisch
-   Englisch
-   Finnisch
-   Französisch
-   Deutsch
-   Griechisch
-   Hebräisch
-   Ungarisch
-   Italienisch
-   Japanisch
-   Koreanisch
-   Norwegisch
-   Polnisch
-   Portugiesisch
-   Portugiesisch (Brasilien)
-   Russisch
-   Spanisch
-   Schwedisch
-   Türkisch

### <a name="software-update-titles-and-descriptions"></a>Titel und Beschreibung von Softwareupdates
Für Titel und Beschreibungen von Softwareupdates werden folgende Sprachen unterstützt.

-   und SharePoint 2010 angezeigten Optionen
-   Chinesisch (vereinfacht)
-   Englisch
-   Französisch
-   Deutsch
-   Italienisch
-   Japanisch
-   Koreanisch
-   Portugiesisch (Brasilien)
-   Russisch
-   Spanisch

## <a name="install-updates-publisher"></a>Installieren von Updates Publisher
Rufen Sie die Datei **UpdatesPubliser.msi** zur Installation von System Center Updates Publisher über das [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=55543) ab.

Führen Sie zur Installation von Updates Publisher **UpdatesPublisher.msi** auf einem Computer aus, der die *Voraussetzungen* erfüllt. Das Installationsprogramm erstellt den folgenden Ordner, der die erforderlichen Dateien zum Ausführen von Updates Publisher enthält: %PROGRAMFILES%\Microsoft\UpdatesPublisher*.

Da dieser Ordner alle Dateien enthält, die zur Verwendung von Updates Publisher erforderlich sind, können Sie den Ordner und dessen Inhalte an einem neuen Speicherort oder auf einen anderen Computer kopieren und Updates Publisher dann von diesem Speicherort aus verwenden. Der neue Speicherort bzw. der andere Computer muss jedoch die Voraussetzung zum Ausführen von Updates Publisher erfüllen.

Um Updates Publisher zu starten, führen Sie nach der Installation **UpdatesPublisher.exe** im *UpdatesPublisher*-Ordner aus.

## <a name="next-steps"></a>Nächste Schritte
 Es wird empfohlen, nach der Installation von Updates Publisher die [Optionen für Updates Publisher zu konfigurieren](updates-publisher-options.md). Bevor Sie bestimmte Funktionen von Updates Publisher verwenden können, müssen Sie einige Optionen konfigurieren.

 Wenn Sie jedoch die Standardwerte verwenden möchten und nicht die Bereitstellung von Updates auf einem Updateserver oder auf verwalteten Geräten planen, können Sie direkt mit [Verwalten von Softwareupdatekatalogen](updates-publisher-catalogs.md) oder [Erstellen von Softwareupdates](create-updates-with-updates-publisher.md) fortfahren und eigenständig Updatekataloge erstellen.
