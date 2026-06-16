---
name: brooklet-word-document-style
description: Use this skill whenever drafting, revising, or formatting Brooklet Word documents, especially agreements, internal notes, and memos. Trigger this skill whenever the user asks for Word output, asks to match prior Brooklet formatting, requests a cleaner legal-professional style, or wants separate format rules for agreement, note, and memo documents.
---

# Brooklet Word Document Style Skill

## Purpose
This skill fixes the default formatting, structure, and language style for Brooklet Word outputs.

The output must feel:
- clean;
- concise;
- professional;
- commercially sensible; and
- easy to review, circulate, and finalise in Word.

This skill must first identify the document type and then apply the relevant format lane:
- Agreement style;
- Note style; or
- Memo style.

## Universal formatting rules
- Font: **Candara** throughout.
- Body text: **12 pt**.
- All table text: **12 pt**.
- Keep spacing neat and conservative.
- Avoid excessive blank lines.
- Avoid decorative formatting.
- Keep headings functional and short.
- Use bracketed placeholders such as [•], [CLIENT], [DATE], [ADDRESS] where information is missing.
- Use **TBC** where a fact exists but is not yet verified.
- Keep the final draft clean enough to paste into Word with minimal tidy-up.
- **Dashes:** Never use en-dash (–) or em-dash (—) in any document. Standard keyboards cannot produce these characters. Use a single hyphen (-) for ranges and hyphenation, or a double hyphen (--) where an em-dash feel is needed. This applies to all text including date ranges, page ranges, and compound terms.
- **All numbered items must use Word-native automatic numbering.** See the "Automatic numbering (mandatory)" section below -- this rule is non-negotiable for every Brooklet Word output. Any paragraph that appears to be part of a numbered list (action items, outstanding points, conclusions, recommendations, numbered steps, etc.) MUST use Word's paragraph-level auto-numbering -- never hard-code "1.", "2.", "3." as literal text.

## Document routing
Before drafting, determine which of the following three styles applies.

### A. Agreement
Use this lane for:
- services agreements;
- referral agreements;
- engagement letters with contractual effect;
- any client-facing legal document with operative clauses.

### B. Note
Use this lane for:
- internal deal notes;
- candidate assessments;
- licence / regulatory summaries;
- short working papers for internal review.

### C. Memo
Use this lane for:
- internal advisory memoranda;
- issue analysis papers;
- structured explanations of a legal, regulatory, or commercial point;
- documents that require more analysis than a note, but are not drafted as contracts.

---

## Agreement lane

### Purpose
Use a formal, clause-based drafting style aligned with Brooklet's agreement templates.

### Agreement formatting
- Center the title.
- Use uppercase for the main agreement title.
- Begin with a formal opening line, e.g. "THIS AGREEMENT is dated [•]..."
- Use clearly separated sections such as:
  - Parties
  - Background
  - Agreed Terms
- Use numbered clauses and sub-clauses.
- Use lettered limbs where needed: (a), (b), (c).
- Use signature blocks.
- Add schedules where appropriate.
- If a commercial summary helps, include a concise key terms table near the front.

### Agreement language style
- Formal and contractual.
- Tight, clear, and enforceable in tone.
- No memo-style commentary.
- No unnecessary narrative.
- No casual phrasing.
- Use defined terms consistently.
- Prefer direct verbs such as: shall, may, must not, is entitled to.

### Agreement default structure
1. Title
2. Date line
3. Parties
4. Background
5. Agreed Terms
6. Key terms / commercial summary table (if useful)
7. Interpretation / definitions
8. Operative clauses
9. Signature block
10. Schedules

### Agreement drafting rule
If the user says "agreement", default to the most formal version among the three lanes.

---

## Note lane

### Purpose
Use this lane for compact internal documents that need speed, clarity, and decision usefulness.

### Note formatting
- Keep the title simple and functional.
- Do not over-format.
- Use short sections.
- Use bullets freely where they improve speed of reading.
- Use tables where they help comparison or chronology.
- Keep the document visually light.

### Note language style
- Direct and concise.
- Minimal background explanation.
- Lead with the current conclusion, view, or issue.
- Avoid textbook explanation.
- Avoid repetition.
- State only what matters for the immediate internal task.

### Note default structure
1. Title
2. Issue / subject
3. Key facts or record summary
4. Current assessment / view
5. Outstanding points / TBC items

### Note drafting rule
If the user asks for a short internal write-up, summary, or assessment, use the note lane unless the task clearly requires more analysis.

