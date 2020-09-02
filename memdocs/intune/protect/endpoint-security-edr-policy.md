---
title: Verwalten der Einstellungen für Endpunkterkennung- und -antwort mit Endpunktsicherheitsrichtlinien in Microsoft Intune | Microsoft-Dokumentation
description: Konfigurieren und Bereitstellen von Richtlinien für Geräte, die Sie mithilfe einer Endpunkterkennungs- und -antwort-Richtlinie in Microsoft Endpoint Manager verwalten.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 08/24/2020
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
ms.openlocfilehash: ff880b564562b3e6d67dc852f97ef7a9f5d6b814
ms.sourcegitcommit: 0c7e6b9b47788930dca543d86a95348da4b0d902
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88915040"
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

**Unterstützung für Configuration Manager-Clients**:

- **Einrichten der Mandantenanfügung für Configuration Manager-Geräte**: Konfigurieren Sie die *Mandantenanfügung*, um die Bereitstellung von EDR-Richtlinien auf Geräten zu unterstützen, die von Configuration Manager verwaltet werden. Hierzu gehört auch die Konfiguration von Configuration Manager-Gerätesammlungen zur Unterstützung der Endpunktsicherheitsrichtlinien von Intune.

  Informationen zum Einrichten der Mandantenanfügung einschließlich Synchronisierung der Configuration Manager-Sammlungen mit Microsoft Endpoint Manager Admin Center und Einrichten der Sammlungen für Endpunktsicherheitsrichtlinien finden Sie unter [Konfigurieren der Mandantenanfügung zur Unterstützung von Endpunktsicherheitsrichtlinien](../protect/tenant-attach-intune.md).

## <a name="edr-profiles"></a>EDR-Profile

[Sehen Sie sich die Einstellungen an](endpoint-security-edr-profile-settings.md), die Sie für die folgenden Plattformen und Profile konfigurieren können.

**Intune** – Die folgenden Aktionen werden für Geräte unterstützt, die Sie mit Intune verwalten:

- Plattform: **Windows 10 und höher** – Intune stellt die Richtlinie für Geräte in ihren Azure AD-Gruppen bereit.
- Profil: **Endpunkterkennung und -antwort (MDM)**

**Configuration Manager:** Folgendes wird für Geräte unterstützt, die Sie mit Configuration Manager verwalten:

- Plattform: **Windows 10 und Windows Server (Configuration Manager)** : Configuration Manager stellt die Richtlinie für Geräte in Ihren Configuration Manager-Sammlungen bereit.
- Profil: **Endpunkterkennung und -antwort (ConfigMgr)**

## <a name="set-up-configuration-manager-to-support-edr-policy"></a>Einrichten von Configuration Manager zur Unterstützung der EDR-Richtlinie

Bevor Sie EDR-Richtlinien für Configuration Manager-Geräte bereitstellen können, schließen Sie die in den folgenden Abschnitten beschriebenen Konfigurationen ab.

Diese Konfigurationen werden innerhalb der Configuration Manager-Konsole und für Ihre Configuration Manager-Bereitstellung vorgenommen. Wenn Sie mit Configuration Manager nicht vertraut sind, planen Sie die Arbeit mit einem Configuration Manager-Administrator ein, um diese Aufgaben durchzuführen.  

In den folgenden Abschnitten werden die erforderlichen Aufgaben behandelt:

