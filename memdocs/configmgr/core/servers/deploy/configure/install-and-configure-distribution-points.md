---
title: Verwalten von Verteilungspunkten
titleSuffix: Configuration Manager
description: Verwenden Sie Verteilungspunkte, um den Inhalt, den Sie für Geräte und Benutzer bereitstellen, zu hosten.
ms.date: 12/03/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: aebafaf9-b3d5-4a0f-9ee5-685758c037a1
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a1cc931bd0e02be66f608db11e0052fde571a427
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81701678"
---
# <a name="install-and-configure-distribution-points-in-configuration-manager"></a>Installieren und Konfigurieren von Verteilungspunkten in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Um die Inhaltsdateien die Inhaltsdateien zu hosten, die Sie für Geräte und Benutzer bereitstellen, können Sie Configuration Manager-Verteilungspunkte installieren. Die Erstellung von Verteilungspunktgruppen erleichtert die Verwaltung von Verteilungspunkten und die Verteilung von Inhalt an die Verteilungspunkte.  

Sie *installieren einen neuen Verteilungspunkt* mithilfe des Installations-Assistenten. Weitere Informationen finden Sie unter [Installieren eines Verteilungspunkts](#bkmk_install). Um *die Eigenschaften eines vorhandenen Verteilungspunkts zu verwalten*, bearbeiten Sie die Eigenschaften des Verteilungspunkts. Weitere Informationen finden Sie unter [Konfigurieren eines Verteilungspunkts](#bkmk_configs).

Konfigurieren Sie einen Großteil der Einstellungen des Verteilungspunkts mit einer der beiden Methoden. Es gibt jedoch einige Einstellungen, die entweder bei der Installation oder bei der Bearbeitung, aber nicht gleichzeitig verfügbar sind:  

- Einstellungen, die nur bei der Installation eines Verteilungspunkts verfügbar sind:  

    - **Zulassen, dass Configuration Manager IIS auf dem Verteilungspunktcomputer installiert**

    - **Konfigurieren der Laufwerksspeicherplatzeinstellungen für den Verteilungspunkt**  

- Einstellungen, die nur bei der Bearbeitung der Eigenschaften eines Verteilungspunkts verfügbar sind:  

    - **Verwalten der Beziehungen zwischen Verteilungspunktgruppen**  

    - **Anzeigen von auf dem Verteilungspunkt bereitgestelltem Inhalt**  

    - **Konfigurieren der Begrenzung der Datenübertragungsrate für Datenübertragungen an Verteilungspunkte**  

    - **Konfigurieren der Zeitpläne für Datenübertragungen an Verteilungspunkte**  


## <a name="install-a-distribution-point"></a><a name="bkmk_install"></a> Installieren eines Verteilungspunkts  

Wählen Sie einen Standortsystemserver als Verteilungspunkt aus, bevor Inhalt für Clientcomputer verfügbar gemacht werden kann. Weisen Sie auch mindestens einer [Begrenzungsgruppe](boundary-groups.md#distribution-points) einen Verteilungspunkt zu, bevor lokale Clientcomputer diesen Verteilungspunkt als Quellspeicherort für Inhalt verwenden können. Fügen Sie die Verteilungspunktrolle zu einem neuen oder vorhandenen Standortsystemserver hinzu.

### <a name="prerequisites"></a><a name="bkmk_install-prereq"></a> Voraussetzungen

Wenn Sie einen neuen Verteilungspunkt installieren, verwenden Sie einen Installations-Assistenten, der mit Ihnen die verfügbaren Einstellungen durchgeht. Bevor Sie beginnen, beachten Sie die folgenden Voraussetzungen:  

- Sie benötigen die folgenden Sicherheitsberechtigungen, um einen Verteilungspunkt zu erstellen und zu konfigurieren:  

    - **Lesen** für das Objekt **Verteilungspunkt**  

    - **Kopieren an Verteilungspunkt** für das Objekt **Verteilungspunkt**  

    - **Ändern** für das Objekt **Standort**  

    - **Zertifikate für Betriebssystembereitstellung verwalten** für das Objekt **Standort**  

- Installieren Sie Internetinformationsdienste (IIS) auf dem Windows-Server, der den Verteilungspunkt hostet. Alternativ kann Configuration Manager bei der Installation der Standortsystemrolle IIS für Sie installieren und konfigurieren.  

### <a name="procedure-to-install-a-distribution-point"></a><a name="bkmk_install-procedure"></a> Installieren eines Verteilungspunkts  

Verwenden Sie dieses Verfahren, um einen neuen Verteilungspunkt hinzuzufügen. Informationen zum Ändern der Konfiguration eines vorhandenen Verteilungspunkts finden Sie im Abschnitt [Konfigurieren eines Verteilungspunkts](#bkmk_configs).  

Beginnen Sie mit der allgemeinen Vorgehensweise [Installieren von Standortsystemrollen](install-site-system-roles.md). Wählen Sie die Rolle **Verteilungspunkt** auf der Seite **Systemrollenauswahl** des Assistenten zum Erstellen von Standortsystemservern aus. Durch diese Aktion werden die folgenden Seiten zum Assistenten hinzugefügt:  

- [Verteilungspunkt](#bkmk_config-general)
- [Kommunikation](#bkmk_config-comm)
- [Laufwerkseinstellungen](#bkmk_config-drive)
- [Pullverteilungspunkt](#bkmk_config-pull)
- [PXE-Einstellungen](#bkmk_config-pxe)
- [Multicast](#bkmk_config-multicast)
- [Inhaltsprüfung](#bkmk_config-valid)
- [Begrenzungsgruppen](#bkmk_config-boundary)

> [!Important]  
> Die folgenden Einstellungen sind nur bei der Installation eines Verteilungspunkts verfügbar:  
>
> - **Zulassen, dass Configuration Manager IIS auf dem Verteilungspunktcomputer installiert**  
>
> - **Konfigurieren der Laufwerksspeicherplatzeinstellungen für den Verteilungspunkt**  

Weitere Informationen zu den Seiten des Assistenten, die speziell die Verteilungspunktrolle betreffen, finden Sie im Abschnitt [Konfigurieren eines Verteilungspunkts](#bkmk_configs). Wenn Sie beispielsweise den Verteilungspunkt als [Pullverteilungspunkt](#bkmk_config-pull) installieren möchten, wählen Sie die Option **Enable this distribution point to pull content from other distribution points** (Inhaltspulling von anderen Verteilungspunkten für diesen Verteilungspunkt aktivieren) aus. Nehmen Sie anschließend die zusätzlichen Konfigurationen vor, die für Pullverteilungspunkte erforderlich sind.  

Nach Abschluss des Assistenten zum Erstellen von Standortsystemservern fügt der Standort die Verteilungspunktrolle zum Standortsystemserver hinzu.  


## <a name="manage-distribution-point-groups"></a><a name="bkmk_manage"></a> Verwalten von Verteilungspunktgruppen  

Verteilungspunktgruppen stellen eine logische Gruppierung von Verteilungspunkten für die Inhaltsverteilung dar. Mithilfe dieser Gruppen können Sie Inhalte von einem zentralen Speicherort für Verteilungspunkte verwalten und überwachen, die mehrere Standorte umfassen. Beachten Sie Folgendes:

- Sie können einer Verteilungspunktgruppe von beliebigen Standorten innerhalb einer Hierarchie einen oder mehrere Verteilungspunkte hinzufügen.  

- Sie können einen Verteilungspunkt zu mehreren Verteilungspunktgruppen hinzufügen.  

- Wenn Sie Inhalt an eine Verteilungspunktgruppe verteilen, wird der Inhalt von Configuration Manager an alle Verteilungspunkte verteilt, die dieser Gruppe angehören.  

- Wenn Sie der Gruppe nach der ersten Inhaltsverteilung einen Verteilungspunkt hinzufügen, wird der Inhalt von Configuration Manager automatisch an das neue Mitglied der Verteilungspunktgruppe verteilt.  

- Sie können einer Verteilungspunktgruppe eine Sammlung zuordnen. Wenn Sie Inhalt an diese Sammlung verteilen, bestimmt Configuration Manager, welche Gruppen der Sammlung zugeordnet sind. Dann wird der Inhalt an alle Verteilungspunkte verteilt, die Mitglieder dieser Gruppen sind.  

    > [!NOTE]  
    > Wenn Sie eine Sammlung einer neuen Verteilungspunktgruppe zuordnen, nachdem bereits Inhalte an die Sammlung verteilt wurden, müssen Sie die Inhalte erneut an die Sammlung verteilen, damit sie auch an die neue Verteilungspunktgruppe verteilt werden.  

In den nächsten Abschnitten werden die Verfahren für die folgenden Aktionen zum Verwalten von Verteilungspunktgruppen aufgeführt:  

- [Erstellen und Konfigurieren einer neuen Verteilungspunktgruppe](#bkmk_dpgroup-create)
- [Ändern einer vorhandenen Verteilungspunktgruppe](#bkmk_dpgroup-modify)
- [Hinzufügen ausgewählter Verteilungspunkte zu vorhandenen Verteilungspunktgruppen](#bkmk_dpgroup-addexist)

### <a name="procedure-to-create-and-configure-a-new-distribution-point-group"></a><a name="bkmk_dpgroup-create"></a> Erstellen und Konfigurieren einer neuen Verteilungspunktgruppe  

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, und wählen Sie den Knoten **Verteilungspunktgruppen** aus.  

2. Klicken Sie im Menüband auf **Gruppe erstellen**.  

3. Geben Sie im Fenster „Neue Verteilungspunktgruppe erstellen“ den **Namen** und optional eine **Beschreibung** für die Gruppe ein.  

4. Klicken Sie auf der Registerkarte **Mitglieder** auf **Hinzufügen**.  

5. Wählen Sie im Fenster „Verteilungspunkte hinzufügen“ einen oder mehrere Verteilungspunkte aus, um sie als Mitglieder zur Gruppe hinzuzufügen. Klicken Sie anschließend auf **Weiter**.  

6. Wechseln Sie, falls erforderlich, zur Registerkarte **Sammlungen** des Fensters „Neue Verteilungspunktgruppe erstellen“, und klicken Sie auf **Hinzufügen**.  

7. Wählen Sie im Fenster „Sammlungen auswählen“ die Sammlungen aus, die der Verteilungspunktgruppe zugeordnet werden sollen, und klicken Sie dann auf **OK**.  

8. Klicken Sie im Fenster „Neue Verteilungspunktgruppe erstellen“ auf **OK**, um die Gruppe zu erstellen.  

#### <a name="create-a-new-group-from-an-existing-distribution-point"></a>Erstellen einer neuen Gruppe aus einem vorhandenen Verteilungspunkt

1. Gehen Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, und wählen Sie dann den Knoten **Verteilungspunkte** aus. Wählen Sie einen oder mehrere Verteilungspunkte aus, um sie zu einer neuen Verteilungspunktgruppe hinzuzufügen.  

2. Klicken Sie im Menüband auf **Ausgewählte Elemente hinzufügen**, und klicken Sie dann auf **Ausgewählte Elemente neuer Verteilungspunktgruppe hinzufügen**.  

Dieser Prozess füllt automatisch die Registerkarte **Mitglieder** des Fensters „Neue Verteilungspunktgruppe erstellen“ mit den ausgewählten Servern auf.

### <a name="procedure-to-modify-an-existing-distribution-point-group"></a><a name="bkmk_dpgroup-modify"></a> Ändern einer vorhandenen Verteilungspunktgruppe  

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, und wählen Sie den Knoten **Verteilungspunktgruppen** aus.  

2. Wählen Sie eine vorhandene Verteilungspunktgruppe aus, die geändert werden soll. Wählen Sie im Menüband **Eigenschaften** aus.  

3. Wechseln Sie zur Registerkarte **Sammlungen**, und klicken Sie auf **Hinzufügen**, um neue Sammlungen zu dieser Gruppe zuzuordnen. Wählen Sie die Sammlungen aus, und klicken Sie dann auf **OK**.  

4. Wechseln Sie zur Registerkarte **Mitglieder**, und klicken Sie auf **Hinzufügen**, um neue Verteilungspunkte zu dieser Gruppe hinzuzufügen. Wählen Sie die Verteilungspunkte aus, und klicken Sie dann auf **OK**.  

5. Wählen Sie **OK** aus, um die Änderungen der Verteilungspunktgruppe zu speichern.  

### <a name="procedure-to-add-selected-distribution-points-to-existing-distribution-point-groups"></a><a name="bkmk_dpgroup-addexist"></a> Hinzufügen ausgewählter Verteilungspunkte zu vorhandenen Verteilungspunktgruppen  

1. Gehen Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, und wählen Sie dann den Knoten **Verteilungspunkte** aus. Wählen Sie einen oder mehrere Verteilungspunkte aus, um diesen bzw. diese zu einer vorhandenen Gruppe hinzuzufügen.  

2. Klicken Sie im Menüband auf **Ausgewählte Elemente hinzufügen**, und klicken Sie dann auf **Ausgewählte Elemente vorhandenen Verteilungspunktgruppen hinzufügen**.  

3. Wählen Sie unter **Verfügbare Verteilungspunktgruppen** die Gruppen aus, zu denen die ausgewählten Verteilungspunkte als Mitglieder hinzugefügt werden sollen. Klicken Sie anschließend auf **Weiter**.  


## <a name="reassign-a-distribution-point"></a><a name="bkmk_reassign"></a> Neuzuweisen eines Verteilungspunkts

<!-- 1306937 -->

Viele Kunden verfügen über eine ausgeprägte Configuration Manager-Infrastruktur und verringern die Anzahl von primären und sekundären Standorten, um ihre Umgebung einfacher zu gestalten. Sie benötigen allerdings weiterhin Verteilungspunkte für die Standorte ihrer Zweigstellen, um Inhalte für verwaltete Clients bereitzustellen. Diese Verteilungspunkte enthalten häufig mehrere Terabytes an Inhalt. Dieser Inhalt nimmt viel Zeit in Anspruch, und es wird eine hohe Netzwerk-Bandbreite benötigt, um die Daten an die Remoteserver zu übermitteln.

Mithilfe dieses Features können Sie einen Verteilungspunkt einem anderen primären Standort neu zuweisen, ohne dabei den Inhalt neu zuweisen zu müssen. Über diese Aktion wird ein Update für die Standortsystemzuweisung ausgeführt. Gleichzeitig wird der gesamte Inhalt dauerhaft auf dem Server gespeichert. Wenn Sie mehrere Verteilungspunkte neu zuweisen müssen, führen Sie diese Aktion zunächst auf einem einzelnen Verteilungspunkt aus. Fahren Sie dann nacheinander mit weiteren Servern fort.

> [!IMPORTANT]  
> Der Zielserver kann nur die Rolle für den Verteilungspunkt hosten. Wenn der Standortsystemserver eine andere Serverrolle von Configuration Manager hostet (z.B. den Zustandsmigrationspunkt), können Sie den Verteilungspunkt nicht neu zuweisen. Außerdem können Sie keinen Verteilunspunkt für die Cloud neu zuweisen.

Fügen Sie das Computerkonto des Zielstandortservers vor dem Neuzuweisen eines Verteilungspunkts der lokalen Administratorgruppe auf dem Zielserver mit dem Verteilungspunkt hinzu.

Führen Sie diese Schritte aus, um einen Verteilungspunkt neu zuzuweisen:

1. Stellen Sie in der Configuration Manager-Konsole eine Verbindung zum Standort der zentralen Verwaltung her.  

2. Gehen Sie zum Arbeitsbereich **Verwaltung**, und klicken Sie dann auf den Knoten **Verteilungspunkte**.  

3. Klicken Sie mit der rechten Maustaste auf den Zielverteilungspunkt, und klicken Sie anschließend auf **Verteilungspunkt neu zuweisen**.  

4. Wählen Sie den Zielstandortserver und den Standortcode aus, denen Sie diesen Verteilungspunkt neu zuweisen möchten.  

Überwachen Sie die Neuzuweisung so wie beim Hinzufügen einer neuen Rolle. Die einfachste Methode dafür ist das Aktualisieren der Konsolenansicht nach einigen Minuten. Fügen Sie der Ansicht die Standortcodespalte hinzu. Dieser Wert ändert sich, wenn Configuration Manager den Server neu zuweist. Wenn Sie versuchen, eine andere Aktion auf dem Zielserver auszuführen, bevor Sie die Konsolenansicht aktualisieren, tritt der Fehler „Objekt nicht gefunden“ auf. Stellen Sie sicher, dass der Prozess abgeschlossen ist, und aktualisieren Sie die Konsolenansicht, bevor Sie eine andere Aktion auf dem Server ausführen.

Aktualisieren Sie das Serverzertifikat nach dem Neuzuweisen eines Verteilungspunkts. Der neue Standortserver muss dieses Zertifikat mit dem öffentlichen Schlüssel neu verschlüsseln und es in der Standortdatenbank speichern. Weitere Informationen finden Sie auf der Registerkarte [Allgemein](#bkmk_config-general) der Eigenschaften des Verteilungspunkts in der Einstellung **Create a self-signed certificate or import a public key infrastructure (PKI) client certificate for the distribution point** (Selbstsigniertes Zertifikat erstellen oder ein PKI-Clientzertifikat für den Verteilungspunkt importieren).

- Für PKI-Zertifikate müssen Sie kein neues Zertifikat erstellen. Importieren Sie dieselbe PFX-Datei, und geben Sie das Kennwort ein.  

- Passen Sie für selbstsignierte Zertifikate das Ablaufdatum oder den Updatezeitpunkt an.  

- Wenn Sie das Zertifikat nicht aktualisieren, liefert der Verteilungspunkt weiterhin Inhalt, die folgenden Funktionen schlagen jedoch fehl:  

    - Nachrichten zur Inhaltsprüfung (die Datei „distmgr.log“ zeigt an, dass das Zertifikat nicht entschlüsselt werden kann)  

    - PXE-Unterstützung für Clients  

### <a name="tips"></a>Tipps

- Führen Sie diese Aktion am Standort der zentralen Verwaltung aus. Dieses Vorgehen hilft bei der Replikation an den primären Standort.  

- Verteilen Sie den Inhalt nicht an den Zielserver, um anschließend zu versuchen, ihn neu zuzuweisen. Verteilte Inhaltstasks, die ausgeführt werden, können bei der Neuzuweisung fehlschlagen, werden jedoch wie normal erneut ausgeführt.  

- Wenn der Server auch ein Configuration Manager-Client ist, achten Sie darauf, auch den Client dem neuen primären Standort neu zuzuweisen. Dieser Schritt ist besonders wichtig für Pullverteilungspunkte, die Inhalt mithilfe von Clientkomponenten herunterladen.  

- Dieser Prozess entfernt den Verteilungspunkt aus der alten Standardbegrenzungsgruppe des Standorts. Falls erforderlich, müssen Sie ihn manuell zur Standardbegrenzungsgruppe des neuen Standorts hinzufügen. Alle anderen Begrenzungsgruppenzuweisungen bleiben unverändert.  


## <a name="maintenance-mode"></a><a name="bkmk_maint"></a> Wartungsmodus

<!--3555754-->

Ab Version 1902 können Sie Verteilungspunkte in den Wartungsmodus versetzen. Aktivieren Sie den Wartungsmodus, wenn Sie Softwareupdates installieren oder an der Serverhardware Änderungen vornehmen.

Ein Verteilungspunkt im Wartungsmodus weist folgende Verhaltensweisen auf:

- Vom Standort werden keine Inhalte an den Verteilungspunkt verteilt.  

- Der Standort dieses Verteilungspunkts wird von Verwaltungspunkten nicht an Clients zurückgegeben.

- Wenn Sie den Standort aktualisieren, wird ein Verteilungspunkt im Wartungsmodus ebenfalls aktualisiert.

- Die Verteilungspunkteigenschaften sind schreibgeschützt. So ist es beispielsweise nicht möglich, das Zertifikat zu ändern oder Begrenzungsgruppen hinzuzufügen.  

- Ein geplanter Task, wie etwa eine Inhaltsprüfung, wird dennoch nach Zeitplan ausgeführt.

Seien Sie vorsichtig, wenn Sie den Wartungsmodus auf mehreren Verteilungspunkten aktivieren. Dadurch kann die Leistung der anderen Verteilungspunkte beeinträchtigt werden. Je nach Begrenzungsgruppenkonfiguration wurde für Clients eine längere Downloadzeit festgelegt oder ist für Clients das Herunterladen von Inhalten nicht möglich.

Der Wartungsmodus sollte kein langfristiger Zustand für einen Verteilungspunkt sein. Für alle Aktionen mit langer Laufzeit sollten Sie zunächst die Verteilungspunktrolle entfernen.

> [!NOTE]
> Während sich ein Verteilungspunkt im Wartungsmodus befindet, führen Sie nicht die folgenden Aktionen durch:<!-- SCCMDocs-pr #4699 -->
>
> - Entfernen einer Rolle
> - Verteilungspunkt neu zuweisen

### <a name="enable-maintenance-mode"></a>Aktivieren des Wartungsmodus

Ihr Benutzerkonto muss über **Bearbeitungsberechtigung** für die **Site**-Klasse verfügen, um einen Verteilungspunkt in den Wartungsmodus zu versetzen. Die integrierten Rollen **Infrastrukturadministrator** und **Hauptadministrator** verfügen beispielsweise über diese Berechtigung.<!-- SCCMDocs-pr issue #3407 -->

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**.  

2. Wählen Sie den Knoten **Verteilungspunkte** aus.  

3. Wählen Sie den Zielverteilungspunkt aus, und klicken Sie im Menüband auf **Wartungsmodus aktivieren**.  

Wenn Sie den aktuellen Status der Verteilungspunkte anzeigen möchten, fügen Sie dem Knoten **Verteilungspunkte** in der Konsole die Spalte „Wartungsmodus“ hinzu.

Weitere Informationen zur Automatisierung dieses Prozesses mithilfe des Configuration Manager SDK finden Sie unter [SetDPMaintenanceMode method in class SMS_DistributionPointInfo (SetDPMaintenanceMode-Methode in der SMS_DistributionPointInfo-Klasse)](../../../../develop/reference/core/servers/configure/setdpmaintenancemode-method-in-class-sms-distributionpointinfo.md).


## <a name="configure-a-distribution-point"></a><a name="bkmk_configs"></a> Konfigurieren eines Verteilungspunkts  

Einzelne Verteilungspunkte unterstützen viele verschiedene Konfigurationen. Allerdings unterstützen nicht alle Verteilungspunkttypen alle Konfigurationen. Cloudverteilungspunkte unterstützen beispielsweise keine PXE- oder multicastfähigen Bereitstellungen. Weitere Informationen zu den spezifischen Einschränkungen finden in den folgenden Artikeln:  

- [Verwenden eines cloudbasierten Verteilungspunkts](../../../plan-design/hierarchy/use-a-cloud-based-distribution-point.md)  

- [Verwenden eines Pullverteilungspunkts](../../../plan-design/hierarchy/use-a-pull-distribution-point.md)  

Die folgenden Abschnitte beschreiben die Konfigurationen für Verteilungspunkte, wenn Sie [einen neuen Verteilungspunkt erstellen](#bkmk_install-procedure) oder [einen vorhandenen Verteilungspunkt bearbeiten](#bkmk_change-procedure):  

- [Allgemeine Einstellungen](#bkmk_config-general)
- [Kommunikation](#bkmk_config-comm)
- [Laufwerkseinstellungen](#bkmk_config-drive)
- [Firewalleinstellungen](#bkmk_firewall)
- [Pullverteilungspunkt](#bkmk_config-pull)
- [PXE-Einstellungen](#bkmk_config-pxe)
- [Multicast](#bkmk_config-multicast)
- [Inhaltsprüfung](#bkmk_config-valid)
- [Begrenzungsgruppen](#bkmk_config-boundary)

#### <a name="procedure-to-change-a-distribution-point"></a><a name="bkmk_change-procedure"></a> Ändern eines Verteilungspunkts

1. Gehen Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, und wählen Sie dann den Knoten **Verteilungspunkte** aus.  

2. Wählen Sie den Verteilungspunkt aus, den Sie konfigurieren möchten. Klicken Sie im Menüband auf **Eigenschaften**.  

3. Verwenden Sie beim Bearbeiten der Eigenschaften des Verteilungspunkts die Informationen in den folgenden Abschnitten.  

4. Nachdem Sie die gewünschten Änderungen vorgenommen haben, klicken Sie auf **OK**, um Ihre Einstellungen zu speichern und die Verteilungspunkteigenschaften zu schließen.  

### <a name="general"></a><a name="bkmk_config-general"></a> Allgemein  

> [!Note]  
> In Version 1902 und früher enthielt diese Seite zusätzliche Einstellungen für HTTP/HTTPS und Zertifikate. Ab Version 1906 befinden sich diese Einstellungen nun auf der Seite [Kommunikation](#bkmk_config-comm).

Die folgenden Einstellungen befinden sich auf der Seite **Verteilungspunkt** des Assistenten zum Erstellen von Standortsystemservern und auf der Registerkarte **Allgemein** des Fensters „Verteilungspunkteigenschaften“:  

- **Beschreibung:** Eine optionale Beschreibung für diese Verteilungspunktrolle.  

- **IIS installieren und konfigurieren, sofern dies für Configuration Manager erforderlich ist:** Wenn IIS noch nicht auf dem Server installiert ist, führt Configuration Manager deren Installation und Konfiguration aus. Configuration Manager benötigt IIS auf allen Verteilungspunkten. Wenn Sie diese Einstellung nicht auswählen und keine IIS auf dem Server installiert sind, müssen Sie zunächst IIS installieren, bevor Configuration Manager den Verteilungspunkt erfolgreich installieren kann.  

    > [!NOTE]  
    > Diese Option ist nur auf der Seite **Verteilungspunkt** des Assistenten zum Erstellen von Standortsystemservern vorhanden. Sie ist nur beim [Installieren eines neuen Verteilungspunkts](#bkmk_install-procedure) verfügbar.  

- **BranchCache für diesen Verteilungspunkt aktivieren und konfigurieren:** Wählen Sie diese Einstellung aus, damit Configuration Manager Windows BranchCache auf dem Verteilungspunktserver installiert. Weitere Informationen finden Sie unter [BranchCache](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#branchcache).  

- **Downloadgeschwindigkeit zur Verwendung der nicht genutzten Netzwerkbandbreite anpassen (Windows LEDBAT)**<!--1358112-->: Ab Version 1806 aktivieren Sie die Verwendung der Netzwerküberlastungssteuerung durch die Verteilungspunkte. Weitere Informationen finden Sie unter [Windows LEDBAT](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#windows-ledbat). Mindestanforderungen für LEDBAT-Unterstützung:<!-- SCCMDocs issue 883 -->  

    - Configuration Manager Version 1806 (allgemeines Release)  

        - Windows Server, Version 1709 oder höher  

    - Configuration Manager Version 1806 mit Updaterollup (4462978) oder höher  

        - Windows Server, Version 1709 oder höher
        - Windows Server 2016 mit den Updates KB4132216 und KB4284833

    - Configuration Manager Version 1810 oder höher:

        - Windows Server, Version 1709 oder höher
        - Windows Server 2016 mit den Updates KB4132216 und KB4284833
        - Windows Server 2019  

- **Diesen Verteilungspunkt für vorab bereitgestellten Inhalt aktivieren:** Mit dieser Einstellung können Sie Inhalt zum Server hinzufügen, bevor Sie Software verteilen. Da sich die Inhaltsdateien bereits in der Inhaltsbibliothek befinden, werden sie bei der Verteilung der Software nicht über das Netzwerk übertragen. Weitere Informationen finden Sie unter [Vorab bereitgestellter Inhalt](../../../plan-design/hierarchy/manage-network-bandwidth.md#BKMK_PrestagingContent).  

- **Aktivieren Sie diesen Verteilungspunkt für die Verwendung als Microsoft Connected Cacheserver:** Ab Version 1906 können Sie einen Microsoft Connected Cache-Server auf Ihren Verteilungspunkten installieren. Wenn Sie diese Art von Inhalt lokal zwischenspeichern, können Ihre Clients von dem Feature zur Übermittlungsoptimierung profitieren, und Sie können dabei helfen, WAN-Links zu schützen. Weitere Informationen, einschließlich einer Beschreibung der zusätzlichen Einstellungen, finden Sie unter [Microsoft Connected Cache in Configuration Manager](../../../plan-design/hierarchy/microsoft-connected-cache.md).


### <a name="communication"></a><a name="bkmk_config-comm"></a> Kommunikation

> [!Note]  
> Ab Version 1906 befinden sich die folgenden Einstellungen auf der Registerkarte **Kommunikation**. In Version 1902 und früher waren diese Einstellungen auf der Registerkarte [Allgemein](#bkmk_config-general) enthalten.

Die folgenden Einstellungen finden sich auf der Seite **Kommunikation** des Assistenten zum Erstellen von Standortsystemservern und im Eigenschaftenfenster für Verteilungspunkte:  

- **Configure how client devices communicate with the distribution point** (Konfigurieren, wie Clientgeräte mit dem Verteilungspunkt kommunizieren): Sowohl bei der Verwendung von **HTTP** als auch von **HTTPS** gibt es Vor- und Nachteile. Weitere Informationen finden Sie unter [Security best practices for content management (Bewährte Sicherheitsmethoden für die Inhaltsverwaltung)](../../../plan-design/hierarchy/security-and-privacy-for-content-management.md#BKMK_Security_ContentManagement).  

- **Clients gestatten, eine anonyme Verbindung herzustellen**: Mit dieser Einstellung geben Sie an, ob vom Verteilungspunkt anonyme Verbindungen von Konfigurations-Manager-Clients mit der Inhaltsbibliothek zugelassen werden sollen.  

<!-- I don't think this applies any more, but commenting instead of removing just in case.
    > [!Important]  
    > If you don't use this setting, apply the changes described in Microsoft Knowledge Base article [2619572](https://support.microsoft.com/help/2619572/) on Windows 7 clients. Otherwise repair of Windows Installer applications can fail.  
    >
    > When you deploy a Windows Installer application, the Configuration Manager client downloads the file to its local cache. The client eventually removes the files after the installation finishes. The Configuration Manager client updates the Windows Installer source list for the application. It sets the content path to the content library on associated distribution points. Later, if you try to repair the application on the device, MSIExec attempts to access the content path by using an anonymous user.  
    >
    > After you install the update on clients and modify the documented registry key, MSIExec accesses the content path by using the signed-in user account.  
 -->

- **Erstellen Sie ein selbstsigniertes Zertifikat, oder importieren Sie ein PKI-Clientzertifikat:** Configuration Manager setzt dieses Zertifikat wie folgt ein:  

    - Durch das Zertifikat wird der Verteilungspunkt gegenüber einem Verwaltungspunkt authentifiziert, bevor vom Verteilungspunkt Statusmeldungen gesendet werden.  

    - Wenn Sie die Option **PXE-Unterstützung für Clients aktivieren** auf der Seite **PXE-Einstellungen** auswählen, sendet der Verteilungspunkt es an Computer mit PXE-Start. Diese Computer verwenden es dann während der Betriebssystembereitstellung, um eine Verbindung zu einem Verwaltungspunkt herzustellen.  

    Wenn Sie alle Ihre Verwaltungspunkte am Standort für HTTP konfigurieren, wählen Sie die Option **Selbstsigniertes Zertifikat erstellen** aus. Wenn Sie die Verwaltungspunkte für HTTPS konfigurieren, verwenden Sie die Option **Zertifikat importieren** von PKI.  

    Navigieren Sie zum Importieren des Zertifikats zu einer gültigen Datei für den Public Key Cryptography Standard (PKCS #12). Diese PFX- oder CER-Datei verfügt über das PKI-Zertifikat mit den folgenden Anforderungen für Configuration Manager:  

    - Die vorgesehene Verwendung umfasst die Clientauthentifizierung.  

    - Lassen Sie zu, dass der private Schlüssel exportiert werden kann.  

    > [!TIP]  
    > Es gibt keine speziellen Anforderungen für den Zertifikatantragsteller oder den alternativen Antragstellernamen (SAN). Sie können bei Bedarf dasselbe Zertifikat für mehrere Verteilungspunkte verwenden.  

    Weitere Informationen zu den Zertifikatanforderungen finden Sie unter [PKI-Zertifikatanforderungen](../../../plan-design/network/pki-certificate-requirements.md).  

    Ein Beispiel für die Bereitstellung dieses Zertifikats finden Sie unter [Bereitstellen des Clientzertifikats für Verteilungspunkte](../../../plan-design/network/example-deployment-of-pki-certificates.md#BKMK_clientdistributionpoint2008_cm2012).  

### <a name="drive-settings"></a><a name="bkmk_config-drive"></a> Laufwerkseinstellungen  

> [!NOTE]  
> Diese Optionen sind nur bei der Installation eines neuen Verteilungspunkts verfügbar.  

Geben Sie die Laufwerkseinstellungen für den Verteilungspunkt an. Konfigurieren Sie bis zu zwei Laufwerke für die Inhaltsbibliothek und zwei Laufwerke für die Paketfreigabe. Configuration Manager kann zusätzliche Laufwerke verwenden, wenn die ersten beiden die konfigurierte Laufwerksspeicherreserve erreichen. Auf der Seite **Laufwerkseinstellungen** werden die Priorität der Laufwerke und der freie Speicherplatz, der auf jedem Laufwerk verbleiben muss, festgelegt.  

- **Laufwerksspeicherreserve (MB):** Dieser Wert legt fest, wie viel freier Speicher auf einem Laufwerk verbleiben muss, bevor Configuration Manager ein anderes Laufwerk auswählt, auf dem der Kopiervorgang fortgesetzt wird. Inhaltsdateien können sich über mehrere Laufwerke erstrecken.  

- **Inhaltsorte:** Geben Sie die Speicherorte für die Inhaltsbibliothek und die Paketfreigabe auf diesem Verteilungspunkt an. Alle Inhaltsorte sind standardmäßig auf **Automatisch** festgelegt. Configuration Manager kopiert solange Inhalte zum primären Inhaltsort, bis die Menge des freien Speicherplatzes den unter **Laufwerksspeicherreserve (MB)** angegebenen Wert erreicht. Wenn Sie **Automatisch** auswählen, legt Configuration Manager als primäre Inhaltsorte das Laufwerk fest, das zum Zeitpunkt der Installation den meisten freien Speicherplatz aufweist. Für die sekundären Speicherorte wird das Laufwerk mit dem zweitmeisten freien Speicherplatz festgelegt. Wenn die Laufwerksspeicherreserve des primären und des sekundären Laufwerks erreicht ist, wählt Configuration Manager ein anderes verfügbares Laufwerk mit dem meisten freien Speicherplatz aus, um den Kopiervorgang dort fortzusetzen.  

> [!Tip]  
> Wenn die Installation durch Configuration Manager nicht auf einem bestimmten Laufwerk erfolgen soll, erstellen Sie eine leere Datei namens **no_sms_on_drive.sms**, und legen Sie sie im Stammordner des Laufwerks ab, bevor Sie den Verteilungspunkt installieren.  

Weitere Informationen finden Sie unter [Die Inhaltsbibliothek](../../../plan-design/hierarchy/the-content-library.md).

### <a name="firewall-settings"></a><a name="bkmk_firewall"></a> Firewalleinstellungen

Für den Verteilungspunkt müssen die folgenden eingehenden Regeln in der Windows-Firewall konfiguriert sein:

- Windows Management Instrumentation (DCOM-In)
- Windows Management Instrumentation (WMI-In)

Ohne diese Regeln wird für Clients beim Herunterladen von Inhalt Fehler 0x801901F4 in „DataTransferService.log“ eingetragen.

### <a name="pull-distribution-point"></a><a name="bkmk_config-pull"></a> Pullverteilungspunkt  

Wenn Sie die Option **Enable this distribution point to pull content from other distribution points** (Inhaltspulling von anderen Verteilungspunkten für diesen Verteilungspunkt aktivieren) auswählen, wird der Verteilungspunkt zu einem Pullverteilungspunkt. Damit ändern Sie das Verhalten, wie der Verteilungspunkt den Inhalt abruft, den Sie an ihn verteilen. Weitere Informationen finden Sie unter [Use a pull-distribution point (Verwenden eines Verteilungspunkts)](../../../plan-design/hierarchy/use-a-pull-distribution-point.md).

Für jeden Pullverteilungspunkt, den Sie konfigurieren, müssen Sie mindestens einen Quellverteilungspunkt angeben, von dem der Inhalt abgerufen wird:  

- Klicken Sie auf **Hinzufügen**, und wählen Sie dann mindestens einen der verfügbaren Verteilungspunkte als Quelle aus.  

- Verwenden Sie die Pfeilschaltflächen, um die Priorität anzupassen. Wenn der Pullverteilungspunkt versucht, Inhalt zu übertragen, bestimmt die Priorität, in welcher Reihenfolge er die Quellverteilungspunkte anspricht. Verteilungspunkte mit dem niedrigsten Wert werden zuerst angesprochen.  

### <a name="pxe"></a><a name="bkmk_config-pxe"></a> PXE  

Geben Sie an, ob PXE auf dem Verteilungspunkt aktiviert werden soll. Verwenden Sie PXE, um Betriebssystembereitstellungen auf Clients zu starten. Weitere Informationen zur Verwendung von PXE in Configuration Manager finden Sie unter [Verwenden von PXE zum Bereitstellen von Windows über das Netzwerk](../../../../osd/deploy-use/use-pxe-to-deploy-windows-over-the-network.md).

Wenn Sie PXE aktivieren, installiert Configuration Manager bei Bedarf die Windows-Bereitstellungsdienste (Windows Deployment Services, WDS) auf dem Server. WDS ist der Dienst, der den PXE-Start zur Installation von Betriebssystemen ausgeführt. Wenn Sie den Assistenten zum Erstellen des Verteilungspunkts abgeschlossen haben, installiert Configuration Manager einen Anbieter in den Windows-Bereitstellungsdiensten, der die PXE-Startfunktionen verwendet.

Ab Version 1806 können Sie PXE auf einem Verteilungspunkt ohne WDS aktivieren.

Wählen Sie die Option **PXE-Unterstützung für Clients aktivieren** aus, und konfigurieren Sie dann die folgenden Einstellungen:  

> [!Note]  
> Klicken Sie im Dialogfeld **Für PXE erforderliche Ports überprüfen** auf **Ja**, um die Aktivierung von PXE zu bestätigen. Configuration Manager konfiguriert automatisch die Standardports der Windows-Firewall. Sie müssen die Ports manuell konfigurieren, wenn Sie eine andere Firewall verwenden.  
>
> Wenn Sie WDS und DHCP auf demselben Server installieren, müssen Sie WDS für das Lauschen an einem anderen Port konfigurieren. DHCP lauscht standardmäßig auf demselben Port. Weitere Informationen finden Sie unter [Aspekte, wenn sich der Windows-Bereitstellungsdienst und DHCP auf demselben Server befinden](../../../../osd/plan-design/infrastructure-requirements-for-operating-system-deployment.md#BKMK_WDSandDHCP).  

- **Antwort auf eingehende PXE-Anforderungen durch diesen Verteilungspunkt zulassen:** Gibt an, ob WDS aktiviert werden soll, um auf PXE-Service Requests zu antworten. Sie können den Dienst mithilfe dieser Einstellung aktivieren oder deaktivieren, ohne die PXE-Funktionalität vom Verteilungspunkt zu entfernen.  

- **Unterstützung für unbekannte Computer aktivieren:** Gibt an, ob die Unterstützung für Computer aktiviert werden soll, die nicht von Configuration Manager verwaltet werden. Weitere Informationen finden Sie unter [Prepare for unknown computer deployments (Vorbereiten auf Bereitstellungen für unbekannte Computer)](../../../../osd/get-started/prepare-for-unknown-computer-deployments.md).  

- **PXE-Antwortdienst ohne Windows-Bereitstellungsdienst aktivieren:** Ab Version 1806 aktiviert diese Option einen PXE-Antwortdienst auf dem Verteilungspunkt, der keine Windows Deployment Services (Windows Deployment Service, WDS) benötigt. Dieser PXE-Antwortdienst unterstützt IPv6-Netzwerke. Wenn Sie diese Option auf einem Verteilungspunkt aktivieren, auf dem PXE bereits aktiviert ist, hält Configuration Manager den WDS-Dienst an. Wenn Sie diese Option deaktivieren, aber trotzdem die Option **PXE-Unterstützung für Clients aktivieren** ausgewählt ist, aktiviert der Verteilungspunkt WDS wieder.<!--1357580-->  

    > [!Note]  
    > Bis zur Version 1810 wird die Verwendung des PXE-Antwortdiensts ohne WDS auf Servern, auf denen auch ein DHCP-Server ausgeführt wird, nicht unterstützt.
    >
    > Ab der Version 1902 gilt: Wenn Sie einen PXE-Antwortdienst auf einem Verteilungspunkt ohne Windows-Bereitstellungsdienst aktivieren, kann er sich nun auf dem gleichen Server befinden wie der DHCP-Dienst. <!--3734270-->  

- **Kennwort erforderlich, wenn PXE von Computern verwendet wird:** Geben Sie ein sicheres Kennwort an, um die Sicherheit für Ihre PXE-Bereitstellungen zusätzlich zu erhöhen.  

- **Affinität zwischen Benutzer und Gerät:** Geben Sie an, wie bei PXE-Bereitstellungen die Zuordnung von Benutzern und Zielcomputer durch den Verteilungspunkt erfolgen soll. Wählen Sie eine der folgenden Optionen aus:  

  - **Affinität zwischen Benutzer und Gerät mit automatischer Genehmigung zulassen:** Wählen Sie diese Einstellung aus, wenn Benutzer dem Zielcomputer automatisch zugeordnet werden sollen, ohne dass auf die Genehmigung gewartet wird.  

  - **Affinität zwischen Benutzer und Gerät mit ausstehender Genehmigung durch den Administrator zulassen:** Wählen Sie diese Einstellung aus, wenn auf die Genehmigung eines Administrators gewartet werden soll, bevor Benutzer dem Zielcomputer zugeordnet werden.  

  - **Affinität zwischen Benutzer und Gerät nicht zulassen:** Wählen Sie diese Einstellung aus, um anzugeben, dass Benutzer dem Zielcomputer nicht zugeordnet werden sollen. Dies ist die Standardeinstellung.  

    Weitere Informationen zur Affinität zwischen Benutzer und Gerät finden Sie unter [Verknüpfen von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

- **Netzwerkschnittstellen:** Geben Sie an, ob vom Verteilungspunkt auf PXE-Anforderungen von allen oder nur von bestimmten Netzwerkschnittstellen geantwortet werden soll. Wenn der Verteilungspunkt nur bestimmten Netzwerkschnittstellen antworten soll, stellen Sie die MAC-Adressen dieser Schnittstellen bereit.  

    > [!Note]  
    > Wenn Sie die Netzwerkschnittstelle ändern, müssen Sie den WDS-Dienst neu starten, um sicherzustellen, dass er die Konfiguration ordnungsgemäß speichert. Wenn Sie ab Version 1806 den PXE-Antwortdienst verwenden, müssen Sie den **ConfigMgr-PXE-Antwortdienst** (SccmPxe) neu starten.<!--SCCMDocs issue 642-->  

- **Reaktionsverzögerung für den PXE-Server (in Sekunden) angeben:** Wenn Sie mehrere PXE-Server verwenden, geben Sie an, wie lange dieser PXE-fähige Verteilungspunkt warten soll, bevor er auf Computeranforderungen reagiert. Standardmäßig reagiert der PXE-fähige Verteilungspunkt von Configuration Manager sofort.  

### <a name="multicast"></a><a name="bkmk_config-multicast"></a> Multicast  

Geben Sie an, ob Multicast auf dem Verteilungspunkt aktiviert werden soll. Bei Multicastbereitstellungen wird die Netzwerkbandbreite eingespart, indem gleichzeitig Daten an mehrere Konfigurations-Manager-Clients gesendet werden. Ohne Multicast sendet der Server eine Kopie der Daten über eine separate Verbindung an jeden Client. Weitere Informationen zur Verwendung von Multicast für Betriebssystembereitstellungen finden Sie unter [Verwenden von Multicast zum Bereitstellen von Windows über das Netzwerk](../../../../osd/deploy-use/use-multicast-to-deploy-windows-over-the-network.md).

Wenn Sie Multicast aktivieren, installiert Configuration Manager bei Bedarf die Windows-Bereitstellungsdienste (Windows Deployment Services, WDS) auf dem Server.  

Wählen Sie die Option **Multicast aktivieren, um gleichzeitig Daten an mehrere Clients zu senden** aus, und konfigurieren Sie dann die folgenden Einstellungen:  

- **Multicastverbindungskonto:** Geben Sie das Konto an, das verwendet werden soll, wenn Sie Configuration Manager-Datenbankverbindungen für Multicast konfigurieren. Weitere Informationen finden Sie unter [Multicastverbindungskonto](../../../plan-design/hierarchy/accounts.md#multicast-connection-account).  

- **Multicastadresseinstellungen:** Geben Sie die IP-Adressen an, die zum Senden von Daten an die Zielcomputer verwendet werden sollen. Standardmäßig wird die IP-Adresse von einem DHCP-Server abgerufen, der für die Verteilung von Multicastadressen aktiviert ist. Je nach Netzwerkumgebung können Sie IP-Adressen im Bereich von 239.0.0.0 bis 239.255.255.255 angeben.  

    > [!IMPORTANT]  
    > Die IP-Adressen, die Sie konfigurieren, müssen für die Zielcomputer, von denen das Betriebssystemimage angefordert wird, zugänglich sein. Vergewissern Sie sich, dass Multicastdatenverkehr von Routern und Firewalls zwischen Zielcomputer und Verteilungspunkt zugelassen wird.  

- **UDP-Portbereich für Multicasts:** Geben Sie den Bereich der UDP-Ports an, der zum Senden von Daten an die Zielcomputer verwendet werden soll.  

    > [!IMPORTANT]  
    > Die UDP-Ports müssen für die Zielcomputer, von denen das Betriebssystemimage angefordert wird, zugänglich sein. Vergewissern Sie sich, dass Multicastdatenverkehr von Routern und Firewalls zwischen Zielcomputer und Standortserver zugelassen wird.  

- **Max. Anzahl von Clients:** Geben Sie die maximale Anzahl von Zielcomputern an, die das Betriebssystemabbild von diesem Verteilungspunkt herunterladen können.  

- **Geplanten Multicast aktivieren:** Geben Sie an, wie Configuration Manager die Startzeit der Bereitstellung des Betriebssystems für Zielcomputer steuert. Konfigurieren Sie die folgenden Optionen:  

    - **Sitzungsstartverzögerung (Minuten):** Geben Sie an, wie viele Minuten Configuration Manager warten soll, bis auf die erste Bereitstellungsanforderung reagiert wird.  

    - **Minimale Sitzungsgröße (Clients):** Geben Sie an, wie viele Anforderungen empfangen werden müssen, bevor Configuration Manager das Betriebssystem bereitstellt.  

> [!IMPORTANT]  
> Damit ab Version 1806 auf der Registerkarte **Multicast** der Verteilungspunkteigenschaften Multicastfunktionen aktiviert und konfiguriert werden können, muss der Verteilungspunkt Windows Deployment Service verwenden.  
>
> - Wenn Sie die Optionen **PXE-Unterstützung für Clients aktivieren** und **Multicast aktivieren, um gleichzeitig Daten an mehrere Clients zu senden** verwenden, können Sie die Option **PXE-Antwortdienst ohne Windows-Bereitstellungsdienste aktivieren** nicht verwenden.  
>
> - Wenn Sie die Optionen **PXE-Unterstützung für Clients aktivieren** und **PXE-Antwortdienst ohne Windows-Bereitstellungsdienste aktivieren** verwenden, können Sie die Option **Multicast aktivieren, um gleichzeitig Daten an mehrere Clients zu senden** nicht verwenden.  

### <a name="group-relationships"></a><a name="bkmk_config-group"></a> Gruppenbeziehungen  

> [!NOTE]  
> Diese Optionen sind nur bei der Bearbeitung der Eigenschaften eines zuvor installierten Verteilungspunkts verfügbar.  

Verwalten Sie die Verteilungspunktgruppen, in denen dieser Verteilungspunkt Mitglied ist.  

Wählen Sie **Hinzufügen** aus, um diesen Verteilungspunkt einer vorhandenen Verteilungspunktgruppe als Mitglied hinzuzufügen. Wählen Sie im Fenster „Zu Verteilungspunktgruppen hinzufügen“ eine vorhandene Gruppe aus, und klicken Sie dann auf **OK**.  

Wählen Sie die Gruppe aus der Liste aus, und klicken Sie dann auf **Entfernen**, um den Verteilungspunkt aus einer Verteilungspunktgruppe zu entfernen. Es wird kein Inhalt aus dem Verteilungspunkt entfernt, wenn dieser aus einer Verteilungspunktgruppe entfernt wird.

### <a name="content"></a><a name="bkmk_config-content"></a> Inhalt  

> [!NOTE]  
> Diese Optionen sind nur bei der Bearbeitung der Eigenschaften eines zuvor installierten Verteilungspunkts verfügbar.  

Verwalten Sie den Inhalt, den Sie an den Verteilungspunkt verteilt haben. Treffen Sie eine Auswahl aus der Liste der Verteilungspakete, und führen Sie die folgenden Aktionen aus:  

- **Überprüfen:** Hiermit starten Sie den Vorgang zum Überprüfen der Integrität der Inhaltsdateien für die Software. Zum Anzeigen der Ergebnisse der Inhaltsprüfung erweitern Sie im Arbeitsbereich **Überwachung** den Bereich **Verteilungsstatus** und wählen Sie den Knoten **Inhaltsstatus** aus. Weitere Informationen finden Sie unter [Überprüfen von Inhalt](deploy-and-manage-content.md#validate-content).  

- **Neu verteilen:** Hiermit kopieren Sie alle Inhaltsdateien für die ausgewählte Software an den Verteilungspunkt und überschreiben die vorhandenen Dateien. Üblicherweise verwenden Sie diese Aktion, um Inhaltsdateien zu reparieren. Weitere Informationen finden Sie unter [Neuverteilen von Inhalt](deploy-and-manage-content.md#redistribute-content).  

- **Entfernen:** Hiermit entfernen Sie die Inhaltsdateien für die Software vom Verteilungspunkt. Weitere Informationen finden Sie unter [Entfernen von Inhalt](deploy-and-manage-content.md#remove-content).  

### <a name="content-validation"></a><a name="bkmk_config-valid"></a> Inhaltsprüfung  

Legen Sie einen Zeitplan für die Überprüfung der Integrität von Inhaltsdateien am Verteilungspunkt fest. Wenn Sie die Inhaltsprüfung nach einem Zeitplan aktivieren, startet Configuration Manager den Vorgang zum festgesetzten Zeitpunkt. Es werden alle Inhalte auf dem Verteilungspunkt anhand der lokalen Klasse „SMS_PackagesInContLib SCCMDP“ überprüft. Sie können auch die Priorität der Inhaltsprüfung konfigurieren. Standardmäßig ist die Priorität auf den Wert **Niedrigste (Standard)** festgelegt. Das Erhöhen der Priorität kann die Prozessor- und Datenträgernutzung auf dem Server während des Überprüfungsprozesses erhöhen, die Überprüfung wird dadurch in der Regel jedoch schneller abgeschlossen.

Zum Anzeigen der Ergebnisse der Inhaltsprüfung erweitern Sie im Arbeitsbereich **Überwachung** den Bereich **Verteilungsstatus** und wählen Sie den Knoten **Inhaltsstatus** aus. Der Inhalt jedes Softwaretyps (wie Anwendung, Softwareupdatepaket und Startimage) wird angezeigt.  

> [!WARNING]  
> Sie geben den Zeitplan für die Inhaltsprüfung zwar anhand der lokalen Zeit des Computers an, der Zeitplan wird in der Configuration Manager-Konsole jedoch anhand der UTC (Coordinated Universal Time, koordinierte Weltzeit) angezeigt.  

Weitere Informationen finden Sie unter [Überprüfen von Inhalt](deploy-and-manage-content.md#validate-content).

### <a name="boundary-groups"></a><a name="bkmk_config-boundary"></a> Boundary groups  

Verwalten Sie die Begrenzungsgruppen, denen Sie diesen Verteilungspunkt zuordnen. Fügen Sie den Verteilungspunkt zu mindestens einer Begrenzungsgruppe hinzu. Bei der Inhaltsbereitstellung müssen sich die Clients in einer Begrenzungsgruppe befinden, die einem Verteilungspunkt zugeordnet ist, damit dieser Verteilungspunkt als Quellspeicherort für Inhalt verwendet werden kann.

Konfigurieren Sie *Beziehungen* für Begrenzungsgruppen, die definieren, wann und auf welche Begrenzungsgruppen ein Client ausweichen kann, um nach Inhalten zu suchen. Weitere Informationen finden Sie unter [Begrenzungsgruppen](boundary-groups.md).

Klicken Sie auf **Hinzufügen**, und wählen Sie eine vorhandene Begrenzungsgruppe aus der Liste aus.

Klicken Sie auf **Erstellen**, um eine neue Begrenzungsgruppe für diesen Verteilungspunkt zu erstellen. Weitere Informationen zum Erstellen und Konfigurieren einer Begrenzungsgruppe finden Sie unter [Procedures for boundary groups (Prozeduren für Begrenzungsgruppen)](boundary-group-procedures.md).

Um die Eigenschaften eines zuvor installierten Verteilungspunkts zu bearbeiten, verwalten Sie die Option **Enable for on-demand distribution** (Für On-Demand-Verteilung aktivieren). Mit dieser Option kann Configuration Manager automatisch Inhalt auf diesen Server verteilen, wenn ein Client diesen anfordert. Weitere Informationen finden Sie unter [On-demand content distribution (Bedarfsgesteuerte Inhaltsverteilung)](../../../plan-design/hierarchy/fundamental-concepts-for-content-management.md#on-demand-content-distribution).

### <a name="schedule"></a><a name="bkmk_config-sched"></a> Zeitplan  

> [!NOTE]  
> Diese Optionen sind nur bei der Bearbeitung der Eigenschaften eines zuvor installierten Verteilungspunkts verfügbar.
>
> Diese Registerkarte ist nur verfügbar, wenn Sie die Eigenschaften für einen Verteilungspunkt bearbeiten, der sich an einem vom Standortserver entfernten Ort befindet.  

Konfigurieren Sie einen Zeitplan, durch den die Zeit eingeschränkt wird, zu der Configuration Manager Daten an den Verteilungspunkt übertragen kann. Schränken Sie Daten nach Priorität ein, oder schließen Sie die Verbindung für ausgewählte Zeiträume.

Wählen Sie das Zeitfenster im Raster und dann eine der folgenden Einschränkungen für **Verfügbarkeit** aus, um die Datenübertragungszeiten einzuschränken:  

- **Offen für alle Prioritäten:** Die Datenübertragung von Configuration Manager an den Verteilungspunkt erfolgt uneingeschränkt. Diese Einstellung ist die Standardeinstellung für alle Zeiträume.  

- **Nur mittlere und hohe Priorität zulassen:** Configuration Manager sendet nur Daten mit mittlerer und hoher Priorität an den Verteilungspunkt.  

- **Nur hohe Priorität zulassen:** Configuration Manager sendet nur Daten mit hoher Priorität an den Verteilungspunkt.  

- **Geschlossen:** Configuration Manager sendet keine Daten an den Verteilungspunkt.  

Konfigurieren Sie die **Verteilungspriorität** der Software auf der Registerkarte **Verteilungseinstellungen** der Softwareeigenschaften.

> [!IMPORTANT]  
> Der Zeitplan basiert auf der Zeitzone des sendenden Standorts, nicht auf der des Verteilungspunkts.  

### <a name="rate-limits"></a><a name="bkmk_config-rate"></a> Begrenzung der Datenübertragungsrate  

> [!NOTE]  
> Diese Optionen sind nur bei der Bearbeitung der Eigenschaften eines zuvor installierten Verteilungspunkts verfügbar.  
>
> Diese Registerkarte ist nur verfügbar, wenn Sie die Eigenschaften für einen Verteilungspunkt bearbeiten, der sich an einem vom Standortserver entfernten Ort befindet.  

Konfigurieren Sie eine Begrenzung der Datenübertragungsrate, um die Netzwerkbandbreite bei der Inhaltsübertragung durch Configuration Manager auf den Verteilungspunkt zu steuern. Wählen Sie aus den folgenden Optionen:  

- **Unbegrenzt beim Senden an dieses Ziel:** Die Inhaltsübertragung von Configuration Manager an den Verteilungspunkt erfolgt ohne Begrenzung der Datenübertragungsrate. Dies ist die Standardeinstellung.  

- **Pulsmodus:** Diese Option gibt die Größe der Datenblöcke an, die der Standortserver an den Verteilungspunkt sendet. Sie können auch eine zeitliche Verzögerung zwischen dem Senden der einzelnen Datenblöcke angeben. Verwenden Sie diese Option, wenn Sie Daten über Netzwerke mit sehr niedriger Bandbreite an den Verteilungspunkt senden müssen. Dies kann beispielsweise der Fall sein, wenn eine Beschränkung vorliegt, dass unabhängig von der Geschwindigkeit der Verknüpfung oder deren Auslastung zu einem bestimmten Zeitpunkt nur alle fünf Sekunden 1 KB Daten gesendet werden dürfen.  

- **Begrenzt auf angegebene maximale Übertragungsraten pro Stunde:** Geben Sie diese Einstellung an, damit die Datenübertragung auf einen Verteilungspunkt nur im konfigurierten Zeitanteil erfolgt. Wenn Sie diese Option verwenden, ermittelt Configuration Manager die verfügbare Netzwerkbandbreite nicht. Stattdessen teilt Configuration Manager die Zeit auf, während der Daten gesendet werden können. Der Server sendet während eines kurzen Zeitraums Daten, gefolgt von Zeiträumen, in denen keine Daten gesendet werden. Wenn Sie die Option **Verfügbare Bandbreite beschränken** beispielsweise auf **50 %** festlegen, überträgt Configuration Manager eine gewisse Zeit lang Daten, gefolgt von einer gleich langen Zeitspanne ohne Datenübertragung. Die tatsächliche Datenmenge bzw. die Größe der Datenblöcke wird nicht verwaltet. Mit dieser Option wird nur die Zeitspanne verwaltet, während der Daten gesendet werden.  
