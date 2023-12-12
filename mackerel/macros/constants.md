---
layout: default
title: Constants
parent: Macros
grand_parent: / Mackerel
nav_order: 1
---

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Empty</b>(in Document) &#10140; string;
</code>

> Expands to the empty string.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">LongText</b>(string) &#10140; Instruction;
</code>

> Expands to the given `string` trimmed of all leading and trailing whitespace.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Text</b>(string) &#10140; Instruction;
</code>

> Expands to the given `string`.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Str</b>(object) &#10140; Instruction;
</code>

> Expands to the result of calling `ToString` on the `object`.