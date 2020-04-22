---
author: mestew
ms.author: mstewart
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: include
ms.date: 08/23/2019
ms.openlocfilehash: d8eaaa403bd1dd97214b4eff82be79d5c2a6566e
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690398"
---
<!--Don't apply H2/H3 in this include file since they are context driven by article-->
1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie den Eintrag **Cloud Services**, und wählen Sie den Knoten **Co-Verwaltung** aus. Klicken Sie im Menüband auf **Co-Verwaltung konfigurieren**, um den **Konfigurations-Assistenten für die Co-Verwaltung** zu öffnen.

2. Wählen Sie auf der Seite **Abonnement** des Assistenten die Option **Anmelden** aus. Melden Sie sich bei Ihrem Intune-Mandanten an, und wählen Sie **Weiter** aus.  

3. Wählen Sie auf der Seite **Aktivierung** Ihre Einstellung für **Automatische Registrierung bei Intune** aus (**Pilot** oder **Alle**). Wenn die Registrierung eines Geräts durch den Benutzer aufgehoben wird, wird es bei der nächsten Auswertung der Richtlinie erneut registriert. <!--3330596--> 

    Diese Aktion aktiviert die automatische Clientregistrierung in Intune für vorhandene Configuration Manager-Clients. Wenn Sie **Pilot** auswählen, werden nur die Konfigurations-Manager-Clients aus der Pilotsammlung automatisch bei Intune registriert. Mit dieser Option können Sie für einen Teil der Clients die Co-Verwaltung aktivieren, um diese zu testen und einen Rollout in Phasen vorzunehmen. 

    > [!Note]  
    > Ab Version 1806 wird die automatische Registrierung nicht sofort für alle Clients ausgeführt. Dadurch kann die Registrierung besser in großen Umgebungen skaliert werden. Configuration Manager führt die Registrierungen basierend auf der Anzahl der Clients zufällig aus. Wenn Ihre Umgebung z.B. über 100.000 Clients verfügt, wird die Registrierung auf mehrere Tage ausgedehnt, wenn Sie diese Einstellung aktivieren.<!--1358003-->  

4. Kopieren und speichern Sie für internetbasierte Geräte, die bereits in Intune registriert sind, die Befehlszeile auf der Seite **Aktivierung**. Sie können diese Befehlszeile zum Installieren des Configuration Manager-Clients als App in Intune verwenden. Wenn Sie diese Befehlszeile jetzt nicht speichern, können Sie die Konfiguration der Co-Verwaltung zu einem beliebigen Zeitpunkt überprüfen, um diese Befehlszeile abzurufen.

5. Wählen Sie auf der Seite **Workloads** für die einzelnen Workloads aus, welche Gerätegruppe Sie mit Intune verwalten möchten. Weitere Informationen finden Sie unter [Workloads](../workloads.md).  

    Wenn Sie nur Co-Verwaltung aktivieren möchten, müssen Sie jetzt keine Workloads verschieben. Sie können später Workloads verschieben. Weitere Informationen finden Sie unter [Verschieben von Workloads](../how-to-switch-workloads.md).  

    Die Einstellung **Pilot Intune** wechselt die zugehörige Workload nur für die Geräte in der Pilotsammlung. Die Einstellung **Intune** schaltet die zugehörige Workload für alle Windows 10-Geräte mit Co-Verwaltung um.  

    > [!Important]
    > Bevor Sie Workloads verschieben, stellen Sie sicher, dass Sie die entsprechende Workload in Intune ordnungsgemäß konfigurieren und bereitstellen. Achten Sie darauf, dass Workloads immer von einem der Verwaltungstools für Ihre Geräte verwaltet werden.  

6. Konfigurieren Sie auf der Seite **Staging** die folgenden Einstellungen:  

    - **Pilot**: Die Pilotgruppe enthält eine oder mehrere Sammlungen, die Sie auswählen. Verwenden Sie diese Gruppe im Rahmen des Rollouts der Co-Verwaltung in mehreren Phasen. Beginnen Sie mit einer kleinen Testsammlung, und fügen Sie der Pilotgruppe nach und nach weitere Sammlungen hinzu, während Sie die Co-Verwaltung für weitere Benutzer und Geräte ausrollen. Die Sammlungen in der Pilotgruppe lassen sich jederzeit ändern.  

    - **Produktion**: Konfigurieren Sie die **Ausschlussgruppe** mit mindestens einer Sammlung. Geräte, die einer der Sammlungen in dieser Gruppe angehören, werden von der Co-Verwaltung ausgeschlossen.  

7. Schließen Sie den Assistenten, um die Co-Verwaltung zu aktivieren.  
