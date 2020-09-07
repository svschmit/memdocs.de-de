---
title: Kennwortanforderungen für bei Intune registrierte Geräte | Microsoft-Dokumentation
description: In diesem Artikel wird beschrieben, wie Sie die Kennwortanforderungen Ihrer Organisation erfüllen, um auf deren Netzwerk zugreifen zu können.
keywords: ''
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/27/2020
ms.topic: end-user-help
ms.prod: ''
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology: ''
ms.assetid: efb3c261-1f6c-4d39-bfa4-18661f8c59c7
searchScope:
- User help
ROBOTS: ''
ms.custom: intune-enduser, contperfq1
ms.collection: ''
ms.openlocfilehash: b9bdada31e280c7fdc8a5d7a5a0a4a7ab7d36ae3
ms.sourcegitcommit: 41e6e6b7f5c2a87aaf7f23d90d0f175dd63c0579
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/28/2020
ms.locfileid: "89057286"
---
# <a name="device-password-requirements"></a>Anforderungen für Gerätekennwörter  

Sie erhalten eine Meldung vom Unternehmensportal, wenn Ihr Gerätekennwort nicht den Sicherheitsanforderungen Ihrer Organisation entspricht. Kennwortanforderungen werden eingerichtet, um Sie und die Daten Ihrer Organisation vor einem unbefugten Zugriff zu schützen. Sie erhalten möglicherweise erst dann Zugriff auf das Netzwerk Ihrer Organisation, nachdem Sie ein sichereres Kennwort erstellt haben.  

Das Unternehmensportal sendet eine Nachricht pro Kennwortanforderung, sodass Sie möglicherweise mehrere Nachrichten gleichzeitig erhalten. Tippen Sie auf eine beliebige Meldung, um weitere Details (sofern vorhanden) anzuzeigen.  

In diesem Artikel werden alle kennwortbezogenen Meldungen aufgelistet, die Sie erhalten können, und es werden zusätzliche Details zu jeder Anforderung für die einzelnen Betriebssystemplattformen bereitstellt.     

## <a name="change-password-passcode-pin"></a>Kennwort ändern, Passcode, PIN  

Im Allgemeinen können Sie für den Zugriff auf Kennworteinstellungen die App-Einstellungen auf Ihrem Gerät öffnen und nach *Sperrbildschirm* oder *Sicherheitseinstellungen* suchen.  

In den folgenden Artikeln wird beschrieben, wie das Gerätekennwort auf den einzelnen Betriebssystemplattformen aktualisiert wird. Die neuesten Anleitungen für Ihr konkretes Gerät finden Sie in der Hilfedokumentation des Geräteherstellers.  

- [Machen Sie Ihr Gerät mit dem richtigen Kennwort sicherer](set-or-change-your-password-windows.md)  
- [Festlegen des Passcodes für ein iOS-Gerät](set-or-change-your-passcode-ios.md)  
- [Festlegen der PIN oder des Kennworts für ein Android-Gerät](set-your-pin-or-password-android.md)  


> [!IMPORTANT]
> Wenn Sie Ihr Kennwort geändert haben, um die Anforderungen zu erfüllen, aber weiterhin Benachrichtigungen erhalten, starten Sie das Gerät neu.  

Wenden Sie sich an den für Sie zuständigen IT-Supportmitarbeiter, wenn Sie spezifische Fragen zu den Kennwortanforderungen Ihrer Organisation haben.  

## <a name="windows-10-password-requirements"></a>Kennwortanforderungen unter Windows 10

| Nachricht | Beheben |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Das Kennwort ist erforderlich. | Legen Sie ein Kennwort fest. Ihre Organisation verlangt, dass Sie ein Kennwort eingeben, um das Gerät zu entsperren. |
| Das Kennwort ist zu einfach. |  Stellen Sie sicher, dass Ihr Kennwort keine sequenziellen oder sich wiederholenden Zahlen wie „1234“ oder „1111“ enthält. |
| Das Kennwort ist zu kurz.| Aktualisieren Sie das Kennwort, oder legen Sie ein Kennwort mit mehr Zeichen fest. Ihre Organisation verlangt, dass Ihr Kennwort eine bestimmte Länge hat. Die tatsächlichen Vorgaben können variieren, aber die erforderliche Länge beträgt mindestens 4 und maximal 16 Zeichen. |
| Password must only contain numbers. (Das Kennwort darf nur Zahlen enthalten.) | Legen Sie ein Kennwort fest, das nur Zahlen enthält.|
| Password must only contain alphanumeric characters. (Das Kennwort darf nur alphanumerische Zeichen enthalten.) | Legen Sie ein Kennwort fest, das eine Mischung aus Zahlen und Buchstaben enthält.|
| Password must contain complex characters. (Das Kennwort muss komplexe Zeichen enthalten.) | Fügen Sie komplexe Zeichen, also z. B. Zahlen, Großbuchstaben und Symbole wie `$`, `%` und `#`, hinzu. Ihre Organisation verlangt eine Mischung aus Buchstaben, Zahlen und nicht alphanumerischen Zeichen, damit andere Benutzer das Kennwort nicht erraten können.|  
| Das Kennwort ist abgelaufen. | Legen Sie ein neues Kennwort fest. Ihre Organisation verlangt, dass Sie Ihr Kennwort nach einer bestimmten Anzahl von Tagen ändern. |
| Das Kennwort wurde erst kürzlich verwendet. | Wählen Sie ein Kennwort aus, das Sie zuvor noch nicht verwendet haben. Ihre Organisation verlangt, dass eine bestimmte Zeitspanne verstrichen ist, bevor Sie ein Kennwort wiederverwenden. |

