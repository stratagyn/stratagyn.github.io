---
layout: page
title: Parse Results
parent: / atomize
nav_order: 2
has_children: true
has_toc: false
---

# `IParseResult<T>`

---

`IParseResult<T>` is the interface for parse attempts.

# Instance Properties

---

Whether the result is a successful one or failure

```
IsToken :: bool
```

Number of characters matched

```
Length :: int
```

Where in the text the match was attempted

```
Offset :: int
```

Reason why a successful match was not made

```
Why :: string
```

The token of a successful parse

```
Value :: T?
```

# Implemented By

---

* [`EmptyToken<T>`]({{ site.baseurl }}{% link atomize/parse-result/empty-token.md %})
* [`Failure<T>`]({{ site.baseurl }}{% link atomize/parse-result/failure.md %})
* [`Lexeme<T>`]({{ site.baseurl }}{% link atomize/parse-result/lexeme.md %})