# Block 1

## Ziel

- Alle haben Zugang zu Ihrer Linux-VM via OneClick.
- Wir haben die Linux-spezifischen Inhalte zu Thema 1 durchgearbeitet.
    - Quelle: [Linux Essentials: Thema 1](https://learning.lpi.org/de/learning-materials/010-160/)

## Ablauf

1. Setup OneClick
2. Inhalte Thema 1
3. Bearbeiten der Übungen
4. Varia
    - Fragerunde
    - persönlicher Support

## Thema 1: Die Linux-Community und Karriere im Open-Source-Umfeld

> **Achtung**: Wir behandeln im Rahmen der sechs Kursabende nur
> Linux-spezifische Inhalte. Allgemeine Informatik-Themen werden vorausgesetzt.
> Wer die Zertifikatsprüfung ablegen will, sollte die Inhalte selbständig
> studieren und die Übungen dazu lösen!

### Die Entwicklung von Linux und gängige Betriebssysteme

- Linux: Unix-artiges Betriebssystem ohne Unix-Code
- Linux-Distribution: Linux-Kernel + Auswahl von Software + Infrastruktur
    - Debian-Familie: `deb`-Pakete; Befehle: `apt`, `dpkg`
        - Debian GNU/Linux: umfassend, vielfältig, stabil
        - Ubuntu: einsteigerfreundlich
    - Red-Hat-Familie: `rpm`-Pakete; Befehl: `yum`, `rpm`
        - Red Hat Enterprise Linux (RHEL): v.a. für Servereinsatz
        - CentOS: Upstream von RHEL
        - Fedora: Desktop-Variante
    - viele weitere (SUSE, Arch), siehe [DistroWatch.com](https://distrowatch.com/)
        - für Smartphones: Android
        - für Container: CoreOS, Alpine
        - für Raspi: Raspbian
        - für Pentester: Kali
    - Achtung: FreeBSD, NetBSD, OpenBSD usw. basieren auf Unix, nicht auf Linux!
- Verbreitung
    - Desktop: vernachlässigbar
    - Webserver: ca. 68% der Server
    - Cloud: 90% der Arbeitslast (Stand: 2017)

### Die wichtigsten Open-Source-Anwendungen

Paketsysteme:

| Familie | Paketformat | Programm (low-level) | Programm (high-level) |
|---------|-------------|----------------------|-----------------------|
| Debian  | deb         | `dpkg`               | `apt`                 |
| Red Hat | rpm         | `rpm`                | `yum`                 |

Befehle:

| Zweck                                    | Debian                | Red Hat                |
|------------------------------------------|-----------------------|------------------------|
| verfügbare Pakete auflisten              | `apt list`            | `yum list --available` |
| installierte Pakete auflisten            | `dpkg -l`             | `yum list --installed` |
| Paket suchen                             | `apt search NAME`     | `yum search NAME`      |
| Paketdetails anzeigen                    | `apt show NAME`       | `yum info NAME`        |
| Paket installieren                       | `apt install NAME`    | `yum install NAME`     |
| Paketindex aktualisieren                 | `apt update`          | `yum update`           |
| Pakete aktualisieren                     | `apt upgrade`         | `yum upgrade`          |
| Paket deinstallieren                     | `apt remove NAME`     | `yum remove NAME`      |
| Paket inkl. Konfiguration deinstallieren | `apt purge NAME`      | ?                      |
| Paket mit Abhängigkeiten deinstallieren  | `apt autoremove NAME` | `yum autoremove NAME`  |
| Paket anhand von Dateinamen installieren | `dpkg -S FILE`        | `yum provides FILE`    |
| Paketinhalte (Dateien) auflisten         | `dpkg -L NAME`        | `repoquery -l NAME`    |
| Unnötige Abhänigkeiten deinstallieren    | `apt autoremove`      | `yum autoremove`       |
| Cache leeren                             | `apt autoclean`       | `yum clean all`        |

Anwendungsprogramme:

| Zweck               | Windows           | Linux                       |
|---------------------|-------------------|-----------------------------|
| Büroanwendungen     | Microsoft Office  | OpenOffice.org, LibreOffice |
| Textverarbeitung    | Office Word       | Writer                      |
| Tabellenkalkulation | Office Excel      | Calc                        |
| Präsentationen      | Office PowerPoint | Impress                     |
| Groupware           | Office Outlook    | Thunderbird                 |
| Bildverarbeitung    | Adobe Photoshop   | GIMP                        |
| Web-Browser         | Edge              | Firefox, Chromium           |
| Web-Server          | IIS               | Apache, nginx, ligthttpd    |
| Datenbankserver     | SQL Server        | MySQL/MariaDB, PostgreSQL   |

Weitere Software:

- Audacity: Audio-Editor
- Blender: 3D-Modellierung
- VLC: Multimedia-Wiedergabe
- ownCloud, Nextcloud: Cloud-Server

- Mit _Samba_ kann eine Linux-Workstation an einen Windows-Domänencontroller angehängt werden.
    - weiter: Teilen von Dateien, Druckern zwischen Windows und Linux
- Mit _NFS_ werden Linux-Dateisysteme übers Netzwerk geteilt.

### Open-Source-Software und -Lizenzen

> "Free" as in "freedom", not "free beer".

- freie Software: vier Freiheiten
    1. Programm unbeschränkt ausführen
    2. Programm untersuchen und anpassen
    3. Programm redistribuieren
    4. Programm verbessern
- Open-Source-Software: der Quellcode ist einsehbar

Copyright & Copyleft:

- Das Copyright sichert dem Urheber Rechte zu.
- Das Copyleft basiert auf dem Copyright und erlaubt es dem Urheber,
  Bedingungen für die Weitergabe festzulegen.
- Share-Alike-Lizenzen: Änderungen müssen unter gleichen Bedingungen
  weitergegeben werden.
    - z.B. GPL
- Permissive Lizenzen: Weitergabe weniger geregelt
    - z.B. BSD, Apache
- Beispiel: OpenOffice.org (permissiv) und LibreOffice (share-alike)
    - LibreOffice darf Anpassungen von OpenOffice.org übernehmen
    - OpenOffice.org darf _keine_ Anpassungen von LibreOffice übernehmen
        - "virale" Lizenz GPL verlangt Freigabe des Quellcodes
- Creative Commons bietet verschiedene Optionen (permissive/share-alike)

Geschäftsmodelle:

- Dual Licensing: frei für Privatgebrauch, kostenpflichtig für professionellen
  Gebrauch (z.B. Red Hat, VirtualBox)
- kostenpflichtiger Support (u.a. im Abomodell)
- Angebot als Service (z.B. Nextcloud)
- Schulungen, Zertifizierungen (z.B. Moodle)

### IKT-Fähigkeiten und Arbeiten mit Linux

