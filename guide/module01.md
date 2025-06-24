# Module 01: Setting up utility functions

Before we can get started writing WebAssembly, we need to first set some utility functions.

<br>

Our first two utility functions will be the unsigned and signed variants for LEB128 encoding.

The WebAssembly specification declares that all integers must be encoded using the LEB128 variable-length integer encoding. This is because LEB128 encoding allows you to store large integers into a small number of bytes. For small numbers though, those are left as a single byte and no encoding is done. <a href="https://en.wikipedia.org/wiki/LEB128">Here is a wikipedia article if you want to read more about it.</a>

The wikipedia article also provides c-like psuedocode and javascript implementations for encoding signed and unsigned 32-bit integers.

Here is the javascript implementation for encoding a signed 32-bit integer.

```
const encodeSignedLeb128FromInt32 = (value) => {
  value |= 0;
  const result = [];
  while (true) {
    const byte_ = value & 0x7f;
    value >>= 7;
    if (
      (value === 0 && (byte_ & 0x40) === 0) ||
      (value === -1 && (byte_ & 0x40) !== 0)
    ) {
      result.push(byte_);
      return result;
    }
    result.push(byte_ | 0x80);
  }
};
```

The wikipedia article doesn't have an implementation for unsigned 32-bit integers, but luckily they have an implementation in c-like psuedocode. With help from <a href="https://blog.nthia.dev/writing-wasm-as-raw-bytes.html">https://blog.nthia.dev/writing-wasm-as-raw-bytes.html</a> we are able to create the javascript implementation.

```
const encodeUnsignedLeb128FromInt32 = (value) => {
  value |= 0;
  const result = [];
  do {
    let byte_ = value & 0x7f
    value >>= 7;
    if (value != 0) {
      byte_ |= 0x80
    }
    result.push(byte_)
  } while (value != 0)
  return result
}
```

Let's also have a function to encode strings into bytes.

```
const convertStringToByte = (string) => {
  const encoder = new TextEncoder()
  return Array.from(encoder.encode(string))
}
```

All we do here, is encode a string, then convert it into an array. We convert it into an array, since at the end is when we will convert into an Uint8Array.

Finally, we will want to add a function for encoding vectors. According to the <a href="https://webassembly.github.io/spec/core/binary/conventions.html#vectors">WebAssembly spec</a>, "Vectors are encoded with their u32 length followed by the encoding of their element sequence." This just means that every vector must have their length first in u32, then their content.

```
const encodeVector() = (things) => {
  return [
    encodeUnsignedLeb128FromInt32(things.length),
    things
  ]
}
```
