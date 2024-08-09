---
sidebar_position: 1
---

## API Documentation Intro

This is a sample Petstore API endpoint built on **Docusaurus in less than 5 minutes**.

---
#### Description of the API
```
id: petstore-api
title: Petstore API Documentation
description: API documentation for the Petstore sample API.
sidebar_label: Petstore API
```

## Writing the API Body
#### Server Information

```yaml
servers:
  - url: https://petstore.example.com/v1
    description: Production server
```

## API Endpoints
 Next, document the API endpoints. Include the paths, HTTP methods, parameters, and responses.


##### List All Pets
```yaml
paths:
  /pets:
    get:
      summary: List all pets
      operationId: listPets
      tags:
        - pets
      parameters:
        - name: limit
          in: query
          description: How many items to return at one time (max 100)
          required: false
          schema:
            type: integer
            format: int32
      responses:
        '200':
          description: A paged array of pets
          content:
            application/json:
              schema:
                type: array
                items:
                  $ref: '#/components/schemas/Pet'
        'default':
          description: unexpected error
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Error'
```


##### **Get Pet by ID**

```yaml
  /pets/{petId}:
    get:
      summary: Info for a specific pet
      operationId: showPetById
      tags:
        - pets
      parameters:
        - name: petId
          in: path
          required: true
          description: The id of the pet to retrieve
          schema:
            type: integer
            format: int64
      responses:
        '200':
          description: Expected response to a valid request
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Pet'
        'default':
          description: unexpected error
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Error'
```

## Add Component Schemas

 Schemas are reusable codes. They help in defining the structure of the data returned by the API. 
#### We are going to include the reusable schemas for `Pet` and `Error`.

### **Pet Schema**

```yaml
components:
  schemas:
    Pet:
      type: object
      required:
        - id
        - name
      properties:
        id:
          type: integer
          format: int64
        name:
          type: string
        tag:
          type: string
```

### **Error Schema**

```yaml
    Error:
      type: object
      required:
        - code
        - message
      properties:
        code:
          type: integer
          format: int32
        message:
          type: string
```