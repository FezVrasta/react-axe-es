# react-axe-es

This project is a thin wrapper around `react-axe`, the only difference is the addition of the
`sideEffects` flag set to `false` in the `package.json`.

Please, read to the official [react-axe docs](https://github.com/dequelabs/react-axe) for
the full documentation.

## Why?

The only supported way to use `react-axe` is to use CommonJS to conditionally import the dependency,
or to use dynamic `import()` statements, that will make your initial app rendering asyncronous.

Neither of the above approaches are acceptable solutions for consumers that follow a pure ES modules
approach, as reccomended by the [webpack documentation](https://webpack.js.org/api/module-methods/#es6-recommended).

To overcome this limitation, `react-axe-es` allows its consumers to statically
import the dependency with a standard static `import` statement, while allowing
the consumer's bundler (such as webpack, rollup, parcel, etc...) to dead code
eliminate the imported dependency in case it ends up not being used in the
production code.

The following example will bundle `react-axe-es` when `NODE_ENV` is not set to
`production`, but will strip it out completely in the other case:

```js
import React from 'react';
import ReactDOM from 'react-dom';
import axe from 'react-axe-es';

if (process.env.NODE_ENV !== 'production') {
  axe(React, ReactDOM, 1000);
}
```

## How

This package has as only dependency `react-axe`, with the `3.0.0` version configured
to allow any `react-axe@3.x` version, this means you don't need to wait for a new
`react-axe-es` release to use the new `react-axe` features.

We tried to get this functionality baked it into the core library, but the maintainers
refused to merge our [pull request](https://github.com/dequelabs/react-axe/pull/115#event-2624893905).