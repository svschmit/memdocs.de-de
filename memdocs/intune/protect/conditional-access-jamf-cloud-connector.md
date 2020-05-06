---
title: Integrieren des Jamf Pro-Cloudconnectors in Microsoft Intune
titleSuffix: Microsoft Intune
description: Verwenden Sie den Jamf Pro-Cloudconnector mit Konformitätsrichtlinien von Microsoft Intune zusammen mit dem bedingten Zugriff von Azure Active Directory, um mit Jamf verwaltete Geräte zu integrieren und zu sichern.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/13/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: arnab
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: f86b418df46069b2a33dd56d06e0e82dbbbf8090
ms.sourcegitcommit: 7f17d6eb9dd41b031a6af4148863d2ffc4f49551
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81538448"
---
# <a name="use-the-jamf-cloud-connector-with-microsoft-intune"></a>Verwenden des Jamf-Cloudconnectors mit Microsoft Intune

Dieser Artikel kann Ihnen helfen, den Jamf-Cloudconnector zu installieren, um Jamf Pro in Microsoft Intune zu integrieren. Der Cloudconnector automatisiert viele der Schritte, die erforderlich sind, wenn Sie die Integration manuell konfigurieren, wie in [Integrieren von Jamf Pro in Intune zu Konformitätszwecken](../protect/conditional-access-integrate-jamf.md) dokumentiert.

Wenn Sie den Cloudconnector einrichten:

- Setup erstellt automatisch die Jamf Pro-Anwendungen in Azure und vermeidet die Notwendigkeit, sie manuell zu konfigurieren.
- Sie können mehrere Instanzen von Jamf Pro mit demselben Azure-Mandanten integrieren, der Ihr Intune-Abonnement hostet.

Die Verbindung mehrerer Instanzen von Jamf Pro mit einem einzelnen Azure-Mandanten wird nur unterstützt, wenn Sie den Cloudconnector verwenden. Wenn Sie eine manuell konfigurierte Verbindung verwenden, kann nur eine einzelne Instanz von Jamf mit einem Azure-Mandanten integriert werden.

Die Verwendung des Cloudconnectors ist optional:

- Für neue Mandanten, die noch nicht in Jamf integriert sind, können Sie den Cloudconnector, wie in diesem Artikel beschrieben, konfigurieren. Oder Sie können die Integration manuell konfigurieren, wie in [Integrieren von Jamf Pro in Intune zu Konformitätszwecken](../protect/conditional-access-integrate-jamf.md) beschrieben.
- Für Mandanten, die bereits über eine manuelle Konfiguration verfügen, können Sie sich dafür entscheiden, diese Integration zu entfernen und dann den Cloudconnector einzurichten. Sowohl das Entfernen einer bestehenden Integration als auch die Einrichtung des Cloudconnectors werden in diesem Artikel beschrieben.

Wenn Sie planen, Ihre bisherige Integration durch den Jamf-Cloudconnector zu ersetzen:

