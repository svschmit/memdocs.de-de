---
title: Massenregistrierung von Geräten
titleSuffix: Configuration Manager
description: Massen Registrierung von Geräten mit der lokalen Verwaltung mobiler Geräte (Mobile Device Management, MDM) in Configuration Manager
ms.date: 01/13/2020
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.assetid: b36f5e4a-2b57-4d18-83f6-197081ac2a0a
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 474d59ec22d1edaf8e662298e90555e6772d302b
ms.sourcegitcommit: 99084d70c032c4db109328a4ca100cd3f5759433
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/20/2020
ms.locfileid: "88698795"
---
# <a name="how-to-bulk-enroll-devices-with-on-premises-mdm-in-configuration-manager"></a>Massen Registrierung von Geräten mit lokalem MDM in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Die Massen Registrierung in Configuration Manager lokale Verwaltung mobiler Geräte (Mobile Device Management, MDM) ist eine automatisierte Methode zum Registrieren von Geräten. Bei der anderen Methode handelt es sich um die Benutzerregistrierung, bei der Benutzer ihre Anmelde Informationen eingeben müssen, um das Gerät zu registrieren. Bei der Massenregistrierung wird ein Registrierungspaket zur Authentifizierung des Geräts während der Anmeldung verwendet. Das Paket ist eine ppkg-Datei, die auch Zertifikat-und WLAN-Profile enthalten kann, um die Registrierung zu unterstützen.

## <a name="create-a-certificate-profile"></a><a name="bkmk_createCert"></a> Erstellen eines Zertifikatprofils

Fügen Sie ein Zertifikat Profil ein, um automatisch ein vertrauenswürdiges Stamm Zertifikat auf dem Gerät zu installieren. Dieses Stamm Zertifikat ist für die vertrauenswürdige Kommunikation zwischen den Geräten und den Standortsystem Rollen erforderlich, die für die lokale Verwaltung mobiler Geräte erforderlich sind.

