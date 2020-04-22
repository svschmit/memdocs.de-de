---
title: Erstellen und Anwenden von Energiesparplänen
titleSuffix: Configuration Manager
description: Hier erhalten Sie Informationen zum Erstellen und Anwenden von Energiesparplänen in Configuration Manager.
ms.date: 04/17/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 738eddaa-52e2-467f-b453-821ef2884d47
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: aca0f3078c046bbc988a289f548ac11e26747088
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81696588"
---
# <a name="how-to-create-and-apply-power-plans-in-configuration-manager"></a>Erstellen und Anwenden von Energiesparplänen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Mithilfe der Energieverwaltung in Configuration Manager können Sie Energiesparpläne, die in Configuration Manager enthalten sind, auf Sammlungen von Computern in der Hierarchie anwenden oder eigene Energiesparpläne erstellen. Gehen Sie zum Anwenden eines integrierten oder benutzerdefinierten Energiesparplans auf Computern wie in diesem Thema beschrieben vor.  

> [!IMPORTANT]  
>  Es können nur Configuration Manager-Energiesparpläne auf Gerätesammlungen angewendet werden.  

 Wenn ein Computer mehreren Sammlungen angehört, für die unterschiedliche Energiesparpläne verwendet werden, werden folgende Aktionen durchgeführt:  

- Energiesparplan: Wenn auf einen Computer mehrere Werte für Energieeinstellungen angewendet werden, wird der am wenigsten restriktive Wert verwendet.  

- Aktivierungszeit: Wenn auf einen Desktopcomputer mehrere Aktivierungszeiten angewendet werden, wird die der Mitternacht nächste Uhrzeit verwendet.  

  Verwenden Sie zum Anzeigen aller Computer, auf die mehrere Energiesparpläne angewendet werden, den Bericht **Computer mit mehreren Energiesparplänen** . Dadurch können Sie Computer mit Energiesparplankonflikten ermitteln. Weitere Informationen zu Berichten zur Energieverwaltung finden Sie unter [Überwachen und Planen der Energieverwaltung](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

> [!IMPORTANT]  
>  Durch Energieeinstellungen, die mithilfe einer Windows-Gruppenrichtlinie konfiguriert wurden, werden die von der Configuration Manager-Energieverwaltung konfigurierten Einstellungen überschrieben.  

 Gehen Sie zum Erstellen und Anwenden eines Configuration Manager-Energiesparplans wie nachfolgend beschrieben vor.  

### <a name="to-create-and-apply-a-power-plan"></a>So erstellen Sie einen Energiesparplan und wenden ihn an  

1. Klicken Sie in der Configuration Manager-Konsole auf **Bestand und Kompatibilität**.  

2. Klicken Sie im Arbeitsbereich **Bestand und Kompatibilität** auf **Gerätesammlungen**.  

3. Klicken Sie in der Liste **Gerätesammlungen** auf die Sammlung, auf die Sie Energieverwaltungseinstellungen anwenden möchten. Klicken Sie dann auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

4. Wählen Sie auf der Registerkarte **Energieverwaltung** im Dialogfeld <em><Sammlungsname\></em>**Eigenschaften** die Option **Energieverwaltungseinstellungen für diese Sammlung angeben**.  

   > [!NOTE]  
   >  Sie können auch auf **Durchsuchen** klicken und die Energieverwaltungseinstellungen von einer ausgewählten Sammlung zur ausgewählten Sammlung kopieren.  

5. Geben Sie in den Feldern **Start** und **Ende** die Start- und Endzeit für Hauptzeitstunden (oder Geschäftszeiten) an.  

6. Aktivieren Sie **Aktivierungszeit (Desktopcomputer)** zum Angeben eines Zeitpunkts, zu dem ein Desktopcomputer aus dem Standby- oder Ruhezustand erneut aktiviert wird, damit geplante Updates oder Softwareinstallationen installiert werden können.  

   > [!IMPORTANT]  
   >  Für die Energieverwaltung wird die Aktivierungszeitfunktion von Windows verwendet, mit der Computer aus dem Standby- oder Ruhezustand erneut aktiviert werden. Aktivierungszeiteinstellungen werden nicht auf tragbare Computer angewendet, damit diese nicht aktiviert werden, wenn sie nicht an die Stromversorgung angeschlossen sind. Die Aktivierungszeit ist zufällig. Computer werden nach Beginn der angegebenen Aktivierungszeit für einen Zeitraum von einer Stunde erneut aktiviert.  

7. Wenn Sie einen benutzerdefinierten Energiesparplan für Hauptzeitstunden (oder Geschäftszeiten) konfigurieren möchten, wählen Sie aus der Dropdownliste **Hauptzeitplan** die Option **Benutzerdefiniert, Hauptzeit (ConfigMgr)** aus, und klicken Sie auf **Bearbeiten**. Wenn Sie einen Energiesparplan für Nebenzeitstunden (oder außerhalb der Geschäftszeiten) konfigurieren möchten, wählen Sie aus der Dropdownliste **Nebenzeitplan** die Option **Benutzerdefiniert, Nebenzeit (ConfigMgr)** aus, und klicken Sie auf **Bearbeiten**.  

   > [!NOTE]  
   >  Mithilfe des Berichts **Computeraktivität** können Sie einfacher bestimmen, welche Zeitpläne für Haupt- und Nebenzeitstunden verwendet werden sollen, wenn Sie Energiesparpläne auf Sammlungen von Computern anwenden. Weitere Informationen finden Sie unter [How to monitor and plan for power management (Überwachen und Planen der Energieverwaltung in Configuration Manager)](../../../../core/clients/manage/power/monitor-and-plan-for-power-management.md).  

    Sie können auch einen der integrierten Energiesparpläne auswählen ( **Ausgeglichen (ConfigMgr)** , **Höchstleistung ConfigMgr)** und **Energiesparmodus (ConfigMgr)** ) und dann zum Anzeigen der Eigenschaften jedes Energiesparplans auf **Anzeigen** klicken.  

   > [!NOTE]  
   >  Die integrierten Energiesparpläne können nicht geändert werden.  

