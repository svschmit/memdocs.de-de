---
title: Erweitern der Hardwareinventur
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie die Hardwareinventur in Configuration Manager erweitern können.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: d5bfab4f-c55e-4545-877c-5c8db8bc1891
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 380ba550a6edb0f639644280df74c500663e19f4
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81695418"
---
# <a name="how-to-extend-hardware-inventory-in-configuration-manager"></a>Erweitern der Hardwareinventur in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Die Hardwareinventur liest Informationen von Windows-PCs mithilfe der Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI). Bei WMI handelt es sich um die Microsoft-Implementierung von Web-Based Enterprise Management (WBEM), einem Industriestandard für den Zugriff auf Verwaltungsinformationen in einem Unternehmen. In vorherigen Versionen von Configuration Manager konnten Sie die Hardwareinventur durch Ändern der Datei „sms_def.mof“ auf dem Standortserver erweitern. In dieser Datei war eine Liste der WMI-Klassen enthalten, die von der Hardwareinventur gelesen werden konnte. Durch das Bearbeiten dieser Datei konnten Sie vorhandene Klassen aktivieren und deaktivieren sowie neue Klassen in der Inventur erstellen.  

Die Datei „Configuration.mof“ wird zur Definition der Datenklassen verwendet, die von der Hardwareinventur auf dem Client inventarisiert werden. Sie wurde seit Configuration Manager 2012 nicht geändert. Datenklassen können erstellt werden, um vorhandene oder benutzerdefinierte WMI-Repositorydatenklassen oder -Registrierungsschlüssel auf Clientsystemen zu inventarisieren.  

 Die Datei "Configuration.MOF" wird auch definiert und registriert die WMI-Anbietern, die Geräteinformationen während der Hardwareinventur zugreifen. Durch das Registrieren von Anbietern werden der zu verwendende Anbietertyp sowie die vom Anbieter unterstützten Klassen definiert.  

 Wenn Configuration Manager-Clients Richtlinien anfordern, wird „Configuration.mof“ dem Richtlinientext angefügt. Diese Datei wird dann heruntergeladen und von Clients kompiliert. Beim Hinzufügen, ändern oder Löschen von Datenklassen aus der Datei "Configuration.MOF" Kompilieren Clients automatisch diese Änderungen Datenklassen Lagerbestand bezieht. Zum Inventarisieren neuer oder geänderter Datenklassen auf Configuration Manager-Clients sind keine weiteren Aktionen erforderlich. Diese Datei befindet sich auf primären Standortservern in **<Configuration Manager-Installationsort\>\Inboxes\clifiles.src\hinv\\** .  

 In Configuration Manager bearbeiten Sie nicht mehr die Datei „sms_def.mof“ wie in Configuration Manager 2007. Stattdessen aktivieren und deaktivieren Sie WMI-Klassen und fügen neue durch die Hardwareinventur zu erfassende Klassen mithilfe von Clienteinstellungen hinzu. Configuration Manager stellt die folgenden Methoden zum Erweitern der Hardwareinventur zur Verfügung.  

> [!NOTE]  
>  Wenn Sie die Datei „Configuration.mof“ zum Hinzufügen benutzerdefinierter Inventarklassen manuell geändert haben, werden diese Änderungen beim Update auf die Version 1602 überschrieben. Wenn Sie benutzerdefinierte Klassen nach der Aktualisierung weiterhin verwenden möchten, müssen Sie sie nach dem Update auf Version 1602 dem Abschnitt „Added extensions“ (Hinzugefügte Erweiterungen) der Datei „Configuration.mof“ hinzufügen.  
> Sie dürfen jedoch keine Elemente bearbeiten, die sich oberhalb dieses Abschnitts befinden, da diese Abschnitte für Änderungen durch Configuration Manager reserviert sind. Eine Sicherung Ihrer benutzerdefinierten Datei „Configuration.mof“ finden Sie unter:  
> **<Configuration Manager-Installationsverzeichnis\>\data\hinvarchive\\** .  

