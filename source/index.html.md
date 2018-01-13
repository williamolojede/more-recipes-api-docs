---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

includes:
  - errors

search: true
---

# Overview &mdash; MoreRecipes Api
Welcome to the MoreRecipes API documentation. This is the API used by the MoreRecipes web interface, so everything the web ui is able to do can also be accomplished via the API.

This API provides the means for you to share, view and manage your recipes and those of others.

**`BASE API URL:`** ` https://more-recipes.herokuapp.com/api/v1/`

# Making Request

An authorization token is required to access all endpoints except the signup and Login endpoints. Use the login/signup endpoint to get a token

A token generated expires 48 hours after it has being generated.

The token can be placed in `req.headers`, `req.body` or `req.query`

`token: averylongrandom.jsonwebtokenstring.requiredforauthentication`

<aside class="notice">
  You must replace <code>averylongrandom.jsonwebtokenstring.requiredforauthentication</code> with your personal auth token.
</aside>

# Returning a list of items
All our api endpoints that returns a list of items are paginated by default, the response body includes pagination metadata which is described below. The pagination can be controlled using the query parameters page and limit

### Query Parameters
Parameter | Default | Description
--------- | ------- | -----------
page | 1 | The page number
limit | 12 | The max number of items per page

### Pagination Metadata
key | Description
--- | -----------
pages | An array of all page numbers
totalCount | Total number of items in the database
pageSize | The number of items returned for a page
page | The current page
last | The last page available

# User
## User signup
> Request Body

```json
  {
    "user": {
      "fullname": "William Olojede",
      "email": "william.olojede@yahoo.com",
      "password": "password"
    }
  }
```

> Response Body

```json
  {
      "status": "success",
      "message": "Account created",
      "user": {
          "id": 29,
          "email": "william.olojede@yahoo.com",
          "fullname": "William Olojede",
          "updatedAt": "2018-01-12T10:31:54.659Z",
          "createdAt": "2018-01-12T10:31:54.659Z",
          "username": null,
          "imgUrl": null
      },
      "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjp7ImlkIjoyOX0sImlhdCI6MTUxNTc1MzExNCwiZXhwIjoxNTE1NzU2NzE0fQ.sG-zNYLLSMTm6MtuhQ3XGZuTzsMqykeZSSzROkUvkNw"
  }
```
Creates a new user

### HTTP Request

* Endpoint: `/users/signin`
* Verb: `POST`
* Body: `(application/json)`

### HTTP Response
* StatusCode: `201 - Created`
* Body: `(application/json)`

## User login
> Request Body

```json
  {
    "user": {
      "email": "william.olojede@yahoo.com",
      "password": "password"
    }
  }
```

> Response Body

```json
  {
    "status": "success",
    "message": "You are successfully logged in",
    "user": {
        "id": 29,
        "username": null,
        "email": "william.olojede@yahoo.com",
        "fullname": "William Olojede",
        "imgUrl": null,
        "createdAt": "2018-01-12T10:31:54.659Z",
        "updatedAt": "2018-01-12T10:31:54.659Z"
    },
    "token":"eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJ1c2VyIjp7ImlkIjoyOX0sImlhdCI6MTUxNTc1Mzg2MywiZXhwIjoxNTE1NzU3NDYzfQ.KTXHD-SDIpJr_I5hixbm9R2OJtttDH1IKK58bCwGykE"
  }
```
Logs in user

### HTTP Request

* Endpoint: `/users/login`
* Verb: `POST`
* Body: `(application/json)`

### HTTP Response
* StatusCode: `200`
* Body: `(application/json)`

## User profile
> Response Body

```json
{
  "status": "success",
  "message": "user found",
  "user": {
    "id": 29,
    "username": null,
    "email": "william.olojede@yahoo.com",
    "fullname": "William Olojede",
    "imgUrl": null,
    "createdAt": "2018-01-12T10:31:54.659Z",
    "updatedAt": "2018-01-12T10:31:54.659Z"
  }
}
```
Gets user profile

### HTTP Request
* Endpoint: `/users/:uid`
* Verb: `GET`
* Body: `(application/json)`

### HTTP Response
* StatusCode: `200`
* Body: `(application/json)`

## User profile update
No endpoint available yet to update a user's detail

## User Favorite list
> Response Body

```json
{
  "status": "success",
  "recipes": [
      {
          "id": 1,
          "name": "Jollof Rice",
          "description": "some random description",
          ...
          "createdAt": "2017-11-17T10:51:14.594Z",
          "updatedAt": "2017-11-17T10:51:14.594Z",
          "owner": 8
      },
      ...
  ],
  "pagination": {
      "pages": [
          1,
          2
      ],
      "totalCount": 21,
      "pageSize": 12,
      "page": 1,
      "last": 2
  }
}
```
Gets a paginated list of all recipes favorited by a user

