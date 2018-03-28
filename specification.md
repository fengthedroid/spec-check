# `spec-check` specification

This is a `spec-check` report which is also an executable specification for `spec-check`. The test will:

-   strip this document of ``✅ `spec-check`ed``
-   strip this document of `❌ Error: ...`
-   run `spec-check --report specification-report.md add=test/add.js specification-input.md`

The result should be identical to this document.

## non js/javascript code blocks

### other code blocks are ignored

    this is not a javascript code block

## js/javascript code blocks ```` ```js```` or ```` ```javascript````

### lines with `>` that eval to subsequent lines are labeled with ✅

```js
> ['Hello', 'world'].join(' ')
'Hello world'
```

✅ [`spec-check`](https://github.com/concept-not-found/spec-check)ed

### requires such as `add=test/add.js` are in scope

```js
> add(1, 1)
2
```

✅ [`spec-check`](https://github.com/concept-not-found/spec-check)ed

### lines that do not eval to subsequent lines are labeled with ❌

```js
> 'i hear you'
'i understand you'
```

❌ `Error: 'i hear you' => expected 'i understand you', but got 'i hear you'`

### errors thrown by input lines can be checked by Error output

```js
> throw new Error('oops')
Error: oops
```

✅ [`spec-check`](https://github.com/concept-not-found/spec-check)ed

### errors thrown by output lines rethrown

```js
> 'everything is fine'
throw new Error('oops')
```

❌ ``Error: failed to eval output `throw new Error('oops')`: oops``

### multiple input lines can contribute to output

```js
> name = 'Bob'
> `Hi ${name}`
'Hi Bob'
```

✅ [`spec-check`](https://github.com/concept-not-found/spec-check)ed

### each block is not isolated from each other, be careful

```js
> name
undefined
```

❌ `Error: name => expected undefined, but got 'Bob'`

### missing input throws an error

```js
42
```

❌ `Error: at least one input required`