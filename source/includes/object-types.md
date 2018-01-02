# Object Types

## Add Object Type

> Definition

```bash
POST https://api.cosmicjs.com/v1/:bucket-slug/add-object-type
```

```javascript
Cosmic.addObjectType()
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
const Cosmic = require('cosmicjs')({
  bucket: 'bucket-slug',
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
Cosmic.addObjectType(params).then(data => {
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
title | true | String | Plural title of your Object Type
slug | false | String | Plural slug of your Object Type
singular | false | String | Singular title of your Object Type
metafields | false | Array | Default Metafields for each Object in this type
pretty | false | Enum | true, Makes the response more reader-friendly
write_key | false | String | Restrict write access to your Bucket

## Get Object Types

> Definition

```bash
GET https://api.cosmicjs.com/v1/:bucket-slug/object-types
```

```javascript
Cosmic.getObjectTypes()
```

> Example Request

```bash
curl "https://api.cosmicjs.com/v1/wedding-site/object-types"
```

```javascript
const Cosmic = require('cosmicjs')({
  bucket: 'wedding-site',
  read_key: ''
})
Cosmic.getObjectTypes().then(data => {
  console.log(data)
}).catch(err => {
  console.log(err)
})
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
          "type": "file",
          "title": "Image",
          "key": "image",
          "value": ""
        },
        {
          "key": "official-title",
          "title": "Official Title",
          "type": "text",
          "value": ""
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
          "type": "file",
          "title": "Image",
          "key": "image",
          "value": ""
        },
        {
          "type": "text",
          "title": "Official Title",
          "key": "",
          "value": ""
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

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
pretty | false | Enum | true, Makes the response more reader-friendly
read_key | false | String | Restrict read access to your Bucket


## Edit Object Type

> Definition

```bash
PUT https://api.cosmicjs.com/v1/:bucket-slug/edit-object-type
```

```javascript
Cosmic.editObjectType()
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
const Cosmic = require('cosmicjs')({
  bucket: 'bucket-slug',
  write_key: ''
})
Cosmic.editObjectType({
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

Edit an exiting Object Type in your Bucket.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
slug | true | String | Plural slug of your Object Type
title | false | String | Plural title of your Object Type
singular | false | String | Singular title of your Object Type
metafields | false | Array | Default Metafields for each Object in this type
write_key | false | String | Restrict write access to your Bucket


## Delete Object Type

> Definition

```bash
DELETE https://api.cosmicjs.com/v1/:bucket-slug/object-types/:object-type-slug
```

```javascript
Cosmic.deleteObjectType()
```


> Example Request Body

```bash
{
  "write_key": "your-key-added-in-bucket-settings" // optional
}
```

```javascript
const Cosmic = require('cosmicjs')({
  bucket: 'bucket-slug',
  write_key: ''
})
Cosmic.deleteObjectType({
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

Delete an exiting Object Type from your Bucket.  * This does not delete Objects in this Object Type.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
write_key | false | String | Restrict write access to your Bucket