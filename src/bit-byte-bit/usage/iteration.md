# Iteration

---

Iteration can be done in several ways. 
* `Bits::iter` -- iterates over individual bits
* `Bits::iter_from` -- iterates over individual bits starting from a given index in the bit string
* `Bits::into_iter` -- iterates over individual bits, consuming bit string
* `Bits::bytes` (via `&[u8]::iter`) -- iterates over underlying bytes
* `Bits::into_bytes` -- iterates over underlying bytes, consuming bit string
* `Vec::<*>::from` -- [converts](/bit-byte-bit/usage/conversion.md) a bit string into a vector, consuming the bit 
  string. `*` is a floating point or integer type that is not `isize` or `usize`, `i128`, `u128` .
* `bits_as::vec_*` -- same as `Vec::<*>::from` but does not consume the bit string.



```rust
# use bit_byte_bit::{Bits, bits_as};
let bits = Bits::new([0xBA, 0xDC, 0xFE]);

let mut ones = 0;

for bit in bits.iter() { if bit == 1 { ones += 1; } }

assert_eq!(ones, 17);

ones = 0;

for bit in bits.iter_from(13) { if bit == 1 { ones += 1; } }

assert_eq!(ones, 9);

let bytes_iter = bits.bytes().iter();

assert_eq!(bytes_iter.next(), Some(&0xAB));

let shorts = bits_as::vec_i16(&bits);
let mut shorts_iter = shorts.into_iter();

assert_eq!(shorts_iter.next(), Some(0xDCBAu16 as i16));
assert_eq!(shorts_iter.next(), Some(0xFFFEu16 as i16));

let ushorts = Vec::<u16>::from(bits);
let mut ushorts_iter = ushorts.into_iter();

assert_eq!(ushorts_iter.next(), Some(0xDCBA));
assert_eq!(ushorts_iter.next(), Some(0x00FE));
```