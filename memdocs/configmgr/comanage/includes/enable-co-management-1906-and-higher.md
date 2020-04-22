---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: include
ms.date: 03/12/2020
ms.openlocfilehash: 37376d137409b06816d4c5dff5a0909f57531443
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690408"
---
<!--3555750 FKA 1357954 --Don't apply H2/H3 in this include file since they are context driven by article-->
1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie den Eintrag **Cloud Services**, und wählen Sie den Knoten **Co-Verwaltung** aus. Klicken Sie im Menüband auf **Co-Verwaltung konfigurieren**, um den **Konfigurations-Assistenten für die Co-Verwaltung** zu öffnen.

2. Konfigurieren Sie im Assistenten auf der Seite **Abonnement** die folgenden Einstellungen:

    - Die zu verwendende **Azure-Umgebung**. Beispiel: die Azure Public Cloud oder die Azure US Government Cloud.<!--4075452-->  

    - Wählen Sie **Anmelden** aus. Melden Sie sich als globaler Azure AD-Administrator an, und klicken Sie auf **Weiter**.  

        > [!TIP]
        > Sie melden sich nur dieses eine Mal für die Zwecke dieses Assistenten an. Die Anmeldeinformation werden weder gespeichert noch anderswo wiederverwendet.

3. Wählen Sie auf der Seite **Aktivierung** die folgenden Einstellungen aus:

   - **Automatic enrollment into Intune** (Automatische Registrierung bei Intune): Diese Option aktiviert die automatische Clientregistrierung in Intune für vorhandene Configuration Manager-Clients. Mit dieser Option können Sie für einen Teil der Clients die Co-Verwaltung aktivieren, um diese zu testen und einen Rollout in Phasen vorzunehmen. Wenn die Registrierung eines Geräts durch den Benutzer aufgehoben wird, wird es bei der nächsten Auswertung der Richtlinie erneut registriert. <!--3330596-->

      - **Pilot**: Es werden nur die Configuration Manager-Clients automatisch bei Intune registriert, die Mitglieder der Sammlung **Automatische Intune-Registrierung** sind.
      - **Alle**: Hiermit wird die automatische Registrierung für alle Windows 10-Clients, Version 1709 oder höher aktiviert.

   - **Automatische Intune-Registrierung**: Diese Sammlung sollte alle Clients enthalten, die Sie in die Co-Verwaltung integrieren möchten. Es ist im Wesentlichen eine Obermenge von allen anderen Stagingsammlungen.

   ![Angeben der Sammlung „Automatische Intune-Registrierung“ ](../media/3555750-co-management-onboarding-enablement.png)

      > [!Note]  
      > Ab Version 1806 wird die automatische Registrierung nicht sofort für alle Clients ausgeführt. Dadurch kann die Registrierung besser in großen Umgebungen skaliert werden. Configuration Manager führt die Registrierungen basierend auf der Anzahl der Clients zufällig aus. Wenn Ihre Umgebung z.B. über 100.000 Clients verfügt, wird die Registrierung auf mehrere Tage ausgedehnt, wenn Sie diese Einstellung aktivieren.<!--1358003-->  
      >
      > Ab Version 1906:
      >
      > - Ein neues co-verwaltetes Gerät wird jetzt automatisch basierend auf seinem Azure AD-*Gerätetoken* (Azure Active Directory) beim Microsoft Intune-Dienst registriert. Es muss nicht warten, bis ein Benutzer sich bei dem Gerät anmeldet, um die automatische Registrierung zu starten. Mit dieser Änderung kann die Anzahl von Geräten mit dem Registrierungsstatus *Benutzeranmeldung steht aus* reduziert werden.<!-- 4454491 --> Um dieses Verhalten zu unterstützen, muss auf dem Gerät Windows 10, Version 1803 oder höher ausgeführt werden. Weitere Informationen finden Sie unter [Registrierungsstatus der Co-Verwaltung](../how-to-monitor.md#co-management-enrollment-status).
      >
      > - Wenn Sie bereits Geräte für die Co-Verwaltung registriert haben, werden neue Geräte nun sofort registriert, sobald sie die [Voraussetzungen](../overview.md#prerequisites) erfüllen.<!--4321130-->

4. Kopieren und speichern Sie für internetbasierte Geräte, die bereits in Intune registriert sind, die Befehlszeile auf der Seite **Aktivierung**. Sie installieren mithilfe dieser Befehlszeile den Configuration Manager-Client als App in Intune für internetbasierte Geräte. Wenn Sie diese Befehlszeile jetzt nicht speichern, können Sie die Konfiguration der Co-Verwaltung zu einem beliebigen Zeitpunkt überprüfen, um diese Befehlszeile abzurufen.

5. Wählen Sie auf der Seite **Workloads** für die einzelnen Workloads aus, welche Gerätegruppe Sie mit Intune verwalten möchten. Weitere Informationen finden Sie unter [Workloads](../workloads.md). Wenn Sie nur Co-Verwaltung aktivieren möchten, müssen Sie jetzt keine Workloads verschieben. Sie können später Workloads verschieben. Weitere Informationen finden Sie unter [Verschieben von Workloads](../how-to-switch-workloads.md).  

    - **Pilot Intune**: Diese Einstellung wechselt die zugehörige Workload nur für die Geräte in den Pilotsammlungen, die Sie auf der Seite **Staging** angeben. Jede Workload kann eine andere Pilotsammlung aufweisen.
    - **Intune**: Schaltet die zugehörige Workload für alle mit Co-Verwaltung verwalteten Windows 10-Geräte um.  

    > [!Important]
    > Bevor Sie Workloads verschieben, stellen Sie sicher, dass Sie die entsprechende Workload in Intune ordnungsgemäß konfigurieren und bereitstellen. Achten Sie darauf, dass Workloads immer von einem der Verwaltungstools für Ihre Geräte verwaltet werden.  

6. Geben Sie auf der Seite **Staging** die Pilotsammlung für jede der Workloads an, die auf **Intune-Pilot** festgelegt sind.

   ![Angeben der Sammlung „Automatische Intune-Registrierung“ ](../media/3555750-co-management-onboarding-staging.png)

7. Schließen Sie den Assistenten, um die Co-Verwaltung zu aktivieren.
