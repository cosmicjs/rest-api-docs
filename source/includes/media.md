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

<script src="https://embed.runkit.com" data-element-id="runkit-get-media"></script>
<pre class="runkit" id="runkit-get-media">
const Cosmic = require('cosmicjs')
const api = Cosmic()
const bucket = api.bucket({
  slug: 'wedding-site',
  read_key: ''
})
bucket.getMedia({
  folder: 'groomsmen',
  limit: 3
}).then(data => {
  console.log(data)
}).catch(err => {
  console.log(err)
})
</pre>

You can add the `folder` parameter to get Media from a certain folder.

### Imgix
<a href="https://imgix.com/" target="_blank">Imgix</a> is included with every account.  You can use the Imgix suite of image processing tools on the URL provided by the `imgix_url` property value.  Check out the <a href="https://docs.imgix.com/" target="_blank">Imgix documentation</a> for more info.

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


If a write key is enabled on the requested bucket, the parameter `write_key` will need to be present.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
write_key | | String | Your Bucket write key