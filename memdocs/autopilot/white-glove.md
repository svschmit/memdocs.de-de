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
ms.openlocfilehash: df7b4bc3cbac23024dc8d108a91defebbf6dde38
ms.sourcegitcommit: 62b451396eae660f2d5289ae3666b19ed1cc666d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88614691"
---
# <a name="windows-autopilot-for-white-glove-deployment"></a>Windows Autopilot für White-Glove-Bereitstellung

**Gilt für: Windows 10, Version 1903** 

Windows Autopilot unterstützt Organisationen bei der einfachen Bereitstellung neuer Geräte mithilfe des vorinstallierten OEM-Abbilds und der Treiber. Dadurch können Endbenutzer Ihre Geräte mit einem einfachen Prozess im geschäftlichen Bereich bereit bringen.

 ![OEM](images/wg01.png)

Windows Autopilot kann auch einen <I>weißen Hand Schuh</I> Dienst bereitstellen, der Partnern oder IT-Mitarbeitern die vorab Bereitstellung eines vollständig konfigurierten und Geschäfts bereiten Windows 10-PCs unterstützt. Aus Sicht des Endbenutzers ist die benutzergesteuerte Windows Autopilot-Darstellung unverändert, aber es ist schneller, das Gerät in einen vollständig bereitgestellten Zustand zu bringen.

Bei **Windows Autopilot für die Bereitstellung eines weißen**handlerprozesses wird der Bereitstellungs Prozess aufgeteilt. Die zeitaufwändigen Teile werden von IT, Partnern oder OEMs erledigt. Der Endbenutzer schließt einfach einige erforderliche Einstellungen und Richtlinien ein und kann dann mit der Verwendung des Geräts beginnen.

 ![OEM](images/wg02.png)

Bei White-Glove-bereit Stellungen wird Microsoft InTune in Windows 10, Version 1903 und höher, verwendet. Solche bereit Stellungen bauen auf vorhandenen Windows Autopilot [-benutzergesteuerten Szenarios](user-driven.md) auf und unterstützen Szenarios im benutzergesteuerten Modus sowohl für Azure Active Directory verbundene als auch für hybride Azure Active Directory verbundene Geräte.

## <a name="prerequisites"></a>Voraussetzungen

Zusätzlich zu den [Windows Autopilot-Anforderungen](software-requirements.md)erfordert die Bereitstellung von Windows Autopilot for White Glove auch Folgendes:

- Windows 10, Version 1903 oder höher.
- Ein InTune-Abonnement.
- Physische Geräte, die TPM 2,0 und den Geräte Nachweis unterstützen. Virtuelle Computer werden nicht unterstützt. Der Hand Schuh Bereitstellungs Prozess verwendet Windows Autopilot-Funktionen zur selbst Bereitstellung, d. h., TPM 2,0 ist erforderlich.
- Physische Geräte mit Ethernet-Konnektivität. Wi-Fi-Konnektivität wird nicht unterstützt, da eine Sprache, ein Gebiets Schema und eine Tastatur zum Herstellen der WLAN-Verbindung ausgewählt werden müssen. Wenn Sie diese Anforderung in einem vorab Bereitstellungs Prozess erzwingen, können Sie verhindern, dass der Benutzer beim Empfang des Geräts seine eigene Sprache, Ihr eigenes Gebiets Schema und seine eigene Tastatur auswählt.

>[!IMPORTANT]
>Da der OEM oder der Hersteller den weißen Hand Schuh Prozess ausführt, <u>erfordert dies keinen Zugriff auf die lokale Domänen Infrastruktur eines Endbenutzers</u>. Dies ist anders als bei einem typischen Hybrid Azure AD verknüpft, da das Neustarten des Geräts verschoben wird. Das Gerät wird vor dem Zeitpunkt, zu dem eine Verbindung mit einem Domänen Controller erwartet wird, neu versiegelt, und das Domänen Netzwerk wird kontaktiert, wenn das Gerät vom Endbenutzer lokal gekapselt wird.

## <a name="preparation"></a>Vorbereitung

Geräte, die für die Bereitstellung von weißen Handlern vorgesehen sind, werden über den normalen Registrierungsprozess für Autopilot registriert. 

Stellen Sie sicher, dass Sie bereits vorhandene Windows Autopilot-benutzergesteuerte Szenarios erfolgreich verwenden können, um Windows Autopilot für die Bereitstellung von White Glove zu testen.

- Benutzergesteuerte Azure AD Join. Stellen Sie sicher, dass Sie Geräte mit Windows Autopilot bereitstellen und Sie mit einem Azure Active Directory Mandanten verknüpfen können.
- Benutzer gesteuert mit Azure AD Hybrid Join. Stellen Sie sicher, dass Sie Geräte mit Windows Autopilot bereitstellen, Sie mit einer lokalen Active Directory Domäne verknüpfen und bei Azure Active Directory registrieren können, um die Azure AD Hybrid joinfeatures zu aktivieren.

