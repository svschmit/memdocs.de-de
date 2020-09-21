---
title: Hinzufügen und Zuweisen von Win32-Apps zu Microsoft Intune
titleSuffix: ''
description: Erfahren Sie, wie Sie Win32-Apps mit Microsoft Intune hinzufügen, zuweisen und verwalten können.
keywords: ''
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 09/09/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 5266f354ea5806743813d1aeb4c456890fa46b19
ms.sourcegitcommit: 4b8c317c71535c2d464f336c03b5bebdd2c6d4c9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/15/2020
ms.locfileid: "90083946"
---
# <a name="add-assign-and-monitor-a-win32-app-in-microsoft-intune"></a>Hinzufügen, Zuweisen und Überwachen einer Win32-App in Microsoft Intune

Nachdem Sie mit dem [Microsoft Win32 Content Prep Tool](https://go.microsoft.com/fwlink/?linkid=2065730) die [Win32-App für den Upload in Intune vorbereitet haben](apps-win32-prepare.md), können Sie die App zu Intune hinzufügen. Weitere Informationen zum Vorbereiten einer Win32-App auf den Upload finden Sie unter [Vorbereiten des Inhalts der Win32-App für den Upload](apps-win32-prepare.md).

## <a name="prerequisites"></a>Voraussetzungen

Stellen Sie sicher, dass die folgenden Kriterien erfüllt sind, wenn Sie die Win32-App-Verwaltung verwenden wollen:

- Verwenden Sie Windows 10 Version 1607 oder höher (Enterprise-, Pro- und Education-Editionen).
- Geräte müssen Azure Active Directory (Azure AD) beigetreten und automatisch registriert sein. Die Intune-Verwaltungserweiterung unterstützt Geräte, die Azure AD und der hybriden Domäne beigetreten und per Gruppenrichtlinie registriert sind. 
  > [!NOTE]
  > Im Szenario der Registrierung per Gruppenrichtlinie verwenden Endbenutzer das lokale Benutzerkonto zum Einbinden ihrer Windows 10-Geräte in Azure AD. Benutzer müssen sich mit ihrem Azure AD-Benutzerkonto beim Gerät anmelden und sich bei Intune registrieren. Intune installiert die Intune-Verwaltungserweiterung auf dem Gerät, wenn ein PowerShell-Skript oder eine Win32-App auf einen Benutzer oder ein Gerät ausgerichtet sind.
- Die Größe der Windows-Anwendung ist auf 8 GB pro App begrenzt.

Sie können eine Win32-App ähnlich wie eine standardmäßige branchenspezifische App (Line-of-Business, LOB) zu Microsoft Intune hinzufügen. Diese Art von App wird typischerweise intern oder von einem Drittanbieter geschrieben. 

## <a name="process-flow-to-add-a-win32-app-to-intune"></a>Prozessflow für das Hinzufügen einer Win32-App zu Intune

<img alt="Flow chart of the process to add a Win32 app to Intune." src="./media/apps-win32-app-management/add-win32-app.svg" width="500">

## <a name="add-a-win32-app-to-intune"></a>Hinzufügen einer Win32-App zu Intune

Die folgenden Schritte helfen Ihnen beim Hinzufügen einer Windows-App zu Intune:

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Apps** > **Alle Apps** > **Hinzufügen** aus.
3. Wählen Sie im Bereich **App-Typ auswählen** unter den App-Typen **Sonstige** die Option **Windows-App (Win32)** aus.

    > [!IMPORTANT]
    > Stellen Sie sicher, dass Sie die neueste Version des Microsoft Win32-Inhaltsvorbereitungstools verwenden. Wenn Sie nicht die neueste Version verwenden, werden Sie in einer Warnung darauf hingewiesen, dass die App mit einer älteren Version des Tools gepackt wurde. 

4. Klicken Sie auf **Auswählen**. Die Schritte **App hinzufügen** werden angezeigt.

## <a name="step-1-app-information"></a>Schritt 1: App-Informationen

### <a name="select-the-app-package-file"></a>Auswählen der App-Paketdatei

1. Klicken Sie im Bereich **App hinzufügen** auf **App-Paketdatei auswählen**. 
2. Klicken Sie im Bereich **App-Paketdatei** auf die Schaltfläche zum Durchsuchen. Wählen Sie dann eine Windows-Installationsdatei mit der Erweiterung *.intunewin* aus.
   Die App-Informationen werden angezeigt.
3. Wenn Sie fertig sind, wählen Sie im Bereich **App-Paketdatei** die Option **OK** aus.

### <a name="set-app-information"></a>Festlegen von App-Informationen

Fügen Sie auf der Seite **App-Informationen** die Details zu Ihrer App hinzu. Je nach ausgewählter App wurden einige der Werte auf dieser Seite möglicherweise automatisch ausgefüllt.

- **Name:** Geben Sie den Namen der App so ein, wie er im Unternehmensportal angezeigt wird. Stellen Sie sicher, dass alle App-Namen eindeutig sind. Wenn ein App-Name zweimal vergeben wird, wird im Unternehmensportal nur eine der Apps angezeigt.
- **Beschreibung:** Geben Sie eine Beschreibung für die App ein. Die Beschreibung wird im Unternehmensportal angezeigt.
- **Herausgeber**: Geben Sie den Namen des Herausgebers der App ein.
- **Kategorie**: Wählen Sie eine oder mehrere der integrierten oder von Ihnen erstellten App-Kategorien aus. Kategorien erleichtern es dem Benutzer, die App über das Unternehmensportal zu finden.
- **Diese App als ausgewählte App im Unternehmensportal anzeigen**: Präsentieren Sie die App herausgehoben auf der Hauptseite des Unternehmensportals, wenn die Benutzer nach Apps suchen.
- **Informations-URL**: Geben Sie optional eine URL zu einer Website ein, die Informationen über diese App enthält. Die URL wird im Unternehmensportal angezeigt.
- **URL der Datenschutzrichtlinien:** Geben Sie optional eine URL zu einer Website ein, die Datenschutzinformationen für diese App enthält. Die URL wird im Unternehmensportal angezeigt.
- **Entwickler**: Geben Sie optional den Namen des App-Entwicklers ein.
- **Besitzer**: Geben Sie optional einen Namen für den Besitzer dieser App ein. Ein Beispiel ist **Personalabteilung**.
- **Anmerkungen**: Geben Sie Hinweise zu dieser App ein.
- **Logo**: Laden Sie ein der App zugeordnetes Symbol hoch. Dieses Symbol wird mit der App angezeigt, wenn Benutzer das Unternehmensportal durchsuchen.

Klicken Sie auf **Weiter**, um die Seite **Programm** anzuzeigen.

## <a name="step-2-program"></a>Schritt 2: Programm

Konfigurieren Sie auf der Seite **Programm** die Befehle zur Installation und Entfernung der App:

- **Installationsbefehl**: Füge die komplette Befehlszeile für die Installation hinzu, um die App zu installieren. 

    Wenn der Dateiname Ihrer App z. B. **MyApp123** lautet, fügen Sie Folgendes hinzu:

    `msiexec /p "MyApp123.msp"`
    
    Wenn die Anwendung `ApplicationName.exe` lautet, besteht der Befehl aus dem Anwendungsnamen gefolgt von den Befehlsargumenten (Optionen), die vom Paket unterstützt werden. Beispiel:

    `ApplicationName.exe /quiet`
    
    Im obigen Befehl unterstützt das Paket `ApplicationName.exe` das Befehlsargument `/quiet`. 
    
    Um die genauen Argumente zu erfahren, die vom Anwendungspaket unterstützt werden, wenden Sie sich an den Anbieter der Anwendung.

    > [!IMPORTANT]
    > Administrator sollten die Befehlstools immer mit Bedacht verwenden. Über die Felder des **Installationsbefehls** und des **Deinstallationsbefehls** könnten unerwartete oder schädliche Befehle übergeben werden.

- **Deinstallationsbefehl**: Fügen Sie die vollständige Befehlszeile ein, um die App basierend auf der App-GUID zu deinstallieren. 

    Beispiel:
    
    `msiexec /x "{12345A67-89B0-1234-5678-000001000000}"`

- **Installationsverhalten**: Legen Sie das Installationsverhalten entweder auf **System** oder **Benutzer** fest.

    > [!NOTE]
    > Sie können eine Win32-App für die Installation im **Benutzerkontext** oder **Systemkontext** konfigurieren. Der **Benutzerkontext** bezieht nur auf einen bestimmten Benutzer. Der **Systemkontext** bezieht sich auf alle Benutzer eines Windows 10-Geräts.
    >
    > Damit Win32-Apps installiert werden können, müssen Benutzer nicht beim Gerät angemeldet sein.
    > 
    > Die Installation und Deinstallation einer Win32-App wird standardmäßig mit Administratorberechtigungen ausgeführt, wenn die App zur Installation im Benutzerkontext festgelegt ist und der Gerätebenutzer über Administratorrechte verfügt.
    
- **Verhalten beim Geräteneustart**: Wählen Sie eine der folgenden Optionen aus:
    - **Verhalten auf Grundlage von Rückgabecodes bestimmen:** Wählen Sie diese Option aus, um das Gerät basierend auf den Rückgabecodes neu zu starten.
    - **Keine bestimmte Aktion:** Wählen Sie diese Option aus, um Geräteneustarts während der App-Installation von MSI-basierten Apps zu unterdrücken.
    - **Bei der App-Installation kann ein Geräteneustart erzwungen werden**: Wählen Sie diese Option aus, um die App-Installation ohne Unterdrückung von Neustarts abzuschließen.
    - **Intune erzwingt einen obligatorischen Geräteneustart**: Wählen Sie diese Option aus, um das Gerät nach einer erfolgreichen App-Installation immer neu zu starten.

- **Geben Sie Rückgabecodes an, um das Verhalten nach der Installation festzulegen**: Fügen Sie die Rückgabecodes hinzu, mit denen das Verhalten bei einer erneuten Installation der App oder das Verhalten nach der Installation angegeben wird. Rückgabecodeeinträge werden standardmäßig bei der Erstellung der App hinzugefügt. Sie können jedoch weitere Rückgabecodes hinzufügen oder bestehende Rückgabecodes ändern.
    1. Legen Sie in der Spalte **Codetyp** für den **Codetyp** einen der folgenden Wert fest:
        - **Fehlgeschlagen:** Der Rückgabewert, der auf einen Fehler bei der App-Installation hinweist.
        - **Harter Neustart**: Der Rückgabecode für den harten Neustart gestattet es nicht, dass die nächste Win32-App ohne Neustart auf dem Client installiert wird. 
        - **Warmneustart**: Dieser Rückgabecode ermöglicht die Installation der nächsten Win32-App, ohne dass ein Neustart des Clients erforderlich ist. Ein Neustart ist erforderlich, um die Installation der aktuellen Anwendung abzuschließen.
        - **Wiederholen:** Bei diesem Rückgabecode versucht der Wiederholungs-Agent dreimal, die App zu installieren. Zwischen den einzelnen Versuchen wird fünf Minuten gewartet. 
        - **Erfolg:** Dieser Rückgabewert gibt an, dass die App erfolgreich installiert wurde.
    2. Klicken Sie ggf. auf **Hinzufügen**, um weitere Rückgabecodes hinzuzufügen, oder ändern Sie bestehende Rückgabecodes.

Klicken Sie auf **Weiter**, um die Seite **Anforderungen** anzuzeigen.    

## <a name="step-3-requirements"></a>Schritt 3: Anforderungen

Geben Sie auf der Seite **Anforderungen** die Anforderungen an, die Geräte vor der App-Installation erfüllen müssen:

- **Betriebssystemarchitektur**: Wählen Sie die Architekturen aus, die zum Installieren der App benötigt werden.
- **Mindestens erforderliches Betriebssystem**: Wählen Sie die für die Installation der App mindestens erforderliche Version des Betriebssystems aus.
- **Erforderlicher Speicherplatz (MB)** : Optional können Sie den freien Speicherplatz hinzufügen, der auf dem Systemlaufwerk erforderlich ist, um die App zu installieren.
- **Erforderlicher physischer Speicher (MB)** : Optional können Sie den für die Installation der App erforderlichen physischen Arbeitsspeicher (RAM) hinzufügen.
- **Mindestens erforderliche Anzahl logischer Prozessoren**: Optional können Sie die Anzahl von logischen Prozessoren hinzufügen, die für die Installation der App mindestens erforderlich sind.
- **Mindestens erforderliche CPU-Geschwindigkeit (MHz)** : Optional können Sie die CPU-Geschwindigkeit hinzufügen, die für die Installation der App mindestens erforderlich ist.
- **Konfigurieren Sie zusätzliche Anforderungsregeln**: 
    1. Wählen Sie **Hinzufügen** aus, um den Bereich **Anforderungsregel hinzufügen** anzuzeigen und weitere Anforderungsregeln zu konfigurieren. Wählen Sie den **Anforderungstyp** aus, um die Art der Regel auszuwählen, mit der Sie bestimmen, auf welche Weise eine Anforderung überprüft wird. Anforderungsregeln können auf Dateisysteminformationen, Registrierungswerten oder PowerShell-Skripts basieren. 
        - **Datei:** Wenn Sie **Datei** als **Anforderungstyp** auswählen, muss die Anforderungsregel eine Datei oder einen Ordner, ein Datum, eine Version oder eine Größe erkennen. 
            - **Pfad:** Der vollständige Pfad des Ordners, der die Datei oder den Order für die Erkennung enthält.
            - **Datei oder Ordner**: Die Datei oder der Ordner, die bzw. der erkannt werden soll.
            - **Eigenschaft**: Wählen Sie die Art der Regel aus, mit der das Vorhandensein der App überprüft wird.
            - **Auf 64-Bit-Clients einer 32-Bit-App zugeordnet**: Wählen Sie **Ja** aus, um Pfadumgebungsvariablen im 32-Bit-Kontext auf 64-Bit-Clients zu erweitern. Wählen Sie **Nein** (Standard) aus, um Pfadvariablen im 64-Bit-Kontext auf 64-Bit-Clients zu erweitern. 32-Bit-Clients verwenden immer den 32-Bit-Kontext.
        - **Registrierung:** Wenn Sie **Registrierung** als **Anforderungstyp** auswählen, muss die Anforderungsregel eine auf Wert, Zeichenfolge, Ganzzahl oder Version basierende Registrierungseinstellung erkennen.
            - **Schlüsselpfad**: Der vollständige Pfad des Registrierungseintrags, der den zu erkennenden Wert enthält.
            - **Wertname**: Der Name des Registrierungswerts, der erkannt werden soll. Wenn dieser Wert leer ist, erfolgt die Erkennung über den Schlüssel. Der (Standard-) Wert eines Schlüssels wird als Erkennungswert verwendet, wenn die Erkennungsmethode eine andere ist als das Vorhandensein von Dateien oder Ordnern.
            - **Registrierungsschlüsselanforderung**: Wählen Sie die Art des Registrierungsschlüsselvergleichs, mit der bestimmt wird, wie die Anforderungsregel überprüft wird.
            - **Auf 64-Bit-Clients einer 32-Bit-App zugeordnet**: Wählen Sie **Ja** aus, um die 32-Bit-Registrierung auf 64-Bit-Clients zu durchsuchen. Wählen Sie **Nein** (Standard) aus, um die 64-Bit-Registrierung auf 64-Bit-Clients zu durchsuchen. 32-Bit-Clients durchsuchen immer die 32-Bit-Registrierung.
        - **Skript:** Wählen Sie **Skript** als **Anforderungstyp** aus, wenn Sie keine Anforderungsregel erstellen können, die auf einer Datei, einer Registrierung oder einer anderen in der Intune-Konsole verfügbaren Methode basiert.
            - **Skriptdatei**: Bei einer auf einem PowerShell-Skript basierenden Regel können Sie STDOUT (das Standardausgabemodell) genauer erkennen, wenn der vorhandene Code 0 lautet. Sie können z. B. STDOUT als einen Integer erkennen, der einen Wert 1 aufweist.
            - **Skript auf 64-Bit-Clients als 32-Bit-Prozess ausführen**: Wählen Sie **Ja** aus, um das Skript in einem 32-Bit-Prozess auf 64-Bit-Clients auszuführen. Wählen Sie **Nein** (Standardeinstellung) aus, um das Skript in einem 64-Bit-Prozess auf 64-Bit-Clients auszuführen. Auf 32-Bit-Clients wird das Skript in einem 32-Bit-Prozess ausgeführt.
            - **Dieses Skript mit den Anmeldeinformationen des angemeldeten Benutzers ausführen:** Wählen Sie **Ja** aus, um das Skript mit den Anmeldeinformationen des angemeldeten Geräts auszuführen.
            - **Skriptsignaturprüfung erzwingen:** Wählen Sie **Ja** aus, um sicherzustellen, dass das Skript von einem vertrauenswürdigen Herausgeber signiert ist, sodass es ohne Warnungen oder Aufforderungen ausgeführt werden kann. Das Skript wird ohne Blockierung ausgeführt. Wählen Sie **Nein** (Standard) aus, um das Skript mit Venutzerbestätigung ohne Signaturüberprüfung auszuführen.
            - **Ausgabedatentyp auswählen:** Wählen Sie den Datentyp aus, der beim Bestimmen einer Übereinstimmung mit einer Anforderungsregel verwendet wird.
    2. Wenn Sie die Anforderungsregeln festgelegt haben, wählen Sie **OK** aus.

Klicken Sie auf **Weiter**, um die Seite **Erkennungsregeln** anzuzeigen. 

## <a name="step-4-detection-rules"></a>Schritt 4: Erkennungsregeln

Konfigurieren Sie auf der Seite **Erkennungsregeln** die Regeln, mit denen erkannt wird, ob die App vorhanden ist:
    
- **Regelformat**: Wählen Sie im Feld aus, wie das Vorhandensein der App erkannt werden soll. Sie können auswählen, ob Sie die Erkennungsregeln manuell konfigurieren oder ein benutzerdefiniertes Skript verwenden möchten, um das Vorhandensein der App zu erkennen. Sie müssen mindestens eine Erkennungsregel auswählen. 

  > [!NOTE]
  > Im Bereich **Erkennungsregeln** können Sie auswählen, ob Sie mehrere Regeln hinzufügen möchten. Die Bedingungen für *alle* Regeln müssen erfüllt sein, um die App zu erkennen.
  >
  > Wenn Intune erkennt, dass die App auf dem Gerät nicht vorhanden ist, bietet es die App nach 24 Stunden erneut an. Dies gilt nur für Apps mit der erforderlichen Absicht.

- **Erkennungsregeln manuell konfigurieren**: Sie können einen der folgenden Regeltypen auswählen:
    - **MSI**: Überprüfung auf der Grundlage der MSI-Versionsprüfung. Diese Option kann nur einmal hinzugefügt werden. Wenn Sie diesen Regeltyp auswählen, gibt es zwei Einstellungen:
        - **MSI-Produktcode**: Fügen Sie einen gültigen MSI-Produktcode für die App hinzu.
        - **Überprüfung der MSI-Produktversion**: Klicken Sie auf **Ja**, um zusätzlich zum MSI-Produktcode auch die MSI-Produktversion zu überprüfen.
    - **Datei:** Überprüfen Sie Datum, Version und Größe basierend auf der Datei- oder Ordnererkennung.
        - **Pfad:** Geben Sie den vollständigen Pfad des Ordners ein, der die Datei oder den Order für die Erkennung enthält.
        - **Datei oder Ordner**: Geben Sie die Datei oder den Ordner ein, die bzw. der erkannt werden soll.
        - **Erkennungsmethode**: Wählen Sie die Erkennungsmethode aus, mit der das Vorhandensein der App überprüft werden soll.
        - **Auf 64-Bit-Clients einer 32-Bit-App zugeordnet**: Wählen Sie **Ja** aus, um Pfadumgebungsvariablen im 32-Bit-Kontext auf 64-Bit-Clients zu erweitern. Wählen Sie **Nein** (Standard) aus, um Pfadvariablen im 64-Bit-Kontext auf 64-Bit-Clients zu erweitern. 32-Bit-Clients verwenden immer den 32-Bit-Kontext.
            
        **Beispiele für dateibasierte Erkennung**

        Überprüfen Sie, ob die Datei vorhanden ist.
         
        ![Screenshot des Bereichs mit Erkennungsregeln – Vorhandensein einer Datei](./media/apps-win32-app-management/apps-win32-app-03.png)
        
        Überprüfen Sie, ob der Ordner vorhanden ist.
        
        ![Screenshot des Bereichs mit Erkennungsregeln – Vorhandensein eines Ordners](./media/apps-win32-app-management/apps-win32-app-04.png)
        
    - **Registrierung:** Überprüfen Sie die Registrierung anhand von Wert, Zeichenfolge, Ganzzahl oder Version.
        - **Schlüsselpfad**: Der vollständige Pfad des Registrierungseintrags mit dem Wert, der erkannt werden soll. Eine gültige Syntax ist HKEY_LOCAL_MACHINE\Software\WinRAR oder HKLM\Software\WinRAR.
        - **Wertname**: Der Name des Registrierungswerts, der erkannt werden soll. Wenn dieser Wert leer ist, erfolgt die Erkennung über den Schlüssel. Der (Standard-) Wert eines Schlüssels wird als Erkennungswert verwendet, wenn die Erkennungsmethode eine andere ist als das Vorhandensein von Dateien oder Ordnern.
        - **Erkennungsmethode**: Wählen Sie die Erkennungsmethode aus, mit der das Vorhandensein der App überprüft werden soll.
        - **Auf 64-Bit-Clients einer 32-Bit-App zugeordnet**: Wählen Sie **Ja** aus, um die 32-Bit-Registrierung auf 64-Bit-Clients zu durchsuchen. Wählen Sie **Nein** (Standard) aus, um die 64-Bit-Registrierung auf 64-Bit-Clients zu durchsuchen. 32-Bit-Clients durchsuchen immer die 32-Bit-Registrierung.
            
        **Beispiele für registrierungsbasierte Erkennung**
        
        Überprüfen Sie, ob der Registrierungsschlüssel vorhanden ist.
            
        ![Screenshot des Erkennungsregelbereichs – Registrierungsschlüssel ist vorhanden](./media/apps-win32-app-management/apps-win32-app-05.png)    
            
        Überprüfen Sie, ob der Registrierungswert vorhanden ist.
        
        ![Screenshot des Erkennungsregelbereichs – Registrierungswert ist vorhanden](./media/apps-win32-app-management/apps-win32-app-06.png)    
        
        Überprüfen Sie, ob die Zeichenfolge für den Registrierungswert identisch ist.
        
        ![Screenshot des Erkennungsregelbereichs – Zeichenfolge für Registrierungswert ist identisch](./media/apps-win32-app-management/apps-win32-app-07.png)    
     
- **Benutzerdefiniertes Skript für die Erkennung verwenden**: Geben Sie das PowerShell-Skript an, das zum Erkennen dieser App verwendet werden soll. 
    
   - **Skriptdatei**: Wählen Sie ein PowerShell-Skript aus, mit dem Vorhandensein der App auf dem Client erkannt werden soll. Die App wird erkannt, wenn das Skript sowohl den Wert **0** für den Exitcode zurückgibt als auch einen Zeichenfolgenwert an STDOUT ausgibt.

   - **Skript auf 64-Bit-Clients als 32-Bit-Prozess ausführen**: Wählen Sie **Ja** aus, um das Skript in einem 32-Bit-Prozess auf 64-Bit-Clients auszuführen. Wählen Sie **Nein** (Standardeinstellung) aus, um das Skript in einem 64-Bit-Prozess auf 64-Bit-Clients auszuführen. Auf 32-Bit-Clients wird das Skript in einem 32-Bit-Prozess ausgeführt.

   - **Skriptsignaturprüfung erzwingen:** Wählen Sie **Ja** aus, um sicherzustellen, dass das Skript von einem vertrauenswürdigen Herausgeber signiert ist, sodass es ohne Warnungen oder Aufforderungen ausgeführt werden kann. Das Skript wird ohne Blockierung ausgeführt. Wählen Sie **Nein** (Standard) aus, um das Skript mit Venutzerbestätigung ohne Signaturüberprüfung auszuführen.
    
   Der Intune-Agent überprüft die Ergebnisse des Skripts. Er liest die vom Skript in den Standardausgabestream (STDOUT), den Standardfehlerstream (STDERR) und den Exitcode geschriebenen Werte. Wenn das Skript mit einem Wert ungleich 0 (null) beendet wird, schlägt das Skript fehl und der Erkennungszustand der Anwendung ist „nicht installiert“. Wenn der Exitcode gleich null ist und in STDOUT Daten enthalten sind, ist der Erkennungszustand der Anwendung„Installiert“. 

   > [!NOTE]
   > Es wird empfohlen, Ihr Skript in UTF-8 zu codieren. Wenn das Skript mit dem Wert **0** beendet wird, war die Skriptausführung erfolgreich. Der zweite Ausgabekanal weist darauf hin, dass die App erkannt wurde. STDOUT-Daten geben an, dass die App auf dem Clientgerät gefunden wurde. In STDOUT wird nicht nach einer bestimmten Zeichenfolge gesucht.

Nachdem Sie Ihre Regel(n) hinzugefügt haben, wählen Sie **Weiter** aus, um die Seite **Abhängigkeiten** anzuzeigen.

## <a name="step-5-dependencies"></a>Schritt 5: -Abhängigkeiten

App-Abhängigkeiten sind Anwendungen, die installiert sein müssen, bevor Ihre Win32-App installiert werden kann. Sie können anfordern, dass andere Apps als Abhängigkeiten installiert werden. 

Insbesondere müssen die abhängigen Apps auf dem Gerät installiert sein, bevor die Win32-App installiert wird. Es sind maximal 100 Abhängigkeiten möglich. Dazu zählen die Abhängigkeiten aller eingeschlossenen Abhängigkeiten sowie die App selbst. 

Sie können Win32-App-Abhängigkeiten erst hinzufügen, nachdem Ihre Win32-App zu Intune hinzugefügt und darin hochgeladen wurde. Nachdem Ihre Win32-App hinzugefügt wurde, sehen Sie die Option **Abhängigkeiten** im Bereich für Ihre Win32-App. 

Jede Win32-App-Abhängigkeit muss auch eine Win32-App sein. Abhängigkeiten von anderen App-Typen, z. B. einzelne branchenspezifische Apps mit MSI oder Microsoft Store-Apps, werden nicht unterstützt.

Zum Hinzufügen einer App-Abhängigkeit können Sie nach dem Namen und dem Herausgeber der App suchen. Darüber hinaus können Sie Ihre hinzugefügten Abhängigkeiten nach Name und Herausgeber der App sortieren. Bereits hinzugefügte App-Abhängigkeiten können in der Liste der hinzugefügten App-Abhängigkeiten nicht ausgewählt werden. 

Sie können auswählen, ob jede abhängige App automatisch installiert wird. Standardmäßig ist für die Option **Automatisch installieren** für jede Abhängigkeit **Ja** festgelegt. Durch das automatische Installieren einer abhängigen App, selbst wenn diese nicht auf den Benutzer oder das Gerät ausgerichtet ist, installiert Intune die App auf dem Gerät. Dadurch wird das Abhängigkeitskriterium erfüllt, bevor Ihre Win32-App installiert wird. 

Beachten Sie unbedingt Folgendes: eine Abhängigkeit kann rekursive Unterabhängigkeiten aufweisen, und jede Unterabhängigkeit wird vor der Hauptabhängigkeit installiert. Zudem erfolgt die Installation von Abhängigkeiten keiner bestimmten Installationsreihenfolge auf Abhängigkeitsebene.

### <a name="select-the-dependencies"></a>Auswählen der Abhängigkeiten

Wählen Sie auf der Seite **Abhängigkeiten** die Anwendungen aus, die installiert sein müssen, bevor Ihre Win32-App installiert werden kann:
1. Klicken Sie auf **Hinzufügen**, um den Bereich **Abhängigkeit hinzufügen** anzuzeigen.
3. Fügen Sie die abhängigen Apps hinzu, und klicken Sie dann auf **Auswählen**.
4. Wählen Sie in der Spalte **Automatisch installieren** die Optionen **Ja** oder **Nein** aus, um anzugeben, ob die abhängigen Apps automatisch installiert werden sollen.

Klicken Sie nach der Auswahl der Abhängigkeiten auf **Weiter**, um die Seite **Bereichstags** anzuzeigen.

### <a name="understand-additional-dependency-details"></a>Weitere Informationen zu zusätzlichen Abhängigkeiten

Benutzer werden in Windows-Benachrichtigungen darauf hingewiesen, dass abhängige Apps heruntergeladen und zusammen mit der Win32-App installiert werden. Wenn eine abhängige App nicht installiert ist, wird den Benutzern außerdem in der Regel eine der folgenden Benachrichtigungen angezeigt:
- Mindestens eine abhängige App konnte nicht installiert werden.
- Für mindestens eine abhängige App sind die Anforderungen nicht erfüllt.
- Für mindestens eine abhängige App steht ein Geräteneustart aus.

Wenn Sie in der Spalte **Automatisch installieren** keine Abhängigkeit angeben, wird nicht versucht, die Win32-App zu installieren. Darüber hinaus zeigt der App-Bericht an, dass die Abhängigkeit als `failed` gekennzeichnet wurde, und gibt eine Fehlerursache an. Durch Auswählen eines Fehlers (oder einer Warnung) in den [Installationsdetails](troubleshoot-app-install.md#win32-app-installation-troubleshooting) der Win32-App können Sie den Installationsfehler für die Abhängigkeit anzeigen.

Jede Abhängigkeit folgt der Intune-Wiederholungslogik für Win32-Apps (drei Installationsversuche mit jeweils fünf Minuten Wartezeit dazwischen) und dem globalen Zeitplan für eine erneute Auswertung. Abhängigkeiten sind außerdem nur zum Zeitpunkt der Installation der Win32-App auf dem Gerät anwendbar. Abhängigkeiten gelten nicht, wenn eine Win32-App deinstalliert wird. Zum Löschen einer Abhängigkeit klicken Sie auf die drei Punkte links neben der abhängigen App am Ende der Zeile in der Abhängigkeitsliste. 

## <a name="step-6-select-scope-tags-optional"></a>Schritt 6: Auswählen von Bereichsmarkierungen (optional)
Sie können Bereichsmarkierungen verwenden, um zu bestimmen, wer Client-App-Informationen in Intune anzeigen kann. Ausführliche Informationen zu Bereichsmarkierungen finden Sie unter [Use role-based access control and scope tags for distributed IT](../fundamentals/scope-tags.md) (Verwenden der rollenbasierten Zugriffssteuerung und von Bereichsmarkierungen für verteilte IT).

Klicken Sie auf **Bereichstags auswählen**, um optional Bereichsmarkierungen für die App hinzuzufügen. Klicken Sie auf **Weiter**, um die Seite **Zuweisungen** anzuzeigen.

## <a name="step-7-assignments"></a>Schritt 7: Zuweisungen

Sie können die Gruppenzuweisungen **Erforderlich**, **Für registrierte Geräte verfügbar** oder **Deinstallieren** für die App auswählen. Weitere Informationen finden Sie unter [Hinzufügen von Gruppen zum Organisieren von Benutzern und Geräten](../fundamentals/groups-add.md) und [Zuweisen von Apps zu Gruppen mit Microsoft Intune](apps-deploy.md).

1. Wählen Sie für die bestimmte App einen Zuweisungstyp aus:
    - **Erforderlich**: Die App wird auf Geräten in den ausgewählten Gruppen installiert.
    - **Für registrierte Geräte verfügbar**: Benutzer installieren die App über die Unternehmensportal-App oder -Website.
    - **Deinstallieren**: Die App wird auf Geräten in den ausgewählten Gruppen deinstalliert.
2. Klicken Sie auf **Gruppe hinzufügen**, und weisen Sie die Gruppen zu, die diese App verwenden werden.
3. Wählen Sie im Bereich **Gruppen auswählen** die Gruppen aus, die basierend auf Benutzern oder Geräten zugewiesen werden sollen.
4. Nach dem Auswählen der Gruppen können Sie auch **Endbenutzerbenachrichtigungen**, **Verfügbarkeit**und **Installationsstichtag** festlegen. Weitere Informationen finden Sie unter [Festlegen der Verfügbarkeit und Benachrichtigungen von Win32-Apps](apps-win32-app-management.md#set-win32-app-availability-and-notifications).
5. Wenn sich diese App-Zuweisung nicht auf Benutzergruppen auswirken soll, wählen Sie unter der Spalte **MODUS** die Option **Eingeschlossen** aus. Ändern Sie im Bereich **Zuweisung bearbeiten** den Wert für den **Modus** von **Eingeschlossen** in **Ausgeschlossen**. Klicken Sie auf **OK**, um den Bereich **Zuweisung bearbeiten** zu schließen.
6. Wählen Sie im Abschnitt **App-Einstellungen** die Einstellung **Priorität der Übermittlungsoptimierung** für die App aus. Mit dieser Einstellung wird festgelegt, wie der App-Inhalt heruntergeladen wird. Sie können den App-Inhalt basierend auf der Zuweisung im Hintergrund oder im Vordergrund herunterladen. 

Nachdem Sie die Zuweisungen für die Apps festgelegt haben, klicken Sie auf **Weiter**, um die Seite **Überprüfen + erstellen** anzuzeigen.

## <a name="step-8-review-and-create"></a>Schritt 8: Überprüfen und erstellen

1. Überprüfen Sie die Werte und Einstellungen, die Sie für die App eingegeben haben. Überprüfen Sie, ob die konfigurierten App-Informationen richtig sind.
2. Wählen Sie **Erstellen** aus, um die App zu Intune hinzuzufügen.

    Der Bereich **Übersicht** für die branchenspezifische App wird angezeigt.

Hiermit haben Sie alle Schritte zum Hinzufügen einer Win32-App zu Intune abgeschlossen. Informationen zur Zuweisung und Überwachung von Apps finden Sie unter [Zuweisen von Apps zu Gruppen mit Microsoft Intune](apps-deploy.md) und [Überwachen von App-Informationen und -Zuweisungen mit Microsoft Intune](apps-monitor.md).

## <a name="next-steps"></a>Nächste Schritte

- [Überwachen von App-Informationen und -Zuweisungen mit Microsoft Intune](apps-monitor.md)
- [Behandeln von Win32-App-Problemen](apps-win32-troubleshoot.md)
