# Conversion

[Bit strings](/bit-byte-bit/reference/bits.md) can be converted using one of the [`From<Bits>`](/bit-byte-bit/reference/bits.md#frombits)
implementations or the [`bits_as`](/bit-byte-bit/reference/bits-as.md) module. This module implements the trait methods as non-consuming methods.

### Example

---

```rust
# use bit_byte_bit::{Bits, bits_as};
let bits = Bits::new([0x10, 0x32, 0x54, 0x76, 0x89, 0xBA, 0xDC, 0xFE]);
let signed_ints_1 = bits_as::vec_i32(&bits);
let signed_ints_2 = Vec::<i32>::from(bits);   // `bits` is moved.

assert_eq!(signed_ints_1, signed_ints_2);

let bits = Bits::new([0x10, 0x32, 0x54, 0x76, 0x89, 0xBA, 0xDC, 0xFE]);
let signed_int_1 = bits_as::int64(&bits);
let float64 = bits_as::float64(&bits);
let signed_int_2 = i64::from(bits);   // `bits` is moved.

assert_eq!(signed_int_1, signed_int_2);
assert_eq!(float64, f64::from_bits(0xFEDCBA9876543210));
```

