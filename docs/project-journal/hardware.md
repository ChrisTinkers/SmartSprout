# Hardware und Verdrahtung

**Status: geplant, soweit nicht anders angegeben.**

## Mechanischer Aufbau

- Lochrasterplatine ca. **160 × 100 mm**, einzelne voneinander isolierte Lötaugen (keine Streifenrasterplatine).
- Vier freie Ecken für M3-Befestigung, ca. 10 mm Abstandshalter, später 3D-gedrucktes Gehäuse.
- Komponenten zunächst trocken positionieren; kurze Verbindungen über Bauteilanschlüsse oder kurze Drahtbrücken, längere Kreuzungen mit isolierten Leitungen auf der Unterseite.
- Hauptversorgung vorzugsweise mit flexibler isolierter Kupferlitze **0,75 mm²**; Signale ca. **0,14–0,25 mm²**; Pumpenleitungen ggf. **0,5 mm²**, abhängig von Steckerkontakten.
- Verzweigung der gemeinsamen +12-V-Versorgung zu sechs Pumpen ist mechanisch noch festzulegen. Keine ungestützten Löt-T-Verbindungen oder überfüllten Lötaugen.

## Stromversorgung

- 12-V-/3-A-Netzteil, bislang gemessen **12,25 V**.
- Geplante **2-A-Sicherung** in der 12-V-Zuleitung.
- **470 µF / 35 V** zwischen +12 V und GND nach der Sicherung.
- **LM2596** als DC/DC-Wandler auf gemessene **5,04 V**; 5-V-Ausgang an ESP32-VIN (Pinbeschriftung des tatsächlich verwendeten Boards vor Anschluss prüfen).
- **100 µF / 35 V** zwischen 5 V und GND.
- Gemeinsame Masse für ESP32, Pumpen und Signalelektronik.

**Wichtig:** Kemo-M158-Versorgung und RGB-LED-Beschaltung vor Erstinbetriebnahme gesondert prüfen; siehe [Sicherheit](sicherheit.md).

## Pumpenkanäle (sechs vorgesehen)

- Fünf Kamoer **NKP-DC-B10G**, 12 V, vorhanden; sechster Kanal als Erweiterung.
- Je Kanal **IRLZ44N** als Low-Side-Schalter.
- Beim Blick auf die beschriftete flache Gehäuseseite des IRLZ44N: **Gate – Drain – Source** von links nach rechts (Einbaulage vor dem Löten prüfen).
- ESP32-GPIO → **100 Ω** → Gate; **10 kΩ** Gate → GND als Pulldown.
- Source → GND; Drain → Pumpen-Minus; Pumpen-Plus → +12 V.
- **1N5819** parallel zum Motor als Freilaufdiode: **Kathode/Markierungsring an +12 V**, Anode an Drain.
- **100 nF** Keramikkondensator parallel zum Motor.
- Pumpenleitungen auf der Platine direkt angelötet; je Pumpe ein **zweipoliger Micro-Fit-3.0-Stecker** ungefähr zwischen Platine und Pumpe, beschriftet P1–P6.
- Im Fritzing-Plan gezeichnete Schraubklemmen sind **Platzhalter**, keine vorgesehenen realen Schraubklemmen.
- Zugentlastung am Gehäuse, nicht durch die Lötstellen.

## RGB-Service-Taster

- TRU Components **TC-GQ16F-10E41RGB**, Conrad 1873653, 12-V-Ausführung, gemeinsame LED-Kathode.
- Taster: COM → GND; NO → GPIO32 mit internem Pullup; NC nicht genutzt.
- RGB-Kathode → GND.
- Je Farbe eine zweistufige Transistorschaltung: NPN **BC547B** steuert PNP **BC327-40** als High-Side-Treiber.
- GPIO → **4,7 kΩ** → NPN-Basis; NPN-Basis → **10 kΩ** → GND; NPN-Emitter → GND.
- NPN-Kollektor → **10 kΩ** → PNP-Basis; PNP-Basis → **10 kΩ** → +12 V.
- PNP-Emitter → +12 V; PNP-Kollektor → jeweilige RGB-Anode.
- Die Strombegrenzung der 12-V-LED ist **noch nicht verifiziert**. Nicht ohne Klärung einschalten.
- Taster fest verdrahtet, mit ausreichend Kabelreserve.

## Sensorik

### Kemo M158 Leckageüberwachung

- Geplante Versorgung aus 12-V-Zweig; **Achtung: 12,25 V gemessen, Modul spezifiziert bis 12 V**. Versorgung vor Anschluss korrigieren/absichern.
- Wasserfühler an die dafür vorgesehenen Elektrodenanschlüsse.
- Potentialfreier Relaiskontakt NO zwischen GPIO25 und GND, interner GPIO-Pullup.
- Geplante Interpretation: trocken = HIGH, nass/Alarm = LOW.
- **Nicht ausfallsicher:** Unterbrochene Signalleitung oder Stromausfall am Kemo werden mit NO-Kontakt nicht zuverlässig als Leckage erkannt.
- Modul trocken und erhöht, Elektroden tief in einer Auffangschale montieren.

### Schwimmerschalter

- PIC **PLS-041B-3PPI**, NC, zwischen GPIO26 und GND, interner Pullup.
- Gewünschte Funktion: Wasser vorhanden → geschlossen/LOW; Wassermangel oder Kabelbruch → offen/HIGH → Pumpensperre.
- Tatsächliche Schaltlage und Montageorientierung **vorher mit Multimeter verifizieren**.
- Tank ca. **6 l**; Befüllen am Standort und Herausheben zur Reinigung vorgesehen, nur im Rahmen der Kabel-/Schlauchreserve.

## Montage und Löttechnik

- ESP32 steckbar über zwei 2,54-mm-Buchsenleisten; tatsächliche Pinzahl und Reihenabstand vorher prüfen.
- Ersa RDS 80, Ersa 0842CD 2,2-mm-Meißelspitze, Felder ISO-Core SAC305 0,75 mm.
- Ca. 350 °C als Ausgangspunkt; mit stromloser Platine arbeiten, Dämpfe gezielt abführen.
- **Erst einen Pumpenkanal komplett aufbauen und messen**, dann weitere Kanäle.
