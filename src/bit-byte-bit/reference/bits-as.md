# `bits_as`

---

Module implementing conversions from bits to other types.

## Module

---

> ```rust
> pub fn float32(bits: &Bits) -> f32
> ```
> 
> Converts up to the first 32 bits of a bit string to a 32 bit float
>
> ```rust
> # use bit_byte_bit::{bits_as, Bits};
> let bits = Bits::new([0x10, 0x32, 0x54, 0x76, 0x98, 0xBA, 0xDC, 0xFE]);
> let float = bits_as::float32(&bits);
>
> assert_eq!(float, f32::from_bits(0x76543210));
>
> let bits = Bits::new([0x10, 0x32, 0x54]);
> let float = bits_as::float32(&bits);
>
> assert_eq!(float, f32::from_bits(0x00543210));
> ```

> ```rust
> pub fn float64(bits: &Bits) -> f64
> ```
>
> Converts up to the first 64 bits of a bit string to a 64 bit float
>
> ```rust
> # use bit_byte_bit::{bits_as, Bits};
> let bits = Bits::new([0x10, 0x32, 0x54, 0x76, 0x98, 0xBA, 0xDC, 0xFE]);
> let float = bits_as::float64(&bits);
>
> assert_eq!(float, f64::from_bits(0xFEDCBA9876543210));
>
> let bits = Bits::new([0x10, 0x32, 0x54]);
> let float = bits_as::float64(&bits);
>
> assert_eq!(float, f64::from_bits(0x0000000000543210));
> ```

> ```rust
> pub fn int8(bits: &Bits) -> i8
> ```
>
> Converts up to the first 8 bits of a bit string to 8 bit signed integer.
>
> If the length of the the bit string is less than 8, the result is sign-extended to 8 bits.
>
> ```rust
> # use bit_byte_bit::{bits_as, Bits};
> let bits = Bits::new([0xFE]);
> let ibyte = bits_as::int8(&bits);
>
> assert_eq!(ibyte, 0xFEu8 as i8);
>
> let bits = Bits::from([0x5E]);
> let ibyte = bits_as::int8(&bits);
>
> assert_eq!(ibyte, 0xDEu8 as i8);
> ```

> ```rust
> pub fn int16(bits: &Bits) -> i16
> ```
>
> Converts up the first 16 bits of a bit string to a 16 bit signed integer.
>
> If the length of the the bit string is less than 16, the result is sign-extended to 16 bits.
>
> ```rust
> # use bit_byte_bit::{bits_as, Bits};
> let bits = Bits::new([0x10, 0xFE]);
> let ishort = bits_as::int16(&bits);
>
> assert_eq!(ishort, 0xFE10u16 as i16);
>
> let bits = Bits::from([0x10, 0x5E]);
> let ishort = bits_as::int16(&bits);
>
> assert_eq!(ishort, 0xDE10u16 as i16);
> ```

> ```rust
> pub fn int32(bits: &Bits) -> i32
> ```
>
> Converts up to the first 32 bits of a bit string to a 32 bit signed integer.
>
> If the length of the the bit string is less than 32, the result is sign-extended to 32 bits.
>
> ```rust
> # use bit_byte_bit::{bits_as, Bits};
> let bits = Bits::new([0x10, 0x32, 0x54, 0x76]);
> let int = bits_as::int32(&bits);
>
> assert_eq!(int, 0x76543210);
>
> let bits = Bits::from([0x10, 0x32, 0x54, 0x76]);
> let int = bits_as::int32(&bits);
>
> assert_eq!(int, 0xF6543210u32 as i32);
> ```

> ```rust
> pub fn int64(bits: &Bits) -> i64
> ```
>
> Converts up to the first 64 bits of a bit string to a 64 bit signed integer.
>
> If the length of the the bit string is less than 64, the result is sign-extended to 64 bits.
>
> ```rust
> # use bit_byte_bit::{bits_as, Bits};
> let bits = Bits::new([0x10, 0x32, 0x54, 0x76]);
> let long = bits_as::int64(&bits);
>
> assert_eq!(long, 0x0000000076543210);
>
> let bits = Bits::from([0x10, 0x32, 0x54, 0x76]);
> let long = bits_as::int64(&bits);
>
> assert_eq!(long, 0xFFFFFFFFF6543210u64 as i64);
> ```

