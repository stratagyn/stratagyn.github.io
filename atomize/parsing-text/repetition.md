---
layout: page
title: Repetition
parent: Parsing Text
grand_parent: / Atomize
nav_order: 5
---

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Exactly&lt;T&gt;</b>(int, Parser&lt;T&gt;) &#10140; Parser&lt;IList&lt;T&gt;&gt;
</code>

> Succeeds if the scanner matches a `Parser<T>` an exact number of times.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">NotExactly&lt;T&gt;</b>(int, Parser&lt;T&gt;) &#10140; Parser&lt;IList&lt;T&gt;&gt;
</code>

> Succeeds if the scanner matches a `Parser<T>` less than or more than a given number of times.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Maximum&lt;T&gt;</b>(int, Parser&lt;T&gt;) &#10140; Parser&lt;IList&lt;T&gt;&gt;
</code>

> Succeeds if the scanner matches a `Parser<T>` at most a given number of times.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Minimum&lt;T&gt;</b>(int, Parser&lt;T&gt;) &#10140; Parser&lt;IList&lt;T&gt;&gt;
</code>

> Succeeds if the scanner matches a `Parser<T>` at least a given number of times.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Repeat&lt;T&gt;</b>(int, int, Parser&lt;T&gt;) &#10140; Parser&lt;IList&lt;T&gt;&gt;
</code>

> Succeeds if the scanner matches a `Parser<T>` between a given minimum and maximum number of times.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Optional&lt;T&gt;</b>(int, Parser&lt;T&gt;) &#10140; Parser&lt;IList&lt;T&gt;&gt;
</code>

> Succeeds whether or not the scanner matches a `Parser<T>`, returning an `EmptyToken<T>` on failure.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">ZeroOrMore&lt;T&gt;</b>(Parser&lt;T&gt;) &#10140; Parser&lt;IList&lt;T&gt;&gt;
</code>

> Succeeds if the scanner matches a `Parser<T>` zero or more times.


