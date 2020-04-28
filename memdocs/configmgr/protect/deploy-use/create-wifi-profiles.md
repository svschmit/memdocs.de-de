---
title: Erstellen von WLAN-Profilen
titleSuffix: Configuration Manager
description: Hier erfahren Sie, wie Sie WLAN-Profile in Configuration Manager verwenden, um Einstellungen für drahtlose Netzwerke für Benutzer in Ihrer Organisation bereitzustellen.
ms.date: 01/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 321b19b2-a093-4b8f-995f-41f74b886eb5
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 21dffd1201b04846a9fffcdc7cc917465daa5905
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81690228"
---
# <a name="create-wi-fi-profiles"></a>Erstellen von WLAN-Profilen

*Gilt für: Configuration Manager (Current Branch)*

Verwenden Sie WLAN-Profile in Configuration Manager, um Einstellungen für drahtlose Netzwerke für Benutzer in Ihrer Organisation bereitzustellen. Durch die Bereitstellung dieser Einstellungen erleichtern Sie den Benutzern das Herstellen einer WLAN-Verbindung.  

Angenommen, Sie haben ein WLAN-Netzwerk eingerichtet. Nun sollen alle Windows-Notebooks eine Verbindung mit diesem Netzwerk herstellen können. Hierzu erstellen Sie ein WLAN-Profil mit den Einstellungen, die zum Herstellen einer Verbindung mit dem Drahtlosnetzwerk erforderlich sind. Stellen Sie dann das Profil für alle Benutzer in Ihrer Hierarchie bereit, die ein Windows-Notebook haben. Die Benutzer dieser Geräte sehen das Unternehmensnetzwerk in der Liste der Drahtlosnetzwerke und können leicht eine Verbindung damit herstellen.  

Sie können WLAN-Profile für die folgenden Betriebssystemversionen konfigurieren:

- Windows 8.1 (32- oder 64-Bit)

- Windows RT 8.1

- Windows 10 oder Windows 10 Mobile

Configuration Manager bietet Ihnen auch die Möglichkeit, mithilfe von lokalem MDM (Mobile Device Management; Verwaltung mobiler Geräte) Einstellungen für Drahtlosnetzwerke auf Mobilgeräten bereitzustellen. Weitere allgemeine Informationen finden Sie unter [Was ist lokales MDM?](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).

Wenn Sie ein WLAN-Profil erstellen, können Sie eine Vielzahl von Sicherheitseinstellungen einfügen. Dazu gehören Zertifikate für die Servervalidierung und die Clientauthentifizierung, die mithilfe von Configuration Manager-Zertifikatprofilen per Push übertragen wurden. Weitere Informationen zu Zertifikatprofilen finden Sie unter [Zertifikatprofile](introduction-to-certificate-profiles.md).

## <a name="create-a-wi-fi-profile"></a>Erstellen eines WLAN-Profils

1. Navigieren Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**, erweitern Sie **Konformitätseinstellungen** und dann **Zugriff auf Unternehmensressourcen**, und wählen Sie den Knoten **WLAN-Profile** aus.

1. Wählen Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** die Option **WLAN-Profil erstellen** aus.

1. Geben Sie auf der Seite **Allgemein** des Assistenten zum Erstellen von WLAN-Profilen die folgenden Informationen an:

    - **Name:** Geben Sie einen eindeutigen Namen ein, um das Profil in der Konsole zu identifizieren.

    - **Beschreibung:** Sie können eine Beschreibung eingeben, um weitere Informationen zum WLAN-Profil bereitzustellen.

    - **Vorhandenes WLAN-Profil aus einer Datei importieren**: Wählen Sie diese Option aus, um die Einstellungen eines anderen WLAN-Profils zu verwenden. Wenn Sie diese Option auswählen, werden im Assistenten nur noch zwei Seiten angezeigt: **WLAN-Profil importieren** und **Unterstützte Plattformen**.

        > [!IMPORTANT]
        > Stellen Sie sicher, dass das zu importierende WLAN-Profil gültigen XML-Code für ein WLAN-Profil enthält. Beim Importieren der Profildatei erfolgt keine Überprüfung durch Configuration Manager.

    - **Schweregrad der Nichtkonformität für Berichte**: Wählen Sie aus, welchen der folgenden Schweregrade das Gerät melden soll, wenn das WLAN-Profil als nicht konform bewertet wird. Ein Profil gilt z. B. dann als nicht konform, wenn die Installation fehlschlägt.

        - **Keine**: Von Computern, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird kein Fehlerschweregrad für Configuration Manager-Berichte gemeldet.

        - **Information**

        - **Warnung**

        - **Kritisch**

        - **Kritisch mit Ereignis**: Von Computern, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet. Geräte protokollieren außerdem den nicht konformen Zustand als Windows-Ereignis im Anwendungsereignisprotokoll.

