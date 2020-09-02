---
title: Verwalten von Geräten mit Endpunktsicherheit in Microsoft Intune | Microsoft-Dokumentation
description: Erfahren Sie, wie Sicherheitsadministratoren mit dem Knoten „Endpunktsicherheit“ Geräte anzeigen und in Microsoft Endpoint Manager verwalten können.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 98b1380254a784dfe8939c607ab574f7bdaa8752
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88914989"
---
# <a name="manage-devices-with-endpoint-security-in-microsoft-intune"></a>Verwalten von Geräten mithilfe der Endpunktsicherheit in Microsoft Intune

Als Sicherheitsadministrator verwenden Sie die Ansicht *Alle Geräte* im Microsoft Endpoint Manager Admin Center, um Ihre Geräte zu überprüfen und zu verwalten. Die Ansicht zeigt eine Liste all Ihrer Geräte in Azure Active Directory (Azure AD). Dies schließt Geräte ein, die über Intune, Configuration Manager und per [Co-Verwaltung](/configmgr/comanage/overview) sowohl über Intune als auch über Configuration Manager verwaltet werden. Geräte können sich in der Cloud und in Ihrer lokalen Infrastruktur befinden, wenn sie in Azure AD integriert sind.

 Um zur Ansicht zu gelangen, öffnen Sie das [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) und klicken auf **Endpunktsicherheit** > **Alle Geräte**.

Die Ansicht *Alle Geräte* zeigt anfänglich Ihre Geräte und wichtige Informationen zu jedem Gerät an:

- Wie wird das Gerät verwaltet?
- Konformitätsstatus
- Details zum Betriebssystem
- Letzter Eincheckvorgang für das Gerät
- und mehr...

![Ansicht „Alle Geräte“ im Admin Center](./media/endpoint-security-manage-devices/all-device-view.png)

Bei der Anzeige von Gerätedetails können Sie ein Gerät auswählen, um einen Drilldown für weitere Informationen durchzuführen.

## <a name="available-details-by-management-type"></a>Verfügbare Details nach Verwaltungstyp

Bei der Anzeige von Geräten im Microsoft Endpoint Manager Admin Center sollten Sie bedenken, wie das Gerät verwaltet wird. Die Verwaltungsquelle hat Einfluss darauf, welche Informationen im Admin Center angezeigt werden und welche Aktionen zum Verwalten des Geräts zur Verfügung stehen.

Überprüfen Sie die folgenden Felder:

- **Verwaltet von**: Diese Spalte gibt an, wie das Gerät verwaltet wird. Folgende Verwaltungsoptionen sind verfügbar:

  - **MDM**: Die Geräte werden von Intune verwaltet. Intune erfasst Konformitätsdaten und meldet diese an das Admin Center.

  - **ConfigMgr**: Diese Geräte erscheinen im Microsoft Endpoint Manager Admin Center, wenn Sie die *Mandantenanfügung* verwenden, um die mit Configuration Manager verwalteten Geräte hinzuzufügen. Für eine Verwaltung muss auf dem Gerät der Configuration Manager-Client ausgeführt werden, und es müssen folgende Voraussetzungen erfüllt sein:

    - Das Gerät befindet sich in einer Arbeitsgruppe (AAD-Beitritt oder anderweitig eingebunden)
    - Das Gerät muss in die Domäne eingebunden sein
    - AAD Hybrid-Einbindung (Einbindung in AD und AAD)

    Der Konformitätsstatus für Geräte, die über Configuration Manager verwaltet werden, ist im Microsoft Endpoint Manager Admin Center nicht sichtbar.

    Weitere Informationen finden Sie unter [Aktivieren der Mandantenanfügung](/configmgr/tenant-attach/device-sync-actions) in der Configuration Manager-Dokumentation.

  - **MDM/ConfigMgr-Agent**: Diese Geräte unterliegen einer Co-Verwaltung über Intune und Configuration Manager.

    Bei der Co-Verwaltung [wählen Sie verschiedene Workloads für die Co-Verwaltung](/configmgr/comanage/how-to-switch-workloads) aus, um zu bestimmen, welche Aspekte von Configuration Manager oder Intune verwaltet werden. Diese Auswahl beeinflusst, welche Richtlinien auf das Gerät angewendet und wie Konformitätsdaten an das Admin Center gemeldet werden.

    Beispielsweise können Sie Intune zum Konfigurieren der Richtlinie für Antivirus, Firewall und Verschlüsselung verwenden. Diese Richtlinientypen sind Richtlinien für *Endpoint Protection*. Damit für ein Gerät mit Co-Verwaltung nicht die Configuration Manager-Richtlinien, sondern die Intune-Richtlinien verwendet werden, legen Sie den Schieberegler der Co-Verwaltung für Endpoint Protection entweder auf *Intune* oder *Intune-Pilot* fest. Wenn der Schieberegler auf Configuration Manager festgelegt ist, verwendet das Gerät stattdessen die Richtlinien und Einstellungen aus Configuration Manager.

