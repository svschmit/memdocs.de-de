---
title: Szenarien für bedingten Zugriff
titleSuffix: Microsoft Intune
description: Erfahren Sie, wie der bedingte Zugriff von Intune im Allgemeinen für den gerätebasierten und den App-basierten bedingten Zugriff verwendet wird.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: a0b8e55e-c3d8-4599-be25-dc10c1027b62
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure; get-started; seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: 6d062af4859dcca6c762bf401e1007a9fc9af126
ms.sourcegitcommit: fdd6d3c4b906e895ebec2856ebc38b0656296d2c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/22/2020
ms.locfileid: "91002663"
---
# <a name="what-are-common-ways-to-use-conditional-access-with-intune"></a>Welche gängigen Möglichkeiten gibt es für die Verwendung des bedingten Zugriffs in Intune?

Es gibt zwei Arten des bedingten Zugriffs in Intune: den gerätebasierten bedingten Zugriff und den App-basierten bedingten Zugriff. Sie müssen die entsprechenden Konformitätsrichtlinien konfigurieren, um die Konformität mit bedingtem Zugriff in Ihrer Organisation zu unterstützen. Der bedingte Zugriff wird häufig verwendet, um Aktionen wie die folgenden auszuführen: Zulassen oder Blockieren des Zugriffs auf Exchange, Steuern des Zugriffs auf das Netzwerk oder Integrieren in eine Mobile Threat Defense-Lösung.
 
In diesem Artikel finden Sie Informationen zur Verwendung der Intune-Funktionen für die Konformität von mobilen *Geräten* und der Intune-Funktionen für die Verwaltung mobiler *Anwendungen* (Mobile Application Management, MAM). 

> [!NOTE]
> Bei dem bedingtem Zugriff handelt es sich um eine Azure Active Directory-Funktion, die in einer Azure Active Directory Premium-Lizenz enthalten ist. Intune erweitert diese Funktion, indem es der Lösung Konformität der mobilen Geräte und Mobile App-Verwaltung hinzufügt. Bei dem Knoten für bedingten Zugriff, auf den aus *Intune* zugegriffen wird, handelt es sich um denselben Knoten, auf den aus *Azure AD* zugegriffen wird.  

## <a name="device-based-conditional-access"></a>Gerätebasierter bedingter Zugriff

Intune und Azure Active Directory stellen gemeinsam sicher, dass nur verwaltete und konforme Geräte Zugriff auf E-Mails, Microsoft 365-Dienste, SaaS-Apps (Software-as-a-Service) und [lokale Apps](/azure/active-directory/active-directory-application-proxy-get-started) erhalten. Zusätzlich können Sie in Azure Active Directory eine Richtlinie festlegen, die nur Computern, die der Domäne angehören, oder mobilen Geräten, die in Intune registriert sind, den Zugriff auf Microsoft 365-Dienste erlaubt.

Intune stellt Funktionen für Gerätekonformitätsrichtlinien bereit, die den Konformitätsstatus der Geräte bewerten. Der Konformitätsstatus wird an Azure Active Directory gemeldet, um die in Azure Active Directory erstellte Richtlinie für den bedingten Zugriff zu erzwingen, wenn ein Benutzer versucht, auf Unternehmensressourcen zuzugreifen.

Gerätebasierte Richtlinien für den bedingten Zugriff für Exchange Online und andere Microsoft 365-Produkte werden im [Azure-Portal](../fundamentals/what-is-intune.md) konfiguriert.

- Erfahren Sie mehr über [Vorschreiben der Verwendung verwalteter Geräte für den Zugriff auf Cloud-Apps mithilfe des bedingten Zugriffs](/azure/active-directory/conditional-access/require-managed-devices).

- Erfahren Sie mehr über die [Gerätekonformität in Intune](device-compliance-get-started.md).

