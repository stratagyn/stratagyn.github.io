# `Bits`

---

> ```rust
> pub struct Bits { ... }
> ```

## `impl Bits`

---

> ```rust
> pub fn new<I: IntoIterator<Item = u8>>(bits: I) -> Self
> ```
> 
> Creates a bit string from a sequence of bytes.
> 
> To ignore leading zeros use `Bits::from` or `Bits::from_iter`.
>
> ```rust
> let mut x = Bits::new([0x0A, 0x0B, 0x0C, 0x00]);
> 
> assert_eq!(x.len(), 32);
> ```

> ```rust
> pub fn aligned<I: IntoIterator<Item = u8>>(units: usize, bits: I) -> Self
> ```
> 
>Creates a bit string with an aligned length.
>
>``` rust
>let mut x = Bits::aligned(17, [0x0A, 0x0B, 0x0C]);
>
>assert_eq!(x.len(), 34);
>assert_eq!(x, Bits::slice(&[0x0A, 0x0B, 0x0C, 0x00, 0x00], 34));
> ```

> ```rust
> pub fn empty() -> Self
> ```
> 
> Creates an empty bit string.
> 
> ```rust
> let mut x = Bits::empty();
> 
> assert_eq!(x.len(), 0);
> ```

> ```rust
> pub fn ones(length: usize) -> Self
> ```
> 
> Creates a bit string of ones.
> 
> ```rust
> let mut x = Bits::ones(4);
> 
> assert_eq!(x.len(), 4);
> assert_eq!(x, Bits::from([0x0F]));
> ```

> ```rust
> pub fn packed<I: IntoIterator<Item = u8>>(bytes: I) -> Self
> ```
> 
> Creates a bit string by concatenating a slice of bytes removing leading zeros.
> 
> ```rust
> let x1 = Bits::packed([0x00, 0x00, 0x00]);
> 
> assert_eq!(x1, Bits::empty());
> 
> let x2 = Bits::packed([0x0A, 0x0B, 0x0C]);
> 
> assert_eq!(x2, Bits::from([0xBA, 0x0C]));
> assert_eq!(x2.len(), 12);
> ```

> ```rust
> pub fn slice(src: &[u8], length: usize) -> Self
> ```
> 
> Creates a bit string by copying a given number of bits from a slice of bytes.
> 
> When the length is greater than the available number of bits in the source, the result is padded with zeros.
> 
> ```rust
> let x1 = Bits::slice(&[], 17);
> 
> assert_eq!(x1, Bits::zeros(17));
> 
> let x2 = Bits::slice(&[0x0A, 0x0B, 0x0C], 0);
> 
> assert_eq!(x2, Bits::empty());
> 
> let x3 = Bits::slice(&[0x0A, 0x0B, 0x0C], 19);
> 
> assert_eq!(x3, Bits::from([0x0A, 0x0B, 0x04]));
> 
> let x4 = Bits::slice(&[0x00, 0x00, 0x00], 19);
> 
> assert_eq!(x4, Bits::zeros(19));
> ```

> ```rust
> pub fn take(src: &[u8], start: usize, length: usize) -> Self
> ```
> 
> Creates a bit string by copying a given range of bits from a slice of bytes.
> 
> When the length is greater than the available number of bits in the source, the result is padded with zeros.
> 
> ```rust
> let x1 = Bits::take(&[], 1, 17);
> 
> assert_eq!(x1, Bits::zeros(17));
> 
> let x2 = Bits::take(&[0x0A, 0x0B, 0x0C], 1, 0);
> 
> assert_eq!(x2, Bits::empty());
> 
> let x3 = Bits::take(&[0x0A, 0x0B, 0x0C], 25, 17);
> 
> assert_eq!(x3, Bits::zeros(17));
> 
> let x4 = Bits::take(&[0x0A, 0x0B, 0x0C], 1, 17);
> 
> assert_eq!(x4.bytes().to_vec(), vec![0x85, 0x05, 0x00]);
> 
> let x5 = Bits::take(&[0x0A, 0x0B, 0x0C], 1, 16);
> 
> assert_eq!(x5.bytes().to_vec(), vec![0x85, 0x05]);
> 
> let x6 = Bits::take(&[0x00, 0x00, 0x00], 1, 17);
> 
> assert_eq!(x6, Bits::zeros(17));
> ```

