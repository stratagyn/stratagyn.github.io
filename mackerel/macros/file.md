---
layout: default
title: File
parent: Macros
grand_parent: / Mackerel
nav_order: 3
---

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">AppendTo</b>(string, int...) &#10140; Instruction;
</code>

> Appends the concatenated content of all valid buffers in a `Document` to the file 
> specified by the given path.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">AppendTo</b>(string, Instruction) &#10140; Instruction;
</code>

> Appends the result of an instruction to the file specified by the given path.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">AppendLineTo</b>(string, int...) &#10140; Instruction;
</code>

> Appends the content of all valid buffers in a `Document`, concatenated with a new line, 
> to the file specified by the given path followed by a new line.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">AppendLineTo</b>(string, Instruction) &#10140; Instruction;
</code>

> Appends the result of an instruction to the file specified by the given path followed by a new 
> line.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Include</b>(string...) &#10140; Instruction;
</code>

> Reads and concatenates with a new line the content of the files specified by the list of paths,
> then writes the result to the current buffer followed by a new line.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Open</b>(string) &#10140; Instruction;
</code>

> Reads the contents of the file specified by the given path.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">SaveTo</b>(string, int...) &#10140; Instruction;
</code>

> Writes the concatenated content of all valid buffers in a `Document` to the file 
> specified by the given path. Overwrites the content of the file if it exists.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">SaveTo</b>(string, Instruction) &#10140; Instruction;
</code>

> Appends the result of an instruction to the file specified by the given path. Overwrites 
> the content of the file if it exists.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">SaveLineTo</b>(string, int...) &#10140; Instruction;
</code>

> Appends the content of all valid buffers in a `Document`, concatenated with 
> a new line, to the file specified by the given path followed by a new line. Overwrites 
> the content of the file if it exists.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">SaveLineTo</b>(string, Instruction) &#10140; Instruction;
</code>

> Appends a new line and the result of an instruction to the file specified by the given path
> followed by a new line. Overwrites the content of the file if it exists.