- **Konformität**: Die Konformität wird anhand der Konformitätsrichtlinien bewertet, die dem Gerät zugewiesen sind. Die Quelle dieser Richtlinien sowie die in der Konsole angezeigten Informationen richten sich danach, wie das Gerät verwaltet wird: über Intune, Configuration Manager oder per Co-Verwaltung. Damit Geräte mit Co-Verwaltung Konformitätsdaten melden, legen Sie den Schieberegler der Co-Verwaltung für die Gerätekonformität entweder auf „Intune“ oder auf „Intune-Pilot“ fest.  

  Nachdem für ein Gerät Konformitätsdaten an das Admin Center gemeldet wurden, können Sie einen Drilldown zur Anzeige weiterer Details durchführen. Ist ein Gerät nicht konform, können Sie über einen Drilldown ermitteln, welche Konformitätsrichtlinien nicht eingehalten werden. Diese Informationen helfen Ihnen dabei, das Problem zu untersuchen und das Gerät in einen konformen Zustand zu versetzen.

- **Letztes Einchecken**: Dieses Feld zeigt, wann das Gerät zum letzten Mal seinen Status gemeldet hat.

## <a name="review-a-devices-policy"></a>Überprüfen einer Geräterichtlinie

Während der Anzeige der Geräteliste können Sie ein Gerät für einen Drilldown zur Anzeige zusätzlicher Informationen auswählen, um die Seite *Übersicht* für dieses Gerät zu öffnen.

Auf der Übersichtsseite für ein Gerät können Sie anschließend auf **Konfiguration der Endpunktsicherheit** klicken, um die Richtlinien zur Endpunktsicherheit anzuzeigen, die für dieses Gerät gelten. Richtliniendetails stehen für Geräte zur Verfügung, die über MDM und Intune verwaltet werden.

![Anzeigen von Details zur Endpunktsicherheitsrichtlinie](./media/endpoint-security-manage-devices/view-policy-details.png)

Für Geräte, die über Configuration Manager verwaltet werden, werden keine Richtliniendetails anzeigt. Um zusätzliche Informationen für diese Geräte anzuzeigen, verwenden Sie die Configuration Manager-Konsole.

## <a name="remote-actions-for-devices"></a>Remoteaktionen für Geräte

Remoteaktionen sind Aktionen, die Sie über Endpoint das Microsoft Endpoint Manager Admin Center für ein Gerät starten oder darauf anwenden können. Wenn Sie Details zu einem Gerät anzeigen, können Sie auf die Remoteaktionen zugreifen, die für das Gerät gelten.

Remoteaktionen werden oben auf der Seite *Übersicht* für die Geräte angezeigt. Aktionen, die aus Platzgründen nicht auf dem Bildschirm angezeigt werden können, können über die Auslassungspunkte auf der rechten Seite ausgewählt werden:

![Anzeigen zusätzlicher Aktionen](./media/endpoint-security-manage-devices/view-additional-actions.png)

Die verfügbaren Remoteaktionen richten sich danach, wie das Gerät verwaltet wird:

