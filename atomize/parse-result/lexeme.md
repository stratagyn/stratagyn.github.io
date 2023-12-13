---
layout: page
title: Lexeme
parent: Parse Results
grand_parent: / Atomize
nav_order: 2
---

# `Lexeme<T> : IParseResult<T>`

---

A successful parse at the given `Offset`, consuming `Length` characters. `Value` holds an object of type `T`.

# Constructors

---

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Lexeme</b>(int, int, T) &#10140; Lexeme&lt;T&gt;
</code>

> Constructs a `Lexeme` for a given index, length, and value.