> ```rust
> pub fn signed(bits: &Bits) -> isize
> ```
> Converts up to the first 64 bits of a bit string to a signed integer.
>
> If the length of the the bit string is less than the length of `isize`, the result is
> sign-extended to 64 bits.
>
> ```rust
> # use bit_byte_bit::{bits_as, Bits};
> let bits = Bits::new([0x10, 0x32, 0x54, 0x76]);
> let signed = bits_as::signed(&bits);
>
> assert_eq!(signed, 0x0000000076543210);
>
> let bits = Bits::from([0x10, 0x32, 0x54, 0x76]);
> let signed = bits_as::signed(&bits);
>
> assert_eq!(signed, 0xFFFFFFFFF6543210u64 as isize);
> ```

> ```rust
> pub fn uint8(bits: &Bits) -> u8
> ```
>
> Converts up to the first 8 bits of a bit string to a 8 bit unsigned integer.
>
> ```rust
> # use bit_byte_bit::{bits_as, Bits};
> let bits = Bits::new([0xFE]);
> let byte = bits_as::uint8(&bits);
>
> assert_eq!(byte, 0xFE);
>
> let bits = Bits::from([0x5E]);
> let byte = bits_as::uint8(&bits);
>
> assert_eq!(byte, 0x5E);
> ```

> ```rust
> pub fn uint16(bits: &Bits) -> u16
> ```
>
> Converts up the first 16 bits of a bit string to a 16 bit unsigned integer.
>
> ```rust
> # use bit_byte_bit::{bits_as, Bits};
> let bits = Bits::new([0x10, 0xFE]);
> let ushort = bits_as::uint16(&bits);
>
> assert_eq!(ushort, 0xFE10);
>
> let bits = Bits::from([0x10, 0x5E]);
> let ushort = bits_as::uint16(&bits);
>
> assert_eq!(ushort, 0x5E10);
> ```

> ```rust
> pub fn uint32(bits: &Bits) -> u32
> ```
>
> Converts up to the first 32 bits of a bit string to a 32 bit unsigned integer.
>
> ```rust
> # use bit_byte_bit::{bits_as, Bits};
> let bits = Bits::new([0x10, 0x32, 0x54, 0x76]);
> let uint = bits_as::uint32(&bits);
>
> assert_eq!(uint, 0x76543210);
>
> let bits = Bits::from([0x10, 0x32, 0x54, 0x76]);
> let uint = bits_as::uint32(&bits);
>
> assert_eq!(uint, 0x76543210);
> ```

> ```rust
> pub fn uint64(bits: &Bits) -> u64
> ```
>
> Converts up to the first 64 bits of a bit string to a 64 bit unsigned integer.
>
> ```rust
> # use bit_byte_bit::{bits_as, Bits};
> let bits = Bits::new([0x10, 0x32, 0x54, 0x76]);
> let ulong = bits_as::uint64(&bits);
>
> assert_eq!(ulong, 0x0000000076543210);
>
> let bits = Bits::from([0x10, 0x32, 0x54, 0x76]);
> let ulong = bits_as::uint64(&bits);
>
> assert_eq!(ulong, 0x0000000076543210);
> ```

> ```rust
> pub fn unsigned(bits: &Bits) -> usize
> ```
> Converts up to the first 64 bits of a bit string to an unsigned integer.
>
> ```rust
> # use bit_byte_bit::{bits_as, Bits};
> let bits = Bits::new([0x10, 0x32, 0x54, 0x76]);
> let unsigned = bits_as::unsigned(&bits);
>
> assert_eq!(unsigned, 0x0000000076543210);
>
> let bits = Bits::from([0x10, 0x32, 0x54, 0x76]);
> let unsigned = bits_as::unsigned(&bits);
>
> assert_eq!(unsigned, 0x0000000076543210);
> ```

>  ```rust
> pub fn vec_bool(bits: &Bits) -> Vec<bool>
> ```
> Converts a bit string to a vector of booleans
>
> ```rust
> # use bit_byte_bit::{Bits, bits_as};
> let bits = Bits::new([0x10, 0x32]);
> let bools = bits_as::vec_bool(&bits);
>
> assert_eq!(bools.len(), bits.len());
>
> assert_eq!(
>     bools,
>     vec![
>         false, false, false, false, true, false, false, false,
>         false, true, false, false, true, true, false, false
>     ]
> );
> ```

> ```rust
> pub fn vec_f32(bits: &Bits) -> Vec<f32>
> ```
> Converts a bit string to a vector of 32 bit floats
>
> ```rust
> # use bit_byte_bit::{bits_as, Bits};
> let bits = Bits::new([0x10, 0x32, 0x54, 0x76, 0x98, 0xBA, 0xDC, 0xFE]);
> let floats = bits_as::vec_f32(&bits);
>
> assert_eq!(floats.len(), 2);
> assert_eq!(floats, vec![f32::from_bits(0x76543210), f32::from_bits(0xFEDCBA98)]);
>
> let bits = Bits::new([0x10, 0x32, 0x54]);
> let floats = bits_as::vec_f32(&bits);
>
> assert_eq!(floats.len(), 1);
> assert_eq!(floats, vec![f32::from_bits(0x00543210)]);
> ```

