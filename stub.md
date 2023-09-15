---
system_prompt: |
  You are an AI programming assistant, code generator and a documentation program.

  Each step of your response must strictly follow this markdown code block format :

  DESCRIPTION 

  ```LANG
  CODE
  ```
  where the tokens must be replaced such that:
  DESCRIPTION is a short but clear description of why you're doing that step. The description should include the fully qualified file name for the code block, including the file extension and the full directory path.
  LANG is the markup code block language for the code's language, and CODE is the code.

  Please note that the code should be fully functional. No placeholders.
  For any commands, add parameters to auto confirm defaults for any prompts on stdin. 
  Assume that the directory for the app has already been created and you are inside it, do not create a new directory.
  Use an env file for any variables like usernames, passwords, auth tokens or secrets.
model: gpt-4
temperature: 0
---

### Create your prompts below and Stub will generate the code and documentation


```stub
Create a high quality codebase with NestJS and TypeORM for all the CRUD API endpoints with the following entity:
- User, with attributes : name, email

Use nest generate resource command. 
Create production quality code that uses the best architecture.

```

<details open id="7829489487c2499e8740c44250e647d5">
<summary></summary>

First, we need to install NestJS CLI globally on your machine. This will allow us to use the `nest` command to generate and manage our NestJS projects.

```bash
npm install -g @nestjs/cli
```

Next, we create a new NestJS project.

```bash
nest new user-crud-app
```

Navigate into the newly created project directory.

```bash
cd user-crud-app
```

Now, we need to install the necessary packages for TypeORM and the database driver. In this case, we'll use PostgreSQL as our database, but you can replace `pg` with the driver of your choice.

```bash
npm install --save @nestjs/typeorm typeorm pg
```

Next, we generate the User resource. This will create all the necessary files and boilerplate code for a CRUD API for the User entity.

```bash
nest generate resource user
```

Now, we need to configure TypeORM. We'll create an `.env` file to store our database connection details. 

```bash
touch .env
```

Inside the `.env` file, add the following:

```env
DATABASE_TYPE=postgres
DATABASE_HOST=localhost
DATABASE_PORT=5432
DATABASE_USERNAME=your_username
DATABASE_PASSWORD=your_password
DATABASE_DATABASE=your_database
```

Next, we need to configure TypeORM to use these environment variables. In the `src/app.module.ts` file, import the `ConfigModule` and `TypeOrmModule`, and add them to the `imports` array in the `@Module` decorator.

```typescript
import { Module } from '@nestjs/common';
import { ConfigModule } from '@nestjs/config';
import { TypeOrmModule } from '@nestjs/typeorm';

@Module({
  imports: [
    ConfigModule.forRoot(),
    TypeOrmModule.forRoot({
      type: process.env.DATABASE_TYPE,
      host: process.env.DATABASE_HOST,
      port: +process.env.DATABASE_PORT,
      username: process.env.DATABASE_USERNAME,
      password: process.env.DATABASE_PASSWORD,
      database: process.env.DATABASE_DATABASE,
      entities: [__dirname + '/**/*.entity{.ts,.js}'],
      synchronize: true,
    }),
  ],
})
export class AppModule {}
```

Finally, we need to define our User entity. In the `src/user/entities/user.entity.ts` file, add the following:

```typescript
import { Entity, Column, PrimaryGeneratedColumn } from 'typeorm';

@Entity()
export class User {
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  name: string;

  @Column()
  email: string;
}
```

This completes the setup for a NestJS project with TypeORM for a User entity with CRUD operations.
</details>



