---
layout: page
title: Packrat Parsers
parent: Parsing Text
grand_parent: / Atomize
nav_order: 8
---



<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Memoize&lt;T&gt;</b>(Parser&lt;T&gt;) &#10140; Parser&lt;T&gt;
</code>

> Transforms a parser into a [packrat parser](https://en.wikipedia.org/wiki/Packrat_parser). 
> The resulting parser does ***not*** necessarily support left recursion.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">DirectLeftRecursion&lt;T&gt;</b>(Parser&lt;T&gt;) &#10140; Parser&lt;T&gt;
</code>

> Transforms a parser into a [packrat parser](https://en.wikipedia.org/wiki/Packrat_parser),
> supporting direct left recursion only. The implementation is based on this 
> [paper](https://web.cs.ucla.edu/~todd/research/pepm08.pdf).

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">LeftRecursion&lt;T&gt;</b>(Parser&lt;T&gt;) &#10140; Parser&lt;T&gt;
</code>

> Transforms a parser into a [packrat parser](https://en.wikipedia.org/wiki/Packrat_parser),
> supporting direct or indirect left recursion. The implementation is based on this 
> [paper](https://web.cs.ucla.edu/~todd/research/pepm08.pdf).