- Erfahren Sie mehr über [Unterstützte Browser für den bedingten Zugriff in Azure Active Directory](/azure/active-directory/conditional-access/technical-reference#supported-browsers).

> [!NOTE]
> Wenn Sie auf Android-Geräten den gerätebasierten Zugriff für SharePoint Online oder den browserbasierten Zugriff auf Exchange Online aktivieren, müssen Benutzer die Option **Browserzugriff aktivieren** auf dem Gerät wie folgt aktivieren:
> 1. Starten Sie die **Unternehmensportal-App**.
> 2. Rufen Sie die Seite **Einstellungen** über die Schaltfläche mit den drei Punkten (…) oder über die physische Menütaste auf.
> 3. Drücken Sie die Schaltfläche **Browserzugriff aktivieren** . 
> 4. Melden Sie sich im Chrome-Browser von Microsoft 365 ab, und starten Sie Chrome erneut.

### <a name="conditional-access-based-on-network-access-control"></a>Bedingter Zugriff basierend auf der Netzwerkzugriffssteuerung

Intune lässt sich in Partnerlösungen wie Cisco ISE, Aruba Clear Pass und Citrix NetScaler integrieren, um die Zugriffssteuerung basierend auf der Intune-Registrierung und dem Konformitätszustand eines Geräts bereitzustellen.

Benutzern kann der Zugriff auf unternehmenseigene WLAN- oder VPN-Ressourcen erlaubt oder verweigert werden, je nachdem, ob das verwendete Gerät verwaltet wird und den Intune-Richtlinien für die Gerätekonformität entspricht.

- Erfahren Sie mehr über die [NAC-Integration in Intune](network-access-control-integrate.md).

### <a name="conditional-access-based-on-device-risk"></a>Bedingter Zugriff basierend auf dem Geräterisiko

Intune arbeitet mit MTD-Anbietern (Mobile Threat Defense) zusammen, um eine Sicherheitslösung bereitzustellen, die Schadsoftware, Trojaner und andere Bedrohungen auf mobilen Geräten erkennt.

#### <a name="how-the-intune-and-mobile-threat-defense-integration-works"></a>Funktionsweise von Intune und der Integration von MTD-Lösungen

Wenn der Mobile Threat Defense-Agent auf mobilen Geräten installiert ist, sendet dieser Benachrichtigungen zum Konformitätszustand an Intune zurück, die eine Meldung enthalten, wenn auf dem mobilen Gerät eine Bedrohung gefunden wurde.

Die Integration von Intune und Mobile Threat Defense ist ein wichtiger Faktor bei Entscheidungen zum bedingten Zugriff basierend auf dem Geräterisiko.

- Erfahren Sie mehr über [Intune Mobile Threat Defense](mobile-threat-defense.md).

### <a name="conditional-access-for-windows-pcs"></a>Bedingter Zugriff für Windows-PCs

Der bedingte Zugriff für PCs bietet eine Funktionalität, die der für mobile Geräte verfügbaren ähnlich ist. Im Folgenden finden Sie Informationen zu den verschiedenen Möglichkeiten, den bedingten Zugriff beim Verwalten von PCs mit Intune zu verwenden.

#### <a name="corporate-owned"></a>Unternehmenseigene Geräte

- **Über Azure AD Hybrid eingebunden**: Diese Option wird häufig von Organisationen genutzt, die bereits mit der Verwaltung ihrer PCs über AD-Gruppenrichtlinien oder Configuration Manager vertraut sind.

- **In die Azure AD-Domäne eingebunden und über Intune verwaltet**: Dieses Szenario eignet sich für Organisationen, die einen Cloud-First-Ansatz (primäre Nutzung von Clouddiensten, sodass weniger lokale Infrastruktur erforderlich ist) oder einen Cloud-Only-Ansatz (gar keine lokale Infrastruktur) verfolgen möchten. Die Azure AD-Einbindung lässt sich gut in einer hybriden Umgebung einsetzen und bietet Zugriff auf Apps und Ressourcen sowohl in der Cloud als auch in der lokalen Infrastruktur. Geräte werden in Azure AD eingebunden und in Intune registriert – dies kann beim Zugriff auf Unternehmensressourcen als Kriterium für den bedingten Zugriff verwendet werden.

#### <a name="bring-your-own-device-byod"></a>Bring Your Own Device (BYOD)

- **Arbeitsplatzbeitritt und Intune-Verwaltung**: Bei dieser Option können Benutzer ihre persönlichen Geräte einbinden, um auf Unternehmensressourcen und -dienste zuzugreifen. Sie können den Arbeitsplatzbeitritt verwenden und Geräte bei Intune MDM registrieren, um Richtlinien auf Geräteebene zu erhalten. Dies ist eine weitere Option zum Auswerten von Kriterien für den bedingten Zugriff.

Erfahren Sie mehr über [Geräteverwaltung in Azure Active Directory](/azure/active-directory/devices/overview).

## <a name="app-based-conditional-access"></a>App-basierter bedingter Zugriff

Intune und Azure Active Directory stellen gemeinsam sicher, dass nur verwaltete Geräte auf Unternehmens-E-Mails oder andere Microsoft 365-Dienste zugreifen können.

- Erfahren Sie mehr über den [App-basierten bedingten Zugriff mit Intune](app-based-conditional-access-intune.md).

### <a name="intune-conditional-access-for-exchange-on-premises"></a>Bedingter Zugriff von Intune für Exchange lokal

Der bedingte Zugriff kann zum Zulassen oder Sperren des Zugriffs auf **Exchange lokal** basierend auf den Konformitätsrichtlinien für Geräte und dem Registrierungsstatus verwendet werden. Wenn der bedingte Zugriff zusammen mit einer Gerätekonformitätsrichtlinie verwendet wird, ist nur konformen Geräten der Zugriff auf Exchange lokal gestattet.

Sie können erweiterte Einstellungen wie die folgenden für den bedingten Zugriff konfigurieren, um eine präzisere Steuerung zu erzielen:

- Zulassen oder Blockieren bestimmter Plattformen

- Sofortiges Blockieren von Geräten, die nicht über Intune verwaltet werden

Jedes Gerät, mit dem auf Exchange lokal zugegriffen wird, wird auf Konformität überprüft, wenn Richtlinien für Gerätekonformität und bedingten Zugriff angewendet werden.

Wenn ein Gerät die festgelegten Bedingungen nicht erfüllt, erhält der Endbenutzer Anweisungen zum Registrieren des Geräts, um das Problem zu beheben, das die Konformität des Geräts verhindert.

> [!NOTE]
> Ab Juli 2020 wird der Exchange Connector nicht mehr unterstützt und durch die [hybride moderne Authentifizierung](/office365/enterprise/hybrid-modern-auth-overview) (HMA) für Exchange ersetzt. Für die Verwendung der HMA muss Intune nicht den Exchange Connector einrichten und verwenden. Durch diese Änderung wurde die Benutzeroberfläche zum Konfigurieren und Verwalten des Exchange Connector für Intune aus dem Admin Center des Microsoft Endpoint Manager entfernt, sofern Sie mit Ihrem Abonnement nicht bereits den Exchange Connector verwenden.
>
> Wenn Sie einen Exchange Connector in Ihrer Umgebung eingerichtet haben, wird Ihr Intune-Mandant weiterhin für dessen Verwendung unterstützt, und Sie haben weiterhin Zugriff auf die Benutzeroberfläche, die dessen Konfiguration unterstützt. Weitere Informationen finden Sie unter [Einrichten des lokalen Intune Exchange Connector](../protect/exchange-connector-install.md). Sie können den Connector weiterhin verwenden oder die HMA konfigurieren und den Connector deinstallieren.
>
> Die hybride moderne Authentifizierung stellt Funktionen bereit, die bisher im Exchange Connector für Intune verfügbar waren: Zuordnen einer Geräteidentität zum entsprechenden Exchange-Datensatz:  Diese Zuordnung ist nun nicht mehr Teil einer von Ihnen in Intune vorgenommenen Konfiguration oder der Anforderung, dass der Intune Connector zum Verbinden von Intune und Exchange verwendet werden soll. Mit der HMA wurde die Anforderung der Verwendung der Intune-spezifischen Konfiguration (des Connectors) aufgehoben.


<!-- Deprecated with change from the connector to Exchange hybrid modern authentication)

