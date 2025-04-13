# Block 3

## Ziel

## Ablauf

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

Kompression einzelner Dateien:

    $ zip ngerman.zip /usr/share/dict/ngerman
    $ bzip2 -k -c /usr/share/dict/ngerman > ngerman.bz2
    $ gzip -k -c /usr/share/dict/ngerman > ngerman.gz
    $ xz -k -c /usr/share/dict/ngerman > ngerman.xz
    $ du -h ngerman.*
    956K    ngerman.bz2
    836K    ngerman.gz
    616K    ngerman.xz
    836K    ngerman.zip

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

### 3.2)

### 3.3)