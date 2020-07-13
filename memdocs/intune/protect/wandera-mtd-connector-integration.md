---
title: Einrichten der Wandera Mobile Threat Protection-Integration mit Intune
titleSuffix: Intune on Azure
description: Einrichten der Wandera Mobile Threat Protection-Lösung in Microsoft Intune, um den Zugriff mobiler Geräte auf Ihre Unternehmensressourcen zu steuern.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/26/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
search.appverid: MET150
ms.collection: M365-identity-device-management
ms.openlocfilehash: fc44bb114d6ff9089a01da2d0b7db7aa7527f4b5
ms.sourcegitcommit: 7de54acc80a2092b17fca407903281435792a77e
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/06/2020
ms.locfileid: "85972146"
---
# <a name="integrate-wandera-mobile-threat-protection-with-intune"></a>Integrieren von Wandera Mobile Threat Protection in Intune  

Führen Sie die folgenden Schritte aus, um die Wandera Mobile Threat Defense-Lösung in Intune zu integrieren.  

## <a name="before-you-begin"></a>Vorbereitung  

Bevor Sie mit der Integration von Wandera in Intune beginnen, stellen Sie sicher, dass die folgenden Voraussetzungen erfüllt sind:

- Intune-Abonnement
- Azure Active Directory-Administratoranmeldeinformationen mit zugewiesener Rolle, die die folgenden Berechtigungen erteilen kann:

    - Anmelden und das Benutzerprofil lesen
    - Zugriff auf das Verzeichnis als angemeldeter Benutzer
    - Lesen der Verzeichnisdaten
    - Senden von Geräterisikoinformationen an Intune
 
- Ein gültiges Wandera-Abonnement
    - Ein Administratorkonto mit Superadministratorberechtigungen

## <a name="integration-overview"></a>Übersicht über die Integration

Das Aktivieren der Mobile Threat Defense-Integration zwischen Wandera und Intune umfasst Folgendes:

- Aktivieren des UEM Connect-Diensts von Wandera zum Synchronisieren von Informationen mit Azure und Intune (Dazu gehören Metadaten der Lebenszyklusverwaltung für Benutzer und Geräte sowie die Gerätebedrohungsstufe von Mobile Threat Defense)
- Erstellen von Aktivierungsprofilen in Wandera zum Definieren des Verhaltens für die Geräteregistrierung
- Drahtlose Bereitstellung von Wandera auf verwalteten iOS- und Android-Geräten
- Konfigurieren von Wandera für Endbenutzer-Self-Service mithilfe von MAM-WE auf nicht verwalteten iOS- und Android-Geräten

## <a name="set-up-wandera-mobile-threat-defense-integration"></a>Einrichten der Wandera Mobile Threat Defense-Integration

Für die Einrichtung der Integration zwischen Wandera und Intune wird keine Unterstützung durch Wandera-Mitarbeiter benötigt, und sie kann problemlos innerhalb weniger Minuten durchgeführt werden.

