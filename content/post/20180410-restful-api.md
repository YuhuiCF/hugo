---
title: 'RESTful API'
date: 2018-04-10T07:56:00+02:00
lastmod: 2018-04-16T15:40:00+02:00
draft: false
tags: ['rest']
categories: ['web']
---


## Guiding Principles of REST

REST is caracterized by: resource-based, noun, URI, representations.

* Uniform Interface
* Stateless
* Cacheable
* Client-Server
* Layered System
* Code on Demand (optional)

<!--more-->

### Uniform Interface

Use HTTP verbs, URIs, and correct HTTP response (status, and body), hypermedia as the engine of application state.

### Stateless

Each request contains enough context to process the message. (Session state is therefore kept entirely on the client.)

### Cacheable

Server responses (representations) are cacheable (or non-cacheable?). If a response is cacheable, then a client cache is given the right to reuse that response data for later, equivalent requests.

### Client-Server

Separate the user interface from the data storage, improve the portability of the user interface, and improve scalability.

### Layered System

The layered system style allows an architecture to be composed of hierarchical layers by constraining component behavior such that each component cannot “see” beyond the immediate layer with which they are interacting.

### Code on Demand (optional)

Transfer logic to client. Client executes logic.

## Some best practices

### Use plural nouns as resource names

```
GET /owners, list all the owners
POST /owners, create a new owner
GET /owners/123, get owner with id 123
PUT /owners/123, update owner with id 123
DELETE /owners/123, delete owner with id 123
GET /owners/123/pets, list all the pets of owner (id 123)
```

### Use correct HTTP status and headers

### Use HATEOAS (Hypermedia as the Engine of Application State)

might be considered

```javascript
{
  "id": "123",
  "surname": "Trump",
  "givenname": "Max",
  "age": 25,
  "pet": [
    {
      "id": "23",
      "name": "Chocolate",
      "links": [
        {
          "rel": "self",
          "href": "/owners/123/pets/23"
        }
      ]
    }
  ]
}
```

### Versioning

Current proposition, support at most 2 versions.

If we neeed to have a new version of `GET /projects`, we would have `GET /projects2` for developing and testing the new endpoint.

The client would have some time test the new endpoint, and switch to use it, and finally confirm that it is working as expected.

Once the behavior of the old endpoint is no more in use, we would implement the `GET /projects` with exactly what is implemented in `GET /projects2`.

The client would get some time and remove the `2` from their API path.

Once we got final confirmation, the temporary `GET /projects2` could be removed.

### Documentation

## Resources

* [What is REST, by REST API Tutorial](https://restfulapi.net/)
* [What exactly is RESTful programming?, on stackoverflow](https://stackoverflow.com/questions/671118/what-exactly-is-restful-programming#answer-671132)
* [RESTful API Designing guidelines — The best practices, on hackernoon](https://hackernoon.com/restful-api-designing-guidelines-the-best-practices-60e1d954e7c9)
* [10 Best Practices for Better RESTful API, on mwaysolutions](https://blog.mwaysolutions.com/2014/06/05/10-best-practices-for-better-restful-api/)
* [
Best Practices for Designing a Pragmatic RESTful API, on vinaysahni](https://www.vinaysahni.com/best-practices-for-a-pragmatic-restful-api)
