# Pluralsight: source code for "Code with us: Angular Quickstart" by John Papa and Ward Bell

## What is this?

This repo holds the complete source code for the Pluralsight course, "[Code with us: Angular Quickstart](https://app.pluralsight.com/library/courses/code-with-us-angular-quick-start)".

The primary application is a harness that runs each section (AKA chapter) within a central window.
Select a course section from the dropdown at the top and see that section's finished code running in the browser.

Almost everything of interest is in the `app/` folder where you'll find the code for each section of the course (including exercises) in its own folder. The `AppComponent` is the harness shell and the `AppModule` registers each section in the harness.
Each section folder is a standalone application that represents the end-state of the corresponding section in the course.

The ["Final Project Walk-through" clip](https://app.pluralsight.com/player?course=code-with-us-angular-quick-start&author=john-papa&name=code-with-us-angular-quick-start-m1&clip=0&mode=live) show the harness in action. It explains how the harness works and how to run a section outside the harness.

The balance of this README comes straight from the Angular Quickstart (the course starting point).
It covers how to install and run the application. It also covers running the tests.
We didn't do much testing in this course but we hope that you'll be inspired to make testing part of your Angular development life.

## Install npm packages

Install the npm packages described in the `package.json` and verify that it works:

```bash
npm install
npm start
```

The `npm start` command first compiles the application, 
then simultaneously re-compiles and runs the `lite-server`.
Both the compiler and the server watch for file changes.

Shut it down manually with `Ctrl-C`.

You're ready to write your application.

### npm scripts

We've captured many of the most useful commands in npm scripts defined in the `package.json`:

* `npm start` - runs the compiler and a server at the same time, both in "watch mode".
* `npm run tsc` - runs the TypeScript compiler once.
* `npm run tsc:w` - runs the TypeScript compiler in watch mode; the process keeps running, awaiting changes to TypeScript files and re-compiling when it sees them.
* `npm run lite` - runs the [lite-server](https://www.npmjs.com/package/lite-server), a light-weight, static file server, written and maintained by
[John Papa](https://github.com/johnpapa) and
[Christopher Martin](https://github.com/cgmartin)
with excellent support for Angular apps that use routing.

Here are the test related scripts:
* `npm test` - compiles, runs and watches the karma unit tests
* `npm run e2e` - run protractor e2e tests, written in JavaScript (*e2e-spec.js)
* `npm run e2e:fast` - run protractor e2e tests a little faster after the first time
## Testing

This repo adds both karma/jasmine unit test and protractor end-to-end testing support.

These tools are configured for specific conventions described below.

*It is unwise and rarely possible to run the application, the unit tests, and the e2e tests at the same time.
We recommend that you shut down one before starting another.*

### Unit Tests
TypeScript unit-tests are usually in the `app` folder. Their filenames must end in `.spec`.

Look for the example `app/app.component.spec.ts`.
Add more `.spec.ts` files as you wish; we configured karma to find them.

Run it with `npm test`

That command first compiles the application, then simultaneously re-compiles and runs the karma test-runner.
Both the compiler and the karma watch for (different) file changes.

Shut it down manually with `Ctrl-C`.

Test-runner output appears in the terminal window.
We can update our app and our tests in real-time, keeping a weather eye on the console for broken tests.
Karma is occasionally confused and it is often necessary to shut down its browser or even shut the command down (`Ctrl-C`) and
restart it. No worries; it's pretty quick.

### End-to-end (E2E) Tests

E2E tests are in the `e2e` directory, side by side with the `app` folder.
Their filenames must end in `.e2e-spec.ts`.

Look for the example `e2e/chapter-1.e2e-spec.ts`.
Add more `.e2e-spec.js` files as you wish (although one usually suffices for small projects);
we configured protractor to find them.

Thereafter, run them with `npm run e2e` (or `npm run e2e:fast`).

That command first compiles, then simultaneously starts the Http-Server at `localhost:8080`
and launches protractor.  

The pass/fail test results appear at the bottom of the terminal window.
A custom reporter (see `protractor.config.js`) generates a  `./_test-output/protractor-results.txt` file
which is easier to read; this file is excluded from source control.

Shut it down manually with `Ctrl-C`.
