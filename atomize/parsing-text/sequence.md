---
layout: page
title: Sequence
parent: Parsing Text
grand_parent: / Atomize
nav_order: 6
---

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Bind&lt;T, U&gt;</b>(Parser&lt;T&gt;, T &#10140; Parser&lt;U&gt;) &#10140; Parser&lt;U&gt;
</code>

> Transforms a successful parse result into a new parser. *Also implemented as* `SelectMany<T, U>`.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Map&lt;T, U&gt;</b>(Parser&lt;T&gt;, T &#10140; U) &#10140; Parser&lt;U&gt;
</code>

> Transforms a successful parse result. *Also implemented as* `Select<T, U>`.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">SelectMany&lt;T, U, V&gt;</b>(Parser&lt;T&gt;, T &#10140; Parser&lt;U&gt;, (T, U) &#10140; V ) &#10140; Parser&lt;V&gt;
</code>

> Transforms a successful parse result into a new parser, combining the results of both parsers.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Partial&lt;T, U&gt;</b>(Parser&lt;T&gt;, T &#10140; Parser&lt;U&gt;) &#10140; Parser&lt;(T, IParseResult&lt;U&gt;)&gt;
</code>

> Attempts to transform a successful parse result into a new parser. On success, the resulting pair has a first element that is the value of the `Parser<T>` if it succeeded, 
> and a second element that is the result of the `Parser<U>` returned from the binding function.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Or&lt;T, U&gt;</b>(Parser&lt;T&gt;, Parser&lt;U&gt;) &#10140; Parser&lt;(IParseResult&lt;T&gt;, IParseResult&lt;U&gt;)&gt;
</code>

> Attempts to match two parsers in sequence, if that fails, attempts to match one or the other. On success, the resulting pair will have a first element that is the result of the`Parser<T>`, 
> and a second element that is the result of the `Parser<U>`, where at least one has succeeded.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Join&lt;T, S&gt;</b>(Parser&lt;S&gt;, params Parser&lt;T&gt;) &#10140; Parser&lt;&lt;T&gt;&gt;
</code>

> Alternates applying a parser from a sequence with a separator parser, ignoring the results of the separator.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">SeparatedBy&lt;T, S&gt;</b>(Parser&lt;T&gt;, Parser&lt;S&gt;) &#10140; Parser&lt;IList&lt;T&gt;&gt;
</code>

> Alternates applying two parsers, returning only the results of the first parser.