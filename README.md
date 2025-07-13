# Monorail Quote SDK

A TypeScript/JavaScript SDK for interacting with the Monorail Quote API, enabling you to fetch swap quotes, routes, and transaction data for EVM-compatible tokens.

## Features
- Fetch swap quotes between EVM tokens
- Get detailed route and fee breakdowns
- Generate transaction data for execution
- TypeScript support

## Installation

```bash
npm install @santi-dev/monorail-quote-sdk
```

## Usage

```typescript
import { Client } from '@santi-dev/monorail-quote-sdk/dist/monorail-quote-sdk';

const client = new Client(); // Optionally pass a custom baseUrl

async function getQuote() {
  try {
    const quote = await client.quote(
      'your-app-id', // source (App ID)
      '0xTokenFrom',  // from token address
      '0xTokenTo',    // to token address
      '1.5',          // amount (human readable)
      '0xSender',     // sender address (optional)
      50,             // max_slippage in bps (optional)
      60,             // deadline in seconds (optional)
      '0xDestination' // destination address (optional)
    );
    console.log(quote);
  } catch (e) {
    console.error(e);
  }
}

getQuote();
```

## API

### `Client`

#### Constructor
```typescript
new Client(baseUrl?: string, instance?: AxiosInstance)
```
- `baseUrl` (optional): Override the default API endpoint.
- `instance` (optional): Provide a custom Axios instance.

#### Methods

##### `quote(...)`
Fetch a quote for swapping tokens.

```typescript
quote(
  source: string,         // App ID
  from: string,           // From token address (EVM)
  to: string,             // To token address (EVM)
  amount: string,         // Amount to trade (human readable)
  sender?: string,        // Sender address (optional)
  max_slippage?: number,  // Max slippage in bps (optional, default 50)
  deadline?: number,      // Deadline in seconds (optional, default 60)
  destination?: string,   // Destination address (optional)
  cancelToken?: CancelToken // Axios cancel token (optional)
): Promise<QuoteOutputV4>
```

Returns a `QuoteOutputV4` object with details about the quote, including routes, fees, and transaction data.

### Types
- `QuoteOutputV4`: Full quote response (amounts, routes, transaction, etc.)
- `ProtocolFeesV4`: Protocol and referrer fee details
- `GeneratedTransaction`: Transaction data for execution
- `Route`, `Split`: Route and split details
- `ErrorResponse`: Error details

## Building

To build the SDK from source:

```bash
npm run build
```

## Requirements
- Node.js >= 14
- TypeScript >= 5.2 (for development)

## License

MIT

## Author

Santi

## Repository

[https://github.com/SantiSjp/monorail-quote-sdk](https://github.com/SantiSjp/monorail-quote-sdk) 