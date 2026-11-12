# CharlieOS stickers

Stickers are small apps for CharlieOS, an operating system for the M5Stack
StickS3. Each sticker is one JSON file with no code: it says what to fetch,
which values to pick out and how to lay them out. The stick draws it with a
built-in player.

## What's here

- `*.json`: the stickers in the catalogue, one file each.
- `samples/`: made-up responses in each API's shape, for the simulator.
- `tests/invalid/`: stickers that must be rejected, used to test the checker.

## How the stick gets them

The catalogue is published as the assets of the `stickers` release in this
repository: `index.json`, its signature `index.json.sig`, and one file per
sticker. The index is signed with an ECDSA P-256 key, and the stick installs
only stickers listed in a correctly signed index whose SHA-256 matches.

## A sticker in brief

```json
{
  "format": 1,
  "id": "btc",
  "name": "Bitcoin",
  "version": "1.0.0",
  "author": "CharlieOS",
  "summary": "Bitcoin price in US dollars",
  "icon": "coin",
  "fetch": { "url": "https://api.coinbase.com/v2/prices/BTC-USD/spot", "every_min": 15 },
  "layout": "big",
  "values": [
    { "label": "BTC in USD", "pick": "data.amount", "format": "money:USD" }
  ],
  "card_line": "BTC {0}"
}
```

Fetch URLs must be `https://` with no secrets. Data is refreshed at most
every 5 minutes, and responses are limited to 8 KB.
