# Instantiation

---


Constructors defined in the [Bits] implementation generate bit strings
with a length that is either input-defined, or in the case of [Bits::new],
`8` times the length of the iterator.

Constructors defined by the [From](Bits::from) or
[FromIterator](Bits::from_iter) traits generate bit strings with a length
based on the input. If a collection of `bool`, the length will be equal to
that of the input. If the input is a collection of `u8`, the length counts
all bits up to and including the most significant one bit.

```rust
# use bit_byte_bit::Bits;

let bits = Bits::new([0x0A, 0x0B, 0x0C]);

assert_eq!(bits.len(), 24);

let bits_no_lz = Bits::from([0x0A, 0x0B, 0x0C]);

assert_eq!(bits_no_lz.len(), 20);

let aligned_bits = Bits::aligned(16, [0x0A, 0x0B, 0x0C]);

assert_eq!(aligned_bits.len(), 32);

let packed_bits = Bits::packed([0x0A, 0x0B, 0x0C]);

assert_eq!(packed_bits, Bits::from([0xBA, 0x0C]));

let bools = Bits::from([true, false, true, false, false, true]);

assert_eq!(bools, Bits::slice(&[0x25], 6));

let slice = Bits::take(&[0x0A, 0x0B, 0x0C], 3, 9);

assert_eq!(slice, Bits::from([0x61, 0x01]));
```

The [bits!](/bit-byte-bit/reference/bits-macro.md) macro is also provided for convenience, wrapping the constructors:
* `Bits::new`
* `Bits::aligned`
* `Bits::ones`
* `Bits::packed`
* `Bits::zeros`

```rust
# use bit_byte_bit::{Bits, bits};
let bits = bits![0x0A, 0x0B, 0x0C];

assert_eq!(bits, Bits::new([0x0A, 0x0B, 0x0C]));

let repeated_bytes = bits![8; 0x0F; 20];

assert_eq!(repeated_bytes, Bits::new([0x0F; 20]));

let aligned_bits = bits![0x0A, 0x0B, 0x0C; => 16];

assert_eq!(aligned_bits.len(), 32);

let ones = bits![1; 20];

assert_eq!(ones, Bits::ones(20));

let packed_bits = bits![0x0A, 0x0B, 0x0C; %];

assert_eq!(packed_bits, Bits::from([0xBA, 0x0C]));

let zeros = bits![0; 20];

assert_eq!(zeros, Bits::zeros(20));

```