---

## Memo lane

### Purpose
Use this lane for internal documents that require structured analysis, but should still remain concise and commercially readable.

### Memo formatting
- Use a clear title.
- Use short, analytical headings.
- Use short paragraphs.
- Use bullets where they sharpen logic.
- Use tables only when they genuinely improve comparison or structure.
- Keep the layout more formal than a note, but less rigid than an agreement.

### Memo language style
- Analytical, organised, and professional.
- Explain the issue clearly, but do not become verbose.
- Focus on the practical significance.
- Distinguish facts, issue, analysis, and recommendation where relevant.
- Keep the tone restrained and businesslike.

### Memo default structure
1. Title
2. Question / issue
3. Background
4. Analysis
5. Practical implications / recommendation
6. Outstanding points / assumptions

### Memo drafting rule
If the user asks for analysis, position comparison, pros and cons, or a reasoned internal recommendation, use the memo lane.

---

## Table rules for all three lanes
- All tables must remain at **12 pt**.
- Keep tables clean and readable.
- Do not overcrowd cells.
- Prefer concise labels.
- Use tables only where they genuinely improve usability.
- Where a table contains a sequence (e.g., a "No." column in a schedule), use Word-native automatic numbering for those cells too — never hard-code "1.", "2.", "3.".

---

## Automatic numbering (mandatory)

### Rule
Every numbered item in a Brooklet Word document **must** use Word's native paragraph-level automatic numbering. Numbers must be generated by Word's list engine via `numbering.xml` (`<w:abstractNum>` / `<w:num>`) and `<w:numPr>` references on each list paragraph — **never** typed as literal text such as `"1."`, `"2."`, `"(a)"`, `"(A)"` at the start of a paragraph.

The outcome required when the document is opened in Microsoft Word:
- adding a new list item auto-assigns the next number;
- deleting any list item auto-renumbers the rest;
- inserting an item in the middle pushes subsequent numbers down by one;
- sub-levels restart automatically when the parent level changes (e.g., (a)(b)(c) restarts under each new clause).

This applies to every numbered structure across all three lanes — agreement clauses, sub-clauses, lettered limbs, Parties, Background, Schedule "No." columns, note action items, memo numbered lists, etc.

### Required list inventory for an Agreement
Define these abstract numbering definitions in `numbering.xml` and bind each to its own `<w:num>` instance:

| Purpose | Format | Restart behaviour |
|---|---|---|
| Parties | `(1)`, `(2)`, ... (decimal in parentheses) | Restart at 1 each time the Parties block appears |
| Background | `(A)`, `(B)`, `(C)`, ... (upperLetter in parentheses) | Restart at A each time the Background block appears |
| Main clauses (multilevel) | Lvl 0 = `1.` (bold); Lvl 1 = `1.1`; Lvl 2 = `(a)` lowerLetter | Continuous at Lvl 0; Lvl 1 and Lvl 2 auto-restart on parent change |
| Schedule "No." column | `1.`, `2.`, `3.`, ... (decimal with full-stop) | Restart at 1 per schedule |

**For Notes and Memos, ALL numbers in the document must be auto-numbering.** This includes TWO categories:

**Category A -- Section headings (1.1, 1.2, 2.1, etc.):** Use abstractNumId **102** (multilevel). The section title paragraph gets `apply_numbering(p, main_numid(), ilvl=0)` for top-level sections (1., 2., 3.) and `apply_numbering(p, main_numid(), ilvl=1)` for sub-sections (1.1, 1.2, 2.1, etc.). The run text must NOT contain the number -- write "Overview" not "1.1 Overview"; the list engine generates the prefix. The main numId (12) is reused across the entire document so top-level sections stay continuous; sub-sections auto-restart on parent change.

**Category B -- Numbered lists (Outstanding Points, Sources, 其他事项):** Use abstractNumId **103** (single-level "1.", "2.", ...) with a fresh restart-at-1 clone per list block via `_clone_num_with_restart(doc, 103)`. Each item gets `apply_numbering(p, num_id, ilvl=0)`.

**The test for Category A vs B:** Ask "should this number continue from the previous section (1.1 -> 1.2 -> 1.3)?" If yes, it's Category A (multilevel section numbering, abstractNumId 102). Ask "should this list restart at 1?" If yes, it's Category B (single-level list, abstractNumId 103). Never hard-code "1.", "1.1", "2." as literal text in ANY paragraph.

