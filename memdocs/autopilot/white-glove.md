---
title: Windows Autopilot für White-Glove-Bereitstellung
description: Windows Autopilot für White-Glove-Bereitstellung
keywords: MDM, Setup, Windows, Windows 10, OOBE, Manage, Bereitstellung, Autopilot, ZTD, Zero-Touchscreen, Partner, msfb, InTune, vorab Bereitstellung
ms.prod: w10
ms.mktglfcycl: deploy
ms.localizationpriority: low
ms.sitesec: library
ms.pagetype: deploy
audience: itproF
manager: laurawi
ms.audience: itpro
author: greg-lindsay
ms.collection: M365-modern-desktop
ms.topic: article
ms.openlocfilehash: e08c69412fef2149d71c684fed6b900b88c9cb60
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/04/2020
ms.locfileid: "87756518"
---
# <a name="windows-autopilot-for-white-glove-deployment"></a>Windows Autopilot für White-Glove-Bereitstellung

**Gilt für: Windows 10, Version 1903** 

Mit Windows Autopilot können Organisationen problemlos neue Geräte bereitstellen, indem Sie das vorinstallierte OEM-Abbild und Treiber mit einem einfachen Prozess nutzen, der vom Endbenutzer ausgeführt werden kann, um das Gerät im Unternehmen bereitzustellen.

 ![OEM](images/wg01.png)

Windows Autopilot kann auch einen <I>weißen Hand Schuh</I> Dienst bereitstellen, der es Partnern oder IT-Mitarbeitern ermöglicht, eine vorab Bereitstellung eines Windows 10-PCs durchzusetzen, sodass er vollständig konfiguriert und betriebsbereit ist. Aus Sicht des Endbenutzers ist die benutzergesteuerte Windows Autopilot-Darstellung unverändert, aber es ist schneller, das Gerät in einen vollständig bereitgestellten Zustand zu bringen.

Bei **Windows Autopilot für die Bereitstellung eines weißen**handlerprozesses wird der Bereitstellungs Prozess aufgeteilt. Die zeitaufwändigen Teile werden von IT, Partnern oder OEMs durchgeführt. Der Endbenutzer schließt einfach einige erforderliche Einstellungen und Richtlinien ein und kann dann mit der Verwendung des Geräts beginnen.

 ![OEM](images/wg02.png)

Aktiviert mit Microsoft InTune in Windows 10, Version 1903 und höher, baut die Bereitstellungs Funktionen von White Glove auf vorhandenen Windows Autopilot [-benutzergesteuerten Szenarien](user-driven.md)auf und unterstützen sowohl den benutzergesteuerten Modus für Azure Active Directory Join als auch den benutzergesteuerten Modus für Hybrid Azure Active Directory joinszenarien.

## <a name="prerequisites"></a>Voraussetzungen

Zusätzlich zu den [Windows Autopilot-Anforderungen](windows-autopilot-requirements.md)fügt Windows Autopilot for White Glove Deployment Folgendes hinzu:

- Windows 10, Version 1903 oder höher, ist erforderlich.
- Ein InTune-Abonnement.
- Physische Geräte, die TPM 2,0 und den Geräte Nachweis unterstützen; virtuelle Computer werden nicht unterstützt.  Der Hand Schuh Bereitstellungs Prozess nutzt die Self-Bereitstellung-Funktionen von Windows Autopilot, sodass die TPM 2,0-Anforderungen erfüllt werden.
- Physische Geräte mit Ethernet-Konnektivität; Wi-Fi-Konnektivität wird nicht unterstützt, weil eine Sprache, ein Gebiets Schema und eine Tastatur zum Herstellen der WLAN-Verbindung ausgewählt werden müssen. Wenn Sie dies in einem vorab Bereitstellungs Prozess durchgeführt haben, können Sie verhindern, dass der Benutzer seine eigene Sprache, Ihr eigenes Gebiets Schema und seine Tastatur beim Empfang des Geräts auswählt.

>[!IMPORTANT]
>Da der OEM oder der Hersteller den weißen Hand Schuh Prozess ausführt, <u>erfordert dies keinen Zugriff auf die lokale Domänen Infrastruktur eines Endbenutzers</u>. Dies ist anders als bei einem typischen Hybrid Azure AD verknüpft, da das Neustarten des Geräts verschoben wird. Das Gerät wird vor dem Zeitpunkt, zu dem eine Verbindung mit einem Domänen Controller erwartet wird, erneut versiegelt, und das Domänen Netzwerk wird kontaktiert, wenn das Gerät vom Endbenutzer lokal geunboxing ist.

## <a name="preparation"></a>Vorbereitung

Geräte, die für die Bereitstellung von weißen Handlern vorgesehen sind, werden über den normalen Registrierungsprozess für Autopilot registriert. 

Um Windows Autopilot für die Bereitstellung von White Glove zu testen, stellen Sie sicher, dass Sie bereits vorhandene Windows Autopilot-benutzergesteuerte Szenarios erfolgreich verwenden können:

