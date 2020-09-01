---
title: 'Azure: Gerätekonformitätsrichtlinien in Microsoft Intune | Microsoft-Dokumentation'
description: Verwenden Sie Drittanbieter-Gerätekonformitätspartner als Konformitätsdatenquelle für Geräte, die Sie mit Intune verwalten.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/17/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.reviewer: samyada
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fe6a46c10f55378292e57548494852c4014c062a
ms.sourcegitcommit: 21b6c0c054e5371f32d611a2411ccd166b0e03bc
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88643702"
---
# <a name="support-third-party-device-compliance-partners-in-intune"></a>Unterstützung von Drittanbieter-Gerätekonformitätspartnern in Intune

Microsoft Intune kann Konformitätszustandsdaten für die Geräte, die Sie mit mindestens einem Drittanbieter-Gerätekonformitätspartner verwalten, zu Azure Active Directory hinzufügen. Mit dieser Konfiguration können Konformitätsdaten dieser Geräte mit Ihren Richtlinien für bedingten Zugriff verwendet werden.

Intune ist standardmäßig als MDM-Autorität (Mobile Device Management, mobile Geräteverwaltung) für Ihre Geräte eingerichtet. Wenn Sie einen Konformitätspartner zu Azure AD und Intune hinzufügen, konfigurieren Sie diesen Partner als Quelle der MDM-Autorität für die Geräte, die Sie dem Partner über eine Azure AD-Benutzergruppe zuweisen.

Führen Sie die folgenden Aufgaben durch, um die Verwendung der Daten von Gerätekonformitätspartner zu ermöglichen:

1. **Konfigurieren Sie Intune für die Zusammenarbeit mit dem Gerätekonformitätspartner**, und konfigurieren Sie dann die Gruppen der Benutzer, deren Geräte von diesem Konformitätspartner verwaltet werden.

2. **Konfigurieren Sie Ihren Konformitätspartner zum Senden von Daten an Intune**.

3. **Registrieren Sie Ihre iOS- oder Android-Geräte bei dem Gerätekonformitätspartner**.

Sobald Sie diese Aufgaben abgeschlossen haben, sendet der Gerätekonformitätspartner Informationen zum Gerätezustand an Intune. Intune fügt diese Informationen dann zu Azure AD hinzu. Beispielsweise wird der Zustand von nicht konformen Geräten zu ihrem Gerätedatensatz in Azure AD hinzugefügt.

Der Konformitätszustand wird dann von Richtlinien für bedingten Zugriff auf dieselbe Weise ausgewertet wie die Konformitätszustandsdaten für von Intune verwaltete Geräte.  Intune ist ein standardmäßig registrierter Konformitätspartner für iOS und Android. Wenn Sie zusätzliche Partner hinzufügen, können Sie die Prioritätsreihenfolge festlegen, um sicherzustellen, dass der richtige Partner die Geräte gemäß Ihrer geschäftlichen Anforderungen verwaltet.

## <a name="supported-device-compliance-partners"></a>Unterstützte Gerätekonformitätspartner

In der öffentlichen Vorschau:

- VMware Workspace ONE UEM (früher AirWatch)

## <a name="prerequisites"></a>Voraussetzungen

- Ein Abonnement für Microsoft Intune und Zugriff auf das [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431)

- Ein Abonnement beim Gerätekonformitätspartner

- Informationen zu unterstützten Geräteplattformen und zusätzlichen Voraussetzungen finden Sie in der Dokumentation Ihrs Konformitätspartners.

## <a name="configure-intune-to-work-with-a-device-compliance-partner"></a>Konfigurieren von Intune zur Zusammenarbeit mit einem Gerätekonformitätspartner

Aktivieren Sie die Unterstützung für einen Gerätekonformitätspartner, wenn Sie Konformitätszustandsdaten von diesem Partner mit Ihren Richtlinien für bedingten Zugriff verwenden möchten.

### <a name="add-a-compliance-partner-to-intune"></a>Hinzufügen eines Konformitätspartners zu Intune

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Navigieren Sie zu **Mandantenverwaltung** > **Connectors und Token** > **Partnerkonformitätsverwaltung** > **Konformitätspartner hinzufügen**.

   > [!div class="mx-imgBorder"]
   > ![Hinzufügen eines Gerätekonformitätspartners](./media/device-compliance-partners/add-compliance-partner.png)

3. Erweitern Sie auf der Seite **Grundlegende Einstellungen** die Dropdownliste **Konformitätspartner**, und wählen Sie den Partner aus, den Sie hinzufügen möchten.

   - Um VMware Workspace ONE als Konformitätspartner für iOS- oder Android-Plattformen zu verwenden, wählen Sie **VMware Workspace ONE – mobile Konformität** aus.

   Klicken Sie als Nächstes auf die Dropdownliste **Plattform**, und wählen Sie die Plattform aus. macOS wird in dieser Vorschau nicht unterstützt.

   Selbst wenn Sie mehrere Konformitätspartner zu Azure AD hinzugefügt haben, sind Sie auf einen einzelnen Partner pro Plattform beschränkt.

