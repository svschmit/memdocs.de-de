---
title: Malwaredefinitionsupdates für Endpoint Protection
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie Configuration Manager-Softwareupdates zum Übermitteln von Definitionsupdates an Clientcomputer konfigurieren.
ms.date: 10/06/2017
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 3b9c4027-a98b-406b-935c-ccabcfe713df
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 16dce8e11edbe41dda3dcbf0fd503374ce05bf83
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81697258"
---
#  <a name="using-configuration-manager-software-updates-to-deliver-definition-updates"></a>Verwenden Configuration Manager-Softwareupdates zum Übermitteln von Definitionsupdates

*Gilt für: Configuration Manager (Current Branch)*


 Konfigurieren Sie Configuration Manager-Softwareupdates zum Übermitteln von Definitionsupdates an Clientcomputer. Dazu werden automatische Bereitstellungsregeln konfiguriert. Bevor Sie mit dem Erstellen von automatischen Bereitstellungsregeln beginnen, stellen Sie sicher, dass Sie Configuration Manager-Softwareupdates konfiguriert haben. Weitere Informationen finden Sie unter [Einführung in Softwareupdates](../../sum/understand/software-updates-introduction.md).

> [!NOTE]
>  Dieses Verfahren betrifft nur die Elemente, die speziell für Endpoint Protection konfiguriert werden müssen. Weitere Informationen zum Assistenten zum Erstellen automatischer Bereitstellungsregeln finden Sie unter [Automatisch Softwareupdates bereitstellen](../../sum/deploy-use/automatically-deploy-software-updates.md).

## <a name="to-configure-an-automatic-deployment-rule-to-deliver-definition-updates"></a>So konfigurieren Sie eine automatische Bereitstellungsregel zum Übermitteln von Definitionsupdates

1. Klicken Sie in der Configuration Manager-Konsole auf **Softwarebibliothek**.

2. Erweitern Sie im Arbeitsbereich **Softwarebibliothek** den Bereich **Softwareupdates**, und klicken Sie dann auf **Automatische Bereitstellungsregeln**.

3. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Automatische Bereitstellungsregel erstellen**.

4. Geben Sie im **Assistenten zum Erstellen automatischer Bereitstellungsregeln** auf der Seite **Allgemein**die folgenden Informationen an:

   -   **Name:** Geben Sie einen eindeutigen Namen für die automatische Bereitstellungsregel ein.

   -   **Sammlung:** Wählen Sie die Sammlung von Clientcomputern aus, für die die Definitionsupdates bereitgestellt werden sollen.

       > [!NOTE]
       >  Es können keine Definitionsupdates für Benutzersammlungen bereitgestellt werden.

5. Klicken Sie auf **Zu einer vorhandenen Softwareupdategruppe hinzufügen**.

6. Vergewissern Sie sich, dass das Kontrollkästchen  **Bereitstellung nach Ausführung dieser Regel aktivieren** aktiviert ist, und klicken Sie dann auf **Weiter**.

7. Wählen Sie im Assistenten auf der Seite **Bereitstellungseinstellungen** in der Liste **Detailstufe** **Nur Fehlermeldungen**aus, und klicken Sie dann auf **Weiter**.

   > [!NOTE]
   >  Durch die Auswahl von **Nur Fehlermeldungen** wird die Anzahl der Zustandsmeldungen reduziert, die von der Definitionsbereitstellung zurückgegeben werden. Durch diese Konfiguration wird die Prozessorauslastung der Configuration Manager-Server reduziert.

8. Aktivieren Sie in der Liste **Eigenschaftsfilter** das Kontrollkästchen **Updateklassifizierung** .

9. Klicken Sie in der Liste **Suchkriterien** auf **<zu suchende Elemente\>** . Wählen Sie dann im Dialogfeld **Suchkriterien** in der Liste **Geben Sie den zu suchenden Wert an** die Option **Definitionsupdates**aus.

10. Klicken Sie auf **OK** , um das Dialogfeld **Suchkriterien** zu schließen.

11. Aktivieren Sie in der Liste **Eigenschaftsfilter** das Kontrollkästchen **Produkt** .

12. Klicken Sie in der Liste **Suchkriterien** auf **<zu suchende Elemente\>** . Wählen Sie dann im Dialogfeld **Suchkriterien** in der Liste **Geben Sie den zu suchenden Wert an** die Option **Forefront Endpoint Protection 2010** für Windows 8.1 und frühere Versionen bzw. **Windows Defender** für Windows 10 und höhere Versionen aus.

13. Klicken Sie auf **OK** , um das Dialogfeld **Suchkriterien** zu schließen, und dann auf **Weiter**.

14. Filtern Sie optional abgelöste Updates heraus.   Gehen Sie hierzu folgendermaßen vor:
    1.  Aktivieren Sie in der Liste **Eigenschaftsfilter** das Kontrollkästchen **Abgelöst** .
    2.  Klicken Sie in der Liste **Suchkriterien** auf **<zu suchende Elemente\>** . Wählen Sie dann im Dialogfeld **Suchkriterien** in der Liste **Geben Sie den zu suchenden Wert an** die Option **Nein**aus.  <br><br>

