description: A detailed look at the various REST actions supported by the Flows resource of the Losant API. Learn more.

# Flows Actions

https://api.losant.com/applications/**`APPLICATION_ID`**/flows

Below are the various requests that can be performed against the
Flows resource, as well as the expected
parameters and the potential responses.

## Get

Returns the flows for an application

### Method And Url <a name="get-method-url"></a>

GET https://api.losant.com/applications/**`APPLICATION_ID`**/flows

### Authentication <a name="get-authentication"></a>

A valid api access token is required to access this endpoint. The token must
include at least one of the following scopes:
all.Application, all.Application.read, all.Organization, all.Organization.read, all.User, all.User.read, flows.*, or flows.get.

### Request Path Components <a name="get-path-components"></a>

| Path Component | Description | Example |
| -------------- | ----------- | ------- |
| APPLICATION_ID | ID associated with the application | 575ec8687ae143cd83dc4a97 |

### Request Query Parameters <a name="get-query-params"></a>

| Name | Required | Description | Default | Example |
| ---- | -------- | ----------- | ------- | ------- |
| sortField | N | Field to sort the results by. Accepted values are: name, id, creationDate | name | name |
| sortDirection | N | Direction to sort the results by. Accepted values are: asc, desc | asc | asc |
| page | N | Which page of results to return | 0 | 0 |
| perPage | N | How many items to return per page | 1000 | 10 |
| filterField | N | Field to filter the results by. Blank or not provided means no filtering. Accepted values are: name |  | name |
| filter | N | Filter to apply against the filtered field. Supports globbing. Blank or not provided means no filtering. |  | my*flow |
| triggerFilter | N | Array of triggers to filter by - always filters against default flow version. See [Workflow Trigger Filter](schemas.md#workflow-trigger-filter) for more details. |  | [Workflow Trigger Filter Example](schemas.md#workflow-trigger-filter-example) |

### Request Headers <a name="get-headers"></a>

| Name | Required | Description | Default |
| ---- | -------- | ----------- | ------- |
| Authorization | Y | The token for authenticating the request, prepended with Bearer | |

### Curl Example <a name="get-curl-example"></a>

```bash
curl -H 'Content-Type: application/json' \
    -H 'Accept: application/json' \
    -H 'Authorization: Bearer YOUR_API_ACCESS_TOKEN' \
    -X GET \
    https://api.losant.com/applications/APPLICATION_ID/flows
```

### Successful Responses <a name="get-successful-responses"></a>

| Code | Type | Description |
| ---- | ---- | ----------- |
| 200 | [Workflows](schemas.md#workflows) | Collection of flows |

### Error Responses <a name="get-error-responses"></a>

| Code | Type | Description |
| ---- | ---- | ----------- |
| 400 | [Error](schemas.md#error) | Error if malformed request |
| 404 | [Error](schemas.md#error) | Error if application was not found |

## Post

Create a new flow for an application

### Method And Url <a name="post-method-url"></a>

POST https://api.losant.com/applications/**`APPLICATION_ID`**/flows

### Authentication <a name="post-authentication"></a>

A valid api access token is required to access this endpoint. The token must
include at least one of the following scopes:
all.Application, all.Organization, all.User, flows.*, or flows.post.

### Request Path Components <a name="post-path-components"></a>

| Path Component | Description | Example |
| -------------- | ----------- | ------- |
| APPLICATION_ID | ID associated with the application | 575ec8687ae143cd83dc4a97 |

### Request Headers <a name="post-headers"></a>

| Name | Required | Description | Default |
| ---- | -------- | ----------- | ------- |
| Authorization | Y | The token for authenticating the request, prepended with Bearer | |

### Request Body <a name="post-body"></a>

The body of the request should be serialized JSON that validates against
the [Workflow Post](schemas.md#workflow-post) schema. For example, the following would be a
valid body for this request:

```json
{
  "name": "My New Workflow",
  "description": "Description of my new workflow"
}
```

### Curl Example <a name="post-curl-example"></a>

```bash
curl -H 'Content-Type: application/json' \
    -H 'Accept: application/json' \
    -H 'Authorization: Bearer YOUR_API_ACCESS_TOKEN' \
    -X POST \
    -d '{"name":"My New Workflow","description":"Description of my new workflow"}' \
    https://api.losant.com/applications/APPLICATION_ID/flows
```

### Successful Responses <a name="post-successful-responses"></a>

| Code | Type | Description |
| ---- | ---- | ----------- |
| 201 | [Workflow](schemas.md#workflow) | Successfully created flow |

### Error Responses <a name="post-error-responses"></a>

| Code | Type | Description |
| ---- | ---- | ----------- |
| 400 | [Error](schemas.md#error) | Error if malformed request |
| 404 | [Error](schemas.md#error) | Error if application was not found |
