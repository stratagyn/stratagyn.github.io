---
layout: page
title: Basic Parsers
parent: Parsing Text
grand_parent: / Atomize
nav_order: 1
---

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Empty&lt;T&gt;</b>(TextScanner) &#10140; IParseResult&lt;T&gt;
</code>

> Always succeeds.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">EndOfText&lt;T&gt;</b>(TextScanner) &#10140; IParseResult&lt;T&gt;
</code>

> Succeeds when the scanner is exhausted.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Fail&lt;T&gt;</b>(TextScanner) &#10140; IParseResult&lt;T&gt;
</code>

> Always fails.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">StartOfText&lt;T&gt;</b>(TextScanner) &#10140; IParseResult&lt;T&gt;
</code>

> Succeeds when the given scanner has yet to consume any characters.