---
title: Erstellen einer Tasksequenz zum Installieren eines Betriebssystems
titleSuffix: Configuration Manager
description: Verwenden Sie Tasksequenzen in Configuration Manager, um automatisch ein Betriebssystemimage und andere Inhalte auf einem Zielcomputer zu installieren.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: how-to
ms.assetid: 217c8a0e-5112-420e-a325-2a6d75326290
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: dae4287b1e4a4a69209672f01f45eeaeb3b540d7
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88125473"
---
# <a name="create-a-task-sequence-to-install-an-os"></a>Erstellen einer Tasksequenz zum Installieren eines Betriebssystems

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie Tasksequenzen in Configuration Manager, um automatisch ein Betriebssystemimage auf einem Zielcomputer zu installieren. Sie erstellen eine Tasksequenz, in der auf Folgendes verwiesen wird: das zum Starten des Zielcomputers verwendete Startimage, das auf dem Zielcomputer zu installierende Betriebssystemimage und sämtlichen zusätzlich zu installierenden Inhalt, beispielsweise andere Anwendungen oder Softwareupdates. Stellen Sie dann die Tasksequenz für die Sammlung bereit, die den Zielcomputer enthält.  

## <a name="create-a-task-sequence-to-install-an-os"></a><a name="BKMK_InstallOS"></a>Erstellen einer Tasksequenz zum Installieren eines Betriebssystems

Es gibt mehrere Szenarien zum Bereitstellen eines Betriebssystems auf Computern in Ihrer Umgebung. In den meisten Fällen erstellen Sie eine Tasksequenz und wählen **Bestehendes Abbildpaket installieren** im Assistenten zum Erstellen von Tasksequenzen aus. Diese Option erstellt eine Tasksequenz, die das Betriebssystem installiert, Benutzereinstellungen migriert, Softwareupdates anwendet und Anwendungen installiert.

### <a name="prerequisites"></a>Voraussetzungen

Bevor Sie eine Tasksequenz zum Installieren eines Betriebssystems erstellen, müssen die folgenden Anforderungen erfüllt sein:

#### <a name="required"></a>Erforderlich

- Ein [Startimage](../get-started/manage-boot-images.md)  

- Ein [Betriebssystemimage](../get-started/manage-operating-system-images.md)  

#### <a name="required-if-used"></a>Erforderlich (sofern verwendet)

- Synchronisieren von [Softwareupdates](../../sum/get-started/synchronize-software-updates.md)  

- Hinzufügen von [Anwendungen](../../apps/deploy-use/create-applications.md)  

### <a name="process-to-create-a-task-sequence-that-installs-an-os"></a>Prozess zum Erstellen einer Tasksequenz zum Installieren eines Betriebssystems  

1. Erweitern Sie in der Configuration Manager-Konsole im Arbeitsbereich **Softwarebibliothek** den Bereich **Betriebssysteme**, und wählen Sie anschließend den Knoten **Tasksequenzen** aus.  

2. Wählen Sie auf der Registerkarte **Start** des Menübands in der Gruppe **Erstellen** die Option **Tasksequenz erstellen** aus. Daraufhin wird der Tasksequenzerstellungs-Assistent gestartet.  

3. Wählen Sie auf der Seite **Neue Tasksequenz erstellen** die Option **Bestehendes Abbildpaket installieren** aus, und wählen Sie dann **Weiter**.  

4. Geben Sie auf der Seite **Informationen zur Tasksequenz** die folgenden Einstellungen an:  

    - **Tasksequenzname:** Geben Sie einen Namen zur Identifikation der Tasksequenz an.  

    - **Beschreibung:** Geben Sie eine Beschreibung der Funktionsweise der Tasksequenz an.  

    - **Startimage:** Geben Sie das Startimage an, das die Tasksequenz zum Installieren des Betriebssystems auf dem Zielcomputer verwendet. Das Startimage enthält eine Version von Windows PE sowie alle zusätzlich erforderlichen Gerätetreiber. Weitere Informationen finden Sie unter [Verwalten von Startimages](../get-started/manage-boot-images.md).  

        > [!IMPORTANT]  
        > Die Architektur des Startabbilds muss kompatibel mit der Hardwarearchitektur des Zielcomputers sein.  

