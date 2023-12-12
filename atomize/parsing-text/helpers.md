---
layout: page
title: Helpers
parent: Parsing Text
grand_parent: / Atomize
nav_order: 9
---

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Island<O, T, C></b>(Parser&lt;O&gt;, Parser&lt;T&gt;, Parser&lt;C&gt;) &#10140; Parser&lt;T&gt;
</code>

> Applies three parsers in sequence, returning the result of the second while ignoring the results of the other two.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Ref</b>(() &#10140; Parser&lt;T&gt;) &#10140; Parser&lt;T&gt;
</code>


> Applies a lazily defined parser

