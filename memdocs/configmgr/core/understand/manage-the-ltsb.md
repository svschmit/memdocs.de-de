---
title: Verwalten des LTSB
titleSuffix: Configuration Manager
description: Unterschiede bei der Verwaltung von LTSB von System Center Configuration Manager
ms.date: 05/01/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8da2887a-fd8e-438c-b926-849c121f7fdf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 86e7579832a5a59c3609d24744eb646e1a4c1fd1
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706868"
---
# <a name="manage-the-long-term-servicing-branch-of-configuration-manager"></a>Verwalten von Long-Term Servicing Branch von Configuration Manager

*Gilt für: System Center Configuration Manager (Long-Term Servicing Branch)*

Wenn Sie Long-Term Servicing Branch (LTSB) von System Center Configuration Manager verwenden, können Sie anhand der folgenden Informationen wichtige Änderungen verstehen, die sich auf die Verwaltung Ihrer Infrastruktur auswirken.

Da LTSB Version 1606 von Current Branch entspricht (mit einigen Ausnahmen wie Intune-Integration und cloudbezogenen Features), sind die meisten Aufgaben für die Planung, Bereitstellung und Konfiguration sowie alltägliche Verwaltung identisch.

LTSB unterstützt z.B. die gleiche Anzahl von Standorten, Standorttypen, Clients und allgemeine Infrastruktur wie Current Branch. Sie verwenden daher den Leitfaden, den Sie in der Standort- und Hierarchieplanung sowie in den Entwurfsthemen für Current Branch finden. Ähnlich ist es bei Funktionen von LTSB, die von beiden Branches unterstützt werden, wie z.B. Softwareupdates oder Betriebssystembereitstellung: Verwenden Sie den Leitfaden, den Sie in den Abschnitten der Current Branch-Dokumentation finden, die den Vorbehalt enthält, dass Sie über keinen Zugriff auf Funktionsänderungen verfügen, die nach Version 1606 von Current Branch eingeführt wurden.

Die folgenden Abschnitte enthalten Informationen zur Verwaltung von Aufgaben, die nicht ähnlich sind.

## <a name="updates-and-servicing"></a>Updates und Wartung
Nur wichtige Sicherheitsupdates werden in LTSB als konsoleninterne Updates verfügbar gemacht.  

Informationen zu herkömmlichen Updates für die nachfolgenden Current Branch-Versionen sind in der Konsole sichtbar, aber nicht auf LTSB verfügbar. Sie werden nicht heruntergeladen und können nicht installiert werden.

Um konsoleninterne Updates für wichtige Sicherheitskorrekturen zu unterstützen, erfordert ein LTSB-Standort die Verwendung des [Dienstverbindungspunkts](../servers/deploy/configure/about-the-service-connection-point.md). Sie können diese Standortsystemrolle wie Current Branch im Offline- oder Onlinemodus konfigurieren. LTSB sammelt und sendet die gleichen Telemetrie- und Nutzungsdaten wie Current Branch.

LTSB unterstützt die Verwendung des Hotfixinstallationsprogramms und des Tools zur Updateregistrierung, so wie für Current Branch dokumentiert.

Allgemeine Informationen zu Updates und zur Wartung finden Sie unter [Updates für System Center Configuration Manager](../servers/manage/updates.md).


## <a name="changes-for-site-expansion-and-the-cdlatest-folder"></a>Änderungen für die Standorterweiterung und den Ordner „CD.Latest“
Wenn Sie LTSB ausführen und einen eigenständigen primären Standort durch die Installation eines neuen Standorts der zentralen Verwaltung erweitern, müssen Sie das Setup und die Quelldateien des Baselinemediums von Version 1606 verwenden. Führen Sie das Setup für Current Branch aus und verwenden Sie die Quelldatei aus dem Ordner „CD.Latest“.

Obwohl Sie das Setup für die Standorterweiterung aus dem Ordner „CD.Latest“ nicht ausführen, verwenden Sie den Ordner „CD.Latest“ weiterhin für die Standortwiederherstellung und zum Installieren eines neuen untergeordneten primären Standorts, wenn Ihr erster LTSB-Standort ein Standort der zentralen Verwaltung war.

Weitere Informationen zur Standorterweiterung finden Sie unter [Erweitern eines eigenständigen primären Standorts](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md#bkmk_expand). Weitere Informationen über den Ordner „CD.Latest“ finden Sie unter [Der Ordner „CD.Latest“ für System Center Configuration Manager](../servers/manage/the-cd.latest-folder.md).


## <a name="recovery"></a>Wiederherstellung
Bei der Wiederherstellung eines Standorts müssen Sie den Standort oder die Standortdatenbank auf den ursprünglichen Branch wiederherstellen. Sie können keine Current Branch-Standortdatenbank auf einer LTSB-Installation wiederherstellen oder umgekehrt.
