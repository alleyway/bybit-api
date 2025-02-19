# Node.js & Typescript Bybit API SDK

[![Tests](https://circleci.com/gh/tiagosiebler/bybit-api.svg?style=shield)](https://circleci.com/gh/tiagosiebler/bybit-api)
[![npm version](https://img.shields.io/npm/v/bybit-api)][1] [![npm size](https://img.shields.io/bundlephobia/min/bybit-api/latest)][1] [![npm downloads](https://img.shields.io/npm/dt/bybit-api)][1]
[![last commit](https://img.shields.io/github/last-commit/tiagosiebler/bybit-api)][1]
[![CodeFactor](https://www.codefactor.io/repository/github/tiagosiebler/bybit-api/badge)](https://www.codefactor.io/repository/github/tiagosiebler/bybit-api)

[![connector logo](https://github.com/tiagosiebler/bybit-api/blob/master/docs/images/logo1.png?raw=true)][1]

[1]: https://www.npmjs.com/package/bybit-api

Node.js SDK for the Bybit APIs and WebSockets:

- Complete integration with all Bybit APIs.
- TypeScript support (with type declarations for most API requests & responses).
- Over 450 end-to-end tests making real API calls & WebSocket connections, validating any changes before they reach npm.
- Robust WebSocket integration with configurable connection heartbeats & automatic reconnect then resubscribe workflows.
- Browser support (via webpack bundle - see "Browser Usage" below).

## Installation

`npm install --save bybit-api`

## Issues & Discussion

- Issues? Check the [issues tab](https://github.com/tiagosiebler/bybit-api/issues).
- Discuss & collaborate with other node devs? Join our [Node.js Algo Traders](https://t.me/nodetraders) engineering community on telegram.

## Related projects

Check out my related projects:

- Try my connectors:
  - [binance](https://www.npmjs.com/package/binance)
  - [bybit-api](https://www.npmjs.com/package/bybit-api)
  - [okx-api](https://www.npmjs.com/package/okx-api)
  - [bitget-api](https://www.npmjs.com/package/bitget-api)
  - [ftx-api](https://www.npmjs.com/package/ftx-api)
- Try my misc utilities:
  - [orderbooks](https://www.npmjs.com/package/orderbooks)
- Check out my examples:
  - [awesome-crypto-examples](https://github.com/tiagosiebler/awesome-crypto-examples)

## Documentation

Most methods accept JS objects. These can be populated using parameters specified by Bybit's API documentation, or check the type definition in each class within the github repository (see table below for convenient links to each class).

- [Bybit API Docs (choose API category from the tabs at the top)](https://bybit-exchange.github.io/docs/v5/intro).

## Structure

This connector is fully compatible with both TypeScript and pure JavaScript projects, while the connector is written in TypeScript. A pure JavaScript version can be built using `npm run build`, which is also the version published to [npm](https://www.npmjs.com/package/bybit-api).

The version on npm is the output from the `build` command and can be used in projects without TypeScript (although TypeScript is definitely recommended).

- [src](./src) - the whole connector written in TypeScript
- [lib](./lib) - the JavaScript version of the project (built from TypeScript). This should not be edited directly, as it will be overwritten with each release.
- [dist](./dist) - the webpack bundle of the project for use in browser environments (see guidance on webpack below).
- [examples](./examples) - some implementation examples & demonstrations. Contributions are welcome!

---

## REST API Clients

Bybit has several API groups (originally one per product). Each generation is labelled with the version number (e.g. v1/v2/v3/v5). Some of the newer API groups can only be used by upgrading your account to the unified account, but doing so will prevent you from using the V1 and V2 APIs.

Refer to the [V5 upgrade guide](https://bybit-exchange.github.io/docs/v5/upgrade-guide) for more information on requirements to use each API group. If you have a choice, you should use the newest generation that is available (e.g. use the V5 instead of the V3 APIs if you can).

Here are the available REST clients and the corresponding API groups described in the documentation:
| Class | Description |
|:------------------------------------------------------------------: |:----------------------------------------------------------------------------------------------------------------------------: |
| [ **V5 API** ] | The new unified V5 APIs (successor to previously fragmented APIs for all API groups). To learn more about the V5 API, please read the [V5 upgrade guideline](https://bybit-exchange.github.io/docs/v5/upgrade-guide). |
| [RestClientV5](src/rest-client-v5.ts) | Unified V5 all-in-one REST client for all [V5 REST APIs](https://bybit-exchange.github.io/docs/v5/intro) |
| [ **Derivatives v3** ] | The Derivatives v3 APIs (successor to the Futures V2 APIs) |
| [UnifiedMarginClient](src/unified-margin-client.ts) | [Derivatives (v3) Unified Margin APIs](https://bybit-exchange.github.io/docs/derivatives/unified/place-order) |
| [ContractClient](src/contract-client.ts) | [Derivatives (v3) Contract APIs](https://bybit-exchange.github.io/docs/derivatives/contract/place-order). |
| [ **Futures v2** ] | The Futures v2 APIs |
| Deprecated! ContractClient or RestClientV5 recommended | Please read the [V5 upgrade guideline](https://bybit-exchange.github.io/docs/v5/upgrade-guide) |
| [~InverseClient~](src/inverse-client.ts)| [Inverse Perpetual Futures (v2) APIs](https://bybit-exchange.github.io/docs/futuresV2/inverse/) |
| [~LinearClient~](src/linear-client.ts) | [USDT Perpetual Futures (v2) APIs](https://bybit-exchange.github.io/docs/futuresV2/linear/#t-introduction) |
| [~InverseFuturesClient~](src/inverse-futures-client.ts) | [Inverse Futures (v2) APIs](https://bybit-exchange.github.io/docs/futuresV2/inverse_futures/#t-introduction) |
| [ **Spot** ] | The spot APIs |
| [SpotClientV3](src/spot-client-v3.ts) | [Spot Market (v3) APIs](https://bybit-exchange.github.io/docs/spot/public/instrument) |
| [~SpotClient~](src/spot-client.ts) (deprecated, SpotClientV3 recommended)| [Spot Market (v1) APIs](https://bybit-exchange.github.io/docs/spot/v1/#t-introduction) |
| [ **USDC Contract** ] | The USDC Contract APIs |
| [USDCPerpetualClient](src/usdc-perpetual-client.ts) | [USDC Perpetual APIs](https://bybit-exchange.github.io/docs/usdc/option/?console#t-querydeliverylog) |
| [USDCOptionClient](src/usdc-option-client.ts) | [USDC Option APIs](https://bybit-exchange.github.io/docs/usdc/option/#t-introduction) |
| [ **Other** ] | Other standalone API groups |
| [CopyTradingClient](src/copy-trading-client.ts) | [Copy Trading APIs](https://bybit-exchange.github.io/docs/category/copy-trade) |
| [AccountAssetClientV3](src/account-asset-client-v3.ts) | [Account Asset V3 APIs](https://bybit-exchange.github.io/docs/account-asset/internal-transfer) |
| [~AccountAssetClient~](src/account-asset-client.ts) (deprecated, AccountAssetClientV3 recommended) | [Account Asset V1 APIs](https://bybit-exchange.github.io/docs/account_asset/v1/#t-introduction) |
| [WebsocketClient](src/websocket-client.ts) | All WebSocket Events (Public & Private for all API categories) |

Examples for using each client can be found in:

- the [examples](./examples) folder.
- the [awesome-crypto-examples](https://github.com/tiagosiebler/awesome-crypto-examples) repository.

If you're missing an example, you're welcome to request one. Priority will be given to [github sponsors](https://github.com/sponsors/tiagosiebler).

### Usage

Create API credentials on Bybit's website:

- [Livenet](https://bybit.com/app/user/api-management?affiliate_id=9410&language=en-US&group_id=0&group_type=1)
- [Testnet](https://testnet.bybit.com/app/user/api-management)

All REST clients have can be used in a similar way. However, method names, parameters and responses may vary depending on the API category you're using!

Not sure which function to call or which parameters to use? Click the class name in the table above to look at all the function names (they are in the same order as the official API docs), and check the API docs for a list of endpoints/parameters/responses.

The following is a minimal example for using the REST clients included with this SDK. For more detailed examples, refer to the [examples](./examples/) folder in the repository on GitHub:

```typescript
const {
  InverseClient,
  LinearClient,
  InverseFuturesClient,
  SpotClientV3,
  UnifiedMarginClient,
  USDCOptionClient,
  USDCPerpetualClient,
  AccountAssetClient,
  CopyTradingClient,
  RestClientV5,
} = require('bybit-api');

const restClientOptions = {
  /** Your API key. Optional, if you plan on making private api calls */
  key?: string;

  /** Your API secret. Optional, if you plan on making private api calls */
  secret?: string;

  /** Set to `true` to connect to testnet. Uses the live environment by default. */
  testnet?: boolean;

  /** Override the max size of the request window (in ms) */
  recv_window?: number;

  /** Disabled by default. This can help on machines with consistent latency problems. */
  enable_time_sync?: boolean;

  /** How often to sync time drift with bybit servers */
  sync_interval_ms?: number | string;

  /** Default: false. If true, we'll throw errors if any params are undefined */
  strict_param_validation?: boolean;

  /**
   * Optionally override API protocol + domain
   * e.g baseUrl: 'https://api.bytick.com'
   **/
  baseUrl?: string;

  /** Default: true. whether to try and post-process request exceptions. */
  parse_exceptions?: boolean;
};

const API_KEY = 'xxx';
const API_SECRET = 'yyy';
const useTestnet = false;

const client = new RestClientV5({
  key: API_KEY,
  secret: API_SECRET,
  testnet: useTestnet
},
  // requestLibraryOptions
);

// For public-only API calls, simply don't provide a key & secret or set them to undefined
// const client = new RestClientV5({});

client.getAccountInfo()
  .then(result => {
    console.log("getAccountInfo result: ", result);
  })
  .catch(err => {
    console.error("getAccountInfo error: ", err);
  });

client.getOrderbook({ category: 'linear', symbol: 'BTCUSD' })
  .then(result => {
    console.log("getOrderBook result: ", result);
  })
  .catch(err => {
    console.error("getOrderBook error: ", err);
  });
```

## WebSockets

All API groups can be used via a shared `WebsocketClient`. However, to listen to multiple API groups at once, you will need to make one WebsocketClient instance per API group.

The WebsocketClient can be configured to a specific API group using the market parameter. These are the currently available API groups:
| API Category | Market | Description |
|:----------------------------: |:-------------------: |-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Unified Margin - Options | `market: 'unifiedOption'`| The [derivatives v3](https://bybit-exchange.github.io/docs/derivativesV3/unified_margin/#t-websocket) category for unified margin. Note: public topics only support options topics. If you need USDC/USDT perps, use `unifiedPerp` instead. |
| Unified Margin - Perps | `market: 'unifiedPerp'` | The [derivatives v3](https://bybit-exchange.github.io/docs/derivativesV3/unified_margin/#t-websocket) category for unified margin. Note: public topics only support USDT/USDC perpetual topics - use `unifiedOption` if you need public options topics. |
| Futures v2 - Inverse Perps | `market: 'inverse'` | The [inverse v2 perps](https://bybit-exchange.github.io/docs/futuresV2/inverse/#t-websocket) category. |
| Futures v2 - USDT Perps | `market: 'linear'` | The [USDT/linear v2 perps](https://bybit-exchange.github.io/docs/futuresV2/linear/#t-websocket) category. |
| Futures v2 - Inverse Futures | `market: 'inverse'` | The [inverse futures v2](https://bybit-exchange.github.io/docs/futuresV2/inverse_futures/#t-websocket) category uses the same market as inverse perps. |
| Spot v3 | `market: 'spotv3'` | The [spot v3](https://bybit-exchange.github.io/docs/spot/v3/#t-websocket) category. |
| Spot v1 | `market: 'spot'` | The older [spot v1](https://bybit-exchange.github.io/docs/spot/v1/#t-websocket) category. Use the `spotv3` market if possible, as the v1 category does not have automatic re-subscribe if reconnected. |
| Copy Trading | `market: 'linear'` | The [copy trading](https://bybit-exchange.github.io/docs/copy_trading/#t-websocket) category. Use the linear market to listen to all copy trading topics. |
| USDC Perps | `market: 'usdcPerp` | The [USDC perps](https://bybit-exchange.github.io/docs/usdc/perpetual/#t-websocket) category. |
| USDC Options | `market: 'usdcOption'`| The [USDC options](https://bybit-exchange.github.io/docs/usdc/option/#t-websocket) category. |
| Contract v3 USDT | `market: 'contractUSDT'`| The [Contract V3](https://bybit-exchange.github.io/docs/derivativesV3/contract/#t-websocket) category (USDT perps) |
| Contract v3 Inverse | `market: 'contractInverse'`| The [Contract V3](https://bybit-exchange.github.io/docs/derivativesV3/contract/#t-websocket) category (inverse perps) |
| V5 Subscriptions | `market: 'v5'` | The [v5](https://bybit-exchange.github.io/docs/v5/ws/connect) websocket topics for all categories under one market. Use the subscribeV5 method when subscribing to v5 topics. |

For more complete examples, look into the ws-\* examples in the [examples](./examples/) folder in the repo on GitHub. Here's a minimal example for using the websocket client:

```javascript
const { WebsocketClient } = require('bybit-api');

const API_KEY = 'xxx';
const PRIVATE_KEY = 'yyy';

const wsConfig = {
  key: API_KEY,
  secret: PRIVATE_KEY,

  /*
    The following parameters are optional:
  */

  // Connects to livenet by default. Set testnet to true to use the testnet environment.
  // testnet: true

  // If you can, use the v5 market (the newest generation of Bybit's websockets)
  market: 'v5',

  // The older generations of Bybit's websockets are still available under the previous markets:
  // market: 'linear',
  // market: 'inverse',
  // market: 'spotv3',
  // market: 'usdcOption',
  // market: 'usdcPerp',
  // market: 'unifiedPerp',
  // market: 'unifiedOption',

  // how long to wait (in ms) before deciding the connection should be terminated & reconnected
  // pongTimeout: 1000,

  // how often to check (in ms) that WS connection is still alive
  // pingInterval: 10000,

  // how long to wait before attempting to reconnect (in ms) after connection is closed
  // reconnectTimeout: 500,

  // config options sent to RestClient (used for time sync). See RestClient docs.
  // restOptions: { },

  // config for axios used for HTTP requests. E.g for proxy support
  // requestOptions: { }

  // override which URL to use for websocket connections
  // wsUrl: 'wss://stream.bytick.com/realtime'
};

const ws = new WebsocketClient(wsConfig);

// (before v5) subscribe to multiple topics at once
ws.subscribe(['position', 'execution', 'trade']);

// (before v5) and/or subscribe to individual topics on demand
ws.subscribe('kline.BTCUSD.1m');

// (v5) subscribe to multiple topics at once
ws.subscribeV5(['orderbook.50.BTCUSDT', 'orderbook.50.ETHUSDT'], 'linear');

// (v5) and/or subscribe to individual topics on demand
ws.subscribeV5('position', 'linear');
ws.subscribeV5('publicTrade.BTC', 'option');

// Listen to events coming from websockets. This is the primary data source
ws.on('update', (data) => {
  console.log('update', data);
});

// Optional: Listen to websocket connection open event (automatic after subscribing to one or more topics)
ws.on('open', ({ wsKey, event }) => {
  console.log('connection open for websocket with ID: ' + wsKey);
});

// Optional: Listen to responses to websocket queries (e.g. the response after subscribing to a topic)
ws.on('response', (response) => {
  console.log('response', response);
});

// Optional: Listen to connection close event. Unexpected connection closes are automatically reconnected.
ws.on('close', () => {
  console.log('connection closed');
});

// Optional: Listen to raw error events. Recommended.
ws.on('error', (err) => {
  console.error('error', err);
});
```

See [websocket-client.ts](./src/websocket-client.ts) for further information.

---

## Logging

### Customise logging

Pass a custom logger (or mutate the imported DefaultLogger class) which supports the log methods `silly`, `debug`, `notice`, `info`, `warning` and `error`, or override methods from the default logger as desired, as in the example below:

```javascript
const { WebsocketClient, DefaultLogger } = require('bybit-api');

// Disable all logging on the silly level
const customLogger = {
  ...DefaultLogger,
  silly: () => {},
};

const ws = new WebsocketClient({ key: 'xxx', secret: 'yyy' }, customLogger);
```

### Debug HTTP requests

In rare situations, you may want to see the raw HTTP requets being built as well as the API response. These can be enabled by setting the `BYBITTRACE` env var to `true`.

## Browser Usage

Build a bundle using webpack:

- `npm install`
- `npm build`
- `npm pack`

The bundle can be found in `dist/`. Altough usage should be largely consistent, smaller differences will exist. Documentation is still TODO.

However, note that browser usage will lead to CORS errors due Bybit. See [issue #79](#79) for more information & alternative suggestions.

---

## Contributions & Thanks

### Donations

#### tiagosiebler

If you found this project interesting or useful, create accounts with my referral links:

- [Bybit](https://www.bybit.com/en-US/register?affiliate_id=9410&language=en-US&group_id=0&group_type=1)
- [Binance](https://www.binance.com/en/register?ref=20983262)

Or buy me a coffee using any of these:

- BTC: `1C6GWZL1XW3jrjpPTS863XtZiXL1aTK7Jk`
- ETH (ERC20): `0xd773d8e6a50758e1ada699bb6c4f98bb4abf82da`

#### pixtron

An early generation of this library was started by @pixtron. If this library helps you to trade better on bybit, feel free to donate a coffee to @pixtron:

- BTC `1Fh1158pXXudfM6ZrPJJMR7Y5SgZUz4EdF`
- ETH `0x21aEdeC53ab7593b77C9558942f0c9E78131e8d7`
- LTC `LNdHSVtG6UWsriMYLJR3qLdfVNKwJ6GSLF`

### Contributions & Pull Requests

Contributions are encouraged, I will review any incoming pull requests. See the issues tab for todo items.

## Star History

[![Star History Chart](https://api.star-history.com/svg?repos=tiagosiebler/ftx-api,tiagosiebler/bybit-api,tiagosiebler/binance,tiagosiebler/orderbooks,tiagosiebler/okx-api,tiagosiebler/awesome-crypto-examples&type=Date)](https://star-history.com/#tiagosiebler/ftx-api&tiagosiebler/bybit-api&tiagosiebler/binance&tiagosiebler/orderbooks&tiagosiebler/okx-api&tiagosiebler/awesome-crypto-examples&Date)
