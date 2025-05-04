# Block 4

## Ziel

- Thema 4 bearbeiten

## Ablauf

- Test mit Cloud Castle durchführen (Alternative zu OneClick)
- 2x
    - zwei Theorieblöcke
    - ein Übungsblock

## Thema 4: Das Linux-Betriebssystem

### 4.1) Ein Betriebssystem auswählen

[Quelle](https://learning.lpi.org/de/learning-materials/010-160/4/4.1/4.1_01/)

Verwendetes Betriebssystem anzeigen:

    uname -r
    uname -a

- Arten von Distributionen
    - Enterprise Linux
        - für den Einsatz in Unternehmen konzipiert
        - besondere Anforderungen an Stabilität bzw. spezielle Server-Hardware
        - z.B. Red Hat Enterprise Linux, Ubuntu LTS
    - Consumer Linux
        - für den Einsatz von Privatanwendern konzipiert
        - Fokus auf neuere Versionen bzw. Unterstützung von Consumer-Hardware
        - z.B. Fedora, Ubuntu non-LTS
    - "Experimentelle"
        - "rolling Release": keine grossen Releases der Distribution
        - kein kommerzieller Support, Support durch Community
        - z.B. Arch Linux, Gentoo
    - siehe auch [Distro Watch](https://distrowatch.com/)

### 4.2) Verständnis von Computer-Hardware

[Quelle](https://learning.lpi.org/de/learning-materials/010-160/4/4.2/4.2_01/)

Speicherauslastung anzeigen (in Megabyte):

    free -m

Prozessorinformationen auflisten (basiert auf `/proc/cpuinfo`):

    lscpu

Blockgeräte auflisten:

    lsblk

Partitionen:

- Warum sind mehrere Partionen sinnvoll?
- Warum ist der Speicher der Cloud-VMs _nicht_ partitioniert?

Peripheriegeräte auflisten (funktioniert _nicht_ auf Cloud-VM, da nicht installiert):

    lsusb

Weitere (Pseudo-)Hardware anzeigen lassen:

    ls -l /dev

Beginnt die Anzeige mit `b` für "Block", handelt es sich um ein Speichergerät.

### 4.3) Wo Daten gespeichert werden

#### Lektion 1

[Quelle](https://learning.lpi.org/de/learning-materials/010-160/4/4.3/4.3_01/)

- Verzeichnisstruktur gemäss [Filesystem Hierarchy Standard (FHS)](http://refspecs.linuxfoundation.org/fhs.shtml) (distributionsübergreifend)
- `/`: "Root"-Verzeichnis
- `/usr`: Software für Mehrbenutzermodus
- `/usr/local`: zusätzliche Software (nich von der Distribution verwaltet)
- `/opt`: weitere Software (oftmals kommerzieller Anbieter)
- Binärdateien
    - `/bin`: essentielle Programme
    - `/sbin`: essentielle Administrationsprogramme
    - `/usr/bin`: weitere Programme für Anwender
    - `/usr/sbin`: weitere Programme für Administratoren
    - oft sind `/bin` bzw. `/sbin` nur Verweise auf `/usr/bin` und `/usr/sbin`
    - `/usr/local/bin` und `/usr/local/sbin`: Programme, die nicht von der Distribution verwaltet werden
    - `$HOME/bin` oder `$HOME/.local/bin`: Programme des Benutzers
    - Der Speicherort von Programmen kann mit `which` ermittelt werden.
        - `which bash`
- Konfigurationsdateien
    - v.a. unter `/etc` ("et cetera") abgelegt
    - Dateien (oft ohne Suffix oder mit `.conf`)
    - Ordner (oft mit Suffix `.d`)
    - im Home-Verzeichnis mit Präfix `.` (ausgeblendet); Ordner und Dateien
- Kerneldateien
    - in `/boot` enthalten (oft als separate Partition)
- Prozessinformationen (Pseudo-Dateien)
    - in `/proc` enthalten
        - `/proc/cpuinfo`: Prozessorinformationen
        - `/proc/cmdline`: Kernel-Parameter
        - `/proc/modules`: geladene Kernelmodule
        - `/proc/sys`: Kernel-Konfigurationseinstellungen (oft mit Inhalt 1 oder 0)
- Geräte
    - in `/dev` enthalten
    - Blockgeräte: `/dev/sdXN`, z.B. `sda1` oder `sdb2`
    - Terminals: `/dev/ttyN`
    - Nullen (zum Lesen): `/dev/zero`
    - Mülleimer (zum Schreiben): `/dev/null`
    - Zufallszahlen: `/dev/urandom`
- Systeminformationen
    - in `/sys` enthalten
    - z.B. MAC-Adresse in `/sys/class/net/eth0/address`

#### Lektion 2

[Quelle](https://learning.lpi.org/de/learning-materials/010-160/4/4.3/4.3_02/)

- `top` (oder `htop`): Prozesse beobachten
    - zahlreiche Sortierungsmöglichkeiten:
        - `M`: Speicherverbrauch
        - `N`: Prozess-ID (PID)
        - `T`: Laufzeit
        - `P`: CPU-Auslastung (%)
        - `R`: auf- bzw. absteigende Sortierung
- `ps`: Prozesse auflisten
    - standardmässig: Prozesse des aktuellen Terminals
    - `-f`: ausführlichere Informationen
    - `-u`: Beziehungen zwischen Eltern- und Kindprozessen
    - `-v`: prozentualen Speicheverbrauch anzeigen
- `/proc`: dynamisch generierte Prozessinformationen im Dateiverzeichnis
- `uptime`: Systemlaufzeit und -last anzeigen
    - letzte Minute
    - letzte fünf Minuten
    - letzte fünfzehn Minuten
- `/var/log`: Logdateien
    - Zugriff mit `less`, `tail`
    - z.B. `/var/log/messages`
- `last`: Anmeldeinformationen gemäss `/var/log/wtmp`
- `dmesg`: Kernel-Nachrichten
- `journalctl`: systemd-Journal

### 4.4) Der Rechner im Netzwerk

[Quelle](https://learning.lpi.org/de/learning-materials/010-160/4/4.4/4.4_01/)

Netzwerkschnittstellen anzeigen:

    ip link show

Zusätzliche IP-Adresse hinzufügen:

    sudo ip addr add 192.168.0.5/255.255.255.0 dev eth0

Routen anzeigen:

    ip route show

Routing-Regeln definieren:

    sudo ip route add default via 192.168.0.1

Konfiguration des DNS-Resolvers einsehen (generierte Datei):

    cat /etc/resolv.conf

DNS-Lookup durchführen:

    host app.cloud-castle.ch

Erweiterter Lookup mit `dig` (Package: dnsutils):

    dig @8.8.8.8 +short app.cloud-castle.ch

Verwendete Sockets auflisten:

    ss
