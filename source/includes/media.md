# Media

## Add Media

> Definition

```bash
POST https://api.cosmicjs.com/v1/:bucket_slug/media
```

```javascript
bucket.addMedia()
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
const bucket = Cosmic.bucket({
  slug: 'bucket-slug',
  write_key: ''
})
bucket.addMedia({
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


The only required post value is `media` which is the name of your media sent. You can also add an optional `folder` and `metadata` params.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
media | required | File | Media object
folder | | String | Media folder slug
metadata | | Object | Key / value data store
write_key | | String | Your Bucket write key


## Get Media

> Definition

```bash
GET https://api.cosmicjs.com/v1/:bucket_slug/media
```

```javascript
Cosmic.getMedia()
```

> Example Request

```bash
curl "https://api.cosmicjs.com/v1/wedding-site/media?pretty=true&folder=groomsmen&limit=3"
```

```javascript
const bucket = Cosmic.bucket({
  slug: 'wedding-site',
  write_key: ''
})
bucket.getMedia({
  folder: 'groomsmen',
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
  "media": [
    {
      "_id": "55b3da7940d7a3791b00001f",
      "name": "069b9650-32fe-11e5-9f75-cb9b4016a019.jpg",
      "original_name": "mke.jpg",
      "size": 30353,
      "type": "image/jpeg",
      "bucket": "55b3d557df0fb1df7600004b",
      "created": "2015-01-02T01:40:40.903Z",
      "folder": "groomsmen",
      "location": "https://s3-us-west-2.amazonaws.com/cosmicjs",
      "url": "https://s3-us-west-2.amazonaws.com/cosmicjs/069b9650-32fe-11e5-9f75-cb9b4016a019.jpg",
      "imgix_url": "https://cosmic-s3.imgix.net/069b9650-32fe-11e5-9f75-cb9b4016a019.jpg"
    },
    {
      "_id": "55b3da7940d7a3791b00001e",
      "name": "069b6f44-32fe-11e5-9f75-cb9b4016a019.jpg",
      "original_name": "dave.jpg",
      "size": 21110,
      "type": "image/jpeg",
      "bucket": "55b3d557df0fb1df7600004b",
      "created": "2015-01-02T01:40:40.814Z",
      "folder": "groomsmen",
      "location": "https://s3-us-west-2.amazonaws.com/cosmicjs",
      "url": "https://s3-us-west-2.amazonaws.com/cosmicjs/069b6f44-32fe-11e5-9f75-cb9b4016a019.jpg",
      "imgix_url": "https://cosmic-s3.imgix.net/069b6f44-32fe-11e5-9f75-cb9b4016a019.jpg"
    },
    {
      "_id": "55b3da7840d7a3791b00001d",
      "name": "069b6f43-32fe-11e5-9f75-cb9b4016a019.jpg",
      "original_name": "selden.jpg",
      "size": 26217,
      "type": "image/jpeg",
      "bucket": "55b3d557df0fb1df7600004b",
      "created": "2015-01-02T01:40:40.655Z",
      "folder": "groomsmen",
      "location": "https://s3-us-west-2.amazonaws.com/cosmicjs",
      "url": "https://s3-us-west-2.amazonaws.com/cosmicjs/069b6f43-32fe-11e5-9f75-cb9b4016a019.jpg",
      "imgix_url": "https://cosmic-s3.imgix.net/069b6f43-32fe-11e5-9f75-cb9b4016a019.jpg"
    }
  ]
}
```


You can add `folder` to get Media from a certain folder.  You can use the full Imgix suite of image processing tools on the URL provided by the `imgix_url` property value.  Check out the <a href="https://docs.imgix.com/" target="_blank">Imgix documentation</a> for more info.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
pretty | | File | Media object
folder | | String | Media folder slug
read_key | | String | Your Bucket read key

## Delete Media

> Definition

```bash
DELETE https://api.cosmicjs.com/v1/:bucket_slug/media/:media_id
```

```javascript
Cosmic.deleteMedia()
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
bucket.deleteMedia({
 id: '5a4b18e12fff7ec0e3c13c65'
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


If a write key is enabled on the requested bucket, the variable `write_key` will need to be present.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
write_key | | String | Your Bucket write key