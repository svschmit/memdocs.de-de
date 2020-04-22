---
title: Prozeduren für Begrenzungsgruppen
titleSuffix: Configuration Manager
description: Konfigurieren Sie Begrenzungsgruppen für die logische Organisation zusammenhängender Netzwerkadressen, die auch als Grenzen bezeichnet werden.
ms.date: 11/27/2018
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a1fe22d0-4695-4de0-8bf0-e3475b03cf0e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: e8a47522cf59cc211f29c572010f9d3250659e1e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697388"
---
# <a name="how-to-configure-boundary-groups-for-configuration-manager"></a>Konfigurieren von Begrenzungsgruppen für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In diesem Artikel finden Sie Methoden zum Konfigurieren von Begrenzungsgruppen. Bevor Sie beginnen, überprüfen Sie, ob Sie mit den Konzepten von Begrenzungsgruppen vertraut sind. Weitere Informationen finden Sie unter [Begrenzungsgruppen](boundary-groups.md).



## <a name="create-a-boundary-group"></a><a name="bkmk_create"></a> Erstellen einer Begrenzungsgruppe  

1.  Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie die Option **Hierarchiekonfiguration**, und klicken Sie auf den Knoten **Begrenzungsgruppen**.  

2.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **Begrenzungsgruppe erstellen** aus.  

3.  Wählen Sie im Dialogfeld **Begrenzungsgruppe erstellen** die Registerkarte **Allgemein** aus, und geben Sie unter **Name** einen Namen für diese Begrenzungsgruppe an. Geben Sie optional eine **Beschreibung** an.  

4.  Klicken Sie auf **OK**, um die neue Begrenzungsgruppe zu speichern, oder fahren Sie mit dem nächsten Abschnitt fort, um die Begrenzungsgruppe zu konfigurieren.  


## <a name="configure-a-boundary-group"></a><a name="bkmk_config"></a> Konfigurieren einer Begrenzungsgruppe  

1.  Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie die Option **Hierarchiekonfiguration**, und klicken Sie auf den Knoten **Begrenzungsgruppen**.  

2.  Wählen Sie die Begrenzungsgruppe aus, die Sie ändern möchten, und klicken Sie auf dem Menüband auf **Eigenschaften**. Über diese Aktion wird das Eigenschaftenfenster der Begrenzungsgruppe geöffnet.  

