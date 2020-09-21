---
title: Verschieben von Workloads für die Co-Verwaltung
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Workloads, die derzeit von Configuration Manager verwaltet werden, zu Microsoft Intune verschieben.
ms.prod: configuration-manager
ms.technology: configmgr-comanage
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 09/15/2020
ms.topic: how-to
ms.assetid: 60e2022f-a4f9-40dd-af01-9ecb37b43878
ms.openlocfilehash: 52a08549087338d0609aafc26f2cc1b3b697d6ba
ms.sourcegitcommit: e533cdf8722156a66b1cc46f710def96587345d0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/15/2020
ms.locfileid: "90568571"
---
# <a name="how-to-switch-configuration-manager-workloads-to-intune"></a>Verschieben von Configuration Manager-Workloads zu Intune

Einer der Vorteile der Co-Verwaltung ist das Verschieben von Workloads von Configuration Manager zu Microsoft Intune. Wenn ein Windows 10-Gerät über den Configuration Manager-Client verfügt und bei Intune angemeldet ist, können Sie die Vorteile beider Dienste nutzen. Sie steuern, für welche Workloads (sofern vorhanden) die Verantwortung von Configuration Manager auf Intune übergeht. Configuration Manager verwaltet weiterhin alle anderen Workloads (einschließlich der Workloads, die Sie nicht an Intune übergeben) und alle anderen Funktionen von Configuration Manager, die die Co-Verwaltung nicht unterstützt.

Wenn Sie eine Workload erst auf Intune umstellen, später aber Ihre Meinung ändern, können Sie wieder zurück zu Configuration Manager wechseln.

Weitere Informationen zu den unterstützten Workloads finden Sie unter [Workloads](workloads.md).

## <a name="switch-workloads-starting-in-version-1906"></a>Verschieben von Workloads ab Version 1906
<!--3555750 FKA 1357954 -->
Ab Version 1906 können Sie verschiedene Pilotsammlungen für die einzelnen Workloads für die Co-Verwaltung konfigurieren. Verschiedene Pilotsammlungen verwenden zu können, ermöglicht es Ihnen, Workloads mit einem präziseren Ansatz zu verschieben. Sie können Workloads verschieben, wenn Sie die Co-Verwaltung aktivieren, oder auch zu einem späteren Zeitpunkt, wenn Sie bereit sind. Wenn Sie Co-Verwaltung nicht bereits aktiviert haben, aktivieren Sie sie zunächst. Weitere Informationen finden Sie unter [Aktivieren der Co-Verwaltung](how-to-enable.md). Nachdem Sie die Co-Verwaltung aktiviert haben, ändern Sie die Einstellungen in den Eigenschaften der Co-Verwaltung.

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie den Eintrag **Cloud Services**, und wählen Sie den Knoten **Co-Verwaltung** aus.  
2. Wählen Sie das Co-Verwaltungsobjekt und anschließend auf dem Menüband **Eigenschaften** aus.  
3. Wechseln Sie zur Registerkarte **Workloads**. Standardmäßig werden alle Workloads auf die Einstellung **Configuration Manager** festgelegt. Um eine Workload zu verschieben, bewegen Sie den Schieberegler für diese Workload auf die gewünschte Einstellung.  

    ![Screenshot der Registerkarte „Workloads“ auf der Eigenschaftenseite für die Co-Verwaltung](media/3555750-co-management-workloads-tab.png)

    - **Configuration Manager:** Configuration Manager verwaltet diese Workload weiterhin.  

    - **Intune-Pilot**: Verschieben Sie diese Workload nur für die Geräte in der Pilotgruppe. Sie können die **Pilotsammlungen** auf der Registerkarte **Staging** der Eigenschaftenseite für die Co-Verwaltung ändern.  

    - **Intune**: Verschieben Sie diese Workload für alle Windows 10-Geräte, die für Co-Verwaltung registriert sind.  

