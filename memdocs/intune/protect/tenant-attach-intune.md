---
title: Verwenden von Intune-Richtlinien mit mandantenbasiert angefügten Configuration Manager-Geräten | Microsoft-Dokumentation
description: Konfigurieren Sie das mandantenbasierte Anfügen von Configuration Manager-Geräten an das Microsoft Endpoint Manager Admin Center, damit Sie unterstützte Richtlinien von Microsoft Intune auf diesen Geräten bereitstellen können.
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
ms.openlocfilehash: d56b06b49846201d6198c1abc81185bf74765ae3
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/25/2020
ms.locfileid: "88823498"
---
# <a name="configure-tenant-attach-to-support-endpoint-security-policies-from-intune"></a>Konfigurieren der Mandantenanfügung zur Unterstützung von Endpunktsicherheitsrichtlinien von Intune

Wenn Sie das Configuration Manager-Szenario für die Mandantenanfügung verwenden, können Sie Endpunktsicherheitsrichtlinien von Intune auf Geräten bereitstellen, die Sie über Configuration Manager verwalten. Um dieses Szenario verwenden zu können, müssen Sie zuerst die Mandantenanfügung für Configuration Manager konfigurieren und Gerätesammlungen von Configuration Manager für die Verwendung mit Intune aktivieren. Nachdem die Verwendung der Sammlungen aktiviert wurde, verwenden Sie das Microsoft Endpoint Manager Admin Center, um Richtlinien zu erstellen und bereitzustellen.

Die folgenden Richtlinientypen werden von Configuration Manager-Geräten unterstützt, die mandantenbasiert angefügt wurden:

- Antivirus-Richtlinie für die Endpunktsicherheit
- Richtlinie für Endpunkterkennung und -antwort für die Endpunktsicherheit

## <a name="requirements-to-use-intune-policy-for-tenant-attach"></a>Anforderungen für die Verwendung von Intune-Richtlinien für die Mandantenanfügung

