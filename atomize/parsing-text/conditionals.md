---
layout: page
title: Conditionals
parent: Parsing Text
grand_parent: / Atomize
nav_order: 4
---

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">If&lt;T, U&gt;</b>(Parser&lt;T&gt;, Parser&lt;U&gt;, Parser&lt;U&gt;) &#10140; Parser&lt;U&gt;
</code>

> Applies the first parser and chooses one of two parsers to apply depending on whether or not it succeeded.
> The chosen parser will then be applied at the current offset.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">IfFollowedBy&lt;T&gt;</b>(Parser&lt;T&gt;, Parser&lt;T&gt;) &#10140; Parser&lt;T&gt;
</code>

> Succeeds if the scanner would match the first `Parser<T>` at its current offset, then match the second `Parser<T>`,
> only consuming the characters of the first parser.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">IfNotFollowedBy&lt;T&gt;</b>(Parser&lt;T&gt;, Parser&lt;T&gt;) &#10140; Parser&lt;T&gt;
</code>

> Succeeds if the scanner would match the first `Parser<T>` at its current offset, then fail to match the second `Parser<T>`.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">IfPrecededBy&lt;T&gt;</b>(Parser&lt;T&gt;, Parser&lt;T&gt;) &#10140; Parser&lt;T&gt;
</code>

> If the scanner would match the first `Parser<T>` at its current offset, it is then searched backwards for a match 
> to the second `Parser<T>` that ends at one less than the where the first parser started.
> Succeeds if it finds one, only consuming the characters of the first parser.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">IfNotPrecededBy&lt;T&gt;</b>(Parser&lt;T&gt;, Parser&lt;T&gt;) &#10140; Parser&lt;T&gt;
</code>

> If the scanner would match the first `Parser<T>` at its current offset, it is then searched backwards for a match 
> to the second `Parser<T>` that ends at one less than the where the first parser started.
> Succeeds if it fails to find one.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Satisfies&lt;T&gt;</b>(Parser&lt;T&gt;, T &#10140; bool) &#10140; Parser&lt;T&gt;
</code>

> Succeeds if the scanner would match the `Parser<T>` at its current offset, and the resulting value passes the given test.
> *Also implemented as* `Where<T>`.