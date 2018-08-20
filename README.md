# Node-Linting-and-Testing

Some basic notes on Linting and Testing with node.js (WIP)

## Linting

* [JSLint](http://jslint.com)
* [JSHint](http://jshint.com)
* [ESLint](http://eslint.org)

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

* [Mocha](http://mochajs.org)
* [Jasmine](http://jasmine.github.io)
* [Jest](http://facebook.github.io/jest)

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

Depending upon your preferences for [TDD](https://www.agilealliance.org/glossary/tdd/)
versus [BDD](https://www.agilealliance.org/glossary/bdd/), any of the following libraries
may be a good choice.

* Assert
* [code](http://github.com/hapijs/code) is a BDD assertion library
* [Chai](http://chaijs.com) is a BDD / TDD assertion library
* [Should.js](http://shouldjs.github.io)

[`Assert` is node's native assertion library and does not need to be installed.]

To install:

```bash
npm install chai -D
```

## Dependency Manipulation Libraries

* [Mocker](http://github.com/mfncooper/mockery)
* [Proxyquire](http://github.com/thlorenz/proxyquire)
* [Rewire](http://github.com/jhnns/rewire)

To install:

```bash
npm install proxyquire -D
```
