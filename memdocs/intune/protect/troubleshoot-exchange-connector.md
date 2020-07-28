---
title: Exchange Connector-Problembehandlung
titleSuffix: Microsoft Intune
description: Erfahren Sie, wie Sie Problemen mit dem lokalen Intune Exchange Connector behandeln.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: a7e3c742-295b-40bb-9afa-17f243062500
ms.reviewer: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3e7f9c984b81bbe98269b0123371d8097d960ffb
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2020
ms.locfileid: "86462132"
---
# <a name="troubleshoot-the-intune-exchange-connector"></a>Problembehandlung für den Intune Exchange Connector

In diesem Artikel wird beschrieben, wie Sie Probleme im Intune Exchange Connector behandeln.

> [!IMPORTANT]
>
> Ab Juli 2020 wird die Unterstützung für den Exchange Connector eingestellt. Der Connector wird durch die [hybride moderne Authentifizierung](https://docs.microsoft.com/office365/enterprise/hybrid-modern-auth-overview) (HMA) für Exchange abgelöst. Dementsprechend wird es nicht mehr möglich sein, Intune einen Exchange Connector hinzuzufügen.
>
> Falls Kunden den Exchange Connector bereits konfiguriert haben und diesen verwenden, erhalten diese weiterhin Unterstützung für den Connector.


## <a name="before-you-start"></a>Vorbereitung

Bevor Sie ein Problem mit einem Exchange-Connector in Intune beheben, erfassen Sie einige grundlegende Informationen, damit Sie über eine solide Arbeitsgrundlage verfügen. Diese Vorgehensweise kann dazu beitragen, die Art des Problems besser zu verstehen und schneller eine Lösung zu finden.

- Vergewissern Sie sich, dass Ihr Vorgehensweise die Installationsanforderungen erfüllt. Informationen finden Sie unter [Einrichten des lokalen Intune Exchange-Connectors](exchange-connector-install.md).
- Stellen Sie sicher, dass Ihr Konto sowohl über Exchange- als auch über Intune-Administratorberechtigungen verfügt.
- Notieren Sie sich den vollständigen und exakten Text der Fehlermeldung sowie die Details und die Stelle, an der die Meldung angezeigt wurde.
- Bestimmen Sie, wann das Problem begann: 
  - Richten Sie den Connector zum ersten Mal ein? 
  - Funktionierte der Connector zunächst ordnungsgemäß und schlug dann fehl?
  - Wenn er zuvor funktioniert hat, welche Änderungen wurden in der Intune-Umgebung, der Exchange-Umgebung oder auf dem Computer vorgenommen, auf dem die Connectorsoftware ausgeführt wird?
- Welche MDM-Autorität wird verwendet?
- Welche Version von Exchange verwenden Sie?

### <a name="use-powershell-to-get-more-data-on-exchange-connector-issues"></a>Verwenden Sie PowerShell, um weitere Daten zu Exchange Connector-Problemen zu erhalten.

- Zum Abrufen einer Liste aller mobilen Geräte für ein Postfach verwenden Sie `Get-ActiveSyncDeviceStatistics -mailbox mbx`.
- Zum Abrufen einer Liste aller SMTP-Adressen für ein Postfach verwenden Sie `Get-Mailbox -Identity user | select emailaddresses | fl`.
- Verwenden Sie `Get-CASMailbox <upn> | fl`, um ausführliche Informationen zum Zugriffsstatus eines Geräts abzurufen.

## <a name="review-the-connector-configuration"></a>Überprüfen der Connectorkonfiguration

Überprüfen Sie die [Anforderungen des lokalen Exchange-Connectors](exchange-connector-install.md#intune-exchange-connector-requirements), um sicherzustellen, dass Ihre Umgebung und der Connector ordnungsgemäß konfiguriert sind. 

### <a name="general-considerations-for-the-connector"></a>Allgemeine Überlegungen zum Connector

- Stellen Sie sicher, dass Ihre Firewall und Ihre Proxyserver die Kommunikation zwischen dem Server, der den Intune Exchange Connector hostet, und dem Intune-Dienst zulassen.

- Der Computer, der den Intune Exchange Connector und den Exchange-Clientzugriffsserver (Client Access Server, CAS) hostet, sollte in die Domäne eingebunden sein und sich im selben LAN befinden. Vergewissern Sie sich, dass dem Konto, das vom Intune Exchange Connector verwendet wird, die erforderlichen Berechtigungen hinzugefügt wurden.

- Das Benachrichtigungskonto wird zum Abrufen der Einstellungen *AutoErmittlung* verwendet. Weitere Informationen zur AutoErmittlung in Exchange finden Sie unter [AutoErmittlungsdienst in Exchange Server](https://docs.microsoft.com/exchange/architecture/client-access/autodiscover?view=exchserver-2016).

- Der Intune Exchange Connector sendet eine Anforderung an die EWS-URL und verwendet dabei die Anmeldeinformationen des Benachrichtigungskontos, um E-Mail-Benachrichtigungen zusammen mit dem Link *Erste Schritte* (für die Intune-Registrierung) zu versenden. Die Registrierung über den Link *Erste Schritte* ist eine Voraussetzung für Android-Geräte, die nicht mit der KNOX-Plattform verwendet werden. Andernfalls werden diese Geräte durch das Feature „Bedingter Zugriff“ gesperrt.

### <a name="common-issues-for-connector-configurations"></a>Häufige Probleme bei Connectorkonfigurationen

- **Kontoberechtigungen**: Stellen Sie im Dialogfeld „Microsoft Intune Exchange Connector“ sicher, dass Sie ein Benutzerkonto angegeben haben, das die richtigen Berechtigungen besitzt, um die erforderlichen [Windows PowerShell-Exchange-Cmdlets](exchange-connector-install.md#exchange-cmdlet-requirements) auszuführen.
- **E-Mail-Benachrichtigungen:** Aktivieren Sie Benachrichtigungen, und geben Sie ein Benachrichtigungskonto an.
- **Synchronisierung mit dem Clientzugriffsserver:** Geben Sie bei der Exchange Connector-Konfiguration einen CAS an, der die geringst mögliche Netzwerklatenz zu dem Server ausweist, der den Exchange Connector hostet. Die Latenz bei der Kommunikation zwischen dem Clientzugriffsserver und dem Exchange Connector kann zu Verzögerungen bei der Geräteerkennung führen, insbesondere bei der dedizierten Verwendung von Exchange Online.
- **Synchronisierungszeitplan**: Bei einem Benutzer mit einem neu registrierten Gerät kann es beim Zugriff zu Verzögerungen kommen, bis der Exchange Connector mit dem Exchange-Clientzugriffsserver synchronisiert wurde. Eine vollständige Synchronisierung erfolgt einmal täglich, während eine schnelle Synchronisierung (Delta) mehrmals täglich durchgeführt wird. Sie können eine [schnelle oder vollständige Synchronisierung manuell erzwingen](exchange-connector-install.md#manually-force-a-quick-sync-or-full-sync), um Verzögerungen zu minimieren.

## <a name="next-steps"></a>Nächste Schritte
Die folgenden Artikel können helfen, häufig auftretende Probleme und bestimmte Fehler zu beheben:

- [Beheben häufig mit dem Intune Exchange Connector auftretender Probleme](troubleshoot-exchange-connector-common-problems.md)
- [Beheben häufig mit dem Intune Exchange Connector auftretender Fehler](troubleshoot-exchange-connector-common-errors.md)

Bei Fragen können Sie sich an den Support oder an die Intune-Community wenden:

- Navigieren Sie zu [Support anfordern](../fundamentals/get-support.md), um das Problem mithilfe der Intune-Konsole zu beheben oder eine Supportanfrage bei Microsoft zu stellen. 
- Posten Sie Ihr Problem in den [Microsoft Intune-Foren](https://social.technet.microsoft.com/Forums/en-US/home?forum=microsoftintuneprod).  
