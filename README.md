# Node-Linting-and-Testing

Some basic notes on Linting and Testing with node.js (WIP)

## Linting

* [JSLint](jslint.com)
* [JSHint](jshint.com)
* [ESLint](eslint.org)

To install:

```bash
npm install eslint -D
```

Update `package.json` as follows:

```
  "scripts": {
    "eslint": "eslint"
  },
```

To run:

```bash
npm run -s eslint
```

Details:

    https://eslint.org/docs/user-guide/command-line-interface

## Testing Frameworks

* [Mocha](mochjs.org)
* [Jasmine](jasmine.github.io)
* [Jest](facebook.github.io/jest)

To install:

```bash
npm install mocha -D
```

Update `package.json` as follows:

```
  "scripts": {
    "test": "mocha"
  },
```

To run:

```bash
npm test
```

## Assertion Libraries

* Assert
* [code](github.com/hapijs/code)
* [Chai](chaijs.com)
* [Should.js](shouldjs.github.io)

[`Assert` is node's native assertion library and does not need to be installed.]

To install:

```bash
npm install chai -D
```

## Dependency Manipulation Libraries

* [Mocker](github.com/mfncooper/mockery)
* [Proxyquire](github.com/thlorenz/proxyquire)
* [Rewire](github.com/jhnns/rewire)

To install:

```bash
npm install proxyquire -D
```
