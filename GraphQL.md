\# Resource

GraphQL 中文社区 有很多不错的学习材料

https://graphql.cn/community/

https://www.prisma.io/blog/graphql-server-basics-the-schema-ac5e2950214e

GraphQL 线上社区

https://discordapp.com/channels/102860784329052160/102860784329052160

GraphiQL Playground

https://graphql.org/swapi-graphql

GraphQL 入门教程:

https://graphql.org/learn/

GraphQL Reference: https://graphql.org/graphql-js/graphql/

\# External Learning

\## [the road to GraphQL]()

GraphQL Query

\```

\# 当使用了variable的时候就必须要用到query关键字，后面接variable的声明

query ($organization: String="ck-private") { #这里还用到了默认值

organization(login: $organization){

name

url

}

}

\```

\```

\# 可以给query起名字

query OrganizationFromChina ($organization: String!) {

organization(login: $organization){

name

url

}

}

\```

query最后的终结点必须是基本类型 Scalar Type 如果不是的话 就需要不断的进行subselect选出需要返回的段

\## [GraphQL Query Official Tutorial](https://graphql.org/learn/)

types + fields on those types

\```

type Query {

me: User

}

type User {

id: ID

name: String

}

\```

provide functions for each field on each type

\```

function Query_me(request) {

return request.auth.user;

}

function User_name(user) {

return user.getName();

}

\```

i.e query

\```

{

me {

name

}

}

\```

i.e. response

\```

{

"me": {

"name": "Luke Skywalker"

}

}

\```

\### [Queries and Mutations](https://graphql.org/learn/queries/)

Fields: String, Object

Arguments: Every field and nested object can get its own set of arguments == making multiple API fetches in REST

\```

\# query

{

human(id: "1000") { # here is arg1

name

height(unit: FOOT) # here is arg2

}

}

\```

\```

\# return

{

"data": {

"human": {

"name": "Luke Skywalker",

"height": 5.64

}

}

}

\```

Argument Types:

\* Enumeration type

[Mutation](https://www.youtube.com/watch?v=DU77lbBPfBI&list=PL4cUxeGkcC9iK6Qhn-QLcXCXPQUov1U7f&index=18)

\#### Aliases: avoid conflict, 因为field在定义的时候是相同的值得话会产生冲突

You can't directly query for the same field with different arguments.

问题: How to define Aliases ? 自定义参数前缀即可?

\```

{

empireHero: hero(episode: EMPIRE) {

name

}

jediHero: hero(episode: JEDI) {

name

}

}

\```

冲突实例:

![356102a17af3f633d4ba6a12f7a3ea04.png](evernotecid://1FC78D12-88FB-4FAC-95A1-F7FB5953B0DF/appyinxiangcom/29211871/ENResource/p83)

\#### Fragments (reusable units - sets of fields)

问题: scalar fields: You can even pass arguments into scalar fields, to implement data transformations once on the server, instead of on every client separately. ? what is this ?

问题: 定义Fragment on 是on 在哪上面的?

\* How to define it ?

\```graphql

{

leftComparison: hero(episode: EMPIRE) {

...comparisonFields

}

rightComparison: hero(episode: JEDI) {

...comparisonFields

}

}

fragment comparisonFields on Character {

name

appearsIn

friends {

name

}

}

\```

\#### Variables (enable us to deal with dynamic parameter)

U

Used in dropdown, search bar

How to use it?

\- Replace the static value in the query with `$variableName`

\- Declare `$variableName` as one of the variables accepted by the query

\- Pass `variableName: value` in the seperate, variables dictionary

\```

query HeroComparison($first: Int = 3) {

leftComparison: hero(episode: EMPIRE) {

...comparisonFields

}

rightComparison: hero(episode: JEDI) {

...comparisonFields

}

}

fragment comparisonFields on Character {

name

friendsConnection(first: $first) { #set the first to 3, only show the first 3 friends

totalCount

edges {

node {

name

}

}

}

}

\```

\#### Operation name

\- `query`

\- `type`

\- `mutation` function？

\- `schema{...}` 最后是在导出？

\####

\#### Directives (dynamically change the stucture and shape of our queries)

Example:

![8e41ac64ab55aa9e56b67c7ea884396c.png](evernotecid://1FC78D12-88FB-4FAC-95A1-F7FB5953B0DF/appyinxiangcom/29211871/ENResource/p84)

A *directive* can be attached to a field or fragment inclusion.

\* `@include(if: Boolean)` : Only include this field in the result if the argument is true

\* `@skip(if: Boolean)`: Skip this field if the argument is true

\#### Mutation (modify server-side data)

\```

mutation CreateReviewForEpisode($ep: Episode!, $review: ReviewInput!) {

createReview(episode: $ep, review: $review) {

stars

commentary

}

}

// Variables

{

"ep": "JEDI",

"review": {

"stars": 5,

"commentary": "This is a great movie!"

}

}

\```

mutate and query the new value of the field with one request.

Distinction between queries and mutations: query are executed in parallel, mutation fields run in series, one after the other. avoid race condition

\#### Inline Fragments

define interfaces and union types

\#### 语法表

\- `!`: 表示non-nullable

\- `...`:

\- $ :

\### [Schemas and Types]()

\#### Types

\- Scalar Type: 标量

\- Object Type

\- input object type: a special kind of object type that can be passed in as an argument

\- Interface

\- Union type

\### [GraphQL Full Course - Youtube](https://www.youtube.com/watch?v=ed8SzALpx1Q)

\* REST vs. GraphQL: query book data

\* REST

\* `domain.com/books/:id`

\* `domain.com/authors/:id`

\* GraphQL

\```graphql

{

book(id: 123) {

title

genre

author {

name

bio

books {

name

}

}

}

}

\```

GraphQL的图模型 嵌套的节点是相邻的

![14a562fbdc9bcfffbee62060a97d0082.png](evernotecid://1FC78D12-88FB-4FAC-95A1-F7FB5953B0DF/appyinxiangcom/29211871/ENResource/p85)

Apollo 是干嘛的 为什么需要在client端使用?

Mutation

Query中的keyword + 各个keyword的作用

什么是GraphQL middleware ?

need to know how our app looks

Schema 是用来描述data 的type + data之间的关联的?

比如上图之中就有Book 和 Author 两个不同的数据类型 关系是怎么组织的?

全部

Object type

Relation between different object

reach into the graph and interact the graph

Root Query -> entry point

Schema Definition:

\* types:

\* relationships:

\* root query

graphql后缀文件

RootQuery

FabricCard

```
union PortalsResponse = PortalsSuccessResponse
```

`input` 关键字

\#### Resolve Function

resolve function 是用来get data的

// dummy data

var books = [

{ name: 'Name of the Wind', genre: 'Fantasy', id: '1' },

{ name: 'The Final Empire', genre: 'Fantasy', id: '2' },

{ name: 'The Long Earth', genre: 'Sci-Fi', id: '3' },

];

```
{"errors":[{"message":"Must provide query string."}]}
```

Define Type

\```

const BookType = new GraphQLObjectType({

name: ''

})

\```

\#### Lesson 13. Type Relations

将相关联的type进行合并查询

在Type之中定义另一个Object Type

然后在另一个Query里面可以直接使用parent变量来上一级Type的信息

```
resolve(parent, args)
```

\* 接受的`parent`是在schema的上一级传入的

\* `args`是用户的query传入的

\#### Lesson 14. GraphQL Lists

定义一个GraphQL List`GraphQLList`

使用

\```

resolve(parent, args){

return _.filter(books, {authorId: parent.id})

}

\```

\## CK Internal Learning

\### [BootCamp- An Intro to GraphQL Development @ CK](https://docs.google.com/presentation/d/1sjaGz1Cu_jMWgncVYaHlsrpE_DC62w8vE8TCKCs5zYg/edit#slide=id.g7c05610e38_2_59)

[GraphQL Sandbox Playground](https://code.corp.creditkarma.com/ck-private/cinf_sandbox-graphql-service)

\#### REST API vs GraphQL API

The Usual Flow - REST API

![edac8a85dbe206f006cd0f0d04de3ac4.png](evernotecid://1FC78D12-88FB-4FAC-95A1-F7FB5953B0DF/appyinxiangcom/29211871/ENResource/p86)

GraphQL is the next step in the evolution of APIs

A query language for APIs and a runtime for fulfilling those queries with

GraphQL allows you to

Ask for what you need and get exactly

Get many resources in a single request

Describe what's po

\* GraphQL Glossary

\- Schema: A set of types describe a graph

\- Types: Representation of the kind of schema object 可以看做一个类，包含多种信息

\- Resolvers: Functions that describe how the fetched data(GraphQL可能需要从不同的source拿数据,process) should be transformed

\- Query: Request for data

\- Mutation: Request to update data

\- Operation Name: Unique name that describes the query/mutation

\- Fragment: Reusable snippets of fields

\- Directive: Dynamic flag to include or skip an operation

\#### Frontend GraphQL at CK & Demo

[Galaxy-Apollo repo](https://code.corp.creditkarma.com/ck-private/fett_galaxy-apollo)

GraphiQL: client

Schema Example

\#### Backend GraphQL Architecture

Clients -> GraphQL Gateway ->

Queries are split up and delegated to services

Common Type Resolvers

问题: Scala 是在哪用到的?

GraphQL gateway 和 FRONTIER是一个作用，FRONTIER更旧

缺点:

One bad apple can block everyone

Transitioning