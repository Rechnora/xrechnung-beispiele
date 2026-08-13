# EN 16931: BT- und BG-Felder im Klartext

**BT** (Business Term) ist ein einzelnes Datenfeld, **BG** (Business Group)
eine Gruppe zusammengehöriger Felder. Prüfberichte verweisen auf diese Nummern.

## Die wichtigsten Felder

| Nummer | Bedeutung |
|---|---|
| BT-1 | Rechnungsnummer |
| BT-2 | Rechnungsdatum |
| BT-3 | Rechnungstyp (380 = Rechnung, 381 = Gutschrift) |
| BT-5 | Währung |
| BT-9 | Fälligkeitsdatum |
| BT-10 | Leitweg-ID (Buyer reference, bei B2G Pflicht) |
| BT-13 | Bestellnummer des Käufers |
| BT-27 | Name des Verkäufers |
| BT-29 | Kennung des Verkäufers |
| BT-30 | Registernummer des Verkäufers (z. B. Handelsregister) |
| BT-31 | USt-IdNr. des Verkäufers |
| BT-32 | Steuernummer des Verkäufers |
| BT-41 | Ansprechpartner beim Verkäufer |
| BT-42 | Telefonnummer des Verkäufers |
| BT-43 | E-Mail des Verkäufers |
| BT-44 | Name des Käufers |
| BT-48 | USt-IdNr. des Käufers |
| BT-72 | Liefer- bzw. Leistungsdatum |
| BT-81 | Zahlungsmittel-Code (58 = SEPA-Überweisung) |
| BT-84 | IBAN des Zahlungsempfängers |
| BT-106 | Summe der Positionsbeträge |
| BT-109 | Gesamtbetrag ohne Umsatzsteuer |
| BT-110 | Umsatzsteuerbetrag gesamt |
| BT-112 | Gesamtbetrag mit Umsatzsteuer |
| BT-115 | Zahlbetrag |
| BT-117 | Steuerbetrag je Kategorie |
| BT-118 | Steuerkategorie |
| BT-119 | Steuersatz je Kategorie |
| BT-120 | Grund der Steuerbefreiung |

## Wichtige Gruppen

| Nummer | Bedeutung |
|---|---|
| BG-4 | Verkäufer |
| BG-7 | Käufer |
| BG-16 | Zahlungsanweisungen |
| BG-23 | Aufschlüsselung nach Steuerkategorien |
| BG-25 | Rechnungsposition |

## Steuerkategorien (BT-118)

| Code | Bedeutung |
|---|---|
| `S` | Regelsteuersatz (19 % / 7 %) |
| `Z` | Nullsatz |
| `E` | steuerbefreit (z. B. Kleinunternehmer nach § 19 UStG) |
| `AE` | Reverse Charge — Steuerschuldnerschaft des Leistungsempfängers |
| `K` | innergemeinschaftliche Lieferung |
| `G` | Ausfuhrlieferung |
| `O` | nicht im Anwendungsbereich der Umsatzsteuer |

Bei `E`, `AE`, `K`, `G` und `O` ist ein Befreiungsgrund (BT-120) anzugeben.

## Syntax: UBL oder CII

EN 16931 ist syntaxneutral. Zugelassen sind zwei XML-Syntaxen:

- **UBL** (OASIS) — `Invoice` / `CreditNote`
- **CII** (UN/CEFACT) — `CrossIndustryInvoice`

XRechnung erlaubt beide. ZUGFeRD verwendet CII, eingebettet in eine PDF/A-3.
Der Inhalt ist identisch, nur die Verpackung unterscheidet sich — beide
Varianten liegen in diesem Repository als Beispiel vor.

## Quellen

- [XRechnung-Spezifikation](https://xeinkauf.de/xrechnung/)
- Einführung: [EN 16931 einfach erklärt](https://rechnora.de/en-16931-einfach-erklaert/)
