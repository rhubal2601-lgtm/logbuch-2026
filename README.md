# logbook

**logbook** ist ein deutschsprachiges, lokal gespeichertes Trainingslogbuch für Bodybuilding. Die responsive App funktioniert ohne Login, Backend, Cloud oder externe Laufzeitbibliotheken.

## Gestaltung

Die Oberfläche folgt dem bereitgestellten logbook-Designentwurf: tiefschwarzer Hintergrund, anthrazitfarbene Karten, gelbe Akzente, einheitliche Formulare und Buttons sowie Icon-Navigation. Auf schmalen Displays bleibt die Navigation am unteren Rand; auf breiten Displays wechselt sie in eine kompakte Seitenleiste. Diagramme verwenden ein gemeinsames Raster, Verlauf und Marker.

## Starten

Für lokale Entwicklung einen HTTP-Server im Projektordner starten:

```bash
python -m http.server 8000
```

Anschließend `http://localhost:8000` öffnen. `file://` reicht für den Service Worker und die Offline-Funktionen nicht aus.

## Installieren

- **iPhone / iPad:** Seite in Safari über HTTPS öffnen, Teilen antippen und **Zum Home-Bildschirm** auswählen.
- **Android:** Seite in Chrome über HTTPS öffnen, Browsermenü öffnen und **App installieren** wählen. Der Menüpunkt kann je nach Browserversion anders heißen.
- **Desktop:** In einem kompatiblen Browser das Installationssymbol in der Adressleiste oder das Browsermenü verwenden.

GitHub Pages kann die Dateien statisch bereitstellen: Repository-Einstellungen → **Pages** → Hauptbranch und Stammverzeichnis wählen. GitHub Pages liefert HTTPS automatisch aus. Der GitHub-Actions-Workflow **Logbook Release Build** prüft bei jedem Push auf `main` die JavaScript-Syntax, das Manifest, die Grunddatenbank und erstellt ein ZIP-Artefakt. Das ZIP findest du nach erfolgreichem Lauf unter **Actions → Logbook Release Build → Artifacts → logbook-release**.

## Nutzung

Die Navigation ist in fünf Bereiche gegliedert: **Home**, **Training**, **Analyse**, **Verlauf** und **Mehr**. Die Gerätebibliothek ist über **Mehr → Geräte verwalten** erreichbar.

1. Unter **Mehr** Profile anlegen oder wechseln, die Gerätebibliothek mit fünf Kategorien durchsuchen und bei Bedarf eigene Geräte sowie individuelle Einstellungen erfassen.
2. Unter **Training** einen der fünf Split-Pläne als Vorlage hinzufügen oder eigene Pläne und Trainingstage erstellen.
3. Ein Training starten, Sätze mit Gewicht, Wiederholungen, RIR und Satztyp protokollieren und die Einheit abschließen.
4. **Analyse** berechnet Satzvolumen, Muskelgruppenvolumen, geschätzte 1RM-Rekorde und Übungsentwicklung ausschließlich aus abgeschlossenen protokollierten Sätzen.
5. **Verlauf** zeigt Einheiten, Trainingskalender, Frequenz und das manuell gepflegte Körpergewichtsdiagramm.

Abgeschlossene Trainings werden als Datensatz gespeichert. Änderungen an späteren Plänen oder Übungen ändern die Übungsnamen und Werte in früheren Einheiten nicht.

## Datenhaltung und Backups

Daten bleiben auf dem Gerät und im jeweiligen Browserprofil. IndexedDB (`logbook-local`) ist der primäre Speicher. Beim Start wird der neueste bestätigte Stand aus IndexedDB und `localStorage` gewählt; fehlt ein IndexedDB-Stand, werden vorhandene lokale Daten übernommen. Änderungen werden zuerst in IndexedDB gespeichert; `localStorage` dient als lokale Wiederherstellungskopie und Fallback. Ist IndexedDB nicht verfügbar, läuft die App mit `localStorage` weiter. Beim ersten Start mit einer älteren logbook-Version werden vorhandene Version-1-Daten in die profilbezogene Struktur übernommen; der alte Schlüssel bleibt erhalten.

Profile besitzen getrennte Pläne, Übungen, Gerätekonfigurationen, Favoriten, Gewichtsverläufe, Trainingseinheiten und aktive Trainingsentwürfe. Die Geräte-Grundbibliothek enthält bei einer Neuinstallation 52 allgemeine Gerätetypen in den Kategorien Freihanteln, Maschinen, Kabelzüge, Körpergewicht und Sonstiges Zubehör. Sie wird bei vorhandenen Profilen ergänzend eingespielt, ohne eigene Geräte zu überschreiben. Hersteller können gesucht und beim Anlegen eines eigenen Geräts frei ergänzt werden. Es gibt keine automatische Synchronisierung zwischen Geräten. Zum Gerätewechsel in **Verwaltung** ein JSON-Backup exportieren und am Zielgerät importieren. Der Import prüft Version, Profile, IDs und Trainingseinheiten, bevor er den aktuellen lokalen Datenbestand ersetzt.

Browserdaten löschen, privater Modus, Geräteverlust oder Browserwechsel können lokale Daten entfernen. Regelmäßig ein JSON-Backup an einem selbst gewählten sicheren Ort ablegen.

## Offlinebetrieb

Nach dem ersten erfolgreichen Laden über HTTPS werden App-Oberfläche, JavaScript, Manifest und Icon durch den Service Worker zwischengespeichert. Anschließend kann die App ohne Netzwerk aufgerufen werden. Änderungen zwischen Geräten werden nicht synchronisiert.

## Technische Hinweise

- Statische Dateien: HTML, CSS und JavaScript; kein Build-Schritt erforderlich.
- Kein Backend, keine Drittanbieter-Analytics, keine Anmeldung, keine Cloud.
- IndexedDB ist der primäre Datenspeicher; `localStorage` ist lokaler Fallback und Wiederherstellungskopie.
- Die Analyse zählt abgeschlossene Arbeitssätze; Aufwärmsätze fließen nicht in Volumen und Rekorde ein.

## Testbericht

Der mitgelieferte [Testbericht](TESTBERICHT.md) trennt ausgeführte technische Prüfungen klar von Browser-, Geräte- und Offlineprüfungen, die in dieser Arbeitsumgebung nicht bestätigt wurden.
