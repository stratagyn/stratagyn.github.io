---
layout: page
title: Empty Token
parent: Parse Results
grand_parent: / Atomize
nav_order: 1
---

# `EmptyToken<T> : IParseResult<T>`

---

A successful parse that records no information about any characters consumed. The `Length` of this token is always `0`, even if it's from a parser that consumed characters, e.g. those returned by `Parse.Ignore`. It does however, record where the token matched in the text.

# Constructors

---

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">EmptyToken</b>(int) &#10140; EmptyToken&lt;T&gt;
</code>

> Constructs an `EmptyToken` for a given index.
