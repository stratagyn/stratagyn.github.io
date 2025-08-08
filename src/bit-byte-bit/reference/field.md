# `Field`

---

```rust
pub struct Field { ... }
```

Defines a region of bits.

Each field has a unit, size, and a flag indicating if the field represents a signed integer. The unit is the minimum
number of bits extracted by the field. The size is the total number of units extracted by the field.

The flag comes into play when a field extracts more bits than are available. If at least one bit is still available 
and the flag is true, the bit string is sign extended to the length of the field.

# Constants

---

Common field types.

|       Constant       | Unit |   Size  | Signed |
|----------------------|:----:|:-------:|:------:|
| `Field::BIT`         |  1   |    1    |
| `Field::BYTES`       |  8   | UNBOUND |
| `Field::SIGNED`      |  1   | UNBOUND |   X
| `Field::SIGNED_2`    |  1   |    2    |   X
| `Field::SIGNED_4`    |  1   |    4    |   X
| `Field::SIGNED_8`    |  1   |    8    |   X
| `Field::SIGNED_16`   |  1   |    16   |   X
| `Field::SIGNED_32`   |  1   |    32   |   X
| `Field::SIGNED_64`   |  1   |    64   |   X
| `Field::UNSIGNED`    |  1   | UNBOUND |
| `Field::UNSIGNED_2`  |  1   |    2    |
| `Field::UNSIGNED_4`  |  1   |    4    |
| `Field::UNSIGNED_8`  |  1   |    8    |
| `Field::UNSIGNED_16` |  1   |    16   |
| `Field::UNSIGNED_32` |  1   |    32   |
| `Field::UNSIGNED_64` |  1   |    64   |

# Implementation

> ```rust
> pub fn aligned(unit: usize, size: isize, signed: bool) -> Self
> ```
> 
> Bit field aligned to a given unit
> 
> When m and n are negative Bits::aligned(m, signed) == Bits::aligned(n, signed), even if m != n.
> 
> 
> ```rust
> let field = Field::aligned(7, 48, false);
> 
> assert_eq!(field.unit(), 7);
> assert_eq!(field.size(), 48);
> assert_eq!(field.len(), 48 * 7);
> 
> let mfield = Field::aligned(7, -1, true);
> let nfield = Field::aligned(7, isize::MIN, true);
> 
> assert_eq!(mfield, nfield);
> assert_eq!(mfield.size(), -1);
> assert_eq!(nfield.size(), -1);
> assert!(mfield.is_signed());
> ```

> ```rust
> pub fn bytes(size: isize, signed: bool) -> Self
> ```
> 
> Byte-aligned bit field
> 
> When m and n are negative Bits::bytes(m, signed) == Bits::bytes(n, signed), even if m != n.
> 
> ```rust
> let field = Field::bytes(48, false);
> 
> assert_eq!(field.unit(), 8);
> assert_eq!(field.size(), 48);
> assert_eq!(field.len(), 48 * 8);
> 
> let mfield = Field::bytes(-1, true);
> let nfield = Field::bytes(isize::MIN, true);
> 
> assert_eq!(mfield, nfield);
> assert_eq!(mfield.size(), -1);
> assert_eq!(nfield.size(), -1);
> assert!(mfield.is_signed());
> ```

> ```rust
> pub fn signed(size: isize) -> Self
> ```
> 
> Bit field
> 
> When m and n are negative Bits::bits(m, signed) == Bits::bits(n, signed), even if m != n.
> 
> ```rust
> let field = Field::signed(96);
> 
> assert_eq!(field.unit(), 1);
> assert_eq!(field.size(), 96);
> assert_eq!(field.len(), 96);
> assert!(field.is_signed());
> 
> let mfield = Field::signed(-1);
> let nfield = Field::signed(isize::MIN);
> 
> assert_eq!(mfield, nfield);
> assert_eq!(mfield.size(), -1);
> assert_eq!(nfield.size(), -1);
> assert!(mfield.is_signed());
> ```

> ```rust
> pub fn unsigned(size: isize) -> Self
> ```
> 
> Bit field
> 
> When m and n are negative Bits::bits(m, signed) == Bits::bits(n, signed), even if m != n.
> 
> 
> ```rust
> 
> let field = Field::unsigned(96);
> assert_eq!(field.unit(), 1);
> assert_eq!(field.size(), 96);
> assert_eq!(field.len(), 96);
> assert!(!field.is_signed());
> 
> let mfield = Field::unsigned(-1);
> let nfield = Field::unsigned(isize::MIN);
> 
> assert_eq!(mfield, nfield);
> assert_eq!(mfield.size(), -1);
> assert_eq!(nfield.size(), -1);
> assert!(!mfield.is_signed());
> ```