> ```rust
> pub fn zeros(length: usize) -> Self
> ```
> 
> Creates a bit string of zeros.
> 
> ```rust
> let mut x = Bits::zeros(4);
> 
> assert_eq!(x.len(), 4);
> assert_eq!(x, Bits::from([false, false, false, false]));
> ```
> 
> ```rust
> pub fn align(&mut self, unit: usize)
> Pads a bit string until the length is a multiple of the given unit.
> 
> ```rust
> let mut x = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x.align(16);
> 
> assert_eq!(x, Bits::new([0x0A, 0x0B, 0x0C, 0x00]));
> assert_eq!(x.len(), 32);
> ```

> ```rust
> pub fn all(&self) -> bool
> ```
> 
> Whether all bits are one.
> 
> ```rust
> let x1 = Bits::empty();
> 
> assert!(x1.all());
> 
> let x2 = Bits::from([0x0F]);
> 
> assert!(x2.all());
> 
> let x3 = Bits::new([0x0F]);
> 
> assert!(!x3.all());
> ```

> ```rust
> pub fn and(&self, rhs: &Bits) -> Bits
> ```
> 
> Bitwise and of two bit strings.
> 
> ```rust
> let x1 = Bits::from([0x20, 0x30, 0x40]);
> let y1 = Bits::from([0xA0, 0xB0, 0xC0]);
> 
> assert_eq!(x1.and(&y1), Bits::new([0x20, 0x30, 0x40]));
> 
> let x2 = Bits::from([0x20, 0x30, 0x40]);
> let y2 = Bits::from([0x0A, 0xB0, 0xC0]);
> 
> assert_eq!(x2.len(), 23);
> assert_eq!(y2.len(), 24);
> 
> let z = x2.and(&y2);
> 
> assert_eq!(z.len(), 24);
> ```

> ```rust
> pub fn and_mut(&mut self, rhs: &Bits)
> ```
>
> Bitwise and of two bit strings.
> 
> ```rust
> let mut x1 = Bits::from([0x20, 0x30, 0x40]);
> let y1 = Bits::from([0xA0, 0xB0, 0xC0]);
> 
> x1.and_mut(&y1);
> 
> assert_eq!(x1, Bits::new([0x20, 0x30, 0x40]));
> 
> let mut x2 = Bits::from([0x20, 0x30, 0x40]);
> let y2 = Bits::from([0x0A, 0xB0, 0xC0]);
> 
> assert_eq!(x2.len(), 23);
> assert_eq!(y2.len(), 24);
> 
> x2.and_mut(&y2);
> 
> assert_eq!(x2.len(), 24);
> ```

> ```rust
> pub fn any(&self) -> bool
> ```
>
> Whether at least one bit is one.
> 
> ```rust
> let x1 = Bits::empty();
> 
> assert!(!x1.any());
> 
> let x2 = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> assert!(x2.any());
> 
> let x3 = Bits::zeros(20);
> 
> assert!(!x3.any());
> ```

> ```rust
> pub fn byte(&self, i: usize) -> u8
> ```
>
> State of a byte.
> 
> ```rust
> let mut x = Bits::from([0x0A, 0x0B]);
> 
> assert_eq!(x.byte(0), 0x0A);
> assert_eq!(x.byte(1), 0x0B);
> ```
>
> <span style="color: red"><span style="color: red">ⓘ</span></span>
> ```rust
> let mut x = Bits::from([0x0A, 0x0B]);
> 
> assert_eq!(x.byte(2), 0x0C);
> ```

> ```rust
> pub fn bytes(&self) -> &[u8]
> ```
>
> Underlying bytes
> 
> ```rust
> let x = Bits::new([0xAB, 0xCD, 0xEF]);
> let y = x.bytes().iter().cloned().collect::<Vec<u8>>();
> 
> assert_eq!(y, vec![0xAB, 0xCD, 0xEF]);
> ```

> ```rust
> pub fn complement(&self) -> Bits
> ```
>
> Flips every bit.
> 
> ```rust
> let x = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> assert_eq!(x.complement(), Bits::slice(&[0xF5, 0xF4, 0x03], 20));
> ```

> ```rust
> pub fn complement_mut(&mut self)
> ```
>
> Flips every bit.
> 
> ```rust
> let mut x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x1.complement_mut();
> 
> assert_eq!(x1, Bits::slice(&[0xF5, 0xF4, 0x03], 20));
> ```

> ```rust
> pub fn consume_left(&mut self, count: usize)
> ```
>
> Shifts out upper bits.
> 
> ```rust
> let mut x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x1.consume_left(4);
> assert_eq!(x1.len(), 16);
> assert_eq!(x1, Bits::new([0x0A, 0x0B]));
> 
> let mut x2 = Bits::new([0x0A, 0x0B, 0x0C]);
> 
> x2.consume_left(4);
> assert_eq!(x2.len(), 20);
> assert_eq!(x2, Bits::from([0x0A, 0x0B, 0x0C]));
> ```

> ```rust
> pub fn consume_right(&mut self, count: usize)
> ```
>
> Shifts out lower bits.
> 
> ```rust
> let mut x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x1.consume_right(4);
> 
> assert_eq!(x1, Bits::from([0xB0, 0xC0]));
> assert_eq!(x1.len(), 16);
> 
> let mut x2 = Bits::new([0x0A, 0x0B, 0x0C]);
> 
> x2.consume_right(4);
> 
> assert_eq!(x2, Bits::slice(&[0xB0, 0xC0, 0x00], 20));
> assert_eq!(x2.len(), 20);
> ```

> ```rust
> pub fn count_zeros(&self) -> usize
> ```
>
> The number of zeros.
> 
> ```rust
> let mut x = Bits::from([15, 15, 15]);
> 
> assert_eq!(x.count_zeros(), 8);
> 
> x = Bits::new([15, 15, 15]);
> 
> assert_eq!(x.count_zeros(), 12);
> ```

> ```rust
> pub fn extend_left(&mut self, bytes: &[u8])
> ```
>
> Adds upper bit padding to a bit string.
> 
> ```rust
> let mut x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x1.extend_left(&[0x0D, 0x0E, 0x0F]);
> 
> assert_eq!(x1.len(), 44);
> assert_eq!(x1, Bits::slice(&[0x0A, 0x0B, 0xDC, 0xE0, 0xF0, 0x00], 44));
> 
> let mut x2 = Bits::new([0x0A, 0x0B, 0x0C]);
> 
> x2.extend_left(&[0x0D, 0x0E, 0x0F]);
> 
> assert_eq!(x2.len(), 48);
> assert_eq!(x2, Bits::new([0x0A, 0x0B, 0x0C, 0x0D, 0x0E, 0x0F]));
> ```

> ```rust
> pub fn extend_right(&mut self, bytes: &[u8])
> ```
>
> 
> Adds lower bit padding to a bit string.
> 
> ```rust
> let mut x1 = Bits::empty();
> 
> x1.extend_right(&[0x0A, 0x0B, 0x0C]);
> 
> assert_eq!(x1.len(), 24);
> assert_eq!(x1, Bits::new([0x0A, 0x0B, 0x0C]));
> 
> let mut x2 = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x2.extend_right(&[0x0D, 0x0E, 0x0F]);
> 
> assert_eq!(x2.len(), 44);
> assert_eq!(x2, Bits::from([0x0D, 0x0E, 0x0F, 0x0A, 0x0B, 0x0C]));
> ```

> ```rust
> pub fn hamming_weight(&self) -> usize
> ```
>
> The number of ones.
> 
> ```rust
> let mut x = Bits::from([15, 15, 15]);
> 
> assert_eq!(x.hamming_weight(), 12);
> ```

> ```rust
> pub fn i(&self, i: usize) -> u8
> ```
>
> State of a bit.
> 
> ```rust
> let mut x = Bits::from([0x0F]);
> 
> assert_eq!(x.i(3), 1u8);
> ```
> 
> <span style="color: red">ⓘ</span>
> ```rust
> let mut x = Bits::from([0x0F]);
> 
> assert_eq!(x.i(4), 0);
> ```

> ```rust
> pub fn into_bytes(self) -> IntoBytes
> ```
>
> An iterator over the individual bits
> 
> ```rust
> let x = Bits::new([0xAB, 0xCD, 0xEF]);
> let y = x.into_bytes().collect::<Vec<u8>>();
> 
> assert_eq!(y, vec![0xAB, 0xCD, 0xEF]);
> ```

> ```rust
> pub fn iter(&self) -> Iter<'_>
> ```
>
> An iterator over the individual bits
> 
> ```rust
> let x = Bits::new([0xAB, 0xCD, 0xEF]);
> let mut ones = 0;
> 
> for bit in x.iter() { if bit == 1 { ones += 1; } }
> 
> assert_eq!(ones, 17);
> ```

> ```rust
> pub fn iter_from(&self, index: usize) -> Iter<'_>
> ```
>
> An iterator over the individual bits
> 
> ```rust
> let x = Bits::new([0xAB, 0xCD, 0xEF]);
> let mut ones = 0;
> 
> for bit in x.iter_from(0) { if bit == 1 { ones += 1; } }
> 
> assert_eq!(ones, 17);
> 
> ones = 0;
> 
> for bit in x.iter_from(13) { if bit == 1 { ones += 1; } }
> 
> assert_eq!(ones, 9);
> ```

> ```rust
> pub fn leading_ones(&self) -> usize
> ```
>
> The number of leading ones.
> 
> ```rust
> let x1 = Bits::from([0x0A, 0xFF, 0x03]);
> 
> assert_eq!(x1.leading_ones(), 10);
> 
> let x2 = Bits::new([0x0A, 0xFF, 0x0B]);
> 
> assert_eq!(x2.leading_ones(), 0);
> ```

> ```rust
> pub fn leading_zeros(&self) -> usize
> ```
>
> The number of leading zeros.
> 
> ```rust
> let x1 = Bits::from([0x0A, 0x00, 0x00]);
> 
> assert_eq!(x1.leading_zeros(), 0);
> 
> let x2 = Bits::zeros(20);
> 
> assert_eq!(x2.leading_zeros(), 20);
> ```

> ```rust
> pub fn len(&self) -> usize
> ```
>
> The number of bits.
> 
> ```rust
> let x1 = Bits::empty();
> 
> assert_eq!(x1.len(), 0);
> 
> let x2 = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> assert_eq!(x2.len(), 20);
> 
> let x3 = Bits::new([0x0A, 0x0B, 0x0C]);
> 
> assert_eq!(x3.len(), 24);
> 
> let x4 = Bits::slice(&[0x0A, 0x0B, 0x0C], 17);
> 
> assert_eq!(x4.len(), 17);
> ```

> ```rust
> pub fn none(&self) -> bool
> ```
>
> Whether all bits are zero.
> 
> ```rust
> let x1 = Bits::empty();
> 
> assert!(!x1.any());
> 
> let x2 = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> assert!(x2.any());
> 
> let x3 = Bits::zeros(20);
> 
> assert!(!x3.any());
> ```

> ```rust
> pub fn or(&self, rhs: &Bits) -> Bits
> ```
>
> Bitwise or of two bit strings.
> 
> ```rust
> let x1 = Bits::from([0x20, 0x30, 0x40]);
> let y1 = Bits::from([0xA0, 0xB0, 0xC0]);
> 
> assert_eq!(x1.or(&y1), Bits::from([0xA0, 0xB0, 0xC0]));
> 
> let x2 = Bits::from([0x20, 0x30, 0x40]);
> let y2 = Bits::from([0x0A, 0xB0, 0xC0]);
> 
> assert_eq!(x2.len(), 23);
> assert_eq!(y2.len(), 24);
> 
> let z = x2.or(&y2);
> 
> assert_eq!(z.len(), 24);
> ```

> ```rust
> pub fn or_mut(&mut self, rhs: &Bits)
> ```
>
> Bitwise or of two bit strings.
> 
> ```rust
> let mut x1 = Bits::from([0x20, 0x30, 0x40]);
> let y1 = Bits::from([0xA0, 0xB0, 0xC0]);
> 
> x1.or_mut(&y1);
> 
> assert_eq!(x1, Bits::from([0xA0, 0xB0, 0xC0]));
> 
> let mut x2 = Bits::from([0x20, 0x30, 0x40]);
> let y2 = Bits::from([0x0A, 0xB0, 0xC0]);
> 
> assert_eq!(x2.len(), 23);
> assert_eq!(y2.len(), 24);
> 
> x2.or_mut(&y2);
> 
> assert_eq!(x2.len(), 24);
> ```

> ```rust
> pub fn pop_left(&mut self) -> u8
> ```
>
> Shifts out the most significant bit.
> 
> ```rust
> let mut x1 = Bits::empty();
> 
> assert_eq!(x1.pop_left(), 0u8);
> 
> let mut x2 = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> assert_eq!(x2.pop_left(), 1u8);
> assert_eq!(x2.len(), 19);
> 
> let mut x3 = Bits::new([0x0A, 0x0B, 0x0C]);
> 
> assert_eq!(x3.pop_left(), 0u8);
> assert_eq!(x3.len(), 23);
> ```

> ```rust
> pub fn pop_right(&mut self) -> u8
> ```
>
> Shifts out the least significant bit.
> 
> ```rust
> let mut x1 = Bits::empty();
> 
> assert_eq!(x1.pop_right(), 0u8);
> 
> let mut x2 = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> assert_eq!(x2.pop_right(), 0u8);
> assert_eq!(x2.len(), 19);
> assert_eq!(x2.pop_right(), 1u8);
> ```

> ```rust
> pub fn push_left(&mut self, bit: bool, count: usize)
> ```
>
> Adds upper bit padding to a bit string.
> 
> ```rust
> let mut x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x1.push_left(true, 17);
> 
> assert_eq!(x1.len(), 37);
> assert_eq!(x1, Bits::from([0x0A, 0x0B, 0xFC, 0xFF, 0x1F]));
> 
> let mut x2 = Bits::new([0x0A, 0x0B, 0x0C]);
> 
> x2.push_left(false, 17);
> 
> assert_eq!(x2.len(), 41);
> assert_eq!(x2, Bits::slice(&[0x0A, 0x0B, 0x0C, 0x00, 0x00, 0x00], 41));
> ```

> ```rust
> pub fn push_byte_left(&mut self, word: u8, count: usize)
> ```
>
> Adds upper bit padding to a bit string.
> 
> ```rust
> let mut x = Bits::from([15, 15, 15]);
> 
> x.push_byte_left(15, 2);
> 
> assert_eq!(x.len(), 36);
> assert_eq!(x, Bits::slice(&[15, 15, 255, 240, 0], 36));
> 
> x = Bits::new([15, 15, 15]);
> 
> x.push_byte_left(31, 2);
> 
> assert_eq!(x.len(), 40);
> assert_eq!(x, Bits::new([15, 15, 15, 31, 31]));
> ```

> ```rust
> pub fn push_right(&mut self, bit: bool, count: usize)
> ```
>
> Adds lower bit padding to a bit string.
> 
> ```rust
> let mut x = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x.push_right(true, 4);
> 
> assert_eq!(x.len(), 24);
> assert_eq!(x, Bits::from([0xAF, 0xB0, 0xC0]));
> ```

> ```rust
> pub fn push_byte_right(&mut self, word: u8, count: usize)
> ```
>
> Adds lower bit padding to a bit string.
> 
> ```rust
> let mut x = Bits::from([15, 15, 15]);
> 
> x.push_byte_right(31, 2);
> 
> assert_eq!(x.len(), 36);
> assert_eq!(x, Bits::from([31, 31, 15, 15, 15]));
> ```

> ```rust
> pub fn reset(&mut self, i: usize)
> ```
>
> Sets a bit to zero.
> 
> ```rust
> let mut x = Bits::new([15]);
> 
> assert_eq!(x.i(3), 1u8);
> 
> x.reset(3);
> 
> assert_eq!(x.i(3), 0u8);
> ```

> ```rust
> pub fn reset_bits(&mut self, start: usize, count: usize)
> ```
>
> Sets the state of a range of bits to zero.
> 
> ```rust
> let mut x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> x1.reset_bits(7, 10);
> 
> assert_eq!(x1, Bits::from([0x0A, 0x00, 0x0C]));
> 
> let mut x2 = Bits::from([0x0A, 0x0B, 0x0C]);
> x2.reset_bits(8, 12);
> 
> assert_eq!(x2, Bits::slice(&[0x0A, 0x00, 0x00], 20));
> ```
>
> <span style="color: red">ⓘ</span>
> ```rust
> let mut x = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x.reset_bits(21, 14);
> ```
>
> <span style="color: red">ⓘ</span>
> ```rust
> let mut x = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x.reset_bits(7, 14);
> ```

> ```rust
> pub fn reset_byte(&mut self, i: usize)
> ```
>
> Sets the state of a byte to zero.
> 
> ```rust
> let mut x = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x.reset_byte(1);
> 
> assert_eq!(x, Bits::from([0x0A, 0x00, 0x0C]));
> 
> x.reset_byte(2);
> 
> assert_eq!(x, Bits::slice(&[0x0A, 0x00, 0x00], 20));
> ```
> 
> <span style="color: red">ⓘ</span>
> ```rust
> let mut x = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x.reset_byte(3);
> ```

> ```rust
> pub fn reset_bytes(&mut self, start: usize, count: usize)
> ```
>
> Sets the state of a range of bytes to zero.
> 
> ```rust
> let mut x = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x.reset_bytes(1, 2);
> 
> assert_eq!(x, Bits::slice(&[0x0A, 0x00, 0x00], 20));
> ```
> 
> <span style="color: red">ⓘ</span>
> ```rust
> let mut x = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x.reset_bytes(3, 2);
> ```
> 
> <span style="color: red">ⓘ</span>
> ```rust
> let mut x = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x.reset_bytes(0, 4);
> ```

> ```rust
> pub fn reverse(&mut self)
> ```
>
> Reverses the order of the bits.
> 
> ```rust
> let mut x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x1.reverse();
> 
> assert_eq!(x1, Bits::slice(&[0x03, 0x0D, 0x05], 20));
> 
> let mut x2 = Bits::new([0x0A, 0x0B, 0x0C]);
> 
> x2.reverse();
> 
> assert_eq!(x2, Bits::new([0x30, 0xD0, 0x50]));
> ```

> ```rust
> pub fn reversed(&self) -> Bits
> ```
>
> Reverses the order of the bits.
> 
> ```rust
> let x1 = Bits::from([0x0A, 0x0B, 0x0C]);
>
> assert_eq!(x1.reversed(), Bits::slice(&[0x03, 0x0D, 0x05], 20));
> 
> let x2 = Bits::new([0x0A, 0x0B, 0x0C]);
> 
> assert_eq!(x2.reversed(), Bits::new([0x30, 0xD0, 0x50]));
> ```

> ```rust
> pub fn rotate_left(&mut self, count: usize)
> ```
>
> Rotates bits to the left.
> 
> ```rust
> let mut x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x1.rotate_left(4);
> 
> assert_eq!(x1, Bits::slice(&[0xAC, 0xB0, 0x00], 20));
> assert_eq!(x1.len(), 20);
> 
> let mut x2 = Bits::new([0x0A, 0x0B, 0x0C]);
> 
> x2.rotate_left(4);
> 
> assert_eq!(x2, Bits::new([0xA0, 0xB0, 0xC0]));
> assert_eq!(x2.len(), 24);
> ```

> ```rust
> pub fn rotated_left(&self, count: usize) -> Self
> ```
>
> Rotates bits to the left.
> 
> ```rust
> let mut x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> assert_eq!(x1.rotated_left(4), Bits::slice(&[0xAC, 0xB0, 0x00], 20));
> assert_eq!(x1.len(), 20);
> 
> let mut x2 = Bits::new([0x0A, 0x0B, 0x0C]);
> 
> assert_eq!(x2.rotated_left(4), Bits::new([0xA0, 0xB0, 0xC0]));
> assert_eq!(x2.len(), 24);
> ```

> ```rust
> pub fn rotate_right(&mut self, count: usize)
> ```
>
> Rotates bits to the right.
> 
> ```rust
> let mut x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x1.rotate_right(4);
> 
> assert_eq!(x1, Bits::slice(&[0xB0, 0xC0, 0x0A], 20));
> assert_eq!(x1.len(), 20);
> 
> let mut x2 = Bits::new([0x0A, 0x0B, 0x0C]);
> 
> x2.rotate_right(4);
> 
> assert_eq!(x2, Bits::new([0xB0, 0xC0, 0xA0]));
> assert_eq!(x2.len(), 24);
> ```

> ```rust
> pub fn rotated_right(&self, count: usize) -> Self
> ```
>
> Rotates bits to the right.
> 
> ```rust
> let mut x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> assert_eq!(x1.rotated_right(4), Bits::slice(&[0xB0, 0xC0, 0x0A], 20));
> assert_eq!(x1.len(), 20);
> 
> let mut x2 = Bits::new([0x0A, 0x0B, 0x0C]);
> 
> assert_eq!(x2.rotated_right(4), Bits::new([0xB0, 0xC0, 0xA0]));
> assert_eq!(x2.len(), 24);
> ```

> ```rust
> pub fn set(&mut self, i: usize)
> ```
>
> Sets a bit to one.
> 
> ```rust
> let mut x = Bits::new([15]);
> 
> assert_eq!(x.i(4), 0u8);
> 
> x.set(4);
> 
> assert_eq!(x.i(4), 1u8);
> ```

> ```rust
> pub fn set_bits(&mut self, start: usize, count: usize)
> ```
>
> Sets the state of a range of bits to one.
> 
> ```rust
> let mut x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> x1.set_bits(7, 10);
> 
> assert_eq!(x1, Bits::from([0x8A, 0xFF, 0x0D]));
> 
> let mut x2 = Bits::from([0x0A, 0x0B, 0x0C]);
> x2.set_bits(8, 12);
> 
> assert_eq!(x2, Bits::slice(&[0x0A, 0xFF, 0x0F], 20));
> ```
> 
> <span style="color: red">ⓘ</span>
> ```rust
> let mut x = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x.set_bits(21, 14);
> ```
> 
> <span style="color: red">ⓘ</span>
> ```rust
> let mut x = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x.set_bits(7, 14);
> ```

> ```rust
> pub fn set_byte(&mut self, i: usize)
> ```
>
> Sets the state of a byte to all ones.
> 
> ```rust
> let mut x = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x.set_byte(1);
> 
> assert_eq!(x, Bits::from([0x0A, 0xFF, 0x0C]));
> 
> x.set_byte(2);
> 
> assert_eq!(x, Bits::slice(&[0x0A, 0xFF, 0x0F], 20));
> ```
> 
> <span style="color: red">ⓘ</span>
> ```rust
> let mut x = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x.toggle_byte(3);
> ```

> ```rust
> pub fn set_bytes(&mut self, start: usize, count: usize)
> ```
>
> Sets the state of a range of bytes to all ones.
> 
> ```rust
> let mut x = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x.set_bytes(1, 2);
> 
> assert_eq!(x, Bits::slice(&[0x0A, 0xFF, 0x0F], 20));
> ```
> 
> <span style="color: red">ⓘ</span>
> ```rust
> let mut x = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x.set_bytes(3, 2);
> ```
> 
> <span style="color: red">ⓘ</span>
> ```rust
> let mut x = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x.set_bytes(0, 4);
> ```

> ```rust
> pub fn shift_left(&mut self, count: usize)
> ```
>
> Shifts out upper bits, shifting in zeros on the lower end.
> 
> ```rust
> let mut x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x1.shift_left(17);
> 
> assert_eq!(x1, Bits::slice(&[0x00, 0x00, 0x04], 20));
> assert_eq!(x1.len(), 20);
> 
> let mut x2 = Bits::new([0x0A, 0x0B, 0x0C]);
> 
> x2.shift_left(4);
> 
> assert_eq!(x2, Bits::new([0xA0, 0xB0, 0xC0]));
> assert_eq!(x2.len(), 24);
> ```

> ```rust
> pub fn shifted_left(&self, count: usize) -> Self
> ```
>
> Shifts out upper bits, shifting in zeros on the lower end.
> 
> ```rust
> let x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> let s1 = x1.shifted_left(17);
> 
> assert_eq!(s1, Bits::slice(&[0x00, 0x00, 0x04], 20));
> assert_eq!(s1.len(), 20);
> 
> let x2 = Bits::new([0x0A, 0x0B, 0x0C]);
> let s2 = x2.shifted_left(4);
> 
> assert_eq!(s2, Bits::new([0xA0, 0xB0, 0xC0]));
> assert_eq!(s2.len(), 24);
> ```

> ```rust
> pub fn shift_right(&mut self, count: usize)
> ```
>
> Shifts out lower bits, shifting zeros into the upper bits.
> 
> ```rust
> let mut x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x1.shift_right(17);
> 
> assert_eq!(x1.len(), 20);
> assert_eq!(x1, Bits::slice(&[0x06, 0x00, 0x00], 20));
> 
> let mut x2 = Bits::new([0x0A, 0x0B, 0x0C]);
> 
> x2.shift_right(4);
> 
> assert_eq!(x2.len(), 24);
> assert_eq!(x2, Bits::new([0xB0, 0xC0, 0x00]));
> ```

> ```rust
> pub fn shifted_right(&self, count: usize) -> Self
> ```
>
> Shifts out lower bits, shifting zeros into the upper bits.
> 
> ```rust
> let x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> let s1 = x1.shifted_right(17);
> 
> assert_eq!(s1.len(), 20);
> assert_eq!(s1, Bits::slice(&[0x06, 0x00, 0x00], 20));
> 
> let x2 = Bits::new([0x0A, 0x0B, 0x0C]);
> let s2 = x2.shifted_right(4);
> 
> assert_eq!(s2.len(), 24);
> assert_eq!(s2, Bits::new([0xB0, 0xC0, 0x00]));
> ```

> ```rust
> pub fn size(&self) -> usize
> ```
>
> The number of bytes.
> 
> ```rust
> let x1 = Bits::empty();
> 
> assert_eq!(x1.size(), 0);
> 
> let x2 = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> assert_eq!(x2.size(), 3);
> 
> let x3 = Bits::new([0x0A, 0x0B, 0x0C]);
> 
> assert_eq!(x3.size(), 3);
> 
> let x4 = Bits::slice(&[0x0A, 0x0B, 0x0C], 13);
> 
> assert_eq!(x4.size(), 2);
> ```

> ```rust
> pub fn split(&self, i: usize) -> (Bits, Bits)
> ```
>
> Splits the bit string.
> 
> When the index is greater than or equal to the length of the bit string, the second element of the returned pair will be empty. When the index is 0, the first element will be empty.
> 
> ```rust
> let x1 = Bits::empty();
> let (l1, r1) = x1.split(11);
> 
> assert_eq!(l1.len(), 0);
> assert_eq!(r1.len(), 0);
> 
> let x2 = Bits::from([0x0A, 0x0B, 0x0C]);
> let (l2, r2) = x2.split(20);
> 
> assert_eq!(l2, x2);
> assert_eq!(r2.len(), 0);
> 
> let (l3, r3) = x2.split(0);
> 
> assert_eq!(l3.len(), 0);
> assert_eq!(r3, x2);
> 
> let (l4, r4) = x2.split(11);
> assert_eq!(l4, Bits::slice(&[0x0A, 0x03], 11));
> assert_eq!(r4, Bits::slice(&[0x81, 0x01], 9));
> ```

> ```rust
> pub fn test(&self, i: usize) -> bool
> ```
>
> Whether a bit is one.
> 
> ```rust
> let mut x = Bits::from([0x0F]);
> 
> assert!(x.test(3));
> assert!(!x.test(4));
> assert!(!x.test(8));
> ```

> ```rust
> pub fn toggle(&mut self, i: usize)
> ```
>
> Flips the state of a bit.
> 
> ```rust
> let mut x = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> assert_eq!(x.i(0), 0u8);
> assert_eq!(x.i(1), 1u8);
> 
> x.toggle(0);
> x.toggle(1);
> 
> assert_eq!(x.i(0), 1u8);
> assert_eq!(x.i(1), 0u8);
> ```
>
> <span style="color: red">ⓘ</span>
> ```rust
> let mut x = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x.toggle(21);
> ```

> ```rust
> pub fn toggle_bits(&mut self, start: usize, count: usize)
> ```
>
> Flips the state of a range of bits.
> 
> ```rust
> let mut x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> x1.toggle_bits(7, 10);
> 
> assert_eq!(x1, Bits::from([0x8A, 0xF4, 0x0D]));
> 
> let mut x2 = Bits::from([0x0A, 0x0B, 0x0C]);
> x2.toggle_bits(8, 12);
> 
> assert_eq!(x2, Bits::slice(&[0x0A, 0xF4, 0x03], 20));
> ```
> 
> <span style="color: red">ⓘ</span>
> ```rust
> let mut x = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x.toggle_bits(21, 14);
> ```
> 
> <span style="color: red">ⓘ</span>
> ```rust
> let mut x = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x.toggle_bits(7, 14);
> ```

> ```rust
> pub fn toggle_byte(&mut self, i: usize)
> ```
>
> Flips the state of a byte.
> 
> ```rust
> let mut x = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x.toggle_byte(1);
> 
> assert_eq!(x, Bits::from([0x0A, 0xF4, 0x0C]));
> 
> x.toggle_byte(2);
> 
> assert_eq!(x, Bits::slice(&[0x0A, 0xF4, 0x03], 20));
> ```
> 
> <span style="color: red">ⓘ</span>
> ```rust
> let mut x = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x.toggle_byte(3);
> ```

> ```rust
> pub fn toggle_bytes(&mut self, start: usize, count: usize)
> ```
>
> Flips the state of a range of bytes.
> 
> ```rust
> let mut x = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x.toggle_bytes(1, 2);
> 
> assert_eq!(x, Bits::slice(&[0x0A, 0xF4, 0x03], 20));
> ```
> 
> <span style="color: red">ⓘ</span>
> ```rust
> let mut x = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x.toggle_bytes(3, 2);
> ```
> 
> <span style="color: red">ⓘ</span>
> ```rust
> let mut x = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x.toggle_bytes(0, 4);
> ```

> ```rust
> pub fn trailing_ones(&self) -> usize
> ```
>
> The number of trailing ones.
> 
> ```rust
> let x = Bits::from([0xFF, 0x0B, 0x0A]);
> 
> assert_eq!(x.trailing_ones(), 10);
> ```

> ```rust
> pub fn trailing_zeros(&self) -> usize
> ```
>
> The number of trailing zeros.
> 
> ```rust
> let x1 = Bits::from([0x00, 0x0A, 0x0B]);
> 
> assert_eq!(x1.trailing_zeros(), 9);
> 
> let x2 = Bits::zeros(20);
> 
> assert_eq!(x2.trailing_zeros(), 20);
> ```

> ```rust
> pub fn trim_end(&mut self, bit: bool)
> ```
>
> Trims leading bits.
> 
> ```rust
> let mut x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x1.trim_end(false);
> 
> assert_eq!(x1.len(), 20);
> assert_eq!(x1, Bits::from([0x0A, 0x0B, 0x0C]));
> 
> x1.trim_end(true);
> 
> assert_eq!(x1.len(), 18);
> assert_eq!(x1, Bits::slice(&[0x0A, 0x0B, 0x00], 18));
> 
> let mut x2 = Bits::new([0x0A, 0x0B, 0x0C]);
> 
> x2.trim_end(true);
> 
> assert_eq!(x2.len(), 24);
> assert_eq!(x2, Bits::new([0x0A, 0x0B, 0x0C]));
> 
> x2.trim_end(false);
> 
> assert_eq!(x2.len(), 20);
> assert_eq!(x2, Bits::from([0x0A, 0x0B, 0x0C]));
> 
> let mut x3 = Bits::slice(&[0x0A, 0x0B, 0x00], 18);
> 
> x3.trim_end(false);
> 
> assert_eq!(x3.len(), 12);
> assert_eq!(x3, Bits::from([0x0A, 0x0B]));
> 
> let mut x4 = Bits::slice(&[0x0A, 0xFB, 0x03], 18);
> 
> x4.trim_end(true);
> 
> assert_eq!(x4.len(), 11);
> assert_eq!(x4, Bits::slice(&[0x0A, 0x0B], 11));
> ```

> ```rust
> pub fn trim_start(&mut self, bit: bool)
> ```
>
> Trims trailing bits.
> 
> ```rust
> let mut x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x1.trim_start(true);
> 
> assert_eq!(x1.len(), 20);
> assert_eq!(x1, Bits::from([0x0A, 0x0B, 0x0C]));
> 
> x1.trim_start(false);
> 
> assert_eq!(x1.len(), 19);
> assert_eq!(x1, Bits::from([0x85, 0x05, 0x06]));
> 
> let mut x2 = Bits::new([0x00, 0x0A, 0x0B]);
> 
> x2.trim_start(false);
> 
> assert_eq!(x2.len(), 15);
> assert_eq!(x2, Bits::slice(&[0x85, 0x05], 15));
> 
> let mut x3 = Bits::new([0xFF, 0x0B, 0x0C]);
> 
> x3.trim_start(true);
> 
> assert_eq!(x3.len(), 14);
> assert_eq!(x3, Bits::slice(&[0x02, 0x03], 14));
> ```

> ```rust
> pub fn xor(&self, rhs: &Bits) -> Bits
> ```
>
> Bitwise exclusive or of two bit strings.
> 
> ```rust
> let x1 = Bits::from([0x20, 0x30, 0x40]);
> let y1 = Bits::from([0xA0, 0xB0, 0xC0]);
> 
> assert_eq!(x1.xor(&y1), Bits::from([0x80, 0x80, 0x80]));
> 
> let x2 = Bits::from([0x20, 0x30, 0x40]);
> let y2 = Bits::from([0x0A, 0xB0, 0xC0]);
> 
> assert_eq!(x2.len(), 23);
> assert_eq!(y2.len(), 24);
> 
> let z = x2.xor(&y2);
> 
> assert_eq!(z.len(), 24);
> ```

> ```rust
> pub fn xor_mut(&mut self, rhs: &Bits)
> ```
>
> Bitwise exclusive or of two bit strings.
> 
> ```rust
> let mut x1 = Bits::from([0x20, 0x30, 0x40]);
> let y1 = Bits::from([0xA0, 0xB0, 0xC0]);
> 
> x1.xor_mut(&y1);
> 
> assert_eq!(x1, Bits::from([0x80, 0x80, 0x80]));
> 
> let mut x2 = Bits::from([0x20, 0x30, 0x40]);
> let y2 = Bits::from([0x0A, 0xB0, 0xC0]);
> 
> assert_eq!(x2.len(), 23);
> assert_eq!(y2.len(), 24);
> 
> x2.xor_mut(&y2);
> 
> assert_eq!(x2.len(), 24);
> ```

> ```rust
> pub fn xrange<R: RangeBounds<usize>>(&self, bounds: R) -> Self
> ```
>
> Creates a bit string by copying a range of bits.
>
> The range is truncated to take no more than the number of available bits from the
> starting bound. For alternative behavior, consider `Bits::take`, which pads zeros
> when the length exceeds the number of available bits.
>
> ```rust
> # use bit_byte_bit::{Bits};
> let x1 = Bits::empty();
> let x1_r1 = x1.xrange(1..18);
>
> assert_eq!(x1_r1, Bits::empty());
>
> let x2 = Bits::zeros(24);
> let x2_r1 = x2.xrange(8..24);
> let x2_r2 = x2.xrange(8..=23);
>
> assert_eq!(x2_r1, Bits::zeros(16));
> assert_eq!(x2_r2, x2_r1);
>
> let x3 = Bits::from([0x0A, 0x0B, 0x0C]);
> let x3_r1 = x3.xrange(1..2);
>
> assert_eq!(x3_r1, Bits::from([0x01]));
>
> let x3_r2 = x3.xrange(0..);
> let x3_r3 = x3.xrange(..);
>
> assert_eq!(x3_r2, x3);
> assert_eq!(x3_r3, x3_r2);
>
> let x3_r4 = x3.xrange(..32);
>
> assert_eq!(x3_r4, Bits::from([0x0A, 0x0B, 0x0C]));
> assert_eq!(x3_r4.len(), 20);
>
> let x3_r5 = x3.xrange(18..32);
>
> assert_eq!(x3_r5, Bits::from([0x3]));
> assert_eq!(x3_r5.len(), 2);
>
> let x3_r6 = x3.xrange(8..0);
>
> as>t_eq!(x3_r6, Bits::empty());
> ``>Trait Implementations

