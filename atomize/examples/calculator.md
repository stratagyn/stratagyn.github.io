---
layout: page
title: Calculator
parent: Examples
grand_parent: / Atomize
nav_order: 1
---

# Grammar

---

```
Additive
: Additive /[+-]/ Multiplicative
| Multiplicative;

Multiplicative
: Multiplicative /[*\/%]/ Atomic
| Atomic;

Atomic
: /[+-]/? NUMBER
| '(' Additive ')';
```

# Implementation

---

```cs
using Atomize;

using static Atomize.Parse;

public static class BasicCalculator
{
   private static readonly Parser<double> Atomic = 
      from sign in Optional(Choice('+', '-'))
      from num in 
         Choice(
            from n in Text.Number 
            select double.Parse(n.Span),

            Island(Atom('('), Ref(() => Additive!), Atom(')'))
         )
      select sign == '-' ? -num : num;

   private static readonly Parser<double> Multiplicative = 
      DirectLeftRecursion(
         Choice(
            from left in Ref(() => Multiplicative!)
            from op in Choice('*', '/', '%'),
            from right in Atomic
            select op switch 
            {
               '*' => left * double.Parse(right.Span),
               '/' => left / double.Parse(right.Span),
               _ => left % double.Parse(right.Span)
            },
            
            Atomic
         )
      );    
   
   private static readonly Parser<double> Additive =
      DirectLeftRecursion(
         Choice(
            from left in Ref(() => Additive!)
            from op in Choice('+', '-'),
            from right in Multiplicative
            select op == '+'
               ? left + double.Parse(right.Span)
               : left - double.Parse(right.Span),
            
            Multiplicative
         )
      ); 

   public static IParseResult<double> Run(string expr) => 
      Additive(new TextScanner(expr, true));

   public static IParseResult<double> Run(TextScanner expr) => 
      Additive(expr);
}
```