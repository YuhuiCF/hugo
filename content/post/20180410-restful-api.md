---
title: 'RESTful API'
date: 2018-04-10T07:56:00+02:00
lastmod: 2018-04-10T08:10:00+02:00
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

## Resources

* [What is REST, by REST API Tutorial](https://restfulapi.net/)
* [What exactly is RESTful programming?, by stackoverflow](https://stackoverflow.com/questions/671118/what-exactly-is-restful-programming#answer-671132)
