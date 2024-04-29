# course-api
Mock API for "Web Services and APIs" course using https://my-json-server.typicode.com/. See guide for Javascript fetch code examples and sample nested routes at https://jsonplaceholder.typicode.com/guide/. Documentation for all available routes at https://github.com/typicode/json-server#routes. NOTE: Free service limits include: 10KB ```db.json``` max, 5 max REST endpoints, and 30 max items per endpoint.
- An example nested route: https://my-json-server.typicode.com/jasonclark/course-api/items/1/users. 
- An example full-text search route: https://my-json-server.typicode.com/jasonclark/course-api/items?q=skateboard. 
- An example using LIKE (_like) operator: https://my-json-server.typicode.com/jasonclark/course-api/items?description_like=play.

# Getting Started
1. Create a repository on GitHub (```<your-username>```/```<your-repo>```)
2. Create a ```db.json``` file
3. Visit https://my-json-server.typicode.com/ ```your-username/your-repo``` to access your server

# Routes

Based on the previous `db.json` file, here are some of the default routes.

## Plural routes

```
GET    /items
GET    /items/1
POST   /items
PUT    /items/1
PATCH  /items/1
DELETE /items/1
```

## Filter

Use `.` to access deep properties

```
GET /items?title=json-server&author=typicode
GET /items?id=1&id=2
GET /users?users.name=user%1
```

## Paginate

Use `_page` and optionally `_limit` to paginate returned data.

In the `Link` header you'll get `first`, `prev`, `next` and `last` links.


```
GET /items?_page=1
GET /items?_page=1&_limit=15
```

_10 items are returned by default_

## Sort

Add `_sort` and `_order` (ascending order by default)

```
GET /items?_sort=views&_order=asc
GET /items/1/users?_sort=id&_order=asc
```

For multiple fields, use the following format:

```
GET /items?_sort=name,id&_order=desc,asc
```

## Slice

Add `_start` and `_end` or `_limit` (an `X-Total-Count` header is included in the response)

```
GET /items?_start=2&_end=4
GET /items/1/users?_start=2&_end=4
GET /items/1/users?_start=2&_limit=5
```

_Works exactly as [Array.slice](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/Array/slice) (i.e. `_start` is inclusive and `_end` exclusive)_

## Operators

Add `_gte` or `_lte` for getting a range

```
GET /items?views_gte=10&views_lte=20
```

Add `_ne` to exclude a value

```
GET /items?id_ne=1
```

Add `_like` to filter (RegExp supported)

```
GET /items?title_like=skate
```

## Full-text search

Add `q`

```
GET /items?q=internet
```

## Relationships

To include children resources, add `_embed`

```
GET /items?_embed=users
GET /items/2?_embed=users
```

To include parent resource, add `_expand`

```
GET /users?_expand=items
GET /userss/1?_expand=items
```

## Database

```
GET /db
```

## Homepage

Returns default index file or serves `./public` directory

```
GET /
```
