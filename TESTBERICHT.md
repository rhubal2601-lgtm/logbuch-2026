# logbook – Release-Testbericht

Stand: 24.11.2026

## In dieser Revision umgesetzt

- Geräte-Grundbestand mit 52 allgemeinen Gerätetypen in fünf Kategorien ergänzt: Freihanteln, Maschinen, Kabelzüge, Körpergewicht und Sonstiges Zubehör.
- Grundbestand wird bei Neuinstallation angelegt und bei bestehenden Profilen rückwärtskompatibel ergänzt. Vorhandene individuelle Geräte bleiben erhalten; bestehende Einträge ohne Kategorie werden unter „Sonstiges Zubehör“ einsortiert.
- Herstellerliste erweitert und Hersteller-Suche ergänzt. Freie Hersteller- und Modellangaben bleiben möglich.
- Gerätebibliothek auf Kachel-Startansicht, Kategorie-/Suchliste, Favoriten und separate Detailansicht umgestellt.
- Individuelle Geräteeinstellungen, profilbezogene Favoriten und die optionale Übungszuordnung bleiben Bestandteil der bestehenden Datenstruktur.
- Speicherreihenfolge angepasst: IndexedDB wird zuerst beschrieben; localStorage dient als Wiederherstellungskopie und Fallback.
- GitHub Actions Workflow ergänzt, der JavaScript-Syntax, Manifest-JSON und ZIP-Integrität prüft und ein Release-ZIP als Build-Artefakt bereitstellt.

## Noch automatisiert zu bestätigen

Der GitHub-Actions-Build wird durch den Push auf den Branch `finish-logbook` gestartet. Erst nach erfolgreichem Workflow gelten die folgenden Prüfungen als bestanden:

- `node --check app.js`
- `node --check sw.js`
- Manifest als JSON lesbar
- ZIP-Erstellung und ZIP-Integrität

## Nicht tatsächlich geprüft

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
- Ein erfolgreicher Syntax- und Paketbuild ersetzt keine manuelle Browser- und Gerätetests.
- Historische Trainingseinheiten bleiben beim Ergänzen des Geräte-Grundbestands unverändert.
