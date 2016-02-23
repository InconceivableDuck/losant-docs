# Structure REST API

Structure is powered by a full REST API that provides access to nearly every feature. The Structure web portal is built on top of the open-source <a href="https://github.com/GetStructure/structure-api-js" target="_blank">structure-api-js</a> Node.js client. This is the recommended client to easily communicate with the Structure API.

## Obtaining API Token

In order to make API requests, you must first obtain an API token. You can generate either an account-level token or a device-level token, depending on your specific application needs.

### Account-Level Token

An account level token provide access to all resources owned by the user account.

`POST: https://api.getstructure.io/auth/user`

Payload:

```json
{
  "username" : "your-username",
  "password" : "your-password"
}
```

Response:

```json
{
  ...
  "token" : "your-api-token"
}
```

The response will include several fields, including your API token.

### Device-Level Token

A device level token will only allow access to resources for a specific device. In order to generate a device-level API token, you must first generate an application [access key](/applications/access-keys).

`POST: https://api.getstructure.io/auth/device`

Payload:

```json
{
  "deviceId" : "your-device-id",
  "key" : "your-access-key",
  "secret" : "your-access-secret"
}
```

Response:

```json
{
  ...
  "token" : "your-api-token"
}
```

The response will include several fields, including your API token.

## API Client

Once a token is obtained you can construct a client, pass it the token, and begin using the API.

```JavaScript
var api = require('structure-api-js');

var client = api.createClient({
  accessToken: 'my-token'
});
```

## Documentation

Full documentation is not yet available. Please refer to the <a href="https://github.com/GetStructure/structure-api-js" target="_blank">Node.js client repository</a> for usage details.