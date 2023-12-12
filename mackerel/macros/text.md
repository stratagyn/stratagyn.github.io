---
layout: default
title: Text
parent: Macros
grand_parent: / Mackerel
nav_order: 7
---

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Concat</b>(Instruction...) &#10140; Instruction;
</code>

> Concatenates the results of a sequence of instructions.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Delete</b>(Instruction, int) &#10140; Instruction;
</code>

> Deletes the characters from the result of an instruction starting at a given index and proceeding
> until to the end of the `string`.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Delete</b>(Instruction, int, int) &#10140; Instruction;
</code>

> Deletes a given number of characters from the result of an instruction starting at a given index.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Join</b>(string, Instruction...) &#10140; Instruction;
</code>

> Concatenates the results of a sequence of instructions with a given `string`.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Join</b>(Instruction, Instruction...) &#10140; Instruction;
</code>

> Concatenates the results of a sequence of instructions with the result of an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Lowercase</b>(Instruction) &#10140; Instruction;
</code>

> Lowercases the result of an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">PadEnd</b>(Instruction, int) &#10140; Instruction;
</code>

> Adds a given number of spaces to the end of the result of an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">PadEnd</b>(Instruction, string, int) &#10140; Instruction;
</code>

> Concatenates a string repeated a given number of times to the end of the result of an instruction.


<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">PadEnd</b>(Instruction, Instruction, int) &#10140; Instruction;
</code>

> Concatenates the result of the second instruction repeated a given number of times to the end 
> of the result of the first.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">PadStart</b>(Instruction, int) &#10140; Instruction;
</code>

> Adds a given number of spaces to the beginning of the result of an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">PadStart</b>(Instruction, string, int) &#10140; Instruction;
</code>

> Concatenates a string repeated a given number of times to the beginning of the result of an instruction.


<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">PadStart</b>(Instruction, Instruction, int) &#10140; Instruction;
</code>

> Concatenates the result of the second instruction repeated a given number of times to the beginning 
> of the result of the first.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Replace</b>(Instruction, char, char) &#10140; Instruction;
</code>

> Replaces instances of the first character with the second in the result of an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Replace</b>(Instruction, char[], char[]) &#10140; Instruction;
</code>

> Replaces instances of the characters in the first array with the character at the same index
> in the second array in the result of an instruction. If the corresponding index is outside the range
> of the second array, the character is removed.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Replace</b>(Instruction, string, string) &#10140; Instruction;
</code>

> Replaces instances of the first string with the second in the result of an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Replace</b>(Instruction, string, Instruction) &#10140; Instruction;
</code>

> Replaces instances of a string with the result of an instruction, in the result of an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Replace</b>(Instruction, string, string &#10140; string) &#10140; Instruction;
</code>

> Transforms instances of a string in the result of an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Replace</b>(Instruction, string, (string, int) &#10140; string) &#10140; Instruction;
</code>

> Transforms and counts instances of a string in the result of an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Replace</b>(Instruction, string, (string, int) &#10140; Instruction) &#10140; Instruction;
</code>

> Transforms and counts instances of a string in the result of an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Replace</b>(Instruction, Regex, string) &#10140; Instruction;
</code>

> Replaces each match of a `Regex` with a stirng in the result of an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Replace</b>(Instruction, Regex, Instruction) &#10140; Instruction;
</code>

> Replaces each match of a `Regex` with the result of an instruction, in the result of an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Replace</b>(Instruction, Regex, string &#10140; string) &#10140; Instruction;
</code>

> Transforms each match of a `Regex` in the result of an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Replace</b>(Instruction, Regex, (string, int) &#10140; string) &#10140; Instruction;
</code>

> Transforms and counts each match of a `Regex` in the result of an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Replace</b>(Instruction, Regex, string &#10140; Instruction) &#10140; Instruction;
</code>

> Transforms each match of a `Regex` in the result of an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Replace</b>(Instruction, Regex, (string, int) &#10140; Instruction) &#10140; Instruction;
</code>

> Transforms and counts each match of a `Regex` in the result of an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Replace</b>(Instruction, Instruction, Instruction) &#10140; Instruction;
</code>

> Replaces each match of the result of the second instruction with that of the third in the result of the first.


<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Replace</b>(Instruction, Instruction, string &#10140; Instruction) &#10140; Instruction;
</code>

> Transforms each match of the result of the second instruction in the result of the first.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Replace</b>(Instruction, Instruction, (string, int) &#10140; Instruction) &#10140; Instruction;
</code>

> Transforms and counts each match of the result of the second instruction in the result of first.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Substring</b>(Instruction, int) &#10140; Instruction;
</code>

> The string of characters from a given index to the end of the result of an instruction

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Substring</b>(Instruction, int, int) &#10140; Instruction;
</code>

> The string of characters with a maximum length starting from a given index of the result of an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Titlecase</b>(Instruction) &#10140; Instruction;
</code>

> Converts the result of an instruction to titlecase.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Trim</b>(Instruction, char...) &#10140; Instruction;
</code>

> Removes all occurences of the given characters from the beginning and end of the result of an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">TrimEnd</b>(Instruction, char...) &#10140; Instruction;
</code>

> Removes all occurences of the given characters from the end of the result of an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">TrimStart</b>(Instruction, char...) &#10140; Instruction;
</code>

> Removes all occurences of the given characters from the beginning of the result of an instruction.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Uppercase</b>(Instruction) &#10140; Instruction;
</code>

> Capitalizes the result of an instruction.

