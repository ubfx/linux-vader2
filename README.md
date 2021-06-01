### Linux-Vader2
Dieses Repository dient zum Bauen der Linux-Vader2-Distribution.

## Grundkonfiguration
Die Grundkonfigurationsdatei findet sich unter `build/local.conf`. Dort müssen Verzeichnisse für Downloads, Cache und das Ausgabeverzeichnis festgelegt werden.

## Layers
Die einzelnen Yocto-Layer sind als Submodule referenziert, müssen also entsprechend gecloned werden.

## Allgemeine Anleitungen
Eine allgemeine Anleitung zur Verwendung von Yocto findet sich unter https://docs.yoctoproject.org/

## Einfacher Build-Prozess
Wenn Yocto entsprechend der Anleitung in der Yocto-Dokumentation korrekt installiert, alle Submodule gecloned sind und die Einstellungen in `local.conf` korrekt sind, kann die Distribution gebaut werden.

```
$ cd poky
$ source oe-init-build-env
$ bitbake vader2-image
```

## Erstellung von SD-Karten
Nach dem erfolgreichen Bauen der Distribution liegen ein Kernel-Image, sowie ein Bootloader, ein Bootloader-Skript und das rootfs im Ausgabeverzeichnis.

Eine Anleitung zur Formatierung der SD-Karte findet sich im [Xilinx Wiki](https://xilinx-wiki.atlassian.net/wiki/spaces/A/pages/18842385/How+to+format+SD+card+for+SD+boot)
Nach der Formatierung müssen das Kernel-Image (Dateiname "Image"), der Bootloader (Dateiname "boot.bin") und das Bootloader-Skript (Dateiname "boot.scr") auf die Boot-Partition kopiert werden.
Das rootfs muss auf die ext4-Partition kopiert werden.

## Wifi-Setup
Die Einstellungen für die WLAN-Verbindung finden sich im rootfs unter `/etc/wpa_supplicant.conf`. Dort wird die SSID und der Netzwerkschlüssel eingetragen.
Falls das WLAN sich nicht verbindet, kann es helfen, über die serielle Konsole `/etc/init.d/networking restart` auszuführen.

Spezifische Informationen zur Konfiguration des Vader2-Layers (Kernelkonfiguration, Hinzufügen/Entfernen von Software, ...) finden sich in der entsprechenden README-Datei im meta-vader2 Repository

## Hardware / Bitstream ändern
Aus Vivado kann eine .xsa-Datei exportiert werden, die die Konfiguration der Logik, des Prozessorsystems, der Interconnects usw. beinhaltet. Dazu nach erstellen des Bitstreams in Vivado auf *File->Export->Export Hardware* und anschließend *Include Bitstream* auswählen.

Die erzeugte .xsa-Datei wird in `system.xsa` umbenannt und in das Verzeichnis `build` bzw. `poky/build` kopiert. Wird anschließend das vader2-image neu gebaut, lädt der Bootloader die Hardware-Konfiguration automatisch beim Starten des Kernels.

Zum schnellen Testen empfiehlt es sich aber, Logik-Designs direkt aus Vivado über JTAG in die Programmierbare Logik zu flashen. Das funktioniert auch während der Prozessor/Linux läuft.