5. Legen Sie die folgenden Einstellungen auf der Seite **Windows installieren** fest:  

    - **Imagepaket:** Geben Sie das Paket an, das das zu installierende Betriebssystemimage enthält. Weitere Informationen finden Sie unter [Verwalten von Betriebssystemimages](../get-started/manage-operating-system-images.md).  

    - **Image:** Wenn das Betriebssystemimagepaket mehrere Images enthält, geben Sie den Index des zu installierenden Betriebssystemimages an.  

    - **Partition and format the target computer installing the operating system** (Zielcomputer, auf dem das Betriebssystem installiert wird, partitionieren und formatieren): Geben Sie an, ob die Tasksequenz den Zielcomputer vor der Installation des Betriebssystems partitionieren und formatieren soll.  

    - **Product Key:** Geben Sie ggf. den Windows-Product Key an. Sie können codierte Volumenlizenzschlüssel und standardmäßige Product Keys angeben. Wenn Sie einen nicht codierten Product Key verwenden, muss jede Gruppe aus fünf Zeichen durch einen Bindestrich (`-`) getrennt werden. Beispiel: *XXXXX-XXXXX-XXXXX-XXXXX-XXXXX*  

    - **Serverlizenzierungsmodus:** Geben Sie an, ob die Serverlizenz **Pro Arbeitsplatz** oder **Pro Server** angegeben ist bzw. dass keine Lizenz angegeben ist. Wenn die Serverlizenz **Pro Server**gilt, geben Sie auch die maximale Anzahl von Serververbindungen an.  

    - Geben Sie an, wie das Administratorkonto für das neue Betriebssystem behandelt werden soll:  

        - **Lokales Administratorkontokennwort zufällig erstellen und das Konto auf allen unterstützten Plattformen deaktivieren (empfohlen):** Windows deaktiviert das lokale Administratorkonto, nachdem die Tasksequenz das Betriebssystemimage bereitgestellt hat.  

        - **Konto aktivieren und lokales Administratorkennwort angeben:** Windows verwendet dasselbe Kennwort für das lokale Administratorkonto auf allen Computern, auf denen durch die Tasksequenz das Betriebssystemimage bereitgestellt wird.  

6. Geben Sie auf der Seite **Netzwerk konfigurieren** die folgenden Einstellungen an:  

    - **Einer Arbeitsgruppe beitreten:** Fügen Sie den Zielcomputer zu einer Arbeitsgruppe hinzu.  

    - **Einer Domäne beitreten:** Fügen Sie den Zielcomputer zu einer Domäne hinzu. Geben Sie unter **Domäne**den Namen der Domäne an.  

        > [!IMPORTANT]  
        > Domänen in der lokalen Gesamtstruktur können Sie suchen, doch bei Domänen in remoten Gesamtstrukturen müssen Sie den Domänennamen angeben.  

        Sie können auch eine Organisationseinheit (OE) im Feld **Domänen-OE** angeben. Diese Einstellung ist optional und gibt den eindeutigen LDAP X.500-Namen der Organisationseinheit an. Wenn es noch nicht vorhanden ist, erstellt Windows das Computerkonto in dieser Organisationseinheit.  

    - **Konto:** Der Benutzername und das Kennwort für das Konto, das über die Berechtigungen verfügt, der angegebenen Domäne beizutreten. Beispiel: *Domäne\Benutzer* oder *%Variable%* .  

        > [!IMPORTANT]  
        > Geben Sie die richtigen Domänenanmeldeinformationen ein, wenn Sie die Domäneneinstellungen oder die Arbeitsgruppeneinstellungen migrieren möchten.  

7. Geben Sie auf der Seite **Configuration Manager installieren** das Configuration Manager-Clientpaket an, das auf dem Zielcomputer installiert werden soll. Sie können auch beliebige Installationseigenschaften einbeziehen.  

