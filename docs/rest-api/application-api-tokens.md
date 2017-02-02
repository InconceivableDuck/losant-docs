# Application Api Tokens Actions

https://api.losant.com/applications/**`APPLICATION_ID`**/tokens

Below are the various requests that can be performed against the
Application Api Tokens resource, as well as the expected
parameters and the potential responses.

## Get

Returns the API tokens for an application

#### Method And Url

GET https://api.losant.com/applications/**`APPLICATION_ID`**/tokens

#### Authentication
A valid api access token is required to access this endpoint. The token must
include at least one of the following scopes:
all.Application, all.Application.read, all.Organization, all.Organization.read, all.User, all.User.read, applicationApiTokens.*, or applicationApiTokens.get.

#### Request Path Components

| Path Component | Description | Example |
| -------------- | ----------- | ------- |
| APPLICATION_ID | ID associated with the application | 575ec8687ae143cd83dc4a97 |

#### Request Headers

| Name | Required | Description | Default |
| ---- | -------- | ----------- | ------- |
| Authorization | Y | The token for authenticating the request, prepended with Bearer | |

#### Curl Example

```bash
curl -H 'Content-Type: application/json' \
    -H 'Accept: application/json' \
    -H 'Authorization: Bearer YOUR_API_ACCESS_TOKEN' \
    -X GET \
    https://api.losant.com/applications/APPLICATION_ID/tokens
```
<br/>

#### Successful Responses

| Code | Type | Description |
| ---- | ---- | ----------- |
| 200 | [API Token](schemas.md#api-token) | Collection of API tokens |

#### Error Responses

| Code | Type | Description |
| ---- | ---- | ----------- |
| 400 | [Error](schemas.md#error) | Error if malformed request |

<br/>

## Post

Create a new API token for an application

#### Method And Url

POST https://api.losant.com/applications/**`APPLICATION_ID`**/tokens

#### Authentication
A valid api access token is required to access this endpoint. The token must
include at least one of the following scopes:
all.Application, all.Organization, all.User, applicationApiTokens.*, or applicationApiTokens.post.

#### Request Path Components

| Path Component | Description | Example |
| -------------- | ----------- | ------- |
| APPLICATION_ID | ID associated with the application | 575ec8687ae143cd83dc4a97 |

#### Request Headers

| Name | Required | Description | Default |
| ---- | -------- | ----------- | ------- |
| Authorization | Y | The token for authenticating the request, prepended with Bearer | |

#### Request Body

The body of the request should be serialized JSON that validates against
the [Application API Token Post](schemas.md#application-api-token-post) schema.  For example, the following would be a
valid body for this request:

```json
{
  "name": "My New API Token",
  "expirationDate": "2017-06-13T04:00:00.000Z",
  "scope": [
    "all.Application"
  ],
  "status": "active"
}
```
<small><br/></small>

#### Curl Example

```bash
curl -H 'Content-Type: application/json' \
    -H 'Accept: application/json' \
    -H 'Authorization: Bearer YOUR_API_ACCESS_TOKEN' \
    -X POST \
    -d '{"name":"My New API Token","expirationDate":"2017-06-13T04:00:00.000Z","scope":["all.Application"],"status":"active"}' \
    https://api.losant.com/applications/APPLICATION_ID/tokens
```
<br/>

#### Successful Responses

| Code | Type | Description |
| ---- | ---- | ----------- |
| 201 | [API Token](schemas.md#api-token) | The successfully created API token |

#### Error Responses

| Code | Type | Description |
| ---- | ---- | ----------- |
| 400 | [Error](schemas.md#error) | Error if malformed request |

<br/>