- **Intune**: Es stehen alle [Intune-Remoteaktionen](../remote-actions/device-management.md) zur Verfügung, die auf die Geräteplattform anwendbar sind.  
- **Configuration Manager:** Sie können die folgenden Configuration Manager-Aktionen verwenden:

  - Computerrichtlinie synchronisieren
  - Benutzerrichtlinie synchronisieren
  - App-Evaluierungszyklus

- **Co-Verwaltung**: Sie können sowohl auf die Intune-Remoteaktionen als auch auf die Configuration Manager-Aktionen zugreifen.

Einige der Intune-Remoteaktionen können dazu beitragen, Geräte zu schützen oder Daten zu schützen, die auf dem Gerät vorhanden sind. Remoteaktionen ermöglichen Folgendes:

- Sperren eines Geräts
- Zurücksetzen eines Geräts
- Entfernen von Unternehmensdaten
- Außerplanmäßiges Ausführen einer Überprüfung auf Schadsoftware
- Rotieren von BitLocker-Schlüsseln

Die folgenden Intune-Remoteaktionen sind für Sicherheitsadministratoren von Interesse und stellen eine Teilmenge der [vollständigen Liste](../remote-actions/device-inventory.md#view-the-device-details) dar. Nicht alle Aktionen sind für alle Geräteplattformen verfügbar. Die Links verweisen auf Inhalte mit ausführlichen Informationen für jede Aktion.

- [Gerät synchronisieren](../remote-actions/device-sync.md): Hiermit wird das Gerät sofort bei Intune eingecheckt. Wird ein Gerät eingecheckt, empfängt es alle ihm zugewiesenen ausstehenden Aktionen oder Richtlinien.  

- [Neu starten](../remote-actions/device-restart.md): Hiermit wird für ein Windows 10-Gerät ein Neustart innerhalb von fünf Minuten erzwungen. Der Gerätebesitzer wird nicht automatisch über den Neustart benachrichtigt und kann Daten verlieren.

- [Schnellüberprüfung](../configuration/device-restrictions-windows-10.md): Hiermit wird Defender angewiesen, eine Schnellüberprüfung des Geräts auf Schadsoftware durchzuführen und die Ergebnisse an Intune zu melden. Bei einer Schnellüberprüfung werden gängige Speicherorte überprüft, an denen Schadsoftware registriert sein kann – z. B. Registrierungsschlüssel und bekannte Windows-Startordner.

- [Vollständige Überprüfung](../configuration/device-restrictions-windows-10.md): Hiermit wird Defender angewiesen, eine Überprüfung des Geräts auf Schadsoftware durchzuführen und die Ergebnisse an Intune zu melden. Bei einer vollständigen Überprüfung werden gängige Speicherorte überprüft, an denen Schadsoftware registriert sein kann. Darüber hinaus werden auch alle Dateien und Ordner auf dem Gerät überprüft.

- Aktualisierung der Windows Defender-Sicherheitsinformationen: Hiermit wird das Gerät angewiesen, seine Schadsoftwaredefinitionen für Microsoft Defender Antivirus zu aktualisieren. Diese Aktion löst keine Überprüfung aus.

- [BitLocker-Schlüsselrotation](../protect/encrypt-devices.md#to-rotate-the-bitlocker-recovery-key): Hiermit können Sie den BitLocker-Wiederherstellungsschlüssel eines Geräts mit Windows 10, Version 1909 oder höher rotieren.

Sie können außerdem **Massengeräteaktionen** verwenden, um einige Aktionen wie etwa *Zurückziehen* und *Zurücksetzen* für mehrere Geräte gleichzeitig zu verwalten. [Massenaktionen](../remote-actions/bulk-device-actions.md) stehen in der Ansicht *Alle Geräte* zur Verfügung. Sie wählen die Plattform und Aktion aus und können dann bis zu 100 Geräte angeben.

![Auswählen von Massenaktionen](./media/endpoint-security-manage-devices/select-bulk-actions.png)

Optionen, die Sie für Geräte verwalten, werden erst beim nächsten Einchecken des Geräts bei Intune wirksam.

## <a name="next-steps"></a>Nächste Schritte

[Verwalten der Endpunktsicherheit in Intune](../protect/endpoint-security.md)