4. Wechseln Sie zur Registerkarte **Staging**, und ändern Sie die **Pilotsammlung** für Workloads, falls erforderlich.
  
   ![Screenshot der Registerkarte „Staging“ auf der Eigenschaftenseite für die Co-Verwaltung](media/3555750-co-management-staging-tab.png)

> [!Important]  
> - Bevor Sie Workloads verschieben, stellen Sie sicher, dass Sie die entsprechende Workload in Intune ordnungsgemäß konfigurieren und bereitstellen. Achten Sie darauf, dass Workloads immer von einem der Verwaltungstools für Ihre Geräte verwaltet werden.
> - Ab Version 1806 von Configuration Manager synchronisieren die gemeinsam verwalteten Geräte automatisch die MDM-Richtlinie von Microsoft Intune, wenn Sie eine gemeinsam verwaltete Workload anpassen. <!--7087526-->

## <a name="switch-workloads-in-version-1902-and-earlier"></a>Verschieben von Workloads in Version 1902 und früher

Sie können Workloads verschieben, wenn Sie die Co-Verwaltung aktivieren, oder auch zu einem späteren Zeitpunkt, wenn Sie bereit sind. Wenn Sie Co-Verwaltung nicht bereits aktiviert haben, aktivieren Sie sie zunächst. Weitere Informationen finden Sie unter [Aktivieren der Co-Verwaltung](how-to-enable.md). Nachdem Sie die Co-Verwaltung aktiviert haben, ändern Sie die Einstellungen in den Eigenschaften der Co-Verwaltung.

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Verwaltung**, erweitern Sie den Eintrag **Cloud Services**, und wählen Sie den Knoten **Co-Verwaltung** aus.  

2. Wählen Sie das Co-Verwaltungsobjekt und anschließend auf dem Menüband **Eigenschaften** aus.
   - Sie werden aufgefordert, sich bei Azure AD anzumelden. Die Eingabeaufforderung hindert Sie nicht daran, Ihr Onboarding zu aktualisieren. Sie werden jedoch jedes Mal, wenn Sie die Seite **Eigenschaften** öffnen, aufgefordert, sich anzumelden.

3. Wechseln Sie zur Registerkarte **Workloads**. Standardmäßig werden alle Workloads auf die Einstellung **Configuration Manager** festgelegt. Um eine Workload zu verschieben, bewegen Sie den Schieberegler für diese Workload auf die gewünschte Einstellung.  

    ![Screenshot der Registerkarte „Workloads“ auf der Eigenschaftenseite für die Co-Verwaltung, Version 1902](media/properties-workloads.png)

    - **Configuration Manager:** Configuration Manager verwaltet diese Workload weiterhin.  

    - **Intune-Pilot**: Verschieben Sie diese Workload nur für die Geräte in der Pilotgruppe. Sie können die **Pilotgruppe** auf der Registerkarte **Staging** der Eigenschaftenseite für die Co-Verwaltung ändern.  

    - **Intune**: Verschieben Sie diese Workload für alle Windows 10-Geräte, die für Co-Verwaltung registriert sind.  

4. Ändern Sie auf der Registerkarte **Staging** der Eigenschaftenseite für die Co-Verwaltung die **Pilotsammlung** für Ihre Workloads, falls erforderlich.

5. Klicken Sie auf **OK**, um die Änderungen zu speichern und die Eigenschaften der Co-Verwaltung zu schließen.

> [!Important]  
> - Bevor Sie Workloads verschieben, stellen Sie sicher, dass Sie die entsprechende Workload in Intune ordnungsgemäß konfigurieren und bereitstellen. Achten Sie darauf, dass Workloads immer von einem der Verwaltungstools für Ihre Geräte verwaltet werden. 
> - Ab Version 1806 von Configuration Manager synchronisieren die gemeinsam verwalteten Geräte automatisch die MDM-Richtlinie von Microsoft Intune, wenn Sie eine gemeinsam verwaltete Workload anpassen. <!--7087526-->

## <a name="next-steps"></a>Nächste Schritte

[Überwachen der Co-Verwaltung](how-to-monitor.md)
