---
title: Erstellen von Abfragen
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie in Configuration Manager Abfragen erstellen und importieren. Enthält Beispiele für Abfragen und Tipps.
ms.date: 05/08/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 868049d3-3209-47ec-b34a-9cc26941893a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 8d15252c3b3c93c7e90e517c502c4c3dd2dfcf20
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700043"
---
# <a name="create-queries-in-configuration-manager"></a>Erstellen von Abfragen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In diesem Artikel erfahren Sie, wie Sie in Configuration Manager Abfragen erstellen und importieren.  

##  <a name="create-a-query"></a><a name="BKMK_Create"></a> Erstellen einer Abfrage  
 Mit diesem Verfahren können Sie Abfragen in Configuration Manager erstellen.  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Wählen Sie im Arbeitsbereich **Überwachung** die Option **Abfragen** aus. Wählen Sie auf der Registerkarte **Start** in der Gruppe **Erstellen** die Option **Abfrage erstellen** aus.  

3.  Geben Sie auf der Registerkarte **Allgemein** im **Abfrageerstellungs-Assistenten** einen eindeutigen Namen und optional einen Kommentar für die Abfrage an.  

4.  Wenn Sie eine vorhandene Abfrage als Grundlage für die neue Abfrage importieren möchten, wählen Sie **Abfrageanweisung importieren** aus. Wählen Sie im Dialogfeld **Abfrage durchsuchen** eine Abfrage aus, die Sie importieren möchten, und klicken Sie dann auf **OK**.  

5.  Wählen Sie den Objekttyp, den die Abfrage zurückgeben soll, aus der Liste **Objekttyp** aus. In der folgenden Tabelle sind einige Beispiele für Objekttypen aufgeführt, nach denen Sie suchen können:  

    |Objekttyp|Beschreibung|  
    |-----------------|-----------------|  
    |**Systemressource**|Ermöglicht die Suche nach typischen Systemattributen wie NetBIOS-Name von Geräten, Clientversion, IP-Adresse des Clients und Active Directory Domain Services-Informationen.|  
    |**Benutzerressource**|Ermöglicht die Suche nach typischen Benutzerinformationen wie Benutzer-, Benutzergruppen- und Sicherheitsgruppennamen.|  
    |**Bereitstellung**|Ermöglicht die Suche nach typischen Attributen einer Bereitstellung wie Bereitstellungsname, Zeitplan sowie Sammlung, der die Bereitstellung zugewiesen wurde.|  

6.  Wählen Sie **Abfrageanweisung bearbeiten** aus, um das Dialogfeld &lt;Eigenschaften der \>Abfragename **-Anweisung** zu öffnen.  

