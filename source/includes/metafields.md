# Metafields

Metafields are powerful components that can be added to Objects and Object Types.  Metafields added to Object Types, will be default for all new Objects in the type.

## Model

> Example Metafields

```json
{
  "metafields": [
    {
      "type": "text",
      "title": "Headline",
      "key": "headline",
      "value": "3030 Palo Alto Blvd.",
      "required": true
    },
    {
      "type": "textarea",
      "title": "Basic Text",
      "key": "basic_text",
      "value": "This home is a must see!",
      "required": true
    },
    {
      "type": "html-textarea",
      "title": "Extended Text",
      "key": "extended_text",
      "value": "<p>Some <strong>HTML content</strong> for <em>dramatic</em> effect!</p>"
    },
    {
      "type": "markdown",
      "title": "Markdown Text",
      "key": "markdown_text",
      "value": "# Hello World!"
    },
    {
      "type": "select-dropdown",
      "title": "State",
      "key": "state",
      "value": "California",
      "options": [
        {
          "key": "CA",
          "value": "California"
        },
        {
          "key": "TX",
          "value": "Texas"
        }
      ]
    },
    {
      "type": "object",
      "title": "Pages",
      "key": "pages",
      "object_type": "pages",
      "value": "5a4806974fa85fc8a7000002"
    },
    {
      "type": "objects",
      "title": "Other Listings",
      "key": "other_listings",
      "object_type": "listings",
      "value": "5a4806974fa85fc8a7000007,5a4806974fa85fc8a7000008"
    },
    {
      "type": "file",
      "title": "Hero",
      "key": "hero",
      "value": "7d276450-5a95-11e7-b717-653f819d86b5.jpg",
      "url": "https://s3-us-west-2.amazonaws.com/cosmicjs/7d276450-5a95-11e7-b717-653f819d86b5.jpg",
      "imgix_url": "https://cosmic-s3.imgix.net/7d276450-5a95-11e7-b717-653f819d86b5.jpg"
    },
    {
      "type": "date",
      "title": "Listing Start Date",
      "key": "listing_start_date",
      "value": ""
    },
    {
      "type": "radio-buttons",
      "title": "Deposit Required",
      "key": "deposit_required",
      "value": "",
      "options": [
        {
          "value": "True"
        },
        {
          "value": "False"
        }
      ]
    },
    {
      "type": "check-boxes",
      "title": "Amenities",
      "key": "amenities",
      "value": [
        "Pool",
        "Gym"
      ],
      "options": [
        {
          "value": "Pool"
        },
        {
          "value": "Gym"
        },
        {
          "value": "Landscaping"
        }
      ]
    },
    {
      "type": "repeater",
      "title": "Testimonials",
      "key": "testimonials",
      "value": "Fiona Apple",
      "repeater_fields": [
        {
          "title": "Name",
          "key": "name",
          "value": "",
          "type": "text",
          "required": false
        },
        {
          "title": "Quote",
          "key": "quote",
          "value": "",
          "type": "text",
          "required": false
        }
      ],
      "children": [
        {
          "children": [
            {
              "type": "text",
              "title": "Name",
              "key": "name",
              "value": "Fiona Apple"
            },
            {
              "type": "text",
              "title": "Name",
              "key": "name",
              "value": "Jon Brion"
            }
          ]
        }
      ]
    }
  ]
}
```

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
type | required | Enum | text, textarea, html-textarea, <br />select-dropdown, object, objects, <br />file, date, radio-buttons, check-boxes, <br />repeater, parent, markdown
title | required | String | Your Bucket title
key | required | String | Unique identifier for your Bucket
value | | String | Metafield value
required | | Bool | A value is required
regex | | String | Restrict the value to match a regular expresssion
regex_message | | Array | The message displayed when the value fails the regex
minlength | | Number | Add minlength to text or textarea Metafields
maxlength | | Number | Add maxlength to text or textarea Metafields
children | | Array | Add nested Metafields

## Validation

You can use optional validation parameters to make sure editors on the Web Dashboard enter the correct values.

> Example Metafields with Validations

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
      "required": true,
      "minlength": 2
    },
    {
      "key": "last_name",
      "title": "Last Name",
      "type": "text",
      "value": "",
      "required": true,
      "minlength": 2
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
      "value": "",
      "maxlength": 50
    }
  ]
}
```

Reference the <a href="#model">Metafield model</a> to learn more.

### Optional Validation Parmeters
Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
required | | Bool | A value is required
regex | | String | Restrict the value to match a regular expresssion
regex_message | | Array | The message displayed when the value fails the regex
minlength | | Number | Add minlength to text or textarea Metafields
maxlength | | Number | Add maxlength to text or textarea Metafields


## Connect Objects

> Definition

```bash
POST https://api.cosmicjs.com/v1/:bucket_slug/add-object
```

```javascript
bucket.addObject()
```

> Example Request

```bash
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
      "object_type": "authors",
      "value": "5a4ab6e0cf2289b18a2f7599"
    },
    {
      "title": "Categories",
      "key": "categories",
      "type": "objects",
      "object_type": "categories",
      "value": "5a4ab6e0cf2289b18a2f7599,5a49d524c1174db128ca2bce"
    }
  ]
}
```

```javascript
const params = {
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
      "object_type": "authors",
      "value": "5a4ab6e0cf2289b18a2f7599"
    },
    {
      "title": "Categories",
      "key": "categories",
      "type": "objects",
      "object_type": "categories",
      "value": "5a4ab6e0cf2289b18a2f7599,5a49d524c1174db128ca2bce"
    }
  ]
}
const bucket = Cosmic.bucket({
  bucket: 'bucket-slug',
  write_key: ''
})
bucket.addObject(params).then(data => {
  console.log(data)
}).catch(err => {
  console.log(err)
})
```

You can connect Objects to create "one to many" and "many to many" relationships using Single and Mulpile Object Metafields.  

### Single Objects
For a Single Object Metafield, add the Object ID (`_id`) as the value to connect the Object.  The full Object will be returned on the Metadata response in the `object` property.

### Multiple Objects
For Multiple Object type Metafields, you can add the Object IDs as comma-separated values which will return the full Objects as an Array on the response.  The full Objects will be returned on the Metadata response in the `objects` property.

