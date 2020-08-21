---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: include
ms.date: 08/11/2020
ms.openlocfilehash: a61bf84a872458f37826c3de07ede05b1b658f0c
ms.sourcegitcommit: d225ccaa67ebee444002571dc8f289624db80d10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2020
ms.locfileid: "88127301"
---
<!--3555750 FKA 1357954 --Don't apply H2/H3 in this include file since they are context driven by article-->

Wenn Sie die Co-Verwaltung aktivieren, können Sie die öffentliche Azure-Cloud, die Azure US Government-Cloud oder Microsoft Azure China 21ViaNet (in Version 2006 hinzugefügt) verwenden. Befolgen Sie zum Aktivieren von Co-Verwaltung ab Configuration Manager, Version 1906 die unten stehenden Anweisungen:

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie den Eintrag **Cloud Services**, und wählen Sie den Knoten **Co-Verwaltung** aus. Wählen Sie im Menüband **Co-Verwaltung konfigurieren** aus, um den **Konfigurations-Assistenten für die Co-Verwaltung** zu öffnen.

1. Konfigurieren Sie auf der Seite **Onboarding von Mandanten** des Assistenten die **Azure-Umgebung**, die Sie verwenden möchten. Wählen Sie eine der folgenden Umgebungen aus:

   - Öffentliche Azure-Cloud
   - Azure-Cloud für US-Behörden<!--4075452-->
   - Azure China-Cloud (in Version 2006 hinzugefügt)<!--7133238-->
      - Aktualisieren Sie den Configuration Manager-Client vor dem Onboarding in Azure China-Cloud auf die neueste Version auf Ihren Geräten. <!--7630213--> 

   Wenn Sie „Azure China-Cloud“ oder „Azure-Cloud für US-Behörden“ auswählen, wird die Option **In Microsoft Endpoint Manager Admin Center hochladen** für [Mandantenanfügung](../../tenant-attach/device-sync-actions.md) deaktiviert.

1. Wählen Sie **Anmelden** aus. Melden Sie sich als globaler Azure AD-Administrator an, und klicken Sie auf **Weiter**. Sie melden sich nur dieses eine Mal für die Zwecke dieses Assistenten an. Die Anmeldeinformation werden weder gespeichert noch anderswo wiederverwendet.

1. Wählen Sie auf der Seite **Aktivierung** die folgenden Einstellungen aus:

   - **Automatic enrollment into Intune** (Automatische Registrierung bei Intune): Diese Option aktiviert die automatische Clientregistrierung in Intune für vorhandene Configuration Manager-Clients. Mit dieser Option können Sie für einen Teil der Clients die Co-Verwaltung aktivieren, um diese zu testen und einen Rollout in Phasen vorzunehmen. Wenn die Registrierung eines Geräts durch den Benutzer aufgehoben wird, wird es bei der nächsten Auswertung der Richtlinie erneut registriert. <!--3330596-->

      - **Pilot**: Es werden nur die Configuration Manager-Clients automatisch bei Intune registriert, die Mitglieder der Sammlung **Automatische Intune-Registrierung** sind.
      - **Alle**: Hiermit wird die automatische Registrierung für alle Windows 10-Clients, Version 1709 oder höher aktiviert.

   - **Automatische Intune-Registrierung**: Diese Sammlung sollte alle Clients enthalten, die Sie in die Co-Verwaltung integrieren möchten. Es ist im Wesentlichen eine Obermenge von allen anderen Stagingsammlungen.

   ![Angeben der Sammlung „Automatische Intune-Registrierung“ ](../media/3555750-co-management-onboarding-enablement.png)
      
      Automatische Registrierung wird nicht sofort für alle Clients ausgeführt. Dadurch kann die Registrierung besser in großen Umgebungen skaliert werden. Configuration Manager führt die Registrierungen basierend auf der Anzahl der Clients zufällig aus. Wenn Ihre Umgebung z.B. über 100.000 Clients verfügt, wird die Registrierung auf mehrere Tage ausgedehnt, wenn Sie diese Einstellung aktivieren.<!--1358003-->

      > [!Note]  
      > Ab Version 1906:
      >
      > - Ein neues co-verwaltetes Gerät wird jetzt automatisch basierend auf seinem Azure AD-*Gerätetoken* (Azure Active Directory) beim Microsoft Intune-Dienst registriert. Es muss nicht warten, bis ein Benutzer sich bei dem Gerät anmeldet, um die automatische Registrierung zu starten. Mit dieser Änderung kann die Anzahl von Geräten mit dem Registrierungsstatus *Benutzeranmeldung steht aus* reduziert werden.<!-- 4454491 --> Um dieses Verhalten zu unterstützen, muss auf dem Gerät Windows 10, Version 1803 oder höher ausgeführt werden. Weitere Informationen finden Sie unter [Registrierungsstatus der Co-Verwaltung](../how-to-monitor.md#co-management-enrollment-status).
      >
      > - Wenn Sie bereits Geräte für die Co-Verwaltung registriert haben, werden neue Geräte nun sofort registriert, sobald sie die [Voraussetzungen](../overview.md#prerequisites) erfüllen.<!--4321130-->

1. Kopieren und speichern Sie für internetbasierte Geräte, die bereits in Intune registriert sind, die Befehlszeile auf der Seite **Aktivierung**. Sie installieren mithilfe dieser Befehlszeile den Configuration Manager-Client als App in Intune für internetbasierte Geräte. Wenn Sie diese Befehlszeile jetzt nicht speichern, können Sie die Konfiguration der Co-Verwaltung zu einem beliebigen Zeitpunkt überprüfen, um diese Befehlszeile abzurufen.

1. Wählen Sie auf der Seite **Workloads** für die einzelnen Workloads aus, welche Gerätegruppe Sie mit Intune verwalten möchten. Weitere Informationen finden Sie unter [Workloads](../workloads.md). Wenn Sie nur Co-Verwaltung aktivieren möchten, müssen Sie jetzt keine Workloads verschieben. Sie können später Workloads verschieben. Weitere Informationen finden Sie unter [Verschieben von Workloads](../how-to-switch-workloads.md).  

    - **Pilot Intune**: Diese Einstellung wechselt die zugehörige Workload nur für die Geräte in den Pilotsammlungen, die Sie auf der Seite **Staging** angeben. Jede Workload kann eine andere Pilotsammlung aufweisen.
    - **Intune**: Schaltet die zugehörige Workload für alle mit Co-Verwaltung verwalteten Windows 10-Geräte um.  

    > [!Important]
    > Bevor Sie Workloads verschieben, stellen Sie sicher, dass Sie die entsprechende Workload in Intune ordnungsgemäß konfigurieren und bereitstellen. Achten Sie darauf, dass Workloads immer von einem der Verwaltungstools für Ihre Geräte verwaltet werden.  

1. Geben Sie auf der Seite **Staging** die Pilotsammlung für jede der Workloads an, die auf **Intune-Pilot** festgelegt sind.

   ![Angeben der Sammlung „Automatische Intune-Registrierung“ ](../media/3555750-co-management-onboarding-staging.png)

1. Schließen Sie den Assistenten, um die Co-Verwaltung zu aktivieren.
