---
layout: page
title: Scanning Text
nav_order: 1
parent: / Atomize
---

# `TextScanner`

---

`TextScanner` creates an object that wraps raw text enabling character-by-character scanning with arbitrary advancement and backtracking. Text can optionally be "*squeezed*" of any unquoted whitespace, i.e. between pairs of unescaped `'` or `"`.

# Constructors

---

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">TextScanner</b>(string, [bool]) &#10140; TextScanner
</code>

> Constructs a new `TextScanner` over given text, optionally ignoring unquoted whitespace, 
> i.e. between pairs of unescaped `'` or `"`. By default all whitespace is considered a token.

# Instance Properties

---

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Index</b> &#10140; int
</code>

> Current location of the scanner in the *raw* text.

```
Index :: int
```

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Offset</b> &#10140; int
</code>

> Total number of characters that have been scanned, not counting whitespace if it is being ignored.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Text</b> &#10140; string
</code>

Raw text being scanned.

# Instance Methods

---

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Advance</b>([int]) &#10140; ()
</code>

> Moves the scanner forward a given number of characters, stopping if it reaches the end. Default is one character.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Backtrack</b>([int]) &#10140; ()
</code>

> Moves the scanner backwards a given number of characters, stopping if it reaches the beginning. Default is one character.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Read</b>([int]) &#10140; ReadOnlyMemory&lt;char&gt;
</code>

> Moves the scanner forward and returns a given number of characters, stopping if it reaches the end. Default is one character.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">ReadToEnd</b>() &#10140; ReadOnlyMemory&lt;char&gt;
</code>

> Moves the scanner forward and returns all unscanned characters.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Reset</b>() &#10140; ()
</code>

> Moves the scanner to the beginning.