## <a name="ios-passcode-requirements"></a>iOS-Passcodeanforderungen

| Nachricht | Beheben |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Passcode is required. (Es ist ein Passcode erforderlich.)| Legen Sie einen Passcode fest. Ihre Organisation verlangt, dass Sie einen Passcode eingeben, um das Gerät zu entsperren. |
| Passcode is too simple. (Der Passcode ist zu einfach.) |  Stellen Sie sicher, dass Ihr Passcode keine sequenziellen oder sich wiederholenden Zahlen wie „1234“ oder „1111“ enthält. |
| Passcode is too short. (Der Passcode ist zu kurz.) | Aktualisieren Sie den Passcode, oder legen Sie einen Passcode mit mehr Zeichen fest. Ihre Organisation verlangt, dass Ihr Passcode eine bestimmte Länge hat. Die tatsächlichen Vorgaben können variieren, aber die erforderliche Länge beträgt mindestens 4 und maximal 14 Zeichen. Wenn Sie Ihren Passcode ändern, wird möglicherweise eine Aufforderung von Apple angezeigt, die Sie darüber informiert, dass Sie 6 oder mehr Zeichen eingeben müssen. Diese Meldung ist nur eine Empfehlung des Apple-Systems. Wenn Ihre Organisation nur einen Passcode mit 4 oder 5 Zeichen verlangt, müssen Sie keinen 6-stelligen Passcode eingeben.|  
| Password must only contain numbers. (Der Passcode darf nur Zahlen enthalten.) | Legen Sie einen Passcode fest, der nur Zahlen enthält.|
| Passcode must only contain alphanumeric characters. (Der Passcode darf nur alphanumerische Zeichen enthalten.)| Legen Sie einen Passcode fest, der eine Mischung aus Zahlen und Buchstaben enthält.|
| Passcode must contain non-alphanumeric characters. (Der Passcode muss nicht alphanumerische Zeichen enthalten.) | Fügen Sie Sonderzeichen wie `&`, `!`, `$`, `%` und `#` hinzu. Ihre Organisation verlangt eine Mischung aus Buchstaben, Zahlen und nicht alphanumerischen Zeichen, damit andere Benutzer den Passcode nicht erraten können.|
| Der Passcode ist abgelaufen. | Legen Sie ein neues Kennwort fest. Ihre Organisation verlangt, dass Sie Ihr Kennwort nach einer bestimmten Anzahl von Tagen ändern. |
| Your passcode was used too recently. (Der Passcode wurde erst kürzlich verwendet.)| Wählen Sie einen Passcode aus, den Sie zuvor noch nicht verwendet haben. Ihre Organisation verlangt, dass eine bestimmte Zeitspanne verstrichen ist, bevor Sie einen Passcode wiederverwenden. |
|Touch ID or Face ID authentication required. (Die Touch ID- oder Face ID-Authentifizierung ist erforderlich.) | Set up Touch ID or Face ID. (Richten Sie eine Touch ID oder Face ID ein.) Ihre Organisation verlangt, dass Sie sich mit einer dieser Methoden authentifizieren, bevor Sie AutoAusfüllen für Kennwörter oder Kreditkarteninformationen verwenden. | 

