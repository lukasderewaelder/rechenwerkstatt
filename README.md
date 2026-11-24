# Rechenwerkstatt – schriftliches Rechnen

Übungsseite für die schriftliche Addition, Subtraktion, Multiplikation und Division (Klasse 5–7). Läuft im Browser ohne Installation und ohne Internetverbindung: alles steckt in `index.html`.

**Online:** https://lukasderewaelder.github.io/rechenwerkstatt/

## Was die Seite kann

- Aufgaben per Zufall nach Schwierigkeit und Anzahl der Zahlen; Division optional mit Rest.
- Multiplikation und Division: Zahlenraum bis 1 000 … 1 000 000.
- Addition und Subtraktion: Stellenzahl „Bunt gemischt (3–7)“ oder fest 3–8 Stellen; der Schalter „Zahlen unterschiedlich lang“ mischt kurze und lange Zahlen in einer Aufgabe (Standard).
- Lösung im Kästchenraster wie im Schulbuch: Stellenwert-Kopf, Überträge, Subtraktion durch Entbündeln, Multiplikation mit eingerückten Teilprodukten, Division mit Rest-Pfeil und Kontrolle.
- Hilfe in Stufen: Strategie → Überschlag → erster Schritt → Lösung Schritt für Schritt mit hervorgehobenen Kästchen.
- Bei falscher Antwort: Hinweis, ab welcher Stelle es nicht stimmt, mit Sprung zu genau diesem Schritt.
- Eigene Ansicht für Handy, Tablet und Computer; druckbar.

## Entwickeln

```powershell
node tools/serve.mjs 4260
```

Dann http://localhost:4260 öffnen. Gestaltungsregeln: `design-system/MASTER.md`.

Erstellt mit Unterstützung von Claude (KI).
