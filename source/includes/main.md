# Introduction


Connect to Cosmic JS through RESTful requests to the Cosmic JS API.  All requests with Body data need to have the correct request header set `Content-Type: application/json`.

> API Endpoint

```bash
https://api.cosmicjs.com
```

```javascript
https://api.cosmicjs.com
```

# Authentication

> Definition

```bash
POST https://api.cosmicjs.com/v1/authenticate
```

```javascript
Cosmic.authenticate()
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
webhooks | false | `Array` | Populate your Bucket with <a href="https://cosmicjs.com/docs/webhooks" target="_blank">Webhooks</a>
extensions | false | `Array` | Populate your Bucket with <a href="https://cosmicjs.com/docs/extensions" target="_blank">Extensions</a>


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


Returns the entire Bucket.  If you would like to restrict read access to your Bucket, you can do so in Your Bucket > Basic Settings.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
read_key | false | `String` | Restrict read access to your Bucket
hide_metafields | false | `Enum` | true, Hides metafields





# Object Types

## Add Object Type

> Definition

```bash
POST https://api.cosmicjs.com/v1/:bucket-slug/add-object-type
```


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

Add a new Object Type to your Bucket.

title is the only required field. You can add Metafields which will be available as default Metafields for each new Object in this Object Type. If a write key is enabled on the requested Bucket, the variable write_key will need to be present in the Body.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
title | true | `String` | Plural title of your Object Type
slug | false | `String` | Plural slug of your Object Type
singular | false | `String` | Singular title of your Object Type
metafields | false | `Array` | Default Metafields for each Object in this type

## Get Object Types

> Definition

```bash
GET https://api.cosmicjs.com/v1/:bucket-slug/object-types
```
```javascript
GET https://api.cosmicjs.com/v1/:bucket-slug/object-types
```

> Example Request

```bash
curl "https://api.cosmicjs.com/v1/wedding-site/object-types"
```
```javascript
Cosmic.getObjectTypes()
```

> Example Response

```json
{ 
  "object_types": [
    {
      "title": "Groomsmen",
      "slug": "groomsmen",
      "singular": "Groomsman",
      "metafields": [
        {
          "edit": "",
          "value": "",
          "key": "image",
          "title": "Image",
          "type": "file",
          "children": null
        },
        {
          "edit": "",
          "value": "",
          "key": "official-title",
          "title": "Official Title",
          "type": "text",
          "children": null
        }
      ],
      "order": 2
    },
    {
      "title": "Bridesmaids",
      "slug": "bridesmaids",
      "singular": "Bridesmaid",
      "metafields": [
        {
          "edit": 1,
          "value": "",
          "key": "",
          "title": "Image",
          "type": "file",
          "children": null
        },
        {
          "edit": 1,
          "value": "",
          "key": "",
          "title": "Official Title",
          "type": "text",
          "children": null
        }
      ],
      "order": 3
    },
    {
      "title": "Sections",
      "slug": "sections",
      "singular": "Section",
      "metafields": [],
      "order": 1
    }
  ]
}
```


Get all Object Types in your Bucket.



# Objects

The following endpoints allow you to add, edit and delete Objects in your Bucket.  If you would like to restrict read or write access to your Bucket, you can do so in Your Bucket > Basic Settings.

## Add Object

> Definition

```bash
POST https://api.cosmicjs.com/v1/:bucket-slug/add-object
```

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
  ],
  "options": {
    "slug_field": false
  }
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
        "title": "Headline",
        "key": "headline",
        "type": "text",
        "value": "Learn Cosmic JS!"
      },
      {
        "title": "Author",
        "key": "author",
        "type": "text",
        "value": "Quasar Jones"
      }
    ],
    "bucket": "568c5bbefd0dce302c000001",
    "type_slug": "examples",
    "created_at": "2016-01-06T00:28:39.982Z",
    "_id": "568c5fb72f0c5d532d000001"
  }
}
```


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

> Definition

```bash
GET https://api.cosmicjs.com/:bucket-slug/objects
```

> Example Request

