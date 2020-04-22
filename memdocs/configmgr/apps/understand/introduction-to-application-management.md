---
title: Einführung in die App-Verwaltung
titleSuffix: Configuration Manager
description: Machen Sie sich mit den wichtigsten Informationen zum Verwalten und Bereitstellen von Anwendungen in Configuration Manager vertraut.
ms.date: 04/01/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 08f711ba-83bf-4b5f-9520-a0778c6ae7eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: d3cd21fe4b1d53ecbb0bc60818405cb795a4f289
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690218"
---
# <a name="introduction-to-application-management-in-configuration-manager"></a>Einführung in die Anwendungsverwaltung in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In diesem Artikel werden die Grundlagen für das Arbeiten mit Configuration Manager-Anwendungen beschrieben.  

> [!TIP]  
> Wenn Sie sich bereits mit der Verwaltung von Anwendungen in Configuration Manager auskennen, können Sie diesen Artikel überspringen Fahren Sie in diesem Fall mit dem Erstellen einer Beispielanwendung fort, wie im folgenden Artikel beschrieben: [Erstellen und Bereitstellen einer Anwendung](../get-started/create-and-deploy-an-application.md).  

## <a name="what-is-an-application"></a>Was ist eine Anwendung?

Obwohl der Begriff *Anwendung* oder *App* im Computingbereich weit verbreitet ist, hat er in Configuration Manager eine besondere Bedeutung. Stellen Sie sich eine Anwendung wie eine Schachtel vor. Diese Schachtel enthält mindestens einen Satz von Installationsdateien für ein Softwarepaket (als *Bereitstellungstyp* bezeichnet) und Anweisungen zum Bereitstellen der Software.  

Wenn Sie die Anwendung auf Geräten bereitstellen, wird auf Grundlage der **Anforderungen** entschieden, welcher Bereitstellungstyp von Configuration Manager auf dem Gerät installiert wird.  

Eine Anwendung bietet viele weitere Möglichkeiten. Mehr zu diesen erfahren Sie bei der Lektüre dieses Leitfadens. In den folgenden Abschnitten werden Konzepte vorgestellt, mit denen Sie sich vertraut machen sollten, bevor Sie sich eingehender mit dem Thema beschäftigen:  

### <a name="deployment-type"></a>Bereitstellungstyp

Wenn man eine *Anwendung* mit einer Schachtel vergleichen möchte, so entspricht deren Inhalt dem *Bereitstellungstyp*. Eine Anwendung benötigt mindestens einen Bereitstellungstyp, da mit diesem festgelegt wird, wie die App installiert wird. Sie können mehr als einen Bereitstellungstyp verwenden, um unterschiedliche Inhalte und Installationsprogramme für dieselbe Anwendung zu konfigurieren.

Angenommen, Ihr Unternehmen nutzt eine branchenspezifische Anwendung mit dem Namen Astoria, und die Anwendungsentwickler stellen folgende Möglichkeiten zum Installieren der App bereit:

- das Windows Installer-Paket, damit die App vollständig von Windows 10-Geräten unterstützt wird
- ein App-V-Paket zur Nutzung der App mit einer Terminalserverfarm
- Eine Web-App für Benutzer mobiler Geräte  

Nun erstellen Sie in Configuration Manager eine Anwendung für Astoria. Mithilfe der Anwendung werden die allgemeinen App-Metadaten definiert, die von allen Installationsvorgängen und Plattformen verwendet werden. Anschließend erstellen Sie drei Bereitstellungstypen für die verfügbaren Installationsvorgänge und stellen die Anwendung für die Benutzer bereit. Configuration Manager wählt daraufhin auf Grundlage der Anforderungen und weiterer Konfigurationen für die Bereitstellungstypen für jeden Anwendungsfall den richtigen Vorgang aus.

