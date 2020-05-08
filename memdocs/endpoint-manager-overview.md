---
title: Übersicht über Microsoft Endpoint Manager – Azure | Microsoft-Dokumentation
description: Endpoint Manager umfasst Intune, Configuration Manager, Co-Verwaltung, Desktop Analytics, Windows Autopilot und das Admin Center für die Verwaltung sämtlicher, also auch lokaler, Geräte.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/04/2020
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: ''
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
ms.custom: get-started
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1dee569d6f2ce4ed1a3bc278c9c9a886f9d23974
ms.sourcegitcommit: 99a6e83219978433ec5a91d09beeaf69acbeb522
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/04/2020
ms.locfileid: "82782257"
---
# <a name="microsoft-endpoint-manager-overview"></a>Übersicht über Microsoft Endpoint Manager

Microsoft Endpoint Manager ermöglicht die Bereitstellung eines modernen Arbeitsplatzes und eine moderne Verwaltung, um Ihre Daten, ob in der Cloud oder lokal, sicher zu speichern. Endpoint Manager bietet Ihnen die Dienste und Tools zur Verwaltung und Überwachung von mobilen Geräten, Desktop- und virtuellen Computern, Embedded-Geräten und Servern.

Endpoint Manager kombiniert Dienste, die Sie möglicherweise kennen und bereits nutzen, darunter Microsoft Intune, Configuration Manager, Desktop Analytics, Co-Verwaltung und Windows Autopilot. Diese Dienste sind Teil des Microsoft 365-Stapels und dienen zum Absichern des Zugriffs, zum Schützen von Daten sowie zum Reagieren auf und Verwalten von Risiken.

Schauen Sie zunächst das zweiminütige Video von Brad Anderson, Microsoft Corporate Vice President für Microsoft 365:

