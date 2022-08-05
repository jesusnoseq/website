---
id: intro
title: Variant Handlers
description: Mocks Server Variant Handlers
keywords:
  - mocks server
  - customization
  - variants
  - types
  - variant types
  - handler
  - format
---

## Preface

As described in the [variants chapter](../usage/variants.md):

> _route variants can be defined in many ways, from [plain objects](../usage/variants/json.md) to [Express middlewares](../usage/variants/middleware.md), and, depending on the variant type, they can act in different ways also, from sending a response to [proxy the request to another host](../usage/variants/proxy.md)_.

This is possible because the route variant itself does not contain the logic at charge of sending the response. __Each route variant can be of a different type, and its type defines which Variant Handler is at charge of receiving the variant options and act in consequence.__

This allows to add new Variant Handlers to provide more features to Mocks Server easily. For example, next variant handlers are included by default in the main distribution of Mocks Server:

* __[`json`](../usage/variants/json.md)__: Defines the JSON body and the status code to be sent when the route is requested. 
* __[`middleware`](../usage/variants/middleware.md)__: Defines an [Express middleware](https://expressjs.com/en/guide/using-middleware.html) to be executed when the request is received. It is completely on your hand to send a response, or to pass the request to the next middleware, etc.
* __[`proxy`](../usage/variants/proxy.md)__: Defines a host to proxy the request when it is received. You can modify the request and/or the response also.

But, adding your own Variant Handlers, you would be able to create new types of variants allowing to:

* Serve an static folder
* Convert an OpenAPI file into Mocks Server routes.
* Send an API response with a predefined body format.
* etc...

## Example

In the next example you can see how route variants define the handler to be used.

```js
module.exports = [
  {
    id: "get-users",
    url: "/api/users",
    method: "GET",
    variants: [
      {
        id: "success",
        delay: 1000,
        type: "json", // variant type. Corresponds to the Variant Handler id
        options: { // options for the Variant Handler
          status: 200,
          body: [
            {
              id: 1,
              name: "John Doe"
            },
            {
              id: 2,
              name: "Jane Doe"
            }
          ]
        },
      }
    ]
  }
];
```

:::tip
Read the [variants chapter](../usage/variants.md) for further info about defining route variants.
:::