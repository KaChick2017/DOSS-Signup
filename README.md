# Gump API

- [1. Overview](#1-overview)
- [2. Authentication](#2-authentication)
- [3. Endpoints](#3-endpoints)
  - [3.1. Register](#31-register)

## 1. Overview

Gump API is a JSON based REST API. All requests are made to endpoints beginning: `https://api.kachick.com`.

Endpoint beginning might change later so its better to put it in a configuration file.

All validation error responses are in this format:
```
{
  "field_name": [
    "This field is required"
  ]
}
```

Example:
```
{
  "display_name": [
    "This field is required"
  ],
  "email": [
    "This field is required"
  ]
}
```

## 2. Authentication

API call should be done in server side and server IP must be whitelisted to allow the request.

## 3. Endpoints

### 3.1. Register

Register a photographer
```
POST /album-creators/register
```

Example request:
```
POST /album-creators/register HTTP/1.1
Host: api.kachick.com
Content-Type: application/json
Accept: application/json
```

With the following fields:

| Parameter       | Type    | Required? | Description                                                                 |
|-----------------|---------|-----------|-----------------------------------------------------------------------------|
| `display_name`  | string  | required  | Full name                                                                   |
| `email`         | string  | required  | Must be a valid email address                                               |
| `password`      | string  | required  | Minimum of 6 characters                                                     |
| `place_id`      | string  | required  | Google place ID. Use google place autocomplete.                             |
| `phone_number`  | string  | required  | Must include area code ex. +639178212769                                    |
| `facebook_url`  | string  | optional  | Facebook profile url ex. https://facebook.com/joey                          |
| `instagram_url` | string  | optional  | Instagram profile url ex. https://instagram.com/joey                        |
| `vimeo_url`     | string  | optional  | Vimeo profile url ex. https://vimeo.com/joey                                |
| `youtube_url`   | string  | optional  | Youtube profile url ex. https://youtube.com/joey                            |
| `website`       | string  | optional  | Website url ex. https://mywebsite.com                                       |
| `promo_code`    | string  | optional  | Promo code for getting additional storage                                   |

Must provide atleast 1 of the following social media fields `facebook_url`, `instagram_url`, `vimeo_url`, `youtube_url`.

The response is a JSON object with the following nodes:

Example response:
```
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8

{
  "id": 232423,
  "success": true,
  "login_url": "https://gump.gg/auth/login/?token=jKlr12..."
}
```

| Node            | Type    | Description                                                                  |
|-----------------|---------|------------------------------------------------------------------------------|
| `id`            | integer | Gump ID                                                                      |
| `success`       | boolean | Flag to determine successful registration                                    |
| `login_url`     | string  | This can be used to auto login and redirect the user to their gump dashboard |

Possible errors:

| HTTP Status Code          | Description       |
|---------------------------|-------------------|
| 400 Bad Request           | Validation error  |
