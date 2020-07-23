---
title: Desktop Analytics
titleSuffix: Configuration Manager
description: Dieser Artikel bietet eine Übersicht über den mit Configuration Manager integrierten Desktop Analytics-Dienst.
ms.date: 06/29/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: overview
ms.assetid: 38b2bed2-20dd-4ce1-abc0-219343d2c4b8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: 09f829bd1695426211ff94381a63b8f23d1b4fe8
ms.sourcegitcommit: 86c2c438fd2d87f775f23a7302794565f6800cdb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/16/2020
ms.locfileid: "86411013"
---
# <a name="what-is-desktop-analytics"></a>Was ist Desktop Analytics?

Desktop Analytics ist ein cloudbasierter Dienst, der in Configuration Manager integriert ist. Der Dienst bietet Einblicke und Informationen, mit denen Sie fundiertere Entscheidungen zur Updatebereitschaft Ihrer Windows-Clients treffen können. Er kombiniert Daten aus Ihrer Organisation mit Daten, die von Millionen von mit Microsoft-Clouddiensten verbunden Geräten aggregiert wurden.

Verwenden Sie Windows Analytics mit Configuration Manager für folgende Zwecke:  

- Erstellen eines Inventars der Apps, die in Ihrer Organisation ausgeführt werden  

- Bewerten der App-Kompatibilität mit den neuesten Windows 10-Featureupdates  

- Identifizieren von Kompatibilitätsproblemen und Empfangen von Vorschlägen zur Risikominderung gemäß Erkenntnissen aus Clouddaten  

- Erstellen von Pilotgruppen, die das gesamte Anwendungs- und Treiberumfeld für eine minimale Anzahl von Geräten darstellen  

- Bereitstellen von Windows 10 für in Pilotprojekten und in der Produktion verwaltete Geräte  

![Screenshot der Startseite von Desktop Analytics im Azure-Portal](media/portal-home.png)

Das folgende Video wurde auf der Ignite 2019 aufgenommen und umfasst weitere Informationen zu Desktop Analytics:

> [!VIDEO https://medius.studios.ms/Embed/Video-nc/IG19-BRK3085]

[Verwenden von Desktopanalysen und Configuration Manager, um Windows-Gesamtkosten durch datengesteuerte Analysen für Verwaltung, Wartung und Support zu verringern](https://myignite.techcommunity.microsoft.com/sessions/81689?source=sessions)

Springen Sie zu 10:00, um sich eine detaillierte Demo anzusehen.

> [!Note]  
> Desktop Analytics ist ein Nachfolger des Windows Analytics-Diensts, der am 31. Januar 2020 eingestellt wurde.
>
> Die Funktionen von Windows Analytics wurden im Desktop Analytics-Dienst kombiniert. Desktop Analytics ist zudem enger in Configuration Manager integriert. Weitere Informationen erhalten Sie in den [häufig gestellten Fragen für vorhandene Windows Analytics-Kunden](faq.md#existing-windows-analytics-customers).

## <a name="benefits"></a>Vorteile

Viele Kunden sind mit der Herausforderung konfrontiert, Windows 10 laufend auf dem aktuellen Stand zu halten. Die größte Aufgabe dabei besteht darin, Anwendungen zu testen. Dieser Prozess erfolgt in der Regel manuell. IT-Administratoren und Anwendungsbesitzer verbringen viel Zeit damit, vorhandene Anwendungen ständig analysieren. Außerdem müssen sie alle auftretenden Probleme beheben.

Desktop Analytics bietet die folgenden Vorteile:

- **Geräte- und Softwareinventar**: Inventuraufnahme von Schlüsselfaktoren wie Apps und Windows-Versionen.  

- **Identifizieren für die Pilotphase**: Identifizieren der kleinsten Gruppe von Geräten, mit der die größte Abdeckung von Faktoren gegeben ist. Der Schwerpunkt liegt dabei auf den Faktoren, die für einen Pilotversuch von Windows-Upgrades und -Updates am wichtigsten sind. Indem Sie eine erfolgreichere Durchführung des Pilotversuchs sicherstellen, können Sie schneller und zuverlässiger zu umfassenden Bereitstellungen in der Produktion wechseln.  

- **Identifizieren von Problemen**: Anhand von aggregierten Marktdaten und Daten aus Ihrer Umgebung prognostiziert der Dienst potenzielle Probleme bei der laufenden Aktualisierung von Windows. Anschließend werden potenzielle Maßnahmen zur Risikominderung vorgeschlagen.  

- **Configuration Manager-Integration**: Ihre lokale Infrastruktur baut auf der Cloud von Diensten auf. Verwenden Sie diese Daten und Analysen, um Windows auf Ihren Geräten bereitzustellen und zu verwalten.  

## <a name="prerequisites"></a>Voraussetzungen

Zum Verwenden von Desktop Analytics müssen Sie sicherstellen, dass Ihre Umgebung die folgenden Voraussetzungen erfüllt.

### <a name="technical"></a>Technisch

- Sie benötigen ein aktives Azure-Abonnement mit den Berechtigungen eines [globalen Administrators](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#company-administrator-permissions). [Microsoft-Konten](https://docs.microsoft.com/windows/security/identity-protection/access-control/microsoft-accounts) werden nicht unterstützt.  

    > [!IMPORTANT]
    > Desktop Analytics ist ein Windows-Dienst, der global in Azure gehostet wird und Windows-Diagnosedaten nutzt. Desktop Analytics ist ein globaler Azure-Dienst, der zwar für US Government-Kunden verfügbar ist, jedoch nicht die Anforderungen der [US Government Community Compliance (GCC)](https://docs.microsoft.com/office365/servicedescriptions/office-365-platform-service-description/office-365-us-government/gcc#us-government-community-compliance) erfüllt. Eine Liste der Complianceangebote für Microsoft-Produkte und -Dienste finden Sie im [Microsoft Trust Center](https://docs.microsoft.com/microsoft-365/compliance/offering-home?view=o365-worldwide). Desktop Analytics ist nicht für GCC High-Kunden oder US Department of Defense-Kunden verfügbar. Die Nutzung von Azure Government-Abonnements zum Hosten von Desktop Analytics-Arbeitsbereichen wird nicht unterstützt.

    - Berechtigungen als **Arbeitsbereichsbesitzer** zum **Einrichten Ihres Arbeitsbereichs** sowie die folgenden Rollen:  

      - Rolle [**Desktop Analytics-Administrator**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#desktop-analytics-administrator-permissions).

      - [**Log Analytics-Mitwirkender**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#log-analytics-contributor) und [**Benutzerzugriffsadministrator**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) für die Ressourcengruppe, um einen vorhandenen Arbeitsbereich zu verwenden oder einen neuen Arbeitsbereich in einer vorhandenen Ressourcengruppe zu erstellen.

      - Berechtigungen [**Besitzer**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) oder [**Mitwirkender**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) und [**Benutzerzugriffsadministrator**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#user-access-administrator) für das Abonnement, um einen Arbeitsbereich in einer neuen Ressourcengruppe zu erstellen.  

    - Um nach dem Onboarding auf das Portal zuzugreifen, benötigen Sie Folgendes:

      - Die Rolle [**Desktop Analytics-Administrator**](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles#desktop-analytics-administrator-permissions) sowie die Berechtigung [**Besitzer**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#owner) oder [**Mitwirkender**](https://docs.microsoft.com/azure/role-based-access-control/built-in-roles#contributor) im erstellten Log Analytics-Arbeitsbereich.

- Configuration Manager, Version 1902 mit Updaterollup (4500571) oder höher. Weitere Informationen finden Sie unter [Aktualisieren von Configuration Manager](connect-configmgr.md#bkmk_hotfix).  

    - Rolle [**Hauptadministrator**](../core/understand/fundamentals-of-role-based-administration.md#bkmk_Planroles) in Configuration Manager  

    > [!NOTE]
    > Desktop Analytics unterstützt mehrere Configuration Manager-Hierarchien, deren Berichte und Meldungen an einen einzigen Azure AD-Mandanten gesendet werden.<!-- 4814075 --> Wenn Sie in Ihrer Umgebung über mehrere Hierarchien verfügen, haben Sie folgende Möglichkeiten:
    >
    > - Einsatz unterschiedlicher kommerzieller IDs und Azure AD-Mandanten.
    > - Konfigurieren einer einzigen kommerziellen ID für beide Hierarchien, um denselben Azure AD-Mandanten und dieselbe Desktop Analytics-Instanz zu nutzen. Verwenden Sie [verschiedenen Apps](connect-configmgr.md#bkmk_connect), um die einzelnen Hierarchien zu verbinden. Nachdem Sie eine Hierarchie vom Portal entkoppelt haben, kann es bis zu 30 Tage dauern, bis Änderungen angezeigt werden. 

- Geräte unter Windows 7, Windows 8.1 oder Windows 10  

    - Installieren Sie die neuesten Updates. Weitere Informationen finden Sie unter [Aktualisieren von Geräten](enroll-devices.md#update-devices).  

    - Auf den Geräten muss außerdem der Konfigurations-Manager-Client, Version 1902 mit Updaterollup (4500571) oder höher installiert sein. Weitere Informationen finden Sie unter [Aktualisieren von Configuration Manager](connect-configmgr.md#bkmk_hotfix).  

    > [!Note]  
    > Desktop Analytics unterstützt keine Upgrades für oder von Windows 10 Long-Term Servicing Channel (LTSC). Weitere Informationen finden Sie unter [Übersicht über Windows-as-a-Service](https://docs.microsoft.com/windows/deployment/update/waas-overview#long-term-servicing-channel).
    >
    > Desktop Analytics ist auf die optimale Unterstützung von Szenarios mit direkten Upgrades ausgelegt. Wenn Sie umfassende Umstellungen vornehmen müssen, z. B. von einer 32-Bit-Architektur zu einer 64-Bit-Architektur, verwenden Sie ein Imagingszenario. Erkenntnisse von Desktop Analytics sind auch in diesen klassischen Szenarien der Betriebssystembereitstellungen hilfreich, Sie können jedoch die spezifischen Anleitungen zu direkten Upgrades ignorieren. Weitere Informationen hierzu finden Sie unter [Szenarios zur Bereitstellung von Unternehmensbetriebssystemen mit Configuration Manager](../osd/deploy-use/scenarios-to-deploy-enterprise-operating-systems.md).

- Windows-Diagnosedaten. Weitere Informationen finden Sie in den folgenden Artikeln:  

    - [Diagnosedatenebenen](enable-data-sharing.md#diagnostic-data-levels)  

    - [Desktop Analytics – Datenschutz](privacy.md)  

- Netzwerkkonnektivität von Geräten zur öffentlichen Microsoft-Cloud. Weitere Informationen finden Sie unter [Aktivieren der Datenfreigabe](enable-data-sharing.md).  

> [!Important]
> Microsoft ist bestrebt, Ihnen Tools und Ressourcen zur Verfügung zu stellen, mit denen Sie die Kontrolle über Ihre Privatsphäre erlangen. Daher erfasst Microsoft keine der folgenden Daten von Geräten, die sich in europäischen Ländern (EWR und Schweiz) befinden:
>
> - Windows-Diagnosedaten von Windows 8.1-Geräten
> - App-Nutzungsdaten für Windows 7

### <a name="licensing-and-costs"></a>Lizenzierung und Kosten

- Ein aktives globales Azure-Abonnement.

    > [!NOTE]
    > Die meisten gleichwertigen Abonnements für Configuration Manager enthalten auch Azure AD. Informationen hierzu finden Sie z. B. auf den Seiten zu den [Microsoft 365-Plänen](https://www.microsoft.com/microsoft-365/compare-all-microsoft-365-plans) und [Enterprise Mobility + Security-Lizenzen](https://www.microsoft.com/licensing/product-licensing/enterprise-mobility-security).

- Für Geräte, die bei Desktop Analytics registriert sind, ist eine gültige Configuration Manager-Lizenz erforderlich. Weitere Informationen hierzu finden Sie unter [Häufig gestellte Fragen für die Configuration Manager-Verzweigungen und -Lizenzierungen](../core/understand/product-and-licensing-faq.md).

- Benutzer des betreffenden Geräts benötigen eine der folgenden Lizenzen:

  - Windows 10 Enterprise E3 oder E5 (enthalten in Microsoft 365 F3, E3 oder E5)

  - Windows 10 Education A3 oder A5 (enthalten in Microsoft 365 A3 oder A5)

  - Windows Virtual Desktop Access E3 oder E5  

> [!NOTE]
> Über die Kosten dieser Lizenzabonnements hinaus fallen keine zusätzlichen Kosten für die Verwendung von Desktop Analytics in Azure Log Analytics an. Für die Datentypen, die von Desktop Analytics erfasst werden, fallen keine Gebühren für die Log Analytics-Datenerfassung und -aufbewahrung an. Aus diesem Grund gibt es für diese Daten auch keine Tageslimits für die Datenerfassung mit Log Analytics. Weitere Informationen finden Sie unter [Verwalten von Nutzung und Kosten mit Azure Monitor-Protokollen](https://docs.microsoft.com/azure/azure-monitor/platform/manage-cost-storage).

## <a name="next-steps"></a>Nächste Schritte

Das folgende Tutorial bietet eine schrittweise Anleitung für den Einstieg in die Arbeit mit Desktop Analytics und Configuration Manager:
  
> [!div class="nextstepaction"]
> [Bereitstellen von Windows 10 für den Pilotversuch](tutorial-windows10.md)
