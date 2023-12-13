---
layout: page
title: Parse Results
parent: / Atomize
nav_order: 2
has_children: true
has_toc: false
---

# `IParseResult<T>`

---

Interface for results returned from parse attempts.

# Instance Properties

---

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">IsToken</b> &#10140; bool
</code>

> Whether the result is a successful one or failure

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Length</b> &#10140; int
</code>

> Number of characters matched

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Offset</b> &#10140; int
</code>

> Where in the text the match began

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Why</b> &#10140; string
</code>

> Reason why a successful match was not made

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Value</b> &#10140; T?
</code>

> The token of a successful parse

# Implemented By

---

* [`EmptyToken<T>`]({{ site.baseurl }}{% link atomize/parse-result/empty-token.md %})
* [`Failure<T>`]({{ site.baseurl }}{% link atomize/parse-result/failure.md %})
* [`Lexeme<T>`]({{ site.baseurl }}{% link atomize/parse-result/lexeme.md %})