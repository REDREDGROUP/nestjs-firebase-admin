## About this package

The original author of this repository is [Aginix Technologies Co., Ltd.](https://github.com/Aginix/nestjs-firebase-admin). The repertoire has been forked.

<a href="https://www.npmjs.com/@redredgroup/nestjs-firebase-admin"><img src="https://img.shields.io/npm/v/@redredgroup/nestjs-firebase-admin.svg" alt="NPM Version" /></a>
<a href="https://www.npmjs.com/@redredgroup/nestjs-firebase-admin"><img src="https://img.shields.io/npm/l/@redredgroup/nestjs-firebase-admin.svg" alt="Package License" /></a>
<a href="https://www.npmjs.com/@redredgroup/nestjs-firebase-admin"><img src="https://img.shields.io/npm/dm/@redredgroup/nestjs-firebase-admin.svg" alt="NPM Downloads" /></a>

## Description

Firebase Admin Module for [Nest.js Framework](https://nestjs.com/)

## Installation

```bash
$ yarn add @redredgroup/nestjs-firebase-admin #yarn
$ npm i @redredgroup/nestjs-firebase-admin --save #npm
```

### Import module

```typescript
import { Module } from '@nestjs/common';
import { FirebaseAdminModule } from '@redredgroup/nestjs-firebase-admin';
import * as admin from 'firebase-admin';

@Module({
  imports: [
    FirebaseAdminModule.forRootAsync({
      useFactory: () => ({
        credential: admin.credential.applicationDefault(),
      }),
    }),
  ],
})
export class AppModule {}

//Or the forRootAsync module using @nestjs/Config

import { Module } from '@nestjs/common';
import { FirebaseAdminModule } from '@redredgroup/nestjs-firebase-admin';
import * as admin from 'firebase-admin';

@Module({
  imports: [
    FirebaseAdminModule.forRootAsync({
      imports: [ConfigModule],
      inject: [ConfigService],
      useFactory: (config: ConfigService) => ({
        credential: admin.credential.cert({
          projectId: config.get('FB_PROJECT_ID'),
          clientEmail: config.get('FB_CLIENT_EMAIL'),
          privateKey: config.get('FB_PRIVATE_KEY'),
        }),
      }),
    }),
  ],
})
export class AppModule {}
```

## Example

### Inject Authentication Service
```typescript
import { Injectable } from '@nestjs/common';
import { FirebaseAuthenticationService } from '@redredgroup/nestjs-firebase-admin';

@Injectable()
export class AppService {
  constructor(private firebaseAuth: FirebaseAuthenticationService) {}

  getUsers() {
    return this.firebaseAuth.listUsers();
  }
}
```

## Compatibility Table

| firebase-admin | NestJS Library |
| -------------- | -------------- |
| `10.xx`        | `master`       |
| `10.xx`        | `1.0.1`        |
| `8.xx`         | `1.xx`         |
