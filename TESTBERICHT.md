# logbook – Release-Testbericht

Stand: 24.11.2026

## In dieser Arbeitsumgebung ausgeführt

- Darstellungsänderungen in den Designbereichen der `index.html` und den zwei Canvas-Zeichenfunktionen in `app.js` gebündelt. Navigation, Training, Profile, Persistenz, Migration und Backupfunktionen wurden nicht umgebaut.
- Prüfsummenvergleich der bisherigen Release-Fassung gegen die aktuelle `app.js` – geprüft, dass Unterschiede auf die Zeichenfunktionen der Diagramme begrenzt sind.
- JavaScript-Syntax von `app.js` und `sw.js` sowie JSON-Syntax des Manifests – erfolgreich.
- Statische Prüfung der fünf `data-page`-Navigationsziele, relevanten Trainings-/Verwaltungsbereiche, SVG-Iconstruktur und responsiven Breakpoints – erfolgreich.
- `node --check app.js` – erfolgreich.
- `node --check sw.js` – erfolgreich.
- `manifest.webmanifest` – als JSON eingelesen, erfolgreich.
- Statische Strukturprüfung – fünf Hauptnavigationseinträge, fünf Splitvorlagen, die Bereiche Planeditor, Übungsbibliothek, aktive Einheit, Analyse, Verlauf, Geräteverwaltung und Profile sind im Quellstand vorhanden.
- Service-Worker-Prüfung – Installations-Cache enthält Startseite, App-Skript, Manifest und Icon; Navigationsanfragen haben einen Cache-Fallback. Dies ist eine Quellprüfung, kein tatsächlicher Offlineaufruf.
- Release-ZIP – nach den Quelländerungen neu erstellt, Dateiliste und Größen gegen die Projektdateien verglichen und ZIP-Integrität geprüft.

## Nicht ausgeführt / nicht bestätigt

- Kein visueller Browservergleich der fertigen App mit der Referenz; die Computer-Use-Umgebung konnte die lokale Browser-URL nicht sicher bestimmen.
- Ein interaktiver Browser-Smoke-Test konnte nicht gestartet werden. Der lokale Testserver war aus der Browserumgebung nicht erreichbar (`ERR_CONNECTION_TIMED_OUT`).
- Kein realer Offline-Neustart mit zuvor installiertem Service Worker.
- Keine Installation oder Bedienprüfung auf iPhone, iPad oder Android-Gerät.
- Keine Prüfung der nativen PWA-Installationsdialoge.
- Keine automatisierte Ende-zu-Ende-Prüfung von Training anlegen/abschließen, Profilwechsel, Backup-Import/Export oder IndexedDB-Wiederherstellung in einem echten Browser.

## Bekannte Einschränkungen

- Speicherung gilt nur für das jeweilige Browserprofil und Gerät. Es gibt keine geräteübergreifende Synchronisierung.
- Wenn IndexedDB vom Browser blockiert oder deaktiviert wird, verwendet die App `localStorage` als Fallback; dadurch gelten dessen Speichergrenzen.
- GitHub-Pages-Bereitstellung, iOS-/Android-Installation und Offlinefunktion müssen vor einer öffentlichen Release auf Zielgeräten praktisch bestätigt werden.
- Der Server- und Browser-Testblocker in dieser Umgebung lässt visuelle und interaktive Regressionen offen. Die Syntax- und Paketprüfung ersetzt diese Tests nicht.
