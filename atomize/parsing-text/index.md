---
layout: page
title: Parsing Text
parent: / Atomize
nav_order: 2
has_children: true
has_toc: false
---

# `Parse`

---

The static `Parse` class provides methods for building recursive-descent parsers, as well as combinators for creating more complex parsers from simpler ones. Parsers are functions that anaylze text producing some arbitrary structure. 

<code class="stratagyn-method-signature">
   delegate <b class="stratagyn-method-name">Parser&lt;T&gt;</b>(TextScanner) &#10140; IParseResult&lt;T&gt;
</code>


All parsers return an `IParseResult<T>` object indicating whether it successfully matched a prefix. In the case of success, the result is either an [`EmptyToken<T>`]({{ site.baseurl }}{% link atomize/parse-result/empty-token.md %}) or a [`Lexeme<T>`]({{ site.baseurl }}{% link atomize/parse-result/lexeme.md %}), otherwise, it is a [`Failure<T>`]({{ site.baseurl }}{% link atomize/parse-result/failure.md %}).