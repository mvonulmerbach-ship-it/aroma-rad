# Aroma-Rad Wein & Kaffee

Interaktives Aromarad mit drei Ebenen (Kategorie → Unterkategorie → Aroma) für Wein, Kaffee oder beides.

**Live:** https://mvonulmerbach-ship-it.github.io/aroma-rad/

## Funktionen

- Filter **Wein & Kaffee**, **Nur Wein**, **Nur Kaffee** (aus denselben Daten; jedes Aroma ist mit `gilt_fuer` markiert).
- Antippen eines Segments hebt den Pfad hervor und blendet den Rest ab; die Kopfzeile zeigt den Pfad.
- **Liste unter dem Rad:** ohne Auswahl die Kategorien, sonst Pfad und die nächste Ebene. Antippen in der Liste geht eine Ebene tiefer, „‹“ eine zurück. Damit lässt sich das Rad am Handy ohne Zoomen bedienen.
- **Beschriftung im Rad nur, wenn sie lesbar ist:** Eine Beschriftung erscheint erst, wenn sie auf dem Bildschirm mindestens 11 px groß ist (Schriftgröße im SVG × Maßstab, gemessen mit `getScreenCTM`). Am Handy ist das Rad deshalb zunächst unbeschriftet. Beim Zoomen erscheinen die Beschriftungen, bei voller Vergrößerung alle.
- Zoomen mit den Knöpfen − ⟳ + unter dem Rad, mit zwei Fingern oder dem Mausrad; ziehen verschiebt.
- Hell/Dunkel: `?theme=dark|light` (von einer einbettenden App) hat Vorrang. Als eigenständige App gibt es oben rechts den Schalter ◐ System (Standard) · ☀️ Hell · 🌙 Dunkel (`localStorage`, Schlüssel `aroma_theme`). Im iframe gibt es keinen Schalter; die einbettende App kann per `postMessage({type:'aromarad-theme', value:'dark'|'light'})` umschalten.

## Dateien

| Datei | Zweck |
|---|---|
| `index.html` | die ganze App (HTML, CSS, JavaScript, Aromadaten) |
| `aromarad.json` | dieselben Aromadaten als eigene Datei (wird von `index.html` nicht geladen) |
| `manifest.webmanifest`, `icon-192.png`, `icon-512.png`, `icon-maskable.png` | Installation als App (🎡) |
| `sw.js` | Service Worker für den Offline-Betrieb |

## Kopien in anderen Apps

`index.html` liegt byte-gleich als `aromarad.html` in vier weiteren Repos:

- `wein-lern-app/aromarad.html`
- `kaffee/aromarad.html`
- `wein-nachschlagewerk/aromarad.html`
- `kaffee-nachschlagewerk/aromarad.html`

**Änderungen nur hier machen, dann in alle vier kopieren** und dort jeweils die Cache-Version in `sw.js` hochzählen. Manifest und Service Worker greifen nur unter `/aroma-rad/`; die Kopien bleiben reine Komponenten und registrieren nichts.

## Auf dem Handy installieren

Seite in Chrome öffnen → Menü ⋮ → „Zum Startbildschirm hinzufügen“ (Safari: Teilen → „Zum Home-Bildschirm“).

## Offline

Nach dem ersten Öffnen läuft das Aroma-Rad ohne Netz (Service Worker, network first mit Cache als Rückfall).
