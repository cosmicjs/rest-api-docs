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
    "_id": "568c5fb72f0c5d532d000001",
    "options": {
      "slug_field": false
    }
  }
}
```


Add a new Object to your Bucket.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
type_slug | true | `String` | Add Object to Object Type
title | true | `String` | Your Bucket title
slug | false | `String` | Unique identifier for your Object
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



## Get Objects in Type

> Definition

```json
GET https://api.cosmicjs.com/v1/:bucket-slug/object-type/:type-slug
```

> Example Request

```bash
curl "https://api.cosmicjs.com/v1/wedding-site/object-type/groomsmen?limit=3"
```
```javascript
Cosmic.getObjectType()
```

> Example Response

```json
{
  "objects": [
    {
      "_id": "55b3da7740d7a3791b000009",
      "bucket": "55b3d557df0fb1df7600004b",
      "slug": "chad-henly",
      "title": "Chad Henly",
      "content": "<p>&nbsp;&nbsp;&nbsp;&nbsp;<br></p>",
      "type_slug": "groomsmen",
      "created": "2015-07-25T18:50:31.820Z",
      "modified": "2015-07-25T18:51:44.249Z",
      "metadata": {
        "image": {
          "url": "https://s3-us-west-2.amazonaws.com/cosmicjs/3181a814-93d9-ad8f-74ce-1eeb64023b61-1420162840289-mke.jpg",
          "imgix_url": "https://cosmic-s3.imgix.net/3181a814-93d9-ad8f-74ce-1eeb64023b61-1420162840289-mke.jpg"
        },
        "official-title": "Best Man"
      }
    },
    {
      "_id": "55b3da7740d7a3791b00000a",
      "bucket": "55b3d557df0fb1df7600004b",
      "slug": "eric-harland",
      "title": "Eric Harland",
      "content": "<p>&nbsp;&nbsp;&nbsp;&nbsp;<br></p>",
      "type_slug": "groomsmen",
      "created": "2015-07-25T18:50:31.821Z",
      "modified": "2015-07-25T18:52:35.032Z",
      "metadata": {
        "image": {
          "url": "https://s3-us-west-2.amazonaws.com/cosmicjs/a499fdab-10b5-5168-9ef1-8981c8e93da4-1420162840650-dave.jpg",
          "imgix_url": "https://cosmic-s3.imgix.net/a499fdab-10b5-5168-9ef1-8981c8e93da4-1420162840650-dave.jpg"
        },
        "official-title": "Groomsman"
      }
    }
  ],
  "total": 5,
  "limit": 3
}
```


Get Objects from an Object Type.



## Search Objects

> Definition

```json
GET https://api.cosmicjs.com/v1/:bucket-slug/object-type/:type-slug/search
```

> Example Request

```bash
curl "https://api.cosmicjs.com/v1/wedding-site/object-type/groomsmen/search?metafield_key=official-title&metafield_value=Best%20Man"
```
```javascript
Cosmic.searchObjectType()
```

> Example Response

```json
{
  "objects": [
    {
      "_id": "55b3da7740d7a3791b000009",
      "bucket": "55b3d557df0fb1df7600004b",
      "slug": "chad-henly",
      "title": "Chad Henly",
      "content": "<p>&nbsp;&nbsp;&nbsp;&nbsp;<br></p>",
      "type_slug": "groomsmen",
      "created": "2015-07-25T18:50:31.820Z",
      "user_id": "55767c3ffbcf5cbb13000001",
      "order": 7,
      "modified": "2015-07-25T18:51:44.249Z",
      "metadata": {
        "image": {
          "url": "https://s3-us-west-2.amazonaws.com/cosmicjs/3181a814-93d9-ad8f-74ce-1eeb64023b61-1420162840289-mke.jpg",
          "imgix_url": "https://cosmic-s3.imgix.net/3181a814-93d9-ad8f-74ce-1eeb64023b61-1420162840289-mke.jpg"
        },
        "official-title": "Best Man"
      }
    }
  ],
  "total": 1
}
```


Search Objects in an Object Type.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
pretty | false | `Enum` | true, Makes the response more reader-friendly
limit | false | `Number` | The number of Objects to return
skip | false | `Number` | The number of Objects to skip
status | false | `Enum` | all, Return published and draft status Objects
read_key | false | `String` | Restrict read access to your Bucket
hide_metafields | false | `Enum` | true, Hides metafields
sort | false | `Enum` | created_at,-created_at,modified_at,<br />-modified_at,random
metafield_key | false | `String` | Metafield key to search for
metafield_value | false | `String` | Exact Metafield value to match
metafield_value_has | false | `String` | Metafield value contains this string
metafield_object_slug | false | `String` | Object Metafield Object slug

## Edit Object

> Definition

```json
PUT https://api.cosmicjs.com/v1/:bucket-slug/edit-object
```

> Example Request Body

```json
{
  "slug": "cosmic-js-example",
  "title": "New Title Edit",
  "content": "This is some rad test content...",
  "metafields": [
    {
      "title": "Headline",
      "key": "headline",
      "value": "Something Big is Coming",
      "type": "text"
    },
    {
      "title": "Subheadline",
      "key": "subheadline",
      "value": "I bet you want to know what it is...",
      "type": "text"
    }
  ]
}
```

> Example Response

```json
{
  "object": {
    "_id": "568c5fb72f0c5d532d000001",
    "slug": "cosmic-js-example",
    "title": "New Title Edit",
    "content": "This is some rad test content...",
    "metafields": [
      {
        "title": "Headline",
        "key": "headline",
        "value": "Something Big is Coming",
        "type": "text"
      },
      {
        "title": "Subheadline",
        "key": "subheadline",
        "value": "I bet you want to know what it is...",
        "type": "text"
      }
    ],
    "bucket": "568c5bbefd0dce302c000001",
    "type_slug": "examples",
    "created": "2016-01-06T00:28:39.982Z"
  }
}
```


Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
type_slug | true | `String` | Add Object to Object Type
title | true | `String` | Your Bucket title
slug | false | `String` | Unique identifier for your Object
content | false | `String` | Add Content to your Object
options.slug_field | false | `Bool` | Set to false to hide the slug field
options.content_editor | false | `Bool` | Set to false to hide the content editor
write_key | false | `String` | Restrict write access to your Bucket
metafields | false | `Array` | Add Metafields to your Object

Edit an existing Object in your Bucket.


## Delete Object

> Definition

```json
DELETE https://api.cosmicjs.com/v1/:bucket-slug/objects/:object-slug
```

> Example Request Body

```json
{
  "write_key": "your-key-added-in-bucket-settings"
}
```

> Example Response

```json
{
  "status": "200",
  "message": "Object deleted"
}
```


Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
write_key | false | `String` | Restrict write access to your Bucket

Edit an existing Object in your Bucket.