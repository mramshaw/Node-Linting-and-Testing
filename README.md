# Node-Linting-and-Testing

Some basic notes on Linting and Testing with node.js (WIP)

The notes will cover using the javascript package manager `npm`
but all of this can probably be done just as easily with `yarn`.

Contents

* [Type Checking](#type-checking)
* [Linting](#linting)
* [Testing](#testing)
    * [Testing Frameworks](#testing-frameworks)
    * [Testing Frameworks](#testing-frameworks)
    * [Assertion Libraries](#assertion-libraries)
    * [Dependency Manipulation Libraries](#dependency-manipulation-libraries)
    * [Functional Testing Tools](#functional-testing-tools)
    * [HTML Parsing](#html-parsing)
* [Code Coverage Libraries](#code-coverage-libraries)
* [Continuous Integration](#continuous-integration)

## Type Checking

* [Flow](http://flow.org)

To install:

```bash
npm install flow-bin -D
```

Update `package.json` as follows:

```
  "scripts": {
    "flow": "flow"
  },
```

To run:

```bash
npm run -s flow
```

[Note that individual files must be annotated in order to be scanned by `flow`.]

Details:

    http://flow.org/en/docs/

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

    http://eslint.org/docs/user-guide/command-line-interface

## Testing

![Test Doubles](/images/Test_Doubles.png)

> xUnit Test Patterns: Refactoring Test Code
> by Gerard Meszaros,
> page 527

#### Testing Frameworks

* [AVA](http://github.com/avajs/ava)
* [Mocha](http://mochajs.org)
* [Jasmine](http://jasmine.github.io)
* [Jest](http://facebook.github.io/jest)
* [Tape](http://github.com/substack/tape)

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

Depending upon your preferences for [TDD](http://www.agilealliance.org/glossary/tdd/)
versus [BDD](http://www.agilealliance.org/glossary/bdd/), any of the following libraries
may be a good choice.

[Note that Ava, Jasmine and Jest include their own assertion libraries.]

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

    http://github.com/thlorenz/proxyquire#usage

It is probably a good idea to also install Sinon:

* [Sinon](http://sinonjs.org/)

Sinon describes itself as "Standalone test spies, stubs and mocks for JavaScript".

It works well with Proxyquire:

    http://github.com/thlorenz/proxyquire/tree/master/examples/sinon

To install:

```bash
npm install sinon -D
```

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

For functional or performance testing, it is useful to be able to parse HTML responses
(rather than `grep` for certain hard-coded text strings).

Either way, determining that the HTML response is correct makes for a very brittle
and error-prone test.

For parsing and validating HTML, Cheerio should be useful - bearing in mind that it
was designed for ___server-side___ HTML Parsing.

* [Cheerio](http://cheerio.js.org/)

To install:

```bash
npm install cheerio -D
```

## Code Coverage Libraries

Opinions differ on whether or not 100% coverage is a realistic or achievable
goal, however code coverage is a very useful statistic for measuring software
quality and how it changes over time.

[My opinion is that anything less than 70% code coverage is unacceptable.
 I have talked with many colleagues, and standards may change depending
 on the specific application or industry, with some sites requiring 80%
 coverage -- or even 100% coverage -- so I am NOT saying that 70% coverage
 is ideal, merely that 70% coverage is the bare minimum to start with,
 even if it results in some time lost in writing tests and/or refactoring.
 If your project is a few thousand lines of code or less, 100% coverage
 is probably the correct goal to shoot for.]

It's important to realize that 100% code coverage does NOT mean bug-free code!

A downside of testing and code coverage is that it often introduces brittle
and difficult-to-maintain tests, all of which increase the number of lines
of code. This should never be used as an excuse ___not___ to write tests,
but it is something to bear in mind. For instance, it is a good idea to
wait until any APIs have been finalized before spending too much time
writing tests - as any API changes will lead to multiple code changes.

A balance must be maintained between writing tests and the burden of
actually maintaining the test code, all while bearing in mind that
tests - while valuable - do not deliver added functionality to the
end user.

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

## Continuous Integration

This is really a ___best practice___ and should include linting and code coverage tests,
as discussed above.

* [BuildBot](http://buildbot.net)
* [Jenkins](http://jenkins.io)
* [Strider CD](http://strider-cd.github.io)

For many uses, CIAAS (Continuous Integration As A Service) may be an attractive option.
GitHub integration is usually relatively easy and painless, and often has a free tier.

* [CircleCI](http://circleci.com)
* [Gitlab](http://gitlab.com)
* [Travis CI](http://travis-ci.org)

In my experience, Travis CI has been easy to use and features an easy integration with
GitHub such that a code commit triggers an automated build as well as CI.
