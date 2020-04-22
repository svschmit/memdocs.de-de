---
title: Lizenzierung und Branches
titleSuffix: Configuration Manager
description: Informationen über die Lizenzierungsanforderungen für die Installationsoptionen, die mit Configuration Manager zur Verfügung stehen
ms.date: 06/04/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 495b87ae-41a4-49ba-abe2-d4f7d22ac0d4
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f18ed2180f1d526e2afa4872e8fa9018c7e18721
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81706878"
---
# <a name="licensing-and-branches-for-configuration-manager"></a>Lizenzierung und Branches für Configuration Manager

*Gilt für: Configuration Manager (Current Branch) und System Center Configuration Manager (Long-Term Servicing Branch)*

In diesem Artikel können Sie mehr über die Lizenzierungsanforderungen für die Installationsoptionen erfahren, die mit Configuration Manager zur Verfügung stehen. Diese Installationsoptionen umfassen die folgenden Branches:

- Current Branch
- Long-Term Servicing Branch (LTSB)
- Evaluierungsinstallation von Current Branch
- Technical Preview-Branch

## <a name="licensing-overview"></a>Übersicht über die Lizenz

Kunden mit aktiver Software Assurance für Configuration Manager-Lizenzen oder mit entsprechenden Abonnementrechten ab 1. Oktober 2016 verfügen über Benutzungsrechte des Configuration Manager-Release 1606 vom Oktober 2016. Kunden, die ab dem 1. Oktober 2016 oder danach über Rechte für Configuration Manager verfügen, erhalten während der Installation zwei lizenzierte Optionen: Current Branch und Long-Term Servicing Branch (LTSB).

