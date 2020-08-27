---
title: Workloads für die Co-Verwaltung
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über die Workloads, die Sie von Configuration Manager in Microsoft Intune verschieben können.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 08/20/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.assetid: 4c90befe-9c4e-4c27-a947-625887e15052
ms.openlocfilehash: e44576401d601c8c510aaf50b28e5924f5c4d6db
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88694864"
---
# <a name="co-management-workloads"></a>Workloads für die Co-Verwaltung

Sie müssen die Workloads nicht wechseln, oder Sie können sie einzeln ausführen, wenn Sie bereit sind. Configuration Manager verwaltet weiterhin alle anderen Workloads (einschließlich der Workloads, die Sie nicht an Intune übergeben) und alle anderen Funktionen von Configuration Manager, die die Co-Verwaltung nicht unterstützt.

Wenn Sie eine Workload erst auf Intune umstellen, später aber Ihre Meinung ändern, können Sie wieder zurück zu Configuration Manager wechseln.

Die Co-Verwaltung unterstützt die folgenden Workloads:

- [Kompatibilitätsrichtlinien](#compliance-policies)  

- [Windows Update-Richtlinien](#windows-update-policies)  

- [Ressourcenzugriffsrichtlinien](#resource-access-policies)  

- [Endpoint Protection](#endpoint-protection)  

- [Gerätekonfiguration](#device-configuration)  

- [Office-Klick-und-Los-Apps](#office-click-to-run-apps)  

- [Client-Apps](#client-apps)  

## <a name="compliance-policies"></a>Kompatibilitätsrichtlinien

Konformitätsrichtlinien definieren die Regeln und Einstellungen, die ein Gerät erfüllen muss, damit es als mit bedingten Zugriffsrichtlinien konform eingestuft wird. Verwenden Sie Konformitätsrichtlinien außerdem, um Konformitätsprobleme bei Geräten unabhängig von bedingten Zugriffsrechten zu überwachen und zu beheben. Ab Version 1910 von Configuration Manager können Sie die Auswertung benutzerdefinierter Konfigurationsbaselines als Regel für die Konformitätsrichtlinienbewertung hinzufügen. Weitere Informationen finden Sie unter [Einbeziehen benutzerdefinierter Konfigurationsbaselines im Rahmen der Konformitätsrichtlinienbewertung](../compliance/deploy-use/create-configuration-baselines.md#bkmk_CAbaselines).

Weitere Informationen zu diesem Intune-Feature finden Sie unter [Kompatibilitätsrichtlinien für Geräte](/intune/device-compliance-get-started).  

## <a name="windows-update-policies"></a>Windows Update-Richtlinien

Mit Windows Update for Business-Richtlinien können Sie Zurückstellungsrichtlinien für Funktionsupdates unter Windows 10 oder für Qualitätsupdates für Windows 10-Geräte konfigurieren, die direkt von Windows Update for Business verwaltet werden.

Weitere Informationen zu diesem Intune-Feature finden Sie unter [Konfigurieren von Windows Update for Business-Zurückstellungsrichtlinien](/intune/windows-update-for-business-configure).  

## <a name="resource-access-policies"></a>Ressourcenzugriffsrichtlinien

Mit Ressourcenzugriffsrichtlinien werden VPN-, WLAN, E-Mail- und Zertifikateinstellungen auf Geräten konfiguriert.

Weitere Informationen zu diesem Intune-Feature finden Sie unter [Bereitstellen von Ressourcenzugriffsprofilen](/intune/device-profiles).

> [!Note]  
> Die Workload für den Ressourcenzugriff ist auch Teil der Gerätekonfiguration. Diese Richtlinien werden von Intune verwaltet, wenn Sie die Workload für die [Gerätekonfiguration](#device-configuration) wechseln.

## <a name="endpoint-protection"></a>Endpoint Protection

<!--1357365-->

Die Endpoint Protection-Workload umfasst die Windows Defender-Suite mit Antischadsoftware-Schutzfunktionen:

- Windows Defender-Antischadsoftware
- Windows Defender Application Guard  
- Windows Defender Firewall  
- Windows Defender-SmartScreen  
- Windows-Verschlüsselung
- Windows Defender Exploit Guard  
- Windows Defender Application Control  
- Windows Defender Security Center  
- Windows Defender Advanced Threat Protection (wird jetzt Microsoft Defender Advanced Threat Protection genannt)

Weitere Informationen zu diesem Intune-Feature finden Sie unter [Endpoint Protection für Microsoft Intune](/intune/endpoint-protection-windows-10).

> [!Note]  
> Wenn Sie diese Workload wechseln, werden die Configuration Manager-Richtlinien auf dem Gerät beibehalten, bis sie von den Intune-Richtlinien überschrieben werden. Mit diesem Verhalten wird sichergestellt, dass das Gerät während des Übergangs über Schutzrichtlinien verfügt.
>
> Die Endpoint Protection-Workload ist auch Teil der Gerätekonfiguration. Das gleiche Verhalten wird angewendet, wenn Sie die Workload für die [Gerätekonfiguration](#device-configuration) wechseln.<!-- SCCMDocs.nl-nl issue #4 --> Wenn Sie die Workload für die Gerätekonfiguration wechseln, umfasst diese auch Richtlinien für die Windows Information Protection-Funktion, die nicht in der Endpoint Protection-Workload enthalten ist.<!-- 4184095 -->
>
> Die Microsoft Defender Antivirus-Einstellungen, die Bestandteil des Profiltyps „Geräteeinschränkungen“ für die Intune-Gerätekonfiguration sind, sind nicht im Bereich des Schiebereglers für den Endpunktschutz enthalten. Verwenden Sie zum Verwalten von Microsoft Defender Antivirus für gemeinsam verwaltete Geräte mit aktiviertem Endpunktschutz-Schieberegler die neuen Antivirenrichtlinien in **Microsoft Endpoint Manager Admin Center** > **Endpunktsicherheit** > **Virenschutz**. Für den neuen Richtlinientyp sind neue und verbesserte Optionen verfügbar, außerdem werden alle im Profil „Geräteeinschränkungen“ vorhandenen Einstellungen unterstützt. <!--6609171-->
>
> Das Windows-Verschlüsselungsfeature beinhaltet die BitLocker-Verwaltung. Weitere Informationen zum Verhalten dieses Features bei der Co-Verwaltung finden Sie unter [Bereitstellen von BitLocker-Verwaltungs](../protect/deploy-use/bitlocker/deploy-management-agent.md#co-management-and-intune).<!-- SCCMDocs#2321 -->

## <a name="device-configuration"></a>Gerätekonfiguration

<!--1357903-->

Die Gerätekonfigurationsworkload umfasst Einstellungen, die Sie für Geräte in Ihrer Organisation verwalten. Das Wechseln dieser Workload verschiebt auch die Workloads **Ressourcenzugriff** und **Endpoint Protection**.

Sie können immer noch Einstellungen von Configuration Manager für gemeinsam verwaltete Geräte bereitstellen, obwohl Intune die Autorität für die Gerätekonfiguration inne hat. Diese Ausnahme kann verwendet werden, um Einstellungen zu konfigurieren, die Ihre Organisation benötigt, die aber noch nicht in Intune verfügbar sind. Geben Sie diese Ausnahme in einer [Configuration Manager-Konfigurationsbaseline](../compliance/deploy-use/create-configuration-baselines.md) an. Aktivieren Sie bei der Erstellung der Baselinie die Option **Diese Baseline auch immer für gemeinsam verwaltete Clients anwenden**. Sie können sie später auf der Registerkarte **Allgemein** der Eigenschaften einer vorhandenen Baseline ändern.  

Weitere Informationen zu diesem Intune-Feature finden Sie unter [Erstellen eines Geräteprofils in Microsoft Intune](/intune/device-profile-create).  

> [!NOTE]
> Wenn Sie die Workload für die Gerätekonfiguration wechseln, umfasst diese auch Richtlinien für die Windows Information Protection-Funktion, die nicht in der Endpoint Protection-Workload enthalten ist.<!-- 4184095 -->

## <a name="office-click-to-run-apps"></a>Office-Klick-und-Los-Apps

<!--1357841-->

Diese Workload verwaltet Microsoft 365 Apps auf gemeinsam verwalteten Geräten.

- Nachdem die Workload verschoben wurde, wird die App auf dem Gerät im **Unternehmensportal** angezeigt.  

- Es kann etwa 24 Stunden dauern, bis Office-Updates im Client angezeigt werden, es sei denn, die Geräte werden neu gestartet.  

- Es gibt die neue globale Bedingung **Are Office 365 applications managed by Intune on the device** (Werden Office 365-Anwendungen auf dem Gerät mit Intune verwaltet?). Diese Bedingung wird neuen Office 365-Anwendungen standardmäßig als Anforderung hinzugefügt. Wenn Sie diese Workload übertragen, entsprechen gemeinsam verwaltete Clients nicht den Anforderungen der Anwendung. Daher sollten sie Office 365 nicht über Configuration Manager installieren.  

Weitere Informationen zu diesem Intune-Feature finden Sie unter [Zuweisen von Office 365-Apps zu Windows 10-Geräten mit Microsoft Intune](/intune/apps-add-office365).

## <a name="client-apps"></a>Client-Apps

<!--1357892-->

Verwenden Sie Intune zum Verwalten von Client-Apps und PowerShell-Skripts auf gemeinsam verwalteten Windows 10-Geräten. Nachdem Sie diese Workload umgestellt haben, sind alle über Intune bereitgestellten verfügbaren Apps im Unternehmensportal verfügbar. Apps, die Sie im Configuration Manager bereitstellen, sind im Softwarecenter verfügbar.

Weitere Informationen zu diesem Intune-Feature finden Sie unter [Was ist Microsoft Intune-App-Verwaltung?](/intune/app-management).

> [!Tip]  
> Dieses Feature wurde erstmals in Version 1806 als [Vorabfeature](../core/servers/manage/pre-release-features.md) eingeführt. Ab Version 2002 ist es kein Vorabfeature mehr.  
>
> Diese Funktion wird in der Featureliste möglicherweise als **Mobile Apps für gemeinsam verwaltete Geräte** angezeigt.<!-- 5849669 -->

Wenn Sie ab Version 1910 Microsoft Connected Cache auf Ihren Configuration Manager-Verteilungspunkten aktivieren, können sie nun Microsoft Intune Win32-Apps für gemeinsam verwaltete Clients verarbeiten. Weitere Informationen finden Sie unter [Microsoft Connected Cache in Configuration Manager](../core/plan-design/hierarchy/microsoft-connected-cache.md#bkmk_intune).

## <a name="diagram-for-app-workloads"></a>Diagramm zu App-Workloads

:::image type="content" source="media/co-management-apps.svg" alt-text="Diagramm zu App-Workloads für die Co-Verwaltung" lightbox="media/co-management-apps.svg":::

> [!TIP]
> Ab Version 2006 können Sie das Unternehmensportal so konfigurieren, dass auch Configuration Manager-Apps angezeigt werden. Wenn Sie diese App-Portalumgebung ändern, werden die im obigen Diagramm beschriebenen Verhaltensweisen geändert. Weitere Informationen finden Sie unter [Verwenden der Unternehmensportal-App auf gemeinsam verwalteten Geräten](company-portal.md).<!--CMADO-3601237,INADO-4297660-->

## <a name="known-issues"></a>Bekannte Probleme

Wenn die Endpoint Protection-Workload zu Intune verschoben wird, berücksichtigt der Client Richtlinien, die von Configuration Manager und Microsoft Defender festgelegt wurden, möglicherweise weiterhin. <!--5024559-->

Um dieses Problem zu umgehen, wenden Sie mithilfe von ConfigSecurityPolicy.exe CleanUpPolicy.xml an, nachdem die Intune-Richtlinien vom Clientcomputer empfangen wurden. Gehen Sie dazu wie folgt vor:

1. Kopieren Sie den folgenden Text, und speichern Sie ihn als `CleanUpPolicy.xml`.

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <SecurityPolicy xmlns="http://forefront.microsoft.com/FEP/2010/01/PolicyData" Name="FEP clean-up policy"><PolicySection Name="FEP.AmPolicy"><LocalGroupPolicySettings><IgnoreKey Name="SOFTWARE\Policies\Microsoft\Microsoft Antimalware"/><IgnoreKey Name="SOFTWARE\Policies\Microsoft\Windows Defender"/></LocalGroupPolicySettings></PolicySection></SecurityPolicy>
   ```

1. Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten bei `ConfigSecurityPolicy.exe`. Normalerweise befindet sich diese ausführbare Datei in einem der folgenden Verzeichnisse:
   - C:\Programme\Windows Defender
   - C:\Programme\Microsoft Security Client

1. Übergeben Sie an der Eingabeaufforderung die XML-Datei, um die Richtlinie zu bereinigen. Beispiel: `ConfigSecurityPolicy.exe C:\temp\CleanUpPolicy.xml`.  

## <a name="next-steps"></a>Nächste Schritte

[Verschieben von Workloads](how-to-switch-workloads.md)