# Introduction


```bash
https://api.cosmicjs.com/v1
```

Connect to Cosmic JS through RESTful requests to the Cosmic JS API.  All requests use the base URL:

### Base URL

`https://api.cosmicjs.com/v1`

# Authentication

> Example Request

```bash
# With shell, you can just pass your email and password
curl -X POST https://api.cosmicjs.com/v1/authenticate -d "email=user@myservice.com&password=mypassword"
```

```javascript
const Cosmic = require('cosmicjs');

const response = await Cosmic.authenticate({ email: "user@myservice.com", password: "mypassword" });
```

> Example Response

```json
{
  "success": true,
  "message": "Token created successfully.",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXV.eyJlbWFpbCI6InNwaXJvbnlAZ21haWwuY29tIiwicGFzc3dvcmQiOiIxNzlhZDQ1YzZjZTJjYjk3Y2YxMDI5ZTIxMjA0NmU4MSIsImlhdCI6MTUxNDQ5NzI3N30.ep4cEgH_SqItQ5McJArJtljS3GSJedyEcDRlnu9yb-U"
}
```

### Endpoint

`https://api.cosmicjs.com/v1/authenticate`

Send your `email` and `password` to receive your access token. Your access token will be used to add Buckets to your account as well as other account-related access. You do not need to use the token to edit your Bucket. Your Bucket has its own read and write keys for restricted access.

# Add Bucket
`title` is the only required property.  See the table below for the other optional properties.

> Example Request

```bash
curl -X POST https://api.cosmicjs.com/v1/buckets\
-H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXV.eyJlbWFpbCI6InNwaXJvbnlAZ21haWwuY29tIiwicGFzc3dvcmQiOiIxNzlhZDQ1YzZjZTJjYjk3Y2YxMDI5ZTIxMjA0NmU4MSIsImlhdCI6MTUxNDQ5NzI3N30.ep4cEgH_SqItQ5McJArJtljS3GSJedyEcDRlnu9yb-U"\
-H "Content-Type: application/json"\
-d '{"title": "My New Bucket"}'
```

```javascript
const Cosmic = require('cosmicjs');

const response = await Cosmic.authenticate({ email: "user@myservice.com", password: "mypassword" });
```

> Example Response

```json
{
  "bucket": {
    "_id": "55b3d557df0fb1df7600004b",
    "slug": "my-new-bucket",
    "title": "My New Bucket"
  }
}
```

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
title | true | `String` | Your Bucket title
slug | false | `String` | Unique identifier for your Bucket
read_key | false | `String` | Used to retrieve content from your Bucket
write_key | false | `String` | Used to edit content in your Bucket
object_types | false | `Array` | Populate your Bucket with Object Types
objects | false | `Array` | Populate your Bucket with Objects
media | false | `Array` | Populate your Bucket with Media
media_folders | false | `Array` | Populate your Bucket with Media Folders
webhooks | false | `Array` | Populate your Bucket with Webhooks
extensions | false | `Array` | Populate your Bucket with Extensions

# Add Content

# Get Content

## MAKE TABLE

### Optional Parameters
All JSON responses can be formatted to be pretty for easy reading by adding the `pretty=true` query parameter to the request URL. There are optional parameters available for pagination where indicated (`limit` and `skip`). You can set the order of your results with the sort order parameter `sort`. If you would like to view draft status Objects in your results you can set `status=all`. And if you've added a read access key to your Bucket, you will need to add the `read_key` query parameter to your request. For POST, PUT and DELETE methods, if you set a write access key to your Bucket you will need to include the `write_key` to your Body request.

### Returning Single Object Revision
If you would like to view a revision, you can add `revision=revision_id` at the end of the single Object endpoint. You can find the revision_id on the Edit Object page in your Dashboard.

### Metafields and Metadata
Metafields extend your Object data. From the API response, the Metafields parameter provides you with additional form field values including title, key and type and is provided in an array format. The Metadata parameter returns a key / value response and is the recommended way to get Metafield values from your Object. To hide Metafields, add the parameter hide_metafields=true to the endpoint URL. All of the following example responses below show results from having hide_metafields=true. Hidden Metafields will be the default behavior in a future API release.

## Bucket

> Example Request

```bash
curl "https://api.cosmicjs.com/v1/wedding-site"
```

```javascript
const config = {
  bucket: {
    slug: 'test-bucket',
    read_key: '1234asdf'
  }
}
const Cosmic = require('cosmicjs');
const api = Cosmic.config(config);
const response = await api.getBucket();
```

> Example Response

```json
{
  "bucket": {
    "_id": "55b3d557df0fb1df7600004b",
    "slug": "wedding-site",
    "title": "Wedding Site",
    "object_types": [
      ...
    ],
    "links": [
      ...
    ],
    "objects": [
      ...
    ],
    "media": [
      ...
    ],
    "media_folders": [
      ...
    ]
  }
}
```


This endpoint returns the entire Bucket.

### HTTP Request

`GET https://api.cosmicjs.com/:bucket-slug`

## Get Objects

> Example Request

```bash
curl "https://api.cosmicjs.com/v1/wedding-site/objects"
```

```javascript
const config = {
  bucket: {
    slug: 'test-bucket',
    read_key: '1234asdf'
  }
}
const Cosmic = require('cosmicjs');
const api = Cosmic.config(config);
const response = await api.getObjects();
```

> Example Response

```json
{
  "objects": [
    ...
  ]
}
```

This endpoint returns all Objects from the specified Bucket.

### HTTP Request

`GET https://api.cosmicjs.com/:bucket-slug`


# Edit Content

# Delete Content
