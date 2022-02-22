# VOTO Rollenkonzept

Durch die Skalierbarkeit von VOTO enstehen verschiedene Ebenen der Zugriffsberechtigungen. Bei VOTO gibt es insgesamt fünf verschiedene Rollen.

## Admin

Admins sind Nutzer, die kompletten Zugriff über alle Funktionen des VOTO haben. Sie können Wahlen erstellen/bearbeiten/löschen sowie Nutzerberechtigungen verteilen. Adminrollen werden ausschließlich an VOTO-Team interne Mitarbeiter und Mitarbeiterinnen vergeben.

## Wahlleiter

Der sogenannte Wahlleiter ist die zentrale Rolle, die eine Wahl ausrichten will. Diese Rolle kann einen neuen VOTO für Ihre Wahl erstellen, modifizieren und löschen. Das heißt, sie kann auch die Thesen, die für eine VOTO Instanz elementar sind, entwerfen und eintragen. Für einige Wahlen ist das Team hinter VOTO im Begriff dieser Rolle. Zukünftig (mit VOTO as a Service) wird dies jedoch auch buchbar sein. Zusätzlich können Wahlleiter, nachdem sie Parteien für die VOTO Instanz angelegt haben, Vertrauenspersonen für Parteien einladen.

## Vertrauensperson

Vertrauenspersonen sind fester Bestandteil einer Wahl. Sie werden von den Wahlleitern eingeladen und sind verantwortlich für die weitere Einladung der Kandidierenden von genau ihrer Liste. Außerdem bekommen Vertrauenspersonen einen Überblick über ihre Kandidierenden und deren Status. Die Vertrauenspersonen dienen als authentifizierter und vertrauenswürdiger Verteiler an die Kandidierenden.

## Kandidat

Kandidierende sind Personen, die bei einer Wahl antreten. Sie haben die Rechte Ihr Profil zu individualisieren und VOTO mit optionalen Freitextantworten zu beantworten. Kandiderende werden von Vertrauenspersonen eingeladen.

## Voter

Diese Rolle nehmen die Wählenden ein, die sich dafür entscheiden, VOTO zu benutzen. Voter können das Frontend von VOTO benutzen und darauf basierend ihre Matches zu ihren Statements finden.

# Berechtigungen

Alle Berechtigungen der einzelnen Rollen können in der zentralen [API-Spezifikation](https://github.com/voto-vote/api-specification) nachgeschaut werden.
