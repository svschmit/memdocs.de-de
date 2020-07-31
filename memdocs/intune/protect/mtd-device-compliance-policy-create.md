---
title: Erstellen einer Mobile Threat Defense-Gerätekonformitätsrichtlinie (MTD) mit Microsoft Intune
titleSuffix: Microsoft Intune
description: Erstellen Sie eine Intune-Konformitätsrichtlinie für Geräte, die die Bedrohungsstufen Ihres MTD-Partners verwendet, um zu ermitteln, ob ein mobiles Gerät auf Unternehmensressourcen zugreifen darf.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/28/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: 5d12254f-ffab-4792-b19c-ab37f5e02f35
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: 88f8a2ff04f536370f613341170e7fae0a808ff6
ms.sourcegitcommit: 19f5838eb3eb8724d22382f36f9564ac9a978b97
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/29/2020
ms.locfileid: "87365524"
---
# <a name="create-mobile-threat-defense-mtd-device-compliance-policy-with-intune"></a>Erstellen einer Mobile Threat Defense-Gerätekompatibilitätsrichtlinie (MTD) mit Intune

Intune mit MTD hilft Ihnen dabei, Bedrohungen zu erkennen und Risiken auf mobilen Geräten zu bewerten. Sie können eine Regel für eine Intune-Gerätekompatibilitätsrichtlinie erstellen, mit der das Risiko bewertet wird, um zu ermitteln, ob das Gerät kompatibel ist oder nicht. Anschließend können Sie eine [Richtlinie für bedingten Zugriff](create-conditional-access-intune.md) verwenden, um den Zugriff auf Dienste basierend auf der Gerätekonformität zu blockieren.

> [!NOTE]
> Diese Informationen gelten für alle Mobile Threat Defense-Partner.

## <a name="before-you-begin"></a>Vorbereitung

Beim Einrichten von MTD haben Sie in der MTD-Partnerkonsole eine Richtlinie erstellt, die verschiedene Bedrohungen als hoch, mittel und niedrig klassifiziert. Als Nächstes legen Sie die Mobile Threat Defense-Stufe in der Intune-Gerätekonformitätsrichtlinie fest.

Voraussetzungen für die Gerätekompatibilitätsrichtlinie mit MTD:

- Einrichten der MTD-Integration in Intune

## <a name="to-create-an-mtd-device-compliance-policy"></a>So erstellen Sie eine MTD-Gerätekonformitätsrichtlinie

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Endpunktsicherheit** > **Gerätekonformität** > **Richtlinie erstellen** aus.

3. Wählen Sie die **Plattform** aus, und klicken Sie dann auf **Erstellen**.

4. Geben Sie unter **Grundlagen** einen **Namen** und optional eine **Beschreibung** der Gerätekonformitätsrichtlinie an. Wählen Sie **Weiter** aus, um den Vorgang fortzusetzen.


5. Erweitern Sie die Optionen unter **Konformitätseinstellungen**, und konfigurieren Sie die **Geräteintegrität**. Wählen Sie aus der Dropdownliste **Anfordern, dass das Gerät höchstens der angegebenen Gerätebedrohungsstufe entspricht** die gewünschte Bedrohungsstufe für mobile Geräte aus.

   - **Secured** (Geschützt): Diese Stufe ist die sicherste Einstellung. Solange auf einem Gerät Bedrohungen vorhanden sind, ist kein Zugriff auf Unternehmensressourcen möglich. Wenn Bedrohungen gefunden werden, wird das Gerät als nicht kompatibel bewertet.

   - **Niedrig:** Das Gerät ist konform, wenn nur Bedrohungen auf niedriger Stufe vorliegen. Durch Bedrohungen höherer Stufen wird das Gerät in einen nicht kompatiblen Status versetzt.

   - **Mittel**: Das Gerät ist konform, wenn auf dem Gerät Bedrohungen niedriger oder mittlerer Stufe gefunden werden. Wenn auf dem Gerät Bedrohungen hoher Stufen erkannt werden, wird es als nicht kompatibel bewertet.

   - **Hoch**: Diese Bedrohungsstufe bietet die geringste Sicherheit. Es werden alle Bedrohungsstufen zugelassen, und Mobile Threat Defense wird nur zu Berichtszwecken verwendet. Auf Geräten muss mit dieser Einstellung die MTD-App aktiviert sein.

6. Wählen Sie **Weiter** aus, um mit den **Zuweisungen** fortzufahren. Wählen Sie die Gruppen aus, die dieses Profil erhalten sollen. Weitere Informationen zum Zuweisen von Profilen finden Sie unter [Zuweisen von Benutzer- und Geräteprofilen](../configuration/device-profile-assign.md).

   Wählen Sie **Weiter** aus.

7. Klicken Sie, wenn Sie fertig sind, auf der Seite **Bewerten + erstellen** auf **Erstellen**. Das neue Profil wird in der Liste angezeigt, wenn Sie den Richtlinientyp für das Profil auswählen, das Sie erstellt haben.

> [!IMPORTANT]
> Wenn Sie Richtlinien für bedingten Zugriff für Office 365 oder andere Dienste erstellen, wird die Konformitätsbewertung ausgewertet, und auf nicht konformen Geräten wird der Zugriff auf Unternehmensressourcen blockiert, bis die Bedrohung auf dem Gerät beseitigt ist.

## <a name="to-assign-an-mtd-device-compliance-policy"></a>So weisen Sie eine MTD-Gerätekonformitätsrichtlinie zu

So weisen Sie Benutzern eine Gerätekonformitätsrichtlinie zu oder ändern die Zuweisung:

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Endpunktsicherheit** > **Gerätekonformität** aus.

3. Wählen Sie die Richtlinie aus, die Sie Benutzern zuweisen möchten, und wählen Sie danach **Eigenschaften** aus.

4. Wählen Sie **Bearbeiten** für die gewünschten Zuweisungen aus, und verwenden Sie dann die verfügbaren Optionen, um Gruppen *einzuschließen* oder *auszuschließen*, die diese Richtlinie erhalten sollen.  

5. Wählen Sie **Überprüfen und speichern** aus, um die Zuweisung abzuschließen. Wenn Sie die Zuweisung speichern, wird die Richtlinie für die ausgewählten Benutzer bereitgestellt, und Ihre Geräte werden auf Konformität ausgewertet.

## <a name="next-steps"></a>Nächste Schritte

[Aktivieren von Mobile Threat Defense in Intune](mtd-connector-enable.md)
