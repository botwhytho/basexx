#basexx

A Lua library which provides base2(bitfield), base16(hex), base32(crockford/rfc), base64 decoding and encoding.

##from_bit / to_bit

Converts a byte string to a bitfield string.

* 0, O and o maps to the same value
* 1, I, i, L and l maps to the same value

<!-- mou problem -->

    basexx.to_bit( "ACDC" ) --> 01000001010000110100010001000011
    basexx.from_bit( "01000001010000110100010001000011" ) --> ACDC
    basexx.from_bit( "o1ooooo1o1oooo11" ) --> AC
    basexx.from_bit( "OioooooiOiooooii" ) --> AC

##from_hex / to_hex

Converts a byte string to a uppercase [hex](http://tools.ietf.org/html/rfc3548#section-6) data string.

    basexx.to_hex( "Hello world!" ) --> 48656C6C6F20776F726C6421
    basexx.from_hex( "48656C6C6F20776F726C6421" ) --> Hello world!
    basexx.from_hex( "48656c6c6f20776f726c6421" ) --> Hello world!

##from_base32 / to_base32

Converts a byte string to a [base32(_rfc3548_)](http://tools.ietf.org/html/rfc3548#section-5) uppercase data string.

* It's case insensitive

<!-- mou problem -->

    basexx.to_base32( "chunky bacon!" ) --> MNUHK3TLPEQGEYLDN5XCC===
	 basexx.from_base32( "MNUHK3TLPEQGEYLDN5XCC===" ) --> chunky bacon!

##from_crockford / to_crockford

Converts a byte string to a [base32(_crockford_)](http://www.crockford.com/wrmg/base32.html) uppercase data string. The optional check value is not implemented. 

* It's case insensitive
* 1, I, i, L and l maps to the same value
* 0, O and o maps to the same value
* U, u, V and v maps to the same value (not part of the official description)

<!-- mou problem -->

    string.lower( basexx.to_crockford( "Hello World" ) ) --> 91jprv3f41bpywkccg
    basexx.from_crockford( "axqqeb10d5u20wk5c5p6ry90exqq4uvk44" ) --> Wow, it really works!

##from_base64 / to_base64

Converts a byte string to a [base64](https://tools.ietf.org/html/rfc4648#section-4) data string.

    basexx.to_base64( "Man") --> TWFu
	 basexx.from_base64( "TWFu" ) --> Man

##from_url64 / to_url64

Same as above, but uses a [URL Safe base64](https://tools.ietf.org/html/rfc4648#section-5) alphabet and no padding.

##from_z85 / to_z85

Converts a byte string to a [Base85(ZeroMQ)](http://rfc.zeromq.org/spec:32) data string.
to_z85 expects only a binary string that length is divisible by 4 with no remainder, and from_z85 expects only printable a string that length is divisible by 5 with no remainder.

    basexx.to_z85( "1234" ) --> f!$Kw
    basexx.from_z85( "f!$Kw" ) --> 1234
   
