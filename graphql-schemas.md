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
    category: Category!
}
```

There are 5 built-in scalar types with GraphQL: `Int`, `Float`, `String`, `Boolean` and `ID`. Scalar types, as opposed to object types, point to actual data. The `ID` type resolves to a string, but expects a unique value.

#### Enumerations

Enumeration types allow to define a specific subset of possible values for a type. In the previous example, the `Category` enum type can take a value of `Clothes`, `Shoes` or `Watches` and anything else will result in a validation error.  We need to update our example providing definition of our enumeration category : 

```text
enum Category {
  Clothes
  Shoes
  Watches
}

type Product { 
    title: String! 
    SKU: ID!
    descirption: String!
    price: Float!
    stock: Int!
    category: Category!
}
```

#### Type modifiers

Modifiers can be used on the type that a field resolves to, by using characters like **`!`** and **`[…]`**. Here’s a breakdown, using the `String` scalar type as an example:

* `String`: nullable string \(the resolved value can be null\)
* `String!`: Non-nullable string \(if the resolved value is null, an error will be raised\) 
* `[String]`: Nullable list of nullable string values. The entire value can be null, or specific list elements can be null. 
* `[String!]`: Nullable list of non-nullable string values. Then entire value can be null, but specific list elements cannot be null. 
* `[String!]!`: Non-nullable list of non-nullable string values. Nothing can be null, neither the whole value nor the individual items. 





