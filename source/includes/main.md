# Introduction


Connect to Cosmic JS through RESTful requests to the Cosmic JS API.  All requests with Body data need to have the correct request header set `Content-Type: application/json`.

> Base URL

```bash
https://api.cosmicjs.com/v1
```

# Authentication

> Definition

```bash
POST https://api.cosmicjs.com/v1/authenticate
```

> Example Request

```bash
# With shell, you can just pass your email and password
curl -X POST https://api.cosmicjs.com/v1/authenticate \
-d email=myname@myservice.com \
-d password=mypassword
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

Send your `email` and `password` to receive your access token. Your access token will be used to add Buckets to your account as well as other account-related access. You do not need to use the token to edit your Bucket. Your Bucket has its own read and write keys for restricted access.  Go to https://cosmicjs.com/signup to create an account.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
email | true | `String` | Your Cosmic JS login email
password | false | `String` | Your Cosmic JS login password













# Buckets


## Add Bucket
`title` is the only required property.  See the table below for the other optional properties.  The Bucket request matches the `bucket.json` file located in Your Bucket Dashboard > Import Export.


> Definition

```bash
POST https://api.cosmicjs.com/v1/buckets
```

> Example Request

```bash
curl -X POST https://api.cosmicjs.com/v1/buckets \
-H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXV.eyJlbWFpbCI6InNwaXJvbnlAZ21haWwuY29tIiwicGFzc3dvcmQiOiIxNzlhZDQ1YzZjZTJjYjk3Y2YxMDI5ZTIxMjA0NmU4MSIsImlhdCI6MTUxNDQ5NzI3N30.ep4cEgH_SqItQ5McJArJtljS3GSJedyEcDRlnu9yb-U" \
-H "Content-Type: application/json" \
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
read_key | false | `String` | Restrict read access to your Bucket
write_key | false | `String` | Restrict write access to your Bucket
object_types | false | `Array` | Populate your Bucket with Object Types
objects | false | `Array` | Populate your Bucket with Objects
media | false | `Array` | Populate your Bucket with Media
media_folders | false | `Array` | Populate your Bucket with Media Folders
webhooks | false | `Array` | Populate your Bucket with Webhooks
extensions | false | `Array` | Populate your Bucket with Extensions


## Get Bucket

> Definition

```bash
GET https://api.cosmicjs.com/:bucket-slug
```

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


Returns the entire Bucket.











# Objects

The following endpoints allow you to add content to your Bucket.  If you would like to restrict read or write access to your Bucket.  You can do so in Your Bucket > Basic Settings.

## Add Object

> Example Request Body

```json
{
  "title": "Cosmic JS Example",
  "type_slug": "examples",
  "content": "Learning the Cosmic JS API is really fun and so easy",
  "metafields": [
    {
      "key": "Headline",
      "type": "text",
      "value": "Learn Cosmic JS!"
    },
    {
      "key": "Author",
      "type": "text",
      "value": "Quasar Jones"
    }
  ]
}
```

> Example Response

```json
{
  "object": {
    "slug": "cosmic-js-example",
    "title": "Cosmic JS Example",
    "content": "Learning the Cosmic JS API is really fun and so easy",
    "metafields": [
      {
        "key": "headline",
        "type": "text",
        "value": "Learn Cosmic JS!",
        "title": "Headline"
      },
      {
        "key": "author",
        "type": "text",
        "value": "Quasar Jones",
        "title": "Author"
      }
    ],
    "bucket": "568c5bbefd0dce302c000001",
    "type_slug": "examples",
    "created": "2016-01-06T00:28:39.982Z",
    "_id": "568c5fb72f0c5d532d000001"
  }
}
```

### Endpoint

`POST https://api.cosmicjs.com/v1/:bucket-slug/add-object`

Add a new Object to your Bucket.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
type_slug | true | `String` | Add Object to Object Type
title | true | `String` | Your Bucket title
slug | false | `String` | Unique identifier for your Bucket
content | false | `String` | Add Content to your Object
options.slug_field | false | `Bool` | Set to false to hide the slug field
options.content_editor | false | `Bool` | Set to false to hide the content editor
write_key | false | `String` | Restrict write access to your Bucket
metafields | false | `Array` | Add Metafields to your Object


Required post values include type_slug and title. You can add Metafields (and children of metafields). If a write key is enabled on the requested Bucket, the property `write_key` will need to be present in the Body.


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

### Endpoint

