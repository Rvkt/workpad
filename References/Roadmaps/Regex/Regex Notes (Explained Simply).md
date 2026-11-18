# Regex Notes (Explained Simply)

Part of [[Regex Roadmap - Index|Regex Mastery Roadmap]].

These notes explain the roadmap's ideas in plain English, with small examples. The goal is understanding, not memorizing.

Before we start, one big idea: a regular expression (people call it "regex" for short) is just a search pattern made of text. You give it a pattern, and it checks a piece of text to see if that pattern shows up in it. Think of it like a very fussy "find" tool: instead of finding the exact word "cat", it can find "any three-letter word" or "any number that looks like a phone number".

---

## Phase 1: Core Syntax and Fundamentals

This phase is about learning the basic alphabet of regex — the small symbols you combine to describe what you're looking for.

### Literal characters vs. special symbols

Most characters in a pattern just mean themselves. If you write `cat`, it looks for the exact letters c-a-t next to each other. But a handful of characters are special "commands" instead of literal text — things like `. ^ $ * + ? { } [ ] \ | ( )`. These are called metacharacters, which is just a fancy word for "characters that mean something other than themselves."

If you actually want to search for one of these symbols as a literal character (say, a real question mark), you put a backslash in front of it, like `\?`. This is called "escaping" — you're telling the pattern, "no, I mean the actual character here, not the special command."

The dot `.` is a special symbol that means "any single character" (except, usually, a line break). So `c.t` matches "cat", "cot", "c9t", or "c t" — anything with a c, then one character, then a t.

### Character classes — "pick one of these"

A character class is a way of saying "match one character, but only if it's one of these options." You write it in square brackets.

- `[abc]` means "match a, b, or c" (just one of them, not all three).
- `[^abc]` means "match anything EXCEPT a, b, or c." The `^` inside brackets flips it to "not these."
- `[a-z]` means "match any lowercase letter from a to z" — the dash makes a range.

There are also shortcuts because some classes are used so often:
- `\d` means "any digit" (0-9). Think of it as shorthand for `[0-9]`.
- `\w` means "any word character" — letters, digits, and underscore.
- `\s` means "any whitespace" — spaces, tabs, line breaks.
- Capitalizing the letter flips it to "not": `\D` means "not a digit", `\W` means "not a word character", `\S` means "not whitespace."

One subtlety: what counts as a "word character" can change depending on the tool and whether it's working in Unicode mode (which understands letters from many languages) or plain ASCII mode (which only understands the basic English alphabet and digits). So `\w` might match an accented letter like "é" in one tool but not another.

Some older tools (mostly on Linux, like certain `grep` modes) also support POSIX classes like `[:alpha:]` (letters) or `[:digit:]` (digits), written inside double brackets like `[[:digit:]]`. They do the same job as `\d` and friends, just with different spelling.

### Anchors and boundaries — "where" something must be, not "what"

Anchors don't match any actual character — they match a *position*. Think of them as markers, not ingredients.

- `^` means "the start of the string" (or the start of a line, if multiline mode is turned on).
- `$` means "the end of the string" (or the end of a line, in multiline mode).
- `\b` means "a word boundary" — the edge between a word character and a non-word character. This is how you match a whole word, not just part of one. For example, `\bcat\b` matches "cat" in "the cat sat" but not the "cat" inside "category", because there's no boundary between "cat" and "egory."
- `\B` is the opposite — "not a word boundary."
- `\A` and `\z`/`\Z` mean "the very start of the whole string" and "the very end of the whole string", no matter what mode you're in. These are more absolute than `^` and `$`, which can get confused by multiline mode.

**Example:** `^\d{5}(-\d{4})?$` matches a US zip code. In plain words: "start of the string, then exactly 5 digits, then optionally a dash followed by 4 more digits, then end of the string." It matches "90210" and "90210-1234", but not "9021" (too short) or "902100" (too long).

### Quantifiers — "how many times"

A quantifier says how many times the thing right before it should repeat.

- `*` means "zero or more times" — it's fine if it doesn't appear at all.
- `+` means "one or more times" — it has to show up at least once.
- `?` means "zero or one time" — it's optional, but can only appear once.
- `{n}` means "exactly n times."
- `{n,}` means "n or more times."
- `{n,m}` means "between n and m times."

**Greedy vs. lazy** is one of the most important ideas in this phase. By default, quantifiers are "greedy" — they try to grab as much text as possible first, and only give characters back (backtrack) if they have to, to let the rest of the pattern match. "Lazy" quantifiers (written with a `?` right after them, like `*?` or `+?`) do the opposite: they grab as little as possible first, and only take more if they're forced to.

