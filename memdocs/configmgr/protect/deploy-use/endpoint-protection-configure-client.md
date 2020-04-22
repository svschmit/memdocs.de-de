---
title: Endpoint Protection-Clienteinstellungen
titleSuffix: Configuration Manager
description: Erfahren Sie, wie Sie benutzerdefinierte Clienteinstellungen für Endpoint Protection konfigurieren.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 25a1803d7a2feebe7947478c0671e0112830b0d3
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81709178"
---
# <a name="configure-custom-client-settings-for-endpoint-protection"></a>Konfigurieren benutzerdefinierter Clienteinstellungen für Endpoint Protection

*Gilt für: Configuration Manager (Current Branch)*

Mit den folgenden Anweisungen konfigurieren Sie benutzerdefinierte Clienteinstellungen für Endpoint Protection, die dann auf einer Gerätesammlung in Ihrer Hierarchie bereitgestellt werden können.

> [!IMPORTANT]  
>  Konfigurieren Sie die Endpoint Protection-Clientstandardeinstellungen nur, wenn Sie sicher sind, dass diese Einstellungen für alle Computer in Ihrer Hierarchie verwendet werden sollen. 



## <a name="to-enable-endpoint-protection-and-configure-custom-client-settings"></a>So aktivieren Sie Endpoint Protection und konfigurieren benutzerdefinierte Clienteinstellungen

1. Klicken Sie in der Configuration Manager-Konsole auf **Verwaltung**.  

2. Klicken Sie im Arbeitsbereich **Verwaltung** auf **Clienteinstellungen**.  

3. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Erstellen** auf **Benutzerdefinierte Geräteclienteinstellungen erstellen**.  

4. Geben Sie im Dialogfeld **Benutzerdefinierte Geräteclienteinstellungen erstellen** einen Namen und eine Beschreibung für die Einstellungsgruppe ein, und wählen Sie dann **Endpoint Protection**aus.  

