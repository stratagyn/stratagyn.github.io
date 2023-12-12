---
layout: page
title: Text
nav_order: 1
parent: / AtoMac
---

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Replace</b>(Instruction, Parser&lt;char&gt;, Instruction) &#10140; Instruction;
</code>

> Replaces each match of a character `Parser` in the result of an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Replace</b>(Instruction, Parser&lt;char&gt;, char &#10140; Instruction) &#10140; Instruction;
</code>

> Transforms each match of a character `Parser` in the result of an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Replace</b>(Instruction, Parser&lt;char&gt;, (char, int) &#10140; Instruction) &#10140; Instruction;
</code>

> Transforms and counts each match of a character `Parser` in the result of an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Replace</b>(Instruction, Parser&lt;ReadOnlyMemory&lt;char&gt;&gt;, Instruction) &#10140; Instruction;
</code>

> Replaces each match of a string `Parser` in the result of an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Replace</b>(Instruction, Parser&lt;ReadOnlyMemory&lt;char&gt;&gt;, string &#10140; Instruction) &#10140; Instruction;
</code>

> Transforms each match of a string `Parser` in the result of an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Replace</b>(Instruction, Parser&lt;ReadOnlyMemory&lt;char&gt;&gt;, (string, int) &#10140; Instruction) &#10140; Instruction;
</code>

> Transforms and counts each match of a string `Parser` in the result of an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Replace</b>(Instruction, Parser&lt;Instruction&gt;, Instruction) &#10140; Instruction;
</code>

> Replaces each match of an instruction `Parser` in the result of an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Replace</b>(Instruction, Parser&lt;Instruction&gt;, string &#10140; Instruction) &#10140; Instruction;
</code>

> Transforms each match of an instruction `Parser` in the result of an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Replace</b>(Instruction, Parser&lt;Instruction&gt;, (string, int) &#10140; Instruction) &#10140; Instruction;
</code>

> Transforms and counts each match of an instruction `Parser` in the result of an instruction.