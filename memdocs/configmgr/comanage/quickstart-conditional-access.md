---
title: Bedingter Zugriff mit Co-Verwaltung
titleSuffix: Configuration Manager
description: Steuern des Benutzerzugriffs auf Unternehmensressourcen auf Grundlage von Intune-Complianceregeln
ms.date: 05/13/2019
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: 4cf640b3-610c-4c3c-b966-c62e9f5654ff
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 94f002ecd12d08ffd5f3d4767e315e0d83714929
ms.sourcegitcommit: 9a700a72735f9a316bdb51c44f86f9cc3bfb7be2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/21/2020
ms.locfileid: "83764049"
---
# <a name="conditional-access-with-co-management"></a>Bedingter Zugriff mit Co-Verwaltung

Durch den bedingten Zugriff wird sichergestellt, dass nur vertrauenswürdige Benutzer über vertrauenswürdige Apps auf vertrauenswürdigen Geräten auf Unternehmensressourcen zugreifen können. Er wird von Grund auf neu in der Cloud erstellt. Unabhängig davon, ob Sie Geräte mit Intune verwalten oder Ihre Configuration Manager-Bereitstellung um Co-Verwaltung erweitern, ist die Funktionsweise identisch.

Im folgenden Video erläutern und demonstrieren Senior Program Manager Joey Glocke und Product Marketing Manager Locky Ainley den bedingten Zugriff mit Co-Verwaltung:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/The-Security-Benefits-of-Conditional-Access/player]

Im Rahmen der Co-Verwaltung wertet Intune jedes Gerät in Ihrem Netzwerk aus, um festzustellen, wie vertrauenswürdig es ist. Diese Auswertung erfolgt auf die folgenden zwei Arten:

1. Intune stellt sicher, dass ein Gerät oder eine App verwaltet und sicher konfiguriert wird. Diese Prüfung hängt davon ab, wie Sie die Compliancerichtlinien Ihres Unternehmens festlegen. Stellen Sie beispielsweise sicher, dass für alle Geräte Verschlüsselung aktiviert ist und keine Jailbreaks vorhanden sind.  

    - Diese Auswertung erfolgt vor einer Sicherheitsverletzung und ist konfigurationsbasiert.  

    - Für gemeinsam verwaltete Geräte führt Configuration Manager auch eine konfigurationsbasierte Auswertung durch. Beispielsweise bezüglich erforderlicher Updates oder der Compliance von Apps. Intune kombiniert diese Auswertung mit einer eigenen Bewertung.  

