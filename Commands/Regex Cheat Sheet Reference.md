# Regex Cheat Sheet Reference

Part of [[Regex Roadmap - Index|Regular Expressions Mastery Roadmap]]. A quick-lookup table; the phase notes cover the *why* behind each construct.

| Category | Syntax | Meaning |
|---|---|---|
| Anchors | `^` `$` | Start / end of string or line |
| Anchors | `\b` `\B` | Word boundary / non-boundary |
| Classes | `[abc]` `[^abc]` `[a-z]` | Set, negated set, range |
| Classes | `\d` `\w` `\s` (+ `\D` `\W` `\S`) | Digit, word char, whitespace (+ negations) |
| Classes | `\p{L}` `\p{N}` | Unicode letter / number category |
| Quantifiers | `*` `+` `?` `{n,m}` | Zero-or-more, one-or-more, optional, range |
| Quantifiers | `*?` `+?` `??` `{n,m}?` | Lazy (minimal match) variants |
| Quantifiers | `*+` `++` | Possessive (no backtracking) variants |
| Alternation | `a\|b` | Match `a` or `b` |
| Groups | `(...)` | Capturing group |
| Groups | `(?:...)` | Non-capturing group |
| Groups | `(?<name>...)` | Named capturing group |
| Groups | `(?>...)` | Atomic group (no backtracking into it) |
| Backreferences | `\1`, `\k<name>` | Match the same text as a prior group |
| Lookahead | `(?=...)` `(?!...)` | Positive / negative lookahead |
| Lookbehind | `(?<=...)` `(?<!...)` | Positive / negative lookbehind |
| Flags | `i` `m` `s` `x`/`g` (`u`/`v` in JS) | Case-insensitive, multiline, dotall, extended/global/Unicode |
| Inline flags | `(?i)` `(?i:...)` | Set a flag globally or scoped to a group |

## Common Pitfalls

- `.` doesn't match newlines unless a dotall/single-line flag is set.
- Greedy quantifiers backtrack; on adversarial input, nested greedy quantifiers can be catastrophic — see [[Phase 3 - Engines, Performance and Cross-Tool Application]].
- `^`/`$` mean string start/end by default, but line start/end under multiline mode — don't assume which without checking the flag.
- Character class shorthand (`\w`, `\d`) is Unicode-aware by default in some flavors (Python 3 `re`) and ASCII-only in others unless a flag is set.
- Lookbehind must be fixed-length in many flavors (classic PCRE/JS); variable-length lookbehind support varies.
- Validating something fully structured (HTML, JSON, deeply nested expressions) with regex alone is usually the wrong tool — use a parser.
