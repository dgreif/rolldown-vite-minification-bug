# rolldown-vite-minification-bug

This is a minimal reproduction of a bug in `rolldown` where it produces invalid minified code when building a Vite project that uses the `@primer/react` package.

To reproduce:

- `npm install`
- `npm run build`
- `npm run preview`
- Open the browser to `http://localhost:4173` and see the error in the console

```
Uncaught SyntaxError: Unexpected template string
```

The error is caused by template strings in object keys, for example:

```js
{size:s,srText:c,`aria-label`:r,className:i,style:o,...a}=e
```

These are produced by `aria-*` keys being spread in the `@primer/react` package, such [this example](https://github.com/primer/react/blob/d74d73e413a9941cdc74c6f5a2cf6b1be9e7e8db/packages/react/src/Spinner/Spinner.tsx#L28-L35).