|Methode|Weitere Informationen|  
|------------|----------------------|  
|Aktivieren oder Deaktivieren von vorhandenen Inventurklassen|Aktivieren oder Deaktivieren Sie die Standardinventurklassen, oder erstellen Sie benutzerdefinierte Clienteinstellungen, mit denen Sie verschiedene Hardwareinventurklassen aus bestimmten Clientsammlungen sammeln können. Weitere Informationen finden Sie im Abschnitt [So aktivieren oder deaktivieren Sie vorhandene Inventurklassen](#BKMK_Enable) in diesem Artikel.|  
|Hinzufügen einer neuen Inventurklasse|Fügen Sie eine neue Inventurklasse aus dem WMI-Namespace eines anderen Geräts hinzu. Weitere Informationen finden im Abschnitt [So fügen Sie eine neue Inventurklasse hinzu](#BKMK_Add) in diesem Artikel.|  
|Importieren und Exportieren von Hardwareinventurklassen|Importieren und exportieren Sie MOF-Dateien (Managed Object Format), die Inventurklassen aus der Configuration Manager-Konsole enthalten. Weitere Informationen finden Sie in den Abschnitten [So importieren Sie Hardwareinventurklassen](#BKMK_Import) und [So exportieren Sie Hardwareinventurklassen](#BKMK_Export) in diesem Artikel.|  
|Erstellen von NOIDMIF-Dateien|Verwenden Sie NOIDMIF-Dateien zum Sammeln von Informationen zu Clientgeräten, die nicht von Configuration Manager inventarisiert werden können. Möglicherweise möchten z. B. Gerät Asset Informationen sammeln, die nur als Etikett auf dem Gerät vorhanden ist. NOIDMIF-Inventur wird automatisch das Clientgerät, dem er entnommen wurde zugeordnet. Weitere Informationen finden im Abschnitt [So erstellen Sie NOIDMIF-Dateien](#BKMK_NOIDMIF) in diesem Artikel.|  
|IDMIF-Dateien erstellen|Verwenden Sie IDMIF-Dateien zum Sammeln von Informationen zu Beständen in Ihrer Organisation, die keinem Configuration Manager-Client zugeordnet sind, z.B. Projektoren, Fotokopierer und Netzwerkdrucker. Weitere Informationen finden im Abschnitt [So erstellen Sie IDMIF-Dateien](#BKMK_IDMIF) in diesem Artikel.|  

## <a name="procedures-to-extend-hardware-inventory"></a>Verfahren zum Erweitern der Hardwareinventur  
Diese Vorgehensweisen können Sie die Standard-Clienteinstellungen für die Hardwareinventur konfigurieren, und sie gelten für alle Clients in Ihrer Hierarchie. Wenn diese Einstellungen nur auf manche Clients angewendet werden sollen, erstellen Sie eine benutzerdefinierte Clientgeräteeinstellung, und weisen Sie diese einer Sammlung von bestimmten Clients zu. Weitere Informationen finden Sie unter [Konfigurieren von Clienteinstellungen](../../../../core/clients/deploy/configure-client-settings.md).  

###  <a name="to-enable-or-disable-existing-inventory-classes"></a><a name="BKMK_Enable"></a> So aktivieren oder deaktivieren Sie vorhandene Inventurklassen  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** > **Clienteinstellungen** > **Clientstandardeinstellungen** aus.  

4.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.  

5.  Wählen Sie im Dialogfeld **Clientstandardeinstellungen** **Hardwareinventur** aus.  

6.  Klicken Sie in der Liste **Geräteeinstellungen** auf **Klassen festlegen**.  

7.  Wählen Sie im Dialogfeld **Hardwareinventurklassen** die Klassen oder Klasseneigenschaften aus, die von der Hardwareinventur gesammelt werden sollen, oder heben Sie deren Markierung auf. Sie können Klassen erweitern, damit einzelne Eigenschaften in der betreffenden Klasse aktiviert oder deaktiviert werden können. Verwenden Sie für die Suche nach einzelnen Klassen das Feld **Inventurklassen suchen** .  

    > [!IMPORTANT]  
    >  Wenn Sie neue Klassen zur Configuration Manager-Hardwareinventur hinzufügen, vergrößert sich die Inventurdatei, die gesammelt und an den Standortserver gesendet wird. Dies kann sich negativ auf die Leistung des Netzwerks und des Configuration Manager-Standorts auswirken. Aktivieren Sie nur die Inventurklassen, die Sie sammeln möchten.  


###  <a name="to-add-a-new-inventory-class"></a><a name="BKMK_Add"></a> So fügen Sie eine neue Inventurklasse hinzu  

Sie können Inventurklassen nur über den Server auf der obersten Ebene der Hierarchie und durch Ändern der Standardeinstellungen für den Client hinzufügen. Diese Option ist nicht verfügbar, wenn Sie benutzerdefinierte Geräteeinstellungen erstellen.

1. Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** > **Clienteinstellungen** > **Clientstandardeinstellungen** aus.  

2. Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.  

3. Wählen Sie im Dialogfeld **Clientstandardeinstellungen** **Hardwareinventur** aus.  

4. Wählen Sie in der Liste **Geräteeinstellungen** **Klassen festlegen** aus.  

5. Wählen Sie im Dialogfeld **Hardwareinventurklassen** **Hinzufügen** aus.  

6. Klicken Sie im Dialogfeld **Hardwareinventurklasse hinzufügen** auf **Verbinden**.  

7. Geben Sie im Dialogfeld **WMI-Verbindung herstellen** den Namen des Computers, von dem die WMI-Klassen abgerufen werden, sowie den WMI-Namespace ein, der zum Abrufen der Klassen verwendet werden soll. Klicken Sie auf **Rekursiv**, wenn Sie alle Klassen unterhalb des angegebenen WMI-Namespaces abrufen möchten. Wenn es sich bei dem Computer, zu dem Sie eine Verbindung herstellen, nicht um einen lokalen Computer handelt, geben Sie Anmeldeinformationen für ein Konto an, das über die Berechtigung verfügt, auf WMI auf dem Remotecomputer zuzugreifen.  

8. Wählen Sie **Verbinden** aus.  

9. Wählen Sie im Dialogfeld **Hardwareinventurklasse hinzufügen** in der Liste **Inventurklassen** die WMI-Klassen aus, die Sie der Configuration Manager-Hardwareinventur hinzufügen möchten.  

10. Wenn Sie Informationen zur ausgewählten WMI-Klasse bearbeiten möchten, wählen Sie **Bearbeiten** aus, und geben Sie im Dialogfeld **Klassenkennzeichner** die folgenden Informationen an:  

    - **Anzeigename:** Dieser Name wird im Ressourcen-Explorer angezeigt.  

    - **Eigenschaften** – Legen Sie die Einheiten fest, in denen jede Eigenschaft der WMI-Klasse angezeigt wird.  

      Sie können Eigenschaften auch als Schlüsseleigenschaft angeben, mit der jede Instanz der Klasse eindeutig bestimmt werden kann. Wenn kein Schlüssel für die Klasse definiert ist, und mehrere Instanzen der Klasse vom Client gemeldet werden, wird nur die aktuelle Instanz, die gefunden wird, in der Datenbank gespeichert.  

      Klicken Sie nach Abschluss der Konfiguration der Eigenschaften auf **OK**, um das Dialogfeld **Klassenkennzeichner** und die anderen geöffneten Dialogfelder zu schließen. 

###  <a name="to-import-hardware-inventory-classes"></a><a name="BKMK_Import"></a> So importieren Sie Hardwareinventurklassen  

Sie können Inventurklassen nur importieren, wenn Sie die Clientstandardeinstellungen ändern. Sie können jedoch mit benutzerdefinierten Clienteinstellungen Informationen importieren, die keine Schemaänderung enthalten. Bei einer solchen Änderung könnte beispielsweise die Eigenschaft einer vorhandenen Klasse von **TRUE** (Wahr) in **FALSE** (Falsch) geändert werden.  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** >  **Clienteinstellungen** > **Clientstandardeinstellungen** aus.  

4.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.  

5.  Wählen Sie im Dialogfeld **Clientstandardeinstellungen** **Hardwareinventur** aus.  

6.  Wählen Sie in der Liste **Geräteeinstellungen** **Klassen festlegen** aus.  

7.  Wählen Sie im Dialogfeld **Hardwareinventurklassen** **Importieren** aus.  

8.  Wählen Sie im Dialogfeld **Importieren** die MOF-Datei (Managed Object Format) aus, die Sie importieren möchten, und wählen Sie dann **OK** aus. Überprüfen Sie die Elemente, die importiert werden, und wählen Sie dann **Importieren** aus.  

###  <a name="to-export-hardware-inventory-classes"></a><a name="BKMK_Export"></a> So exportieren Sie Hardwareinventurklassen  

1.  Wählen Sie in der Configuration Manager-Konsole die Optionen **Verwaltung** > **Clienteinstellungen** > **Clientstandardeinstellungen** aus.  

4.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus.  

5.  Wählen Sie im Dialogfeld **Clientstandardeinstellungen** **Hardwareinventur** aus.  

6.  Wählen Sie in der Liste **Geräteeinstellungen** **Klassen festlegen** aus.  

7.  Wählen Sie im Dialogfeld **Hardwareinventurklassen** **Exportieren** aus.  

    > [!NOTE]  
    >  Wenn Sie Klassen exportieren, werden alle aktuell ausgewählten Klassen exportiert.  

8.  Legen Sie im Dialogfeld **Exportieren** die MOF-Datei (Managed Object Format) fest, in die Sie die Klassen exportieren möchten, und wählen Sie dann **Speichern** aus.  

### <a name="configure-hardware-inventory-to-collect-strings-larger-than-255-characters"></a><a name="bkmk_GreaterThan255"></a> Konfigurieren der Hardwareinventur zum Erfassen von Zeichenfolgen mit mehr als 255 Zeichen
Ab Configuration Manager Version 1802 können Sie festlegen, dass die Zeichenfolgenlänge für Hardwareinventureigenschaften 255 Zeichen überschreiten kann. Diese Änderung gilt nur für neu hinzugefügte Klassen und Eigenschaften der Hardwareinventur, bei denen es sich nicht um Schlüssel handelt. <!-- 1357389 -->

1. Klicken Sie im Arbeitsbereich **Verwaltung** auf die **Clienteinstellungen**, markieren Sie eine Einstellung des Clientgeräts, um diese zu bearbeiten, führen Sie einen Rechtsklick durch, und klicken Sie auf **Eigenschaften**.

2. Klicken Sie auf **Hardwareinventur** > **Klassen festlegen** > **Hinzufügen**.

3. Klicken Sie auf die Schaltfläche **Verbinden**.

4. Geben Sie einen **Computernamen** und einen **WMI-Namespace** ein, und klicken Sie ggf. auf **Rekursiv**. Geben Sie ggf. Anmeldeinformationen ein, um eine Verbindung herzustellen. Klicken Sie auf **Verbinden**, um die Namespaceklassen abzurufen.

5. Wählen Sie eine neue Klasse aus, und klicken Sie dann auf **Bearbeiten**.

6. Legen Sie für die **Länge** einer Eigenschaft, bei der es sich um eine Zeichenfolge und nicht um einen Schlüssel handelt, mehr als 255 Zeichen fest. Klicken Sie auf **OK**. 

7. Vergewissern Sie sich, dass die bearbeitete Eigenschaft für **Hardwareinventurklasse hinzufügen** ausgewählt ist, und klicken Sie auf **OK**. 


## <a name="how-to-use-management-information-files-mif-files-to-extend-hardware-inventory"></a>Verwenden von MIF (Management Information Format)-Dateien zum Erweitern der Hardwareinventur  
 Verwenden Sie MIF (Management Information Format)-Dateien zum Erweitern von Hardwareinventurinformationen, die Configuration Manager von Clients sammelt. Während der Hardwareinventur werden die in MIF-Dateien gespeicherten Informationen dem Clientinventurbericht hinzugefügt und in der Standortdatenbank gespeichert, wo Sie die Daten auf die gleiche Weise wie Standard-Clientinventurdaten verwenden können. Es gibt zwei Arten von MIF-Dateien: NOIDMIF und IDMIF.

> [!IMPORTANT]  
>  Vor dem Hinzufügen von Informationen aus MIF-Dateien an die Configuration Manager-Datenbank müssen Sie Klasseninformationen für sie erstellen oder importieren. Weitere Informationen finden Sie in den Abschnitten [So fügen Sie eine neue Inventurklasse hinzu](#BKMK_Add) und [So importieren Sie Hardwareinventurklassen](#BKMK_Import) in diesem Artikel.  

###  <a name="to-create-noidmif-files"></a><a name="BKMK_NOIDMIF"></a> So erstellen Sie NOIDMIF-Dateien  
 NOIDMIF-Dateien können verwendet werden, um einer Clienthardwareinventur Informationen hinzuzufügen, die normalerweise nicht durch Configuration Manager gesammelt werden können und einem bestimmten Clientgerät zugeordnet sind. Beispielsweise vergeben viele Unternehmen für alle Computer in der Organisation eine Bestandsnummer und katalogisieren diese dann manuell. Wenn Sie eine NOIDMIF-Datei erstellen, können diese Informationen der Configuration Manager-Datenbank hinzugefügt und für Abfragen und Berichte verwendet werden. Weitere Informationen zum Erstellen von NOIDMIF-Dateien finden Sie in der Configuration Manager SDK-Dokumentation.  

> [!IMPORTANT]  
>  Wenn Sie eine NOIDMIF-Datei erstellen, müssen Sie diese in einem ANSI-codierten Format speichern. In UTF-8-codiertem Format gespeicherte NOIDMIF-Dateien können nicht von Configuration Manager gelesen werden.  

 Nachdem Sie eine NOIDMIF-Datei erstellt haben, speichern Sie diese im Ordner _%Windir%_ **\CCM\Inventar\Noidmifs** auf jedem Client. Während des nächsten geplanten Hardwareinventurzyklus sammelt Configuration Manager Informationen aus NOIDMIF-Dateien in diesem Ordner.  

###  <a name="to-create-idmif-files"></a><a name="BKMK_IDMIF"></a> So erstellen Sie IDMIF-Dateien  
 Mithilfe von IDMIF-Dateien können Sie der Configuration Manager-Datenbank Informationen zu Beständen hinzufügen, die normalerweise nicht von Configuration Manager inventarisiert werden können und keinem bestimmten Clientgerät zugeordnet sind. In den IDMIF-Dateien können Sie z.B. Informationen zu Projektoren, DVD-Playern, Fotokopierern oder anderen Geräten sammeln, auf denen kein Configuration Manager-Client vorhanden ist. Weitere Informationen zum Erstellen von IDMIF-Dateien finden Sie in der Configuration Manager SDK-Dokumentation.  

 Nachdem Sie eine IDMIF-Datei erstellt haben, speichern Sie diese im Ordner _%Windir%_ **\CCM\Inventar\Idmifs** auf den Clientcomputern. Während des nächsten geplanten Hardwareinventurzyklus wird Configuration Manager Informationen aus dieser Datei sammeln. Sie müssen für die in der Datei enthaltenen Informationen neue Klassen deklarieren, indem Sie sie hinzufügen oder importieren.  

> [!NOTE]
> MIF-Dateien können große Datenmengen enthalten. Das Sammeln dieser Daten kann sich negativ auf die Leistung Ihres Standorts auswirken. Aktivieren Sie die MIF-Sammlung nur im Bedarfsfall, und konfigurieren Sie die Option **Maximale benutzerdefinierte MIF-Dateigröße (KB)** in den Einstellungen der Hardwareinventur. Weitere Informationen finden Sie unter [Einführung in die Hardwareinventur](introduction-to-hardware-inventory.md).
