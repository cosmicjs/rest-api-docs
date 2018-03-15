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
  "media": "your-media-object",
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

const media_object = req.files[0] // Using Multer
// OR:
// const media_object = { originalname: filename, buffer: filedata } // Not using Multer

bucket.addMedia({
  media: media_object,
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

/*
As an example, another popular upload library for express is [express-fileupload](https://www.npmjs.com/package/express-fileupload). File objects obtained through this have the following properties:
req.files.foo.name: "car.jpg"
req.files.foo.mimetype: The mimetype of your file
req.files.foo.data: A buffer representation of your file
*/

// In order to pass the file `req.files.foo` to Cosmic you would do:
const media_object = {
  originalname: req.files.foo.name,
  buffer: req.files.foo.data,
}
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


The only required post value is the `media` object. You can also add optional `folder` and `metadata` params.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
media | required | Media Object (see below) | Media object with specific properties
folder | | String | Media folder slug
metadata | | Object | Key / value data store
write_key | | String | Your Bucket write key

### Media Object
The Media Object must be an object with certain properties indicated below. If using the <a href="https://www.npmjs.com/package/multer" target="blank">multer NPM module</a> the file objects have these by default. Otherwise you should create an object with these properties:


Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
originalname | required | String | The name of your file (something.jpg)
buffer | | File Buffer | The File Buffer


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

<script src="https://embed.runkit.com"></script>
<pre class="runkit" id="runkit-get-media"></pre>
<script>var notebook = RunKit.createNotebook({
    // the parent element for the new notebook
    element: document.getElementById("runkit-get-media"),
    // specify the source of the notebook
    source: "const Cosmic = require('cosmicjs')\n\
const api = Cosmic()\n\
const bucket = api.bucket({\n\
  slug: 'wedding-site',\n\
  read_key: ''\n\
})\n\
bucket.getMedia({\n\
  folder: 'groomsmen',\n\
  limit: 3\n\
}).then(data => {\n\
  console.log(data)\n\
}).catch(err => {\n\
  console.log(err)\n\
})"
})</script>

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
