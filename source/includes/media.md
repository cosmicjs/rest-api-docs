# Media

## Add Media

> Definition

```json
POST https://api.cosmicjs.com/v1/:bucket-slug/media
```

> Example Request

```bash
{
  "media": "your-media-multipart-form-data",
  "folder": "your-folder-slug",
  "metadata": {
    "caption": "Beautiful picture of the beach",
    "credit": "Tyler Jackson"
  }
}
```

```javascript
const Cosmic = require('cosmicjs')({
  bucket: 'bucket-slug',
  write_key: ''
})
Cosmic.addMedia({
  media: '<FILE_DATA>',
  folder: 'your-folder-slug',
  metadata: {
    caption: 'Beautiful picture of the beach',
    credit: 'Tyler Jackson'
  }
}).then(data => {
  console.log(data)
}).catch(err => {
  console.log(err)
})
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
    "imgix_url": "https://cosmic-s3.imgix.net/c20391e0-b8a4-11e6-8836-fbdfd6956b31-bird.jpg",
    "metadata": [
      {
        "key": "caption",
        "value": "Beautiful picture of the beach"
      },
      {
        "key": "credit",
        "value": "Tyler Jackson"
      }
    ]
  }
}
```


The only required post value is `media` which is the name of your media sent. If a write key is enabled on the requested bucket, the parameter `write_key` will need to be present in the Body. You can also add an optional `folder` and `metadata` params.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
media | true | File | Media object
folder | false | String | Media folder slug
metadata | false | Object | Key / value data store
write_key | false | String | Your Bucket write key

## Delete Media

> Definition

```json
DELETE https://api.cosmicjs.com/v1/:bucket-slug/media/:media_id
```

> Example Request

```json
{
  "write_key": "your-key-added-in-bucket-settings"
}
```


> Example Response

```json
{
  "status": "200",
  "message": "Object Type deleted."
}
```


Required post values include media which is the name of your media sent. If a write key is enabled on the requested bucket, the variable `write_key` will need to be present in the Body. You can also add an optional folder param to add the Media to a specific folder.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
write_key | false | String | Your Bucket write key