`GET https://api.cosmicjs.com/:bucket-slug/objects`


Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
pretty | false | `Enum` | true, Makes the response more reader-friendly
limit | false | `Number` | The number of Objects to return
skip | false | `Number` | The number of Objects to skip
status | false | `Enum` | all, Return published and draft status Objects
write_key | false | `String` | Restrict write access to your Bucket
revision | false | `String` | The revision_id of the Object Revision
hide_metafields | false | `Enum` | true, Hides metafields
sort | false | `Enum` | created_at,-created_at,modified_at,-modified_at,random



## Metafields

> Example Request

```json
{
  "title": "Users",
  "singular": "User",
  "slug": "users",
  "metafields": [
    {
      "key": "avatar",
      "title": "Avatar",
      "type": "file",
      "value": ""
    },
    {
      "key": "tagline",
      "title": "Tagline",
      "type": "text",
      "value": ""
    },
    {
      "key": "email",
      "title": "Email",
      "type": "text",
      "value": "",
      "regex": "/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/",
      "regex_message": "You must enter a valid email."
    }
  ]
}
```


### Example: Add Metafields to Object Type

### Endpoint

`POST https://api.cosmicjs.com/v1/:bucket-slug/add-object-type`

Metafields can be added to Objects and Object Types via the API. The model matches the Metafields model on API GET requests which includes minimum properties `type`, `title`, `key` and `value`. For text and textarea Metafields, you can also add validation via the `regex` and `regex_message` properties.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
type | true | `Enum` | text, textarea, html-textarea, <br />select-dropdown, object, objects, <br />file, date, radio-buttons, check-boxes, <br />repeater, parent, markdown
title | true | `String` | Your Bucket title
key | true | `String` | Unique identifier for your Bucket
value | true | `String` | Metafield value
required | true | `Bool` | A value is required
regex | false | `String` | Restrict the value to match a regular expresssion
regex_message | false | `Array` | The message displayed when the value fails the regex
children | false | `Array` | Add nested Metafields






# Object Types

## Add Object Type

> Example Request Body

```json
{
  "title": "Pages",
  "singular": "Page",
  "slug": "pages",
  "metafields": [
    {
      "type": "text",
      "title": "Headline",
      "key": "headline",
      "required": true
    },
    {
      "type": "file",
      "title": "Hero",
      "key": "hero",
      "required": true
    }
  ]
}
```

> Example Response

```json
{
  "object_type": {
    "slug": "pages",
    "title": "Pages",
    "singular": "Page",
    "metafields": [
      {
        "type": "text",
        "title": "Headline",
        "key": "headline",
        "required": true
      },
      {
        "type": "file",
        "title": "Hero",
        "key": "hero",
        "required": true
      }
    ],
    "created_at": "2017-05-30T02:06:35.373Z",
    "metadata": null
  }
}
```

### Endpoint

`POST https://api.cosmicjs.com/v1/:bucket-slug/add-object-type`

Add a new Object Type to your Bucket.

title is the only required field. You can add Metafields which will be available as default Metafields for each new Object in this Object Type. If a write key is enabled on the requested Bucket, the variable write_key will need to be present in the Body.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
title | true | `String` | Plural title of your Object Type
slug | false | `String` | Plural slug of your Object Type
singular | false | `String` | Singular title of your Object Type
metafields | false | `Array` | Default Metafields for each Object in this type








# Media

> Example Request

```json
{
  "media": "your-media-multipart-form-data",
  "folder": "your-folder-slug"
}
```


> Example Response

```json
{
  "media": {
    "name": "c20391e0-b8a4-11e6-8836-fbdfd6956b31-bird.jpg",
    "original_name": "bird.jpg",
    "size": 457307,
    "type": "image/jpeg",
    "bucket": "5839c67f0d3201c114000004",
    "created": "2016-12-02T15:34:05.054Z",
    "location": "https://cosmicjs.com/uploads",
    "url": "https://s3-us-west-2.amazonaws.com/cosmicjs/c20391e0-b8a4-11e6-8836-fbdfd6956b31-bird.jpg",
    "imgix_url": "https://cosmic-s3.imgix.net/c20391e0-b8a4-11e6-8836-fbdfd6956b31-bird.jpg"
  }
}
```

### Endpoint

`POST https://api.cosmicjs.com/v1/:bucket-slug/media`

Required post values include media which is the name of your media sent. If a write key is enabled on the requested bucket, the variable `write_key` will need to be present in the Body. You can also add an optional folder param to add the Media to a specific folder.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
media | true | `File` | Media object
write_key | false | `String` | Your Bucket write key
folder | false | `String` | Media folder slug



