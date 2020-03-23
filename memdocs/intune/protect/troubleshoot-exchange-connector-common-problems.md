---
title: Behandlung häufig auftretender Probleme in Bezug auf den Intune Exchange Connector
titleSuffix: Microsoft Intune
description: Behandeln und lösen Sie häufig auftretende Probleme in Bezug auf den lokalen Microsoft Intune Exchange Connector.
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/26/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: ''
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 55f51f94cf26aa2486ef390d5fbb668eaf013e10
ms.sourcegitcommit: 3d895be2844bda2177c2c85dc2f09612a1be5490
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79350628"
---
# <a name="resolve-common-problems-with-the-intune-exchange-connector"></a>Lösen häufig auftretender Probleme mit dem Intune Exchange Connector
 
Dieser Artikel kann Intune-Administratoren dabei helfen, häufig auftretende Probleme beim Ausführen des Intune Exchange Connectors zu lösen.

Bevor Sie mit der Problembehandlung beginnen, lesen Sie [Problembehandlung für den Intune Exchange Connector](troubleshoot-exchange-connector.md), um grundlegende Informationen zum Connector zu erhalten. Lesen Sie außerdem Informationen zu häufig auftretenden Problemen in Bezug auf die Konfiguration des Connectors.

## <a name="an-exchange-activesync-device-isnt-discovered-from-exchange"></a>Ein Exchange ActiveSync-Gerät wurde von Exchange nicht ermittelt.

