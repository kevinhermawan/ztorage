# Ztorage

![Minified size](https://img.shields.io/bundlephobia/min/ztorage) ![Test coverage](https://img.shields.io/codecov/c/github/kevinhermawan/ztorage) ![Monthly download](https://img.shields.io/npm/dm/ztorage)

Ztorage is a flexible and type-safe wrapper for key-value storage that is designed to work with various storage mediums, including [Web Storage API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Storage_API) and other storage backends. It takes advantage of [Zod](https://github.com/colinhacks/zod), a powerful TypeScript schema validation library, to provide automatic parsing and validation of data.

## Features

- Works with various storage mediums
- Provides type safety for key-value storage
- Enables automatic parsing and validation of data
- Zero dependencies

## Installation

To use Ztorage, you must have Zod installed. You can install `ztorage` and `zod`, by running the following command:

**NPM**

```
npm install ztorage zod
```

**Yarn**

```
yarn add ztorage zod
```

**pnpm**

```
pnpm add ztorage zod
```

## Usage

```ts
import { z } from "zod";
import Ztorage from "ztorage";

// Define a schema for the data you want to store
const schema = z.object({
  isDarkModeEnabled: z.boolean(),
});

// Instantiate a Ztorage object with a schema and storage functions
const storage = new Ztorage({
  schema,
  onGetItem: async (key) => {
    return localStorage.getItem(key);
  },
  onSetItem: async (key, value) => {
    localStorage.setItem(key, value);
  },
  onRemoveItem: async (key) => {
    localStorage.removeItem(key);
  },
});

// Set item to storage
await storage.setItem("isDarkModeEnabled", true);

// Get item from storage
const isDarkModeEnabled = await storage.getItem("isDarkModeEnabled");
console.log(isDarkModeEnabled); // true

// Remove item from storage
await storage.removeItem("isDarkModeEnabled");
```

## License

[MIT License](/LICENSE)