# Extensions

## Add Extension

> Definition

```bash
POST https://api.cosmicjs.com/v1/:bucket_slug/extensions
```

```javascript
bucket.addExtension()
```

> Example Request

```bash
{
  "zip": "your-media-multipart-form-data",
  "write_key": "your-key-added-in-bucket-settings"
}
```

```javascript
const bucket = Cosmic.bucket({
  slug: 'bucket-slug',
  write_key: ''
})
bucket.addExtension({
  zip: '<ZIP_FILE_DATA>'
}).then(data => {
  console.log(data)
}).catch(err => {
  console.log(err)
})
```


> Example Response

```json
{
  "extension": {
    "id": "c62defe0-5f93-11e7-8054-873245f0e98d",
    "title": "Amazon Product Search",
    "image_url": "https://s3-us-west-2.amazonaws.com/cosmicjs/f1f1bd40-5dcd-11e7-b529-51f126a4b6ee-shopping-cart.jpg",
    "url": "http://localhost:3000/extensions/c62defe0-5f93-11e7-8054-873245f0e98d/dist",
    "zip_url": "http://localhost:3000/extensions/c62defe0-5f93-11e7-8054-873245f0e98d/src/build.zip",
    "installed_at": "2017-07-03T02:03:14.825Z",
    "font_awesome_class": "fa-shopping-basket"
  }
}
```


Adds an Extension to your Bucket.  The only required post value is `zip` which is the name of your file sent.   Read more about Extensions on the <a href="https://cosmicjs.com/docs/extensions" target="_blank">Extensions documentation page</a>.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
zip | required| File | Media object
write_key | | String | Your Bucket write key


## Delete an Extension

> Definition

```bash
DELETE https://api.cosmicjs.com/v1/:bucket_slug/extensions/:extension_id
```

```javascript
Cosmic.deleteExtension()
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
bucket.deleteExtension({
  id: 'c62defe0-5f93-11e7-8054-873245f0e98d'
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
  "message": "Extension deleted."
}
```


If a write key is enabled on the requested bucket, the parameter `write_key` will need to be present.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
write_key | | String | Your Bucket write key