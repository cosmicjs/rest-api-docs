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
status | | Enum | draft, published, defaults to published
options.slug_field | | Bool | Set to false to hide the slug field
options.content_editor | | Bool | Set to false to hide the content editor
metafields | | Array | Add Metafields to your Object. See <a href="#model">Metafields Model</a>.
locale | | String | Add localization to the Object
write_key | | String | Your Bucket write key
publish_at | | Number | UNIX millisecond timestamp.  Publish automatically at a later time.


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

<script src="https://embed.runkit.com"></script>
<pre class="runkit" id="runkit-get-objects"></pre>
<script>var notebook = RunKit.createNotebook({
    // the parent element for the new notebook
    element: document.getElementById("runkit-get-objects"),
    // specify the source of the notebook
    source: "const Cosmic = require('cosmicjs')\n\
const api = Cosmic()\n\
const bucket = api.bucket({\n\
  slug: 'wedding-site',\n\
  read_key: ''\n\
})\n\
bucket.getObjects({\n\
  limit: 2\n\
}).then(data => {\n\
  console.log(data)\n\
}).catch(err => {\n\
  console.log(err)\n\
})"
})</script>

Returns all Objects from your Bucket.


Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
limit | | Number | The number of Objects to return
skip | | Number | The number of Objects to skip
status | | Enum | all, Return published and draft status Objects
hide_metafields | | Enum | true, Hides metafields
sort | | Enum | created_at, -created_at,<br />modified_at, -modified_at,<br />random
locale | | String | Filter by locale
filters[_id] | | String | Filter by Object IDs (comma separated for multiple)
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

<script src="https://embed.runkit.com"></script>
<pre class="runkit" id="runkit-get-object"></pre>
<script>var notebook = RunKit.createNotebook({
    // the parent element for the new notebook
    element: document.getElementById("runkit-get-object"),
    // specify the source of the notebook
    source: "const Cosmic = require('cosmicjs')\n\
const api = Cosmic()\n\
const bucket = api.bucket({\n\
  slug: 'wedding-site',\n\
  read_key: ''\n\
})\n\
bucket.getObject({\n\
  slug: 'registry'\n\
}).then(data => {\n\
  console.log(data)\n\
}).catch(err => {\n\
  console.log(err)\n\
})"
})</script>

Returns a single Object from your Bucket.


Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
slug | required | String | Unique identifier for your Object
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

<script src="https://embed.runkit.com"></script>
<pre class="runkit" id="runkit-get-objects-by-type"></pre>
<script>var notebook = RunKit.createNotebook({
    // the parent element for the new notebook
    element: document.getElementById("runkit-get-objects-by-type"),
    // specify the source of the notebook
    source: "const Cosmic = require('cosmicjs')\n\
const api = Cosmic()\n\
const bucket = api.bucket({\n\
  slug: 'wedding-site',\n\
  read_key: ''\n\
})\n\
bucket.getObjectsByType({\n\
  type_slug: 'groomsmen',\n\
  limit: 3\n\
}).then(data => {\n\
  console.log(data)\n\
}).catch(err => {\n\
  console.log(err)\n\
})"
})</script>


Get Objects from an Object Type.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
type_slug | required | String | The Object Type slug
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

<script src="https://embed.runkit.com"></script>
<pre class="runkit" id="runkit-search-object-type"></pre>
<script>var notebook = RunKit.createNotebook({
    // the parent element for the new notebook
    element: document.getElementById("runkit-search-object-type"),
    // specify the source of the notebook
    source: "const Cosmic = require('cosmicjs')\n\
const api = Cosmic()\n\
const bucket = api.bucket({\n\
  slug: 'wedding-site',\n\
  read_key: ''\n\
})\n\
bucket.searchObjectType({\n\
  type_slug: 'groomsmen',\n\
  metafield_key: 'official-title',\n\
  metafield_value: 'Best Man'\n\
}).then(data => {\n\
  console.log(data)\n\
}).catch(err => {\n\
  console.log(err)\n\
})"
})</script>


Search Objects in an Object Type.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
type_slug | | String | The Object Type slug
limit | | Number | The number of Objects to return
skip | | Number | The number of Objects to skip
status | | Enum | all, Return published and draft status Objects
hide_metafields | | Enum | true, Hides metafields
sort | | Enum | created_at, -created_at,<br />modified_at, -modified_at,<br />random
q | | String | Searches title and content properties for this string
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
status | | Enum | draft, published, defaults to published
options.slug_field | | Bool | Set to false to hide the slug field
options.content_editor | | Bool | Set to false to hide the content editor
metafields | | Array | Add Metafields to your Object. See <a href="#model">Metafields Model</a>.
locale | | String | Edit Object locale
write_key | | String | Your Bucket write key
publish_at | | Number | UNIX millisecond timestamp. Publish automatically at a later time.


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