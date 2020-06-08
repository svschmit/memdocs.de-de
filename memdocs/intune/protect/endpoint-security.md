---
title: Verwalten der Endpunktsicherheit in Microsoft Intune | Microsoft-Dokumentation
description: Erfahren Sie, wie Sicherheitsadministratoren über den Knoten „Endpunktsicherheit“ die Gerätesicherheit verwalten und Probleme mit Geräten in Microsoft Endpoint Manager beheben können.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: mattsha
ms.openlocfilehash: 99ac1e069386c69011543ac40878dd62a0d50527
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83990826"
---
# <a name="manage-endpoint-security-in-microsoft-intune"></a>Verwalten der Endpunktsicherheit in Microsoft Intune

Als Sicherheitsadministrator verwenden Sie den Knoten *Endpunktsicherheit* in Intune, um die Gerätesicherheit zu konfigurieren und Sicherheitsaufgaben für Geräte zu verwalten, wenn für diese Geräte ein Risiko besteht. Mit den Endpunktsicherheitsrichtlinien können Sie Sicherheitseinstellungen für Ihre Geräte festlegen und Risiken mindern. Mithilfe der verfügbaren Aufgaben lassen sich Geräte ermitteln, für die ein Risiko besteht. Anschließend können Sie die vorliegenden Probleme behandeln und dafür sorgen, dass die Geräte erneut Ihren Sicherheitsvorgaben entsprechen.

Im Knoten „Endpunktsicherheit“ werden die über Intune verfügbaren Tools gruppiert, mit denen Sie die Sicherheit Ihrer Geräte überprüfen und gewährleisten:

