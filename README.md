# XRechnung- und ZUGFeRD-Beispieldateien (EN 16931)

Validierte Beispieldateien und deutschsprachige Referenz zur E-Rechnung.
Jede Datei in diesem Repository wurde mit dem **offiziellen KoSIT-Validator**
(XRechnung 3.0.2) geprüft und wird als *accepted* zurückgegeben — ohne Fehler.

Gedacht für Entwickler, die eine E-Rechnung erzeugen oder einlesen müssen, und
für Händler, die wissen wollen, wie eine gültige E-Rechnung von innen aussieht.

---

## Warum es dieses Repository gibt

Die E-Rechnungspflicht in Deutschland verweist auf die Norm **EN 16931**. Wer
zum ersten Mal eine XRechnung erzeugt, scheitert selten am Konzept, sondern an
Details: eine fehlende Telefonnummer, eine Steuerkategorie, die nicht zum
Steuersatz passt, ein Summenfeld, das um einen Cent abweicht.

Öffentliche, *validierte* Beispiele für genau diese Fälle sind in deutscher
Sprache schwer zu finden. Dieses Repository schließt die Lücke.

## Fristen (Stand 2026)

| Ab wann | Was gilt | Für wen |
|---|---|---|
| 01.01.2025 | E-Rechnungen **empfangen** und aufbewahren | alle Unternehmen |
| bis 31.12.2026 | Übergangsfrist: PDF im B2B noch zulässig | alle |
| 01.01.2027 | E-Rechnungen **ausstellen** | Vorjahresumsatz > 800.000 € |
| 01.01.2028 | E-Rechnungen **ausstellen** | alle übrigen |

Betroffen sind Rechnungen an Geschäftskunden in Deutschland (B2B).
B2C ist ausgenommen.

## Die Beispieldateien

| Datei | Fall | Besonderheit |
|---|---|---|
| [`beispiele/ubl/rechnung-gemischte-steuersaetze.xml`](beispiele/ubl/rechnung-gemischte-steuersaetze.xml) | Rechnung mit 19 % und 7 % | zwei `TaxSubtotal`-Gruppen, je Position eigene Kategorie |
| [`beispiele/ubl/rechnung-reverse-charge.xml`](beispiele/ubl/rechnung-reverse-charge.xml) | B2B ins EU-Ausland | Kategorie `AE`, 0 %, beide USt-IdNr., Befreiungsgrund |
| [`beispiele/ubl/rechnung-kleinunternehmer.xml`](beispiele/ubl/rechnung-kleinunternehmer.xml) | § 19 UStG | Kategorie `E`, Steuernummer statt USt-IdNr., **BT-30 nötig** |
| [`beispiele/ubl/gutschrift.xml`](beispiele/ubl/gutschrift.xml) | Gutschrift / Storno | Typ `381`, Bezug auf die Ursprungsrechnung |
| [`beispiele/cii/rechnung-gemischte-steuersaetze.xml`](beispiele/cii/rechnung-gemischte-steuersaetze.xml) | dieselbe Rechnung in CII | UN/CEFACT-Syntax statt UBL |

Alle Dateien enthalten ausschließlich frei erfundene Firmen, Adressen,
Steuernummern und IBANs.

## Referenz

- [**BR-DE-Fehlercodes erklärt**](docs/br-de-fehlercodes.md) — was `BR-DE-5`,
  `BR-CO-10` oder `BR-S-08` bedeuten und wie man sie behebt
- [**Pflichtangaben nach § 14 UStG**](docs/pflichtangaben-14-ustg.md) — die
  neun Angaben und ihre BT-Nummern
- [**EN 16931: BT- und BG-Felder**](docs/en16931-feldreferenz.md) — die
  wichtigsten Feldnummern im Klartext

## Selbst validieren

Der offizielle Validator der KoSIT ist frei verfügbar:

```bash
# Validator + Konfiguration von https://github.com/itplr-kosit/validator laden
java -jar validationtool-x.x.x-standalone.jar \
     -s scenarios.xml \
     -r . \
     beispiele/ubl/rechnung-gemischte-steuersaetze.xml
```

Ergebnis `accepted` bedeutet: die Datei erfüllt EN 16931 **und** die deutschen
Zusatzregeln der XRechnung.

Wer nur schnell eine Datei prüfen will, ohne Java zu installieren, kann den
kostenlosen [E-Rechnung-Checker](https://rechnora.de/e-rechnung-checker/)
im Browser verwenden.

## Häufige Stolpersteine

1. **Eine PDF ist keine E-Rechnung.** Maßgeblich sind die strukturierten Daten.
   Bei ZUGFeRD ist die eingebettete XML das Original, nicht die PDF-Ansicht.
2. **BR-DE-Regeln gehen über EN 16931 hinaus.** Eine europaweit gültige
   Rechnung kann in Deutschland an einer `BR-DE`-Regel scheitern — etwa am
   fehlenden Ansprechpartner (BT-41) oder der Telefonnummer (BT-42).
3. **Kleinunternehmer ohne USt-IdNr.** brauchen eine andere Kennung, sonst
   greift `BR-CO-26`. Im Beispiel gelöst über die Handelsregisternummer (BT-30).
4. **Summen müssen exakt aufgehen.** `BR-CO-10` und `BR-CO-13` prüfen auf den
   Cent genau; kaufmännisch gerundet reicht nicht.
5. **Die Rechnungsnummer** muss einmalig und fortlaufend sein (BT-1). Die
   Bestellnummer aus dem Shop ist dafür ungeeignet, weil sie Lücken enthält.

## Weiterführend

Ausführliche deutschsprachige Erklärungen zu diesen Themen:

- [E-Rechnungspflicht 2027/2028](https://rechnora.de/e-rechnungspflicht-shopify-2027-2028/)
- [XRechnung vs. ZUGFeRD](https://rechnora.de/xrechnung-vs-zugferd-shopify/)
- [E-Rechnungen GoBD-konform archivieren](https://rechnora.de/e-rechnung-archivieren-gobd/)
- [Reverse Charge und USt-IdNr.](https://rechnora.de/reverse-charge-shopify-ust-id/)
- [EN 16931 einfach erklärt](https://rechnora.de/en-16931-einfach-erklaert/)

## Über Rechnora

Gepflegt von [Rechnora](https://rechnora.de) — einer Shopify-App, die aus jeder
Bestellung automatisch eine geprüfte E-Rechnung (XRechnung und ZUGFeRD) erzeugt,
GoBD-konform archiviert und für DATEV exportiert.
[Im Shopify App Store ansehen](https://apps.shopify.com/xrechnung-exporter).

Fehler gefunden oder ein Beispiel vermisst? Gern ein Issue eröffnen.

## Lizenz

Beispieldateien und Dokumentation stehen unter
[CC BY 4.0](LICENSE) — Verwendung erlaubt, auch kommerziell, mit Namensnennung.

---

*Diese Sammlung ist keine Steuerberatung und ersetzt kein Gespräch mit einem
Steuerberater.*
