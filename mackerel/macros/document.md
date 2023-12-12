---
layout: default
title: Document
parent: Macros
grand_parent: / Mackerel
nav_order: 2
---

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Buffer</b>(int) &#10140; Instruction;
</code>

> Alters the output buffer of a `Document`. If the buffer is invalid, all
> subsequent writes to the document are ignored until a valid buffer is given.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Clear</b>(in Document) &#10140; string;
</code>

> Clears the contents and resets the state of a `Dcoument`.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Get</b>(string) &#10140; Instruction;
</code>

> Retrieves the value with the given name in a `Document` and converts it
> to a `string`. If the name is not defined, `""` is returned.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Get&lt;T&gt;</b>(string, T &#10140; Instruction) &#10140; Instruction;
</code>

> Retrieves the value with the given name and type in a `Document` and applies an instruction transformer
> to it. If the name is not defined or of the given type, `""` is returned.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">RAW</b>(Instruction, int...) &#10140; Instruction;
</code>

> Concatenates the content of all valid buffers after applying an instruction
> to a `Document`.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Read</b>(int...) &#10140; Instruction;
</code>

> Concatenates the contents of all valid buffers in a sequence.
> If the sequence is empty, the last buffer set is read.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">ReadLine</b>(int...) &#10140; Instruction;
</code>

> Concatenates the contents of all valid buffers in a sequence with a new line.
> If the sequence is empty, the last buffer set is read.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Set&lt;T&gt;</b>(string, T) &#10140; Instruction;
</code>

> Binds the given name to the specified value in a `Document`, if the document does not
> have a definition for it.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">SetOrUpdate&lt;T&gt;</b>(string, T) &#10140; Instruction;
</code>

> Binds the given name to the specified value in a `Document`, overwriting the previous
> definition if one exists.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Unset&lt;T&gt;</b>(string) &#10140; Instruction;
</code>

> Removes the given name in a `Document` if it is defined.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Update&lt;T&gt;</b>(string, T) &#10140; Instruction;
</code>

> Binds the given name to the specified value in a `Document`, if the document has a definition
> for it.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">WAR</b>(int...) &#10140; Instruction;
</code>

> Concatenates the content of all valid buffers and writes the result to the current buffer of 
> a `Document`.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Write</b>(Instruction...) &#10140; Instruction;
</code>

> Concatenates the results of each instruction in a sequence and writes the result 
> to the current buffer of a `Document`.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Write</b>(IEnumerable&lt;string&gt;) &#10140; Instruction;
</code>

> Concatenates a collection of strings and writes the result to the current buffer of 
> a `Document`.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">WriteLine</b>(Instruction...) &#10140; Instruction;
</code>

> Concatenates the results of each instruction in a sequence with a new line and writes 
> the result to the current buffer of a `Document` followed by a new line.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">WriteLine</b>(IEnumerable&lt;string&gt;) &#10140; Instruction;
</code>

> Concatenates a collection of strings with a new line and writes the result to the current 
> buffer of a `Document` followed by a new line.

