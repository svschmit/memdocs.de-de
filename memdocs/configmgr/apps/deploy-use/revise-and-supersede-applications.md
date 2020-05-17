---
title: Überarbeiten und Ablösen von Anwendungen
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Configuration Manager-Anwendungsversionen verwenden und Anwendungen ersetzen.
ms.date: 05/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 30170d70-489f-47f7-bebf-9ed0115db26b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 6afed00b8207edb338b2a6dc62e083a5267fa47e
ms.sourcegitcommit: 4c129bb04ea4916c78446e89fbff956397cbe828
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/13/2020
ms.locfileid: "83343132"
---
# <a name="revise-and-supersede-applications-in-configuration-manager"></a>Überarbeiten und Ablösen von Anwendungen in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

In diesem Thema erfahren Sie, wie Sie mit Configuration Manager-Anwendungsversionen arbeiten und wie Anwendungen durch eine neue Version abgelöst werden.  

##  <a name="application-revisions"></a>Anwendungsrevisionen  
 Wenn Sie an einer Anwendung oder an einem in einer Anwendung enthaltenen Bereitstellungstyp Änderungen vornehmen, wird in Configuration Manager eine neue Revision der Anwendung erstellt. Sie können den Verlauf jeder Anwendungsrevision anzeigen. Außerdem können Sie die Eigenschaften anzeigen, eine ältere Revision einer Anwendung wiederherstellen oder eine ältere Revision löschen.  

### <a name="to-display-an-application-revision-history"></a>So zeigen Sie einen Anwendungsrevisionsverlauf an  

1.  Wählen Sie in der Configuration Manager-Konsole **Softwarebibliothek** > **Anwendungsverwaltung** > **Anwendungen** und anschließend die gewünschte Anwendung aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Anwendung** die Option **Revisionsverlauf** aus, um das Dialogfeld **Anwendungsrevisionsverlauf** zu öffnen.  

### <a name="to-view-an-application-revision"></a>So zeigen Sie eine Anwendungsrevision an  

1.  Wählen Sie im Dialogfeld **Anwendungsrevisionsverlauf** eine Anwendungsrevision aus, und wählen Sie dann **Anzeigen** aus.  

2.  Sehen Sie sich im Dialogfeld **Eigenschaften** die Eigenschaften der ausgewählten Anwendung an.  

    > [!NOTE]  
    >  Die angezeigten Anwendungseigenschaften sind schreibgeschützt.  

3.  Schließen Sie das Dialogfeld **Eigenschaften** .  

### <a name="to-restore-an-application-revision"></a>So stellen Sie eine Anwendungsrevision wieder her  

1.  Wählen Sie im Dialogfeld **Anwendungsrevisionsverlauf** eine Anwendungsrevision aus, und wählen Sie dann **Wiederherstellen** aus.  

2.  Wählen Sie im Dialogfeld zum **Bestätigen der Wiederherstellung der Revision** **Ja** aus, um die ausgewählte Anwendungsrevision wiederherzustellen.  

### <a name="to-delete-an-application-revision"></a>So löschen Sie eine Anwendungsrevision  

1.  Wählen Sie im Dialogfeld **Anwendungsrevisionsverlauf** eine Anwendungsrevision aus, und wählen Sie dann **Löschen** aus.  

2.  Wählen Sie im Dialogfeld zum **Bestätigen des Löschens der Anwendungsrevision** **Ja** aus.  

> [!IMPORTANT]  
>  Sie können die aktuelle Anwendungsrevision nur löschen, wenn die Anwendung zuvor außer Kraft gesetzt wurde und keine Verweise enthält.  

##  <a name="application-supersedence"></a>Anwendungsablösung  
 Die Anwendungsverwaltung in Configuration Manager ermöglicht es Ihnen, vorhandene Anwendungen mithilfe einer Ablösungsbeziehung zu aktualisieren oder zu ersetzen. Wenn Sie eine Anwendung ablösen, können Sie einen neuen Bereitstellungstyp als Ersatz für den Bereitstellungstyp der abgelösten Anwendung angeben. Sie können außerdem festlegen, ob vor dem Installieren der ablösenden Anwendung ein Upgrade der abzulösenden Anwendung ausgeführt oder die abzulösende Anwendung deinstalliert werden soll. Generell empfehlen wir, Supersenzketten auf maximal fünf Ebenen zu begrenzen.
 
> [!IMPORTANT]  
>  Wenn die Option zum Deinstallieren des abgelösten Bereitstellungstyps ausgewählt wurde, ist es nicht möglich, für die Ablösung einen Bereitstellungstyp zu verwenden, der für einen anderen Sammlungstyp bereitgestellt wurde.  Beispielsweise kann bei dieser Optionsauswahl ein Bereitstellungstyp, der für eine Gerätesammlung bereitgestellt wurde, nicht durch einen Bereitstellungstyp abgelöst werden, der für eine Benutzersammlung bereitgestellt wurde.  

### <a name="decide-whether-to-upgrade-or-replace-an-application"></a>Festlegen, ob eine Anwendung ersetzt oder ein Upgrade ausgeführt werden soll  
 Im Dialogfeld **Ablösungsbeziehung angeben** unter den Anwendungseigenschaften geben Sie an, ob eine Anwendung ersetzt oder ein Upgrade ausgeführt werden soll. Der Ablösungstyp hängt davon ab, ob Sie in diesem Dialogfeld die Option **Deinstallieren** aktivieren:  

