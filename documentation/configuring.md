
### Configuring jsonapi-server

```javascript
jsonApi.setConfig({
  // (optional) HTTP / HTTPS
  protocol: "http",
  // (optional) The hostname the API will be sat behind, from the customer's perspective
  hostname: "localhost",
  // (required) The port the customer will be using (OPTIONAL)
  port: 16006,
  // (optional) Define a url prefix for the apiConfig
  // eg http://-----/rest/
  base: "rest",
  // (optional) meta block to appear in the root of every response
  meta: {
    copyright: "Blah"
  }
});
```

#### Error Handling

```javascript
jsonApi.onUncaughtException(function(request, error) {
  // log the error somewhere
});
```

#### Basic Authentication

```javascript
// This function will be invoked on every request, as soon as the HTTP
// request has been parsed into a "request" object.
jsonApi.authenticate(function(request, callback) {
  // If you callback with an error, the client will receive a HTTP 401 Unauthorised
  if (request.headers.blockme) return callback("Fail");

  // If you callback with no error, the request will continue onwards
  return callback();
});
```

#### Starting jsonapi-server

Note: You should only start the server once you've called `setConfig` as per the example above. Resources can be defined before OR after the server has been started.

```javascript
jsonApi.start();
```

#### Stopping jsonapi-server

To gracefully shutdown the service, you can call `.close()`. This will inform all handlers that the server is shutting down, they'll have an opportunity to close any open files or connections, then the HTTP server will stop listening.

```javascript
jsonApi.close();
```