### HTTP Request
* Endpoint: `/users/:uid/favorites`
* Verb: `GET`
* Body: `(application/json)`

### HTTP Response
* StatusCode: `200`
* Body: `(application/json)`


## User Recipes List
> Response Body

```json
{
  "status": "success",
  "recipes": [
      {
          "id": 1,
          "name": "Jollof Rice",
          "description": "some random description",
          ...
          "createdAt": "2017-11-17T10:51:14.594Z",
          "updatedAt": "2017-11-17T10:51:14.594Z",
          "owner": 8
      },
      ...
  ],
  "pagination": {
      "pages": [
          1,
          2
      ],
      "totalCount": 21,
      "pageSize": 12,
      "page": 1,
      "last": 2
  }
}
```
Gets a paginated list of all recipes created by a user

### HTTP Request
* Endpoint: `/users/:uid/favorites`
* Verb: `GET`
* Body: `(application/json)`

### HTTP Response
* StatusCode: `200`
* Body: `(application/json)`

# Recipes
## Create recipe
> Request Body

```json
{
  "recipe": {
    "name": "very delicious dish",
    "description": "This is the recipe for a very delicious dish",
    "img_url": "https://imgurlfordish.com/verydelicousdish.jpg",
    "ingredients": [
      "ingredient 1",
      "ingredient 2"
    ],
    "instructions": [
      "This is the first step in cooking this delicious dish",
      "This is the next step"
    ]
  }
}
```

> Response Body

```json
{
  "recipe": {
    "upVoteCount": 0,
    "downVoteCount": 0,
    "favoriteCount": 0,
    "viewCount": 0,
    "id": 5,
    "name": "very delicious dish",
    "description": "This is the recipe for a very delicious dish",
    "img_url": "https://imgurlfordish.com/verydelicousdish.jpg",
    "ingredients": [
        "ingredient 1",
        "ingredient 2"
    ],
    "instructions": [
        "This is the first step in cooking this delicious dish",
        "This is the next step"
    ],
    "owner": 29,
    "updatedAt": "2018-01-12T13:21:52.287Z",
    "createdAt": "2018-01-12T13:21:52.287Z"
  },
  "message": "recipe created successfully",
  "status": "success"
}
```

Creates a new recipe

### HTTP Request
* Endpoint: `/recipes`
* Verb: `POST`
* **Requires Token: True**

### HTTP Response
* StatusCode: `201: Created`
* Body: `(application/json)`


## Get all recipes
> Response body

```json
{
  "recipes": [
    {
      "id": 27,
      "name": "very delicious dish",
      "description": "This is one of my 'go to' recipes ",
      ...
      "User": {
        "id": 11,
        "username": null,
        "fullname": "Email Mail"
      }
    },
    ...
    {
      "id": 28,
      "name": "very delicious dish",
      "description": "This is one of my 'go to' recipes ",
      ...
      "User": {
        "id": 11,
        "username": null,
        "fullname": "Email Mail"
      }
    }
  ],
  "pagination": {
    "pages": [
        1,
        2,
        ...
        10,
        11,
        12
    ],
    "totalCount": 139,
    "pageSize": 12,
    "page": 1,
    "last": 12
  },
  "status": "success"
}
```

### HTTP Request
* Endpoint: `/recipes`
* Verb: `GET`

### HTTP Response
* StatusCode: `200: Ok`
* Body: `(application/json)`

### Query Parameters

Parameter | Values | Description
--------- | ------- | -----------
sort | upvotes | Sort by criteria
order | descending | Direction of ordering

## Get a recipe
> Response Body

```json
{
  "recipe": {
    "id": 35,
    "name": "very delicious dish",
    "description": "This is the recipe for a very delicious dish",
    "img_url": "https://imgurlfordish.com/verydelicousdish.jpg",
    "ingredients": [
      "ingredient 1",
      "ingredient 2"
    ],
    "instructions": [
      "This is the first step in cooking this delicious dish",
      "This is the next step"
    ],
    "upVoteCount": 0,
    "downVoteCount": 0,
    "favoriteCount": 0,
    "viewCount": 1,
    "createdAt": "2017-11-11T09:07:14.446Z",
    "updatedAt": "2018-01-12T14:05:39.097Z",
    "owner": 11,
    "User": {
      "id": 11,
      "username": null,
      "fullname": "Email Mail"
    }
  },
  "status": "success"
}
```

### HTTP Request
* Endpoint: `/recipes/:id`
* Verb: `GET`
* `:id`: `recipe id`

### HTTP Response
* StatusCode: `200: Ok`
* Body: `(application/json)`

## Add review on recipe
> Request Body

```json
{
  "content": "Whoever told u that u can cook is a bloody liar"
}
```

> Response Body

