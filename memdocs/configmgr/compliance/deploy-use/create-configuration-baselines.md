---
title: Erstellen von Konfigurationsbaselines
titleSuffix: Configuration Manager
description: Erstellen Sie in Configuration Manager Konfigurationsbaselines, die Sie in einer Sammlung bereitstellen können.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 678c9622-c61b-47d1-ba25-690616e431c7
author: mestew
manager: dougeby
ms.author: mstewart
ms.openlocfilehash: 01355230d0dc8969555740cc25a08e0b8d2967d0
ms.sourcegitcommit: 9ec77929df571a6399f4e06f07be852314a3c5a4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2020
ms.locfileid: "86240472"
---
# <a name="create-configuration-baselines-in-configuration-manager"></a>Erstellen von Konfigurationsbaselines in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*


Konfigurationsbaselines in Configuration Manager enthalten vordefinierte Konfigurationselemente und gegebenenfalls andere Konfigurationsbaselines. Nachdem eine Konfigurationsbasislinie erstellt wurde, können Sie sie für eine Sammlung bereitstellen. Auf diese Weise wird die Konfigurationsbasislinie von Geräten in dieser Sammlung heruntergeladen und deren Konformität mit der Konfigurationsbasislinie ausgewertet.  

> [!TIP]
> Es gibt keine Möglichkeit, die Reihenfolge anzugeben, in der die Konfigurationselemente in einer Baseline vom Configuration Manager-Client ausgewertet werden. Diese ist nicht deterministisch.<!-- MEMDocs#175 -->

## <a name="configuration-baselines"></a>Konfigurationsbasislinien

 Konfigurationsbaselines können in Configuration Manager bestimmte Revisionen von Konfigurationselementen enthalten, oder sie können so konfiguriert werden, dass sie immer die neueste Version eines Konfigurationselements verwenden. Weitere Informationen zu Konfigurationselementrevisionen finden Sie unter [Verwaltungstasks für Konfigurationsdaten](../../compliance/deploy-use/management-tasks-for-configuration-data.md).  

 Es gibt zwei Methoden, mit denen Sie Konfigurationsbaselines erstellen können:  

- Importieren Sie Konfigurationsdaten aus einer Datei. Klicken Sie zum Starten des **Assistenten zum Importieren von Konfigurationsdaten**im Arbeitsbereich **Bestand und Kompatibilität** auf den Knoten **Konfigurationselemente** oder **Konfigurationsbasislinien** , und klicken Sie dann auf **Konfigurationsdaten importieren**. Weitere Informationen finden Sie unter [Importieren von Konfigurationsdaten mit System Center Configuration Manager](import-configuration-data.md).

- Verwenden Sie zum Erstellen einer neuen Konfigurationsbasislinie das Dialogfeld **Konfigurationsbasislinie erstellen** .  

## <a name="create-a-configuration-baseline"></a>Erstellen einer Konfigurationsbaseline

Gehen Sie wie folgt vor, um mithilfe des Dialogfelds **Konfigurationsbaseline erstellen** eine Konfigurationsbaseline zu erstellen:  

1. Klicken Sie in der Configuration Manager-Konsole auf **Assets und Konformität** > **Konformitätseinstellungen** > **Konfigurationsbaselines**.  

2. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Konfigurationsbaseline erstellen**.  

3. Geben Sie im Dialogfeld **Konfigurationsbasislinie erstellen** einen eindeutigen Namen und eine Beschreibung für die Konfigurationsbasislinie ein. Sie können für den Namen maximal 255 Zeichen verwenden, für die Beschreibung sind maximal 512 Zeichen zulässig.  

4. In der Liste **Konfigurationsdaten** werden alle Konfigurationselemente oder Konfigurationsbasislinien angezeigt, die in dieser Konfigurationsbasislinie enthalten sind. Klicken Sie auf **Hinzufügen** , um der Liste ein neues Konfigurationselement oder eine neue Konfigurationsbasislinie hinzuzufügen. Folgende Elemente stehen Ihnen zur Auswahl:  

   - **Bestand und Kompatibilität**  

   - **Softwareupdates**  

   - **Konfigurationselemente**  
     > [!IMPORTANT]
     > Sie müssen jede Konfigurationsbaseline auf nicht mehr als 1.000 Softwareupdates begrenzen.
