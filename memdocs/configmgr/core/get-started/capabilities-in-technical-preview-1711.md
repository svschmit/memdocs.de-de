---
title: Technical Preview 1711 | Microsoft-Dokumentation
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über Features, die in der Technical Preview-Version 1711 für Configuration Manager zur Verfügung stehen.
ms.date: 11/17/2017
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 2e68dc12-6776-437a-9138-45cd7d4bf9cf
author: aczechowski
ms.author: aaroncz
manager: dougeby
ROBOTS: NOINDEX
ms.openlocfilehash: e6f8ed1562392899b46a082bf8f64872c7e1b67d
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81705098"
---
# <a name="capabilities-in-technical-preview-1711-for-configuration-manager"></a>Funktionen in der Technical Preview 1711 für Configuration Manager

*Gilt für: Configuration Manager (Technical Preview-Branch)*

In diesem Artikel werden die Features vorgestellt, die in der Technical Preview-Version 1711 für Configuration Manager verfügbar sind. Sie können diese Version installieren, um neue Funktionen für Ihren Configuration Manager Technical Preview-Standort zu aktualisieren oder hinzuzufügen. Bevor Sie diese Technical Preview-Version installieren, lesen Sie [Technical Preview für Configuration Manager](../../core/get-started/technical-preview.md), um sich mit den allgemeinen Anforderungen und Einschränkungen bei der Verwendung einer Technical Preview-Version vertraut zu machen und zu erfahren, wie Sie Updates für Versionen durchführen und Feedback zu den Funktionen in einer Technical Preview-Version geben können.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Bekannte Probleme in dieser Technical Preview:**
- **Unterstützung für Windows 10-Version 1709 (auch Fall Creators Update genannt)** .  Ab diesem Windows-Release umfassen Windows-Medien mehrere Editionen. Achten Sie beim Konfigurieren einer Tasksequenz für ein Betriebssystem-Upgradepaket oder ein Betriebssystemimage darauf, eine [Edition auszuwählen, die für Configuration Manager unterstützt wird](../plan-design/configs/support-for-windows-10.md#windows-10-as-a-client).
- **Beim Update auf die Vorschauversion tritt ein Fehler auf, wenn Sie einen Standortserver im passiven Modus haben**. Wenn Sie eine Vorschauversion ausführen, die über einen [primären Standortserver im passiven Modus](capabilities-in-technical-preview-1706.md#site-server-role-high-availability) verfügt, müssen Sie den Standortserver im passiven Modus deinstallieren, bevor Sie Ihren Vorschaustandort auf diese neue Vorschauversion aktualisieren können. Sie können den Standortserver im passiven Modus erneut installieren, wenn das Update an Ihrem Standort abgeschlossen wurde.

  So deinstallieren Sie den Standortserver im passiven Modus:
  1. Navigieren Sie in der Konsole zu **Administration** > **Übersicht** > **Standortkonfiguration** > **Server und Standortsystemrollen**, und wählen Sie den Standortserver im passiven Modus aus.
  2. Klicken Sie im Bereich **Standortsystemrollen** mit der rechten Maustaste auf die Rolle **Standortserver**, und wählen Sie dann **Rolle entfernen**.
  3. Klicken Sie mit der rechten Maustaste auf den Standortserver im passiven Modus, und wählen Sie dann **Löschen**.
  4. Starten Sie nach dem Deinstallieren des Standortservers auf dem aktiven primären Standortserver den Dienst **CONFIGURATION_MANAGER_UPDATE** neu.

**Im Folgenden werden neue Features aufgelistet, die Sie mit dieser Version ausprobieren können.**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## <a name="improvements-to-run-task-sequence"></a>Verbesserungen bei „Tasksequenz ausführen“
<!-- 1261338 -->

In dieser Technical Preview-Version wird der Schritt „Tasksequenz ausführen“ verbessert. Diese Verbesserungen umfassen Folgendes:

- Unterstützung für alle Szenarien der Betriebssystembereitstellung mithilfe von Softwarecenter, PXE und Medien.
- Verbesserungen bei Konsolenaktionen wie Kopieren, Importieren, Exportieren und Warnung beim Löschen von Objekten.
- Unterstützung für den Assistenten **Vorabbereitstellen von Inhalt**.
- Integration in die Überprüfung der Bereitstellung.
- Der Schritt "Tasksequenz ausführen" kann nun über mehrere Ebenen von Tasksequenzen hinweg verwendet werden, nicht nur für eine einzelne Beziehung zwischen über- und untergeordneten Elementen. Bei Beziehungen mit mehreren Ebenen erhöht sich die Komplexität, daher ist Vorsicht geboten. Diese Beziehungen werden nach wie vor auf Zirkelbezüge geprüft.

### <a name="try-it-out"></a>Probieren Sie es aus!  

Versuchen Sie, die folgenden Aufgaben auszuführen, und senden Sie uns dann **Feedback** über die Registerkarte **Start** des Menübands, um uns zu wissen zu lassen, wie es funktioniert hat:

1. Klicken Sie im Tasksequenz-Editor auf **Hinzufügen**, wählen Sie **Allgemein** aus, und klicken Sie auf **Tasksequenz ausführen**.
2. Klicken Sie auf **Durchsuchen**, um die untergeordnete Tasksequenz auszuwählen.

## <a name="allow-user-interaction-when-installing-an-application----1356976---"></a>Ermöglichen der Benutzerinteraktion beim Installieren einer Anwendung <!-- 1356976 -->

In dieser Vorschauversion können Sie einem Endbenutzer erlauben, während der Ausführung der Tasksequenz mit einer Anwendungsinstallation zu interagieren. Führen Sie beispielsweise einen Setupvorgang aus, der den Endbenutzer nach verschiedenen Optionen befragt. Einige Anwendungsinstallationsprogramme können Eingabeaufforderungen an Benutzer nicht deaktivieren, oder der Installationsprozess fordert bestimmte Konfigurationswerte an, die nur dem Benutzer bekannt sind. Mithilfe dieser Funktion behalten Sie diese Installationsszenarien im Griff.

### <a name="try-it-out"></a>Probieren Sie es aus!

Versuchen Sie, die folgenden Aufgaben auszuführen, und senden Sie uns dann **Feedback** über die Registerkarte **Start** des Menübands, um uns zu wissen zu lassen, wie es funktioniert hat:

1.  Erstellen oder bearbeiten Sie eine Anwendung. Weitere Informationen finden Sie unter [Erstellen von Anwendungen mit Configuration Manager](../../apps/deploy-use/create-applications.md).

    a. Wählen Sie in **Eigenschaften von Windows Installer (\*MSI-Datei)** die Registerkarte **Benutzeroberfläche** aus.

    b. Wählen Sie **Für System installieren** für **Installationsverhalten** aus.

    c. Wählen Sie **Unabhängig von Benutzeranmeldung** für **Anmeldeanforderung** aus.

    d. Wählen Sie **Normal** für **Sichtbarkeit des Installationsprogramms**. Folgende drei Optionen stehen Ihnen zur Auswahl: **Minimiert**, **Normal** und **Maximiert**.

    e. Aktivieren Sie das Kontrollkästchen **Benutzern gestatten, die Programminstallation anzuzeigen und mit ihr zu interagieren**.

2.  Erstellen oder bearbeiten Sie eine Tasksequenz, um die Anwendung mit dem Schritt **Anwendung installieren** zu installieren. Weitere Informationen finden Sie unter [Tasksequenzschritte](../../osd/understand/task-sequence-steps.md) im Abschnitt [Anwendung installieren](../../osd/understand/task-sequence-steps.md#BKMK_InstallApplication).

    a. Tasksequenz „Imageerstellung“ nach dem Schritt „Windows und Configuration Manager einrichten“.

    b. Tasksequenz „Direktes Upgrade“ in der Gruppe „Nachbearbeitungsgrupp“.

3.  Stellen Sie die Tasksequenz auf einem Client bereit.
4.  Installieren Sie die Tasksequenz über das Softwarecenter.

Im Verlauf der Tasksequenz wird die Oberfläche zur Anwendungsinstallation auf dem Zielgerät des Endbenutzers angezeigt. Die Tasksequenz wird angehalten, bis der Endbenutzer den Workflow zur Installation der Anwendung abgeschlossen hat.

### <a name="install-using-the-wizard"></a>Installieren mithilfe des Assistenten

Sie können diese Funktion auch verwenden, wenn Sie eine Anwendung mithilfe des Assistenten bereitstellen.

1. Erstellen oder bearbeiten Sie eine Anwendung.
2. Stellen Sie die Anwendung einem Client bereit.
3. Installieren Sie die Anwendung über das Softwarecenter. Die Oberfläche für die Installation der Anwendung sollte angezeigt werden. Wenn der Endbenutzer dem Installations-Assistenten der Anwendung folgt, wird die Anwendung erfolgreich installiert.




<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## <a name="next-steps"></a>Nächste Schritte
Informationen zur Installation oder zum Update des Technical Preview-Branch finden Sie unter [Technical Preview für Configuration Manager](technical-preview.md).    
