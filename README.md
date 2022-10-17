Step-1 commitlint and Husky Git Hooks
we need husky Hooks to enforce commit lint for our code with commitlint Lets first install https://github.com/conventional-changelog/commitlint module

<h1 align="center">
  NodeJS / TypeScript Server Starter Kit 
</h1>

> Basic starter kit to create an App using `npx gts init` and most of the best packges or tools for dates, fetching, tests, coverage, linting, formatting and more.

## About GTS

GTS is Google's TypeScript style guide, and the configuration for our formatter, linter, and automatic code fixer. No lint rules to edit, no configuration to update, and no more bikeshedding over syntax.

To add webhooks features please add the following command:

`npx husky add .husky/commit-msg "npx --no -- commitlint --edit ${1}"`

## Table of Contents

- [About GTS](#about-gts)
- [Table of Contents](#table-of-contents)
- [Getting Started](#getting-started)
- [Prerequisites](#prerequisites)
- [VS Code Plugins](#vs-code-plugins)
  - [Must](#must)
  - [Optionals](#optionals)
- [Available Scripts](#available-scripts)
  - [`npm start:dev`](#npm-startdev)
  - [`npm test`](#npm-test)
  - [`npm run build`](#npm-run-build)
  - [`npm run eject`](#npm-run-eject)
  - [`npm run lint`](#npm-run-lint)
- [File Structure](#file-structure)
- [Conventions](#conventions)
  - [Organization / Best practices](#organization--best-practices)
- [Tools](#tools)

## Getting Started

For Luminus Life+ we need to have a good starter point to start a project with NodeJS / TypeScript, including basic plugins, best practices, conventions, file structure, and more. You should use this template for API, Services and BackEnd projects that not include NESTJS or STRAPI as main framework.

So basically, what you have here is a nodejs starter project created with `npx gts init` and essential configurations to start a clean and fast NodeJS App:

- Support for reactive programming (RxJs).
- Support for functional programming (Ramda).
- Support for IoC, DI (inversify).
- Support for Reflection (reflect-metadata).
- Object-object mapping support (AutoMapperTs).
- Unit testing and Coverage tests (jest, supertest).
- Lint and formatting (ESLint + GTS + Prettier).
- Datetime library (moment).
- Solid and recommended file structure.
- Configuration files.

So feel free to fork, propose new features and tools. We will be checking constantly PRs and merging the best features.

Run `npm i` and then `npm run start:dev`.

## Prerequisites

NodeJS
https://nodejs.org/en/

GTS
https://github.com/google/gts

## VS Code Plugins

Our official IDE is VS Code so we are going to include a list of basic plugins for NodeJs.

### Must

- Jest
- ESLint
- Prettier
- EditorConfig for VS Code
- DotENV

### Optionals

- Auto Close Tag
- Auto Rename Tag
- Auto import - ES6
- Path Intellisense
- TODO Highlight

## Available Scripts

In the project directory, you can run:

### `npm start:dev`

Runs the app in the development mode.<br>

### `npm test`

Launches the test runner in the interactive watch mode.<br>

### `npm run build`

Builds the app for production to the `build` folder.<br>

### `npm run eject`

**Note: this is a one-way operation. Once you `eject`, you can’t go back!**

### `npm run lint`

Lints all the files inside `./src` and shows the result without fixing.

## File Structure

Folder structure is based on productivity:

```text
src
├── application             * Application Layer (dto, services, adapters, etc).
│   └── ...
├── assets                  * Assets that are imported into your components(images, custom svg, etc).
│   └── ...
├── config                  * Config files (bootstrapper, etc.)
│   └── ...
├── core                    * Core interfaces and implementations for the app.
│   └── interfaces          * Contracts, interfaces.
│   └── impl                * Implementations or concret classes
├── domain                  * Domain Layer (model objects, aggregate, entities, value objects, etc).
│   └── ...
├── infrastructure          * Infrastructure Layer (database, service bus, etc).
│   └── ...
├── models                  * Common data models, constants, etc.
│   └── ...
├── shared                  * Common code (utils, providers, builders, etc.)
│   └── ...
├── index.ts                * Main execution point.
```

**Some important root files**

```text
.
├── .editorconfig           * Coding styles (also by programming language).
├── .env                    * Environment variables (env.production, env.local, env.uat, etc).
├── .eslintrc.json          * ESLint configuration and rules.
├── .prettierrc             * Formatting Prettier options.
└── tsconfig.json           * TS compiler configurations (eg. set the root folder for roots when import files).
```

## Conventions

All the conventions are based on Google Style Guide: https://google.github.io/styleguide/tsguide.html

### Organization / Best practices

Fo reference to our best practices, please see: https://llplus.atlassian.net/wiki/spaces/TT/pages/34242619/Patterns+and+Best+Practices

## Tools

- [Ramda](https://ramdajs.com/) A practical functional library for JavaScript/TypeScript programmers.
- [RxJs](https://rxjs.dev/) A practical Reactive Extensions Library for JavaScript/TypeScript.
- [Inversify](https://inversify.io/) A powerful and lightweight inversion of control container.
- [Automapper](https://automapperts.netlify.app/) An object-object mapping solution by convention in TypeScript
