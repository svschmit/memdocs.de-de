---
title: Konfigurieren der Ermittlung
titleSuffix: Configuration Manager
description: Konfigurieren von Ermittlungsmethoden zum Finden von Ressourcen, die Sie von Ihrem Netzwerk, Active Directory und Azure Active Directory verwalten
ms.date: 06/03/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 49505eb1-d44d-4121-8712-e0f3d8b15bf5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: cfda27df7df537ededb1f103afdd6107354af786
ms.sourcegitcommit: d498e5eceed299f009337228523d0d4be76a14c2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/04/2020
ms.locfileid: "84347286"
---
# <a name="configure-discovery-methods-for-configuration-manager"></a>Konfigurieren von Ermittlungsmethoden für Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Konfigurieren Sie Ermittlungsmethoden zum Finden von Ressourcen, die Sie von Ihrem Netzwerk, Active Directory und Azure Active Directory (Azure AD) verwalten. Aktivieren und konfigurieren Sie zunächst jede Methode, die Sie zum Suchen in Ihrer Umgebung verwenden möchten. Sie können außerdem jede Methode mit den gleichen Schritten deaktivieren, mit denen sie aktiviert wird. Die einzigen Ausnahmen hiervon sind Frequenzermittlung und Serverermittlung:  

- Die **Frequenzermittlung** ist standardmäßig aktiviert, wenn Sie einen primären Configuration Manager-Standort installieren. Sie wird so konfiguriert, dass sie nach einem Zeitplan ausgeführt wird. Lassen Sie die Frequenzermittlung aktiviert. Durch diese Methode wird sichergestellt, dass die Discovery Data Records (DDRs) für Geräte aktuell sind. Weitere Informationen zur Frequenzermittlung finden Sie unter [Informationen zur Frequenzermittlung](about-discovery-methods.md#bkmk_aboutHeartbeat).  

- Die **Serverermittlung** ist eine Methode für die automatische Ermittlung. Sie sucht nach Computern, die Sie als Standortsysteme verwenden. Sie können sie nicht konfigurieren oder deaktivieren.  


## <a name="active-directory-forest-discovery"></a><a name="BKMK_ConfigADForestDisc"></a> Active Directory-Gesamtstrukturermittlung  

Um die Konfiguration der Active Directory-Gesamtstrukturermittlung abzuschließen, konfigurieren Sie Einstellungen an den folgenden Stellen der Configuration Manager-Konsole:  

- Im Knoten **Ermittlungsmethoden**:

  - Sie können diese Ermittlungsmethode festlegen.  

  - Sie können einen Abfragezeitplan festlegen.  

  - Sie können auswählen, ob die Ermittlung automatisch Grenzen für die Active Directory-Standorte und Subnetze erstellt, die entdeckt werden.  

- Im Knoten **Active Directory-Gesamtstrukturen**:

  - Sie können Gesamtstrukturen hinzufügen, die Sie ermitteln möchten.  

  - Sie können die Ermittlung von Active Directory-Standorten und Subnetzen in dieser Gesamtstruktur aktivieren.  

  - Sie können Einstellungen konfigurieren, über die Configuration Manager-Standorte ihre Standortinformationen für die Gesamtstruktur veröffentlichen können.  

  - Sie können ein Konto zuweisen, das als Konto für die Active Directory-Gesamtstruktur für die einzelnen Gesamtstrukturen verwendet wird.  

Wenden Sie die folgenden Verfahren an, um die Active Directory-Gesamtstrukturermittlung zu aktivieren und individuelle Gesamtstrukturen für die Verwendung mit der Active Directory-Gesamtstrukturermittlung zu konfigurieren.  

### <a name="configure-active-directory-forest-discovery"></a>Konfigurieren der Active Directory-Gesamtstrukturermittlung  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie die Option **Hierarchiekonfiguration**, und wählen Sie den Knoten **Ermittlungsmethoden** aus.  

2. Wählen Sie die Methode Active Directory-Gesamtstrukturermittlung für den Standort, an dem die Ermittlung konfiguriert werden soll, aus.  

3. Wählen Sie auf der Registerkarte **Startseite** des Menübands die Option **Eigenschaften** aus.  

4. Konfigurieren Sie auf der Registerkarte **Allgemein** der Eigenschaften die folgenden Einstellungen:  

    - Aktivieren Sie die Ermittlungsmethode.

    - Geben Sie Optionen zum Erstellen von Standortgrenzen für ermittelte Orte an.  

    - Geben Sie einen Zeitplan für die Ausführung der Ermittlung an.  

5. Klicken Sie auf **OK**, um die Konfiguration zu speichern.  

### <a name="configure-a-forest-for-active-directory-forest-discovery"></a>Konfigurieren einer Gesamtstruktur für die Active Directory-Gesamtstrukturermittlung  

1. Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Hierarchiekonfiguration**, und klicken Sie dann auf den Knoten **Active Directory-Gesamtstrukturen**. Wenn eine Active Directory-Gesamtstrukturermittlung bereits ausgeführt wurde, werden die ermittelten Gesamtstrukturen im Ergebnisbereich angezeigt. Wenn diese Ermittlungsmethode ausgeführt wird, ermittelt sie die lokale Gesamtstruktur sowie alle vertrauenswürdigen Gesamtstrukturen. Fügen Sie nicht vertrauenswürdige Gesamtstrukturen manuell hinzu.  

    - Wählen Sie zum Konfigurieren einer bereits ermittelten Gesamtstruktur die gewünschte Gesamtstruktur im Ergebnisbereich aus. Wählen Sie im Menüband die Option **Eigenschaften** aus, um die Gesamtstruktureigenschaften zu öffnen.

    - Klicken Sie zum Konfigurieren einer nicht aufgeführten Gesamtstruktur auf der Registerkarte **Start** in der Gruppe **Erstellen** auf **Gesamtstruktur hinzufügen**. Diese Aktion öffnet das Dialogfeld **Gesamtstruktur hinzufügen**.

2. Schließen Sie auf der Registerkarte **Allgemein** die Konfiguration für die zu ermittelnde Gesamtstruktur ab, und geben Sie das **Konto für die Active Directory-Gesamtstruktur** an. Weitere Informationen zu diesem Konto finden Sie unter [Konten](../../../plan-design/hierarchy/accounts.md#active-directory-forest-account).  

    > [!NOTE]  
    > Für die Active Directory-Gesamtstrukturermittlung ist ein globales Konto erforderlich, damit Ermittlung und Veröffentlichung in nicht vertrauenswürdigen Gesamtstrukturen möglich sind. Wenn Sie nicht das Computerkonto des Standortservers verwenden, können Sie nur ein globales Konto auswählen.  

3. Wenn Sie planen, eine Veröffentlichung von Standortdaten in dieser Gesamtstruktur zu ermöglichen, konfigurieren Sie auf der Registerkarte **Veröffentlichen** das Veröffentlichen in dieser Gesamtstruktur.  

    > [!NOTE]  
    > Wenn Sie die Veröffentlichung von Standorten in einer Gesamtstruktur zulassen, erweitern Sie das Active Directory-Schema dieser Gesamtstruktur für Configuration Manager. Das Konto für die Active Directory-Gesamtstruktur muss Vollzugriff auf den Systemcontainer in dieser Gesamtstruktur besitzen.  

4. Klicken Sie auf **OK**, um die Konfiguration zu speichern.  


## <a name="active-directory-discovery-for-computers-users-or-groups"></a><a name="BKMK_ConfigADDiscGeneral"></a> Active Directory-Ermittlung für Computer, Benutzer oder Gruppen  

Um die Ermittlung von Computern, Benutzern oder Gruppen zu konfigurieren, beginnen Sie mit diesen allgemeinen Schritten:

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie die Option **Hierarchiekonfiguration**, und wählen Sie den Knoten **Ermittlungsmethoden** aus.  

2. Wählen Sie die Ermittlungsmethode für den Standort aus, an dem die Ermittlung konfiguriert werden soll.  

3. Wählen Sie auf der Registerkarte **Startseite** des Menübands die Option **Eigenschaften** aus.  

4. Aktivieren Sie auf der Registerkarte **Allgemein** der Eigenschaften das Kontrollkästchen zum Aktivieren der Ermittlung. Oder Sie können die Ermittlung auch sofort konfigurieren und später zurückkehren, um sie zu aktivieren.  

Befolgen Sie dann die Informationen in den folgenden Abschnitten, um die spezifischen Ermittlungsmethoden zu konfigurieren:  

- [Active Directory-Gruppenermittlung](#bkmk_config-adgd)  

- [Active Directory-Systemermittlung](#bkmk_config-adgd)  

- [Active Directory-Benutzerermittlung](#bkmk_config-adud)  

> [!NOTE]  
> Die Informationen in diesem Abschnitt gelten nicht für die Active Directory-Gesamtstrukturermittlung.  

Obwohl jede dieser Ermittlungsmethoden unabhängig von den anderen angewendet werden kann, sind ihre Optionen jedoch vergleichbar. Weitere Informationen zu diesen Konfigurationsoptionen finden Sie unter [Allgemeine Funktionen der Active Directory-Gruppenermittlung, Systemermittlung und Benutzerermittlung](about-discovery-methods.md#bkmk_shared).  

> [!WARNING]  
> Durch die Active Directory-Abfragen im Rahmen jeder dieser Ermittlungsmethoden kann eine erhebliche Netzwerkauslastung verursacht werden. Erwägen Sie, die Ermittlungsmethoden für Zeiten zu planen, wenn die geschäftliche Nutzung des Netzwerks durch eine solche Netzwerkauslastung nicht beeinträchtigt wird.  

### <a name="configure-active-directory-group-discovery"></a><a name="bkmk_config-adgd"></a> Konfigurieren der Active Directory-Gruppenermittlung  

1. Klicken Sie im Eigenschaftenfenster von „Active Directory-Gruppenermittlung“ auf der Registerkarte **Allgemein** auf **Hinzufügen**, um einen Ermittlungsbereich zu konfigurieren. Wählen Sie entweder **Gruppen** oder **Ort** aus. Schließen Sie im Dialogfeld **Gruppen hinzufügen** oder **Active Directory-Ort hinzufügen** die folgenden Konfigurationen ab:  

    1. Geben Sie einen **Namen** für diesen Ermittlungsbereich an.  

    2. Geben Sie eine **Active Directory-Domäne** oder einen **Ort** zum Durchsuchen an:  

        - Wenn Sie **Gruppen** ausgewählt haben, geben Sie mindestens eine Active Directory-Gruppe an, die ermittelt werden soll.  

        - Wenn Sie **Ort** ausgewählt haben, geben Sie einen Active Directory-Container als Ort an, der ermittelt werden soll. Sie können auch eine rekursive Suche in den untergeordneten Active Directory-Containern dieses Orts aktivieren.  

    3. Geben Sie das **Konto für die Active Directory-Sicherheitsgruppenermittlung** an, das zum Durchsuchen dieses Ermittlungsbereichs verwendet werden soll. Weitere Informationen finden Sie unter [Konten](../../../plan-design/hierarchy/accounts.md#active-directory-group-discovery-account).  

    4. Klicken Sie auf **OK**, um die Konfiguration des Ermittlungsbereichs zu speichern.  

2. Wiederholen Sie den vorherigen Schritt für jeden zusätzlichen Ermittlungsbereich, den Sie definieren möchten.  

3. Konfigurieren Sie auf der Registerkarte **Abfragezeitplan** den Zeitplan für die vollständige Ermittlungsabfrage sowie die Deltaermittlung.

4. Konfigurieren Sie auf der Registerkarte **Option** Einstellungen zum Herausfiltern oder Ausschließen veralteter Computerdatensätze von der Ermittlung. Konfigurieren Sie auch die Ermittlung der Mitgliedschaft von Verteilergruppen.  

    > [!NOTE]  
    > Von der Active Directory-Gruppenermittlung wird standardmäßig nur die Mitgliedschaft von Sicherheitsgruppen ermittelt.  

5. Klicken Sie auf **OK**, um die Konfiguration zu speichern.  

### <a name="configure-active-directory-system-discovery"></a><a name="bkmk_config-adsd"></a> Konfigurieren der Active Directory-Systemermittlung  

1. Klicken Sie im Eigenschaftenfenster von „Active Directory-Gruppenermittlung“ auf der Registerkarte **Allgemein** auf das Symbol **Neu**![Symbol „Neu“](media/Disc_new_Icon.gif), um einen neuen Active Directory-Container anzugeben. Beenden Sie im Dialogfeld **Active Directory-Container** die folgenden Konfigurationen:  

    1. Sie können einen Speicherort für den **Pfad** eingeben oder zu diesem navigieren. Dieser Wert ist ein gültiger LDAP-Pfad zu einem Container oder einer Organisationseinheit (OU). Der Standort fragt diesen Pfad nach Ressourcen ab. Beispiel: `LDAP://CN=Computers,DC=contoso,DC=com`  

    2. Geben Sie Optionen an, die das Suchverhalten ändern:  

        - **Objekte in Active Directory-Gruppen ermitteln:** Der Standort berücksichtigt auch die Mitgliedschaft von Gruppen unter diesem Pfad.  

        - **Untergeordnete Active Directory-Container rekursiv durchsuchen:** Wenn Sie diese Option aktivieren, sucht der Standort nach allen zusätzlichen Containern oder OUs unter dem obigen Pfad. Wenn Sie diese Option deaktivieren, sucht der Standort Ressourcen nur im angegebenen Pfad.  

          Wählen Sie ab Version 1806 Untercontainer aus, die von dieser rekursiven Suche ausgeschlossen werden sollen. Diese Option ist hilfreich zum Reduzieren der Anzahl ermittelter Objekte. Klicken Sie auf **Hinzufügen**, um die Container unter dem obigen Pfad auszuwählen. Wählen Sie im Dialogfeld „Neuer Container“ einen untergeordneten Container aus, der ausgeschlossen werden soll. Klicken Sie auf **OK**, um das Dialogfeld „Neuen Container auswählen“ zu schließen.<!--1358143-->

          > [!Tip]  
          > Im Eigenschaftenfenster der Active Directory-Systemermittlung sehen Sie, dass die Liste der Active Directory-Container die Spalte **Umfasst Ausschlüsse** aufweist. Wenn Sie auszuschließende Container auswählen, ist dieser Wert **Ja**.  

    3. Geben Sie für jeden Speicherort ein Konto an, das als **Active Directory-Ermittlungskonto**verwendet werden soll. Weitere Informationen finden Sie unter [Konten](../../../plan-design/hierarchy/accounts.md#active-directory-system-discovery-account).  

        > [!TIP]  
        > Sie können für jeden angegebenen Speicherort einen Satz von Ermittlungsoptionen und ein eindeutiges Active Directory-Ermittlungskonto konfigurieren.  

    4. Klicken Sie auf **OK**, um die Konfiguration des Active Directory-Containers zu speichern.  

2. Konfigurieren Sie auf der Registerkarte **Abfragezeitplan** den Zeitplan für die vollständige Ermittlungsabfrage sowie die Deltaermittlung.  

3. Sie können auf der Registerkarte **Active Directory-Attribute** zusätzliche Active Directory-Attribute für Computer konfigurieren, die ermittelt werden sollen. Auf dieser Registerkarte sind die Standardobjektattribute aufgelistet.  

    > [!Tip]  
    > Ihre Organisation verwendet beispielsweise das Attribut **Beschreibung** für das Computerkonto in Active Directory. Klicken Sie auf **Benutzerdefiniert**, und fügen Sie `Description` als benutzerdefiniertes Attribut hinzu. Sobald die Ermittlungsmethode ausgeführt wird, wird dieses Attribut auf der Registerkarte „Geräteeigenschaften“ in der Configuration Manager-Konsole angezeigt.<!--513948-->  

4. Konfigurieren Sie auf der Registerkarte **Option** Einstellungen zum Herausfiltern oder Ausschließen veralteter Computerdatensätze von der Ermittlung.  

5. Klicken Sie auf **OK**, um die Konfiguration zu speichern.  

### <a name="configure-active-directory-user-discovery"></a><a name="bkmk_config-adud"></a> Konfigurieren der Active Directory-Benutzerermittlung  

1. Klicken Sie im Eigenschaftenfenster von „Active Directory-Benutzerermittlung“ auf der Registerkarte **Allgemein** auf das Symbol **Neu**![Symbol „Neu“](media/Disc_new_Icon.gif), um einen neuen Active Directory-Container anzugeben. Beenden Sie im Dialogfeld **Active Directory-Container** die folgenden Konfigurationen:  

    1. Geben Sie mindestens einen Speicherort an, der durchsucht werden soll.  

    2. Geben Sie für jeden Speicherort Optionen an, von denen das Suchverhalten geändert wird.  

    3. Geben Sie für jeden Speicherort ein Konto an, das als **Active Directory-Ermittlungskonto**verwendet werden soll. Weitere Informationen finden Sie unter [Konten](../../../plan-design/hierarchy/accounts.md#active-directory-user-discovery-account).  

        > [!NOTE]  
        > Sie können für jeden angegebenen Speicherort einen eindeutigen Satz von Ermittlungsoptionen und ein eindeutiges Active Directory-Ermittlungskonto konfigurieren.  

    4. Klicken Sie auf **OK**, um die Konfiguration des Active Directory-Containers zu speichern.  

2. Konfigurieren Sie auf der Registerkarte **Abfragezeitplan** den Zeitplan für die vollständige Ermittlungsabfrage sowie die Deltaermittlung.  

3. Sie können auf der Registerkarte **Active Directory-Attribute** zusätzliche Active Directory-Attribute für Computer konfigurieren, die ermittelt werden sollen. Auf dieser Registerkarte sind die Standardobjektattribute aufgelistet.  

4. Klicken Sie auf **OK**, um die Konfiguration zu speichern.  


## <a name="azure-ad-user-discovery"></a><a name="azureaadisc"></a> Azure AD-Benutzerermittlung

Die Aktivierung der Azure AD-Benutzerermittlung unterscheidet sich von der Aktivierung anderer Ermittlungsmethoden. Konfigurieren Sie sie, wenn Sie den Configuration Manager-Standort in Azure AD integrieren.

Weitere Informationen finden Sie unter [Azure AD-Benutzerermittlung](about-discovery-methods.md#azureaddisc).

### <a name="prerequisites"></a>Voraussetzungen

[Konfigurieren Sie Azure-Dienste](azure-services-wizard.md) für **Cloud Management**, um diese Ermittlungsmethode zu aktivieren und zu konfigurieren.

Wenn Sie die Azure-App mit Configuration Manager *erstellen*, wird die App mit den erforderlichen Berechtigungen konfiguriert.

Wenn Sie die App erst in Azure erstellen und anschließend in Configuration Manager *importieren*, müssen Sie die App manuell konfigurieren. Bei dieser Konfiguration werden die Server-App-Berechtigungen zum Lesen von Verzeichnisdaten gewährt.

1. Öffnen Sie das [Azure-Portal](https://portal.azure.com) als Benutzer mit den Berechtigungen für *Globaler Administrator*. Wechseln Sie zu **Azure Active Directory**, und wählen Sie **App-Registrierungen** aus. Wechseln Sie ggf. zu **Alle Anwendungen**.

1. Wählen Sie die Zielanwendung aus.

1. Wählen Sie im Menü **Verwalten** die Option **API-Berechtigungen** aus.  

    1. Wählen Sie im Bereich **API-Berechtigungen** die Option **Berechtigung hinzufügen** aus.  

    2. Wechseln Sie im Bereich **API-Berechtigungen anfordern** zu **Von meiner Organisation verwendete APIs**.  

    3. Suchen Sie nach der **Microsoft Graph**-API, und wählen Sie sie aus.  

        > [!Tip]
        > Verwenden Sie in Version 1810 und früher die **Azure Active Directory Graph**-API.

    4. Wählen Sie die Gruppe **Anwendungsberechtigungen** aus. Erweitern Sie **Verzeichnis**, und wählen Sie **Directory.Read.All** aus.  

    5. Wählen Sie **Berechtigungen hinzufügen** aus.  

1. Wählen Sie im Bereich **API-Berechtigungen** im Abschnitt **Einwilligung erteilen** die Option **Administratoreinwilligung gewähren** aus. Wählen Sie **Ja** aus.  

### <a name="configure-azure-ad-user-discovery"></a>Konfigurieren der Azure AD-Benutzerermittlung

Führen Sie beim Konfigurieren des Azure-Diensts **Cloud Management** Folgendes durch:

- Klicken Sie auf der Seite **Ermittlung** des Assistenten auf **Azure Active Directory-Benutzerermittlung aktivieren**.
- Wählen Sie **Einstellungen** aus.
- Konfigurieren Sie im Dialogfeld „Einstellungen der Azure AD-Benutzerermittlung“ einen Zeitplan für die Ermittlung. Sie können auch die Deltaermittlung aktivieren, bei der nur eine Überprüfung auf neue oder geänderte Konten in Azure AD erfolgt.

> [!Note]  
> Wenn der Benutzer eine Verbundsidentität oder synchronisierte Identität ist, müssen Sie in Configuration Manager die [Active Directory-Benutzerermittlung](about-discovery-methods.md#bkmk_aboutUser) und die Azure AD-Benutzerermittlung verwenden. Weitere Informationen zu Hybrididentitäten finden Sie unter [Definieren einer Strategie zur Hybrididentitätsübernahme](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy).<!--497750-->


## <a name="azure-ad-user-group-discovery"></a><a name="bkmk_azuregroupdisco"></a> Konfigurieren der Azure AD-Benutzergruppenermittlung

<!--3611956-->
> [!Tip]  
> Dieses Feature wurde erstmals in Version 1906 als [Vorabfeature](../../manage/pre-release-features.md) eingeführt. Ab Version 2002 ist es kein Vorabfeature mehr.  

Sie können Benutzergruppen und Mitglieder dieser Gruppen aus Azure AD ermitteln. Wenn der Standort Benutzer in Azure AD-Gruppen ermittelt, die zuvor nicht ermittelt wurden, fügt er diese in Configuration Manager als neue Benutzerressourcen hinzu. Ein Benutzergruppen-Datensatz wird erstellt, wenn die Gruppe eine Sicherheitsgruppe ist.

### <a name="prerequisites"></a>Voraussetzungen

- [Azure-Dienst](azure-services-wizard.md) zur Cloudverwaltung
- Berechtigung zum Lesen und Suchen von Azure AD-Gruppen

### <a name="limitations"></a>Einschränkungen

Die Deltaermittlung ist für die Ermittlung von Azure AD-Benutzergruppen in Version 1906 deaktiviert. Sie können sie ab Configuration Manager Version 1910 aktivieren.

### <a name="log-files"></a>Protokolldateien

Verwenden Sie die Protokolldatei SMS_AZUREAD_DISCOVERY_AGENT.log für die Problembehandlung. Dieses Protokoll wird auch für die Azure AD Benutzerermittlung freigegeben. Weitere Informationen finden Sie in den [Protokolldateien](../../../plan-design/hierarchy/log-files.md#BKMK_ServerLogs).

### <a name="enable-azure-ad-user-group-discovery"></a>Aktivieren der Azure AD-Benutzergruppenermittlung

So aktivieren Sie die Ermittlung für einen vorhandenen **Cloud Management**-Azure-Dienst:

1. Erweitern Sie im Arbeitsbereich **Verwaltung** den Bereich **Clouddienste**, und wählen Sie dann den Knoten **Azure-Dienste**  aus.
1. Wählen Sie einen Ihrer Azure-Dienste aus, und klicken Sie dann im Menüband auf **Eigenschaften**.
1. Aktivieren Sie auf der Registerkarte **Ermittlung** das Kontrollkästchen **Azure Active Directory-Gruppenermittlung aktivieren**, und wählen Sie dann **Einstellungen** aus.
1. Klicken Sie auf der Registerkarte **Ermittlungsbereiche** auf **Hinzufügen**.
    - Sie können den **Abfragezeitplan** auf der anderen Registerkarte ändern.
1. Wählen Sie mindestens eine Benutzergruppe aus. Sie können nach Namen **Suchen** und wahlweise **Nur Sicherheitsgruppen** anzeigen.
    - Wenn Sie das erste Mal **Suchen** auswählen, werden Sie aufgefordert, sich bei Azure anzumelden.
1. Wählen Sie **OK** aus, wenn Sie die Gruppen ausgewählt haben.
1. Nach Abschluss der Erkennung können Sie Ihre Azure AD-Benutzergruppen im Knoten **Benutzer** durchsuchen.

So aktivieren Sie die Ermittlung beim Konfigurieren eines neuen **Cloud Management**-Azure-Diensts:

- Klicken Sie auf der Seite **Ermittlung** des Assistenten auf **Azure Active Directory-Gruppenermittlung aktivieren**.
- Wählen Sie **Einstellungen** aus.
- Konfigurieren Sie im Dialogfeld „Azure AD Group Discovery Settings“ (Einstellungen der Azure AD-Gruppenermittlung) Ihren Ermittlungsbereich sowie einen Zeitplan für die Ermittlung.


## <a name="heartbeat-discovery"></a><a name="BKMK_ConfigHBDisc"></a> Frequenzermittlung

Configuration Manager aktiviert die Frequenzermittlungsmethode, wenn Sie einen primären Standort installieren. Wenn Sie den Standardzeitplan „Alle sieben Tage“ verwenden möchten, gibt es nichts weiter zu konfigurieren. Andernfalls müssen Sie lediglich mithilfe eines Zeitplans festlegen, wie oft die Discovery Data Records der Frequenzermittlung von den Clients an einen Verwaltungspunkt gesendet werden sollen.  

> [!NOTE]  
> Wenn Sie an einem Standort die Clientpushinstallation und den Standortwartungstask **Installationsflag löschen** zugleich aktivieren, legen Sie den Zeitplan für die Frequenzermittlung mit einem kürzeren Zeitraum als dem **Clientneuermittlungs-Zeitraum** des Standortwartungstasks **Installationsflag löschen** fest. Weitere Informationen zu Standortwartungstasks finden Sie unter [Wartungstasks](../../manage/maintenance-tasks.md).  

### <a name="configure-the-heartbeat-discovery-schedule"></a>Konfigurieren des Zeitplans für die Frequenzermittlung  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie die Option **Hierarchiekonfiguration**, und wählen Sie den Knoten **Ermittlungsmethoden** aus.  

2. Wählen Sie die Methode **Frequenzermittlung** für den Standort aus, an dem die Frequenzermittlung konfiguriert werden soll.  

3. Wählen Sie auf der Registerkarte **Startseite** des Menübands die Option **Eigenschaften** aus.  

4. Konfigurieren Sie die Häufigkeit, mit der Discovery Data Records der Frequenzermittlung von den Clients übermittelt werden sollen. Klicken Sie dann auf **OK**, um die Konfiguration zu speichern.  


<a name="BKMK_AboutConfigNetworkDisc"></a>

## <a name="network-discovery"></a><a name="BKMK_ConfigNetworkDisc"></a> Netzwerkermittlung  

Bevor Sie die Netzwerkermittlung konfigurieren können, müssen Sie die folgenden Themen verstehen:  

- Verfügbare Ebenen der Netzwerkermittlung  

- Verfügbare Optionen der Netzwerkermittlung  

- Begrenzen der Netzwerkermittlung im Netzwerk  

Weitere Informationen finden Sie in [Informationen zur Netzwerkermittlung](about-discovery-methods.md#bkmk_aboutNetwork).  

In den folgenden Abschnitten finden Sie Informationen zu häufig verwendeten Konfigurationen für die Netzwerkermittlung. Sie können eine oder mehrere dieser Konfigurationen innerhalb einer Ermittlungsausführung verwenden. Wenn Sie mehrere Konfigurationen verwenden, müssen Sie die Interaktionen berücksichtigen, durch die die Ermittlungsergebnisse beeinflusst werden können.  

Angenommen, Sie ermitteln alle SNMP-Geräte (Simple Network Management Protocol) mit einem bestimmten öffentlichen SNMP-Namen. Für dieselbe Ermittlungsausführung deaktivieren Sie die Ermittlung in einem bestimmten Subnetz. Wenn die Ermittlung ausgeführt wird, werden die SNMP-Geräte mit dem angegebenen öffentlichen Namen im deaktivierten Subnetz nicht ermittelt.  

### <a name="determine-your-network-topology"></a><a name="BKMK_DetermineNetTopology"></a> Bestimmen der Netzwerktopologie  

Sie können eine topologiebezogene Ermittlung verwenden, um Ihr Netzwerk zuzuordnen. Von dieser Art der Ermittlung werden keine potenziellen Clients erkannt. Die topologiebezogene Netzwerkermittlung beruht auf SNMP.  

Wenn Sie Ihre Netzwerktopologie zuordnen, konfigurieren Sie im Dialogfeld **Netzwerkermittlung Eigenschaften** auf der Registerkarte **SNMP** die **Maximale Hopanzahl**. Bei einer geringen Hopanzahl ist es einfacher, die Netzwerkauslastung beim Ausführen der Ermittlung zu kontrollieren. Mit zunehmender Ermittlung des Netzwerks können Sie die Hopanzahl steigern, um sich ein besseres Bild Ihrer Netzwerktopologie zu verschaffen.  

Nachdem Sie sich mit Ihrer Netzwerktopologie vertraut gemacht haben, konfigurieren Sie zusätzliche Eigenschaften für die Netzwerkermittlung. Diese Eigenschaften helfen, potenzielle Clients und deren Betriebssysteme zu ermitteln. Konfigurieren Sie auch die Netzwerkermittlung so, dass die Netzwerksegmente eingeschränkt werden, die durchsucht werden können.  

Weitere Informationen finden Sie unter [Bestimmen der Netzwerktopologie](#bkmk_proc-top).

### <a name="network-discovery-search-options"></a>Suchoptionen für die Netzwerkermittlung

Configuration Manager unterstützt die folgenden Methoden zum Durchsuchen des Netzwerks:

- [Begrenzen von Suchvorgängen mithilfe von Subnetzen](#BKMK_LimitBySubnet)
- [Durchsuchen einer bestimmten Domäne](#BKMK_SearchByDomain)
- [Begrenzen von Suchvorgängen mithilfe von SNMP-Communitynamen](#BKMK_LimitBySNMPname)
- [Durchsuchen eines bestimmten DHCP-Servers](#BKMK_SearchByDHCP)

#### <a name="limit-searches-by-using-subnets"></a><a name="BKMK_LimitBySubnet"></a> Begrenzen von Suchvorgängen mithilfe von Subnetzen  

Sie können die Netzwerkermittlung so konfigurieren, dass bestimmte Subnetze durchsucht werden, wenn eine Ermittlung ausgeführt wird. Standardmäßig wird von der Netzwerkermittlung das Subnetz des Servers, auf dem die Ermittlung ausgeführt wird, durchsucht. Für alle zusätzlichen Subnetze, die Sie konfigurieren und aktivieren, gelten nur die Suchoptionen von SNMP und DHCP. Wenn von der Netzwerkermittlung Domänen durchsucht werden, gilt dabei keine konfigurierte Begrenzung auf Subnetze.  

Wenn Sie im Dialogfeld **Netzwerkermittlung** im Bereich „Eigenschaften“ auf der Registerkarte **Subnetze** ein oder mehrere Subnetze angeben, werden nur die Subnetze durchsucht, die Sie als **Aktiviert** gekennzeichnet haben.  

Wenn Sie ein Subnetz deaktivieren, wird es vom Standort von der Ermittlung ausgeschlossen, und es gelten die folgenden Bedingungen:  

- SNMP-basierte Abfragen werden nicht im Subnetz ausgeführt.  

- Von DHCP-Servern wird keine Liste mit Ressourcen zurückgegeben, die sich im Subnetz befinden.  

- Von domänenbasierten Abfragen können Ressourcen im Subnetz ermittelt werden.  

#### <a name="search-a-specific-domain"></a><a name="BKMK_SearchByDomain"></a> Durchsuchen einer bestimmten Domäne  

Sie können die Netzwerkermittlung so konfigurieren, dass bei einer Ermittlungsausführung eine bestimmte Domäne oder ein bestimmter Domänensatz durchsucht wird. Standardmäßig wird von der Netzwerkermittlung die lokale Domäne des Servers, auf dem die Ermittlung ausgeführt wird, durchsucht.  

Wenn Sie im Dialogfeld **Netzwerkermittlung** im Bereich „Eigenschaften“ auf der Registerkarte **Domänen** eine oder mehrere Domänen angeben, werden nur die Domänen durchsucht, die Sie als **Aktiviert** gekennzeichnet haben.  

Wenn Sie eine Domäne deaktivieren, wird sie vom Standort von der Ermittlung ausgeschlossen, und es gelten die folgenden Bedingungen:  

- Von der Netzwerkermittlung werden keine Domänencontroller in dieser Domäne abgefragt.  

- SNMP-basierte Abfragen können auf Subnetzen in der Domäne weiterhin ausgeführt werden.  

- Von DHCP-Servern werden weiterhin Listen mit Ressourcen in der Domäne zurückgegeben.  

#### <a name="limit-searches-by-using-snmp-community-names"></a><a name="BKMK_LimitBySNMPname"></a> Begrenzen von Suchvorgängen mithilfe von SNMP-Communitynamen  

Sie können die Netzwerkermittlung so konfigurieren, dass eine bestimmte SNMP-Community oder ein bestimmter Communitysatz durchsucht wird, wenn eine Ermittlung ausgeführt wird. Standardmäßig konfiguriert die Methode den **öffentlichen** Communitynamen.  

Die Netzwerkermittlung verwendet Communitynamen für den Zugriff auf Router, bei denen es sich um SNMP-Geräte handelt. Von einem Router können Informationen zu verknüpften Routern und Subnetzen für die Netzwerkermittlung bereitgestellt werden.  

> [!NOTE]  
> SNMP-Communitynamen sind mit Kennwörtern vergleichbar. Die Netzwerkermittlung kann nur Informationen von einem SNMP-Medium beziehen, für das Sie einen Communitynamen angegeben haben. Jedes SNMP-Gerät kann einen eigenen Communitynamen besitzen, oft verwenden jedoch mehrere Medien denselben Communitynamen. Zusätzlich haben die meisten SNMP-Geräte den Standardcommunitynamen **Öffentlich**. Von einigen Unternehmen wird der **öffentliche** Communityname jedoch als Sicherheitsmaßnahme von den Geräten gelöscht.  

Wenn im Dialogfeld **Netzwerkermittlung** im Bereich „Eigenschaften“ auf der Registerkarte **SNMP** mehrere SNMP-Communitys hinzugefügt werden, werden diese in der angezeigten Reihenfolge durchsucht. Stellen Sie sicher, dass die am häufigsten verwendeten Namen ganz oben in der Liste stehen. Diese Konfiguration trägt dazu bei, den Netzwerkdatenverkehr zu minimieren, den der Standort generiert, wenn er versucht, ein Gerät unter verschiedenen Namen zu kontaktieren.

> [!NOTE]  
> Zusätzlich zum SNMP-Communitynamen können Sie auch die IP-Adresse oder den auflösbaren Namen eines bestimmten SNMP-Geräts verwenden. Diese Aktion erfolgt im Dialogfeld **Eigenschaften der Netzwerkermittlung** auf der Registerkarte **SNMP-Geräte**.  

#### <a name="search-a-specific-dhcp-server"></a><a name="BKMK_SearchByDHCP"></a> Durchsuchen eines bestimmten DHCP-Servers  

Sie können die Netzwerkermittlung zur Verwendung eines oder mehrerer bestimmter DHCP-Server zum Ermitteln der DHCP-Clients konfigurieren.  

Jeder DHCP-Server, den Sie im Dialogfeld **Netzwerkermittlung Eigenschaften** auf der Registerkarte **DHCP** angeben, wird von der Netzwerkermittlung durchsucht. Wenn die IP-Adresse durch den Server, von dem die Ermittlung ausgeführt wird, von einem DHCP-Server geleast wird, können Sie die Ermittlung für das Durchsuchen dieses DHCP-Servers konfigurieren. Aktivieren Sie dieses Verhalten, indem Sie das Kontrollkästchen **Den vom Standortserver verwendeten DHCP-Server einschließen** aktivieren.  

> [!NOTE]  
> Zum erfolgreichen Konfigurieren eines DHCP-Servers für die Netzwerkermittlung ist es erforderlich, dass IPv4 von der Umgebung unterstützt wird. Sie können die Netzwerkermittlung nicht für die Verwendung eines DHCP-Servers in einer nativen IPv6-Umgebung konfigurieren.  

### <a name="how-to-configure-network-discovery"></a><a name="BKMK_HowToConfigNetDisc"></a> Konfigurieren der Netzwerkermittlung  

Wenden Sie die folgenden Verfahren an, um zunächst nur Ihre Netzwerktopologie zu ermitteln und die Netzwerkermittlung danach für das Ermitteln potenzieller Clients mithilfe einer oder mehrerer verfügbarer Netzwerkermittlungsoptionen zu konfigurieren.  

#### <a name="how-to-determine-your-network-topology"></a><a name="bkmk_proc-top"></a> Bestimmen der Netzwerktopologie  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie die Option **Hierarchiekonfiguration**, und wählen Sie den Knoten **Ermittlungsmethoden** aus.  

2. Wählen Sie die **Netzwerkermittlung**smethode für den Standort aus, an dem die Ermittlung erfolgen werden soll.  

3. Wählen Sie auf der Registerkarte **Startseite** des Menübands die Option **Eigenschaften** aus.  

    - Aktivieren Sie auf der Registerkarte **Allgemein** die Option **Netzwerkermittlungsmethode aktivieren**. Wählen Sie dann in den Optionen von **Art der Ermittlung** den Eintrag **Topologie** aus.  

    - Aktivieren Sie auf der Registerkarte **Subnetze** die Option **Lokale Subnetze durchsuchen**.  

      > [!TIP]  
      > Wenn Sie die Subnetze kennen, aus denen Ihr Netzwerk besteht, deaktivieren Sie das Kontrollkästchen **Lokale Subnetze durchsuchen**. Klicken Sie anschließend auf das Symbol **Neu**![Symbol „Neu“](media/Disc_new_Icon.gif), um die bestimmten Subnetze hinzuzufügen, die Sie durchsuchen möchten. Durchsuchen Sie bei großen Netzwerken nur ein oder zwei Subnetze auf einmal, um die Belegung der Netzwerkbandbreite zu minimieren.  

    - Aktivieren Sie auf der Registerkarte **Domänen** die Option **Lokale Domäne durchsuchen**.  

    - Wählen Sie auf der Registerkarte **SNMP** in der Dropdownliste **Maximale Hopanzahl** eine Option aus. Diese Option gibt die Anzahl der Routerhops an, die von der Netzwerkermittlung bei der Zuordnung der Topologie ausgeführt werden können.  

      > [!TIP]  
      > Für die erste Zuordnung Ihrer Netzwerktopologie konfigurieren Sie nur wenige Routerhops, um die Netzwerkauslastung zu minimieren.  

4. Klicken Sie auf der Registerkarte **Zeitplan** auf das Symbol **Neu**![Symbol „Neu“](media/Disc_new_Icon.gif), um einen Zeitplan für die Ausführung der Ermittlung festzulegen.  

    > [!NOTE]  
    > Es ist nicht möglich, einzelnen Zeitplänen für die Netzwerkermittlung verschiedene Ermittlungskonfigurationen zuzuweisen. Bei jedem Ausführen der Netzwerkermittlung wird die aktuelle Ermittlungskonfiguration verwendet.  

5. Klicken Sie auf **OK**, um die Konfigurationen zu übernehmen. Die Netzwerkermittlung wird zum geplanten Zeitpunkt ausgeführt.  

#### <a name="how-to-configure-network-discovery"></a><a name="bkmk_proc-config"></a> Konfigurieren der Netzwerkermittlung  

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie die Option **Hierarchiekonfiguration**, und wählen Sie den Knoten **Ermittlungsmethoden** aus.  

2. Wählen Sie die **Netzwerkermittlung**smethode für den Standort aus, an dem die Ermittlung erfolgen werden soll.  

3. Wählen Sie auf der Registerkarte **Startseite** des Menübands die Option **Eigenschaften** aus.  

4. Aktivieren Sie auf der Registerkarte **Allgemein** die Option **Netzwerkermittlungsmethode aktivieren**.  

    - Wählen Sie in den Optionen unter **Art der Ermittlung** die Art der Ermittlung, die Sie ausführen möchten.  

    - Aktivieren Sie die Option **Langsames Netzwerk**, damit Configuration Manager bei Netzwerken mit geringer Bandbreite automatische Anpassungen vornimmt.  

5. Um die Ermittlung für die Suche nach Subnetzen zu konfigurieren, wechseln Sie zur Registerkarte **Subnetze**. Konfigurieren Sie dann ein oder mehrere der folgenden Optionen:  

    - Aktivieren Sie das Kontrollkästchen **Lokale Subnetze durchsuchen**, um die Ermittlung in Subnetzen auszuführen, die sich lokal auf dem Computer befinden, von dem die Ermittlung ausgeführt wird.  

    - Wenn ein bestimmtes Subnetz durchsucht werden soll, muss es unter **Zu durchsuchende Subnetze** aufgeführt sein, und der Wert **Suchen** muss **Aktiviert** lauten:  

      1. Ist das Subnetz nicht aufgeführt, klicken Sie auf das Symbol **Neu**![Symbol „Neu“](media/Disc_new_Icon.gif). Geben Sie im Dialogfeld **Neue Subnetzzuweisung** die Informationen zu **Subnetz** und **Maske** ein, und klicken Sie dann auf **OK**. Es wird standardmäßig ein neues Subnetz für die Suche aktiviert.  

      2. Um den Wert **Suche** für ein aufgelistetes Subnetz zu ändern, wählen Sie es in der Liste aus. Klicken Sie dann auf das **Umschaltsymbol**, um den Wert zwischen **Deaktiviert** und **Aktiviert** umzuschalten.  

6. Um die Ermittlung für die Suche nach Domänen zu konfigurieren, wechseln Sie zur Registerkarte **Domänen**. Konfigurieren Sie dann ein oder mehrere der folgenden Optionen:  

    - Aktivieren Sie das Kontrollkästchen **Lokale Domäne durchsuchen**, um die Ermittlung in der Domäne des Computers auszuführen, der die Ermittlung ausführt.  

    - Wenn eine bestimmte Domäne durchsucht werden soll, muss sie unter **Domänen** aufgeführt sein, und der Wert **Suchen** muss **Aktiviert** lauten:  

      1. Wenn die Domäne nicht aufgeführt ist, klicken Sie auf das Symbol **Neu**![Symbol „Neu“](media/Disc_new_Icon.gif). Geben Sie im Dialogfeld **Domäneneigenschaften** die Informationen für die **Domäne** ein, und klicken Sie dann auf **OK**. Es wird standardmäßig eine neue Domäne für die Suche aktiviert.  

      2. Um den Wert **Suche** für eine aufgelistete Domäne zu ändern, wählen Sie sie in der Liste aus. Klicken Sie dann auf das **Umschaltsymbol**, um den Wert zwischen **Deaktiviert** und **Aktiviert** umzuschalten.  

7. Zum Konfigurieren der Ermittlung für das Durchsuchen bestimmter SNMP-Communitynamen für SNMP-Geräte wechseln Sie zur Registerkarte **SNMP**. Konfigurieren Sie dann ein oder mehrere der folgenden Optionen:  

    - Klicken Sie zum Hinzufügen eines SNMP-Communitynamens zur Liste **SNMP-Communitynamen** auf das Symbol **Neu**![Symbol „Neu“](media/Disc_new_Icon.gif). Geben Sie im Dialogfeld **Neuer SNMP-Communityname** den **Namen** der SNMP-Community ein, und klicken Sie dann auf **OK**.  

    - Wenn Sie einen SNMP-Communitynamen entfernen möchten, wählen Sie den Namen und anschließend das Symbol **Löschen**![Symbol „Löschen“](media/Disc_delete_Icon.gif) aus.  

    - Um die Suchreihenfolge der SNMP-Communitynamen anzupassen, wählen Sie einen Communitynamen in der Liste aus. Klicken Sie dann auf das Symbol **Element nach oben verschieben**![Symbol „Element nach oben verschieben“](media/Disc_moveUp_Icon.gif) oder **Element nach unten verschieben**![Symbol „Element nach oben verschieben“](media/Disc_moveDown_Icon.gif). Beim Ausführen der Ermittlung werden die Communitynamen von oben nach unten durchsucht. 

    - Zum Konfigurieren der maximalen Anzahl von Routerhops bei SNMP-Suchen wählen Sie die gewünschte Anzahl in der Dropdownliste **Maximale Hopanzahl** aus.  

8. Um ein SNMP-Gerät zu konfigurieren, wechseln Sie zur Registerkarte **SNMP-Geräte**. Wenn das Gerät nicht aufgeführt ist, klicken Sie auf das Symbol **Neu**![Symbol „Neu“](media/Disc_new_Icon.gif). Geben Sie im Dialogfeld **Neues SNMP-Gerät** die IP-Adresse oder den Gerätenamen des SNMP-Geräts ein, und klicken Sie auf **OK**.  

    > [!NOTE]  
    > Wenn Sie einen Gerätenamen angeben, muss der NetBIOS-Name von Configuration Manager in eine IP-Adresse aufgelöst werden können.  

9. Zum Konfigurieren der Ermittlung für die Abfrage bestimmter DHCP-Server wechseln Sie zur Registerkarte **DHCP**. Konfigurieren Sie dann ein oder mehrere der folgenden Optionen:  

    - Wenn der DHCP-Server auf dem Computer, auf dem die Ermittlung ausgeführt wird, abgefragt werden soll, aktivieren Sie **Immer den DHCP-Server des Standortservers verwenden**.  

      > [!NOTE]  
      > Dabei ist es erforderlich, dass die IP-Adresse durch den Server von einem DHCP-Server geleast wird. Es kann keine statische IP-Adresse verwendet werden.  

    - Klicken Sie zum Abfragen eines bestimmten DHCP-Servers auf das Symbol **Neu**![Symbol „Neu“](media/Disc_new_Icon.gif). Geben im Dialogfeld **Neuer DHCP-Server** die IP-Adresse bzw. den Servernamen des DHCP-Servers an, und klicken Sie dann auf **OK**.  

      > [!NOTE]  
      > Wenn Sie einen Servernamen angeben, muss der NetBIOS-Name von Configuration Manager in eine IP-Adresse aufgelöst werden können.  

10. Um zu konfigurieren, wann die Ermittlung ausgeführt wird, wechseln Sie zur Registerkarte **Zeitplan**. Klicken Sie auf das Symbol **Neu**![Symbol „Neu“](media/Disc_new_Icon.gif), um einen Zeitplan für die Ausführung der Netzwerkermittlung festzulegen. Sie können mehrere sich wiederholende und sich nicht wiederholende Zeitpläne konfigurieren.  

    > [!NOTE]  
    > Wenn auf der Registerkarte **Zeitplan** mehrere Zeitpläne gleichzeitig angezeigt werden, wird die Netzwerkermittlung für alle Zeitpläne ausgeführt, wie sie zu der im Zeitplan angegebenen Zeit konfiguriert ist. Dieses Verhalten gilt auch für Zeitpläne mit Wiederholung.  

11. Klicken Sie auf **OK**, um die Konfigurationen zu speichern.  

### <a name="how-to-verify-that-network-discovery-has-finished"></a><a name="BKMK_HowToVerifyNetDisc"></a> Überprüfen, ob die Netzwerkermittlung abgeschlossen ist  

Die Zeit, die für die Netzwerkermittlung erforderlich ist, wird von mindestens einem der folgenden Faktoren beeinflusst:  

- Die Größe des Netzwerks  

- Die Topologie des Netzwerks  

- Die maximale Anzahl von Hops, die zum Suchen von Routern im Netzwerk konfiguriert ist  

- Die Art der Ermittlung, die ausgeführt wird  

Bei der Netzwerkermittlung werden keine Benachrichtigungen erstellt, die Sie über den Abschluss informieren. Gehen Sie wie folgt vor, um zu überprüfen, ob die Ermittlung abgeschlossen wurde:  

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Überwachung**. Erweitern Sie **Systemstatus**, und wählen Sie dann den Knoten **Statusmeldungsabfragen** aus.  

2. Wählen Sie die Abfrage **Alle Statusmeldungen** aus.  

3. Wählen Sie auf dem Menüband auf der Registerkarte **Start** in der Gruppe **Statusmeldungsabfragen** die Option **Meldungen anzeigen** aus.  

4. Wählen Sie im Fenster „Alle Statusmeldungen“ in der Dropdownliste **Datum und Uhrzeit auswählen** einen Wert aus, der berücksichtigt, wie viel Zeit seit dem Start der Ermittlung vergangen ist. Klicken Sie dann auf **OK**, um die **Configuration Manager-Statusmeldungsanzeige** zu öffnen.  

    > [!TIP]  
    > Mithilfe der Option **Datum und Uhrzeit angeben** können Sie auch den Zeitpunkt (Datum und Uhrzeit) auswählen, zu dem die Ermittlung ausgeführt wurde. Diese Option ist nützlich, wenn Sie die Netzwerkermittlung an einem bestimmten Termin ausgeführt haben und nur Meldungen von diesem Datum abrufen möchten.  

5. Suchen Sie nach einer Statusmeldung mit den folgenden Details, um zu überprüfen, ob die Netzwerkermittlung abgeschlossen ist:  

    - Meldungs-ID: **502**  

    - Komponente: **SMS_NETWORK_DISCOVERY**  

    - Beschreibung: **Diese Komponente wurde beendet.**  

    Wenn diese Statusmeldung nicht vorhanden ist, ist die Netzwerkermittlung nicht abgeschlossen.  

6. Suchen Sie nach einer Statusmeldung mit den folgenden Details, um zu überprüfen, wann die Netzwerkermittlung gestartet wurde:  

    - Meldungs-ID: **500**  

    - Komponente: **SMS_NETWORK_DISCOVERY**  

    - Beschreibung: **Diese Komponente wurde gestartet.**  

    Dadurch wird bestätigt, dass die Netzwerkermittlung gestartet wurde. Wenn diese Informationen fehlen, planen Sie die Netzwerkermittlung neu.  
