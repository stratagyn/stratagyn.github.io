---
layout: page
title: Failure
parent: Parse Results
grand_parent: / Atomize
nav_order: 3
---

# `Failure<T> : IParseResult<T>`

---

A failed parse at the given `Offset`, explained by `Why`. All other properties are `default`.

# Constructors

---

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Failure</b>(int, string) &#10140; Failure&lt;T&gt;
</code>

> Constructs a `Failure` for a given index and reason.