# `Scheme`

---

```rust
pub struct Scheme(...);
```

Defines a pattern giving meaning to different regions of a bit string.

# Implementation

---

> ```rust
> pub fn new<I: IntoIterator<Item = Field>>(pattern: I) -> Self
> ```
> 
> Creates a new scheme from the sequence of fields.
> 
> ```rust
> let unsigned_3 = Field::unsigned(3);
> 
> let scheme = Scheme::new([
>     Field::signed(5),
>     Field::BIT,
>     unsigned_3,
>     unsigned_3,
>     Field::UNSIGNED_4,
>     Field::aligned(23, 1, true),
>     Field::unsigned(32),
>     Field::signed(32),
>     Field::bytes(4, false),
>     Field::aligned(6, 8, true)
> ]);
> 
> let time_since_epoch = Field::UNSIGNED_64;
> let identifier = Field::UNSIGNED_8;
> let datatype = Field::UNSIGNED_4;
> let data = Field::BYTES;
> 
> let scheme2 = Scheme::new([time_since_epoch, identifier, datatype, data]);
> ```

> ```rust
> pub fn len(&self) -> isize
> ```
>
> Number of bits extracted
> 
> If any field in the scheme has a negative length, this method returns -1, indicating the scheme extracts a variable
> number of bits.
> 
> ```rust
> let unsigned_3 = Field::unsigned(3);
> 
> let scheme = Scheme::new([
>     Field::signed(5), Field::BIT, unsigned_3, unsigned_3, Field::UNSIGNED_4
> ]);
> 
> assert_eq!(scheme.len(), 16);
> 
> let scheme2 = Scheme::new([
>     Field::aligned(23, 1, true),
>     Field::unsigned(0),
>     Field::unsigned(32),
>     Field::bytes(4, false),
>     Field::aligned(0, 8, false),
>     Field::aligned(7, 8, true)
> ]);
> 
> let scheme3 = Scheme::new([
>     Field::aligned(23, 1, true),
>     Field::unsigned(0),
>     Field::unsigned(32),
>     Field::signed(-1),
>     Field::bytes(4, false),
>     Field::aligned(0, 8, false),
>     Field::aligned(7, 8, true)
> ]);
> 
> assert_eq!(scheme3.len(), -1);

> ```rust
> pub fn split_bits(&self, bits: &Bits) -> Vec<Bits>
> ```
> 
> Extracts the data associated with the fields of this scheme
> 
> ```rust
> 
> let unsigned_3 = Field::unsigned(3);
> 
> let scheme = Scheme::new([
>     Field::signed(5), Field::BIT, unsigned_3, unsigned_3, Field::UNSIGNED_4
> ]);
> 
> let bits = Bits::new([0xBA, 0x1C]);
> let parts = scheme.split_bits(&bits);
> 
> assert_eq!(bits_as::int8(&parts[0]), -6);
> assert_eq!(bits_as::uint8(&parts[1]), 1);
> assert_eq!(bits_as::uint8(&parts[2]), 2);
> assert_eq!(bits_as::uint8(&parts[3]), 6);
> assert_eq!(bits_as::uint8(&parts[4]), 1);
> 
> let bits2 = Bits::new([0xBA]);
> let parts2 = scheme.split_bits(&bits2);
> 
> assert_eq!(bits_as::int8(&parts2[0]), -6);
> assert_eq!(bits_as::uint8(&parts2[1]), 1);
> assert_eq!(bits_as::uint8(&parts2[2]), 2);
> assert_eq!(bits_as::uint8(&parts2[3]), 0);
> assert_eq!(bits_as::uint8(&parts2[4]), 0);
> 
> let scheme2 = Scheme::new([
>     Field::aligned(23, -1, true),
>     Field::aligned(0, -1, false),
>     Field::bytes(-1, false),
>     Field::signed(-1),
>     Field::unsigned(-1),
>     Field::unsigned(0),
>     Field::unsigned(32),
>     Field::bytes(4, false),
>     Field::aligned(0, 8, false),
>     Field::aligned(7, 8, true),
>     Field::signed(-1),
>     Field::unsigned(-1)
> ]);
> 
> let bytes = [0xBA, 0xDC, 0xFE, 0x10, 0x32];
> let bits3 = Bits::from(bytes.as_slice()); // 38-bits
> let parts = scheme2.split_bits(&bits3);
> 
> assert_eq!(bits_as::int32(&parts[0]), 0xFFFEDCBAu32 as i32);
> assert_eq!(parts[1], Bits::empty());
> assert_eq!(bits_as::vec_u8(&parts[2]), vec![0x21]);
> assert_eq!(bits_as::vec_i32(&parts[3]), vec![-28]);
> assert_eq!(parts[4], Bits::empty());
> assert_eq!(parts[5], Bits::empty());
> assert_eq!(parts[6], Bits::zeros(32));
> assert_eq!(parts[7], Bits::zeros(32));
> assert_eq!(parts[8], Bits::empty());
> assert_eq!(parts[9], Bits::zeros(56));
> assert_eq!(parts[10], Bits::empty());
> assert_eq!(parts[11], Bits::empty());
> ```

> ```rust
> pub fn split_bits_at(&self, index: usize, bits: &Bits) -> Vec<Bits>
> ```
> 
> Extracts the data associated with the fields of this scheme.
> 
> ```rust
> 
> let unsigned_3 = Field::unsigned(3);
> 
> let scheme = Scheme::new([
>     Field::signed(5), Field::BIT, unsigned_3, unsigned_3, Field::UNSIGNED_4
> ]);
> 
> let bits = Bits::new([0xBA, 0x1C]);
> let parts = scheme.split_bits_at(0, &bits);
> 
> assert_eq!(bits_as::int8(&parts[0]), -6);
> assert_eq!(bits_as::uint8(&parts[1]), 1);
> assert_eq!(bits_as::uint8(&parts[2]), 2);
> assert_eq!(bits_as::uint8(&parts[3]), 6);
> assert_eq!(bits_as::uint8(&parts[4]), 1);
> 
> let parts2 = scheme.split_bits_at(8, &bits);
> 
> assert_eq!(bits_as::int8(&parts2[0]), -4);
> assert_eq!(bits_as::uint8(&parts2[1]), 0);
> assert_eq!(bits_as::uint8(&parts2[2]), 0);
> assert_eq!(bits_as::uint8(&parts2[3]), 0);
> assert_eq!(bits_as::uint8(&parts2[4]), 0);
> 
> let scheme2 = Scheme::new([
>     Field::aligned(23, -1, true),
>     Field::aligned(0, -1, false),
>     Field::bytes(-1, false),
>     Field::signed(-1),
>     Field::unsigned(-1),
>     Field::unsigned(0),
>     Field::unsigned(32),
>     Field::bytes(4, false),
>     Field::aligned(0, 8, false),
>     Field::aligned(7, 8, true),
>     Field::signed(-1),
>     Field::unsigned(-1)
> ]);
> 
> let bytes = [0xBA, 0xDC, 0xFE, 0x10, 0x32];
> let bits3 = Bits::from(bytes.as_slice()); // 38-bits
> let parts = scheme2.split_bits_at(4, &bits3);
> 
> assert_eq!(bits_as::int32(&parts[0]), 0x0FEDCB);
> assert_eq!(parts[1], Bits::empty());
> assert_eq!(bits_as::vec_u8(&parts[2]), vec![0x42]);
> assert_eq!(bits_as::vec_i32(&parts[3]), vec![-2]);
> assert_eq!(parts[4], Bits::empty());
> assert_eq!(parts[5], Bits::empty());
> assert_eq!(parts[6], Bits::zeros(32));
> assert_eq!(parts[7], Bits::zeros(32));
> assert_eq!(parts[8], Bits::empty());
> assert_eq!(parts[9], Bits::zeros(56));
> assert_eq!(parts[10], Bits::empty());
> assert_eq!(parts[11], Bits::empty());f
> ```

> ```rust
> pub fn split_bytes<I: IntoIterator<Item = u8>>(&self, bytes: I) -> Vec<Bits>
> ```
>
> Extracts the data associated with the fields of this scheme
> 
> ```rust
> 
> let unsigned_3 = Field::unsigned(3);
> 
> let scheme = Scheme::new([
>     Field::signed(5), Field::BIT, unsigned_3, unsigned_3, Field::UNSIGNED_4
> ]);
> 
> let parts = scheme.split_bytes([0xBA, 0x1C]);
> 
> assert_eq!(bits_as::int8(&parts[0]), -6);
> assert_eq!(bits_as::uint8(&parts[1]), 1);
> assert_eq!(bits_as::uint8(&parts[2]), 2);
> assert_eq!(bits_as::uint8(&parts[3]), 6);
> assert_eq!(bits_as::uint8(&parts[4]), 1);
> 
> let parts2 = scheme.split_bytes([0xBA]);
> 
> assert_eq!(bits_as::int8(&parts2[0]), -6);
> assert_eq!(bits_as::uint8(&parts2[1]), 1);
> assert_eq!(bits_as::uint8(&parts2[2]), 2);
> assert_eq!(bits_as::uint8(&parts2[3]), 0);
> assert_eq!(bits_as::uint8(&parts2[4]), 0);
> 
> let scheme2 = Scheme::new([
>     Field::aligned(23, -1, true),
>     Field::aligned(0, -1, false),
>     Field::bytes(-1, false),
>     Field::signed(-1),
>     Field::unsigned(-1),
>     Field::unsigned(0),
>     Field::unsigned(32),
>     Field::bytes(4, false),
>     Field::aligned(0, 8, false),
>     Field::aligned(7, 8, true),
>     Field::signed(-1),
>     Field::unsigned(-1)
> ]);
> 
> let parts = scheme2.split_bytes(vec![0xBA, 0xDC, 0xFE, 0x10, 0x32]);
> 
> assert_eq!(bits_as::int32(&parts[0]), 0xFFFEDCBAu32 as i32);
> assert_eq!(parts[1], Bits::empty());
> assert_eq!(bits_as::vec_u8(&parts[2]), vec![0x21, 0x64]);
> assert_eq!(parts[3], Bits::zeros(1));
> assert_eq!(bits_as::int64(&parts[4]), 0);
> assert_eq!(parts[5], Bits::empty());
> assert_eq!(parts[6], Bits::zeros(32));
> assert_eq!(parts[7], Bits::zeros(32));
> assert_eq!(parts[8], Bits::empty());
> assert_eq!(parts[9], Bits::zeros(56));
> assert_eq!(parts[10], Bits::empty());
> assert_eq!(parts[11], Bits::empty());
> ```

> ```rust
> pub fn split_bytes_at<I: IntoIterator<Item = u8>>(
>     &self,
>     index: usize,
>     bytes: I,
> ) -> Vec<Bits>
> ```
> 
> Extracts the data associated with the fields of this scheme.
> 
> ```rust
> 
> let unsigned_3 = Field::unsigned(3);
> 
> let scheme = Scheme::new([
>     Field::signed(5), Field::BIT, unsigned_3, unsigned_3, Field::UNSIGNED_4
> ]);
> 
> let parts = scheme.split_bytes_at(0, [0xBA, 0x1C]);
> 
> assert_eq!(bits_as::int8(&parts[0]), -6);
> assert_eq!(bits_as::uint8(&parts[1]), 1);
> assert_eq!(bits_as::uint8(&parts[2]), 2);
> assert_eq!(bits_as::uint8(&parts[3]), 6);
> assert_eq!(bits_as::uint8(&parts[4]), 1);
> 
> let parts2 = scheme.split_bytes_at(8, [0xBA, 0x1C]);
> 
> assert_eq!(bits_as::int8(&parts2[0]), -4);
> assert_eq!(bits_as::uint8(&parts2[1]), 0);
> assert_eq!(bits_as::uint8(&parts2[2]), 0);
> assert_eq!(bits_as::uint8(&parts2[3]), 0);
> assert_eq!(bits_as::uint8(&parts2[4]), 0);
> 
> let scheme2 = Scheme::new([
>     Field::aligned(23, -1, true),
>     Field::aligned(0, -1, false),
>     Field::bytes(-1, false),
>     Field::signed(-1),
>     Field::unsigned(-1),
>     Field::unsigned(0),
>     Field::unsigned(32),
>     Field::bytes(4, false),
>     Field::aligned(0, 8, false),
>     Field::aligned(7, 8, true),
>     Field::signed(-1),
>     Field::unsigned(-1)
> ]);
> 
> let parts = scheme2.split_bytes_at(4, [0xBA, 0xDC, 0xFE, 0x10, 0x32]);
> 
> assert_eq!(bits_as::int32(&parts[0]), 0x0FEDCB);
> assert_eq!(parts[1], Bits::empty());
> assert_eq!(bits_as::vec_u8(&parts[2]), vec![0x42]);
> assert_eq!(bits_as::vec_i32(&parts[3]), vec![6]);
> assert_eq!(parts[4], Bits::empty());
> assert_eq!(parts[5], Bits::empty());
> assert_eq!(parts[6], Bits::zeros(32));
> assert_eq!(parts[7], Bits::zeros(32));
> assert_eq!(parts[8], Bits::empty());
> assert_eq!(parts[9], Bits::zeros(56));
> assert_eq!(parts[10], Bits::empty());
> assert_eq!(parts[11], Bits::empty());
> ```