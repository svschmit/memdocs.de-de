---
title: Für Softwareupdates verwendete Symbole
titleSuffix: Configuration Manager
description: Die Configuration Manager-Konsole enthält Symbole, die einen Status für das synchronisierte Update oder die Softwareupdategruppe angeben.
manager: dougeby
ms.date: 10/06/2016
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 63c5ef72-5715-4d86-85a2-71beba469fab
author: mestew
ms.author: mstewart
ms.openlocfilehash: 0ca0509893ecadc4c54d06ca98c18531959fb941
ms.sourcegitcommit: 8fc1704ed0e1141f46662bdd32b52bec00fb93b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2020
ms.locfileid: "89608407"
---
# <a name="icons-used-for-software-updates-in-configuration-manager"></a>Für Softwareupdates verwendete Symbole in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Synchronisierte Softwareupdates werden in der Configuration Manager-Konsole angezeigt, wobei die erste Spalte für jedes Softwareupdate ein Symbol enthält, das einen bestimmten Zustand kennzeichnet. Softwareupdategruppen werden ebenfalls mit einem Symbol dargestellt, das Informationen über den Zustand der Softwareupdates bereitstellt, die in der Gruppe enthalten sind. Dieser Abschnitt enthält Informationen zu allen Softwareupdatesymbolen sowie zur Bedeutung jedes Symbols.  

## <a name="icons-for-software-updates"></a>Symbole für Softwareupdates  
 Synchronisierte Softwareupdates werden durch eines der folgenden Symbole dargestellt.  

### <a name="normal-icon"></a>Symbol „Normal“  
 ![Symbol „Normal“](../media/Normal.jpg) Das Symbol mit dem grünen Pfeil steht für ein normales Softwareupdate.  

 **Beschreibung:**  

 Ein normales Softwareupdates wurde synchronisiert und ist zur Softwarebereitstellung verfügbar.  

 **Einsatzbedenken:**  

 Keine Einsatzbedenken.  

### <a name="expired-icon"></a>Symbol „Abgelaufen“  
 ![Symbol „Abgelaufen“](../media/Expired.jpg) Das Symbol mit dem schwarzen X kennzeichnet ein abgelaufenes Softwareupdate. Sie können abgelaufene Softwareupdates auch erkennen, indem Sie die Spalte **Abgelaufen** für das Softwareupdate anzeigen, wenn es in der Configuration Manager-Konsole eingeblendet wird.  

 **Beschreibung:**  

 Abgelaufene Softwareupdates konnten zuvor für Clientcomputer bereitgestellt werden. Nachdem ein Softwareupdate jedoch abgelaufen ist, können keine neuen Bereitstellungen für die Softwareupdates erstellt werden. Abgelaufene Softwareupdates werden aus aktiven Bereitstellungen entfernt und Clients nicht mehr zur Verfügung gestellt.  

 **Einsatzbedenken:**  

 Keine Einsatzbedenken.

### <a name="superseded-icon"></a>Symbol „Abgelöst“  
 ![Symbol „Abgelöst“](../media/Superseded.jpg) Das Symbol mit dem gelben Stern kennzeichnet ein abgelöstes Softwareupdate. Sie können ein abgelöstes Softwareupdate auch erkennen, indem Sie die Spalte **Abgelöst** für das Softwareupdate anzeigen, wenn es in der Configuration Manager-Konsole eingeblendet wird.  

 **Beschreibung:**  

 Abgelöste Softwareupdates wurden durch neuere Versionen des Softwareupdates ersetzt. Mit einem Softwareupdate, das ein anderes Softwareupdate ablöst, wird in der Regel Folgendes bewirkt:  

- Erweiterung, Verbesserung oder Ergänzung der Korrekturen, die von früher herausgegebenen Softwareupdates bereitgestellt wurden.  

- Steigerung der Effizienz seines Softwareupdatedateipakets, das von Clients installiert wird, sofern das Softwareupdate zur Installation genehmigt ist. Beispielsweise könnte das abgelöste Softwareupdate Dateien enthalten, die für die Korrektur oder die vom neuen Softwareupdate unterstützten Betriebssysteme nicht mehr relevant sind. Diese Dateien sind dann im Dateipaket des abgelösten Softwareupdates nicht enthalten.  

