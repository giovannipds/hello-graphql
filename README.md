# Learning GraphQL

https://www.howtographql.com/

- Created by Facebook in 2012, presented to the world in 2015 and open-sourced
- It's a query language for APIs, not a database tech
- Single endpoint (REST needs multiple, it's more efficient than REST)
- Faster development: backend and frontend can work without communication
- Accepts different clients/frontends: you can request whaetever you want, declarative data fetching
- Returns a JSON with the prop "data"
- Designed due to the increase mobile usage (less data travelling)
- Large community already
- Better than REST
- It's always a POST request
- Resolves overfetching and underfetching
- Analytics for Backend
- Schema and Type System: SDL = Schema Defition Language
- Netflix created an alternative called Falcor: https://netflix.github.io/falcor/

We use query to fetch something:

```graphql
query {
  TypeName(filters) {
    fields
  }
}
```

SDL:

```graphql
type Person {
  name: String!
  age: Int!
  father: Person!
  friends: [Person!]!
}
````

- The ! means required
- Can have relations, single and multiple
- rootFields and arguments fields (allPersons is root, name is arguments)

Queries:

```graphql
{
  allPersons {
    name
  }
}
```

- last parameter to return only the last 2 items
- first paramter to return the first N items
- The changes to the API are made through Mutations (updating, creating, deleting). They always start with the Mutation keyword

```graphql
mutation {
  createPerson(name: "Bob", age: 36) {
    name
    age
    id
  }
}
```

- GraphQL adds/have unique IDs for entities
- Realtime updates are done by Subscriptions

```graphql
subscription {
  newPerson {
    name
    age
  }
}
```

- root Types: type Query, type Mutation, type Subscription
- To allow allPersons query, how to do:

```graphql
{
  allPersons {
    name
  }
}

type Query {
  allPersons(last: Int): [Person!]!
}
```

- To create a mutation, it's similar, needs to define a typeMutation with that name. Same for subscription. It will end up with a whole Schema that definies all the capabilities. Later we add the allPosts to the type Query. Exercise: update relationship between Person and Post. What I would answer:

type Mutation {
  updatePostAuthor(author: Person!): Post!
}

- Spec: http://spec.graphql.org/
- Needs a GraphQL server/service for that

Architecture cases:
- GraphQL server connected with a database
- GraphQL server to integrate existing system
- Hybrid approach of the ones above

Resolver functions
```graphql
User(id: String!): User
````

GraphQL libraries like Relay or Apollo allows you to just describe and display.
