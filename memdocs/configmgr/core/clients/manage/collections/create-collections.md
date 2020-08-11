---
title: Erstellen von Sammlungen
titleSuffix: Configuration Manager
description: Erstellen Sie Sammlungen in Configuration Manager, um Benutzergruppen und Geräte leichter zu verwalten.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 1401a35e-4312-4d3b-8ceb-0abbb10d4f05
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 5e81bc9b2135d17c445f8a86ff2214db394f63db
ms.sourcegitcommit: 2ee50bfc416182362ae0b8070b096e1cc792bf68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87865488"
---
# <a name="how-to-create-collections-in-configuration-manager"></a>Erstellen von Sammlungen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Bei Sammlungen handelt es sich um Gruppierungen von Benutzern und Geräten. Nutzen Sie Sammlungen für Aufgaben wie die Verwaltung von Anwendungen, Bereitstellung von Konformitätseinstellungen und Installation von Softwareupdates. Außerdem können Sammlungen zur Verwaltung von Clienteinstellungsgruppen verwendet werden. Möglich ist auch eine Verwendung von Sammlungen mit rollenbasierter Verwaltung zum Angeben der Ressourcen, auf die ein Administrator zugreifen kann. In Configuration Manager sind einige Sammlungen bereits integriert. Weitere Informationen finden Sie unter [Einführung in Sammlungen](introduction-to-collections.md).  

> [!NOTE]  
> Eine Sammlung kann nur Benutzer oder Geräte enthalten, aber nicht beide.  


Dieser Artikel kann Ihnen beim Erstellen von Sammlungen in Configuration Manager helfen. Sie können auch Sammlungen importieren, die am aktuellen oder einem anderen Configuration Manager-Standort erstellt wurden. Informationen zum Exportieren und Importieren von Sammlungen finden Sie unter [Verwalten von Sammlungen](manage-collections.md).  


## <a name="collection-rules"></a>Sammlungsregeln

Es gibt verschiedene Regeltypen, mit deren Hilfe Sie die Mitglieder einer Sammlung in Configuration Manager konfigurieren können.  


### <a name="direct-rule"></a>Direktregel

Verwenden Sie Direktregeln zum Wählen der Benutzer oder Computer, die Sie einer Sammlung hinzufügen möchten. Die Mitgliedschaft ändert sich nicht, es sei denn, Sie entfernen eine Ressource aus Configuration Manager. Die Ressourcen müssen von Configuration Manager ermittelt oder von Ihnen importiert worden sein, bevor Sie sie einer Direktregelsammlung hinzufügen können. Direktregelsammlungen haben einen höheren Verwaltungsaufwand als Abfrageregelsammlungen, weil dieser Sammlungstyp manuell geändert werden muss.


### <a name="query-rule"></a>Abfrageregel

Aktualisieren Sie die Mitgliedschaft dynamisch auf Basis einer Abfrage, die von Configuration Manager nach einem Zeitplan ausgeführt wird. Sie können beispielsweise eine Sammlung von Benutzern erstellen, die Mitglieder der Organisationseinheit "Personal" in den Active Directory-Domänendiensten sind. Diese Sammlung wird automatisch aktualisiert, wenn neue Benutzer der Organisationseinheit „Personalwesen“ hinzugefügt bzw. daraus entfernt werden.

Beispielabfragen, die Sie zum Erstellen von Sammlungen verwenden können, finden Sie unter [Erstellen von Abfragen](../../../servers/manage/create-queries.md).


### <a name="device-category-rule"></a>Gerätekategorieregel

Sie können die Verwaltung Ihrer Geräte vereinfachen, indem Sie den Gerätesammlungen Gerätekategorien zuordnen. 

Weitere Informationen finden Sie unter [Automatisches Kategorisieren von Geräten in Sammlungen](automatically-categorize-devices-into-collections.md).<!-- SCCMDocs issue 552 -->


### <a name="include-collection-rule"></a>Regel "Sammlungen einschließen"

Mit dieser Regel können Sie die Mitglieder einer anderen Sammlung in eine Configuration Manager-Sammlung einbeziehen. Die Mitgliedschaft der aktuellen Sammlung wird von Configuration Manager nach einem Zeitplan aktualisiert, wenn sich die einbezogene Sammlung ändert.

Sie können einer Sammlung mehrere Regeln "Sammlungen einschließen" hinzufügen.


### <a name="exclude-collection-rule"></a>Regel "Sammlungen ausschließen"

