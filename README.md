# Node-Linting-and-Testing

![node.js](/images/nodejs.png)

Some notes on Linting and Testing with node.js as well as some
general thoughts on BDD & TDD frameworks.

[Most of these tools may be used when developing with plain javascript
 as well as with javascript frameworks such as React.]

All of the main browsers have extensions that can verify javascript.
When testing client-side javascript components, these are probably
the first place to start.

The notes will cover using the package manager `npm`
but all of this can probably be done just as easily with `yarn`.

## Contents

* [Type Checking](#type-checking)
* [Linting](#linting)
    * [Disabling eslint rules](#disabling-eslint-rules)
* [Testing](#testing)
    * [Testing Frameworks](#testing-frameworks)
    * [Assertion Libraries](#assertion-libraries)
    * [Dependency Manipulation Libraries](#dependency-manipulation-libraries)
    * [Functional Testing Tools](#functional-testing-tools)
    * [HTML Parsing](#html-parsing)
* [Code Coverage Libraries](#code-coverage-libraries)
* [Dependency Checking](#dependency-checking)
    * [npm audit](#npm-audit)
    * [OWASP](#owasp)
* [Vulnerability Scanning](#vulnerability-scanning)
    * [Retire.js](#retirejs)
    * [Snyk.io](#snykio)
* [Continuous Integration](#continuous-integration)
* [To Do](#to-do)

## Type Checking

Type checking adds an extra level of validation when developing in javascript.

[This is the type of validation normally provided by a compiler.]

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

To initialize:

```bash
npm run -s flow init
```

[This will create a `.flowconfig` file, which should be committed.]

To run:

```bash
npm run -s flow
```

Note that individual files must be annotated as follows in order to be scanned by `flow`:

```javascript
// @flow

```

Status:

```bash
npm run -s flow status
```

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

To set `eslint` options (if not set globally):

```bash
npm run -s eslint -- --init
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

#### Disabling eslint rules

It is straightforward to disable eslint rules for specific lines of code:

```node.js
// eslint-disable-next-line no-unused-vars
const routes = require("./routes.js")(app);
```

Reference:

    http://eslint.org/docs/user-guide/configuring#disabling-rules-with-inline-comments

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

[My take on this is that BDD and TDD are really complementary disciplines. Both take
___best practices___ from __Design by Contract__ and __Use Cases__ (pre-conditions
and post-conditions) and focus on putting Descartes before the horse (by writing
the acceptance tests before the code - and only writing code once tests fail). This
is in contrast to what I call 'Happy Path coding' which does not take exceptions or
errors into consideration. My easy mnemonic for remembering which is which is 'T'
for technical (such as testing for exceptions, errors or edge cases) testing and 'B'
for business (business-related user acceptance criteria) testing.]

There are a number of BDD frameworks for languages such as Ruby (Cucumber, minitest)
and Java (JGiven) but the focus here is on frameworks for javascript.

UPDATE: It seems that Cucumber has been ported to Javascript -
[Cucumber.js](http://www.npmjs.com/package/cucumber). There is
at least one use of it in the wild -
[Botium BDD Samples](https://github.com/codeforequity-at/botium-bdd-samples)
(Botium is a testing framework for chatbots - it describes itself as
"The Selenium for Chatbots").

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
* [Cypress](http://www.cypress.io)

We will install Chai HTTP but __Cypress__ is also worth considering
(especially for Front-end Developers, as it can make them more Agile).

Cypress is a relative newcomer but shows promise. It plays well with __Mocha__ and __Chai__.

As contrasted with __Selenium__, browser support is more limited - as of November, 2020:

1. Chrome
2. Firefox
3. Edge
4. Electron
5. Brave

[These are probably sufficient for most purposes.]

Cypress is JavaScript-based which makes navigating a DOM straightforward. This may
well obviate [HTML Parsing](#html-parsing), as described below. So, no __Cheerio__
needed.

Cypress operates directly in the browser, however the browser may be invoked headlessly.
See my [hello-world-cypress](http://github.com/mramshaw/hello-world-cypress) repo.
Being browser-based, it looks like Cypress can bypass some CORS limitations.

Unlike other tools, Cypress does not use a __Selenium WebDriver__. This should mean
that Cypress testing is faster (no WebDriver ramp-up time needed), also no network
lag.

Cypress records video of the tests (this video needs to be slowed-down quite a lot).

Cypress can interact with Electron applications (such as __Postman__ and Cypress
Test Runner).

To install Chai HTTP:

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

## Dependency Checking

Any build effort should include a tool to scan dependencies for known vulnerabilities.

#### npm audit

Probably the first place to start is with `npm` (the node package manager) itself.

For an introduction to `npm audit`:

    http://docs.npmjs.com/getting-started/running-a-security-audit

> `npm audit` requires packages to have `package.json` and `package-lock.json` files.

To see what vulnerabilities it can detect:

```bash
$ npm audit
```

To see what fixes can be automatically made:

```bash
$ npm audit fix --dry-run
```

To apply the fixes:

```bash
$ npm audit fix
```

For a more comprehensive list of `npm audit` options:

    http://docs.npmjs.com/cli/audit

[It is not clear whether or not this information relies on OWASP, probably best to use both.]

#### OWASP

The [Open Web Application Security Project (OWASP)](http://www.owasp.org/index.php/Main_Page)
sponsors a number of security projects, among them a dependency checker:

* [OWASP Dependency-Check](http://www.owasp.org/index.php/OWASP_Dependency_Check)

[Platforms other than __Java__ and __.NET__ are supported via the Command Line tool.]

This tool ___may___ require that a Java Runtime Environment (JRE) be installed.

For more details:

    http://jeremylong.github.io/DependencyCheck/general/thereport

OWASP also sponsors (along with others) the [OWASP .NET Project](http://www.owasp.org/index.php/OWASP_.NET_Project)
and the [OWASP  Node js Goat Project](http://www.owasp.org/index.php/OWASP_Node_js_Goat_Project).

While there are no doubt many other places to search for security vulnerabilities,
OWASP is probably as good a place as any to start.

## Vulnerability Scanning

Any build effort should include tools to scan for vulnerabilities.

* [Burp](http://portswigger.net/burp)
* [Retire.js](http://github.com/RetireJS/retire.js/) [can be integrated as a Burp plugin]
* [Snyk](http://snyk.io)

#### Retire.js

[Retire.js](http://retirejs.github.io/retire.js/) publishes a list of the vulnerabilities
that it can scan for, which is definitely worth a look.

#### Snyk.io

Snyk offers reports, notifications and an attractive dashboard. It also offers a number
of helpful integrations, such as GitHub and Travis/Jenkins. While Snyk will scan code
whenever code is checked-in, it will also scan code on a regular basis as well. For a
higher frequency of vulnerability scanning, a commercial license is recommended.

Snyk publishes a list of the vulnerabilities that it can scan for:

    http://snyk.io/vuln

Snyk uses dependency manifests in order to determine the dependencies to scan:

    http://support.snyk.io/getting-started/languages-support

This ___may___ be an issue to be aware of. For instance, note that for Golang repo
testing, Snyk only supports a few of the possible manifest options offered by Golang's
myriad dependency managers. And for Python, there will need to be a __requirements.txt__
file. While very useful, it's worth bearing in mind that Snyk only scans projects
under the control of a package manager - and uses the ___package manifest___ to do this.
As the manifest may not actually reflect the ___installed___ packages, this needs
to be taken into account (this should not be a concern in a __CI__ or build pipeline).

For example, if the `requirements.txt` file contains `Flask>=0.12.2` then Snyk will
scan with the ___latest___ Flask (`flask@1.0.2` at the time of writing). This may not
reflect the locally installed version of the particular dependency (Flask here).

Snyk scans ___recursively___, which is a very nice feature indeed. This means that
that each package manifest will be scanned (and generate a report).

Snyk also offers a CLI option, but I believe you will need a Snyk account to use it.

For more details:

    http://snyk.io/docs

## Continuous Integration

This is really a ___best practice___ and should include linting and code coverage tests,
as discussed above.

* [BuildBot](http://buildbot.net)
* [GitHub Actions](http://help.github.com/en/actions/automating-your-workflow-with-github-actions/using-nodejs-with-github-actions)
* [Jenkins](http://jenkins.io)
* [Strider CD](http://strider-cd.github.io)

For many uses, CIaaS (Continuous Integration as a Service) may be an attractive option.
GitHub integration is usually relatively easy and painless, and often has a free tier.

* [CircleCI](http://circleci.com)
* [GitLab](http://gitlab.com)
* [Travis CI](http://travis-ci.org)

CircleCI is relatively easy to use, and integrates well with GitHub.

[For an example, check out my [Circling](https://github.com/mramshaw/Circling) repo.]

GitLab features their own CI/CD pipelines and tools. Other options are possible,
but as they offer a pretty full slate of services, why use anything else?

In my experience, Travis CI has been easy to use and features an easy integration with
GitHub such that a code commit triggers an automated build as well as CI testing.

Not surprisingly, GitHub Actions integrate pretty well with GitHub too. They are not
yet the most easy to use (being still pretty much the new kid on the block) but will
probably get there eventually.

[For an example, check out my [ReactAWS](https://github.com/mramshaw/ReactAWS) repo.]

## To Do

- [x] Investigate [Cucumber](http://cucumber.io/) [BDD framework for Ruby] and __Gherkin__ (English-like DSL for expressing acceptance criteria)
- [ ] Investigate [Cucumber.js](http://github.com/cucumber/cucumber-js) [BDD framework for Javascript]
- [x] Add some notes on [Cypress](http://www.cypress.io/)
- [x] Add a note on when Snyk.io conducts vulnerability scans (on code check-in, as well as scheduled scans)
- [x] Add a note on disabling `eslint` rules
- [x] Add a note about GitHub Actions
- [ ] Investigate [Serenity](http://thucydides.info/#/) [BDD framework for validating use cases]
- [ ] Investigate [SpecFlow](http://specflow.org/) [BDD framework that describes itself as "Cucumber for .NET"]
