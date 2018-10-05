# Object Types

## Add Object Type

> Definition

```bash
POST https://api.cosmicjs.com/v1/:bucket_slug/add-object-type
```

```javascript
bucket.addObjectType()
```

> Example Request

```bash
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

```javascript
const bucket = Cosmic.bucket({
  slug: 'bucket-slug',
  write_key: ''
})
const params = {
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
bucket.addObjectType(params).then(data => {
  console.log(data)
}).catch(err => {
  console.log(err)
})
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

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
title | required | String | Plural title of your Object Type
slug |  | String | Plural slug of your Object Type
singular |  | String | Singular title of your Object Type
metafields |  | Array | Default Metafields for each Object in this type
pretty |  | Enum | true, Makes the response more reader-friendly
write_key |  | String | Restrict write access to your Bucket

## Get Object Types

> Definition

```bash
GET https://api.cosmicjs.com/v1/:bucket_slug/object-types
```

```javascript
bucket.getObjectTypes()
```

> Example Request

```bash
curl "https://api.cosmicjs.com/v1/wedding-site/object-types"
```

<script src="https://embed.runkit.com"></script>
<pre class="runkit" id="runkit-get-object-types"></pre>
<script>var notebook = RunKit.createNotebook({
    // the parent element for the new notebook
    element: document.getElementById("runkit-get-object-types"),
    // specify the source of the notebook
    source: "const Cosmic = require('cosmicjs')\n\
const api = Cosmic()\n\
const bucket = api.bucket({\n\
  slug: 'simple-blog-website'\n\
})\n\
const data = (await bucket.getObjectTypes()).object_types"
})</script>

Get all Object Types in your Bucket.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
pretty |  | Enum | true, Makes the response more reader-friendly
read_key |  | String | Restrict read access to your Bucket


## Edit Object Type

> Definition

```bash
PUT https://api.cosmicjs.com/v1/:bucket_slug/edit-object-type
```

```javascript
bucket.editObjectType()
  ```

> Example Request

```bash
{
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
    },
    {
      "type": "text",
      "title": "Tagline",
      "key": "tagline",
      "required": true
    }
  ]
}
```


```javascript
const bucket = Cosmic.bucket({
  slug: 'bucket-slug',
  write_key: ''
})
bucket.editObjectType({
  slug: 'posts',
  title: 'New Posts Title'
}).then(data => {
  console.log(data)
}).catch(err => {
  console.log(err)
})
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
      },
      {
        "type": "text",
        "title": "Tagline",
        "key": "tagline",
        "required": true
      }
    ],
    "modified_at": "2017-05-30T02:10:35.373Z",
    "created_at": "2017-05-30T02:06:35.373Z",
    "metadata": null
  }
}
```

Edit an existing Object Type in your Bucket.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
slug | required | String | Plural slug of your Object Type
title |  | String | Plural title of your Object Type
singular |  | String | Singular title of your Object Type
metafields |  | Array | Default Metafields for each Object in this type
write_key |  | String | Restrict write access to your Bucket


## Delete Object Type

> Definition

```bash
DELETE https://api.cosmicjs.com/v1/:bucket_slug/object-types/:type_slug
```

```javascript
bucket.deleteObjectType()
```


> Example Request Body

```bash
{
  "write_key": "your-key-added-in-bucket-settings" // optional
}
```

```javascript
const bucket = Cosmic.bucket({
  slug: 'bucket-slug',
  write_key: ''
})
bucket.deleteObjectType({
  slug: 'posts'
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
  "message": "Object Type deleted."
}
```

Delete an existing Object Type from your Bucket.  * This does not delete Objects in this Object Type.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
write_key |  | String | Restrict write access to your Bucket