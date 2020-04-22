---
title: Inhaltsbibliothek-Explorer
titleSuffix: Configuration Manager
description: Im Inhaltsbibliothek-Explorer können Sie die Inhaltsbibliothek an einem Configuration Manager-Verteilungspunkt anzeigen und Fehler beheben.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 691896d9-ec0f-461f-a3f2-40378ebd3121
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 92aa778dded970800a65cab9074a547e870bf88e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707858"
---
# <a name="content-library-explorer"></a>Inhaltsbibliothek-Explorer

*Gilt für: Configuration Manager (Current Branch)*

Der Inhaltsbibliothek-Explorer ist eines der [Configuration Manager-Tools](tools.md). Sie können das Tool für die folgenden Aktivitäten verwenden:  

- Durchsuchen der Inhaltsbibliothek nach einem bestimmten Verteilungspunkt  

- Behandlung von Problemen mit der Inhaltsbibliothek  

- Kopieren von Paketen, Inhalten, Ordnern und Dateien aus der Inhaltsbibliothek  

- Neuverteilung von Paketen an den Verteilungspunkt  

- Überprüfen von Paketen in Remoteverteilungspunkten  



## <a name="requirements"></a>Anforderungen

- Führen Sie das Tool mit einem Konto aus, das auf folgende Bereiche Administratorzugriff hat:  

    - Den Zielverteilungspunkt  

    - Den WMI-Anbieter auf dem Standortserver  

    - Den Configuration Manager-Anbieter  