> ```rust
> pub fn vec_f64(bits: &Bits) -> Vec<f64>
> ```
> Converts a bit string to a vector of 64 bit floats
>
> ```rust
> # use bit_byte_bit::{bits_as, Bits};
> let bits = Bits::new([0x10, 0x32, 0x54, 0x76, 0x98, 0xBA, 0xDC, 0xFE]);
> let floats = bits_as::vec_f64(&bits);
>
> assert_eq!(floats.len(), 1);
> assert_eq!(floats, vec![f64::from_bits(0xFEDCBA9876543210)]);
>
> let bits = Bits::new([0x10, 0x32, 0x54]);
> let floats = bits_as::vec_f64(&bits);
>
> assert_eq!(floats.len(), 1);
> assert_eq!(floats, vec![f64::from_bits(0x0000000000543210)]);
> ```

> ```rust
> pub fn vec_i8(bits: &Bits) -> Vec<i8>
> ```
>
> Converts a bit string to a vector of 8 bit signed integers.
>
> If the length of the the bit string is not divisible by 8 it is
> sign-extended to the next length that is, then it is converted.
>
> ```rust
> # use bit_byte_bit::{bits_as, Bits};
> let bits = Bits::new([0x10, 0xFE]);
> let ibytes = bits_as::vec_i8(&bits);
>
> assert_eq!(ibytes.len(), 2);
> assert_eq!(ibytes, vec![0x10, 0xFEu8 as i8]);
>
> let bits = Bits::from([0x10, 0x5E]);
> let ibytes = bits_as::vec_i8(&bits);
>
> assert_eq!(ibytes.len(), 2);
> assert_eq!(ibytes, vec![0x10, 0xDEu8 as i8]);
> ```

> ```rust
> pub fn vec_i16(bits: &Bits) -> Vec<i16>
>```
>
> Converts a bit string to a vector of 16 bit signed integers.
>
> If the length of the the bit string is not divisible by 16 it is
> sign-extended to the next length that is, then it is converted.
>
> ```rust
> # use bit_byte_bit::{bits_as, Bits};
> let bits = Bits::new([0x10, 0xFE]);
> let ishorts = bits_as::vec_i16(&bits);
>
> assert_eq!(ishorts.len(), 1);
> assert_eq!(ishorts, vec![0xFE10u16 as i16]);
>
> let bits = Bits::from([0x10, 0x5E]);
> let ishorts = bits_as::vec_i16(&bits);
>
> assert_eq!(ishorts.len(), 1);
> assert_eq!(ishorts, vec![0xDE10u16 as i16]);
> ```

> ```rust
> pub fn vec_i32(bits: &Bits) -> Vec<i32>
> ```
>
> Converts a bit string to a vector of 32 bit signed integers.
>
> If the length of the the bit string is not divisible by 32 it is
> sign-extended to the next length that is, then it is converted.
>
> ```rust
> # use bit_byte_bit::{bits_as, Bits};
> let bits = Bits::new([0x10, 0x32, 0x54, 0x76]);
> let ints = bits_as::vec_i32(&bits);
>
> assert_eq!(ints.len(), 1);
> assert_eq!(ints, vec![0x76543210]);
>
> let bits = Bits::from([0x10, 0x32, 0x54, 0x76]);
> let ints = bits_as::vec_i32(&bits);
>
> assert_eq!(ints.len(), 1);
> assert_eq!(ints, vec![0xF6543210u32 as i32]);
> ```

> ```rust
> pub fn vec_i64(bits: &Bits) -> Vec<i64>
> ```
>
> Converts a bit string to a vector of 64 bit signed integers.
>
> If the length of the the bit string is not divisible by 64 it is
> sign-extended to the next length that is, then it is converted.
>
> ```rust
> # use bit_byte_bit::{bits_as, Bits};
> let bits = Bits::new([0x10, 0x32, 0x54, 0x76]);
> let longs = bits_as::vec_i64(&bits);
>
> assert_eq!(longs.len(), 1);
> assert_eq!(longs, vec![0x0000000076543210]);
>
> let bits = Bits::from([0x10, 0x32, 0x54, 0x76]);
> let longs = bits_as::vec_i64(&bits);
>
> assert_eq!(longs.len(), 1);
> assert_eq!(longs, vec![0xFFFFFFFFF6543210u64 as i64]);
> ```