### <a name="enable-support-for-wandera-in-intune"></a>Aktivieren der Unterstützung für Wandera in Intune

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Klicken Sie auf **Mandantenverwaltung** > **Connectors und Token** > **Mobile Threat Defense** > **Hinzufügen**.
3. Wählen Sie auf der Seite **Connector hinzufügen** in der Dropdownliste den Eintrag **Wandera** aus. Wählen Sie dann **Erstellen** aus.  
4. Wählen Sie im Bereich „Mobile Threat Defense“ den **Wandera** MTD-Connector in der Liste der Connectors aus, um den Bereich **Connector bearbeiten** zu öffnen. Wählen Sie **Open the Wandera admin console** (Die Wandera-Verwaltungskonsole öffnen) aus, um [RADAR](https://radar.wandera.com/login), die Wandera-Verwaltungskonsole, zu öffnen und sich anzumelden. 
5. Navigieren Sie in der Wandera RADAR-Konsole zu **Integrations > UEM Integration** (Integrationen > UEM-Integrationen), und wählen Sie dann die Registerkarte **UEM Connect** aus. Wählen Sie in der Dropdownliste „EMM Vendor“ (EMM-Anbieter) **Microsoft Intune** aus.
6. Daraufhin wird Ihnen eine Anzeige ähnlich der folgenden angezeigt, die angibt, welche Berechtigungen zum Abschließen der Integration gewährt werden müssen:

   ![Integrationen und Berechtigungen](./media/wandera-mtd-connector-integration/integrations-and-permissions.png) 

7. Klicken Sie neben „Intune User and Device Sync“ (Intune-Benutzer und Gerätesynchronisierung) auf „Gewähren“, um den Prozess zur Einwilligung zu starten, damit Wandera Funktionen zur Lebenszyklusverwaltung mit Azure und Intune ausführen kann.
8. Wenn Sie dazu aufgefordert werden, geben Sie Ihre Azure-Administratoranmeldeinformationen ein. Überprüfen Sie die angeforderten Berechtigungen, und aktivieren Sie dann das Kontrollkästchen „Zustimmung im Namen Ihrer Organisation“. Klicken Sie schließlich auf „Akzeptieren“, um die Integration der Lebenszyklusverwaltung zu autorisieren.

   ![Akzeptieren von Berechtigungen](./media/wandera-mtd-connector-integration/permissions.png)

10. Anschließend kehren Sie automatisch zur RADAR-Verwaltungskonsole zurück.  Wenn die Autorisierung erfolgreich war, wird ein grünes Häkchen neben der Schaltfläche „Gewähren“ angezeigt.
11. Wiederholen Sie diesen Einwilligungsprozess für die restlichen aufgeführten Integrationen, indem Sie auf die entsprechenden Gewähren-Schaltflächen klicken, bis neben allen grüne Häkchen angezeigt werden.

    ![Synchronisierungsgruppe](./media/wandera-mtd-connector-integration/sync-group-name.png)

12. Wechseln Sie zurück zur Intune-Konsole, und bearbeiten Sie den Wandera MTD-Connector. Legen Sie alle verfügbaren Optionen auf „Ein“ fest, und speichern Sie die Konfiguration.

    ![Aktivieren von Wandera](./media/wandera-mtd-connector-integration/enable-wandera.png)

Intune und Wandera sind nun verbunden.

## <a name="create-activation-profiles-in-wandera"></a>Erstellen von Aktivierungsprofilen in Wandera

Auf Intune basierende Bereitstellungen werden mithilfe von Wandera-Aktivierungsprofilen durchgeführt, die in RADAR definiert werden.  Jedes Aktivierungsprofil definiert spezifische Konfigurationsoptionen, z. B. Authentifizierungsanforderungen, Dienstfunktionen und anfängliche Gruppenmitgliedschaft.

Nachdem Sie ein Aktivierungsprofil in Wandera erstellt haben, müssen Sie dieses Benutzern und Geräten in Intune „zuweisen“.  Während ein Aktivierungsprofil universell für Geräteplattformen und Verwaltungsstrategien verwendet werden kann, wird in den folgenden Schritten beschrieben, wie Sie Intune basierend auf den Unterschieden konfigurieren.

In den nachfolgenden Schritten wird davon ausgegangen, dass Sie ein Aktivierungsprofil in Wandera erstellt haben, das Sie per Intune auf Ihren Zielgeräten bereitstellen möchten. Weitere Informationen zum Erstellen und Verwenden von Wandera-Aktivierungsprofilen finden Sie im [Handbuch zu Aktivierungsprofilen](https://radar.wandera.com/?return_to=https://wandera.force.com/Customer/s/article/Enrollment-Links).

> [!NOTE]
> Stellen Sie beim Erstellen von Aktivierungsprofilen für die Bereitstellung per Intune oder MAM-WE sicher, dass Sie für die bestmögliche Sicherheit für den zugeordneten Benutzer die Option für die Authentifizierung durch den Identitätsanbieter „Azure Active Directory“, die plattformübergreifende Kompatibilität und eine optimierte Benutzeroberfläche auswählen.

## <a name="deploying-wandera-over-the-air-to-mdm-managed-devices"></a>Drahtloses Bereitstellen von Wandera auf Geräten mit mobiler Geräteverwaltung

Für von Intune verwaltete iOS- und Android-Geräte kann Wandera für schnelle pushbasierte Aktivierungen drahtlos bereitgestellt werden. Stellen Sie sicher, dass Sie die erforderlichen Aktivierungsprofile bereits erstellt haben, bevor Sie mit diesem Abschnitt fortfahren. Das Bereitstellen von Wandera auf verwalteten Geräten umfasst:
- Hinzufügen von Wandera-Konfigurationsprofilen zu Intune und Zuweisen zu Zielgeräten
- Hinzufügen der Wandera-App und der entsprechenden App-Konfigurationen zu Intune und Zuweisen zu Zielgeräten

### <a name="configure-and-deploy-ios-configuration-profiles"></a>Konfigurieren und Bereitstellen von iOS-Konfigurationsprofilen 

In diesem Abschnitt laden Sie die **erforderlichen** iOS-Gerätekonfigurationsdateien herunter und stellen diese drahtlos per MDM auf Ihren verwalteten Intune-Geräten bereit.

1. Navigieren Sie in **RADAR** zu dem Aktivierungsprofil, das Sie bereitstellen möchten („Geräte > Aktivierungen“), und klicken Sie dann auf **Deployment Strategies > Managed Devices > Microsoft Endpoint Manager** (Bereitstellungsstrategien > Verwaltete Geräte > Microsoft Endpoint Manager).
2. Erweitern Sie den Abschnitt **Apple iOS Supervised** oder **Apple iOS Unsupervised** basierend auf der Konfiguration Ihrer Geräte.
3. Laden Sie die bereitgestellten Konfigurationsprofile herunter, und bereiten Sie diese mit dem folgenden Schritt auf den Upload vor.
4. Öffnen Sie die **Microsoft Intune-Verwaltungskonsole**, und navigieren Sie zu **Geräte > iOS/iPadOS > Konfigurationsprofile**.  Klicken Sie auf **Profil erstellen**.
5. Wählen Sie im daraufhin angezeigten Bereich unter **Plattform** die Option **iOS/iPadOS** aus, und wählen Sie dann unter „Profil“ die Option **Benutzerdefiniert** aus. Klicken Sie dann auf **Erstellen**.
6. Geben Sie im Feld **Name** einen beschreibenden Titel für die Konfiguration ein, der idealerweise mit dem Namen des Aktivierungsprofil in RADAR übereinstimmt. Dies vereinfacht zukünftige Querverweise. Alternativ können Sie den Code für das Aktivierungsprofil angeben. Es wird empfohlen, dass Sie angeben, ob die Konfiguration für überwachte oder nicht überwachte Geräte vorgesehen ist, indem Sie einen entsprechenden Suffix zum Namen hinzufügen.
7. Geben Sie optional eine **Beschreibung** mit weiteren Informationen zum Zweck bzw. zur Verwendung der Konfiguration für andere Administratoren an. Klicken Sie auf **Weiter**.
8. Klicken Sie auf **Datei auswählen**, und suchen Sie nach dem heruntergeladenen Konfigurationsprofil, das dem in Schritt 3 heruntergeladenen Aktivierungsprofil entspricht. Achten Sie darauf, dass Sie das entsprechende überwachte oder nicht überwachte Profil auswählen, wenn Sie beide heruntergeladen haben. Klicken Sie auf **Weiter**.
   <!-- image placeholder - ending future availability -->
9.  Definieren Sie **Bereichstags** entsprechend Ihrer Methoden für die rollenbasierte Zugriffsteuerung von Intune.  Klicken Sie auf **Weiter**.
10. Als Nächstes müssen Sie das Konfigurationsprofil den Benutzergruppen oder Geräten **zuweisen**, für die Wandera bereits installiert sein sollte.  Es wird empfohlen, dass Sie mit einer Testgruppe beginnen und diese erweitern, nachdem Sie festgestellt haben, dass die Aktivierungen zur Validierung ordnungsgemäß funktionieren. Klicken Sie auf **Weiter**.
11. Überprüfen Sie die Konfiguration auf Richtigkeit, und nehmen Sie bei Bedarf Änderungen vor. Klicken Sie dann auf **Erstellen**, um das Konfigurationsprofil zu erstellen und bereitzustellen.

> [!NOTE]
> Wandera bietet ein erweitertes Bereitstellungsprofil für überwachte iOS-Geräte an. Wenn Sie über mehrere überwachte und nicht überwachte Geräte verfügen, wiederholen Sie die obigen Schritte nach Bedarf für den anderen Profiltyp. Sie müssen dieselben Schritte für alle zukünftigen Aktivierungsprofile durchführen, die über Intune bereitgestellt werden sollen. Wenden Sie sich an den Wandera-Support, wenn Sie über überwachte und nicht überwachte iOS-Geräte verfügen und Hilfe bei Richtlinienzuweisungen benötigen, die auf dem überwachten Modus basieren. 

## <a name="deploying-wandera-to-mam-we-devices"></a>Bereitstellen von Wandera auf MAM-WE-Geräten
Für MAM-WE-Geräte, die nicht von Intune verwaltet werden, verwendet Wandera ein integriertes Onboarding basierend auf der Authentifizierung, um Unternehmensdaten in den MAM-fähigen Apps zu aktivieren und zu schützen. 

In den folgenden Abschnitten wird beschrieben, wie Sie Wandera und Intune konfigurieren, um Endbenutzern das Aktivieren von Wandera zu ermöglichen, bevor sie auf Unternehmensdaten zugreifen können. 

### <a name="configure-azure-device-provisioning-in-a-wandera-activation-profile"></a>Konfigurieren der Azure-Gerätebereitstellung in einem Wandera-Aktivierungsprofil
Für Aktivierungsprofile, die mit MAM-WE verwendet werden, muss für den zugeordneten Benutzer die Option für die Authentifizierung durch den Identitätsanbieter „Azure Active Directory“ festgelegt werden.
1. Wählen Sie im **Wandera RADAR**-Portal ein vorhandenes Aktivierungsprofil aus, oder erstellen Sie ein neues, das MAM-WE-Geräte während der Registrierung unter „Geräte > Aktivierungen“ verwenden. 
2. Klicken Sie auf die **Registerkarte „Deployment Strategies“ (Bereitstellungsstrategien) und dann auf „Nicht verwaltete Geräte“** , und scrollen Sie dann zum Abschnitt **Azure Device Provisioning** (Azure-Gerätebereitstellung).
3. Geben Sie Ihre **Azure AD-Mandanten-ID** in das entsprechende Textfeld ein. Wenn Sie Ihre Mandanten-ID nicht zur Hand haben, klicken Sie auf den Link **Get my Tenant ID** (Mandanten-ID abrufen) klicken, um Azure AD in einer neuen Registerkarte zu öffnen, damit Sie den Wert problemlos in Ihre Zwischenablage kopieren können.
4. Legen Sie optional **Gruppen-IDs** fest, um Benutzeraktivierungen auf spezifische Gruppen zu beschränken.
   - Wenn mindestens eine **Gruppen-ID** definiert ist, muss ein Benutzer, der MAM-WE aktiviert, ein Mitglied von mindestens einer der festgelegten Gruppen sein, damit er die Aktivierung mithilfe dieses Aktivierungsprofils durchführen kann.
   - Sie können mehrere Aktivierungsprofile mit derselben Azure-Mandanten-ID, aber mit anderen Gruppen-IDs einrichten. Dadurch können Sie Geräte in Wandera basierend auf der Azure-Gruppenmitgliedschaft registrieren, sodass unterschiedliche Funktionen je nach Gruppe zum Zeitpunkt der Aktivierung zugewiesen werden können.
   - Sie können ein einzelnes Standardaktivierungsprofil konfigurieren, für das keine Gruppen-IDs festgelegt sind.  Diese Gruppe fungiert als Catch-All für alle Aktivierungen, für die der authentifizierte Benutzer kein Mitglied einer Gruppe ist, die einem anderen Aktivierungsprofil zugeordnet ist.
5. Klicken Sie in der oberen rechten Ecke der Seite auf **Speichern**.

## <a name="next-steps"></a>Nächste Schritte
- Da Ihre Wandera-Aktivierungsprofile nun in RADAR geladen sind, erstellen Sie als Nächstes Client-Apps in Intune, um die Wandera-App auf Android- und iOS/iPadOS-Geräten bereitzustellen. Die Wandera-App-Konfiguration stellt wesentliche Funktionen bereit, die die übertragenen Gerätekonfigurationsprofile ergänzen und werden für alle Bereitstellungen empfohlen. Unter [Hinzufügen von MTD-Apps](mtd-apps-ios-app-configuration-policy-add-assign.md) finden Sie die für die Wandera-Apps spezifischen Verfahren und benutzerdefinierten Details. 
- Da Sie Wandera nun mit Endpoint Manager integriert haben, können Sie Ihre Konfiguration optimieren, Berichte anzeigen und umfassendere Bereitstellungen für Ihre mobilen Geräte durchführen. Ausführliche Anleitungen zur Konfiguration finden Sie in der Wandera-Dokumentation unter [Support Center Getting Started Guide (Anleitung zu den ersten Schritten des Support Centers)](https://radar.wandera.com/?return_to=https://wandera.force.com/Customer/s/getting-started).
