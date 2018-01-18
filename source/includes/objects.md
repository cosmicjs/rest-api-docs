# Objects

The following endpoints allow you to add, edit and delete Objects in your Bucket.  If you would like to restrict read or write access to your Bucket, you can do so in Your Bucket > Basic Settings.

## Add Object

> Definition

```bash
POST https://api.cosmicjs.com/v1/:bucket_slug/add-object
```

```javascript
bucket.addObject()
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
const params = {
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
const bucket = Cosmic.bucket({
  slug: 'bucket-slug',
  write_key: ''
})
bucket.addObject(params).then(data => {
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
type_slug | required | String | Add Object to Object Type
title | required | String | Your Object title
slug | | String | Unique identifier for your Object
content | | String | Add Content to your Object
options.slug_field | | Bool | Set to false to hide the slug field
options.content_editor | | Bool | Set to false to hide the content editor
metafields | | Array | Add Metafields to your Object. See <a href="#model">Metafields Model</a>.
locale | | String | Add localization to the Object
write_key | | String | Your Bucket write key


## Get Objects

> Definition

```bash
GET https://api.cosmicjs.com/:bucket_slug/objects
```

```javascript
bucket.getObjects()
```

> Example Request

```bash
curl "https://api.cosmicjs.com/v1/wedding-site/objects?pretty=true&hide_metafields=true&limit=2"
```

```javascript
const bucket = Cosmic.bucket({
  slug: 'wedding-site',
  read_key: ''
})
bucket.getObjects({
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
        "footer-text": "Cosmic JS &copy; 2018"
      }
    }
  ]
}
```

Returns all Objects from your Bucket.


Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
limit | | Number | The number of Objects to return
skip | | Number | The number of Objects to skip
status | | Enum | all, Return published and draft status Objects
revision | | String | The revision_id of the Object Revision
hide_metafields | | Enum | true, Hides metafields
sort | | Enum | created_at, -created_at,<br />modified_at, -modified_at,<br />random
locale | | String | Filter by locale
pretty | | Enum | true, Makes the response more reader-friendly
read_key | | String | Your Bucket read key


## Get Object

> Definition

```bash
GET https://api.cosmicjs.com/:bucket_slug/object/:slug
```

```javascript
bucket.getObject()
```

> Example Request

```bash
curl "https://api.cosmicjs.com/v1/wedding-site/object/registry"
```

```javascript
const bucket = Cosmic.bucket({
  slug: 'wedding-site',
  read_key: ''
})
bucket.getObject({
  slug: 'registry'
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
    "_id": "55b3da7740d7a3791b000011",
    "bucket": "55b3d557df0fb1df7600004b",
    "slug": "registry",
    "title": "Registry",
    "content": "<p>Carol and Jack are registered at Pottery Barn, Macy's and Crate and Barrel.</p>",
    "type_slug": "sections",
    "created": "2015-07-25T18:50:31.851Z",
    "metadata": {
      "pottery-barn": "http://www.potterybarn.com",
      "macys": "http://www.macys.com",
      "crate-and-barrel": "http://www.crateandbarrel.com/"
    }
  }
}
```

Returns a single Object from your Bucket.


Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
status | | Enum | all, Return published and draft status Objects
revision | | String | The revision_id of the Object Revision
hide_metafields | | Enum | true, Hides metafields
locale | | String | Filter by locale
pretty | | Enum | true, Makes the response more reader-friendly
read_key | | String | Your Bucket read key

## Get Objects by Type

> Definition

```bash
GET https://api.cosmicjs.com/v1/:bucket_slug/object-type/:type_slug
```

```javascript
bucket.getObjectsByType()
```

> Example Request

```bash
curl "https://api.cosmicjs.com/v1/wedding-site/object-type/groomsmen?limit=3"
```
```javascript
const bucket = Cosmic.bucket({
  slug: 'wedding-site',
  read_key: ''
})
bucket.getObjectsByType({
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
type_slug | | String | The Object Type slug
limit | | Number | The number of Objects to return
skip | | Number | The number of Objects to skip
status | | Enum | all, Return published and draft status Objects
revision | | String | The revision_id of the Object Revision
hide_metafields | | Enum | true, Hides metafields
sort | | Enum | created_at, -created_at,<br />modified_at, -modified_at,<br />random
locale | | String | Filter by locale
pretty | | Enum | true, Makes the response more reader-friendly
read_key | | String | Your Bucket read key

## Search Objects

> Definition

```bash
GET https://api.cosmicjs.com/v1/:bucket_slug/object-type/:type_slug/search
```

```javascript
bucket.searchObjectType()
```

> Example Request

```bash
curl "https://api.cosmicjs.com/v1/wedding-site/object-type/groomsmen/search?metafield_key=official-title&metafield_value=Best%20Man"
```

```javascript
const bucket = Cosmic.bucket({
  slug: 'wedding-site',
  read_key: ''
})
bucket.searchObjectType({
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
type_slug | | String | The Object Type slug
limit | | Number | The number of Objects to return
skip | | Number | The number of Objects to skip
status | | Enum | all, Return published and draft status Objects
hide_metafields | | Enum | true, Hides metafields
sort | | Enum | created_at, -created_at,<br />modified_at, -modified_at,<br />random
metafield_key | | String | Metafield key to search for
metafield_value | | String | Exact Metafield value to match
metafield_value_has | | String | Metafield value contains this string
metafield_object_slug | | String | Object Metafield Object slug
locale | | String | Filter by locale
pretty | | Enum | true, Makes the response more reader-friendly
read_key | | String | Your Bucket read key

## Edit Object

> Definition

```bash
PUT https://api.cosmicjs.com/v1/:bucket_slug/edit-object
```

```javascript
bucket.editObject()
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
const bucket = Cosmic.bucket({
  slug: 'bucket-slug',
  write_key: ''
})
bucket.editObject({
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
slug | required | String | Unique identifier for your Object
type_slug | | String | Object Type
title | | String | Your Bucket title
content | | String | Add Content to your Object
options.slug_field | | Bool | Set to false to hide the slug field
options.content_editor | | Bool | Set to false to hide the content editor
metafields | | Array | Add Metafields to your Object. See <a href="#model">Metafields Model</a>.
locale | | String | Edit Object locale
write_key | | String | Your Bucket write key


## Delete Object

> Definition

```bash
DELETE https://api.cosmicjs.com/v1/:bucket_slug/objects/:object_slug
```

```javascript
bucket.deleteObject()
```

> Example Request

```bash
{
  "write_key": "your-key-added-in-bucket-settings"
}
```

```javascript
const bucket = Cosmic.bucket({
  slug: 'bucket-slug',
  write_key: ''
})
bucket.deleteObject({
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


Delete an existing Object in your Bucket.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
slug | required | String | Unique identifier for your Object
write_key | | String | Your Bucket write key