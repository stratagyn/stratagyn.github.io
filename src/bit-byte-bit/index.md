# `bit-byte-bit`

Implements a [bit string](/bit-byte-bit/introduction/bit-strings.md) type represented as 
&lceil; `n/8` &rceil; bytes. The library also implements a mechanism for creating 
[bit schemes](/introduction/bit-schemes.md), a type which extracts from data from regions 
of a bit string.


## Instantiation

---

Constructors defined in the `Bits` implementation generate bit strings with a length that 
is either input-defined, or in the case of `Bits::new`, `8` times the length of the iterator.

Constructors defined by the `From` or `FromIterator` traits generate bit strings with a length
based on the input. If a collection of `bool`, the length will be equal to that of the input. 
If the input is a collection of `u8`, the length counts all bits up to and including the most 
significant one bit.

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
let bit_string = bits![0x0A, 0x0B, 0x0C];

assert_eq!(bit_string, Bits::new([0x0A, 0x0B, 0x0C]));

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

## Indexing

---

`Bits::i` can be used to access an individual bit. Bits can be `set` to one, `reset` to zero, or `toggled`.

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

## Bitwise Operations

---

Bit strings support and, or, not, xor, left and right shifting and rotation.

```rust
# use bit_byte_bit::{Bits};
let x = Bits::new([0x20, 0x30, 0x40]);
let y = Bits::new([0xA0, 0xB0, 0xC0]);

assert_eq!(x.and(&y), Bits::new([0x20, 0x30, 0x40]));
assert_eq!(x.complement(), Bits::new([0xDF, 0xCF, 0xBF]));
assert_eq!(x.or(&y), Bits::new([0xA0, 0xB0, 0xC0]));
assert_eq!(x.xor(&y), Bits::new([0x80, 0x80, 0x80]));

let bits = Bits::from([0x0A, 0x0B, 0x0C]);

assert_eq!(bits.len(), 20);
assert_eq!(bits.shifted_left(17), Bits::slice(&[0x00, 0x00, 0x04], 20));
assert_eq!(bits.shifted_right(17), Bits::slice(&[0x06, 0x00, 0x00], 20));
assert_eq!(bits.rotated_left(4), Bits::slice(&[0xAC, 0xB0, 0x00], 20));
assert_eq!(bits.rotated_right(4), Bits::slice(&[0xB0, 0xC0, 0x0A], 20));
```

## Iteration

---

Iteration can be done bit-by-bit, or byte-by-byte using:
* `Bits::iter`
* `Bits::iter_from`
* `Bits::into_iter`
* `Bits::bytes` (via `&[u8]::iter`)
* `Bits::into_bytes`

```rust
# use bit_byte_bit::{Bits};
let x = Bits::new([0xAB, 0xCD, 0xEF]);

let mut ones = 0;

for bit in x.iter() { if bit == 1 { ones += 1; } }

assert_eq!(ones, 17);

ones = 0;

for bit in x.iter_from(13) { if bit == 1 { ones += 1; } }

assert_eq!(ones, 9);

let mut y = x.bytes().iter();

assert_eq!(y.next(), Some(&0xAB));
```

### Note about endianness

While the library does not implement any notion of endianness, indexing and methods ending
in either `_left` or `_right` assume bit<sub>0</sub> of an n-bit string is the most right bit,
while bit<sub>n-1</sub> is most left.
