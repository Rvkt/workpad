---
tags: [roadmap, roadmap/regex]
---

# Phase 1: Core Syntax and Fundamentals

Part of [[Regex Roadmap - Index|Regular Expressions Mastery Roadmap]]. Next: [[Phase 2 - Groups, Lookaround and Advanced Constructs]].

**Duration:** Weeks 1–2
**Objective:** Build fluency with the literal building blocks of a pattern.

## Week 1: Literals, Character Classes and Anchors

### Literals and Metacharacters

- [ ] Understand literal characters vs. metacharacters (`. ^ $ * + ? { } [ ] \ | ( )`).
- [ ] Escaping metacharacters with `\`.
- [ ] The dot (`.`) and what it does/doesn't match (newlines, with and without a dotall/single-line flag).

### Character Classes

- [ ] `[abc]`, `[^abc]` (negation), `[a-z]` (ranges).
- [ ] Shorthand classes: `\d`, `\w`, `\s` and their negations `\D`, `\W`, `\S`.
- [ ] Understand what counts as a "word character" varies by flavor (Unicode vs. ASCII mode).
- [ ] POSIX character classes (`[:alpha:]`, `[:digit:]`) in flavors that support them.

### Anchors and Boundaries

- [ ] `^` and `$` for start/end of string or line (and how multiline mode changes this).
- [ ] `\b` and `\B` for word boundaries.
- [ ] `\A` and `\z`/`\Z` for absolute string start/end in flavors that support them.

### Practical Tasks

- [ ] Match a US zip code (5 digits, optionally with a 4-digit extension) using character classes.
- [ ] Match a word that appears as a whole word only, not as a substring of another word, using `\b`.
- [ ] Write a pattern distinguishing `^`/`$` as line anchors vs. string anchors, and verify the difference with multiline test input.

**Deliverable:** Fluent reading and writing of character-level patterns, anchors, and boundaries.

## Week 2: Quantifiers and Alternation

### Quantifiers

- [ ] `*`, `+`, `?`, `{n}`, `{n,}`, `{n,m}`.
- [ ] Greedy quantifiers and how they consume as much as possible before backtracking.
- [ ] Lazy quantifiers (`*?`, `+?`, `??`, `{n,m}?`) and how they consume as little as possible.
- [ ] Possessive quantifiers (`*+`, `++`) in flavors that support them, and why they prevent backtracking entirely.

### Alternation and Grouping (Introductory)

- [ ] `|` for alternation, and its precedence relative to concatenation.
- [ ] Parentheses for grouping alternation scope: `cat|dog` vs. `(cat|dog)s`.
- [ ] Understand that unparenthesized alternation spans the whole pattern unless grouped.

### Practical Tasks

- [ ] Write a pattern matching an HTML-like tag's content lazily vs. greedily, and show how the results differ on `<a>text</a><b>more</b>`.
- [ ] Write a pattern matching "cat", "dog", or "fish" as a whole word using alternation, with correct grouping.
- [ ] Match a quoted string without using lookaround, and identify where greedy matching gives a wrong result on multiple quoted strings in one line.

**Deliverable:** The ability to choose the correct quantifier for a given matching intent, and to predict greedy vs. lazy behavior before testing it.
