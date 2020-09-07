---
title: 'Behandeln von Problemen mit E-Mail-Profilen in Microsoft Intune: Azure | Microsoft-Dokumentation'
description: Häufig auftretende Probleme und Lösungen für E-Mail-Profile in Microsoft Intune, darunter doppelte E-Mail-Profile und Fehler auf Android-Geräten mit Samsung KNOX Standard.
keywords: ''
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 07/20/2020
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology: ''
ms.assetid: f5c944ea-32a6-48af-bb57-16d5f1f3c588
ROBOTS: ''
ms.reviewer: tscott
ms.suite: ems
search.appverid: MET150
ms.custom: intune-classic
ms.collection: M365-identity-device-management
ms.openlocfilehash: 3d011d6111ede4bb5879e53e771d20b792bf00d3
ms.sourcegitcommit: fde92731a7e27c892d32c63f515cf19545e02ceb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "88995125"
---
# <a name="common-issues-and-resolutions-with-email-profiles-in-microsoft-intune"></a>Häufig auftretende Probleme und Lösungen für E-Mail-Profile in Microsoft Intune

Erfahren Sie mehr zu einigen häufig auftretenden Problemen mit E-Mail-Profilen und den entsprechenden Lösungen.

## <a name="users-are-repeatedly-prompted-to-enter-their-password"></a>Benutzer werden wiederholt zur Kennworteingabe aufgefordert

Benutzer werden wiederholt zur Eingabe des Kennworts für das E-Mail-Profil aufgefordert. Wenn für die Authentifizierung und Autorisierung der Benutzer Zertifikate verwendet werden, überprüfen Sie die Zuweisungen aller Zertifikatsprofile. In der Regel werden diese Zertifikatsprofile Benutzergruppen zugewiesen und nicht Gerätegruppen. Ist eines der Zertifikatsprofile nicht auf einen Benutzer ausgerichtet, versucht Intune, das E-Mail-Profil noch mal bereitzustellen.

Wenn die E-Mail-Profilkette Benutzergruppen zugewiesen wird, müssen Sie darauf achten, dass Ihre Zertifikatsprofile auch Benutzergruppen zugewiesen werden.

## <a name="profiles-deployed-to-device-groups-show-errors-and-latency"></a>Für Gerätegruppen bereitgestellte Profile zeigen Fehler und weisen eine hohe Wartezeit auf

E-Mail-Profile werden in der Regel Benutzergruppen zugewiesen. Es gibt jedoch manche Fälle, in denen sie Gerätegruppen zugewiesen werden.

- Zertifikatsbasierte E-Mail-Profile sollten beispielsweise nur Surface-Geräten zugewiesen werden, keinen Desktopgeräten. In diesem Szenario wären Gerätegruppen sinnvoll. Denken Sie jedoch daran, dass die Geräte als nicht konform angezeigt werden können, möglicherweise Fehler zurückgeben und Ihre E-Mail-Profile möglicherweise nicht sofort abrufen.

  In diesem Beispiel erstellen Sie das E-Mail-Profil und weisen das Profil Gerätegruppen zu. Das Gerät wird neu gestartet, und es kommt zu einer Verzögerung, bevor sich ein Benutzer anmelden kann. Während dieser Verzögerung wird Ihr PKCS-Zertifikatsprofil bereitgestellt, das Benutzergruppen zugewiesen ist. Da noch keine Benutzer vorhanden sind, führt das PKCS-Zertifikatsprofil dazu, dass das Gerät als nicht konform gilt. Möglicherweise werden in der Ereignisanzeige Fehler auf dem Gerät angezeigt.

  Damit das Gerät als konform gilt, muss sich ein Benutzer auf dem Gerät anmelden und eine Synchronisierung mit Intune durchführen, um die Richtlinien zu erhalten. Benutzer können manuell eine neue Synchronisierung durchführen oder auf die nächste reguläre warten.

- Angenommen, Sie nutzen dynamische Gruppen. Wenn die dynamischen Gruppen in Azure AD nicht sofort aktualisiert werden, werden diese Geräte möglicherweise als nicht konform angezeigt.

In diesen Szenarios entscheiden Sie, ob es wichtiger ist, Gerätegruppen zu verwenden oder alle Richtlinien als konform anzuzeigen.

