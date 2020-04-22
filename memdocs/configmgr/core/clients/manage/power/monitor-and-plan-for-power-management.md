---
title: Überwachen und Planen der Energieverwaltung
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie die Energieverwaltung in Configuration Manager überwachen und planen.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 507bf676-2679-4e4d-8831-3ffc9cf8557e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: a4e5ee9c35dd96f79ea1a88ab09200d4386a7535
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696558"
---
# <a name="how-to-monitor-and-plan-for-power-management-in-configuration-manager"></a>Überwachen und Planen der Energieverwaltung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Überwachen und planen Sie die Energieverwaltung in Configuration Manager anhand der folgenden Informationen.  

##  <a name="how-to-use-reports-for-power-management"></a><a name="BKMK_How_to_use_reports"></a> Verwenden von Berichten für die Energieverwaltung  
 In der Energieverwaltung in Configuration Manager sind verschiedene Berichte enthalten, um die Analyse von Energieverbrauch und Energieeinstellungen der Computer Ihrer Organisation zu vereinfachen. Die Berichte können auch zur Problembehandlung verwendet werden.  

 Bevor Sie Energieverwaltungsberichte verwenden können, müssen Sie die Berichterstattung für Ihre Hierarchie konfigurieren. Weitere Informationen zur Berichterstellung in Configuration Manager finden Sie unter [Einführung in die Berichterstellung](../../../servers/manage/introduction-to-reporting.md).  

> [!NOTE]  
>  Energieverwaltungsinformationen, die für Tagesberichte verwendet werden, bleiben 31 Tage lang in der Configuration Manager-Standortdatenbank gespeichert.  
>           Energieverwaltungsinformationen, die für Monatsberichte verwendet werden, bleiben 13 Monate lang in der Configuration Manager-Standortdatenbank gespeichert.  
>   
>  Wenn Sie während der Überwachungs- und Planungsphase bzw. während der Kompatibilitätsphase der Energieverwaltung Berichte ausführen, dann speichern oder exportieren Sie die Ergebnisse aller Berichte, deren Daten Sie zum späteren Vergleich behalten möchten, für den Fall, dass sie später von Configuration Manager entfernt werden.  

## <a name="list-of-power-management-reports"></a>Liste der Energieverwaltungsberichte  
 In der folgenden Liste sind die in Configuration Manager verfügbaren Energieverwaltungsberichte aufgeführt.  

> [!NOTE]  
>  In Energieverwaltungsberichten wird die Anzahl physischer sowie virtueller Computer in einer ausgewählten Sammlung angezeigt. Es werden allerdings nur für physische Computer Energieverwaltungsinformationen angezeigt.  

###  <a name="computer-activity-report"></a><a name="BKMK_Activity"></a> Bericht "Computeraktivität"  
 Im Bericht **Computeraktivität** wird ein Diagramm mit der folgenden Aktivität für eine angegebene Sammlung über einen bestimmten Zeitraum angezeigt:  

- **Computer Ein** : Der Computer war eingeschaltet.  

- **Monitor Ein** : Der Monitor war eingeschaltet.  

- **Benutzer aktiv** : Aktivität von der Computermaus, der Computertastatur oder einer Remotedesktopverbindung mit dem Computer wurde erkannt.  

  Dieser Bericht wird während der Überwachungs-, Planungs- und Erzwingungsphasen verwendet, um das Zusammenwirken zwischen Computeraktivität, Monitoraktivität und Benutzeraktivität über einen Zeitraum von 24 Stunden zu erfassen. Wenn Sie diesen Bericht über mehrere Tage hinweg ausführen, werden die Daten dieses Zeitraums aggregiert. Verwenden Sie den Bericht, um typische Haupt- und Nebenzeiten für eine bestimmte Sammlung zu bestimmen und zu entscheiden, zu welchen Zeiten konfigurierte Energiesparpläne angewendet werden sollen.  

  Das Diagramm zeigt Zeiträume, in denen ein Computer möglicherweise eingeschaltet ist, jedoch keine Benutzeraktivität festgestellt wird. Erwägen Sie, in diesen Zeiten restriktivere Energieeinstellungen anzuwenden, um Energiekosten bei Computern zu sparen, die eingeschaltet sind, aber nicht verwendet werden. Ein Computer gilt als aktiv, wenn pro dargestellter Stunde im Diagramm mindestens eine Minute lang Prozessor-, Benutzer- oder Monitoraktivitäten festgestellt werden. Wenn von einem Computer keine Energieverwaltungsdaten gemeldet werden, wird er nicht in den Bericht **Computeraktivität** eingeschlossen.  

  Verwenden Sie die folgenden Parameter, um diesen Bericht zu konfigurieren.  

#### <a name="required-report-parameters"></a>Erforderliche Berichtsparameter  
 Die folgenden Parameter müssen angegeben werden, um diesen Bericht auszuführen.  

|Parametername|Beschreibung|  
|--------------------|-----------------|  
|**Startdatum**|Wählen Sie in der Dropdownliste das Startdatum für diesen Bericht aus.|  
|**Enddatum (optional)**|Wählen Sie in der Dropdownliste ein optionales Enddatum für diesen Bericht aus.|  
|**Sammlungsnamen**|Wählen Sie in der Dropdownliste eine Sammlung aus, auf die sich der Bericht bezieht.|  
|**Gerätetyp**|Wählen Sie in der Dropdownliste den Computertyp aus, für den ein Bericht erstellt werden soll. Gültige Werte sind **Alle** (Desktop- und tragbare Computer), **Desktop** (nur Desktopcomputer) und **Laptop** (nur tragbare Computer).|  

#### <a name="hidden-report-parameters"></a>Ausgeblendete Berichtsparameter  
 Dieser Bericht hat keine ausgeblendeten Parameter, die Sie festlegen können.  

#### <a name="report-links"></a>Berichtslinks  
 Wenn für die Option **Enddatum (optional)** kein Wert festgelegt wird, enthält dieser Bericht einen Link zu dem folgenden Bericht, der weitere Informationen enthält.  

