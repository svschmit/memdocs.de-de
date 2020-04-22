---
title: 'Installieren eines Standorts mit 1606-Baselinemedien '
titleSuffix: Configuration Manager
description: Installieren von oder Durchführen eines Upgrades auf LTSB für System Center Configuration Manager
ms.date: 09/06/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: f4f9a5fd-f573-4b99-ad93-b2c76812e922
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 7d70611aff329f48c8223a47dfa238e5a4559972
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81707008"
---
# <a name="install-and-upgrade-with-the-version-1606-baseline-media"></a>Installieren und Upgraden mit dem Baselinemedium von Version 1606

*Gilt für: System Center Configuration Manager (Long Term Servicing Branch)*

Wenn Sie ein Setup vom Baselinemedium Version 1606 für Configuration Manager ausführen, können Sie einen Long-Term Servicing Branch-Standort von System Center Configuration Manager installieren.

Das Baselinemedium ist als Teil der Version Microsoft System Center 2016 oder der Version System Center Configuration Manager (Long-Term Servicing Branch 1606) auf DVD verfügbar. Weitere Informationen zum Baselinemedium finden Sie auf der Seite zu den [Baseline- und Updateversionen](../servers/manage/updates.md#bkmk_Baselines).


Wenn Sie das Baselinemedium von Version 1606 verwenden, ist der Standort, den Sie installieren oder auf den Sie aktualisieren:
- Ein *Current Branch-Standort*, der einem Standort entspricht, der anfänglich mit dem 1511-Baselinemedium installiert wurde und später auf Version 1606 und das entsprechende 1606-Hotfixrollup „KB3186654“ aktualisiert wurde.
- Ein *LTSB-Standort*, der dem Current Branch-Standort entspricht, der die Version 1606 und das entsprechende 1606-Hotfixrollup „KB3186654“ ausführt. Das Baselinemedium enthält bereits das Hotfixrollup.  Wie im Artikel [Einführung in Long-Term Servicing Branch von System Center Configuration Manager](introduction-to-the-ltsb.md) beschrieben wird, unterstützt LTSB jedoch nicht alle Features oder Funktionen, die in Current Branch verfügbar sind.

Wenn Sie nicht mit den verschiedenen Branches von Configuration Manager vertraut sind, finden Sie weitere Informationen unter [Welcher Branch von Configuration Manager soll verwendet werden?](which-branch-should-i-use.md).




## <a name="changes-to-setup-with-the-1606-baseline-media"></a>Änderungen an dem Setup mit dem 1606-Baselinemedium
Das 1606-Baselinemedium führt die folgenden Neuerungen für das Configuration Manager-Setup ein.

### <a name="branch-and-edition"></a>Branch und Edition
Wenn Sie das Setup ausführen, wird Ihnen jetzt eine Lizenzierungsseite angezeigt, in dem Sie den Branch von Configuration Manager auswählen können, den Sie installieren möchten. Sie können Current Branch oder LTSB als lizenzierte Installation auswählen. Alternativ können Sie sich für eine Evaluierungsversion von Current Branch als nicht lizenzierte Installation entscheiden.

Weitere Informationen finden Sie unter [Lizenzierung und Branches für Configuration Manager](learn-more-editions.md).

### <a name="software-assurance-expiration"></a>Ablauf der Software Assurance
Während des Setups können Sie das **Software Assurance-Ablaufdatum** eingeben. Dies ist ein optionaler Wert, den Sie als praktische Erinnerung angeben können.

> [!NOTE]
> Microsoft überprüft das eingegebene Ablaufdatum nicht und verwendet es auch nicht für die Lizenzüberprüfung.  Stattdessen können Sie das Ablaufdatum angeben, um daran erinnert zu werden. Dies ist hilfreich, da Configuration Manager regelmäßig überprüft, ob neue Softwareupdates online angeboten werden, und Ihr Software Assurance-Lizenzstatus sollte aktuell sein, damit Sie von diesen zusätzlichen Updates profitieren können.    

- Sie können das Datum auf der Seite **Product Key** des Setup-Assistenten angeben, wenn Sie das Setup vom Baselinemedium von Configuration Manager-Version 1606 ausführen.
- Sie können dieses Datum ferner angeben, indem Sie auf der Configuration Manager-Konsole **Eigenschaften von Hierarchieeinstellungen** > **Lizenzierung** auswählen.

Weitere Informationen finden Sie im Abschnitt „Software Assurance-Verträge“ des Artikels [Lizenzierung und Branches für Configuration Manager](learn-more-editions.md).


### <a name="additional-pre-upgrade-configurations"></a>Zusätzliche Konfigurationen vor dem Upgrade
Vor dem Starten eines Upgrades von System Center 2012 Configuration Manager auf LTSB, müssen Sie für die Prüfliste die folgenden zusätzlichen Schritte ausführen.  
Deinstallieren Sie die nicht von LTSB unterstützten Standortsystemrollen:
- Asset Intelligence-Synchronisierungspunkt
- Microsoft Intune-Connector
- Cloudbasierte Verteilungspunkte

Weitere Informationen finden Sie unter [Upgrade auf System Center Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md).


### <a name="new-scripted-installation-options"></a>Neue Skriptinstallationsoptionen
Das Baselinemedium von Version 1606 unterstützt einen neuen, unbeaufsichtigten Skriptdateischlüssel für skriptgesteuerte Installationen eines neuen Standorts der obersten Ebene. Dies gilt sowohl für die Installation eines neuen, eigenständigen primären Standorts als auch eines Standorts der zentralen Verwaltung im Rahmen eines Standorterweiterungsszenarios.

Wenn Sie ein unbeaufsichtigtes Skript verwenden, um einen lizenzierten Branch zu installieren, müssen Sie den folgenden Abschnitt, Schlüsselnamen und Werte im Abschnitt „Optionen“ Ihres Skripts hinzufügen. Sie müssen diese Werte nicht verwenden, um ein Skript für die Installation einer Evaluierungsversion von Current Branch zu erstellen:  

 **SABranchOptions**
- **Schlüsselname: SAActive**
  - Werte: 0 oder 1  
  - Details:  Mit 0 wird eine nicht lizenzierte Auswertungsedition von Current Branch und mit 1 die lizenzierte Edition installiert.   

- **CurrentBranch**
  - Werte: 0 oder 1  
  - Details:  Mit 0 wird Long-Term Servicing Branch und mit 1 Current Branch installiert.  

Um eine lizenzierte Current Branch-Edition zu erstellen, würden Sie z.B. Folgendes verwenden:

**Schlüsselname: SABranchOptions**
- **SAActive = 1**
- **CurrentBranch = 1**


> [!IMPORTANT]  
> **SABranchOptions** funktioniert nur mit dem Setup vom Baselinemedium. Es funktioniert nicht, wenn Sie das Setup aus dem Ordner „CD.Latest“ ausführen, den Sie zuvor mithilfe des Baselinemediums von Version 1606 installiert haben.
>
> **SABranchOptions** funktioniert nicht für skriptgesteuerte Upgrades von System Center 2012 Configuration Manager und installiert immer Current Branch.

Weitere Informationen finden Sie unter [Verwenden einer Befehlszeile zum Installieren von Configuration Manager-Standorten](../servers/deploy/install/use-a-command-line-to-install-sites.md).


## <a name="install-a-new-site"></a>Installieren eines neuen Standorts
Wenn Sie das 1606-Baselinemedium verwenden, um einen neuen Standort für jeden Branch zu installieren, verwenden Sie die Standortplanung, die Vorbereitung und die Installationsprozedur, die im Thema [Ressourcen für die Installation von Configuration Manager-Standorten](../servers/deploy/install/installing-sites.md) dokumentiert sind, zusätzlich zu den folgenden Überlegungen zum Setup:

- Während des Setups müssen Sie den Configuration Manager-Branch auswählen, den Sie installieren möchten, und Sie können Details zu Ihrem Software Assurance-Vertrag angeben.
- Alle Standorte in derselben Hierarchie müssen denselben Branch ausführen. Eine Hierarchie mit einer Mischung aus LTSB und Current Branch an unterschiedlichen Standorten wird nicht unterstützt.
- Neue Skriptinstallation. Weitere Informationen finden Sie unter „Neue Skriptinstallationsoptionen“ weiter oben in diesem Artikel.

## <a name="expand-a-stand-alone-primary-site"></a>Erweitern eines eigenständigen primären Standorts
Sie können einen eigenständigen primären Standort erweitern, auf dem LTSB ausgeführt wird.  Der Prozess unterscheidet sich nicht von dem, der für einen Current Branch-Standort verwendet wird, jedoch mit einer Einschränkung:

- Bei der Installation des neuen Standorts der zentralen Verwaltung müssen Sie das Setup vom ursprünglichen Quellmedium verwenden, das Sie zum Installieren des LTSB-Standorts verwendet haben. Die Ausführung des Setups aus dem Ordner „CD.Latest“ wird für dieses Szenario nicht unterstützt.

Weitere Informationen zur Standorterweiterung finden Sie im Abschnitt „Erweitern eines eigenständigen primären Standorts“ des Artikels [Verwenden des Setup-Assistenten zum Installieren von System Center Configuration Manager-Standorten](../servers/deploy/install/use-the-setup-wizard-to-install-sites.md).

## <a name="upgrade-from-system-center-2012-configuration-manager"></a>Upgrade von System Center 2012 Configuration Manager
Bei einem Upgrade von System Center 2012 Configuration Manager sollten Sie die im Thema [Upgraden auf Current Branch für Configuration Manager](../servers/deploy/install/upgrade-to-configuration-manager.md) beschriebene(n) Standortplanung, Vorbereitung und Prozeduren verwenden, allerdings mit den folgenden Änderungen:

**Upgrade auf Current Branch:**
- Während des Setups müssen Sie Current Branch auswählen, und Sie können Details zu Ihrem Software Assurance-Vertrag angeben.
- Neue Skriptinstallation. Weitere Informationen finden Sie unter „Neue Skriptinstallationsoptionen“ weiter oben in diesem Artikel.

**Upgrade auf LTSB:**  
- Zusätzliche Schritte zu der vor dem Upgrade durchzugehenden Prüfliste
- Während des Setups müssen Sie LTSB auswählen, und Sie können Details zu Ihrem Software Assurance-Vertrag angeben.
- Sie können ein Upgrade nur für einen Standort durchführen, der System Center 2012 Configuration Manager mit Service Pack 1, System Center 2012 Configuration Manager mit Service Pack 2, System Center 2012 R2 Configuration Manager mit Service Pack 1 oder System Center 2012 R2 Configuration Manager ohne Service Pack ausführt.

### <a name="in-place-upgrade-paths-for-the-1606-baseline-media"></a>Pfade für direkte Upgrades für das 1606-Baselinemedium
Sie können das 1606-Baselinemedium verwenden, um folgende Versionen auf eine lizenzierte Version von Configuration Manager upzugraden:
- System Center 2012 R2 Configuration Manager mit Service Pack 1
- System Center 2012 R2 Configuration Manager ohne Service Pack (dies erfordert die Verwendung der Baselinemedien für Version 1606, die am 15. Dezember 2016 wieder veröffentlicht wurde.)
- System Center 2012 Configuration Manager mit Service Pack 2
- System Center 2012 Configuration Manager mit Service Pack 1 (dies erfordert die Verwendung der Baselinemedien für Version 1606, die am 15. Dezember 2016 wieder veröffentlicht wurde.)


Sie können diese Medien auch dazu verwenden, um eine nicht lizenzierte Evaluierungsversion von Current Branch auf eine vollständig lizenzierte Version von Current Branch upzugraden.

Das Medium unterstützt kein Upgrade von:
- Anderen Versionen von System Center 2012 Configuration Manager
- Configuration Manager 2007 oder früher
- Einer Release Candidate-Installation von Configuration Manager

## <a name="about-the-cdlatest-folder-and-the-ltsb"></a>Informationen zu dem Ordner „CD.Latest“ und LTSB
Die folgenden Einschränkungen betreffen die Verwendung der Medien, die Configuration Manager im Ordner „CD.Latest“ auf dem Standortserver erstellt. Diese Einschränkungen gelten für Standorte, die LTSB ausführen:

Medien im Ordner „CD.Latest“ werden unterstützt für:
- Standortwiederherstellung
- Standortwartung
- Installation zusätzlicher untergeordneter primärer Standorte

Medien werden im Ordner „CD.Latest“ nicht unterstützt für:  
- Die Installation eines Standorts der zentralen Verwaltung im Rahmen eines Szenarios zur Standorterweiterung.

Weitere Informationen finden Sie unter [Der Ordner „CD.Latest“ für System Center Configuration Manager](../servers/manage/the-cd.latest-folder.md).

## <a name="backup-recovery-and-site-maintenance-for-the-ltsb"></a>Sicherung, Wiederherstellung und Standartwartung für LTSB
Verwenden Sie zum Sichern, Wiederherstellen oder Ausführen der Wartung eines Standorts, der LTSB ausführt, den Leitfaden und die Prozeduren, die im Artikel zu [Sicherung und Wiederherstellung in Configuration Manager](../servers/manage/backup-and-recovery.md) beschrieben werden.  

Verwenden Sie das Configuration Manager-Setup im Ordner „CD.Latest“ der Sicherung Ihres LTSB-Standorts.
