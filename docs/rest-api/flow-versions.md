# Flow Versions Actions

https://api.losant.com/applications/**`APPLICATION_ID`**/flows/**`FLOW_ID`**/versions

Below are the various requests that can be performed against the
Flow Versions resource, as well as the expected
parameters and the potential responses.

## Get

Returns the flow versions for a flow

#### Method And Url

GET https://api.losant.com/applications/**`APPLICATION_ID`**/flows/**`FLOW_ID`**/versions

#### Authentication
A valid api access token is required to access this endpoint. The token must
include at least one of the following scopes:
all.Application, all.Application.read, all.Organization, all.Organization.read, all.User, all.User.read, flowVersions.*, or flowVersions.get.

#### Request Path Components

| Path Component | Description | Example |
| -------------- | ----------- | ------- |
| APPLICATION_ID | ID associated with the application | 575ec8687ae143cd83dc4a97 |
| FLOW_ID | ID associated with the flow | 575ed18f7ae143cd83dc4aa6 |

#### Request Query Parameters

| Name | Required | Description | Default | Example |
| ---- | -------- | ----------- | ------- | ------- |
| sortField | N | Field to sort the results by. Accepted values are: version, id, creationDate | version | version |
| sortDirection | N | Direction to sort the results by. Accepted values are: asc, desc | asc | asc |
| page | N | Which page of results to return | 0 | 0 |
| perPage | N | How many items to return per page | 1000 | 10 |
| filterField | N | Field to filter the results by. Blank or not provided means no filtering. Accepted values are: version |  | version |
| filter | N | Filter to apply against the filtered field. Supports globbing. Blank or not provided means no filtering. |  | my*version |

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
    https://api.losant.com/applications/APPLICATION_ID/flows/FLOW_ID/versions
```
<br/>

#### Successful Responses

| Code | Type | Description |
| ---- | ---- | ----------- |
| 200 | [Workflow Versions](schemas.md#workflow-versions) | Collection of flow versions |

#### Error Responses

| Code | Type | Description |
| ---- | ---- | ----------- |
| 400 | [Error](schemas.md#error) | Error if malformed request |
| 404 | [Error](schemas.md#error) | Error if flow was not found |

<br/>

## Post

Create or replace a flow version for a flow

#### Method And Url

POST https://api.losant.com/applications/**`APPLICATION_ID`**/flows/**`FLOW_ID`**/versions

#### Authentication
A valid api access token is required to access this endpoint. The token must
include at least one of the following scopes:
all.Application, all.Organization, all.User, flowVersions.*, or flowVersions.post.

#### Request Path Components

| Path Component | Description | Example |
| -------------- | ----------- | ------- |
| APPLICATION_ID | ID associated with the application | 575ec8687ae143cd83dc4a97 |
| FLOW_ID | ID associated with the flow | 575ed18f7ae143cd83dc4aa6 |

#### Request Query Parameters

| Name | Required | Description | Default | Example |
| ---- | -------- | ----------- | ------- | ------- |
| allowReplacement | N | Allow replacement of an existing flow version with same version name | false | true |

#### Request Headers

| Name | Required | Description | Default |
| ---- | -------- | ----------- | ------- |
| Authorization | Y | The token for authenticating the request, prepended with Bearer | |

#### Request Body

The body of the request should be serialized JSON that validates against
the [Workflow Version Post](schemas.md#workflow-version-post) schema. For example, the following would be a
valid body for this request:

```json
{
  "version": "v1.2.3",
  "notes": "Notes about my new workflow version",
  "enabled": false
}
```
<small><br/></small>

#### Curl Example

```bash
curl -H 'Content-Type: application/json' \
    -H 'Accept: application/json' \
    -H 'Authorization: Bearer YOUR_API_ACCESS_TOKEN' \
    -X POST \
    -d '{"version":"v1.2.3","notes":"Notes about my new workflow version","enabled":false}' \
    https://api.losant.com/applications/APPLICATION_ID/flows/FLOW_ID/versions
```
<br/>

#### Successful Responses

| Code | Type | Description |
| ---- | ---- | ----------- |
| 201 | [Workflow Version](schemas.md#workflow-version) | Successfully created flow version |

#### Error Responses

| Code | Type | Description |
| ---- | ---- | ----------- |
| 400 | [Error](schemas.md#error) | Error if malformed request |
| 404 | [Error](schemas.md#error) | Error if flow was not found |

<br/>