1. Geben Sie auf der Seite **WLAN-Profil** des Assistenten die folgenden Informationen an:

    - **Netzwerkname**: Stellen Sie den Namen bereit, den Geräte als Netzwerknamen anzeigen werden.

        > [!IMPORTANT]
        > Configuration Manager unterstützt weder den Apostroph (`'`) noch das Komma (`,`) im Netzwerknamen.

    - **SSID**: Geben Sie die ID des Drahtlosnetzwerks an. Achten Sie dabei auf die Groß- und Kleinschreibung.

    - **Automatisch verbinden, wenn dieses Netzwerk in Reichweite ist**
    - **Look for other wireless network while connected to this network** (Bei hergestellter Verbindung mit diesem Netzwerk andere Funknetzwerke suchen)
    - **Auch dann verbinden, wenn der Name (SSID) des Netzwerks nicht von diesem gesendet wird**

1. Geben Sie auf der Seite **Sicherheitskonfiguration** die folgenden Informationen an:

    > [!IMPORTANT]
    > Wenn Sie für [lokales MDM](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) ein WLAN-Profil erstellen, unterstützt Current Branch von Configuration Manager nur die folgenden WLAN-Sicherheitskonfigurationen:  
    >
    > - Sicherheitstypen: **WPA2-Enterprise** oder **WPA2-Personal**  
    > - Verschlüsselungstypen: **AES** oder **TKIP**  
    > - EAP-Typen: **Smartcard- oder anderes Zertifikat** oder **PEAP**  

    - **Sicherheitstyp:** Wählen Sie das Sicherheitsprotokoll aus, das vom Drahtlosnetzwerk verwendet wird, oder wählen Sie **Keine Authentifizierung (Offen)** aus, wenn das Netzwerk nicht gesichert ist.

    - **Verschlüsselung:** Legen Sie die Verschlüsselungsmethode für das Drahtlosnetzwerk fest, wenn der Sicherheitstyp dies unterstützt.

    - **EAP-Typ**: Wählen Sie das Authentifizierungsprotokoll für die ausgewählte Verschlüsselungsmethode aus.

        > [!NOTE]
        > Nur für Windows Phone-Geräte: Die EAP-Typen **LEAP** und **EAP-FAST** werden nicht unterstützt.

        Klicken Sie auf **Konfigurieren**, um Einstellungen für den ausgewählten EAP-Typ vorzunehmen. Diese Option ist für bestimmte EAP-Typen nicht verfügbar.

        > [!IMPORTANT]
        > Das Fenster für die Konfiguration des EAP-Typs stammt aus Windows. Stellen Sie sicher, dass Sie die Configuration Manager-Konsole auf einem Computer ausführen, der den ausgewählten EAP-Typ unterstützt.

    - **Benutzeranmeldeinformationen bei jeder Anmeldung speichern**: Wählen Sie diese Option aus, um Benutzeranmeldeinformationen zu speichern. Dann müssen Benutzer nicht mehr bei jeder Anmeldung in Windows die Anmeldeinformationen für das Drahtlosnetzwerk angeben.

1. Legen Sie auf der Seite **Erweiterte Einstellungen** des Assistenten zusätzliche Einstellungen für das WLAN-Profil fest. Abhängig von den Optionen ab, die Sie auf der Seite **Sicherheitskonfiguration** des Assistenten ausgewählt haben, sind die erweiterten Einstellungen nicht oder nur eingeschränkt verfügbar. Das betrifft beispielsweise die Einstellungen für den Authentifizierungsmodus und das einmalige Anmelden.

1. Wenn in Ihrem Drahtlosnetzwerk ein Proxyserver verwendet wird, wählen Sie auf der Seite **Proxyeinstellungen** die Option  **Proxyeinstellungen für dieses WLAN-Profil konfigurieren** aus. Geben Sie dann die Konfigurationsinformationen für den Proxy an.

1. Wählen Sie auf der Seite **Unterstützte Plattformen** die Betriebssystemversionen aus, auf die dieses WLAN-Profil anwendbar ist.

1. Schließen Sie den Assistenten ab.

## <a name="next-step"></a>Nächster Schritt

> [!div class="nextstepaction"]
> [Bereitstellen von WLAN-Profilen](deploy-wifi-vpn-email-cert-profiles.md)
