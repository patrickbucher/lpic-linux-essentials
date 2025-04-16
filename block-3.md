# Block 3

## Ziel

- Kompression und Dekompression auf der Kommandozeile verwenden können
- Daten in Dateien suchen und extrahieren (`grep`) können
- einfache Skripte schreiben können

## Ablauf

- Erneuter Test OneClick (sollte nun funktionieren)
- 3x
    - Theorieblock à 15 min.
    - Übungsblock à 10 min.

## Thema 3: Die Macht der Befehlszeile

### 3.1) Dateien mithilfe der Befehlszeile archivieren

[Quelle](https://learning.lpi.org/de/learning-materials/010-160/3/3.1/3.1_01/)

- Arten von Kompression
    - verlustbehaftet: v.a. Bilder, Audios und Videos (jpeg, mp3, h264, h265, aom usw.)
    - verlustfrei: Software, Dokumente, Quellcode (exe, docx, txt usw.)
        - Schulbuch-Beispiel: [Huffman-Kodierung](https://www.paedubucher.ch/articles/dfde-huffman/)
- Mechanismen
    - Archivierung: mehrere Dateien zu "Tarballs" (.tar) zusammenführen
    - Komprimierung: einzelne Datei (auch Tarball) verkleinern (zip, bzip2, gzip, xz usw.)
- Kompromiss: Kompressionsrate & Kompressionsgeschwindigkeit
    - hohe Kompressionsrate: kleinere Dateien, langsamere Kompression
    - tiefe Kompressionsrate: grössere Dateien, schnellere Kompression
    - Portabilität: zip funktioniert praktisch überall

Kompression einzelner Dateien (Vorsicht: Quelldatei wird standardmässig gelöscht!):

Beispieldaten (grosse Textdateien): Wörterbücher

    $ sudo apt install wswiss wngerman

Programme:

    $ sudo apt install zip unzip bzip2

Kompression einzelner Datien:

    $ /usr/share/dict/swiss .
    $ zip swiss.zip swiss
    $ bzip2 swiss
    $ bunzip2 swiss.bz2

    $ zip ngerman.zip /usr/share/dict/ngerman
    $ bzip2 -k -c /usr/share/dict/ngerman > ngerman.bz2
    $ gzip -k -c /usr/share/dict/ngerman > ngerman.gz
    $ xz -k -c /usr/share/dict/ngerman > ngerman.xz
    $ du -h ngerman.*
    956K    ngerman.bz2
    836K    ngerman.gz
    616K    ngerman.xz
    836K    ngerman.zip

Standardmässig wird die Textdatei ins gleiche Verzeichnis (`/usr/share/dict`) geschrieben und gelöscht. Dies ist aufgrund der fehlenden Berechtigung nicht möglich. Darum soll die Originaldatei mit `-k` beibehalten und mit `-c` die Ausgabe auf die Standardausgabe ausgegeben werden, die dann in eine Datei umgeleitet wird.

Angabe der Kompressionsstufe (kleinere Zahl = höhere Kompression):

    $ bzip2 -k -c -1 /usr/share/dict/ngerman > ngerman.1.bz2
    $ bzip2 -k -c -9 /usr/share/dict/ngerman > ngerman.9.bz2
    $ du -h ngerman.*.bz2
    888K    ngerman.1.bz2
    956K    ngerman.9.bz2

Dekompression:

    $ unzip ngerman.zip
    $ bunzip2 ngerman.bz2
    $ gunzip ngerman.gz
    $ unxz ngerman.xz

Betrachten von komprimierten Textdateien (Präfix `z` für gzip):

    $ zcat ngerman.gz
    $ zless ngerman.gz

Gebräuchlicher ist die Verwendung von `tar`, welches Archive erstellt und die
Kompression sogleich weiterdelegiert:

- Kompression
    - `-c`: "create" (Archiv erstellen)
    - `-f`: "filename" (Dateiname des Archivs)
    - Algorithmus
        - `-j`: bzip2
        - `-z`: gzip
        - `-J`: xz
- Dekompression
    - `-x`: "eXtract" (Archiv entpacken)

Beispiel:

    $ tar -cjf words.tar.bz2 /usr/share/dict/*

Bestehende unkomprimierte(!) Archive können auch erweitert werden.

Verzeichnisse werden automatisch rekursiv komprimiert. (Bei `zip` ist `-r` nötig.)

### 3.2) Daten in Dateien suchen und extrahieren

#### Lektion 1

[Quelle](https://learning.lpi.org/de/learning-materials/010-160/3/3.2/3.2_01/)

Prozesse können mit Dateien interagieren. Jeder Prozess hat standardmässig drei _File Handles_:

- 0: `stdin` (Standardeingabe)
    - Umleitung: `<`, z.B. `sort <words.txt`
- 1: `stdout` (Standardausgabe)
    - Umleitung: `>`, z.B. `ls >files.txt`
- 2: `stderr` (Standardfehler)
    - Umleitung: `2>`, z.B. `find / 2>errors.txt`

Mit `>` wird die Ausgabedatei überschrieben! Mit `>>` wird Inhalt angehängt.

Standardausgabe und -fehler in die gleiche Datei umleiten:

    find / >out.txt 2>&1

Alternative Syntax:

    find / &>out.txt

"Die Ausgabe in `out.txt`, die Fehler in die gleiche Datei wie die Ausgabe!"

Das pseudo-Gerät `/dev/null` fungiert als "schwarzes Loch", wenn man Informationen ignorieren möchte:

    find / 2>/dev/null

Mithilfe einer _Pipe_ wird die Ausgabe von einem Prozess zur Eingabe vom nächsten Prozess:

    cat some-words.txt more-words.txt | grep '^[A-Z]' | sort | uniq | head

Die einzelnen Prozesse können dabei teilweise _parallell_ ausgeführt werden!

[Unix-Philosophie](https://shop.elsevier.com/books/the-unix-philosophy/gancarz/978-0-08-094819-5): Programme sind _Filter_ und verzichten möglichst auf Interaktion.

#### Lektion 2

[Quelle](https://learning.lpi.org/de/learning-materials/010-160/3/3.2/3.2_02/)

Der Befehl `grep`:

- Herkunft: Editor-Befehl "Global Regular Expression Print"
- Verwendung: Filterung von Textzeilen nach Mustern (reguläre Ausdrücke)
- Parameter
    - `-i`: case insensitiv
    - `-r`: rekursive Suche durch Verzeichnisbaum
    - `-c`: Anzahl Treffer ("count")
    - `-v`: invertierte Suche (unpassende Ergebnisse anzeigen)
    - Auswahl des Dialekts (in aufsteigender Komplexität)
        - `-F`: Suche nach fixen Strings
        - `-G`: grundlegende reguläre Ausdrücke (Standard), siehe `man 7 regex` oder [Mastering Regular Expressions](https://www.oreilly.com/library/view/mastering-regular-expressions/0596528124/)
        - `-E`: erweiterte reguläre Ausdrücke (Alias: `egrep` für `grep -E`)
        - `-P`: Perl-kompatible reguläre Ausdrücke (PCRE)

Moderne Neuimplementierung: [ripgrep](https://github.com/BurntSushi/ripgrep) alias `rg`

### 3.3) Von Befehlen zum Skript

Zum Schreiben von Skripten benötigt man einen Texteditor:

- `nano`: einsteigerfreundlich
- `emacs`: eisnteigerfreundlich, aber sehr mächtig
    - verwendet v.a. Tastenkombinationen
- `vi`, `vim`: für Fortgeschrittene
    - verwendet Modi: Navigationsmodus, Bearbeitungsmodus, Befehlsmodus
- `ed`: für Masochisten (oder für Leute mit Nadeldrucker aber ohne Bildschirm)

Beispiel: `nano hello.sh`

```sh
echo "Hello, World!"
```

Skript ausführbar machen:

```sh
chmod +x hello.sh
```

Skript ausführen:

```sh
./hello.sh
```

Zur Erinnerung: Nur Skripte inerhalb der in `$PATH` aufgelisteten Verzeichnisse können mit dem Namen ausgeführt werden!

Der Interpreter wird mit der sogenannten "Shebang"-Zeile ("Hash, Bang") angegeben:

```sh
!#/usr/bin/bash
```

Zur Erinnerung: Variablen wurden in [Block 2](block-2.md) behandelt.

Argumente sind durchnummerierte Variablen (`$1`, `$2`). `$0` ist der Name des jeweiligen Skripts. `$#` beinhaltet die Anzahl der mitgegebenen Argumente.

Logik mit `if`/`then`/`else`:

```sh
#!/usr/bin/bash

if [ $# -eq 1 ]
then
    echo "Hello, $1."
else
    echo "Hello."
fi
```

`[` ist ein Alias für `test` (eingebauter Shell-Befehl). Siehe `man 1 test`.