- Benutzergesteuerte Azure AD Join.  Geräte können mithilfe von Windows Autopilot bereitgestellt und mit einem Azure Active Directory Mandanten verknüpft werden.
- Benutzer gesteuert mit Azure AD Hybrid Join.  Geräte können mithilfe von Windows Autopilot bereitgestellt und mit einer lokalen Active Directory Domäne verknüpft und dann bei Azure Active Directory registriert werden, um die Azure AD Hybrid joinfeatures zu aktivieren.

Wenn diese Szenarios nicht vollständig ausgeführt werden können, ist die Bereitstellung von Windows Autopilot für weiß Handschuhe ebenfalls nicht erfolgreich, da Sie zusätzlich zu diesen Szenarien aufbaut.

Um die Bereitstellung von White Glove zu aktivieren, muss der Kunde oder der IT-Administrator über sein InTune-Konto eine zusätzliche Autopilot-Profileinstellung konfigurieren, bevor der weiße Hand Schuh Prozess in der Bereitstellung-Dienst Einrichtung beginnt:

 ![weißen Handschuh zulassen](images/allow-white-glove-oobe.png)

Bei der vorab Bereitstellung des Windows Autopilot for White Glove Deployment werden alle Geräte orientierten Richtlinien von InTune angewendet.  Dazu gehören Zertifikate, Sicherheits Vorlagen, Einstellungen, Apps und mehr – alles, was auf das Gerät abzielt.  Außerdem werden alle apps (Win32 oder Lob), die für die Installation im Gerätekontext konfiguriert sind und auf den Benutzer abzielen, der dem Autopilot-Gerät vorab zugewiesen wurde, ebenfalls installiert. Stellen Sie sicher, dass Sie nicht sowohl Win32-als auch branchenspezifische apps auf dasselbe Gerät ausrichten. 

> [!NOTE]
> Wählen Sie den Sprachmodus in Autopilot-Profilen als Benutzer aus, um den einfachen Zugriff auf den Modus für die Bereitstellung im White-Glove In der Technik des White-Turn-Technikers werden alle Geräte orientierten apps sowie alle benutzerorientierten und Gerätekontext-apps installiert, die für den zugewiesenen Benutzer vorgesehen sind. Wenn kein zugewiesener Benutzer vorhanden ist, werden nur die Geräte orientierten apps installiert. Andere benutzerorientierte Richtlinien gelten erst, wenn sich der Benutzer beim Gerät anmeldet. Stellen Sie sicher, dass Sie für Geräte und Benutzer geeignete apps und Richtlinien erstellen, um diese Verhaltensweisen zu überprüfen.

## <a name="scenarios"></a>Szenarien

Die Bereitstellung von Windows Autopilot for White Glove unterstützt zwei unterschiedliche Szenarien:
- Benutzergesteuerte bereit Stellungen mit Azure AD Join.  Das Gerät wird einem Azure AD Mandanten hinzugefügt.
- Benutzergesteuerte bereit Stellungen mit Azure AD Hybrid Join.  Das Gerät wird einer lokalen Active Directory Domäne hinzugefügt und separat bei Azure AD registriert.
Jedes dieser Szenarien besteht aus zwei Teilen: einem Techniker Fluss und einem Benutzer Fluss.  Auf hoher Ebene sind diese Teile für Azure AD Join und Azure AD Hybrid Join identisch. Unterschiede werden hauptsächlich vom Endbenutzer in den Authentifizierungs Schritten erkannt.

### <a name="technician-flow"></a>Techniker Fluss

Nachdem der Kunde oder IT-Administrator alle apps und Einstellungen, die Sie für Ihre Geräte durch InTune haben möchten, als Ziel haben, kann der weiß Hand Schuh Techniker den weißen Hand Schuh Prozess beginnen.  Der Techniker kann ein Mitglied der IT-Mitarbeiter, eines Dienst Partners oder eines OEM sein – jede Organisation kann entscheiden, wer diese Aktivitäten durchführen soll. Unabhängig vom Szenario ist der Prozess, der vom Techniker ausgeführt werden soll, identisch:
- Starten Sie das Gerät (Ausführen von Windows 10 pro, Enterprise oder Education-SKUs, Version 1903 oder höher).
- Klicken Sie im ersten OOBE-Bildschirm (bei dem es sich um eine Sprachauswahl oder einen Gebiets Schema Auswahl-Bildschirm handeln kann) nicht auf **weiter**.  Drücken Sie stattdessen die Windows-Taste fünfmal, um ein weiteres Dialogfeld mit den Optionen anzuzeigen.  Wählen Sie auf diesem Bildschirm die Option **Windows Autopilot Bereitstellung** aus, und klicken Sie dann auf **weiter**.

  ![choice](images/choice.png)

