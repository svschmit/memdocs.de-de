---
title: Upgrade auf Windows 10
titleSuffix: Configuration Manager
description: Aktualisieren von Geräten, die für die Co-Verwaltung erforderlich sind, auf Windows 10, Version 1709 oder höher.
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 561eb5b6-f90c-485a-91c2-e45bb0ce7877
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: e11a6130fb9f7d86b7d3377cc4120d4e61c43d2d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81691198"
---
# <a name="upgrade-windows-10-for-co-management"></a>Upgrade auf Windows 10 für Co-Verwaltung

Während sie darauf hinarbeiten, Ihr Unternehmen in die Co-Verwaltung zu integrieren, stellt die aktuelle Windows-Version für einige Kunden eine erhebliche Hürde dar. Für Co-Verwaltung ist [Windows 10, Version 1709](https://docs.microsoft.com/windows/whats-new/whats-new-windows-10-version-1709) oder höher erforderlich. Sobald Sie Windows aktualisieren und die automatische Registrierung konfigurieren, werden Ihre Clients automatisch für die Co-Verwaltung angemeldet.

Im folgenden Video erläutern und zeigen Senior Program Manager Rob York und Product Marketing Manager Locky Ainley das Upgrade auf Windows 10 für Co-Verwaltung:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Upgrading-to-Windows-10-to-Enable-Co-Management/player]



## <a name="why-upgrade"></a>Warum ist ein Upgrade erforderlich?

Neben anderen Plattformverbesserungen unterstützt Windows 10, Version 1709 oder höher, die automatische Registrierung. Dieses Verhalten bewirkt, dass sich ein Gerät automatisch bei Intune registriert, wenn es in Azure Active Directory (Azure AD) eingebunden wird. 

Weitere Informationen finden Sie unter [Aktivieren der automatischen Windows 10-Registrierung](https://docs.microsoft.com/intune/windows-enroll#enable-windows-10-automatic-enrollment).


## <a name="how-to-do-it"></a>Vorgehensweise

Wir haben bereits Tausende von Kunden dabei unterstützt, schnell auf die aktuelle Version umzusteigen. Hier sind einige Tipps, die auf unseren Erfahrungen basieren:

- Verwenden Sie stufenweise Bereitstellungen, um dieses Upgrade für die richtigen Personen zur richtigen Zeit bereitzustellen. Weitere Informationen finden Sie unter [Erstellen von stufenweisen Bereitstellungen mit Configuration Manager](../osd/deploy-use/create-phased-deployment-for-task-sequence.md).  

- Verwenden Sie vorgeschaltete Zwischenspeicherung, um Wartezeiten für Benutzer zu verringern. Weitere Informationen finden Sie unter [Konfigurieren des zwischengespeicherten Inhalts](../osd/deploy-use/configure-precache-content.md).  

- Verwenden Sie die Standardvorlage der Tasksequenz für ein direktes Upgrade. Konfigurieren Sie dann die vor und nach dem Upgrade erforderlichen Schritte sowie etwaige Fehlermaßnahmen. Weitere Informationen finden Sie unter [Empfohlene Tasksequenzschritte nach der Verarbeitung](../osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system.md#recommended-task-sequence-steps-for-post-processing).  

- Wenn Ihre Umgebung über hochgradig mobile Mitarbeiter verfügt, unterstützt Configuration Manager ein direktes Upgrade über das Cloudverwaltungsgateway (Cloud Management Gateway, CMG). Mit diesem Feature können Sie Ihre Windows 10-Clients aktualisieren, wenn sie internetbasiert sind. Weitere Informationen zum CMG finden Sie unter [Bereitstellen eines direkten Upgrades für Windows 10 über das CMG](../osd/deploy-use/deploy-a-task-sequence.md#deploy-windows-10-in-place-upgrade-via-cmg).  

- Bieten Sie ein Abonnement für Co-Verwaltung für Benutzer an, die frühzeitige Anwender sein möchten. Dieser Ansatz beschleunigt die Ersteinführung. Indem Sie diese Personen im Voraus identifizieren, können Sie eine gute Abdeckung in den ersten Tagen eines Rollouts sicherstellen. Sie erhalten auch Bestätigung und Feedback von Benutzern, die sich über Änderungen freuen und an häufigeren Releases interessiert sind. Programme für frühzeitige Anwender wecken das Interesse an den neuen Technologien und wachsen mit der Zeit.  


## <a name="case-studies"></a>Fallstudien

Die IT-Abteilung von Microsoft hat Windows 10 für 96.000 verteilte Benutzer bei Microsoft bereitgestellt. Die Bereitstellung umfasste sowohl Remotebenutzer als auch Benutzer im Unternehmensnetzwerk. Die Bereitstellung wurde in neun Wochen abgeschlossen. Weitere Informationen zu den dabei gewonnenen Erfahrungen finden Sie unter [Bereitstellen von Windows 10 bei Microsoft als direktes Upgrade](https://www.microsoft.com/itshowcase/deploying-windows-10-at-microsoft-as-an-in-place-upgrade).  

Ein großer europäischen Softwarehersteller setzt erfolgreich eine Gruppe mit frühzeitigen Anwendern ein. Nach anfänglichen Tests und Pilotgruppen erhalten rund 2.000 Mitarbeiter das erste Update, Upgrades und Software. Diese Gruppe umfasst IT-Mitarbeiter und freiwillige Teilnehmer. Dieses Engagement gegenüber den Nutzern verleiht dem Unternehmen ein höheres Maß an Selbstvertrauen beim Testen und mehr Glaubwürdigkeit, wenn die Massenrollouts beginnen.



## <a name="contact-fasttrack"></a>Kontaktaufnahme mit FastTrack

Wenn Sie Unterstützung bei Ihrem Windows 10-Upgrade zu irgendeinem Zeitpunkt des Vorgangs benötigen, navigieren Sie zu [Microsoft FastTrack](https://Microsoft.com/FastTrack/), melden Sie sich an, und fordern Sie Unterstützung an. 

Weitere Informationen finden Sie unter [Abrufen von Hilfe aus FastTrack](quickstart-fasttrack.md). 

