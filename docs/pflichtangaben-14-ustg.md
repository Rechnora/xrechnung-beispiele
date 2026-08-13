# Pflichtangaben einer Rechnung nach § 14 UStG

§ 14 Abs. 4 UStG listet die Angaben auf, die eine Rechnung enthalten muss.
Fehlt eine davon, darf der Rechnungsempfänger die Vorsteuer nicht ziehen.

| # | Pflichtangabe | Feld in EN 16931 |
|---|---|---|
| 1 | vollständiger Name und Anschrift des leistenden Unternehmers | BG-4 |
| 2 | vollständiger Name und Anschrift des Leistungsempfängers | BG-7 |
| 3 | Steuernummer oder USt-IdNr. des Ausstellers | BT-31 / BT-32 |
| 4 | Ausstellungsdatum | BT-2 |
| 5 | fortlaufende, einmalige Rechnungsnummer | BT-1 |
| 6 | Menge und Art der gelieferten Gegenstände oder Umfang der Leistung | BT-129, BT-153 |
| 7 | Zeitpunkt der Lieferung oder Leistung | BT-72 |
| 8 | nach Steuersätzen aufgeschlüsseltes Entgelt | BG-23 |
| 9 | Steuersatz und Steuerbetrag, oder Hinweis auf die Steuerbefreiung | BT-119, BT-117, BT-120 |

## Worauf es in der Praxis ankommt

**Die Rechnungsnummer (BT-1)** muss einmalig vergeben und fortlaufend sein.
Eine strikt lückenlose Reihe schreibt das Gesetz nicht ausdrücklich vor, Lücken
sind bei einer Betriebsprüfung aber erklärungsbedürftig. Bestellnummern aus
einem Shopsystem eignen sich nicht, weil abgebrochene Bestellungen Lücken
erzeugen.

**Der Leistungszeitpunkt (BT-72)** wird am häufigsten vergessen. Er ist eine
eigene Pflichtangabe neben dem Rechnungsdatum; die Angabe des Kalendermonats
genügt.

**Die Aufschlüsselung nach Steuersätzen (BG-23)** verlangt eine eigene
Steuergruppe je Satz. Eine Rechnung mit 19 % und 7 % braucht zwei Gruppen.

**Bei Steuerbefreiung** ist der Grund anzugeben — etwa
„Steuerschuldnerschaft des Leistungsempfängers“ bei Reverse Charge oder
„Kleinunternehmer gemäß § 19 UStG“.

## Zusätzlich bei innergemeinschaftlichen B2B-Umsätzen

- USt-IdNr. des Leistungsempfängers (BT-48)
- ausdrücklicher Hinweis auf die Steuerschuldnerschaft des Leistungsempfängers
- kein Steuerausweis, Steuersatz 0 %, Kategorie `AE`

Ist die USt-IdNr. des Kunden ungültig, kann das Finanzamt die Steuerfreiheit
versagen — die Steuer schuldet dann der Rechnungsaussteller.

## Quellen

- [§ 14 UStG](https://www.gesetze-im-internet.de/ustg_1980/__14.html)
- Ausführlich: [B2B-Rechnung: Pflichtfelder](https://rechnora.de/shopify-b2b-rechnung/)