5. Verwenden Sie zum Angeben des Verhaltens eines Konfigurationselements, das Sie in der Liste **Konfigurationsdaten** angegeben haben, die Liste **Zweck ändern**. Folgende Elemente stehen Ihnen zur Auswahl:  

   -   **Erforderlich:** Die Konfigurationsbaseline wird als nicht konform ausgewertet, wenn das Konfigurationselement auf einem Clientgerät nicht erkannt wird. Wenn es erkannt wird, wird es auf Konformität geprüft.  

   -   **Optional:** Die Konformität des Konfigurationselements wird nur ausgewertet, wenn die Anwendung, auf die es verweist, auf Clientcomputern gefunden wird. Wird die Anwendung nicht gefunden, wird die Konfigurationsbaseline nicht als nicht konform markiert (gilt nur für Anwendungskonfigurationselemente).  

   -   **Nicht zugelassen:** Die Konfigurationsbaseline wird als nicht konform ausgewertet, wenn das Konfigurationselement auf Clientcomputern erkannt wird (gilt nur für Anwendungskonfigurationselemente).  

   > [!NOTE]
   >  Die Liste **Zweck ändern** ist nur verfügbar, wenn Sie auf der Seite **Allgemein** des **Assistenten zum Erstellen von Konfigurationselementen** auf die Option **Dieses Konfigurationselement enthält Anwendungseinstellungen**geklickt haben.  

6. Verwenden Sie die Liste **Revision ändern** , um eine bestimmte oder die aktuelle Revision des Konfigurationselements für die Auswertung der Kompatibilität auf Clientgeräten auszuwählen, oder wählen Sie **Immer aktuelle verwenden** aus, damit immer die aktuelle Revision verwendet wird. Weitere Informationen zu Konfigurationselementrevisionen finden Sie unter [Verwaltungstasks für Konfigurationsdaten](../../compliance/deploy-use/management-tasks-for-configuration-data.md).  

7. Wählen Sie zum Entfernen eines Konfigurationselements aus der Konfigurationsbaseline ein Konfigurationselement aus, und klicken Sie auf **Entfernen**.  

8. Wählen Sie ab Version 1806 aus, ob Sie **Diese Baseline immer für gemeinsam verwaltete Clients anwenden** möchten. Wenn diese Option aktiviert ist, wird diese Baseline sogar auf Clients angewendet, die von Intune verwaltet werden.  Diese Ausnahme kann genutzt werden, um Einstellungen zu konfigurieren, die Ihre Organisation benötigt, jedoch noch nicht in Intune verfügbar sind.

9. Klicken Sie optional auf **Kategorien**, um der Baseline Kategorien zum Suchen und Filtern zuzuweisen. 

10. Klicken Sie auf **OK** , um das Dialogfeld **Konfigurationsbasislinie erstellen** zu schließen und die Konfigurationsbasislinie zu erstellen.  

>[!NOTE]
> Durch Ändern einer vorhandenen Baseline, z.B. das Einstellen von **Diese Baseline immer für gemeinsam verwaltete Clients anwenden**, wird die Inhaltsversion der Baseline erhöht. Clients müssen die neue Version auswerten, um die Berichterstellung für die Baseline zu aktualisieren.

## <a name="include-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a><a name="bkmk_CAbaselines"></a> Einbeziehen benutzerdefinierter Konfigurationsbaselines im Rahmen der Konformitätsrichtlinienbewertung
<!--3608345-->
*(Eingeführt in Version 1910)*

Ab Version 1910 können Sie die Auswertung benutzerdefinierter Konfigurationsbaselines als Regel für die Konformitätsrichtlinienbewertung hinzufügen. Wenn Sie eine Konfigurationsbaseline bearbeiten oder erstellen, können Sie die Option **Diese Baseline als Teil der Konformitätsrichtlinienbewertung auswerten** auswählen. Beim Hinzufügen oder Bearbeiten einer Konformitätsrichtlinienregel ist eine Bedingung mit dem Namen **Konfigurierte Baselines in Konformitätsrichtlinienauswertung einbeziehen** verfügbar. Bei gemeinsam verwalteten Geräten und wenn Sie Intune so konfigurieren, dass die Ergebnisse der Konformitätsbewertung von Configuration Manager als Teil des Gesamtkonformitätsstatus übernommen werden, werden diese Informationen an Azure AD gesendet. Sie können diese dann für den bedingten Zugriff auf Ihre Office 365-Ressourcen verwenden. Weitere Informationen finden Sie unter [Bedingter Zugriff mit Co-Verwaltung](../../comanage/quickstart-conditional-access.md).

