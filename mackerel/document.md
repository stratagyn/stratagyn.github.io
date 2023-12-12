---
layout: default
title: Document
parent: / Mackerel
nav_order: 1
---

A stateful object managing multiple text output buffers.

# Constructors

---

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Document</b>(int) &#10140; Document
</code>

> Constructs a new `Document` with a given number of buffers. If the count is negative
> the default, `2` is used.

<code class="stratagyn-method-signature">
   <b class="stratagyn-method-name">Document</b>(IEnumerable&lt;KeyValuePair&lt;string, object&gt;&gt;, int) &#10140; Document
</code>

> Constructs a new `Document` with a predefined environment and given number of buffers. 
> If the count is negative the default, `2` is used.