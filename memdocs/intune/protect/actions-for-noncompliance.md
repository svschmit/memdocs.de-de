---
title: 'Nicht konforme Nachrichten und Aktionen mit Microsoft Intune: Azure | Microsoft-Dokumentation'
description: Erstellen einer E-Mail-Benachrichtigung für nicht konforme Geräte. Hinzufügen von Aktionen, nachdem ein Gerät als nicht konform markiert wurde, z.B. das Hinzufügen einer Toleranzperiode, in der das Gerät konform werden soll, oder das Erstellen eines Zeitplans, um den Zugriff zu blockieren, bis das Gerät konform ist. Verwenden Sie dazu Microsoft Intune in Azure.
keywords: ''
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/26/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology: ''
ms.suite: ems
search.appverid: MET150
ms.reviewer: samyada
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.openlocfilehash: fff21eac61f7b68e00989aefc1f9ea6dc3ad7c0a
ms.sourcegitcommit: 302556d3b03f1a4eb9a5a9ce6138b8119d901575
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/27/2020
ms.locfileid: "83989315"
---
# <a name="configure-actions-for-noncompliant-devices-in-intune"></a>Konfigurieren von Aktionen für nicht konforme Geräte in Intune

Für Geräte, die nicht Ihren Konformitätsrichtlinien oder -regeln entsprechen, können Sie **Aktionen bei Inkompatibilität** hinzufügen. Dieses Feature konfiguriert eine zeitlich angeordnete Sequenz an Aktionen wie z. B. E-Mails an den Endbenutzer.

## <a name="overview"></a>Übersicht

Standardmäßig enthält jede Konformitätsrichtlinie die Aktion bei Nichtkonformität von **Gerät als nicht konform markieren** mit einem Zeitplan von null Tagen (**0**). Wenn Intune feststellt, dass ein Gerät nicht konform ist, markiert Intune das Gerät sofort als „nicht konform“. Das kann das Gerät durch den [bedingten Zugriff](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) von Azure Active Directory (AD) blockiert werden.

Durch die Konfiguration von **Aktionen bei Nichtkonformität** gewinnen Sie die Flexibilität, zu entscheiden, wie und wann mit nicht konformen Geräten zu verfahren ist. Sie können beispielsweise auswählen, dass das Gerät nicht sofort blockiert werden soll, und dem Benutzer eine Toleranzperiode einräumen, in der er dafür sorgen kann, dass das Gerät konform wird.

Für jede Aktion, die Sie festlegen können, können Sie einen Zeitplan konfigurieren, der bestimmt, wann diese Aktion wirksam wird, basierend auf der Anzahl der Tage, nachdem das Gerät als nicht konform markiert wurde. Sie können auch mehrere Instanzen einer Aktion konfigurieren. Wenn Sie mehrere Instanzen einer Aktion in einer Richtlinie festlegen, wird die Aktion zu dieser später geplanten Zeit erneut ausgeführt, wenn das Gerät weiterhin nicht konform ist.

Nicht alle Aktionen sind für alle Plattformen verfügbar.

## <a name="available-actions-for-noncompliance"></a>Verfügbare Aktionen bei Nichtkonformität

Im folgenden finden Sie die verfügbaren Aktionen für die Nichtkonformität. Sofern nicht anders angegeben, ist jede Aktion für alle Plattformen verfügbar, die von Intune unterstützt werden:

- **Mark device non-compliant** (Markieren des Geräts als nicht konform): Standardmäßig wird diese Aktion für jede Konformitätsrichtlinie festgelegt und hat einen Zeitplan von null (**0**) Tagen, wobei Geräte sofort als nicht konform markiert werden.

  Wenn Sie den Standardzeitplan ändern, geben Sie eine Toleranzperiode an, innerhalb derer ein Benutzer Probleme beheben oder die Konformität herstellen kann, ohne als nicht konform markiert zu werden.

