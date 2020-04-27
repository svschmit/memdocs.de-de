---
title: Planen der Berechtigungen von Zertifikatvorlagen
titleSuffix: Configuration Manager
description: Erfahren Sie mehr über das Planen der Berechtigungen, die Sie für das Konfigurieren von Zertifikatvorlagen benötigen, die Configuration Manager verwendet.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: eab0e09d-b09e-4c14-ab14-c5f87472522e
author: mestew
ms.author: mstewart
manager: dougeby
ms.openlocfilehash: 075d371a334f26a788c656fe85ec01ae2338eb26
ms.sourcegitcommit: 1442a4717ca362d38101785851cd45b2687b64e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "82074825"
---
# <a name="planning-for-certificate-template-permissions-for-certificate-profiles-in-configuration-manager"></a>Planen der Berechtigungen von Zertifikatvorlagen für Zertifikatprofile in Configuration Manager

*Gilt für: Configuration Manager (Current Branch)*


Die folgenden Informationen können Ihnen beim Planen der Konfiguration von Berechtigungen für die Zertifikatvorlagen helfen, die von Configuration Manager beim Bereitstellen von Zertifikatprofilen verwendet werden.  

## <a name="default-security-permissions-and-considerations"></a>Standardsicherheitsberechtigungen und Überlegungen  
 Die Standardsicherheitsberechtigungen, die für die Zertifikatvorlagen erforderlich sind, die von Configuration Manager zum Anfordern von Zertifikaten für Benutzer und Geräte verwendet werden, lauten wie folgt:  

- „Lesen“ und „Anmelden“ für das Konto, das vom NDES-Anwendungspool verwendet wird  

- „Lesen“ für das Konto, mit dem die Configuration Manager-Konsole ausgeführt wird  

  Weitere Informationen zu diesen Sicherheitsberechtigungen finden Sie unter [Konfigurieren der Zertifikatinfrastruktur](../deploy-use/certificate-infrastructure.md).  

  Indem Sie diese Standardkonfiguration verwenden, können Benutzer und Geräte Zertifikate nicht direkt von den Zertifikatvorlagen anfordern, und Sie können festlegen, dass alle Anforderungen vom Registrierungsdienst für Netzwerkgeräte initiiert werden müssen. Dies ist eine wichtige Einschränkung, da diese Zertifikatvorlagen mit **Informationen werden in der Anforderung angegeben** für den Zertifikatantragsteller konfiguriert werden müssen. Das bedeutet, dass die Gefahr des Identitätswechsels besteht, wenn von einem nicht autorisierten Benutzer oder von einem gefährdeten Gerät ein Zertifikat angefordert wird. Mit der Standardkonfiguration muss eine Anforderung vom Registrierungsdienst für Netzwerkgeräte initiiert werden. Die Gefahr des Identitätswechsels bleibt jedoch bestehen, wenn der Dienst, unter dem der Registrierungsdienst für Netzwerkgeräte ausgeführt wird, gefährdet ist. Wenn Sie diese Gefahr vermeiden möchten, befolgen Sie alle bewährten Sicherheitsmethoden für den Registrierungsdienst für Netzwerkgeräte und den Computer, auf dem dieser Rollendienst ausgeführt wird.  

  Wenn die Standardsicherheitsberechtigungen Ihre Unternehmensanforderungen nicht erfüllen, haben Sie eine weitere Option zum Konfigurieren der Sicherheitsberechtigungen in den Zertifikatvorlagen: Sie können die Berechtigungen „Lesen“ und „Registrieren“ für Benutzer und Computer hinzufügen.  

