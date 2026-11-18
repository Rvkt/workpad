# Phase 2: Groups, Lookaround and Advanced Constructs

Part of [[Regex Roadmap - Index|Regular Expressions Mastery Roadmap]]. Previous: [[Phase 1 - Core Syntax and Fundamentals]]. Next: [[Phase 3 - Engines, Performance and Cross-Tool Application]].

**Duration:** Weeks 3–4
**Objective:** Capture, reference, and conditionally assert on structure within a match.

## Week 3: Groups and Backreferences

### Groups

- [ ] Capturing groups `( )` and how they're numbered.
- [ ] Non-capturing groups `(?: )` and when to prefer them.
- [ ] Named capturing groups `(?<name> )` / `(?P<name> )` depending on flavor.
- [ ] Nested groups and numbering order (outermost-left to innermost).

### Backreferences

- [ ] Backreferences within a pattern (`\1`, `\k<name>`) to match repeated content.
- [ ] Backreferences in replacement strings (`$1`, `\1`, depending on tool).
- [ ] Understand that backreferences match the *same text*, not the same pattern, as the referenced group.

### Practical Tasks

- [ ] Write a pattern detecting a doubled word (e.g. "the the") using a backreference.
- [ ] Extract a date into named groups (year, month, day) and use the names in code to build a different format.
- [ ] Use non-capturing groups to apply a quantifier to an alternation without polluting the capture list.
- [ ] Use a backreference in a find-and-replace to swap two captured fields (e.g. "Last, First" → "First Last").

**Deliverable:** Comfortable extracting structured data via named/numbered groups and matching repeated content via backreferences.

## Week 4: Lookaround and Conditional Constructs

### Lookaround

- [ ] Positive lookahead `(?=...)` and negative lookahead `(?!...)`.
- [ ] Positive lookbehind `(?<=...)` and negative lookbehind `(?<!...)`.
- [ ] Understand that lookaround asserts without consuming characters.
- [ ] Understand variable-length lookbehind support differences across flavors (not universally supported).
- [ ] Combine multiple lookaheads to express an "AND" condition (e.g. password must contain a digit AND an uppercase letter).

### Other Advanced Constructs

- [ ] Inline flags (`(?i)`, `(?m)`, `(?s)`) and scoped inline flags `(?i:...)`.
- [ ] Atomic groups `(?>...)` and how they relate to possessive quantifiers.
- [ ] Conditional patterns `(?(1)yes|no)` in flavors that support them, at a conceptual level.
- [ ] Unicode property escapes (`\p{L}`, `\p{N}`) for script- and category-aware matching.

### Practical Tasks

- [ ] Write a password-strength pattern requiring a digit, an uppercase letter, and a minimum length, using only lookaheads plus a final match.
- [ ] Extract a number immediately following the word "Total:" using lookbehind, without capturing "Total:" itself.
- [ ] Write a pattern matching a value only when it's NOT preceded by a specific word, using negative lookbehind.
- [ ] Match any Unicode letter (not just ASCII) using a Unicode property escape, and test it against non-Latin script input.

**Deliverable:** The ability to express compound, context-sensitive matching conditions without manual post-processing.
