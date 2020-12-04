# Handlers

## Overview

To simplify authorization and authentication process code.store platform provide an opportunity to create an authorization handler for REST and context handler for your GraphQL API.

Authorization handlers released as middlewares and allows to implement custom authorization logic. 

## Generation

### Auth handler

To generate auth handler execute `cs generate:resolver` CLI command, select `auth` handler type:

```text
> cs generate:handler

? Select the type of resolver (Use arrow keys)
❯ auth 
  context 
```

{% hint style="info" %}
Also, you can use flags:

**-t** handler type, one of: 'context' or 'auth'
{% endhint %}

After command execution will be generated file `auth.handler.ts` in `src/resolvers` directory:

```text
import { AuthHandler } from 'codestore-utils';

const authHandler: AuthHandler = async (context) => {
  // your code goes here
  return {};
};

export default authHandler;
```

#### Usage

You can specify your authentication strategy here. This handler works as an authentication middleware which will be called for all GraphQL queries/mutations marked with directive @auth.

In order to use that directive in your GraphQL schema, add a following directive declaration at the top of your GraphQL file:

```text
directive @auth on FIELD_DEFINITION
```

Then use it in query/mutation declarations, for example:

```text
type Query {
    helloWorld: String! @auth
}
```

### Context handler

Use context handler as a handler, which will be execute before each GraphQL resolver. To generate context handler execute `cs generate:resolver` CLI command, select `context` handler type:

```text
> cs generate:handler

? Select the type of resolver (Use arrow keys)
  auth 
❯ context 
```

{% hint style="info" %}
Also, you can use flags:

**-t** handler type, one of: 'context' or 'auth'
{% endhint %}

After command execution will be generated file `context.handler.ts` in `src/resolvers` directory:

```text
import { ContextHandler } from 'codestore-utils';

const contextHandler: ContextHandler = async (context) => ({
  //  your code goes here
});

export default contextHandler;
```