```bash
curl "https://api.cosmicjs.com/v1/wedding-site/objects?pretty=true&hide_metafields=true&limit=2"
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
    {
      "_id": "55b3da7740d7a3791b000002",
      "bucket": "55b3d557df0fb1df7600004b",
      "slug": "main-menu",
      "title": "Main Menu",
      "content": "<p><br></p>",
      "type_slug": "sections",
      "created": "2015-07-25T18:50:31.809Z",
      "metadata": {
        "our-story": "Our Story",
        "accomodations": "Accomodations",
        "registry": "Registry"
      }
    },
    {
      "_id": "55b3da7740d7a3791b000003",
      "bucket": "55b3d557df0fb1df7600004b",
      "slug": "global",
      "title": "Global",
      "content": "<p><br></p>",
      "type_slug": "sections",
      "created": "2015-07-25T18:50:31.812Z",
      "metadata": {
        "site-title": "Carol and Jack Wedding Website",
        "menu-title": "Carol & Jack",
        "description": "This is the wedding website for the Jack and Carol Wedding on November 22, 2014 in Dallas, TX.",
        "author": "Tony Spiro",
        "footer-text": "Cosmic JS &copy; 2015"
      }
    }
  ]
}
```

This endpoint returns all Objects from the specified Bucket.


Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
pretty | false | `Enum` | true, Makes the response more reader-friendly
limit | false | `Number` | The number of Objects to return
skip | false | `Number` | The number of Objects to skip
status | false | `Enum` | all, Return published and draft status Objects
read_key | false | `String` | Restrict read access to your Bucket
revision | false | `String` | The revision_id of the Object Revision
hide_metafields | false | `Enum` | true, Hides metafields
sort | false | `Enum` | created_at,-created_at,modified_at,-modified_at,random









# Metafields

Metafields can be added to Objects and Object Types via the API. The model matches the Metafields model on API GET requests which includes minimum properties `type`, `title`, `key` and `value`. For text and textarea Metafields, you can also add validation via the `regex` and `regex_message` properties.

As a general rule, you can copy the Metafields response model on GET requests and send it in a request body to add Metafields via the API.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
type | true | `Enum` | text, textarea, html-textarea, <br />select-dropdown, object, objects, <br />file, date, radio-buttons, check-boxes, <br />repeater, parent, markdown
title | true | `String` | Your Bucket title
key | true | `String` | Unique identifier for your Bucket
value | false | `String` | Metafield value
required | false | `Bool` | A value is required
regex | false | `String` | Restrict the value to match a regular expresssion
regex_message | false | `Array` | The message displayed when the value fails the regex
children | false | `Array` | Add nested Metafields
minlength | false | `Number` | Add minlength to `text` or `textarea` Metafields
maxlength | false | `Number` | Add maxlength to `text` or `textarea` Metafields

## Add to Object Type

Add default Metafields to Object Types via the API.

> Definition

```bash
POST https://api.cosmicjs.com/v1/:bucket-slug/add-object-type
```

> Example Request

```json
{
  "title": "Users",
  "singular": "User",
  "slug": "users",
  "metafields": [
    {
      "key": "first_name",
      "title": "First Name",
      "type": "text",
      "value": "",
      "required": true
    },
    {
      "key": "last_name",
      "title": "Last Name",
      "type": "text",
      "value": "",
      "required": true
    },
    {
      "key": "email",
      "title": "Email",
      "type": "text",
      "value": "",
      "regex": "/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/",
      "regex_message": "You must enter a valid email."
    },
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
    }
  ]
}
```


## Add to Object

> Definition

```bash
POST https://api.cosmicjs.com/v1/:bucket-slug/add-object
```

> Example Request

```json
{
  "title": "Blog Post Example",
  "type_slug": "blog-posts",
  "content": "This is some amazing blog content...",
  "metafields": [
    {
      "title": "Headline",
      "key": "headline",
      "type": "text",
      "value": "What I Learned Today"
    },
    {
      "title": "Author",
      "key": "author",
      "type": "object",
      "value": "55b3d557df0fb1df7600004b"
    },
    {
      "title": "Categories",
      "key": "categories",
      "type": "objects",
      "value": "55b3d557df0fb1df7600004a,55b3d557df0fb1df7600004e,55b3d557df0fb1df7600004i"
    },
  ]
}
```

For Single Object type Metafields, you can add the Object ID as the value to connect the Object.  For Multiple Object type Metafields, you can add the Object IDs as comma-separated values to connect the Object.





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