Mit Regeln des Typs „Sammlungen ausschließen“ können Sie die Mitglieder einer anderen Sammlung aus einer anderen Configuration Manager-Sammlung ausschließen. Die Mitgliedschaft der aktuellen Sammlung wird von Configuration Manager nach einem Zeitplan aktualisiert, wenn sich die ausgeschlossene Sammlung ändert.

Sie können einer Sammlung mehrere Regeln "Sammlungen ausschließen" hinzufügen. Wenn eine Sammlung sowohl die Regel „Sammlungen einschließen“ als auch die Regel „Sammlungen ausschließen“ enthält und die Regeln in Konflikt stehen, hat die Regel „Sammlungen ausschließen“ Priorität.

#### <a name="example"></a>Beispiel
Sie erstellen eine Sammlung, die eine Regel "Sammlungen einschließen" und eine Regel "Sammlungen ausschließen" enthält. Die Regel "Sammlungen einschließen" bezieht sich auf eine Sammlung von Dell-Desktops. Die Regel „Sammlungen ausschließen“ bezieht sich auf eine Sammlung von Computern mit weniger als 4 GB RAM. Die neue Sammlung enthält Desktop-PCs von Dell, die über mindestens 4 GB RAM verfügen.



## <a name="create-a-collection"></a><a name="bkmk_create"></a> Erstellen einer Sammlung  

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**.  

    - Um eine *Gerätesammlung* zu erstellen, wählen Sie den Knoten **Gerätesammlungen** aus. Wählen Sie auf der Registerkarte **Start** im Menüband in der Gruppe **Erstellen** den Befehl **Gerätesammlung erstellen** aus.  

    - Um eine *Benutzersammlung* zu erstellen, wählen Sie den Knoten **Benutzersammlungen** aus. Wählen Sie auf der Registerkarte **Start** im Menüband in der Gruppe **Erstellen** den Befehl **Benutzersammlung erstellen** aus.  

2. Geben Sie auf der Seite **Allgemein** des Assistenten einen **Namen** und einen **Kommentar** ein. Wählen Sie im Bereich **Begrenzende Sammlung** zum Auswählen einer begrenzenden Sammlung **Durchsuchen** aus. In der Sammlung, die Sie erstellen, sind nur Mitglieder aus der begrenzenden Sammlung enthalten.  