Vollständige Nutzungsbedingungen für die Produkte, die Sie über Microsoft-Volumenlizenzprogramme erwerben, finden Sie unter [Lizenzierungsbedingungen und Dokumentation](https://go.microsoft.com/fwlink/?LinkId=800052).


## <a name="licensed-branches"></a>Lizenzierte Branches

Dieser Artikel verweist auf den Software Assurance-Vertrag oder entsprechende Abonnementrechte. Dieser Microsoft-Lizenzvertrag gewährt Rechte zum Installieren und Verwenden von Configuration Manager.

### <a name="current-branch"></a>Current Branch

Current Branch erfordert einen aktiven Software Assurance-Vertrag oder entsprechende Rechte für Configuration Manager. Weitere Informationen finden Sie unter [Software Assurance und Current Branch](#software-assurance-and-the-current-branch).

Dieser Branch wird für die Verwendung in Produktionsumgebungen unterstützt, die regelmäßig Qualitäts- und Featureupdates von Microsoft erhalten möchten. Er bietet Zugriff auf alle Features und Verbesserungen.

Ab Version 1710 wird jede Updateversion ab dem Veröffentlichungsdatum der allgemeinen Verfügbarkeit 18 Monate lang unterstützt. Weitere Informationen finden Sie unter [Support für die Versionen des aktuellen Branches von System Center Configuration Manager](../servers/manage/current-branch-versions-supported.md).

### <a name="long-term-servicing-branch-ltsb"></a>Long-Term Servicing Branch (LTSB)

LTSB erfordert einen aktuellen Software Assurance-Vertrag mit Microsoft ab dem 1. Oktober 2016. Weitere Informationen finden Sie unter [Software Assurance und LTSB](#software-assurance-and-the-ltsb).

Dieser Branch wird für die Verwendung in Produktionsumgebungen unterstützt. Er ist vorgesehen für Kunden, die ihre Software Assurance oder entsprechenden Abonnementrechte für Configuration Manager nach dem 1. Oktober 2016 haben ablaufen lassen. Dieser Branch hat Einschränkungen im Vergleich zu Current Branch.

Kritische Sicherheitsupdates für Configuration Manager sind für diesen Branch verfügbar, allerdings stehen keine neuen Features zur Verfügung.

### <a name="evaluation-installation-of-the-current-branch"></a>Evaluierungsinstallation von Current Branch

Die Evaluierungsversion erfordert keinen Software Assurance-Vertrag mit Microsoft. [Evaluierungsinstallationen](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection) sind immer Teil von Current Branch, und Sie können sie 180 Tage lang verwenden.

Sie können die Evaluierungsinstallation auf eine vollständige Installation von Current Branch upgraden. Eine Evaluierungsinstallation können Sie nicht auf Long-Term Servicing Branch upgraden.

### <a name="technical-preview-branch"></a>Technical Preview-Branch

[Technical Preview-Branch](https://www.microsoft.com/evalcenter/evaluate-system-center-configuration-manager-and-endpoint-protection-technical-preview) steht ebenfalls zur Verfügung. Dieser Branch ist ein eingeschränkter Build von Configuration Manager, mit dem Sie neue Features ausprobieren können. Sie installieren die Technical Preview mit anderen Medien als die lizenzierten Versionen. Weitere Informationen finden Sie unter [Technical Preview](../get-started/technical-preview.md).


## <a name="software-assurance-agreements"></a>Software Assurance-Verträge

Der Status der Software Assurance für Ihre Configuration Manager-Lizenzen oder die entsprechenden Abonnementrechte am 1. Oktober 2016 oder danach bestimmt bzw. bestimmen den Branch, den Sie installieren und verwenden können.

### <a name="software-assurance-and-the-current-branch"></a>Software Assurance und Current Branch

Die Nutzungsrechte für Current Branch von Configuration Manager können wie folgt bereitgestellt werden:

- **System Center:** Kunden mit einer aktiven Software Assurance auf System Center Standard- oder System Center Datacenter-Lizenzen können die Current Branch-Option von Configuration Manager installieren und verwenden.

- **System Center Configuration Manager:** Kunden, die über eine aktive Software Assurance für Configuration Manager-Lizenzen oder über entsprechende Abonnementrechte verfügen, können die Current Branch-Option von Configuration Manager installieren und verwenden.

Wenn Sie am 1. Oktober 2016 oder danach eine aktive Software Assurance für Configuration Manager-Lizenzen oder entsprechende Abonnementrechte besitzen:

- Sie können Current Branch installieren und verwenden.
- Sie müssen Sie Current Branch deinstallieren, wenn Sie Ihre Software Assurance oder Ihr Abonnement verfallen lassen.

### <a name="software-assurance-and-the-ltsb"></a>Software Assurance und LTSB

Wenn Sie am 1. Oktober 2016 oder danach eine aktive Software Assurance für Configuration Manager-Lizenzen oder entsprechende Abonnementrechte besitzen:

- können Sie LTSB installieren und verwenden. Kunden, die über unbefristete Rechte für Configuration Manager verfügen oder die die Software Assurance oder das Abonnement auslaufen lassen, können die LTSB-Version von Configuration Manager installieren, die zum Zeitpunkt des jeweiligen Auslaufens aktuell ist.

LTSB basiert auf der Current Branch-Version 1606 und weist die folgenden Einschränkungen auf:

- Es gibt keine Unterstützung für das Konvertieren von Current Branch in LTSB. Wenn an Ihrem Standort derzeit Current Branch installiert ist, müssen Sie LTSB als neuen Standort installieren.  

- LTSB unterstützt nicht alle Funktionen von Current Branch. Weitere Informationen finden Sie unter [Einführung in Long-Term Servicing Branch](introduction-to-the-ltsb.md). Diese Einschränkungen beinhalten eine begrenzte Funktionsgruppe, begrenzte Upgradeoptionen und einen separaten Lebenszyklus für die Produktunterstützung.  

### <a name="software-assurance-expiration-date"></a>Ablaufdatum der Software Assurance

Seit der Veröffentlichung der Baselinemedien, Version 1606, für Configuration Manager im Oktober 2016 können Sie das Ablaufdatum Ihres Software Assurance-Vertrags angeben. Das **Ablaufdatum der Software Assurance** ist ein optionaler Wert als praktische Erinnerung. Fügen Sie ihn bei der Ausführung des Configuration Manager-Setups oder zu einem späteren Zeitpunkt über die Configuration Manager-Konsole hinzu.

> [!NOTE]
> Microsoft überprüft das angegebene Ablaufdatum nicht und verwendet es auch nicht für die Lizenzüberprüfung. Verwenden Sie es als Erinnerung an das Ablaufdatum. Dieser Wert ist hilfreich, wenn Configuration Manager regelmäßig online überprüft, ob neue Softwareupdates angeboten werden. Ihr Software Assurance-Lizenzstatus sollte aktuell sein, damit Sie berechtigt sind, diese zusätzlichen Updates zu verwenden.

#### <a name="to-specify-the-software-assurance-expiration-date"></a>So geben Sie das Ablaufdatum der Software Assurance an

- Wenn Sie Setup aus den Configuration Manager-Medien ausführen, geben Sie den Wert auf der Seite **Product Key** des Setup-Assistenten an.

- Geben Sie den Wert in der Configuration Manager-Konsole unter **Hierarchieeinstellungen** in der Registerkarte **Lizenzierung** an.


## <a name="licensing-resources"></a>Ressourcen zu „Lizenzierung“

Wenn Sie mehr über die Produktlizenzierungsdetails erfahren möchten, nutzen Sie die folgenden Ressourcen.

### <a name="microsoft-volume-licensing-service-center-vlsc"></a>Microsoft Volume Licensing Service Center (VLSC)

- [Übersicht über das VLSC](https://www.microsoft.com/Licensing/existing-customer/vlsc-training-and-resources.aspx)

- [Produktbedingungen für die Microsoft-Volumenlizenzierung](https://go.microsoft.com/fwlink/?LinkId=800052)

- Einen Überblick über ihre Lizenzen finden Volumenlizenzkunden im [Volume Licensing-Servicecenter](https://www.microsoft.com/Licensing/servicecenter/default.aspx). Wechseln Sie zum Menü **Lizenzen**, und wählen Sie **Licenses Summary** (Zusammenfassung der Lizenzen) aus.

### <a name="vlsc-videos"></a>VLSC-Videos

- Wenn Sie sich Trainingsvideos zur Funktionsweise von VLSC ansehen möchten, wechseln Sie zu [Microsoft Volume Licensing Service Center training and resources (Microsoft Volume Licensing Service Center – Training und Ressourcen)](https://www.microsoft.com/licensing/existing-customer/vlsc-training-and-resources), und wählen Sie **„Gewusst-wie“-Videos** aus.

- [Video zur Frage, wo Sie Ihren aktiven Software Assurance-Vertrag finden können](https://www.microsoft.com/showcase/video.aspx?uuid=fe1846cb-1d26-49fc-b064-57b25dcc31a0) (ab Sekunde 43)  

- [Video zum Abrufen von Berechtigungen für das VLSC](https://www.microsoft.com/showcase/video.aspx?uuid=ac4ed1ca-d0a9-43cd-89fa-74ccb555dec4) Sie können anderen Personen in Ihrer Organisation Lese- und Schreibberechtigungen im VLSC erteilen.