- **E-Mail an Endbenutzer senden:** Diese Aktion sendet eine E-Mail-Benachrichtigung an den Benutzer.
Wenn Sie diese Aktion aktivieren:

  - Wählen Sie eine *Benachrichtigungsvorlage* aus, die mit dieser Aktion gesendet wird. Sie müssen eine [Benachrichtigungsvorlage](#create-a-notification-message-template) erstellen, bevor Sie dieser Aktion eine solche zuweisen können. Wenn Sie die benutzerdefinierte Benachrichtigung erstellen, passen Sie den Betreff und den Nachrichtentext an und können das Firmenlogo, den Firmennamen und zusätzliche Kontaktinformationen einbeziehen.
  - Wählen Sie aus, die Nachricht an weitere Empfänger zu senden, indem Sie mindestens eine Ihrer Azure AD-Gruppen auswählen.

Wenn die E-Mail gesendet wurde, bezieht Intune Einzelheiten zu dem nicht konformen Gerät in die E-Mail-Benachrichtigung ein.

- **Nicht konformes Gerät remote sperren:** Verwenden Sie diese Aktion, um eine Remotesperre für ein Gerät auszugeben. Zum Entsperren des Geräts wird der Benutzer dann zur Eingabe einer PIN oder eines Kennworts aufgefordert. Weitere Informationen zur Funktion [Remotesperre](../remote-actions/device-remote-lock.md).

  Folgende Plattformen unterstützen diese Aktion:
  - Android:
    - Android-Geräteadministrator
    - Android Enterprise-Gerätebesitzer
    - Android Enterprise: Arbeitsprofil
    - Android Enterprise-Kioskgeräte
  - iOS/iPadOS
  - macOS
  - Windows 10 Mobile
  - Windows Phone 8.1 und höher

- **Retire the noncompliant device** (Nicht konformes Gerät deaktivieren): Diese Aktion entfernt alle Unternehmensdaten vom Gerät und dann das Gerät aus der Intune-Verwaltung. Damit ein Gerät nicht versehentlich gelöscht wird, unterstützt diese Aktion einen minimalen Zeitplan von **30** Tagen.

  Folgende Plattformen unterstützen diese Aktion:
  - Android:
    - Android-Geräteadministrator
    - Android Enterprise-Gerätebesitzer
    - Android Enterprise: Arbeitsprofil
  - iOS/iPadOS
  - macOS
  - Windows 10 Mobile
  - Windows Phone 8.1 und höher

  Weitere Informationen zum [Außerbetriebnehmen](../remote-actions/devices-wipe.md#retire) von Geräten.

- **Pushbenachrichtigung an Endbenutzer senden**: Konfigurieren Sie diese Aktion so, dass eine Pushbenachrichtigung über die Nichtkonformität an ein Gerät über die Unternehmensportal-App oder die Intune-App auf dem Gerät gesendet wird.

  Folgende Plattformen unterstützen diese Aktion:
  - Android:
    - Android-Geräteadministrator
    - Android Enterprise-Gerätebesitzer
    - Android Enterprise: Arbeitsprofil
  - iOS/iPadOS

  Die Pushbenachrichtigung wird gesendet, wenn ein Gerät zum ersten Mal bei Intune eingecheckt wird und als nicht konform zur Konformitätsrichtlinie eingestuft wird. Wenn ein Benutzer die Benachrichtigung auswählt, wird die Unternehmensportal-App oder Intune-App geöffnet, und es werden Informationen darüber angezeigt, warum sie nicht konform sind. Der Benutzer kann dann Maßnahmen ergreifen, um das Problem zu beheben. Die Nachrichtendetails über die Nichtkonformität werden von Intune generiert und können nicht angepasst werden.

  > [!IMPORTANT]
  > Weder Intune noch die Unternehmensportal-App oder die Microsoft Intune-App kann die Zustellung von Pushbenachrichtigungen garantieren. Benachrichtigungen können, wenn überhaupt, erst mit mehrstündiger Verspätung eintreffen. Dies gilt auch, wenn Benutzer Pushbenachrichtigungen deaktiviert haben.
  >
  > Verlassen Sie sich bei dringenden Nachrichten nicht auf diese Benachrichtigungsmethode.

  Jede Instanz der Aktion sendet ein einziges Mal eine Benachrichtigung. Um dieselbe Benachrichtigung erneut von einer Richtlinie aus zu senden, konfigurieren Sie zusätzliche Instanzen der Aktion in dieser Richtlinie, jede mit einem anderen Zeitplan.
  
  Sie können z. B. die erste Aktion für null Tage planen und dann eine zweite Instanz der Aktion hinzufügen, die für drei Tage geplant ist. Diese Verzögerung vor der zweiten Benachrichtigung gibt dem Benutzer einige Tage Zeit, um das Problem zu beheben und die zweite Benachrichtigung zu vermeiden.

  Um zu vermeiden, dass Benutzer mit zu vielen doppelten Nachrichten belästigt werden, überprüfen und optimieren Sie, welche Konformitätsrichtlinien eine Pushbenachrichtigung bei Nichtkonformität enthalten, und überprüfen Sie die Zeitpläne, um zu vermeiden, dass wiederholte Benachrichtigungen für dasselbe Problem zu oft gesendet werden.

  Zu berücksichtigen:
  - Bei einer einzelnen Richtlinie, die mehrere Instanzen einer für denselben Tag festgelegten Pushbenachrichtigung enthält, wird für diesen Tag nur eine einzige Benachrichtigung gesendet.

  - Wenn mehrere Konformitätsrichtlinien die gleichen Konformitätsbedingungen und die Pushbenachrichtigungsaktion mit demselben Zeitplan enthalten, werden mehrere Benachrichtigungen am selben Tag an dasselbe Gerät gesendet.

## <a name="before-you-begin"></a>Vorbereitung

Sie können [Aktionen für die Nichtkonformität](#add-actions-for-noncompliance) hinzufügen, wenn Sie die Richtlinie für die Gerätekonformität konfigurieren, oder Sie fügen sie später durch Bearbeiten der Richtlinie hinzu. Sie können zu jeder Richtlinie zusätzliche Aktionen hinzufügen, um Ihren Anforderungen zu entsprechen. Denken Sie daran, dass jede Konformitätsrichtlinie automatisch die Standardaktion für die Nichtkonformität enthält, die Geräte als nicht konform markiert, wobei der Zeitplan auf null Tage festgelegt ist.

Wenn Sie Gerätekonformitätsrichtlinien verwenden, um den Zugriff auf Unternehmensressourcen durch Geräte zu blockieren, muss der bedingte Zugriff von Azure AD eingerichtet sein. Anleitungen dazu finden Sie unter [Bedingter Zugriff in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal) oder [Gängige Möglichkeiten für die Verwendung des bedingten Zugriffs mit Intune](conditional-access-intune-common-ways-use.md).

Plattformspezifische Informationen zum Erstellen einer Gerätekonformitätsrichtlinie finden Sie hier:

- [Android](compliance-policy-create-android.md)
- [Android-Arbeitsprofile](compliance-policy-create-android-for-work.md)
- [iOS](compliance-policy-create-ios.md)
- [macOS](compliance-policy-create-mac-os.md)
- [Windows](compliance-policy-create-windows.md)

## <a name="create-a-notification-message-template"></a>Erstellen einer Benachrichtigungsvorlage

Zum Senden einer E-Mail an Ihre Benutzer müssen Sie eine Benachrichtigungsvorlage erstellen. Wenn ein Gerät nicht konform ist, werden die Einzelheiten, die Sie in die Vorlage eingeben, in den von Ihnen an die Benutzer gesendeten E-Mails angezeigt.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.
2. Wählen Sie **Geräte** > **Konformitätsrichtlinien** > **Benachrichtigung** > **Benachrichtigung erstellen** aus.
3. Geben Sie dann unter *Grundlagen* die folgenden Informationen an:

   - **Name**
   - **Antragsteller**
   - **Message**

4. Konfigurieren Sie ebenfalls unter *Grundlagen* die folgenden Optionen für die Benachrichtigung, bei denen standardmäßig *Aktiviert* ausgewählt ist:

   - **E-Mail-Kopfzeile: Unternehmenslogo einschließen**
   - **E-Mail-Fußzeile: Unternehmensnamen einschließen**
   - **E-Mail-Fußzeile: Kontaktinformationen einschließen**

   Das Logo, das Sie für das Branding des Unternehmensportals hochladen, wird für E-Mail-Vorlagen verwendet. Weitere Informationen zum Branding des Unternehmensportals finden Sie unter [Anpassen des Unternehmensbrandings](../apps/company-portal-app.md#customizing-the-user-experience).

   ![Beispiel einer Benachrichtigung zur Konformität in Intune](./media/actions-for-noncompliance/actionsfornoncompliance-1.PNG)

   Wählen Sie **Weiter** aus, um den Vorgang fortzusetzen.

5. Überprüfen Sie Ihre Konfigurationen unter **Überprüfen und Erstellen**, um sicherzustellen, dass die Benachrichtigungsvorlage einsatzbereit ist. Wählen Sie **Erstellen** aus, um die Erstellung der Benachrichtigung abzuschließen.

> [!NOTE]
> Sie können auch eine bereits erstellte Benachrichtigungsvorlage auswählen und deren Informationen **bearbeiten**, um die Vorlage zu aktualisieren.

## <a name="add-actions-for-noncompliance"></a>Hinzufügen von Aktionen bei Nichtkonformität

Wenn Sie eine Konformitätsrichtlinie für Geräte erstellen, erstellt Intune automatisch eine Aktion für Nichtkonformität. Wenn ein Gerät Ihre Konformitätsrichtlinie nicht einhält, wird das Gerät von dieser Aktion als „nicht konform“ gekennzeichnet. Sie können anpassen, wie lange das Gerät als „nicht konform“ gekennzeichnet wird. Diese Aktion kann nicht entfernt werden.

Sie können beim Erstellen einer Konformitätsrichtlinie oder Aktualisieren einer vorhandenen Konformitätsrichtlinie weitere optionale Aktionen hinzufügen.

1. Melden Sie sich beim [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431) an.

2. Wählen Sie **Geräte** > **Konformitätsrichtlinien** > **Richtlinien**, anschließend eine Ihrer Richtlinien und dann **Eigenschaften** aus.

   Haben Sie noch keine Richtlinie? Erstellen Sie eine Richtlinie für [Android](compliance-policy-create-android.md), [iOS](compliance-policy-create-ios.md), [Windows](compliance-policy-create-windows.md) oder eine andere Plattform.

   > [!NOTE]
   > JAMF-Geräte und Geräte als Teil von Gerätegruppen können zu diesem Zeitpunkt keine Konformitätsaktionen empfangen.

3. Wählen Sie **Aktionen für Nichtkonformität** > **Hinzufügen** aus.

4. Wählen Sie Ihre **Aktion** aus:

   - **E-Mail an Endbenutzer senden:** Senden Sie dem Benutzer eine E-Mail, wenn das Gerät nicht konform ist. Ferner gilt Folgendes:
     - Wählen Sie die zuvor erstellte **Nachrichtenvorlage** aus
     - Geben Sie durch die Auswahl von Gruppen **zusätzliche Empfänger** ein

   - **Nicht konformes Gerät remote sperren:** Sperren Sie das Gerät, wenn es nicht konform ist. Durch diese Aktion wird der Benutzer zur Eingabe einer PIN oder eines Kennworts gezwungen, um das Gerät zu entsperren

   - **Retire the noncompliant device** (Nicht konformes Gerät deaktivieren): Wenn das Gerät nicht konform ist, entfernen Sie alle Unternehmensdaten vom Gerät, und entfernen Sie das Gerät aus der Intune-Verwaltung.

   - **Pushbenachrichtigung an Endbenutzer senden**: Konfigurieren Sie diese Aktion so, dass eine Pushbenachrichtigung über die Nichtkonformität an ein Gerät über die Unternehmensportal-App oder die Intune-App auf dem Gerät gesendet wird.

5. Konfigurieren Sie einen **Zeitplan**: Geben Sie die Anzahl von Tagen (0 bis 365) nach der Nichtkonformität ein, nach der die Aktion auf Benutzergeräten ausgelöst werden soll. (*Nicht konformes Gerät zurückziehen* unterstützt mindestens 30 Tage.) Nach Ablauf dieser Nachfrist können Sie eine Richtlinie für [bedingten Zugriff](conditional-access-intune-common-ways-use.md) erzwingen. Wenn Sie als Anzahl von Tagen **0** (null) eingeben, wird der bedingte Zugriff **sofort** wirksam. Wenn beispielsweise ein Gerät nicht konform ist, können Sie mithilfe des bedingten Zugriffs sofort den Zugriff auf E-Mails, SharePoint und andere Organisationsressourcen blockieren.

   Wenn Sie eine Konformitätsrichtlinie erstellen, wird automatisch die Aktion **Gerät als nicht konform markieren** erstellt und auf **0** Tage (sofort) festgelegt. Durch diese Aktion wird das Gerät beim Einchecken sofort als nicht konform ausgewertet. Wenn Sie auch den bedingten Zugriff verwenden, wird dieser umgehend wirksam. Wenn Sie eine Nachfrist zulassen möchten, ändern Sie den **Zeitplan** für die Aktion **Gerät als nicht konform markieren**.

   Sie möchten den Benutzer außerdem in Ihrer Konformitätsrichtlinie benachrichtigen. Fügen Sie die Aktion **E-Mail an Endbenutzer senden** hinzu. Legen Sie für diese Aktion **E-Mail senden** den **Zeitplan** auf zwei Tage fest. Wird das Gerät oder der Endbenutzer an Tag zwei weiterhin als nicht konform ausgewertet, wird Ihre E-Mail an Tag zwei gesendet. Wenn Sie dem Benutzer an Tag fünf der Nichtkonformität erneut eine E-Mail senden möchten, fügen Sie eine weitere Aktion hinzu, und legen Sie den **Zeitplan** auf fünf Tage fest.

  Weitere Informationen zur Konformität und den integrierten Aktionen finden Sie in der [Konformitätsübersicht](device-compliance-get-started.md).

6. Klicken Sie zum Speichern Ihrer Änderungen auf **Hinzufügen** > **OK**.

## <a name="next-steps"></a>Nächste Schritte

[Überwachen von Intune-Richtlinien zur Gerätekompatibilität](compliance-policy-monitor.md).
