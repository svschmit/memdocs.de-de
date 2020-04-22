---
title: Definieren von Grenzen
titleSuffix: Configuration Manager
description: Hier erfahren Sie, wie Sie Netzwerkadressen in Ihrem Internet festlegen können. Diese können Geräte umfassen, die Sie verwalten möchten
ms.date: 03/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4a9dc4d9-e114-42ec-ae2b-73bee14ab04f
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: f53088843e0bf42a93c1d959255c7885b07dfe35
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81704848"
---
# <a name="define-network-locations-as-boundaries-for-configuration-manager"></a>Definieren von Netzwerkpfaden als Begrenzungsgruppen für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Grenzen von Configuration Manager sind Netzwerkpfade in Ihrem Netzwerk, die Geräte enthalten können, die Sie verwalten möchten. Die Grenze, auf der sich ein Gerät befindet, entspricht dem Standort von Active Directory oder der IP-Adresse des Netzwerks, die vom Konfigurations-Manager-Client erkannt wird, der auf dem Gerät installiert ist.
- Sie können einzelne Grenzen manuell erstellen. In Configuration Manager wird allerdings die direkte Eingabe eines Supernetzes als Grenze nicht unterstützt. Verwenden Sie stattdessen den Grenztyp IP-Adressbereich.
- Sie können die Methode [Active Directory-Gesamtstrukturermittlung](../../../../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutForest) für die automatische Erkennung und Erstellung von Grenzen für jeden erkannten IP-Subnetz- und Active Directory-Standort konfigurieren. Wenn von der Active Directory-Gesamtstrukturermittlung ein Supernetz identifiziert wird, das einem Active Directory-Standort zugewiesen ist, konvertiert Configuration Manager das Supernetz in eine Grenze vom Typ IP-Adressbereich.  

Es ist nicht ungewöhnlich, dass ein Client eine IP-Adresse verwendet, die dem Configuration Manager-Administrator unbekannt ist. Wenn der Netzwerkpfad des Geräts zweifelhaft ist, prüfen Sie, was das Gerät als seinen Pfad angibt, indem Sie den Befehl **IPCONFIG** auf dem Gerät aufrufen.  

Wenn Sie eine Grenze erstellen, erhält sie automatisch einen Namen, der auf dem Typ und Bereich der Grenze basiert. Dieser Name kann nicht geändert werden. Stattdessen können Sie beim Konfigurieren der Grenze eine Beschreibung angeben, anhand derer Sie die Grenze in der Configuration Manager-Konsole identifizieren können.  

Jede Grenze kann von jedem Standort in Ihrer Hierarchie verwendet werden. Sie können die Eigenschaften einer vorhandenen Grenze zu folgenden Zwecken ändern:  
- Hinzufügen der Grenze zu einer oder mehreren Begrenzungsgruppen  
- Ändern des Typs oder des Bereichs der Grenze  
- Anzeigen der Registerkarte **Standortsysteme** für die Grenze, um festzustellen, welche Standortsystemserver (Verteilungspunkte, Zustandsmigrationspunkte und Verwaltungspunkte) der Grenze zugeordnet sind.  

## <a name="to-create-a-boundary"></a>So erstellen Sie eine Grenze  

1.  Klicken Sie in der Configuration Manager-Konsole auf**Verwaltung** > **Hierarchiekonfiguration** > **Grenzen**.  

2.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Erstellen Boundary.**  

3.  Auf der Registerkarte **Allgemein** des Dialogfelds **Grenze erstellen** können Sie eine Beschreibung angeben, um die Grenze anhand eines Anzeigenamens oder einer Referenz zu identifizieren.  

4.  Wählen Sie einen **Typ** für diese Grenze aus:  

    - Bei Auswahl von **IP-Subnetz**müssen Sie eine **Subnetz-ID** für diese Grenze angeben.  
      > [!TIP]  
      > Sie können **Netzwerk** und **Subnetzmaske** angeben, um die **Subnetz-ID** automatisch zuordnen zu lassen. Wenn Sie die Grenze speichern, wird nur der Wert für die Subnetz-ID gespeichert.  

    - Bei Auswahl von **Active Directory-Standort**müssen Sie in der lokalen Gesamtstruktur des Standortservers einen Active Directory-Standort angeben oder durch Klicken auf **Durchsuchen** auswählen.  
        
      - Wenn Sie einen Active Directory-Standort für eine Grenze angeben, umfasst die Grenze alle IP-Subnetze, die Mitglieder dieses Active Directory-Standorts sind. Wenn die Konfiguration des Active Directory-Standorts in Active Directory geändert wird, werden auch die in dieser Grenze enthaltenen Netzwerkorte geändert.  

      - Active Directory-Standortgrenzen funktionieren nicht bei reinen Azure AD-Clients. Wenn sie lokal wandern, liegen sie nicht innerhalb einer Begrenzung, wenn sie nur mithilfe von AD-Standorten definiert werden.

    - Bei Auswahl von **IPv6-Präfix**müssen Sie ein **Präfix** im IPv6-Präfixformat angeben.  

    - Bei Auswahl von **IP-Adressbereich**müssen Sie eine **IP-Startadresse** und eine **IP-Endadresse** angeben, die einen Teil eines IP-Subnetzes oder mehrere IP-Subnetze abdeckt.    

5.  Klicken Sie auf **OK** , um die neue Grenze zu speichern.  

## <a name="to-configure-a-boundary"></a>So konfigurieren Sie eine Grenze  

1.  Klicken Sie in der Configuration Manager-Konsole auf**Verwaltung** > **Hierarchiekonfiguration** > **Grenzen**.  

2.  Wählen Sie die Grenze aus, die Sie ändern möchten.  

3.  Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** auf **Eigenschaften**.  

4.  Wählen Sie im Dialogfeld **Eigenschaften** für die Grenze die Registerkarte **Allgemein** aus, um die **Beschreibung** oder den **Typ** der Grenze zu bearbeiten. Sie können darüber hinaus den Bereich einer Grenze ändern, indem Sie die Netzwerkorte für die Grenze bearbeiten. Sie können beispielsweise für eine Active Directory-Standortgrenze einen neuen Active Directory-Standortnamen angeben.  

5.  Wählen Sie die Registerkarte **Standortsysteme** aus, um die Standortsysteme anzuzeigen, die dieser Grenze zugeordnet sind. Diese Konfiguration kann nicht über die Eigenschaften einer Grenze geändert werden.  

    > [!TIP]  
    > Ein Standortsystemserver wird nur dann als Standortsystem für eine Grenze aufgelistet, wenn der Standortsystemserver als solcher mindestens einer Begrenzungsgruppe zugeordnet ist, in der diese Grenze enthalten ist. Dies wird auf der Registerkarte **Referenzen** einer Begrenzungsgruppe konfiguriert.  

6.  Wählen Sie die Registerkarte **Begrenzungsgruppen** aus, um die Begrenzungsgruppenmitgliedschaft für diese Grenze zu ändern:  

    - Wenn Sie Begrenzungsgruppen diese Grenze hinzufügen möchten, klicken Sie auf **Hinzufügen**, aktivieren Sie das Kontrollkästchen für die betreffende(n) Begrenzungsgruppe(n), und klicken Sie dann auf **OK**.  

    - Wenn Sie diese Grenze aus einer Begrenzungsgruppe entfernen möchten, wählen Sie die Begrenzungsgruppe aus, und klicken Sie auf **Entfernen**.  

7.  Klicken Sie auf **OK** , um die Eigenschaften der Grenze zu schließen und die Konfiguration zu speichern.  
