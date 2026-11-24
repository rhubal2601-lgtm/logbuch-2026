# logbook – Release-Testbericht

Stand: 24.11.2026

## Aktueller Repository-Stand

Geprüfter Branch: `main`

- Die Geräte-Grunddatenbank enthält 184 allgemeine Gerätetypen in fünf Kategorien (24 Freihantel-, 80 Maschinen-, 26 Kabelzug-, 19 Körpergewichts- und 35 Zubehör-Einträge): Freihanteln, Maschinen, Kabelzüge, Körpergewicht und Sonstiges Zubehör.
- Die Herstellerliste enthält 63 Marken-/Herstellereinträge im Quellcode; eigene Hersteller- und Modellangaben bleiben möglich.
- Der Grundbestand wird beim Normalisieren vorhandener Profile ergänzt, ohne Einträge mit bereits vorhandenen IDs zu duplizieren.
- Die Gerätebibliothek besitzt eine Kachel-Startansicht, Kategorie-/Suchlisten, Favoriten und eine separate Detailansicht.
- Die Kategorieauswahl initialisiert ihren Zustand explizit; beim Öffnen einer Kategorie wird ein vorheriger Suchfilter zurückgesetzt.
- IndexedDB wird als primärer Speicher verwendet; localStorage bleibt Wiederherstellungskopie und Fallback.
- Der Service-Worker-Cache wurde auf `logbook-cache-v4` angehoben, damit zuvor zwischengespeicherte App-Dateien beim nächsten erfolgreichen Laden ersetzt werden.
- Ein GitHub-Actions-Workflow unter `.github/workflows/release.yml` prüft Quellcode und Manifest, kontrolliert Mindestbestände der Geräte- und Herstellerdaten und erstellt ein ZIP-Artefakt.

## Automatisierte Prüfungen im Release-Workflow

Der Workflow wird bei Pushes auf `main` und manuell über GitHub Actions gestartet. Er führt folgende Schritte aus:

- `node --check app.js`
- `node --check sw.js`
- Manifest-JSON-Prüfung
- Prüfung erforderlicher Projektdateien
- Mindestbestandsprüfung für Geräte und Hersteller
- Erstellung von `logbook-release.zip`
- ZIP-Integritätsprüfung

**Wichtig:** Diese Prüfungen werden erst dann als bestanden gewertet, wenn der Workflow in GitHub Actions erfolgreich abgeschlossen wurde.

## Noch nicht tatsächlich geprüft

- Interaktive Bedienung in einem echten Browser.
- Tatsächliche IndexedDB-Persistenz nach Browserneustart und bei blockiertem localStorage.
- JSON-Dateidialoge und Wiederherstellung echter Nutzerdaten.
- Service-Worker-Offlinebetrieb nach echtem Neustart.
- PWA-Installation und Bedienung auf iPhone, iPad und Android.
- Responsive Darstellung auf physischen Geräten.
- Visuelle Übereinstimmung mit sämtlichen ursprünglichen Designreferenzen.

## Hinweise vor dem produktiven Einsatz

- Vor dem ersten Update auf bestehende Nutzerdaten ein JSON-Backup exportieren.
- Die App speichert lokal pro Browserprofil und synchronisiert nicht zwischen Geräten.
- Ein erfolgreicher Syntax- und Paketbuild ersetzt keine manuellen Browser- und Gerätetests.
- Historische Trainingseinheiten sollen beim Ergänzen des Geräte-Grundbestands unverändert bleiben.
