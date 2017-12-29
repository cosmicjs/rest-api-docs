# Metafields

Metafields can be added to Objects and Object Types via the API. The model matches the Metafields model on API GET requests which includes minimum properties `type`, `title`, `key` and `value`. For text and textarea Metafields, you can also add validation via the `regex` and `regex_message` properties.

As a general rule, you can copy the Metafields response model on GET requests and send it in a request body to add Metafields via the API.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
type | true | `Enum` | text, textarea, html-textarea, <br />select-dropdown, object, objects, <br />file, date, radio-buttons, check-boxes, <br />repeater, parent, markdown
title | true | `String` | Your Bucket title
key | true | `String` | Unique identifier for your Bucket
value | false | `String` | Metafield value
required | false | `Bool` | A value is required
regex | false | `String` | Restrict the value to match a regular expresssion
regex_message | false | `Array` | The message displayed when the value fails the regex
children | false | `Array` | Add nested Metafields
minlength | false | `Number` | Add minlength to `text` or `textarea` Metafields
maxlength | false | `Number` | Add maxlength to `text` or `textarea` Metafields

## Add to Object Type

Add default Metafields to Object Types via the API.

> Definition

```bash
POST https://api.cosmicjs.com/v1/:bucket-slug/add-object-type
```

> Example Request

```json
{
  "title": "Users",
  "singular": "User",
  "slug": "users",
  "metafields": [
    {
      "key": "first_name",
      "title": "First Name",
      "type": "text",
      "value": "",
      "required": true
    },
    {
      "key": "last_name",
      "title": "Last Name",
      "type": "text",
      "value": "",
      "required": true
    },
    {
      "key": "email",
      "title": "Email",
      "type": "text",
      "value": "",
      "regex": "/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/",
      "regex_message": "You must enter a valid email."
    },
    {
      "key": "avatar",
      "title": "Avatar",
      "type": "file",
      "value": ""
    },
    {
      "key": "tagline",
      "title": "Tagline",
      "type": "text",
      "value": ""
    }
  ]
}
```


## Connect Objects

> Definition

```bash
POST https://api.cosmicjs.com/v1/:bucket-slug/add-object
```

> Example Request

```json
{
  "title": "Blog Post Example",
  "type_slug": "blog-posts",
  "content": "This is some amazing blog content...",
  "metafields": [
    {
      "title": "Headline",
      "key": "headline",
      "type": "text",
      "value": "What I Learned Today"
    },
    {
      "title": "Author",
      "key": "author",
      "type": "object",
      "value": "55b3d557df0fb1df7600004b"
    },
    {
      "title": "Categories",
      "key": "categories",
      "type": "objects",
      "value": "55b3d557df0fb1df7600004a,55b3d557df0fb1df7600004e,55b3d557df0fb1df7600004i"
    },
  ]
}
```

You can connect Objects using Single and Mulpile Object Metafields.  For a Single Object Metafield, add the Object ID (`_id`) as the value to connect the Object.  The full Object will be returned on the Metadata response.  For Multiple Object type Metafields, you can add the Object IDs as comma-separated values which will return the full Objects as an Array on the response.

