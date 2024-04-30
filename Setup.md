# Installieren von Raspberry OS

1. Download [Raspberry OS](https://www.raspberrypi.com/software/)
2. Exe ausführen
3. SD Karte auswählen
4. OS wählen (Raspberry Pi OS Lite 64 Bit)
	weiter
5. Einstellungen bearbeiten
6. Hostname ändern in: host-t07x > x= je nach Einteilung innerhalb des Teams a, b oder c
7. Die weiteren Abschnitte einrichte 
8. Zum Tab Dienste wechseln und SSH aktivieren
9. OS brennen

## Verbinden mit Raspberry

1. SD Karte in Raspberry einfügen
2. Raspberry an Pingen 'ping -4 host-t07x'
3. Über ssh mit Raspberry verbinden 'ssh user@ip'

# Raspberry einstellungen

- Copy bashrc file 'cp bashrc bashrc-SAVE'
- bashrc file bearbeiten je nach Präferenzen
## Swap grösse ändern

1. '/etc/dphys-swapfile' > dphys-swapfile öffnen
2. swapfactor auf 1 ändern
3. swapsize kommentieren
4. file speichern
5. 'service dphys-swapfile restart'

## Raspberry Config anpassen

1. 'raspi-config' in die Console eingeben
2. interface options auswählen
3. serial port aktivieren