### Implementation notes (python-docx)
When building a `.docx` programmatically, follow this checklist -- full reference code is in `references/auto-numbering.py`:

1. **CRITICAL FIRST STEP:** Call `install_brooklet_numbering(doc)` immediately after creating the Document. This replaces the numbering.xml with Brooklet definitions.
2. For each numbered list block that should restart at 1, call `_clone_num_with_restart(doc, 103)` (or `new_note_list_numid(doc)` if using the convenience wrapper) to get a fresh numId.
3. For each numbered item, add a paragraph and call `apply_numbering(p, num_id, ilvl=0)`. Do **not** prepend `"1. "`, `"2. "` into the run text -- the list engine generates the number.
4. For multi-level Agreement clauses, reuse the main numId (bound to abstractNumId 102) across the document so Lvl 0 stays continuous. Sub-levels auto-restart on parent change.
5. For schedule "No." columns, attach the schedule numId to the paragraph in each row's first cell and leave the run text empty.

**DO NOT use `style='List Number'` as a shortcut.** python-docx's `style='List Number'` only applies a style name -- it does NOT create the required `<w:numPr>` references or numbering.xml definitions. The resulting .docx will show literal text numbers that do not auto-renumber in Word. Always use the `install_brooklet_numbering()` + `apply_numbering()` approach from `references/auto-numbering.py`.

### Verification before delivery
Before sharing any Word output, confirm:
- `word/numbering.xml` contains the four abstract definitions and their `<w:num>` bindings;
- `word/document.xml` references `<w:numId>` for every numbered-list paragraph;
- no paragraph run text begins with a literal number-prefix pattern (`\d+\.`, `\([a-zA-Z0-9]\)`, etc.) for items that should be auto-numbered;
- a quick render test still shows the correct numbers (1., 2., 1.1, (a), (A), etc.).
- **Specifically for Notes/Memos:** open the .docx in Word, add a new item to any numbered list, and verify the subsequent items auto-renumber.

### Failure modes to avoid
- **Using `style='List Number'` instead of `install_brooklet_numbering()` + `apply_numbering()`.** This is the #1 defect -- it produces plain-text numbers that do not auto-renumber. The entire document must be regenerated if this shortcut was taken.
- Hard-coding `"1. "`, `"2.1 "`, `"(a) "`, `"(A) "` as run text -- this defeats auto-renumber.
- Using a single shared numId for both Parties and Background (they will continue each other's count instead of restarting).
- Forgetting `<w:lvlOverride><w:startOverride w:val="1"/></w:lvlOverride>` on restartable lists -- Word will continue counting from the previous block.
- Mixing manual tab-prefixed sub-clauses (`"2.1\t..."`) with auto-numbered ones in the same document -- pick auto-numbering and keep it consistent.

## Style boundaries
- Do not draft an agreement in note language.
- Do not draft a note in essay form.
- Do not let a memo become a contract or a textbook chapter.
- Match depth to document type.

## Formatting references to imitate
When Brooklet agreement templates are provided, mirror their style characteristics where relevant:
- centered all-caps agreement title;
- formal opening line;
- separate Parties / Background / Agreed Terms sections;
- concise front-end key terms table where useful;
- numbered clauses;
- signature blocks;
- schedules.

For non-agreement documents, retain the same clean and understated Brooklet feel, but simplify the structure appropriately.

## Default reusable prompt
"Draft this in Brooklet Word style. Use Candara throughout, with 12 pt body text and 12 pt tables. First choose the correct format lane: agreement, note, or memo. For agreements, use formal clause-based drafting aligned with Brooklet agreement templates. For notes, keep it compact, direct, and decision-useful. For memos, use a structured analytical format that stays concise and commercially readable. Avoid filler, avoid over-formatting, and use TBC or bracketed placeholders for any missing or unverified information. All numbered items (Parties, Background, clauses, sub-clauses, lettered limbs, schedule No. columns, action items) must use Word-native automatic numbering — never hard-code numbers as literal text. Adding or deleting any list item in Word must auto-renumber the rest. See references/auto-numbering.py for the exact implementation pattern."

## Short prompt version
"Use Brooklet Word style: Candara, 12 pt body and 12 pt tables. Route the document into agreement / note / memo format. Agreement = formal clause drafting; note = compact internal summary; memo = concise analytical write-up. Keep it clean, understated, and non-redundant. Use TBC / [•] where needed. All numbered lists must be Word-native auto-numbering (no literal '1.', '2.', '(a)' in text) so adding/deleting items auto-renumbers in Word."
