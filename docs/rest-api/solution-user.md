description: A detailed look at the various REST actions supported by the Solution User resource of the Losant API. Learn more.

# Solution User Actions

https://api.losant.com/orgs/**`ORG_ID`**/solutions/**`SOLUTION_ID`**/users/**`SOLUTION_USER_ID`**

Below are the various requests that can be performed against the
Solution User resource, as well as the expected
parameters and the potential responses.

## Delete

Deletes a solution user

### Method And Url <a name="delete-method-url"></a>

DELETE https://api.losant.com/orgs/**`ORG_ID`**/solutions/**`SOLUTION_ID`**/users/**`SOLUTION_USER_ID`**

### Authentication <a name="delete-authentication"></a>

A valid api access token is required to access this endpoint. The token must
include at least one of the following scopes:
all.Organization, all.User, solutionUser.*, or solutionUser.delete.

### Request Path Components <a name="delete-path-components"></a>

| Path Component | Description | Example |
| -------------- | ----------- | ------- |
| ORG_ID | ID associated with the organization | 575ed6e87ae143cd83dc4aa8 |
| SOLUTION_ID | ID associated with the solution | 57955788124b37010084c053 |
| SOLUTION_USER_ID | ID associated with the solution user | 566116085df4b701000258e3 |

### Request Headers <a name="delete-headers"></a>

| Name | Required | Description | Default |
| ---- | -------- | ----------- | ------- |
| Authorization | Y | The token for authenticating the request, prepended with Bearer | |

### Curl Example <a name="delete-curl-example"></a>

```bash
curl -H 'Content-Type: application/json' \
    -H 'Accept: application/json' \
    -H 'Authorization: Bearer YOUR_API_ACCESS_TOKEN' \
    -X DELETE \
    https://api.losant.com/orgs/ORG_ID/solutions/SOLUTION_ID/users/SOLUTION_USER_ID
```

### Successful Responses <a name="delete-successful-responses"></a>

| Code | Type | Description |
| ---- | ---- | ----------- |
| 200 | [Success](schemas.md#success) | If solution user was successfully deleted |

### Error Responses <a name="delete-error-responses"></a>

| Code | Type | Description |
| ---- | ---- | ----------- |
| 400 | [Error](schemas.md#error) | Error if malformed request |
| 404 | [Error](schemas.md#error) | Error if solution user was not found |

## Get

Retrieves information on a solution user

### Method And Url <a name="get-method-url"></a>

GET https://api.losant.com/orgs/**`ORG_ID`**/solutions/**`SOLUTION_ID`**/users/**`SOLUTION_USER_ID`**

### Authentication <a name="get-authentication"></a>

A valid api access token is required to access this endpoint. The token must
include at least one of the following scopes:
all.Organization, all.Organization.read, all.User, all.User.read, solutionUser.*, or solutionUser.get.

### Request Path Components <a name="get-path-components"></a>

| Path Component | Description | Example |
| -------------- | ----------- | ------- |
| ORG_ID | ID associated with the organization | 575ed6e87ae143cd83dc4aa8 |
| SOLUTION_ID | ID associated with the solution | 57955788124b37010084c053 |
| SOLUTION_USER_ID | ID associated with the solution user | 566116085df4b701000258e3 |

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
    https://api.losant.com/orgs/ORG_ID/solutions/SOLUTION_ID/users/SOLUTION_USER_ID
```

### Successful Responses <a name="get-successful-responses"></a>

| Code | Type | Description |
| ---- | ---- | ----------- |
| 200 | [Solution User](schemas.md#solution-user) | Solution user information |

### Error Responses <a name="get-error-responses"></a>

| Code | Type | Description |
| ---- | ---- | ----------- |
| 400 | [Error](schemas.md#error) | Error if malformed request |
| 404 | [Error](schemas.md#error) | Error if solution user was not found |

## Patch

Updates information about a solution user

### Method And Url <a name="patch-method-url"></a>

PATCH https://api.losant.com/orgs/**`ORG_ID`**/solutions/**`SOLUTION_ID`**/users/**`SOLUTION_USER_ID`**

### Authentication <a name="patch-authentication"></a>

A valid api access token is required to access this endpoint. The token must
include at least one of the following scopes:
all.Organization, all.User, solutionUser.*, or solutionUser.patch.

### Request Path Components <a name="patch-path-components"></a>

| Path Component | Description | Example |
| -------------- | ----------- | ------- |
| ORG_ID | ID associated with the organization | 575ed6e87ae143cd83dc4aa8 |
| SOLUTION_ID | ID associated with the solution | 57955788124b37010084c053 |
| SOLUTION_USER_ID | ID associated with the solution user | 566116085df4b701000258e3 |

### Request Headers <a name="patch-headers"></a>

| Name | Required | Description | Default |
| ---- | -------- | ----------- | ------- |
| Authorization | Y | The token for authenticating the request, prepended with Bearer | |

### Request Body <a name="patch-body"></a>

The body of the request should be serialized JSON that validates against
the [Solution User Patch](schemas.md#solution-user-patch) schema. For example, the following would be a
valid body for this request:

```json
{
  "password": "aNewUserPassword",
  "forcePasswordResetOnNextLogin": true
}
```

### Curl Example <a name="patch-curl-example"></a>

```bash
curl -H 'Content-Type: application/json' \
    -H 'Accept: application/json' \
    -H 'Authorization: Bearer YOUR_API_ACCESS_TOKEN' \
    -X PATCH \
    -d '{"password":"aNewUserPassword","forcePasswordResetOnNextLogin":true}' \
    https://api.losant.com/orgs/ORG_ID/solutions/SOLUTION_ID/users/SOLUTION_USER_ID
```

### Successful Responses <a name="patch-successful-responses"></a>

| Code | Type | Description |
| ---- | ---- | ----------- |
| 200 | [Solution User](schemas.md#solution-user) | Updated solution user information |

### Error Responses <a name="patch-error-responses"></a>

| Code | Type | Description |
| ---- | ---- | ----------- |
| 400 | [Error](schemas.md#error) | Error if malformed request |
| 404 | [Error](schemas.md#error) | Error if solution user was not found |
