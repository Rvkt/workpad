# Phase 3: Engines, Performance and Cross-Tool Application

Part of [[Regex Roadmap - Index|Regular Expressions Mastery Roadmap]]. Previous: [[Phase 2 - Groups, Lookaround and Advanced Constructs]].

**Duration:** Weeks 5–6
**Objective:** Understand how the matching engine actually works, avoid performance traps, and apply regex correctly across real tools and languages.

## Week 5: How Backtracking Engines Work

### The Matching Process

- [ ] Understand NFA-based backtracking engines (most mainstream flavors: PCRE, Python `re`, JavaScript, Java) vs. DFA-based engines (RE2, POSIX `grep` in some modes).
- [ ] Trace through a simple pattern's matching steps by hand, including backtrack points.
- [ ] Understand why alternation and nested quantifiers create many possible backtracking paths.
- [ ] Understand why DFA engines can't support backreferences or lookaround, and what they trade off for guaranteed linear-time matching.

### Catastrophic Backtracking

- [ ] Recognize the classic vulnerable pattern shape: nested quantifiers over overlapping character sets, e.g. `(a+)+$`.
- [ ] Understand why such a pattern can take exponential time on a crafted non-matching input (ReDoS).
- [ ] Fix vulnerable patterns using atomic groups, possessive quantifiers, or rewriting to remove ambiguity.
- [ ] Understand why user-supplied regex (or regex applied to user-supplied, adversarial input) is a security concern.

### Practical Tasks

- [ ] Construct a deliberately catastrophic pattern and time it against a crafted input that triggers exponential backtracking.
- [ ] Rewrite that pattern using an atomic group or possessive quantifier and confirm the fix eliminates the blowup.
- [ ] Trace a moderately complex real pattern step by step using a visual regex debugger (e.g. regex101's debugger) and narrate what each backtrack does.

**Deliverable:** The ability to spot a ReDoS-vulnerable pattern on sight and fix it, backed by a measured before/after.

## Week 6: Flavor Differences and Practical Application

### Flavor Differences

- [ ] Compare PCRE, Python `re`, JavaScript `RegExp`, and POSIX ERE on: lookbehind support, named groups syntax, Unicode handling, multiline defaults.
- [ ] Understand `re` vs. `regex` module differences in Python (variable-length lookbehind, atomic groups, possessive quantifiers).
- [ ] Understand JavaScript's `u` and `v` flags and their effect on Unicode matching.
- [ ] Know when a tool's regex dialect doesn't support a construct you're used to, and the workaround.

### Practical Application

- [ ] Validation: when regex is appropriate (format checks) vs. inappropriate (e.g. fully validating an email address or parsing HTML).
- [ ] Extraction: pulling structured fields out of semi-structured text (logs, CSV-like data) with named groups.
- [ ] Transformation: find-and-replace with backreferences/named group references across a codebase or dataset.
- [ ] Command-line regex: `grep -E`, `sed`, `awk` pattern differences from PCRE.
- [ ] Knowing when to reach for a real parser (JSON/HTML/CSV library) instead of regex.

### Practical Tasks

- [ ] Write the same extraction pattern in Python and JavaScript, and document any syntax adjustments needed.
- [ ] Parse a log file's timestamp, log level, and message into named groups, then transform it into a different format.
- [ ] Use `grep -E` and `sed` to accomplish a text transformation task from the shell, then compare the equivalent in Python.
- [ ] Identify a parsing task in a past or current project that used regex for structured data (HTML/JSON) and explain why a parser would have been more correct.

**Deliverable:** A cross-language reference of flavor differences built from direct experience, and the judgment to know when regex is — and isn't — the right tool.
