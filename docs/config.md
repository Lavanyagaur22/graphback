---
id: config
title: CRUD Config
---

GraphBack takes input model and generates CRUD operations as queries and mutations.
 These include `create`, `update`, `delete`, `find` and `findAll`. These operations can be generated for each `type` in your model.
 Further Graphback also generates three predefined subscriptions, namely `new`, `updated` and `deleted`.
We can use them in clients to receive live updates for every change that is happening on the server.
  
 Graphback allows user to customize the generation process by using `configuration` and `directives`.

## Configuration
Graphback uses flags to allow user to choose between the CRUD operations and subscriptions. These are present in `config.json`, created during `init`,
in the root of your project folder under the `generation` key. The default config is
```json
{
  ...,
  "generation": {
    "create": true,
    "update": true,
    "findAll": true,
    "find": true,
    "delete": false,
    "subCreate": false,
    "subUpdate": false,
    "subDelete": false
  }
}
```
Changing these flags and performing `generate`, regenerates your `schema` and `resolvers` with provided config.
> **Note**: For subscriptions, the user needs to change the value of the respective operations to `true`. For example, changing 
`subDelete` to `true` won't work unless, `delete` is `true`.

## Directives
Changing the generator config applies the config to all the types in your schema. Graphback allows you to change these for any single type using directives. All the config flags are available as directives 
- `@create`
- `@update` 
- `@delete` 
- `@find`
- `@findAll`
- `@subCreate`
- `@subUpdate` 
- `@subDelete`.

User can use these directives to have more control on individual elements. For example, 
```
type Note @delete {
  ...
}
```
will create the `delete` mutation for `Note` type only.

> **Note**: Directives override the configuration flags to `true`, so to enable a operation through directive for a single `type`,
> the default configuration should be `false`. Otherwise it will effect every `type`, using flags from the configuration.