1. [Installieren des Updates für Configuration Manager](#task-1-install-the-update-for-configuration-manager)
2. [Aktivieren der Mandantenanfügung](#task-2-configure-tenant-attach-and-synchronize-collections)  

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

Folgendes wird für Geräte unterstützt, die Sie mit Intune verwalten:

- Plattform: **Windows 10 und höher** – Intune stellt die Richtlinie für Geräte in ihren Azure AD-Gruppen bereit.
  - Profil: **Endpunkterkennung und -antwort (MDM)**

### <a name="devices-managed-by-configuration-manager-in-preview"></a>Von Configuration Manager verwaltete Geräte *(in der Vorschau)*

Folgendes wird für Geräte unterstützt, die Sie mit Configuration Manager über das Szenario der *Mandantenanfügung* verwalten:

- Plattform: **Windows 10 und Windows Server (Configuration Manager)** : Configuration Manager stellt die Richtlinie für Geräte in Ihren Configuration Manager-Sammlungen bereit.
  - Profil: **Endpunkterkennung und -antwort (ConfigMgr) (Vorschau)**

## <a name="create-and-deploy-edr-policies"></a>Erstellen und Bereitstellen von EDR-Richtlinien

Wenn Sie Ihr Microsoft Defender ATP-Abonnement in Intune integrieren, können Sie EDR-Richtlinien erstellen und bereitstellen. Es gibt zwei verschiedene Typen von EDR-Richtlinien, die Sie erstellen können. Ein Richtlinientyp für Geräte, die Sie über MDM mit Intune verwalten. Der zweite Typ ist für Geräte, die Sie mit Configuration Manager verwalten.

Beim Konfigurieren einer neuen EDR-Richtlinie geben Sie den neu zu erstellenden Typ an, indem Sie ein Plattform für die Richtlinie auswählen.

Bevor Sie Richtlinien für Geräte bereitstellen können, die von Configuration Manager verwaltet werden, müssen Sie den Schritt Einrichten von Configuration Manager zur Unterstützung der EDR-Richtlinie aus dem Microsoft Endpoint Manager Admin Center durchführen. Mehr dazu erfahren Sie unter [Konfigurieren der Mandantenanfügung zur Unterstützung von Endpunktsicherheitsrichtlinien](../protect/tenant-attach-intune.md).


### <a name="create-edr-policies"></a>Erstellen von EDR-Richtlinien

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Endpoint Security-**  > **Endpunkterkennung und -antwort** > **Richtlinie erstellen** aus.

3. Wählen Sie die Plattform und das Profil für Ihre Richtlinie aus. Die folgenden Informationen zeigen, welche Optionen Sie dabei haben:

   - Intune – Intune stellt die Richtlinie für Geräte in ihren Azure AD Gruppen bereit. Wenn Sie die Richtlinie erstellen, wählen Sie Folgendes aus:
     - Plattform: **Windows 10 und höher**
     - Profil: **Endpunkterkennung und -antwort (MDM)**

   - Configuration Manager – Der Configuration Manager stellt die Richtlinie für Geräte in Ihren Configuration Manager-Sammlungen bereit. Wenn Sie die Richtlinie erstellen, wählen Sie Folgendes aus:
     - Plattform: **Windows 10 und Windows Server (Configuration Manager)**
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

  Das Diagramm für **Geräte mit ATP-Sensor** zeigt nur Geräte an, deren Onboarding in Microsoft Defender ATP erfolgreich mithilfe des Profils **Windows 10 und höher** durchgeführt wurde. Um sicherzustellen, dass Sie über eine vollständige Darstellung Ihrer Geräte in diesem Diagramm verfügen, müssen Sie das Onboardingprofil auf allen Ihren Geräten bereitstellen. Geräte, deren Onboarding in Microsoft Defender ATP mithilfe externer Methoden erfolgte, etwa durch Gruppenrichtlinie oder PowerShell, gelten als **Geräte ohne ATP-Sensor**.

- Bei Richtlinien, die auf die Plattform **Windows 10 und Windows Server (Configuration Manager)** ausgerichtet sind, wird eine Übersicht über die Konformität mit der Richtlinie angezeigt, aber Sie können kein Drilldown durchführen, um genauere Details anzuzeigen. Die Ansicht ist begrenzt, da das Admin Center eingeschränkte Statusdetails vom Configuration Manager empfängt, der die Bereitstellung der Richtlinie auf Configuration Manager-Geräten verwaltet.

[Sehen Sie sich die Einstellungen an](endpoint-security-edr-profile-settings.md), die Sie für Plattformen und Profile konfigurieren können.

## <a name="next-steps"></a>Nächste Schritte

- [Konfigurieren von Endpunktsicherheitsrichtlinien](endpoint-security-policy.md#create-an-endpoint-security-policy)
- Weitere Informationen zur [Endpunkterkennung und -antwort](/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response) finden Sie in der Dokumentation zu Microsoft Defender ATP.