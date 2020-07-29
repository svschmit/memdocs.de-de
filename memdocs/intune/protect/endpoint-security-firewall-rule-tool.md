---
title: Tool für die Migration der Firewallregeln zur Endpunktsicherheit für Microsoft Intune – Azure | Microsoft-Dokumentation
description: In diesem Artikel erfahren Sie, wie Sie das Migrationstool für Firewallregeln zur Endpunktsicherheit für Microsoft Intune verwenden.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/14/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
mr.reviewer: mattsha
ms.openlocfilehash: 7dd6d3a01d18e4d8b334bdeee3f72eeaeed67c0a
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2020
ms.locfileid: "86465000"
---
# <a name="endpoint-security-firewall-rule-migration-tool-overview"></a>Übersicht über das Migrationstool für Firewallregeln zur Endpunktsicherheit

Viele Organisation möchten ihre Sicherheitskonfiguration zum Endpoint Manager von Microsoft migrieren, um von der modernen cloudbasierten Verwaltung zu profitieren.

Die Endpunktsicherheit im Endpoint Manager bietet umfassende Verwaltungsfunktionen für die Windows Firewall-Konfiguration und die präzise Verwaltung von Firewallregeln.

In vielen Organisationen werden bereits Gruppenrichtlinien verwendet, um Windows-Firewallregeln zu verwalten. Die Migration zur modernen Verwaltung kann komplex sein, da das manuelle Erstellen von Hunderten Firewallregeln sehr ermüdend sein kann.

Zur Unterstützung der Kunden bei der Migration ihrer Firewallregelkonfiguration zu Endpunktsicherheitsrichtlinien im Endpoint Manager wurde das **Migrationstool für Firewallregeln zur Endpunktsicherheit** entwickelt.

Kunden können das **Migrationstool für Firewallregeln zur Endpunktsicherheit** auf einem vorkonfigurierten Windows 10-Client ausführen und automatisch Firewallregelrichtlinien für die Endpunktsicherheit im Endpoint Manager erstellen. Sobald diese erstellt wurden, können Administratoren diese Regeln für Azure AD-Gruppen verwenden, um die mobile Geräteverwaltung und gemeinsam verwaltete Clients zu konfigurieren.

