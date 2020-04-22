---
title: Hierarchiewartungstool
titleSuffix: Configuration Manager
description: Hier erhalten Sie Informationen zur Funktionsweise und Verwendung des Hierarchieverwaltungstools. Dieses Thema enthält eine Übersicht über Befehlszeilenoptionen.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: cead6825-6113-4ba5-a381-ac3598dfee86
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: b564575dfc135a9c82c7e102a02d70f1b6dbf6eb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692598"
---
# <a name="hierarchy-maintenance-tool-preinstexe-for-configuration-manager"></a>Hierarchiewartungstool (Preinst.exe) für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Mithilfe des Hierarchieverwaltungstools (Preinst.exe) werden Befehle an den Hierarchie-Manager von Configuration Manager übergeben, während dieser ausgeführt wird. Das Hierarchieverwaltungstool wird bei der Installation eines Configuration Manager-Standorts automatisch installiert. Sie finden „Preinst.exe“ auf dem Standortserver im freigegebenen Ordner \\&lt;*Standortservername*>\SMS_&lt;*Standortcode*\bin\X64\00000409.  

 Sie können das Hierarchieverwaltungstool in folgenden Szenarien verwenden:  

-   Ist ein sicherer Schlüsselaustausch erforderlich, gibt es Situationen, in denen Sie den ersten Austausch des öffentlichen Schlüssels zwischen Standorten manuell ausführen müssen. Weitere Informationen finden Sie unter [Manuelles Austauschen von öffentlichen Schlüsseln zwischen Standorten](#BKMK_ManuallyExchangeKeys) in diesem Thema.  

-   Entfernen aktiver Aufträge für einen Zielstandort, der nicht mehr verfügbar ist  

-   Löschen eines Standortservers in der Configuration Manager-Konsole, wenn der Standort nicht über Setup installiert werden kann. Wenn Sie beispielsweise einen Configuration Manager-Standort physisch entfernen, ohne zunächst den Standort durch Ausführen von Setup zu deinstallieren, sind die Standortinformationen auch weiterhin in der Datenbank des übergeordneten Standorts vorhanden, und vom übergeordneten Standort wird weiterhin versucht, mit dem untergeordneten Standort zu kommunizieren. Sie können dieses Problem lösen, indem Sie das Hierarchieverwaltungstool ausführen und den untergeordneten Standort manuell aus der Datenbank des übergeordneten Standorts löschen.  

-   Gleichzeitiges Beenden aller Configuration Manager-Dienste eines Standorts.  

-   Bei der Wiederherstellung eines Standorts können Sie die öffentlichen Schlüssel mithilfe der CHILDKEYS-Option von mehreren untergeordneten Standorten an den wiederherzustellenden Standort verteilen.  

Zum Ausführen des Hierarchieverwaltungstools muss der aktuelle Benutzer über Administratorberechtigungen auf dem lokalen Computer verfügen. Zudem muss er explizit über das Sicherheitsrecht zum Verwalten des Standorts verfügen. Dabei reicht es nicht aus, wenn er dieses Recht aufgrund seiner Zugehörigkeit zu einer Gruppe geerbt hat, die über diese Berechtigung verfügt.  

## <a name="hierarchy-maintenance-tool-command-line-options"></a>Befehlszeilenoptionen des Hierarchieverwaltungstools  
Das Hierarchieverwaltungstool muss lokal auf dem Servercomputer für den Standort der zentralen Verwaltung, den primären Standort oder den sekundären Standort ausgeführt werden.  

Für die Ausführung des Hierarchieverwaltungstools gilt folgende Syntax: „preinst.exe /&lt;Option\>“. Folgende Befehlszeilenoptionen stehen zur Verfügung:  

 **/DELJOB &lt;*Standortcode*>** : Verwenden Sie diese Option, um alle Aufträge oder Befehle zu löschen, die vom aktuellen Standort an den angegebenen Zielstandort gesendet wurden.  

 **/DELSITE &lt;*Standortcode des zu löschenden untergeordneten Standorts*>** : Verwenden Sie diese Option auf einem übergeordneten Standort, um die Daten für untergeordnete Standorte aus der Datenbank des übergeordneten Standorts zu löschen. In der Regel verwenden Sie diese Option, wenn ein Standortservercomputer außer Betrieb gesetzt wird, bevor der darauf vorhandene Standort deinstalliert wurde.  

> [!NOTE]  
>  Mit der Option /DELSITE wird der Standort auf dem über den Parameter „Standortcode des zu löschenden untergeordneten Standorts“ angegebenen Computer nicht deinstalliert. Mit dieser Option werden nur die Standortinformationen aus der Configuration Manager-Standortdatenbank entfernt.  

**/DUMP &lt;*Standortcode*>** : Verwenden Sie diese Option auf dem lokalen Standortserver, um Standortsteuerungsimages in den Stammordner des Laufwerks zu schreiben, auf dem der Standort installiert ist. Sie können ein bestimmtes Standortsteuerungsabbild oder alle Standortsteuerungsabbilder in der Hierarchie in den Ordner schreiben.  

-   Mithilfe von „/DUMP &lt;*Standortcode*>“ wird lediglich das Standortsteuerungsimage für den angegebenen Standort geschrieben.  

-   Mithilfe von /DUMP werden die Standortsteuerungsabbilder für alle Standorte geschrieben.  

Ein Image ist eine binäre Darstellung der Standortsteuerungsdatei, die in der Configuration Manager-Standortdatenbank gespeichert ist. Das ausgegebene Standortsteuerungsdatei-Abbild ist die Summe des Basisabbilds und der ausstehenden Deltaabbilder.  

Nach der Ausgabe eines Standortsteuerungsdatei-Images mithilfe des Hierarchieverwaltungstools weist der Dateiname das Format „sitectrl_&lt;*Standortcode*>.ct0“ auf.  

**/STOPSITE** – Verwenden Sie diese Option auf dem lokalen Standortserver, um einen Beendigungszyklus für den Configuration Manager-Dienst „Standortkomponenten-Manager“ zu initiieren und so den Standort teilweise zurückzusetzen. Während dieses Beendigungszyklus werden einige Configuration Manager-Dienste auf einem Standortserver und seinen Remotestandortsystemen beendet. Diese Dienste werden für die Neuinstallation gekennzeichnet. Als Folge dieses Beendigungszyklus werden einige Kennwörter bei der Neuinstallation der Dienste automatisch geändert.  

> [!NOTE]  
>  Wenn Sie eine Aufzeichnung des Beendigungszyklus, der Neuinstallation und der Kennwortänderungen für den Standortkomponenten-Manager anzeigen möchten, müssen Sie die Protokollierung für diese Komponente aktivieren, bevor Sie diese Befehlszeilenoption verwenden.  

Nachdem der Beendigungszyklus gestartet wurde, wird er automatisch fortgesetzt, wobei alle nicht antwortenden Komponenten oder Computer übersprungen werden. Wenn der Standortkomponenten-Manager-Dienst jedoch während des Beendigungszyklus nicht auf ein Remotestandortsystem zugreifen kann, werden die auf dem Remotestandortsystem installierten Komponenten beim Neustart des Standortkomponenten-Manager-Diensts neu installiert. Beim Neustart versucht der Standortkomponenten-Manager-Dienst so lange, alle für die Neuinstallation gekennzeichneten Dienste zu installierten, bis die Installation erfolgreich ist.  

Sie können den Standortkomponenten-Manager-Dienst mithilfe des Dienst-Managers neu starten. Nach dem Neustart werden alle betroffenen Dienste deinstalliert, neu installiert und erneut gestartet. Nachdem Sie den Beendigungszyklus mit der Option /STOPSITE initiiert haben, können die Neuinstallationszyklen nach dem Neustart des Standortkomponenten-Manager-Diensts nicht vermieden werden.  

**/KEYFORPARENT** – Verwenden Sie diese Option auf einem Standort, um den öffentlichen Schlüssel des Standorts an einen übergeordneten Standort zu verteilen.  

Mithilfe der Option /KEYFORPARENT wird der öffentliche Schlüssel des Standorts im Stammverzeichnis des Laufwerks für Programmdateien in die Datei „&lt;*Standortcode*>.CT4“ geschrieben. Nach dem Ausführen von „preinst.exe“ mit dieser Option müssen Sie die Datei „&lt;*Standortcode*>.CT4“ manuell in den Ordner „\Inboxes\hman.box“ (nicht „hman.box\pubkey“) des übergeordneten Standorts kopieren.  

**/KEYFORCHILD** – Verwenden Sie diese Option auf einem Standort, um den öffentlichen Schlüssel des Standorts an einen untergeordneten Standort zu verteilen.  

Mithilfe der Option /KEYFORCHILD wird der öffentliche Schlüssel des Standorts im Stammverzeichnis des Laufwerks für Programmdateien in die Datei „&lt;*Standortcode*>.CT5“ geschrieben. Nach dem Ausführen von „preinst.exe“ mit dieser Option müssen Sie die Datei „&lt;*Standortcode*>.CT5“ manuell in den Ordner „\Inboxes\hman.box“ (nicht „hman.box\pubkey“) des untergeordneten Standorts kopieren.  

**/CHILDKEYS** – Sie können diese Option auf den untergeordneten Standorten eines wiederherzustellenden Standorts verwenden. Verwenden Sie diese Option, um öffentliche Schlüssel von mehreren untergeordneten Standorten an den wiederherzustellenden Standort zu verteilen.  

Mithilfe der Option /CHILDKEYS wird der Schlüssel des Standorts, auf dem der Befehl ausgeführt wird, sowie die öffentlichen Schlüssel sämtlicher untergeordneter Standorte dieses Standorts in die Datei „&lt;*Standortcode*>.CT6“ geschrieben.  

Nach dem Ausführen von „preinst.exe“ mit dieser Option müssen Sie die Datei „&lt;*Standortcode*>.CT6“ manuell in den Ordner „\Inboxes\hman.box“ (nicht „hman.box\pubkey“) des wiederherzustellenden Standorts kopieren.  

**/PARENTKEYS** – Sie können diese Option auf dem übergeordneten Standort eines wiederherzustellenden Standorts verwenden. Verwenden Sie diese Option, um öffentliche Schlüssel von allen übergeordneten Standorten an den wiederherzustellenden Standort zu verteilen.  

Mithilfe der Option /PARENTKEYS wird der Schlüssel des Standorts, auf dem der Befehl ausgeführt wird, sowie die Schlüssel sämtlicher übergeordneter Standorte dieses Standorts in die Datei „&lt;Standortcode\>.CT7“ geschrieben.  

Nach dem Ausführen von „preinst.exe“ mit dieser Option müssen Sie die Datei „&lt;*Standortcode*>.CT7“ manuell in den Ordner „\Inboxes\hman.box“ (nicht „hman.box\pubkey“) des wiederherzustellenden Standorts kopieren.  

##  <a name="manually-exchange-public-keys-between-sites"></a><a name="BKMK_ManuallyExchangeKeys"></a> Manuelles Austauschen von öffentlichen Schlüsseln zwischen Standorten  
Die Option **Sicherer Schlüsselaustausch erforderlich** ist für Configuration Manager-Standorte standardmäßig aktiviert. Ist ein sicherer Schlüsselaustausch erforderlich, gibt es zwei Situationen, in denen Sie den ersten Schlüsselaustausch zwischen Standorten manuell ausführen müssen:  

-   Wenn das Active Directory-Schema für Configuration Manager nicht erweitert wurde  

-   Von Configuration Manager-Standorten werden keine Standortdaten in Active Directory veröffentlicht.  

Mit dem Hierarchieverwaltungstool können Sie die öffentlichen Schlüssel für die einzelnen Standorte exportieren. Nachdem die Schlüssel exportiert wurden, müssen Sie sie manuell zwischen den Standorten austauschen.  

> [!NOTE]  
>  Nachdem die öffentlichen Schlüssel manuell ausgetauscht wurden, können Sie die Protokolldatei **hman.log** , in der Änderungen an der Standortkonfiguration sowie die Veröffentlichung von Standortinformationen in Active Directory-Domänendiensten aufgezeichnet werden, auf dem Server des übergeordneten Standorts überprüfen, um sicherzustellen, dass der neue öffentliche Schlüssel vom primären Standort verarbeitet wurde.  

#### <a name="to-manually-transfer-the-child-site-public-key-to-the-parent-site"></a>So übertragen Sie den öffentlichen Schlüssel des untergeordneten Standorts manuell auf den übergeordneten Standort  

1.  Melden Sie sich am untergeordneten Standort an, öffnen Sie eine Eingabeaufforderung, und wechseln Sie zum Speicherort von **Preinst.exe**.  

2.  Geben Sie Folgendes ein, um den öffentlichen Schlüssel des untergeordneten Standorts zu exportieren: **Preinst /keyforparent**  

3.  Mithilfe der Option „/keyforparent“ wird der öffentliche Schlüssel des untergeordneten Standorts in der Datei **&lt;Standortcode\>.CT4** im Stammverzeichnis des Systemlaufwerks gespeichert.  

4.  Verschieben Sie die Datei **&lt;Standortcode\>.CT4** in den Ordner **&lt;Installationsverzeichnis\>\inboxes\hman.box** des übergeordneten Standorts.  

#### <a name="to-manually-transfer-the-parent-site-public-key-to-the-child-site"></a>So übertragen Sie den öffentlichen Schlüssel des übergeordneten Standorts manuell auf den untergeordneten Standort  

1.  Melden Sie sich am übergeordneten Standort an, öffnen Sie eine Eingabeaufforderung, und wechseln Sie zum Speicherort von **Preinst.exe**.  

2.  Geben Sie Folgendes ein, um den öffentlichen Schlüssel des übergeordneten Standorts zu exportieren: **Preinst /keyforchild**.  

3.  Mithilfe der Option „/keyforchild“ wird der öffentliche Schlüssel des übergeordneten Standorts in der Datei **&lt;Standortcode\>.CT5** im Stammverzeichnis des Systemlaufwerks gespeichert.  

4.  Verschieben Sie die Datei **&lt;Standortcode\>.CT5** in das Verzeichnis **&lt;Installationsverzeichnis\>\inboxes\hman.box** des untergeordneten Standorts.  