---

## `impl Binary for Bits`

---

> ```rust
> fn fmt(&self, f: &mut Formatter<'_>) -> Result
> ```
>
> Formats the value using the given formatter. Read more


## `impl BitAnd<&Bits> for &Bits`

---

> ```rust
> fn bitand(self, rhs: &Bits) -> Self::Output
> ```
>
> Bitwise and of two bit strings.
> 
> ```rust
> type Output = Bits
> ```
> 
> The resulting type after applying the & operator.
>
> ```rust
> let x1 = Bits::from([0x20, 0x30, 0x40]);
> let y1 = Bits::from([0xA0, 0xB0, 0xC0]);
> 
> assert_eq!(x1 & &y1, Bits::new([0x20, 0x30, 0x40]));
> 
> let x2 = Bits::from([0x20, 0x30, 0x40]);
> let y2 = Bits::from([0x0A, 0xB0, 0xC0]);
> 
> assert_eq!(x2.len(), 23);
> assert_eq!(y2.len(), 24);
> 
> let z = x2 & &y2;
> 
> assert_eq!(z.len(), 24);
> ```



## `impl BitAnd<&Bits> for Bits`

---

> ```rust
> fn bitand(self, rhs: &Bits) -> Self::Output
> ```
>
> Bitwise and of two bit strings.
> 
> ```rust
> type Output = Bits
> ```
> 
> The resulting type after applying the & operator.
> 
> ```rust
> let x1 = Bits::from([0x20, 0x30, 0x40]);
> let y1 = Bits::from([0xA0, 0xB0, 0xC0]);
> 
> assert_eq!(x1 & &y1, Bits::new([0x20, 0x30, 0x40]));
> 
> let x2 = Bits::from([0x20, 0x30, 0x40]);
> let y2 = Bits::from([0x0A, 0xB0, 0xC0]);
> 
> assert_eq!(x2.len(), 23);
> assert_eq!(y2.len(), 24);
> 
> let z = x2 & &y2;
> 
> assert_eq!(z.len(), 24);
> ```



