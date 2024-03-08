[![Banner](./resources/banner.png)](thhps://github.com/decaf-ts)

![Licence](https://img.shields.io/github/license/decaf-ts/decaf-ts.svg)


# decaf-ts
### Decaf's almost a Framework

##### Why we need a TS almost framework?

I know... like there aren't enough... Good this DECAF is not quite a Framework.

No. Really,

Often when developing distinct Typescript based R&D projects, I often struggled (or kept reinventing the wheel) to find standard ORM features other languages already offer. Be it because
- For some specific reason fell off the usual tech stacks:
  - unusual storage systems (eg: Blockchain);
  - strict lightweight requirements (near vanilla JS developments);
  - lack of consistent model validation for node;
  - non-relational storage;
- Or in more classical projects:
  - Insufficient/complex model control (validation, serialization, hashing, equality) that other languages typically support;
  - Consistent ORM behaviour in the frontend and backend;
  - Consistent Validation behaviour;
  - Boiler plate code in services/repositories;
- Or even when just considering the UI:
  - Boiler plate code in views for CRUD and listing;
  - Boiler plate code in controllers/services;
  - Lack of code portability;
  - Hi dependency-volume (hi bundle sizes);

Over time I started standardizing the functionality I really required (and that for the nature of the projects and some of the reasons above,
standard WebFrameworks were not desirable) into very small, lightweight modules that can be combined according to the feature required for each project

***Under development***

Wait for it...
Typescript library suite meant to fill the void of cross-platform, stable Typescript ORM frameworks 

### Modules

#### [@decaf-ts/decorator-validation](https://github.com/decaf-ts/decorator-validation)

Standalone module, defines the base Model class:
- decorator based validation api with recursive validation;
- hashing via configurable method;
- customizable serialization/deserialization to instantiation;
- Customizable Model building factories enabling nested instantiation;
- model equality;
- Easily extended custom validation;
- Java like date handling (format and serialization);
- Configurable error messages;

#### [@decaf-ts/db-decorators](https://github.com/decaf-ts/db-decorators)

Extension of `decorator-validation`, defines the base DBModel class:
- update capable decorator based validation api with recursive validation;
- implements configurable decorated based hooks for all CRUD operations:
  - on<operation>: hook will be called before the `operation`;
  - after<operation>: hook will be called after the `operation`;
- Defines the abstract `Repository` class that calls the respective hooks for each CRUD operation:
  - Developers are responsible for implementing the actual CRUD methods for their storage systems;

#### [@decaf-ts/injectable-decorators](https://github.com/decaf-ts/injectable-decorators)

Standalone module, exposes a simple implementation for Dependency injection:
- Injectables are singletons;
- they are injected by overriding a class's attribute `getter` and are only requested when actually needed, simplifying the injection order;
- Developer is responsible for originally instantiating them;

#### [@decaf-ts/transactional-decorators](https://github.com/decaf-ts/transactional-decorators)

Standalone module, exposes a simple implementation to handle concurrency:
- decorate methods as `@transactional()` for control;
- decorate classes as `@Transactional()`, enabling Instance proxying and keeping transactions across different classes/method calls (grouping several calls in a sing transaction)l
- Customizable Transaction Lock;
- Seamless integration with `db-decorators`;

#### [@decaf-ts/ui-decorators](https://github.com/decaf-ts/ui-decorators)

Extension of `db-decorators`, exposes a simple implementation to handle automatic model rendering:
- decorate classes and attributes as UI elements or UI element properties;
- provides the base objects to implement `ui-adapters` specific to each tech (Ionic, Angular, React, HTML5, etc);
  - automatic CRUD view rendering;
  - automatic UI validation according to `decorator-validation`'s decorators;
  - enables automatic custom validation (not HTML standard);

#### [@decaf-ts/ionic-ui-adapter](https://github.com/decaf-ts/ionic-ui-adapter)

Ionic adapter for `ui-decorators` (JSX);

#### [@decaf-ts/angular-ui-adapter](https://github.com/decaf-ts/angular-ui-adapter)

Angular adapter for `ui-decorators` (JSX);

#### [@decaf-ts/react-ui-adapter](https://github.com/decaf-ts/react-ui-adapter)

React adapter for `ui-decorators` (JSX);

#### [@decaf-ts/storage-wrapper](https://github.com/decaf-ts/storage-wrapper)

More opinionated (but very convenient) extension of `db-decorators`, and exposes all the functionality from the previous modules in a very extensible and developer friendly way:
- wraps any storage (blockchain, relational/non-relational databases and any other storage mechanism);
- automates the boiled plate code from `decorator-validation`, `db-decorators` and `injectable-decorators`;
- provides raw access to the storage;
- provides querying capabilities;
- Provides Repository apis for all selector Models;
- Initializes the storage according to the selected Models;

#### [@decaf-ts/sql-syntax](https://github.com/sql-syntax)

A very opinionated (but very convenient for certain cases, eg non relational dbs) extension of `storage-wrapper`, that wraps the native statement syntax
for each specific storage type in an easily recognizable SQL-like syntax in a functional approach:
- Extensible for all Database like storages;

#### [@decaf-ts/couchdb-wrapper](https://github.com/decaf-ts/couchdb-wrapper)

Extension of `storage-wrapper` and `sql-syntax` wrapper for couchdb compatible objects (couchDb, pouchdb, etc);

#### [@decaf-ts/hl-fabric-wrapper](https://github.com/decaf-ts/hl-fabric-wrapper)

Extension of `storage-wrapper` and `sql-syntax` wrapper to be used in Hyperledger Fabric SmartContracts:
  - Standard CRUD SmartContract for Maintaining state in the Ledger;
  - Standard ERC-20 SmartContract for maintaining token/currency;

### DECAF Lite

- @decaf-ts/decorator-validation;
- @decaf-ts/db-decorators;

### Backend DECAF suite

  - @decaf-ts/decorator-validation;
  - @decaf-ts/db-decorators;
  - @decaf-ts/injectable-decorators;
  - @decaf-ts/transactional-decorators; (optional)
  - @decaf-ts/storage-wrapper;
  - @decaf-ts/sql-syntax; (optional)
  - @decaf-ts/<storage>-wrapper; Suited for your storage (or many)

### Fullstack DECAF suite

  - @decaf-ts/decorator-validation;
  - @decaf-ts/db-decorators;
  - @decaf-ts/injectable-decorators;
  - @decaf-ts/transactional-decorators; (optional)
  - @decaf-ts/storage-wrapper;
  - @decaf-ts/sql-syntax; (optional)
  - @decaf-ts/<storage>-wrapper; Suited for your storage (or many)
  - @decaf-ts/ui-decorators;
  - @decaf-ts/<adapter>-ui-adapter; Suited for your frontend Framework (or several);

### Considerations

#### Typescript Compilation options

Even though all code is exported in both CommonJS and ESM format, and the default is ES2022
in order to take advantage to all the latest Typescript and JS features,
when importing  these libraries the following flag in `tsconfig.compilerOptions` is mandatory:
```json
  ...
  "experimentalDecorators": true,
  "emitDecoratorMetadata": true,
  "useDefineForClassFields": false
  ...
```

When using the `storage-wrapper` module, the following flag is also required:
```json
  ...
  "esModuleInterop": true,
  ...
```




### Related Projects

- [Pharmaledger](https://pharmaledger.h2020.eu): R&D project where the [OpenDSU Framework](www.opendsu.com) was used as a middleware to store data on the Quorum/Hyperledger Fabric blockchain. Initial concept and approach developed over the course of this project;
- [Glass](https://glass.h2020.eu): R&D project where the initial version of this suite was developed and implemented to store Self Sovereign Data on the Hyperledger Fabric Blockchain and render data via in an Ionic environment;
- [Aeon](https://glass.h2020.eu): R&D project the beta version of this suite was implemented in full (Angular, couchdb, pouchdb, Hyperledger Fabric and nestJS integration);

### Social

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://pt.linkedin.com/in/tiagovenceslau)
