# GraphQL Schemas

On code.store platform we decided to use GraphQL as a primary way to interact with your services. You'll need to learn GraphQL basics   to create code.store services.

While you'll find all the details on [GraphQL site](https://graphql.org/), we've prepared you a short summary of GraphQL basics here. 

### What is GraphQL ?

GraphQL is an API standard that provides a more efficient, powerful and flexible alternative to REST. It was developed and open-sourced by Facebook but now many companies, including us support and rely of GraphQL. We do think it will become worldwide API standard very soon.

code.store GraphQL service is created by defining types and fields on those types, then providing micro-services for each field on each type.

### GraphQL types

GraphQL has its own type system that’s used to define the schema of an API. The syntax for writing schemas is called [Schema Definition Language ](https://graphql.org/learn/schema/)\(SDL\).

Here is an example how we can use the SDL to define a simple type called `Product`:

```text
type Product { 
    title: String! 
    SKU: ID!
    descirption: String!
    price: Float!
    stock: Int! 
}
```

There are 5 built-in scalar types with GraphQL: `Int`, `Float`, `String`, `Boolean` and `ID`. Scalar types, as opposed to object types, point to actual data. The `ID` type resolves to a string, but expects a unique value.