Wenn ein Exchange ActiveSync-Gerät von Exchange nicht erkannt wird, [überwachen Sie die Aktivitäten des Exchange Connectors](exchange-connector-install.md#on-premises-intune-exchange-connector-high-availability-support), um festzustellen, ob der Exchange Connector mit dem Exchange-Server synchronisiert wird. Wenn seit dem Hinzufügen des Geräts keine Synchronisierung stattgefunden hat, sammeln Sie die Synchronisierungsprotokolle, und fügen Sie sie an eine Supportanfrage an. Wenn seit dem Hinzufügen des Geräts eine vollständige Synchronisierung oder Schnellsynchronisierung erfolgreich durchgeführt wurde, überprüfen Sie, ob eines der folgenden Probleme vorliegt:

- Stellen Sie sicher, dass die Benutzer über eine Intune-Lizenz verfügen. Ansonsten erkennt der Exchange Connector ihre Geräte nicht.

- Wenn die primäre SMTP-Adresse eines Benutzers sich von seinem Benutzerprinzipalnamen (UPN) in Azure Active Directory (Azure AD) unterscheidet, erkennt der Exchange Connector keine Geräte für diesen Benutzer. Korrigieren Sie die primäre SMTP-Adresse, um das Problem zu beheben.

- Wenn in Ihrer Umgebung Exchange 2010- und Exchange 2013-Postfachserver vorhanden sind, wird empfohlen, den Exchange Connector auf einen Exchange 2013-Clientzugriffsserver (CAS) zu verweisen. Wenn der Exchange Connector für die Kommunikation mit einem Exchange 2010-Clientzugriffsserver eingerichtet ist, erkennt dieser keine Exchange 2013-Geräte von Benutzern.

- Für Exchange Online Dedicated-Umgebungen müssen Sie den Exchange Connector während des anfänglichen Setups an einen Exchange 2013-Clientzugriffsserver (nicht an einen Exchange 2010-Clientzugriffsserver) in der dedizierten Umgebung verweisen. Der Connector kommuniziert nur beim Ausführen von PowerShell-Cmdlets mit einem Exchange 2013-Clientzugriffsserver.

## <a name="problems-with-the-notification-email-message"></a>Probleme mit der Benachrichtigungs-E-Mail

Stellen Sie sicher, dass die Registrierung in Intune über die vom Intune Exchange Connector gesendete „Get Started Now“-E-Mail (Jetzt starten) erfolgt, um bedingten Zugriff für lokale Postfächer auf Geräten, auf denen kein Android Knox ausgeführt wird, zu unterstützen. Durch das Starten der Registrierung über die E-Mail wird sichergestellt, dass das Gerät eine eindeutige ActiveSyncID für alle Plattformen erhält (Exchange, Azure AD, Intune).

Ein Benutzer erhält aus den folgenden Gründen möglicherweise keine Benachrichtigungs-E-Mail:

- Das Benachrichtigungskonto wurde falsch eingerichtet.
- Bei der AutoErmittlung für das Benachrichtigungskonto ist ein Fehler aufgetreten.
- Die Exchange-Webdienste-Anforderung (EWS, Exchange Web Services) für das Senden der E-Mail ist fehlgeschlagen.

Lesen Sie die folgenden Abschnitte, um Probleme in Bezug auf die E-Mail-Benachrichtigung zu behandeln.

### <a name="check-the-notification-account-that-retrieves-autodiscover-settings"></a>Überprüfen Sie das Benachrichtigungskonto, das die Einstellungen für den AutoErmittlungsdienst abruft.

1. Stellen Sie sicher, dass der AutoErmittlungsdienst und die Exchange-Webdienste in den Exchange-Clientzugriffsdiensten konfiguriert sind. Weitere Informationen finden Sie unter [Clientzugriffsdienste](https://docs.microsoft.com/Exchange/architecture/client-access/client-access) und [AutoErmittlungsdienst in Exchange Server](https://docs.microsoft.com/Exchange/architecture/client-access/autodiscover?view=exchserver-2019).

2. Vergewissern Sie sich, dass Ihr Benachrichtigungskonto die folgenden Anforderungen erfüllt:

   - Das Konto verfügt über ein aktives Postfach, das von Ihrem lokalen Exchange-Server gehostet wird.

   - Der UPN des Kontos stimmt mit der SMTP-Adresse überein.

3. Die AutoErmittlung erfordert einen DNS-Server mit einem DNS-Eintrag für **Autodiscover.SMTP-Domäne.com** (z. B. Autodiscover.contoso.com), der auf Ihren Exchange-Clientzugriffsserver verweist. Geben Sie Ihren FQDN anstelle von *Autodiscover.SMTP-Domäne.com* an, und führen Sie die folgenden Schritte aus, um nach dem Eintrag zu suchen:

   1. Geben Sie in eine Eingabeaufforderung *NSLOOKUP* ein.

   2. Geben Sie *Autodiscover.SMTP-Domäne.com* ein. Die Ausgabe sollte ähnlich wie im folgenden Bild aussehen: ![NSLOOKUP-Ergebnisse](./media/troubleshoot-exchange-connector-common-problems/nslookup-results.png
      )

   Sie können den AutoErmittlungsdienst auch im Internet unter https://testconnectivity.microsoft.com testen. Alternativ können Sie ihn mit dem Microsoft-Verbindungsuntersuchungstool von einer lokalen Domäne aus testen. Weitere Informationen finden Sie unter [Microsoft-Verbindungsuntersuchung](https://docs.microsoft.com/previous-versions/office/exchange-remote-connectivity/jj851141(v=exchg.80)).


### <a name="check-autodiscovery"></a>AutoErmittlung überprüfen

Führen Sie die folgenden Schritte aus, wenn bei der AutoErmittlung ein Fehler auftritt:

1. [Konfigurieren Sie einen gültigen DNS-Eintrag für die AutoErmittlung](https://docs.microsoft.com/previous-versions/exchange-server/exchange-150/mt473798(v=exchg.150)).

2. Geben Sie die EWS-URL als vordefinierten Code in die Konfigurationsdatei für den Intune Exchange Connector ein:

   1. Ermitteln Sie die EWS-URL. Die standardmäßige EWS-URL für Exchange ist `https://<mailServerFQDN>/ews/exchange.asmx`. Ihre URL kann jedoch eine andere sein. Wenden Sie sich an den Exchange-Administrator, um die richtige URL für Ihre Umgebung herauszufinden.

   2. Bearbeiten Sie die Datei *OnPremisesExchangeConnectorServiceConfiguration.xml*. Standardmäßig befindet sich diese Datei im Ordner *%ProgramData%\Microsoft\Windows Intune Exchange Connector* auf dem Computer, auf dem der Exchange Connector ausgeführt wird. Öffnen Sie die Datei in einem Text-Editor, und ändern Sie die folgende Zeile so, dass dort die EWS-URL für Ihre Umgebung steht: `<ExchangeWebServiceURL>https://<YourExchangeHOST>/EWS/Exchange.asmx</ExchangeWebServiceURL>`.

3. Speichern Sie die Datei, und starten Sie dann den Microsoft Intune Exchange Connector neu.

>[!NOTE]
> Mit dieser Konfiguration verwendet der Intune Exchange Connector nicht mehr die AutoErmittlung, sondern stellt direkt eine Verbindung zur EWS-URL her.

## <a name="next-steps"></a>Nächste Schritte

Hilfestellungen zu bestimmten Fehlern finden Sie unter [Beheben häufig auftretender Fehler in Bezug auf den Intune Exchange Connector](troubleshoot-exchange-connector-common-errors.md).

Gehen Sie wie folgt vor, um Support anzufordern oder Hilfe von der Intune-Community zu erhalten:

- Navigieren Sie zu [Support anfordern](../fundamentals/get-support.md), um das Problem mithilfe der Intune-Konsole zu beheben oder eine Supportanfrage bei Microsoft zu stellen.
- Posten Sie Ihr Problem in den [Microsoft Intune-Foren](https://social.technet.microsoft.com/Forums/home?forum=microsoftintuneprod).