## <a name="adding-read-and-enroll-permissions-for-users-and-computers"></a>Hinzufügen der Berechtigungen „Lesen“ und „Anmelden“ für Benutzer und Computer  
 Das Hinzufügen der Berechtigungen „Lesen“ und „Registrieren“ für Benutzer und Computer kann angemessen sein, wenn das Infrastrukturteam Ihrer Zertifizierungsstelle von einem separaten Team verwaltet wird und dieses wünscht, dass mithilfe von Configuration Manager überprüft wird, ob Benutzer über ein gültiges Konto für Active Directory Domain Services verfügen, bevor es diesen Benutzern ein Zertifikatprofil zur Anforderung eines Benutzerzertifikats sendet. Bei dieser Konfiguration müssen Sie mindestens eine Sicherheitsgruppe angeben, die die Benutzer enthält, und diesen Gruppen die Berechtigungen „Lesen“ und „Anmelden“ für die Zertifikatvorlagen zuweisen. In diesem Szenario wird die Sicherheitssteuerung vom Zertifizierungsstellenadministrator verwaltet.  

 Entsprechend können Sie mindestens eine Sicherheitsgruppe angeben, die die Computerkonten enthält, und diesen Gruppen die Berechtigungen „Lesen“ und „Anmelden“ für die Zertifikatvorlagen zuweisen. Wenn Sie ein Computerzertifikatprofil für einen Computer bereitstellen, der ein Domänenmitglied ist, müssen dem Computerkonto dieses Computers die Berechtigungen „Lesen“ und „Anmelden“ zugewiesen werden. Diese Berechtigungen sind nicht erforderlich, wenn der Computer kein Mitglied einer Domäne ist, also wenn es sich beispielsweise um einen Arbeitsgruppencomputer oder um ein persönliches mobiles Gerät handelt.  

 Obwohl bei dieser Konfiguration eine zusätzliche Sicherheitsmaßnahme zum Einsatz kommt, wird diese Methode nicht empfohlen. Der Grund ist, dass die angegebenen Benutzer oder Besitzer der Geräte Zertifikate unabhängig von Configuration Manager anfordern und Werte für den Zertifikatantragsteller angeben können, mit deren Hilfe die Identität eines anderen Benutzers oder Geräts angenommen werden kann.  

 Zudem tritt bei der Zertifikatanforderung standardmäßig ein Fehler auf, wenn Sie Konten angeben, die zu dem Zeitpunkt, zu dem das Zertifikat angefordert wird, nicht authentifiziert werden können. Ein Fehler bei der Zertifikatanforderung tritt beispielsweise auf, wenn sich der Server, auf dem der Registrierungsdienst für Netzwerkgeräte ausgeführt wird, in einer Active Directory-Gesamtstruktur befindet, die von der Gesamtstruktur, die den Standortsystemserver für den Zertifikatregistrierungspunkt enthält, als nicht vertrauenswürdig eingestuft wird. Sie können den Zertifikatregistrierungspunkt konfigurieren, um den Vorgang fortzusetzen, wenn ein Konto aufgrund einer fehlenden Antwort von einem Domänencontroller nicht authentifiziert werden kann. Allerdings ist dies keine bewährte Sicherheitsmethode.  

 Wenn der Zertifikatregistrierungspunkt für die Überprüfung von Kontoberechtigungen konfiguriert wurde und ein Domänencontroller verfügbar ist, von dem die Authentifizierungsanforderung abgelehnt wird (wenn das Konto beispielsweise gesperrt oder gelöscht wurde), tritt bei der Zertifikatregistrierungsanforderung ein Fehler auf.  

#### <a name="to-check-for-read-and-enroll-permissions-for-users-and-domain-member-computers"></a>So prüfen Sie, ob Benutzer und Computer, die Mitglieder einer Domäne sind, über die Berechtigungen „Lesen“ und „Anmelden“ verfügen  

1.  Erstellen Sie auf dem Standortsystemserver, auf dem der Zertifikatregistrierungspunkt gehostet wird, den DWORD-Registrierungsschlüssel mit dem Wert „0“: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SCCM\CRP\SkipTemplateCheck  

2.  Gehen Sie wie folgt vor, um die Berechtigungsprüfung zu umgehen, wenn ein Konto aufgrund einer fehlenden Antwort von einem Domänencontroller nicht authentifiziert werden kann:  

    -   Erstellen Sie auf dem Standortsystemserver, auf dem der Zertifikatregistrierungspunkt gehostet wird, den DWORD-Registrierungsschlüssel mit dem Wert „1“: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\SCCM\CRP\SkipTemplateCheckOnlyIfAccountAccessDenied  

3.  Fügen Sie bei der ausstellenden Zertifizierungsstelle auf der Registerkarte **Sicherheit** in den Eigenschaften für die Zertifikatsvorlage mindestens eine Sicherheitsgruppe hinzu, um den Benutzer- oder Gerätekonten die Berechnungen „Lesen“ oder „Anmelden“ zu gewähren.  
