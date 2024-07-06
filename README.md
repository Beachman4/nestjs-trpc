<a href="https://nestjs-trpc.io/" target="_blank" rel="noopener">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="https://i.imgur.com/JvsOXCg.png" />
    <img alt="tRPC" src="https://i.imgur.com/JvsOXCg.png" />
  </picture>
</a>

<div align="center">
  <h1>Nestjs tRPC Adapter</h1>
  <h3>An opinionated approach to building<br />End-to-end typesafe APIs with tRPC within NestJS.</h3>
  <figure>
    <img src="https://assets.trpc.io/www/v10/v10-dark-landscape.gif" alt="Demo" />
    <figcaption>
      <p align="center">
        The client above is <strong>not</strong> importing any code from the server, only its type declarations.
      </p>
    </figcaption>
  </figure>
</div>

## Introduction
**NestJS RPC** is a library designed to integrate the capabilities of tRPC into the NestJS framework. It aims to provide native support for decorators and implement an opinionated approach that aligns with NestJS conventions.

## Features
- ✅&nbsp; Supports most tRPC features out of the box with more to come.
- 🧙‍&nbsp; Full static typesafety & autocompletion on the client, for inputs, outputs, and errors.
- 🙀&nbsp; Implements the Nestjs opinionated approach to how tRPC works.
- ⚡️&nbsp; Same client-side DX - We generate the AppRouter on the fly.
- 🔋&nbsp; Examples are available in the ./examples folder.
- 📦&nbsp; Out of the box support for **Dependency Injection** within the routes and procedures.
- 👀&nbsp; Native support for `express`, and `zod` with more drivers to come!

## Quickstart

### Installation
To install **NestJS tRPC** with your preferred package manager, you can use any of the following commands:

```shell
# npm
npm install trpc-nestjs

# pnpm
pnpm add trpc-nestjs

# yarn
yarn add trpc-nestjs
```

## How to use
Here's a brief example demonstrating how to use the decorators available in **NestJS tRPC**:

```typescript
// users.router.ts
import { Router, Query, Procedure } from 'trpc-nestjs';
import { UserService } from './user.service';
import { TRPCError } from '@trpc/server';

const userSchema = z.object({
  name: z.string(),
  password: z.string()
})

@Router()
class UserRouter {
  constructor(
    @Inject(UserService) private readonly userService: UserService
  ) {
  }

  @Procedure(ProtectedProcedure)
  @Query({ output: z.array(userSchema) })
  async getUsers() {
    try {
      const users = await this.userService.getUsers();
      return users;
    } catch (e: unknown) {
      throw new TRPCError("An error has occured when trying to get users.", e)
    }
  }
}
```

**👉 See full documentation on [NestJS-tRPC.io](https://nestjs-trpc.io/docs). 👈**

## All contributors

> tRPC is developed by [Kevin Edry](https://twitter.com/KevinEdry), which taken a huge inspiration from both NestJS and tRPC inner workings.

<a href="https://github.com/KevinEdry/nestjs-trpc/graphs/contributors">
  <p align="center">
    <img width="720" height="50" src="https://contrib.rocks/image?repo=kevinedry/nestjs-trpc" alt="A table of avatars from the project's contributors" />
  </p>
</a>