# Simple Grid Syntaxes For LLM Collaboration

A collection of lightweight, human-editable syntaxes for defining grid/table structures for ad-hoc collaboration with LLMs. Ideal for generating HTML/Markdown tables or CSS grids without verbose markup. Structure only—no embedded content or styling.

## Purpose

Large language models(LLM) can interpret abstract, human-friendly descriptions of grid and table structures and reliably generate correct HTML, Markdown, or CSS output. Pre-LLM markup languages (HTML tables, Markdown, CSS grid-template-areas, AsciiDoc, etc.) were designed for direct parsing by rigid tools and therefore tend to be verbose, repetitive, or cognitively taxing when merged cells are involved.

This repository proposes minimal, intuitive textual notations that separate structure from content and styling, allowing humans to describe grids quickly and naturally while leveraging the LLM as an intelligent translator to produce deployable code.

## About

**X**: [@5ynthaire](https://x.com/5ynthaire)  
**GitHub**: [https://github.com/5ynthaire](https://github.com/5ynthaire)  
**Mission**: Transcending creative limits through human-AI synergy  
**Attribution**: Developed with Grok 4.1 by xAI (no affiliation).  

## Visual Row Span Syntax 

Concept: Notate cells as visualized, with HTML \<table\> style cell merging, but using shorthands

**Syntax Rules**

- Lines represent rows.
- Entries are space-separated and aligned.
- Standalone "1" indicates a single 1x1 cell.
- "WxH" indicates a merged cell spanning W columns and H rows.
- Merged cells are only mentioned at their top-left primary position; covered positions below/right are skipped (blank/indented).

Example grid structure:
```
4x1
1x3 1 1 1
1 1 1
1 1 1
4x1
```

## Tensor Grid Syntax

Concept: Define the outer grid first, add modifications

**Syntax Rules**

- Base = columns x rows (total grid size; all start as 1x1 cells)
- Merges: list of "start_row,start_col - end_row,end_col" (1-indexed, inclusive, rectangular only)
- Only merged cells are specified; everything else is single 1x1

**Example**

```
Base = 4x5
Merges:
1,1 - 4,1    # top header
1,2 - 1,4    # left sidebar (3 rows high)
1,5 - 4,5    # bottom footer
```

## Useage

Collaborate with LLMs by providing

1. Syntax rules
2. Grid definition
3. Instructions

**Example input**
```
Generate a complete, standalone HTML <table> (with proper colspan and rowspan attributes) that exactly matches this grid structure. Use basic inline styles for borders, padding, and centering to make it visible. Fill cells with simple placeholder text like "Header", "Sidebar", "Cell RowX-ColY", or "Footer" since no content is provided.

**Syntax Rules**
- Lines represent rows.
- Entries are space-separated and aligned.
- Standalone "1" indicates a single 1x1 cell.
- "WxH" indicates a merged cell spanning W columns and H rows.
- Merged cells are only mentioned at their top-left primary position; covered positions below/right are skipped (blank/indented).

Grid structure:
4x1
1x3  1  1  1
      1  1  1
      1  1  1
4x1

```

**Example output**
```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Grid Table</title>
  <style>
    table { width: 100%; border-collapse: collapse; }
    td { border: 1px solid #000; padding: 20px; text-align: center; }
  </style>
</head>
<body>

<table>
  <tr>
    <td colspan="4">Header</td>
  </tr>
  <tr>
    <td rowspan="3">Sidebar</td>
    <td>Cell Row2-Col2</td>
    <td>Cell Row2-Col3</td>
    <td>Cell Row2-Col4</td>
  </tr>
  <tr>
    <td>Cell Row3-Col2</td>
    <td>Cell Row3-Col3</td>
    <td>Cell Row3-Col4</td>
  </tr>
  <tr>
    <td>Cell Row4-Col2</td>
    <td>Cell Row4-Col3</td>
    <td>Cell Row4-Col4</td>
  </tr>
  <tr>
    <td colspan="4">Footer</td>
  </tr>
</table>

</body>
</html>
```

## Comparison

| Aspect |  Visual Row Span Syntax | Tensor Grid Syntax |
|--------|-------------------------|--------------------|
| Best for | Irregular/art panels, small grids | Large data tables, few merges |
| Cognitive style | Drawing/sketching rows | Declarative ranges |
| Verbosity for uniform | Higher (explicit "1"s, copy-paste rows) | Lower (define once, list exceptions) |
| Visual intuitiveness | High (WYSIWYG alignment) | Medium (mental coordinate mapping) |
| LLM reliability | Excellent (explicit positions) | Excellent (simple list parsing) |


## License

Released under the [MIT License](LICENSE). Free to use, modify, and distribute.

