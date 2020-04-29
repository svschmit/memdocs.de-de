---
title: Erstellen von Konfigurationselementen für Windows 10
titleSuffix: Configuration Manager
description: Verwenden Sie das Windows 10-Konfigurationselement, um Einstellungen für Windows 10-Computer zu verwalten, die durch den Configuration Manager-Client verwaltet werden.
ms.date: 01/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 14226fbe-dd07-4432-910b-130790624a4e
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 9a1bda440ab3ccd02432f0b023a134b9f54cdafb
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81692538"
---
# <a name="create-configuration-items-for-windows-10-devices"></a>Erstellen von Konfigurationselementen für Windows 10-Geräte

Verwenden Sie das Configuration Manager-Konfigurationselement für **Windows 10**, um Einstellungen für Windows 10-Computer zu bearbeiten, die mit dem Configuration Manager-Client verwaltet werden.  
  
> [!IMPORTANT]  
>  Wenn Sie in dieser Version eine **Kennwort**-Einstellung als Teil eines Konfigurationselements vom Typ **Windows 10** erstellt haben (für ein Gerät, das mit dem Configuration Manager-Client verwaltet wird), sollten Sie sich des folgenden Problems bewusst sein. Wenn die Einstellung nicht bereits vorhanden ist oder nicht auf dem Windows 10-Gerät konfiguriert wurde, wird sie fälschlicherweise zu „konform“ ausgewertet.  
>   
>  Um das Problem beim Erstellen einer Einstellung für diese Geräte zu umgehen, stellen sicher, dass auf den Einstellungsseiten des Assistenten zum Erstellen von Konfigurationselementen **Nicht kompatible Einstellungen wiederherstellen** ausgewählt ist. Wenn Sie darüber hinaus eine Konfigurationsbasislinie mit einem Windows 10-Konfigurationselement bereitstellen, das Kennworteinstellungen enthält, wählen Sie im Dialogfeld die Option **Nicht konforme Regeln wiederherstellen, falls dies unterstützt wird** aus. Sie treffen diese Auswahl im Dialogfeld „Bereitstellen von Konfigurationsbaselines“. Durch diese Problemumgehung wird die Einstellung überwacht und korrigiert, falls sie nicht konform ist. Nach der Wiederherstellung wird die Einstellung ordnungsgemäß als **Konform** angegeben (es sei denn, aufgrund eines Problems wird ein **Fehler** festgestellt).  
  
### <a name="to-create-a-windows-10-configuration-item"></a>So erstellen Sie ein Windows 10-Konfigurationselement  
  
1. Wählen Sie in der Configuration Manager-Konsole die Option **Assets und Konformität** aus.  
  
2. Erweitern Sie im Arbeitsbereich **Assets und Konformität** die **Konformitätseinstellungen**, und wählen Sie dann **Konfigurationselemente** aus.  
  
3. Klicken Sie auf der Registerkarte **Start** in der Gruppe **Erstellen** auf **Konfigurationselement erstellen**.  
  
4. Geben Sie auf der Seite **Allgemein** des Assistenten zum **Erstellen von Konfigurationselementen** einen Namen und optional eine Beschreibung für das Konfigurationselement an.  
  
5. Wählen Sie unter **Typ des zu erstellenden Konfigurationselements angeben**den Typ **Windows 10**aus.  
  
6. Wenn Sie Kategorien erstellen und zuweisen, um das Durchsuchen und Filtern von Konfigurationselementen in der Configuration Manager-Konsole zu erleichtern, wählen Sie **Kategorien** aus.  
  
7. Wählen Sie auf der Seite **Unterstützte Plattformen** des Assistenten die jeweiligen Windows 10-Plattformen zur Bewertung des Konfigurationselements aus.  
  