## <a name="device-already-has-an-email-profile-installed"></a>Auf dem Gerät ist bereits ein E-Mail-Profil installiert

Wenn Benutzer vor der Registrierung bei Intune oder Microsoft 365 MDM ein E-Mail-Profil erstellen, funktioniert das von Intune bereitgestellte E-Mail-Profil möglicherweise nicht wie erwartet:

- **iOS/iPadOS**: Intune erkennt basierend auf dem Hostnamen und der E-Mail-Adresse ein vorhandenes doppeltes E-Mail-Profil. Das vom Benutzer erstellte E-Mail-Profil blockiert die Bereitstellung des von Intune erstellten Profils. Dieses Problem tritt häufig auf, da iOS-/iPadOS-Benutzer in der Regel zuerst ein E-Mail-Profil erstellen und dann die Registrierung vornehmen. In der Unternehmensportal-App wird der Benutzer als nicht konform aufgeführt, und der Benutzer wird möglicherweise aufgefordert, das E-Mail-Profil zu entfernen.

  Der Benutzer muss sein E-Mail-Profil, damit das Intune-Profil bereitgestellt werden kann. Weisen Sie die Benutzer an, sich erst zu registrieren und anschließend Intune die Bereitstellung des Profils zu gestatten, um dieses Problem zu vermeiden. Anschließend können die Benutzer ihr E-Mail-Profil erstellen.

- **Windows**: Intune erkennt basierend auf dem Hostnamen und der E-Mail-Adresse ein vorhandenes doppeltes E-Mail-Profil. Intune überschreibt das vorhandene vom Benutzer erstellte E-Mail-Profil.

- **Samsung KNOX Standard**: Intune identifiziert basierend auf der E-Mail-Adresse ein doppeltes E-Mail-Konto und überschreibt es mit dem Intune-Profil. Wenn der Benutzer dieses Konto konfiguriert, wird es erneut durch das Intune-Profil überschrieben. Dies kann für den Benutzer, dessen Kontokonfiguration überschrieben wird, verwirrend sein.

Samsung KNOX identifiziert das Profil nicht anhand des Hostnamens. Es wird empfohlen, nicht mehrere E-Mail-Profile zur Bereitstellung derselben E-Mail-Adresse auf unterschiedlichen Hosts zu erstellen, da diese sich gegenseitig überschreiben.

## <a name="error-0x87d1fde8-for-knox-standard-device"></a>Fehler „0x87D1FDE8“ für KNOX Standard-Gerät

**Problem**: Nach dem Erstellen und Bereitstellen eines Exchange Active Sync-E-Mail-Profils für Samsung KNOX Standard für verschiedene Android-Geräte melden diese den Fehler **0x87D1FDE8**, oder es wird ein **Fehler bei der Wiederherstellung** auf der Registerkarte „Eigenschaften“ > „Richtlinie“ des Geräts angezeigt.

Überprüfen Sie die Konfiguration Ihres EAS-Profils für Samsung KNOX und die Quellrichtlinie. Die Samsung-Option zum Synchronisieren von Notizen wird nicht mehr unterstützt, und diese Option sollte in Ihrem Profil nicht ausgewählt werden. Achten Sie darauf, dass Geräte genug Zeit hatten, um die Richtlinie zu verarbeiten (bis zu 24 Stunden).

## <a name="unable-to-send-images-from--email-account"></a>Senden von Bildern über E-Mail-Konto nicht möglich

Benutzer, deren E-Mail-Konten automatisch konfiguriert wurden, können keine Bilder von ihren Geräten senden. Dies ist der Fall, wenn die Option **E-Mail-Versand aus Anwendungen von Drittanbietern zulassen** nicht aktiviert ist.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Geräte** > **Konfigurationsprofile** aus.
3. Klicken Sie auf Ihr E-Mail-Profil > **Eigenschaften** > **Einstellungen**.
4. Legen Sie die Einstellung **E-Mail-Versand aus Anwendungen von Drittanbietern zulassen** auf **Aktivieren** fest.

## <a name="next-steps"></a>Nächste Schritte

Fordern Sie [Hilfe beim Microsoft-Support](../fundamentals/get-support.md) an, oder nutzen Sie die [Communityforen](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune).