## `impl BitAnd for Bits`

---

> ```rust
> fn bitand(self, rhs: Self) -> Self::Output
> ```
>
> Bitwise and of two bit strings.
> 
> ```rust
> type Output = Bits
> ```
> 
> The resulting type after applying the & operator.
> 
> ```rust
> let x1 = Bits::from([0x20, 0x30, 0x40]);
> let y1 = Bits::from([0xA0, 0xB0, 0xC0]);
> 
> assert_eq!(x1 & y1, Bits::new([0x20, 0x30, 0x40]));
> 
> let x2 = Bits::from([0x20, 0x30, 0x40]);
> let y2 = Bits::from([0x0A, 0xB0, 0xC0]);
> 
> assert_eq!(x2.len(), 23);
> assert_eq!(y2.len(), 24);
> 
> let z = x2 & y2;
> 
> assert_eq!(z.len(), 24);
> ```


## `impl BitAndAssign<&Bits> for Bits`

---

> ```rust
> fn bitand_assign(&mut self, rhs: &Bits)
> ```
>
> Bitwise and of two bit strings.
> 
> ```rust
> let mut x1 = Bits::from([0x20, 0x30, 0x40]);
> let y1 = Bits::from([0xA0, 0xB0, 0xC0]);
> 
> x1 &= &y1;
> 
> assert_eq!(x1, Bits::new([0x20, 0x30, 0x40]));
> 
> let mut x2 = Bits::from([0x20, 0x30, 0x40]);
> let y2 = Bits::from([0x0A, 0xB0, 0xC0]);
> 
> assert_eq!(x2.len(), 23);
> assert_eq!(y2.len(), 24);
> 
> x2 &= &y2;
> 
> assert_eq!(x2.len(), 24);
> ```