Wenn diese Szenarien nicht vollständig ausgeführt werden können, ist die Bereitstellung von Windows Autopilot für weiß Handschuhe ebenfalls nicht erfolgreich, da Sie zusätzlich zu diesen Szenarien aufbaut.

Bevor Sie den weißen Hand Schuh Prozess in der Bereitstellung-Dienst Einrichtung starten, müssen Sie eine zusätzliche Autopilot-Profileinstellung mithilfe Ihres InTune-Kontos konfigurieren:

 ![weißen Handschuh zulassen](images/allow-white-glove-oobe.png)

Bei der vorab Bereitstellung des Windows Autopilot for White Glove Deployment werden alle Geräte orientierten Richtlinien von InTune angewendet. Dazu gehören Zertifikate, Sicherheits Vorlagen, Einstellungen, Apps und mehr – alles, was auf das Gerät abzielt. Außerdem werden alle Win32-oder Lob-apps installiert, wenn Sie diese beiden Bedingungen erfüllen:
- konfiguriert für die Installation von im Gerätekontext.
- Ziel für den Benutzer, der dem Autopilot-Gerät vorab zugewiesen ist.

Stellen Sie sicher, dass Sie nicht sowohl Win32-als auch branchenspezifische apps auf dasselbe Gerät ausrichten. 

> [!NOTE]
> Wählen Sie den Sprachmodus in Autopilot-Profilen als Benutzer aus, um den einfachen Zugriff auf den Modus für die Bereitstellung im White-Glove Mit der Technik des White Glove Technikers werden alle Geräte orientierten apps und alle benutzerorientierten und Gerätekontext-apps installiert, die auf den zugewiesenen Benutzer ausgerichtet sind. Wenn kein zugewiesener Benutzer vorhanden ist, werden nur die Geräte orientierten apps installiert. Andere benutzerorientierte Richtlinien gelten erst, wenn sich der Benutzer beim Gerät anmeldet. Stellen Sie sicher, dass Sie für Geräte und Benutzer geeignete apps und Richtlinien erstellen, um diese Verhaltensweisen zu überprüfen.

## <a name="scenarios"></a>Szenarien

Die Bereitstellung von Windows Autopilot for White Glove unterstützt zwei unterschiedliche Szenarien:
- Benutzergesteuerte bereit Stellungen mit Azure AD Join. Das Gerät wird einem Azure AD Mandanten hinzugefügt.
- Benutzergesteuerte bereit Stellungen mit Azure AD Hybrid Join. Das Gerät wird einer lokalen Active Directory Domäne hinzugefügt und separat bei Azure AD registriert.

Jedes dieser Szenarien besteht aus zwei Teilen: einem Techniker Fluss und einem Benutzer Fluss. Auf hoher Ebene sind diese Teile für Azure AD Join und Azure AD Hybrid Join identisch. Die Unterschiede werden hauptsächlich vom Endbenutzer in den Authentifizierungs Schritten erkannt.

### <a name="technician-flow"></a>Techniker Fluss

Nachdem der Kunde oder IT-Administrator alle apps und Einstellungen, die Sie für Ihre Geräte durch InTune haben möchten, als Ziel haben, kann der weiß Hand Schuh Techniker den weißen Hand Schuh Prozess beginnen. Der Techniker kann ein Mitglied der IT-Mitarbeiter, eines Dienst Partners oder eines OEM sein – jede Organisation kann entscheiden, wer diese Aktivitäten durchführen soll. Ungeachtet des Szenarios ist der vom Techniker ausgeführte Prozess derselbe:
- Starten Sie das Gerät (Ausführen von Windows 10 pro, Enterprise oder Education-SKUs, Version 1903 oder höher).
- Klicken Sie im ersten OOBE-Bildschirm (bei dem es sich um eine Sprachauswahl oder einen Gebiets Schema Auswahl-Bildschirm handeln kann) nicht auf **weiter** Drücken Sie stattdessen die Windows-Taste fünfmal, um ein weiteres Dialogfeld mit den Optionen anzuzeigen. Wählen Sie auf diesem Bildschirm die Option **Windows Autopilot Bereitstellung** aus, und klicken Sie dann auf **weiter**.

 ![choice](images/choice.png)

