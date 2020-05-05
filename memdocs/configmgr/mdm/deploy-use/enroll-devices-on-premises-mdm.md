---
title: Registrieren von Geräten für die lokale Verwaltung mobiler Geräte
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über die Methoden zum Registrieren von Geräten für die lokale Verwaltung mobiler Geräte (Mobile Device Management, MDM) in Configuration Manager.
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: b58472e3-31a5-4305-8eb6-2522befebe02
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 1ca7f792bb6b419dd1d20d495bdb53bc7c2be506
ms.sourcegitcommit: 578ad1e8088f7065b565e8a4f4619f5a26b94001
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81724604"
---
# <a name="enroll-devices-for-on-premises-mdm-in-configuration-manager"></a>Registrieren von Geräten für die lokale Verwaltung mobiler Geräte (MDM) in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Zum Verwalten von Geräten mit Configuration Manager lokalen Verwaltung mobiler Geräte (Mobile Device Management, MDM) müssen Sie diese zunächst registrieren. Anschließend können Configuration Manager mit den Geräten für Verwaltungsaufgaben kommunizieren. Configuration Manager bietet zwei Methoden zum Registrieren von Geräten:

- **Benutzer**Registrierung: Benutzer starten die Registrierung auf Ihrem Gerät. Damit die Benutzerregistrierung erfolgreich ist, installieren Sie das vertrauenswürdige Stamm Zertifikat auf dem Gerät, und stellen Sie den Benutzer für die Registrierung in den Client Einstellungen bereit. Zum Registrieren eines Geräts muss der Benutzer nur Ihre Anmelde Informationen eingeben.

    Weitere Informationen finden Sie unter Gewusst [wie: Registrieren von Geräten durch Benutzer](user-enroll-devices-on-premises-mdm.md).

- **Massen**Registrierung: der Benutzer des Geräts beginnt nicht mit der Registrierung. Sie erstellen ein Massen Registrierungspaket in Configuration Manager. Wenn Sie es auf dem Gerät öffnen, stellt das Paket die zum Registrieren des Geräts erforderlichen Informationen bereit.

    Weitere Informationen finden Sie unter [Massen](bulk-enroll-devices-on-premises-mdm.md)Registrierung von Geräten.

Weitere Informationen zu den Betriebssystemversionen, die Configuration Manager für die Geräteregistrierung in der lokalen MDM unterstützt, finden Sie [unter Unterstützte Konfigurationen](../../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md#bkmk_OnpremOS).
