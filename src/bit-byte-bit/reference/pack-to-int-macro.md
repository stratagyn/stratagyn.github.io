# `pack-to-int!`

---

```rust
macro_rules! pack_to_int {
    ($int:ty; $bytes:expr; $length_in_bits:expr) => { ... };
    ($int:ty; $b0:expr, $b1:expr) => { ... };
    ($int:ty; $b0:expr, $b1:expr, $b2:expr) => { ... };
    ($int:ty; $b0:expr, $b1:expr, $b2:expr, $b3:expr) => { ... };
    ($int:ty; $b0:expr, $b1:expr, $b2:expr, $b3:expr, $b4:expr) => { ... };
    ($int:ty; $b0:expr, $b1:expr, $b2:expr, $b3:expr, $b4:expr, $b5:expr) => { ... };
    ($int:ty; $b0:expr, $b1:expr, $b2:expr, $b3:expr, $b4:expr, $b5:expr, $b6:expr) => { ... };
    ($int:ty; $b0:expr, $b1:expr, $b2:expr, $b3:expr, $b4:expr, $b5:expr, $b6:expr, $b7:expr) => { ... };
    ($bytes:expr; $length_in_bits:expr) => { ... };
    ($b0:expr, $b1:expr) => { ... };
    ($b0:expr, $b1:expr, $b2:expr) => { ... };
    ($b0:expr, $b1:expr, $b2:expr, $b3:expr) => { ... };
    ($b0:expr, $b1:expr, $b2:expr, $b3:expr, $b4:expr) => { ... };
    ($b0:expr, $b1:expr, $b2:expr, $b3:expr, $b4:expr, $b5:expr) => { ... };
    ($b0:expr, $b1:expr, $b2:expr, $b3:expr, $b4:expr, $b5:expr, $b6:expr) => { ... };
    ($b0:expr, $b1:expr, $b2:expr, $b3:expr, $b4:expr, $b5:expr, $b6:expr, $b7:expr) => { ... };
}
```

> Macro that packs up to 64 bits as a given integral type.
>
> `$bytes` is a byte array large enough to pack `min($length_in_bits, 64)` bits. `$int` is an 
> integral type large enough to hold a value with `min($length_in_bits, 64)` bits.
>
> In some cases, it could be more efficient to use one of the unrolled forms, over the general one.
> This is because the general case first tries to figure out which version of the unrolled code to use.
>
> ```rust
> # use bit_byte_bit::{pack_to_int};
> let bytes = [0x01u8, 0x23, 0x45, 0x67, 0x89, 0xAB, 0xCD, 0xEF];
> let bytes_u64 = [0x01u64, 0x23, 0x45, 0x67, 0x89, 0xAB, 0xCD, 0xEF];
>
> let pack_u64_general = pack_to_int!(u64; bytes; 48);
> 
> let pack_u64_general_u64 = pack_to_int!(bytes_u64; 48);
>
> let pack_u64_unrolled = pack_to_int!(u64;
>     bytes[0], bytes[1], bytes[2], bytes[3], bytes[4], bytes[5]
> );
>
> let pack_u64_unrolled_u64 = pack_to_int!(
>     bytes_u64[0], bytes_u64[1], bytes_u64[2], 
>     bytes_u64[3], bytes_u64[4], bytes_u64[5]
> );
>
> let pack_u64_unrolled_bytes = pack_to_int!(u64;
>     0x01, 0x23, 0x45, 0x67, 0x89, 0xAB
> );
> 
> let pack_u64_unrolled_u64_bytes = pack_to_int!(
>     0x01u64, 0x23, 0x45, 0x67, 0x89, 0xAB
> );
>
> assert_eq!(pack_u64_general, 0xAB8967452301);
> assert_eq!(pack_u64_general, pack_u64_general_u64);
> assert_eq!(pack_u64_general, pack_u64_unrolled);
> assert_eq!(pack_u64_general, pack_u64_unrolled_u64);
> assert_eq!(pack_u64_general, pack_u64_unrolled_bytes);
> assert_eq!(pack_u64_general, pack_u64_unrolled_u64_bytes);
> ```
>
> Note in the case of `bytes_u64` and `pack_u64_unrolled_u64_bytes`, while the type is defined by the 
> values, each is still in the range of [0-255]. If this were not the case, the resulting packed value 
> may not be what's expected since ones could appear in the upper bits where they otherwise would not have.
> However, this can be exploited to "prepend" a byte to another integer.
>
> ```rust
> # use bit_byte_bit::{pack_to_int};
> let pack_u64 = pack_to_int!(0x2301u64, 0x45);
> 
> assert_equal!(pack_u64, 0x6701);
>
> let prepend_byte = pack_to_int!(0x01u32, 0x4523);
> 
> assert_equal(prepend_byte, 0x452301);
> ```
>
> <span style="color: red"><span style="color: red">ⓘ</span></span>
> ```rust
> # use bit_byte_bit::{pack_to_int};
> let bytes = vec![0x01, 0x23];
>
> // panics since `bytes.len() == 2` and 8 bytes are expected
> let pack_u16 = pack_to_int!(u64; bytes; 64);
> ```
>
> <span style="color: red"><span style="color: red">ⓘ</span></span>
> ```rust
> # use bit_byte_bit::{pack_to_int};
> let bytes = [0x01, 0x23, 0x45, 0x67, 0x89, 0xAB, 0xCD, 0xEF];
>
> // panics because of an eventual left shift with overflow due to treating a
> // u16 value as if it had 64 bits.
> let pack_u16 = pack_to_int!(u16; bytes; 64);
> ```