4. Wählen Sie auf der Seite **Mitgliedschaftsregel** in der Liste **Regel hinzufügen** den Typ der Mitgliedschaftsregel aus, den Sie für die Sammlung verwenden möchten. Sie können für jede Sammlung mehrere Regeln konfigurieren. Die Konfiguration für jede Regel variiert. Weitere Informationen zur Konfiguration der einzelnen Regeln finden Sie in den folgenden Abschnitten dieses Artikels:  
    - [Direktregel](#bkmk-direct)
    - [Abfrageregel](#bkmk-query)
    - [Gerätekategorieregel](#bkmk-category)
    - [Regel „Sammlungen einschließen“](#bkmk-include)
    - [Regel „Sammlungen ausschließen“](#bkmk-exclude)

5. Überprüfen Sie zudem auf der Seite **Mitgliedschaftsregeln** die folgenden Einstellungen.

    - **Inkrementelle Updates für diese Sammlung verwenden**: Wählen Sie diese Option, um regelmäßig nach neuen oder geänderten Ressourcen aus der vorherigen Sammlungsauswertung zu suchen und nur diese zu aktualisieren. Dieser Prozess ist unabhängig von einer vollständigen Auswertung der Sammlung. Standardmäßig erfolgen inkrementelle Updates in Abständen von 5 Minuten.  

        > [!IMPORTANT]  
        >  Sammlungen mit Abfrageregeln, in denen folgende Klassen verwendet werden, unterstützen inkrementelle Updates nicht:  
        >   
        > -   SMS_G_System_CollectedFile  
        > -   SMS_G_System_LastSoftwareScan  
        > -   SMS_G_System_AppClientState  
        > -   SMS_G_System_DCMDeploymentState  
        > -   SMS_G_System_DCMDeploymentErrorAssetDetails  
        > -   SMS_G_System_DCMDeploymentCompliantAssetDetails  
        > -   SMS_G_System_DCMDeploymentNonCompliantAssetDetails  
        > -   SMS_G_User_DCMDeploymentCompliantAssetDetails (nur für Benutzersammlungen)  
        > -   SMS_G_User_DCMDeploymentNonCompliantAssetDetails (nur für Benutzersammlungen)  
        > -   SMS_G_System_SoftwareUsageData  
        > -   SMS_G_System_CI_ComplianceState  
        > -   SMS_G_System_EndpointProtectionStatus  
        > -   SMS_GH_System_*  
        > -   SMS_GEH_System_*  

    - **Vollständiges Update für diese Sammlung planen**: Wählen Sie diese Option aus, um eine reguläre, vollständige Auswertung der Sammlungsmitgliedschaft zu planen.  

        Ab Version 1810 können diese Änderungen am Verhalten von Sammlungsauswertungen die Leistung der Website verbessern:<!--3607726-->  

        - Wenn Sie bislang einen Zeitplan für eine abfragebasierte Sammlung konfiguriert haben, hat die Website die Abfrage weiterhin ausgewertet, unabhängig davon, ob die Sammlungseinstellung **Vollständiges Update für diese Sammlung planen** aktiviert ist. Um den Zeitplan vollständig zu deaktivieren, müssen Sie den Zeitplan auf **Kein** festlegen.

            Nun löscht die Website den Zeitplan, wenn Sie diese Einstellung deaktivieren. Um einen Zeitplan für die Auswertung anzugeben, aktivieren Sie die Option **Vollständiges Update für diese Sammlung planen**.  

            Wenn Sie Ihre Website aktualisieren, aktiviert die Website für jede vorhandene Sammlung, für die Sie einen Zeitplan angegeben haben, die Option **Vollständiges Update für diese Sammlung planen**. Obwohl diese Konfiguration vielleicht nicht von Ihnen beabsichtigt ist, war es das tatsächliche Verhalten des Zeitplans, bevor Sie den Standort aktualisiert haben. Deaktivieren Sie diese Option, wenn die Website Sammlungen nicht nach einem Zeitplan auswerten soll.  

        - Die Auswertung von integrierten Sammlungen wie **Alle Systeme** lässt sich nicht deaktivieren, doch nun können Sie den Zeitplan konfigurieren. Mit diesem Verhalten können Sie diese Aktion zu einem Zeitpunkt anpassen, der Ihren Anforderungen entspricht. 

            > [!TIP]  
            > Ändern Sie für integrierte Sammlungen nur die **Zeit** des benutzerdefinierten Zeitplans. Ändern Sie nicht das **Serienmuster**. Künftige Iterationen können ein bestimmtes Serienmuster erzwingen.  

6. Schließen Sie den Assistenten ab, um die neue Sammlung zu erstellen. Die neue Sammlung wird im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Gerätesammlungen** angezeigt.  

> [!NOTE]  
> Sie müssen die Configuration Manager-Konsole aktualisieren oder erneut laden, um die Sammlungsmitglieder anzuzeigen. Sie werden erst nach dem ersten geplanten Update in der Sammlung angezeigt. Sie können **Mitgliedschaft aktualisieren** auch manuell für die Sammlung auswählen. Es dauert möglicherweise einige Minuten, bis die Aktualisierung einer Sammlung abgeschlossen ist.  

        
### <a name="configure-a-direct-rule"></a><a name="bkmk-direct"></a> Konfigurieren einer Direktregel  

1. Geben Sie im **Assistenten für die Erstellung von Regeln der direkten Mitgliedschaft** auf der Seite **Ressourcen suchen** die folgenden Informationen an.  

    - **Ressourcenklasse:** Wählen Sie den Ressourcentyp aus, den Sie suchen und der Sammlung hinzufügen möchten. Beispiel:
        - **Systemressource**: Suche nach Bestandsdaten, die von Clientcomputern zurückgegeben werden
        - **Unbekannter Computer**: Auswahl aus Werten, die von unbekannten Computern zurückgegeben werden
        - **Benutzerressource**: Suche nach Benutzerinformationen, die von Configuration Manager gesammelt wurden
        - **Benutzergruppenressource**: Suche nach Gruppeninformationen, die von Configuration Manager gesammelt wurden

    - **Attributname:** Wählen Sie das Attribut aus, das der ausgewählten Ressourcenklasse zugeordnet ist, die Sie suchen möchten. Beispiel:  

        - Wenn Sie Computer nach NetBIOS-Namen auswählen möchten, wählen Sie in der Liste **Ressourcenklasse** die Option **Systemressource** und in der Liste **Attributname** die Option **NetBIOS-Name** aus.  

        - Wenn Sie Benutzer nach dem Namen der Organisationseinheit auswählen möchten, wählen Sie in der Liste **Ressourcenklasse** die Option **Benutzerressource** und in der Liste **Attributname** die Option **Benutzer-Organisationseinheitsname** aus.  

    - **Als veraltet markierte Ressourcen ausschließen**: Wenn ein Clientcomputer als veraltet markiert wird, schließen Sie diesen Wert nicht in die Suchergebnisse ein.  

    - **Ressourcen ausschließen, für die der Konfigurations-Manager-Client nicht installiert wurde** Diese Ressourcen werden in den Suchergebnissen nicht angezeigt.  

    - **Wert:** Geben Sie einen Wert ein, um den ausgewählten Attributnamen zu suchen. Sie können das Prozentzeichen (%) als Platzhalter verwenden. Beispiel:  
        - Um nach Computern zu suchen, deren NetBIOS-Name mit „M“ beginnt, geben Sie in dieses Feld **M%** ein.  
        - Wenn Sie nach Benutzern in der Organisationseinheit „Contoso“ suchen, geben Sie in dieses Feld **Contoso** ein.

2. Wählen Sie auf der Seite **Ressourcen auswählen** die Ressourcen aus, die Sie der Sammlung in der Liste **Ressourcen** hinzufügen möchten, und klicken Sie dann auf **Weiter**.  


### <a name="configure-a-query-rule"></a><a name="bkmk-query"></a> Konfigurieren einer Abfrageregel  

Geben Sie im Dialogfeld **Eigenschaften für Abfrageregel** die folgenden Informationen an.  

- **Name:** Geben Sie einen eindeutigen Namen für die Abfrage an.  

- **Abfrageanweisung importieren**: Damit wird das Dialogfeld **Abfrage durchsuchen** geöffnet. Wählen Sie eine [Configuration Manager-Abfrage](../../../servers/manage/create-queries.md) aus, die als Abfrageregel für die Sammlung verwendet werden soll.   

- **Ressourcenklasse:** Wählen Sie den Ressourcentyp aus, den Sie suchen und der Sammlung hinzufügen möchten. Wählen Sie aus **Systemressource** einen Wert zur Suche von Inventurdaten aus, die von Clientcomputern zurückgegeben wurden, oder wählen Sie **Unbekannter Computer** aus, um Werte auszuwählen, die von unbekannten Computern zurückgegeben wurden.  

- **Abfrageanweisung bearbeiten**: Öffnet das Dialogfeld **Eigenschaften der Abfrageanweisung**, in dem Sie eine Abfrage erstellen können, die als Regel für die Sammlung verwendet werden soll. Weitere Informationen zu Abfragen finden Sie unter [Einführung in Abfragen in System Center Configuration Manager](../../../servers/manage/introduction-to-queries.md).  

    > [!TIP]  
    > Auf der Registerkarte „Allgemein“ kann das Aktivieren des Kontrollkästchens **Doppelte Zeilen unterdrücken (eindeutige Auswahl)** zu weniger zurückgegebenen Zeilen und möglicherweise schnelleren Ergebnissen führen.

### <a name="device-category-rule"></a><a name="bkmk-category"></a> Gerätekategorieregel

Die folgenden Aktionen sind im Fenster **Gerätekategorien auswählen** verfügbar.

- **Erstellen:** Geben Sie einen Namen an, um eine neue Kategorie erstellen.
- **Umbenennen**: Benennen Sie die ausgewählte Kategorie um.
- **Löschen** Wählen Sie eine oder mehrere Kategorien aus, und entfernen Sie sie mit dieser Aktion aus der Liste.

Weitere Informationen finden Sie unter [Automatisches Kategorisieren von Geräten in Sammlungen](automatically-categorize-devices-into-collections.md).<!-- SCCMDocs issue 552 -->


### <a name="configure-an-include-collection-rule"></a><a name="bkmk-include"></a> Konfigurieren einer Regel „Sammlungen einschließen“  

Wählen Sie im Dialogfeld **Sammlungen auswählen** die Sammlungen aus, die Sie in die neue Sammlung einschließen möchten, und klicken Sie dann auf **OK**.  


### <a name="configure-an-exclude-collection-rule"></a><a name="bkmk-exclude"></a> Konfigurieren einer Regel „Sammlungen ausschließen“  

Wählen Sie im Dialogfeld **Sammlungen auswählen** die Sammlungen aus, die Sie aus der neuen Sammlung ausschließen möchten, und klicken Sie dann auf **OK**.  



## <a name="import-a-collection"></a><a name="bkmk_import"></a> Importieren einer Sammlung  

Wenn Sie eine Sammlung aus einem Standort exportieren, speichert der Configuration Manager sie als MOF-Datei (Managed Object Format). Verwenden Sie dieses Verfahren, um diese Datei in Ihre Standortdatenbank zu importieren. Zum Abschließen dieser Schritte benötigen Sie Berechtigungen des Typs **Erstellen** für die „collections“-Klasse.

> [!IMPORTANT]  
> - Stellen Sie sicher, dass die Datei nur Sammlungsdaten enthält, aus einer vertrauenswürdigen Quelle stammt und nicht manipuliert wurde.  
> 
> - Vergewissern Sie sich, dass die Datei aus einem Standort exportiert wurde, der die gleiche Configuration Manager-Version hat.  

Weitere Informationen zum Exportieren von Sammlungen finden Sie unter [Verwalten von Sammlungen](manage-collections.md).


1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**. Wählen Sie entweder den Knoten **Benutzersammlungen** oder **Gerätesammlungen** aus.  

2. Wählen Sie auf der Registerkarte **Start** im Menüband in der Gruppe **Erstellen** den Befehl **Sammlungen importieren** aus.  

3. Klicken Sie im **Assistenten zum Importieren von Sammlungen** auf der Seite **Allgemein** auf **Weiter**.  

4. Klicken Sie auf der Seite **MOF-Dateiname** auf **Durchsuchen**. Suchen Sie die MOF-Datei, die die zu importierenden Sammlungsinformationen enthält.  

5. Schließen Sie den Assistenten ab, um die Sammlung zu importieren. Die neue Sammlung wird im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Benutzersammlungen** oder **Gerätesammlungen** angezeigt. Aktualisieren Sie die Configuration Manager-Konsole, oder laden Sie sie erneut, um die Sammlungsmitglieder für die neu importierte Sammlung anzuzeigen.  

## <a name="synchronize-collection-membership-results-to-azure-active-directory-groups"></a><a name="bkmk_aadcollsync"></a> Synchronisieren der Sammlungsmitgliedschaftsergebnisse mit Azure Active Directory-Gruppen

<!--3607475-->
> [!Tip]  
> Dieses Feature wurde erstmals in Version 1906 als [Vorabfeature](../../../servers/manage/pre-release-features.md) eingeführt. Ab Version 2002 ist es kein Vorabfeature mehr.  

Sie können die Synchronisierung von Sammlungsmitgliedschaften mit einer Azure Active Directory-Gruppe (Azure AD) aktivieren. Durch diese Synchronisierung können Sie Ihre vorhandenen lokalen Gruppierungsregeln in der Cloud verwenden, indem Sie Azure AD-Gruppenmitgliedschaften auf Grundlage der Erfassungsergebnisse für Mitgliedschaften erstellen. Sie können Gerätesammlungen synchronisieren. Es werden nur Geräte mit einem Azure Active Directory-Eintrag in der Azure AD-Gruppe widergespiegelt. Sowohl Geräte mit Azure AD Hybrid-Einbindung als auch per Azure Active Director eingebundene Geräte werden unterstützt.

Die Azure AD-Synchronisierung erfolgt alle fünf Minuten. Dies ist ein unidirektionaler Vorgang von Configuration Manager zu Azure AD. In Azure AD vorgenommene Änderungen werden nicht in Configuration Manager-Sammlungen berücksichtigt, jedoch nicht von Configuration Manager überschrieben. Wenn beispielsweise die Configuration Manager-Sammlung aus zwei Geräten und die Azure AD-Gruppe aus drei anderen Geräten besteht, enthält die Azure AD-Gruppe nach der Synchronisierung fünf Geräte.

### <a name="prerequisites"></a>Voraussetzungen

- Integration in Azure AD für die [Cloudverwaltung](../../../servers/deploy/configure/azure-services-wizard.md)
- [Azure Active Directory-Benutzerermittlung](../../../servers/deploy/configure/about-discovery-methods.md#azureaddisc)
- Einen für HTTPS oder den [erweiterten HTTP](../../../plan-design/hierarchy/enhanced-http.md) aktivierten Verwaltungspunkt
- Zugriff auf die Sammlung **Alle Systeme**

### <a name="create-a-group-and-set-the-owner-in-azure-ad"></a>Erstellen einer Gruppe und Festlegen des Besitzers in Azure AD

1. Wechseln Sie zu [https://portal.azure.com](https://portal.azure.com).
1. Navigieren Sie **Azure Active Directory** > **Gruppen** > **Alle Gruppen**.
1. Klicken Sie auf **Neue Gruppe**, und geben Sie **Gruppenname** und optional **Gruppenbeschreibung** ein.
1. Der Wert für **Mitgliedschaftstyp** muss **Zugewiesen** lauten.
1. Wählen Sie **Besitzer** aus, und fügen Sie dann die Identität hinzu, von der die Synchronisierungsbeziehung in Configuration Manager erstellt wird.
1. Klicken Sie auf **Erstellen**, um die Azure AD-Gruppe fertigzustellen.

### <a name="enable-collection-synchronization-for-the-azure-service"></a>Aktivieren der Sammlungssynchronisierung für den Azure-Dienst

1. Wechseln Sie in der Configuration Manager-Konsole zu **Verwaltung** > **Übersicht** > **Clouddienste** > **Azure-Dienste**.
1. Klicken Sie mit der rechten Maustaste auf den Azure AD-Mandanten, in dem Sie die Gruppe erstellt haben, und wählen Sie **Eigenschaften** aus.
1. Aktivieren Sie auf der Registerkarte **Sammlungssynchronisierung** das Kontrollkästchen für **Azure Active Directory-Gruppensynchronisierung aktivieren**.
1. Klicken Sie auf **OK**, um die Einstellung zu speichern.

### <a name="enable-the-collection-to-synchronize"></a>Aktivieren der Synchronisierung der Sammlung

1. Gehen Sie in der Configuration Manager-Konsole zu **Bestand und Kompatibilität** > **Übersicht** > **Gerätesammlungen**.
1. Klicken Sie mit der rechten Maustaste auf die zu synchronisierende Sammlung, und klicken Sie dann auf **Eigenschaften**. 
1. Klicken Sie auf der Registerkarte **Cloudsynchronisierung** auf **Hinzufügen**.
1. Wählen Sie im Dropdownmenü den **Mandanten** aus, in dem Sie Ihre Azure AD-Gruppe erstellt haben.
1. Geben Sie im Feld **Name beginnt mit** Ihre Suchkriterien ein, und klicken Sie dann auf **Suchen**.
  - Wenn Sie aufgefordert werden, sich anzumelden, verwenden Sie die Identität, die Sie als Besitzer für die Azure AD-Gruppe angegeben haben.
1. Wählen Sie die Zielgruppe aus, und klicken Sie auf **OK**, um die Gruppe hinzuzufügen. Klicken Sie erneut auf **OK**, um die Eigenschaften der Gruppe zu schließen.
1. Sie müssen etwa 5 bis 7 Minuten warten, bis Sie die Gruppenmitgliedschaften im Azure-Portal überprüfen können.
   - Zum Initiieren einer vollständigen Synchronisierung klicken Sie mit der rechten Maustaste auf die Sammlung, und wählen Sie **Mitgliedschaft synchronisieren** aus.


### <a name="verify-the-azure-ad-group-membership"></a>Überprüfen der Azure AD-Gruppenmitgliedschaft

1. Wechseln Sie zu [https://portal.azure.com](https://portal.azure.com).
1. Navigieren Sie **Azure Active Directory** > **Gruppen** > **Alle Gruppen**.
1. Suchen Sie die von Ihnen erstellte Gruppe, und wählen Sie **Mitglieder** aus. 
1. Vergewissern Sie sich, dass die Mitglieder denen in der Konfigurations-Manager-Sammlung entsprechen.
   - Nur Geräte mit Azure AD-Identität werden in der Gruppe angezeigt.


![Synchronisieren von Sammlungen mit Azure AD](media/3607475-sync-collection-to-azuread.png)

## <a name="using-powershell"></a><a name="bkmk_powershell"></a> Verwenden von PowerShell

PowerShell kann zum Erstellen und Importieren von Sammlungen verwendet werden. Weitere Informationen finden Sie in folgenden Quellen:

* [New-CMCollection](https://docs.microsoft.com/powershell/module/configurationmanager/new-cmcollection)
* [Set-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Set-CMCollection)
* [Import-CMCollection](https://docs.microsoft.com/powershell/module/ConfigurationManager/Import-CMCollection)

## <a name="next-steps"></a>Nächste Schritte

[Verwalten von Sammlungen](manage-collections.md)
