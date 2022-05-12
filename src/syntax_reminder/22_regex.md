<!-- markdownlint-disable MD001 -->

# Regex

- [Character literals](#character-literals)
- [Character classes](#character-classes)
- [Character groups](#character-groups)
- [Meta characters](#meta-characters)
- [Flags](#flags)
- [Repetitions](#repetitions)
- [Quantifiers](#quantifiers)
- [Modifiers](#modifiers)

### Character literals

``` javascript
abc // Matches abc
123 // Matches 123
```

### Character classes

Match any single character in the string from characters present inside the brackets; any character except `^`, `-`, `]` or `\` is a literal in character classes

``` javascript
[abc] // Only a, b or c
[^abc] // Not a, b nor c
[a-z] // Characters a to z
[0-9] // Numbers 0 to 9
```

### Character groups

Match the entire group inside the parentheses

``` javascript
(abc) // Matches abc
(abc){2} // Matches abcabc
(abc|def) // Matches abc or def
(a(bc)) // Capture sub-group
(.*) // Capture all

(x) // Matches x and remembers the match
(?:x) // Matches x and does not remember the match
x(?=y) // Matches x only if x is followed by y
```

### Meta characters

``` javascript
\d // Match any digit character (same as [0-9])
\D // Match any non digit character (same as [^0–9])
\w  // Match any word character, i.e alphanumeric character (same as [a-zA-Z0–9_])
\W // Match any non word character (same as [^a-zA-Z0–9_])
\s // Match a whitespace character (spaces, tabs, etc.)
\S  // Match a non whitespace character
\t // Match a tab character only
\b  // Find a match at beginning or ending of a word (word boundary)

^ // Matches the beginning of the string
$ // Matches the end of the string
^...$ // Starts and ends

.  // Matches any character except for newline
\. // Match periods

| // alternation
```

### Flags

``` javascript
/.../g // global
/.../i // case insensitive
/.../m // multiline
/.../s // single line
/.../u // unicode
/.../y // sticky (perform search at given position)
```

### Repetitions

``` javascript
{N} // Matches exactly N occurrences of the preceding regular expression
{N,} // Matches at least N occurrences of the preceding regular expression
{N,M} // Matches at least N occurrences and at most M occurrences of the preceding regular expression (where M > N)
```

### Quantifiers

``` javascript
+ // Matches the preceding expression 1 or more times
* // Matches the preceding expression 0 or more times
? // Matches the preceding expression 0 or 1 time
```

### Modifiers

Not supported by any regex flavor

``` javascript
(?i) // case insensitive
(?c) // case sensitive
```