Laden Sie das [Migrationstool für Firewallregeln zur Endpunktsicherheit](https://aka.ms/EndpointSecurityFWRuleMigrationTool) herunter:<br>
<a href="https://aka.ms/EndpointSecurityFWRuleMigrationTool"><img alt="Download the tool" src="./media/endpoint-security-firewall-rule-tool/downloadtool.png" width="170"></a>

## <a name="tool-usage"></a>Verwenden des Tools

Das Tool wird auf einem Referenzcomputer ausgeführt und migriert die aktuelle Windows-Firewallregelkonfiguration. Durch die Ausführung des Tools werden alle auf dem Gerät vorhandenen, aktivierten Firewallregeln exportiert, und neue Intune-Richtlinien werden automatisch anhand der erfassten Regeln erstellt.

1. Melden Sie sich mit lokalen Administratorrechten beim Referenzcomputer an.
2. Laden Sie die Datei `Export-FirewallRules.zip` herunter, und entpacken Sie diese. <br>
   Die ZIP-Datei enthält die Skriptdatei `Export-FirewallRules.ps1`. 
3. Führen Sie das Skript `Export-FirewallRules.ps1` auf dem Computer aus. <br>
   Das Skript lädt alle für die Ausführung erforderlichen Komponenten herunter. Geben Sie die entsprechenden Intune-Administratoranmeldeinformationen ein, wenn Sie dazu aufgefordert werden. Weitere Informationen zu den erforderlichen Berechtigungen finden Sie unter [Erforderliche Berechtigungen](#required-permissions).
4. Geben Sie einen Richtliniennamen ein, wenn Sie dazu aufgefordert werden. <br>
   Diese Richtlinie wird im [Microsoft Endpoint Manager](https://go.microsoft.com/fwlink/?linkid=2109431) im Bereich **Endpunktsicherheit** > **Firewall** angezeigt. 

    > [!IMPORTANT]
    > Der Richtlinienname muss für den Mandanten eindeutig sein.

    Wenn mehr als 150 Firewallregeln gefunden werden, werden mehrere Richtlinien erstellt.

    > [!NOTE]
    > Standardmäßig werden nur aktivierte Firewallregeln migriert. Außerdem werden standardmäßig nur Firewallregeln migriert, die vom GPO (Gruppenrichtlinienobjekt) erstellt wurden. Zum Anpassen dieser Standardwerte werden Optionen bereitgestellt. Weitere Informationen finden Sie unter [Optionen](#switches).
    >
    > Abhängig von der Anzahl der gefundenen Firewallregeln erfordert die Ausführung des Tools möglicherweise mehr Zeit.

5. Sobald die Ausführung abgeschlossen ist, gibt das Tool eine Anzahl der Firewallregeln aus, die nicht automatisch migriert werden konnten. Weitere Informationen finden Sie unter [Nicht unterstützte Konfigurationen](#unsupported-configuration).

## <a name="switches"></a>Optionen

Sie können die folgenden Optionen (Parameter) verwenden, um die Standardfunktionalität des Tools zu ändern.

- `IncludeLocalRules`: Mit dieser Option werden alle lokal erstellten bzw. standardmäßigen Windows-Firewallregeln in den Exportvorgang eingeschlossen. Beachten Sie, dass das Aktivieren dieser Option dazu führen kann, dass viele Regeln eingeschlossen werden. 
- `IncludedDisabledRules`: Mit dieser Option werden alle aktivierten und deaktivierten Windows-Firewallregeln in den Exportvorgang eingeschlossen. Beachten Sie, dass das Aktivieren dieser Option dazu führen kann, dass viele Regeln eingeschlossen werden.

## <a name="unsupported-configuration"></a>Nicht unterstützte Konfigurationen

Die folgenden auf der Registrierung basierenden Einstellungen werden aufgrund mangelnder MDM-Unterstützung in Windows nicht unterstützt. Diese Einstellungen sind selten. Sollten Sie diese Einstellungen dennoch benötigen, sollten Sie dies über Ihre Standardsupportkanäle melden.

|     GPO-Feld    |     Grund    |
|-|-|
|      TYPE-VALUE =/ "Security=" IFSECURE-VAL    |     Dies ist eine IPSec-bezogene Einstellung, die nicht von der mobilen Geräteverwaltung von Windows unterstützt wird.    |
|      TYPE-VALUE =/ "Security2_9=" IFSECURE2-9-VAL    |     Dies ist eine IPSec-bezogene Einstellung, die nicht von der mobilen Geräteverwaltung von Windows unterstützt wird.    |
|      TYPE-VALUE =/ "Security2=" IFSECURE2-10-VAL     |     Dies ist eine IPSec-bezogene Einstellung, die nicht von der mobilen Geräteverwaltung von Windows unterstützt wird.    |
|      TYPE-VALUE =/ "IF=" IF-VAL    |     Die Schnittstellenkennung (LUID) kann nicht verwaltet werden.    |
|      TYPE-VALUE =/ "Defer=" DEFER-VAL    |     Eingehender NAT-Durchlauf wird nicht über Gruppenrichtlinien oder die mobile Geräteverwaltung von Windows zur Verfügung gestellt.    |
|      TYPE-VALUE =/ "LSM=" BOOL-VAL    |     Lockere Quellzuordnungsdateien werden nicht über Gruppenrichtlinien oder die mobile Geräteverwaltung von Windows zur Verfügung gestellt.    |
|      TYPE-VALUE =/ "Platform=" PLATFORM-VAL    |     Die Betriebssystem-Versionsverwaltung wird nicht über Gruppenrichtlinien oder die mobile Geräteverwaltung von Windows zur Verfügung gestellt.    |
|      TYPE-VALUE =/ "RMauth=" STR-VAL    |     Dies ist eine IPSec-bezogene Einstellung, die nicht von der mobilen Geräteverwaltung von Windows unterstützt wird.    |
|      TYPE-VALUE =/ "RUAuth=" STR-VAL    |     Dies ist eine IPSec-bezogene Einstellung, die nicht von der mobilen Geräteverwaltung von Windows unterstützt wird.    |
|      TYPE-VALUE =/ "AuthByPassOut=" BOOL-VAL    |     Dies ist eine IPSec-bezogene Einstellung, die nicht von der mobilen Geräteverwaltung von Windows unterstützt wird.    |
|      TYPE-VALUE =/ "LOM=" BOOL-VAL    |     Nur lokal zugeordnete Regeln werden nicht über Gruppenrichtlinien oder die mobile Geräteverwaltung von Windows zur Verfügung gestellt.    |
|      TYPE-VALUE =/ "Platform2=" PLATFORM-OP-VAL    |     Redundante Einstellungen werden nicht über Gruppenrichtlinien oder die mobile Geräteverwaltung von Windows zur Verfügung gestellt.    |
|      TYPE-VALUE =/ "PCross=" BOOL-VAL    |     Das Zulassen von Profilüberschreitungen wird nicht über Gruppenrichtlinien oder die mobile Geräteverwaltung von Windows zur Verfügung gestellt.    |
|      TYPE-VALUE =/ "LUOwn=" STR-VAL    |     Die Besitzer-SID des lokalen Benutzers gilt nicht für die mobile Geräteverwaltung.    |
|      TYPE-VALUE =/ "TTK=" TRUST-TUPLE-KEYWORD-VAL    |     Das Anpassen des Datenverkehrs mit dem vertrauenswürdigen Tupel-Schlüsselwort wird nicht über Gruppenrichtlinien oder die mobile Geräteverwaltung von Windows zur Verfügung gestellt.    |
|      TYPE-VALUE =/ “TTK2_22=” TRUST-TUPLE-KEYWORD-VAL2-22    |     Das Anpassen des Datenverkehrs mit dem vertrauenswürdigen Tupel-Schlüsselwort wird nicht über Gruppenrichtlinien oder die mobile Geräteverwaltung von Windows zur Verfügung gestellt.    |
|      TYPE-VALUE =/ “TTK2_27=” TRUST-TUPLE-KEYWORD-VAL2-27    |     Das Anpassen des Datenverkehrs mit dem vertrauenswürdigen Tupel-Schlüsselwort wird nicht über Gruppenrichtlinien oder die mobile Geräteverwaltung von Windows zur Verfügung gestellt.    |
|      TYPE-VALUE =/ “TTK2_28=” TRUST-TUPLE-KEYWORD-VAL2-28    |     Das Anpassen des Datenverkehrs mit dem vertrauenswürdigen Tupel-Schlüsselwort wird nicht über Gruppenrichtlinien oder die mobile Geräteverwaltung von Windows zur Verfügung gestellt.    |
|      TYPE-VALUE =/ "NNm=" STR-ENC-VAL    |     Dies ist eine IPSec-bezogene Einstellung, die nicht von der mobilen Geräteverwaltung von Windows unterstützt wird.    |
|      TYPE-VALUE =/ "SecurityRealmId=" STR-VAL    |     Dies ist eine IPSec-bezogene Einstellung, die nicht von der mobilen Geräteverwaltung von Windows unterstützt wird.    |

## <a name="unsupported-setting-values"></a>Nicht unterstützte Einstellungswerte
Die folgenden Einstellungswerte werden nicht für die Migration unterstützt:

**Ports**
- `PlayToDiscovery` wird nicht als lokaler oder Remoteportbereich unterstützt.

**Adressbereiche**
- `LocalSubnet6` wird nicht als lokaler oder Remoteadressbereich unterstützt. 
- `LocalSubnet4` wird nicht als lokaler oder Remoteadressbereich unterstützt.
- `PlatToDevice` wird nicht als lokaler oder Remoteadressbereich unterstützt.

Sobald das Tool ausgeführt wurde, wird ein Bericht mit den Regeln generiert, die nicht erfolgreich migriert wurden. Sie können diese Regeln einsehen, indem Sie `RulesError.csv` in `C:\<folder needed>` anzeigen. 

## <a name="required-permissions"></a>Erforderliche Berechtigungen
Der Endpunktsicherheits-Manager, Intune-Dienstadministratoren oder globale Administratorbenutzer können Windows-Firewallregeln zu Endpunktsicherheitsrichtlinien migrieren. Alternativ kann eine benutzerdefinierte Rolle verwendet werden, der Berechtigungen für Sicherheitsbaselines zum **Löschen**, **Lesen**, **Zuweisen**, **Erstellen** und **Aktualisieren** zugewiesen wurden. Weitere Informationen finden Sie unter [Gewähren von Administratorberechtigungen für Intune](../fundamentals/users-add.md#grant-admin-permissions).

## <a name="next-steps"></a>Nächste Schritte

- Weisen Sie die Regeln Azure AD-Gruppen zu, um die mobile Geräteverwaltung und gemeinsam verwaltete Clients zu konfigurieren. Weitere Informationen finden Sie unter [Hinzufügen von Gruppen zum Organisieren von Benutzern und Geräten](../fundamentals/groups-add.md).
