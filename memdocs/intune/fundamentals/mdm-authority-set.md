---
title: Festlegen der Autorität für die Verwaltung mobiler Geräte
titleSuffix: Microsoft Intune
description: Festlegen der Autorität für die Verwaltung mobiler Geräte in Intune.
keywords: ''
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/16/2019
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: fundamentals
ms.localizationpriority: high
ms.assetid: 8deff871-5dff-4767-9484-647428998d82
ms.reviewer: damionw
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 7244872fa888aaee164187e62a2355a94f793499
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83985185"
---
# <a name="set-the-mobile-device-management-authority"></a>Festlegen der Autorität für die Verwaltung mobiler Geräte

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Die Einstellung für die Autorität für die Verwaltung mobiler Geräte (Mobile Device Management, MDM) bestimmt, wie Sie Ihre Geräte verwalten. Als IT-Administrator müssen Sie eine MDM-Autorität festlegen, damit Benutzer Geräte zur Verwaltung registrieren können.

Die möglichen Konfigurationen sind Folgende:

- **Intune Standalone:** Ausschließliche Verwaltung in der Cloud, die Sie mithilfe des Azure-Portals konfigurieren. Ihnen stehen alle Funktionen von Intune zur Verfügung. [Legen Sie die MDM-Autorität in der Intune-Konsole fest](#set-mdm-authority-to-intune).

- **Co-Verwaltung in Intune:** Integration der Intune-Cloudlösung in Configuration Manager für Windows 10-Geräte. Sie konfigurieren Intune mithilfe der Configuration Manager-Konsole. [Konfigurieren der automatischen Registrierung von Geräten in Intune](https://docs.microsoft.com/configmgr/comanage/tutorial-co-manage-clients#configure-auto-enrollment-of-devices-to-intune) 

- **Verwaltung mobiler Geräte für Office 365:** Integration von Office 365 in die Intune-Cloudlösung. Sie konfigurieren Intune über das Microsoft 365 Admin Center. Ihnen steht eine Teilmenge der Funktionen von Intune Standalone zur Verfügung. Weitere Informationen finden Sie unter [Einrichten der Verwaltung mobiler Geräte (MDM) in Office 365](https://support.office.com/en-us/article/Set-up-Mobile-Device-Management-MDM-in-Office-365-dd892318-bc44-4eb1-af00-9db5430be3cd).

- **Office 365 MDM Coexistence** (MDM-Koexistenz für Office 365): Sie können MDM für Office und Intune für Ihren Mandanten gleichzeitig aktivieren und verwenden, und Sie können die Verwaltungsautorität für alle Benutzer entweder auf Intune oder MDM für Office festlegen, um zu bestimmen, welcher Dienst zum Verwalten ihrer mit MDM verwalteten Geräte verwendet wird. Die Verwaltungsautorität jedes Benutzers wird basierend auf der dem Benutzer zugeordneten Lizenz definiert. Wenn der Benutzer nur eine Lizenz für Microsoft 365 Basic oder Standard verfügt, werden dessen Geräte von MDM für Office verwaltet. Wenn der Benutzer über eine Lizenz für Intune verfügt, werden die Geräte von Intune verwaltet. Wenn Sie einem Benutzer, der zuvor von MDM für Office verwaltet wurde, eine Lizenz für Intune hinzufügen, werden seine Geräte auf die Intune-Verwaltung umgestellt. Stellen Sie sicher, dass Intune-Konfigurationen den Benutzern zugewiesen sind, um MDM für Office zu ersetzen, bevor Sie Benutzer zu Intune verschieben, andernfalls verlieren ihre Geräte die MDM-Konfiguration für Office, und sie erhalten keinen Ersatz von Intune.

## <a name="set-mdm-authority-to-intune"></a>Festlegen der MDM-Autorität in Intune

Führen Sie folgende Schritte durch, wenn Sie die MDM-Autorität noch nicht festgelegt haben.

1. Klicken Sie im [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) auf das orangefarbene Banner, um die Einstellung **Autorität für die Verwaltung mobiler Geräte** zu öffnen. Der orangefarbene Banner wird nur angezeigt, wenn Sie die MDM-Autorität noch nicht festgelegt haben.
2. Wählen Sie unter **Autorität für die Verwaltung mobiler Geräte** Ihre MDM-Autorität aus den folgenden Optionen aus:
   - **Intune-MDM-Autorität**
   - **Keine**

   ![Screenshot vom Intune-Bildschirm zum Festlegen der Autorität für die mobile Geräteverwaltung](./media/mdm-authority-set/set-mdm-auth.png)

   Eine Meldung zeigt an, dass Sie die MDM-Autorität erfolgreich auf Intune festgelegt haben.

### <a name="workflow-of-intune-administration-ui"></a>Workflow der Intune-Verwaltungsbenutzeroberfläche
Wenn die Verwaltung von Android- oder Apple-Geräten aktiviert ist, sendet Intune Geräte- und Benutzerinformationen zur Integration mit diesen Drittanbieterdiensten, um die jeweiligen Geräte zu verwalten.

Szenarios, die eine Zustimmung zur Datenfreigabe hinzufügen, werden unter den folgenden Bedingungen eingeschlossen:
- Sie aktivieren Android-Arbeitsprofile.
- Apple-MDM-Push-Zertifikate werden aktiviert und hochgeladen.
- Einer der Apple-Dienste wie das Programm zur Geräteregistrierung, School Manager oder Volume Purchase Program wird aktiviert.

In jedem Fall muss die Zustimmung erteilt werden, wenn ein Verwaltungsdienst für mobile Geräte ausgeführt wird. Beispielsweise zum Bestätigen, dass ein IT-Administrator Google- oder Apple-Geräte zur Registrierung autorisiert hat. An den folgenden Speicherorten finden Sie die Dokumentation zur Frage, welche Informationen freigegeben werden, wenn die neuen Workflows live sind:
- [Von Intune an Google gesendete Daten](https://aka.ms/Data-intune-sends-to-google)
- [Von Intune an Apple gesendete Daten](https://aka.ms/data-intune-sends-to-apple)

## <a name="key-considerations"></a>Wichtige Überlegungen
Nachdem Sie auf die neue MDM-Autorität umgestellt haben, gibt es wahrscheinlich eine Übergangszeit (bis zu acht Stunden), bevor das Gerät eingecheckt und mit dem Dienst synchronisiert wird. Sie müssen die Einstellungen in der neuen MDM-Autorität konfigurieren, um sicherzustellen, dass registrierte Geräte nach der Umstellung weiterhin verwaltet und geschützt werden. 
- Geräte müssen nach der Umstellung eine Verbindung mit dem Dienst herstellen, damit die Einstellungen der neuen MDM-Autorität (eigenständiges Intune) die vorhandenen Einstellungen auf dem Gerät ersetzen.
- Nach dem Ändern der MDM-Autorität verbleiben einige der grundlegenden Einstellungen (z.B. Profile) aus der vorherigen MDM-Autorität für bis zu sieben Tage oder bis zur ersten Verbindung des Geräts mit dem Dienst auf dem Gerät. Es wird empfohlen, dass Sie Apps und Einstellungen (Richtlinien, Profile, Apps usw.) so bald wie möglich in der neuen MDM-Autorität konfigurieren und die Einstellung den Benutzergruppen bereitstellen, die Benutzer mit gegenwärtig registrierten Geräten enthalten. Sobald ein Gerät nach der Umstellung der MDM-Autorität eine Verbindung mit dem Dienst herstellt, werden die neuen Einstellungen der neuen MDM-Autorität übertragen, und Lücken bei Verwaltung und Schutz werden verhindert.
- Geräte, denen keine Benutzer zugeordnet sind (dies ist typischerweise der Fall, wenn Sie das iOS/iPadOS-Programm zur Geräteregistrierung oder die Massenregistrierung verwenden), werden nicht zur neuen MDM-Autorität migriert. Für diese Geräte müssen Sie sich mit dem Support in Verbindung setzen, um Hilfe beim Verschieben dieser Geräte zur neuen MDM-Autorität zu erhalten.

## <a name="mobile-device-cleanup-after-mdm-certificate-expiration"></a>Bereinigen mobiler Geräte nach Ablauf des MDM-Zertifikats

Das MDM-Zertifikat wird automatisch erneuert, wenn mobile Geräte mit dem Intune-Dienst kommunizieren. Wenn mobile Geräte zurückgesetzt werden oder für längere Zeit keine Kommunikation mit dem Intune-Dienst stattfindet, wird das MDM-Zertifikat nicht erneuert. Das Gerät wird 180 Tage nach Ablauf des MDM-Zertifikats aus dem Azure-Portal entfernt.

## <a name="remove-mdm-authority"></a>Entfernen der MDM-Autorität

Die MDM-Autorität kann nicht in „Unbekannt“ geändert werden. Der Dienst verwendet die MDM-Autorität, um zu bestimmen, an welches Portal diese registrierten Geräte melden (Microsoft Intune oder Office 365 MDM).

## <a name="what-to-expect-after-changing-the-mdm-authority"></a>Was passiert nach der Umstellung der MDM-Autorität

- Wenn der Intune-Dienst erkennt, dass die MDM-Autorität eines Mandanten umgestellt wurde, sendet er eine Benachrichtigung an alle registrierten Geräte, damit sie beim Dienst eingecheckt und synchronisiert werden (diese Benachrichtigung befindet sich außerhalb der regelmäßig geplanten Eincheckvorgänge). Daher werden nach der Umstellung der MDM-Autorität für den Mandanten von eigenständigem Intune alle eingeschalteten und online befindlichen Geräte mit dem Dienst verbunden. Sie empfangen die neue MDM-Autorität und werden von ihr verwaltet. Es gibt keine Unterbrechung bei der Verwaltung und bei dem Schutz dieser Geräte.
- Selbst für Geräte, die während (oder kurz nach) der Umstellung der MDM-Autorität eingeschaltet und online sind, gibt es eine Verzögerung von bis zu acht Stunden (je nach Zeitpunkt des nächsten geplanten regulären Eincheckvorgangs), bevor Geräte unter der neuen MDM-Autorität beim Dienst registriert werden.    

  > [!IMPORTANT]    
  > In der Zeit zwischen der Umstellung der MDM-Autorität und dem Hochladen des erneuerten APNs-Zertifikats in die neue Autorität schlagen neue Registrierungen und Eincheckvorgänge für iOS/iPadOS-Geräte fehl. Aus diesem Grund ist es wichtig, dass Sie das APNs-Zertifikat so bald wie möglich nach der Umstellung der MDM-Autorität überprüfen und in die neue Autorität hochladen.

- Benutzer können schnell auf die neue MDM-Autorität umstellen, indem sie manuell einen Eincheckvorgang des Geräts beim Dienst starten. Benutzer können diese Änderung problemlos mithilfe der Unternehmensportal-App und dem Initiieren einer Überprüfung der Gerätekonformität vornehmen.
- Um zu überprüfen, ob nach der Umstellung der MDM-Autorität und dem Einchecken und Synchronisieren der Geräte beim Dienst alles ordnungsgemäß funktioniert, suchen Sie in der neuen MDM-Autorität nach den Geräten.
- Es gibt eine Übergangszeit, bis ein Gerät beim Dienst eingecheckt wird, wenn das Gerät während der Umstellung der MDM-Autorität offline war. Um sicherzustellen, dass das Gerät während dieser Übergangszeit geschützt und funktionsfähig bleibt, verbleiben die folgenden Profile bis zu sieben Tage lang auf dem Gerät (oder bis das Gerät eine Verbindung mit der neuen MDM-Autorität herstellt und die neuen Einstellungen empfängt, die die vorhandenen überschreiben):
  - E-Mail-Profil
  - VPN-Profil
  - Zertifikatprofil
  - WLAN-Profil
  - Konfigurationsprofile
- Nachdem Sie auf die neue MDM-Autorität umgestellt haben, kann es bis zu einer Woche dauern, bis die Kompatibilitätsinformationen in der Microsoft Intune-Verwaltungskonsole richtig gemeldet werden. Allerdings sind die Konformitätszustände in Azure Active Directory und auf dem Gerät richtig, sodass das Gerät weiterhin geschützt ist.
- Stellen Sie sicher, dass die neuen Einstellungen, mit denen die vorhandenen Einstellungen überschrieben werden sollen, den gleichen Namen aufweisen wie die vorherigen, damit die alten Einstellungen tatsächlich überschrieben werden. Andernfalls weisen die Geräte möglicherweise redundante Profile und Richtlinien auf.    

  > [!TIP]    
  > Es empfiehlt sich, alle Verwaltungseinstellungen und Konfigurationen sowie Bereitstellungen kurz nach Abschluss der Umstellung der MDM-Autorität zu erstellen. Dadurch wird sichergestellt, dass Geräte in der Übergangszeit geschützt und aktiv verwaltet werden.

- Führen Sie nach der Umstellung der MDM-Autorität die folgenden Schritte aus, um zu überprüfen, ob neue Geräte erfolgreich bei der neuen Autorität registriert werden:   
  - Registrieren eines neuen Geräts
  - Stellen Sie sicher, dass das neu registrierte Gerät in der neuen MDM-Autorität angezeigt wird.
  - Führen Sie über die Verwaltungskonsole auf dem Gerät eine Aktion aus, z.B. Remotesperre. Wenn sie erfolgreich ist, wird das Gerät durch die neue MDM-Autorität verwaltet.
- Wenn Sie Probleme mit bestimmten Geräten haben, können Sie die Registrierung der Geräte aufheben und sie erneut registrieren, damit sie so schnell wie möglich mit der neuen Autorität verbunden und von ihr verwaltet werden.

## <a name="next-steps"></a>Nächste Schritte

Da die MDM-Autorität nun festgelegt ist, können Sie mit der [Geräteregistrierung](../enrollment/device-enrollment.md) beginnen.
