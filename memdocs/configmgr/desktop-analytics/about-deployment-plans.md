---
title: Bereitstellungspläne in Desktop Analytics
titleSuffix: Configuration Manager
description: In diesem Artikel werden Bereitstellungspläne in Desktop Analytics erläutert.
ms.date: 07/28/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 0f369f3a-f251-4f34-9302-1bdc6ea5d139
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.reviewer: acabello
ms.openlocfilehash: acaa7c8a906edd78f0c54c5735c97c55434d848b
ms.sourcegitcommit: 7ee69b207261ffc282e535f793a536540d160557
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/29/2020
ms.locfileid: "87400714"
---
# <a name="about-deployment-plans-in-desktop-analytics"></a>Bereitstellungspläne in Desktop Analytics

Desktop Analytics sammelt und analysiert Geräte-, Anwendungs- und Treiberdaten in Ihrer Organisation. Auf der Grundlage dieser Analyse und Ihrer Eingabe können Sie mit dem Dienst Bereitstellungspläne für Windows 10 erstellen. Bereitstellungspläne bieten die folgenden Features:  

- Automatische Empfehlungen, welche Geräte in Pilotversuche eingeschlossen werden sollten  

- Identifizieren von Kompatibilitätsproblemen und Empfehlen von Risikominderungen  

- Bewertungen der Integrität der Bereitstellung vor, während und nach Updates  

- Verfolgen des Fortschritts der Bereitstellung  

Im Rahmen des Bereitstellungsplans führen Sie die folgenden Aktionen aus:  

- Sie legen fest, welche Versionen von Windows 10 bereitgestellt werden sollen.  

- Sie wählen aus, welche Gruppen von Geräten bereitgestellt werden sollen.  

- Sie erstellen Bereitschaftsregeln für die Bereitstellung.  

- Sie definieren die Wichtigkeit Ihrer Apps.  

- Sie wählen Pilotgeräten auf der Grundlage automatischer Empfehlungen aus.  

- Sie entscheiden auf der Grundlage von Empfehlungen von Desktop Analytics, wie Probleme mit Apps behoben werden.  

