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
curl "https://api.zeromac.com/v1/machines" \
  -H "Authorization: Token zzzzzzz"
```

> The above command returns JSON structured like this:

```json
{
  "data": [
    {
      "id": "85B03DB2-C3DA-4AF2-A89B-B63E8FBCED17",
      "name": "test worker 1",
      "public_ip": "5.6.7.8",
      "created_at": "2019-01-29T00:06:50.865Z",
      "status": "provisioned"
    },
    {
      "id": "E50DE994-7E47-4C4D-8CB4-29FDF2516999",
      "name": "test worker 2",
      "public_ip": "1.2.3.4",
      "created_at": "2019-01-30T00:07:32.228Z",
      "status": "provisioned"
    }
  ]
}
```

This endpoint retrieves all machines.

### HTTP Request

`GET https://api.zeromac.com/v1/machines`

## Get a Specific Machine

```shell
curl "https://api.zeromac.com/v1/machine/85B03DB2-C3DA-4AF2-A89B-B63E8FBCED17" \
  -H "Authorization: Token zzzzzzz"
```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "85B03DB2-C3DA-4AF2-A89B-B63E8FBCED17",
    "name": "test worker 1",
    "public_ip": "5.6.7.8",
    "created_at": "2019-01-29T00:06:50.865Z",
    "status": "provisioned",
    "share_link": null
  }
}
```

This endpoint retrieves a specific machine.

### HTTP Request

`GET https://api.zeromac.com/v1/machine/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the machine to retrieve

## Delete a Specific Machine

```shell
curl "https://api.zeromac.com/v1/machine/85B03DB2-C3DA-4AF2-A89B-B63E8FBCED17" \
  -X DELETE \
  -H "Authorization: Token zzzzzzz"
```

> The above command returns JSON structured like this:

```json
{
  "id": "85B03DB2-C3DA-4AF2-A89B-B63E8FBCED17",
  "message" : "Machine was successfully deleted"
}
```

This endpoint deletes a specific machine.

### HTTP Request

`DELETE https://api.zeromac.com/v1/machine/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the machine to delete


## Create a Machine

```shell
curl "https://api.zeromac.com/v1/machines" \
  -H "Authorization: Token zzzzzzz" \
  -H "Content-type: application/json" \
  --data '{
    "name": "Test Box 1",
    "type": "1cpu",
    "password": "hello123"
  }'

```

> The above command returns JSON structured like this:

```json
{
  "id": "85B03DB2-C3DA-4AF2-A89B-B63E8FBCED17",
  "message" : "Machine is provisioning"
}
```

This endpoint creates a machine.

### HTTP Request

`POST https://api.zeromac.com/v1/machines`

### Query Parameters

Parameter | Description
--------- | -----------
name | (Required) Name of the machine to create
type | (Required) Type of virtual machines to create: `1cpu`, `2cpu`, `4cpu`, or `6cpu`
password | (Required) Password to be set for `admin` user
vnc | Enable the Screen Sharing server: `true` or `false`. Defaults to `true`
ssh_github_username | If specified, enables sshd and authorizes the public keys from the specified GitHub user.
ssh_pubkey | If specified, enables sshd and installs the specified public keys. Multiple keys can be specified in the string, separated by newlines.
disable_sip | `true` or `false`. If `true`, System Integrity Protection is disabled. Defaults to `false`
image |  `10.15`, `10.14`, `10.13`, `10.12`, `10.11`, `10.10`, or `latest`. If not specified, defaults to `latest`, which is currently `10.15`

## Disable share link for a machine

```shell
curl "https://api.zeromac.com/v1/machines/<id>/share_link" \
  -H "Authorization: Token zzzzzzz" \
  -XDELETE

```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "85B03DB2-C3DA-4AF2-A89B-B63E8FBCED17",
    "name": "test worker 1",
    "public_ip": "5.6.7.8",
    "created_at": "2019-01-29T00:06:50.865Z",
    "status": "provisioned",
    "share_link": null
  }
}
```

This endpoint diisables the share link on a machine. The share link provides
unauthenticated access to a web VNC console for the machine. You can use
share links to provide access to the machine to members outside your
organization.

### HTTP Request

`DELETE https://api.zeromac.com/v1/machine/<id>/share_link`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the machine to retrieve

## Enable share link for a machine

```shell
curl "https://api.zeromac.com/v1/machines/<id>/share_link" \
  -H "Authorization: Token zzzzzzz" \
  -XPUT

```

> The above command returns JSON structured like this:

```json
{
  "data": {
    "id": "85B03DB2-C3DA-4AF2-A89B-B63E8FBCED17",
    "name": "test worker 1",
    "public_ip": "5.6.7.8",
    "created_at": "2019-01-29T00:06:50.865Z",
    "status": "provisioned",
    "share_link": "https://zeromac.com/machines/share/05Ea9O9RuQpSdFJ5XQGEJYw4N8j7dxe3GmxFNg6zu7dQvupy12fSiLRpdzr9feWouvIM0Vs57V2JwBdO9ajjHruMW6lTTdTmcoJvh7ij35cYh9ggnyqK7YTCrH63S7xx"
  }
}
```

This endpoint enables the share link on a machine. The share link provides
unauthenticated access to a web VNC console for the machine. You can use
share links to provide access to the machine to members outside your
organization.

### HTTP Request

`PUT https://api.zeromac.com/v1/machine/<id>/share_link`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the machine to retrieve