8. Geben Sie auf der Seite **Zustandsmigration** die folgenden Informationen an:  

    - **Benutzereinstellungen erfassen:** Die Tasksequenz erfasst den Benutzerzustand. Weitere Informationen zum Erfassen und Wiederherstellen des Benutzerstatus finden Sie unter [Verwalten des Benutzerstatus](../get-started/manage-user-state.md).  

    - **Netzwerkeinstellungen erfassen:** Die Tasksequenz erfasst Netzwerkeinstellungen vom Zielcomputer. Sie erfasst die Mitgliedschaft der Domäne oder Arbeitsgruppe sowie die Einstellungen des Netzwerkadapters.  

    - **Microsoft Windows-Einstellungen erfassen:** Die Tasksequenz erfasst die Windows-Einstellungen vom Zielcomputer, bevor dieser das Betriebssystemimage installiert. Es werden der Computername, die Namen von registrierten Benutzern und Organisationen sowie die Zeitzoneneinstellungen erfasst.  

9. Geben Sie auf der Seite **Updates einschließen** an, ob erforderliche Softwareupdates, alle Softwareupdates oder keine Softwareupdates installiert werden sollen. Wenn Sie angeben, dass Softwareupdates installiert werden sollen, werden von Configuration Manager nur Softwareupdates installiert, die für Sammlungen bestimmt sind, in denen der Zielcomputer Mitglied ist.  

10. Geben Sie auf der Seite **Anwendungen installieren** die Anwendungen an, die auf dem Zielcomputer installiert werden sollen. Wenn Sie mehrere Anwendungen angeben, können Sie auch angeben, dass die Tasksequenz fortgesetzt werden soll, wenn bei der Installation einer bestimmten Anwendung ein Fehler auftritt.  

11. Schließen Sie den Assistenten ab.  

Sie können jetzt die Tasksequenz für eine Sammlung von Computern bereitstellen. Weitere Informationen finden Sie unter [Deploy a task sequence](deploy-a-task-sequence.md).


## <a name="pre-cache-content"></a>Zwischengespeicherter Inhalt

<!--4224642-->
Ab Version 1906 können Sie diese Art von Tasksequenz aktivieren, um Inhalte vorab zwischenzuspeichern. Clients können mithilfe des Features zum Vorabzwischenspeichern für verfügbare Bereitstellungen von Tasksequenzen relevante Inhalte herunterladen, bevor der Benutzer die Tasksequenz installiert.  

Weitere Informationen finden Sie unter [Konfigurieren des zwischengespeicherten Inhalts](configure-precache-content.md).


## <a name="example-task-sequence"></a><a name="BKMK_InstallExistingOSImageTSExample"></a> Tasksequenzbeispiel

Orientieren Sie sich an der folgenden Tabelle, während Sie eine Tasksequenz zur Bereitstellung eines Betriebssystems mithilfe eines vorhandenen Images erstellen. Mithilfe dieser Tabelle können Sie die allgemeine Sequenz für Ihre Tasksequenzschritte festlegen und diese Tasksequenzschritte in logischen Gruppen organisieren. Die von Ihnen erstellte Tasksequenz kann von diesem Beispiel abweichen und eine andere Anzahl von Tasksequenzschritten und Tasksequenzgruppen enthalten.  

> [!NOTE]  
> Verwenden Sie zum Erstellen dieser Tasksequenz den Tasksequenzerstellungs-Assistenten.  
>
> Einige Namen der Schritte zum Erstellen der neuen Tasksequenz im Tasksequenzerstellungs-Assistenten unterscheiden sich von den Namen der Schritte beim manuellen Hinzufügen der Tasksequenzschritte zu einer vorhandenen Tasksequenz.

