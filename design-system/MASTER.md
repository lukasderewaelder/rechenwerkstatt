# Rechenwerkstatt – Designsystem (Master)

Stand: 24.11.2026. Quelle für alle Gestaltungsentscheidungen. Seitenspezifische Abweichungen gehören nach `design-system/pages/`.

## Leitidee: „Heft mit Rand“

- **Bühne (links, breit):** nur das Wesentliche – Rechenart, die Aufgabe in großen Ziffern, ein Eingabefeld, ein Knopf „Prüfen“. Die Lösung erscheint hier im Kästchenraster wie im Schulbuch.
- **Randspalte (rechts, schmal):** alle Hinweise, abgesetzt durch eine rote Heftrand-Linie. Hilfe kommt nur auf Wunsch und in Stufen.
- **Asymmetrie:** Bühne ≈ 2/3, Rand ≈ 1/3; die Bühne hat links mehr Innenabstand als rechts. Die obere Leiste ist links bündig (Marke, Rechenarten), die Einstellungen sitzen rechts als kompakter Knopf.
- **Hinweise an der benötigten Stelle:**
  1. Fehlerhinweis direkt unter dem Eingabefeld: welche Stellen schon stimmen und ab welcher Stelle geprüft werden muss, mit Knopf „Diese Stelle zeigen“.
  2. Hilfe-Leiter im Rand: Tipp 1 Strategie → Tipp 2 Überschlag (bei Division: Stellenzahl) → Tipp 3 erster Schritt.
  3. Lösung Schritt für Schritt: Der aktuelle Schritt wird im Raster hervorgehoben (Spalte oder Zeile hellblau, neu geschriebene Ziffern gelb), noch nicht erreichte Ziffern sind ausgeblendet.

Stil laut ui-ux-pro-max: „Minimalism & Swiss Style“ (klar, viel Weißraum, eine Akzentfarbe, klare Typohierarchie). Schrift: Systemschrift (offline, keine externen Fonts); für Schrift gab es keinen passenden Datenbanktreffer.

## Tokens

| Gruppe | Token | Wert | Verwendung |
|---|---|---|---|
| Fläche | `--bg` | `#F5F6F8` | Seitenhintergrund |
| | `--surface` | `#FFFFFF` | Bühne, Notizen, Felder |
| Text | `--ink` | `#141B2D` | Haupttext, Aufgabe |
| | `--ink-2` | `#46526A` | Beschriftungen |
| | `--ink-3` | `#667085` | leise Hinweise (≥ 4.5:1 auf Weiß) |
| Linien | `--line` / `--line-strong` | `#E2E6ED` / `#CBD3DF` | Rahmen, Feldränder |
| Akzent | `--accent` / `--accent-strong` / `--accent-soft` | `#2B59C3` / `#1F4396` / `#EBF0FC` | Hauptaktion, Rechenzeichen, Schrittfokus |
| Hinweis | `--hint` / `--hint-soft` / `--hint-line` | `#8A4B00` / `#FFF4DE` / `#F3C77A` | Hilfe-Leiter |
| Rand | `--margin-line` | `#EFA39A` | Heftrand-Linie |
| Rückmeldung | `--ok` / `--ok-soft`, `--err` / `--err-soft` | `#15693B` / `#E5F4EA`, `#A8251C` / `#FCECEA` | Richtig / Noch nicht |
| Raster | `--grid`, `--grid-ink`, `--rest` | `#D5E1F2`, `#26324A`, `#D23F1A` | Kästchen, Ziffern, Rest |
| Schritt | `--focus-bg`, `--now-bg` | `rgb(43 89 195 / .09)`, `rgb(255 196 0 / .30)` | aktive Spalte/Zeile, neue Ziffern |
| Radius | `--r-s` / `--r-m` / `--r-l` | 8 / 14 / 24 px | Felder / Notizen / Bühne |
| Abstand | `--space-1 … --space-8` | 4, 8, 12, 16, 24, 32, 48, 64 px | |
| Bewegung | `--t-fast` / `--t` | 140 / 220 ms, `--ease` | nur Farbe, Deckkraft, kleine Verschiebung; `prefers-reduced-motion` schaltet ab |
| Kästchen | `--sq` | 34 px (Handy 28–30 px) | Rastergröße |

Schriftgrößen: Aufgabe `clamp(36px, 5.6vw, 64px)` 750; Ergebnisfeld 26 px 700; Fließtext 15–16 px; Beschriftungen 13 px 700. Ziffern immer `tabular-nums`.

## Komponenten

| Komponente | Klasse | Zustände |
|---|---|---|
| Obere Leiste | `.topbar`, `.brand`, `.ops > .op[aria-current]` | aktiv = dunkle Pille |
| Einstellungen | `details.settings > summary.settings-toggle + .settings-panel` | zu / offen (Popover; Handy: Bottom-Sheet) |
| Bühne | `.stage`, `.stage-head`, `#title`, `#regenerate` | – |
| Aufgabe | `.expression > .num / .opr / .eq` | – |
| Antwort | `form.answer-form > .answer-fields > .field-answer / .field-rest / .btn-check` | Fokus-Ring, `aria-invalid` |
| Rückmeldung | `.feedback.is-correct / .is-wrong` (`role=status`) | mit Folgeaktion `new` bzw. `goto` |
| Lösung | `.solution(.stepping) > .papers > figure.paper[data-g] > .paper-grid > .cell[data-r][data-c][data-s]` | `.focus`, `.now`, `.pending` |
| Randnotiz | `.note.note-help`, `.note.note-steps` | Tipp-Liste `.tips > .tip`, `.progress`, `.stepper` |
| Knöpfe | `.btn-primary`, `.btn-soft`, `.btn-ghost`, `.btn-link`, `.icon-btn` | hover, active, disabled, focus-visible |

Aktionen laufen über `data-action`: `check` (Formular-Submit), `new`, `tip`, `steps`, `all`, `hide`, `prev`, `next`, `goto` (`data-step`).

## Responsive

- Grundstil = einspaltig. Ab 760 px Bühne + Randspalte (Datei `index.html`).
- Unter 760 px: Handy-Variante als eigener `<style>`-Block in `index.html` (`@media screen and (max-width:759.98px)`, `screen` damit Druck auf A4 nicht betroffen ist). Antwortleiste unten im Daumenbereich (`--dock` reserviert Platz, `--keyboard-inset` per `visualViewport`), Einstellungen als Bottom-Sheet, Schritt-Karte als Sheet unten, Querformat mit Bühne und Rand nebeneinander.
- Regeln: keine waagrechte Seiten-Scrollleiste (das Raster scrollt in seinem Kasten), Tippflächen ≥ 44 px, Ziffern-Tastatur (`inputmode="numeric"`), sichere Ränder (`env(safe-area-inset-*)`).

## Nicht tun

- Keine Emojis als Symbole (SVG-Linien-Icons im Stil Lucide).
- Hilfe nicht ungefragt aufdrängen; die Lösung nie automatisch zeigen.
- Keine zweite Akzentfarbe für Aktionen; Gelb nur für Hinweise.
