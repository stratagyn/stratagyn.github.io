# Indexing

---

`Bits::i` can be used to access an individual bit. Bits can be `set` to one,
`reset` to zero, or `toggled`.

```rust
# use bit_byte_bit::{Bits};
let mut bits = Bits::new([0x0A, 0x0B, 0x0C]);

assert_eq!(bits.i(0), 0);
assert_eq!(bits.i(1), 1);

bits.set(0);
bits.reset(1);

assert_eq!(bits.i(0), 1);
assert_eq!(bits.i(1), 0);

bits.toggle(0);
bits.toggle(1);

assert_eq!(bits.i(0), 0);
assert_eq!(bits.i(1), 1);
```