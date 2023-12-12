---
layout: page
title: Empty Token
parent: Parse Results
grand_parent: / atomize
nav_order: 1
---

# `EmptyToken<T>`

---

A successful parse that records no information about any characters consumed. The `Length` of this token is always `0`, even if it's from a parser that consumed characters, e.g. those returned by `Parse.Ignore`. It does however, record where the token matched in the text.

# Constructors

---

Constructs an `EmptyToken` for a given index.

```
EmptyToken t :: int > EmptyToken t
```
