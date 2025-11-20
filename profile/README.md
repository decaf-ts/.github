# Decaf-TS ☕️

![Banner](./resources/banner.png)

Welcome to **Decaf-TS** – the TypeScript framework that’s as modular as your morning coffee order, and just as likely to keep you up at night (with excitement, not bugs). If you’ve ever wanted to build fullstack apps with a dash of humor and a shot of flexibility, you’re in the right place!

## What is Decaf-TS?

Decaf-TS is a highly modular, TypeScript-first framework for building robust, scalable, and maintainable applications. Whether you’re brewing up a backend, a frontend, or a full-stack concoction, Decaf-TS lets you pick only the modules you need. No more gulping down monolithic frameworks!

## Why Decaf-TS?
- **Modular**: Like a coffee shop menu, pick only what you need.
- **TypeScript All The Way**: Strong types, strong coffee.
- **Persistence Adapters**: CouchDB, PouchDB, TypeORM, and more – we support more databases than your local café has milk alternatives.
- **UI Engines**: Angular, React, and more. Your UI, your way.
- **Decorator Magic**: Decorators everywhere. Because who doesn’t love a little syntactic sugar?

## Packages & Main Functionalities

### ☕️ Core Modules
- **@decaf-ts/decorator-validation**: Validate your models and your life choices.
  - *Use case*: Add validation rules to your models with decorators.
  - *Example*:
    ```ts
    @model()
    class User {
	  @required()
      name!: string;
    
      @email()
      email: string;
    }
    ```
- **@decaf-ts/db-decorators**: Decorators for database models. Because plain classes are so last season.
  - *Use case*: Define database schemas and relationships with decorators.
  - *Example*:
    ```ts
    @model()
    class Product {
      @id()
      id: string;
      
      @timestamp()
      updatedAt: Date;
    
      @onUpdated(onUpdateHandler, {})
      onUpdateField: string;
    }
    ```
- **@decaf-ts/core**: The heart of Decaf-TS. Repository patterns, query engines, and more.
  - *Use case*: Abstract data access and business logic.
  - *Example*:
    ```ts
    @table("product")
    @model()
    class Product {
      @gtin()
      @pk({type: "serial", generated: false})
      id: string;
      
      @column("created_at")
      @createdAt()
      createdAt: Date;
    
      @updatedAt()
      updatedAt: Date;
    
      @createdBy()
      createdBy: string;
    
      @updatedBy()
      updatedcy: string;
    
      @version()
      version: number;
    }
    
    const repo = Repository.forModel(Product);
    const created = await repo.create(new Product());
    
    const products = await repo.select().execute();
    ```
- **@decaf-ts/injectable-decorators**: Dependency injection, but make it TypeScript.
  - *Use case*: Inject services and repositories into your classes.
  - *Example*:
    ```ts
    @injectable()
    class UserService { ... }
    
    
    class Other {
      @inject()
      private userService!: UserService;
    
    }
    ```
- **@decaf-ts/transactional-decorators**: Transaction management. Because sometimes you need to roll back your mistakes.
  - *Use case*: Mark methods as transactional.
  - *Example*:
    ```ts
    @transactional()
    async updateUser(user: User) { ... }
    ```

### 🗄️ Persistence Adapters
- **@decaf-ts/for-couchdb**: CouchDB adapter. For when you want your data to lounge comfortably.
  - *Use case*: Integrate CouchDB with your repositories.
- **@decaf-ts/for-pouch**: PouchDB adapter. For digital wallets and offline dreams.
  - *Use case*: Use PouchDB for local-first apps.
  - *Example*:
    ```ts
    const pouchRepo = new PouchRepository<User>(User);
    ```
- **@decaf-ts/for-nano**: Nano adapter for CouchDB. Small, but mighty.
  - *Use case*: Use nano for lightweight CouchDB access.
- **@decaf-ts/for-typeorm**: TypeORM adapter. For the relationally inclined.
  - *Use case*: Use TypeORM with Decaf-TS repositories.
- **@decaf-ts/for-fabric**: Hyperledger Fabric adapter. Blockchain, but without the stress.
  - *Use case*: Integrate with Hyperledger Fabric for enterprise blockchain needs.

### 🎨 UI Engines
- **@decaf-ts/for-angular**: Angular UI engine. Turns your models into functional CRUD screens faster than you can say "ng serve".
  - *Use case*: Auto-generate Angular CRUD UIs from your models.
- **@decaf-ts/for-react**: React UI engine. Because hooks are the new black.
  - *Use case*: Build React UIs with model-driven forms and lists.
- **@decaf-ts/for-react-native**: React UI engine. Because hooks are the new black.
  - *Use case*: Build React UIs with model-driven forms and lists.
- **@decaf-ts/for-nextjs**: React UI engine. Because hooks are the new black.
  - *Use case*: Build React UIs with model-driven forms and lists.
- **@decaf-ts/ui-decorators**: UI decorators for all your rendering needs.
  - *Use case*: Annotate your models for UI rendering hints.

### 🛠️ Utilities & More
- **@decaf-ts/utils**: Utility functions. The duct tape of Decaf-TS.
  - *Use case*: Common helpers for all Decaf-TS modules.
- **@decaf-ts/logging**: Logging utilities. Because you need to know what went wrong (and right).
  - *Use case*: Structured logging for your app.
- **@decaf-ts/mcp-server**: Microservices, prompts, and more. For when you want to go big, but stay decaf.
  - *Use case*: Build microservices and prompt-driven workflows.
- **@decaf-ts/as-zod**: Zod integration. For schema validation that’s actually fun.
  - *Use case*: Use Zod schemas with Decaf-TS models.
- **@decaf-ts/decoration**: Advanced decoration utilities. Because your code deserves to look good.
  - *Use case*: Custom decorators and metadata utilities.

## Common Usage Example

```ts
import { Repository } from '@decaf-ts/core';
import { Entity, PrimaryKey } from '@decaf-ts/db-decorators';
import { IsEmail } from '@decaf-ts/decorator-validation';

@model()
class User {
  @pk()
  id: string;

  @email()
  email: string;
}

const repo = Repository.forModel(User);
const created = await repo.create(new User());
```

## Documentation & Website
- [Documentation](https://decaf-ts.github.io/decaf-ts)
- [Website](https://decaf-ts.github.io)

## Getting Started
1. Pick your modules.
2. Install with npm or yarn.
3. Add some decorators.
4. Profit (or at least, build something cool).

## Logo & Banner
![Logo](./resources/icon.png)

### Social

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0077B5?style=for-the-badge&logo=linkedin&logoColor=white)](https://pt.linkedin.com/in/tiagovenceslau)
---

> Decaf-TS: For developers who want all the flavor, none of the jitters.