15. Klicken Sie auf **OK** , um das Dialogfeld **Suchkriterien** zu schließen, und dann auf **Weiter**.

16. Wählen Sie im Assistenten auf der Seite **Auswertungszeitplan** die Option **Regel zur Ausführung nach Zeitplan aktivieren**aus, und konfigurieren Sie dann den Zeitplan, nach dem die Definitionsupdates heruntergeladen werden sollen. Konfigurieren Sie den Zeitplan so, dass die Regel mindestens zwei Stunden nach der letzten Synchronisierung des Softwareupdatepunkts ausgeführt wird. Klicken Sie auf **Weiter**.

17. Konfigurieren Sie im Assistenten auf der Seite **Bereitstellungszeitplan** die folgenden Einstellungen:

    -   **Zeit basiert auf**: Wählen Sie **UTC** aus, wenn die neuesten Definitionen von allen Clients in der Hierarchie zur selben Zeit installiert werden sollen. Die tatsächliche Installationszeit verteilt sich innerhalb eines Zeitfensters von zwei Stunden. Diese Einstellung ist eine empfohlene bewährte Methode.

    -   **Zeitpunkt der Verfügbarkeit der Software**: Geben Sie die verfügbare Zeit für die Bereitstellung an, die von dieser Regel erstellt wird. Der angegebene Zeitpunkt muss mindestens eine Stunde nach der Ausführung der automatischen Bereitstellungsregel liegen. Dadurch wird sichergestellt, dass genügend Zeit zum Replizieren des Inhalts auf die Verteilungspunkte in Ihrer Hierarchie zur Verfügung steht. In einigen Definitionsupdates können auch Antischadsoftware-Engine-Updates enthalten sein, für die zum Erreichen der Verteilungspunkte mehr Zeit erforderlich sein kann.

    -   **Installationsstichtag**: Wählen Sie **So bald wie möglich** aus.

        > [!NOTE]
        >  Softwareupdatefristen sind über einen Zeitraum von zwei Stunden gefächert, um zu verhindern, dass von sämtlichen Clients zur selben Zeit ein Update angefordert wird.

18. Klicken Sie auf **Weiter**.

19. Wählen Sie im Assistenten auf der Seite **Benutzerfreundlichkeit** in der Liste **Benutzerbenachrichtigungen** die Option **In Softwarecenter und allen Benachrichtigungen ausblenden**aus.   Dadurch wird sichergestellt, dass die Definitionsupdates im Hintergrund installiert werden. Klicken Sie auf **Weiter**.

20. Auf der Seite **Warnungen** des Assistenten müssen Sie keine Warnungen konfigurieren. Endpoint Protection in Configuration Manager erstellt alle Warnungen, die erforderlich sein könnten. Klicken Sie auf **Weiter**.

21. Wählen Sie im Assistenten auf der Seite **Bereitstellungspaket** ein bestehendes Bereitstellungspaket aus, oder erstellen Sie ein neues, in dem die der Regel zugeordneten Softwareupdatedateien enthalten sein werden.

    > [!NOTE]
    >  Es kann ratsam sein, Definitionsupdates in einem Paket anzuordnen, das keine anderen Softwareupdates enthält. Dadurch wird ein kleineres Definitionsupdatepaket erreicht, das somit schneller an die Verteilungspunkte repliziert werden kann.

22. Wählen Sie bei Erstellung eines neuen Pakets auf der Seite **Verteilungspunkte** des Assistenten mindestens einen Verteilungspunkt aus, auf den die Inhalte dieses Pakets kopiert werden sollen, und klicken Sie dann auf **Weiter**.

23. Wählen Sie auf der Seite **Downloadort** des Assistenten die Option **Softwareupdates aus dem Internet herunterladen**aus, und klicken Sie dann auf **Weiter**.

24. Wählen Sie auf der Seite **Sprachauswahl** des Assistenten die gewünschten Sprachversionen der herunterzuladenden Updates aus, und klicken Sie dann auf **Weiter**.

25. Wählen Sie im Assistenten auf der Seite **Downloadeinstellungen** das erforderliche Downloadverhalten der Softwareupdates aus, und klicken Sie dann auf **Weiter**.

26. Überprüfen Sie auf der Seite **Zusammenfassung** des Assistenten die Einstellungen, und klicken Sie dann auf **Weiter**.

26. Schließen Sie den Assistenten zum Erstellen automatischer Bereitstellungsregeln ab.

27. Vergewissern Sie sich, dass die neue Regel im Knoten **Automatische Bereitstellungsregeln** der Configuration Manager-Konsole angezeigt wird.


> [!div class="button"]
> [Nächster Schritt >](endpoint-antimalware-policies.md)
> 
> [!div class="button"]
> [Zurück >](endpoint-configure-alerts.md)
