---
title: Bereitstellen von Ressourcenzugriffsprofilen
titleSuffix: Configuration Manager
description: Informationen zum Bereitstellen von WLAN-, VPN- und Zertifikatprofilen in Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3753608d-b539-44dc-8e3f-b631319e7687
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 0272c50429973cc3e15c295303b91593075ebe01
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709458"
---
# <a name="deploy-resource-access-profiles-in-configuration-manager"></a>Bereitstellen von Ressourcenzugriffsprofilen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Nachdem Sie eines der folgenden Ressourcenzugriffsprofile erstellt haben, stellen Sie es für eine oder mehrere Sammlungen bereit:

- [WLAN](create-wifi-profiles.md)
- [VPN](create-vpn-profiles.md)
- [Zertifikat](create-certificate-profiles.md)

Wenn Sie diese Profile bereitstellen, geben Sie die Zielsammlung an und legen fest, wie oft der Client das Profil auf Konformität bewerten soll.  

## <a name="deploy-a-profile"></a>Profil bereitstellen

1. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**. Erweitern Sie **Konformitätseinstellungen**und **Zugriff auf Unternehmensressourcen**, und wählen Sie dann den entsprechenden Profilknoten aus. Beispielsweise **WLAN-Profile**.

1. Wählen Sie in der Liste von Profilen das Profil aus, das Sie bereitstellen möchten. Wählen Sie dann auf der Registerkarte **Home** des Menübands unter der **Bereitstellungsgruppe** die Option **Bereitstellen** aus.  

1. Geben Sie im Fenster „Profil bereitstellen“ die folgenden Informationen an:  

    - **Sammlung:** Wählen Sie die Sammlung aus, in der Sie das Profil bereitstellen möchten.

    - **Warnung generieren:** Aktivieren Sie diese Option, um eine Warnung konfigurieren zu können. Diese Warnung wird von der Site generiert, wenn die Profilkonformität am angegebenen Datum und der angegebenen Uhrzeit unter dem festgelegten Prozentwert liegt. Sie können außerdem auswählen, ob eine Warnung an System Center Operations Manager gesendet werden soll.

    - **Zufällige Verzögerung (Stunden):** Geben Sie ein Verzögerungsfenster an für Zertifikatprofile, die Einstellungen für Simple Certificate Enrollment Protocol (SCEP) enthalten, um übermäßige Verarbeitung im Registrierungsdienst für Netzwerkgeräte zu vermeiden. Der Standardwert beträgt `64` Stunden.  

    - **Geben Sie den Zeitplan für die Konformitätsauswertung dieses ... Profils an**: Geben Sie an, wie oft der Client die Konformität für dieses Profil auswerten soll. Wählen Sie einen **einfachen Zeitplan** aus, oder konfigurieren Sie einen **benutzerdefinierten Zeitplan**. Standardmäßig ist das Intervall des einfachen Zeitplans auf `12` Stunden eingestellt.

1. Klicken Sie auf **OK**, um das Fenster zu schließen und die Bereitstellung zu erstellen.

## <a name="delete-a-deployment"></a>Löschen einer Bereitstellung

Wenn Sie eine Bereitstellung löschen möchten, wählen Sie sie aus der Liste aus. Wechseln Sie im Detailbereich zur Registerkarte **Bereitstellungen**. Wählen Sie die Bereitstellung und dann auf der Registerkarte **Bereitstellung** des Menübands die Option **Löschen** aus.

> [!IMPORTANT]
> Wenn Sie eine VPN-Profil Bereitstellung entfernen, entfernt Configuration Manager das VPN-Profil nicht aus Windows. Wenn Sie das Profil von dem Gerät löschen möchten, entfernen Sie es manuell.

## <a name="next-steps"></a>Nächste Schritte

[Überwachen von WLAN- und VPN-Profilen](monitor-wifi-email-vpn-profiles.md)

[Überwachen von Zertifikatprofilen](monitor-certificate-profiles.md)
