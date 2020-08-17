---
title: Aktivieren von Windows Defender | Microsoft-Dokumentation
description: Erfahren Sie, wie Windows Defender aktiviert wird, um auf Unternehmensressourcen zuzugreifen.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/07/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: d16dd2de-3ed5-474f-a04b-36dcd350162c
searchScope:
- User help
ROBOTS: ''
ms.reviewer: shburbid
ms.suite: ems
ms.custom: intune-enduser
ms.collection: ''
ms.openlocfilehash: a57010a5c8089b0ac979cf43c3706467d83faea2
ms.sourcegitcommit: 532a06163f462527254d23e7dc505b18c0c4f938
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/11/2020
ms.locfileid: "88110697"
---
# <a name="turn-on-windows-defender-to-access-company-resources"></a>Aktivieren von Windows Defender zum Zugriff auf Unternehmensressourcen

Für Organisationen ist es von größtem Interesse, dass die Geräte, über die auf die Ressourcen der Organisation zugegriffen wird, gesichert sind. Aus diesem Grund kann Ihre Organisation von Ihnen verlangen, [Windows Defender](https://www.microsoft.com/safety/pc-security/windows-defender.aspx) zu verwenden. Windows Defender ist eine im Lieferumfang von Windows enthaltene Antivirensoftware und hilft Ihnen, Ihr Gerät vor Viren, Schadsoftware und anderen Bedrohungen zu schützen. 

In diesem Artikel wird beschrieben, wie Sie Ihre Geräteeinstellungen aktualisieren, um die Antivirenanforderungen Ihrer Organisation zu erfüllen und Zugriffsprobleme zu beheben. 

## <a name="turn-on-windows-defender"></a>Aktivieren von Windows Defender
Führen Sie die folgenden Schritte aus, um Windows Defender auf Ihrem Gerät zu aktivieren. 

1. Klicken Sie auf das Menü **Start**.
2. Geben Sie **Gruppenrichtlinie** in die Suchleiste ein. Wählen Sie dann **Gruppenrichtlinie bearbeiten** aus den aufgeführten Vorschlägen aus. Der lokale Gruppenrichtlinien-Editor wird geöffnet.
4. Klicken Sie auf **Computerkonfiguration** > **Administrative Vorlagen** > **Windows-Komponenten** > **Windows Defender Antivirus**. 
5. Scrollen Sie zum Ende der Liste, und klicken Sie auf **Windows Defender Antivirus deaktivieren**.  
6. Wählen Sie **Deaktiviert** oder **Nicht konfiguriert** aus. Möglicherweise erscheint es Ihnen nicht logisch, diese Optionen zu aktivieren, da die Namen darauf hindeuten, dass Sie Windows Defender deaktivieren. Dabei stellen diese Optionen in Wirklichkeit sicher, dass Windows Defender aktiviert ist. 
7. Klicken Sie auf **Anwenden** > **OK**.  


## <a name="turn-on-real-time-and-cloud-delivered-protection"></a>Aktivieren des cloudbasierten Echtzeitschutzes

Führen Sie die folgenden Schritte aus, um den in der Cloud bereitgestellten Echtzeitschutz zu aktivieren. In Kombination schützen Sie diese Antivirenfeatures gegen Spyware und können Fixes für Probleme mit Schadsoftware über die Cloud bereitstellen. 

1. Klicken Sie auf das Menü **Start**.
2. Geben Sie **Windows-Sicherheit** in die Suchleiste ein. Wählen Sie den gleichnamigen Vorschlag aus. 
3. Klicken Sie auf **Virus & threat protection** (Viren- und Bedrohungsschutz).
4. Wählen Sie unter **Virus & threat protection settings** (Einstellungen für den Viren- und Bedrohungsschutz) auf **Einstellungen verwalten**.
5. Aktivieren Sie unter **Echtzeitschutz** und **Schutz in der Cloud** jeden Schalter, um die Einstellungen zu aktivieren. 

Wenn diese Optionen nicht auf dem Bildschirm angezeigt werden, sind sie möglicherweise ausgeblendet. Führen Sie die folgenden Schritte aus, um sie sichtbar zu machen.  

1. Klicken Sie auf das Menü **Start**.  
2. Geben Sie **Gruppenrichtlinie** in die Suchleiste ein. Wählen Sie dann **Gruppenrichtlinie bearbeiten** aus den aufgeführten Vorschlägen aus. Der lokale Gruppenrichtlinien-Editor wird geöffnet.
3. Klicken Sie auf **Computerkonfiguration** > **Administrative Vorlagen** > **Windows-Komponenten** > **Windows-Sicherheit** > **Viren- und Bedrohungsschutz**.
4. Klicken Sie auf **Hide the Virus and threat protection area** (Bereich für Viren- und Bedrohungsschutz ausblenden).
5. Klicken Sie auf **Deaktiviert** > **Anwenden** > **OK**.  

## <a name="update-your-antivirus-definitions"></a>Aktualisieren Sie Ihre Virusdefinitionen
Führen Sie die folgenden Schritte aus, um Ihre Virendefinitionen zu aktualisieren.  
1. Klicken Sie auf das Menü **Start**.
2. Geben Sie **Windows-Sicherheit** in die Suchleiste ein. Wählen Sie den gleichnamigen Vorschlag aus. 
3. Klicken Sie auf **Virus & threat protection** (Viren- und Bedrohungsschutz).
4. Klicken Sie unter **Virus & threat protection updates** (Updates für den Viren- und Bedrohungsschutz) auf **Auf Updates prüfen**. Wenn diese Option nicht auf dem Bildschirm angezeigt wird, führen Sie die ersten Schritte aus dem Absatz [Aktivieren des cloudbasierten Echtzeitschutzes](turn-on-defender-windows.md#turn-on-real-time-and-cloud-delivered-protection) aus. Versuchen Sie anschließend noch einmal, nach Updates zu suchen. 

## <a name="next-steps"></a>Nächste Schritte  

Benötigen Sie weitere Unterstützung? Kontaktieren Sie den Support Ihres Unternehmens. Die entsprechenden Kontaktinformationen finden Sie auf der [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980).
