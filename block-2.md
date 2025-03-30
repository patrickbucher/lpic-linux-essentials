# Block 2

## Ziel

## Ablauf

## Thema 2

### 2.1) Grundlagen der Befehlszeile

#### Lektion 1

[Quelle](https://learning.lpi.org/de/learning-materials/010-160/2/2.1/2.1_01/)

- Shell: textbasierte Benutzerschnittstelle
    - `bash`: Bourne-Again Shell (am weitesten verbreitet)
    - `csh`: C Shell (einfacher)
    - `ksh`: Korn Shell (sehr nahe am POSIX-Standard)
    - `zsh`: Z Shell (sehr mächtig)
- Prompt
    - `$`: normaler Benutzer
    - `#`: Administrator (`root`)
- Befehl, z.B. `ls -l /home/user`
    - Befehl (Programm): `ls`
    - Optionen/Parameter: `-l`
    - Argument(e): `/home/user`
- Befehlstypen
    - eingabaut (built-in): durch die Shell zur Verfügung gestellt (z.B. `cd`, `pwd`)
    - extern: Befehle in Dateien (Skripte, Binärdateien)
    - weitere: Funktionen, Aliase
    - `type BEFEHL`
- Quoting
    - doppelte Anführungszeichen: `"…"`
        - mit Expansion von Variablen
    - einfache Anführungszeichen: `'…'`
        - ohne Expansion von Variablen
    - Escape-Zeichen: `\`
        - Aufhebung von Spezialbedeutung

#### Lektion 2

[Quelle](https://learning.lpi.org/de/learning-materials/010-160/2/2.1/2.1_02/)

- `env`: Variablen anzeigen
- lokale Variablen: nur im aktuellen Prozess verfügbar
    - Konvention: `kleinschreibung`
- Umgebungsvariablen: in aktuellem und in allen Unterprozessen verfügbar
    - Konvention: `GROSSSCHREIBUNG`
- Deklaration: `name=Wert` bzw. `NAME=Wert` (ohne Leerzeichen!)
- `export VARIABLE|DEFINITION`: macht lokale zu globaler Variablen
    - entweder
        - `export LOG_LEVEL=3`
    - oder
        - `LOG_LEVEL=3`
        - `export LOG_LEVEL`
- Variable für einen Unterprozess überschreiben:
    - `date`: gibt Datum und Uhrzeit unter Berücksichtigung der Zeitzone (`TZ`) aus
    - `TZ=UTC date`: gibt die UTC-Zeit aus
- Wert vs. Name
    - Beispiel: `LOG_LEVEL=3`
    - Name der Variablen: `LOG_LEVEL`
    - Zugriff auf ihren Wert: `$LOG_LEVEL` (mit führendem `$`!)
- `unset VARIABLE`: Variable entfernen
    - `unset LOG_LEVEL`
- `PATH`-Variable: Suchpfade für Befehle, durch `:` getrennt
    - Beispiel: `/usr/local/sbin:/usr/local/bin:/usr/bin`
    - Erweiterung: `export PATH=$PATH:$HOME/bin`
    - Wichtig: Reihenfolge beachten! Die erste Angabe "gewinnt".
- `which`: Datei zum Befehl suchen
    - `which bash`: `/usr/bin/bash`

### 2.2) 

[Quelle]

### 2.3)

### 2.4)
