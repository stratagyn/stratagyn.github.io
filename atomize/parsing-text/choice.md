---
layout: page
title: Choice
parent: Parsing Text
grand_parent: / Atomize
nav_order: 7
---

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Choice</b>(char...) &#10140; Parser&lt;char&gt;
</code>

> Succeeds if a scanner matches a `char` int the list, at its current offset.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Choice</b>(string...) &#10140; Parser&lt;ReadOnlyMemory&lt;char&gt;&gt;
</code>

> Succeeds if a scanner matches a `string` in the list at its current offset.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Choice</b>(Regex...) &#10140; Parser&lt;ReadOnlyMemory&lt;char&gt;&gt;
</code>

> Succeeds if a scanner matches a pattern in the list at its current offset.


<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Choice</b>(Parser&lt;T&gt;...) &#10140; Parser&lt;T&gt;
</code>

> Succeeds if a scanner would match a parser in the list at its current offset.