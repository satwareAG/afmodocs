# Contributing to Amicron Faktura Documentation

Thank you for contributing to the AFMO ERFA community documentation!

## How to Contribute

### ERFA Members: Adding FAQs from Support Tickets

1. **Identify a common question** from your support tickets
2. **Find the right FAQ file** in `docs/faq/` (or request a new one)
3. **Add your Q&A** following the template below
4. **Submit a Pull Request**

### FAQ Entry Template

```markdown
## Q: [Clear question as the customer would ask it]

**Quick Answer:** [1-2 sentence answer]

**Details:** [Longer explanation if needed]

**See also:** [Link to full documentation](../reference/related-doc.md)

**Source:** ERFA Support Ticket (anonymized)
```

### Adding Technical Reference

For undocumented features or technical details:

1. Create a new file in `docs/reference/`
2. Use the frontmatter template below
3. Include examples and screenshots where possible

### Frontmatter Template

```yaml
---
title: "Your Document Title"
category: "Reference|FAQ|Tutorial|Troubleshooting"
scope: "Use when user asks about [specific topic]"
last_updated: "YYYY-MM-DD"
author: "Your Name or ERFA-anonymous"
related_topics: ["topic1", "topic2"]
search_keywords: ["keyword1", "keyword2"]
---
```

## Documentation Structure

```
docs/
├── getting-started/     # Quickstart guides
├── reference/           # Technical reference (single-topic files)
├── vendor-reference/    # Original Amicron docs (do not modify)
├── community/           # Tutorials and tips
├── faq/                 # Per-topic FAQ files
└── troubleshooting/     # Problem-solution docs
```

## Guidelines

### DO ✅

- Keep files focused (1000-3000 words, single topic)
- Use clear, searchable headings
- Include practical examples
- Link to related documentation
- Add frontmatter metadata

### DON'T ❌

- Create monolithic documents
- Duplicate existing content
- Modify `vendor-reference/` files
- Include customer-identifiable information
- Add unverified information without marking it

## RAG Optimization Tips

This documentation is indexed by AI tools. To improve retrieval:

1. **Use descriptive headings** that match how users ask questions
2. **Include keywords** in frontmatter `search_keywords`
3. **Keep paragraphs focused** on single concepts
4. **Use bullet points** for lists of steps or items

## Questions?

Contact the maintainers:
- Michael Wegener: mw@satware.com
- ERFA Arbeitskreis: [Internal contact]

---

*Documentation is auto-indexed by DeepWiki weekly when the badge is present in README.*
