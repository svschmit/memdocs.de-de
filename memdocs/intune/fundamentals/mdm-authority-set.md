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
ms.openlocfilehash: 676e7a4db54558eaea87ad2fa8efbe8af546f035
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88996570"
---
# <a name="set-the-mobile-device-management-authority"></a>Festlegen der Autorität für die Verwaltung mobiler Geräte

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Die Einstellung für die Autorität für die Verwaltung mobiler Geräte (Mobile Device Management, MDM) bestimmt, wie Sie Ihre Geräte verwalten. Als IT-Administrator müssen Sie eine MDM-Autorität festlegen, damit Benutzer Geräte zur Verwaltung registrieren können.

Die möglichen Konfigurationen sind Folgende:

- **Intune Standalone:** Ausschließliche Verwaltung in der Cloud, die Sie mithilfe des Azure-Portals konfigurieren. Ihnen stehen alle Funktionen von Intune zur Verfügung. [Legen Sie die MDM-Autorität in der Intune-Konsole fest](#set-mdm-authority-to-intune).

- **Co-Verwaltung in Intune:** Integration der Intune-Cloudlösung in Configuration Manager für Windows 10-Geräte. Sie konfigurieren Intune mithilfe der Configuration Manager-Konsole. [Konfigurieren der automatischen Registrierung von Geräten in Intune](/configmgr/comanage/tutorial-co-manage-clients#configure-auto-enrollment-of-devices-to-intune) 

- **Basic Mobility and Security for Office 365** (Einfache Mobilität und Sicherheit für Microsoft 365): Wenn Sie diese Konfiguration aktiviert haben, wird die MDM-Autorität auf „Office 365“ festgelegt. Wenn Sie Intune verwenden möchten, müssen Sie zuvor Intune-Lizenzen kaufen.

- **Grundlegende Mobilität und Sicherheit für Microsoft 365 – [Koexistenz](#coexistence)** : Sie können Intune Ihrem Mandanten hinzufügen, wenn Sie die Konfiguration „Grundlegende Mobilität und Sicherheit für Microsoft 365“ bereits verwenden. Außerdem können Sie die Verwaltungsautorität für alle Benutzer entweder auf „Intune“ oder auf „Grundlegende Mobilität und Sicherheit für Microsoft 365“ festlegen, um zu bestimmen, welcher Dienst zum Verwalten Ihrer bei MDM registrierten Geräte verwendet wird. Die Verwaltungsautorität jedes Benutzers wird basierend auf der dem Benutzer zugeordneten Lizenz definiert. Wenn der Benutzer nur eine Lizenz für Microsoft 365 Basic oder Standard verfügt, werden dessen Geräte von „Basic Mobility and Security for Microsoft 365“ verwaltet. Wenn der Benutzer über eine Lizenz für Intune verfügt, werden die Geräte von Intune verwaltet. Wenn Sie einem Benutzer, der zuvor von „Basic Mobility and Security for Microsoft 365“ verwaltet wurde, eine Lizenz für Intune hinzufügen, werden seine Geräte auf die Intune-Verwaltung umgestellt. Stellen Sie sicher, dass den Benutzern Intune-Konfigurationen zugewiesen sind, um „Basic Mobility and Security for Microsoft 365“ zu ersetzen, bevor Sie Benutzer zu Intune verschieben, andernfalls verlieren ihre Geräte die Konfiguration „Basic Mobility and Security for Microsoft 365“, und sie erhalten keinen Ersatz von Intune.

## <a name="set-mdm-authority-to-intune"></a>Festlegen der MDM-Autorität in Intune

Bei Mandanten mit Dienstrelease 1911 oder höher ist die MDM-Autorität automatisch auf Intune festgelegt.

Bei Mandanten mit Releases vor 1911 führen Sie folgende Schritte durch, wenn Sie die MDM-Autorität noch nicht festgelegt haben.

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
- Nach dem Ändern der MDM-Autorität verbleiben einige der grundlegenden Einstellungen (z.B. Profile) aus der vorherigen MDM-Autorität für bis zu sieben Tage oder bis zur ersten Verbindung des Geräts mit dem Dienst auf dem Gerät. Sie sollten Apps und Einstellungen (wie Richtlinien, Profile und Apps) so bald wie möglich in der neuen MDM-Autorität konfigurieren und die Einstellung den Benutzergruppen bereitstellen, die Benutzer mit gegenwärtig registrierten Geräten enthalten. Sobald ein Gerät nach der Umstellung der MDM-Autorität eine Verbindung mit dem Dienst herstellt, werden die neuen Einstellungen der neuen MDM-Autorität übertragen, und Lücken bei Verwaltung und Schutz werden verhindert.
- Geräte, denen keine Benutzer zugeordnet sind (dies ist typischerweise der Fall, wenn Sie das iOS/iPadOS-Programm zur Geräteregistrierung oder die Massenregistrierung verwenden), werden nicht zur neuen MDM-Autorität migriert. Für diese Geräte müssen Sie sich mit dem Support in Verbindung setzen, um Hilfe beim Verschieben dieser Geräte zur neuen MDM-Autorität zu erhalten.

## <a name="coexistence"></a>Coexistence

Durch das Aktivieren der Koexistenz können Sie Intune für eine neue Gruppe von Benutzern verwenden und dabei weiterhin „Basic Mobility and Security“ für die vorhandenen Benutzer verwenden. Sie können über den Benutzer steuern, welche Geräte von Intune verwaltet werden. Wenn ein Benutzer einer Intune-Lizenz zugewiesen oder die Intune-Co-Verwaltung mit Configuration Manager verwendet wird, werden alle seine registrierten Geräte von Intune verwaltet. Andernfalls wird der Benutzer von „Basic Mobility and Security“ verwaltet.

Zum Aktivieren der Koexistenz sind drei Hauptschritte erforderlich:
1. Vorbereitung
2. Hinzufügen der Intune-MDM-Autorität
3. Benutzer- und Gerätemigration (optional).

### <a name="preparation"></a>Vorbereitung

Berücksichtigen Sie die folgenden Punkte, bevor Sie die Koexistenz mit „Basic Mobility and Security“ aktivieren:
- Stellen Sie sicher, dass Sie über ausreichende [Intune-Lizenzen](licenses.md) für die Benutzer verfügen, die Sie über Intune verwalten möchten.
- Überprüfen Sie, welchen Benutzern Intune-Lizenzen zugewiesen sind. Nachdem Sie die Koexistenz aktiviert haben, werden die Geräte von Benutzern, denen bereits eine Intune-Lizenz zugewiesen wurde, an Intune übertragen. Um unerwartete Geräteübertragungen zu vermeiden, sollten Sie Intune-Lizenzen erst dann zuweisen, wenn Sie die Koexistenz aktiviert haben.
- Erstellen Sie Intune-Richtlinien zum Ersetzen von Gerätesicherheitsrichtlinien, die ursprünglich über das Office 365 Security & Compliance-Portal bereitgestellt wurden, und stellen Sie sie bereit. Diese Ersetzung sollte für alle Benutzer durchgeführt werden, von denen Sie erwarten, dass sie von „Basic Mobility and Security“ zu Intune wechseln. Wenn diesen Benutzern keine Intune-Richtlinien zugewiesen sind, können sie durch das Aktivieren der Koexistenz die „Basic Mobility and Security“-Einstellungen verlieren. Diese Einstellungen, wie z. B. verwaltete E-Mail-Profile, gehen ohne Ersetzung verloren. Auch beim Ersetzen von Richtlinien zur Gerätesicherheit durch Intune-Richtlinien werden Benutzer aufgefordert, ihre E-Mail-Profile erneut zu authentifizieren, nachdem das Gerät in die Intune-Verwaltung verschoben wurde.

### <a name="add-intune-mdm-authority"></a>Hinzufügen der Intune-MDM-Autorität

Um die Koexistenz zu aktivieren, müssen Sie Intune als MDM-Autorität für Ihre Umgebung hinzufügen:

1. Melden Sie sich mit Rechten als globaler Azure AD-Administrator oder Intune-Dienstadministrator bei „endpoint.microsoft.com“ an.
2. Navigieren Sie zu **Geräte**.
3. Das Blatt **MDM-Autorität hinzufügen** wird angezeigt.
4. Um die MDM-Autorität von *Office 365* auf *Intune* zu übertragen und die Koexistenz zu aktivieren, wählen Sie **Intune-MDM-Autorität** > **Hinzufügen** aus.
  ![Screenshot des Bildschirms „MDM-Autorität hinzufügen“](./media/mdm-authority-set/add-mdm-authority.png)

### <a name="migrate-users-and-devices-optional"></a>Migrieren von Benutzern und Geräten (optional)

Nachdem die Intune-MDM-Autorität aktiviert ist, wird die Koexistenz aktiviert, und Sie können mit der Verwaltung von Benutzern über Intune beginnen. Wenn Sie Geräte, die zuvor mit der Option „Grundlegende Mobilität und Sicherheit“ verwaltet wurden, der Verwaltung durch Intune zuordnen möchten, weisen Sie diesen Benutzern optional eine Intune-Lizenz zu. Die Geräte der Benutzer werden beim nächsten MDM-Einchecken an Intune übertragen. Über „Basic Mobility and Security“ auf diese Geräte angewendete Einstellungen werden nicht mehr angewendet und von den Geräten entfernt.

## <a name="mobile-device-cleanup-after-mdm-certificate-expiration"></a>Bereinigen mobiler Geräte nach Ablauf des MDM-Zertifikats

Das MDM-Zertifikat wird automatisch erneuert, wenn mobile Geräte mit dem Intune-Dienst kommunizieren. Wenn mobile Geräte zurückgesetzt werden oder für längere Zeit keine Kommunikation mit dem Intune-Dienst stattfindet, wird das MDM-Zertifikat nicht erneuert. Das Gerät wird 180 Tage nach Ablauf des MDM-Zertifikats aus dem Azure-Portal entfernt.

## <a name="remove-mdm-authority"></a>Entfernen der MDM-Autorität

Die MDM-Autorität kann nicht in „Unbekannt“ geändert werden. Der Dienst verwendet die MDM-Autorität, um zu bestimmen, an welches Portal diese registrierten Geräte melden (Microsoft Intune oder Basic Mobility and Security for Microsoft 365).

## <a name="what-to-expect-after-changing-the-mdm-authority"></a>Was passiert nach der Umstellung der MDM-Autorität

- Wenn der Intune-Dienst erkennt, dass die MDM-Autorität eines Mandanten umgestellt wurde, sendet er eine Benachrichtigung an alle registrierten Geräte, damit sie beim Dienst eingecheckt und synchronisiert werden (diese Benachrichtigung befindet sich außerhalb der regelmäßig geplanten Eincheckvorgänge). Daher werden nach der Umstellung der MDM-Autorität für den Mandanten von eigenständigem Intune alle eingeschalteten und online befindlichen Geräte mit dem Dienst verbunden. Sie empfangen die neue MDM-Autorität und werden von ihr verwaltet. Verwaltung und Schutz dieser Geräte werden nicht unterbrochen.
- Selbst für Geräte, die während (oder kurz nach) der Umstellung der MDM-Autorität eingeschaltet und online sind, gibt es eine Verzögerung von bis zu acht Stunden (je nach Zeitpunkt des nächsten geplanten regulären Eincheckvorgangs), bevor Geräte unter der neuen MDM-Autorität beim Dienst registriert werden.  

 > [!IMPORTANT]  
 > In der Zeit zwischen der Umstellung der MDM-Autorität und dem Hochladen des erneuerten APNs-Zertifikats in die neue Autorität schlagen neue Registrierungen und Eincheckvorgänge für iOS/iPadOS-Geräte fehl. Aus diesem Grund ist es wichtig, dass Sie das APNs-Zertifikat so bald wie möglich nach der Umstellung der MDM-Autorität überprüfen und in die neue Autorität hochladen.

- Benutzer können schnell auf die neue MDM-Autorität umstellen, indem sie manuell einen Eincheckvorgang des Geräts beim Dienst starten. Benutzer können diese Änderung problemlos mithilfe der Unternehmensportal-App und durch Starten einer Überprüfung der Gerätekonformität vornehmen.
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