# Node-Linting-and-Testing

Some basic notes on Linting and Testing with node.js (WIP)

Contents

* [Linting](#linting)
* [Testing](#testing)
    * [Testing Frameworks](#testing-frameworks)
    * [Testing Frameworks](#testing-frameworks)
    * [Assertion Libraries](#assertion-libraries)
    * [Dependency Manipulation Libraries](#dependency-manipulation-libraries)
    * [Functional Testing Tools](#functional-testing-tools)
    * [HTML Parsing](#html-parsing)
* [Code Coverage Libraries](#code-coverage-libraries)

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
npm run -s eslint .
```

To run and fix errors:

```bash
npm run -s eslint -- --fix .
```

Details:

    https://eslint.org/docs/user-guide/command-line-interface

## Testing

![Test Doubles](/images/Test_Doubles.png)

> xUnit Test Patterns: Refactoring Test Code
> by Gerard Meszaros,
> page 527

#### Testing Frameworks

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

#### Assertion Libraries

Depending upon your preferences for [TDD](https://www.agilealliance.org/glossary/tdd/)
versus [BDD](https://www.agilealliance.org/glossary/bdd/), any of the following libraries
may be a good choice.

TDD is an older and more established software practice, also hacker-friendly.

BDD is a related but more formal practice, which aims to align the tests with
the functional specifications (which means that there need to be written
functional specifications in place, perhaps more of a waterfall approach than
an agile approach).

* Assert
* [code](http://github.com/hapijs/code) is a BDD assertion library
* [Chai](http://chaijs.com) is a BDD / TDD assertion library
* [Should.js](http://shouldjs.github.io)

[`Assert` is node's native assertion library and does not need to be installed.]

To install:

```bash
npm install chai -D
```

#### Dependency Manipulation Libraries

* [Mockery](http://github.com/mfncooper/mockery)
* [Proxyquire](http://github.com/thlorenz/proxyquire)
* [Rewire](http://github.com/jhnns/rewire)

To install:

```bash
npm install proxyquire -D
```

For more details:

    https://github.com/thlorenz/proxyquire#usage

#### Functional Testing Tools

* [PhantomJS](http://phantomjs.org)
* [CasperJS](http://casperjs.org)
* [Selenium WebDriver](http://seleniumhq.org)
* [NightwatchJS](http://nightwatchjs.org)
* [WebdriverIO](http://webdriver.io)
* [SuperAgent](http://visionmedia.github.io/superagent)
* [Chai HTTP](http://chaijs.com/plugins/chai-http)

To install:

```bash
npm install chai-http -D
```

#### HTML Parsing

For functional testing, it is useful to be able to parse the HTML responses (rather
than `grep` for certain hard-coded text strings).

Either way, determining that the HTML response is correct makes for a very brittle
and error-prone test.

For parsing and validating HTML, the following library may be useful:

    https://cheerio.js.org/

[Cheerio is designed for ___server-side___ HTML Parsing.]

To install:

```bash
npm install cheerio -D
```

## Code Coverage Libraries

Opinions differ on whether or not 100% coverage is a realistic or achievable
goal, however this is a very useful statistic for measuring software quality
and how it changes over time.

* Blanket (no longer maintained)
* JSCoverage (no longer maintained)
* [Istanbul](http://istanbul.js.org)

To install:

```bash
npm install nyc -D
```

Update `package.json` as follows:

```
  "scripts": {
    "coverage": "nyc --reporter=text --reporter=html mocha"
  },
```

To run:

```bash
npm run -s coverage
```
