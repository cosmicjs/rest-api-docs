# Webhooks

## Add Webhooks

> Definition

```bash
POST https://api.cosmicjs.com/v1/:bucket_slug/webhooks
```

```javascript
Cosmic.addWebhooks()
```

> Example Request

```bash
{
  "event": "object.created.published",
  "endpoint": "http://my-listener.com",
  "write_key": "your-key-added-in-bucket-settings"
}
```

```javascript
const Cosmic = require('cosmicjs')({
  bucket: 'bucket-slug',
  write_key: ''
})
Cosmic.addWebhook({
	event: 'object.created.published',
	endpoint: 'http://my-listener.com'
}).then(data => {
  console.log(data)
}).catch(err => {
  console.log(err)
})
```


> Example Response

```json
{
  "webhook": {
	  "id": "e39b2480-f043-11e7-ba08-234e3fae7762",
	  "title": "Object created and published",
	  "event": "object.created.published",
	  "endpoint": "http://my-listener.com"
  }
}
```


Sends a POST request to the endpoint of your choice when the event occurs.  The data payload in the same fomat as Object and Media.  Read more about Webhooks including the payload sent to the endpoint on the <a href="https://cosmicjs.com/docs/webhooks" target="_blank">Webhooks documentation page</a>.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
event | required | Enum | object.created.draft, object.created.published<br />object.edited.draft, object.edited.published<br />object.deleted, media.created<br />media.edited, media.deleted<br />
endpoint | required | String | The endpoint that will receive the data
write_key | | String | Your Bucket write key

## Delete a Webhook

> Definition

```bash
DELETE https://api.cosmicjs.com/v1/:bucket_slug/webhooks/:webhook_id
```

```javascript
Cosmic.deleteWebhook()
```

> Example Request

```bash
{
  "write_key": "your-key-added-in-bucket-settings"
}
```

```javascript
const Cosmic = require('cosmicjs')({
  bucket: 'bucket-slug',
  write_key: ''
})
Cosmic.deleteWebhook({
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
  "message": "Webhook deleted."
}
```

If a write key is enabled on the requested bucket, the variable `write_key` will need to be present in the Body.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
write_key | | String | Your Bucket write key