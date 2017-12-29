# Webhooks

## Add Webhooks

> Definition

```json
POST https://api.cosmicjs.com/v1/:bucket-slug/webhooks
```

> Example Request

```json
{
  "event": "object.created.published",
  "endpoint": "http://my-listener.com"
}
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


Sends a POST request to the endpoint of your choice when the event occurs.  Read more about Webhooks on the <a href="https://cosmicjs.com/docs/webhooks" target="_blank">Webhooks documentation page</a>.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
write_key | false | `String` | Your Bucket write key
event | true | `Enum` | object.created.draft, object.created.published<br />object.edited.draft, object.edited.published<br />object.deleted, media.created<br />media.edited, media.deleted<br />
endpoint | true | `String` | The endpoint that will receive the data