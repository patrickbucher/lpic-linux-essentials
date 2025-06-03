# Block 5

## Ablauf/Ziel

- Informationen über das Ablegen der Prüfung
- Thema 4 abschliessen
- Thema 5 anfangen

## Thema 5: Sicherheit und Dateiberechtigungen

### Sicherheitsgrundlagen und Identifizierung von Benutzertypen

[Quelle](https://learning.lpi.org/de/learning-materials/010-160/5/5.1/5.1_01/)

- User und Group Identifier (UID/GID)
    - unabhängig voneinander nummeriert mit 64-Bit-Zahl
    - i.d.R. wird pro Benutzer auch eine Gruppe mit gleicher ID angelegt
    - pro Benutzer gibt es eine primäre Gruppe und beliebig viele weitere Gruppenzugehörigkeiten
    - `root`: UID 0, GID 0 mit Home-Verzeichnis `/root`
- Standard-Benutzerkonten
    - UID/GID starten für normale Benutzer bei 1000 (aufsteigend durchnummeriert)
    - für jeden Benutzer wird ein Home-Verzeichnis (unterhalb `/home`) und eine Login-Shell festgelegt
- System-Benutzerkonten und Service-Accounts
    - UID/GID unter 100 bzw. zwischen 500 und 1000 bei Sytem-Benutzerkonten (normalerweise höhere Rechte)
    - UID/GID > 1000 bei Service-Accounts (normalerweise eingeschränkte Rechte)
    - `/sbin/nologin` als Login-Shell verbietet interaktives Login
- Login-Shells
    - z.B. `bash`, `csh`, `ksh`, `zsh`
    - mithilfe von `chsh` änderbar
        - für sich selber: `$ chsh -s /usr/bin/bash`
        - für anderen Benutzer: `# chsh USERNAME -s /usr/bin/bash`
- Benutzerinformationen abfragen
    - `id`: zeigt UID/GID und Gruppenzugehörigkeiten an
    - `last`: zeigt letzte Anmeldungen an
    - `w` und `who`: aktive Anmeldungen
- Benutzerwechsel
    - `su`: Login als Super-User
        - `su -`: Umgebung initialisieren
        - `su USER`: zu Benutzer `USER` werden
        - `su USER -`: zu Benutzer `USER` werden und dessen Umgebung initialisieren
    - `sudo`: Befehl als Super-User ausführen ("super user do")
        - `sudo BEFEHL`: Befehl als Super-User ausführen
        - `sudo su -`: ohne Passwort zum Super-User werden
- Konfigurationsdateien
    - `/etc/passwd`: Informationen über Benutzerkonten (keine Passwörter!)
        - sog. GECOS-Daten via `chfn` änderbar
    - `/etc/group`: Informationen über Benutzergruppen
    - `/etc/shadow`: gehashte Passwörter für Benutzerkonten
        - via `passwd` änderbar
    - `/etc/gshadow`: detaillierte Gruppeninformationen, inkl. gehashte Passwörter
    - `/etc/sudoers`: Konfiguration von `sudo`
        - Achtung: immer nur über `visudo` anpassen! (Syntaxprüfung, Backup)
    - `/etc/sudoers.d/`: ergänzende `sudo`-Konfigurationen

### Benutzer und Gruppen anlegen

[Quelle](https://learning.lpi.org/de/learning-materials/010-160/5/5.2/5.2_01/)

- `useradd(8)`: Benutzer hinzufügen
    - `-c`: Kommentar (z.B. voller Name)
    - `-d`: Home-Verzeichnis spezifizieren (bei Abweichungen von `/home/BENUTZERNAME`)
    - `-f N`: Passwort muss innerhalb von `N` Tagen aktualisiert werden
    - `-g GID`: GID definieren
    - `-G GROUPS`: Den Benutzer weiteren Gruppen hinzufügen
    - `-m`: ein Home-Verzeichnis erstellen
    - `-s SHELL`: Login-Shell definieren
    - `-u UID`: UID definieren
    - Der Inhalt des Home-Verzeichnis wird aus "Skeleton-Verzeichnis" `/etc/skel` erstellt
- `userdel(8)`: Benutzer entfernen
    - `-r`: auch Home-Verzeichnis löschen
- `groupadd(8)`: Benutzergruppe hinzufügen
    - `-g GID`: GID definieren
- `groupdel(8)`: Benutzergruppe entfernen
- `passwd [BENUTZER]`: Passwort ändern
    - `-d`: Passwort löschen (passwortloses Konto)
    - `-e`: Passwortänderung durch Benutzer erzwingen
    - `-l`: Benutzerkonto sperren
    - `-u`: Sperrung aufheben
    - `-S`: Statusinformationen ausgeben

### Dateiberechtigungen und Dateieigentum verwalten

[Quelle](https://learning.lpi.org/de/learning-materials/010-160/5/5.3/5.3_01/)

- dreistufiges Sicherheitskonzept
    1. Besitzer (user: `u`)
    2. Gruppe (group: `g`)
    3. Rest (others: `o`)
- Ausgabe von `ls -l` (erste Spalte):
    - `drwxr-x---`
        - Typ: `d`: Verzeichnis (directory)
        - user: `rwx`: read, write, execute
        - group: `r-x`: read, execute
        - others: `---`: [keine Berechtigungen]
        - "execute" steht in diesem Kontext für das Betreten eines Verzeichnisses
    - `-rw-rw-r--`
        - Typ: `-`: Datei (file)
        - user: `rw-`: read, write
        - group: `rw-`: read, write
        - others: `r--`: read
- Bedeutung für Dateien
    - `r`: Datei lesen (ausgeben)
    - `w`: Datei schreiben (editieren)
    - `x`: Datei ausführen (Skript, Binärprogramm)
- Bedeutung für Verzeichnisse
    - `r`: Dateinamen auflisten
    - `w`: Dateien im Verzeichnis erstellen & löschen; Berechtigungen ändern
    - `x`: ins Verzeichnis wechseln (mit `cd`)
- weitere Typen:
    - `l`: soft link
    - `b`: block device
    - `c`: character device
    - `s`: socket
- Oktalwerte
    - `r`: 4
    - `w`: 2
    - `x`: 1
- Anpassung der Berechtigungen mit `chmod`
    - absolut: mit Oktalzahlen ("numeric mode")
        - `chmod 777`: setzt alle Berechtigungen auf `rwx`
        - `chmod 750`: setzt die Berechtigungen auf `rwxrw----`
        - `chmod 644`: setzt die Berechtigungen auf `rw-r--r--`
    - relativ: mit Stufenangabe ("symbolic mode")
        - `chmod ug+x,o-r`: dem Besitzer und der Gruppe "execute" erlauben; dem Rest "read" verbieten
        - `chmod +r`: allen "read" erlauben
- Anpassung des Dateibesitzes
    - Besitzer: `chown user DATEI` ("CHange OWNership")
    - Besitzer & Gruppe: `chown user:group DATEI`
    - Gruppe: `chgrp group DATEI` ("CHange GRouP")
- Spezialberechtigungen
    - Leitfragen
        - Wie kann ich verhindern, dass Benutzer in einem geteilten Verzeichnis Dateien löschen oder umbenennen?
        - Wie kann ich es normalen Benutzern erlauben, Programme mit den Berechtigungen einer priviligierten Gruppe auszuführen?
        - Wie kann ich es normalen Benutzern erlauben, Programme mit den Berechtigugnen eines priviligierten Benutzers auszuführen?
    - Sticky Bit: 1 bzw. `t` statt `x` in "others"
        - Verhindert Löschung/Umbenennung von Datei durch Nicht-Besitzer.
        - `chmod 1755`
        - `chmod o+t`
    - Set GID: 2 bzw. `s` statt `x` in "group"
        - Dateien: Prozess läuft mit Berechtigung der Gruppe statt des ausführenden Benutzers.
        - Verzeichnisse: Darunterliegende Verzeichnisse erben Gruppenberechtigung.
        - `chmod 2755`
        - `chmod g+s`
    - Set UID: 4 bzw. `s` statt `x` in "user"
        - Dateien: Prozess läuft mit Berechtigung des Besitzers statt des ausführenden Benutzers.
        - `chmod 6755`
        - `chmod u+s`

### Besondere Verzeichnisse und Dateien

[Quelle](https://learning.lpi.org/de/learning-materials/010-160/5/5.4/5.4_01/)
