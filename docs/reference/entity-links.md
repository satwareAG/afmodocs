---
title: "Entity-Links Referenz"
category: "Referenz"
scope: "Verwenden wenn Benutzer nach internen Links, Hyperlinks, Querverweisen zwischen Datensätzen oder Navigation zwischen Entitäten in Amicron fragt"
last_updated: "2026-01-09"
author: "Michael Wegener, satware AG"
related_topics: ["Schnellsuche", "LFDNR", "Datenbank-Navigation", "Textfelder"]
search_keywords: ["link", "termin", "artikel", "aufgabe", "hyperlink", "navigation", "verknüpfung", "lfdnr", "schnellsuche"]
---

# Entity-Links in Amicron-Faktura

Amicron-Faktura unterstützt interne Hyperlinks, die Querverweise zwischen Datensätzen ermöglichen. Diese Links können in Textfelder (Bemerkung, Notizen, etc.) eingegeben oder eingefügt werden und werden zu klickbaren Navigationselementen.

## Link-Format

```
\\EntityType:LFDNR
\\EntityType:LFDNR (Optionale Bezeichnung)
```

### Bestandteile

| Bestandteil | Beschreibung | Erforderlich |
|-------------|--------------|--------------|
| `\\` | Doppelter Backslash als Präfix | ✅ Ja |
| `EntityType` | Entitätsbezeichner (Groß-/Kleinschreibung egal) | ✅ Ja |
| `:` | Trennzeichen | ✅ Ja |
| `LFDNR` | Interne Datensatz-ID (Datenbankspalte `LFDNR`) | ✅ Ja |
| `(Bezeichnung)` | Lesbare Beschreibung | ❌ Optional |

### Beispiele

```
\\Artikel:12345
\\artikel:12345
\\Termin:14186330 (MW: Besprechung mit Kunde)
\\aufgabe:14175522
```

## Verhalten

| Aspekt | Detail |
|--------|--------|
| **Groß-/Kleinschreibung** | **Nicht relevant** – `\\Termin:`, `\\terMin:`, `\\termin:` funktionieren alle |
| **Bezeichnung** | Optional – `\\termin:14186330` funktioniert ohne `(Bezeichnung)` |
| **Darstellung** | Amicron konvertiert zu klickbarem Hyperlink in Textfeldern |
| **Navigation** | Klick öffnet den referenzierten Datensatz in seiner Detailansicht |
| **Schnellsuche** | Links können zum Navigieren in die Schnellsuche eingefügt werden |

## Bekannte Entity-Typen

Die folgenden Entity-Typen unterstützen nachweislich Links. Die `LFDNR`-Spalte in jeder Datenbanktabelle enthält die Datensatz-ID.

| Entity-Typ | Deutscher Name | Datenbanktabelle | Beschreibung |
|------------|----------------|------------------|--------------|
| `Artikel` | Artikel | ARTIKEL | Produkte/Artikel |
| `Auftrag` | Kundenauftrag | AUFTRAG | Kundenaufträge |
| `Bestellung` | Lieferantenbestellung | AUFTRAG | Lieferantenbestellungen |
| `Kunde` | Kunde/Adresse | ADRESSEN | Kunden |
| `Lieferant` | Lieferant | ADRESSEN | Lieferanten |
| `Mitarbeiter` | Mitarbeiter | MITARBEITER | Mitarbeiter |
| `Termin` | Termin | TERMINE | Termine |
| `Aufgabe` | Aufgabe | AUFGABEN | Aufgaben |
| `contact` | Kontakt | KONTAKTE | Kontakte |
| `apos` | Auftragsposition | ATRPOS | Auftragspositionen |
| `bplate` | Textbaustein | TXTBAUSTEINE | Textbausteine |

> ⚠️ **Hinweis**: Diese Liste basiert auf Community-Recherche. Weitere Entity-Typen können existieren. Siehe [Mitwirken](../../CONTRIBUTING.md) um weitere hinzuzufügen.

## Anwendungsbeispiele

### In Textfeldern

Links funktionieren in jedem mehrzeiligen Textfeld:

- **Bemerkung** (Remarks)
- **Notizen** (Notes)
- **Beschreibung** (Description)

Beispiel in einem Termin:

```
08.01.2026 DH
\\aufgabe:14175522
Bitte:
1. Kundenkonto prüfen
2. Rückruf vereinbaren
```

### In der Schnellsuche

Füge einen Link direkt in das Schnellsuche-Feld ein zum Navigieren:

```
\\termin:14186330
```

### Links kopieren

1. Rechtsklick auf einen Datensatz
2. Wähle „Link kopieren" oder ähnliche Option
3. In Ziel-Textfeld einfügen

Das kopierte Format enthält die Bezeichnung:
```
\\Termin:14186330 (MW: DieJugendherbergen AI business platform anlegen (oB))
```

## Die LFDNR finden

Die `LFDNR` ist die interne Datensatz-ID. So findest du sie:

1. **In der Oberfläche**: Einige Ansichten zeigen die ID in der Statusleiste oder Titelzeile
2. **In der Datenbank**: Direkte Abfrage der `LFDNR`-Spalte
3. **Über Link kopieren**: Rechtsklick → Link kopieren enthält die LFDNR

## Technische Details

### Datenbank-Implementierung

Links werden als Klartext in Datenbankfeldern gespeichert. Amicrons UI-Schicht parst das `\\EntityType:LFDNR`-Muster und stellt klickbare Links dar.

### PHP Entity Bundle Referenz

Für Entwickler: Die `__toString()`-Methode in Entity-Klassen gibt das Link-Format zurück:

```php
public function __toString(): string
{
    return \sprintf('\\\\Artikel:%s (%s)', $this->getLfdnr(), $this->getArtikelnr());
}
```

Siehe: [satag-amicron-entity-bundle](https://github.com/satwareAG/satag-amicron-entity-bundle) (intern)

## Fehlerbehebung

### Link nicht klickbar

- Stelle sicher, dass doppelter Backslash `\\` als Präfix verwendet wird (nicht einzelnes `\`)
- Überprüfe die Schreibweise des Entity-Typs (obwohl Groß-/Kleinschreibung egal ist)
- Verifiziere, dass die LFDNR in der Datenbank existiert

### Link öffnet falschen Datensatz

- Die LFDNR wurde möglicherweise wiederverwendet (selten)
- Datensatz wurde möglicherweise gelöscht und ID neu vergeben

## Zukünftige Recherche

Die folgenden Entity-Typen müssen noch verifiziert werden:

- [ ] Rechnung (Invoice)
- [ ] Angebot (Quote)
- [ ] Lieferschein (Delivery note)
- [ ] Projekt (Project)

**Community-Mitglieder**: Bitte Erkenntnisse über [GitHub Issues](https://github.com/satwareAG/afmodocs/issues) oder die [satware® Amicron Business Solutions Community](https://www.facebook.com/groups/amicron) beitragen.

---

**Siehe auch:**
- [Tastenkürzel](./keyboard-shortcuts.md) (Platzhalter)
- [Datenbankschema](./database-schema.md) (Platzhalter)
