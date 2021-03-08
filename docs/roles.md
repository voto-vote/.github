# VOTO Rollenkonzept

Durch die Skalierbarkeit von VOTO enstehen verschiedene Ebenen der Zugriffsberechtigungen. Bei VOTO gibt es insgesamt fünf verschiedene Rollen.

## Admin

Admins sind Nutzer, die kompletten Zugriff über alle Funktionen des VOTO haben. Sie können Wahlen erstellen/bearbeiten/löschen sowie Nutzerberechtigungen verteilen. Adminrollen werden ausschließlich an VOTO-Team interne Mitarbeiter vergeben.

## Wahlleiter

Die sogenannten Wahlleiter sind die zentrale Rolle, die eine Wahl ausrichten will. Diese Rolle kann einen neuen VOTO für Ihre Wahl erstellen modifizieren und löschen. Das heißt, sie kann auch die Thesen, die für eine VOTO Instanz elementar sind, entwerfen und eintragen. Für einige Wahlen ist das Team hinter VOTO im Begriff dieser Rolle. Zukünftig (mit VOTO as a Service) wird dies jedoch auch buchbar sein. Zusätzlich können Wahlleiter, nachdem sie Parteien für die VOTO Instanz angelegt haben, Vertrauenspersonen für Parteien einladen.

## Vertrauensperson

Vertrauenspersonen sind fester Bestandteil einer Wahl. Sie werden von den Wahlleitern eingeladen und sind verantwortlich für die weitere Einladung der Kandidierenden von genau Ihrer Liste. Außerdem bekommen Vertrauenspersonen einen Überblick über Ihre Kandidierenden und deren Status. Die Vertrauenspersonen dienen als authentifizierter und vertrauenswürdiger Verteiler an die Kandidierenden.

## Kandidat

Kandidierende sind Personen, die bei einer Wahl antreten. Sie haben die Rechte Ihr Profil zu individualisieren und VOTO mit optionalen Freitextantworten zu beantworten. Kandiderende werden von Vertrauenspersonen eingeladen.

## Voter

Diese Rolle nehmen die Wählenden ein, die sich dafür entscheiden VOTO zu benutzen. Voter können das Frontend von VOTO benutzen und darauf basierend Ihre Matches zu Ihren Statements finden.

# Berechtigungen

Die nachfolgende Tabelle zeigt die Berechtigungen der einzelnen Rollen. Zu beachten ist, dass hierbei nicht zwischen `einer` und `vielen` unterschieden wird. Beispielsweise kann eine Kandidierende Person natürlich nur ihr eigenes Profil ändern und die Entität `Candidate` editieren - dargestellt ist es jedoch gleich.

| Action              | Admin | ElectionManager | TrustPerson | Candidate | Voter |
| ------------------- | ----- | --------------- | ----------- | --------- | ----- |
| **ADMIN**           |       |                 |             |           |
| - Get               | ✅    | ⬜️             | ⬜️         | ⬜️       | ⬜️   |
| - Create            | ✅    | ⬜️             | ⬜️         | ⬜️       | ⬜️   |
| - Edit              | ✅    | ⬜️             | ⬜️         | ⬜️       | ⬜️   |
| - Remove            | ✅    | ⬜️             | ⬜️         | ⬜️       | ⬜️   |
| **ELECTIONMANAGER** |       |                 |             |           |       |
| - Get               | ✅    | ✅              | ⬜️         | ⬜️       | ⬜️   |
| - Create            | ✅    | ⬜️             | ⬜️         | ⬜️       | ⬜️   |
| - Edit              | ✅    | ✅              | ⬜️         | ⬜️       | ⬜️   |
| - Remove            | ✅    | ⬜️             | ⬜️         | ⬜️       | ⬜️   |
| **TRUSTPERSON**     |       |                 |             |           |       |
| - Get               | ✅    | ✅              | ✅          | ✅        | ⬜️   |
| - Create            | ✅    | ✅              | ⬜️         | ⬜️       | ⬜️   |
| - Edit              | ✅    | ✅              | ✅          | ⬜️       | ⬜️   |
| - Remove            | ✅    | ✅              | ⬜️         | ⬜️       | ⬜️   |
| **CANDIDATE**       |       |                 |             |           |       |
| - Get               | ✅    | ✅              | ✅          | ✅        | ✅    |
| - Create            | ✅    | ⬜️             | ✅          | ⬜️       | ⬜️   |
| - Edit              | ✅    | ⬜️             | ✅          | ✅        | ⬜️   |
| - Remove            | ✅    | ⬜️             | ✅          | ⬜️       | ⬜️   |
| **ELECTION**        |       |                 |             |           |       |
| - Get               | ✅    | ✅              | ✅          | ✅        | ✅    |
| - Create            | ✅    | ✅              | ⬜️         | ⬜️       | ⬜️   |
| - Edit              | ✅    | ✅              | ⬜️         | ⬜️       | ⬜️   |
| - Remove            | ✅    | ✅              | ⬜️         | ⬜️       | ⬜️   |
| **INSTANCE**        |       |                 |             |           |       |
| - Get               | ✅    | ✅              | ⬜️         | ⬜️       | ⬜️   |
| - Create            | ✅    | ✅              | ⬜️         | ⬜️       | ⬜️   |
| - Edit              | ✅    | ✅              | ⬜️         | ⬜️       | ⬜️   |
| - Remove            | ✅    | ✅              | ⬜️         | ⬜️       | ⬜️   |
| **LOCALIZATION**    |       |                 |             |           |       |
| - Get               | ✅    | ✅              | ⬜️         | ⬜️       | ✅    |
| - Create            | ✅    | ✅              | ⬜️         | ⬜️       | ⬜️   |
| - Edit              | ✅    | ✅              | ⬜️         | ⬜️       | ⬜️   |
| - Remove            | ✅    | ✅              | ⬜️         | ⬜️       | ⬜️   |
| **PARTIES**         |       |                 |             |           |       |
| - Get               | ✅    | ✅              | ✅          | ✅        | ✅    |
| - Create            | ✅    | ✅              | ⬜️         | ⬜️       | ⬜️   |
| - Edit              | ✅    | ✅              | ✅          | ⬜️       | ⬜️   |
| - Remove            | ✅    | ✅              | ⬜️         | ⬜️       | ⬜️   |
| **VOTES**           |       |                 |             |           |       |
| - Get               | ✅    | ✅              | ✅          | ✅        | ⬜️   |
| - Create            | ⬜️   | ⬜️             | ⬜️         | ⬜️       | ✅    |
| - Edit              | ⬜️   | ⬜️             | ⬜️         | ⬜️       | ⬜️   |
| - Remove            | ⬜️   | ⬜️             | ⬜️         | ⬜️       | ⬜️   |
