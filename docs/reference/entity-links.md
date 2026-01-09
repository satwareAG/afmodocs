---
title: "Entity Links Reference"
category: "Reference"
scope: "Use when user asks about internal links, hyperlinks, cross-referencing records, or navigating between entities in Amicron"
last_updated: "2026-01-09"
author: "Michael Wegener, satware AG"
related_topics: ["Schnellsuche", "LFDNR", "Database Navigation", "Textfelder"]
search_keywords: ["link", "termin", "artikel", "aufgabe", "hyperlink", "navigation", "verknüpfung", "lfdnr", "schnellsuche"]
---

# Entity Links in Amicron Faktura

Amicron Faktura supports internal hyperlinks that allow cross-referencing between records. These links can be typed or pasted into text fields (Bemerkung, Notizen, etc.) and become clickable navigation elements.

## Link Format

```
\\EntityType:LFDNR
\\EntityType:LFDNR (Optional Label)
```

### Components

| Component | Description | Required |
|-----------|-------------|----------|
| `\\` | Double backslash prefix | ✅ Yes |
| `EntityType` | Entity identifier (case-insensitive) | ✅ Yes |
| `:` | Separator | ✅ Yes |
| `LFDNR` | Internal record ID (database column `LFDNR`) | ✅ Yes |
| `(Label)` | Human-readable description | ❌ Optional |

### Examples

```
\\Artikel:12345
\\artikel:12345
\\Termin:14186330 (MW: Besprechung mit Kunde)
\\aufgabe:14175522
```

## Behavior

| Aspect | Detail |
|--------|--------|
| **Case Sensitivity** | **Case-insensitive** - `\\Termin:`, `\\terMin:`, `\\termin:` all work |
| **Label** | Optional - `\\termin:14186330` works without `(Label)` |
| **Rendering** | Amicron converts to clickable hyperlink in text fields |
| **Navigation** | Click opens the referenced record in its detail view |
| **Schnellsuche** | Links can be pasted into Quick Search for navigation |

## Known Entity Types

The following entity types are confirmed to support links. The `LFDNR` column in each database table contains the record ID.

| Entity Type | German Name | Database Table | Description |
|-------------|-------------|----------------|-------------|
| `Artikel` | Artikel | ARTIKEL | Products/Articles |
| `Auftrag` | Kundenauftrag | AUFTRAG | Customer orders |
| `Bestellung` | Lieferantenbestellung | AUFTRAG | Supplier orders |
| `Kunde` | Kunde/Adresse | ADRESSEN | Customers |
| `Lieferant` | Lieferant | ADRESSEN | Suppliers |
| `Mitarbeiter` | Mitarbeiter | MITARBEITER | Employees |
| `Termin` | Termin | TERMINE | Appointments |
| `Aufgabe` | Aufgabe | AUFGABEN | Tasks |
| `contact` | Kontakt | KONTAKTE | Contacts |
| `apos` | Auftragsposition | ATRPOS | Order line items |
| `bplate` | Textbaustein | TXTBAUSTEINE | Text templates |

> ⚠️ **Note**: This list is based on community research. Additional entity types may exist. See [Contributing](../../CONTRIBUTING.md) to add more.

## Usage Examples

### In Text Fields

Links work in any multi-line text field:

- **Bemerkung** (Remarks)
- **Notizen** (Notes)
- **Beschreibung** (Description)

Example in a Termin (Appointment):

```
08.01.2026 DH
\\aufgabe:14175522
Bitte:
1. Kundenkonto prüfen
2. Rückruf vereinbaren
```

### In Schnellsuche

Paste a link directly into the Quick Search field to navigate:

```
\\termin:14186330
```

### Copying Links

1. Right-click on a record
2. Select "Link kopieren" or similar option
3. Paste into target text field

The copied format includes the label:
```
\\Termin:14186330 (MW: DieJugendherbergen AI business platform anlegen (oB))
```

## Finding the LFDNR

The `LFDNR` is the internal record ID. To find it:

1. **In the UI**: Some views display the ID in the status bar or title
2. **In the database**: Query the `LFDNR` column directly
3. **Via link copy**: Right-click → Copy Link includes the LFDNR

## Technical Details

### Database Implementation

Links are stored as plain text in database fields. Amicron's UI layer parses the `\\EntityType:LFDNR` pattern and renders clickable links.

### PHP Entity Bundle Reference

For developers: The `__toString()` method in entity classes returns the link format:

```php
public function __toString(): string
{
    return \sprintf('\\\\Artikel:%s (%s)', $this->getLfdnr(), $this->getArtikelnr());
}
```

See: [satag-amicron-entity-bundle](https://github.com/satwareAG/satag-amicron-entity-bundle) (internal)

## Troubleshooting

### Link Not Clickable

- Ensure double backslash `\\` prefix (not single `\`)
- Check entity type spelling (though case-insensitive)
- Verify LFDNR exists in the database

### Link Opens Wrong Record

- The LFDNR may have been reused (rare)
- Record may have been deleted and ID reassigned

## Future Research

The following entity types need verification:

- [ ] Rechnung (Invoice)
- [ ] Angebot (Quote)
- [ ] Lieferschein (Delivery note)
- [ ] Projekt (Project)

**ERFA members**: Please contribute findings via [GitHub Issues](https://github.com/satwareAG/afmodocs/issues).

---

**See also:**
- [Keyboard Shortcuts](./keyboard-shortcuts.md) (placeholder)
- [Database Schema](./database-schema.md) (placeholder)
