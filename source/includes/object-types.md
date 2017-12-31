# Object Types

## Add Object Type

> Definition

```json
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

```json
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

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
pretty | false | Enum | true, Makes the response more reader-friendly
read_key | false | String | Restrict read access to your Bucket


## Edit Object Type

> Definition

```json
PUT https://api.cosmicjs.com/v1/:bucket-slug/edit-object-type
```


> Example Request Body

```json
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

```json
DELETE https://api.cosmicjs.com/v1/:bucket-slug/object-types/:object-type-slug
```


> Example Request Body

```json
{
  "write_key": "your-key-added-in-bucket-settings" // optional
}
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