## <a name="macos-password-requirements"></a>Kennwortanforderungen unter macOS
| Nachricht | Beheben |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Das Kennwort ist erforderlich. | Legen Sie ein Kennwort fest. Ihre Organisation verlangt, dass Sie ein Kennwort eingeben, um das Gerät zu entsperren. |
| Das Kennwort ist zu einfach.|  Stellen Sie sicher, dass Ihr Kennwort keine sequenziellen oder sich wiederholenden Zahlen wie „1234“ oder „1111“ enthält. |
| Das Kennwort ist zu kurz. | Aktualisieren Sie das Kennwort, oder legen Sie ein Kennwort mit mehr Zeichen fest. Ihre Organisation verlangt, dass Ihr Kennwort eine bestimmte Länge hat.|
| Password must only contain numbers. (Das Kennwort darf nur Zahlen enthalten.) | Legen Sie ein Kennwort fest, das nur Zahlen enthält.|
| Password must only contain alphanumeric characters. (Das Kennwort darf nur alphanumerische Zeichen enthalten.) | Legen Sie ein Kennwort fest, das eine Mischung aus Zahlen und Buchstaben enthält.|
| Password must contain non-alphanumeric characters. (Das Kennwort muss nicht alphanumerische Zeichen enthalten.) | Fügen Sie Sonderzeichen wie `&`, `!`, `$`, `%` und `#` hinzu. Ihre Organisation verlangt eine Mischung aus Buchstaben, Zahlen und nicht alphanumerischen Zeichen, damit andere Benutzer das Kennwort nicht erraten können.|
| Das Kennwort ist abgelaufen. | Legen Sie ein neues Kennwort fest. Ihre Organisation verlangt, dass Sie Ihr Kennwort nach einer bestimmten Anzahl von Tagen ändern. |
| Das Kennwort wurde erst kürzlich verwendet. | Wählen Sie ein Kennwort aus, das Sie zuvor noch nicht verwendet haben. Ihre Organisation verlangt, dass eine bestimmte Zeitspanne verstrichen ist, bevor Sie ein Kennwort wiederverwenden. |

## <a name="android-password-requirements"></a>Kennwortanforderungen unter Android
| Nachricht | Beheben |
|-----------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Das Kennwort ist erforderlich. | Set a password or PIN. (Legen Sie ein Kennwort oder eine PIN fest.) Ihre Organisation verlangt, dass Sie ein Kennwort eingeben, um das Gerät zu entsperren. |
| Das Kennwort ist zu einfach. |  Stellen Sie sicher, dass Ihr Kennwort oder Ihre PIN keine sequenziellen oder sich wiederholenden Zahlen wie „1234“ oder „1111“ enthält. |
| Das Kennwort ist zu kurz. | Aktualisieren Sie das Kennwort, oder legen Sie ein Kennwort mit mehr Zeichen fest. Ihre Organisation verlangt, dass Ihr Kennwort eine bestimmte Länge hat.|
| Das Kennwort muss Ziffern enthalten. | Legen Sie ein Kennwort oder eine PIN fest, die Zahlen enthält.|
| Das Kennwort muss Buchstaben enthalten. | Legen Sie ein Kennwort fest, das Buchstaben aus dem Alphabet enthält.|
| Password must contain alphanumeric characters. (Das Kennwort muss alphanumerische Zeichen enthalten.) | Legen Sie ein Kennwort fest, das eine Mischung aus Zahlen und Buchstaben enthält.|
| Password must contain alphanumeric characters. (Das Kennwort muss alphanumerische Zeichen und Symbole enthalten.) | Legen Sie ein Kennwort fest, das eine Kombination aus Buchstaben, Zahlen und Sonderzeichen enthält (z. B. `&`, `!`, `$`, `%` und `#`). |
| Password must use biometric technology. (Für das Kennwort muss Biometrietechnologie verwendet werden.)| Richten Sie Ihr Gerät für die Verwendung der biometrischen Authentifizierung (z. B. Fingerabdruck oder Gesichtserkennung) ein.
| Das Kennwort ist abgelaufen. | Legen Sie ein neues Kennwort fest. Ihre Organisation verlangt, dass Sie Ihr Kennwort nach einer bestimmten Anzahl von Tagen ändern. |
| Das Kennwort wurde erst kürzlich verwendet. | Wählen Sie ein Kennwort aus, das Sie zuvor noch nicht verwendet haben. Ihre Organisation verlangt, dass eine bestimmte Zeitspanne verstrichen ist, bevor Sie ein Kennwort wiederverwenden. |

## <a name="next-steps"></a>Nächste Schritte
Wenn Sie nach dem Aktualisieren Ihres Kennworts weiterhin kennwortbezogene Nachrichten erhalten, sollten Sie versuchen, Ihr Gerät neu zu starten. 

Benötigen Sie weitere Unterstützung? Wenden Sie sich an Ihren Ansprechpartner beim IT-Support. Die entsprechenden Kontaktinformationen finden Sie auf der [Unternehmensportal-Website](https://go.microsoft.com/fwlink/?linkid=2010980).  


