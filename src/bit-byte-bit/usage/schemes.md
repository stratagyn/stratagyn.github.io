# Bit Schemes

[Scheme](/bit-byte-bit/reference/scheme.md) implements a simple bit string pattern matcher inspired by Erlang's
bit syntax. Schemes are used to give meaning to different regions of a bit string.

### Example

---

`ipv4_header_scheme` will define the part of the IPv4 datagram header that does not include the options. 
This scheme will then be used to process more bits from the bit string. `Scheme::split_*` methods return a vector
of `Bits` corresponding to each field. `Scheme::extract_from_*` methods return a hashmap, corresponding each
field with a key.

```rust
# use bit_byte_bit::{Bits, bits_as, Field, Scheme};
const IPV4_HEADER_BIT_LEN: usize = 160;
const IPV4_HEADER_BYTE_LEN: usize = 20;

const IPV4_HEADER_KEYS: [&str; 13] = [
    "Version",
    "IHL",
    "DSCP",
    "ECN",
    "Total Length",
    "Identification",
    "Flags",
    "Fragment Offset",
    "TTL",
    "Protocol",
    "Header Checksum",
    "Source Address",
    "Destination Address"
];

let ipv4_header_scheme: Scheme = Scheme::new([ 
    Field::UNSIGNED_4,    // Version
    Field::UNSIGNED_4,    // Internet Header Length
    Field::unsigned(6),   // Differentiated Services Code Point
    Field::UNSIGNED_2,    // Explicit Congestion Notification
    Field::UNSIGNED_16,   // Total Length
    Field::UNSIGNED_16,   // Identification
    Field::unsigned(3),   // Flags
    Field::unsigned(13),  // Fragment Offset
    Field::UNSIGNED_8,    // Time To Live
    Field::UNSIGNED_8,    // Protocol
    Field::UNSIGNED_16,   // Header Checksum
    Field::UNSIGNED_32,   // Source Address
    Field::UNSIGNED_32    // Destination Address
]);

let bits = Bits::new([
   0x54, 0x00, 0x34, 0x00, 0x16, 0x41, 0x02, 0x00,
   128, 6, 0, 0, 192, 168, 5, 45, 91, 198, 174, 192
]);

let mut data = ipv4_header_scheme.extract_from_bits(&bits, &IPV4_HEADER_KEYS);

let total_length = bits_as::unsigned(&data[&"Total Length"]);
let header_32_bit_len = bits_as::unsigned(&data[&"IHL"]);
let options_byte_len = (header_32_bit_len - 5) * 4;
let options_bit_len = options_byte_len * 8;
let options = Bits::take(bits.bytes(), IPV4_HEADER_BIT_LEN, options_bit_len);
let payload_start = IPV4_HEADER_BIT_LEN + options_bit_len;
let payload_bit_len = (total_length - IPV4_HEADER_BYTE_LEN - options_byte_len) * 8;
let payload = Bits::take(bits.bytes(), IPV4_HEADER_BIT_LEN + options_bit_len, payload_bit_len);

assert_eq!(bits_as::uint8(&data[&"Version"]), 4);
assert_eq!(bits_as::uint8(&data[&"IHL"]), 5);
assert_eq!(bits_as::uint8(&data[&"DSCP"]), 0);
assert_eq!(bits_as::uint8(&data[&"ECN"]), 0);
assert_eq!(bits_as::uint16(&data[&"Total Length"]), 52);
assert_eq!(bits_as::uint16(&data[&"Identification"]), 0x4116);
assert_eq!(bits_as::uint8(&data[&"Flags"]), 2);
assert_eq!(bits_as::uint16(&data[&"Fragment Offset"]), 0);
assert_eq!(bits_as::uint8(&data[&"TTL"]), 128);
assert_eq!(bits_as::uint8(&data[&"Protocol"]), 6);
assert_eq!(bits_as::uint16(&data[&"Header Checksum"]), 0);
assert_eq!(bits_as::vec_u8(&data[&"Source Address"]), vec![192, 168, 5, 45]);
assert_eq!(bits_as::vec_u8(&data[&"Destination Address"]), vec![91, 198, 174, 192]);
assert_eq!(options, Bits::empty());
assert_eq!(payload, Bits::zeros(8 * 32));
```