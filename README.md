# LaTeX-Vorlage: IHK-Projektdokumentation (FIAE)

Wiederverwendbare, projektunabhängige LaTeX-Vorlage für die
Projektdokumentation zur Abschlussprüfung Teil 1/2
(Fachinformatiker/-in Anwendungsentwicklung).

Basis:
- `Checkliste_zur_Projektdokumentation.docx` (IHK, formale Vorgaben)
- Beispieldokumentation Berg (2025/26) — Kapitel-/Anhangstruktur
  (gleicher Ausbildungsbetrieb-Kontext wie diese Vorlage, daher als
  Struktur-Vorbild gewählt statt des generischeren Feldhaus-Beispiels)
- `latex-vorlage-fiae-master` (Stefan Macke) — Grundgerüst
- Präambel (Schrift/Ränder/Zeilenabstand) übernommen aus der bereits
  funktionierenden Konfiguration in `.tmp/ihk/latex/main.tex`

Ausführliche Anforderungs- und Abgleichsanalyse: siehe
`.tmp/ihk/anforderungen-und-abgleich.md` (gleiches Repository).

## Verwendung

1. Verzeichnis in ein neues Projekt kopieren (eigenes Git-Repo, falls
   gewünscht).
2. Alle `[PLATZHALTER: ...]`-Stellen suchen und ersetzen (Editor-Suche über
   alle Dateien, z.B. `grep -rn "PLATZHALTER" .`).
3. `kapitel/*.tex`: Überschriften/Struktur sind vorgegeben, Inhalte
   schreiben.
4. `anhang/*.tex`: jede der 18 vorbereiteten Anlagen entweder befüllen oder
   — falls im eigenen Projekt nicht zutreffend — Datei löschen und die
   zugehörige `\input`-Zeile in `anhang.tex` entfernen. Nicht leer stehen
   lassen.
5. Kompilieren: `latexmk -pdf main.tex` (oder `pdflatex main.tex` zweimal).

## Formale Vorgaben (bereits in `main.tex` umgesetzt)

| Vorgabe | Umsetzung |
|---|---|
| Schriftgröße 11pt | `\documentclass[...,11pt,...]` |
| Schriftart Arial oder Tahoma | `helvet` (Helvetica-Metrik-Klon, lizenzfrei); für echtes Arial: `lualatex` + `fontspec` + `\setmainfont{Arial}` |
| Zeilenabstand 1,3 | `\usepackage{setspace}` + `\setstretch{1.3}` |
| Seitenränder nach DIN 5008 | `geometry`-Paket, siehe `main.tex` |
| Hauptteil max. 15 DIN-A4-Seiten | selbst einhalten — nach dem Schreiben mit `latexmk` prüfen, arabische Seitenzahl des letzten Hauptteil-Kapitels |
| Anlagen max. 20 Seiten | selbst einhalten, siehe Hinweis in `anhang.tex` |
| Gesamtgröße Upload i.d.R. begrenzt (oft 4 MB) | eingebundene PDFs/Scans vor Abgabe prüfen/komprimieren |

## Inhaltliche Vorgaben (Checkliste umgesetzt als Struktur/Hinweise)

- **Vollständiger Prozess, keine reine Produktbeschreibung:** Kapitel 1–8
  decken Ausgangssituation → Anforderungsanalyse → Planung → Umsetzung →
  Test → Übergabe → Abschluss ab, nicht nur das fertige Ergebnis.
- **Lösungsalternativen, Analysen, Entscheidungen erläutern:** Platzhalter
  in Kapitel 2 (Soll-Konzept) und Kapitel 3 (Projektplanung) erinnern
  explizit daran, Alternativen zu vergleichen statt nur die Wahl zu nennen.
- **Nicht allgemeingültige Abkürzungen vermeiden/erläutern:**
  `abkuerzungen.tex` — nur tatsächlich verwendete, nicht allgemein bekannte
  Abkürzungen eintragen.
- **Abweichungen vom Projektantrag nachvollziehbar begründen:**
  Abschnitt "Soll-Ist-Vergleich" in Kapitel 7 (`sec:soll_ist_vergleich`),
  mit Verweis auf Anlage 1 (Projektantrag).
- **Vertrauliche/datenschutzrelevante Daten kennzeichnen:** Hinweise dazu in
  `deckblatt.tex`, `sperrvermerk.tex` (nur falls benötigt — sonst entfernen)
  und Anlage 13 (Screenshots).
- **Keine falschen Datumsangaben, Nachvollziehbarkeit der Prozessschritte:**
  alle Datums-Platzhalter sind bewusst nicht vorausgefüllt.
- **Durchführung erst nach Genehmigung:** Platzhalter für das
  Genehmigungsdatum in Kapitel 3.
- **Eindeutiger Verweis auf jede zitierte Anlage:** jede `anhang/*.tex`
  trägt ein `\label{anh:...}`; die Kapitel referenzieren es bereits per
  `\ref{}` an der passenden Stelle — beim Ausfüllen weitere Verweise analog
  ergänzen.
- **Nicht selbst erstellte Anlagen kennzeichnen:** in Anlage 17 (Protokoll
  zur Projektarbeit) und Anlage 18 (Persönliche Erklärung) bereits vermerkt
  — beide Formulare sind offizielle IHK-Downloads, kein eigener Text.

## Struktur

```
main.tex                  Dokumentklasse, Präambel, Einbindung aller Teile
deckblatt.tex              Titelseite
sperrvermerk.tex            optional — entfernen, falls nicht benötigt
abkuerzungen.tex            Abkürzungsverzeichnis
literaturverzeichnis.tex    Literaturverzeichnis
kapitel/
  01_einleitung.tex
  02_anforderungsanalyse.tex
  03_projektplanung.tex
  04_vorgehensmodell_und_methodik.tex
  05_umsetzung.tex
  06_testphase_und_fehlerbehebung.tex
  07_bereitstellung_und_abnahme.tex
  08_abschluss.tex
anhang.tex                 Anhang-Übersicht + Hinweise
anhang/
  01_projektantrag.tex
  02_lastenheft.tex
  03_pflichtenheft.tex
  04_gantt_diagramm.tex
  05_zeitplanung.tex
  06_kostenplanung.tex
  07_risikoanalyse.tex
  08_stakeholderanalyse.tex
  09_vorgehensmodell.tex
  10_testprotokoll.tex
  11_diagramme.tex           Use-Case, ER-/Tabellenmodell, Aktivitätsdiagramme
  12_mockups.tex
  13_screenshots.tex
  14_entwicklerdokumentation.tex
  15_kundendokumentation.tex
  16_quellcode_ausschnitte.tex
  17_protokoll_zur_projektarbeit.tex   nicht selbst erstellt (IHK-Formular)
  18_persoenliche_erklaerung.tex       nicht selbst erstellt (IHK-Formular)
anlagen/                    Ablageort für eingebundene PDFs (leer, .gitkeep)
bilder/                     Ablageort für Grafiken/Diagramme (leer, .gitkeep)
```

## Nicht enthalten (bewusst)

- Kein `biblatex`/`biber` — einfache `thebibliography` reicht für den
  üblichen Umfang und braucht keine zusätzliche Toolchain.
- Kein separates `Meta.tex` — Metadaten-Makros stehen direkt in `main.tex`
  (wie in der bereits funktionierenden `.tmp/ihk/latex/main.tex`).
