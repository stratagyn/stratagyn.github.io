---
layout: page
title: Assertions
parent: Parsing Text
grand_parent: / Atomize
nav_order: 3
---

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">FollowedBy&lt;T&gt;</b>(Parser&lt;T&gt;) &#10140; Parser&lt;T&gt;
</code>

> Succeeds if the scanner would match the given `Parser<T>` at its current offset, but doesn't consume
> any characters, returning an `EmptyToken<T>` on success instead.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">NotFollowedBy&lt;T&gt;</b>(Parser&lt;T&gt;) &#10140; Parser&lt;T&gt;
</code>

> Succeeds if the scanner fails to match the given `Parser<T>` at its current offset, 
> returning an `EmptyToken<T>` instead.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">PrecededBy&lt;T&gt;</b>(Parser&lt;T&gt;) &#10140; Parser&lt;T&gt;
</code>

> Searches backwards for a match to a `Parser<T>` that ends at one less than the current offset.
> Succeeds if it finds one, but doesn't consume any characters, returning an `EmptyToken<T>` on 
> success instead.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">NotPrecededBy&lt;T&gt;</b>(Parser&lt;T&gt;) &#10140; Parser&lt;T&gt;
</code>

> Searches backwards for a match to a `Parser<T>` that ends at one less than the current offset.
> Succeeds if it fails to find one, returning an `EmptyToken<T>` instead.