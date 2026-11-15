# ESP32 – geplante GPIO-Belegung

| Funktion | GPIO | Signal / Bedeutung |
|---|---:|---|
| Pumpe 1 | 16 | MOSFET-Gate über 100 Ω |
| Pumpe 2 | 17 | MOSFET-Gate über 100 Ω |
| Pumpe 3 | 18 | MOSFET-Gate über 100 Ω |
| Pumpe 4 | 19 | MOSFET-Gate über 100 Ω |
| Pumpe 5 | 21 | MOSFET-Gate über 100 Ω |
| Pumpe 6 | 22 | MOSFET-Gate über 100 Ω |
| Leckage Kemo M158 | 25 | INPUT_PULLUP; LOW = Relais NO geschlossen / Alarm |
| Tank-Schwimmerschalter | 26 | INPUT_PULLUP; HIGH = Wassermangel bzw. Unterbrechung (nach Kontaktprüfung) |
| Service-Taster | 32 | INPUT_PULLUP; LOW = gedrückt |
| RGB Blau | 33 | NPN/PNP-Treiber |
| RGB Grün | 14 | NPN/PNP-Treiber |
| RGB Rot | 13 | NPN/PNP-Treiber |

**Status:** Pinplanung; tatsächliche Verkabelung und Firmware noch nicht getestet.

## Grundregeln für die Firmware

1. Alle Pumpenausgänge beim Booten zunächst **AUS**.
2. Pumpen nur freigeben, wenn der Tankfüllstand plausibel und keine Leckage gemeldet ist.
3. Maximale Pumpenlaufzeit je Kanal erzwingen.
4. Zunächst nur eine Pumpe gleichzeitig betreiben; Stromaufnahme und Sicherungsdimensionierung messen.
5. Sensorausfälle und Wiederanlaufverhalten gesondert testen; die Kemo-NO-Leitung ist nicht ausfallsicher.
