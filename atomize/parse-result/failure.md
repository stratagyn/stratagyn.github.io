---
layout: page
title: Failure
parent: Parse Results
grand_parent: / atomize
nav_order: 3
---

# `Failure<T>`

---

A failed parse at the given `Offset`, explained by `Why`. All other properties are `default`.

# Constructors

---

Constructs a `Failure` for a given index and reason.

```
Failure t :: (int, string) > Failure t
```