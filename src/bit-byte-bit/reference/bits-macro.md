# `bits!`

---

```rust
macro_rules! bits {
    () => { ... };
    (0; $n:expr) => { ... };
    (1; $n:expr) => { ... };
    (8; $byte:expr; $n:expr) => { ... };
    ($($byte:expr),+ $(,)?) => { ... };
    ($($byte:expr),+; => $n:expr) => { ... };
    ($($byte:expr),+; %) => { ... };
}
```

Macro implementing a subset of the Bits constructors

## Example

``` rust
let x1 = bits![];

assert_eq!(x1, Bits::empty());

let x2 = bits![0x0A, 0x0B, 0x0C];

assert_eq!(x2, Bits::new([0x0A, 0x0B, 0x0C]));

let x3 = bits![0x0A, 0x0B, 0x0C; => 16];

assert_eq!(x3, Bits::aligned(16, [0x0A, 0x0B, 0x0C]));

let x4 = bits![0x0A, 0x0B, 0x0C; %];

assert_eq!(x4, Bits::packed([0x0A, 0x0B, 0x0C]));

let x5 = bits![1; 17];

assert_eq!(x5, Bits::ones(17));

let x6 = bits![0; 17];

assert_eq!(x6, Bits::zeros(17));
assert_eq!(x6.len(), 17);

let x7 = bits![8; 0; 17];

assert_eq!(x7, Bits::new(vec![0; 17]));
assert_eq!(x7.len(), 136);
```