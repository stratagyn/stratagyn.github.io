# Bitwise Operations

---

Bit strings support 
* complement
* and
* or
* xor
* left and right shifting
* left and right rotation
* reversal
* counting ones or zeros
* counting leading ones or zeros
* counting trailing ones or zeros

Each of `complement`, `and`, `or`, and `xor` can be done in-place by calling the `*_mut` version of the method.
Reversal, shifting, and rotation can be done in-place using the verb form of the method, as opposed to the 
adjective form that is, `reverse` versus `reversed`, or `rotate_left` versus `rotated_left`. 

Also note that the method for counting ones is called `hamming_weight`.

> <span style="color: #cf5dfcff">ⓘ</span>
> For methods ending in either `_left` or `_right`, bit 0 is considered the most right bit, while bit *n-1* is 
> the most left.

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