Konfigurieren Sie die folgenden Einstellungen:  
- [Hinzufügen oder Entfernen von Begrenzungen](#bkmk_add)  
- [Konfigurieren der Standortzuweisung und Auswählen von Standortsystemservern](#bkmk_references)  
- [Konfigurieren des Fallbackverhaltens](#bkmk_bg-fallback)  
- [Konfigurieren von Begrenzungsgruppenoptionen](#bkmk_options)  


### <a name="add-or-remove-boundaries"></a><a name="bkmk_add"></a> Hinzufügen oder Entfernen von Begrenzungen

Wählen Sie im Eigenschaftenfenster der Begrenzungsgruppe die Registerkarte **Allgemein** aus, um die Grenzen zu ändern, die Mitglieder dieser Begrenzungsgruppe sind:  

- Wenn Sie Grenzen hinzufügen möchten, klicken Sie auf **Hinzufügen**. Aktivieren Sie im Fenster „Grenzen hinzufügen“ das Kontrollkästchen für eine oder mehrere Grenzen, und klicken Sie dann auf **OK**.  

- Wenn Sie Grenzen entfernen möchten, wählen Sie die Grenze aus, und klicken Sie dann auf **Entfernen**.  


### <a name="configure-site-assignment-and-select-site-system-servers"></a><a name="bkmk_references"></a> Konfigurieren der Standortzuweisung und Auswählen von Standortsystemservern

Um die Standortzuweisung und die zugehörige Konfiguration des Standortsystemservers zu ändern, wechseln Sie im Eigenschaftenfenster der Begrenzungsgruppe zur Registerkarte **Referenzen**.  

- Wählen Sie zum Aktivieren dieser Begrenzungsgruppe für die Verwendung durch Clients für die Standortzuweisung die Option **Use this boundary group for site assignment** (Diese Begrenzungsgruppe für die Standortzuweisung verwenden) aus. Wählen Sie anschließend aus der Dropdownliste **Zugewiesener Standort** einen Standort aus. Weitere Informationen finden Sie unter [Standortzuweisung](boundary-groups.md#site-assignment).  

- Wenn Sie dieser Begrenzungsgruppe verfügbare Standortsystemserver zuordnen möchten, klicken Sie auf **Hinzufügen**. Das Fenster „Standortsysteme hinzufügen“ listet nur die Server auf, die unterstützte Standortsystemrollen aufweisen. Aktivieren Sie das Kontrollkästchen für einen oder mehrere Server, und klicken Sie auf **OK**. Die Server werden als dieser Begrenzungsgruppe zugeordnete Standortsystemserver hinzugefügt.  

    > [!NOTE]  
    >  Sie können eine beliebige Kombination verfügbarer Standortsysteme von einem beliebigen Standort in der Hierarchie auswählen. Ausgewählte Standortsysteme werden in den Eigenschaften jeder Grenze, die dieser Begrenzungsgruppe angehört, auf der Registerkarte **Standortsysteme** aufgelistet.  

- Wenn Sie einen Server aus dieser Begrenzungsgruppe entfernen möchten, wählen Sie den Server aus, und klicken Sie dann auf **Entfernen**.  

    > [!NOTE]  
    >  Wenn diese Begrenzungsgruppe nicht mehr zum Zuordnen von Standortsystemen verwendet werden soll, müssen Sie alle Server entfernen, die als zugeordnete Standortsystemserver aufgelistet sind.  


### <a name="configure-fallback-behavior"></a><a name="bkmk_bg-fallback"></a> Konfigurieren des Fallbackverhaltens

Um das Fallbackverhalten zu konfigurieren, wechseln Sie im Eigenschaftenfenster der Begrenzungsgruppe zur Registerkarte **Beziehungen**.  

- So erstellen eine Beziehung mit einer anderen Begrenzungsgruppe  

  - Klicken Sie auf **Hinzufügen**. Wählen Sie im Fenster „Begrenzungsgruppen für Fallback“ die zu konfigurierende Begrenzungsgruppe aus.  

  - Legen Sie für die folgenden Standortsystemrollen eine Fallbackzeit fest:  
    - Verteilungspunkt  
    - Softwareupdatepunkt  
    - Verwaltungspunkt  

      > [!Note]  
      > Angenommen, Sie öffnen das Eigenschaftenfenster der Begrenzungsgruppe „Zweigstelle“. Im Fenster „Begrenzungsgruppen für Fallback“ wählen Sie die Begrenzungsgruppe „Zentrale“ aus. Sie legen die Fallbackzeit für Verteilungspunkte auf `20` fest. Wenn Sie diese Konfiguration speichern, beginnen die Clients in der Begrenzungsgruppe „Zweigstelle“ nach 20 Minuten mit der Suche nach Inhalten auf den Verteilungspunkten in der Begrenzungsgruppe „Zentrale“.  

  - Um ein Fallback zu einer bestimmten Begrenzungsgruppe zu verhindern, wählen Sie zuerst die Begrenzungsgruppe und dann **Nie ein Fallback durchführen** für den Typ der Standortsystemrolle aus. Diese Aktion kann die *standardmäßige Standortbegrenzungsgruppe* einschließen.  

- Um die Konfiguration einer vorhandenen Beziehung zu ändern, wählen Sie die Begrenzungsgruppe in der Liste und dann **Ändern** aus. Diese Aktion öffnet das Fenster „Begrenzungsgruppen für Fallback“ nur für diese Begrenzungsgruppe.  
 
- Wenn Sie eine Beziehung entfernen möchten, wählen Sie die Begrenzungsgruppe in der Liste und dann **Entfernen** aus.  

Weitere Informationen finden Sie unter [Fallback](boundary-groups.md#fallback). 


### <a name="configure-boundary-group-options"></a><a name="bkmk_options"></a> Konfigurieren von Begrenzungsgruppenoptionen
<!--1356193-->
Ab Version 1806 wechseln Sie zur Konfiguration zusätzlicher Optionen für Clients in dieser Begrenzungsgruppe zur Registerkarte **Optionen**. Weitere Informationen finden Sie unter [Begrenzungsgruppenoptionen für Peerdownloads](boundary-groups.md#bkmk_bgoptions).

- **Peerdownloads in dieser Begrenzungsgruppe zulassen:** Diese Option ist standardmäßig aktiviert. Der Verwaltungspunkt bietet Clients eine Liste der Speicherorte für Inhalt, die Peerquellen enthält.  

    - **Bei Peerdownloads nur Peers in demselben Subnetz verwenden:** Diese Einstellung ist abhängig von der davor. Wenn Sie diese Option aktivieren, enthält der Verwaltungspunkt nur in der Inhaltsspeicherort-Liste Peerquellen, die sich im gleichen Subnetz wie der Client befinden.  


## <a name="configure-a-fallback-site-for-automatic-site-assignment"></a><a name="bkmk_site-fallback"></a> Konfigurieren eines Fallbackstandorts für die automatische Standortzuweisung  

Wenn sich Clients nicht in einer Begrenzungsgruppe mit einem zugewiesenen Standort befinden, weisen Sie sie diesem Standort zu, sobald sie installiert sind.

1.  Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Standorte** aus.  

2.  Klicken Sie auf dem Menüband auf der Registerkarte **Start** in der Gruppe **Standorte** auf **Hierarchieeinstellungen**.  

3.  Aktivieren Sie auf der Registerkarte **Allgemein** das Kontrollkästchen **Fallbackstandort verwenden**. Wählen Sie anschließend in der Dropdownliste **Fallbackstandort** einen Standort aus.  

4.  Klicken Sie auf **OK**, um die Konfiguration zu speichern.  

Weitere Informationen finden Sie unter [Standortzuweisung](boundary-groups.md#site-assignment).


## <a name="enable-use-of-preferred-management-points"></a><a name="bkmk_proc-prefer"></a> Aktivieren der Verwendung bevorzugter Verwaltungspunkte  

Weitere Informationen finden Sie unter [Bevorzugte Verwaltungspunkte](boundary-groups.md#bkmk_preferred).

1.  Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Standortkonfiguration**, und wählen Sie den Knoten **Standorte** aus.  

2. Klicken Sie auf dem Menüband auf der Registerkarte **Start** in der Gruppe **Standorte** auf **Hierarchieeinstellungen**.  

3. Wählen Sie auf der Registerkarte **Allgemein** die Option **Clients bevorzugen das Verwenden von in Begrenzungsgruppen angegebenen Verwaltungspunkten** aus.  

4. Klicken Sie auf **OK**, um die Konfiguration zu speichern.  