> ```rust
> pub fn vec_isize(bits: &Bits) -> Vec<isize>
> ```
> Converts a bit string to a vector of signed integers.
> 
> If the length of the the bit string is not divisible by the length of `isize`, it is
> sign-extended to the next length that is, then it is converted.
> 
> ```rust
> # use bit_byte_bit::{bits_as, Bits};
> let bits = Bits::new([0x10, 0x32, 0x54, 0x76]);
> let signed_ints = bits_as::vec_isize(&bits);
> 
> assert_eq!(signed_ints.len(), 1);
> assert_eq!(signed_ints, vec![0x0000000076543210]);
> 
> let bits = Bits::from([0x10, 0x32, 0x54, 0x76]);
> let signed_ints = bits_as::vec_i64(&bits);
> 
> assert_eq!(signed_ints.len(), 1);
> assert_eq!(signed_ints, vec![0xFFFFFFFFF6543210u64 as i64]);
> ```
    

> ```rust
> pub fn vec_u8(bits: &Bits) -> Vec<u8>
> ```
>
> Converts a bit string to a vector of 8 bit unsigned integers.
>
> ```rust
> # use bit_byte_bit::{bits_as, Bits};
> let bits = Bits::new([0x10, 0xFE]);
> let bytes = bits_as::vec_u8(&bits);
>
> assert_eq!(bytes.len(), 2);
> assert_eq!(bytes, vec![0x10, 0xFE]);
>
> let bits = Bits::from([0x10, 0x5E]);
> let bytes = bits_as::vec_u8(&bits);
>
> assert_eq!(bytes.len(), 2);
> assert_eq!(bytes, vec![0x10, 0x5E]);
> ```

> ```rust
> pub fn vec_u16(bits: &Bits) -> Vec<u16>
> ```
>
> Converts a bit string to a vector of 16 bit unsigned integers.
>
> ```rust
> # use bit_byte_bit::{bits_as, Bits};
> let bits = Bits::new([0x10, 0xFE]);
> let shorts = bits_as::vec_u16(&bits);
>
> assert_eq!(shorts.len(), 1);
> assert_eq!(shorts, vec![0xFE10]);
>
> let bits = Bits::from([0x10, 0x5E]);
> let shorts = bits_as::vec_u16(&bits);
>
> assert_eq!(shorts.len(), 1);
> assert_eq!(shorts, vec![0x5E10])
> ```

> ```rust
> pub fn vec_u32(bits: &Bits) -> Vec<u32>
>```
> Converts a bit string to a vector of 32 bit unsigned integers.
>
> ```rust
> # use bit_byte_bit::{bits_as, Bits};
> let bits = Bits::new([0x10, 0x32, 0x54, 0x76]);
> let uints = bits_as::vec_u32(&bits);
>
> assert_eq!(uints.len(), 1);
> assert_eq!(uints, vec![0x76543210]);
>
> let bits = Bits::from([0x10, 0x32, 0x54, 0x76]);
> let uints = bits_as::vec_u32(&bits);
>
> assert_eq!(uints.len(), 1);
> assert_eq!(uints, vec![0x76543210]);
> ```

> ```rust
> pub fn vec_u64(bits: &Bits) -> Vec<u64>
> ```
>
> Converts a bit string to a vector of 64 bit unsigned integers.
>
> If the length of the the bit string is not divisible by 64 it is
> sign-extended to the next length that is, then it is converted.
>
> ```rust
> # use bit_byte_bit::{bits_as, Bits};
> let bits = Bits::new([0x10, 0x32, 0x54, 0x76]);
> let ulongs = bits_as::vec_u64(&bits);
>
> assert_eq!(ulongs.len(), 1);
> assert_eq!(ulongs, vec![0x0000000076543210]);
>
> let bits = Bits::from([0x10, 0x32, 0x54, 0x76]);
> let ulongs = bits_as::vec_u64(&bits);
>
> assert_eq!(ulongs.len(), 1);
> assert_eq!(ulongs, vec![0x0000000076543210]);
> ```

> ```rust
> pub fn vec_usize(bits: &Bits) -> Vec<usize>
> ```
> 
> Converts a bit string to a vector of unsigned integers.
>
> ```rust
> # use bit_byte_bit::{bits_as, Bits};
> let bits = Bits::new([0x10, 0x32, 0x54, 0x76]);
> let unsigned_ints = bits_as::vec_usize(&bits);
>
> assert_eq!(unsigned_ints.len(), 1);
> assert_eq!(unsigned_ints, vec![0x0000000076543210]);
>
> let bits = Bits::from([0x10, 0x32, 0x54, 0x76]);
> let unsigned_ints = bits_as::vec_usize(&bits);
>
> assert_eq!(unsigned_ints.len(), 1);
> assert_eq!(unsigned_ints, vec![0x0000000076543210]);
> ```