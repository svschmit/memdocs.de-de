---
title: Konfigurieren von Azure-Diensten
titleSuffix: Configuration Manager
description: Verbinden Sie Ihre Configuration Manager-Umgebung mit Azure-Diensten für die Cloudverwaltung, Microsoft Store für Unternehmen und Log Analytics.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: how-to
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 7cb0a2c71a3ea326348b87d6b34e3109a8ef9f20
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700128"
---
# <a name="configure-azure-services-for-use-with-configuration-manager"></a>Konfigurieren von Azure-Diensten zur Verwendung mit dem Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Mit dem **Assistenten für Azure-Dienste** können Sie die Konfiguration der von Ihnen mit Configuration Manager verwendeten Azure-Clouddienste vereinfachen. Dieser Assistent bietet eine Erfahrung mit der allgemeinen Konfiguration durch Verwendung der Registrierungen für Azure AD-Web-Apps (Azure Active Directory). Diese Apps bieten Einzelheiten zu Abonnements und Konfiguration. Zudem authentifizieren sie die Kommunikation bei Azure AD. Durch die App müssen Sie nicht jedes Mal dieselben Informationen erneut eingeben, wenn Sie mit Azure eine neue Komponente oder einen neuen Dienst für Configuration Manager einrichten.

## <a name="available-services"></a>Verfügbare Dienste

Konfigurieren Sie die folgenden Azure-Dienste mithilfe dieses Assistenten:  

