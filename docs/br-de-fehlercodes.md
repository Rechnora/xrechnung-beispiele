# XRechnung-Fehlercodes: BR, BR-CO, BR-DE und BR-S erklärt

Wenn ein Validator eine E-Rechnung ablehnt, nennt er einen Code wie `BR-DE-5`.
Dieser Code zeigt immer auf ein konkretes Feld oder eine Rechenregel.

## Die Code-Familien

| Präfix | Herkunft | Typische Ursache |
|---|---|---|
| `BR-` | EN 16931 Grundregeln | Pflichtfeld fehlt |
| `BR-CO-` | EN 16931 Rechenregeln | Summen passen nicht zusammen |
| `BR-S-`, `BR-E-`, `BR-AE-`, `BR-Z-`, `BR-G-`, `BR-O-` | Steuerkategorien | Steuersatz und Kategorie widersprechen sich |
| `BR-DE-` | deutsche CIUS (XRechnung) | in Deutschland zusätzlich gefordertes Feld |
| `PEPPOL-` | Peppol BIS | nur beim Versand über Peppol relevant |

`BR-DE`-Regeln sind der häufigste Grund für Ablehnungen, weil sie über die
europäische Norm hinausgehen. Eine Rechnung kann EN-16931-konform sein und
trotzdem in Deutschland scheitern.

## Fehler oder Warnung?

- **error** — die Rechnung ist ungültig und wird abgelehnt.
- **warning** — die Rechnung ist gültig, ein Feld ist aber unvollständig oder
  unüblich. Manche Empfänger prüfen strenger als der Standardvalidator.

Reihenfolge beim Beheben: erst alle Fehler, dann die Warnungen, und nach jeder
Änderung erneut validieren.

## Häufige Codes

### Verkäuferangaben

| Code | Bedeutung | Lösung |
|---|---|---|
| `BR-DE-1` | Zahlungsangaben (BG-16) fehlen | Zahlungsart angeben; bei Überweisung IBAN ergänzen |
| `BR-DE-2` … `BR-DE-4` | Teile der Verkäuferanschrift fehlen | Straße, PLZ, Ort und Land vollständig hinterlegen |
| `BR-DE-5` | Name des Ansprechpartners (BT-41) fehlt | Kontaktperson in den Stammdaten pflegen |
| `BR-DE-6` | Telefonnummer des Verkäufers (BT-42) fehlt | Telefonnummer ergänzen |
| `BR-DE-7` | E-Mail des Verkäufers (BT-43) fehlt | Kontakt-E-Mail ergänzen |

### Identifikation

| Code | Bedeutung | Lösung |
|---|---|---|
| `BR-CO-26` | Weder Verkäufer-Kennung (BT-29), noch Registernummer (BT-30), noch USt-IdNr. (BT-31) vorhanden | mindestens eine davon angeben — für Kleinunternehmer ohne USt-IdNr. meist BT-30 |
| `BR-DE-15` | Leitweg-ID (BT-10) fehlt | nur bei öffentlichen Auftraggebern: Leitweg-ID des Empfängers eintragen |
| `BR-DE-17` | unzulässiger Rechnungstyp | nur zugelassene Codes verwenden: 326, 380, 384, 389, 381, 875, 876, 877 |

### Zahlung

| Code | Bedeutung | Lösung |
|---|---|---|
| `BR-DE-23` | Zahlungsmittel 58 (SEPA) ohne IBAN | IBAN ergänzen oder anderen Code wählen |
| `BR-DE-26` | Zahlungsmittel 68 mit widersprüchlichen Angaben | Detailangaben zum gewählten Code passend setzen |

### Summen

| Code | Bedeutung | Lösung |
|---|---|---|
| `BR-CO-10` | Summe der Positionen ≠ `LineExtensionAmount` | Positionsbeträge und Summenfeld exakt abgleichen |
| `BR-CO-13` | `TaxExclusiveAmount` passt nicht zu Positionen und Nachlässen | Rabatte und Zuschläge korrekt verteilen |
| `BR-CO-15` | `TaxInclusiveAmount` ≠ netto + Steuer | Rundung je Steuergruppe prüfen |

Summenregeln prüfen **auf den Cent genau**. Kaufmännisch plausibel genügt nicht.

### Steuerkategorien

| Code | Bedeutung | Lösung |
|---|---|---|
| `BR-S-08` | Steuerbetrag je Kategorie stimmt nicht | pro Steuersatz eine eigene Gruppe mit passender Bemessungsgrundlage |
| `BR-E-10` | steuerbefreite Position ohne Befreiungsgrund | `TaxExemptionReason` setzen |
| `BR-AE-10` | Reverse Charge ohne Befreiungsgrund | Hinweis auf die Steuerschuldnerschaft des Leistungsempfängers ergänzen |

Der häufigste Fehler in dieser Gruppe: eine Rechnung mit 19 % und 7 % wird in
**eine** Steuergruppe geschrieben. Richtig ist eine Gruppe je Steuersatz, und
jede Position verweist auf ihre eigene Kategorie.

## Einen Prüfbericht abarbeiten

1. Fehlercode und zugehörigen XPath oder die BT-Nummer notieren.
2. Das Feld im erzeugenden System identifizieren — meist fehlt eine
   Stammdatenangabe, kein technischer Defekt.
3. Wert ergänzen, Rechnung neu erzeugen.
4. Erneut validieren, bis keine Fehler mehr gemeldet werden.

## Quellen

- [KoSIT-Validator](https://github.com/itplr-kosit/validator)
- [XRechnung-Spezifikation (KoSIT)](https://xeinkauf.de/xrechnung/)
- Ausführlich erklärt: [XRechnung-Fehlercodes](https://rechnora.de/xrechnung-fehler-br-de-codes/)
