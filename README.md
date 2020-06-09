# Postman to OAS

Converts [Postman 2.1](https://schema.getpostman.com/json/collection/latest/docs/index.html) to [OpenAPI 3.0](https://github.com/OAI/OpenAPI-Specification/blob/master/versions/3.0.3.md)

## Introduction

I looked all over the internet for this tool, because I didn't want to have to build it. It didn't exist, or was broken for a reason. Postman schema doesn't convert well to OpenAPI. There's a lot of data missing.

To get around that, I've created some configuration options and implemented defaults where necessary.

This project intends to get you a valid but basic `openapi.yaml` from your Postman collection. That way you can generate basic interoperability.

## Installation

```sh
npm install [-g] mikeralphson/postman-to-oas
```

## Example

```js
const p2o = require('postman-to-oas')
const yaml = require('yaml')
const fs = require('fs')
const postmanJson = require('./postman_collection.json')
const openapiJson = p2o(postmanJson, {
  info: {
    version: 'v1'
  }
})

//let output = JSON.stringify(openapiJson, null, 2)
let output = yaml.stringify(openapiJson)

// Save to file
fs.writeFileSync('Swagger.yaml',output,'utf8');
```

## Defaults

```js
const defaults = {
  source_spec: "postman2.1",
  target_spec: "openapi3.0",
  require_all: ["headers", "body", "query", "path"],
  omit: {
    headers: ["Content-Type", "X-Requested-With"]
  },
  info: {},
  host: null,
  basepath: null,
  schemes: null,
  responses: {
    200: {
      description: "OK"
    }
  }
}
```

## License

MIT