2. Intune erkennt aktive Sicherheitsincidents auf einem Gerät. Intune nutzt die intelligente Sicherheit von [Microsoft Defender Advanced Threat Protection](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection) (früher Windows Defender ATP) und anderen [Anbietern von Mobile Threat Defense](https://www.lookout.com/about/partners/microsoft). Diese Partner führen laufend Verhaltensanalysen auf Geräten aus. Diese Analyse erkennt aktive Incidents und leitet diese Informationen dann an Intune zur Complianceauswertung in Echtzeit weiter.  

    - Diese Auswertung erfolgt nach der Sicherheitsverletzung und basiert auf Incidents.  

Microsoft Corporate Vice President Brad Anderson hat den bedingten Zugriff in der Keynote zur Ignite 2018 ausführlich mit Livedemos erläutert. 

> [!VIDEO https://www.youtube.com/embed/7tDbUhVCX_I?start=1071]

Mit dem bedingten Zugriff erhalten Sie auch einen zentralen Ort, an dem Sie die Integrität aller mit dem Netzwerk verbundenen Geräte einsehen können. Sie profitieren von den Vorteilen der Cloudskalierung, die sich insbesondere beim Testen von Configuration Manager-Produktionsinstanzen bewährt.


## <a name="benefits"></a>Vorteile

Jedes IT-Team ist von Netzwerksicherheit besessen. Es ist zwingend erforderlich, dass jedes Gerät Ihren Sicherheits- und Geschäftsanforderungen entspricht, bevor es auf Ihr Netzwerk zugreift. Mit dem bedingten Zugriff können Sie die Folgendes ermitteln: 
- Ob jedes Gerät verschlüsselt ist  
- Ob Malware installiert ist  
- Ob seine Einstellungen aktualisiert werden  
- Ob Nutzungsbeschränkungen entfernt wurden  

Der bedingte Zugriff kombiniert präzise Kontrolle über Unternehmensdaten mit einer Benutzeroberfläche, die die Produktivität der Mitarbeiter auf jedem Gerät maximiert, egal wo sie sich befinden.

Das folgende Video zeigt, wie [Advanced Thread Protection](https://www.microsoft.com/windowsforbusiness/windows-atp) (ATP) in gängige Szenarien integriert wird, die Sie regelmäßig erleben:

> [!VIDEO https://www.youtube.com/embed/A7IrxAH87wc?start=178]

Durch Co-Verwaltung kann Intune die Verantwortlichkeiten von Configuration Manager für die Bewertung der Einhaltung Ihrer Sicherheitsstandards bei erforderlichen Updates oder Apps übernehmen. Dieses Verhalten ist wichtig für jedes IT-Unternehmen, das Configuration Manager weiterhin für komplexe App- und Patchverwaltung einsetzen möchte.

Der bedingte Zugriff ist auch ein wichtiger Teil der Entwicklung Ihrer [Zero Trust-Netzwerkarchitektur](https://cloudblogs.microsoft.com/microsoftsecure/2018/06/14/building-zero-trust-networks-with-microsoft-365/). Dank des bedingten Zugriffs wird die Grundfunktionalität des Zero Trust-Netzwerks von den Zugriffsteuerungsfunktionen der konformen Geräte abgedeckt. Diese Funktionalität ist ein wesentlicher Aspekt für die zukünftige Sicherung Ihres Unternehmens.

Weitere Informationen finden Sie im Blogbeitrag zu [Optimieren des bedingten Zugriffs mit Computerrisikodaten aus Microsoft Defender Advanced Threat Protection](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Enhancing-conditional-access-with-machine-risk-data-from-Windows/ba-p/250559).



## <a name="case-studies"></a>Fallstudien

Das IT-Beratungsunternehmen Wipro schützt und verwaltet die Geräte, die von den 91.000 Mitarbeitern genutzt werden, mithilfe des bedingten Zugriffs. In einer aktuellen Fallstudie hat der Vice President der IT bei Wipro Folgendes angemerkt:

> *Der bedingte Zugriff ist ein großer Gewinn für Wipro. Jetzt verfügen alle unsere Mitarbeiter bei Bedarf über mobilen Zugriff auf Informationen.* 
> *Wir haben unseren Sicherheitsstatus und unsere Mitarbeiterproduktivität verbessert. Jetzt profitieren 91.000 Mitarbeiter überall von einem hochsicheren Zugriff auf mehr als 100 Apps und von jedem Gerät aus.*

<!-- waiting for the case study to be public
For more information, see [Wipro drives mobile productivity with Microsoft cloud security tools to improve customer engagements](https://customers.microsoft.com/story/446f72f9-2f50-4697-b688-6d279786e010)
-->

Weitere Beispiele: 

- Nestlé nutzt den app-basierten bedingten Zugriff für über 150.000 Mitarbeiter.  

- Das Automatisierungssoftwareunternehmen Cadence, das nun sicherstellen kann, dass „nur noch verwaltete Geräte Zugriff auf Office 365-Apps wie Teams und das Intranet des Unternehmens haben“. Es kann seinen Mitarbeitern auch „einen sichereren Zugriff auf andere cloudbasierte Apps wie Workday und Salesforce“ bieten. Weitere Informationen zu den Erfahrungen, die Cadence mit Intune gemacht hat, finden Sie unter [Cadence increases the pace of business with mobile collaboration tools in Microsoft 365](https://customers.microsoft.com/story/cadence-partner-professional-services-microsoft-365) (Cadence erhöht das Geschäftstempo mit Tools für die mobile Zusammenarbeit in Microsoft 365).

Intune ist auch vollständig in Partner wie Cisco ISE, Aruba Clear Pass und Citrix NetScaler integriert. Mit diesen Partnern können Sie Zugriffssteuerungen auf der Grundlage der Intune-Anmeldung und des Compliancestatus der Geräte auf diesen anderen Plattformen verwalten.

Weitere Informationen finden Sie in den folgenden Videos:
- [Brad Anderson zeigt den bedingten Zugriff im Detail](https://youtu.be/8321obNofgM?t=547)  
- [Weitere Details von Endpoint Zone 1805](https://youtu.be/f-ILlEuBFZg?t=196)  


## <a name="value-proposition"></a>Leistungsversprechen

Mit dem bedingtem Zugriff und einer ATP-Integration stärken Sie eine grundlegende Komponente einer jeden IT-Organisation: den sicheren Cloudzugriff.

Bei mehr als 63 % aller Datenschutzverletzungen erhalten die Angreifer durch schwache, unterlassene oder gestohlene Benutzeranmeldeinformationen Zugriff auf das Netzwerk des Unternehmens. Da der bedingte Zugriff die Benutzeridentität sichert, schränkt er den Diebstahl von Anmeldeinformationen ein. Der bedingter Zugriff verwaltet und schützt Ihre Identitäten, unabhängig davon, ob sie privilegiert oder nicht privilegiert sind. Es gibt keine bessere Möglichkeit, die Geräte und die darauf gespeicherten Daten zu schützen.

Da der bedingte Zugriff eine Kernkomponente von Enterprise Mobility + Security (EMS) ist, ist weder eine lokale Einrichtung noch eine lokale Architektur erforderlich. Mit Intune und Azure Active Directory (Azure AD) können Sie den bedingten Zugriff in der Cloud schnell konfigurieren. Wenn Sie derzeit Configuration Manager verwenden, können Sie Ihre Umgebung mit Co-Verwaltung problemlos auf die Cloud ausweiten und sofort mit der Nutzung beginnen.

Weitere Informationen zur ATP-Integration finden Sie im Blogbeitrag [Microsoft Defender ATP-Risikobewertung für Geräte deckt neue Cyberangriffe auf und treibt den Netzwerkschutz mithilfe des bedingten Zugriffs an](https://cloudblogs.microsoft.com/microsoftsecure/2018/11/28/windows-defender-atp-device-risk-score-exposes-new-cyberattack-drives-conditional-access-to-protect-networks/). Darin wird beschrieben, wie eine erfahrene Hackergruppe noch nie zuvor gesehene Tools eingesetzt hat. Die Hacker wurden jedoch von der Microsoft-Cloud erkannt und aufgehalten, weil die betroffenen Benutzer über bedingten Zugriff verfügten. Der Angriff hat die risikobasierte Geräterichtlinie für den bedingten Zugriff aktiviert. Obwohl der Angreifer bereits im Netzwerk Fuß gefasst hatte, wurden die angegriffenen Computer automatisch vom Zugriff auf Dienste und Daten der Organisation, die von Azure AD verwaltet werden, ausgeschlossen.



## <a name="configure"></a>Konfigurieren

Der bedingte Zugriff ist einfach zu verwenden, wenn Sie die [Co-Verwaltung](how-to-enable.md) aktivieren. Dazu muss die Workload der **Compliancerichtlinien** in Intune verschoben werden. Weitere Informationen finden Sie unter [Verschieben von Configuration Manager-Workloads zu Intune](how-to-switch-workloads.md). 

Weitere Informationen zum bedingten Zugriff finden in den folgenden Artikeln: 

- [Bedingter Zugriff in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)  

- [Intune-Gerätekonformitätsrichtlinien](https://docs.microsoft.com/intune/device-compliance)  

- [App-basierter bedingter Zugriff mit Intune](https://docs.microsoft.com/intune/app-based-conditional-access-intune)  

> [!Note]  
> Die Features für den bedingten Zugriff sind sofort für Geräte mit Azure AD-Hybrideinbindung verfügbar. Zu diesen Funktionen gehören mehrstufige Authentifizierung und Azure AD Hybrid Join-Zugriffssteuerung. Dieses Verhalten ist darauf zurückzuführen, dass sie auf Azure AD-Eigenschaften basieren. Um die konfigurationsbasierte Auswertung von Intune und Configuration Manager zu nutzen, aktivieren Sie die Co-Verwaltung. Diese Konfiguration ermöglicht Ihnen die Zugriffssteuerung für konforme Geräte direkt aus Intune heraus. Außerdem steht Ihnen die Funktion zur Auswertung der Compliancerichtlinien von Intune zur Verfügung.  

