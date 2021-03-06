# API Tokens

API Tokens are used for authenticating with the API. They are used in combination with your normal login as part of a standard HTTP Basic Auth payload. See [Authentication](#authentication) for more details on how to authenticate to the API with a token.

You may have as many API Tokens as you like to help limit your exposure to single compromised token. If you happen to accidentally lose control of a token by emailing it or pasting it on a website, it is convenient to deactivate or delete that token, rendering it inoperable for authentication, without interfering with the operation of other agents or clients using other tokens. We recommend having as many API Tokens as is convenient for each client or group of clients to have their own.

#### API Token Properties

Property | Definition
-------- | ----------
name | A name for the API Token. There is no limit on length or uniqueness, so use whatever naming scheme makes it easiest for you to keep them organized. Name may be `null` for any legacy or auto generated tokens, but it is required for any new tokens created.
token | A long random string of characters to be used as the "password" segment of the basic auth header. This is auto-generated, and any attempt to set it will be ignored.
active | A true/false value indicating the ability of a Token to be used for authentication. Attempting to authenticate using a token that has active set to false will result in a 401 response.
role | The name of the role that encapsulates the permissions this token has. Must be one of: "admin", "recorder", or "viewer". See the [Knowledge Base Article](https://docs.appoptics.com/kb/user_org/tokens/) for more details.


## Create a Token

#### HTTP Request

`POST https://api.appoptics.com/v1/api_tokens`

>Create a new API Token by specifying the `name` and `role`:

```bash
curl \
  -u $APPOPTICS_TOKEN: \
  -d 'name=My New Token&role=admin' \
  -X POST \
  'https://api.appoptics.com/v1/api_tokens'
```

```ruby
Not available
```

>Using JSON

```json
{
  "name": "My New Token",
  "role": "admin"
}
```

>Response Code

```
201 Created
```

>Response Headers

```
Location: /v1/api_tokens/28
```

>Response Body

```json
{
  "name": "My New Token",
  "token": "24f9fb2134399595b91da1dcac39cb6eafc68a07fa08ad3d70892b7aad10e1cf",
  "active": true,
  "role": "admin",
  "href": "http://api.appoptics.dev/v1/api_tokens/28",
  "created_at": "2013-02-01 18:53:38 UTC",
  "updated_at": "2013-02-01 18:53:38 UTC"
}
```

Creates a new API Token.

#### Headers

This specifies the format of the data sent to the API.

For HTML (default):

`Content-Type: application/x-www-form-urlencoded`

For JSON:

`Content-Type: application/json`


## Retrieve a Token

>Retrieve a token that contains the word "token" within the `name` parameter:

```bash
curl \
  -i \
  -u $APPOPTICS_TOKEN: \
  -X GET \
  'https://api.appoptics.com/v1/api_tokens?name=*token*'
```

>Response Code

```
200 OK
```

>Response Body

```json
{
  "api_tokens": [
    {
      "name": "Token for collectors",
      "token": "24f9fb2134399595b91da1dcac39cb6eafc68a07fa08ad3d70892b7aad10e1cf",
      "active": true,
      "role": "recorder",
      "href": "http://api.appoptics.com/v1/api_tokens/28",
      "created_at": "2013-02-01 18:53:38 UTC",
      "updated_at": "2013-02-01 18:53:38 UTC"
    },
    {
      "name": "Token that has been disabled",
      "active": false,
      "role": "viewer",
      "href": "http://api.appoptics.com/v1/api_tokens/29",
      "token": "d1ffbbbe327c6839a71023c2a8c9ba921207e32e427a49fb221843d74d63f7b8",
      "created_at": "2013-02-01 18:54:28 UTC",
      "updated_at": "2013-02-01 18:54:28 UTC"
    }
  ],
    "query": {
        "found": 2,
        "length": 2,
        "offset": 0,
        "total": 2
    }
}
```

Returns the details for API Tokens that match a name. Supports wildcards,
e.g. `? name=*token*`.

#### HTTP Request

`GET https://api.appoptics.com/v1/api_tokens/:name`

### Retrieve a Token by ID

>Retrieve the token with the `id` 28:

```bash
curl \
  -i \
  -u $APPOPTICS_TOKEN: \
  -X GET \
  'https://api.appoptics.com/v1/api_tokens/28'
```

>Response Code

```
200 OK
```

>Response Body

```json
{
  "name": "My New Token",
  "token": "24f9fb2134399595b91da1dcac39cb6eafc68a07fa08ad3d70892b7aad10e1cf",
  "active": true,
  "role": "admin",
  "href": "http://api.appoptics.dev/v1/api_tokens/28",
  "created_at": "2013-02-01 18:53:38 UTC",
  "updated_at": "2013-02-01 18:53:38 UTC"
}
```

Returns the details for a specific API Token by providing the `id` of the token. The `id` can be found in the URL of the `href` parameter provided when [listing all API tokens](#list-all-tokens).

#### HTTP Request

`GET https://api.appoptics.com/v1/api_tokens/:id`

## Update a Token

>Update the token associated with the `id` 28:

```bash
curl \
  -u $APPOPTICS_TOKEN: \
  -d 'name=New Token Name&active=false&role=admin' \
  -X PUT \
  'https://api.appoptics.com/v1/api_tokens/28'
```

```ruby
Not available
```

```python
Not available
```

>Response Code

```
200 OK
```

>Response Body

```
{
  "name": "New Token Name",
  "token": "24f9fb2134399595b91da1dcac39cb6eafc68a07fa08ad3d70892b7aad10e1cf",
  "active": false,
  "role": "admin",
  "href": "http://api.appoptics.dev/v1/api_tokens/28",
  "created_at": "2013-02-01 18:53:38 UTC",
  "updated_at": "2013-02-01 19:51:22 UTC"
}
```

Modify an API Token, such as changing the name, or flagging as active/inactive.

#### HTTP Request

`PUT https://api.appoptics.com/v1/api_tokens/:id`

#### Headers

This specifies the format of the data sent to the API.

For HTML (default):

`Content-Type: application/x-www-form-urlencoded`

For JSON:

`Content-Type: application/json`

## Delete a Token

>Delete the API token with ID `28`:

```bash
curl \
  -i \
  -u $APPOPTICS_TOKEN: \
  -X DELETE \
  'https://api.appoptics.com/v1/api_tokens/28'
```

```ruby
Not available
```

>Response Code

```
204 No Content
```

Delete the API Token identified by `:id`.

#### HTTP Request

`DELETE https://api.appoptics.com/v1/api_tokens/:id`

## List all Tokens

```bash
curl \
  -i \
  -u $APPOPTICS_TOKEN: \
  -X GET \
  'https://api.appoptics.com/v1/api_tokens'
```

```ruby
Not available
```

>Response Code

```
200 OK
```

>Response Body

```json
{
  "query": {
    "found": 3,
    "length": 3,
    "offset": 0,
    "total": 3
  },
  "api_tokens": [
    {
      "name": null,
      "token": "9b593b3dff7cef442268c3056625981b92d5feb622cfe23fef8d716d5eecd2c3",
      "active": true,
      "role": "admin",
      "href": "http://api.appoptics.com/v1/api_tokens/2",
      "created_at": "2013-01-22 18:08:15 UTC",
      "updated_at": "2013-01-22 18:08:15 UTC"
    },
    {
      "name": "Token for collectors",
      "token": "24f9fb2134399595b91da1dcac39cb6eafc68a07fa08ad3d70892b7aad10e1cf",
      "active": true,
      "role": "recorder",
      "href": "http://api.appoptics.com/v1/api_tokens/28",
      "created_at": "2013-02-01 18:53:38 UTC",
      "updated_at": "2013-02-01 18:53:38 UTC"
    },
    {
      "name": "Token that has been disabled",
      "active": false,
      "role": "viewer",
      "href": "http://api.appoptics.com/v1/api_tokens/29",
      "token": "d1ffbbbe327c6839a71023c2a8c9ba921207e32e427a49fb221843d74d63f7b8",
      "created_at": "2013-02-01 18:54:28 UTC",
      "updated_at": "2013-02-01 18:54:28 UTC"
    }
  ]
}
```

Returns all API Tokens.

#### HTTP Request

`GET https://api.appoptics.com/v1/api_tokens`
