---
title: Verwenden von Berichten zur Updatekonformität für Windows Updates in Microsoft Intune
titleSuffix: Microsoft Intune
description: Verwenden von OMS-Updatekonformität zum Abrufen von Berichtsdaten für Windows Update, die mit Intune bereitgestellt werden
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/01/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: 297707da0afb03650eaab91b26abad9947c6a951
ms.sourcegitcommit: 75d6ea42a0f473dc5020ae7fcb667c9bdde7bd97
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/01/2020
ms.locfileid: "89286151"
---
# <a name="intune-compliance-reports-for-updates"></a>Berichte zur Updatekonformität für Intune

Wenn Sie Intune verwenden, um Windows-Updates auf Windows 10-Geräten bereitzustellen, können Sie mithilfe von Intune oder der kostenlosen Lösung *Updatekonformität* Details zur Updatekonformität abrufen. Updatekonformität ist Teil der Microsoft Operations Management Suite (OMS).

## <a name="use-intune"></a>Verwenden von Intune

Gehen Sie wie folgt vor, um Richtlinienberichte zum Bereitstellungsstatus für die von Ihnen konfigurierten Windows 10-Updateringe zu prüfen:

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Geräte** > **Übersicht** > **Softwareupdatestatus** aus. Hier finden Sie allgemeine Informationen zum Status der Updateringe, die Sie zugewiesen haben.

3. Wählen Sie **Überwachen** aus, um weitere Details anzuzeigen. Wählen Sie dann unter **Softwareupdates** die Option **Bereitstellungsstatus pro Updatering** aus, und wählen Sie den zu überprüfenden Bereitstellungsring aus.

   Wählen Sie im Abschnitt **Überwachen** einen der folgenden Berichte aus, um weitere Informationen zum Updatering anzuzeigen:

   - **Gerätestatus**: Hiermit wird der Status der Gerätekonfiguration angezeigt. Weitere Informationen finden Sie unter [Aktualisieren von deviceConfigurationDeviceStatus]( /graph/api/intune-deviceconfig-deviceconfigurationdevicestatus-update?view=graph-rest-1.0).

   - **Benutzerstatus**: Hiermit werden der Benutzername, der Status und das Datum des letzten Berichts angezeigt. Weitere Informationen finden Sie unter [Auflisten von deviceConfigurationUserStatus](/graph/api/intune-deviceconfig-deviceconfigurationuserstatus-list?view=graph-rest-1.0).

   - **Endbenutzer-Updatestatus**: Hiermit wird der Updatestatus der Windows-Geräte angezeigt. Weitere Informationen finden Sie unter [windowsUpdateState](/graph/api/resources/intune-shared-windowsupdatestate?view=graph-rest-beta).

## <a name="use-update-compliance"></a>Verwenden der Updatekonformität

Sie können Windows 10-Updaterollouts mithilfe der [Updatekonformität](/windows/deployment/update/update-compliance-monitor) überwachen. Die Updatekonformität wird im Azure-Portal angeboten und ist für Geräte kostenlos, die die entsprechenden [Voraussetzungen](/windows/deployment/update/update-compliance-get-started#update-compliance-prerequisites) erfüllen.  

Bei Verwendung dieser Lösung können Sie eine Organisations-ID für jedes Ihrer mit Intune verwalteten Windows 10-Geräte bereitstellen, für das Sie Updateüberwachungsberichte verwenden möchten.  

Die Organisations-ID können Sie in Intune mithilfe der OMA-URI-Einstellungen einer benutzerdefinierten Richtlinie konfigurieren. Siehe [Verwenden von benutzerdefinierten Einstellungen für Windows 10-Geräte in Intune](../configuration/custom-settings-windows-10.md).

Der OMA-URI-Pfad (Groß-/Kleinschreibung beachten) zum Konfigurieren der Organisations-ID lautet *./Vendor/MSFT/DMClient/Provider/MS DM Server/CommercialID*.

Unter **OMA-URI-Einstellung hinzufügen oder bearbeiten** können Sie beispielsweise folgende Werte verwenden:

- **Einstellungsname**: Kommerzielle Windows Analytics-ID
- **Einstellungsbeschreibung**: Konfigurieren der kommerziellen ID für Windows Analytics-Lösungen
- **OMA-URI** (Groß-/Kleinschreibung beachten): *./Vendor/MSFT/DMClient/Provider/ProviderID/CommercialID*
- **Datentyp**: Zeichenfolge
- **Wert**: \<Use the GUID shown on the Windows Telemetry tab in your OMS workspace>

> [!NOTE]
> Weitere Informationen über MS DM-Server finden Sie unter [DMClient configuration service provider (CSP) (DMClient-Konfigurationsdienstanbieter (CSP))]( /windows/client-management/mdm/dmclient-csp).

## <a name="next-steps"></a>Nächste Schritte

[Verwalten von Softwareupdates in Intune](windows-update-for-business-configure.md)
