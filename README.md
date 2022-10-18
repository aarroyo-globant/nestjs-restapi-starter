<h1 align="center">
  NESTJS API RESTFul Starter Kit 
</h1>

NEST includes out of the box several components. tools and utils predefined. Therefore, our priority is use those as much as we can. Hence,
our approach will be 100% based on the NESTJS definitions.

</br>

## Table of Contents

- [Table of Contents](#table-of-contents)
  - [**Features**](#features)
- [Project Setup](#project-setup)
- [Configuration and Database Setup](#configuration-and-database-setup)
- [Constants & Exceptions](#constants--exceptions)
- [Migrations Setup](#migrations-setup)
- [Basic Security Setup](#basic-security-setup)
- [Swagger Setup](#swagger-setup)
- [File Structure](#file-structure)
- [Tools](#tools)

</br>

### **Features**

- Quick start.
- API Versioning.
- Integrated ESLint, Prettier and Husky.
- Simple and Standard scaffolding.
- Production-Ready Skeleton.
- Followed SOLID Principles.
- Centralized error handling mechanism.
- Request data validation using [Nest JS Pipe](https://docs.nestjs.com/techniques/validation).
- Support for logging using [Winston](https://github.com/winstonjs/winston).
- Testing: unit and integration tests with [Jest](https://jestjs.io/).
- API documentation with [Open API / Swagger](https://www.openapis.org/).
- Dependency management with [npm](https://www.npmjs.com/)
- Environment variables using [dotenv](https://github.com/motdotla/dotenv).
- Set security HTTP headers using [helmet](https://helmetjs.github.io/)
- Cross-Origin Resource-Sharing enabled using [cors](https://github.com/expressjs/cors)
- Gzip compression with [compression](https://github.com/expressjs/compression)
- Git hooks with [husky](https://github.com/typicode/husky).
- [TypeORM](https://typeorm.io/), the most complete TypeScript ORM solution.
- [PostgreSQL](https://www.postgresql.org/), a free and open-source relational database management system.
- [Joi](https://www.npmjs.com/package/joi), for validation schemas, especially that of the configuration module.
- [Passport](https://www.passportjs.org/) for authentication.
- [Passport-jwt](http://www.passportjs.org/packages/passport-jwt/) for access token generation and verification.
- [Bcrypt](https://github.com/kelektiv/node.bcrypt.js) for hashing passwords.
- [Express-rate-limit](https://github.com/nfriedly/express-rate-limit) allows rate-limiting to protect the API against brute-force attacks.

</br>

## Project Setup

First, make sure you install all the dependencies of the project:

```javascript
npm install --save @nestjs/typeorm typeorm pg @nestjs/swagger @nestjs/config @nestjs/passport @nestjs/jwt passport passport-jwt bcrypt helmet express-rate-limit dotenv joi class-validator class-transformer

npm install --save-dev @types/passport-jwt @types/passport-jwt @types/bcrypt
```

To add webhooks features please add the following command:

> npx husky add .husky/commit-msg "npx --no -- commitlint --edit ${1}"

</br>

## Configuration and Database Setup

We’ll be putting most of our configuration in a .env file. So create a file of name .env in your project directory and paste the following content into it:

```javascript
# APP GENERAL
NODE_ENV="development"
PORT=3000
DEBUG=true

# DATABASE
DB_HOST=localhost
DB_PORT=5432
DB_USERNAME=postgres
DB_PASSWORD=your_db_password
DB_DATABASE=accounting-app
DB_SSL=false

# JWT SECURITY
JWT_SECRET=YourJwtSecretHere
ADMIN_ACCESS_TOKEN=YourSecureAdminAccessToken1234567
```

The values should be replaced with the correct ones for each of the environment variables.

> Since environment variables are not supposed to be exposed, make sure you add the.env file to your .gitignore file.

</br>

## Constants & Exceptions

Up to now, we’ve been focusing on environment variables but the API will also need constants such as the app’s name, set up somewhere in the app.

For this, we created a folder named `common` in your src folder and place two files in it: constants.ts and exceptions.ts

Place put in those files information used by the system and that can be constant:

```javascript
export const APP_NAME = 'NESTJS REST API Starter Kit';
export const APP_VERSION = '1.0.0';
export const PASSWORD_HASH_SALT: number = 10;
```

</br>
And the following in your exceptions.ts file:

```javascript
export const E_USER_EMAIL_TAKEN = 'Oops! This email is already taken!';
export const E_USER_NOT_FOUND = 'User not found!';
export const E_INCORRECT_EMAIL_OR_PASSWORD =
  'Email or password entered is incorrect!';
```

</br>

## Migrations Setup

Migrations are files that contain SQL queries for updating a database schema or applying new changes to an
existing database.

> TypeORM allows you to synchronize the database schema with the entities by setting `synchronize: true` in
> the database module configuration object. This is not recommended in production though,
> because they might cause unwanted data loss or transformation; Which is why, it’s better to set up migrations.

We have defined 4 script command in the `package.json` file:

| javascript         | Description                                                          |
| ------------------ | -------------------------------------------------------------------- |
| migration:create   | create migration                                                     |
| migration:generate | generate migrations based on --dataSource src/database/datasource.ts |
| migration:run      | execute migration                                                    |
| migration:revert   | revert a migration                                                   |

- Generate a migration whenever there’s a change in your entities: `Run: npm run migration:generate src/database/migrations/NameOfTheChange` . Make sure you replace NameOfTheChange with a name referring to the change you’ve actually made in your entities. Eg: CreateUsersTable
- Run migrations after every migration change. Make sure you’ve done npm run build before running migrations. Use the following command to run migrations: `npm run migration:run`

The above commands just allow you to work faster but you can always manually write your own migrations. To do so, first create an empty migration by running npm run migration:create src/database/migrations/NameOfTheChange , then open the migration generated at src/database/migrations/.

Inside every migration file there are two functions:

- Up: This is where you write the SQL code that applies the change in your database schema.
- Down: Here you write the SQL code that reverses whatever is done in the up function.

For more details, click [here](https://typeorm.io/migrations)

</br>

## Basic Security Setup

In order to mitigate or protect our API against certain security exploits, we’re going to implement helmet package,
enable CORS, and rate limiting. Hence, we are including in the main.ts file a basic configuration.

> **Note:**
> Nest has its own rate limiter called `@nestjs/throttler` which is actually richer and easier to use.
> I chose the express-rate-limit package because `@nestjs/throttler` seems, at the time of writing this article,
> to be having dependency conflicts with the latest Nest version.

</br>

## Swagger Setup

Nest provides the module `@nestjs/swagger`, which allows generating the OpenAPI specification using decorators,
and thus, automatically generating the documentation for our REST API.

We did add the code to your main.ts file’s bootstrap function before `app.listen()`.

> Our API’s documentation will, now, be accessible at the /docs path.

The `APP_NAME, APP_DESCRIPTION and APP_VERSION` in the code, are imported from
the `src/common/constants.ts` file that we set up earlier and the `DocumentBuilder`
and `SwaggerModule` objects are imported from the `@nestjs/swagger` module.

You may read more about implementing the OpenAPI specification(OAS) to a NestJS app [here](https://docs.nestjs.com/openapi/introduction).

</br>

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

</br></br></br></br></br></br>

## Tools

- [Ramda](https://ramdajs.com/) A practical functional library for JavaScript/TypeScript programmers.
- [RxJs](https://rxjs.dev/) A practical Reactive Extensions Library for JavaScript/TypeScript.
- [Inversify](https://inversify.io/) A powerful and lightweight inversion of control container.
- [Automapper](https://automapperts.netlify.app/) An object-object mapping solution by convention in TypeScript