7.  Geben Sie auf der Registerkarte **Allgemein** im Dialogfeld &lt;Eigenschaften der \>Abfragename **-Anweisung** die Attribute, die von der Abfrage zurückgegeben werden, sowie die Anzeigeart an. Klicken Sie auf das Symbol **Neu**, um ein neues Attribut hinzuzufügen. Sie können auch **Abfragesprache anzeigen** auswählen, um die Abfrage direkt in der WMI-Abfragesprache (WMI Query Language, WQL) einzugeben oder zu ändern. Beispiele für WMI-Abfragen finden Sie im Abschnitt [Beispiele von WQL-Abfragen](#BKMK_Example) in diesem Artikel.  

    > [!TIP]  
    > Mithilfe der folgenden Referenzdokumentation können Sie eigene WQL-Abfragen erstellen:  
    >   
    > -   [WQL (SQL für WMI)](/windows/win32/wmisdk/wql-sql-for-wmi)  
    > -   [WHERE-Klausel](/windows/win32/wmisdk/where-clause)  
    > -   [WQL-Operatoren](/windows/win32/wmisdk/wql-operators)  

8.  Geben Sie auf der Registerkarte **Kriterien** im Dialogfeld &lt;Eigenschaften der \>Abfragename **-Anweisung** Kriterien zum Optimieren der Abfrageergebnisse an. Sie könnten beispielsweise nur Ressourcen mit dem Standortcode **XYZ** zurückgeben lassen. Sie können mehrere Kriterien für eine Abfrage konfigurieren.  

    > [!IMPORTANT]  
    > Wenn Sie eine Abfrage ohne Kriterien erstellen, gibt diese alle Geräte in der Sammlung **Alle Systeme** aus.  

9. Auf der Registerkarte **Verknüpfungen** im Dialogfeld &lt;Eigenschaften der \>Abfragename **-Anweisung** können Sie Daten aus zwei verschiedenen Attributen in Ihren Abfrageergebnissen kombinieren. Von Configuration Manager werden zwar automatisch Abfrageverknüpfungen erstellt, wenn verschiedene Attribute für die Abfrageergebnisse ausgewählt werden, doch die Registerkarte **Verknüpfungen** bietet erweiterte Optionen. Configuration Manager unterstützt die folgenden Attributklassen:  

    |Verknüpfungstyp|Beschreibung|  
    |---------------|-----------------|  
    |Innerhalb|Zeigt nur übereinstimmende Ergebnisse an. Wird immer von automatisch erstellten Verknüpfungen verwendet.|  
    |Links|Zeigt alle Ergebnisse für das Basisattribut und nur die übereinstimmenden Ergebnisse für das Verknüpfungsattribut an.|  
    |Rechts|Zeigt alle Ergebnisse für das Verknüpfungsattribut und nur die übereinstimmenden Ergebnisse für das Basisattribut an.|  
    |Vollständig|Zeigt alle Ergebnisse für sowohl das Basisattribut als auch das Verknüpfungsattribut an.|  

     Weitere Informationen zum Verwenden von Verknüpfungsoperationen finden Sie in der SQL Server-Dokumentation.  

10. Klicken Sie auf **OK**, um das Dialogfeld &lt;Eigenschaften der \>Abfragename **-Anweisung** zu schließen.  

11. Geben Sie auf der Registerkarte **Allgemein** des **Abfrageerstellungs-Assistenten** an, dass die Ergebnisse der Abfrage auf die Mitglieder einer Sammlung bzw. auf die Mitglieder einer angegebenen Sammlung begrenzt werden sollen oder dass bei jeder Ausführung der Abfrage nach einer Sammlung gefragt werden soll.  

12. Schließen Sie den Abfrageerstellungs-Assistenten ab. Die neue Abfrage wird im Knoten **Abfragen** des Arbeitsbereichs **Überwachung** angezeigt.  

##  <a name="import-a-query"></a><a name="BKMK_Import"></a> Importieren einer Abfrage  
 Verwenden Sie dieses Verfahren, um eine Abfrage in Configuration Manager zu importieren. Informationen zum Exportieren von Abfragen finden Sie unter [Verwalten von Abfragen](../../../core/servers/manage/manage-queries.md).  

1.  Klicken Sie in der Configuration Manager-Konsole auf **Überwachung**.  

2.  Wählen Sie im Arbeitsbereich **Überwachung** die Option **Abfragen** aus. Wählen Sie auf der Registerkarte **Start** in der Gruppe **Erstellen** die Option **Objekte importieren** aus.  

3.  Wählen Sie auf der Seite **MOF-Dateiname** des **Assistenten zum Importieren von Objekten** die Option **Durchsuchen** aus, um die MOF-Datei (Managed Object Format) mit der zu importierenden Abfrage auszuwählen.  

4.  Überprüfen Sie die Informationen zur Abfrage, die importiert werden soll, und schließen Sie den Assistenten ab. Die neue Abfrage wird im Knoten **Abfragen** des Arbeitsbereichs **Überwachung** angezeigt.  

##  <a name="example-wql-queries"></a><a name="BKMK_Example"></a> Example WQL queries

Dieser Abschnitt enthält Beispiele für WQL-Abfragen, die Sie in Ihrer Hierarchie verwenden oder für andere Zwecke ändern können. Um diese Abfragen zu verwenden, wählen Sie im Dialogfeld **Eigenschaften der Abfrageanweisung** die Option **Abfragesprache anzeigen** aus. Kopieren Sie anschließend die Abfrage in das Feld **Abfrageanweisung**.  

> [!TIP]  
> Verwenden Sie das Platzhalterzeichen `%`, um eine beliebige Zeichenfolge anzugeben. `%Visio%` gibt beispielsweise „Microsoft Office Visio 2010“ zurück.  

### <a name="computers-that-run-windows-10"></a>Computer, auf denen Windows 10 ausgeführt wird

Verwenden Sie die folgende Abfrage, um den NetBIOS-Namen und die Betriebssystemversion aller Computer mit Windows 7 zurückgegeben.  

``` WQL
select SMS_R_System.NetbiosName,  
SMS_R_System.OperatingSystemNameandVersion from
SMS_R_System where
SMS_R_System.OperatingSystemNameandVersion like "%Workstation 10%"  
```  

### <a name="computers-with-a-specific-software-package-installed"></a>Computer, auf denen ein bestimmtes Softwarepaket installiert ist  

Verwenden Sie die folgende Abfrage, um den NetBIOS-Namen und den Softwarepaketnamen aller Computer zurückzugeben, auf denen ein bestimmtes Softwarepaket installiert ist. In diesem Beispiel werden alle Computer zurückgegeben, auf denen eine Version von Microsoft Visio installiert ist. Ersetzen Sie `Microsoft%Visio%` durch das Softwarepaket, nach dem Sie mit der Abfrage suchen möchten.  

> [!TIP]  
> Diese Abfrage sucht anhand der Namen, die in der Liste der Programme in der Windows-Systemsteuerung angezeigt werden, nach dem Softwarepaket.  

``` WQL
select SMS_R_System.NetbiosName,
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName from
SMS_R_System inner join SMS_G_System_ADD_REMOVE_PROGRAMS on
SMS_G_System_ADD_REMOVE_PROGRAMS.ResourceId =
SMS_R_System.ResourceId where
SMS_G_System_ADD_REMOVE_PROGRAMS.DisplayName like "Microsoft%Visio%"  
```  

### <a name="computers-in-a-specific-active-directory-domain-services-organizational-unit"></a>Computer in einer bestimmten Active Directory Domain Services-Organisationseinheit

Verwenden Sie die folgende Abfrage, um den NetBIOS-Namen und den Namen der Organisationseinheit (Organizational Unit, OU) aller Computer in einer bestimmten Organisationseinheit zurückzugeben. Ersetzen Sie den Text `OU Name` durch den Namen der Organisationseinheit, nach der Sie mit der Abfrage suchen möchten.  

``` WQL
select SMS_R_System.NetbiosName,
SMS_R_System.SystemOUName from
SMS_R_System where
SMS_R_System.SystemOUName = "OU Name"  
```  

### <a name="computers-with-a-specific-netbios-name"></a>Computer mit einem bestimmten NetBIOS-Namen

Verwenden Sie die folgende Abfrage, um den NetBIOS-Namen aller Computer zurückzugeben, die mit einer bestimmten Zeichenfolge beginnen. In diesem Beispiel gibt die Abfrage alle Computer mit einem NetBIOS-Namen zurück, der mit `ABC` beginnt.  

``` WQL
select SMS_R_System.NetbiosName from
SMS_R_System where SMS_R_System.NetbiosName like "ABC%"  
```  

###  <a name="devices-of-a-specific-type"></a><a name="BKMK_DeviceType"></a> Geräte eines bestimmten Typs

Gerätetypen werden in der Configuration Manager-Datenbank unter der Ressourcenklasse **sms_r_system** und dem Attributnamen **AgentEdition** gespeichert. Verwenden Sie die folgende Abfrage, um nur die Geräte abzurufen, die mit der angegebenen Agent-Edition des Gerätetyps übereinstimmen:  

``` WQL
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = <Device ID>  
```  

Verwenden Sie einen der folgenden Werte für &lt;Geräte-ID\>:  

|Gerätetyp|Wert von „AgentEdition“|  
|-----------------|---------------------------|  
|Windows-Desktop oder -Laptop|0|  
|Windows-ARM-basiertes Gerät (mit Windows RT)|1|  
|Windows Mobile 6.5|2|  
|Nokia Symbian|3|  
|Windows Phone|4|  
|Macintosh-Computer|5|  
|Windows CE|6|  
|Windows Embedded|7|  
|Intel-System auf einem Chip|12|  
|UNIX- und Linux-Server|13|  
|Microsoft HoloLens (MDM)|15|
|Microsoft Surface Hub (MDM)|16|

> [!NOTE]
> Werte, die in dieser Tabelle nicht aufgeführt sind, sind Geräten zugeordnet, die nicht mehr unterstützt werden.

<!-- removed with hybrid EOL
|iOS|8|  
|iPad|9|  
|iPod touch|10|  
|Android|11|  
|Apple macOS (MDM)|14|
|Android for Work|17|
 -->

Wenn die Abfrage z.B. nur Mac-Computer zurückgeben soll, verwenden Sie die folgende Abfrage:  

``` WQL
Select SMS_R_System.ClientEdition from SMS_R_System where SMS_R_System.ClientEdition = 5  
```  

## <a name="next-steps"></a>Nächste Schritte

[Verwalten von Abfragen](manage-queries.md)