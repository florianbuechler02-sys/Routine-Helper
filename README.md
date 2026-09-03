# Tagesgerüst

Eine geführte Morgen- und Abendroutine als Web-App. Kein Habit-Tracker, der
im Nachhinein Häkchen sammelt, sondern ein Gerüst, das einen durch die
Routine führt: ein Schritt pro Bildschirm, Timer laufen selbst, das Handy
liegt daneben statt in der Hand.

Entstanden aus einem konkreten Problem — morgens vergingen über 60 Minuten
bis zur Haustür, Dehnübungen wurden vergessen oder zu kurz gehalten, und
abends verschob das Sofa das Zubettgehen.

**Live:** https://claude.ai/code/artifact/b1256078-2cb5-43b0-802b-8065d6de97c5
(privat, nur mit dem eigenen Konto erreichbar)

## Was die App macht

**Läufer.** Ein Schritt füllt den Bildschirm. Halteübungen zählen als
Countdown herunter, geben einen Ton und springen selbst weiter. Häkchen-
Schritte warten. Für beide Plank-Durchgänge gibt es eine Stoppuhr, deren
Ring sich bis zur bisherigen Bestzeit füllt.

**Sitzungsuhr.** Oben läuft mit, wie lange man schon dabei ist, wie viel
Soll-Zeit die Routine hat und — wichtigster Teil — um wie viel Uhr man bei
diesem Tempo aus dem Haus wäre beziehungsweise im Bett läge. Die Anzeige
wird rot, sobald die Zielzeit reißt.

**Übersicht.** Die ganze Routine am Stück, mit der kumulierten Zeit ab Start
in der linken Spalte. Dort wird sichtbar, wo die Zeit tatsächlich liegt.
Ein Schritt lässt sich antippen, um mitten in der Routine einzusteigen.

**Schlaffenster.** Zubettgehzeit eintragen, die Weckzeit rechnet sich aus
Schlafdauer plus Einschlafzeit. Daraus leitet sich auch ab, ab wann das
Handy weg sein muss.

**Denkanstöße.** Bei einigen Halteübungen erscheint eine Frage zum
Nachdenken. Aus einem Pool von 34 werden täglich drei gezogen, wechselnd.
Hat man am Vorabend "wichtigste Sache morgen" beantwortet, ist genau das
der erste Anstoß am nächsten Morgen.

**Kurzversion.** Ein Schalter pro Routine, der die als optional markierten
Schritte auslässt — für Trainingsabende, an denen es spät wird.

**Verlauf im Hintergrund.** Plank-Zeiten als Balken mit Bestzeit, dazu ein
Sieben-Tage-Streifen, welche Routinen komplett durchliefen. Bewusst
zurückhaltend: das Gerüst steht im Vordergrund, nicht die Statistik.

## Aufbau

Eine einzige Datei, `tagesgeruest.html`, ohne Build-Schritt und ohne
Abhängigkeiten. Geladen werden nur die Schriften von Google Fonts
(Bricolage Grotesque, Instrument Sans, Martian Mono).

Die Routinen stehen als `DEFAULT_CONFIG` im Skript und lassen sich in der
App selbst bearbeiten — Schritte umbenennen, verschieben, löschen, Dauer und
Art ändern. Vier Schritt-Arten: `check` (Häkchen), `timer` (Countdown),
`stopwatch` (Stoppuhr mit Verlauf), `reflect` (die drei Abendfragen).

`DEFAULT_CONFIG.v` ist eine Versionsnummer. Wird sie erhöht, ersetzt die App
beim nächsten Start die gespeicherte Konfiguration durch die neue Vorgabe —
gedacht für Fälle, in denen sich die Routine grundlegend ändert. Eigene
Anpassungen gehen dabei verloren, deshalb nur bewusst erhöhen.

## Daten

Als Artifact veröffentlicht nutzt die App die Artifact-Datenbank mit den
Collections `config` (die Routinen), `logs` (ein Eintrag pro Durchlauf) und
`planks` (jede gemessene Zeit). Dadurch sind die Daten auf allen Geräten
gleich, auf denen man mit demselben Konto angemeldet ist.

Ist die Datenbank nicht erreichbar — etwa beim Öffnen der Datei direkt im
Browser — fällt die App auf `localStorage` zurück und funktioniert
vollständig, nur eben pro Gerät getrennt.

Ein angefangener Durchlauf wird zwischengespeichert: schließt man die Seite
mittendrin und öffnet sie innerhalb von drei Stunden wieder, geht es an
derselben Stelle weiter.

## Lokal ansehen

```bash
python3 -m http.server 8000
```

Dann `http://localhost:8000/tagesgeruest.html` öffnen. Direkt per Doppelklick
geht auch, dann fehlt nur die Zeichensatz-Angabe des Servers und Umlaute
sehen falsch aus.