Weitere Informationen finden Sie unter [Bereitstellungstypen für die Anwendung erstellen](../deploy-use/create-applications.md#bkmk_create-dt) in diesem Thema.

### <a name="requirements"></a>Anforderungen

In früheren Versionen von Configuration Manager wurde üblicherweise eine Gerätesammlung erstellt, für die Anwendung bereitgestellt wurde. Dieser Schritt ist zwar auch weiterhin möglich, jedoch sollten Sie ausführliche Kriterien zur Anwendungsbereitstellung mithilfe von *Anforderungen* definieren.

Angenommen, Sie legen fest, dass eine Anwendung nur auf Geräten unter Windows 10 installiert werden darf. Wenn Sie die Anwendung nun auf allen Geräten bereitstellen, wird sie nur auf denjenigen mit Windows 10 installiert.

Durch das Auswerten von Anforderungen ermittelt Configuration Manager, ob eine Anwendung und deren Bereitstellungstypen installiert werden sollen. Anschließend wird der für die Installation einer Anwendung richtige Bereitstellungstyp ermittelt. Der Konfigurations-Manager-Client wertet standardmäßig alle sieben Tage die Anforderungsregeln neu aus, um zu ermitteln, ob entsprechend der Clienteinstellung **Erneute Auswertung für Bereitstellungen planen** Konformität gewährleistet ist.

Weitere Informationen finden Sie unter [Erstellen und Bereitstellen einer Anwendung](../get-started/create-and-deploy-an-application.md) und [Deployment type Requirements (Anforderungen für den Bereitstellungstyp)](../deploy-use/create-applications.md#bkmk_dt-require).

### <a name="global-conditions"></a>Globale Bedingungen

Sie können Anforderungen mit einem bestimmten Bereitstellungstyp in einer einzelnen Anwendung verwenden. Zusätzlich haben Sie auch die Möglichkeit, *globale Bedingungen* zu erstellen. Bei diesen Bedingungen handelt es sich um eine Bibliothek mit vordefinierten Anforderungen, die Sie mit jeder Anwendung und jedem Bereitstellungstyp verwenden können. Configuration Manager enthält eine Reihe integrierter globaler Bedingungen. Sie können jedoch auch eigene Bedingungen erstellen.

Weitere Informationen finden Sie unter [Erstellen von globalen Bedingungen](../deploy-use/create-global-conditions.md).

### <a name="simulated-deployment"></a>Simulierte Bereitstellung

Eine *simulierte Bereitstellung* wertet die Anforderungen, die Erkennungsmethode und die Abhängigkeiten für eine Anwendung aus. Ein Client gibt die Ergebnisse aus, ohne dass die Anwendung installiert wird.

Weitere Informationen finden Sie unter [Simulate application deployments (Simulieren von Anwendungsbereitstellungen)](../deploy-use/simulate-application-deployments.md).  

### <a name="deployment-action"></a>Bereitstellungsaktion

Durch eine *Bereitstellungsaktion* wird festgelegt, ob Sie die bereitzustellende Anwendung installieren oder deinstallieren möchten. Nicht alle Bereitstellungstypen unterstützen den Deinstallationsvorgang.

Weitere Informationen finden Sie unter [Bereitstellen von Anwendungen](../deploy-use/deploy-applications.md).  

### <a name="deployment-purpose"></a>Bereitstellungszweck

Durch den *Bereitstellungszweck* wird festgelegt, ob die Bereitstellungs-App **Erforderlich** oder **Verfügbar** ist:  

- Eine *erforderliche* Bereitstellung wird vom Client automatisch entsprechend dem festgelegten Zeitplan installiert. Wenn die Anwendung nicht ausgeblendet ist, kann ein Benutzer deren Bereitstellungsstatus nachverfolgen. Der Benutzer kann auch das Softwarecenter verwenden, um die Anwendung vor Ablauf der Frist zu installieren.  

- Wenn Sie für den Benutzer eine *verfügbare* Anwendung bereitstellen, wird diese im Softwarecenter angezeigt und kann bei Bedarf angefordert werden.  

Weitere Informationen finden Sie unter [Bereitstellen von Anwendungen](../deploy-use/deploy-applications.md).  

### <a name="revisions"></a>Revisionen

Wenn Sie an einer Anwendung oder an einem Bereitstellungstyp *Revisionen* vornehmen, wird in Configuration Manager eine neue Version der Anwendung erstellt. In der Configuration Manager-Konsole haben Sie die Möglichkeit, eine der folgenden Aktionen auszuführen:

- Anzeigen des Verlaufs der Anwendungsrevisionen
- Aufrufen der zugehörigen Eigenschaften
- Wiederherstellen einer früheren Anwendungsversion
- Löschen einer früheren Version

Weitere Informationen finden Sie unter [Aktualisieren und Deinstallieren von Anwendungen ](../deploy-use/update-and-retire-applications.md).  

### <a name="detection-method"></a>Erkennungsmethode

Mit *Erkennungsmethoden* ermitteln Sie, ob auf einem Gerät eine Anwendung bereits installiert ist. Wenn die Erkennungsmethode darauf hinweist, dass die Anwendung installiert ist, versucht Configuration Manager nicht, sie erneut zu installieren.

Weitere Informationen finden Sie unter [Erkennungsmethodenoptionen für Bereitstellungstypen](../deploy-use/create-applications.md#bkmk_dt-detect).

### <a name="dependencies"></a>-Abhängigkeiten

Mit *Abhängigkeiten* wird mindestens ein Bereitstellungstyp einer anderen Anwendung definiert, der vom Client installiert werden muss, bevor der eigentliche Bereitstellungstyp installiert wird.

Weitere Informationen finden Sie unter [Abhängigkeiten von Bereitstellungstypen](../deploy-use/create-applications.md#bkmk_dt-depend).  

### <a name="supersedence"></a>Ablösung

Configuration Manager ermöglicht es Ihnen, mithilfe einer *Ablösungsbeziehung* vorhandene Anwendungen zu ersetzen oder ein Upgrade für diese auszuführen. Wenn Sie eine Anwendung ablösen, geben Sie einen neuen Bereitstellungstyp als Ersatz für den Bereitstellungstyp der abgelösten Anwendung an. Sie können außerdem festlegen, ob für die abzulösende Anwendung ein Upgrade durchgeführt oder diese deinstalliert werden soll, bevor der Client die ablösende Anwendung installiert.

Weitere Informationen finden Sie unter [Anwendungsablösung](../deploy-use/revise-and-supersede-applications.md#application-supersedence).  

### <a name="user-centric-management"></a>Benutzerzentrierte Verwaltung

Configuration Manager-Anwendungen unterstützen die *benutzerorientierte Verwaltung*, mit der Sie bestimmten Benutzern bestimmte Geräte zuordnen können. Anstatt sich den Namen des Benutzergeräts merken zu müssen, können Sie Apps für den Benutzer und das Gerät bereitstellen. Mit dieser Funktion stellen Sie sicher, dass die wichtigsten Apps jederzeit auf allen Benutzergeräten verfügbar sind. Wenn Benutzer einen neuen Computer verwenden, installiert Configuration Manager automatisch ihre Apps auf dem Gerät, bevor die Benutzer sich anmelden.

Weitere Informationen finden Sie unter [Verknüpfen von Benutzern und Geräten mit Affinität zwischen Benutzer und Gerät](../deploy-use/link-users-and-devices-with-user-device-affinity.md).  

### <a name="application-group"></a>Anwendungsgruppe

Ab Version 1906 können Sie eine Gruppe von Anwendungen erstellen, die Sie als einzelne Bereitstellung an eine Benutzer- oder Gerätesammlung senden können. Die Metadaten, die Sie für die App-Gruppe angeben, werden im Softwarecenter als Einheit dargestellt. Sie können die Apps in der Gruppe so anordnen, dass der Client sie in einer bestimmten Reihenfolge installiert.

Weitere Informationen finden Sie unter [Create application groups](../deploy-use/create-app-groups.md) (Erstellen von Anwendungsgruppen).

## <a name="what-application-types-can-you-deploy"></a>Welche Anwendungstypen können bereitgestellt werden?

Configuration Manager unterstützt die Bereitstellung folgender App-Typen:  

- Windows Installer (msi)  

- Windows-App-Paket und App Bundle (appx, appxbundle, msix, msixbundle)  

- Windows-App-Paket im Microsoft Store  

- Skriptinstallationsprogramm für Installationsprogramme von Drittanbietern und Skriptwrapper

- Microsoft App-V v4 und v5  

- macOS  

- Eine Tasksequenz für Nicht-Betriebssystembereitstellungen für komplexe Apps

Beim Verwalten von Geräten mit der [lokalen Geräteverwaltung](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) von Configuration Manager können Sie zusätzlich folgende App-Typen verwalten:  

- Windows Phone-App-Paket (xap)  

- Windows Phone-App-Paket im Microsoft Store  

- Windows Installer über MDM (msi)  

- Webanwendung

## <a name="state-based-applications"></a>Zustandsbasierte Anwendungen  

Configuration Manager-Anwendungen nutzen die zustandsbasierte Überwachung. Dadurch können Sie den letzten Anwendungsbereitstellungszustand für Benutzer und Geräte nachverfolgen. In den Zustandsmeldungen werden Informationen zu einzelnen Geräten angezeigt. Wenn Sie beispielsweise eine Anwendung für eine Sammlung von Benutzern bereitstellen, können Sie den Konformitätszustand und den Zweck der Bereitstellung in der Configuration Manager-Konsole anzeigen. Mithilfe des Arbeitsbereichs **Überwachung** überwachen Sie in der Configuration Manager-Konsole die Bereitstellung sämtlicher Software. Weitere Informationen finden Sie unter [Überprüfen von Anwendungen](../deploy-use/monitor-applications-from-the-console.md).  

Der Konfigurations-Manager-Client wertet Anwendungsbereitstellungen regelmäßig neu aus. Beispiel:  

- Ein Benutzer deinstalliert eine bereitgestellte Anwendung. Im nächsten Auswertungsintervall wird von Configuration Manager festgestellt, dass die App nicht vorhanden ist. Der Client installiert daraufhin die App automatisch neu.  

- Configuration Manager hat eine Anwendung auf einem Gerät nicht installiert, da für dieses die Anforderungen nicht erfüllt waren. Später wird eine Änderung an dem Gerät vorgenommen, sodass es die Anforderungen erfüllt. Configuration Manager erkennt diese Änderung, und der Client installiert die Anwendung.  

Sie können das Neuauswertungsintervall für Anwendungsbereitstellungen selbst festlegen. Verwenden Sie dazu die Clienteinstellung **Erneute Auswertung für Bereitstellungen planen** in der Gruppe **Softwarebereitstellung**. Weitere Informationen finden Sie unter [About client settings (Informationen zu Clienteinstellungen)](../../core/clients/deploy/about-client-settings.md#software-deployment).  

## <a name="get-started-creating-an-application"></a>Erste Schritte beim Erstellen einer Anwendung  

Wenn Sie gleich mit dem Erstellen einer Anwendung beginnen möchten, finden Sie im Artikel [Erstellen und Bereitstellen einer Anwendung](../get-started/create-and-deploy-an-application.md) eine ausführliche Anleitung.  

Wenn Sie mit den Grundlagen vertraut sind und ausführlichere Referenzinformationen zu allen verfügbaren Optionen benötigen, finden Sie unter [Erstellen von Anwendungen](../deploy-use/create-applications.md) weitere Informationen.  

## <a name="software-center"></a>Software Center  

Das Softwarecenter ist eine Windows-Anwendung, die zusammen mit dem Konfigurations-Manager-Client installiert wird. Die Anwendung bietet Ihnen die Möglichkeit, folgende Aktionen auszuführen:  

- Suchen und Anfordern von Anwendungen, die für ein Gerät oder einen Benutzer bereitgestellt werden
- Installieren und Planen von Softwareinstallationen
- Anzeigen des Installationsstatus für Anwendungen, Softwareupdates und Betriebssysteme
- Konfigurieren von Einstellungen für die Remotesteuerung
- Einrichten der Energieverwaltung

Weitere Informationen finden Sie in den folgenden Artikeln:  

- [Planen und Konfigurieren der Anwendungsverwaltung](../plan-design/plan-for-and-configure-application-management.md)
- [Planen für Software Center](../plan-design/plan-for-software-center.md)
- [Benutzerleitfaden des Softwarecenters](../../core/understand/software-center.md)

> [!Note]  
> Die Unterstützung für die Anwendungskatalogrollen endet mit Version 1910. Weitere Informationen finden Sie unter [Entfernen des Anwendungskatalogs](../plan-design/plan-for-and-configure-application-management.md#bkmk_remove-appcat).  

## <a name="packages-and-programs"></a>Pakete und Programme  

Configuration Manager unterstützt auch weiterhin Pakete und Programme, die in vorherigen Produktversionen verwendet wurden.

Weitere Informationen finden Sie unter [Pakete und Programme](../deploy-use/packages-and-programs.md).  

## <a name="next-steps"></a>Nächste Schritte

Sie sind nun mit den Grundlagen der Anwendungsverwaltung in Configuration Manager vertraut und können mit den folgenden Artikeln fortfahren:

- [Erstellen und Bereitstellen einer Beispielanwendung](../get-started/create-and-deploy-an-application.md)
- [Planen und Konfigurieren der Anwendungsverwaltung](../plan-design/plan-for-and-configure-application-management.md)
- [Erstellen von Anwendungen](../deploy-use/create-applications.md)
