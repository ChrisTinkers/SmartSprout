# Sicherheit und Prüfplan

## Vor dem ersten Einschalten – offene Punkte

- [ ] **Kemo M158:** Datenblatt-Grenze 12 V mit gemessenen 12,25 V des Netzteils abgleichen. Vor Anschluss geeignete Versorgung **innerhalb der Spezifikation** bereitstellen; nicht einfach 12,25 V anlegen.
- [ ] **RGB-Taster:** Nachweisen, ob die 12-V-RGB-LED bereits geeignete Vorwiderstände/Strombegrenzung enthält. Andernfalls je Farbe korrekt dimensionierte Vorwiderstände vorsehen.
- [ ] **Schwimmerschalter:** Kontaktzustände bei vollem und leerem Tank sowie bei Leitungsunterbrechung mit Multimeter prüfen.
- [ ] **ESP32:** tatsächliche Board-Pinbelegung, VIN-Tauglichkeit und Sockelabstände prüfen.
- [ ] **MOSFETs und Transistoren:** Pinbelegung der konkret gelieferten Bauteile vor dem Löten gegen Datenblatt kontrollieren.
- [ ] **Stromversorgung:** Sicherung, Leitungsquerschnitte, Masseführung und maximale Pumpenströme prüfen.
- [ ] **Leckagesensor:** NO-Kontakt testweise auslösen; Verhalten bei Stromausfall oder Drahtbruch ausdrücklich dokumentieren.

## Messungen an stromloser Platine

- [ ] Sichtkontrolle beider Seiten und mechanische Zugentlastung.
- [ ] Keine ungewollten Brücken zwischen benachbarten isolierten Lötaugen.
- [ ] Kein Kurzschluss zwischen +12 V und GND bzw. +5 V und GND.
- [ ] Freilaufdioden polaritätsrichtig.
- [ ] Gate-Pulldowns und Widerstandswerte plausibel.
- [ ] MOSFET-Gate nicht unbeabsichtigt mit Drain oder Source verbunden.

## Kontrollierte Inbetriebnahme

- [ ] Spannungen ohne ESP32 und ohne empfindliche Verbraucher kontrollieren.
- [ ] LM2596-Ausgang vor Anschluss an ESP32 messen.
- [ ] Zunächst nur einen Pumpenkanal testen.
- [ ] Abschaltung bei niedrigem Wasserstand, Leckage und Zeitlimit testen.
- [ ] Verhalten nach Neustart, Stromausfall und Sensorfehlern prüfen.
- [ ] Stromaufnahme unter Last messen; Sicherungswert erst danach endgültig bestätigen.

**Grundsatz:** Ein geplanter Schutz ist erst nach realem Funktionstest als geprüft zu markieren.