- Nur die Rollen **Hauptadministrator** und **Analyst mit Leseberechtigung** verfügen über genügend Rechte, um sämtliche Informationen von diesem Tool anzuzeigen.  

    - Andere Rollen, wie z.B. **Anwendungsadministrator**, können nur Teilinformationen anzeigen. Weitere Informationen finden Sie unter [Deaktivierte Pakete](#bkmk_disabled-packages).  

    - Der **Analyst mit Leseberechtigung** darf Pakete von diesem Tool nicht neu verteilen.  

- Sie können das Tool von einem beliebigen Computer ausführen, solange dieser eine Verbindung zu folgenden Komponenten herstellen kann:  

    - Den Zielverteilungspunkt  

    - Dem primären Standortserver  

    - Den Configuration Manager-Anbieter  

- Wenn der Verteilungspunkt mit dem Standortserver verbunden ist, ist weiterhin Verwaltungszugriff auf den Standortserver erforderlich.  



## <a name="usage"></a>Verwendung 

Geben Sie beim Starten von **ContentLibraryExplorer.exe** die vollqualifizierten Domänennamen (Fully Qualified Domain Name, FQDN) des Zielverteilungspunkts ein. Dieser stellt anschließend eine Verbindung mit dem Verteilungspunkt her. Wenn der Verteilungspunkt Teil des sekundären Standorts ist, werden Sie dazu aufgefordert, den FQDN des primären Standortsservers und den Code für den primären Standort einzugeben.

Im linken Bereich können Sie die Pakete anzeigen, die an diesen Verteilungspunkt verteilt wurden. Erweitern Sie die Pakete, und durchsuchen Sie deren Ordnerstruktur. Diese Struktur entspricht der Ordnerstruktur, aus der Sie das Paket erstellt haben.

Wenn Sie einen Ordner auswählen, werden im rechten Bereich alle Dateien angezeigt, die in dem Ordner enthalten sind. Diese Ansicht enthält die folgenden Informationen: 
- Dateiname
- Dateigröße
- Das zugehörige Laufwerk
- Weitere Pakete, die dieselbe Datei auf dem Laufwerk verwenden
- Den Zeitpunkt, zu dem die Datei auf dem Verteilungspunkt zuletzt geändert wurde

Darüber hinaus stellt das Tool eine Verbindung mit dem Configuration Manager-Anbieter her. Diese Verbindung dient der Ermittlung, welche Pakete an den Verteilungspunkt verteilt wurden und ob diese aktuell in der Inhaltsbibliothek des Verteilungspunkts enthalten sind. Ein Paket mit einer ausstehenden Verteilung könnte beispielsweise noch nicht in der Inhaltsbibliothek vorhanden sein. Ein solches Paket würde als „AUSSTEHEND“ im Tool angezeigt, und es würden keine Aktionen für dieses Paket aktiviert werden.


### <a name="disabled-packages"></a><a name="bkmk_disabled-packages"></a> Deaktivierte Pakete

Einige Pakete sind auf dem Verteilungspunkt vorhanden, in der Configuration Manager-Konsole jedoch nicht sichtbar. Diese Pakete sind mit einem Sternchen gekennzeichnet (\*). In diesen Paketen können keine Aktionen durchgeführt werden. Andere Pakete sind möglicherweise ebenfalls mit einem Sternchen markiert und weisen deaktivierte Aktionen auf. 

Für deaktivierte Pakete gibt es drei Hauptgründe:  

- Bei dem Paket handelt es sich um das Konfigurations-Manager-Clientupgradepaket. Dieses Paket enthält die Datei „ccmsetup.exe“.  

- Ihr Benutzerkonto hat keinen Zugriff auf das Paket, wahrscheinlich aufgrund einer rollenbasierten Verwaltung. Der Rolle **Anwendungsautor** werden beispielsweise keine Treiberpakete in der Konsole angezeigt. Folglich sind sämtliche Treiberpakete auf dem Verteilungspunkt als deaktiviert gekennzeichnet.  

- Das Paket ist auf dem Verteilungspunkt verwaist.  


### <a name="validate-packages"></a>Überprüfen von Paketen

Sie können Pakete über **Paket** > **Überprüfen** in der Symbolleiste überprüfen. Wählen Sie zunächst im linken Bereich einen Paketknoten aus. Wählen Sie keinen Inhalt oder Ordner aus. Das Tool stellt für diese Aktion eine Verbindung mit dem WMI-Anbieter auf dem Verteilungspunkt her. Wenn das Tool gestartet wird, werden Pakete mit einem oder mehreren fehlenden Inhalten als ungültig markiert. Durch Überprüfen des Pakets wird deutlich, welche Inhalte fehlen. Wenn sämtliche Inhalte vorhanden sind, die Daten jedoch beschädigt sind, wird diese Beschädigung bei der Überprüfung erkannt.


### <a name="redistribute-packages"></a>Neuverteilung von Paketen

Sie können Pakete über **Paket** > **Neu verteilen** in der Symbolleiste neu verteilen. Wählen Sie zunächst im linken Bereich einen Paketknoten aus. Für diese Aktion sind Berechtigungen zur Neuverteilung von Paketen erforderlich.


### <a name="other-actions"></a>Weitere Aktionen

Verwenden Sie **Bearbeiten** > **Kopieren** zum Kopieren von Paketen, Inhalten, Ordnern und Dateien aus der Inhaltsbibliothek in einen bestimmten Ordner. Die Inhaltsbibliothek selbst kann nicht kopiert werden. Sie können mehr als eine Datei, jedoch nicht mehrere Ordner auswählen.

Suchen Sie über **Bearbeiten** > **Paket suchen** nach Paketen. Bei dieser Aktion wird im Paketnamen und in der Paket-ID nach Ihrer Abfrage gesucht.



## <a name="limitations"></a>Einschränkungen

- Die Inhaltsbibliothek kann nicht auf direktem Wege von dem Tool bearbeitet werden. An der Inhaltsbibliothek vorgenommene Änderungen können Fehler verursachen.  

- Das Tool kann Pakete neu verteilen, jedoch nur an den Zielverteilungspunkt.  

- Wenn Sie den Verteilungspunkt mit dem Standortserver verbinden, können Sie die Paketdaten nicht überprüfen. Verwenden Sie stattdessen die Configuration Manager-Konsole. Das Tool überprüft weiterhin das Paket, um sicherzustellen, dass der gesamte Inhalt vorhanden, jedoch nicht unbedingt unbeschädigt ist.  

- Mit diesem Tool können keine Inhalte gelöscht werden.



## <a name="see-also"></a>Weitere Informationen:

- [Grundlegende Konzepte für das Content Management](../plan-design/hierarchy/fundamental-concepts-for-content-management.md)
- [Die Inhaltsbibliothek](../plan-design/hierarchy/the-content-library.md)