## `impl BitAndAssign for Bits`

---

> ```rust
> fn bitand_assign(&mut self, rhs: Self)
> ```
>
> Bitwise and of two bit strings.
> 
> ```rust
> let mut x1 = Bits::from([0x20, 0x30, 0x40]);
> let y1 = Bits::from([0xA0, 0xB0, 0xC0]);
> 
> x1 &= y1;
> 
> assert_eq!(x1, Bits::new([0x20, 0x30, 0x40]));
> 
> let mut x2 = Bits::from([0x20, 0x30, 0x40]);
> let y2 = Bits::from([0x0A, 0xB0, 0xC0]);
> 
> assert_eq!(x2.len(), 23);
> assert_eq!(y2.len(), 24);
> 
> x2 &= y2;
> 
> assert_eq!(x2.len(), 24);
> ```

## `impl BitOr<&Bits> for &Bits`

---

> ```rust
> fn bitor(self, rhs: &Bits) -> Self::Output
> ```
>
> Bitwise or of two bit strings.
> 
> ```rust
> type Output = Bits
> ```
> 
> The resulting type after applying the \| operator.
> 
> ```rust
> let x1 = Bits::from([0x20, 0x30, 0x40]);
> let y1 = Bits::from([0xA0, 0xB0, 0xC0]);
> 
> assert_eq!(x1 | &y1, Bits::from([0xA0, 0xB0, 0xC0]));
> 
> let x2 = Bits::from([0x20, 0x30, 0x40]);
> let y2 = Bits::from([0x0A, 0xB0, 0xC0]);
> 
> assert_eq!(x2.len(), 23);
> assert_eq!(y2.len(), 24);
> 
> let z = x2 | &y2;
> 
> assert_eq!(z.len(), 24);
> ```