-   Wenn Sie ein Update auf eine neuere Version der gleichen Anwendung (mit der gleichen Anwendungs-ID) ausführen möchten, aktiveren Sie **nicht** die Option **Deinstallieren**.  

-   Wenn Sie zu einer anderen Anwendung (mit einer anderen Anwendungs-ID) wechseln möchten, aktivieren Sie die Option **Deinstallieren**. Sie müssen die abgelöste Version der Anwendung entfernen.  

### <a name="supersede-dependent-applications"></a>Ablösen abhängiger Anwendungen  
 In diesem Beispiel bezieht sich **Masteranwendung** auf die von Ihnen bereitgestellte Anwendung, die die Abhängigkeiten enthält.  

 Sie können eine Ablösungsbeziehung erstellen, mit der die abhängige Anwendung auf eine neue Version aktualisiert wird.  

1. Stellen Sie sicher, dass die neue abhängige Anwendung und die ursprüngliche abhängige Anwendung in der gleichen Abhängigkeitsgruppe der Masteranwendung enthalten sind.  

2. Erstellen Sie eine Ablösungsbeziehung, bei der die ursprüngliche abhängige Anwendung durch die neue abhängige Anwendung ersetzt wird.  

   Während neuer Installationen der Masteranwendung wird die neue abhängige Anwendung installiert. Vorhandene Installationen der Masteranwendung werden mit der neuen abhängigen Anwendung aktualisiert.  

   Als Endergebnis verwenden alle Bereitstellungen der Masteranwendung die neue abhängige Anwendung.  

### <a name="further-considerations"></a>Weitere Überlegungen  

-   Sie können mehrere Ablösungsbeziehungen für abhängige Anwendungen angeben. Die höchste abhängige Anwendung in der Ablösungskette wird installiert.  

-   Abhängige Anwendungen müssen auf dem Gerät bereitgestellt werden, auf dem die Masteranwendung installiert ist. Andernfalls wird die abhängige Anwendung nicht installiert.  

-   Wenn bei neuen Installationen der Masteranwendung mehrere Abhängigkeiten bestehen, bestimmt die Abhängigkeitsreihenfolge, welche Version der abhängigen Anwendung installiert wird.  

### <a name="to-specify-a-supersedence-relationship"></a>So geben Sie eine Ablösungsbeziehung an  

1.  Wählen Sie in der Configuration Manager-Konsole **Softwarebibliothek** > **Anwendungsverwaltung** > **Anwendungen** und anschließend die Anwendung aus, die eine andere ablösen soll.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus, um das Dialogfeld **Eigenschaften** für die Anwendung zu öffnen.  

4.  Wählen Sie auf der Registerkarte **Ablösung** im Dialogfeld **Eigenschaften von** *<Anwendungsname\>* die Option **Hinzufügen** aus.  

5.  Klicken Sie im Dialogfeld **Ablösungsbeziehung angeben** auf **Durchsuchen**.  

6.  Wählen Sie im Dialogfeld **Anwendung auswählen** die Anwendung aus, die Sie ablösen möchten, und wählen Sie dann **OK** aus.  

7.  Wählen Sie im Dialogfeld **Ablösungsbeziehung angeben** den Bereitstellungstyp aus, von dem der Bereitstellungstyp der abzulösenden Anwendung abgelöst werden soll.  

    > [!NOTE]  
    >  Standardmäßig wird der Bereitstellungstyp der abzulösenden Anwendung nicht vom neuen Bereitstellungstyp deinstalliert. Dieses Szenario wird häufig verwendet, wenn Upgrades für vorhandene Anwendungen bereitgestellt werden sollen. Wählen Sie **Deinstallieren** aus, um den vorhandenen Bereitstellungstyp zu deinstallieren, bevor der neue Bereitstellungstyp installiert wird. Probieren Sie das Upgrade zunächst in einer Testumgebung aus, bevor Sie es für eine Anwendung ausführen.  

8.  Wählen Sie **OK** aus, um das Dialogfeld **Ablösungsbeziehung angeben** zu schließen.  

9. Wählen Sie **OK** aus, um das Dialogfeld **Eigenschaften von** *<Anwendungsname\>* zu schließen.  

### <a name="to-display-applications-that-supersede-the-current-application"></a>So zeigen Sie Anwendungen an, von der die aktuelle Anwendung abgelöst wird  

1.  Wählen Sie in der Configuration Manager-Konsole die Option **Softwarebibliothek** aus.  

2.  Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Anwendungsverwaltung**, und wählen Sie **Anwendungen** und dann die gewünschte Anwendung aus.  

3.  Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Eigenschaften** die Option **Eigenschaften** aus, um das Dialogfeld **Eigenschaften von** *<Anwendungsname\>* zu öffnen.  

4.  Wählen Sie auf der Registerkarte **Referenzen** im Dialogfeld **Eigenschaften von** *<Anwendungsname\>* in der Dropdownliste **Beziehungstyp** die Option **Anwendungen, die diese Anwendung ablösen** aus.  

5.  Prüfen Sie die Liste der Anwendungen, von denen die ausgewählte Anwendung abgelöst wird, und wählen Sie dann **OK** aus, um das Dialogfeld **Eigenschaften von** *<Anwendungsname\>* zu schließen.  
