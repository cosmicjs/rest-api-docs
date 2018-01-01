# Objects

The following endpoints allow you to add, edit and delete Objects in your Bucket.  If you would like to restrict read or write access to your Bucket, you can do so in Your Bucket > Basic Settings.

## Add Object

> Definition

```bash
POST https://api.cosmicjs.com/v1/:bucket-slug/add-object
```

```javascript
api.addObject()
```

> Example Request

```bash
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

```javascript
const Cosmic = require('cosmicjs')
const api = Cosmic.config({
  bucket: 'bucket-slug',
  write_key: ''
})
api.addObject({
  type_slug: 'posts',
  title: 'Post Title'
}).then(data => {
  console.log(data)
}).catch(err => {
  console.log(err)
})
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
type_slug | true | String | Add Object to Object Type
title | true | String | Your Object title
slug | false | String | Unique identifier for your Object
content | false | String | Add Content to your Object
options.slug_field | false | Bool | Set to false to hide the slug field
options.content_editor | false | Bool | Set to false to hide the content editor
metafields | false | Array | Add Metafields to your Object
locale | false | String | Add localization to the Object
write_key | false | String | Your Bucket write key


## Get Objects

> Definition

```bash
GET https://api.cosmicjs.com/:bucket-slug/objects
```

```javascript
api.getObjects()
```

> Example Request

```bash
curl "https://api.cosmicjs.com/v1/wedding-site/objects?pretty=true&hide_metafields=true&limit=2"
```

```javascript
const Cosmic = require('cosmicjs')
const api = Cosmic.config({
  bucket: 'wedding-site',
  read_key: ''
})
api.getObjects({
  limit: 2
}).then(data => {
  console.log(data)
}).catch(err => {
  console.log(err)
})
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
      "content": "",
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
      "content": "",
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

Returns all Objects from your Bucket.


Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
limit | false | Number | The number of Objects to return
skip | false | Number | The number of Objects to skip
status | false | Enum | all, Return published and draft status Objects
revision | false | String | The revision_id of the Object Revision
hide_metafields | false | Enum | true, Hides metafields
sort | false | Enum | created_at,-created_at,modified_at,-modified_at,random
locale | false | String | Filter by locale
pretty | false | Enum | true, Makes the response more reader-friendly
read_key | false | String | Your Bucket read key

## Get Objects by Type

> Definition

```bash
GET https://api.cosmicjs.com/v1/:bucket-slug/object-type/:type-slug
```

```javascript
api.getObjectsByType()
```

> Example Request

```bash
curl "https://api.cosmicjs.com/v1/wedding-site/object-type/groomsmen?limit=3"
```
```javascript
const Cosmic = require('cosmicjs')
const api = Cosmic.config({
  bucket: 'wedding-site',
  read_key: ''
})
api.getObjectsByType({
  type_slug: 'groomsmen',
  limit: 3
}).then(data => {
  console.log(data)
}).catch(err => {
  console.log(err)
})
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
    },
    {
      "_id": "55b3da7740d7a3791b00000c",
      "bucket": "55b3d557df0fb1df7600004b",
      "slug": "lance-bergstrom",
      "title": "Lance Bergstrom",
      "content": "<p><br></p>",
      "type_slug": "groomsmen",
      "created": "2015-07-25T18:50:31.823Z",
      "modified": "2015-07-25T18:53:26.148Z",
      "metadata": {
        "image": {
          "url": "https://s3-us-west-2.amazonaws.com/cosmicjs/4c6a5b21-e335-237f-2731-a455d361ddd1-1420162839613-colin.jpg",
          "imgix_url": "https://cosmic-s3.imgix.net/4c6a5b21-e335-237f-2731-a455d361ddd1-1420162839613-colin.jpg"
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

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
limit | false | Number | The number of Objects to return
skip | false | Number | The number of Objects to skip
status | false | Enum | all, Return published and draft status Objects
revision | false | String | The revision_id of the Object Revision
hide_metafields | false | Enum | true, Hides metafields
sort | false | Enum | created_at,-created_at,modified_at,-modified_at,random
locale | false | String | Filter by locale
pretty | false | Enum | true, Makes the response more reader-friendly
read_key | false | String | Your Bucket read key

## Search Objects

> Definition

```bash
GET https://api.cosmicjs.com/v1/:bucket-slug/object-type/:type-slug/search
```

```javascript
api.searchObjectType()
```

> Example Request

```bash
curl "https://api.cosmicjs.com/v1/wedding-site/object-type/groomsmen/search?metafield_key=official-title&metafield_value=Best%20Man"
```

```javascript
const Cosmic = require('cosmicjs')
const api = Cosmic.config({
  bucket: 'wedding-site',
  read_key: ''
})
api.searchObjectType({
  type_slug: 'groomsmen',
  metafield_key: 'official-title',
  metafield_value: 'Best Man'
}).then(data => {
  console.log(data)
}).catch(err => {
  console.log(err)
})
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
pretty | false | Enum | true, Makes the response more reader-friendly
limit | false | Number | The number of Objects to return
skip | false | Number | The number of Objects to skip
status | false | Enum | all, Return published and draft status Objects
hide_metafields | false | Enum | true, Hides metafields
sort | false | Enum | created_at,-created_at,modified_at,<br />-modified_at,random
metafield_key | false | String | Metafield key to search for
metafield_value | false | String | Exact Metafield value to match
metafield_value_has | false | String | Metafield value contains this string
metafield_object_slug | false | String | Object Metafield Object slug
locale | false | String | Filter by locale
read_key | false | String | Your Bucket read key

## Edit Object

> Definition

```bash
PUT https://api.cosmicjs.com/v1/:bucket-slug/edit-object
```

```javascript
api.editObject()
```

> Example Request

```bash
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

```javascript
const Cosmic = require('cosmicjs')
const api = Cosmic.config({
  bucket: 'bucket-slug',
  write_key: ''
})
api.editObject({
  slug: 'cosmic-js-example',
  title: 'New Title Edit'
}).then(data => {
  console.log(data)
}).catch(err => {
  console.log(err)
})
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

Edit an existing Object in your Bucket.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
type_slug | true | String | Add Object to Object Type
title | true | String | Your Bucket title
slug | false | String | Unique identifier for your Object
content | false | String | Add Content to your Object
options.slug_field | false | Bool | Set to false to hide the slug field
options.content_editor | false | Bool | Set to false to hide the content editor
metafields | false | Array | Add Metafields to your Object
locale | false | String | Edit Object locale
write_key | false | String | Your Bucket write key


## Delete Object

> Definition

```bash
DELETE https://api.cosmicjs.com/v1/:bucket-slug/objects/:object-slug
```

```javascript
api.deleteObject()
```

> Example Request

```bash
{
  "write_key": "your-key-added-in-bucket-settings"
}
```

```javascript
const Cosmic = require('cosmicjs')
const api = Cosmic.config({
  bucket: 'bucket-slug',
  write_key: ''
})
api.deleteObject({
  slug: 'cosmic-js-example'
}).then(data => {
  console.log(data)
}).catch(err => {
  console.log(err)
})
```

> Example Response

```json
{
  "status": "200",
  "message": "Object deleted"
}
```


Edit an existing Object in your Bucket.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
write_key | false | String | Your Bucket write key