- Verwenden Sie das Verfahren zum [Entfernen Ihrer aktuellen Konfiguration](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant), wozu auch das Löschen der Enterprise-Apps für Jamf Pro und das Deaktivieren der manuellen Integration gehören. Dann können Sie das [Verfahren zum Konfigurieren des Cloudconnectors verwenden](#configure-the-cloud-connector-for-a-new-tenant).
- Sie müssen Geräte nicht neu registrieren. Geräte, die bereits registriert sind, können den Cloudconnector ohne zusätzliche Konfiguration nutzen.
- Stellen Sie sicher, dass Sie den Cloudconnector innerhalb von 24 Stunden nach dem Entfernen Ihrer manuellen Integration konfigurieren, um sicherzustellen, dass Ihre registrierten Geräte weiterhin ihren Status melden können.

Weitere Informationen zum Jamf-Cloudconnector finden Sie unter [Konfigurieren der macOS-Integration von Intune mithilfe des Cloudconnectors](https://docs.jamf.com/technical-papers/jamf-pro/microsoft-intune/10.17.0/Configuring_the_macOS_Intune_Integration_using_the_Cloud_Connector.html) auf docs.jamf.com.

## <a name="prerequisites"></a>Voraussetzungen

**Produkte und Dienste**:  
- Jamf Pro 10.18 oder höher
- Ein Jamf Pro-Benutzerkonto mit bedingten Zugriffsrechten  
- Microsoft Intune
- Microsoft Azure AD Premium
- [Die Unternehmensportal-App für macOS](https://aka.ms/macoscompanyportal)
- macOS-Geräte mit OS X 10.12 Yosemite oder höher

**Netzwerk**:  
Jamf und Intune müssen auf die folgenden Ports und Endpunkte zugreifen können, um eine einwandfreie Integration zu gewährleisten:

- **Intune**: Port 443
- **Apple**: Ports 2195, 2196 und 5223 (Pushbenachrichtigungen an Intune)
- **Jamf**: Ports 80 und 5223

- Endpunkte:
  - login.microsoftonline.com
  - graph.windows.net  
  - *.manage.microsoft.com  

Damit APNS im Netzwerk ordnungsgemäß funktioniert, müssen Sie auch ausgehende Verbindungen und Umleitungen für folgende Ports aktivieren:

- Den Apple-Block 17.0.0.0/8 über die TCP-Ports 5223 und 443 aus allen Clientnetzwerken.
- Ports 2195 und 2196 von Jamf Pro-Servern.

Weitere Informationen zu diesen Ports finden Sie in den folgenden Artikeln:

- [Bandbreiten- und andere Anforderungen an die Netzwerkkonfiguration für Intune](../fundamentals/network-bandwidth-use.md)
- [Network Ports Used by Jamf Pro](https://www.jamf.com/jamf-nation/articles/34/network-ports-used-by-jamf-pro) (von Jamf Pro verwendete Netzwerkports) auf jamf.com
- [Von Apple-Softwareprodukten verwendete TCP- und UDP-Ports](https://support.apple.com/HT202944) auf support.apple.com

**Konten**:  
Die Verfahren in diesem Artikel erfordern die Verwendung von Konten mit den folgenden Berechtigungen:

- **Jamf Pro-Konsole**: Ein Konto mit Berechtigungen zum Verwalten von JAMF Pro
- **Microsoft Endpoint Management Admin Center**: Globaler Administrator
- **Azure-Portal**: Globaler Administrator

## <a name="remove-the-jamf-pro-integration-for-a-previously-configured-tenant"></a>Entfernen der Jamf Pro-Integration für einen zuvor konfigurierten Mandanten

Verwenden Sie das folgende Verfahren, um eine manuell konfigurierte Integration von Jamf Pro von Ihrem Azure-Mandanten zu entfernen, *bevor* Sie den Cloudconnector konfigurieren können.

Wenn Sie zuvor noch keine Verbindung zwischen Jamf Pro und Intune eingerichtet haben, oder wenn Sie eine oder mehrere Verbindungen besitzen, die bereits den Cloudconnector verwenden, überspringen Sie diesen Vorgang, und beginnen Sie mit dem [Konfigurieren des Cloudconnector für einen neuen Mandanten](#configure-the-cloud-connector-for-a-new-tenant).

### <a name="remove-a-manually-configured-jamf-pro-integration"></a>Entfernen einer manuell konfigurierten Jamf Pro-Integration

1. Melden Sie sich bei der Jamf Pro-Konsole an.

2. Wählen Sie **Einstellungen** (das Zahnradsymbol in der oberen rechten Ecke) aus, und wechseln Sie dann zu **Globale Verwaltung** > **Bedingter Zugriff**.

   ![Navigieren zum bedingten Zugriff](./media/conditional-access-jamf-cloud-connector/navigate-jamf-console-1.png)

3. Wählen Sie **Bearbeiten** aus.

4. Deaktivieren Sie das Kontrollkästchen **Enable Intune Integration for macOS** (Integration von Intune für macOS aktivieren).

   Wenn Sie diese Einstellung deaktivieren, deaktivieren Sie die Verbindung, speichern aber Ihre Konfiguration.

5. Melden Sie sich im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an, und wechseln Sie zu **Mandantenverwaltung** > **Partnergeräteverwaltung**.

   Löschen Sie auf dem Knoten **Partnergeräteverwaltung** die **Anwendungs-ID** im Feld **Die Azure Active Directory-App-ID für Jamf angeben** an, und wählen Sie dann **Speichern** aus.

   Die Anwendungs-ID ist die ID der Azure Enterprise-App, die in Azure erstellt wurde, als Sie eine manuelle Integration in Jamf Pro eingerichtet haben.

6. Melden Sie sich beim [Azure-Portal](https://portal.azure.com/) mit einem Konto an, das über Berechtigungen des globalen Administrators verfügt, und wechseln Sie zu **Azure Active Directory** > **Enterprise-Anwendungen**.

   Suchen Sie die beiden Jamf-Apps und löschen Sie sie. Neue Anwendungen werden automatisch erstellt, wenn Sie den Jamf-Cloudconnector im nächsten Verfahren konfigurieren.

   ![Wählen Sie die zu löschenden Jamf-Apps aus.](./media/conditional-access-jamf-cloud-connector/delete-jamf-apps.png)

   Nachdem Sie die Integration in Jamf Pro deaktiviert und die Unternehmensanwendungen gelöscht haben, zeigt der Knoten **Partnergeräteverwaltung** den Verbindungsstatus **Beendet** an.

   ![Verbindungsstatus „Beendet“](./media/conditional-access-jamf-cloud-connector/terminated-connection-status.png)

Nachdem Sie die manuelle Konfiguration für die Jamf Pro-Integration erfolgreich entfernt haben, können Sie jetzt die Integration mit dem Cloudconnector einrichten. Entsprechende Informationen finden Sie in diesem Artikel unter [Konfigurieren des Cloudconnectors für einen neuen Mandanten](#configure-the-cloud-connector-for-a-new-tenant).

## <a name="configure-the-cloud-connector-for-a-new-tenant"></a>Konfigurieren des Cloudconnectors für einen neuen Mandanten

Gehen Sie wie folgt vor, um den Jamf-Cloudconnector für die Integration von Jamf Pro und Microsoft Intune in den folgenden Situationen zu konfigurieren:

- Sie haben keine Integration zwischen Jamf Pro und Intune für Ihren Azure-Mandanten konfiguriert.
- Sie haben bereits einen Cloudconnector zwischen Jamf Pro und Intune in Ihrem Azure-Mandanten eingerichtet und möchten eine zusätzliche Jamf-Instanz in Ihr Abonnement integrieren.

Wenn Sie derzeit über eine manuell konfigurierte Integration zwischen Intune und Jamf Pro verfügen, finden Sie unter [Entfernen der Jamf Pro-Integration für einen zuvor konfigurierten Mandanten](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant) in diesem Artikel Informationen zum Entfernen dieser Integration, bevor Sie fortfahren. Das Entfernen einer manuell konfigurierten Integration ist erforderlich, bevor Sie den Jamf-Cloudconnector erfolgreich einrichten können.

### <a name="create-a-new-connection"></a>Erstellen einer neuen Verbindung

1. Melden Sie sich bei der Jamf Pro-Konsole an.

2. Wählen Sie **Einstellungen** (das Zahnradsymbol in der oberen rechten Ecke) aus, und wechseln Sie dann zu **Globale Verwaltung** > **Bedingter Zugriff**.

   ![Navigieren zum bedingten Zugriff](./media/conditional-access-jamf-cloud-connector/navigate-jamf-console-1.png)

3. Wählen Sie **Bearbeiten** aus.

4. Aktivieren Sie das Kontrollkästchen **Enable Intune Integration for macOS** (Integration von Intune für macOS aktivieren).
   - Wählen Sie diese Einstellung aus, damit Jamf Pro Inventaraktualisierungen an Microsoft Intune sendet.
   - Sie können diese Einstellung abwählen, um die Verbindung zu deaktivieren, aber speichern Sie Ihre Konfiguration.

   > [!IMPORTANT]
   > Wenn **Intune-Integration für macOS aktivieren** bereits ausgewählt und der *Verbindungstyp* auf **Manuell** festgelegt ist, müssen Sie diese Integration entfernen, bevor Sie fortfahren können. Bevor Sie fortfahren, sind weitere Informationen in diesem Artikel unter [Entfernen der Jamf Pro-Integration für einen zuvor konfigurierten Mandanten](#remove-the-jamf-pro-integration-for-a-previously-configured-tenant) verfügbar.

5. Wählen Sie unter *Verbindungstyp* die Option **Cloudconnector** aus.

   ![Auswählen des Cloudconnectors in der Jamf Pro-Konsole](./media/conditional-access-jamf-cloud-connector/select-cloud-connector.png)

6. Wählen Sie aus dem Popupmenü **Sovereign Cloud** den Standort Ihrer Sovereign Cloud von Microsoft aus.

7. Wählen Sie eine der folgenden Landing Page-Optionen für Computer aus, die von Microsoft Azure nicht erkannt werden:
   - **Seite „Jamf Pro-Standardgeräteregistrierung“** : Abhängig vom Status des macOS-Geräts leitet diese Option Benutzer entweder zum Jamf Pro-Geräteregistrierungsportal (zur Registrierung bei Jamf Pro) oder zur Intune-Unternehmensportal-App (zur Registrierung bei Azure AD) um.
   - **Seite „Zugriff verweigert“**
   - **Benutzerdefinierte URL**

8. Wählen Sie **Verbinden** aus. Sie werden zur Registrierung der Jamf Pro-Anwendungen zu Azure umgeleitet.

   Wenn Sie dazu aufgefordert werden, geben Sie Ihre Microsoft Azure-Anmeldeinformationen an, und folgen Sie den Anweisungen auf dem Bildschirm, um die angeforderten Berechtigungen zu erteilen. Sie erteilen Berechtigungen für den **Cloudconnector** und dann wieder für die **Cloudconnector-App für die Benutzerregistrierung**. Beide Apps sind in Azure als Unternehmensanwendungen registriert.

   Nachdem die Berechtigungen für beide Apps erteilt wurden, wird die Seite **Anwendungs-ID** geöffnet.

9. Wählen Sie auf der Seite **Anwendungs-ID** die Option **Intune kopieren und öffnen** aus.

   ![Anwendungs-ID](./media/conditional-access-jamf-cloud-connector/copy-application-id.png)

   Die *Anwendungs-ID* wird zur Verwendung im nächsten Schritt in die Zwischenablage Ihres Systems kopiert, und der Knoten **Partnergeräteverwaltung** im *Microsoft Endpoint Manager Admin Center* wird geöffnet. (**Mandantenverwaltung** > **Partnergeräteverwaltung**).

10. Auf dem Knoten **Partnergeräteverwaltung** *fügen* Sie die **Anwendungs-ID** in das Feld **Azure Active Directory-App-ID für Jamf angeben** ein, und wählen Sie dann **Speichern** aus.

    ![Konfigurieren der Partnergeräteverwaltung](./media/conditional-access-jamf-cloud-connector/partner-device-management.png)

11. Kehren Sie zur Seite „Anwendungs-ID“ in Jamf Pro zurück, und wählen Sie **Bestätigen** aus.

12. Jamf Pro schließt die Konfiguration ab, testet sie und zeigt einen Erfolg oder Fehler der Verbindung auf der Seite mit den Einstellungen für den bedingten Zugriff an. Die folgende Abbildung ist ein Beispiel für einen Erfolg:

    ![In Jamf Pro bestätigte erfolgreiche Konfiguration](./media/conditional-access-jamf-cloud-connector/successful-configuration.png)

13. Aktualisieren Sie im Microsoft Endpoint Manager Admin Center den Knoten **Partnergeräteverwaltung**. Die Verbindung sollte jetzt als **Aktiv** angezeigt werden:

    ![Verbindungsstatus ist „Aktiv“](./media/conditional-access-jamf-cloud-connector/active-connection-status.png)

Wenn die Verbindung zwischen Jamf Pro und Microsoft Intune erfolgreich hergestellt ist, sendet Jamf Pro Inventarinformationen an Microsoft Intune für jeden Computer, der bei Azure AD registriert ist (die Registrierung bei Azure AD ist ein Endbenutzerworkflow). In Jamf Pro können Sie in der Kategorie „Lokales Benutzerkonto“ der Inventarinformationen eines Computers in Jamf Pro den Inventarstatus für den bedingten Zugriff für einen Benutzer und einen Computer anzeigen.

Nachdem Sie eine Instanz von Jamf Pro mithilfe des Jamf-Cloudconnectors integriert haben, können Sie dasselbe Verfahren verwenden, um weitere Instanzen von Jamf Pro mit demselben Intune-Abonnement in Ihrem Azure-Mandanten zu konfigurieren.  

## <a name="set-up-compliance-policies-and-register-devices"></a>Einrichten von Konformitätsrichtlinien und Registrieren von Geräten

Nach dem Konfigurieren der Integration zwischen Intune und Jamf verwenden Sie die Option [Anwenden von Konformitätsrichtlinien auf mit Jamf verwaltete Geräte](../protect/conditional-access-assign-jamf.md).

## <a name="disconnect-jamf-pro-and-intune"></a>Trennen von Jamf Pro und Intune

Wenn Sie die Integration von Jamf Pro in Intune entfernen müssen, führen Sie die folgenden Schritte aus, um die Verbindung innerhalb der Jamf Pro-Konsole zu entfernen. Diese Informationen gelten sowohl für den Cloudconnector als auch für die manuell konfigurierte Integration.

1. Navigieren Sie in Jamf Pro zu **Global Management** > **Conditional Access** (Globale Verwaltung > Bedingter Zugriff). Klicken Sie auf der Registerkarte **macOS Intune Integration** (Intune-Integration in macOS) auf **Edit** (Bearbeiten).

2. Deaktivieren Sie das Kontrollkästchen **Enable Intune Integration for macOS** (Integration von Intune für macOS aktivieren).

3. Wählen Sie **Speichern** aus. Jamf Pro sendet Ihre Konfiguration an Intune, und die Integration wird beendet.

4. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

5. Wählen Sie **Mandantenverwaltung** > **Connectors and tokens** > **Partnergeräteverwaltung** (Mandantenverwaltung > Connectors und Token > Partnergeräteverwaltung) aus, um zu bestätigen, dass der Status jetzt **Beendet** ist.

   > [!NOTE]
   > Die Mac-Geräte Ihrer Organisation werden an dem Datum (3 Monate) entfernt, das in der Konsole angezeigt wird.

## <a name="get-support-for-the-cloud-connector"></a>Erhalten von Support für den Cloudconnector

Da der Cloudconnector automatisch die für die Integration erforderlichen Azure Enterprise-Apps erstellt, sollte Ihr erster Ansprechpartner hinsichtlich des Supports **Jamf** sein. Zu den Optionen gehören:

- E-Mail-Support unter `support@jamf.com`
- Verwenden des Support-Portals von Jamf Nation: https://www.jamf.com/support/ 


Vor der Kontaktaufnahme mit dem Support:

- Überprüfen Sie die Voraussetzungen wie Ports und Produktversion, die Sie verwenden.
- Bestätigen Sie, dass die Berechtigungen für die folgenden zwei in Azure erstellten Jamf Pro-Apps nicht geändert wurden. Änderungen an den App-Berechtigungen werden von Intune nicht unterstützt und können dazu führen, dass bei der Integration Fehler auftreten.

  **Cloudconnector-App für die Benutzerregistrierung**:
  - API-Name: Microsoft Graph
    - Berechtigung: Anmelden und das Benutzerprofil lesen
    - Type: Delegiert
    - Gewährt über: Zustimmung des Administrators
    - Gewährt von: Administrator

  **Cloudconnector-App**:
  - API-Name: Microsoft Graph (Instanz 1)
    - Berechtigung: Anmelden und das Benutzerprofil lesen
    - Type: Delegiert
    - Gewährt über: Zustimmung des Administrators
    - Gewährt von: Administrator

  - API-Name: Microsoft Graph (Instanz 2)
    - Berechtigung: Lesen der Verzeichnisdaten
    - Type: Anwendung
    - Gewährt über: Zustimmung des Administrators
    - Gewährt von: Administrator

  - API-Name: Intune-API
    - Berechtigung: Geräteattribut an Microsoft Intune senden
    - Type: Anwendung
    - Gewährt über: Zustimmung des Administrators
    - Gewährt von: Administrator

## <a name="common-questions-about-the-jamf-cloud-connector"></a>Häufige Fragen zum Jamf-Cloudconnector

### <a name="what-data-is-shared-via-the-cloud-connector"></a>Welche Daten werden über den Cloudconnector freigegeben?

Der Cloudconnector authentifiziert sich bei Microsoft Azure und sendet Geräteinventardaten von Jamf Pro an Azure. Darüber hinaus verwaltet der Cloudconnector die Diensterkennung in Azure, den Tokenaustausch, Kommunikationsfehler und die Notfallwiederherstellung.

### <a name="where-is-device-inventory-data-stored"></a>Wo werden Geräteinventardaten gespeichert?

Geräteinventardaten werden in der Jamf Pro-Datenbank gespeichert.

### <a name="what-credentials-are-stored"></a>Welche Anmeldeinformationen werden gespeichert?

Es werden keine Anmeldeinformationen gespeichert. Bei der Konfiguration des Cloudconnectors müssen die Administratoren dem Hinzufügen der mehrinstanzenfähigen Jamf-App und der nativen macOS-Connector-App zu ihrem Azure AD-Mandanten zustimmen. Sobald die mehrinstanzenfähige Anwendung hinzugefügt ist, fordert der Cloudconnector Zugriffstoken an, um mit der Azure-API zu interagieren. Der Zugriff auf die Anwendung kann in Microsoft Azure jederzeit widerrufen werden, um den Zugriff einzuschränken.

### <a name="how-is-data-encrypted"></a>Wie werden Daten verschlüsselt?

Der Cloudconnector verwendet TLS (Transport Layer Security) für Daten, die zwischen Jamf Pro und Microsoft Azure gesendet werden.

### <a name="how-does-jamf-know-which-device-is-associated-with-which-instance-of-jamf-pro"></a>Woher weiß Jamf, welches Gerät zu welcher Instanz von Jamf Pro zugeordnet ist?

Jamf Pro verwendet Microservices in AWS, um die Geräteinformationen ordnungsgemäß an die richtige Instanz weiterzuleiten.

### <a name="can-i-switch-from-using-the-cloud-connector-to-the-manual-connection-type"></a>Kann ich von der Verwendung des Cloudconnectors zum Verbindungstyp „Manuell“ wechseln?

Ja. Sie können den Verbindungstyp wieder in „Manuell“ ändern und die Schritte für das manuelle Setup befolgen. Wenn Sie Fragen haben, sollten Sie diese an Jamf richten, um Unterstützung zu erhalten.

### <a name="permissions-were-modified-on-one-or-both-required-apps-cloud-connector-and-cloud-connector-user-registration-app-and-registration-is-not-working-is-this-supported"></a>Die Berechtigungen wurden für eine oder beide erforderlichen Apps (*Cloudconnector* und *Cloudconnector-App für die Benutzerregistrierung*) geändert und die Registrierung funktioniert nicht, wird dies unterstützt?

Das Ändern der Berechtigungen für die Apps wird nicht unterstützt.

## <a name="next-steps"></a>Nächste Schritte

- [Anwenden von Konformitätsrichtlinien auf mit Jamf verwaltete Geräte](../protect/conditional-access-assign-jamf.md)
- [Von Jamf Pro an Intune gesendete Daten](../protect/data-jamf-sends-to-intune.md)