Wenn Sie den Standort für das lokale MDM vorbereiten, exportieren Sie das vertrauenswürdige Stamm Zertifikat. Verwenden Sie dieses Zertifikat im Zertifikat Profil des Registrierungs Pakets. Weitere Informationen zum erhalten des vertrauenswürdigen Stamm Zertifikats finden Sie unter [Exportieren des vertrauenswürdigen Stamm Zertifikats](../get-started/set-up-certificates-on-premises-mdm.md#bkmk_exportCert).

Verwenden Sie das exportierte Zertifikat, um ein Zertifikat Profil zu erstellen. Weitere Informationen finden Sie unter [Erstellen von Zertifikat Profilen](../../protect/deploy-use/create-certificate-profiles.md).

## <a name="create-a-wi-fi-profile"></a><a name="CreateWifi"></a> Erstellen eines WLAN-Profils

Eine andere Komponente des Massen Registrierungs Pakets ist ein WLAN-Profil. Dieses Profil kann sicherstellen, dass das Gerät über die Netzwerk Konnektivität verfügt, um die Registrierung zu unterstützen.

Weitere Informationen zum Erstellen eines WLAN-Profils in Configuration Manager finden Sie unter [Erstellen von WLAN-Profilen](../../protect/deploy-use/create-wifi-profiles.md).

### <a name="wi-fi-profile-limitations"></a>Einschränkungen für das WLAN-Profil

Wenn Sie ein WLAN-Profil für die lokale MDM-Massen Registrierung erstellen, überprüfen Sie die folgenden Einschränkungen.

#### <a name="wi-fi-security-configurations-for-on-premises-mdm"></a>Wi-Fi-Sicherheits Konfigurationen für lokales MDM

Der Current Branch von Configuration Manager unterstützt nur die folgenden WLAN-Sicherheits Konfigurationen für lokales MDM:

- Sicherheitstypen: **WPA2-Enterprise** oder **WPA2-Personal**

- Verschlüsselungstypen: **AES** oder **TKIP**

- EAP-Typen: **Smartcard- oder anderes Zertifikat** oder **PEAP**

#### <a name="proxy-server"></a>Proxyserver

Obwohl Configuration Manager über eine Einstellung für Proxy Server Informationen im WLAN-Profil verfügt, wird der Proxy beim Registrieren des Geräts nicht konfiguriert. Wenn Sie einen Proxy Server für Massen registrierte Geräte einrichten müssen:

- Stellen Sie die Einstellungen mithilfe von Konfigurationselementen bereit, sobald die Geräte registriert sind.

- Erstellen Sie mit dem Windows-Image und Configuration Designer (ICD) ein zweites Paket, und stellen Sie es zusammen mit dem Massen Registrierungspaket bereit.

## <a name="create-an-enrollment-profile"></a><a name="bkmk_createEnroll"></a> Erstellen eines Anmeldungsprofils

Das Registrierungs Profil ermöglicht Ihnen, Einstellungen anzugeben, die für die Geräteregistrierung erforderlich sind. Diese Einstellungen umfassen ein [Zertifikat Profil](#bkmk_createCert) und ein [WLAN-Profil](#CreateWifi).

1. Wechseln Sie in der Configuration Manager Konsole zum Arbeitsbereich bestand **und** Kompatibilität, erweitern Sie **alle unternehmenseigenen Geräte**, erweitern Sie **Windows**, und wählen Sie dann den Knoten Registrierungs **profile** aus.

1. Wählen Sie im Menüband die Option Registrierungs **Profil erstellen**aus.

1. Geben Sie auf der Seite **Allgemein** des Assistenten zum Erstellen von anmeldungsprofilen die folgenden Informationen an:

    - **Name**: ein eindeutiger Name zum Identifizieren des Profils.

    - **Beschreibung**: ein optionales Feld zur weiteren Beschreibung des Profils

    - **Verwaltungs Autorität**: nur **lokale** auswählen

1. Wählen Sie auf der Seite **Standort Zuweisung** den **Verwaltungsstandort Code** mit einem Geräte Verwaltungspunkt aus.

1. Wählen Sie auf der Seite anmeldungsproxypunkt **auswählen** die Option **nur Intranet**aus, und wählen Sie dann einen oder mehrere anmeldungsproxypunkte aus. Das Gerät verwendet diese Server, um den Registrierungsprozess zu starten.

1. Wählen Sie auf der Seite **vertrauenswürdiges Stamm Zertifikat auswählen** das Zertifikat Profil aus, das das vertrauenswürdige Stamm Zertifikat enthält.

1. Wählen Sie auf der Seite **WLAN-Profile** das WLAN-Profil aus, das die erforderlichen Netzwerkeinstellungen für Geräte zum Herstellen einer Verbindung enthält.

    > [!TIP]
    > Wenn Sie für Ihr Registrierungspaket kein WLAN-Profil verwenden, überspringen Sie diesen Schritt.

1. Schließen Sie den Assistenten ab.

## <a name="create-an-enrollment-package"></a><a name="bkmk_createPpkg"></a> Erstellen eines Registrierungs Pakets

Das Registrierungspaket (ppkg) ist die Datei, die Sie für die Massen Registrierung von Geräten für die lokale Verwaltung mobiler Geräte (MDM) verwenden. Erstellen Sie diese Datei mit Configuration Manager. Obwohl Sie mit Windows-ICD ähnliche Typen von Paketen erstellen können, können nur Pakete, die Sie in Configuration Manager erstellen, zum Registrieren von Geräten für die lokale Verwaltung mobiler Geräte verwendet werden. Ein Paket, das Sie mit Windows-ICD erstellen, kann nur den für die Registrierung erforderlichen Benutzer Prinzipal Namen (User Principal Name, UPN) bereitstellen. der tatsächliche Registrierungsvorgang kann nicht gestartet werden.

Zum Erstellen des Registrierungspakets muss das Windows Assessment and Deployment Toolkit (ADK) für Windows 10 verwendet werden. Installieren Sie auf dem Computer, auf dem die Configuration Manager-Konsole ausgeführt wird, die neueste Version von Windows ADK. Wählen Sie das Feature **Imaging and Configuration Designer (ICD)** und alle Abhängigkeiten aus. (Diese Version muss nicht mit der Version identisch sein, die von der Configuration Manager Site für die Betriebssystem Bereitstellung verwendet wird.) Weitere Informationen finden Sie unter [herunterladen des Windows ADK für Windows 10](/windows-hardware/get-started/adk-install).

1. Wechseln Sie in der Configuration Manager Konsole zum Arbeitsbereich bestand **und** Kompatibilität, erweitern Sie **alle unternehmenseigenen Geräte**, erweitern Sie **Windows**, und wählen Sie dann den Knoten Registrierungs **profile** aus.

1. Wählen Sie ein vorhandenes Registrierungs Profil aus. Wählen Sie im Menüband die Option **exportieren**aus.

1. Geben Sie im Fenster Registrierungspaket exportieren die folgenden Informationen an:

    - **Gültigkeitsdauer (Tage)**: Standardmäßig legt Configuration Manager fest, dass das Registrierungspaket in zwei Wochen (14 Tage) abläuft. Sie können das Paket nicht für die Geräteregistrierung verwenden, nachdem die Gültigkeitsdauer abgelaufen ist. Geben Sie eine ganze Zahl zwischen 1 und 30 ein.

    - **Paketdatei**: Geben Sie einen lokalen Pfad oder einen Netzwerk Dateipfad und-Namen für die ppkg-Datei an.

    - **Paket verschlüsseln**: Aktivieren Sie diese Option, um das Paket mit einem Kennwort zu schützen. Nachdem Sie das Paket exportiert haben, wird in Configuration Manager das generierte Kennwort angezeigt. Kopieren Sie das Kennwort, und speichern Sie es an einem sicheren Ort. Das exportierte Registrierungspaket kann ohne das Kennwort nicht verwendet werden.

        > [!IMPORTANT]
        > Configuration Manager speichert das Kennwort nicht, und Sie können es nicht anpassen oder ändern. Wenn Sie das Fenster schließen, in dem das Kennwort angezeigt wird, gibt es keine Möglichkeit, das Kennwort abzurufen.

1. Wählen Sie **Exportieren** aus. Configuration Manager verwendet das Windows ADK, um das Registrierungspaket zu erstellen.

Configuration Manager nachverfolgt gültige Registrierungs Pakete. Erweitern Sie in der-Konsole den Knoten Registrierungs **Profil** , und klicken Sie auf **exportierte Pakete**.

> [!TIP]
> Wenn Sie ein Registrierungspaket aus der Configuration Manager Konsole entfernen, können Sie es nicht zum Registrieren von Geräten verwenden. Verwenden Sie diese Methode, um Registrierungs Pakete zu verwalten, die nicht von anderen für die Massen Registrierung verwendet werden sollen.

## <a name="bulk-enroll-a-device"></a><a name="bkmk_getPpkg"></a> Massen Registrierung eines Geräts

Sie können ein Paket verwenden, um Geräte vor oder nach dem Out-of-Box-Erfahrungsprozess (OOBE) des Geräts zu registrieren. Das Registrierungspaket kann auch als Teil eines OEM-Bereitstellungs Pakets (Original Equipment Manufacturer) enthalten sein.

Um das Paket für die Massen Registrierung verwenden zu können, müssen Sie es physisch an das Gerät übermitteln. Abhängig von Ihren Anforderungen gibt es verschiedene Methoden, z. b.:

- Kopieren aus dem Dateisystem

- An eine e-Mail anfügen

- Kopieren über eine NFC-Verbindung (Near Field Communication)

- Kopieren von einer Speicherkarte

- Scannen eines Barcodes

- Durch Kopieren von einem verbundenen Gerät

- In ein OEM-Bereitstellungs Paket einschließen

### <a name="enroll-a-device-with-bulk-enrollment-package"></a>Registrieren eines Geräts mit einem Massen Registrierungspaket

1. Öffnen Sie auf einem Gerät die ppkg-Datei. Führen Sie bei Bedarf als Administrator aus.

1. Windows fragt, ob das Paket aus einer vertrauenswürdigen Quelle ist. Wählen Sie **Ja**aus.

Der Registrierungsvorgang wird gestartet.

## <a name="verify-enrollment"></a><a name="bkmk_verifyEnroll"></a> Überprüfen der Registrierung

### <a name="verify-bulk-enrollment-on-the-device"></a>Überprüfen der Massen Registrierung auf dem Gerät

1. Öffnen Sie auf dem Gerät die **Einstellungen**.

1. Wählen Sie Konten aus, und klicken Sie auf **Arbeits-oder Schul** **Konto**. Wenn die Registrierung erfolgreich ist, wird unter **companyapps**ein Konto angezeigt.

1. Wählen Sie das Konto aus, und wählen Sie dann **Synchronisieren**aus. Diese Aktion beginnt mit der Verwaltung mit Configuration Manager.

### <a name="verify-enrollment-in-the-console"></a>Überprüfen der Registrierung in der-Konsole

Verwenden Sie die Configuration Manager Konsole, um zu überprüfen, ob Geräte erfolgreich registriert wurden. Wechseln Sie in der Configuration Manager-Konsole zum Arbeitsbereich **Assets und Konformität**, und wählen Sie **Geräte** aus. Suchen Sie in der Liste der Geräte nach dem registrierten Gerät, oder suchen Sie nach diesem.