- Auf dem **Windows Autopilot-Konfigurations** Bildschirm werden Informationen zum Gerät angezeigt:
 - Das Autopilot-Profil, das dem Gerät zugewiesen ist.
 - Der Name der Organisation für das Gerät.
 - Der Benutzer, der dem Gerät zugewiesen ist (sofern vorhanden).
 - Ein QR-Code, der einen eindeutigen Bezeichner für das Gerät enthält. Sie können diesen Code verwenden, um das Gerät in InTune zu suchen. Dies kann beispielsweise erforderlich sein, um Konfigurationsänderungen vorzunehmen, wie z. b. das Zuweisen eines Benutzers oder das Hinzufügen des Geräts zu Gruppen, die für die APP-oder Richtlinien Ziel
 - **Hinweis**: die QR-Codes können mithilfe einer begleitenden App gescannt werden. Die APP konfiguriert außerdem das Gerät, um anzugeben, wem es angehört. Ein [Open Source-Beispiel der begleitenden App](https://github.com/Microsoft/WindowsAutopilotCompanion) , die mithilfe des Graph-API in InTune integriert wurde, wurde vom Autopilot-Team auf GitHub veröffentlicht.
- Überprüfen Sie die angezeigten Informationen. Wenn Änderungen erforderlich sind, nehmen Sie die Änderungen vor, und klicken Sie dann auf **Aktualisieren** , um die aktualisierten Autopilot-Profildetails erneut herunterzuladen.

 ![Anle](images/landing.png)

- Klicken Sie auf bereitstellen, um den **Bereitstellungs** Prozess zu starten.

Wenn der vorab Bereitstellungs Vorgang erfolgreich abgeschlossen wurde:
- Der Bildschirm grüner Status wird mit Informationen zum Gerät angezeigt, einschließlich der zuvor dargestellten Details. Beispielsweise Autopilot Profile, Organisationsname, zugewiesener Benutzer und QR-Code. Die verstrichene Zeit für die Schritte vor der Bereitstellung wird ebenfalls bereitgestellt.
 ![White-Glove-result](images/white-glove-result.png)
- Klicken Sie auf **reseal** , um das Gerät zu schließen. An diesem Punkt kann das Gerät an den Endbenutzer ausgeliefert werden.

>[!NOTE]
>Der Techniker Fluss erbt das Verhalten des [selbst Bereitstellungs Modus](self-deploying.md). In der Dokumentation für den selbst Bereitstellungs Modus wird die Seite Anmeldungs Status verwendet, um das Gerät in einen Bereitstellungs Status aufzunehmen, und es wird verhindert, dass der Benutzer nach der Registrierung auf den Desktop wechselt, aber bevor die Software und die Konfiguration angewendet werden. Wenn die Seite für den Registrierungs Status deaktiviert ist, wird die Schaltfläche reseal möglicherweise angezeigt, bevor die Software und Konfiguration abgeschlossen ist, sodass Sie mit dem Benutzer Ablauf fortfahren können, bevor die Bereitstellung des Techniker Flusses abgeschlossen ist. Der grüne Bildschirm überprüft, ob die Registrierung erfolgreich war, und nicht, dass der Techniker Flow zwangsläufig abgeschlossen ist.

Wenn der vorab Bereitstellungs Prozess fehlschlägt:
- Der Bildschirm roter Status wird mit Informationen zum Gerät angezeigt, einschließlich der zuvor dargestellten Details. Beispielsweise Autopilot Profile, Organisationsname, zugewiesener Benutzer und QR-Code. Die verstrichene Zeit für die Schritte vor der Bereitstellung wird ebenfalls bereitgestellt.
- Diagnoseprotokolle können vom Gerät gesammelt und dann zurückgesetzt werden, um den Prozess erneut zu starten.

### <a name="user-flow"></a>Benutzerflow

Wenn der vorab Bereitstellungs Vorgang erfolgreich abgeschlossen wurde und das Gerät neu versiegelt wurde, können Sie es an den Endbenutzer übermitteln. Der Endbenutzer schließt den normalen Windows Autopilot-benutzergesteuerten Prozess ab, indem er die folgenden Schritte durchführt:

- Schalten Sie das Gerät ein.
- Wählen Sie die entsprechende Sprache, das Gebiets Schema und das Tastaturlayout aus.
- Stellen Sie eine Verbindung mit einem Netzwerk her (bei Verwendung von Wi-Fi). Der Internet Zugang ist immer erforderlich. Wenn Sie Azure AD Hybrid Join verwenden, müssen Sie auch eine Verbindung mit einem Domänen Controller herstellen.
- Geben Sie auf dem Bildschirm Branding-Anmeldung die Anmelde Informationen des Benutzers Azure Active Directory ein.
- Wenn Sie Azure AD Hybrid Join verwenden, wird das Gerät neu gestartet. Geben Sie nach dem Neustart die Active Directory Anmelde Informationen des Benutzers ein.
- Weitere Richtlinien und apps werden an das Gerät übermittelt, wie von der Seite zum Registrierungs Status (ESP) nachverfolgt. Sobald der Benutzer fertig ist, kann er auf den Desktop zugreifen.

## <a name="related-topics"></a>Zugehörige Themen

[Whiteglove-Video](https://youtu.be/nE5XSOBV0rI)
