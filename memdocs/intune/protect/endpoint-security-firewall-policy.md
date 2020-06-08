---
title: Verwalten von Firewalleinstellungen mit Endpunktsicherheitsrichtlinien in Microsoft Intune | Microsoft-Dokumentation
description: Konfigurieren und Bereitstellen von Richtlinien für Geräte, die Sie mithilfe von Firewallrichtlinien für Endpunktsicherheit in Microsoft Endpoint Manager verwalten.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: f98d7a30d219aee63e38a63a74d8f1713deb198a
ms.sourcegitcommit: 48005a260bcb2b97d7fe75809c4bf1552318f50a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2020
ms.locfileid: "83431617"
---
# <a name="firewall-policy-for-endpoint-security-in-intune"></a>Firewallrichtlinie für Endpunktsicherheit in Intune

Verwenden Sie die Firewallrichtlinie für Endpunktsicherheit in Intune, um eine integrierte Firewall für Geräte zu konfigurieren, die unter macOS und Windows 10 ausgeführt werden. Integrierte Firewalls sind in BitLocker für Windows-Geräten und FileVault für macOS enthalten.

Obwohl Sie die gleichen Firewalleinstellungen mithilfe von Endpoint Protection-Profilen für die Gerätekonfiguration konfigurieren können, enthalten die Gerätekonfigurationsprofile zusätzliche Einstellungskategorien. Diese zusätzlichen Einstellungen stehen nicht im Zusammenhang mit Firewalls und können die Konfiguration reiner Firewalleinstellungen für Ihre Umgebung erschweren.

Die Endpunktsicherheitsrichtlinien für Firewalls finden Sie unter *Verwalten* im Knoten **Endpunktsicherheit** des [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).

Zeigen Sie die [Einstellungen für Firewallprofile](../protect/endpoint-security-Firewall-profile-settings.md) an.

## <a name="prerequisites-for-firewall-profiles"></a>Voraussetzungen für Firewallprofile

- Windows 10 oder höher
- Eine unterstützte Version von macOS

## <a name="firewall-profiles"></a>Firewallprofile

**macOS-Profile**:

- **macOS-Firewall**: Aktivieren und konfigurieren Sie Einstellungen für die integrierte Firewall unter macOS.

**Windows 10-Profile**:

- **Microsoft Defender Firewall**: Konfigurieren Sie Einstellungen für Windows Defender Firewall mit erweiterter Sicherheit. Windows Defender Firewall bietet hostbasierte, bidirektionale Filterung des Netzwerkdatenverkehrs für ein Gerät und kann nicht autorisierten eingehenden und ausgehenden Netzwerkdatenverkehr auf dem Gerät blockieren.

- **Microsoft Defender Firewall-Regeln** *(Vorschau)* : Definieren Sie differenzierte Firewallregeln mit bestimmten Ports, Protokollen, Anwendungen und Netzwerken, um Netzwerkdatenverkehr zuzulassen oder zu blockieren. Jede Instanz dieses Profils unterstützt bis zu 150 benutzerdefinierte Regeln.

## <a name="firewall-rule-mergers-and-policy-conflicts"></a>Zusammenführungen von Firewallregeln und Richtlinienkonflikte

Planen Sie Firewallrichtlinien, die mit nur einer Richtlinie auf ein Gerät angewendet werden. Durch die Verwendung einer einzelnen Richtlinieninstanz und eines Richtlinientyps wird verhindert, dass zwei separate Richtlinien verschiedene Konfigurationen auf dieselbe Einstellung anwenden, wodurch Konflikte entstehen. Wenn zwischen zwei Richtlinieninstanzen oder Typen von Richtlinien, die dieselbe Einstellung mit unterschiedlichen Werten verwalten, ein Konflikt besteht, wird die Einstellung nicht an das Gerät gesendet.

- Diese Art von Richtlinienkonflikt gilt für das **Microsoft Defender Firewall**-Profil, das mit anderen Microsoft Defender Firewall-Profilen in Konflikt stehen kann, oder eine Firewallkonfiguration, die von einem anderen Richtlinientyp bereitgestellt wird, etwa von einer Gerätekonfiguration.

  Microsoft *Defender Firewall-Profile* stehen nicht mit *Microsoft Defender Firewall-Regelprofilen* in Konflikt.

Wenn Sie **Microsoft Defender Firewall-Regelprofile** verwenden, können Sie mehrere Regelprofile auf dasselbe Gerät anwenden. Wenn jedoch unterschiedliche Regeln für denselben Zweck mit unterschiedlichen Konfigurationen vorhanden sind, werden beide an das Gerät gesendet und verursachen einen Konflikt auf diesem Gerät.

- Wenn z. B. eine Regel *Teams.exe* durch die Firewall blockiert und eine zweite Regel *Teams.exe* zulässt, werden beide Regeln an den Client übermittelt. Dieses Ergebnis unterscheidet sich von Konflikten, die durch andere Richtlinien für Firewalleinstellungen verursacht werden.

Wenn Regeln aus mehreren Regelprofilen nicht miteinander in Konflikt stehen, werden die Regeln der einzelnen Profile von den Geräten zusammengeführt, um eine kombinierte Firewallregelkonfiguration auf dem Gerät zu erstellen. Dieses Verhalten ermöglicht es Ihnen, mehr als die 150 Regeln bereitzustellen, die von den einzelnen Profilen für ein Gerät unterstützt werden.

- Beispielsweise verfügen Sie über zwei Microsoft Defender Firewall-Regelprofile. Das erste Profil ermöglicht *Teams.exe* über die Firewall. Das zweite Profil ermöglicht *Outlook.exe* über die Firewall. Wenn ein Gerät beide Profile erhält, wird das Gerät so konfiguriert, dass beide Apps über die Firewall zulässig sind.

## <a name="next-steps"></a>Nächste Schritte

[Konfigurieren von Endpunktsicherheitsrichtlinien](../protect/endpoint-security-policy.md#create-an-endpoint-security-policy)
