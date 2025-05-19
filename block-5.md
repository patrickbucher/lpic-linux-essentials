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

### Dateiberechtigungen und Dateieigentum verwalten

[Quelle](https://learning.lpi.org/de/learning-materials/010-160/5/5.3/5.3_01/)

### Besondere Verzeichnisse und Dateien

[Quelle](https://learning.lpi.org/de/learning-materials/010-160/5/5.4/5.4_01/)