> [!VIDEO https://www.youtube.com/embed/GS7oNPInFuw]

## <a name="what-you-get"></a>Funktionsumfang

Endpoint Manager umfasst die folgenden Dienste:

- **Microsoft Intune**: Intune ist ein vollständig cloudbasierte Lösung zur Verwaltung mobiler Geräte (MDM, Mobile Device Management) und mobiler Anwendungen (MAM, Mobile Application Management) für Apps und Geräte. Mit Intune können Sie Features und Einstellungen auf Geräten mit Android, Android Enterprise, iOS/iPadOS, macOS und Windows 10 steuern. Intune lässt sich in andere Dienste integrieren, darunter Azure Active Directory (AD), Abwehr von Bedrohungen für Mobilgeräte, ADMX-Vorlagen, Win32- und benutzerdefinierte branchenspezifische Apps und vieles mehr.

  Wenn Sie über eine lokale Infrastruktur verfügen, z. B. Exchange oder Active Directory, sind auch die folgenden Intune-Connectors verfügbar:

  - Der **Intune-Connector für Active Directory** fügt Ihrer lokalen Active Directory-Domäne Einträge für Computer hinzu, die sich mit Windows Autopilot registrieren. Weitere Informationen finden Sie unter [Bereitstellen von in Azure AD Hybrid eingebundenen Geräten mit Intune und Windows Autopilot](/mem/intune/enrollment/windows-autopilot-hybrid).
  - Der **Intune Exchange Connector** ermöglicht (oder blockiert) den Gerätezugriff auf Ihre Exchange-Server, wenn die Geräte bei Intune registriert sind und Ihren Richtlinien entsprechen. Weitere Informationen finden Sie unter [Einrichten des lokalen Intune Exchange Connectors](/mem/intune/protect/exchange-connector-install).
  - Der **Intune Certificate Connector** verarbeitet Zertifikatsanforderungen von Geräten, die Zertifikate für die Authentifizierung und Verschlüsselung von E-Mail mit S/MIME verwenden. Weitere Informationen finden Sie unter [Verwenden von Zertifikaten für die Authentifizierung](/mem/intune/protect/certificates-configure).

  Als Teil von Endpoint Manager dient Intune zum Erstellen und Überprüfen von Konformität sowie zum Bereitstellen von Apps, Features und Einstellungen auf Ihren Geräten mithilfe der Cloud.

  Weitere Informationen finden Sie unter [Was ist Microsoft Intune?](https://docs.microsoft.com/intune/fundamentals/what-is-intune).

- **Configuration Manager:** Configuration Manager ist eine lokale Verwaltungslösung zum Verwalten von Servern, Desktop- und Laptopcomputern, die sich in Ihrem Netzwerk oder im Internet befinden. Sie können Configuration Manager cloudfähig machen, um die Integration in Intune, Azure AD, Microsoft Defender ATP und andere Clouddienste zu ermöglichen. Nutzen Sie Configuration Manager zum Bereitstellen von Apps, Softwareupdates und Betriebssystemen. Sie können auch Konformität überwachen, in Echtzeit Clientcomputer abfragen und Aktionen auf diese anwenden und vieles mehr.

  Verwenden Sie Configuration Manager als Teil von Endpoint Manager weiterhin wie gewohnt. Wenn Sie bereit sind, einige Aufgaben in die Cloud zu verlagern, sollten Sie [Co-Verwaltung](https://docs.microsoft.com/configmgr/comanage/) in Betracht ziehen.

  Weitere Informationen finden Sie unter [Was ist Configuration Manager?](https://docs.microsoft.com/configmgr/core/understand/introduction).

- **Co-Verwaltung**: Für Co-Verwaltung werden Ihre bisherigen Investitionen in lokalen Configuration Manager unter Verwendung von Intune und anderen Microsoft 365-Clouddiensten mit der Cloud kombiniert. Sie wählen, ob Configuration Manager oder Intune die Verwaltungsautorität für die sieben Workloadgruppen ist.

  Als Teil von Endpoint Manager werden für Co-Verwaltung Cloudfeatures, wie z. B. bedingter Zugriff, verwendet. Sie belassen einige Aufgaben lokal, während Sie andere Aufgaben mit Intune in der Cloud ausführen.

  Weitere Informationen finden Sie unter [What is co-management? (Was ist die Co-Verwaltung?)](https://docs.microsoft.com/configmgr/comanage/overview).

- **Desktop Analytics**: Desktop Analytics ist ein cloudbasierter Dienst, der in Configuration Manager integriert ist. Der Dienst bietet Einblicke und Informationen, mit denen Sie fundiertere Entscheidungen zur Updatebereitschaft Ihrer Windows-Clients treffen können. Desktop Analytics kombiniert Daten aus Ihrer Organisation mit Daten, die von Millionen von mit der Microsoft-Cloud verbunden Geräten aggregiert wurden. Der Dienst bietet Informationen zu Sicherheitsupdates, Apps und Geräten in Ihrer Organisation und deckt Kompatibilitätsprobleme mit Apps und Treibern auf. Erstellen Sie ein Pilotprojekt für Geräte, die am ehesten die nützlichsten Erkenntnisse zu Ressourcen in Ihrer Organisation bieten.

  Nutzen Sie als Teil von Endpoint Manager die cloudbasierten Erkenntnisse von Desktop Analytics, um Windows 10-Geräte auf dem neuesten Stand zu halten.

  Weitere Informationen finden Sie unter [Was ist Desktop Analytics?](https://docs.microsoft.com/configmgr/desktop-analytics/overview).

- **Windows Autopilot**: Windows Autopilot richtet neue Geräte ein und konfiguriert Sie vorab so, dass sie einsatzbereit sind. Der Dienst wurde entwickelt, um den Lebenszyklus von Windows-Geräten sowohl für die IT-Abteilung als auch für Endbenutzer von der ersten Bereitstellung bis zum Ende der Lebensdauer zu vereinfachen.

  Nutzen Sie Autopilot als Teil von Endpoint Manager zur Vorabkonfiguration von Geräten und zur automatischen Registrierung von Geräten bei Intune. Für komplexere Gerätekonfigurationen können Sie auch Autopilot, Configuration Manager und Co-Verwaltung integrieren (in der Vorschauphase).

  Weitere Informationen finden Sie unter [Übersicht über Windows Autopilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-autopilot) und [Registrieren von Windows-Geräten in Intune mithilfe von Windows Autopilot](/mem/intune/enrollment/enrollment-autopilot).

- **Azure AD Premium**: Azure AD wird von Endpoint Manager für Geräte, Benutzer, Gruppen, dynamische Gruppen, automatische Registrierung, mehrstufige Authentifizierung und bedingten Zugriff verwendet. Diese Features sind für den Schutz von Geräten, Apps und Daten entscheidend.

  Weitere Informationen finden Sie unter [Hinzufügen von Benutzern und Gewähren von Administratorrechten für Intune](/mem/intune/fundamentals/users-add), [Registrierung von Windows-Geräten](/mem/intune/enrollment/windows-enroll)und [Erfahren Sie mehr zum bedingten Zugriff und Intune](/mem/intune/protect/conditional-access).

- **Endpoint Manager Admin Center**: Das [Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) ist eine zentrale Website, auf der Sie Richtlinien erstellen und Ihre Geräte verwalten können. Es ist in andere wichtige Geräteverwaltungsdienste eingebunden, einschließlich Gruppen, Sicherheit, bedingter Zugriff und Berichterstellung. In diesem Admin Center werden auch Geräte angezeigt, die von Configuration Manager und Intune verwaltet werden (in der Vorschau).

## <a name="choose-whats-right-for-you"></a>Wählen der geeignetsten Lösung

Es gibt mehrere Möglichkeiten zu bestimmen, was für Ihre Organisation am geeignetsten ist. Ihre nächsten Schritte hängen davon ab, was Ihre Organisation tut. Berücksichtigen Sie, was Sie zu erreichen versuchen.

Beispiel:

- Wenn Sie ständig neue Geräte bereitstellen, beginnen Sie mit Windows Autopilot.
- Wenn Sie Regeln und Steuerungseinstellungen für Ihre Benutzer, Apps und Geräte hinzufügen, beginnen Sie mit Intune.
- Wenn Sie derzeit Configuration Manager für die Bereitstellung von Apps einsetzen und bedingten Zugriff auf Grundlage von Sicherheitsanforderungen nutzen möchten, beginnen Sie mit der Co-Verwaltung.
- Wenn Sie derzeit Configuration Manager einsetzen und dafür verantwortlich sind, Windows 10-Geräte auf dem neuesten Stand zu halten, beginnen Sie mit Desktop Analytics.
- Wenn Sie die ersten Schritte mit MDM und MAM unternehmen oder ADMX-Vorlagen zur Steuerung von Office-, Microsoft Edge- und Windows-Einstellungen nutzen, beginnen Sie mit Intune.

Sie können sich Endpoint Manager auch in drei Varianten vorstellen: Cloud, lokal und Cloud + lokal:

- **Cloud**: Alle Daten werden in Azure gespeichert. Es gibt keine weiteren Rechenzentren. Dieser Ansatz bietet Ihnen die Mobilitätsvorteile der Cloud und die Sicherheitsvorteile von Azure.

- **Lokal**: Wenn Sie über eine lokale Infrastruktur mit Configuration Manager verfügen oder noch nicht bereit sind, die Cloud zu nutzen, können Sie Ihre vorhandenen Systeme beibehalten.

- **Cloud + lokal**: Viele Umgebungen sind heterogen und befolgen den Ansatz der Cloudanbindung. Dies bedeutet, dass eine Kombination aus Cloud- und lokalen Lösungen verwendet wird. Nutzen Sie bei neuen Geräten die Vorteile von Intune für den Zugriff auf und den Schutz von Daten. Wenn Sie Configuration Manager verwenden, stellen Sie eine Verbindung mit der Cloud her, um zusätzliche Funktionalität und Analysen zu erhalten. Wenn Sie einige Workloads in die Cloud verlagern möchten, ist Co-Verwaltung eine sinnvolle Option.

## <a name="what-you-need-to-get-started"></a>Was Sie für die ersten Schritte benötigen

Der Microsoft Endpoint Manager ist eine Lösungsplattform, die verschiedene Technologien vereint. Es handelt sich nicht um eine neue Lizenz. Die Dienste werden gemäß den jeweiligen Lizenzbedingungen lizenziert. Weitere Informationen finden Sie unter [Ressourcen zur Lizenzierung](https://www.microsoft.com/licensing/product-licensing/products).

Wenn Sie derzeit Configuration Manager nutzen, erhalten Sie auch Microsoft Intune zur Co-Verwaltung Ihrer Windows-Geräte. Für andere Plattformen, wie z. B. iOS/iPadOS und Android, benötigen Sie eine eigene Intune-Lizenz.

In den meisten Szenarien ist Microsoft 365 wohl die beste Option, da Ihnen damit Endpoint Manager und Office 365 zur Verfügung stehen. Weitere Informationen finden Sie unter [Microsoft 365](https://www.microsoft.com/licensing/product-licensing/microsoft-365-enterprise).

## <a name="next-steps"></a>Nächste Schritte

[Nutzen der Leistungsfähigkeit intelligenter Cloudlösungen zur Vereinfachung und Beschleunigung von IT und des Umstiegs auf einen modernen Arbeitsplatz](https://www.microsoft.com/microsoft-365/blog/2019/11/04/use-the-power-of-cloud-intelligence-to-simplify-and-accelerate-it-and-the-move-to-a-modern-workplace/)

[Microsoft Endpoint Manager](https://www.microsoft.com/microsoft-365/microsoft-endpoint-manager)

[Tutorial: Exemplarische Vorgehensweise für Intune in Microsoft Endpoint Manager](/intune/fundamentals/tutorial-walkthrough-endpoint-manager)

[Microsoft Learn-Modul: Was ist Microsoft 365?](https://docs.microsoft.com/learn/modules/what-is-m365/index)
