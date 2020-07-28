---
title: Verschlüsseln von macOS-Geräten mit FileVault-Datenträgerverschlüsselung mit Intune
titleSuffix: Microsoft Intune
description: Verschlüsseln Sie macOS-Geräte mithilfe von integrierten Verschlüsselungsmethoden wie FileVault, und verwalten Sie die Wiederherstellungsschlüssel für diese verschlüsselten Geräte über das Intune-Portal.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/17/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.assetid: ''
ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.openlocfilehash: cdfec1d82d68e97544172c56cecc416846b4a0f6
ms.sourcegitcommit: eccf83dc41f2764675d4fd6b6e9f02e6631792d2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2020
ms.locfileid: "86460483"
---
# <a name="use-filevault-disk-encryption-for--macos-with-intune"></a>Verwenden von FileVault-Verschlüsselung für macOS mit Intune

Intune unterstützt FileVault-Datenträgerverschlüsselung für macOS. FileVault ist ein Verschlüsselungsprogramm für ganze Datenträger, das im Lieferumfang von macOS enthalten ist. Verwenden Sie Intune, um FileVault auf Geräten zu konfigurieren, auf denen **macOS 10.13 oder höher** ausgeführt wird.

Verwenden Sie einen der folgenden Richtlinientypen, um FileVault auf Ihren verwalteten Geräten zu konfigurieren:

