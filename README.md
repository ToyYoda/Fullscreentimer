# Stakeholder-Map

Drag-and-drop-Tool für Stakeholder-Management als **eine einzige HTML-Datei**: kein Server, keine Datenbank, keine Installation.

## Nutzung

1. `index.html` im Browser öffnen (Doppelklick genügt).
2. In der **Stakeholderliste** Stakeholder mit „+ Stakeholder“ anlegen und direkt in der Tabelle bearbeiten: Name, Kürzel, Rolle, Organisation, Haltung, Notizen.
   - `Enter` im Namensfeld legt direkt darunter eine neue Zeile an und springt hinein.
   - Das **Kürzel** steht im Kreis in der Matrix. Bleibt es leer, werden die Initialen des Namens verwendet (z. B. „AS“ für Anna Schmidt). Bis zu 4 Zeichen.
3. Stakeholder aus „Nicht platziert“ per Drag & Drop in die **Einfluss-/Interesse-Matrix** ziehen und dort frei verschieben. Wer zurück in die Ablage gezogen wird, ist nicht mehr platziert.
   - Ohne Ziehen (praktisch auf dem Handy): Stakeholder antippen, dann auf die gewünschte Stelle in der Matrix tippen. Dazwischen kann gescrollt werden. Die Leiste am unteren Rand zeigt, wer gerade platziert wird; „Aus Matrix entfernen“ legt ihn zurück in die Ablage.
4. **Speichern unter…** wählt die JSON-Datei, in der alle Daten liegen.
5. **PDF** lädt eine PDF-Datei (A4 quer) herunter: Seite 1 zeigt die Matrix mit einer Übersicht nach Quadranten, danach folgt die vollständige Stakeholderliste mit Notizen.

## SEFE-Branding

Das Tool ist für SEFE gestaltet. Logo und Farben sind noch **Platzhalter** und müssen durch die offiziellen Vorgaben ersetzt werden:

- **Logo:** In `index.html` steht im Kopfbereich `<span class="brand-logo placeholder">SEFE</span>`. Dort das offizielle Logo als inline-SVG oder `<img>` einsetzen und die Klasse `placeholder` entfernen.
- **Farben:** Die geschätzten Werte `--brand-blue`, `--brand-sky` und `--brand-green` stehen am Anfang des `<style>`-Blocks. Für den PDF-Export gelten dieselben Werte in `PDF_COLORS`.

## Datenhaltung

Alle Daten liegen in einer JSON-Datei, die du selbst auswählst (z. B. `stakeholder.json`).

- **Chrome / Edge:** Die Datei wird direkt geschrieben. Nach dem ersten Speichern wird jede Änderung automatisch gesichert. Beim nächsten Start bietet die Seite an, die zuletzt verwendete Datei wieder zu öffnen (gemerkt wird nur der Verweis auf die Datei, nicht die Daten).
- **Firefox / Safari:** Diese Browser können keine Dateien überschreiben. „Öffnen…“ lädt die Datei, „Speichern (Download)“ lädt die aktuelle Fassung herunter.

- **Handy / Tablet:** Die Seite passt sich an kleine Bildschirme an: Die Liste wird zu Karten, Stakeholder lassen sich mit dem Finger in die Matrix ziehen. Mobile Browser nutzen in der Regel den Download-Weg wie Firefox/Safari.

Tastenkürzel: `Strg/Cmd + S` speichert, `Strg/Cmd + Umschalt + S` heißt „Speichern unter…“.

### Dateiformat

```json
{
  "app": "stakeholder-map",
  "version": 1,
  "updatedAt": "2026-10-19T12:00:00.000Z",
  "stakeholders": [
    {
      "id": "s-…",
      "name": "Anna Schmidt",
      "short": "",
      "role": "Bereichsleitung",
      "org": "Vertrieb",
      "attitude": "pro",
      "notes": "Monatliches Update",
      "x": 0.8,
      "y": 0.75
    }
  ]
}
```

- `short`: eigenes Kürzel; leer heißt Initialen des Namens
- `attitude`: `pro` (Unterstützer), `neutral` oder `con` (Kritiker)
- `x`: Interesse von 0 (niedrig) bis 1 (hoch), `y`: Einfluss von 0 bis 1; `null` heißt nicht platziert
- Quadranten: Eng einbinden (hoher Einfluss, hohes Interesse), Zufriedenstellen (hoher Einfluss, geringes Interesse), Informieren (geringer Einfluss, hohes Interesse), Beobachten (geringer Einfluss, geringes Interesse)