#### How conditional access for Exchange on-premises works

Conditional access for Exchange on-premises works differently than Azure Conditional Access based policies. You install the Intune Exchange on-premises connector to directly interact with Exchange server. The Intune Exchange connector pulls in all the Exchange Active Sync (EAS) records that exist at the Exchange server so Intune can take these EAS records and map them to Intune device records. These records are devices enrolled and recognized by Intune. This process allows or blocks e-mail access.

If the EAS record is new and Intune isn't aware of it, Intune issues a cmdlet (pronounced "command-let") that directs the Exchange server to block access to e-mail. Following are more details on how this process works:

![Exchange on-premises with CA flow-chart](./media/conditional-access-intune-common-ways-use/ca-intune-common-ways-1.png)

1. User tries to access corporate email, which is hosted on Exchange on-premises 2010 SP1 or later.

2. If the device is not managed by Intune, access to email will be blocked. Intune sends a block notification to the EAS client.

3. EAS receives the block notification, moves the device to quarantine, and sends the quarantine email with remediation steps that contain links so the users can enroll their devices.

4. The Workplace join process happens, which is the first step to have the device managed by Intune.

5. The device gets enrolled into Intune.

6. Intune maps the EAS record to a device record, and saves the device compliance state.

7. The EAS client ID gets registered by the Azure AD Device Registration process, which creates a relationship between the Intune device record, and the EAS client ID.

8. The Azure AD Device Registration saves the device state information.

9. If the user meets the conditional access policies, Intune issues a cmdlet through the Intune Exchange connector that allows the mailbox to sync.

10. Exchange server sends the notification to EAS client so the user can access e-mail.
-->

#### <a name="whats-the-intune-role"></a>Was ist die Intune-Rolle?

Intune bewertet und verwaltet den Gerätezustand.

#### <a name="whats-the-exchange-server-role"></a>Was ist die Exchange-Server-Rolle?

Der Exchange-Server stellt die API und die Infrastruktur bereit, um Geräte in die Quarantäne zu verschieben.

> [!IMPORTANT]
> Denken Sie daran, dass dem Benutzer, der das Gerät verwendet, ein Konformitätsprofil und eine Intune-Lizenz zugewiesen sein müssen, damit das Gerät hinsichtlich der Konformität bewertet werden kann. Wenn keine Konformitätsrichtlinie für den Benutzer bereitgestellt wird, wird das Gerät als konform behandelt, und es werden keine Zugriffsbeschränkungen angewendet.

## <a name="next-steps"></a>Nächste Schritte

[Konfigurieren des bedingten Zugriffs in Azure Active Directory](/azure/active-directory/active-directory-conditional-access-azure-portal)

[Einrichten App-basierter Richtlinien für bedingten Zugriff](app-based-conditional-access-intune-create.md)

[Erstellen einer Richtlinie für den bedingten Zugriff auf Exchange lokal](conditional-access-exchange-create.md)
