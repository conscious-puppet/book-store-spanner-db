# book-store

# How to Test
- Run [pgAdapter](https://github.com/GoogleCloudPlatform/pgadapter)
- Add the following envs
    ```bash
    export dbHost="localhost" # host of pgAdapter
    export dbPort="5433" # port on which pgAdapter is running
    export dbName="psql-interface" # spanner db name
    export dbUser=""
    export dbPassword=""
    ```
- Run the application, which we can test the DML queries.

## Routes
```
@route   GET /version
@desc    App version

@route   GET /healthcheck
@desc    Healthcheck API

@route   GET /books
@desc    Get all books
@resp
[
    {
        "id": "52302b94-5241-4cac-ad1a-6d42c73a93ee",
        "name": "The Heart Is a Lonely Hunter",
        "author": "Carson McCullers"
    },
    {
        "id": "01136e18-a56e-420a-8e2c-db3319745255",
        "name": "The Lord of the Rings",
        "author": "J. R. R. Tolkien"
    }
]

@route   GET /books/:id
@desc    Get a book by id
@resp
{
    "id": "01136e18-a56e-420a-8e2c-db3319745255",
    "name": "The Lord of the Rings",
    "author": "J. R. R. Tolkien"
}

@route   POST /books
@desc    Create a new book
@req
{
    "name": "Heart Is a Lonely Hunter",
    "author": "Carson McCullers"
}
@resp
{
    "id": "52302b94-5241-4cac-ad1a-6d42c73a93ee",
    "name": "Heart Is a Lonely Hunter",
    "author": "Carson McCullers"
}

@route   POST /books
@desc    Update a book by id
@req
{
    "id": "52302b94-5241-4cac-ad1a-6d42c73a93ee",
    "name": "The Heart Is a Lonely Hunter",
    "author": "Carson McCullers"
}
@resp
{
    "id": "52302b94-5241-4cac-ad1a-6d42c73a93ee",
    "name": "The Heart Is a Lonely Hunter",
    "author": "Carson McCullers"
}

@route   DELETE /books/:id
@desc    Delete a book by id
@resp    NoContent
```

# Docker Image
```
nix build .#dockerImage
```
