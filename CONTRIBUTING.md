# Mitwirken an der Amicron-Faktura Dokumentation

Vielen Dank für deinen Beitrag zur [satware® Amicron Business Solutions Community](https://www.facebook.com/groups/amicron)-Dokumentation!

## Wie du beitragen kannst

### Community-Mitglieder: FAQs aus Support-Tickets hinzufügen

1. **Identifiziere eine häufige Frage** aus deinen Support-Tickets
2. **Finde die passende FAQ-Datei** in `docs/faq/` (oder fordere eine neue an)
3. **Füge deinen Frage-Antwort-Eintrag hinzu** nach der Vorlage unten
4. **Erstelle einen Pull Request**

### FAQ-Eintrags-Vorlage

```markdown
## F: [Klare Frage, wie der Kunde sie stellen würde]

**Kurze Antwort:** [1-2 Sätze Antwort]

**Details:** [Ausführlichere Erklärung bei Bedarf]

**Siehe auch:** [Link zur vollständigen Dokumentation](../reference/zugehoerige-doku.md)

**Quelle:** Community Support-Ticket (anonymisiert)
```

### Technische Referenz hinzufügen

Für undokumentierte Features oder technische Details:

1. Erstelle eine neue Datei in `docs/reference/`
2. Verwende die Frontmatter-Vorlage unten
3. Füge Beispiele und Screenshots hinzu, wo möglich

### Frontmatter-Vorlage

```yaml
---
title: "Dein Dokumenttitel"
category: "Reference|FAQ|Tutorial|Troubleshooting"
scope: "Verwenden wenn Benutzer nach [spezifischem Thema] fragt"
last_updated: "JJJJ-MM-TT"
author: "Dein Name oder Community-anonym"
related_topics: ["thema1", "thema2"]
search_keywords: ["stichwort1", "stichwort2"]
---
```

## Dokumentationsstruktur

```
docs/
├── getting-started/     # Schnellstart-Anleitungen
├── reference/           # Technische Referenz (Einzelthemen-Dateien)
├── vendor-reference/    # Original Amicron-Doku (nicht ändern)
├── community/           # Tutorials und Tipps
├── faq/                 # Themenspezifische FAQ-Dateien
└── troubleshooting/     # Problem-Lösungs-Dokumentation
```

## Richtlinien

### MACHEN ✅

- Dateien fokussiert halten (1000-3000 Wörter, einzelnes Thema)
- Klare, durchsuchbare Überschriften verwenden
- Praktische Beispiele einbeziehen
- Auf verwandte Dokumentation verlinken
- Frontmatter-Metadaten hinzufügen

### NICHT MACHEN ❌

- Monolithische Dokumente erstellen
- Bestehende Inhalte duplizieren
- Dateien in `vendor-reference/` ändern
- Kundenidentifizierbare Informationen einbeziehen
- Ungeprüfte Informationen ohne Kennzeichnung hinzufügen

## RAG-Optimierungstipps

Diese Dokumentation wird von KI-Tools indexiert. Um die Auffindbarkeit zu verbessern:

1. **Beschreibende Überschriften verwenden**, die zur Art passen, wie Benutzer Fragen stellen
2. **Stichwörter einbeziehen** im Frontmatter `search_keywords`
3. **Absätze fokussiert halten** auf einzelne Konzepte
4. **Aufzählungszeichen verwenden** für Listen von Schritten oder Elementen

## Fragen?

Kontaktiere die Maintainer:
- Michael Wegener: mw@satware.com
- [satware® Amicron Business Solutions Community](https://www.facebook.com/groups/amicron)

---

*Die Dokumentation wird wöchentlich automatisch von DeepWiki indexiert, wenn das Badge in der README vorhanden ist.*
