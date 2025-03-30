# Block 2

## Ziel

- Grundlagen der Befehlszeile erarbeiten (Befehle, Variablen).
- Wissen, wie man sich selber helfen kann.
- Dateien suchen und finden.

## Ablauf

- erneuter Test OneClick
- Theorie Unterthemen 2.1 und 2.2
- Übungen Unterthemen 2.1 und 2.2
- Theorie Unterthemen 2.3 und 2.4
- Übungen Unterthemen 2.3 und 2.4
- Fragerunde

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

[Quelle](https://learning.lpi.org/de/learning-materials/010-160/2/2.2/2.2_01/)

- eingebaute Hilfe: `BEFEHL --help` oder `BEFEHL -h`
    - nicht immer einheitlich, eher kurz
- Manpages (_manual pages_)
    - umfassende Hilfeseiten zu Befehlen und anderen Konzepten
        - in mehrere Abschnitte gegliedert (immer ähnlicher Aufbau)
        - mithilfe von Pager betrachtet (`less`)
    - mehrere Bereiche
        - 1: Benutzerbefehle
        - 5: Konfigurationsdateien, Dateiformate
        - 7: Verschiedenes
        - 8: Systemadministrationsbefehle
    - `man`
        - `man BEGRIFF`
            - z.B. `man passwd` (Benutzerbefehl)
        - `man BEREICH BEGRIFF`
            - z.B. `man 5 passwd` (Konfigurationsdatei)
    - `apropos SUCHBEGRIFF`
        - `apropos auth`: in allen Bereichen suchen
        - `apropos -s 1 auth`: nur in Benutzerbefehlen suchen
    - `whatis BEFEHL`
        - Erklärung zu bekanntem Befehl erhalten
- GNU Info
    - Ersatz/Ergänzung zu Manpages vom GNU-Projekt
    - mit Verlinkung
    - `info BEGRIFF`
- Dateien suchen
    - `locate`: sucht nach Name im Index
        - Index muss mit `updatedb` neu erstellt werden
    - `find`: Filtert Dateien in Echtzeit
        - Syntax: `find PFAD FILTER1 FILTER2 …`
        - `find ~ -type d -name Steuern`
        - `find ~ -type f -iname '*rechnung*.pdf`

### 2.3) Verzeichnisse verwenden und Dateien auflisten

#### Lektion 1

[Quelle](https://learning.lpi.org/de/learning-materials/010-160/2/2.3/2.3_01/)

- `tree`: Auflistung eines Verzeichnis(unter)baums
- Konvention: keine Leerzeichen und Sonderzeichen in Dateinamen!
    - erfordert Escaping/Quoting: `cd Steuern\ Jahr \ 2024` oder `cd 'Steuern Jahr 2024'`
- `pwd`: aktuelles Arbeitsverzeichnis ausgeben
- absolute Pfade: beginnen mit `/`
- spezielle Pfade
    - `.`: aktuelles Verzeichnis
    - `..`: Elternverzeichnis
- `ls`: Dateien/Verzeichnisse auflisten
    `-a`: auch versteckte Dateien/Verzeichnisse
        - starten mit `.` im Namen

#### Lektion 2

[Quelle](https://learning.lpi.org/de/learning-materials/010-160/2/2.3/2.3_02/)

- `/`: Wurzelverzeichnis
    - organisiert gemäss _Filesystem Hierarchy Standard_ (FHS)
    - nur durch `root` bearbeitbar
- `/home/$USER`: durch Benutzer `$USER` bearbeitbar
    - Alias: `~` entspricht `$HOME` entspricht `/home/$USER`
- `ls`: Dateien/Verzeichnisse auflisten
    `-l`: detaillierte Auflistung
         - Dateityp und Berechtigung
         - Anzahl der Links zur Datei
         - Eigentümer und -gruppe
         - Grösse in Byte
         - letzte Änderung
         - Dateiname
    - weitere Optionen: siehe Manpage!
        - `-lh`, `-d`, `-t`, `-r`, `-X`, `-S`, `-R`

### 2.4) Erstellen, Verschieben und Löschen von Dateien

[Quelle](https://learning.lpi.org/de/learning-materials/010-160/2/2.4/2.4_01/)

- `mkdir`: Verzeichnis anlegen
    - `mkdir -p`: fehlende Elternverzeichnise mitanlegen
- `touch`: Datei anlegen oder deren Zeitstempel aktualisieren
- `mv`: Datei "verschieben" bzw. umbenennen
    - `-i`: interaktiv (nachfragen)
- `rm`: Dateien und Verzeichniss löschen
    - `-r`: rekursiv (für Verzeichnisse)
    - `-i`: interaktiv (nachfragen)
- `rmdir`: leere Verzeichnisse löschen
- `cp`: kopieren von Dateien und Verzeichnissen
    - `-r`: rekursiv (für Verzeichnisse)
- Glob-Patterns
    - `*`: beliebige Zeichen (0, 1, n)
    - `?`: ein oder kein Zeichen (0, 1)
    - `[]`: Zeichenklasse
        - z.B. `[aeiou]` für Vokale
        - z.B. `[0-9a-zA-Z]` für alpha-numerische Zeichen
    - `[[:ZEICHENKLASSE:]]` siehe `man 7 regex`