8. Wählen Sie auf der Seite **Geräteeinstellungen** des Assistenten die Einstellungsgruppe aus, die Sie konfigurieren möchten. (Weitere Informationen finden Sie unter [Referenz zu Einstellungen des Konfigurationselements für Windows 10](#BKMK_Ref) in diesem Artikel.) Klicken Sie dann auf **Weiter**.  
  
   > [!TIP]  
   >  Ist die gewünschte Einstellung nicht aufgeführt, aktivieren Sie das Kontrollkästchen **Zusätzliche Einstellungen konfigurieren, die in den Standardeinstellungsgruppen nicht enthalten sind**.  
  
9. Konfigurieren Sie auf jeder Einstellungsseite die erforderlichen Einstellungen, und legen Sie fest, ob sie korrigiert werden sollen, wenn sie auf Geräten nicht kompatibel sind (sofern unterstützt).  
  
10. Sie können für jede Einstellungsgruppe auch den Schweregrad konfigurieren, der gemeldet wird, wenn ermittelt wird, dass ein Konfigurationselement nicht konform ist:  
  
    -   **Keine**: Für Geräte, bei denen bei dieser Konformitätsregel ein Fehler auftritt, wird kein Fehlerschweregrad für Configuration Manager-Berichte gemeldet.  
  
    -   **Information**: Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Information** für Configuration Manager-Berichte gemeldet.  
  
    -   **Warnung:** Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Warnung** für Configuration Manager-Berichte gemeldet.  
  
    -   **Kritisch**: Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet.  
  
    -   **Kritisch mit Ereignis**: Von Geräten, bei denen bei dieser Kompatibilitätsregel ein Fehler auftritt, wird der Fehlerschweregrad **Kritisch** für Configuration Manager-Berichte gemeldet. Dieser Schweregrad wird zudem im Anwendungsereignisprotokoll als Windows-Ereignis protokolliert.  
  
11. Überprüfen Sie auf der Seite **Plattformanwendbarkeit** des Assistenten alle Einstellungen, die mit den zuvor ausgewählten unterstützten Plattformen nicht kompatibel sind. Sie können zurückkehren und diese Einstellungen entfernen oder den Vorgang fortsetzen.  
  
    > [!TIP]  
    >  Nicht unterstützte Einstellungen werden nicht auf Kompatibilität überprüft.  
  
12. Schließen Sie den Assistenten ab.  
  
    Sie können das neue Konfigurationselement im Arbeitsbereich **Bestand und Kompatibilität** im Knoten **Konfigurationselemente** anzeigen.  
  
## <a name="windows-10-configuration-item-settings-reference"></a><a name="BKMK_Ref"></a> Windows 10 configuration item settings reference  
  
### <a name="password"></a>Kennwort  
  
|Einstellung|Details|  
|-------------|-------------|  
|**Kennworteinstellungen auf Geräten erforderlich**|Auf unterstützten Geräten ein Kennwort erfordern.|  
|**Minimale Kennwortlänge (Zeichen)**|Die Mindestlänge für das Kennwort in Zeichen.|  
|**Kennwortablauf in Tagen**|Die Anzahl der Tage, bevor ein Kennwort geändert werden muss.|  
|**Anzahl der gespeicherten Kennwörter**|Verhindert die Wiederverwendung vorheriger Kennwörter.|  
|**Anzahl der gescheiterten Anmeldeversuche vor dem Zurücksetzen eines Geräts**|Setzt das Gerät zurück, wenn die angegebene Anzahl nicht erfolgreicher Anmeldeversuche erreicht ist.|  
|**Leerlaufzeit vor dem Sperren des Geräts**|Gibt an, wie viele Minuten das Gerät inaktiv sein muss, bevor es automatisch gesperrt wird.|  
|**Kennwortkomplexität**|Wählen Sie aus, ob Sie eine PIN wie „1234“ angeben können oder ob ein sicheres Kennwort erforderlich ist.|
|**Anzahl komplexer Zeichengruppen, die im Kennwort erforderlich sind**|Wenn Sie ein **Sicheres** Kennwort ausgewählt haben, verwenden Sie diese Einstellung, um die Anzahl der erforderlichen komplexen Zeichensätze zu konfigurieren. Bei einem sicheren Kennwort sollte diese Einstellung mindestens auf **3** festgelegt werden, was bedeutet, dass sowohl Buchstaben als auch Ziffern erforderlich sind. Wählen Sie **4** aus, wenn Sie ein Kennwort erzwingen möchten, das zusätzlich Sonderzeichen wie z.B. **(%$** erfordert.<br>(ausschließlich Windows 10)  |
  
###  <a name="device"></a>Gerät  
  
|Name der Einstellung|Details|  
|------------------|-------------|  
|**Bluetooth**|Ermöglicht die Verwendung des Bluetooth-Features auf dem Gerät.|  
  
### <a name="cloud"></a>Cloud  
  
|Name der Einstellung|Details|  
|------------------|-------------|  
|**Synchronisierung der Einstellungen**|Ermöglicht die Synchronisierung von Einstellungen zwischen Geräten.|  
|**Synchronisierung der Anmeldeinformationen**|Ermöglicht die Synchronisierung von Anmeldeinformationen zwischen Geräten.|  
|**Synchronisierung von Einstellungen über getaktete Verbindungen**|Ermöglicht die Synchronisierung von Einstellungen, wenn die Internetverbindung getaktet ist.|  
  
### <a name="roaming"></a>Roaming  
  
|Name der Einstellung|Details|  
|------------------|-------------|  
|**Datenroaming**|Ermöglicht beim Zugriff auf Daten das Roaming zwischen Netzwerken.|  
  
### <a name="encryption"></a>Verschlüsselung  
  
|Name der Einstellung|Details|  
|------------------|-------------|  
|**Dateiverschlüsselung auf Gerät**|Erfordert die Verschlüsselung der Dateien auf dem Gerät.|  
  
### <a name="system-security"></a>Systemsicherheit  
  
|Name der Einstellung|Details|  
|------------------|-------------|  
|**Benutzerkontensteuerung**|Konfiguriert die Funktionsweise der Windows-Benutzerkontensteuerung auf dem Gerät.<br />Sie können sie z. B. deaktivieren oder die Stufe festlegen, bei der Sie benachrichtigt werden.|  
|**Netzwerkfirewall**|Aktiviert oder deaktiviert die Windows-Firewall.|  
|**SmartScreen**|Aktiviert oder deaktiviert Windows SmartScreen.|  
|**Virenschutz**|Erfordert, dass Antivirensoftware installiert und konfiguriert ist.|  
|**Virenschutzsignaturen sind aktuell**|Erfordert, dass die Signaturdateien für die Antivirensoftware auf dem Gerät auf dem aktuellen Stand sind|  
  
### <a name="windows-information-protection"></a>Windows Information Protection

Mit dem Anstieg von Geräten im Besitz der Mitarbeiter im Unternehmen entsteht auch ein höheres Risiko einer unbeabsichtigten Preisgabe von Daten durch Apps und Dienste, z. B. über E-Mail, soziale Medien und die öffentliche Cloud. Diese befinden sich außerhalb der Kontrolle des Unternehmens. Beispiele hierfür sind, wenn ein Mitarbeiter wie folgt vorgeht:

- Sendet die neuesten technischen Bilder von seinem persönlichen E-Mail-Konto aus.
- Kopiert Produktinformationen und fügt sie in einen Tweet ein.
- Speichert einen laufenden Umsatzbericht in seinem öffentlichen Cloudspeicher.

Windows Information Protection (WIP, früher „Unternehmensdatenschutz“) bietet Schutz vor potenziellen Datenlecks, ohne dass die Benutzerfreundlichkeit für die Mitarbeiter darunter leidet. Die Lösung schützt auch Unternehmens-Apps und -daten vor versehentlichen Datenlecks auf unternehmenseigenen sowie auf persönlichen Geräten, die die Mitarbeiter bei der Arbeit verwenden. WIP erfordert keine Änderungen an Ihrer Umgebung oder anderen Apps.

Windows Information Protection-Konfigurationselemente von Configuration Manager verwalten Folgendes:

- Die Liste der von WIP geschützten Apps
- Unternehmensnetzwerkadressen
- Schutzgrad
- Verschlüsselungseinstellungen
  
Weitere Informationen zum Konfigurieren von WIP mit Configuration Manager finden Sie unter:

- [Schützen von Unternehmensdaten mit Windows Information Protection (WIP)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip)
- [Erstellen und Bereitstellen einer Windows Information Protection-Richtlinie (WIP) mithilfe von Configuration Manager](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/create-wip-policy-using-configmgr)
- [Einschränkungen beim Verwenden von Windows Information Protection (WIP)](https://docs.microsoft.com/windows/security/information-protection/windows-information-protection/limitations-with-wip)

## <a name="see-also"></a>Weitere Informationen:  
[Konfigurationselemente für Geräte, die mit dem Configuration Manager-Client verwaltet werden](../../compliance/deploy-use/create-configuration-items.md)
