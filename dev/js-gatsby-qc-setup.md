# Working with Gatsby: Quality Control Setup <!-- omit in toc -->

- [🔍 Overview](#-overview)
- [1. Static testing](#1-static-testing)
  - [Pre-commit linting and formatting](#pre-commit-linting-and-formatting)
  - [Pre-commit commit message linting](#pre-commit-commit-message-linting)
  - [Static type checking](#static-type-checking)
- [2. End-to-end testing](#2-end-to-end-testing)
  - [Cypress + Cypress Testing Library](#cypress--cypress-testing-library)
- [3. Unit testing](#3-unit-testing)
  - [Jest + React Testing Library](#jest--react-testing-library)
- [4. CI](#4-ci)
  - [Automated testing](#automated-testing)
  - [Automated versioning](#automated-versioning)
  - [Automated packaging](#automated-packaging)
- [5. CD](#5-cd)
  - [Automated deployment](#automated-deployment)
  - [Automated monitoring](#automated-monitoring)

## 🔍 Overview

This document provides instruction on how to add testing and extra quality
control measures to an existing Gatsby project environment.

## 1. Static testing

### Pre-commit linting and formatting

NB. Gatsby supports ESLint by default

- `yarn add -D husky lint-staged prettier`
- (package.json) add husky pre-commit lint-staged hook
- (.eslintrc.json) add prefs
- (.prettierrc.json) add prefs
- (.lintstagedrc.json) add linters settings object

#### Further information <!-- omit in toc -->

<https://prettier.io/docs/en/precommit.html>

<https://github.com/prettier/eslint-config-prettier>

### Pre-commit commit message linting

- `yarn add -D husky commitlint @commitlint/cli @commitlint/config-conventional`
- (package.json) add husky pre-commit commitlint hook

#### Further information <!-- omit in toc -->

<https://commitlint.js.org/#/guides-local-setup>

### Static type checking

N.B. Gatsby supports Typescript by default

- `npm install -g typescript`
- (.tsconfig) create with `tsc --init`, then uncomment `jsx` key
- (package.json) add `tsc` npm script

#### Further information <!-- omit in toc -->

<https://www.gatsbyjs.org/docs/typescript/>

## 2. End-to-end testing

### Cypress + Cypress Testing Library

- Core installation and configuration

```shell
yarn add -D cypress
npx rimraf cypress/integration cypress/fixtures cypress/screenshots
mkdir cypress/e2e
echo cypress/screenshots >> .gitignore
```

```json
// (cypress.json)

{
  "baseUrl": "http://localhost:8000/",
  "integrationFolder": "cypress/e2e"
}
```

```json
// (package.json)

{
  "scripts": {
    ...
    "cy:open" : "cypress open",
    ...
  }
}
```

- Set up Cypress Testing Library

```shell
yarn add -D @testing-library/cypress
```

```js
// (cypress/support/commands.js)

import "@testing-library/cypress/add-commands";
```

- Add type definitions to Typescript `compilerOptions` object

```json
// (tsconfig.json)

{
  ...
  "types": [
    "cypress",
    "@types/testing-library__cypress",
    ...
  ]
  ...
}
```

- Write and run smoke test

```shell
$EDITOR cypress/e2e/smoke.js
yarn cy:open
```

- ...

```shell
yarn add -D eslint-plugin-cypress
```

#### Further information <!-- omit in toc -->

[End-to-end Testing in Gatsby Projects](https://www.gatsbyjs.org/docs/end-to-end-testing/)

[Writing Cypress Tests](https://docs.cypress.io/guides/getting-started/writing-your-first-test.html#Write-a-real-test)

[CTL Intellisense for JavaScript with VS Code](https://github.com/testing-library/cypress-testing-library#installation)

## 3. Unit testing

### Jest + React Testing Library

- `yarn add -D jest react-testing-library`
- (jest.config.js) configure as per link below
- (package.json) add `jest` npm script
- write unit test & run

#### Further information <!-- omit in toc -->

<https://www.gatsbyjs.org/docs/unit-testing/>

## 4. CI

### Automated testing

TODO:

### Automated versioning

TODO:

### Automated packaging

TODO:

## 5. CD

### Automated deployment

TODO:

### Automated monitoring

TODO:
