# APDU

Rust-like APDU protocol for TypeScript

```bash
npm i @hazae41/apdu
```

[**Node Package 📦**](https://www.npmjs.com/package/@hazae41/apdu)

## Features

### Current features
- 100% TypeScript and ESM
- No external dependencies
- Rust-like patterns
- Uses `@hazae41/result`

## Usage

### Request and response

```tsx
import { ApduRequest, ApduResponse } from "@hazae41/apdu"
import { Readable, Writable, Empty } from "@hazae41/binary"

function send(bytes: Uint8Array): Promise<Uint8Array>;

const request = ApduRequest.fromOrThrow({ cla: 0xe0, ins: 0x06, p1: 0x00, p2: 0x00, fragment: new Empty() })
const output = Writable.writeToBytesOrThrow(request)
const input = await send(output)
const response = Readable.readFromBytesOrThrow(ApduResponse, input)

if (response.isOk())
  console.log(response.get())
else
  console.error(response.getErr())
```