|Berichtsname|Details|  
|-----------------|-------------|  
|**Computeraktivitätsdetails**|Klicken Sie auf den Link **Klicken Sie hier, um detaillierte Informationen anzuzeigen** , um eine Liste aktiver, inaktiver und nicht meldender Computer für das angegebene Datum anzuzeigen.<br /><br /> Weitere Informationen finden Sie unter [Computer Activity Details Report](#BKMK_Activity_Details) in diesem Thema.|  

###  <a name="computer-activity-by-computer-report"></a><a name="BKMK_Comp_Activity_by_computer"></a> Bericht "Computeraktivität nach Computer"  
 Im Bericht **Computeraktivität nach Computer** wird ein Diagramm mit der folgenden Aktivität für einen angegebenen Computer an einem bestimmten Datum angezeigt:  

- **Computer Ein** : Der Computer war eingeschaltet.  

- **Monitor Ein** : Der Monitor war eingeschaltet.  

- **Benutzer aktiv** : Aktivität von der Computermaus, der Computertastatur oder einer Remotedesktopverbindung mit dem Computer wurde erkannt.  

  Dieser Bericht kann unabhängig ausgeführt oder vom Bericht **Computeraktivitätsdetails** aus aufgerufen werden.  

> [!NOTE]  
>  Während der Hardwareinventur werden von Clientcomputern Informationen zur Computeraktivität gesammelt. Je nach der Uhrzeit, zu der die Hardwareinventur ausgeführt wird, können Aktivitäten während aktiver Haupt- und Nebenzeitenergiesparpläne gesammelt werden.  

 Verwenden Sie die folgenden Parameter, um diesen Bericht zu konfigurieren.  

#### <a name="required-report-parameters"></a>Erforderliche Berichtsparameter  
 Die folgenden Parameter müssen angegeben werden, um diesen Bericht auszuführen.  

|Parametername|Beschreibung|  
|--------------------|-----------------|  
|**Berichtsdatum**|Wählen Sie in der Dropdownliste ein Datum für diesen Bericht aus.|  
|**Computername**|Geben Sie den Namen eines Computers ein, für den ein Bericht erstellt werden soll.|  

#### <a name="hidden-report-parameters"></a>Ausgeblendete Berichtsparameter  
 Dieser Bericht hat keine ausgeblendeten Parameter, die Sie festlegen können.  

#### <a name="report-links"></a>Berichtslinks  
 Dieser Bericht enthält Links zum folgenden Bericht, in dem weitere Informationen zum ausgewählten Element bereitgestellt werden.  

|Berichtsname|Details|  
|-----------------|-------------|  
|**Computerdetails**|Klicken Sie auf den Link **Klicken Sie hier, um detaillierte Informationen anzuzeigen** , um die Energiefunktionen, Energieeinstellungen und angewendeten Energiesparpläne für den ausgewählten Computer anzuzeigen.|  

###  <a name="computer-activity-details-report"></a><a name="BKMK_Activity_Details"></a> Computer Activity Details report  
 Im Bericht **Computeraktivitätsdetails** wird eine Liste aktiver bzw. inaktiver Computer mit ihren Standby- und Aktivierungsfunktionen angezeigt. In diesem Bericht wird aufgerufen, indem die [Computer Activity Report](#BKMK_Activity) und nicht direkt vom Administrator ausgeführt werden soll.  

 Verwenden Sie die folgenden Parameter, um diesen Bericht zu konfigurieren.  

#### <a name="required-report-parameters"></a>Erforderliche Berichtsparameter  
 Die folgenden Parameter müssen angegeben werden, um diesen Bericht auszuführen.  

|Parametername|Beschreibung|  
|--------------------|-----------------|  
|**Sammlungsnamen**|Wählen Sie in der Dropdownliste eine Sammlung aus, auf die sich der Bericht bezieht.|  
|**Berichtsdatum**|Wählen Sie in der Dropdownliste ein Datum für diesen Bericht aus.|  
|**Berichtsstunde**|Wählen Sie in der Dropdownliste eine Stunde aus, zu der dieser Bericht am angegebenen Datum ausgeführt werden soll. Gültige Werte liegen zwischen **00.00 Uhr** und **23.00 Uhr**.|  
|**Computerstatus**|Wählen Sie in der Dropdownliste den Computerstatus aus, für den dieser Bericht ausgeführt werden soll. Gültige Werte sind **Alle** (Computer, die aktiviert oder deaktiviert wurden), **Ein** (Computer, die eingeschaltet wurden) und **Aus** (Computer, die ausgeschaltet wurden oder sich im Standbymodus oder im Ruhezustand befinden). Diese Werte werden nur für den ausgewählten Berichtszeitraum zurückgegeben.|  
|**Gerätetyp**|Wählen Sie in der Dropdownliste den Computertyp aus, für den ein Bericht erstellt werden soll. Gültige Werte sind **Alle** (Desktop- und tragbare Computer), **Desktop** (nur Desktopcomputer) und **Laptop** (nur tragbare Computer). Diese Werte werden nur für den ausgewählten Berichtszeitraum zurückgegeben.|  
|**Standbyfähig**|Wählen Sie in der Dropdownliste aus, ob im Bericht standbyfähige Computer angezeigt werden sollen. Gültige Werte sind **Alle** (Computer, die standbyfähig und die nicht standbyfähig sind), **Nein** (Computer, die nicht standbyfähig sind) und **Ja** (Computer, die standbyfähig sind).|  
|**Aktivierungsfähig nach Standbymodus**|Wählen Sie in der Dropdownliste aus, ob im Bericht Computer angezeigt werden sollen, die nach dem Standbymodus aktivierungsfähig sind. Gültige Werte sind **Alle** (Computer, die nach dem Standbymodus aktivierungsfähig und die nicht nach dem Standbymodus aktivierungsfähig sind), **Nein** (Computer, die nicht nach dem Standbymodus aktivierungsfähig sind) und **Ja** (Computer, die nach dem Standbymodus aktivierungsfähig sind).|  
|**Energiesparplan**|Wählen Sie in der Dropdownliste die Energiesparplantypen aus, die im Bericht angezeigt werden sollen. Gültige Werte sind **Alle** (Computer, ohne Energieverwaltungspläne; Computer mit Energieverwaltungsplan; aus der Energieverwaltung ausgeschlossene Computer), **Nicht angegeben** (Computer ohne Energieverwaltungsplan), **Definiert** (Computer mit Energieverwaltungsplan) und **Ausgeschlossen** (Computer, die aus der Energieverwaltung ausgeschlossen wurden).|  
|**Betriebssystem**|Wählen Sie in der Dropdownliste die Computerbetriebssysteme aus, die im Bericht angezeigt werden sollen, oder wählen Sie **Alle** aus, damit alle Betriebssysteme angezeigt werden.|  

#### <a name="hidden-report-parameters"></a>Ausgeblendete Berichtsparameter  
 Dieser Bericht hat keine ausgeblendeten Parameter, die Sie festlegen können.  

#### <a name="report-links"></a>Berichtslinks  
 Dieser Bericht enthält Links zum folgenden Bericht, in dem weitere Informationen zum ausgewählten Element bereitgestellt werden.  

|Berichtsname|Details|  
|-----------------|-------------|  
|**Computeraktivität nach Computer**|Klicken Sie auf einen Computernamen, um bestimmte Aktivitäten für diesen Computer über einer angegebenen Berichtszeitraum anzuzeigen. Hierzu zählen **Computer ein** (wurde der Computer eingeschaltet?), **Monitor ein** (wurde der Monitor eingeschaltet?) und **Benutzer aktiv** (Aktivität von der Computermaus, der Computertastatur oder einer Remotedesktopverbindung wurde erkannt).<br /><br /> Weitere Informationen finden Sie unter [Computer Activity by Computer Report](#BKMK_Comp_Activity_by_computer) in diesem Thema.|  

###  <a name="computer-details-report"></a><a name="BKMK_Computer_Details"></a> Bericht "Computerdetails"  
 Im Bericht **Computerdetails** werden detaillierte Informationen über Energiefunktionen, Energieeinstellungen und aktive Energiesparpläne eines bestimmten Computers angezeigt. Dieser Bericht wird von den Berichten **Computeraktivität nach Computer** , **Computer mit mehreren Energiesparplänen** , **Energiefunktionen** und **Energieeinstellungsdetails** aus aufgerufen. Es wird nicht direkt vom Standortadministrator ausgeführt.  

#### <a name="required-report-parameters"></a>Erforderliche Berichtsparameter  
 Die folgenden Parameter müssen angegeben werden, um diesen Bericht auszuführen.  

|Parametername|Beschreibung|  
|--------------------|-----------------|  
|**Computername**|Geben Sie den Namen eines Computers ein, für den ein Bericht erstellt werden soll.|  
|**Energiesparmodus**|Wählen Sie in der Dropdownliste den Typ der Energieeinstellungen aus, der in den Berichtergebnissen angezeigt werden soll. Wählen Sie **Netzbetrieb** aus, um die Energieeinstellungen anzuzeigen, die für den Fall konfiguriert wurden, dass der Computer im Netzbetrieb ausgeführt wird. Wählen Sie **Akkubetrieb** aus, um die Energieeinstellungen anzuzeigen, die für den Fall konfiguriert wurden, dass der Computer im Akkubetrieb ausgeführt wird.|  

#### <a name="hidden-report-parameters"></a>Ausgeblendete Berichtsparameter  
 Für diesen Bericht gibt es keine ausgeblendeten Parameter, die festgelegt werden können.  

#### <a name="report-links"></a>Berichtslinks  
 Dieser Bericht enthält keine Links zu anderen Energieverwaltungsberichten.  

###  <a name="computer-not-reporting-details-report"></a><a name="BKMK_Not_Reporting"></a> Bericht "Computer meldet keine Details"  
 Im Bericht **Computer meldet keine Details** wird eine Liste von Computern in einer bestimmten Sammlung angezeigt, von denen an einem bestimmten Datum zu einer bestimmten Uhrzeit keine Energieaktivitäten gemeldet wurden. Dieser Bericht wird durch den **Computer Activity Report** aufgerufen und sollte nicht direkt vom Standortadministrator ausgeführt werden.  

> [!NOTE]  
>  Energieverwaltungsinformationen werden von Computern als Teil des Hardwareinventur-Zeitplans gemeldet. Bevor Sie einen Computer als nicht meldend betrachten, vergewissern Sie sich, dass von ihm Hardwareinventar gemeldet wurden.  

 Verwenden Sie die folgenden Parameter, um diesen Bericht zu konfigurieren.  

#### <a name="required-report-parameters"></a>Erforderliche Berichtsparameter  
 Die folgenden Parameter müssen angegeben werden, um diesen Bericht auszuführen.  

|Parametername|Beschreibung|  
|--------------------|-----------------|  
|**Sammlungsnamen**|Wählen Sie in der Dropdownliste eine Sammlung aus, auf die sich der Bericht bezieht.|  
|**Berichtsdatum**|Wählen Sie in der Dropdownliste ein Datum für diesen Bericht aus.|  
|**Berichtsstunde**|Wählen Sie in der Dropdownliste eine Stunde aus, zu der dieser Bericht am angegebenen Datum ausgeführt werden soll. Gültige Werte liegen zwischen **00.00 Uhr** und **23.00 Uhr**.|  
|**Gerätetyp**|Wählen Sie in der Dropdownliste den Computertyp aus, für den ein Bericht erstellt werden soll. Gültige Werte sind **Alle** (Desktop- und tragbare Computer), **Desktop** (nur Desktopcomputer) und **Laptop** (nur tragbare Computer). Diese Werte werden nur für den ausgewählten Berichtszeitraum zurückgegeben.|  

#### <a name="hidden-report-parameters"></a>Ausgeblendete Berichtsparameter  
 Dieser Bericht hat keine ausgeblendeten Parameter, die Sie festlegen können.  

#### <a name="report-links"></a>Berichtslinks  
 Dieser Bericht enthält keine Links zu anderen Energieverwaltungsberichten.  

###  <a name="computers-excluded"></a><a name="BKMK_Excluded"></a> Ausgeschlossene Computer  
 Im Bericht **Ausgeschlossene Computer** wird eine Liste von Computern einer bestimmten Sammlung angezeigt, die aus der Configuration Manager-Energieverwaltung ausgeschlossen wurden.  

 Verwenden Sie die folgenden Parameter, um diesen Bericht zu konfigurieren.  

#### <a name="required-report-parameters"></a>Erforderliche Berichtsparameter  
 Die folgenden Parameter müssen angegeben werden, um diesen Bericht auszuführen.  

|Parametername|Beschreibung|  
|--------------------|-----------------|  
|**Sammlung**|Wählen Sie in der Dropdownliste eine Sammlung aus, auf die sich dieser Bericht bezieht.|  
|**Grund**|Wählen Sie in der Dropdownliste den Grund aus, aus dem die Computer aus der Energieverwaltung ausgeschlossen wurden. Sie können Folgendes anzeigen: **Alle** (alle ausgeschlossenen Computer), **Von Administrator ausgeschlossen** (nur Computer, die von einem Administrator ausgeschlossen wurden) und **Von Benutzer ausgeschlossen** (nur Computer, die von einem Softwarecenterbenutzer ausgeschlossen wurden).|  

#### <a name="hidden-report-parameters"></a>Ausgeblendete Berichtsparameter  
 Dieser Bericht hat keine ausgeblendeten Parameter, die Sie festlegen können.  

#### <a name="report-links"></a>Berichtslinks  
 Dieser Bericht enthält Links zum folgenden Bericht, in dem weitere Informationen zum ausgewählten Element bereitgestellt werden.  

|Berichtsname|Details|  
|-----------------|-------------|  
|**Energie Computerdetails**|Klicken Sie auf einen Computernamen, um die Energiefunktionen, Energieeinstellungen und angewendeten Energiesparpläne des ausgewählten Computers anzuzeigen.<br /><br /> Weitere Informationen finden Sie unter [Computer Details Report](#BKMK_Computer_Details) in diesem Thema.|  

###  <a name="computers-with-multiple-power-plans"></a><a name="BKMK_Multiple"></a> Computer mit mehreren Energiesparplänen  
 Im Bericht **Computer mit mehreren Energiesparplänen** wird eine Liste von Computern angezeigt, die Mitglieder mehrerer Sammlungen mit jeweils verschiedenen Energiesparplänen sind. Es werden für jeden Computer mit möglicherweise in Konflikt stehenden Energieeinstellungen der Computername und die Energiesparpläne angezeigt, die für jede Sammlung angewendet werden, in der der Computer Mitglied ist.  

> [!IMPORTANT]  
>  Wenn ein Computer Mitglied mehrerer Sammlungen ist und jede Sammlung über unterschiedliche Energiesparpläne verfügt, wird der am wenigsten einschränkende Energiesparplan angewendet.  
>   
>  Wenn ein Computer Mitglied mehrerer Sammlungen ist und jede Sammlung über unterschiedliche Aktivierungszeiten verfügt, wird die der Mitternacht nächste Uhrzeit verwendet.  

 Verwenden Sie die folgenden Parameter, um diesen Bericht zu konfigurieren.  

#### <a name="required-report-parameters"></a>Erforderliche Berichtsparameter  
 Die folgenden Parameter müssen angegeben werden, um diesen Bericht auszuführen.  

|Parametername|Beschreibung|  
|--------------------|-----------------|  
|**Sammlungsnamen**|Wählen Sie in der Dropdownliste eine Sammlung aus, auf die sich dieser Bericht bezieht.|  

#### <a name="hidden-report-parameters"></a>Ausgeblendete Berichtsparameter  
 Dieser Bericht hat keine ausgeblendeten Parameter, die Sie festlegen können.  

#### <a name="report-links"></a>Berichtslinks  
 Dieser Bericht enthält Links zum folgenden Bericht, in dem weitere Informationen zum ausgewählten Element bereitgestellt werden.  

|Berichtsname|Details|  
|-----------------|-------------|  
|**Energie Computerdetails**|Klicken Sie auf einen Computernamen, um die Energiefunktionen, Energieeinstellungen und angewendeten Energiesparpläne des ausgewählten Computers anzuzeigen.<br /><br /> Weitere Informationen finden Sie unter [Computer Details Report](#BKMK_Computer_Details) in diesem Thema.|  

###  <a name="energy-consumption-report"></a><a name="BKMK_Consumption"></a> Bericht "Stromverbrauch"  
 Im Bericht **Stromverbrauch** werden die folgenden Informationen angezeigt:  

- In einem Diagramm wird für die angegebene Sammlung und den angegebenen Zeitraum der gesamte monatliche Stromverbrauch der Computer in Kilowattstunden (kWh) angezeigt.  

- In einem Diagramm wird für die angegebene Sammlung und den angegebenen Zeitraum der durchschnittliche Stromverbrauch jedes Computers in Kilowattstunden (kWh) angezeigt.  

- In einer Tabelle werden für die angegebene Sammlung und den angegebenen Zeitraum der gesamte monatliche Stromverbrauch in Kilowattstunden (kWh) und der durchschnittliche Stromverbrauch der Computer angezeigt.  

  Mithilfe dieser Informationen können Sie Trends beim Stromverbrauch in Ihrer Umgebung erkennen. Der Stromverbrauch von Computern sollte nach der Anwendung eines Energiesparplans auf Computer in der ausgewählten Sammlung sinken.  

> [!NOTE]  
>  Wenn Sie nach der Anwendung eines Energiesparplans Mitglieder zur Sammlung hinzufügen bzw. daraus entfernen, hat dies Einfluss auf die Ergebnisse, die vom Bericht **Stromverbrauch** angezeigt werden, und erschwert den Vergleich von Ergebnissen aus der Überwachungs- und Planungsphase mit der Erzwingungsphase.  

 Verwenden Sie die folgenden Parameter, um diesen Bericht zu konfigurieren.  

#### <a name="required-report-parameters"></a>Erforderliche Berichtsparameter  
 Die folgenden Parameter müssen angegeben werden, um diesen Bericht auszuführen.  

|Parametername|Beschreibung|  
|--------------------|-----------------|  
|**Startdatum**|Wählen Sie in der Dropdownliste ein Startdatum für diesen Bericht aus.|  
|**Enddatum**|Wählen Sie in der Dropdownliste ein Enddatum für diesen Bericht aus.|  
|**Sammlungsnamen**|Wählen Sie in der Dropdownliste eine Sammlung aus, auf die sich dieser Bericht bezieht.|  
|**Gerätetyp**|Wählen Sie in der Dropdownliste den Computertyp aus, für den ein Bericht erstellt werden soll. Gültige Werte sind **Alle** (Desktop- und tragbare Computer), **Desktop** (nur Desktopcomputer) und **Laptop** (nur tragbare Computer). Diese Werte werden nur für den ausgewählten Berichtszeitraum zurückgegeben.|  

#### <a name="hidden-report-parameters"></a>Ausgeblendete Berichtsparameter  
 Die folgenden ausgeblendeten Parameter können optional festgelegt werden, um das Verhalten dieses Berichts zu ändern.  

|Parametername|Beschreibung|  
|--------------------|-----------------|  
|**Desktopcomputer an**|Geben Sie den Stromverbrauch eines eingeschalteten Desktopcomputers an. Der Standardwert beträgt **0,07** kWh.|  
|**Laptop an**|Geben Sie den Stromverbrauch eines eingeschalteten tragbaren Computers an. Der Standardwert beträgt **0,02** kWh.|  
|**Desktopcomputer Standbymodus**|Geben Sie den Stromverbrauch eines im Standbymodus befindlichen Desktopcomputers an. Der Standardwert beträgt **0,003** kWh.|  
|**Laptop Standbymodus**|Geben Sie den Stromverbrauch eines im Standbymodus befindlichen tragbaren Computers an. Der Standardwert beträgt **0,001** kWh.|  
|**Desktopcomputer aus**|Geben Sie den Stromverbrauch eines ausgeschalteten Desktopcomputers an. Der Standardwert beträgt **0** kWh.|  
|**Laptop aus**|Geben Sie den Stromverbrauch eines ausgeschalteten tragbaren Computers an. Der Standardwert beträgt **0** kWh.|  
|**Desktopmonitor an**|Geben Sie den Stromverbrauch des eingeschalteten Monitors eines Desktopcomputers an. Der Standardwert beträgt **0,028** kWh.|  
|**Laptopmonitor an**|Geben Sie den Stromverbrauch des eingeschalteten Monitors eines tragbaren Computers an. Der Standardwert beträgt **0** kWh.|  

#### <a name="report-links"></a>Berichtslinks  
 Dieser Bericht enthält keine Links zu anderen Energieverwaltungsberichten.  

###  <a name="energy-consumption-by-day-report"></a><a name="BKMK_Consumption_by_Day"></a> Bericht "Stromverbrauch nach Tag"  
 Im Bericht **Stromverbrauch nach Tag** werden die folgenden Informationen angezeigt:  

- In einem Diagramm wird für die angegebene Sammlung der gesamte tägliche Stromverbrauch der Computer in Kilowattstunden (kWh) in den letzten 31 Tagen angezeigt.  

- Ein Diagramm mit den täglichen Durchschnittswerten (in kWh) für den Stromverbrauch der Computer in der angegebenen Sammlung während der letzten 31 Tage  

- Eine Tabelle mit den täglichen Gesamtwerten und den täglichen Durchschnittswerten (in kWh) für den Stromverbrauch der Computer in der angegebenen Sammlung während der letzten 31 Tage  

  Mithilfe dieser Informationen können Sie Trends beim Stromverbrauch in Ihrer Umgebung erkennen. Der Stromverbrauch von Computern sollte nach der Anwendung eines Energiesparplans auf Computer in der ausgewählten Sammlung sinken.  

> [!NOTE]  
>  Wenn Sie nach der Anwendung eines Energiesparplans Mitglieder zur Sammlung hinzufügen bzw. daraus entfernen, hat dies Einfluss auf die Ergebnisse, die vom Bericht **Stromverbrauch** angezeigt werden, und erschwert den Vergleich von Ergebnissen aus der Überwachungs- und Planungsphase mit der Erzwingungsphase.  

 Verwenden Sie die folgenden Parameter, um diesen Bericht zu konfigurieren.  

#### <a name="required-report-parameters"></a>Erforderliche Berichtsparameter  
 Die folgenden Parameter müssen angegeben werden, um diesen Bericht auszuführen.  

|Parametername|Beschreibung|  
|--------------------|-----------------|  
|**Sammlung**|Wählen Sie in der Dropdownliste eine Sammlung aus, auf die sich dieser Bericht bezieht.|  
|**Device Type**|Wählen Sie in der Dropdownliste den Computertyp aus, für den ein Bericht erstellt werden soll. Gültige Werte sind **Alle** (Desktop- und tragbare Computer), **Desktop** (nur Desktopcomputer) und **Laptop** (nur tragbare Computer). Diese Werte werden nur für den ausgewählten Berichtszeitraum zurückgegeben.|  

#### <a name="hidden-report-parameters"></a>Ausgeblendete Berichtsparameter  
 Die folgenden ausgeblendeten Parameter können optional festgelegt werden, um das Verhalten dieses Berichts zu ändern.  

|Parametername|Beschreibung|  
|--------------------|-----------------|  
|**Desktopcomputer an**|Geben Sie den Stromverbrauch eines eingeschalteten Desktopcomputers an. Der Standardwert beträgt **0,07** kWh.|  
|**Laptop an**|Geben Sie den Stromverbrauch eines eingeschalteten tragbaren Computers an. Der Standardwert beträgt **0,02** kWh.|  
|**Desktopcomputer Standbymodus**|Geben Sie den Stromverbrauch eines im Standbymodus befindlichen Desktopcomputers an. Der Standardwert beträgt **0,003** kWh.|  
|**Laptop Standbymodus**|Geben Sie den Stromverbrauch eines im Standbymodus befindlichen tragbaren Computers an. Der Standardwert beträgt **0,001** kWh.|  
|**Desktopcomputer aus**|Geben Sie den Stromverbrauch eines ausgeschalteten Desktopcomputers an. Der Standardwert beträgt **0** kWh.|  
|**Laptop aus**|Geben Sie den Stromverbrauch eines ausgeschalteten tragbaren Computers an. Der Standardwert beträgt **0** kWh.|  
|**Desktopmonitor an**|Geben Sie den Stromverbrauch des eingeschalteten Monitors eines Desktopcomputers an. Der Standardwert beträgt **0,028** kWh.|  
|**Laptopmonitor an**|Geben Sie den Stromverbrauch des eingeschalteten Monitors eines tragbaren Computers an. Der Standardwert beträgt **0** kWh.|  

#### <a name="report-links"></a>Berichtslinks  
 Dieser Bericht enthält keine Links zu anderen Energieverwaltungsberichten.  

###  <a name="energy-cost-report"></a><a name="BKMK_Cost"></a> Bericht "Stromkosten"  
 Im Bericht **Stromkosten** werden die folgenden Informationen angezeigt:  

- Ein Diagramm mit den monatlichen Gesamtwerten für die Stromkosten der Computer in der angegebenen Sammlung über einen bestimmten Zeitraum  

- Ein Diagramm mit den monatlichen Durchschnittswerten für die Stromkosten der Computer in der angegebenen Sammlung über einen bestimmten Zeitraum  

- Eine Tabelle mit den monatlichen Gesamtwerten und den monatlichen Durchschnittswerten für die Stromkosten der Computer in der angegebenen Sammlung über einen bestimmten Zeitraum  

  Anhand dieser Informationen können Sie Stromkostentrends in Ihrer Umgebung erkennen. Die Stromkosten für Computer sollten nach der Anwendung eines Stromsparplans auf Computer in der ausgewählten Sammlung sinken.  

  Verwenden Sie die folgenden Parameter, um diesen Bericht zu konfigurieren.  

#### <a name="required-report-parameters"></a>Erforderliche Berichtsparameter  
 Die folgenden Parameter müssen angegeben werden, um diesen Bericht auszuführen.  

|Parametername|Beschreibung|  
|--------------------|-----------------|  
|**Startdatum**|Wählen Sie in der Dropdownliste ein Startdatum für diesen Bericht aus.|  
|**Enddatum**|Wählen Sie in der Dropdownliste ein Enddatum für diesen Bericht aus.|  
|**Kosten einer kWh**|Geben Sie den Kilowattstundenpreis an. Der Standardwert ist **0,09**.<br /><br /> Sie können die in diesem Bericht verwendete Währungseinheit im Bereich der ausgeblendeten Parameter ändern.|  
|**Sammlungsnamen**|Wählen Sie in der Dropdownliste eine Sammlung aus, auf die sich der Bericht bezieht.|  
|**Gerätetyp**|Wählen Sie in der Dropdownliste den Computertyp aus, für den ein Bericht erstellt werden soll. Gültige Werte sind **Alle** (Desktop- und tragbare Computer), **Desktop** (nur Desktopcomputer) und **Laptop** (nur tragbare Computer). Diese Werte werden nur für den ausgewählten Berichtszeitraum zurückgegeben.|  

#### <a name="hidden-report-parameters"></a>Ausgeblendete Berichtsparameter  
 Die folgenden ausgeblendeten Parameter können optional festgelegt werden, um das Verhalten dieses Berichts zu ändern.  

|Parametername|Beschreibung|  
|--------------------|-----------------|  
|**Desktopcomputer an**|Geben Sie den Stromverbrauch eines eingeschalteten Desktopcomputers an. Der Standardwert beträgt **0,07** kWh.|  
|**Laptop an**|Geben Sie den Stromverbrauch eines eingeschalteten tragbaren Computers an. Der Standardwert beträgt **0,02** kWh.|  
|**Desktopcomputer Standbymodus**|Geben Sie den Stromverbrauch eines im Standbymodus befindlichen Desktopcomputers an. Der Standardwert beträgt **0,003** kWh.|  
|**Laptop Standbymodus**|Geben Sie den Stromverbrauch eines im Standbymodus befindlichen tragbaren Computers an. Der Standardwert beträgt **0,001** kWh.|  
|**Desktopcomputer aus**|Geben Sie den Stromverbrauch eines ausgeschalteten Desktopcomputers an. Der Standardwert beträgt **0** kWh.|  
|**Laptop aus**|Geben Sie den Stromverbrauch eines ausgeschalteten tragbaren Computers an. Der Standardwert beträgt **0** kWh.|  
|**Desktopmonitor an**|Geben Sie den Stromverbrauch des eingeschalteten Monitors eines Desktopcomputers an. Der Standardwert beträgt **0,028** kWh.|  
|**Laptopmonitor an**|Geben Sie den Stromverbrauch des eingeschalteten Monitors eines tragbaren Computers an. Der Standardwert beträgt **0** kWh.|  
|**Währung**|Geben Sie die für diesen Bericht zu verwendende Währungsbezeichnung an. Der Standardwert ist **USD ($)** .|  

#### <a name="report-links"></a>Berichtslinks  
 Dieser Bericht enthält keine Links zu anderen Energieverwaltungsberichten.  

###  <a name="energy-cost-by-day-report"></a><a name="BKMK_Cost_by_Day"></a> Bericht "Stromkosten nach Tag"  
 Im Bericht **Stromkosten nach Tag** werden die folgenden Informationen angezeigt:  

- Ein Diagramm mit den täglichen Gesamtwerten für die Stromkosten der Computer in der angegebenen Sammlung während der letzten 31 Tage  

- Ein Diagramm mit den täglichen Durchschnittswerten für die Stromkosten der Computer in der angegebenen Sammlung während der letzten 31 Tage  

- Eine Tabelle mit den täglichen Gesamtwerten und den täglichen Durchschnittswerten für die Stromkosten der Computer in der angegebenen Sammlung während der letzten 31 Tage  

  Anhand dieser Informationen können Sie Stromkostentrends in Ihrer Umgebung erkennen. Die Stromkosten für Computer sollten nach der Anwendung eines Stromsparplans auf Computer in der ausgewählten Sammlung sinken.  

  Verwenden Sie die folgenden Parameter, um diesen Bericht zu konfigurieren.  

#### <a name="required-report-parameters"></a>Erforderliche Berichtsparameter  
 Die folgenden Parameter müssen angegeben werden, um diesen Bericht auszuführen.  

|Parametername|Beschreibung|  
|--------------------|-----------------|  
|**Sammlungsnamen**|Wählen Sie in der Dropdownliste eine Sammlung aus, auf die sich der Bericht bezieht.|  
|**Gerätetyp**|Wählen Sie in der Dropdownliste den Computertyp aus, für den ein Bericht erstellt werden soll. Gültige Werte sind **Alle** (Desktop- und tragbare Computer), **Desktop** (nur Desktopcomputer) und **Laptop** (nur tragbare Computer). Diese Werte werden nur für den ausgewählten Berichtszeitraum zurückgegeben.|  
|**Kosten einer kWh**|Geben Sie den Kilowattstundenpreis an. Der Standardwert ist **0,09**.<br /><br /> Sie können die in diesem Bericht verwendete Währungseinheit im Bereich der ausgeblendeten Parameter ändern.|  

#### <a name="hidden-report-parameters"></a>Ausgeblendete Berichtsparameter  
 Die folgenden ausgeblendeten Parameter können optional festgelegt werden, um das Verhalten dieses Berichts zu ändern.  

|Parametername|Beschreibung|  
|--------------------|-----------------|  
|**Desktopcomputer an**|Geben Sie den Stromverbrauch eines eingeschalteten Desktopcomputers an. Der Standardwert beträgt **0,07** kWh.|  
|**Laptop an**|Geben Sie den Stromverbrauch eines eingeschalteten tragbaren Computers an. Der Standardwert beträgt **0,02** kWh.|  
|**Desktopcomputer Standbymodus**|Geben Sie den Stromverbrauch eines im Standbymodus befindlichen Desktopcomputers an. Der Standardwert beträgt **0,003** kWh.|  
|**Laptop Standbymodus**|Geben Sie den Stromverbrauch eines im Standbymodus befindlichen tragbaren Computers an. Der Standardwert beträgt **0,001** kWh.|  
|**Desktopcomputer aus**|Geben Sie den Stromverbrauch eines ausgeschalteten Desktopcomputers an. Der Standardwert beträgt **0** kWh.|  
|**Laptop aus**|Geben Sie den Stromverbrauch eines ausgeschalteten tragbaren Computers an. Der Standardwert beträgt **0** kWh.|  
|**Desktopmonitor an**|Geben Sie den Stromverbrauch des eingeschalteten Monitors eines Desktopcomputers an. Der Standardwert beträgt **0,028** kWh.|  
|**Laptopmonitor an**|Geben Sie den Stromverbrauch des eingeschalteten Monitors eines tragbaren Computers an. Der Standardwert beträgt **0** kWh.|  
|**Währung**|Geben Sie die für diesen Bericht zu verwendende Währungsbezeichnung an. Der Standardwert ist **USD ($)** .|  

#### <a name="report-links"></a>Berichtslinks  
 Dieser Bericht enthält keine Links zu anderen Energieverwaltungsberichten.  

###  <a name="environmental-impact-report"></a><a name="BKMK_Environmental_Impact"></a> Bericht "Umweltbelastung"  
 Im Bericht **Umweltbelastung** werden die folgenden Informationen angezeigt:  

- In einem Diagramm wird der gesamte monatliche CO2-Ausstoß (in Tonnen) der Computer in der angegebenen Sammlung im angegebenen Zeitraum angezeigt.  

- In einem Diagramm wird der durchschnittliche monatliche CO2-Ausstoß (in Tonnen) jedes Computers in der angegebenen Sammlung im angegebenen Zeitraum angezeigt.  

- In einer Tabelle wird der gesamte monatliche CO2-Ausstoß und der durchschnittliche monatliche CO2-Ausstoß der Computer in der angegebenen Sammlung im angegebenen Zeitraum angezeigt.  

  Im Bericht **Umweltbelastung** wird die erzeugte Menge CO2 (in Tonnen) anhand der Dauer berechnet, die ein Computer bzw. Monitor innerhalb eines 24-stündigen Zeitraums eingeschaltet war.  

  Verwenden Sie die folgenden Parameter, um diesen Bericht zu konfigurieren.  

#### <a name="required-report-parameters"></a>Erforderliche Berichtsparameter  
 Die folgenden Parameter müssen angegeben werden, um diesen Bericht auszuführen.  

|Parametername|Beschreibung|  
|--------------------|-----------------|  
|**Berichtsstartdatum**|Wählen Sie in der Dropdownliste ein Startdatum für diesen Bericht aus.|  
|**Berichtsenddatum**|Wählen Sie in der Dropdownliste ein Enddatum für diesen Bericht aus.|  
|**Sammlungsnamen**|Wählen Sie in der Dropdownliste eine Sammlung aus, auf die sich dieser Bericht bezieht.|  
|**Gerätetyp**|Wählen Sie in der Dropdownliste den Computertyp aus, für den ein Bericht erstellt werden soll. Gültige Werte sind **Alle** (Desktop- und tragbare Computer), **Desktop** (nur Desktopcomputer) und **Laptop** (nur tragbare Computer). Diese Werte werden nur für den ausgewählten Berichtszeitraum zurückgegeben.|  

#### <a name="hidden-report-parameters"></a>Ausgeblendete Berichtsparameter  
 Die folgenden ausgeblendeten Parameter können optional festgelegt werden, um das Verhalten dieses Berichts zu ändern.  

|Parametername|Beschreibung|  
|--------------------|-----------------|  
|**Desktopcomputer an**|Geben Sie den Stromverbrauch eines eingeschalteten Desktopcomputers an. Der Standardwert beträgt **0,07** kWh.|  
|**Laptop an**|Geben Sie den Stromverbrauch eines eingeschalteten tragbaren Computers an. Der Standardwert beträgt **0,02** kWh.|  
|**Desktopcomputer Standbymodus**|Geben Sie den Stromverbrauch eines im Standbymodus befindlichen Desktopcomputers an. Der Standardwert beträgt **0,003** kWh.|  
|**Laptop Standbymodus**|Geben Sie den Stromverbrauch eines im Standbymodus befindlichen tragbaren Computers an. Der Standardwert beträgt **0,001** kWh.|  
|**Desktopcomputer aus**|Geben Sie den Stromverbrauch eines ausgeschalteten Desktopcomputers an. Der Standardwert beträgt **0** kWh.|  
|**Laptop aus**|Geben Sie den Stromverbrauch eines ausgeschalteten tragbaren Computers an. Der Standardwert beträgt **0** kWh.|  
|**Desktopmonitor an**|Geben Sie den Stromverbrauch des eingeschalteten Monitors eines Desktopcomputers an. Der Standardwert beträgt **0,028** kWh.|  
|**Laptopmonitor an**|Geben Sie den Stromverbrauch des eingeschalteten Monitors eines tragbaren Computers an. Der Standardwert beträgt **0** kWh.|  
|**CO2-Faktor (Tonnen/kWh)** (CO2-Mix)|Geben Sie den Wert für den CO2-Faktor (in Tonnen/kWh) an, den Sie bei Ihrem Energieversorgungsunternehmen erfragen können. Der Standardwert beträgt **0,0015** Tonnen pro kWh.|  

#### <a name="report-links"></a>Berichtslinks  
 Dieser Bericht enthält keine Links zu anderen Energieverwaltungsberichten.  

###  <a name="environmental-impact-by-day-report"></a><a name="BKMK_Environmental_Impact_by_Day"></a> Bericht "Umweltbelastung nach Tag"  
 Im Bericht **Umweltbelastung nach Tag** werden die folgenden Informationen angezeigt:  

- Ein Diagramm mit dem täglichen CO2-Gesamtausstoß (in Tonnen) für die Computer in der angegebenen Sammlung während der letzten 31 Tage.  

- Ein Diagramm mit dem durchschnittlichen täglichen CO2-Ausstoß (in Tonnen) für jeden Computer in der angegebenen Sammlung während der letzten 31 Tage.  

- Eine Tabelle mit dem gesamten täglichen CO2-Ausstoß und dem durchschnittlichen täglichen CO2-Ausstoß der Computer in der angegebenen Sammlung während der letzten 31 Tage.  

  Im Bericht **Umweltbelastung nach Tag** wird die erzeugte Menge CO2 (in Tonnen) anhand der Dauer berechnet, die ein Computer bzw. Monitor innerhalb eines 24-stündigen Zeitraums eingeschaltet war.  

#### <a name="required-report-parameters"></a>Erforderliche Berichtsparameter  
 Die folgenden Parameter müssen angegeben werden, um diesen Bericht auszuführen.  

|Parametername|Beschreibung|  
|--------------------|-----------------|  
|**Sammlungsnamen**|Wählen Sie in der Dropdownliste eine Sammlung aus, auf die sich dieser Bericht bezieht.|  
|**Gerätetyp**|Wählen Sie in der Dropdownliste den Computertyp aus, für den ein Bericht erstellt werden soll. Gültige Werte sind **Alle** (Desktop- und tragbare Computer), **Desktop** (nur Desktopcomputer) und **Laptop** (nur tragbare Computer). Diese Werte werden nur für den ausgewählten Berichtszeitraum zurückgegeben.|  

#### <a name="hidden-report-parameters"></a>Ausgeblendete Berichtsparameter  
 Die folgenden ausgeblendeten Parameter können optional festgelegt werden, um das Verhalten dieses Berichts zu ändern.  

|Parametername|Beschreibung|  
|--------------------|-----------------|  
|**Desktopcomputer an**|Geben Sie den Stromverbrauch eines eingeschalteten Desktopcomputers an. Der Standardwert beträgt **0,07** kWh.|  
|**Laptop an**|Geben Sie den Stromverbrauch eines eingeschalteten tragbaren Computers an. Der Standardwert beträgt **0,02** kWh.|  
|**Desktopcomputer aus**|Geben Sie den Stromverbrauch eines ausgeschalteten Desktopcomputers an. Der Standardwert beträgt **0** kWh.|  
|**Laptop aus**|Geben Sie den Stromverbrauch eines ausgeschalteten tragbaren Computers an. Der Standardwert beträgt **0** kWh.|  
|**Desktopcomputer Standbymodus**|Geben Sie den Stromverbrauch eines im Standbymodus befindlichen Desktopcomputers an. Der Standardwert beträgt **0,003** kWh.|  
|**Laptop Standbymodus**|Geben Sie den Stromverbrauch eines im Standbymodus befindlichen tragbaren Computers an. Der Standardwert beträgt **0,001** kWh.|  
|**Desktopmonitor an**|Geben Sie den Stromverbrauch des eingeschalteten Monitors eines Desktopcomputers an. Der Standardwert beträgt **0,028** kWh.|  
|**Laptopmonitor an**|Geben Sie den Stromverbrauch des eingeschalteten Monitors eines tragbaren Computers an. Der Standardwert beträgt **0** kWh.|  
|**CO2-Faktor (Tonnen/kWh)** (CO2-Mix)|Geben Sie den Wert für den CO2-Faktor (in Tonnen/kWh) an, den Sie bei Ihrem Energieversorgungsunternehmen erfragen können. Der Standardwert beträgt **0,0015** Tonnen pro kWh.|  

#### <a name="report-links"></a>Berichtslinks  
 Dieser Bericht enthält keine Links zu anderen Energieverwaltungsberichten.  

###  <a name="insomnia-computer-details-report"></a><a name="BKMK_Insomnia_Computer_Details"></a> Bericht "Störungsdetails für Computer"  
 Im Bericht **Störungsdetails für Computer** wird eine Liste von Computern angezeigt, die sich aus einem bestimmten Grund innerhalb eines angegebenen Zeitraums nicht im Standby- oder Ruhezustand befunden haben. Dieser Bericht wird vom **Störungsbericht** aus aufgerufen und nicht direkt vom Administrator ausgeführt.  

 Im Bericht **Störungsbericht** werden Computer als **Nicht energiesparmodusfähig** angezeigt, wenn sie nicht energiesparmodusfähig sind und innerhalb des gesamten angegebenen Berichtsintervalls eingeschaltet waren. Im Bericht werden Computer als **Nicht ruhezustandsfähig** angezeigt, wenn sie nicht ruhezustandsfähig sind und innerhalb des gesamten angegebenen Berichtsintervalls eingeschaltet waren.  

> [!NOTE]  
>  Von der Energieverwaltung können nur Ursachen für Energiesparmodus- und Ruhezustandsunfähigkeit von Computern gesammelt werden, auf denen Windows 7 oder Windows Server 2008 R2 ausgeführt wird.  

 Verwenden Sie die folgenden Parameter, um diesen Bericht zu konfigurieren.  

#### <a name="required-report-parameters"></a>Erforderliche Berichtsparameter  
 Die folgenden Parameter müssen angegeben werden, um diesen Bericht auszuführen.  

|Parametername|Beschreibung|  
|--------------------|-----------------|  
|**Sammlungsnamen**|Wählen Sie in der Dropdownliste eine Sammlung aus, auf die sich der Bericht bezieht.|  
|**Berichtsintervall (Tage)**|Geben Sie die Anzahl der Tage ein, auf die sich der Bericht bezieht. Der Standardwert ist **7** Tage.|  
|**Ursache der Störung**|Wählen Sie in der Dropdownliste eine der Ursachen aus, die einen Wechsel in den Standbymodus oder Ruhezustand für Computer verhindern können.|  

#### <a name="hidden-report-parameters"></a>Ausgeblendete Berichtsparameter  
 Dieser Bericht hat keine ausgeblendeten Parameter, die Sie festlegen können.  

#### <a name="report-links"></a>Berichtslinks  
 Dieser Bericht enthält Links zum folgenden Bericht, in dem weitere Informationen zum ausgewählten Element bereitgestellt werden.  

|Berichtsname|Details|  
|-----------------|-------------|  
|**Computerdetails**|Klicken Sie auf den Link **Klicken Sie hier, um detaillierte Informationen anzuzeigen** , um die Energiefunktionen, Energieeinstellungen und angewendeten Energiesparpläne für den ausgewählten Computer anzuzeigen.<br /><br /> Weitere Informationen finden Sie unter [Computer Details Report](#BKMK_Computer_Details) in diesem Thema.|  

###  <a name="insomnia-report"></a><a name="BKMK_Insomnia"></a> Insomnia report  
 Im **Störungsbericht** wird eine Liste der häufigsten Ursachen angezeigt, deretwegen für Computer weder der Standbymodus noch der Ruhezustand aktiviert werden konnte, sowie die Anzahl von Computern, die für einen bestimmten Zeitraum von jeder Ursache betroffen waren. Es gibt viele Ursachen, deretwegen für Computer weder der Standbymodus noch der Ruhezustand aktiviert werden kann: z. B. ein Prozess, der auf einem Computer ausgeführt wird, eine offene Remotedesktopsitzung oder die fehlende Funktion für den Standbymodus oder Ruhezustand. Aus diesem Bericht können Sie den Bericht **Störungsdetails für Computer** öffnen, in dem eine Liste der betroffenen Computer sowie der jeweiligen Ursache angezeigt wird, deretwegen sich die Computer nicht im Standbymodus oder Ruhezustand befinden.  

 Im Bericht "Energiestörung" werden Computer als **Nicht energiesparmodusfähig** angezeigt, wenn sie nicht energiesparmodusfähig sind und innerhalb des gesamten angegebenen Berichtsintervalls eingeschaltet waren. Im Bericht werden Computer als **Nicht ruhezustandsfähig** angezeigt, wenn sie nicht ruhezustandsfähig sind und innerhalb des gesamten angegebenen Berichtsintervalls eingeschaltet waren.  

> [!NOTE]  
>  Von der Energieverwaltung können nur Ursachen für Energiesparmodus- und Ruhezustandsunfähigkeit von Computern gesammelt werden, auf denen Windows 7 oder Windows Server 2008 R2 ausgeführt wird.  

 Verwenden Sie die folgenden Parameter, um diesen Bericht zu konfigurieren.  

#### <a name="required-report-parameters"></a>Erforderliche Berichtsparameter  
 Die folgenden Parameter müssen angegeben werden, um diesen Bericht auszuführen.  

|Parametername|Beschreibung|  
|--------------------|-----------------|  
|**Sammlungsnamen**|Wählen Sie in der Dropdownliste eine Sammlung aus, auf die sich der Bericht bezieht.|  
|**Berichtsintervall (Tage)**|Geben Sie die Anzahl der Tage ein, auf die sich der Bericht bezieht. Der Standardwert ist **7** Tage. Der Höchstwert ist **365** Tage. Geben Sie **0** an, um den Bericht für den laufenden Tag durchzuführen.|  

#### <a name="hidden-report-parameters"></a>Ausgeblendete Berichtsparameter  
 Dieser Bericht hat keine ausgeblendeten Parameter, die Sie festlegen können.  

#### <a name="report-links"></a>Berichtslinks  
 Dieser Bericht enthält Links zum folgenden Bericht, in dem weitere Informationen zum ausgewählten Element bereitgestellt werden.  

|Berichtsname|Details|  
|-----------------|-------------|  
|**Störungsdetails für Computer**|Klicken Sie in der Spalte **Betroffene Computer** auf eine Nummer, um eine Liste der Computer anzuzeigen, für die der Standbymodus oder Ruhezustand aufgrund der ausgewählten Ursache nicht aktiviert werden kann.<br /><br /> Weitere Informationen finden Sie unter [Insomnia Computer Details Report](#BKMK_Insomnia_Computer_Details) in diesem Thema.|  

###  <a name="power-capabilities-report"></a><a name="BKMK_Capabilites"></a> Bericht "Energiefunktionen"  
 Im Bericht **Energiefunktionen** werden die Hardwareenergieverwaltungsfunktionen von Computern in der angegebenen Sammlung angezeigt. Dieser Bericht wird typischerweise in der Überwachungsphase der Energieverwaltung verwendet, um die Energieverwaltungsfunktionen von Computern in Ihrer Organisation zu bestimmen. Die im Bericht angezeigten Informationen können dann zur Erstellung von Computersammlungen verwendet werden, auf die Energiesparpläne angewendet werden sollen oder die aus der Energieverwaltung ausgeschlossen werden sollen. Die in diesem Bericht angezeigten Energieverwaltungsfunktionen umfassen:  

- **Standbyfähig** : gibt an, ob der Computer in der Lage ist, bei entsprechender Konfiguration in den Standbymodus zu schalten.  

- **Ruhezustandsfähig** : gibt an, ob der Computer bei entsprechender Konfiguration in den Ruhezustand schalten kann.  

- **Aktivierung nach Standbymodus** : gibt an, ob der Computer bei entsprechender Konfiguration aus dem Standbymodus aktiviert werden kann.  

- **Aktivierung nach Ruhezustand** : gibt an, ob der Computer bei entsprechender Konfiguration aus dem Ruhezustand aktiviert werden kann.  

  Mit den im Bericht **Energiefunktionen** angezeigten Werten werden die von Windows gemeldeten Funktionen für den Standbymodus und den Ruhezustand angegeben. Dabei werden jedoch keine Fälle berücksichtigt, in denen diese Funktionen durch Windows- oder BIOS-Einstellungen blockiert werden.  

  Verwenden Sie die folgenden Parameter, um diesen Bericht zu konfigurieren.  

#### <a name="required-report-parameters"></a>Erforderliche Berichtsparameter  
 Die folgenden Parameter müssen angegeben werden, um diesen Bericht auszuführen.  

|Parametername|Beschreibung|  
|--------------------|-----------------|  
|**Sammlung**|Wählen Sie in der Dropdownliste eine Sammlung aus, auf die sich dieser Bericht bezieht.|  
|**Filter anzeigen**|Wählen Sie in der Dropdownliste **Nicht unterstützt** aus, um nur Computer in der angegebenen Sammlung anzuzeigen, die die Funktionen für Standbymodus, Ruhezustand, Aktivierung nach Standbymodus oder Aktivierung nach Ruhezustand nicht unterstützen. Wählen Sie **Alle anzeigen** aus, um alle Computer in der angegebenen Sammlung anzuzeigen.|  

#### <a name="hidden-report-parameters"></a>Ausgeblendete Berichtsparameter  
 Dieser Bericht hat keine ausgeblendeten Parameter, die Sie festlegen können.  

#### <a name="report-links"></a>Berichtslinks  
 Dieser Bericht enthält Links zum folgenden Bericht, in dem weitere Informationen zum ausgewählten Element bereitgestellt werden.  

|Berichtsname|Details|  
|-----------------|-------------|  
|**Computerdetails**|Klicken Sie auf einen Computernamen, um die Energiefunktionen, Energieeinstellungen und angewendeten Energiesparpläne des ausgewählten Computers anzuzeigen.<br /><br /> Weitere Informationen finden Sie unter [Computer Details Report](#BKMK_Computer_Details) in diesem Thema.|  

###  <a name="power-settings-report"></a><a name="BKMK_Settings"></a> Bericht "Energieeinstellungen"  
 Im Bericht **Energieeinstellungen** wird eine aggregierte Liste der aktuellen Energieeinstellungen angezeigt, die von Computern in der angegebenen Sammlung verwendet werden. Für jede Energieeinstellung werden die möglichen Energiestatus, Werte und Einheiten angezeigt, ebenso wie die Anzahl der Computer, von denen diese Werte verwendet werden. Mithilfe dieses Berichts kann der Administrator während der Überwachungsphase der Energieverwaltung die Energieeinstellungen der Computer am Standort ermitteln und optimale Energieeinstellungen planen, die anschließend mittels eines Energieverwaltungsplans angewendet werden. Auch bei der Fehlerbehebung ist dieser Bericht nützlich, wenn überprüft werden muss, ob die Energieeinstellungen ordnungsgemäß angewendet wurden.  

> [!NOTE]  
>  Die angezeigten Einstellungen werden von Clientcomputern während der Hardwareinventur gesammelt. Je nach Uhrzeit, zu der die Hardwareinventur ausgeführt wird, können Einstellungen von aktiven Haupt- und Nebenzeit-Energiesparplänen gesammelt werden.  

 Verwenden Sie die folgenden Parameter, um diesen Bericht zu konfigurieren.  

#### <a name="required-report-parameters"></a>Erforderliche Berichtsparameter  
 Die folgenden Parameter müssen angegeben werden, um diesen Bericht auszuführen.  

|Parametername|Beschreibung|  
|--------------------|-----------------|  
|**Sammlungsnamen**|Wählen Sie in der Dropdownliste eine Sammlung aus, auf die sich dieser Bericht bezieht.|  

#### <a name="hidden-report-parameters"></a>Ausgeblendete Berichtsparameter  
 Die folgenden ausgeblendeten Parameter können optional festgelegt werden, um das Verhalten dieses Berichts zu ändern.  

|Parametername|Beschreibung|  
|--------------------|-----------------|  
|**numberOfLocalizations**|Geben Sie die Anzahl der Sprachen an, in denen die von Clientcomputern gemeldeten Energieeinstellungsnamen angezeigt werden sollen. Wenn Sie möchten, dass nur die am häufigsten verwendete Sprache angezeigt wird, übernehmen Sie die Standardeinstellung **1**. Legen Sie für diesen Parameter den Wert **0**fest, um alle Sprachen anzuzeigen.|  

#### <a name="report-links"></a>Berichtslinks  
 Dieser Bericht enthält Links zum folgenden Bericht, in dem weitere Informationen zum ausgewählten Element bereitgestellt werden.  

|Berichtsname|Details|  
|-----------------|-------------|  
|**Energieeinstellungsdetails**|Klicken Sie in der Spalte **Computer** auf die Anzahl der Computer, um eine Liste aller Computer anzuzeigen, auf denen die in dieser Zeile angezeigten Energieeinstellungen verwendet werden.<br /><br /> Weitere Informationen finden Sie unter [Power Settings Details Report](#BKMK_Settings_Details) in diesem Thema.|  

###  <a name="power-settings-details-report"></a><a name="BKMK_Settings_Details"></a> Power Settings Details report  
 Im Bericht **Energieeinstellungsdetails** werden weitere Informationen zu Computern angezeigt, die im Bericht **Energieeinstellungen** ausgewählt wurden. Dieser Bericht wird vom Bericht **Energieeinstellungen** aufgerufen und nicht direkt vom Standortadministrator ausgeführt.  

#### <a name="required-report-parameters"></a>Erforderliche Berichtsparameter  
 Die folgenden Parameter müssen angegeben werden, um diesen Bericht auszuführen.  

|Parametername|Beschreibung|  
|--------------------|-----------------|  
|**Sammlung**|Wählen Sie in der Dropdownliste eine Sammlung aus, auf die sich der Bericht bezieht.|  
|**GUID der Energieeinstellung**|Wählen Sie aus der Dropdownliste die GUID der Energieeinstellung aus, für die Sie einen Bericht erstellen möchten. Eine Liste aller Energieeinstellungen und deren Verwendung finden Sie unter [Verfügbare Einstellungen des Energieverwaltungsplans](../../../../core/clients/manage/power/create-and-apply-power-plans.md#BKMK_Plans) im Thema [Erstellen und Anwenden von Energiesparplänen](../../../../core/clients/manage/power/create-and-apply-power-plans.md).|  
|**Power Mode**|Wählen Sie in der Dropdownliste den Typ der Energieeinstellungen aus, der in den Berichtergebnissen angezeigt werden soll. Wählen Sie **Netzbetrieb** aus, um die Energieeinstellungen anzuzeigen, die für den Fall konfiguriert wurden, dass der Computer im Netzbetrieb ausgeführt wird. Wählen Sie **Akkubetrieb** aus, um die Energieeinstellungen anzuzeigen, die für den Fall konfiguriert wurden, dass der Computer im Akkubetrieb ausgeführt wird.|  
|**Einstellungsindex**|Wählen Sie in der Dropdownliste den Wert für den Namen der ausgewählten Energieeinstellung aus, für die ein Bericht erstellt werden soll. Beispiel: Wählen Sie zum Anzeigen aller Computer, bei denen für die Einstellung **Festplatte ausschalten nach** der Wert **10** Minuten festgelegt wurde, für **Name der Energieeinstellung** die Option **Festplatte ausschalten nach** und für **Einstellungsindex** die Option **10**aus.|  

#### <a name="hidden-report-parameters"></a>Ausgeblendete Berichtsparameter  
 Die folgenden ausgeblendeten Parameter können optional festgelegt werden, um das Verhalten dieses Berichts zu ändern.  

|Parametername|Beschreibung|  
|--------------------|-----------------|  
|**numberOfLocalizations**|Geben Sie die Anzahl der Sprachen an, in denen die von Clientcomputern gemeldeten Energieeinstellungsnamen angezeigt werden sollen. Wenn Sie möchten, dass nur die am häufigsten verwendete Sprache angezeigt wird, übernehmen Sie die Standardeinstellung **1**. Legen Sie für diesen Parameter den Wert **0**fest, um alle Sprachen anzuzeigen.|  

#### <a name="report-links"></a>Berichtslinks  
 Dieser Bericht enthält Links zum folgenden Bericht, in dem weitere Informationen zum ausgewählten Element bereitgestellt werden.  

|Berichtsname|Details|  
|-----------------|-------------|  
|**Computerdetails**|Klicken Sie auf einen Computernamen, um die Energiefunktionen, Energieeinstellungen und angewendeten Energiesparpläne des ausgewählten Computers anzuzeigen.<br /><br /> Weitere Informationen finden Sie unter [Computer Details Report](#BKMK_Computer_Details) in diesem Thema.|  