```json
{
  "status": "success",
  "reviews": [
    {
      "id": 86,
      "content": "Whoever told u that u can cook is a bloody liar",
      "createdAt": "2018-01-13T00:41:59.673Z",
      "User": {
        "id": 29,
        "username": null,
        "fullname": "William Olojede"
      }
    },
    ...
  ],
  "pagination": {
    "pages": [
      1,
      2,
      3
    ],
    "totalCount": 30,
    "pageSize": 12,
    "page": 1,
    "last": 3
  },
  "message": "Your review has been recorded"
}
```

## Get all reviews for a recipe
> Response Body

```json
{
    "status": "success",
    "reviews": [
        {
            "id": 84,
            "content": "dude really???",
            "createdAt": "2018-01-09T03:33:40.835Z",
            "User": {
                "id": 27,
                "username": null,
                "fullname": "Ajale Aj"
            }
        },
        ...
        {
            "id": 83,
            "content": "shit sucks3",
            "createdAt": "2018-01-09T03:27:25.255Z",
            "User": {
                "id": 27,
                "username": null,
                "fullname": "Ajale Aj"
            }
        }
    ],
    "pagination": {
        "pages": [
            1,
            2,
            3
        ],
        "totalCount": 29,
        "pageSize": 12,
        "page": 1,
        "last": 3
    }
}
```

### HTTP Request
* Endpoint: `/recipes/:id/reviews`
* Verb: `GET`
* `:id`: `recipe id`

### HTTP Response
* StatusCode: `200: Ok`
* Body: `(application/json)`


## Modify a recipe
> Request Body

```json
{
	"update": {
	  "name": "some random very delicious dish"
	}
}
```

> Response body

```json
{
  "status": "success",
  "message": "Recipe updated successfully",
  "recipe": {
    "id": 169,
    "name": "some random very delicious dish",
    "description": "This is the recipe for a very delicious dish",
    ...
    "createdAt": "2018-01-13T00:09:15.646Z",
    "updatedAt": "2018-01-13T00:10:48.024Z",
    "owner": 29
  }
}
```



### HTTP Request
* Endpoint: `/recipes/:id`
* Verb: `PUT`
* `:id`: `recipe id`
* **Must be owner**

### HTTP Response
* StatusCode: `200: Ok`
* Body: `(application/json)`


## (up, down)Vote a recipe
> Response body &mdash; downVote

```json
{
  "recipe": {
    "id": 169,
    "name": "some random very delicious dish",
    "description": "This is the recipe for a very delicious dish",
    ...
    "upVoteCount": 0,
    "downVoteCount": 1,
    "favoriteCount": 0,
    "viewCount": 1,
    "createdAt": "2018-01-13T00:09:15.646Z",
    "updatedAt": "2018-01-13T00:13:58.362Z",
    "owner": 29
  },
  "status": "success",
  "message": "You disliked this recipe"
}
```

> Response body &mdash; upVote

```json
{
  "recipe": {
    "id": 169,
    "name": "some random very delicious dish",
    "description": "This is the recipe for a very delicious dish",
    "img_url": "https://imgurlfordish.com/verydelicousdish.jpg",
    ...
    "upVoteCount": 1,
    "downVoteCount": 0,
    "favoriteCount": 0,
    "viewCount": 1,
    "createdAt": "2018-01-13T00:09:15.646Z",
    "updatedAt": "2018-01-13T00:17:57.324Z",
    "owner": 29
  },
  "status": "success",
  "message": "You liked this recipe"
}
```

### HTTP Request
* Endpoint: `/recipes/:id/vote-{up, down}`
* Verb: `POST`
* `:id`: `recipe id`

### HTTP Response
* StatusCode: `200: Ok`
* Body: `(application/json)`

## Favorite a recipe

> Response body

```json
{
  "recipe": {
    "id": 2,
    "name": "Jollof Rice",
    ...
    "upVoteCount": 0,
    "downVoteCount": 0,
    "favoriteCount": 3,
    "viewCount": 5,
    "createdAt": "2017-10-23T08:08:47.566Z",
    "updatedAt": "2018-01-13T00:34:03.699Z",
    "owner": 2
  },
  "status": "success",
  "message": "Recipe added to your favorite list"
}
```

### HTTP Request
* Endpoint: `/recipes/:id/favorite`
* Verb: `POST`
* `:id`: `recipe id`

### HTTP Response
* StatusCode: `200: Ok`
* Body: `(application/json)`

## Delete Recipe
> Response body

```json
{
  "status": "success",
  "message": "Recipe deleted successfully"
}
```

### HTTP Request
* Endpoint: `/recipes/:id`
* Verb: `DELETE`
* `:id`: `recipe id`
* **Must be owner**

### HTTP Response
* StatusCode: `200: Ok`
* Body: `(application/json)`
