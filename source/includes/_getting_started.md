# Getting Started
## Introduction

**Juvonno API** is a collection of RESTful endpoints, which communicate directly with our back-end Business Objects, thus allowing users to **Create, Read, Update & Delete** (CRUD) the corresponding resources. 

Juvonno API has strict validations and will throw detailed messages upon encountering any errors, thus enabling developers with better integration to our Juvonno App. 

<aside class="warning">
This guide is currently in development.
</aside>

## API Reference

This document will serve as a guideline & an introduction to our Juvonno API & our business logic.

For detailed API Document of all of our available Endpoints, please use this [reference here in Swaggerhub](https://app.swaggerhub.com/apis-docs/globaloffice/juvonno/2.0.1). 

## What is a REST API?

API stands for "Application Programming Interface". It's a set of rules that enables various programs to talk to each other, regardless of the programming languages they were written in.

The programs talk to each other through a set of predefined URLs which can be accessed via HTTP Protocol.

These URLs represent various **resources**. A Resource represents a **Juvonno Business Object**, such as an **Appointment**, a **Customer**, or a **Staff Member**, etc. Resources will be returned in JSON format.

We utilize various HTTP Methods to perform different operations on a resource:

Method | Function
--------- | ------- |
<span class="http-get">GET</span> | to retrieve a resource (or sometimes a list of resources)
<span class="http-post">POST</span> | to create a new resource 
<span class="http-put">PUT</span> | to update an existing resource
<span class="http-delete">DELETE</span> | to delete an existing resource    

## Authentication

Juvonno uses API keys to allow access to the API. You can register a new API key under your own profile in your Juvonno App.

> Always append your api key using the query parameter "api_key" to your HTTP Request:

```shell
curl -X POST "https://tenant-id.juvonno.com/
api/{RESOURCES}?api_key={YOUR_API_KEY}"
```

```http
POST "https://tenant-id.juvonno.com/api/{RESOURCES}?api_key={YOUR_API_KEY}"
```

API key must be included in all API requests to the server as a *query parameter* called **"api_key"** that looks like the following:

`https://tenant-id.juvonno.com/api/{RESOURCES}?api_key=fhOkwr12kfslsdqwe8`

<aside class="notice">
You must replace <code>fhOkwr12kfslsdqwe8</code> with your personal API key.
</aside>