## `impl BitOr<&Bits> for Bits`

---

> ```rust
> fn bitor(self, rhs: &Bits) -> Self::Output
> ```
>
> Bitwise or of two bit strings.
> 
> ```rust
> type Output = Bits
> ```
>
> The resulting type after applying the \| operator. 
> 
> ```rust
> let x1 = Bits::from([0x20, 0x30, 0x40]);
> let y1 = Bits::from([0xA0, 0xB0, 0xC0]);
> 
> assert_eq!(x1 | &y1, Bits::from([0xA0, 0xB0, 0xC0]));
> 
> let x2 = Bits::from([0x20, 0x30, 0x40]);
> let y2 = Bits::from([0x0A, 0xB0, 0xC0]);
> 
> assert_eq!(x2.len(), 23);
> assert_eq!(y2.len(), 24);
> 
> let z = x2 | &y2;
> 
> assert_eq!(z.len(), 24);
> ```


## `impl BitOr for Bits`

---

> ```rust
> fn bitor(self, rhs: Self) -> Self::Output
> ```
>
> Bitwise or of two bit strings.
> 
> ```rust
> type Output = Bits
> ```
> 
> The resulting type after applying the \| operator.
> 
> ```rust
> let x1 = Bits::from([0x20, 0x30, 0x40]);
> let y1 = Bits::from([0xA0, 0xB0, 0xC0]);
> 
> assert_eq!(x1 | y1, Bits::from([0xA0, 0xB0, 0xC0]));
> 
> let x2 = Bits::from([0x20, 0x30, 0x40]);
> let y2 = Bits::from([0x0A, 0xB0, 0xC0]);
> 
> assert_eq!(x2.len(), 23);
> assert_eq!(y2.len(), 24);
> 
> let z = x2 | y2;
> 
> assert_eq!(z.len(), 24);
> ```



## `impl BitOrAssign<&Bits> for Bits`

---

> ```rust
> fn bitor_assign(&mut self, rhs: &Bits)
> ```
>
> Bitwise or of two bit strings.
> 
> ```rust
> let mut x1 = Bits::from([0x20, 0x30, 0x40]);
> let y1 = Bits::from([0xA0, 0xB0, 0xC0]);
> 
> x1 |= &y1;
> 
> assert_eq!(x1, Bits::from([0xA0, 0xB0, 0xC0]));
> 
> let mut x2 = Bits::from([0x20, 0x30, 0x40]);
> let y2 = Bits::from([0x0A, 0xB0, 0xC0]);
> 
> assert_eq!(x2.len(), 23);
> assert_eq!(y2.len(), 24);
> 
> x2 |= &y2;
> 
> assert_eq!(x2.len(), 24);
> ```

## `impl BitOrAssign for Bits`

---

> ```rust
> fn bitor_assign(&mut self, rhs: Self)
> ```
>
> Bitwise or of two bit strings.
> 
> ```rust
> let mut x1 = Bits::from([0x20, 0x30, 0x40]);
> let y1 = Bits::from([0xA0, 0xB0, 0xC0]);
> 
> x1 |= y1;
> 
> assert_eq!(x1, Bits::from([0xA0, 0xB0, 0xC0]));
> 
> let mut x2 = Bits::from([0x20, 0x30, 0x40]);
> let y2 = Bits::from([0x0A, 0xB0, 0xC0]);
> 
> assert_eq!(x2.len(), 23);
> assert_eq!(y2.len(), 24);
> 
> x2 |= y2;
> 
> assert_eq!(x2.len(), 24);
> ```

## `impl BitXor<&Bits> for &Bits`

---

> ```rust
> fn bitxor(self, rhs: &Bits) -> Self::Output
> ```
> 
> Bitwise exclusive or of two bit strings.
> 
> ```rust
> type Output = Bits
> ```
> 
> The resulting type after applying the ^ operator.
> 
> ```rust
> let x1 = Bits::from([0x20, 0x30, 0x40]);
> let y1 = Bits::from([0xA0, 0xB0, 0xC0]);
> 
> assert_eq!(x1 ^ &y1, Bits::from([0x80, 0x80, 0x80]));
> 
> let x2 = Bits::from([0x20, 0x30, 0x40]);
> let y2 = Bits::from([0x0A, 0xB0, 0xC0]);
> 
> assert_eq!(x2.len(), 23);
> assert_eq!(y2.len(), 24);
> 
> let z = x2 ^ &y2;
> 
> assert_eq!(z.len(), 24);
> ```



## `impl BitXor<&Bits> for Bits`

---

> ```rust
> fn bitxor(self, rhs: &Bits) -> Self::Output
> ```
> 
> Bitwise exclusive or of two bit strings.
> 
> ```rust
> type Output = Bits
> ```
> 
> The resulting type after applying the ^ operator.
> 
> ```rust
> let x1 = Bits::from([0x20, 0x30, 0x40]);
> let y1 = Bits::from([0xA0, 0xB0, 0xC0]);
> 
> assert_eq!(x1 ^ &y1, Bits::from([0x80, 0x80, 0x80]));
> 
> let x2 = Bits::from([0x20, 0x30, 0x40]);
> let y2 = Bits::from([0x0A, 0xB0, 0xC0]);
> 
> assert_eq!(x2.len(), 23);
> assert_eq!(y2.len(), 24);
> 
> let z = x2 ^ &y2;
> 
> assert_eq!(z.len(), 24);
> ```



## `impl BitXor for Bits`

---

> ```rust
> fn bitxor(self, rhs: Self) -> Self::Output
> ```
> 
> Bitwise exclusive or of two bit strings.
> 
> ```rust
> type Output = Bits
> ```
> 
> The resulting type after applying the ^ operator.
> 
> ```rust
> let x1 = Bits::from([0x20, 0x30, 0x40]);
> let y1 = Bits::from([0xA0, 0xB0, 0xC0]);
> 
> assert_eq!(x1 ^ y1, Bits::from([0x80, 0x80, 0x80]));
> 
> let x2 = Bits::from([0x20, 0x30, 0x40]);
> let y2 = Bits::from([0x0A, 0xB0, 0xC0]);
> 
> assert_eq!(x2.len(), 23);
> assert_eq!(y2.len(), 24);
> 
> let z = x2 ^ y2;
> 
> assert_eq!(z.len(), 24);
> ```



## `impl BitXorAssign<&Bits> for Bits`

---

> ```rust
> fn bitxor_assign(&mut self, rhs: &Bits)
> ```
> 
> Bitwise exclusive or of two bit strings.
> 
> ```rust
> let mut x1 = Bits::from([0x20, 0x30, 0x40]);
> let y1 = Bits::from([0xA0, 0xB0, 0xC0]);
> 
> x1 ^= &y1;
> 
> assert_eq!(x1, Bits::from([0x80, 0x80, 0x80]));
> 
> let mut x2 = Bits::from([0x20, 0x30, 0x40]);
> let y2 = Bits::from([0x0A, 0xB0, 0xC0]);
> 
> assert_eq!(x2.len(), 23);
> assert_eq!(y2.len(), 24);
> 
> x2 ^= &y2;
> 
> assert_eq!(x2.len(), 24);
> ```

## `impl BitXorAssign for Bits`

---

