---
author: brenduns
ms.author: brenduns
ms.service: microsoft-intune
ms.subservice: protect
ms.topic: include
ms.date: 08/24/2020
ms.openlocfilehash: 01179c35274ff14d4a91283e9a38aa5e6fee8e03
ms.sourcegitcommit: 9408d103e7dff433bd0ace5a9ab8b7bdcf2a9ca2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/25/2020
ms.locfileid: "88823493"
---
<!--Don't apply H2/H3 in this include file since they are context driven by article-->
1. Klicken Sie in einer Configuration Manager Konsole, die mit dem Standort der obersten Ebene verbunden ist, mit der rechten Maustaste auf eine Gerätesammlung, die Sie mit Microsoft Endpoint Manager Admin Center synchronisieren, und wählen Sie **Eigenschaften** aus.

2. Aktivieren Sie auf der Registerkarte **Cloudsynchronisierung** die Option **Stellen Sie diese Sammlung zur Verfügung, um Richtlinien für die Endpunktsicherheit über das Admin Center von Microsoft Endpoint Manager zuzuweisen**.

   - Sie können diese Option nicht auswählen, wenn Ihre Configuration Manager-Hierarchie nicht mit einem Mandanten verbunden ist.
   - Die Sammlungen, die für diese Option zur Verfügung stehen, sind durch den [für den Upload ausgewählten Sammlungsbereich](../../../configmgr/tenant-attach/device-sync-actions.md#bkmk_edit) eingeschränkt. <!--CM7423168-->
  
   ![Konfigurieren der Cloudsynchronisierung](../media/tenant-attach-intune/cloud-sync.png)

3. Klicken Sie auf **OK**, um die Konfiguration zu speichern.

   Das Onboarding von Geräten in dieser Sammlung kann jetzt über Microsoft Defender ATP erfolgen, und die Geräte unterstützen die Sicherheitsrichtlinien für Intune-Endpunkte.
