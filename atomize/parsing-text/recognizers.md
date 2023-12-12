---
layout: page
title: Recognizers
parent: Parsing Text
grand_parent: / Atomize
nav_order: 2
---

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Atom</b>(char) &#10140; Parser&lt;char&gt;
</code>

> Succeeds if the scanner would match a given `char` at its current offset.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Atom</b>(string) &#10140; Parser&lt;ReadOnlyMemory&lt;char&gt;&gt;
</code>

> Succeeds if the scanner would match the given `string` at its current offset.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Atom</b>(Regex) &#10140; Parser&lt;ReadOnlyMemory&lt;char&gt;&gt;
</code>

> Succeeds if the scanner would match the given `Regex` at its current offset.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Ignore</b>(char) &#10140; Parser&lt;char&gt;
</code>

> Succeeds if the scanner would match the given `char`at its current offset, ignoring the match.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Ignore</b>(string) &#10140; Parser&lt;ReadOnlyMemory&lt;char&gt;&gt;
</code>

> Succeeds if the scanner would match the given `string` at its current offset, ignoring the match.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Ignore</b>(Regex) &#10140; Parser&lt;ReadOnlyMemory&lt;char&gt;&gt;
</code>

> Succeeds if the scanner would match the given `Regex` at its current offset, ignoring the match.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Ignore&lt;T&gt;</b>(Parser&lt;T&gt;) &#10140; Parser&lt;T&gt;
</code>

> Succeeds if the scanner would match the given `Parser<T>` at its current offset, ignoring whether or not any 
characters were consumed by the parser.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Peek&lt;T&gt;</b>(Parser&lt;T&gt;) &#10140; Parser&lt;T&gt;
</code>

> Succeeds if the scanner would match the given `Parser<T>` at its current offset. However, no characters are
consumed by the match.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Until</b>(char) &#10140; Parser&lt;ReadOnlyMemory&lt;char&gt;&gt;
</code>

> Always succeeds, consuming characters until the given `char` has been matched, or the scanner has been exhausted.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Until</b>(string) &#10140; Parser&lt;ReadOnlyMemory&lt;char&gt;&gt;
</code>

> Always succeeds, consuming characters until the given `string` has been matched, or the scanner has been exhausted.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Until</b>(Regex) &#10140; Parser&lt;ReadOnlyMemory&lt;char&gt;&gt;
</code>

> Always succeeds, consuming characters until the given `Regex` has been matched, or the scanner has been exhausted.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Until&lt;T&gt;</b>(Parser&lt;T&gt;) &#10140; Parser&lt;ReadOnlyMemory&lt;char&gt;&gt;
</code>

> Always succeeds, consuming characters until the given `Parser` succeeds, or the scanner has been exhausted.

<br>

# Common Regular Expression Parsers

---

| Pattern             | `Parse.Single`        | `Parse.Multiple` 
|:------------------- |:--------------------- |:----------
| Alphanumeric        | `[a-zA-Z0-9]`         |  `[a-zA-Z0-9]+`
| Any                 | `.`                   |  `.+`
| Control             | `[\x00-\x1F\x7F]+`    |  `[\x00-\x1F\x7F]+`
| Digit               | `[0-9]`               | `[0-9]+`
| DoubleQuotedString  |                       | `"(.*(?<!\\))"`
| EscapeSequence      | `\\[\\'0abfnrtv""]`   | `(\\[\\'0abfnrtv""])+`
| EscapedHex          | `\\x[0-9a-fA-F]{1,4}` | `(\\x[0-9a-fA-F]{1,4})+`
| Escaped Unicode     | `(\\u[0-9a-fA-F]{4}])|(\\U[0-9a-fA-F]{8})` | `((\\u[0-9a-fA-F]{4}])|(\\U[0-9a-fA-F]{8}))+`
| HexDigit            | `[a-fA-F0-9]`         | `[a-fA-F0-9]+`
| Identifier          | `[a-zA-Z0-9_]`        | `[a-zA-Z_][a-zA-Z0-9_]*`
| Letter              | `[a-zA-Z]`            | `[a-zA-Z]+`
| LowercaseIdentifier | `[a-z0-9_]`           | `[a-z_][a-z0-9_]*`
| LowercaseLetter     | `[a-z]`               | `[a-z]+`
| NewLine             | `(\r\n|\r|\n|\u0085|\u2028|\u2029)` | `(\r\n|\r|\n|\u0085|\u2028|\u2029)+`
| NonIdentifier       | `[^a-zA-Z0-9_]`       | `[^a-zA-Z0-9_]+`
| Number              |                       | `([0-9]*\.[0-9]+)|([0-9][0-9]*)`
| Punctuation         | ``\\|[!"#$%&'()*+,./:;<=>?@^_{|}\[\]~`-]`` | ``(\\|[!"#$%&'()*+,./:;<=>?@^_{|}\[\]~`-])+``
| QuotedString        |                       | `("(.*(?<!\\))")|('(.*(?<!\\))')`
| SingleQuotedString  |                       | `'(.*(?<!\\))'`
| Unicode             | `\\u(?:([0-9a-fA-F]{4})|(?:\{((?:10[0-9a-fA-F]{4})|(?:0?[0-9a-fA-F]{5})|(?:[0-9a-fA-F]{1,4}))\}))` | `(\\u(?:([0-9a-fA-F]{4})|(?:\{((?:10[0-9a-fA-F]{4})|(?:0?[0-9a-fA-F]{5})|(?:[0-9a-fA-F]{1,4}))\})))+`
| UppercaseIdentifier | `[A-Z0-9_]`           | `[A-Z_][A-Z0-9_]*`
| UppercaseLetter     | `[A-Z]`               | `[A-Z]+`
| Whitespace          | `\u0009|\u000B|\u000C|\u0020|\u00A0|\u1680|\u180E|[\u2000-\u200A]|\u202F|\u3000|\u205F` | `(\u0009|\u000B|\u000C|\u0020|\u00A0|\u1680|\u180E|[\u2000-\u200A]|\u202F|\u3000|\u205F)+`