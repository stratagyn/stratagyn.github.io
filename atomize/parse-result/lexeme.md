---
layout: page
title: Lexeme
parent: Parse Results
grand_parent: / atomize
nav_order: 2
---

# `Lexeme<T>`

---

A successful parse at the given `Offset`, consuming `Length` characters. `Value` holds an object of type `T`.

# Constructors

---

Constructs a `Lexeme` for a given index, length, and value.

```
Failure t :: (int, int, t) > Lexeme t
```