Die Configuration Manager-Umgebung erfordert die folgenden Konfigurationen, damit die Verwendung von Intune-Endpunktsicherheitsrichtlinien mit Configuration Manager-Geräten unterstützt werden kann. Eine [Anleitung für die Konfiguration](#set-up-configuration-manager-to-support-intune-policies) finden Sie in diesem Artikel:

### <a name="general-requirements-for-tenant-attach"></a>Allgemeine Anforderungen für die Mandantenanfügung

- **Konfigurieren der Mandantenanfügung**: Mit dem Szenario der *Mandantenanfügung* können Sie Gerätesammlungen aus Configuration Manager mit dem Microsoft Endpoint Manager Admin Center synchronisieren. Dann können Sie unterstützte Richtlinien für diese Sammlungen über das Admin Center bereitstellen.

  Die Mandantenanfügung wird häufig zusammen mit der Co-Verwaltung konfiguriert, aber Sie können die Mandantenanfügung auch eigenständig konfigurieren.

- **Synchronisieren von Configuration Manager-Sammlungen** – Wenn Sie die Mandantenanfügung konfigurieren, können Sie die Configuration Manager-Gerätesammlungen auswählen, die mit dem Microsoft Endpoint Manager Admin Center synchronisiert werden sollen. Sie können die zum Synchronisieren vorgesehenen Gerätesammlungen auch später noch ändern. Unterstützte Richtlinien für Configuration Manager Geräte können nur Sammlungen zugewiesen werden, die Sie synchronisiert haben.

  Nach Auswahl der zu synchronisierenden Sammlungen müssen Sie diese für die Verwendung mit Endpunktsicherheitsrichtlinien von Intune aktivieren.

- **Berechtigungen für Azure AD**: Um die Einrichtung der Mandantenanfügung abzuschließen, benötigen Sie ein Konto mit globalen Administratorberechtigungen für Ihr Azure-Abonnement.

### <a name="specific-requirements-for-intune-endpoint-security-policies"></a>Spezielle Anforderungen für Intune-Endpunktsicherheitsrichtlinien

- **Antivirus-Richtlinie** (*Vorschau*):

  - **Configuration Manager** – die folgenden Umgebungen werden unterstützt:

    - **Configuration Manager, Current Branch-Version 2006 oder höher**: Mit dieser Current Branch-Version wurde Unterstützung für Intune-Antivirenrichtlinien hinzugefügt.
    <!--
    - **Configuration Manager technical preview 2007 or later** - Support for Intune antivirus policies was added with this technical preview version. -->

  - **Mandant für Microsoft Defender Advanced Threat Protection**: Ihr Microsoft Defender ATP-Mandant muss in Ihren Microsoft Endpoint Manager-Mandanten (Intune-Abonnement) integriert sein.  Weitere Informationen finden Sie in [Verwenden von Microsoft Defender ATP](advanced-threat-protection.md) in der Intune-Dokumentation.

- **Richtlinie für Endpunkterkennung und -antwort**:

  - **Configuration Manager** – die folgenden Umgebungen werden unterstützt:

    - **Configuration Manager, Technical Preview 2003 oder höher**: Unterstützung für Intune-Richtlinien für Endpunkterkennung und -antwort wurde mit der Technical Preview-Version 2003 hinzugefügt.

    - **Configuration Manager, Current Branch-Version 2002 oder höher**: Wenn Sie Configuration Manager mit Version 2002 verwenden, müssen Sie das konsoleninterne Update **Configuration Manager 2002 Hotfix (KB4563473)** installieren. Dieses Update aktiviert die Unterstützung von Endpunktsicherheitsrichtlinien in Configuration Manager 2002.

  - **Mandant für Microsoft Defender Advanced Threat Protection**: Ihr Microsoft Defender ATP-Mandant muss in Ihren Microsoft Endpoint Manager-Mandanten (Intune-Abonnement) integriert sein.  Weitere Informationen finden Sie in [Verwenden von Microsoft Defender ATP](advanced-threat-protection.md) in der Intune-Dokumentation.

## <a name="set-up-configuration-manager-to-support-intune-policies"></a>Einrichten von Configuration Manager zur Unterstützung von Intune-Richtlinien

Bevor Sie Intune-Richtlinien auf Configuration Manager-Geräten bereitstellen können, führen Sie die in den folgenden Abschnitten beschriebenen Konfigurationen aus. Diese Konfigurationen führen ein Onboarding Ihrer Configuration Manager-Geräte bei Microsoft Defender ATP durch und aktivieren die Verwendung der Geräte mit den Intune-Richtlinien.

Die folgenden Aufgaben werden in der Configuration Manager-Konsole ausgeführt. Wenn Sie mit Configuration Manager nicht vertraut sind, arbeiten Sie bei diesen Aufgaben mit einem Configuration Manager-Administrator zusammen.

1. [Installieren des Updates für Configuration Manager](#task-1-install-the-update-for-configuration-manager)
2. [Aktivieren der Mandantenanfügung](#task-2-configure-tenant-attach-and-synchronize-collections)  
3. [Auswählen der zu synchronisierenden Sammlungen](#task-3-select-collections-to-synchronize)
4. [Aktivieren von Sammlungen für die Unterstützung von Intune-Richtlinien](#task-4-enable-collections-for-endpoint-security-policies)

> [!TIP]
> Weitere Informationen zur Verwendung von Microsoft Defender ATP mit Configuration Manager finden Sie in den folgenden Artikeln des Configuration Manager-Inhalts:
>
> - [Durchführen des Onboardings für Configuration Manager-Clients in Microsoft Defender ATP über das Microsoft Endpoint Manager Admin Center](../../configmgr/core/get-started/2020/technical-preview-2003.md#bkmk_atp)
> - [Anfügen von Mandanten in Microsoft Endpoint Manager: Gerätesynchronisierung und Geräteaktionen](../../configmgr/core/get-started/2020/technical-preview-2002-2.md#bkmk_attach).

### <a name="task-1-install-the-update-for-configuration-manager"></a>Aufgabe 1: Installieren des Updates für Configuration Manager

Wenn Sie die Current Branch-Version 2002 von Configuration Manager verwenden, installieren Sie das folgende konsoleninterne Update, das Unterstützung für die von Ihnen über das Microsoft Endpoint Manager Admin Center bereitgestellten Endpunktsicherheitsrichtlinien hinzufügt.

**Updatedetails**:

- **Configuration Manager 2002 Hotfix (KB4563473)**

Befolgen Sie zum Installieren dieses Updates die Anleitung unter [Installieren konsoleninterner Updates](../../configmgr/core/servers/manage/install-in-console-updates.md) in der Configuration Manager-Dokumentation.

Kehren Sie nach der Installation des Updates hierher zurück, um die Konfiguration Ihrer Umgebung für die Unterstützung der Endpunktsicherheitsrichtlinien über das Microsoft Endpoint Manager Admin Center fortzusetzen.

### <a name="task-2-configure-tenant-attach-and-synchronize-collections"></a>Aufgabe 2: Konfigurieren von Mandantenanfügung und Synchronisieren von Sammlungen

Mit der Mandantenanfügung geben Sie Sammlungen von Geräten aus Ihrer Configuration Manager-Bereitstellung an, die mit dem Microsoft Endpoint Manager Admin Center synchronisiert werden sollen. Nach der Synchronisierung von Sammlungen können Sie im Admin Center Informationen zu diesen Geräten anzeigen und eine Endpunktsicherheitsrichtlinie aus Intune auf den Geräten bereitstellen.

Weitere Informationen zum Szenario der Mandantenanfügung finden Sie unter [Aktivieren der Mandantenanfügung](../../configmgr/tenant-attach/device-sync-actions.md) im Configuration Manager-Inhalt.

#### <a name="enable-tenant-attach-when-co-management-hasnt-been-enabled"></a>Aktivieren der Mandantenanfügung, wenn die Co-Verwaltung noch nicht aktiviert wurde

> [!TIP]
> Mit dem **Konfigurationsassistenten für die Co-Verwaltung** in der Configuration Manager-Konsole aktivieren Sie die Mandantenanfügung. Die Co-Verwaltung müssen Sie jedoch nicht aktivieren.
>
> Wenn Sie die Aktivierung der Co-Verwaltung planen, sollten Sie sich mit der Co-Verwaltung, den Voraussetzungen und der Verwaltung von Workloads vertraut machen, bevor Sie fortfahren. Weitere Informationen finden Sie unter [Was ist Co-Verwaltung?](../../configmgr/comanage/overview.md) in der Configuration Manager-Dokumentation.

1. Navigieren Sie in der Configuration Manager-Administratorkonsole zu **Verwaltung** > **Übersicht** > **Clouddienste** > **Co-Verwaltung**.
2. Klicken Sie im Menüband auf **Configure co-management** (Co-Verwaltung konfigurieren), um den Assistenten zu öffnen.
3. Wählen Sie auf der Seite **Onboarding von Mandanten** **AzurePublicCloud** als Umgebung aus. Azure Government-Clouds werden nicht unterstützt.
   1. Klicken Sie auf **Anmelden**. Melden Sie sich mit Ihrem *globalen Administratorkonto* an.

   2. Stellen Sie sicher, dass auf der Seite **Onboarding von Mandanten** die Option **Upload ins Microsoft Endpoint Manager Admin Center** aktiviert ist.

   3. Entfernen Sie das Kästchen bei **Automatische Clientregistrierung für Co-Verwaltung aktivieren**.

      Wenn diese Option ausgewählt ist, zeigt der Assistent zusätzliche Seiten an, um die Einrichtung der Co-Verwaltung abzuschließen. Weitere Informationen finden Sie unter [Aktivieren der Co-Verwaltung](../../configmgr/comanage/how-to-enable.md) im Configuration Manager-Inhalt.

     ![Konfigurieren der Mandantenanfügung](./media/tenant-attach-intune/tenant-onboarding.png)

4. Klicken Sie auf **Weiter** und dann auf **Ja**, um die Meldung **AAD-Anwendung erstellen** zu akzeptieren. Diese Aktion stellt einen Dienstprinzipal bereit und erstellt eine Azure AD-Anwendungsregistrierung, um die Synchronisierung von Sammlungen mit dem Microsoft Endpoint Manager Admin Center zu vereinfachen.

5. Konfigurieren Sie auf der Seite **Upload konfigurieren**, welche Sammlungen synchronisiert werden sollen. Sie können Ihre Konfiguration auf eine oder mehrere Gerätesammlungen beschränken oder die empfohlene Einstellung für den Geräte-Upload für **Alle mit Microsoft Endpoint Configuration Manager verwalteten Geräte** verwenden.

   > [!TIP]
   > Sie können die Auswahl von Sammlungen jetzt überspringen und später die Informationen aus der folgenden Aufgabe (Aufgabe 3) verwenden, um zu konfigurieren, welche Sammlungen mit dem Microsoft Endpoint Manager Admin Center synchronisiert werden.

6. Klicken Sie auf **Zusammenfassung**, um Ihre Auswahl zu überprüfen, und klicken Sie dann auf **Weiter**.

7. Klicken Sie auf **Schließen**, wenn der Assistent abgeschlossen ist.

   Damit ist die Mandantenanfügung konfiguriert, und die ausgewählten Sammlungen werden mit dem Microsoft Endpoint Manager Admin Center synchronisiert.

#### <a name="enable-tenant-attach-when-you-already-use-co-management"></a>Aktivieren der Mandantenanfügung, wenn die Co-Verwaltung bereits verwendet wird

1. Navigieren Sie in der Configuration Manager-Administratorkonsole zu **Verwaltung** > **Übersicht** > **Clouddienste** > **Co-Verwaltung**.

2. Klicken Sie mit der rechten Maustaste auf die Co-Verwaltungseinstellungen und dann auf **Eigenschaften**.

3. Klicken Sie in der Registerkarte **Configure upload** (Upload konfigurieren) auf **Upload to Microsoft Endpoint Manager admin center** (Upload ins Microsoft Endpoint Manager Admin Center). Klicken Sie auf **Übernehmen**.

   Die Standardeinstellung für den Upload von Geräten ist **All my devices managed by Microsoft Endpoint Configuration Manager** (Alle von Microsoft Endpoint Configuration Manager verwalteten Geräte). Sie können auch festlegen, dass die Konfiguration auf eine oder mehrere Gerätesammlungen beschränkt werden soll.

   ![Anzeigen der Registerkarte „Eigenschaften der Co-Verwaltung“](./media/tenant-attach-intune/configure-upload.png)

   > [!TIP]
   > Sie können die Auswahl von Sammlungen jetzt überspringen und später die Informationen aus der folgenden Aufgabe (Aufgabe 3) verwenden, um zu konfigurieren, welche Sammlungen mit dem Microsoft Endpoint Manager Admin Center synchronisiert werden.

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

### <a name="task-4-enable-collections-for-endpoint-security-policies"></a>Aufgabe 4: Aktivieren von Sammlungen für Endpunktsicherheitsrichtlinien

Nachdem Sie Sammlungen konfiguriert haben, die mit dem Microsoft Endpoint Manager Admin Center synchronisiert werden sollen, aktivieren Sie diese Sammlungen für Endpunktsicherheitsrichtlinien. Wenn Sie Sammlungen aus Geräten für Endpunktsicherheitsrichtlinien aus Intune aktivieren, konfigurieren Sie Geräte in diesen Sammlung für ein Onboarding bei Microsoft Defender ATP.

#### <a name="enable-collections-for-use-with-endpoint-security-policies"></a>Aktivieren von Sammlungen für die Verwendung mit Endpunktsicherheitsrichtlinien

[!INCLUDE [Enable endpoint security policies for a Configuration Manager collection](includes/make-configmgr-collection-available-edr.md)]

## <a name="next-steps"></a>Nächste Schritte

- [Konfigurieren Sie Endpunktsicherheitsrichtlinien](endpoint-security-policy.md#create-an-endpoint-security-policy) für *Antivirus* und *Endpunkterkennung und -antwort*.

- Weitere Informationen zur [Endpunkterkennung und -antwort](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/overview-endpoint-detection-response) finden Sie in der Dokumentation zu Microsoft Defender ATP.