|Tasksequenzgruppe oder -schritt|Beschreibung|  
|---------------------------------|-----------------|  
|Dateien und Einstellungen erfassen – **(Neue Tasksequenzgruppe)**|Erstellen Sie eine Tasksequenzgruppe. Mithilfe einer Tasksequenzgruppe können Sie ähnliche Tasksequenzschritte zur besseren Organisation und Fehlersteuerung gruppieren.<br /><br /> Diese Gruppe enthält die zum Erfassen von Dateien und Einstellungen vom Betriebssystem des Referenzcomputers erforderlichen Schritte.|  
|Windows-Einstellungen erfassen|Mithilfe dieses Tasksequenzschritts können Sie die Microsoft Windows-Einstellungen identifizieren, die vom Referenzcomputer erfasst werden müssen. Sie können den Computernamen, Benutzer- und Unternehmensinformationen sowie Zeitzoneneinstellungen erfassen.|  
|Netzwerkeinstellungen erfassen|Mithilfe dieses Tasksequenzschritts können Sie die Netzwerkeinstellungen vom Referenzcomputer erfassen. Sie können die Domänen- oder Arbeitsgruppenmitgliedschaft des Referenzcomputers sowie Informationen zur Netzwerkkarteneinstellung erfassen.|  
|Benutzerdateien und Einstellungen erfassen – **(Neue Tasksequenz-Untergruppe)**|Erstellen Sie eine Tasksequenzgruppe innerhalb einer anderen Tasksequenzgruppe. Diese Untergruppe enthält die zum Erfassen der Benutzerzustandsdaten erforderlichen Schritte. Ähnlich der ersten Gruppe, die Sie hinzugefügt haben, gruppiert diese Untergruppe ähnliche Tasksequenzschritte, wodurch die Organisation verbessert und Fehler vermieden werden.|  
|Benutzerzustandsspeicher anfordern|Mithilfe dieses Tasksequenzschritts können Sie Zugriff auf einen Zustandsmigrationspunkt anfordern, auf dem die Benutzerzustandsdaten gespeichert sind. Sie können diesen Tasksequenzschritt so konfigurieren, dass die Benutzerzustandsinformationen erfasst oder wiederhergestellt werden.|  
|Benutzerdateien und Einstellungen erfassen|Mithilfe dieses Tasksequenzschritts können Sie den Benutzerzustand und die Einstellungen unter Verwendung von Windows-EasyTransfer bzw. USMT von dem Referenzcomputer erfassen, auf dem die mit diesem Taskschritt verknüpfte Tasksequenz empfangen wird. Sie können die Standardoptionen erfassen oder die zu erfassenden Optionen konfigurieren.|  
|Benutzerzustandsspeicher freigeben|Mithilfe dieses Tasksequenzschritts können Sie den Zustandsmigrationspunkt darüber benachrichtigen, dass die Erfassungs- oder Wiederherstellungsaktion abgeschlossen ist.|  
|Betriebssystem installieren – **(Neue Tasksequenzgruppe)**|Erstellen Sie eine weitere Untergruppe der Tasksequenz. Diese Untergruppe enthält die zum Installieren und Konfigurieren der Windows PE-Umgebung erforderlichen Schritte.|  
|Neustart mit Windows PE|Mithilfe dieses Tasksequenzschritts können Sie die Neustartoptionen für den Zielcomputer angeben, auf dem diese Tasksequenz empfangen wird. In diesem Schritt wird eine Meldung angezeigt, um den Benutzer darüber zu informieren, dass der Computer zum Fortsetzen der Installation neu gestartet wird.<br /><br /> In diesem Schritt wird die schreibgeschützte Tasksequenzvariable **_SMSTSInWinPE** verwendet. Wenn der Variablen der Wert **false** zugeordnet ist, wird der Tasksequenzschritt fortgesetzt.|  
|Festplatte 0 partitionieren|Mithilfe dieses Tasksequenzschritts werden die zum Formatieren der Festplatte auf dem Zielcomputer erforderlichen Aktionen angegeben. Die standardmäßige Datenträgernummer ist **0**.<br /><br /> In diesem Schritt wird die schreibgeschützte Tasksequenzvariable **_SMSTSClientCache** verwendet. Dieser Schritt wird ausgeführt, wenn kein Configuration Manager-Clientcache vorhanden ist.|  
|Betriebssystem anwenden|Mithilfe dieses tasksequenzschritts das Betriebssystemabbild auf dem Zielcomputer installieren. In diesem Schritt werden zunächst alle Dateien auf diesem Volume mit Ausnahme von Configuration Manager-spezifischen Steuerungsdateien gelöscht. Anschließend werden alle in der WIM-Datei enthaltenen Volumeimages auf das entsprechende sequenzielle Datenträgervolume auf dem Zielcomputer angewendet. Sie können eine **sysprep** -Antwortdatei angeben und auch konfigurieren, welche Festplattenpartition für die Installation verwendet wird.|  
|Windows-Einstellungen anwenden|Mithilfe dieses Tasksequenzschritts können Sie die Konfigurationsinformationen für die Windows-Einstellungen des Zielcomputers angeben. Folgende Windows-Einstellungen können anwendet werden: Benutzer- und Unternehmensinformationen, Produkt- oder Lizenzschlüsselinformationen, Zeitzone und lokales Administratorkennwort.|  
|Netzwerkeinstellungen anwenden|Mithilfe dieses Tasksequenzschritts können Sie die Konfigurationsinformationen für das Netzwerk oder die Arbeitsgruppe des Zielcomputers angeben. Sie können auch angeben, ob vom Computer ein DHCP-Server verwendet wird, oder Sie können die IP-Adressinformationen statisch zuweisen.|  
|Gerätetreiber anwenden|Mithilfe dieses Tasksequenzschritts können Sie Gerätetreiber als Teil der Betriebssystembereitstellung installieren. Sie können durch Auswahl von **Treiber aller Kategorien berücksichtigen** zulassen, dass alle vorhandenen Treiberkategorien von Windows Setup durchsucht werden, oder die von Windows Setup zu durchsuchenden Treiberkategorien durch Auswahl von **Nur Treiber in bestimmten Kategorien berücksichtigen**einschränken.<br /><br /> In diesem Schritt wird die schreibgeschützte Tasksequenzvariable **_SMSTSMediaType** verwendet. Dieser Tasksequenzschritt wird nur ausgeführt, wenn der Wert der Variablen ungleich **FullMedia**ist.|  
|Treiberpaket anwenden|Mithilfe dieses Tasksequenzschritts können Sie alle Gerätetreiber in einem Treiberpaket für Windows Setup zur Verfügung stellen.|  
|Betriebssystem einrichten – **(Neue Tasksequenzgruppe)**|Erstellen Sie eine weitere Untergruppe der Tasksequenz. Diese Untergruppe enthält die zum Einrichten des installierten Betriebssystems erforderlichen Schritte.|  
|Windows und ConfigMgr einrichten|Mit diesem Tasksequenzschritt können Sie die Configuration Manager-Clientsoftware installieren. Mit dem Configuration Manager wird die GUID des Configuration Manager-Clients installiert und registriert. Sie können die erforderlichen Installationsparameter im Fenster **Installationseinstellungen** zuweisen.|  
|Updates installieren|Mithilfe dieses Tasksequenzschritts können Sie angeben, wie Softwareupdates auf dem Zielcomputer installiert werden. Der Zielcomputer wird erst dann auf geeignete Softwareupdates überprüft, wenn dieser Tasksequenzschritt ausgeführt wird. An diesem Punkt wird der Zielcomputer ähnlich wie jeder andere von Configuration Manager verwaltete Client hinsichtlich Softwareupdates ausgewertet.<br /><br /> In diesem Schritt wird die schreibgeschützte Tasksequenzvariable **_SMSTSMediaType** verwendet. Dieser Tasksequenzschritt wird nur ausgeführt, wenn der Wert der Variablen ungleich **FullMedia**ist.|  
|Benutzerdateien und -einstellungen wiederherstellen – **(Neue Tasksequenz-Untergruppe)**|Erstellen Sie eine weitere Untergruppe der Tasksequenz. Diese Untergruppe enthält die zum Wiederherstellen der Benutzerdateien und -einstellungen erforderlichen Schritte.|  
|Benutzerzustandsspeicher anfordern|Mithilfe dieses Tasksequenzschritts können Sie Zugriff auf einen Zustandsmigrationspunkt anfordern, auf dem die Benutzerzustandsdaten gespeichert sind.|  
|Benuterzdateien und -einstellungen wiederherstellen|Mithilfe dieses Tasksequenzschritts können Sie das Migrationstool für den Benutzerstatus (User State Migration Tool, USMT) ausführen, um den Benutzerstatus und die Benutzereinstellungen auf einem Zielcomputer wiederherzustellen.|  
|Benutzerzustandsspeicher freigeben|Mithilfe dieses Tasksequenzschritts können Sie den Zustandsmigrationspunkt darüber benachrichtigen, dass die Benutzerzustandsdaten nicht mehr benötigt werden.|  