**Example:** Imagine the text `<a>text</a><b>more</b>` and the pattern `<.+>` (greedy). Because `.+` is greedy, it tries to eat as much as possible, so it ends up matching all the way from the first `<` to the very last `>` — way more than you probably wanted. Now use the lazy version, `<.+?>`: it grabs as little as possible, so it stops at the very first `>` it finds, matching just `<a>`. Lazy matching is usually what you want when there are multiple similar chunks on one line and you want them matched separately rather than swallowed together.

There's also "possessive" quantifiers (`*+`, `++`), supported in some tools like PCRE. These are like greedy quantifiers but they refuse to backtrack at all — once they've grabbed text, they never give it back, even if that means the overall match fails. This sounds restrictive, but it's actually a performance tool (more on why in Phase 3).

### Alternation — "this or that"

The pipe symbol `|` means "or." `cat|dog` means "match either 'cat' or 'dog'." Be careful with how far the "or" reaches — without parentheses, alternation stretches across the whole pattern. So `cat|dogs` means "cat" OR "dogs" — not "cat" or "dog" followed by "s". If you want the "s" to apply to both, you need to group them: `(cat|dog)s` means "cat" or "dog", followed by "s" either way — so it matches "cats" or "dogs."

---

## Phase 2: Groups, Lookaround and Advanced Constructs

Phase 1 was about matching characters. Phase 2 is about organizing a pattern into pieces, pulling specific pieces out, and checking conditions around a match without actually consuming those characters.

### Groups — putting parentheses around part of a pattern

Parentheses `( )` do two things at once: they group a piece of the pattern together (so a quantifier or alternation can apply to the whole group), and they "capture" whatever text matched inside them so you can grab it afterward.

Groups are numbered left to right, based on where their opening parenthesis appears. So in `(\d{4})-(\d{2})-(\d{2})` (a date like 2024-05-10), group 1 is the year, group 2 is the month, group 3 is the day.

Sometimes you want the grouping behavior (to apply a quantifier, say) but you don't care about capturing the text. For that, use a non-capturing group: `(?:cat|dog)s`. It behaves just like a normal group for matching purposes, but it won't show up in your list of captured results — useful when you have lots of groups and don't want to clutter the output with ones you don't need.

Named groups let you label a group instead of just numbering it: `(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})`. Later, in code, you can ask for `year` instead of trying to remember that it was "group 1." Much easier to read.

### Backreferences — "match the same text again"

A backreference lets you say "whatever text matched in an earlier group, match that exact same text again here." It's written `\1` (for group 1), `\2` (for group 2), or `\k<name>` for a named group.

This is different from just repeating the pattern — a backreference matches the literal text that was captured, not the same rule. For example, `\b(\w+) \1\b` matches a doubled word like "the the", because after group 1 captures "the", `\1` demands the exact same word again. It would not match "the them", because "them" isn't the same text as "the."

Backreferences are also used in find-and-replace. If you want to swap "Last, First" into "First Last", you'd capture the last name as group 1 and the first name as group 2, then write the replacement as `$2 $1` (or `\2 \1` depending on the tool) — "put group 2 first, then group 1."

### Lookaround — checking nearby text without "eating" it

This is one of the trickier ideas, so here's the plain-English version: normally, when part of a pattern matches some text, that text gets "used up" (consumed) and the next part of the pattern continues after it. Lookaround is different — it checks that some text is nearby, but doesn't consume it. It's like peeking over your shoulder to check something is there, without actually stepping there.

- Positive lookahead `(?=...)` means "what follows must look like this" — but don't include it in the match.
- Negative lookahead `(?!...)` means "what follows must NOT look like this."
- Positive lookbehind `(?<=...)` means "what comes before must look like this."
- Negative lookbehind `(?<!...)` means "what comes before must NOT look like this."

**Example:** To grab the number right after the word "Total:" without including "Total:" in the result, you'd write `(?<=Total:\s*)\d+`. In plain words: "look behind and make sure 'Total:' (plus maybe some spaces) comes right before, but only actually match the digits."

**Example:** A password rule needing a digit AND an uppercase letter AND a minimum length can be written using lookaheads stacked at the very start, like `(?=.*\d)(?=.*[A-Z]).{8,}`. Each lookahead is a separate condition checked from the same starting position — "somewhere ahead there's a digit," "somewhere ahead there's an uppercase letter" — and then the final `.{8,}` actually consumes at least 8 characters. It's like a checklist of requirements that all have to be true before you accept the string.

