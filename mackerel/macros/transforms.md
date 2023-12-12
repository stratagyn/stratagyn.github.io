---
layout: default
title: Transforms
parent: Macros
grand_parent: / Mackerel
nav_order: 4
---

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Bind</b>(Instruction, string &#10140; Instruction) &#10140; Instruction;
</code>

> Transforms the result of an instruction into a new instruction. *Also implemented as* `SelectMany`.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Map</b>(Instruction, string &#10140; string) &#10140; Instruction;
</code>

> Transforms the result of an instruction. *Also implemented as* `Select`.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">SelectMany</b>(Instruction, string &#10140; Instruction, (string, string) &#10140; string) &#10140; Instruction;
</code>

> Transforms the result of an instruction into a new instruction, then combines their results.