8. Konfigurieren Sie im Dialogfeld <em><Energiesparplanname\></em>**Eigenschaften** die folgenden Einstellungen:  

   -   **Name:** Geben Sie einen Namen für diesen Energiesparplan an, oder verwenden Sie den angegebenen Standardwert.  

   -   **Beschreibung:**  Geben Sie eine Beschreibung für diesen Energiesparplan an, oder verwenden Sie den angegebenen Standardwert.  

   -   **Eigenschaften für diesen Energiesparplan angeben:** Konfigurieren Sie die Eigenschaften des Energiesparplans. Deaktivieren Sie zum Deaktivieren einer Eigenschaft das entsprechende Kontrollkästchen. Weitere Informationen über die verfügbaren Einstellungen finden Sie in diesem Thema unter [Available power management plan settings](#BKMK_Plans) .  

       > [!IMPORTANT]  
       >  Aktivierte Einstellungen werden auf die Computer angewendet, sobald der Energiesparplan angewendet wird. Wenn Sie ein Kontrollkästchen der Energieeinstellung deaktivieren, wird der Wert auf dem Clientcomputer nicht geändert, wenn der Energiesparplan angewendet wird. Durch Deaktivieren eines Kontrollkästchens wird der Wert für die Energieeinstellung nicht auf den Wert wiederhergestellt, der vor dem Anwenden eines Energiesparplans angegeben war.  

9. Klicken Sie auf **OK**, um das Dialogfeld <em><Energiesparplanname\></em>**Eigenschaften** zu schließen.  

10. Klicken Sie auf **OK**, um das Dialogfeld <em><Sammlungsname\></em>**Einstellungen** zu schließen.  

##  <a name="available-power-management-plan-settings"></a><a name="BKMK_Plans"></a> Available power management plan settings  
 In der folgenden Tabelle sind die in Configuration Manager verfügbaren Energieverwaltungseinstellungen aufgelistet. Sie können separate Einstellungen für folgende Vorkommnisse konfigurieren: wenn ein Computer nicht an die Stromversorgung angeschlossen ist oder sich im Akkubetrieb befindet. Je nachdem welche Windows-Version Sie verwenden, können Sie einige Einstellungen möglicherweise nicht konfigurieren.  

> [!NOTE]  
>  Bei Energieeinstellungen, die nicht konfiguriert werden, wird der aktuelle Wert auf den Clientcomputern beibehalten.  

|Name|Beschreibung|  
|----------|-----------------|  
|**Bildschirm ausschalten nach (Minuten)**|Gibt die Zeitdauer in Minuten an, die der Computer inaktiv sein muss, bevor der Bildschirm ausgeschaltet wird. Geben Sie den Wert **0** an, wenn Sie nicht möchten, dass der Bildschirm von der Energieverwaltung ausgeschaltet wird.|  
|**Standbymodus nach (Minuten)**|Gibt die Zeitdauer in Minuten an, die der Computer inaktiv sein muss, bevor er in den Standbymodus versetzt wird. Geben Sie den Wert **0** an, wenn Sie nicht möchten, dass der Computer von der Energieverwaltung in den Standbymodus versetzt wird.|  
|**Kennwort bei Reaktivierung anfordern**|**Ja** oder **Nein** gibt an, ob ein Kennwort erforderlich ist, um den Computer bei der Reaktivierung zu entsperren.|  
|**Netzschalteraktion**|Gibt die Aktion an, die ausgeführt wird, wenn der Netzschalter des Computers gedrückt wird. Mögliche Werte **Nichts unternehmen**, **Standbymodus**, **Ruhezustand**, und **Herunterfahren**.|  
|**Ein-/Aus-Schalter im Startmenü**|Gibt die Aktion an, die durchgeführt wird, wenn Sie auf den Ein-/Aus-Schalter im **Startmenü** des Computers klicken. Mögliche Werte **Standbymodus**, **Ruhezustand**, und **Herunterfahren**.|  
|**Energiespartastenaktion**|Gibt die Aktion an, die durchgeführt wird, wenn Sie die **Energiespartaste** des Computers drücken. Mögliche Werte **Nichts unternehmen**, **Standbymodus**, **Ruhezustand**, und **Herunterfahren**.|  
|**Zuklappaktion**|Gibt die Aktion an, die durchgeführt wird, wenn der Benutzer den tragbaren Computers schließt. Mögliche Werte **Nichts unternehmen**, **Standbymodus**, **Ruhezustand**, und **Herunterfahren**.|  
|**Festplatte ausschalten nach (Minuten)**|Gibt die Zeitdauer in Minuten an, die die Festplatte des Computers inaktiv sein muss, bevor sie ausgeschaltet wird. Geben Sie den Wert **0** an, wenn Sie nicht möchten, dass die Festplatte des Computers von der Energieverwaltung ausgeschaltet wird.|  
|**Ruhezustand nach (Minuten)**|Gibt die Zeitdauer in Minuten an, die der Computer inaktiv sein muss, bevor er in den Ruhezustand versetzt wird. Geben Sie den Wert **0** an, wenn Sie nicht möchten, dass der Computer von der Energieverwaltung in den Ruhezustand versetzt wird.|  
|**Aktion bei niedriger Akkukapazität**|Gibt die Aktion an, die durchgeführt wird, wenn der Akku des Computers die festgelegte Benachrichtigungsebene für niedrige Akkukapazität erreicht. Mögliche Werte **Nichts unternehmen**, **Standbymodus**, **Ruhezustand**, und **Herunterfahren**.|  
|**Aktion bei kritischer Akkukapazität**|Gibt die Aktion an, die durchgeführt wird, wenn der Akku des Computers die festgelegte Benachrichtigungsebene für kritische Akkukapazität erreicht. Bei der Einstellung **On battery** (Akkubetrieb) lauten die möglichen Werte **Standbymodus**, **Ruhezustand** und **Herunterfahren**. Bei der Einstellung **Netzbetrieb** lauten die möglichen Werte **Nichts unternehmen**, **Standbymodus**, **Ruhezustand** und **Herunterfahren**.|  
|**Hybriden Standbymodus zulassen**|**Ein** oder **Aus** gibt an, ob von Windows beim Wechsel in den Standbymodus eine Ruhezustandsdatei gespeichert wird, die verwendet werden kann, um den Zustand des Computers im Falle eines Stromausfalls beim Wechsel in den Standbymodus wiederherzustellen.<br /><br /> Der hybride Standbymodus wurde für Desktopcomputer entwickelt und ist auf tragbaren Computern standardmäßig nicht aktiviert. Wenn auf Computern, die unter Windows 7 ausgeführt werden, der hybride Standbymodus aktiviert wird, wird die Ruhezustandsfunktion deaktiviert.|  
|**Wechsel in den Standbymodus auf Benutzeranforderung zulassen**|Mit **Ein** oder **Aus** kann der Computer in den Standbymodus versetzt werden. Dabei verbraucht er immer noch Energie, kann jedoch schneller reaktiviert werden. Wenn für diese Einstellung **Deaktiviert**festgelegt wird, kann der Computer nur in den Ruhezustand versetzt oder ausgeschaltet werden.|  
|**Erforderlicher Leerlauf für Standbymodus (%)**|Gibt den prozentualen Anteil der Leerlaufzeit an der Computerprozessorzeit an, die erforderlich ist, damit der Computer in den Standbymodus versetzt wird. Auf Computern, auf denen Windows 7 ausgeführt wird, ist dieser Wert immer auf **0**gesetzt.|  
|**Windows-Aktivierungszeitgeber für Desktopcomputer aktivieren**|Auswählen von **aktivieren** oder **deaktivieren** für den integrierten Windows-Zeitgeber, wodurch die Energieverwaltung zum Reaktivieren eines Desktopcomputers verwendet werden kann. Wird ein Desktopcomputer vom Windows-Aktivierungszeitgeber erneut aktiviert, verbleibt er standardmäßig 10 Minuten im Normalzustand, damit auf dem Computer Updates installiert oder Richtlinien empfangen werden können.<br /><br /> Aktivierungszeitgeber werden auf tragbaren Computern nicht unterstützt, um zu verhindern, dass die Computer aktiviert werden, solange sie sich nicht im Netzbetrieb befinden.|  
