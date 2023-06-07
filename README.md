# open-api-schema-design-sample


# Dillinger
Designing an API schema YAML file based on the Open API 3.0 specification involves defining the routes, parameters, responses, and other details about your API. Let's go through a basic example to demonstrate how this is done. In this example, we will create a simple API for a book store which has endpoints for adding a book, fetching all books, and getting a single book by its ID.

1. Basic Information:
Start by defining some basic information about your API. You will need to provide details about your API like its title, version, and more.

```
openapi: 3.0.0
info:
  title: Book Store API
  version: 1.0.0
  description: This is a simple API for managing books in a store.

```
2. Servers:
Next, define the servers that your API will run on. In most cases, this will be the base URL for your API. For example, if your API endpoints look like http://mybookstore.com/api/books, your server would be http://mybookstore.com/api.

```
servers:
  - url: http://mybookstore.com/api

```

3. Paths:
Paths are where you define your API's endpoints and the operations (like get, post, put, delete, etc.) that can be performed on them. Each operation can have parameters, responses, and other details. For now, let's create endpoints for adding a book (POST operation) and fetching all books (GET operation).

```
paths:
  /books:
    get:
      summary: Returns a list of books
      responses:
        '200':
          description: A list of books
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Book'
    post:
      summary: Adds a new book
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Book'
      responses:
        '201':
          description: Book created successfully

```

3.1. Components
Components are a way to define schemas, responses, parameters, and other elements that can be reused throughout your API. For this example, let's create a schema for our book model.
```
components:
  schemas:
    Book:
      type: object
      required:
        - id
        - title
        - author
        - published_date
      properties:
        id:
          type: integer
          format: int64
        title:
          type: string
        author:
          type: string
        published_date:
          type: string
          format: date

```

4. Path for single book
We can add another path to get a single book by its ID. The get operation on this path will have a parameter for the book's ID.

```
paths:
  /books/{id}:
    get:
      summary: Returns a single book by its ID
      parameters:
        - name: id
          in: path
          required: true
          schema:
            type: integer
            format: int64
      responses:
        '200':
          description: A single book
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Book'

```