4. Wählen Sie unter **Zuweisungen** die Benutzergruppen aus, deren Geräte von diesem Partner verwaltet werden sollen. Durch diese Zuweisung ändern Sie die MDM-Autorität für zulässige Geräte zur Verwendung dieses Partners. Benutzern, deren Geräte vom Partner verwaltet werden, muss ebenfalls eine Lizenz für Intune zugewiesen werden.

5. Überprüfen Sie Ihre Konfiguration auf der Seite **Überprüfen + erstellen**, und klicken Sie dann auf **Erstellen**, um die Konfiguration abzuschließen.

Ihre Konfiguration erscheint nun auf der Seite „Partnerkonformitätsverwaltung“.

### <a name="modify-the-configuration-for-a-compliance-partner"></a>Ändern der Konfiguration für einen Konformitätspartner

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Navigieren Sie zu **Mandantenverwaltung** > **Connectors und Tokens** > **Partnerkonformitätsverwaltung**, und wählen Sie dann die Partnerkonfiguration aus, die Sie ändern möchten. Die Konfigurationen werden nach Plattformtyp sortiert.

3. Klicken Sie auf der Seite **Übersicht** der Partnerkonfiguration auf **Eigenschaften**, um die Seite „Eigenschaften“ zu öffnen, auf der Sie die Zuweisungen bearbeiten können.

4. Klicken Sie auf der Seite **Eigenschaften** auf **Bearbeiten**, um die Ansicht „Zuweisungen“ zu öffnen, in der Sie die Gruppen ändern können, die diese Konfiguration verwenden.

5. Klicken Sie auf **Überprüfen + speichern** und dann auf **Speichern**, um Ihre Änderungen zu speichern.

6. *Dieser Schritt gilt nur, wenn Sie VMware Workspace ONE verwenden*:

   Sie müssen die Änderungen, die Sie im Admin Center von Microsoft Endpoint Manager gespeichert haben, manuell über die Workspace ONE UEM-Konsole synchronisieren. Bevor Sie die Änderungen manuell synchronisieren, hat Workspace ONE UEM keine Kenntnis der Konfigurationsänderungen, daher wird für Benutzer in von Ihnen zugewiesenen neuen Gruppen keine Konformität gemeldet.

   So synchronisieren Sie Änderungen von Azure-Diensten manuell:
   1. Melden Sie sich bei Ihrer VMware Workspace ONE UEM-Konsole an.
   2. Wechseln Sie zu **Settings** > **System** > **Enterprise Integration** > **Directory Services** (Einstellungen > System > Unternehmensintegration > Verzeichnisdienste).
   3. Klicken Sie unter *Sync Azure Services* (Azure-Dienste synchronisieren) auf **SYNC**.

      Alle Änderungen, die Sie seit der anfänglichen Konfiguration oder der letzten manuellen Synchronisierung vorgenommen haben, werden von Azure-Diensten mit UEM synchronisiert.  

## <a name="configure-your-compliance-partner-to-work-with-intune"></a>Konfigurieren Ihres Konformitätspartner zur Zusammenarbeit mit Intune

Damit ein Gerätekonformitätspartner mit Intune zusammenarbeiten kann, müssen Sie spezifische Konfigurationen für den jeweiligen Partner vornehmen. Informationen zu dieser Aufgabe finden Sie in der Dokumentation des jeweiligen Partners:

- [VMware Workspace ONE UEM](https://docs.vmware.com/en/VMware-Workspace-ONE-UEM/services/Directory_Service_Integration/GUID-800FB831-AA66-4094-8F5A-FA5899A3C70C.html)  

## <a name="enroll-your-ios-or-android-devices-to-that-device-compliance-partner"></a>Registrieren Sie Ihre iOS- oder Android-Geräte bei dem Gerätekonformitätspartner.

Informationen zum Registrieren von Geräten mit dem Partner finden Sie in den Dokumentationen der Gerätekonformitätspartner. Nachdem Geräte registriert und die Konformitätsdaten an den Partner übermittelt wurden, werden diese Konformitätsdaten an Intune weitergeleitet und zu Azure AD hinzugefügt.

## <a name="monitor-devices-managed-by-third-party-device-compliance-partners"></a>Überwachen der von Drittanbieter-Gerätekonformitätsanbietern verwalteten Geräte

Nachdem Sie Drittanbieter-Gerätekonformitätsanbieter konfiguriert und Geräte mit diesen bereitgestellt haben, leitet der Partner Konformitätsinformationen an Intune weiter. Sobald Intune diese Daten empfangen hat, können Sie Informationen zu den Geräten im Azure-Portal anzeigen.

Melden Sie sich beim Azure-Portal an, und wechseln Sie zu **Azure AD** > **Geräte** > [**Alle Geräte**](https://portal.azure.com/#blade/Microsoft_AAD_Devices/DevicesMenuBlade/Devices/menuId/).

## <a name="next-steps"></a>Nächste Schritte

Nutzen Sie die Dokumentation Ihres Drittanbieterpartners, um Konformitätsrichtlinien für Geräte zu erstellen.

- [VMware Workspace ONE UEM](https://docs.vmware.com/en/VMware-Workspace-ONE-UEM/services/Directory_Service_Integration/GUID-800FB831-AA66-4094-8F5A-FA5899A3C70C.html)
