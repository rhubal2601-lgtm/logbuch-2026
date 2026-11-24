# logbook – Release-Testbericht

Stand: 24.11.2026

## Aktueller Stand

- Die App ist als responsive, lokal gespeicherte PWA angelegt.
- Die Hauptnavigation besteht aus Home, Plan, Analyse, Verlauf und Mehr.
- Plan bündelt Trainingspläne, Übungsbibliothek und aktive Einheit.
- Mehr bündelt Profile, Gerätebibliothek, Backups und Darstellungseinstellungen.
- Die Gerätebibliothek ist studio- und herstellerunabhängig. Sie enthält mehr als 170 allgemeine Gerätetypen in fünf Kategorien; Hersteller, Modelle und individuelle Geräteeinstellungen sind frei ergänzbar.
- Die Gerätebibliothek wird als zentrale Quelle für die Geräteauswahl in Trainingsplänen verwendet.
- Vorhandene Geräte- und Trainingsdaten bleiben bei der Ergänzung der Grundbibliothek erhalten; abgeschlossene Trainingseinheiten werden als historische Datensätze behandelt.
- Die Release-Prüfung validiert JavaScript-Syntax, Manifest, Pflichtdateien, Geräte-Grunddaten und das erstellte ZIP-Paket.

## Automatisierte Prüfungen

Der Workflow `Logbook Release Build` läuft bei Pushes auf `main` und manuell über GitHub Actions. Er prüft:

- `node --check app.js`
- `node --check sw.js`
- Manifest-JSON
- erforderliche Projektdateien
- mindestens 170 allgemeine Gerätevorlagen
- mindestens 15 Hersteller-Schnellvorschläge
- Erstellung und Integrität von `logbook-release.zip`

Ein erfolgreicher Workflow bestätigt diese automatisierten Prüfungen, aber keine vollständige Bedienbarkeit in jedem Browser.

## Noch nicht physisch bzw. manuell geprüft

- Interaktive Bedienung in Safari, Chrome und Firefox.
- IndexedDB-Persistenz nach Browserneustart und Wiederherstellung aus JSON-Backup.
- Offlinebetrieb nach echtem Neustart.
- PWA-Installation und Bedienung auf iPhone, iPad und Android.
- Responsive Darstellung auf physischen Geräten.
- Vollständige Ende-zu-Ende-Prüfung aller Trainingsabläufe mit realen Nutzerdaten.

## Hinweise vor dem produktiven Einsatz

- Vor dem ersten Update auf bestehende Nutzerdaten ein JSON-Backup exportieren.
- Daten bleiben lokal pro Browserprofil; es gibt keine automatische Synchronisierung zwischen Geräten.
- Browserdaten löschen, privater Modus oder Geräteverlust können lokale Daten entfernen.
- Ein erfolgreicher Syntax- und Paketbuild ersetzt keine manuellen Browser- und Gerätetests.