> ```rust
> pub fn is_signed(&self) -> bool
> ```
> 
> Whether this field represents a signed integer.
> 
> ```rust
> assert!(Field::aligned(7, 48, true).is_signed());
> assert!(!Field::aligned(7, 48, false).is_signed());
> assert!(Field::bytes(-1, true).is_signed());
> assert!(!Field::bytes(-1, false).is_signed());
> assert!(Field::signed(96).is_signed());
> assert!(!Field::unsigned(96).is_signed());
> ```

> ```rust
> pub fn len(&self) -> isize
> ```
> 
> Number of bits extracted by the field
> 
> -1 means that the field extracts the maximum number of bits that can be divided by the unit of the field. Extraction never exceeds the remaining the number of bits.
> 
> ```rust
> assert_eq!(Field::aligned(0, -1, true).len(), 0);
> assert_eq!(Field::aligned(7, 0, false).len(), 0);
> assert_eq!(Field::aligned(7, 48, true).len(), 48 * 7);
> assert_eq!(Field::aligned(7, -1, false).len(), -1);
> assert_eq!(Field::aligned(7, isize::MIN, true).len(), -1);
> assert_eq!(Field::bytes(48, true).len(), 48 * 8);
> assert_eq!(Field::bytes(-1, false).len(), -1);
> assert_eq!(Field::bytes(isize::MIN, true).len(), -1);
> assert_eq!(Field::signed(48).len(), 48);
> assert_eq!(Field::signed(-1).len(), -1);
> assert_eq!(Field::signed(isize::MIN).len(), -1);
> assert_eq!(Field::unsigned(48).len(), 48);
> assert_eq!(Field::unsigned(-1).len(), -1);
> assert_eq!(Field::unsigned(isize::MIN).len(), -1);
> ```

> ```rust
> pub fn size(&self) -> isize
> ```
> 
> Number of units in the field
> 
> ```rust
> assert_eq!(Field::aligned(7, 48, true).size(), 48);
> assert_eq!(Field::aligned(7, -1, false).size(), -1);
> assert_eq!(Field::aligned(7, isize::MIN, true).size(), -1);
> assert_eq!(Field::bytes(48, true).size(), 48);
> assert_eq!(Field::bytes(-1, false).size(), -1);
> assert_eq!(Field::bytes(isize::MIN, true).size(), -1);
> assert_eq!(Field::signed(48).size(), 48);
> assert_eq!(Field::signed(-1).size(), -1);
> assert_eq!(Field::signed(isize::MIN).size(), -1);
> assert_eq!(Field::unsigned(48).size(), 48);
> assert_eq!(Field::unsigned(-1).size(), -1);
> assert_eq!(Field::unsigned(isize::MIN).size(), -1);
> ```

> ```rust
> pub fn unit(&self) -> usize
> ```
> 
> Minimum number of bits extracted by the field.
> 
> ```rust
> 
> assert_eq!(Field::aligned(7, 48, true).unit(), 7);
> assert_eq!(Field::aligned(7, -1, false).unit(), 7);
> assert_eq!(Field::aligned(7, isize::MIN, true).unit(), 7);
> assert_eq!(Field::bytes(48, true).unit(), 8);
> assert_eq!(Field::bytes(-1, false).unit(), 8);
> assert_eq!(Field::bytes(isize::MIN, true).unit(), 8);
> assert_eq!(Field::signed(48).unit(), 1);
> assert_eq!(Field::signed(-1).unit(), 1);
> assert_eq!(Field::signed(isize::MIN).unit(), 1);
> assert_eq!(Field::unsigned(48).unit(), 1);
> assert_eq!(Field::unsigned(-1).unit(), 1);
> assert_eq!(Field::unsigned(isize::MIN).unit(), 1);
> ```

# Traits

---

## `Clone`

---

> ```rust
> fn clone(&self) -> Field
> ```
> 
> Returns a copy of the value.

> ```rust
> fn clone_from(&mut self, source: &Self)
> ```
> 
> Performs copy-assignment from source.

## `Debug`

---

> ```rust
> fn fmt(&self, f: &mut Formatter<'_>) -> Result
> ```
> 
> Formats the value using the given formatter. Read more

## `PartialEq`

---

> ```rust
> fn eq(&self, other: &Field) -> bool
> ```
> 
> Tests for self and other values to be equal, and is used by ==.

> ```rust
> fn ne(&self, other: &Rhs) -> bool
> ```
> 
> Tests for !=. The default implementation is almost always sufficient, and should not be overridden without very good reason.


## `Copy`

## `Eq`