- Ausführung eines Updates für neuere Produktversionen, das heißt, das Update gilt nicht mehr für ältere Versionen oder Konfigurationen eines Produkts. Softwareupdates können außerdem durch andere Softwareupdates abgelöst werden, wenn zur Erweiterung der Sprachunterstützung entsprechende Änderungen vorgenommen wurden. Beispielsweise wäre es möglich, dass in einer späteren Version eines Produktupdates für Microsoft 365-Apps ein älteres Betriebssystem nicht mehr unterstützt, dafür aber in der Erstversion des Softwareupdates die Sprachunterstützung erweitert wird.  

  Auf der Registerkarte „Ablösungsregeln“ in den Eigenschaften der jeweiligen „Softwareupdatepunkt-Komponente“ können Sie angeben, wie abgelöste Softwareupdates verwaltet werden sollen. Weitere Informationen finden Sie unter [Supersedence rules](../plan-design/plan-for-software-updates.md#BKMK_SupersedenceRules).  

  **Einsatzbedenken:**  

  Nach Möglichkeit sollten Sie für Clientcomputer nicht das abgelöste Softwareupdate, sondern das ablösende Softwareupdate bereitstellen. Sie können eine Liste der Softwareupdates, die das Softwareupdate ablösen, auf der Registerkarte **Ablösungsinformationen** in den Eigenschaften des Softwareupdates anzeigen.  

### <a name="invalid-icon"></a>Symbol „Ungültig“  
 ![Symbol „Ungültig“](../media/Invalid.jpg) Das Symbol mit dem roten X kennzeichnet ein ungültiges Softwareupdate.  

 **Beschreibung:**  

 Ungültige Softwareupdates sind in einer aktiven Bereitstellung enthalten, aber der Inhalt (Softwareupdatedateien) ist aus irgendeinem Grund nicht verfügbar. Dieser Zustand kann auftreten, wenn einer der folgenden Fälle vorliegt:  

- Sie haben das Softwareupdate erfolgreich bereitgestellt, aber die Softwareupdatedatei wurde aus dem Bereitstellungspaket entfernt und ist nicht mehr verfügbar.  

- Sie erstellen eine Softwareupdatebereitstellung in einem Standort, und das Bereitstellungsobjekt wird erfolgreich an einen untergeordneten Standort repliziert, aber das Bereitstellungspaket wurde nicht erfolgreich an den untergeordneten Standort repliziert.  

  **Einsatzbedenken:**  

  Wenn der Inhalt für ein Softwareupdate fehlt, können Clients das Softwareupdate solange nicht installieren, bis der Inhalt auf einem Verteilungspunkt verfügbar geworden ist. Sie können den Inhalt erneut an Verteilungspunkte verteilen, indem Sie die **Neu verteilen** -Aktion verwenden. Wenn Inhalt für ein Softwareupdate in einer Bereitstellung fehlt, die in einem übergeordneten Standort erstellt wurde, muss das Softwareupdate erneut an den untergeordneten Standort repliziert oder verteilt werden. Weitere Informationen zur erneuten Verteilung von Inhalten finden Sie unter [Verwalten der Inhalte, die Sie verteilt haben](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage).  

### <a name="metadata-only-icon"></a>Symbol für reines Metadatensoftwareupdate
 ![Symbol für reines Metadatensoftwareupdate](../media/MetadataOnly.png) Das Symbol mit dem blauen Pfeil kennzeichnet ein nur Metadaten enthaltendes Softwareupdate.

 **Beschreibung:**  

 Nur Metadaten enthaltende Softwareupdates sind zur Berichterstellung in der Configuration Manager-Konsole verfügbar. Sie können nur Metadaten enthaltende Softwareupdates weder bereitstellen noch herunterladen, weil keine Softwareupdatedatei mit den Metadaten von Softwareupdates verknüpft ist.  

 **Einsatzbedenken:**  

 Nur Metadaten enthaltende Softwareupdates stehen für Berichterstattungszwecke zur Verfügung und sind nicht zur Softwareupdatebereitstellung vorgesehen.  

## <a name="icons-for-software-update-groups"></a>Symbole für Softwareupdategruppen  
 Softwareupdategruppen werden durch eines der folgenden Symbole dargestellt.  

### <a name="normal-icon"></a>Symbol „Normal“  
 ![Softwareupdategruppen – Symbol „Normal“](../media/Normal.jpg) Das Symbol mit dem grünen Pfeil steht für eine softwareupdategruppe, die nur normale Softwareupdates enthält.  

 **Einsatzbedenken:**  

 Keine Einsatzbedenken.  

### <a name="expired-icon"></a>Symbol „Abgelaufen“  
 ![Softwareupdategruppen – Symbol „Abgelaufen“](../media/Expired.jpg) Das Symbol mit dem schwarzen X steht für eine softwareupdategruppe, die eine oder mehrere Abgelaufene Softwareupdates enthält.  

 **Einsatzbedenken:**  

 Sie sollten abgelaufene Softwareupdates in der Softwareupdategruppe nach Möglichkeit entfernen oder ersetzen.  

### <a name="superseded-icon"></a>Symbol „Abgelöst“  
 ![Softwareupdategruppen – Symbol „Abgelöst“](../media/Superseded.jpg) Das Symbol mit dem gelben Stern steht für eine Gruppe zum Aktualisieren von Software, die eine oder mehrere abgelösten Softwareupdates enthält.  

 **Einsatzbedenken:**  

 Sie sollten ein abgelöstes Softwareupdates in der Softwareupdategruppe nach Möglichkeit durch das ablösende Softwareupdate ersetzen.  

### <a name="invalid-icon"></a>Symbol „Ungültig“  
 ![Softwareupdategruppen – Symbol „Ungültig“](../media/Invalid.jpg) Das Symbol mit dem roten X steht für eine softwareupdategruppe, die eine oder mehrere ungültige Softwareupdates enthält.  

 **Einsatzbedenken:**  

 Wenn der Inhalt für ein Softwareupdate fehlt, können Clients das Softwareupdate solange nicht installieren, bis der Inhalt auf einem Verteilungspunkt verfügbar geworden ist. Sie können den Inhalt erneut an Verteilungspunkte verteilen, indem Sie die **Neu verteilen** -Aktion verwenden. Wenn Inhalt für ein Softwareupdate in einer Bereitstellung fehlt, die in einem übergeordneten Standort erstellt wurde, muss das Softwareupdate erneut an den untergeordneten Standort repliziert oder verteilt werden. Weitere Informationen zur erneuten Verteilung von Inhalten finden Sie unter [Verwalten der Inhalte, die Sie verteilt haben](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_manage).  


## <a name="next-steps"></a>Nächste Schritte 

[Planen von Softwareupdates](../plan-design/plan-for-software-updates.md)