description: A detailed look at the various REST actions supported by the Webhooks resource of the Losant API. Learn more.

# Webhooks Actions

https://api.losant.com/applications/**`APPLICATION_ID`**/webhooks

Below are the various requests that can be performed against the
Webhooks resource, as well as the expected
parameters and the potential responses.

## Get

Returns the webhooks for an application

#### Method And Url

GET https://api.losant.com/applications/**`APPLICATION_ID`**/webhooks

#### Authentication
A valid api access token is required to access this endpoint. The token must
include at least one of the following scopes:
all.Application, all.Application.read, all.Organization, all.Organization.read, all.User, all.User.read, webhooks.*, or webhooks.get.

#### Request Path Components

| Path Component | Description | Example |
| -------------- | ----------- | ------- |
| APPLICATION_ID | ID associated with the application | 575ec8687ae143cd83dc4a97 |

#### Request Query Parameters

| Name | Required | Description | Default | Example |
| ---- | -------- | ----------- | ------- | ------- |
| sortField | N | Field to sort the results by. Accepted values are: name, id, creationDate | name | name |
| sortDirection | N | Direction to sort the results by. Accepted values are: asc, desc | asc | asc |
| page | N | Which page of results to return | 0 | 0 |
| perPage | N | How many items to return per page | 1000 | 10 |
| filterField | N | Field to filter the results by. Blank or not provided means no filtering. Accepted values are: name |  | name |
| filter | N | Filter to apply against the filtered field. Supports globbing. Blank or not provided means no filtering. |  | my*webhook |

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
    https://api.losant.com/applications/APPLICATION_ID/webhooks
```
<br/>

#### Successful Responses

| Code | Type | Description |
| ---- | ---- | ----------- |
| 200 | [Webhooks](schemas.md#webhooks) | Collection of webhooks |

#### Error Responses

| Code | Type | Description |
| ---- | ---- | ----------- |
| 400 | [Error](schemas.md#error) | Error if malformed request |
| 404 | [Error](schemas.md#error) | Error if application was not found |

<br/>

## Post

Create a new webhook for an application

#### Method And Url

POST https://api.losant.com/applications/**`APPLICATION_ID`**/webhooks

#### Authentication
A valid api access token is required to access this endpoint. The token must
include at least one of the following scopes:
all.Application, all.Organization, all.User, webhooks.*, or webhooks.post.

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
the [Webhook Post](schemas.md#webhook-post) schema. For example, the following would be a
valid body for this request:

```json
{
  "name": "My New Webhook"
}
```
<small><br/></small>

#### Curl Example

```bash
curl -H 'Content-Type: application/json' \
    -H 'Accept: application/json' \
    -H 'Authorization: Bearer YOUR_API_ACCESS_TOKEN' \
    -X POST \
    -d '{"name":"My New Webhook"}' \
    https://api.losant.com/applications/APPLICATION_ID/webhooks
```
<br/>

#### Successful Responses

| Code | Type | Description |
| ---- | ---- | ----------- |
| 201 | [Webhook](schemas.md#webhook) | Successfully created webhook |

#### Error Responses

| Code | Type | Description |
| ---- | ---- | ----------- |
| 400 | [Error](schemas.md#error) | Error if malformed request |
| 404 | [Error](schemas.md#error) | Error if application was not found |

<br/>

