---
layout: default
title: General
parent: Macros
grand_parent: / Mackerel
nav_order: 8
---

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Block</b>(Instruction...) &#10140; Instruction;
</code>

> Applies a sequence of instructions returning the result of the last one.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Mutate&lt;T&gt;</b>(T, T &#10140; Instruction) &#10140; Instruction;
</code>

> Transforms a value to an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Mutate&lt;T&gt;</b>(Instruction, string &#10140; T, T &#10140; Instruction) &#10140; Instruction;
</code>

> Transforms the result of an instruction to a value, then transforms that value to an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Print</b>(Instruction) &#10140; Instruction;
</code>

> Writes the result of an instruction to the standard output.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">PrintError</b>(Instruction) &#10140; Instruction;
</code>

> Writes the result of an instruction to the standard error output.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">PrintErrorLine</b>(Instruction) &#10140; Instruction;
</code>

> Writes the result of an instruction to the standard error output followed by a new line.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">PrintLine</b>(Instruction) &#10140; Instruction;
</code>

> Writes the result of an instruction to the standard output followed by a new line.