- Auf dem **Windows Autopilot-Konfigurations** Bildschirm werden Informationen zum Gerät angezeigt:
    - Das Autopilot-Profil, das dem Gerät zugewiesen ist.
    - Der Name der Organisation für das Gerät.
    - Der Benutzer, der dem Gerät zugewiesen ist (sofern vorhanden).
    - Ein QR-Code, der einen eindeutigen Bezeichner für das Gerät enthält, der nützlich ist, um das Gerät in InTune zu suchen und Änderungen an der Konfiguration vorzunehmen (z. b. das Zuweisen eines Benutzers, das Hinzufügen des Geräts zu weiteren Gruppen, die für die APP-oder Richtlinien Zuweisung erforderlich sind
    - **Hinweis**: die QR-Codes können mithilfe einer begleitenden App gescannt werden, die auch das Gerät so konfiguriert, dass es angibt, wem es angehört.  Ein [Open Source-Beispiel der begleitenden App](https://github.com/Microsoft/WindowsAutopilotCompanion) , das über die Graph-API in InTune integriert wurde, wurde vom Autopilot-Team auf GitHub veröffentlicht.
- Überprüfen Sie die angezeigten Informationen.  Wenn Änderungen erforderlich sind, führen Sie diese aus, und klicken Sie dann auf **Aktualisieren** , um die aktualisierten Autopilot-Profildetails erneut herunterzuladen.

  ![Anle](images/landing.png)

- Klicken Sie auf bereitstellen, um den **Bereitstellungs** Prozess zu starten.

Wenn der vorab Bereitstellungs Vorgang erfolgreich abgeschlossen wurde:
- Ein grüner Statusbildschirm wird mit Informationen zum Gerät angezeigt, einschließlich der zuvor dargestellten Details (z. b. Autopilot Profile, Organisationsname, zugewiesener Benutzer, QR-Code) sowie der verstrichenen Zeit für die Schritte vor der Bereitstellung.
 ![White-Glove-result](images/white-glove-result.png)
- Klicken Sie auf **reseal** , um das Gerät zu schließen.  An diesem Punkt kann das Gerät an den Endbenutzer ausgeliefert werden.

>[!NOTE]
>Der Techniker Fluss erbt das Verhalten des [selbst Bereitstellungs Modus](self-deploying.md). In der Dokumentation für den selbst Bereitstellungs Modus wird die Seite Anmeldungs Status genutzt, um das Gerät in einen Bereitstellungs Status aufzunehmen, und es wird verhindert, dass der Benutzer nach der Registrierung auf den Desktop wechselt, aber bevor die Software und die Konfiguration angewendet werden. Wenn die Seite für den Registrierungs Status deaktiviert ist, wird die Schaltfläche reseal möglicherweise angezeigt, bevor die Software und Konfiguration abgeschlossen ist, sodass Sie mit dem Benutzer Ablauf fortfahren können, bevor die Bereitstellung des Techniker Flusses abgeschlossen ist. Der grüne Bildschirm überprüft, ob die Registrierung erfolgreich war, und nicht, dass der Techniker Flow zwangsläufig abgeschlossen ist.

Wenn der vorab Bereitstellungs Prozess fehlschlägt:
- Ein roter Statusbildschirm wird mit Informationen zum Gerät angezeigt, einschließlich der zuvor dargestellten Details (z. b. Autopilot Profile, Organisationsname, zugewiesener Benutzer, QR-Code) sowie der verstrichenen Zeit für die Schritte vor der Bereitstellung.
- Diagnoseprotokolle können vom Gerät gesammelt und dann zurückgesetzt werden, um den Prozess erneut zu starten.

### <a name="user-flow"></a>Benutzerflow

Wenn der Prozess vor der Bereitstellung erfolgreich abgeschlossen wurde und das Gerät erneut versiegelt wurde, kann er an den Endbenutzer übermittelt werden, um den normalen Windows Autopilot-benutzergesteuerten Prozess abzuschließen.  Sie führen einen Standardsatz von Schritten aus:

- Schalten Sie das Gerät ein.
- Wählen Sie die entsprechende Sprache, das Gebiets Schema und das Tastaturlayout aus.
- Stellen Sie eine Verbindung mit einem Netzwerk her (bei Verwendung von Wi-Fi).  Der Internet Zugang ist immer erforderlich.  Wenn Sie Azure AD Hybrid Join verwenden, müssen Sie auch eine Verbindung mit einem Domänen Controller herstellen.
- Geben Sie auf dem Bildschirm Branding-Anmeldung die Anmelde Informationen des Benutzers Azure Active Directory ein.
- Wenn Sie Azure AD Hybrid Join verwenden, wird das Gerät neu gestartet. Geben Sie nach dem Neustart die Active Directory Anmelde Informationen des Benutzers ein.
- Weitere Richtlinien und apps werden an das Gerät übermittelt, wie von der Seite zum Registrierungs Status (ESP) nachverfolgt.  Sobald der Benutzer fertig ist, kann er auf den Desktop zugreifen.

## <a name="related-topics"></a>Zugehörige Themen

[Whiteglove-Video](https://youtu.be/nE5XSOBV0rI)
