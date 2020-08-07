---
title: Windows Autopilot mit Co-Verwaltung
titleSuffix: Configuration Manager
description: Verwenden Sie Windows Autopilot mit Co-Verwaltung in Configuration Manager, um das Einrichten neuer Windows 10-Geräte zu vereinfachen.
ms.date: 07/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-comanage
ms.topic: conceptual
ms.assetid: e3e3c97f-5945-49ab-a622-9f6fe6b9737e
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: f77cb76e3cfd9c932a6f3789f98e5616cdaa27eb
ms.sourcegitcommit: e2cf3b80d1a4523d98542ccd7bba2439046c3830
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/04/2020
ms.locfileid: "87546432"
---
# <a name="windows-autopilot-with-co-management"></a>Windows Autopilot mit Co-Verwaltung

Das Erhalten eines neuen Windows 10-Geräts ist spannend. Es kann jedoch einige Zeit dauern, bis Sie alle Ihre Einstellungen und Apps so konfiguriert haben, dass Sie produktiv damit arbeiten können. Co-Verwaltung löst dieses Gerätebereitstellungsproblem mit Windows Autopilot.

Autopilot bietet in den folgenden Situationen eine vereinfachte Umgebung für Sie und Ihre Benutzer:
- Einrichten und Vorkonfigurieren neuer Windows 10-Geräte  
- Zurücksetzen, Wiederverwenden und Wiederherstellen vorhandener Geräte  

Autopilot reduziert Zeit, Ressourcen und Komplexität, die mit der Bereitstellung, Verwaltung und Außerbetriebnahme von Geräten verbunden sind. Gleichzeitig ist die Erfahrung für Ihre Benutzer vom ersten Start an optimiert und einfach.

Windows Autopilot unterstützt mehrere Szenarien, die alle durch Co-Verwaltung maximiert werden:

- Benutzer können ihre eigenen Bereitstellungen neuer Geräte entweder in Active Directory mit Azure AD-Hybrideinbindung oder in Azure Active Directory (Azure AD) einbinden.  

- Sie können neue Gerätebereitstellungen in Azure AD für gemeinsam genutzte Geräte und Kioske einrichten, die sich selbst bereitstellen.  

- Verwenden Sie mit Windows Autopilot für vorhandene Geräte Configuration Manager, um ein vorhandenes Gerät von Windows 7 und Active Directory zu Windows 10 und Azure AD zu migrieren.  

Im folgenden Video erläutern und zeigen Senior Programm Manager Danny Guillory und Principal Programm Manager Andrew McMurray Windows Autopilot mit Co-Verwaltung:

> [!VIDEO https://channel9.msdn.com/Series/Endpoint-Zone/Using-Windows-Autopilot-with-Co-Management/player]



## <a name="benefits"></a>Vorteile

Wenn Sie Co-Verwaltung und Autopilot gemeinsam nutzen, stellen Sie sicher, dass neue Geräte, die in Ihr Netzwerk aufgenommen werden, den gleichen Verwaltungszustand aufweisen. In diesem Setup werden Geräte bei Intune registriert und verfügen über einen Configuration Manager-Client.  Es ermöglicht Ihnen die Verwendung des neuen Windows 10-Bereitstellungsmodells und hilft Ihnen, die Notwendigkeit der Erstellung, Wartung und Aktualisierung benutzerdefinierter Betriebssystemimages zu vermeiden. 

In all diesen Szenarien können Sie [Co-Verwaltung automatisch durch Intune aktivieren](how-to-prepare-Win10.md). Diese Automatisierung unterstützt den Bereitstellungsvorgang sowie die fortlaufende Verwaltung des Geräts.

Mit Autopilot müssen Sie sich keine Gedanken über Images und Treiber machen. Konzentrieren Sie sich auf die Bereitstellung von Geräten durch diesen automatisierten Prozess mit Intune und Configuration Manager über Co-Verwaltung.


So können Co-Verwaltung und Autopilot in Kombination Sie jetzt unterstützen:

#### <a name="reduce-time-costs-and-complexity"></a>Verringern von Zeit, Kosten und Komplexität
Windows Autopilot verwendet die OEM-optimierte Version von Windows 10, die auf dem Gerät vorinstalliert ist. Diese Konfiguration erspart Unternehmen den Aufwand, für jedes verwendete Gerätemodell benutzerdefinierte Images und Treiber verwalten zu müssen. Anstatt das Gerät mit einem neuen Image zu versehen, transformieren Sie die vorhandene Windows 10-Installation in einen „geschäftsbereiten“ Zustand. Einstellungen und Richtlinien werden angewendet, Apps installiert, und die Edition von Windows 10 wird geändert. Beispielsweise ein Upgrade von Windows 10 Pro auf Windows 10 Enterprise, damit Sie erweiterte Funktionen unterstützen können.

#### <a name="improve-the-user-experience"></a>Verbessern der Benutzererfahrung
Die bestmögliche Benutzererfahrung führt zu der geringsten Unterbrechung und erleichtert es Benutzern, sich auf ihre Arbeit zu konzentrieren. Windows Autopilot bietet einen einfachen Ansatz, um Ihre Benutzer dabei zu unterstützen, sich mit wenigen einfachen Mausklicks und ihren Azure AD-Anmeldeinformationen schnell einzurichten. Für viele Unternehmen mit zahlreichen Mitarbeitern in Außenstellen verwenden Sie Windows Autopilot, um neue Geräte direkt vom Hersteller auszuliefern.

#### <a name="use-autopilot-and-configuration-manager-to-migrate-existing-windows-7-devices-to-windows-10"></a>Verwenden von Autopilot und Configuration Manager zum Migrieren vorhandener Windows 7-Geräte zu Windows 10
Mit Windows Autopilot für vorhandene Geräte erstellen Sie eine Konfigurationsdatei und stellen diese mit einer Configuration Manager-Tasksequenz bereit. Dieser Prozess migriert vorhandene Geräte ganz einfach von Windows 7 zu Windows 10. Sie verwenden in Configuration Manager ein Windows 10-Signaturimage und wenden es dann mit der Autopilot-Konfiguration auf das vorhandene Windows 7-Gerät an. Wenn der Benutzer das Gerät startet, verwendet er den benutzergesteuerten Autopilot-Onboardingprozess.

Dies sind die Schritte für Autopilot für vorhandene Geräte:

![Prozessübersicht für Windows Autopilot für vorhandene Geräte](media/autopilot-for-existing-devices.png)

1. Bereitstellen der Gruppenrichtlinie, um bekannte Ordner an OneDrive umzuleiten
2. Generieren der Autopilot-Konfigurationsdatei
3. Bereitstellen der Tasksequenz, um ein Upgrade auf Windows 10 durchzuführen
4. Der Windows 10-Computer durchläuft Autopilot beim ersten Start

#### <a name="modernizing-device-provisioning-for-all-types-of-workers"></a>Modernisieren der Gerätebereitstellung für alle Arten von Mitarbeitern
Mit Autopilot können Sie nun eine unbeaufsichtigte Betriebssystembereitstellung auf unbemannten oder gemeinsam genutzten Geräten im Selbstbereitstellungsmodus bereitstellen. Dieses Setup erfüllt die Anforderungen der verschiedenen Typen von Mitarbeitern. Außerdem sorgt die Zurücksetzungsfunktion von Windows Autopilot dafür, dass die erneute Bereitstellung eines Geräts für einen neuen Benutzer einfach und unkompliziert ist. Dieser Prozess vereinfacht die bisher schwierige Aufgabe, wenn Sie Saison- oder Leiharbeiter beschäftigen. 



## <a name="case-study"></a>Fallstudie

Der deutsche Logistik- und Speditionsdienstleister DB Schenker steigert mit Autopilot die Produktivität der Mitarbeiter und entlastet seine IT-Teams bei der täglichen Arbeit im Support. DB Schenker hat die traditionelle Imageverwendung aufgegeben und durch Bereitstellungen über die Cloud ersetzt. Das Unternehmen verwendet jetzt Azure AD-Einbindung und Intune, um neue Geräte schnell einzurichten und auszuführen. 

Mitarbeiter im Außendienst müssen keine Zeit mehr damit verschwenden, an einen Ort mit IT-Dienstleistungen zu reisen. Stattdessen verwendet DB Schenker jetzt Windows Autopilot. Das Unternehmen versendet die Hardware für seine Mitarbeiter direkt vom Hersteller an die jeweilige lokale Außenstelle. Der Mitarbeiter verbindet das neue Gerät mit dem Internet und meldet sich mit seinen Azure AD-Anmeldeinformationen an. Das Gerät stellt dann eine Verbindung mit den Anwendungen und Diensten her, die die IT-Abteilung von DB Schenker dem individuellen Profil des Benutzers zuordnet.

Weitere Informationen finden Sie unter [Global logistics firm centralizes IT, unites employees with modern digital workplace](https://customers.microsoft.com/story/db-schenker-travel-transportation-windows-10) (Globales Logistikunternehmen zentralisiert IT, vereint Mitarbeiter mit modernem digitalen Arbeitsplatz).



## <a name="value-proposition"></a>Leistungsversprechen

Schaffen Sie Zufriedenheit in Ihrer Organisation, indem Sie eine bessere Benutzererfahrung für Ihre Benutzer bereitstellen. Verwenden Sie Windows Autopilot, um Kosten zu senken. Schaffen Sie Zeit für andere Projekte, um mehr Wertschöpfung und Wirkung für Ihr Unternehmen zu erzielen.



## <a name="configure"></a>Konfigurieren

Weitere Informationen finden Sie in den folgenden Artikeln:

[Verwenden von Intune zum Erstellen von Windows Autopilot-Profilen](https://docs.microsoft.com/intune/enrollment-autopilot)

[Windows Autopilot für vorhandene Geräte](../../autopilot/existing-devices.md)
