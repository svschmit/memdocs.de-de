---
title: Erstellen von Windows Embedded-Anwendungen
titleSuffix: Configuration Manager
description: Erfahren Sie, was Sie beim Erstellen und Bereitstellen von Anwendungen für Windows Embedded-Geräte berücksichtigen müssen.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 16acfd63-0c40-424c-82f4-8c63f7f1c30b
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: bec9765e5152863bb8b55a0b75f1e5c2fc580550
ms.sourcegitcommit: bbf820c35414bf2cba356f30fe047c1a34c5384d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/21/2020
ms.locfileid: "81689838"
---
# <a name="create-windows-embedded-applications-with-configuration-manager"></a>Erstellen von Windows Embedded-Anwendungen mit Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*

Zusätzlich zu den anderen Configuration Manager-Anforderungen und -Verfahren zum Erstellen einer Anwendung müssen beim Erstellen und Bereitstellen von Anwendungen für Windows Embedded-Geräte die folgenden Aspekte berücksichtigt werden.  

## <a name="general-considerations"></a>Allgemeine Aspekte  

-   Beim Bereitstellen von Anwendungen für Windows Embedded-Geräte mit aktivierten Schreibfiltern können Sie angeben, ob der Schreibfilter auf dem Gerät während der App-Bereitstellung deaktiviert werden soll. Sie können zudem auswählen, dass der Schreibfilter nach der App-Bereitstellung neu gestartet werden soll. Wenn der Schreibfilter nicht deaktiviert ist, wird die Software auf einem temporären Overlay bereitgestellt. Das bedeutet, dass die Software bei einem Neustart des Geräts nicht mehr installiert wird, es sei denn, die Beibehaltung der Änderungen wird durch eine andere Bereitstellung erzwungen.  

-   Stellen Sie beim Bereitstellen einer Anwendung auf einem Windows Embedded-Gerät sicher, dass das Gerät Mitglied einer Sammlung ist, für die ein Wartungsfenster konfiguriert ist. So können Sie verwalten, wann der Schreibfilter deaktiviert bzw. aktiviert ist und wann das Gerät neu gestartet wird.  

-   Das Verhalten der Schreibfilter wird über das Kontrollkästchen **Änderungen zum Stichtag oder während eines Wartungsfensters ausführen (erfordert Neustart)** gesteuert.  

## <a name="tips-for-deploying-applications"></a>Tipps zum Bereitstellen von Anwendungen  

**Verwenden von erforderlichen Anwendungen anstelle von verfügbaren Anwendungen für Windows Embedded-Geräte mit aktivierten Schreibfiltern.** Da Benutzer auf einem Windows Embedded-Gerät, für das Schreibfilter aktiviert sind, keine Apps aus dem Softwarecenter installieren können, sollten Sie anstelle von **verfügbaren** Anwendungen immer Anwendungen bereitstellen, die auch wirklich **erforderlich** sind. Normalerweise ist dies kein Problem, da auf Computern mit Windows Embedded-Betriebssystem häufig eine einzelne Anwendung ausgeführt wird, die für mehrere Benutzer gleich ausgeführt werden muss. Daher verfügen diese Geräte über einen hohen Verwaltungsgrad und sind von der IT-Abteilung gesperrt. Erforderliche Anwendungen sind für dieses Szenario gut geeignet.

 Falls Benutzer auf eingebetteten Geräten jedoch mehr als eine Anwendung ausführen, wenn Schreibfilter aktiviert sind, sollten Sie diese Benutzer über die folgenden Einschränkungen informieren:  

-   Benutzer können erforderliche Software nicht über das Softwarecenter installieren.  

-   Benutzer können ihre Geschäftszeiten im Softwarecenter auf der Registerkarte „Optionen“ nicht ändern.  

-   Benutzer können die Installation einer erforderlichen Anwendung nicht verschieben.  

Benutzer mit geringen Rechten können sich nicht während eines Wartungszeitraums anmelden, wenn Configuration Manager Änderungen für Softwareinstallationen und Updates übernimmt. Während dieses Zeitraums wird Benutzern die Meldung angezeigt, dass das Gerät nicht verfügbar ist, weil es gewartet wird.  

**Vermeiden der Bereitstellung von Anwendungen auf Windows Embedded-Geräten mit aktivierten Schreibfiltern, wenn die Anwendungen von Benutzern erfordern, dass den Lizenzbedingungen zugestimmt wird.** Wenn die Schreibfilter deaktiviert sind, sodass von Configuration Manager Software auf eingebetteten Geräten installiert werden kann, können sich Benutzer mit geringen Rechten auf dem Gerät nicht anmelden. Wenn die Installation die Zustimmung zu den Lizenzbedingungen durch den Benutzer erfordert, ist dies nicht möglich, und bei der Installation tritt ein Fehler auf. Stellen Sie sicher, dass Sie keine Software auf Windows Embedded-Geräten bereitstellen, wenn für die Installation eine Benutzerinteraktion erforderlich ist. Sie können die Liste „Zutreffende Plattformen“ zum Filtern dieser Betriebssysteme verwenden.  
