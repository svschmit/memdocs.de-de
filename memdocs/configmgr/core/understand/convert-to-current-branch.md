---
title: Durchführen eines Upgrades von Long-Term Servicing Branch auf Current Branch
titleSuffix: Configuration Manager
description: Informationen zum Konvertieren eines Long-Term Servicing Branch-Standorts auf einen Current Branch-Standort.
ms.date: 02/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ec5b54cf-62b7-4ed1-9bb3-e8c63b9641c8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: b9f79eae1eee29fee33a9a841a303aae55686c55
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707228"
---
# <a name="upgrade-the-long-term-servicing-branch-to-the-current-branch"></a>Upgrade von Long-Term Servicing Branch auf Current Branch

*Gilt für: System Center Configuration Manager (Long Term Servicing Branch)*

In diesem Thema erfahren Sie, wie man ein Upgrade eines Standorts und einer Hierarchie durchführt (konvertiert), die Long-Term Servicing Branch (LTSB) von Configuration Manager auf Current Branch ausführen.

Wenn Sie über einen aktuellen Software Assurance-Vertrag (oder ähnliche Lizenzrechte) verfügen, der Ihnen Rechte gewährt, Current Branch zu verwenden, können Sie Ihre Installation von LTSB auf Current Branch konvertieren.  Dies ist eine unidirektionale Konvertierung, weil das Konvertieren eines Current Branch-Standorts nach LTSB nicht unterstützt wird.

Wenn Sie über mehrere Standorte verfügen, müssen Sie nur den Standort der obersten Ebene Ihrer Hierarchie konvertieren. Nachdem der Standort der obersten Ebene konvertiert ist:
- Konvertieren untergeordnete primäre Standorte automatisch.
- Müssen Sie sekundäre Standorte in der Configuration Manager-Konsole manuell aktualisieren.

## <a name="run-setup-to-convert-the-long-term-servicing-branch"></a>Ausführen von Setup zum Konvertieren von Long-Term Servicing Branch
Sie können auf dem Standort der obersten Ebene Ihrer Hierarchie das Configuration Manager-Setup mit einem berechtigtem Baselinemedium ausführen, und **Standortwartung** auswählen.  Wählen Sie dann auf der Lizenzierungsseite die Option für Current Branch aus, und schließen Sie den Assistenten ab.

Sobald Ihr Standort in Current Branch konvertiert wurde, stehen Ihnen Features und Funktionen zur Verfügung, die bisher nicht verfügbar waren.

> [!NOTE]  
> Ein berechtigtes Baselinemedium ist ein Medium der gleichen oder höheren Version Ihrer LTSB-Installation.

Beispiel: Da LTSB auf Version 1606 basiert, können Sie kein Baselinemedium der Version 1511 verwenden, um in Current Branch zu konvertieren. Führen Sie Setup stattdessen von der gleichen Version 1606 des Baselinemediums aus, die Sie zur Installation des LTSB-Standorts verwendet haben, und wählen Sie die Lizenzierungsoption für Current Branch aus.  Alternativ können Sie das Setup auch von einer höheren Version des Baselinemediums von Current Branch ausführen.

Sie finden eine Liste der Baselineversionen unter **Baseline and update versions (Baseline- und Updateversionen)** in [Updates for Configuration Manager (Updates für Configuration Manager)](../servers/manage/updates.md).

## <a name="use-the-configuration-manager-console-to-convert-the-long-term-servicing-branch"></a>Verwenden der Configuration Manager-Konsole zum Konvertieren von Long-Term Servicing Branch
Wenn Ihr Standort LTSB ausführt, können Sie die folgende Option in der Configuration Manager-Konsole ausführen, um auf Current Branch zu konvertieren:

 1. Wechseln Sie in der Konsole zu **Verwaltung** > **Standortkonfiguration** > **Standorte**, und öffnen Sie dann die **Hierarchieeinstellungen**.  

 2. Wechseln Sie in den **Hierarchieeinstellungen** zur Registerkarte **Lizenzierung**. Wählen Sie die Option **In Current Branch konvertieren** aus, und klicken Sie dann auf **Anwenden**.  

Sobald Ihr Standort in Current Branch konvertiert wurde, stehen Ihnen Features und Funktionen zur Verfügung, die bisher nicht verfügbar waren.
