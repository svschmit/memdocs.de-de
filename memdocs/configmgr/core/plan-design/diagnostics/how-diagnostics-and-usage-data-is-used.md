---
title: Verwenden von Diagnosedaten
titleSuffix: Configuration Manager
description: Erfahren Sie mehr darüber, wie Microsoft die Diagnose- und Nutzungsdaten verwendet, die Configuration Manager sammelt.
ms.date: 12/23/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: a8021bc8-2799-41f4-83c2-e27d1242028c
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f6a014d60c49b0ff7e10cd74c101294dd002266d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697128"
---
# <a name="how-microsoft-uses-configuration-manager-diagnostics-and-usage-data"></a>Wie Microsoft Diagnose- und Nutzungsdaten aus Configuration Manager verwendet

*Gilt für: Configuration Manager (Current Branch)*

Die von Configuration Manager erfassten Diagnose- und Nutzungsdaten stellen Microsoft ein nahezu unmittelbares Feedback zum Betrieb des Produkts bereit und dienen zur Anpassung zukünftiger Updates. Außerdem werden Microsoft dadurch Konfigurationsdaten zur Verfügung gestellt, mit deren Hilfe Konfigurationen entwickelt und getestet werden können, die Sie in der Praxis verwenden. Beispiel:

- Die von Standortservern verwendeten Windows Server-Versionen

- Installierte Sprachpakete

- Das Delta zwischen SQL-Schema und Standardwert des Produkts

Mithilfe dieser Daten kann das Entwicklungsteam zukünftige Tests planen, um die beste Lösung für die am häufigsten verwendeten Konfigurationen zu finden. Sie sind essenziell, um Änderungen schnell und in kurzen Releasezyklen vornehmen zu können.

Ebenso wichtig ist, wie Diagnose- und Nutzungsdaten nicht verwendet werden. Microsoft verwendet diese Daten nicht für folgende Zwecke:

- Lizenzierungsüberwachung, z.B. Vergleich der Verwendung mit Lizenzverträgen

- Überwachung von Produkten, die nicht mehr unterstützt werden

- Werbung basierend auf verfügbaren Daten wie z.B. Featureverwendung oder geografischem Standort (Zeitzone)

Microsoft verwendet die verfügbaren Daten für die Verbesserung des Produkts. Beispiel:

- In der anfänglichen Unterstützung, die vom aktuellen Branch von Configuration Manager angeboten wurde, war der Unterstützungszeitraum für Windows Server 2008 R2 eingeschränkt. Microsoft hat die Nutzungsdaten von Kunden untersucht, die ein Upgrade auf den aktuellen Branch von Configuration Manager durchgeführt hatten. Dabei wurde festgestellt, dass eine Anpassung und Verlängerung dieses Zeitraums erforderlich war, um Kunden, die weiterhin dieses Betriebssystem verwenden, zu unterstützen.

- Die Voraussetzungsprüfung für das Installieren von Updates wurde verbessert. Veraltete Regeln wurden entfernt, weitere Fälle berücksichtigt und diverse Probleme automatisch behoben.  

> [!div class="nextstepaction"]
> [Sammeln von Diagnose- und Nutzungsdaten mit Configuration Manager](how-diagnostics-and-usage-data-is-collected.md)
