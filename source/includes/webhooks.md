# Webhooks

## Add Webhooks

> Definition

```bash
POST https://api.cosmicjs.com/v1/:bucket-slug/webhooks
```

```javascript
Cosmic.addWebhooks()
```

> Example Request

```bash
{
  "event": "object.created.published",
  "endpoint": "http://my-listener.com"
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
    "title": "Object created and published",
    "event": "object.created.published",
    "endpoint": "http://my-listener.com"
  }
}
```


Sends a POST request to the endpoint of your choice when the event occurs.  The data payload in the same fomat as Object and Media.  Read more about Webhooks including the payload sent to the endpoint on the <a href="https://cosmicjs.com/docs/webhooks" target="_blank">Webhooks documentation page</a>.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
event | true | Enum | object.created.draft, object.created.published<br />object.edited.draft, object.edited.published<br />object.deleted, media.created<br />media.edited, media.deleted<br />
endpoint | true | String | The endpoint that will receive the data
write_key | false | String | Your Bucket write key