> ```rust
> fn bitxor_assign(&mut self, rhs: Self)
> ```
> 
> Bitwise exclusive or of two bit strings.
> 
> ```rust
> let mut x1 = Bits::from([0x20, 0x30, 0x40]);
> let y1 = Bits::from([0xA0, 0xB0, 0xC0]);
> 
> x1 ^= y1;
> 
> assert_eq!(x1, Bits::from([0x80, 0x80, 0x80]));
> 
> let mut x2 = Bits::from([0x20, 0x30, 0x40]);
> let y2 = Bits::from([0x0A, 0xB0, 0xC0]);
> 
> assert_eq!(x2.len(), 23);
> assert_eq!(y2.len(), 24);
> 
> x2 ^= y2;
> 
> assert_eq!(x2.len(), 24);
> ```

## `impl Clone for Bits`

---

> ```rust
> fn clone(&self) -> Self
> ```
> 
> Returns a copy of the value.

> ```rust
> fn clone_from(&mut self, source: &Self)
> ```
> 
> Performs copy-assignment from source.

## `impl Debug for Bits`

---

> ```rust
> fn fmt(&self, f: &mut Formatter<'_>) -> Result
> ```
> 
> Formats the value using the given formatter.


## `impl Display for Bits`

---

> ```rust
> fn fmt(&self, f: &mut Formatter<'_>) -> Result
> ```
> 
> Formats the value using the given formatter.


## `impl Div<usize> for Bits`

---

> ```rust
> fn div(self, index: usize) -> Self::Output
> ```
> 
> Performs the / operation. Read more
> 
> ```rust
> type Output = (Bits, Bits)
> ```
> 
> The resulting type after applying the / operator.


## `impl Drop for Bits`

---

> ```rust
> fn drop(&mut self)
> ```
> 
> Executes the destructor for this type.


## `impl From<&[bool]> for Bits`

---

> ```rust
> fn from(bits: &[bool]) -> Self
> ```
> 
> Creates a bit string from booleans.
> 
> ```rust
> let bits1 = vec![true, false, true, true, false, true, true];
> let x1 = Bits::from(bits1.as_slice());
> 
> assert_eq!(x1.len(), 7);
> assert_eq!(x1, Bits::from([0x6D]));
> 
> let bits2 = vec![true, false, true, false, false, false, false, false, false];
> let x2 = Bits::from(bits2.as_slice());
> 
> assert_eq!(x2.len(), 9);
> assert_eq!(x2, Bits::slice(&[0x05, 0x00], 9));
> ```

## `impl From<&[u8]> for Bits`

---

> ```rust
> fn from(data: &[u8]) -> Self
> ```
> 
> Converts to this type from the input type.


## `impl<const N: usize> From<[bool; N]> for Bits`

---

> ```rust
> fn from(bits: [bool; N]) -> Self
> ```
> 
> Creates a bit string from booleans.
> 
> ```rust
> let x1 = Bits::from([true, false, true, true, false, true, true]);
> 
> assert_eq!(x1.len(), 7);
> assert_eq!(x1, Bits::from([0x6D]));
> 
> let x2 = Bits::from([true, false, true, false, false, false, false, false, false]);
> 
> assert_eq!(x2.len(), 9);
> assert_eq!(x2, Bits::slice(&[0x05, 0x00], 9));
> ```

# `impl<const N: usize> From<[u8; N]> for Bits`

---

> ```rust
> fn from(bytes: [u8; N]) -> Self
> ```
> 
> Converts to this type from the input type.

## `impl From<Vec<bool>> for Bits`

---

> ```rust
> fn from(bits: Vec<bool>) -> Self
> ```
> 
> Creates a bit string from booleans.
> 
> ```rust
> let bits1 = vec![true, false, true, true, false, true, true];
> let x1 = Bits::from(bits1);
> 
> assert_eq!(x1.len(), 7);
> assert_eq!(x1, Bits::from([0x6D]));
> 
> let bits2 = vec![true, false, true, false, false, false, false, false, false];
> let x2 = Bits::from(bits2);
> 
> assert_eq!(x2.len(), 9);
> assert_eq!(x2, Bits::slice(&[0x05, 0x00], 9));
> ```

## `impl From<Vec<u8>> for Bits`

---

> ```rust
> fn from(bytes: Vec<u8>) -> Self
> ```
> 
> Converts to this type from the input type.


## `impl FromIterator<bool> for Bits`

---

> ```rust
> fn from_iter<I: IntoIterator<Item = bool>>(iter: I) -> Self
> ```
> 
> Creates a value from an iterator. Read more


## `impl FromIterator<u8> for Bits`

---

> ```rust
> fn from_iter<I: IntoIterator<Item = u8>>(iter: I) -> Self
> ```
> 
> Creates a value from an iterator.


## `impl IntoIterator for Bits`

---

> ```rust
> fn into_iter(self) -> Self::IntoIter
> ```
> 
> Creates an iterator from a value.
> 
> ```rust
> type Item = u8
> ```
> 
> The type of the elements being iterated over. 
>  
> ```rust
> type IntoIter = IntoBits
> ```
> 
> Which kind of iterator are we turning this into?

## `impl Not for &Bits`

---

> ```rust
> fn not(self) -> Self::Output
> ```
> 
> Flips every bit.
> 
> ```rust
> type Output = Bits
> ```
> 
> The resulting type after applying the ! operator.
> 
> ```rust
> let x = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> assert_eq!(!&x, Bits::slice(&[0xF5, 0xF4, 0x03], 20));
> ```



## `impl Not for Bits`

---

> ```rust
> fn not(self) -> Self::Output
> ```
> 
> Flips every bit.
> 
> ```rust
> type Output = Bits
> ```
> 
> The resulting type after applying the ! operator.
> 
> ```rust
> let x = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> assert_eq!(!x, Bits::slice(&[0xF5, 0xF4, 0x03], 20));
> ```


## `impl Ord for Bits`

---

> ```rust
> fn cmp(&self, other: &Self) -> Ordering
> ```
> 
> Compares a bit string with another
> 
> ```rust
> let x = Bits::from([0x0A, 0x0B, 0x0C]);
> let y = Bits::from([0x09, 0x0B, 0x0C]);
> let z = Bits::from([0x0A, 0x09, 0x0D]);
> 
> assert_eq!(x.cmp(&y), Ordering::Greater);
> assert_eq!(x.cmp(&z), Ordering::Less);
> ```

> ```rust
> fn max(self, other: Self) -> Self
> where Self: Sized
> ```
> 
> Compares and returns the maximum of two values.

> ```rust
> fn min(self, other: Self) -> Self
> where Self: Sized
> ```
> 
> Compares and returns the minimum of two values.

> ```rust
> fn clamp(self, min: Self, max: Self) -> Self
> where Self: Sized
> ```
> 
> Restrict a value to a certain interval. Read more


## `impl PartialEq for Bits`

---

> ```rust
> fn eq(&self, other: &Self) -> bool
> ```
> 
> Whether two bit strings are equal.
> 
> ```rust
> let x = Bits::from([0x20, 0x30, 0x40]);
> 
> assert!(Bits::eq(&x, &x));
> 
> let y = Bits::from([0xA0, 0xB0, 0xC0]);
> 
> assert!(Bits::ne(&x, &y));
> 
> let z1 = Bits::from([0x20, 0x30, 0x40, 0x00]);
> 
> assert!(Bits::eq(&x, &z1));
> 
> let z2 = Bits::new([0x20, 0x30, 0x40, 0x00]);
> 
> assert!(Bits::ne(&x, &z2));
> ```

> ```rust
> fn ne(&self, other: &Rhs) -> bool
> ```
> 
> Tests for !=. The default implementation is almost always sufficient, and should not be overridden without very good reason.

## `impl PartialOrd for Bits`

---

> ```rust
> fn partial_cmp(&self, other: &Self) -> Option<Ordering>
> ```
> 
> Compares a bit string with another
> 
> ```rust
> 
> let x = Bits::from([0x0A, 0x0B, 0x0C]);
> let y = Bits::from([0x09, 0x0B, 0x0C]);
> let z = Bits::from([0x0A, 0x09, 0x0D]);
> 
> assert_eq!(x.partial_cmp(&y), Some(Ordering::Greater));
> assert_eq!(x.partial_cmp(&z), Some(Ordering::Less));
> ```

> ```rust
> fn lt(&self, other: &Rhs) -> bool
> ```
> 
> Tests less than (for self and other) and is used by the < operator.

> ```rust
> fn le(&self, other: &Rhs) -> bool
> ```
> 
> Tests less than or equal to (for self and other) and is used by the <= operator.

> ```rust
> fn gt(&self, other: &Rhs) -> bool
> ```
> 
> Tests greater than (for self and other) and is used by the > operator. 

> ```rust
> fn ge(&self, other: &Rhs) -> bool
> ```
> 
> Tests greater than or equal to (for self and other) and is used by the >= operator.


## `impl Shl<&usize> for &Bits`

---

