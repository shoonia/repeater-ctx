# repeater-scope

[![ci build](https://github.com/shoonia/repeater-scope/actions/workflows/ci.yml/badge.svg)](https://github.com/shoonia/repeater-scope/actions/workflows/ci.yml)
[![npm version](https://badgen.net/npm/v/repeater-scope)](https://www.npmjs.com/package/repeater-scope)
[![minzip](https://badgen.net/bundlephobia/minzip/repeater-scope)](https://bundlephobia.com/result?p=repeater-scope)

The utils for repeated item scope event handlers in [Velo](https://www.wix.com/velo) by Wix.

![Velo by Wix](https://static.wixstatic.com/shapes/e3b156_89be007cf73e40da8513b7cede9bf089.svg)

## API

### useScope

**Page Code**

```js
import { useScope } from 'repeater-scope';

$w.onReady(() => {
  // use a dynamic event handler
  $w('#repeatedButton').onClick((event) => {
    const { $item, itemData, index, data } = useScope(event);
  });
});

// or a static event handler
export function repeatedButton_dblClick(event) {
  const { $item, itemData, index, data } = useScope(event);
}
```

### createScope

**Page Code**

```js
import { createScope } from 'repeater-scope';

// Create a scope with a callback function that returns actual repeater data.
const useScope = createScope(() => {
  return $w('#repeater').data;
});

export function repeatedButton_dblClick(event) {
  const { $item, itemData, index, data } = useScope(event);
}
```

## Syntax

```ts
function useScope(event: $w.Event): ScopeData;

type ScopeData = {
  $item: $w;
  itemData: ItemData;
  index: number;
  data: ItemData[];
}

type ItemData = {
  _id: string;
  [key: string]: any;
};
```

### Parameters

- **$item** - A selector function with [repeated item scope](https://www.wix.com/velo/reference/$w/repeater/introduction#$w_repeater_introduction_repeated-item-scope).
- **itemData** - The object from the repeater's `data` array that corresponds to the repeated item being created.
- **index** - The index of the `itemData` object in the `data` array.
- **data** - [A repeater's data array](https://www.wix.com/velo/reference/$w/repeater/data)

## Resources

- [Repeater Introduction](https://www.wix.com/velo/reference/$w/repeater/introduction)
- [Event handling of Repeater Item](https://shoonia.site/event-handling-of-repeater-item/)

## License

[MIT](./LICENSE)