5. Konfigurieren Sie die Endpoint Protection-Clienteinstellungen, die Sie benötigen. Eine vollständige Liste der Endpoint Protection-Clienteinstellungen, die Sie konfigurieren können, finden Sie im Abschnitt „Endpoint Protection“ unter [Informationen zu Clienteinstellungen](../../core/clients/deploy/about-client-settings.md#endpoint-protection).  

   > [!IMPORTANT]  
   >  Installieren Sie die Endpoint Protection-Standortsystemrolle, bevor Sie Clienteinstellungen für Endpoint Protection konfigurieren.  

6. Klicken Sie auf **OK** , um das Dialogfeld **Benutzerdefinierte Geräteclienteinstellungen erstellen** zu schließen. Die neuen Clienteinstellungen erscheinen im Knoten **Clienteinstellungen** des Arbeitsbereichs **Verwaltung** .  

7. Stellen Sie anschließend die Clienteinstellungen einer Sammlung bereit. Wählen Sie die benutzerdefinierten Clienteinstellungen aus, die Sie bereitstellen möchten. Klicken Sie auf der Registerkarte **Startseite** in der Gruppe **Clienteinstellungen** auf **Bereitstellen**.  

8. Wählen Sie im Dialogfeld **Sammlung auswählen** die Sammlung aus, für die Sie die Clienteinstellungen bereitstellen möchten, und klicken Sie dann auf **OK**. Die neue Bereitstellung erscheint im Detailbereich auf der Registerkarte **Bereitstellungen** .  

Die Clients werden beim nächsten Clientrichtliniendownload mit diesen Einstellungen konfiguriert. Weitere Informationen finden Sie unter [Initiieren des Richtlinienabrufs für einen Konfigurations-Manager-Client](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  



## <a name="how-to-provision-the-endpoint-protection-client-in-a-disk-image"></a>Bereitstellen des Endpoint Protection-Clients in einem Datenträgerimage

Installieren Sie den Endpoint Protection-Client auf einem Computer, den Sie als Datenträgerimagequelle für die Betriebssystembereitstellung von Configuration Manager verwenden möchten. Dieser Computer wird in der Regel als Referenzcomputer bezeichnet. Nachdem Sie das Betriebssystemimage erstellt haben, verwenden Sie die Configuration Manager-Betriebssystembereitstellung, um das Image bereitzustellen.

> [!Important]  
> Unter Windows 10 und Windows Server 2016 ist Windows Defender standardmäßig vorinstalliert. Dieses Verfahren ist auf diesen Versionen von Windows nicht erforderlich.  

Mithilfe der folgenden Verfahren können Sie den Endpoint Protection-Client auf einem Referenzcomputer installieren und konfigurieren.


### <a name="prerequisites"></a>Voraussetzungen

Die folgende Liste enthält die erforderlichen Voraussetzungen für die Installation der Endpoint Protection-Clientsoftware auf einem Referenzcomputer.

- Sie benötigen Zugriff auf das Endpoint Protection-Clientinstallationspaket **scepinstall.exe**. Suchen Sie dieses Paket im Ordner **Client** des Configuration Manager-Installationsordners auf dem Standortserver.  

- Erstellen und exportieren Sie eine Richtlinie für Antischadsoftware, um den Endpoint Protection-Client mit der für Ihre Organisation erforderlichen Konfiguration bereitzustellen. Geben Sie diese Richtlinie dann an, wenn Sie den Endpoint Protection-Client manuell installieren. Weitere Informationen finden Sie unter [Erstellen und Bereitstellen von Richtlinien für Antischadsoftware](endpoint-antimalware-policies.md).  

  > [!NOTE]  
  >  Die **Standardclientrichtlinie für Antischadsoftware** kann nicht exportiert werden.  

- Wenn Sie den Endpoint Protection-Client mit den aktuellen Definitionen installieren möchten, laden Sie diese über [Windows Defender Security Intelligence](https://www.microsoft.com/wdsi) herunter.  

> [!NOTE]  
> Ab Configuration Manager Version 1802 muss der Endpoint Protection-Agent (SCEPInstall) nicht mehr auf Windows 10-Geräten installiert werden. Wenn dieser bereits auf Windows 10-Geräten installiert ist, wird er von Configuration Manager nicht entfernt. Administratoren können den Endpoint Protection-Agent auf Windows 10-Geräten entfernen, auf denen die Clientversion 1802 oder eine neuere Version ausgeführt wird. „SCEPInstall.exe“ ist möglicherweise immer noch unter C:\Windows\ccmsetup auf einigen Computern vorhanden, sollte aber nicht auf neue Clientinstallationen heruntergeladen werden. <!--503654-->


### <a name="how-to-install-the-endpoint-protection-client-on-the-reference-computer"></a>Installieren des Endpoint Protection-Clients auf dem Referenzcomputer

Installieren Sie den Endpoint Protection-Client über eine Eingabeaufforderung lokal auf dem Referenzcomputer. Laden Sie zunächst die Installationsdatei **scepinstall.exe** herunter. Weitere Informationen finden Sie unter [So installieren Sie den Endpoint Protection-Client über eine Eingabeaufforderung](#bkmk_manual-install).

Fügen Sie bei Bedarf eine vorkonfigurierte Richtlinie für Antischadsoftware oder eine zuvor exportierte Richtlinie für Antischadsoftware hinzu. 



## <a name="to-install-the-endpoint-protection-client-from-a-command-prompt"></a><a name="bkmk_manual-install"></a> So installieren Sie den Endpoint Protection-Client über eine Eingabeaufforderung

1. Kopieren Sie die Datei **scepinstall.exe** aus dem Ordner **Client** des Configuration Manager-Installationsordners auf den Computer, auf dem Sie die Endpoint Protection-Clientsoftware installieren möchten.  

2. Öffnen Sie eine Eingabeaufforderung als Administrator. Ändern Sie das Verzeichnis in den Ordner, der den Installer enthält. Führen Sie anschließend `scepinstall.exe` aus, und fügen Sie dabei nach Bedarf zusätzliche Befehlszeileneigenschaften hinzu:


   |  Eigenschaft   |                                  Beschreibung                                   |
   |-------------|--------------------------------------------------------------------------------|
   |    `/s`     |                           Führt den Installer im Hintergrund aus                           |
   |    `/q`     |                        Extrahiert die Setupdateien im Hintergrund                        |
   |    `/i`     |                           Führt den Installer wie gewohnt aus                           |
   |  `/policy`  | Gibt die Datei mit der Richtlinie für Antischadsoftware an, die bei der Installation zum Konfigurieren des Clients verwendet werden soll. |
   | `/sqmoptin` |     Aktiviert das Microsoft-Programm zur Verbesserung der Benutzerfreundlichkeit (CEIP)     |


3. Befolgen Sie die Bildschirmanweisungen, um die Clientinstallation abzuschließen.  

4. Wenn Sie das aktuellste Updatedefinitionspaket heruntergeladen haben, kopieren Sie das Paket auf den Clientcomputer und doppelklicken Sie darauf, um es zu installieren.  

   > [!NOTE]  
   >  Nach dem Abschluss der Endpoint Protection-Clientinstallation führt der Client automatisch eine Definitionsupdateprüfung aus. Bei erfolgreicher Updateprüfung muss das aktuelle Definitionsupdate nicht manuell installiert werden.  

#### <a name="example-install-the-client-with-an-antimalware-policy"></a>Beispiel: Installation des Clients mit einer Richtlinie für Antischadsoftware

`scepinstall.exe /policy <full path>\<policy file>`



## <a name="verify-the-endpoint-protection-client-installation"></a>Überprüfen der Endpoint Protection-Clientinstallation

Überprüfen Sie nach der Installation des Endpoint Protection-Clients auf Ihrem Referenzcomputer, ob der Client ordnungsgemäß funktioniert.

1.  Öffnen Sie auf dem Referenzcomputer **System Center Endpoint Protection** über den Infobereich von Windows.  

2.  Überprüfen Sie im Dialogfeld **System Center Endpoint Protection** auf der Registerkarte **Start**, ob die Einstellung **Ein** für den **Echtzeitschutz** festgelegt wurde.  

3.  Überprüfen Sie, ob für **Virus and spyware definitions** (Viren- und Spywaredefinitionen) der Status **Aktuell**angezeigt wird.  

4.  Wählen Sie unter **Scanoptionen**den Eintrag **Vollständig** aus, und klicken Sie dann auf **Jetzt scannen**, um sicherzustellen, dass der Referenzcomputer für die Imageerstellung bereit ist.  



## <a name="prepare-the-endpoint-protection-client-for-imaging"></a>Vorbereiten des Endpoint Protection-Clients für die Imageerstellung

Führen Sie die folgenden Schritte aus, um den Endpoint Protection-Client für die Imageerstellung vorzubereiten:

1. Melden Sie sich auf dem Referenzcomputer als Administrator an.  

2. Laden Sie die **PsExec**-Datei von [Windows SysInternals](https://docs.microsoft.com/sysinternals/downloads/psexec) herunter, und installieren Sie sie.  

3. Führen Sie eine Eingabeaufforderung als Administrator aus, ändern Sie das Verzeichnis in den Ordner, in dem Sie PsTools installiert haben, und geben Sie dann folgenden Befehl ein:  

   `psexec.exe -s -i regedit.exe`  

   > [!IMPORTANT]  
   >  Seien Sie vorsichtig, wenn Sie den Registrierungs-Editor auf diese Art ausführen. „PsExec.exe“ führt diesen im LocalSystem-Kontext aus.  

4. Löschen Sie im Registrierungs-Editor folgende Registrierungsschlüssel:  

   > [!IMPORTANT]  
   >  Löschen Sie die Registrierungsschlüssel in einem letzten Schritt, bevor vom Referenzcomputer ein Image erstellt wird. Der Endpoint Protection-Client erstellt diese Schlüssel neu, wenn er gestartet wird. Bei einem Neustart des Referenzcomputers müssen die Registrierungsschlüssel erneut gelöscht werden.  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\InstallTime`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanRun`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastScanType`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastQuickScanID`   

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Antimalware\Scan\LastFullScanID`  

   -   `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\RemovalTools\MRT\GUID`

Sie können den Referenzcomputer nun auf die Imageerstellung vorbereiten.

Wenn Sie ein Betriebssystemimage bereitstellen, das den Endpoint Protection-Client enthält, werden automatisch Informationen an den Configuration Manager-Standort gesendet, der dem Gerät zugewiesen ist. Der Client lädt alle entsprechenden Richtlinien für Antischadsoftware herunter und wendet diese an.  



## <a name="see-also"></a>Weitere Informationen:

Weitere Informationen zur Betriebssystembereitstellung in Configuration Manager finden Sie unter [Verwalten von Betriebssystemimages](../../osd/get-started/manage-operating-system-images.md).

