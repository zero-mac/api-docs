---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

#includes:
#  - errors

search: true
---

# Introduction

Welcome to the zeromac API documentation! You can use our API to create, destroy, and view information around your provisioned machines.

Our documentation shows examples on how to use our HTTP API with curl in your shell, but you can use the HTTP libraries available in any programming language to make the same API calls.

# Authentication

> To authorize, use this code:

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: Token zzzzzzz"
```

> Make sure to replace `zzzzzzz` with your API key.

zeromac uses API tokens to allow access to the API. You can register a new API token in [your dashboard ](https://zeromac.com/api).

zeromac expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: Token zzzzzzz`

<aside class="notice">
You must replace <code>zzzzzzz</code> with your personal API key.
</aside>

# Machines

## Get All Machines

```shell
curl "https://api.zeromac.com/v1/machines"
  -H "Authorization: zzzzzzz"
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": "85B03DB2-C3DA-4AF2-A89B-B63E8FBCED17",
    "name": "test worker 1",
    "public_ip": "5.6.7.8",
    "created_at": "2019-01-29T00:06:50.865Z"
  },
  {
    "id": "E50DE994-7E47-4C4D-8CB4-29FDF2516999",
    "name": "test worker 2",
    "public_ip": "1.2.3.4",
    "created_at": "2019-01-30T00:07:32.228Z"
  }
]
```

This endpoint retrieves all machines.

### HTTP Request

`GET https://api.zeromac.com/v1/machines`

## Get a Specific Machine

```shell
curl "https://api.zeromac.com/v1/machine/85B03DB2-C3DA-4AF2-A89B-B63E8FBCED17"
  -H "Authorization: zzzzzzz"
```

> The above command returns JSON structured like this:

```json
{
  "id": "85B03DB2-C3DA-4AF2-A89B-B63E8FBCED17",
  "name": "test worker 1",
  "public_ip": "5.6.7.8",
  "created_at": "2019-01-29T00:06:50.865Z"
}
```

This endpoint retrieves a specific machine.

### HTTP Request

`GET https://api.zeromac.com/v1/machines/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the machine to retrieve

## Delete a Specific Machine

```shell
curl "https://api.zeromac.com/v1/machine/85B03DB2-C3DA-4AF2-A89B-B63E8FBCED17"
  -X DELETE
  -H "Authorization: zzzzzzz"
```

> The above command returns JSON structured like this:

```json
{
  "id": "85B03DB2-C3DA-4AF2-A89B-B63E8FBCED17",
  "message" : "Machine was successfully deleted."
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE https://api.zeromac.com/v1/machine/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