- **[Endpunktsicherheitsrichtlinie für FileVault für macOS](#create-endpoint-security-policy-for-filevault)** . Das FileVault-Profil in *Endpunktsicherheit* ist eine fokussierte Gruppe von Einstellungen, die für die Konfiguration von FileVault vorgesehen ist.

  Zeigen Sie die [FileVault-Einstellungen an, die in Profilen für Datenträger-Verschlüsselungsrichtlinien verfügbar sind](../protect/endpoint-security-disk-encryption-profile-settings.md).

- **[Gerätekonfigurationprofil für Endpunktschutz für macOS FileVault](#create-endpoint-security-policy-for-filevault)** . Die FileVault-Einstellungen gehören zu den verfügbaren Einstellungskategorien in Endpoint Protection unter macOS. Weitere Informationen zum Verwenden eines Gerätekonfigurationsprofils finden Sie unter [Erstellen eines Geräteprofils in Intune](../configuration/device-profile-create.md).

  Zeigen Sie die [FileVault-Einstellungen an, die in Endpunktschutzprofilen für die Gerätekonfigurationsrichtlinie verfügbar sind](../protect/endpoint-protection-macos.md#filevault).

Weitere Informationen zum Verwalten von BitLocker für Windows 10 finden Sie unter [Verwalten der BitLocker-Richtlinie](../protect/encrypt-devices.md).

> [!TIP]
> Intune beinhaltet einen integrierten [Verschlüsselungsbericht](encryption-monitor.md), in dem Details zum Verschlüsselungsstatus Ihrer verwalteten Geräte angezeigt werden.

Sobald Sie eine Richtlinie für die Geräteverschlüsselung mit FileVault erstellt haben, wird die Richtlinie in zwei Phasen auf die Geräte angewendet. Zuerst wird das Gerät vorbereitet, damit Intune den Wiederherstellungsschlüssel abrufen und sichern kann. Dies wird als Schlüsselhinterlegung bezeichnet. Sobald dieser Vorgang abgeschlossen ist, kann die Datenträgerverschlüsselung beginnen.

Zusätzlich zur Verwendung von Intune-Richtlinien zum Verschlüsseln eines Geräts mit FileVault können Sie Richtlinien auf einem verwalteten Gerät bereitstellen, um Intune zu ermöglichen, [die Verwaltung von FileVault zu übernehmen, wenn das Gerät vom Benutzer verschlüsselt wurde](#assume-management-of-filevault-on-previously-encrypted-devices). In diesem Szenario ist erforderlich, dass das Gerät die FileVault-Richtlinie von Intune empfängt. Anschließend muss der Benutzer seinen persönlichen Wiederherstellungsschlüssel in Intune hochladen.

Damit FileVault auf einem Gerät funktioniert, ist eine vom Benutzer genehmigte Geräteregistrierung erforderlich. Der Benutzer muss das Verwaltungsprofil manuell anhand von Systemeinstellungen genehmigen, damit die Registrierung als vom Benutzer genehmigt angesehen wird.

## <a name="permissions-to-manage-filevault"></a>Berechtigungen zum Verwalten von FileVault

Damit Sie FileVault in Intune verwalten können, muss Ihr Konto in Intune über die entsprechenden Berechtigungen für die [rollenbasierte Zugriffssteuerung](../fundamentals/role-based-access-control.md) (RBAC) verfügen.

Im Folgenden sind die FileVault-Berechtigungen aufgelistet, die zur Kategorie der **Remoteaufgaben** gehören, sowie die integrierten RBAC-Rollen für das Erteilen der jeweiligen Berechtigung:

- **Get FileVault key** (FileVault-Schlüssel erhalten):
  - Helpdesk-Operator
  - Endpoint security manager (Endpunktsicherheits-Manager)

- **Rotate FileVault key** (FileVault-Schlüssel rotieren)
  - Helpdesk-Operator

## <a name="create-device-configuration-policy-for-filevault"></a>Erstellen einer Gerätekonfigurationsrichtlinie für FileVault

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Geräte** > **Konfigurationsprofile** > **Profil erstellen** aus.

3. Legen Sie auf der Seite **Profil erstellen** die folgenden Optionen fest, und klicken Sie dann auf **Erstellen**:
   - **Plattform**: macOS
   - **Profil**: Endpoint Protection

   ![Auswählen des FileVault-Profils](./media/encrypt-devices-filevault/select-macos-filevault-dc.png)

4. Geben Sie auf der Seite **Grundlagen** die folgenden Eigenschaften ein:

   - **Name:** Geben Sie einen aussagekräftigen Namen für die Richtlinie ein. Benennen Sie Ihre Richtlinien so, dass Sie diese später leicht wiedererkennen. Ein guter Richtlinienname enthält beispielsweise den Profiltyp und die Plattform.

   - **Beschreibung:** Geben Sie eine Beschreibung für die Richtlinie ein. Diese Einstellung ist optional, wird jedoch empfohlen.

5. Wählen Sie auf der Seite **Konfigurationseinstellungen** die Option **FileVault** aus, um die verfügbaren Einstellungen aufzuklappen:

   > [!div class="mx-imgBorder"]
   > ![FileVault-Einstellungen](./media/encrypt-devices-filevault/filevault-settings.png)

6. Konfigurieren Sie die folgenden Einstellungen:
  
   - Wählen Sie für *FileVault* die Option **Ja** aus.

   - Wählen Sie für *Art des Wiederherstellungsschlüssels* die Option **Persönlicher Schlüssel** aus.

   - Fügen Sie für *Beschreibung des Hinterlegungsstandorts für den persönlichen Wiederherstellungsschlüssel* eine Meldung hinzu, um Benutzer zu informieren, [wie sie den Wiederherstellungsschlüssel für ihr Gerät abrufen können](#retrieve-a-personal-recovery-key). Diese Informationen können für Ihre Benutzer nützlich sein, wenn Sie die Einstellung für die Rotation persönlicher Wiederherstellungsschlüssel verwenden. Dadurch können regelmäßig automatisch neue Wiederherstellungsschlüssel für die Geräte generiert werden.

     Beispiel: Melden Sie sich auf einem beliebigen Gerät bei der Intune-Unternehmensportal-Website an, um verlorene oder kürzlich rotierte Wiederherstellungsschlüssel abrufen. Navigieren Sie im Portal zu *Geräte*, wählen Sie das Gerät aus, für das FileVault aktiviert ist, und klicken Sie dann auf *Wiederherstellungsschlüssel abrufen*. Dann wird der aktuelle Wiederherstellungsschlüssel angezeigt.

   Konfigurieren Sie die restlichen [FileVault-Einstellungen](endpoint-protection-macos.md#filevault) entsprechend Ihren Geschäftsanforderungen, und wählen Sie anschließend **Weiter** aus.

7. Klicken Sie auf der Seite **Bereich (Markierungen)** auf **Bereichstags auswählen**, um den Bereich „Markierungen auswählen“ zu öffnen, in dem Sie dem Profil Bereichstags zuweisen.

   Wählen Sie **Weiter** aus, um den Vorgang fortzusetzen.

8. Wählen Sie auf der Seite **Zuweisungen** die Gruppen aus, die dieses Profil erhalten sollen. Weitere Informationen zum Zuweisen von Profilen finden Sie unter „Zuweisen von Benutzer- und Geräteprofilen“.
Wählen Sie **Weiter** aus.

9. Klicken Sie, wenn Sie fertig sind, auf der Seite **Bewerten + erstellen** auf **Erstellen**. Das neue Profil wird in der Liste angezeigt, wenn Sie den Richtlinientyp für das Profil auswählen, das Sie erstellt haben.

## <a name="create-endpoint-security-policy-for-filevault"></a>Erstellen einer Endpunktsicherheitsrichtlinie für FileVault

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Endpunktsicherheit** > **Datenträgerverschlüsselung** > **Richtlinie erstellen** aus.

3. Geben Sie auf der Seite **Grundlagen** die folgenden Eigenschaften ein, und wählen Sie dann **Weiter** aus.
   - **Plattform**: macOS
   - **Profil**: FileVault

   ![Auswählen des FileVault-Profils](./media/encrypt-devices-filevault/select-macos-filevault-es.png)

4. Auf der Seite **Konfigurationseinstellungen**:
   1. Legen Sie *FileVault aktivieren* auf **Ja** fest.
   2. Als *des Wiederherstellungsschlüsseltyp* wird nur **Persönlicher Wiederherstellungsschlüssel** unterstützt.
   3. Konfigurieren Sie zusätzliche Einstellungen, um Ihre Anforderungen zu erfüllen.

   Fügen Sie ggf. eine Meldung hinzu, um Benutzer zu informieren, [wie sie den Wiederherstellungsschlüssel für ihr Gerät abrufen können](#retrieve-a-personal-recovery-key). Diese Informationen können für Ihre Benutzer nützlich sein, wenn Sie die Einstellung für die Rotation persönlicher Wiederherstellungsschlüssel verwenden. Dadurch können regelmäßig automatisch neue Wiederherstellungsschlüssel für die Geräte generiert werden.

   Beispiel: Melden Sie sich auf einem beliebigen Gerät bei der Intune-Unternehmensportal-Website an, um verlorene oder kürzlich rotierte Wiederherstellungsschlüssel abrufen. Navigieren Sie im Portal zu „Geräte“, wählen Sie das Gerät aus, für das FileVault aktiviert ist, und klicken Sie dann auf *Wiederherstellungsschlüssel abrufen*. Dann wird der aktuelle Wiederherstellungsschlüssel angezeigt.

5. Wenn Sie fertig sind mit dem Konfigurieren der Einstellungen, klicken Sie auf **Weiter**.

6. Klicken Sie auf der Seite **Bereich (Markierungen)** auf **Bereichstags auswählen**, um den Bereich „Markierungen auswählen“ zu öffnen, in dem Sie dem Profil Bereichstags zuweisen.

   Wählen Sie **Weiter** aus, um den Vorgang fortzusetzen.

7. Wählen Sie auf der Seite **Zuweisungen** die Gruppen aus, die dieses Profil erhalten sollen. Weitere Informationen zum Zuweisen von Profilen finden Sie unter „Zuweisen von Benutzer- und Geräteprofilen“.
Wählen Sie **Weiter** aus.

8. Klicken Sie, wenn Sie fertig sind, auf der Seite **Bewerten + erstellen** auf **Erstellen**. Das neue Profil wird in der Liste angezeigt, wenn Sie den Richtlinientyp für das Profil auswählen, das Sie erstellt haben.

## <a name="manage-filevault"></a>Verwalten von FileVault

Informationen zu Geräten, die die FileVault-Richtlinie erhalten, finden Sie unter [Überwachen der Datenträgerverschlüsselung](../protect/encryption-monitor.md).

Wenn Intune zum ersten Mal ein macOS-Gerät mithilfe von FileVault verschlüsselt, wird ein persönlicher Wiederherstellungsschlüssel erstellt. Bei der Verschlüsselung zeigt das Gerät dem Gerätebenutzer den persönlichen Schlüssel ein Mal an.

Bei verwalteten Geräten kann Intune eine Kopie des persönlichen Wiederherstellungsschlüssels hinterlegen. Durch die Hinterlegung von Schlüsseln können Intune-Administratoren die Schlüssel zum Schutz von Geräten rotieren, und die Benutzer können verlorene oder rotierte persönliche Wiederherstellungsschlüssel wiederherstellen.

Intune hinterlegt einen Wiederherstellungsschlüssel, wenn die Intune-Richtlinie ein Gerät verschlüsselt oder nachdem ein Benutzer seinen Wiederherstellungsschlüssel für das Gerät hochgeladen hat, das er manuell verschlüsselt hat.

Nachdem Intune den persönlichen Wiederherstellungsschlüssel hinterlegt hat:

- können Administratoren die FileVault-Wiederherstellungsschlüssel für ein beliebiges verwaltetes macOS-Gerät mithilfe des Intune-Verschlüsselungsberichts verwalten und rotieren.
- können Administratoren den persönlichen Wiederherstellungsschlüssel nur für verwaltete macOS-Geräte anzeigen, die als *unternehmenseigen* gekennzeichnet sind. Sie können nicht den Wiederherstellungsschlüssel für persönliche Geräte anzeigen.
- können Benutzer [ihren persönlichen Wiederherstellungsschlüssel über einen unterstützten Ort anzeigen und abrufen](#retrieve-a-personal-recovery-key). Beispielsweise kann der Benutzer die Remotegeräteaktion *Wiederherstellungsschlüssel abrufen* über die Unternehmensportalwebsite verwenden.

### <a name="assume-management-of-filevault-on-previously-encrypted-devices"></a>Übernehmen der Verwaltung von FileVault auf zuvor verschlüsselten Geräten

Intune kann die FileVault-Datenträgerverschlüsselung auf macOS-Geräten verwalten, die mithilfe von Intune-Richtlinien verschlüsselt wurden. Intune kann ebenfalls die Verwaltung von FileVault auf Geräten übernehmen, die von Benutzern und nicht über die Intune-Richtlinie verschlüsselt wurden.

#### <a name="prerequisites-to-assume-management-of-filevault"></a>Voraussetzungen zum Übernehmen der Verwaltung von FileVault

Zum Übernehmen der Verwaltung von zuvor verschlüsselten Geräten müssen die folgenden Bedingungen erfüllt werden:

1. **Eine FileVault-Richtlinie muss auf dem Gerät bereitgestellt werden**. Das zuvor verschlüsselte Geräte muss eine Richtlinie von Intune erhalten, die die FileVault-Datenträgerverschlüsselung aktiviert.

   In diesem Szenario wird das Gerät durch die Richtlinie weder entschlüsselt noch erneut verschlüsselt. Stattdessen ermöglicht die Richtlinie Intune, die Verwaltung der FileVault-Verschlüsselung zu übernehmen, die bereits auf dem Gerät aktiviert ist.  Sie können entweder die Datenträgerverschlüsselungsrichtlinie für Endpunktsicherheit oder eine Gerätekonfigurationsrichtlinie für Endpunktsicherheit zum Verschlüsseln von Geräten mit FileVault verwenden.

   Weitere Informationen finden Sie unter [Erstellen und Bereitstellen einer Richtlinie](#create-device-configuration-policy-for-filevault).

2. **Benutzer müssen ihre persönlichen Wiederherstellungsschlüssel in Intune hochladen**.  Nachdem das Gerät die FileVault-Richtlinie empfangen hat, weisen Sie den Benutzer des Geräts an, der das Gerät verschlüsselt hat, seinen persönlichen Wiederherstellungsschlüssel in Intune hochzuladen. Wenn der Schlüssel erfolgreich eingegeben wird, übernimmt Intune die Verwaltung der FileVault-Verschlüsselung und ein neuer persönlicher Wiederherstellungsschlüssel wird für das Gerät und den Benutzer erstellt.

   > [!IMPORTANT]
   > Intune benachrichtigt Benutzer nicht darüber, dass sie ihre persönlichen Wiederherstellungsschlüssel zum Abschließen der Verschlüsselung hochladen müssen. Stattdessen müssen Sie Ihre üblichen IT-Kommunikationskanäle verwenden, um Benutzer zu benachrichtigen, die ihre macOS-Geräte zuvor mit FileVault verschlüsselt haben, dass sie ihre persönlichen Wiederherstellungsschlüssel in Intune hochladen müssen.  
   >
   > Geräte können basierend auf Ihrer Konformitätsrichtlinie am Zugriff auf Unternehmensressourcen gehindert werden, bis Intune erfolgreich die Verwaltung der FileVault-Verschlüsselung übernommen hat.

#### <a name="upload-a-personal-recovery-key"></a>Hochladen eines persönlichen Wiederherstellungsschlüssels

Damit Intune FileVault auf einem zuvor verschlüsselten Gerät verwalten kann, muss der Gerätebenutzer die Unternehmensportalwebsite verwenden, um seinen aktuellen persönlichen Wiederherstellungsschlüssel für das Gerät in Intune hochzuladen.  Anschließend rotiert Intune den Schlüssel, um einen neuen persönlichen Wiederherstellungsschlüssel zu erstellen, der dann von Intune für zukünftige Wiederherstellungen gespeichert wird.

Auf der Unternehmensportalwebsite muss der Benutzer nach seine, verschlüsselten macOS-Gerät suchen und die Option **Wiederherstellungsschlüssel speichern** auswählen. Sobald der persönliche Wiederherstellungsschlüssel eingegeben wurde, versucht Intune, den Schlüssel zu rotieren, um einen neuen Schlüssel zu generieren. Die Rotation wird durchgeführt, um zu festzustellen, ob der richtige Schlüssel für das Gerät eingegeben wurde. Diese neue Schlüssel wird dann gespeichert und zur späteren Verwendung von Intune verwaltet, wenn der Benutzer sein Gerät wiederherstellen muss.

Wenn die Schlüsselrotation fehlschlägt, hat das Gerät entweder die FileVault-Richtlinie nicht verarbeitet oder es wurde ein falscher Schlüssel für das Gerät eingegeben.

Nach einer erfolgreichen Rotation kann der Benutzer [seinen neuen persönlichen Wiederherstellungsschlüssel über einen unterstützten Ort abrufen](#retrieve-a-personal-recovery-key).

 Weitere Informationen finden Sie im Artikel zum [Hochladen des persönlichen Wiederherstellungsschlüssels](../user-help/store-recovery-key.md).

> [!IMPORTANT]
> Für ein Gerät, das von einem Benutzer und nicht von Intune verschlüsselt wurde, kann Intune die FileVault-Verschlüsselung nicht verwalten, bis das Gerät eine FileVault-Richtlinie erhält und der Benutzer des Geräts erfolgreich seinen persönlichen Wiederherstellungsschlüssel hochgeladen hat.

### <a name="retrieve-a-personal-recovery-key"></a>Abrufen eines persönlichen Wiederherstellungsschlüssels

Für macOS-Geräte mit der von Intune verwalteter FileVault-Verschlüsselung können Endbenutzer ihre persönlichen Wiederherstellungsschlüssel (FileVault-Schlüssel) mit einem beliebigen Gerät über folgende Orte abrufen:

- Unternehmensportal-Website
- Unternehmensportal-App für iOS/iPadOS
- Android-Unternehmensportal-App
- Intune-App

Administratoren können persönliche Wiederherstellungsschlüssel für verschlüsselte macOS-Geräte anzeigen, die als *unternehmenseigene* Geräte gekennzeichnet sind. Sie können nicht den Wiederherstellungsschlüssel für persönliche Geräte anzeigen.

Das Gerät mit dem persönlichen Wiederherstellungsschlüssel muss bei Intune registriert und über Intune mit FileVault verschlüsselt sein. Über die iOS-Unternehmensportal-App, die Android-Unternehmensportal-App, die Android-Intune-App oder die Unternehmensportal-Website können Benutzer den **FileVault**-Wiederherstellungsschlüssel anzeigen, den sie für den Zugriff auf ihre Mac-Geräte benötigen.

Gerätebenutzer können **Geräte** > *verschlüsseltes und registriertes macOS-Gerät* > **Wiederherstellungsschlüssel abrufen** auswählen. Der Browser zeigt das Web-Unternehmensportal und darin den Wiederherstellungsschlüssel an.

### <a name="rotate-recovery-keys"></a>Rotieren von Wiederherstellungsschlüsseln

Intune unterstützt mehrere Optionen für das Rotieren oder Wiederherstellen von persönlichen Wiederherstellungsschlüsseln. Beispielsweise werden Schlüssel rotiert, wenn der aktuelle persönliche Schlüssel verloren geht oder als gefährdet eingestuft wird.

- **Automatische Rotation:** Als Administrator können Sie festlegen, dass durch die FileVault-Einstellung „Rotation für persönlichen Wiederherstellungsschlüssel“ in regelmäßigen Abständen automatisch neue Wiederherstellungsschlüssel erstellt werden. Wenn ein neuer Schlüssel für ein Gerät generiert wird, wird dieser nicht dem Benutzer angezeigt. Stattdessen muss der Benutzer den Schlüssel entweder bei einem Administrator anfragen oder über die Unternehmensportal-App abrufen.

- **Manuelle Rotation:** Als Administrator können Sie Informationen zu einem über FileVault verschlüsselten Gerät abrufen, das Sie mit Intune verwalten. Anschließend können Sie den Wiederherstellungsschlüssel für Unternehmensgeräte manuell rotieren. Wiederherstellungsschlüssel für persönliche Geräte können nicht rotiert werden.

  So rotieren Sie einen Wiederherstellungsschlüssel:

  1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

  2. Klicken Sie auf **Geräte** > **Alle Geräte**.

  3. Wählen Sie aus der Geräteliste das verschlüsselte Gerät aus, für das Sie den Schlüssel rotieren möchten. Klicken Sie dann unter „Überwachen“ auf  **Wiederherstellungsschlüssel**.
  
  4. Klicken Sie im Bereich „Wiederherstellungsschlüssel“ auf die Option **FileVault-Wiederherstellungsschlüssel rotieren**.

     Wenn das Gerät das nächste Mal bei Intune eincheckt, wird dann der persönliche Schlüssel rotiert. Falls erforderlich kann der neue Schlüssel vom Benutzer über das Unternehmensportal abgerufen werden.

### <a name="recover-recovery-keys"></a>Wiederherstellen von Wiederherstellungsschlüsseln

- **Administrator:** Administratoren können keine persönlichen Wiederherstellungsschlüssel für Geräte abrufen, die mit FileVault verschlüsselt sind.

- **Endbenutzer:** Endbenutzer können ihre persönlichen Wiederherstellungsschlüssel für ihre verwalteten Geräte über die Unternehmensportal-Website abrufen. Über die Unternehmensportal-App ist dies nicht möglich.

  So rufen Sie einen Wiederherstellungsschlüssel ab:
  
  1. Melden Sie sich auf einem beliebigen Gerät bei der *Intune-Unternehmensportal*-Website an.

  2. Navigieren Sie im Portal zu **Geräte**, und wählen Sie das macOS-Gerät aus, das über FileVault verschlüsselt ist.

  3. Klicken Sie auf **Wiederherstellungsschlüssel abrufen**. Dann wird der aktuelle Wiederherstellungsschlüssel angezeigt.

## <a name="next-steps"></a>Nächste Schritte

[Verwalten der BitLocker-Richtlinie](../protect/encrypt-devices.md)

[Überwachen der Datenträgerverschlüsselung](../protect/encryption-monitor.md)