> ```rust
> fn shl(self, count: &usize) -> Self::Output
> ```
> 
> Shifts out upper bits, shifting in zeros on the lower end.
> 
> ```rust
> let x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> let s1 = &x1 << &17;
> 
> assert_eq!(s1, Bits::slice(&[0x00, 0x00, 0x04], 20));
> assert_eq!(s1.len(), x1.len());
> 
> let x2 = Bits::new([0x0A, 0x0B, 0x0C]);
> let s2 = &x2 << &4;
> 
> assert_eq!(s2, Bits::new([0xA0, 0xB0, 0xC0]));
> assert_eq!(s2.len(), x2.len());
> ```
> 
> ```rust
> type Output = Bits
> ```
> 
> The resulting type after applying the << operator.


## `impl Shl<&usize> for Bits`

---

> ```rust
> fn shl(self, count: &usize) -> Self::Output
> ```
> 
> Shifts out upper bits, shifting in zeros on the lower end.
> 
> ```rust
> let x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> let s1 = x1 << &17;
> 
> assert_eq!(s1, Bits::slice(&[0x00, 0x00, 0x04], 20));
> assert_eq!(s1.len(), 20);
> 
> let x2 = Bits::new([0x0A, 0x0B, 0x0C]);
> let s2 = x2 << &4;
> 
> assert_eq!(s2, Bits::new([0xA0, 0xB0, 0xC0]));
> assert_eq!(s2.len(), 24);
> ```
> 
> ```rust
> type Output = Bits
> ```
> 
> The resulting type after applying the << operator.


## `impl Shl<usize> for &Bits`

---

> ```rust
> fn shl(self, count: usize) -> Self::Output
> ```
> 
> Shifts out upper bits, shifting in zeros on the lower end.
> 
> ```rust
> let x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> let s1 = &x1 << 17;
> 
> assert_eq!(s1, Bits::slice(&[0x00, 0x00, 0x04], 20));
> assert_eq!(s1.len(), x1.len());
> 
> let x2 = Bits::new([0x0A, 0x0B, 0x0C]);
> let s2 = &x2 << 4;
> 
> assert_eq!(s2, Bits::new([0xA0, 0xB0, 0xC0]));
> assert_eq!(s2.len(), x2.len());
> ```
> 
> ```rust
> type Output = Bits
> ```
> 
> The resulting type after applying the << operator.

## `impl Shl<usize> for Bits`

---

> ```rust
> fn shl(self, count: usize) -> Self::Output
> ```
> 
> Shifts out upper bits, shifting in zeros on the lower end.
> 
> ```rust
> let x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> let s1 = x1 << 17;
> 
> assert_eq!(s1, Bits::slice(&[0x00, 0x00, 0x04], 20));
> assert_eq!(s1.len(), 20);
> 
> let x2 = Bits::new([0x0A, 0x0B, 0x0C]);
> let s2 = x2 << 4;
> 
> assert_eq!(s2, Bits::new([0xA0, 0xB0, 0xC0]));
> assert_eq!(s2.len(), 24);
> ```
> 
> ```rust
> type Output = Bits
> ```
> 
> The resulting type after applying the << operator.


## `impl ShlAssign<&usize> for Bits`

---

> ```rust
> fn shl_assign(&mut self, count: &usize)
> ```
> 
> Shifts out upper bits, shifting in zeros on the lower end.
> 
> ```rust
> let mut x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x1 <<= &17;
> 
> assert_eq!(x1, Bits::slice(&[0x00, 0x00, 0x04], 20));
> assert_eq!(x1.len(), 20);
> 
> let mut x2 = Bits::new([0x0A, 0x0B, 0x0C]);
> 
> x2 <<= &4;
> 
> assert_eq!(x2, Bits::new([0xA0, 0xB0, 0xC0]));
> assert_eq!(x2.len(), 24);
> ```

## `impl ShlAssign<usize> for Bits`

---

> ```rust
> fn shl_assign(&mut self, count: usize)
> ```
> 
> Shifts out upper bits, shifting in zeros on the lower end.
> 
> ```rust
> let mut x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x1 <<= 17;
> 
> assert_eq!(x1, Bits::slice(&[0x00, 0x00, 0x04], 20));
> assert_eq!(x1.len(), 20);
> 
> let mut x2 = Bits::new([0x0A, 0x0B, 0x0C]);
> 
> x2 <<= 4;
> 
> assert_eq!(x2, Bits::new([0xA0, 0xB0, 0xC0]));
> assert_eq!(x2.len(), 24);
> ```

## `impl Shr<&usize> for &Bits`

---

> ```rust
> fn shr(self, count: &usize) -> Self::Output
> ```
> 
> Shifts out lower bits, shifting zeros into the upper bits.
> 
> ```rust
> let x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> let s1 = &x1 >> &17;
> 
> assert_eq!(s1.len(), x1.len());
> assert_eq!(s1, Bits::slice(&[0x06, 0x00, 0x00], 20));
> 
> let x2 = Bits::new([0x0A, 0x0B, 0x0C]);
> let s2 = &x2 >> &4;
> 
> assert_eq!(s2.len(), 24);
> assert_eq!(s2, Bits::new([0xB0, 0xC0, 0x00]));
> ```
> 
> ```rust
> type Output = Bits
> ```
> 
> The resulting type after applying the >> operator.


## `impl Shr<&usize> for Bits`

---

> ```rust
> fn shr(self, count: &usize) -> Self::Output
> ```
> 
> Shifts out lower bits, shifting zeros into the upper bits.
> 
> ```rust
> let x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> let s1 = x1 >> &17;
> 
> assert_eq!(s1.len(), 20);
> assert_eq!(s1, Bits::slice(&[0x06, 0x00, 0x00], 20));
> 
> let x2 = Bits::new([0x0A, 0x0B, 0x0C]);
> let s2 = x2 >> &4;
> 
> assert_eq!(s2.len(), 24);
> assert_eq!(s2, Bits::new([0xB0, 0xC0, 0x00]));
> ```
> 
> ```rust
> type Output = Bits
> ```
> 
> The resulting type after applying the >> operator.

## `impl Shr<usize> for &Bits`

---

> ```rust
> fn shr(self, count: usize) -> Self::Output
> ```
> 
> Shifts out lower bits, shifting zeros into the upper bits.
> 
> ```rust
> let x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> let s1 = &x1 >> 17;
> 
> assert_eq!(s1.len(), x1.len());
> assert_eq!(s1, Bits::slice(&[0x06, 0x00, 0x00], 20));
> 
> let x2 = Bits::new([0x0A, 0x0B, 0x0C]);
> let s2 = &x2 >> 4;
> 
> assert_eq!(s2.len(), x2.len());
> assert_eq!(s2, Bits::new([0xB0, 0xC0, 0x00]));
> ```
> 
> ```rust
> type Output = Bits
> ```
> 
> The resulting type after applying the >> operator.


## `impl Shr<usize> for Bits`

---

> ```rust
> fn shr(self, count: usize) -> Self::Output
> ```
> 
> Shifts out lower bits, shifting zeros into the upper bits.
> 
> ```rust
> let x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> let s1 = x1 >> 17;
> 
> assert_eq!(s1.len(), 20);
> assert_eq!(s1, Bits::slice(&[0x06, 0x00, 0x00], 20));
> 
> let x2 = Bits::new([0x0A, 0x0B, 0x0C]);
> let s2 = x2 >> 4;
> 
> assert_eq!(s2.len(), 24);
> assert_eq!(s2, Bits::new([0xB0, 0xC0, 0x00]));
> ```
> 
> ```rust
> type Output = Bits
> ```
> 
> The resulting type after applying the >> operator.


## `impl ShrAssign<&usize> for Bits`

---

> ```rust
> fn shr_assign(&mut self, count: &usize)
> ```
> 
> Shifts out lower bits, shifting zeros into the upper bits.
> 
> ```rust
> let mut x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x1 >>= &17;
> 
> assert_eq!(x1.len(), 20);
> assert_eq!(x1, Bits::slice(&[0x06, 0x00, 0x00], 20));
> 
> let mut x2 = Bits::new([0x0A, 0x0B, 0x0C]);
> 
> x2 >>= &4;
> 
> assert_eq!(x2.len(), 24);
> assert_eq!(x2, Bits::new([0xB0, 0xC0, 0x00]));
> ```

## `impl ShrAssign<usize> for Bits`

---

> ```rust
> fn shr_assign(&mut self, count: usize)
> ```
> 
> Shifts out lower bits, shifting zeros into the upper bits.
> 
> ```rust
> let mut x1 = Bits::from([0x0A, 0x0B, 0x0C]);
> 
> x1 >>= 17;
> 
> assert_eq!(x1, Bits::slice(&[0x06, 0x00, 0x00], 20));
> assert_eq!(x1.len(), 20);
> 
> let mut x2 = Bits::new([0x0A, 0x0B, 0x0C]);
> 
> x2 >>= 4;
> 
> assert_eq!(x2, Bits::new([0xB0, 0xC0, 0x00]));
> assert_eq!(x2.len(), 24);
> ```

## `impl Eq for Bits`

## `impl Send for Bits`

## `impl Sync for Bits`