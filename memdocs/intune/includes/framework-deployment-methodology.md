<!-- This include file is for both the Android Enterprise framework and the APP data protection framework. Therefore, do not edit this file to be specific to either.-->

Vor Bereitstellung des Frameworks empfiehlt Microsoft eine Ringmethode zum Testen der Validierung. Das Definieren von Bereitstellungsringen ist in der Regel ein einmaliges (oder zumindest seltenes) Ereignis. Die IT-Abteilung sollte diese Gruppen jedoch erneut überprüfen, um sicherzustellen, dass die Sequenzierung weiterhin stimmt.

Microsoft empfiehlt den folgenden Ansatz für einen Bereitstellungsring für das Framework:

| Bereitstellungsring  | Mandant  | Bewertungsteams  | Ausgabe  | Zeitachse  |
|--------------------|------------------------|-------------------------------------------------------------------|----------------------------------------------------------|----------------------------------------|
| Qualitätssicherung  | Präproduktionsmandant  | Inhaber mobiler Funktionen, Sicherheit, Risikobewertung, Datenschutz, Servicequalität  | Funktionelle Szenarioüberprüfung, Entwurfsdokumentation  | 0-30 Tage  |
| Vorschau  | Produktionsmandant  | Inhaber mobiler Funktionen, Servicequalität  | Überprüfung von Endbenutzerszenarien, Benutzerdokumentation  | 7-14 Tage, nach der Qualitätssicherung  |
| Produktion  | Produktionsmandant  | Inhaber mobiler Funktionen, IT-Helpdesk  | N/V  | 7 Tage bis zu mehreren Wochen, nach der Vorschauphase  |

Alle Änderungen an den App-Schutzrichtlinien sollten zunächst in einer Präproduktionsumgebung erfolgen, um die Auswirkungen der Richtlinieneinstellung zu verstehen. Nach den Tests können die Änderungen in die Produktion übertragen werden, und auf eine Teilmenge der Produktionsbenutzer, die IT-Abteilung und andere geeignete Gruppen angewendet werden. Schließlich erfolgt die vollständige Einführung für den Rest der mobilen Benutzer. Die Einführung in die Produktion kann je nach Ausmaß der Auswirkungen der Änderungen länger dauern. Wenn es keine Auswirkungen auf die Benutzer gibt, sollte die Änderung schnell umgesetzt werden. Wenn es Auswirkungen auf die Benutzer gibt, muss die Einführung möglicherweise langsamer erfolgen, da Änderungen an die Zielgruppe kommuniziert werden müssen.