Standardmäßig aktualisiert Desktop Analytics die Daten des Bereitstellungsplans täglich. Das Verarbeiten von Änderungen, die Sie in einem Bereitstellungsplan vornehmen (z. B. das Zuweisen der Wichtigkeit zu einer App oder das Auswählen eines in den Pilotversuch einzuschließenden Geräts) dauert bis zu 24 Stunden. Fordern Sie die bedarfsgesteuerte Datenaktualisierung an, um die Verarbeitung zu beschleunigen. Weitere Informationen finden Sie unter [Desktop Analytics – Häufig gestellte Fragen](faq.md#can-i-reduce-the-amount-of-time-it-takes-for-data-to-refresh-in-my-desktop-analytics-portal).  

Wählen Sie nach dem Herstellen der Verbinden von Desktop Analytics mit Configuration Manager ihre Sammlungen in den Bereitstellungsplänen aus. Mit dieser Integration können Sie Windows in einer Sammlung bereitstellen, die auf den Desktop Analytics-Daten basiert.

Bereitstellungspläne unterstützen die drei neuesten Windows 10-Versionen. Desktop Analytics fügt Unterstützung für eine neue Windows 10-Version innerhalb von 45 Tagen nach der Verfügbarkeit hinzu. Zu diesem Zeitpunkt löscht der Dienst auch die älteste Version. Sie können keine Bereitstellungspläne verwenden, die auf älteste Versionen abzielen. Wenn Sie keine fortlaufende Bereitstellungspläne besitzen, die die älteste unterstützte Version in Desktop Analytics anzielen, vervollständigen Sie die Bereitstellung innerhalb von 45 Tagen, nachdem eine neue Windows 10-Version verfügbar ist.

## <a name="readiness-rules"></a>Bereitschaftsregeln

Die folgenden Bereitschaftsregeln sind in Bereitstellungsplänen verfügbar:

- Ob Ihre Geräte automatisch Treiber aus Windows-Update beziehen. Wenn Geräte Treiber-Updates von Windows-Update erhalten, werden alle etwaigen im Rahmen der Bereitschaftsbewertung festgestellten Treiberprobleme automatisch als **Bereit** markiert.  

- Schwellenwert für niedrige Anzahl von Installationen für Ihre Windows-Apps. Wenn eine App auf einem Prozentsatz der Computer installiert ist, der diesen Schwellenwert überschreitet, wird diese App vom Bereitstellungsplan als **Beachtenswert** markiert. Dieses Tag bedeutet, dass Sie entscheiden können, wie wichtig ein Test der App während der Pilotphase ist.  

## <a name="plan-assets"></a>Planobjekte

<!-- 4670224 -->

Während im Bereich [Objekte](about-assets.md) auch Geräte und Apps angezeigt werden, enthält der Bereich **Planobjekte** unter einem bestimmten Bereitstellungsplan zusätzliche Informationen.

### <a name="devices"></a>Geräte

Überprüfen Sie die **Windows-Upgradeentscheidung** für jedes Gerät im Bereitstellungsplan.

Die Windows-Upgradeentscheidung **Gerät ersetzen** kann einen der folgenden Gründe haben:

- Eine erforderliche Windows 10-Prozessorprüfung wurde nicht bestanden. Weitere Informationen finden Sie unter [Mindesthardwareanforderungen](https://docs.microsoft.com/windows-hardware/design/minimum/minimum-hardware-requirements-overview#31-processor).
- Ein BIOS-Block ist vorhanden.
- Der Arbeitsspeicher ist unzureichend.
- Der Treiber einer für den Start erforderlichen Komponente im System wurde blockiert.
- Ein Upgrade des spezifischen Typs und Modells ist nicht möglich.
- Es gibt eine Anzeigeklassenkomponente mit einem Treiberblock, die folgende Merkmale aufweist:
  - Es erfolgt keine Außerkraftsetzung,
  - Es ist kein Treiber in der neuen Betriebssystemversion vorhanden.
  - Sie ist noch nicht in Windows-Update enthalten.
- Es gibt eine weitere Plug-and-Play-Komponente im System, die das Upgrade blockiert.
- Es gibt eine drahtlose Komponente, die einen XP-emulierten Treiber verwendet.
- Eine Netzwerkkomponente mit einer aktiven Verbindung verliert ihren Treiber. Mit anderen Worten: Nach dem Upgrade kann ihre Netzwerkkonnektivität verloren gehen.

Die Windows-Upgradeentscheidung zur **Neuinstallation** gibt an, dass für das Upgrade im Gegensatz zu einem direkten Upgrade eine Neuinstallation erforderlich ist.

Eine Windows-Upgrade-Entscheidung kann aus den folgenden Gründen **blockiert** werden:

- Sie haben die Upgrade-Entscheidung für mindestens ein Objekt auf **Unable** (Nicht möglich) festgelegt.

- Die Inventurdaten für dieses Gerät sind unvollständig, und Desktop Analytics kann keine vollständige Kompatibilitätsbewertung durchführen.

### <a name="apps"></a>Apps

Legen Sie die **Upgradeentscheidung** und die **Wichtigkeit** für diese App in diesem Bereitstellungsplan fest. Weitere Informationen finden Sie unter [Erstellen von Bereitstellungsplänen](create-deployment-plans.md).

In den Details der App werden auch die folgenden Informationen angezeigt: Empfehlungen, Faktoren für Kompatibilitätsrisiken sowie MS bekannte Probleme. Legen Sie anhand dieser Informationen die **Upgradeentscheidung** fest. Weitere Informationen finden Sie unter [Bewertung der Kompatibilität](compat-assessment.md).

Die Apps, die von Desktop Analytics als *Beachtenswert* ausgewiesen werden, basieren auf dem Schwellenwert für eine niedrige Anzahl von Installationen für die Bereitschaftsregeln des Bereitstellungsplans. Weitere Informationen finden Sie unter [Bereitschaftsregeln](create-deployment-plans.md#readiness-rules).

   > [!Tip]
   > Weitere Informationen zur App-Kategorie „Nicht wichtig“ erhalten Sie unter [Entscheidungen zum automatischen Upgrade von System-und Store-Apps](about-assets.md#bkmk_plan-autoapp). <!-- 3587232 -->

Die Einstellung **Details zu App-Versionen** ist standardmäßig deaktiviert, sodass alle Versionen von Apps mit dem gleichen Namen und Herausgeber zusammengefasst werden.<!-- 5542186 --> Das Standardverhalten trägt dazu bei, die Gesamtzahl der angezeigten Apps zu reduzieren. Dadurch lasst sich der Aufwand beim Kommentieren der Apps verringern. Die App-Anzahl auf der Kachel **Beachtenswerte Apps** spiegelt ebenfalls diese Einstellung wider. Anstatt Hunderte von Instanzen von Microsoft Edge aufzulisten, wird jetzt eine Instanz für alle Versionen angezeigt. Sie können Entscheidungen einmal für alle Versionen treffen. Wenn Sie Entscheidungen für bestimmte Versionen einer App treffen müssen, aktivieren Sie diese Einstellung. Sie können diese Einstellung auch auf der Ebene der globalen Objekte konfigurieren. Weitere Informationen finden Sie unter [Informationen zu Objekten: Apps](about-assets.md#apps).

Wenn die Einstellung **Details zu App-Versionen** deaktiviert ist, wird im Bereich „App-Details“ die Anzahl der App-Versionen und Sprachen angezeigt, die zusammengefasst wurden. Wenn Sie Änderungen an den App-Details speichern, gilt dies für alle Versionen. Legen Sie beispielsweise die **Upgradeentscheidung** oder **Wichtigkeit** fest. In einigen Werten wird „Mehrere“ angezeigt. Das bedeutet, dass kein konsistenter Wert für alle Versionen vorliegt. Der Dienst führt weiterhin Kompatibilitätsrisikobewertungen für jede Version durch. Aktivieren Sie **Details zu App-Versionen**, um die Kompatibilitätsrisikobewertung für eine bestimmte App-Version anzuzeigen.

### <a name="drivers"></a>Treiber

Überprüfen Sie die Liste der in diesem Bereitstellungsplan enthaltenen Treiber. Legen Sie die **Upgradeentscheidung** fest, prüfen Sie die Empfehlung von Microsoft, und untersuchen Sie die Kompatibilitätsrisikofaktoren.

## <a name="importance"></a>Wichtigkeit

Legen Sie im Rahmen des Bereitstellungsplans die *Wichtigkeit* der Apps fest. Diese Apps werden von Desktop Analytics als auf den Zielgeräten als installiert erkannt. Mit dieser Einstellung kann Desktop Analytics ermitteln, welche Geräte in die Pilotphase der Bereitstellung aufgenommen werden.

Wenn eine App auf weniger als 2 % der Zielgeräte installiert ist, wird sie mit **Niedrige Anzahl von Installationen** markiert. Der Standardwert ist 2 Prozent. Sie können den Schwellenwert in den Bereitschaftseinstellungen von 0 % bis 10 % anpassen. Diese Apps werden von Desktop Analytics automatisch als **Bereit für Upgrade** markiert.  

Wählen Sie für Apps die Wichtigkeit **Kritisch**, **Wichtig** oder **Nicht wichtig** aus. Wenn Sie eine App als „Kritisch“ oder „Wichtig“ markieren, nimmt Desktop Analytics einige Geräte mit der betreffenden App in die Pilotbereitstellung auf. Der Dienst nimmt in den Pilotversuch mehr Instanzen einer wichtigen App auf. Wenn Sie eine App als „Nicht wichtig“ markieren, wird sie von Desktop Analytics automatisch als **Bereit für Upgrade** festgelegt.

## <a name="pilot-devices"></a>Pilotgeräte

Desktop Analytics kombiniert ihre Informationen zur Wichtigkeit mit den Einstellungen des weltweiten Piloten. Anschließend wird eine Empfehlung erstellt, welche Geräte bei der Pilotbereitstellung berücksichtigt werden sollten. Die empfohlene Pilotbereitstellung umfasst Geräte mit unterschiedlichen Hardwarekonfigurationen sowie eine oder mehrere Instanzen aller kritischen und wichtigen Apps. Wenn eine App als „Kritisch“ markiert ist, empfiehlt der Dienst, weitere Geräte mit dieser App in den Pilotversuch aufzunehmen.

## <a name="deployment-plans-in-configuration-manager"></a>Bereitstellungspläne in Configuration Manager

Nachdem Sie einen Bereitstellungsplan erstellt haben, stellen Sie die Produkte mithilfe von Configuration Manager bereit. Nach dem Starten der Bereitstellung überwacht Desktop Analytics die Bereitstellung gemäß den Einstellungen im Plan.

## <a name="next-steps"></a>Nächste Schritte

- [Informationen zu Desktop Analytics-Objekten](about-assets.md): Geräte, Treiber und Apps  

- [Informationen zu Sicherheits- und Featureupdates](about-updates.md)  

- [Erstellen eines Bereitstellungsplans](create-deployment-plans.md)  
