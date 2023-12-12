---
layout: default
title: Conditionals
parent: Macros
grand_parent: / Mackerel
nav_order: 5
---

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">If</b>(string &#10140; bool, Instruction, Instruction, Instruction) &#10140; Instruction;
</code>

> Applies a test to the result of the first instruction and returns the second if it is `true`,
> otherwise the third instruction is returned.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">If&lt;T&gt;</b>(T &#10140; bool, T, Instruction, Instruction) &#10140; Instruction;
</code>

> Applies a test to a value and returns the first instruction if it is `true`, otherwise the second.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">IfDef</b>(string, Instruction, Instruction) &#10140; Instruction;
</code>

> Checks if a name is defined in a `document` and returns the first instruction if it is `true`, otherwise the second.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">IfN</b>(string &#10140; bool, Instruction, Instruction, Instruction) &#10140; Instruction;
</code>

> Applies a test to the result of the first instruction and returns the second if it is `false`,
> otherwise the third instruction is returned.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">IfN&lt;T&gt;</b>(T &#10140; bool, T, Instruction, Instruction) &#10140; Instruction;
</code>

> Applies a test to a value and returns the first instruction if it is `false`, otherwise the second.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">IfNDef</b>(string, Instruction, Instruction) &#10140; Instruction;
</code>

> Checks if a name is defined in a `document` and returns the first instruction if it is `true`, otherwise the second.