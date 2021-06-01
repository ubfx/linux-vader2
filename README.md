### Linux-Vader2
Dieses Repository dient zum Bauen der Linux-Vader2-Distribution.

## Layers
Die einzelnen Yocto-Layer sind als Submodule referenziert, müssen also entsprechend gecloned werden.

## Allgemeine Anleitungen
Eine allgemeine Anleitung zur Verwendung von Yocto findet sich unter https://docs.yoctoproject.org/

## Erstellung von SD-Images
Nach dem erfolgreichen Bauen der Distribution liegen ein Kernel-Image, sowie ein Bootloader, ein Bootloader-Skript und das rootfs im Ausgabeverzeichnis.

Eine Anleitung zur Formatierung der SD-Karte findet sich unter https://xilinx-wiki.atlassian.net/wiki/spaces/A/pages/18842385/How+to+format+SD+card+for+SD+boot
Nach der Formatierung müssen das Kernel-Image (Dateiname "Image"), der Bootloader (Dateiname "boot.bin") und das Bootloader-Skript (Dateiname "boot.scr") auf die Boot-Partition kopiert werden.
Das rootfs muss auf die ext4-Partition kopiert werden.

## Wifi-Setup
Die Einstellungen für die WLAN-Verbindung finden sich im rootfs unter `/etc/wpa_supplicant.conf`. Dort wird die SSID und der Netzwerkschlüssel eingetragen.
Falls das WLAN sich nicht verbindet, kann es helfen, über die serielle Konsole `/etc/init.d/networking restart` auszuführen.

Spezifische Informationen zur Konfiguration des Vader2-Layers (Kernelkonfiguration, Hinzufügen/Entfernen von Software, ...) finden sich in der entsprechenden README-Datei im meta-vader2 Repository