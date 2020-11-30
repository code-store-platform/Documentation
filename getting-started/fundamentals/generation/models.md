# Models

## Overview

code.store platform by default use [Postgres](https://www.postgresql.org/) RDBMS with [TypeORM](https://typeorm.io/#/) and provides opportunity to generate  models and migrations based on your `schema.graphql`. 

> \_\_[_PostgreSQL_](https://www.postgresql.org/) is a powerful, open source object-relational database based on SQL and supports many of the features of the SQL standard.

> [_TypeORM_](https://typeorm.io/#/) is amazing ORM for TypeScript and JavaScript \(ES7, ES6, ES5\). Supports many SQL databases, including MySQL, PostgreSQL,

Each time, when you develop your application you should carry about your `data layer` - the place, where database entities, migrations, seeds... are defined. code.store shared developers pain and provide amazing ability automatically generate [TypeORM](https://typeorm.io/#/) entities and SQL migrations for your database. 

When you create a new type or input for your query or mutation inside `schema.graphql`, which located in your `src` service directory, or make changes to already existed types you should make changes inside your data models and think about migrations... You don't have to do it each time, code.store platform provides `cs generate:models` CLI command, which allows to do whole magic for you!

## Generate models and migrations

Models and migrations are powerful tool, which allows you to generate complex things. Generator supports different types and relations such as one-to-one, one-to-many, many-to-many... 

### Simple entity

First of all, you should define your types in `schema.graphql`, which located in `src` directory of your service. For example, let's define a simple type `Post` with some fields:

```text
type Post {
    id: ID!
    createdAt: String!
    title: String!
    body: String!
    authorName: String!
}
```

After `schema.graphql` modification execute `cs generate:models` CLI command, which will trigger generation process. During command execution `schema.graphql` file will upload to code.store's generator. code.store's generator will validate this schema, generate TypeORM entities and migrations and save it on your local machine on `src/generatedData` folder:

```text
> cs generate:models

✔ Reading the service schema
✔ Uploading the service schema to the generator
✔ Generated code has been saved to ...demo_app/generatedData 
```

### Generated data

`generatedData/` includes two directories:

* `entities/` dir with your TypeORM entities
* `migrations/` dir with SQL migrations

{% hint style="success" %}
code.store's generator allows you to generate models and migrations both for service which already has models and migrations and for an empty project, where you just define your GraphQL schema.
{% endhint %}

For `Post` type generated next migration in `src/generatedData/migrations/Migration1606769241856.ts` file:

```text
import {MigrationInterface, QueryRunner} from "typeorm";

export class Migration1606769241856 implements MigrationInterface {
    name = 'Migration1606769241856'

    public async up(queryRunner: QueryRunner): Promise<any> {
        await queryRunner.query(`CREATE TABLE "Post" ("id" BIGSERIAL NOT NULL, "createdAt" varchar NOT NULL, "title" varchar NOT NULL, "body" varchar NOT NULL, "authorName" varchar NOT NULL, CONSTRAINT "PK_c4d3b3dcd73db0b0129ea829f9f" PRIMARY KEY ("id"))`, undefined);
    }

    public async down(queryRunner: QueryRunner): Promise<any> {
        await queryRunner.query(`DROP TABLE "Post"`, undefined);
    }
}
```

There are two methods you must fill with your migration code: `up` and `down`. `up` has to contain the code you need to perform the migration. `down` has to revert whatever `up` changed. `down` method is used to revert the last migration. To learn more about TypeORM migrations visit [TypeORM migrations](https://github.com/typeorm/typeorm/blob/master/docs/migrations.md) page. 

Also, you can find a [TypeORM entity](https://github.com/typeorm/typeorm/blob/master/docs/entities.md) inside `generatedData/entities/Post.ts` file.

```text
import { Column, Entity, PrimaryGeneratedColumn } from 'typeorm';

@Entity('Post')
export default class Post {
  @PrimaryGeneratedColumn()
  id: number;

  @Column()
  createdAt: string;
  
  @Column()
  title: string;
  
  @Column()
  body: string;
  
  @Column()
  authorName: string;
}

```

### Apply generated changes

If everything is OK and generated files meet your needs - just copy them to the appropriate directories: `src/data/entities`  and `src/data/migrations`.

To make sure that generated entity is correct, just execute `cs dev` CLI command. As a result you can find the `Post` table inside your database. More information about local launch of your code you can find in [local development](https://app.gitbook.com/@code-store/s/docs/~/drafts/-MN4H3I2PJY1gdFVV4SY/getting-started/fundamentals/services#local-development) section.

{% hint style="danger" %}
We recommend use entities and migrations generation as bootstrap feature. Always check the files that are generated to avoid surprises.
{% endhint %}