One catch: not every tool supports lookbehind with varying lengths (where the amount of text to look back over isn't fixed). Some tools only allow lookbehind of a fixed size.

### Other advanced bits

- **Inline flags** like `(?i)` turn on behavior (here, case-insensitive matching) from that point in the pattern onward, instead of setting it outside the pattern. `(?i:cat)` scopes that flag to just the group instead of the whole pattern.
- **Atomic groups** `(?>...)` are like regular groups, but once they match something, they lock it in and refuse to backtrack into it — similar in spirit to possessive quantifiers. This matters for performance, covered in Phase 3.
- **Conditional patterns** `(?(1)yes|no)` mean "if group 1 matched, require 'yes' here; otherwise require 'no'." It's an if/else built right into the pattern — a niche feature, but handy for tightly coupled structures.
- **Unicode property escapes** like `\p{L}` match "any letter in any language" (L stands for "Letter" category), and `\p{N}` matches "any number character," including digits from non-Latin scripts. These are broader than `\w` or `\d`, which often default to just the ASCII alphabet unless Unicode mode is explicitly turned on.

---

## Phase 3: Engines, Performance and Cross-Tool Application

Phases 1 and 2 taught you the vocabulary. Phase 3 is about understanding what's happening "under the hood" when a regex runs, so you can avoid writing something that is slow, dangerous, or wrong for the tool you're using.

### How the matching engine actually works

Most regex tools you'll use day to day — PCRE (used by PHP and many others), Python's `re`, JavaScript's regex, Java's regex — use something called a "backtracking engine." Here's the plain idea: the engine tries one path through the pattern, and if that path leads to a dead end, it backs up (backtracks) and tries a different path, repeating until it either finds a match or runs out of options.

Think of it like walking through a maze and trying a branch; if that branch is a dead end, you walk back to the last fork and try a different direction. That's backtracking.

There's another kind of engine, used by tools like RE2 and some `grep` modes, called a DFA-based engine (DFA stands for "deterministic finite automaton," but you don't need to remember that term — the point is simply that it works differently). These engines track all possible paths at once instead of trying them one at a time, which guarantees they finish in a predictable amount of time. The tradeoff is that they can't support backreferences or lookaround, because those features require "remembering" things from earlier in the match in a way that doesn't fit this all-at-once approach.

### Catastrophic backtracking — when the maze has too many dead ends

This is the scary part of backtracking engines. If a pattern has nested repetition over characters that overlap in what they can match — the classic toy example is `(a+)+$` — then for certain non-matching input, the engine can end up trying an enormous, exploding number of possible paths before giving up. Each extra character in the input can roughly double the work, which means for a long enough string, this can effectively never finish. This is called "catastrophic backtracking," and when it's triggered deliberately by an attacker feeding in bad input, it's called ReDoS (Regular Expression Denial of Service) — a way to make a program hang or crash just by giving it a sneaky string.

The fix is usually one of:
- Rewrite the pattern so there's no ambiguity about how repeated parts can divide up the text (e.g., don't nest two "repeat this" rules over the same kind of character).
- Use an atomic group or a possessive quantifier, which tells the engine "once you've matched this, don't backtrack into it" — cutting off the exploding search before it starts.

Because this is a real security issue (anywhere user input gets run through a regex you wrote), it's worth testing any pattern you write against deliberately nasty input, not just the normal cases.

### Flavor differences — regex isn't one single language

Different tools implement "regex" with small but important differences — these are called "flavors." For example:
- Not every flavor supports lookbehind, and some that do only support fixed-length lookbehind.
- Named group syntax differs: `(?<name>...)` in some tools, `(?P<name>...)` in Python's `re`.
- Python has two regex modules: the built-in `re`, and a more powerful third-party `regex` module that adds things like variable-length lookbehind and possessive quantifiers that `re` doesn't support.
- JavaScript has a `u` flag (and a newer `v` flag) that switch the engine into full Unicode-aware mode, changing how certain characters and classes behave.

The practical lesson: a pattern that works perfectly in one language might throw an error, or silently behave differently, in another. Always check the documentation for the specific tool you're using rather than assuming "regex is regex everywhere."

### When regex is the right tool (and when it isn't)

Regex is great for simple-to-moderate pattern checks: "does this look like a zip code," "does this line start with a timestamp," "pull out everything between quotes." It struggles badly with anything that has nested, recursive structure — like fully validating an email address according to every rule in the spec, or parsing HTML or JSON. Those formats can nest arbitrarily deep (tags inside tags, objects inside objects), and regex has no good way to "count" how deep it currently is. For those jobs, use a real parser library built for that format — it will be more correct and far less fragile than a hand-written pattern.

A good rule of thumb: use regex for flat, line-shaped, predictable text (log lines, simple format checks, find-and-replace). Reach for a parser when the data has real structure that can nest or vary in depth.

### Practical skills this phase builds

- Reading a log line like `2024-05-10 ERROR Something failed` and turning it into named groups for date, level, and message, so you can reformat or filter it in code.
- Using command-line tools like `grep -E` (extended regex) and `sed` for quick text transformations directly in the terminal, and noticing that their regex dialect is close to but not identical to what you'd use in Python or JavaScript.
- Building the habit of asking, before reaching for regex, "is this text actually flat and predictable, or does it have nested structure that a parser would handle more safely?"