Gehen Sie wie folgt vor, um benutzerdefinierte Konfigurationsbaselines in die Konformitätsrichtlinienauswertung einzubeziehen:

- Erstellen Sie eine Konformitätsrichtlinie mit der Regel [**Konfigurierte Baselines in Konformitätsrichtlinienauswertung einbeziehen**](#bkmk_CA), und stellen Sie sie für eine Benutzersammlung bereit.
- Wählen Sie bei einer Konfigurationsbaseline, die für eine Gerätesammlung konfiguriert wird, die Option [**Diese Baseline als Teil der Konformitätsrichtlinienbewertung auswerten**](#bkmk_eval-baseline) aus.

> [!IMPORTANT]
> Wenn die Bereitstellung für gemeinsam verwaltete Geräte erfolgt, müssen Sie sicherstellen, dass Sie die [Voraussetzungen für die Co-Verwaltung](../../comanage/overview.md#prerequisites) erfüllen.

### <a name="example-evaluation-scenario"></a>Beispielszenario für die Auswertung

Wenn ein Benutzer Teil einer Sammlung ist, für die eine Kompatibilitätsrichtlinie festgelegt ist, die die Regelbedingung **Konfigurierte Baselines in Konformitätsrichtlinienauswertung einbeziehen** enthält, werden alle Baselines mit ausgewählter Option **Diese Baseline als Teil der Konformitätsrichtlinienbewertung auswerten**, die für den Benutzer oder das Gerät des Benutzers bereitgestellt sind, im Hinblick auf Konformität ausgewertet. Beispiel:

- `User1` ist in `User Collection 1` enthalten.
- `User1` verwendet `Device1`, das in `Device Collection 1` und `Device Collection 2` enthalten ist.
- `Compliance Policy 1` verfügt über die Regelbedingung **Konfigurierte Baselines in Konformitätsrichtlinienauswertung einbeziehen** und wird für `User Collection 1` bereitgestellt.
- Für `Configuration Baseline 1` ist **Diese Baseline als Teil der Konformitätsrichtlinienbewertung auswerten** ausgewählt, und sie wird für `Device Collection 1` bereitgestellt.
- Für `Configuration Baseline 2` ist **Diese Baseline als Teil der Konformitätsrichtlinienbewertung auswerten** ausgewählt, und sie wird für `Device Collection 2` bereitgestellt.

Wenn `Compliance Policy 1` in diesem Szenario für `User1` mit `Device1` ausgewertet wird, werden sowohl `Configuration Baseline 1` als auch `Configuration Baseline 2` ebenfalls ausgewertet.

- `User1` verwendet manchmal `Device2`.
- `Device2` ist ein Element von `Device Collection 2` und `Device Collection 3`.
- Für `Device Collection 3` wird `Configuration Baseline 3` bereitgestellt, aber **Diese Baseline als Teil der Konformitätsrichtlinienbewertung auswerten** ist nicht ausgewählt.

Wenn `User1``Device2` verwendet, wird nur `Configuration Baseline 2` ausgewertet, wenn `Compliance Policy 1` ausgewertet wird.

> [!NOTE]
><!--5582516-->
> Wenn die Kompatibilitätsrichtlinie eine neue Baseline auswertet, die noch nie zuvor auf dem Client ausgewertet wurde, wird möglicherweise Nichtkonformität gemeldet. Dies tritt auf, wenn die Baselineauswertung noch ausgeführt wird, wenn die Konformität ausgewertet wird. Um dieses Problem zu umgehen, klicken Sie im **Softwarecenter** auf **Kompatibilität überprüfen**.

### <a name="create-and-deploy-a-compliance-policy-with-a-rule-for-baseline-compliance-policy-assessment"></a><a name="bkmk_CA"></a> Erstellen und Bereitstellen einer Konformitätsrichtlinie mit einer Regel für die Baselinekonformitätsrichtlinienauswertung

1. Erweitern Sie im Arbeitsbereich **Bestand und Kompatibilität** die **Kompatibilitätseinstellungen**, und wählen Sie dann den Knoten **Kompatibilitätsrichtlinien** aus.
1. Klicken Sie im Menüband auf **Konformitätsrichtlinie erstellen**, um den **Assistenten zum Erstellen von Kompatibilitätsrichtlinien** zu aktivieren. 
1. Wählen Sie auf der Seite **Allgemein** die Option **Konformitätsregeln für Geräte, die mit dem Configuration Manager-Client verwaltet werden** aus.
   - Geräte müssen mit dem Configuration Manager-Client verwaltet werden, um benutzerdefinierte Konfigurationsbaselines als Teil der Bewertung der Kompatibilitätsrichtlinie zu berücksichtigen.
1. Wählen Sie auf den Seiten **Unterstützte Plattformen** Ihre Plattformen aus.
1. Wählen Sie auf der Seite **Regeln** die Option **Neu** aus, und wählen Sie dann die Bedingung **Konfigurierte Baselines in Konformitätsrichtlinienauswertung einbeziehen** aus.

   ![Konfigurierte Baselines in Konformitätsrichtlinienauswertung einbeziehen](./media/3608345-create-compliance-policy-rule.png)

1. Klicken Sie auf **OK** und dann auf **Weiter**, um zur Seite **Zusammenfassung** zu gelangen.
1. Überprüfen Sie die Auswahl, und klicken Sie dann auf **Weiter** und auf **Schließen**.
1. Klicken Sie im Knoten **Konformitätsrichtlinien** mit der rechten Maustaste auf die Richtlinie, die Sie erstellt haben, und wählen Sie **Bereitstellen** aus.
1. Wählen Sie Ihre Sammlung, die Einstellungen für die Warnungsgenerierung und den Zeitplan für die Kompatibilitätsauswertung für die Richtlinie aus.
1. Klicken Sie auf **OK**, um die Konformitätsrichtlinie bereitzustellen.

### <a name="select-a-configuration-baseline-and-check-evaluate-this-baseline-as-part-of-compliance-policy-assessment"></a><a name="bkmk_eval-baseline"></a>Auswählen einer Konfigurationsbaseline und Aktivieren der Option „Diese Baseline als Teil der Konformitätsrichtlinienbewertung auswerten“

1. Erweitern Sie im Arbeitsbereich **Bestand und Konformität** die **Konformitätseinstellungen**, und wählen Sie dann den Knoten **Konfigurationsbaselines** aus.
1. Klicken Sie mit der rechten Maustaste auf eine vorhandene Baseline, die in einer Gerätesammlung bereitgestellt wird, und wählen Sie dann **Eigenschaften** aus. Bei Bedarf können Sie eine neue Baseline erstellen.
   - Die Baseline muss für eine Gerätesammlung, nicht für eine Benutzersammlung bereitgestellt werden.
1. Aktivieren Sie die Einstellung **Diese Baseline als Teil der Konformitätsrichtlinienbewertung auswerten**.
   - Für gemeinsam verwaltete Geräte, bei denen Intune als Autorität für die **Gerätekonfiguration** gilt, müssen Sie sicherstellen, dass auch die Option **Diese Baseline auch immer für gemeinsam verwaltete Clients anwenden** ausgewählt ist.
1. Klicken Sie auf **OK**, um die Änderungen an der Konfigurationsbaseline zu speichern.

   ![Dialogfeld „Eigenschaften der Konfigurationsbaseline“](./media/3608345-configuration-baseline-properties.png)

### <a name="log-files-for-custom-configuration-baselines-as-part-of-compliance-policy-assessment"></a>Protokolldateien für benutzerdefinierte Konfigurationsbaselines als Teil der Konformitätsrichtlinienauswertung

- ComplianceHandler.log
- SettingsAgent.log
- DCMAgent.log
- CIAgent.log

## <a name="next-steps"></a>Nächste Schritte

[Importieren von Konfigurationsdaten](import-configuration-data.md)