- **Überprüfen des Status all Ihrer verwalteten Geräte**. In der Ansicht [Alle Geräte](#manage-devices) können Sie eine allgemeine Übersicht über den Konformitätsstatus Ihrer Geräte anzeigen. Außerdem können Sie Details für bestimmte Geräte aufrufen, um herauszufinden, mit welchen Richtlinien diese Geräte nicht übereinstimmen.

- **Bereitstellen von Sicherheitsbaselines, mit denen Sicherheitskonfigurationen für Geräte definiert werden, die Best Practices entsprechen**. Intune umfasst [Sicherheitsbaselines](#manage-security-baselines) für Windows-Geräte sowie verschiedene Anwendungen wie beispielsweise Microsoft Defender Advanced Threat Protection (Defender ATP) und Microsoft Edge. Sicherheitsbaselines sind vorkonfigurierte Gruppen von Windows-Einstellungen, die Ihnen helfen, eine bekannte Zusammenstellung von Einstellungen und Standardwerten anzuwenden, die von den maßgeblichen Sicherheitsteams empfohlen werden.

- **Verwalten von Sicherheitskonfigurationen auf Geräten mithilfe spezialisierter Richtlinien**.  Jede [Endpunktsicherheitsrichtlinie](#use-policies-to-manage-device-security) wurde für bestimmte Aspekte der Gerätesicherheit erstellt. Dazu zählen z. B. Antivirus, Datenträgerverschlüsselung, Firewalls und verschiedene andere Bereiche, die durch eine Integration in Defender ATP verfügbar sind.

- **Definieren von Geräte- und Benutzeranforderungen mithilfe einer Konformitätsrichtlinie**. Über [Konformitätsrichtlinien](../protect/device-compliance-get-started.md) werden die Regeln festgelegt, die Geräte und Benutzer einhalten müssen, um als konform eingestuft zu werden. Diese Regeln können Betriebssystemversionen, Kennwortanforderungen, Gerätebedrohungsstufen usw. umfassen.

  Wenn Sie [Azure AD-Richtlinien für bedingten Zugriff](#configure-conditional-access) (Azure Active Directory) zum Erzwingen von Konformitätsrichtlinien integrieren, können Sie den Zugriff auf Unternehmensressourcen für verwaltete Geräte und Geräte, die noch nicht verwaltet werden, steuern.

- **Integration von Intune in Microsoft Defender ATP**. Durch die [Integration in Defender ATP](#set-up-integration-with-defender-atp) erhalten Sie Zugang zu [Sicherheitsaufgaben](#review-security-tasks-from-defender-atp). Mit Sicherheitsaufgaben werden Defender ATP und Intune eng miteinander verknüpft, damit Ihr Sicherheitsteam Geräte ermitteln kann, bei denen ein Risiko vorliegt. Anschließend können diese Mitarbeiter die Intune-Administratoren über die genauen Schritte informieren, mit denen sich die vorliegenden Risiken beseitigen lassen.

In den folgenden Abschnitten werden die verschiedenen Aufgaben erläutert, die Sie über den Knoten „Endpunktsicherheit“ im Admin Center ausführen können. Außerdem werden die Berechtigungen der rollenbasierten Zugriffssteuerung beschrieben, die für die Verwendung der Aufgaben erforderlich sind.

## <a name="manage-devices"></a>Verwalten von Geräten

Der Knoten „Endpunktsicherheit“ umfasst die Ansicht *Alle Geräte*, in der Sie eine Liste aller Geräte in Ihrer Azure AD-Umgebung anzeigen können, die in Microsoft Endpoint Manager verfügbar sind.

Wenn Sie Geräte in dieser Ansicht auswählen, können Sie weitere Informationen zu diesen Geräten anzeigen (z. B. die Richtlinien, mit denen ein Gerät nicht konform ist). Außerdem können Sie über diese Ansicht Probleme für ein Gerät beheben. Sie können beispielsweise ein Gerät neu starten, eine Überprüfung auf Schadsoftware durchführen oder BitLocker-Schlüssel auf einem Windows 10-Gerät rotieren.

Weitere Informationen finden Sie unter [Verwalten von Geräten mit Endpunktsicherheit in Microsoft Intune](../protect/endpoint-security-manage-devices.md).

## <a name="manage-security-baselines"></a>Verwalten von Sicherheitsbaselines

Sicherheitsbaselines in Intune sind vorkonfigurierte Gruppen von Einstellungen, die Best Practice-Empfehlungen der maßgeblichen Microsoft-Sicherheitsteams für das Produkt entsprechen. In Intune werden Sicherheitsbaselines für Windows 10-Geräteeinstellungen, Microsoft Edge, Microsoft Defender Advanced Threat Protection und weitere Anwendungen unterstützt.

Mithilfe von Sicherheitsbaselines lassen sich im Handumdrehen *Best Practice*-Konfigurationen von Geräte- und Anwendungseinstellungen bereitstellen, um Ihre Benutzer und Geräte zu schützen. Sicherheitsbaselines werden bei Geräten mit Windows 10, Version 1809 und höher, unterstützt.

Weitere Informationen finden Sie unter [Konfigurieren von Windows 10-Geräten in Intune mithilfe von Sicherheitsbaselines](../protect/security-baselines.md).

Sicherheitsbaselines sind eine von mehreren Methoden in Intune, mit denen Sie Einstellungen auf Geräten konfigurieren können. Beim Verwalten von Einstellungen sollten Sie wissen, welche weiteren Methoden in Ihrer Umgebung verwendet werden, über die Ihre Geräte konfiguriert werden können. Dies ist wichtig, um Konflikte zu vermeiden. Weitere Informationen finden Sie unter [Vermeiden von Richtlinienkonflikten](#avoid-policy-conflicts) weiter unten in diesem Artikel.

## <a name="review-security-tasks-from-defender-atp"></a>Überprüfen von Sicherheitsaufgaben aus Defender ATP

Wenn Sie Intune in Microsoft Defender Advanced Threat Protection (Defender ATP) integrieren, können Sie die *Sicherheitsaufgaben* in Intune überprüfen, mit denen Geräte ermittelt werden, bei denen ein Risiko vorliegt. Anschließend können Sie die erforderlichen Schritte ausführen, um das jeweilige Risiko zu beseitigen. Über die Aufgaben kann dann eine Meldung an Defender ATP zurückgesendet werden, sobald die Risiken erfolgreich beseitigt wurden.

- Ihr Defender ATP-Team ermittelt die Geräte, bei denen ein Risiko vorliegt, und gibt diese Informationen als Sicherheitsaufgabe an Ihr Intune-Team weiter. Mit nur wenigen Klicks erstellen diese Mitarbeiter eine Sicherheitsaufgabe für Intune, in der die Geräte, die jeweiligen Sicherheitsrisiken sowie die erforderlichen Schritte zum Beseitigen der Risiken enthalten sind.

- Die Intune-Administratoren überprüfen die Sicherheitsaufgaben und führen in Intune die erforderlichen Schritte aus. Nachdem die genannten Risiken beseitigt wurden, wird die Aufgabe als abgeschlossen markiert, und dieser Status wird an das Defender ATP-Team übermittelt.

Mithilfe von Sicherheitsaufgaben sind beide Teams stets darüber informiert, bei welchen Geräten Risiken vorliegen und wann diese Risiken beseitigt werden.

Weitere Informationen zur Verwendung von Sicherheitsaufgaben finden Sie unter [Verwenden von Intune zum Korrigieren von mit Microsoft Defender ATP identifizierten Sicherheitsrisiken](../protect/atp-manage-vulnerabilities.md).

## <a name="use-policies-to-manage-device-security"></a>Verwalten der Gerätesicherheit mithilfe von Richtlinien

Als Sicherheitsadministrator verwenden Sie die Sicherheitsrichtlinien, die im Knoten „Endpunktsicherheit“ unter *Verwalten* aufgeführt sind. Mit diesen Richtlinien können Sie die Gerätesicherheit konfigurieren, ohne dazu die Vielzahl von Einstellungen in den Gerätekonfigurationsprofilen und Sicherheitsbaselines bearbeiten zu müssen.

![Verwalten von Richtlinien](./media/endpoint-security/endpoint-security-policies.png)

Weitere Informationen zur Verwendung dieser Sicherheitsrichtlinien finden Sie unter [Verwalten der Gerätesicherheit mit Endpunktsicherheitsrichtlinien](../protect/endpoint-security-policy.md).

Endpunktsicherheitsrichtlinien sind eine von mehreren Methoden in Intune, mit denen Sie Einstellungen auf Geräten konfigurieren können. Beim Verwalten von Einstellungen sollten Sie wissen, welche weiteren Methoden in Ihrer Umgebung verwendet werden, über die Ihre Geräte konfiguriert werden können. Dies ist wichtig, um Konflikte zu vermeiden. Weitere Informationen finden Sie unter [Vermeiden von Richtlinienkonflikten](#avoid-policy-conflicts) weiter unten in diesem Artikel.

Darüber hinaus finden Sie im Abschnitt *Verwalten* Richtlinien zur *Gerätekonformität* und für den *bedingten Zugriff*. Bei diesen Richtlinien handelt es sich nicht um Sicherheitsrichtlinien für die Konfiguration von Endpunkten, sondern um wichtige Tools für die Verwaltung der Geräte und des Zugriffs auf Ihre Unternehmensressourcen.

## <a name="use-device-compliance-policy"></a>Verwenden von Richtlinien für Gerätekonformität

Mithilfe von Richtlinien für Gerätekonformität legen Sie fest, unter welchen Bedingungen Geräte und Benutzer auf Ihr Netzwerk und Unternehmensressourcen zugreifen können.

Die [verfügbaren Konformitätseinstellungen](../protect/device-compliance-get-started.md#next-steps) hängen von der verwendeten Plattform ab. Nachfolgend sind einige der gängigsten Richtlinienregeln aufgeführt:

- Festlegen, dass auf Geräten eine Mindestversion bzw. eine bestimmte Version eines Betriebssystems ausgeführt werden muss
- Festlegen von Kennwortanforderungen
- Festlegen, welche Gerätebedrohungsstufe maximal zulässig ist. Diese Stufe wird von Defender ATP oder einem anderen Mobile Threat Defense-Partner bestimmt

Zusätzlich zu den Richtlinienregeln unterstützen Konformitätsrichtlinien Folgendes:

- [Standorte](../protect/use-network-locations.md), die Sie in Intune definieren. Bei Verwendung von Standorten mit einer Konformitätsrichtlinie kann mit der Richtlinie sichergestellt werden, dass Geräte mit einem Firmennetzwerk verbunden sind.
- [Aktionen bei Nichtkonformität](../protect/actions-for-noncompliance.md). Diese Aktionen sind eine zeitlich geordnete Abfolge von Aktionen, die auf nicht konforme Geräte angewendet werden. Zu diesen Aktionen zählen u. a. das Senden von E-Mails oder Benachrichtigungen, um Gerätebenutzer über die Nichtkonformität zu informieren. Außerdem können nicht konforme Geräte remote gesperrt oder sogar außer Betrieb genommen werden. Auch das Entfernen von Unternehmensdaten von diesen Geräten ist möglich.

Wenn Sie Intune in [Azure AD-Richtlinien für bedingten Zugriff](#configure-conditional-access) integrieren, um Konformitätsrichtlinien zu erzwingen, können beim bedingten Zugriff Konformitätsdaten verwendet werden, um den Zugriff auf Unternehmensressourcen von verwalteten und nicht verwalteten Geräten zu steuern.

Weitere Informationen finden Sie unter [Legen Sie mit Intune Regeln auf Geräten fest, um Zugriff auf Ressourcen in Ihrer Organisation zu gewähren](../protect/device-compliance-get-started.md).

Richtlinien für Gerätekonformität sind eine von mehreren Methoden in Intune, mit denen Sie Einstellungen auf Geräten konfigurieren können. Beim Verwalten von Einstellungen sollten Sie wissen, welche weiteren Methoden in Ihrer Umgebung verwendet werden, über die Ihre Geräte konfiguriert werden können. Dies ist wichtig, um Konflikte zu vermeiden. Weitere Informationen finden Sie unter [Vermeiden von Richtlinienkonflikten](#avoid-policy-conflicts) weiter unten in diesem Artikel.

## <a name="configure-conditional-access"></a>Konfigurieren des bedingten Zugriffs

Zum Schutz Ihrer Geräte und Unternehmensressourcen können Sie Azure AD-Richtlinien für bedingten Zugriff (Azure Active Directory) mit Intune verwenden.

Intune übergibt die Ergebnisse Ihrer Gerätekonformitätsrichtlinien an Azure AD. Dort wird mithilfe von Richtlinien für bedingten Zugriff erzwungen, welche Geräte und Apps auf Ihre Unternehmensressourcen zugreifen dürfen. Mithilfe von Richtlinien für bedingten Zugriff lässt sich der Zugriff für Geräte steuern, die nicht von Intune verwaltet werden. Sie können sogar Konformitätsdetails von [Mobile Threat Defense-Partnern](../protect/mobile-threat-defense.md) nutzen, die in Intune integriert sind.

Nachfolgend sind zwei gängige Methoden beschrieben, wie der bedingte Zugriff mit Intune verwendet wird:

- **Gerätebasierter bedingter Zugriff**, um sicherzustellen, dass nur verwaltete und konforme Geräte auf Netzwerkressourcen zugreifen können.
- **App-basierter bedingter Zugriff**, bei dem App-Schutzrichtlinien verwendet werden, um den Zugriff auf Netzwerkressourcen durch Benutzer auf Geräten zu steuern, die nicht mit Intune verwaltet werden.

Weitere Informationen zur Verwendung des bedingten Zugriffs mit Intune finden Sie unter [Erfahren Sie mehr zum bedingten Zugriff und Intune](../protect/conditional-access.md).

## <a name="set-up-integration-with-defender-atp"></a>Einrichten der Integration in Defender ATP

Durch die Integration von Microsoft Defender Advanced Threat Protection (Defender ATP) in Intune sind Sie besser in der Lage, Risiken zu ermitteln und zu beseitigen.

Wenngleich Intune die Integration in eine Vielzahl von [Mobile Threat Defense-Partnern](../protect/mobile-threat-defense.md) ermöglicht, bietet die Verwendung von Defender ATP den Vorteil einer nahtlosen Integration von Defender ATP und Intune. Bei dieser Integration profitieren Sie von Zugriff auf umfassende Optionen zum Geräteschutz, wie beispielsweise den folgenden:

- Sicherheitsaufgaben: Nahtlose Kommunikation zwischen ATP- und Intune-Administratoren zu Geräten, bei denen ein Risiko vorliegt. Außerdem können die erforderlichen Schritte zur Risikobeseitigung und eine Bestätigung übermittelt werden, sobald die Risiken beseitigt wurden.
- Optimiertes Onboarding für Defender ATP auf Clients.
- Verwendung von ATP-Geräterisikosignalen in Intune-Konformitätsrichtlinien.
- Zugriff auf Funktionen zum *Manipulationsschutz*.

 Weitere Informationen zur Verwendung von Defender ATP mit Intune finden Sie unter [Erzwingen der Konformität für Microsoft Defender ATP mit bedingtem Zugriff in Intune](../protect/advanced-threat-protection.md).

## <a name="role-based-access-control-requirements"></a>Anforderungen für die rollenbasierte Zugriffssteuerung

Für die Verwaltung von Aufgaben im Knoten „Endpunktsicherheit“ im Admin Center von Microsoft Endpoint Manager benötigt ein Konto Folgendes:

- Eine zugewiesene Lizenz für Intune.
- RBAC-Berechtigungen (Role-Based Access Control, rollenbasierte Zugriffssteuerung), die den Berechtigungen der integrierten Intune-Rolle **Endpunktsicherheits-Manager** entsprechen. Mit der Rolle *Endpunktsicherheits-Manager* erhalten Sie Zugriff auf das Admin Center von Microsoft Endpoint Manager. Diese Rolle kann von Einzelbenutzern für die Verwaltung von Sicherheits- und Konformitätsfeatures verwendet werden (z. B. Sicherheitsbaselines, Gerätekonformität, bedingter Zugriff und Microsoft Defender ATP).

Weitere Informationen finden Sie unter [Rollenbasierte Zugriffssteuerung für Microsoft Intune](../fundamentals/role-based-access-control.md)

### <a name="permissions-granted-by-the-endpoint-security-manager-role"></a>Berechtigungen, die mit der Rolle *Endpunktsicherheits-Manager* erteilt werden

Die folgende Liste mit Berechtigungen befindet sich im Admin Center von Microsoft Endpoint Manager unter **Mandantenverwaltung** > **Rollen** > **Alle Rollen**. Wählen Sie dort **Endpunktsicherheits-Manager** > **Eigenschaften** aus.

**Berechtigungen:**

- **Android for Work**
  - Lesen
- **Überwachungsdaten**
  - Lesen
- **Bezeichner von Unternehmensgeräten**
  - Lesen
- **Gerätekompatibilitätsrichtlinien**
  - Zuweisen
  - Erstellen
  - Löschen
  - Lesen
  - Update
  - Anzeigen von Berichten
- **Gerätekonfigurationen**
  - Lesen
- **Geräteregistrierungs-Manager**
  - Lesen
- **Endpoint Protection-Berichte**
  - Lesen
- **Registrierungsprogramme**
  - Gerät lesen
  - Profil lesen
  - Token lesen
- **Intune Data Warehouse**
  - Lesen
- **Verwaltete Apps**
  - Lesen
- **Verwaltete Geräte**
  - Löschen
  - Lesen
  - Primären Benutzer festlegen
  - Update
- **Mobile Apps**
  - Lesen
- **Organisation**
  - Lesen
- **Richtliniensätze**
  - Lesen
- **Remoteunterstützung**
  - Lesen
- **Remoteaufgaben**
  - FileVault-Schlüssel abrufen
- **Rollen**
  - Lesen
- **Sicherheitsbaselines**
  - Zuweisen
  - Erstellen
  - Löschen
  - Lesen
  - Update
- **Sicherheitsaufgaben**
  - Lesen
  - Update
- **Telekommunikationsausgaben**
  - Lesen
- **Geschäftsbedingungen**
  - Lesen

## <a name="avoid-policy-conflicts"></a>Vermeiden von Richtlinienkonflikten

Eine Vielzahl von Einstellungen, die Sie für Geräte konfigurieren können, lassen sich über unterschiedliche Features in Intune verwalten. Dazu zählen u. a. die folgenden Features:

- Endpunktsicherheitsrichtlinien
- Sicherheitsbaselines
- Richtlinien zur Gerätekonfiguration
- Windows 10-Registrierungsrichtlinien

Die in den Endpunktsicherheitsrichtlinien enthaltenen Einstellungen sind beispielsweise eine Untermenge der Einstellungen, die in den Profilen *Endpoint Protection* und *Geräteeinschränkungen* in der Gerätekonfigurationsrichtlinie enthalten sind und ebenfalls über verschiedene Sicherheitsbaselines verwaltet werden.

Eine Möglichkeit, um Konflikte zu vermeiden, besteht darin, keine unterschiedlichen Baselines, Instanzen derselben Baseline oder Richtlinienarten und Instanzen für die Verwaltung derselben Einstellungen für ein Gerät zu verwenden. Dazu muss vorab geplant werden, welche Methoden für die Bereitstellung der Konfigurationen auf verschiedenen Geräten verwendet werden sollen. Wenn Sie mehrere Methoden oder Instanzen derselben Methode verwenden, um ein und dieselbe Einstellung zu konfigurieren, müssen Sie entweder sicherstellen, dass sie übereinstimmen, oder dass sie nicht auf denselben Geräten angewendet werden.

Falls doch einmal Konflikte auftreten, können Sie die integrierten Tools in Intune verwenden, um die Ursache dieser Konflikte zu ermitteln und zu beheben. Weitere Informationen finden Sie in folgenden Quellen:

- [Richtlinien und Profile zur Problembehandlung in Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)
- [Überwachen Ihrer Sicherheitsbaselines](../protect/security-baselines-monitor.md#troubleshoot-using-per-setting-status)

## <a name="next-steps"></a>Nächste Schritte

Konfiguration von:

- [Sicherheitsbaselines](../protect/security-baselines.md)
- [Kompatibilitätsrichtlinien](../protect/device-compliance-get-started.md)
- [Richtlinien für bedingten Zugriff](#configure-conditional-access)
- [Integration in Defender ATP](../protect/advanced-threat-protection.md)
