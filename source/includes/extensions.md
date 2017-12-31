# Extensions

## Add Extension

> Definition

```json
POST https://api.cosmicjs.com/v1/:bucket-slug/extensions
```

> Example Request

```json
{
  "zip": "your-media-multipart-form-data"
}
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


Adds an Extension to your Bucket.  Read more about Extensions on the <a href="https://cosmicjs.com/docs/extensions" target="_blank">Extensions documentation page</a>.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
zip | true | File | Media object
write_key | false | String | Your Bucket write key


## Delete an Extension

> Definition

```json
DELETE https://api.cosmicjs.com/v1/:bucket-slug/extensions/:extension_id
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
  "message": "Extension deleted."
}
```


Required post values include media which is the name of your media sent. If a write key is enabled on the requested bucket, the variable `write_key` will need to be present in the Body. You can also add an optional folder param to add the Media to a specific folder.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
write_key | false | String | Your Bucket write key