---
tags: [roadmap, roadmap/regex]
---

# Regular Expressions Mastery Roadmap

**Level:** Intermediate → Senior/Lead
**Duration:** 6 Weeks
**Weekly Commitment:** 2–3 Hours
**Learning Approach:** Deliberate practice building and debugging real patterns, understanding the matching engine rather than memorizing syntax.

---

## Learning Objectives

By completing this roadmap, the goal is to develop competency in:

- [ ] Core regex syntax: literals, character classes, quantifiers, anchors.
- [ ] Groups, backreferences, and alternation.
- [ ] Lookahead and lookbehind assertions.
- [ ] The difference between greedy, lazy, and possessive quantifiers.
- [ ] How backtracking engines actually match (and why they sometimes don't terminate quickly).
- [ ] Catastrophic backtracking: recognizing, avoiding, and fixing it.
- [ ] Flavor differences across PCRE, Python `re`, JavaScript, and POSIX.
- [ ] Practical application: validation, extraction, and text transformation.
- [ ] Knowing when *not* to reach for regex.

---

## Roadmap Notes

- [[Phase 1 - Core Syntax and Fundamentals]] (Weeks 1–2)
- [[Phase 2 - Groups, Lookaround and Advanced Constructs]] (Weeks 3–4)
- [[Phase 3 - Engines, Performance and Cross-Tool Application]] (Weeks 5–6)
- [[Regex Cheat Sheet Reference]]
- [[Learning Resources (Regex)]]

---

## Weekly Progress Tracking

- [ ] [[Phase 1 - Core Syntax and Fundamentals|Phase 1: Core Syntax and Fundamentals]]
- [ ] [[Phase 2 - Groups, Lookaround and Advanced Constructs|Phase 2: Groups, Lookaround and Advanced Constructs]]
- [ ] [[Phase 3 - Engines, Performance and Cross-Tool Application|Phase 3: Engines, Performance and Cross-Tool Application]]

### Completion Criteria

The roadmap should not be considered complete merely because all topics have been studied.

You should be able to:

- [ ] Write a pattern from a plain-English description without trial-and-error guessing.
- [ ] Read an unfamiliar, moderately complex pattern and explain what it matches, piece by piece.
- [ ] Choose between a capturing group, non-capturing group, and lookaround deliberately, not by habit.
- [ ] Identify a pattern vulnerable to catastrophic backtracking before it ships, and rewrite it safely.
- [ ] Explain why the same pattern can behave differently in Python, JavaScript, and grep.
- [ ] Decide when a simple string method or a parser is the better tool instead of regex.
- [ ] Debug a regex that "almost works" by isolating which part of the pattern is wrong.

---

## Execution Rules

1. Follow the phases in order; performance and backtracking (Phase 3) only make sense once the matching model from Phase 1–2 is solid.
2. Use an interactive regex tester (e.g. regex101) to see the engine's matching steps, not just the final result.
3. Write a plain-English description of what a pattern should match *before* writing the pattern itself.
4. Test every pattern against both matching and non-matching examples, including edge cases and empty input.
5. When a pattern gets hard to read, prefer named groups and verbose/extended mode over cleverness.
6. Treat every non-trivial pattern as code: commented where the intent isn't obvious, and covered by test cases.

**Final Goal:** Write, read, and debug regular expressions confidently across languages and tools, understand why the engine matches the way it does, and recognize when regex is the wrong tool for the job.
