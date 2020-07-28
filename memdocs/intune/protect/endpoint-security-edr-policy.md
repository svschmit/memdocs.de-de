---
title: Verwalten der Einstellungen für Endpunkterkennung- und -antwort mit Endpunktsicherheitsrichtlinien in Microsoft Intune | Microsoft-Dokumentation
description: Konfigurieren und Bereitstellen von Richtlinien für Geräte, die Sie mithilfe einer Endpunkterkennungs- und -antwort-Richtlinie in Microsoft Endpoint Manager verwalten.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: b1711dad8163409d05c5299e8d3b54ad619b48ec
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2020
ms.locfileid: "86462064"
---
# <a name="endpoint-detection-and-response-policy-for-endpoint-security-in-intune"></a>Endpunkterkennungs- und -antwort-Richtlinie für die Endpunktsicherheit in Intune

Wenn Sie Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) in Intune integrieren, können Sie Endpunktsicherheitsrichtlinien für die Endpunkterkennung und -antwort (Endpoint Detection and Response, EDR) verwenden, um die EDR-Einstellungen zu verwalten und das Onboarding von Geräten für Microsoft Defender ATP durchzuführen.

Die Funktionen der Endpunkterkennung- und -antwort von Microsoft Defender ATP bieten erweiterte Angriffserkennungen, die nahezu in Echtzeit erfolgen und aussagekräftig sind. Sicherheitsanalysten können damit Warnungen effektiv priorisieren, Einblicke in den gesamten Umfang einer Sicherheitsverletzung erhalten und Antwortaktionen durchführen, um Bedrohungen abzuwenden.

EDR-Richtlinien enthalten plattformspezifische Profile zum Verwalten der EDR-Einstellungen. Die Profile enthalten automatisch ein *Onboardingpaket* für Microsoft Defender ATP. Die Onboardingpakete bestimmen, wie Geräte konfiguriert werden, damit sie mit Microsoft Defender ATP funktionieren. Nach dem Onboarding eines Geräts können Sie mit der Verwendung von Bedrohungsdaten von diesem Gerät beginnen.

Die EDR-Richtlinien werden für Gruppen von Geräten in Azure Active Directory (Azure AD) bereitgestellt, die Sie mit Intune verwalten, sowie für Sammlungen von lokalen Geräten, die Sie mit Configuration Manager verwalten, einschließlich Windows-Servern. Die EDR-Richtlinien für die verschiedenen Verwaltungspfade erfordern unterschiedliche Onboardingpakete. Daher erstellen Sie getrennte EDR-Richtlinien für die verschiedenen Arten der von Ihnen verwalteten Geräte.

Die Endpunktsicherheitsrichtlinien für EDR finden Sie unter *Verwalten* im Knoten **Endpunktsicherheit** des [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).

Rufen Sie die [Einstellungen für Endpunkterkennungs- und -antwort-Profile](endpoint-security-edr-profile-settings.md) auf.

## <a name="prerequisites-for-edr-policies"></a>Voraussetzungen für EDR-Richtlinien

**Allgemein:**

- **Mandant für Microsoft Defender Advanced Threat Protection**: Ihr Microsoft Defender ATP-Mandant muss in Ihren Microsoft Endpoint Manager-Mandanten (Intune-Abonnement) integriert werden, bevor Sie EDR-Richtlinien erstellen können. Weitere Informationen finden Sie in [Verwenden von Microsoft Defender ATP](advanced-threat-protection.md) in der Intune-Dokumentation.

**So unterstützen Sie Geräte aus Configuration Manager**:

Um die Verwendung von EDR-Richtlinien mit Configuration Manager-Geräten zu unterstützen, sind für Ihre Configuration Manager-Umgebung die folgenden zusätzlichen Konfigurationen erforderlich. Eine [Anleitung für die Konfiguration](#set-up-configuration-manager-to-support-edr-policy) finden Sie in diesem Artikel:

- **Configuration Manager mit Version 2002 oder höher** – An Ihrem Standort muss Configuration Manager 2002 oder höher ausgeführt werden.

- **Installieren des Configuration Manager-Updates** – Um in Configuration Manager 2002 die Unterstützung für die Verwendung der im Microsoft Endpoint Manager Admin Center erstellten EDR-Richtlinie zu aktivieren, installieren Sie das folgende Update in der Configuration Manager-Konsole:
  - **Configuration Manager 2002 Hotfix (KB4563473)**

- **Konfigurieren der Mandantenanfügung** – Die Mandantenanfügung ermöglicht Ihnen das Synchronisieren von Gerätesammlungen aus Configuration Manager mit dem Microsoft Endpoint Manager Admin Center. Sie können dann das Admin Center verwenden, um EDR-Richtlinien für diese Sammlungen bereitzustellen.

  Die Mandantenanfügung wird häufig zusammen mit der Co-Verwaltung konfiguriert, aber Sie können die Mandantenanfügung auch eigenständig konfigurieren.

- **Synchronisieren von Configuration Manager-Sammlungen** – Wenn Sie die Mandantenanfügung konfigurieren, können Sie die Configuration Manager-Gerätesammlungen auswählen, die mit dem Microsoft Endpoint Manager Admin Center synchronisiert werden sollen. Sie können die zum Synchronisieren vorgesehenen Gerätesammlungen auch später noch ändern. Die EDR-Richtlinie für Configuration Manager Geräte kann nur Sammlungen zugewiesen werden, die Sie synchronisiert haben.

  Nachdem Sie die zu synchronisierenden Sammlungen ausgewählt haben, müssen Sie diese für die Verwendung mit Microsoft Defender ATP aktivieren.

- **Berechtigungen für Azure AD** – Sie benötigen ein Konto mit globalen Administratorberechtigungen für Ihr Azure-Abonnement, um die Einrichtung der Mandantenanfügung abzuschließen und um die Configuration Manager-Sammlungen zu konfigurieren, die Sie mit dem Microsoft Endpoint Manager Admin Center synchronisieren wollen.

## <a name="edr-profiles"></a>EDR-Profile

[Sehen Sie sich die Einstellungen an](endpoint-security-edr-profile-settings.md), die Sie für die folgenden Plattformen und Profile konfigurieren können.

**Intune** – Die folgenden Aktionen werden für Geräte unterstützt, die Sie mit Intune verwalten:

- Plattform: **Windows 10 und höher** – Intune stellt die Richtlinie für Geräte in ihren Azure AD-Gruppen bereit.
- Profil: **Endpunkterkennung und -antwort (MDM)**

**Configuration Manager:** Folgendes wird für Geräte unterstützt, die Sie mit Configuration Manager verwalten:

- Plattform: **Windows 10 und Windows Server** – Configuration Manager stellt die Richtlinie für Geräte in Ihren Configuration Manager-Sammlungen bereit.
- Profil: **Endpunkterkennung und -antwort (ConfigMgr)**

## <a name="set-up-configuration-manager-to-support-edr-policy"></a>Einrichten von Configuration Manager zur Unterstützung der EDR-Richtlinie

Bevor Sie EDR-Richtlinien für Configuration Manager-Geräte bereitstellen können, schließen Sie die in den folgenden Abschnitten beschriebenen Konfigurationen ab.

Diese Konfigurationen werden innerhalb der Configuration Manager-Konsole und für Ihre Configuration Manager-Bereitstellung vorgenommen. Wenn Sie mit Configuration Manager nicht vertraut sind, planen Sie die Arbeit mit einem Configuration Manager-Administrator ein, um diese Aufgaben durchzuführen.  

In den folgenden Abschnitten werden die erforderlichen Aufgaben behandelt:

1. [Installieren des Updates für Configuration Manager](#task-1-install-the-update-for-configuration-manager)
2. [Aktivieren der Mandantenanfügung](#task-2-configure-tenant-attach-and-synchronize-collections)  
3. [Auswählen der zu synchronisierenden Sammlungen](#task-3-select-collections-to-synchronize)
4. [Aktivieren von Sammlungen für Microsoft Defender ATP](#task-4-enable-collections-for-microsoft-defender-atp)

> [!TIP]
> Weitere Informationen zur Verwendung von Microsoft Defender ATP mit Configuration Manager finden Sie in den folgenden Artikeln des Configuration Manager-Inhalts:
>
> - [Durchführen des Onboardings für Configuration Manager-Clients in Microsoft Defender ATP über das Microsoft Endpoint Manager Admin Center](../../configmgr/core/get-started/2020/technical-preview-2003.md#bkmk_atp)
> - [Anfügen von Mandanten in Microsoft Endpoint Manager: Gerätesynchronisierung und Geräteaktionen](../../configmgr/core/get-started/2020/technical-preview-2002-2.md#bkmk_attach).

### <a name="task-1-install-the-update-for-configuration-manager"></a>Aufgabe 1: Installieren des Updates für Configuration Manager

Configuration Manager Version 2002 erfordert ein Update zur Unterstützung der Verwendung mit Endpunkterkennungs- und -antwort-Richtlinien, die Sie über das Microsoft Endpoint Manager Admin Center bereitstellen.

**Updatedetails**:

- **Configuration Manager 2002 Hotfix (KB4563473)**

Sie finden dieses Update als *konsoleninternes Update* für Configuration Manager 2002.

Befolgen Sie zum Installieren dieses Updates die Anleitung unter [Installieren konsoleninterner Updates](../../configmgr/core/servers/manage/install-in-console-updates.md) in der Configuration Manager-Dokumentation.

Kehren Sie nach der Installation des Updates hierher zurück, um die Konfiguration Ihrer Umgebung für die Unterstützung der EDR-Richtlinie über das Microsoft Endpoint Manager Admin Center fortzusetzen.

### <a name="task-2-configure-tenant-attach-and-synchronize-collections"></a>Aufgabe 2: Konfigurieren von Mandantenanfügung und Synchronisieren von Sammlungen

Wenn die Co-Verwaltung zuvor aktiviert war, ist die Mandantenanfügung bereits eingerichtet, und Sie können mit [Aufgabe 3](#task-3-select-collections-to-synchronize) fortfahren.

Mit der Mandantenanfügung geben Sie Sammlungen von Geräten aus Ihrer Configuration Manager-Bereitstellung an, die mit dem Microsoft Endpoint Manager Admin Center synchronisiert werden sollen. Verwenden Sie nach der Synchronisierung von Sammlungen das Admin Center, um Informationen zu diesen Geräten anzuzeigen und ihnen eine EDR-Richtlinie aus Intune bereitzustellen.  

Weitere Informationen zum Szenario der Mandantenanfügung finden Sie unter [Aktivieren der Mandantenanfügung](../../configmgr/tenant-attach/device-sync-actions.md) im Configuration Manager-Inhalt.

#### <a name="enable-tenant-attach-when-co-management-hasnt-been-enabled"></a>Aktivieren der Mandantenanfügung, wenn die Co-Verwaltung noch nicht aktiviert wurde

> [!TIP]
> Mit dem **Konfigurationsassistenten für die Co-Verwaltung** in der Configuration Manager-Konsole aktivieren Sie die Mandantenanfügung. Die Co-Verwaltung müssen Sie jedoch nicht aktivieren.

Wenn Sie beabsichtigen, die Co-Verwaltung zu aktivieren, sollten Sie sich mit der Co-Verwaltung, den Voraussetzungen dafür und mit der Verwaltung von Workloads vertraut machen, bevor Sie fortfahren. Weitere Informationen finden Sie unter [Was ist Co-Verwaltung?](../../configmgr/comanage/overview.md) in der Configuration Manager-Dokumentation.

1. Navigieren Sie in der Configuration Manager-Administratorkonsole zu **Verwaltung** > **Übersicht** > **Clouddienste** > **Co-Verwaltung**.
2. Klicken Sie im Menüband auf **Configure co-management** (Co-Verwaltung konfigurieren), um den Assistenten zu öffnen.
3. Wählen Sie auf der Seite **Onboarding von Mandanten** **AzurePublicCloud** als Umgebung aus. Azure Government-Clouds werden nicht unterstützt.
   1. Klicken Sie auf **Anmelden**. Melden Sie sich mit Ihrem *globalen Administratorkonto* an.

   2. Stellen Sie sicher, dass auf der Seite **Onboarding von Mandanten** die Option **Upload ins Microsoft Endpoint Manager Admin Center** aktiviert ist.

   3. Entfernen Sie das Kästchen bei **Automatische Clientregistrierung für Co-Verwaltung aktivieren**.

      Wenn diese Option ausgewählt ist, zeigt der Assistent zusätzliche Seiten an, um die Einrichtung der Co-Verwaltung abzuschließen. Weitere Informationen finden Sie unter [Aktivieren der Co-Verwaltung](../../configmgr/comanage/how-to-enable.md) im Configuration Manager-Inhalt.

     ![Konfigurieren der Mandantenanfügung](media/endpoint-security-edr-policy/tenant-onboarding.png)

4. Klicken Sie auf **Weiter** und dann auf **Ja**, um die Meldung **AAD-Anwendung erstellen** zu akzeptieren. Diese Aktion stellt einen Dienstprinzipal bereit und erstellt eine Azure AD-Anwendungsregistrierung, um die Synchronisierung von Sammlungen mit dem Microsoft Endpoint Manager Admin Center zu vereinfachen.

5. Konfigurieren Sie auf der Seite **Upload konfigurieren**, welche Sammlungen synchronisiert werden sollen. Sie können Ihre Konfiguration auf eine oder mehrere Gerätesammlungen beschränken oder die empfohlene Einstellung für den Geräte-Upload für **Alle mit Microsoft Endpoint Configuration Manager verwalteten Geräte** verwenden.

6. Klicken Sie auf **Zusammenfassung**, um Ihre Auswahl zu überprüfen, und klicken Sie dann auf **Weiter**.

7. Klicken Sie auf **Schließen**, wenn der Assistent abgeschlossen ist.

   Damit ist die Mandantenanfügung konfiguriert, und die ausgewählten Sammlungen werden mit dem Microsoft Endpoint Manager Admin Center synchronisiert.

#### <a name="enable-tenant-attach-when-you-use-co-management"></a>Aktivieren der Mandantenanfügung bei Verwendung der Co-Verwaltung

1. Navigieren Sie in der Configuration Manager-Administratorkonsole zu **Verwaltung** > **Übersicht** > **Clouddienste** > **Co-Verwaltung**.

2. Klicken Sie mit der rechten Maustaste auf die Co-Verwaltungseinstellungen und dann auf **Eigenschaften**.

3. Klicken Sie in der Registerkarte **Configure upload** (Upload konfigurieren) auf **Upload to Microsoft Endpoint Manager admin center** (Upload ins Microsoft Endpoint Manager Admin Center). Klicken Sie auf **Übernehmen**.
   - Die Standardeinstellung für den Upload von Geräten ist **All my devices managed by Microsoft Endpoint Configuration Manager** (Alle von Microsoft Endpoint Configuration Manager verwalteten Geräte). Sie können auch festlegen, dass die Konfiguration auf eine oder mehrere Gerätesammlungen beschränkt werden soll.

     ![Anzeigen der Registerkarte „Eigenschaften der Co-Verwaltung“](media/endpoint-security-edr-policy/configure-upload.png)

4. Melden Sie sich mit Ihrem *globalen Administratorkonto* an, wenn Sie dazu aufgefordert werden.

5. Klicken Sie auf **Ja**, um die Meldung **AAD-Anwendung erstellen** zu akzeptieren. Durch diese Aktion wird ein Dienstprinzipal bereitgestellt und eine Azure AD-Anwendungsregistrierung erstellt, um das Synchronisieren zu vereinfachen.

6. Klicken Sie auf **OK**, um die Eigenschaften für die Co-Verwaltung zu verlassen, sobald Sie alle Änderungen vorgenommen haben.

   Damit ist die Mandantenanfügung konfiguriert, und die ausgewählten Sammlungen werden mit dem Microsoft Endpoint Manager Admin Center synchronisiert.

### <a name="task-3-select-collections-to-synchronize"></a>Aufgabe 3: Auswählen der zu synchronisierenden Sammlungen

Wenn die Mandantenanfügung konfiguriert ist, können Sie die Sammlungen für die Synchronisierung auswählen. Wenn Sie noch keine Sammlungen synchronisiert haben oder die zu synchronisierenden Sammlungen neu konfigurieren müssen, können Sie zu diesem Zweck die Eigenschaften der Co-Verwaltung in der Configuration Manager-Konsole bearbeiten.

#### <a name="select-collections"></a>Auswählen der Sammlungen

1. Navigieren Sie in der Configuration Manager-Administratorkonsole zu **Verwaltung** > **Übersicht** > **Clouddienste** > **Co-Verwaltung**.

2. Klicken Sie mit der rechten Maustaste auf die Co-Verwaltungseinstellungen und dann auf **Eigenschaften**.

3. Klicken Sie in der Registerkarte **Configure upload** (Upload konfigurieren) auf **Upload to Microsoft Endpoint Manager admin center** (Upload ins Microsoft Endpoint Manager Admin Center). Klicken Sie auf **Übernehmen**.

   Die Standardeinstellung für den Upload von Geräten ist **All my devices managed by Microsoft Endpoint Configuration Manager** (Alle von Microsoft Endpoint Configuration Manager verwalteten Geräte). Sie können auch festlegen, dass die Konfiguration auf eine oder mehrere Gerätesammlungen beschränkt werden soll.

### <a name="task-4-enable-collections-for-microsoft-defender-atp"></a>Aufgabe 4: Aktivieren von Sammlungen für Microsoft Defender ATP

Nachdem Sie Sammlungen für die Synchronisierung mit dem Microsoft Endpoint Manager Admin Center konfiguriert haben, müssen Sie diese Sammlungen noch für das Onboarding-und für Microsoft Defender ATP-Richtlinien aktivieren.  Zu diesem Zweck bearbeiten Sie die Eigenschaften der einzelnen Sammlungen in der Configuration Manager Konsole.

#### <a name="enable-collections-for-use-with-advanced-threat-protection"></a>Aktivieren von Sammlungen für die Verwendung mit Advanced Threat Protection

1. Klicken Sie in einer Configuration Manager Konsole, die mit dem Standort der obersten Ebene verbunden ist, mit der rechten Maustaste auf eine Gerätesammlung, die Sie mit Microsoft Endpoint Manager Admin Center synchronisieren, und wählen Sie **Eigenschaften** aus.

2. Aktivieren Sie auf der Registerkarte **Cloud Sync** (Cloudsynchronisierung) die Option **Make this collection available to assign Microsoft Defender ATP policies in Intune** (Diese Sammlung zum Zuweisen von Microsoft Defender ATP-Richtlinien in Intune zur Verfügung stellen).

   - Sie können diese Option nicht auswählen, wenn Ihre Configuration Manager-Hierarchie nicht mit einem Mandanten verbunden ist.
  
   ![Konfigurieren der Cloudsynchronisierung](media/endpoint-security-edr-policy/cloud-sync.png)

3. Klicken Sie auf **OK**, um die Konfiguration zu speichern.

   Die Geräte in dieser Sammlung können jetzt die Microsoft Defender ATP-Richtlinie erhalten.

## <a name="create-and-deploy-edr-policies"></a>Erstellen und Bereitstellen von EDR-Richtlinien

Wenn Ihr Microsoft Defender ATP-Abonnement in Intune integriert ist, können Sie EDR-Richtlinien erstellen und bereitstellen. Es gibt zwei verschiedene Typen von EDR-Richtlinien, die Sie erstellen können. Ein Richtlinientyp für Geräte, die Sie über MDM mit Intune verwalten. Der zweite Typ ist für Geräte, die Sie mit Configuration Manager verwalten.

Sie wählen den Typ der Richtlinie aus, die Sie beim Erstellen einer neuen EDR-Richtlinie erstellen, wenn Sie die Plattform für die Richtlinie auswählen.

Bevor Sie Richtlinien für Geräte bereitstellen können, die von Configuration Manager verwaltet werden, müssen Sie den Schritt [Einrichten von Configuration Manager zur Unterstützung der EDR-Richtlinie](#set-up-configuration-manager-to-support-edr-policy) aus dem Microsoft Endpoint Manager Admin Center durchführen.

### <a name="create-edr-policies"></a>Erstellen von EDR-Richtlinien

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Endpoint Security-**  > **Endpunkterkennung und -antwort** > **Richtlinie erstellen** aus.

3. Wählen Sie die Plattform und das Profil für Ihre Richtlinie aus. Die folgenden Informationen zeigen, welche Optionen Sie dabei haben:

   - Intune – Intune stellt die Richtlinie für Geräte in ihren Azure AD Gruppen bereit. Wenn Sie die Richtlinie erstellen, wählen Sie Folgendes aus:
     - Plattform: **Windows 10 und höher**
     - Profil: **Endpunkterkennung und -antwort (MDM)**

   - Configuration Manager – Der Configuration Manager stellt die Richtlinie für Geräte in Ihren Configuration Manager-Sammlungen bereit. Wenn Sie die Richtlinie erstellen, wählen Sie Folgendes aus:
     - Plattform: **Windows 10 und Windows Server**:
     - Profil: **Endpunkterkennung und -antwort (ConfigMgr)**

4. Wählen Sie **Erstellen** aus.

5. Geben Sie auf der Seite **Grundeinstellungen** einen Namen und eine Beschreibung für das Profil ein, und klicken Sie dann auf **Weiter**.

6. Konfigurieren Sie auf der Seite **Konfigurationseinstellungen** die Einstellungen, die Sie mit diesem Profil verwalten möchten. Das Onboardingpaket ist automatisch enthalten und kann nicht konfiguriert werden.

   Wenn Sie fertig sind mit dem Konfigurieren der Einstellungen, klicken Sie auf **Weiter**.

7. *Dieser Schritt gilt nur für das Profil **Endpunkterkennung und -antwort (MDM)***:  

   Klicken Sie auf der Seite **Bereichstags** auf **Bereichstags auswählen**, um das Fenster *Tags auswählen* zu öffnen, in dem Sie dem Profil Bereichstags zuweisen.
  
   Wählen Sie **Weiter** aus, um den Vorgang fortzusetzen.

8. Wählen Sie auf der Seite **Zuweisungen** die Gruppen aus, die dieses Profil erhalten sollen. Die Auswahl hängt von der Plattform und dem Profil ab, die Sie ausgewählt haben:

   - Für Intune wählen Sie Gruppen aus Azure AD aus.
   - Für Configuration Manager wählen Sie Sammlungen aus Configuration Manager aus, die Sie mit dem Microsoft Endpoint Manager Admin Center synchronisiert und für die Microsoft Defender ATP-Richtlinie aktiviert haben.

   Sie können zu diesem Zeitpunkt auch keine Gruppen oder Sammlungen zuzuweisen, und die Richtlinie später bearbeiten, um eine Zuweisung hinzuzufügen.

   Klicken Sie auf **Weiter**, wenn Sie bereit sind fortzufahren.

9. Klicken Sie, wenn Sie fertig sind, auf der Seite **Bewerten + erstellen** auf **Erstellen**.

   Das neue Profil wird in der Liste angezeigt, wenn Sie den Richtlinientyp für das Profil auswählen, das Sie erstellt haben.

## <a name="edr-policy-reports"></a>Berichte zu EDR-Richtlinien

Details zu den von Ihnen bereitgestellten EDR-Richtlinien können Sie im Microsoft Endpoint Manager Admin Center anzeigen. Um Details anzuzeigen, wechseln Sie zu **Endpoint Security-**  > **Endpunktbereitstellung und -antwort**, und wählen Sie eine Richtlinie aus, für die Sie Konformitätsdetails anzeigen möchten:

- Für Richtlinien, die auf die Plattform **Windows 10 und höher** (Intune) ausgerichtet sind, wird eine Übersicht über die Konformität der Richtlinie angezeigt. Sie können auch das Diagramm auswählen, um eine Liste der Geräte anzuzeigen, die die Richtlinie erhalten haben, und einen Drilldown zu einzelnen Geräten durchführen, um weitere Informationen zu erhalten.

  Im Diagramm **Geräte mit ATP-Sensor** werden nur Geräte angezeigt, deren Onboarding in Microsoft Defender ATP erfolgreich über das Profil **Windows 10 und höher** erfolgt ist. Um sicherzustellen, dass Sie über eine vollständige Darstellung Ihrer Geräte in diesem Diagramm verfügen, müssen Sie das Onboardingprofil auf allen Ihren Geräten bereitstellen. Geräte, deren Onboarding in Microsoft Defender ATP mithilfe externer Methoden erfolgte, etwa durch Gruppenrichtlinie oder PowerShell, gelten als **Geräte ohne ATP-Sensor**.

- Für Richtlinien, die auf die Plattform **Windows 10-und Windows Server** (Configuration Manager) ausgerichtet sind, wird eine Übersicht über die Konformität der Richtlinie angezeigt, aber es kann kein Drilldown durchgeführt werden, um weitere Details anzuzeigen. Die Ansicht ist begrenzt, da das Admin Center eingeschränkte Statusdetails vom Configuration Manager empfängt, der die Bereitstellung der Richtlinie auf Configuration Manager-Geräten verwaltet.


[Sehen Sie sich die Einstellungen an](endpoint-security-edr-profile-settings.md), die Sie für Plattformen und Profile konfigurieren können.

## <a name="next-steps"></a>Nächste Schritte

- [Konfigurieren von Endpunktsicherheitsrichtlinien](endpoint-security-policy.md#create-an-endpoint-security-policy)
- Weitere Informationen zur [Endpunkterkennung und -antwort](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response) finden Sie in der Dokumentation zu Microsoft Defender ATP.