- **Cloud Management**: Dieser Dienst ermöglicht die Identifizierung von Standort und Clients über Azure AD. Durch diese Authentifizierung werden weitere Szenarios aktiviert, wie z.B.:  

  - [Installieren und Zuweisen von Windows 10-Clients in Configuration Manager mit Authentifizierung über Azure AD](../../../clients/deploy/deploy-clients-cmg-azure.md)  

  - [Configure Azure AD User Discovery (Konfigurieren der Azure AD-Benutzerermittlung)](configure-discovery-methods.md#azureaadisc)  

  - [Configure Azure AD User Group Discovery (Konfigurieren der Azure AD-Benutzergruppenermittlung)](configure-discovery-methods.md#bkmk_azuregroupdisco)

  - Unterstützung bestimmter [Cloud Management Gateway-Szenarios](../../../clients/manage/cmg/plan-cloud-management-gateway.md#scenarios)  

  - [E-Mail-Benachrichtigungen zur Genehmigung von Anwendungen](../../../../apps/deploy-use/app-approval.md#bkmk_email-approve)

- **Log Analytics-Connector**: [Herstellen einer Verbindung mit Azure Log Analytics](/azure/azure-monitor/platform/collect-sccm). Synchronisieren Sie die erfassten Daten mit Log Analytics.  

    > [!Note]  
    > Dieser Artikel beschreibt den *Log Analytics-Connector*, der früher *OMS-Connector* hieß. Die Funktionsweise ist identisch. Weitere Informationen finden Sie unter [Azure-Verwaltung – Überwachung](/azure/azure-monitor/terminology#log-analytics).  

- **Microsoft Store für Unternehmen**: Herstellen einer Verbindung mit dem [Microsoft Store für Unternehmen](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md). Hier erhalten Sie Store-Apps für Ihre Organisation, die Sie mit Configuration Manager bereitstellen können.  

### <a name="service-details"></a>Dienstdetails

Die folgende Tabelle enthält Einzelheiten zu den einzelnen Diensten.  

- **Mandanten**: Die Anzahl der konfigurierbaren Dienstinstanzen. Bei jeder Instanz muss es sich um einen anderen Azure AD-Mandanten handeln.  

- **Clouds**: Die globale Azure-Cloud wird von sämtlichen Diensten unterstützt. Private Clouds wie die Azure US Government Cloud werden jedoch nicht von allen Diensten unterstützt.  

- **Web-App**: Gibt an, ob der Dienst eine Azure AD-App vom Typ *Web-App/API* verwendet, die in Configuration Manager auch als Server-App bezeichnet wird.  

- **Native App**: Gibt an, ob der Dienst eine Azure AD-App vom Typ *Nativ* verwendet, die in Configuration Manager auch als Client-App bezeichnet wird.  

- **Aktionen**: Gibt an, ob Sie diese Apps im Assistent für Azure-Dienste von Configuration Manager importieren oder erstellen können.  

|Dienst  |Mandanten  |Clouds  |Web-App  |Native App  |Aktionen  |
|---------|---------|---------|---------|---------|---------|
|Cloudverwaltung mit<br>Azure AD-Ermittlung | Mehrere | Öffentlich, privat | ![Unterstützt](media/green_check.png) | ![Unterstützt](media/green_check.png) | Importieren, Erstellen |
|Log Analytics-Connector | Einer | Öffentlich, privat | ![Unterstützt](media/green_check.png) | ![Nicht unterstützt](media/Red_X.png) | Importieren |
|Microsoft Store für<br>Business | Einer | Öffentlich | ![Unterstützt](media/green_check.png) | ![Nicht unterstützt](media/Red_X.png) | Importieren, Erstellen |

### <a name="about-azure-ad-apps"></a>Informationen zu Azure AD-Apps

Für verschiedene Azure-Dienste sind unterschiedliche Konfigurationen erforderlich. Diese nehmen Sie im Azure-Portal vor. Darüber hinaus sind für die Apps der einzelnen Dienste möglicherweise separate Berechtigungen für Azure-Ressourcen erforderlich.  

Sie können eine einzige App für mehrere Dienste verwenden. In Configuration Manager und Azure AD muss nur ein Objekt verwaltet werden. Wenn der Sicherheitsschlüssel für die App abläuft, müssen Sie lediglich einen Schlüssel aktualisieren.

Wenn Sie weitere Azure-Dienste im Assistenten erstellen, kann Configuration Manager Informationen, die für verschiedene Dienste gleich sind, wiederverwenden. Dadurch müssen Sie die gleichen Informationen nicht mehrmals eingeben.

Weitere Informationen zu den erforderlichen App-Berechtigungen und Konfigurationen für die einzelnen Dienste finden Sie im zugehörigen Configuration Manager-Artikel unter [Verfügbare Dienste](#available-services).

Weitere Informationen zu Azure-Apps finden Sie in den folgenden Artikeln:

- [Authentifizierung und Autorisierung in Azure App Service](/azure/app-service/app-service-authentication-overview)
- [Web-App-Übersicht](/azure/app-service-web/app-service-web-overview)
- [Grundlagen der Anwendungsregistrierung in Azure AD](/azure/active-directory/develop/authentication-scenarios)  
- [Registrieren Sie Ihrer Anwendung bei Ihrem Azure Active Directory-Mandanten](/azure/active-directory/active-directory-app-registration)

## <a name="before-you-begin"></a>Vorbereitung

Nachdem Sie entschieden haben, mit welchem Dienst Sie sich verbinden möchten, sollten Sie sich die Tabelle unter [Dienstdetails](#service-details) ansehen. Diese Tabelle enthält die Informationen, die Sie zum Ausführen des Assistenten für Azure-Dienste benötigen. Besprechen Sie dies vorab mit Ihrem Azure AD-Administrator. Entscheiden Sie, welche der folgenden Aktionen durchgeführt werden sollen:

- Erstellen Sie die Apps manuell im Voraus im Azure-Portal. Importieren Sie anschließend die App-Details in Configuration Manager.  

- Verwenden Sie Configuration Manager zum direkten Erstellen der Apps in Azure AD. Lesen Sie die Informationen in den anderen Abschnitten dieses Artikels, um die notwendigen Daten von Azure AD erfassen.  

Bei einigen Diensten müssen die Azure AD-Apps über bestimmte Berechtigungen verfügen. Überprüfen Sie die Informationen für die einzelnen Dienste, um alle erforderlichen Berechtigungen zu bestimmen. Bevor Sie eine Web-App importieren können, muss diese z.B. zunächst von einem Administrator im [Azure-Portal](https://portal.azure.com) erstellt werden.

Erteilen Sie beim Konfigurieren des Log Analytics-Connectors Ihrer neu registrierten Web-App die Berechtigung *Mitwirkender* für die Ressourcengruppe, die den relevanten Arbeitsbereich enthält. Mit dieser Berechtigung kann Configuration Manager auf diesen Arbeitsbereich zugreifen. Suchen Sie beim Zuweisen der Berechtigung im Bereich **Benutzer hinzufügen** im Azure-Portal nach dem Namen der App-Registrierung. Dieser Vorgang ist identisch mit der [Configuration Manager-Bereitstellung mit Berechtigungen für Log Analytics](/azure/log-analytics/log-analytics-sccm#grant-configuration-manager-with-permissions-to-log-analytics). Ein Azure-Administrator muss diese Berechtigungen zuweisen, bevor Sie die App in Configuration Manager importieren können.

## <a name="start-the-azure-services-wizard"></a>Starten des Assistenten für Azure-Dienste

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie den Eintrag **Clouddienste**, und wählen Sie anschließend den Knoten **Azure-Dienste** aus.  

2. Wählen Sie im Menüband auf der Registerkarte **Start** in der Gruppe **Azure-Dienste** die Option **Azure-Dienste konfigurieren** aus.  

3. Gehen Sie auf der Seite **Azure-Dienste** des Assistenten für Azure-Dienste wie folgt vor:  

    1. Geben Sie einen **Namen** für das Objekt in Configuration Manager an.  

    2. Geben Sie eine optionale **Beschreibung** an, mit der Sie den Dienst identifizieren können.  

    3. Wählen Sie den Azure-Dienst aus, den Sie mit Configuration Manager verbinden möchten.  

4. Klicken Sie auf **Weiter**, um mit der Seite [Azure-App-Eigenschaften](#azure-app-properties) des Assistenten für Azure-Dienste fortzufahren.  

## <a name="azure-app-properties"></a>Azure-App-Eigenschaften

Wählen Sie auf der Seite **App** des Assistenten für Azure-Dienste zunächst die **Azure-Umgebung** aus der Liste aus. In der Tabelle unter [Dienstdetails](#service-details) finden Sie Informationen darüber, welche Umgebung derzeit für den Dienst verfügbar ist.

Die restlichen Inhalte der Seite „App“ variieren je nach angegebenem Dienst. In der Tabelle unter [Dienstdetails](#service-details) finden Sie Informationen darüber, welche Art von App der Dienst verwendet, und welche Aktion Sie verwenden können.

- Klicken Sie auf **Durchsuchen**, wenn die App sowohl Import- als auch Erstellaktionen unterstützt. Durch diese Aktion wird das Dialogfeld [Server-App](#server-app-dialog) oder das Dialogfeld [Client-App](#client-app-dialog) geöffnet.  

- Klicken Sie auf **Importieren**, wenn die App nur die Importaktion unterstützt. Durch diese Aktion wird das Dialogfeld [Apps importieren (Server)](#import-apps-dialog-server) oder das Dialogfeld [Apps importieren (Client)](#import-apps-dialog-client) geöffnet.

Klicken Sie nach Angabe der Apps auf dieser Seite auf **Weiter**, um mit der Seite [Konfiguration oder Ermittlung](#configuration-or-discovery) des Assistenten für Azure-Dienste fortzufahren.

### <a name="web-app"></a>Web-App

Diese App ist eine Azure-AD-App vom Typ *Web-App/API*, die in Configuration Manager auch als Server-App bezeichnet wird.

#### <a name="server-app-dialog"></a>Dialogfeld „Server-App“

Wenn Sie auf der Seite „App“ des Assistenten für Azure-Dienste bei der **Web-App** auf **Durchsuchen** klicken, wird das Dialogfeld „Server-App“ geöffnet. Es zeigt eine Liste an, die folgende Eigenschaften sämtlicher vorhandener Web-Apps enthält:

- Anzeigename des Mandanten
- App-Anzeigename
- Diensttyp

Sie können über das Dialogfeld „Server-App“ drei Aktionen ausführen:

- Wenn Sie eine vorhandene Web-App wiederverwenden möchten, wählen Sie diese aus der Liste aus.
- Klicken Sie auf **Importieren**, um das Dialogfeld [Apps importieren](#import-apps-dialog-server) zu öffnen.
- Klicken Sie auf **Erstellen**, um das Dialogfeld [Serveranwendung erstellen](#create-server-application-dialog) zu öffnen.

Klicken Sie nach dem Auswählen, Importieren oder Erstellen einer Web-App auf **OK**, um das Dialogfeld „Server-App“ zu schließen. Diese Aktion kehrt zur Seite [App](#azure-app-properties) des Assistenten für Azure-Dienste zurück.

#### <a name="import-apps-dialog-server"></a>Dialogfeld „Apps importieren (Server)“

Wenn Sie auf der Seite „App“ des Assistenten für Azure-Dienste im Dialogfeld „Server-App“ die Option **Importieren** auswählen, wird das Dialogfeld „Apps importieren“ geöffnet. Auf dieser Seite können Sie die Informationen zu einer Azure AD-Web-App eingeben, die bereits im Azure-Portal erstellt wurde. Zudem werden Metadaten zu dieser Web-App in Configuration Manager importiert. Geben Sie die folgenden Informationen an:

- **Name des Azure AD-Mandanten**: Der Name Ihres Azure AD-Mandanten.
- **ID des Azure AD-Mandanten**: Die GUID Ihres Azure AD-Mandanten.
- **Anwendungsname**: Ein Anzeigename der App (z. B. in der App-Registrierung).
- **Client-ID:** Der Wert **Anwendungs- (Client-) ID** der App-Registrierung. Das Format ist eine Standard-GUID.
- **Geheimer Schlüssel**: Sie müssen den geheimen Schlüssel kopieren, wenn Sie die App in Azure AD registrieren.
- **Ablauf des geheimen Schlüssels**: Wählen Sie im Kalender ein Datum in der Zukunft aus.
- **App-ID-URI**: Dieser Wert muss bei Ihrem Azure AD-Mandanten eindeutig sein. Es handelt sich dabei um das Zugriffstoken, mit dem der Konfigurations-Manager-Client Zugriff auf den Dienst anfordert. Der Wert ist der **URI der Anwendungs-ID** des App-Registrierungseintrags im Azure AD-Portal. Das Format ähnelt `https://ConfigMgrService`.

Klicken Sie nach Eingabe der Informationen auf **Überprüfen**. Klicken Sie anschließend auf **OK**, um das Dialogfeld „Apps importieren“ zu schließen. Diese Aktion kehrt entweder zur Seite [App](#azure-app-properties) des Assistenten für Azure-Dienste oder zum Dialogfeld [Server-App](#server-app-dialog) zurück.

> [!TIP]
> Wenn Sie die App in Azure AD registrieren, müssen Sie möglicherweise den folgenden **Umleitungs-URI** manuell angeben: `ms-appx-web://Microsoft.AAD.BrokerPlugin/<ClientID>`. Geben Sie z. B. die GUID der Client-ID der App an: `ms-appx-web://Microsoft.AAD.BrokerPlugin/a26a653e-17aa-43eb-ab36-0e36c7d29f49`.<!-- SCCMDocs#1135 -->

#### <a name="create-server-application-dialog"></a>Dialogfeld „Serveranwendung erstellen“

Wenn Sie im Dialogfeld „Server-App“ die Option **Erstellen** auswählen, wird das Dialogfeld „Serveranwendung erstellen“ geöffnet. Auf dieser Seite wird die Erstellung einer Web-App in Azure AD automatisiert. Geben Sie die folgenden Informationen an:

- **Anwendungsname**: Der Anzeigename für die App.
- **URL für Startseite**: Dieser Wert wird nicht von Configuration Manager verwendet, ist jedoch für Azure AD erforderlich. Der Standardwert beträgt `https://ConfigMgrService`.  
- **App-ID-URI**: Dieser Wert muss bei Ihrem Azure AD-Mandanten eindeutig sein. Es handelt sich dabei um das Zugriffstoken, mit dem der Konfigurations-Manager-Client Zugriff auf den Dienst anfordert. Der Standardwert beträgt `https://ConfigMgrService`.  
- **Gültigkeitsdauer des geheimen Schlüssels:** Wählen Sie entweder **1 Jahr** oder **2 Jahre** aus der Dropdownliste aus. Ein Jahr ist der Standardwert.

Klicken Sie auf **Anmelden**, um sich bei Azure als Administrator zu authentifizieren. Diese Anmeldeinformationen werden nicht in Configuration Manager gespeichert. Für diese Persona sind keine Berechtigungen in Configuration Manager erforderlich. Zudem muss das Konto nicht mit dem Konto identisch sein, auf dem der Assistent für Azure-Dienste ausgeführt wird. Nach einer erfolgreichen Authentifizierung in Azure, wird zu Referenzzwecken der **Name des Azure AD-Mandanten** auf der Seite angezeigt.

Klicken Sie auf **OK**, um die Web-App in Azure AD zu erstellen und das Dialogfeld „Serveranwendung erstellen“ zu schließen. Diese Aktion kehrt zum Dialogfeld [Server-App](#server-app-dialog) zurück.

> [!NOTE]
> Wenn Sie eine Richtlinie für den bedingten Azure AD-Zugriff definiert haben, die für **alle Cloud-Apps** gilt, müssen Sie die erstellte Serveranwendung aus dieser Richtlinie ausschließen. Weitere Informationen zum Ausschließen bestimmter Apps finden Sie in der [Dokumentation zum bedingten Zugriff mit Azure AD](/azure/active-directory/conditional-access/).

### <a name="native-client-app"></a>Native Client-App

Diese App ist eine Azure-AD-App vom Typ *Nativ*, die in Configuration Manager auch als Client-App bezeichnet wird.

#### <a name="client-app-dialog"></a>Dialogfeld „Client-App“

Wenn Sie auf der Seite „App“ des Assistenten für Azure-Dienste bei der **Nativen Client-App** auf **Durchsuchen** klicken, wird das Dialogfeld „Client-App“ geöffnet. Es zeigt eine Liste an, die folgende Eigenschaften sämtlicher vorhandener nativer Apps enthält:

- Anzeigename des Mandanten
- App-Anzeigename
- Diensttyp

Sie können über das Dialogfeld „Client-App“ drei Aktionen ausführen:

- Wenn Sie eine vorhandene native App wiederverwenden möchten, wählen Sie diese aus der Liste aus. 
- Klicken Sie auf **Importieren**, um das Dialogfeld [Apps importieren](#import-apps-dialog-client) zu öffnen.
- Klicken Sie auf **Erstellen**, um das Dialogfeld [Clientanwendung erstellen](#create-client-application-dialog) zu öffnen.

Klicken Sie nach dem Auswählen, Importieren oder Erstellen einer nativen App auf **OK**, um das Dialogfeld „Client-App“ zu schließen. Diese Aktion kehrt zur Seite [App](#azure-app-properties) des Assistenten für Azure-Dienste zurück.

#### <a name="import-apps-dialog-client"></a>Dialogfeld „Apps importieren (Client)“

Wenn Sie beim Dialogfeld „Client-App“ die Option **Importieren** auswählen, wird das Dialogfeld „Apps importieren“ geöffnet. Auf dieser Seite können Sie die Informationen zu einer nativen Azure AD-App eingeben, die bereits im Azure-Portal erstellt wurde. Zudem werden Metadaten zu dieser nativen App in Configuration Manager importiert. Geben Sie die folgenden Informationen an:

- **Anwendungsname**: Der Anzeigename für die App.
- **Client-ID:** Der Wert **Anwendungs- (Client-) ID** der App-Registrierung. Das Format ist eine Standard-GUID.

Klicken Sie nach Eingabe der Informationen auf **Überprüfen**. Klicken Sie anschließend auf **OK**, um das Dialogfeld „Apps importieren“ zu schließen. Diese Aktion kehrt zum Dialogfeld [Client-App](#client-app-dialog) zurück.

#### <a name="create-client-application-dialog"></a>Dialogfeld „Clientanwendung erstellen“

Wenn Sie im Dialogfeld „Client-App“ die Option **Erstellen** auswählen, wird das Dialogfeld „Clientanwendung erstellen“ geöffnet. Auf dieser Seite wird die Erstellung einer nativen App in Azure AD automatisiert. Geben Sie die folgenden Informationen an:

- **Anwendungsname**: Der Anzeigename für die App.
- **Antwort-URL**: Dieser Wert wird nicht von Configuration Manager verwendet, ist jedoch für Azure AD erforderlich. Der Standardwert beträgt `https://ConfigMgrService`.

Klicken Sie auf **Anmelden**, um sich bei Azure als Administrator zu authentifizieren. Diese Anmeldeinformationen werden nicht in Configuration Manager gespeichert. Für diese Persona sind keine Berechtigungen in Configuration Manager erforderlich. Zudem muss das Konto nicht mit dem Konto identisch sein, auf dem der Assistent für Azure-Dienste ausgeführt wird. Nach einer erfolgreichen Authentifizierung in Azure, wird zu Referenzzwecken der **Name des Azure AD-Mandanten** auf der Seite angezeigt.

Klicken Sie auf **OK**, um die native App in Azure AD zu erstellen und das Dialogfeld „Clientanwendung erstellen“ zu schließen. Diese Aktion kehrt zum Dialogfeld [Client-App](#client-app-dialog) zurück.

## <a name="configuration-or-discovery"></a>Konfiguration oder Ermittlung

Nach der Angabe der Web-Apps und nativen Apps auf der Seite „Apps“ fährt der Assistent für Azure-Dienste mit der Seite **Konfiguration** oder der Seite **Ermittlung** fort. Dies hängt von dem Dienst ab, mit dem Sie eine Verbindung herstellen. Die Details auf dieser Seite variieren abhängig vom jeweiligen Dienst. Weitere Informationen finden Sie in den folgenden Artikeln:  

- Dienst **Cloud Management**, Seite **Discovery**: [Configure Azure AD User Discovery (Konfigurieren der Azure AD-Benutzerermittlung)](configure-discovery-methods.md#azureaadisc)  

- Dienst **Log Analytics-Connector**, Seite **Konfiguration**: [Konfigurieren der Verbindung mit Log Analytics](/azure/azure-monitor/platform/collect-sccm)  

- Dienst **Microsoft Store für Unternehmen**, Seite **Konfigurationen**: [Konfigurieren der Synchronisierung mit Microsoft Store für Unternehmen](../../../../apps/deploy-use/manage-apps-from-the-windows-store-for-business.md#bkmk_config)  

Schließlich können Sie den Assistenten für Azure-Dienste über die Seiten „Zusammenfassung“, „Status“ und „Abschluss“ abschließen. Sie haben die Konfiguration eines Azure-Diensts in Configuration Manager abgeschlossen. Anhand dieser Anleitung können Sie auch weitere Azure-Dienste konfigurieren.

## <a name="renew-secret-key"></a><a name="bkmk_renew"></a> Geheimen Schlüssel erneuern

Sie müssen den geheimen Schlüssel der Azure AD-App vor Ablauf der Gültigkeitsdauer erneuern. Wenn Sie den Schlüssel ablaufen lassen, kann Configuration Manager sich nicht bei Azure AD authentifizieren, was dazu führt, dass Ihre verbundenen Azure-Dienste nicht mehr funktionieren.

Ab Version 2006 zeigt die Configuration Manager-Konsole Benachrichtigungen für die folgenden Umstände an:<!--6386392-->

- Mindestens ein geheimer Azure AD-Schlüssel für die App läuft bald ab
- Mindestens ein geheimer Azure AD-Schlüssel für die App ist abgelaufen

Um beide Probleme zu beheben, erneuern Sie den geheimen Schlüssel.

Weitere Informationen zur Interaktion mit diesen Benachrichtigungen finden Sie unter [Configuration Manager-Konsolenbenachrichtigungen](../../manage/admin-console-notifications.md).

### <a name="renew-key-for-created-app"></a>Schlüssel für erstellte App erneuern

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie **Clouddienste**, und wählen Sie den Knoten **Azure Active Directory-Mandanten** aus.

1. Wählen Sie im Detailbereich den Azure AD-Mandanten für die App aus.

1. Wählen Sie im Menüband die Option **Geheimen Schlüssel erneuern** aus. Geben Sie die Anmeldeinformationen des App-Besitzers oder eines Azure AD-Administrators ein.

### <a name="renew-key-for-imported-app"></a>Schlüssel für importierte App erneuern

Wenn Sie die Azure-App in Configuration Manager importiert haben, erneuern Sie den Schlüssel über das Azure-Portal. Notieren Sie den neuen geheimen Schlüssel und das Ablaufdatum. Fügen Sie diese Information im Assistent **Geheimen Schlüssel erneuern** hinzu.  

> [!NOTE]
> Speichern Sie den geheimen Schlüssel, bevor Sie die Seite **Schlüssel** unter den Eigenschaften der Azure-Anwendung schließen. Diese Informationen werden entfernt, wenn Sie die Seite schließen.

## <a name="view-the-configuration-of-an-azure-service"></a>Anzeigen der Konfiguration eines Azure-Diensts

Zeigen Sie die Eigenschaften eines Azure-Diensts an, den Sie zur Verwendung konfiguriert haben. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie den Eintrag **Clouddienste**, und wählen Sie **Azure-Dienste** aus. Wählen Sie den Dienst aus, den Sie anzeigen oder bearbeiten möchten, und klicken Sie anschließend auf **Eigenschaften**.

Wenn Sie einen Dienst auswählen und anschließend im Menüband auf **Löschen** klicken, wird durch diese Aktion die Verbindung in Configuration Manager gelöscht. Die App in Azure AD wird dadurch nicht entfernt. Bitten Sie Ihren Azure-Administrator, die App zu löschen, wenn sie nicht mehr benötigt wird. Alternativ können Sie den Assistenten für Azure-Dienste ausführen, um die App zu importieren.<!--483440-->

## <a name="cloud-management-data-flow"></a>Datenfluss bei der Cloudverwaltung

Bei dem folgenden Diagramm handelt es sich um einen konzeptionellen Datenfluss zwischen Configuration Manager, Azure AD und verbundenen Clouddiensten. In diesem konkreten Beispiel wird der Dienst **Cloudverwaltung** verwendet, der einen Windows 10-Client sowie Server- und Client-Apps umfasst. Die Abläufe bei anderen Diensten sind vergleichbar.

![Datenflussdiagramm für Configuration Manager mit Azure AD und Cloudverwaltung](media/aad-auth.png)

1. Der Configuration Manager-Administrator importiert oder erstellt die Client- und Server-Apps in Azure AD.  

2. Die Methode für die Azure AD-Benutzerermittlung in Configuration Manager wird ausgeführt. Der Standort verwendet das Token der Azure AD-Server-App für die Abfrage von Microsoft Graph nach Benutzerobjekten.  

3. Der Standort speichert Daten zu den Benutzerobjekten. Weitere Informationen finden Sie unter [Azure AD-Benutzerermittlung](about-discovery-methods.md#azureaddisc).  

4. Der Configuration Manager-Client fordert das Azure AD-Benutzertoken an. Der Client stellt den Anspruch mit der Anwendungs-ID der Azure AD-Client-App und der Server-App als Zielgruppe. Weitere Informationen finden Sie unter [Ansprüche in Azure AD-Sicherheitstokens](/azure/active-directory/develop/authentication-scenarios#security-tokens).  

5. Der Client authentifiziert sich beim Standort durch die Bereitstellung des Azure AD-Tokens für Cloud Management Gateway und den lokalen HTTPS-fähigen Verwaltungspunkt.  

Weitere ausführliche Informationen finden Sie unter [Workflow für die Azure AD-Authentifizierung](../../../clients/manage/azure-ccmsetup.md).