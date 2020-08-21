---
title: Installieren des Exchange Connectors
titleSuffix: Configuration Manager
description: Installieren und konfigurieren Sie den Exchange Connector für Configuration Manager zum Verwalten mobiler Geräte über ActiveSync.
ms.date: 12/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: e179e30a-a1fc-461e-8087-ff3a55803450
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e0db550369ca2d81f42a25e68960b5f8f27be168
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88700479"
---
# <a name="install-and-configure-the-exchange-connector"></a>Installieren und Konfigurieren von Exchange Connector

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie dieses Verfahren, um einen Exchange Server-Connector zum Verwalten mobiler Geräte zu installieren und zu konfigurieren. Von Configuration Manager wird nur jeweils ein Connector in einer Exchange-Organisation unterstützt.

Vergewissern Sie sich vor der Installation des Exchange Server-Connector für Configuration Manager, dass Sie über die erforderlichen Berechtigungen und Versionen verfügen. Weitere Informationen finden Sie unter [Geräteverwaltung mit Exchange und Configuration Manager](manage-mobile-devices-with-exchange-activesync.md#prerequisites).

## <a name="exchange-connection-account"></a>Exchange-Verbindungs Konto

Entscheiden Sie, mit welchem Konto eine Verbindung mit dem Exchange-Clientzugriffsserver hergestellt wird, um die mobilen Geräte zu verwalten. Dabei kann es sich um das Computerkonto des Standortservers oder um ein Windows-Benutzerkonto handeln.

Konfigurieren Sie dieses Konto anschließend in einer Exchange-Rollen Gruppe, um die folgenden Exchange Server-Cmdlets auszuführen:

- **Clear-ActiveSyncDevice**  

- **Get-ActiveSyncDevice**  

- **Get-ActiveSyncDeviceAccessRule**  

- **Get-ActiveSyncDeviceStatistics**  

- **Get-ActiveSyncMailboxPolicy**  

- **Get-ActiveSyncOrganizationSettings**  

- **Get-ExchangeServer**  

- **Get-Mailbox**

- **Get-Recipient**  

- **Set-ADServerSettings**  

- **Set-ActiveSyncDeviceAccessRule**  

- **Set-ActiveSyncMailboxPolicy**  

- **Set-CASMailbox**  

- **New-ActiveSyncDeviceAccessRule**  

- **New-ActiveSyncMailboxPolicy**  

- **Remove-ActiveSyncDevice**  

- **Get-CasMailbox**  

- **"Get-User"**  

- **Set-ActiveSyncOrganizationSettings**  

Diese Cmdlets sind in folgenden Exchange Server-Verwaltungsrollen enthalten:

- Empfänger Verwaltung
- Organisationsverwaltung nur anzeigen
- Server Management

Weitere Informationen finden Sie Untergrund Legendes zu [Verwaltungs Rollen Gruppen](/exchange/understanding-management-role-groups-exchange-2013-help) in der Dokumentation zu Exchange Server 2013.

> [!TIP]  
> Wenn Sie versuchen, den Exchange Server-Connector ohne die erforderlichen Cmdlets zu installieren oder zu verwenden, wird in der Datei "easdisc. log" auf dem Standort Server Computer der folgende Fehler angezeigt: `Invoking cmdlet <cmdlet> failed` .

## <a name="install-the-connector"></a>Installieren des Connectors

1. Wechseln Sie in der Configuration Manager Konsole zum Arbeitsbereich **Verwaltung** , erweitern Sie **Hierarchie Konfiguration**, und wählen Sie dann **Exchange Server-Connectors**aus.

1. Wählen Sie auf der Registerkarte **Startseite** des Menübands in der Gruppe **Erstellen** die Option **Exchange-Server hinzufügen**aus.

1. Wählen Sie auf der Seite **Allgemein** des Assistenten zum Hinzufügen von Exchange Server eine der Exchange Server-Umgebungen aus:

    - Lokaler **Exchange-Server**: Geben Sie für jede Active Directory Site einen einzelnen Server oder ein Client Zugriffs Server-Array an.

        Wenn der Server oder das Array offline sind, wird von Configuration Manager versucht, einen Clientzugriffsserver für die Verwendung zu ermitteln. Gelingt dies nicht, dann wird von Configuration Manager nachfolgend ein Postfachserver zur Herstellung einer Verbindung mit einem Clientzugriffsserver verwendet. Wenn der Verbindungsversuch wiederholt wird, werden die folgenden Warnungen in der Datei "easdisc. log" auf dem Standort Server Computer protokolliert: `Failed to open runspace for site <site_name>` .

    - **Gehosteter Exchange-Server**: Geben Sie die Server Adresse Ihrer Exchange Online-Umgebung an.

    Wählen Sie dann den primären Standort aus, an dem der Exchange Server-Connector ausgeführt wird.

1. Geben Sie auf der Seite **Konto** das Konto für die Verbindung mit dem Exchange-Server an. Weitere Informationen finden Sie unter [Exchange-Verbindungs Konto](#exchange-connection-account).

1. Konfigurieren Sie auf **der Seite Ermittlung den** Synchronisierungs Zeitplan und die Regeln für die Suche nach Geräten.

1. Konfigurieren Sie auf der Seite **Einstellungen** die Einstellungen für mobile Geräte in den folgenden Gruppen:

    - **Allgemein**
    - **Kennwort**
    - **E-Mail Verwaltung**
    - **Security**
    - **Anwendung**

    Weitere Informationen finden Sie unter [Exchange Connector-Einstellungen](manage-mobile-devices-with-exchange-activesync.md#policies).

    Wenn Sie mobile Geräte auch mithilfe von Configuration Manager lokalen [MDM](../understand/manage-mobile-devices-with-on-premises-infrastructure.md)anmelden, aktivieren Sie die Option **externe Verwaltung mobiler Geräte zulassen**. Diese Einstellung ermöglicht es diesen mobilen Geräten, nach der Configuration Manager Registrierung weiterhin e-Mails von Exchange zu empfangen.

1. Schließen Sie den Assistenten ab.

## <a name="verify-and-monitor"></a>Überprüfen und überwachen

Überprüfen Sie die Installation des Exchange Server-Verbindungs Servers mit Statusmeldungen und Protokolldateien:

- Vergewissern Sie sich, dass der Exchange Server-Connector Standortkomponenten-Manager erfolgreich installiert wurde. Suchen Sie in der **SMS_EXCHANGE_CONNECTOR** Komponente nach der Nachrichten Status-ID **1015** .

    Bei der Installation kann ein Fehler auftreten, wenn der angegebene Client Zugriffs Server offline ist. Wenn Configuration Manager den Connector nicht erfolgreich installieren kann, versucht Configuration Manager, die Installation alle 60 Minuten zu wiederholen. Der Vorgang wird so lange wiederholt, bis die Installation erfolgreich war, oder Sie entfernen den Exchange Server-Connector.

- Überprüfen Sie auf dem Standort Server Computer die **Datei sitecomp. log** auf den folgenden Eintrag: `Component SMS_EXCHANGE_CONNECTOR flagged for installation` . Anschließend wird die erfolgreiche Installation mit folgendem Text protokolliert: `STATMSG: ID=1015` .

Überwachen Sie nach Abschluss der Installation die mobilen Geräte, die vom Connector gefunden und verwaltet werden. Anzeigen der Sammlungen mobiler Geräte und Verwenden der Berichte für mobile Geräte.

> [!NOTE]  
> Configuration Manager generiert Namen für die gefundenen mobilen Geräte. Dabei wird das Format *Benutzername*_*Gerätetyp*verwendet. Beispielsweise **jdoe_WindowsPhone**. Wenn ein Benutzer über mehrere mobile Geräte mit dem gleichen Gerätetyp verfügt, wird in der Configuration Manager-Konsole und in Berichten der gleiche Name für diese mobilen Geräte angezeigt.  

## <a name="see-also"></a>Weitere Informationen

- [Von Konfigurations Clients und Standort Systemen verwendete Ports](../../core/plan-design/hierarchy/ports.md#BKMK_PortsExchangeConnectorHosted)
- [Proxyserverunterstützung](../../core/plan-design/network/proxy-server-support.md#site-system-roles-that-use-a-proxy)
- [Sicherheitsempfehlungen für mobile Geräte](../../core/clients/deploy/plan/security-and-privacy-for-clients.md#bkmk_mobile)
- [Informationen zum Datenschutz für mobile Geräte, die mit dem Exchange Server-Connector verwaltet werden](../../core/clients/deploy/plan/security-and-privacy-for-clients.md#BKMK_Privacy_ExchangeConnector)