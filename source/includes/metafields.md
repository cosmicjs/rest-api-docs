# Metafields

## Model

> Example Model

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
      "key": "basic_text",
      "title": "Basic Text",
      "value": "This home is a must see!",
      "required": true
    },
    {
      "type": "html-textarea",
      "key": "extended_text",
      "title": "Extended Text",
      "value": "<p>Some <strong>HTML content</strong> for <em>dramatic</em> effect!</p>"
    },
    {
      "type": "select-dropdown",
      "key": "state",
      "title": "State",
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
      ],
    },
    {
      "type": "object",
      "object_type": "pages",
      "key": "pages",
      "title": "Pages",
      "value": "5a4806974fa85fc8a7000002",
      "object": {
        "_id": "5a4806974fa85fc8a7000002",
        "bucket": "5a45d643bfbf2ea2e390826e",
        "slug": "home-page",
        "title": "Home Page",
        "content": "<h1>Welcome to Cosmic Real Estate!</h1><p>Check out our awesome real estate listings - stored and managed with Cosmic JS and rendered right in your browser.</p>",
        "metafields": [
          {
            "value": "c96fb400-5a1a-11e7-a5ab-a93ac173447a-cover-photo.jpg",
            "key": "header_image",
            "title": "Header Image",
            "type": "file",
            "children": null,
            "url": "https://s3-us-west-2.amazonaws.com/cosmicjs/c96fb400-5a1a-11e7-a5ab-a93ac173447a-cover-photo.jpg",
            "imgix_url": "https://cosmic-s3.imgix.net/c96fb400-5a1a-11e7-a5ab-a93ac173447a-cover-photo.jpg"
          },
          {
            "value": "555-555-5555",
            "key": "phone",
            "title": "Phone",
            "type": "text",
            "children": null
          },
          {
            "value": "1234 REIT Road, New York, NY",
            "key": "address",
            "title": "Address",
            "type": "text",
            "children": null
          },
          {
            "value": "agent@cosmicrealestate.com",
            "key": "email",
            "title": "Email",
            "type": "text",
            "children": null
          }
        ],
        "type_slug": "pages",
        "created": "2017-12-30T21:35:19.815Z",
        "created_at": "2017-12-30T21:35:19.815Z",
        "status": null,
        "metadata": {
          "header_image": {
            "url": "https://s3-us-west-2.amazonaws.com/cosmicjs/c96fb400-5a1a-11e7-a5ab-a93ac173447a-cover-photo.jpg",
            "imgix_url": "https://cosmic-s3.imgix.net/c96fb400-5a1a-11e7-a5ab-a93ac173447a-cover-photo.jpg"
          },
          "phone": "555-555-5555",
          "address": "1234 REIT Road, New York, NY",
          "email": "agent@cosmicrealestate.com"
        }
      }
    },
    {
      "type": "objects",
      "object_type": "listings",
      "key": "other_listings",
      "title": "Other Listings",
      "value": "5a4806974fa85fc8a7000007",
      "objects": [
        {
          "_id": "5a4806974fa85fc8a7000007",
          "bucket": "5a45d643bfbf2ea2e390826e",
          "slug": "single-family-home",
          "title": "Single Family Home",
          "content": "<p><span>Don&#39;t miss this lovely, large family home in the Brook Park Manor neighborhood. Step through the welcoming front door into the soaring open foyer and make yourself at home. Entertaining is a breeze, enjoy gathering in the living-room or family room featuring a wood-burning fireplace and full wet-bar area. Enjoy meals in the eat-in kitchen with 2 story window offering views of your own private forest or gather in the large formal dining-room for special occasions. Storage is no problem with the large walk-in pantry and 1st floor laundry is so convenient. New cook-top and oven make cooking a pleasure. Upstairs boasts an oversized master suite and 3 generous bedrooms. The unique floor-plan is evident in the upstairs hallway. Need even more space? Head to the full finished basement with a game-room and 5th bedroom/office/craft-room(your choice) and 3rd full bath. Above grade windows let in natural light and make it inviting. Make this wonderful home yours with a few cosmetic updates.</span></p>",
          "metafields": [
            {
              "required": true,
              "value": 423900,
              "key": "price",
              "title": "Price",
              "type": "text",
              "children": null
            },
            {
              "required": true,
              "value": "1513 King David Dr",
              "key": "address",
              "title": "Address",
              "type": "text",
              "children": null
            },
            {
              "value": "d5038cc0-560e-11e7-8404-673376a63c89-single_family_home.jpg",
              "key": "profile",
              "title": "Profile",
              "type": "file",
              "children": null,
              "url": "https://s3-us-west-2.amazonaws.com/cosmicjs/d5038cc0-560e-11e7-8404-673376a63c89-single_family_home.jpg",
              "imgix_url": "https://cosmic-s3.imgix.net/d5038cc0-560e-11e7-8404-673376a63c89-single_family_home.jpg"
            }
          ],
          "type_slug": "listings",
          "created": "2017-12-30T21:35:19.823Z",
          "created_at": "2017-12-30T21:35:19.823Z",
          "status": null,
          "metadata": {
            "price": 423900,
            "address": "1513 King David Dr",
            "profile": {
              "url": "https://s3-us-west-2.amazonaws.com/cosmicjs/d5038cc0-560e-11e7-8404-673376a63c89-single_family_home.jpg",
              "imgix_url": "https://cosmic-s3.imgix.net/d5038cc0-560e-11e7-8404-673376a63c89-single_family_home.jpg"
            },
            "style": "House",
            "beds": 4,
            "baths": 3,
            "square_feet": "",
            "neighborhood": "Brook Park Manor",
            "upvotes": 1
          }
        }
      ]
    },
    {
      "type": "file",
      "key": "hero",
      "title": "Hero",
      "value": "7d276450-5a95-11e7-b717-653f819d86b5.jpg",
      "url": "https://s3-us-west-2.amazonaws.com/cosmicjs/7d276450-5a95-11e7-b717-653f819d86b5.jpg",
      "imgix_url": "https://cosmic-s3.imgix.net/7d276450-5a95-11e7-b717-653f819d86b5.jpg"
    },
    {
      "type": "date",
      "key": "listing_start_date",
      "title": "Listing Start Date",
      "value": ""
    },
    {
      "type": "radio-buttons",
      "key": "deposit_required",
      "title": "Deposit Required",
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
      "key": "amenities",
      "title": "Amenities",
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
      "key": "testimonials",
      "title": "Testimonials",
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
          "name": "Fiona Apple",
          "quote": "Checks all the boxes"
        },
        {
          "name": "Jon Brion",
          "quote": "Great Acoustics!"
        }
      ]
    }
  ]
}
```

Metafields are powerful components that can be added to extend data for Objects and Object Types.

As a general rule, you can copy the Metafields response model on GET requests and send it in a request body to add Metafields via the API.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
type | true | Enum | text, textarea, html-textarea, <br />select-dropdown, object, objects, <br />file, date, radio-buttons, check-boxes, <br />repeater, parent, markdown
title | true | String | Your Bucket title
key | true | String | Unique identifier for your Bucket
value | false | String | Metafield value
required | false | Bool | A value is required
regex | false | String | Restrict the value to match a regular expresssion
regex_message | false | Array | The message displayed when the value fails the regex
minlength | false | Number | Add minlength to text or textarea Metafields
maxlength | false | Number | Add maxlength to text or textarea Metafields
children | false | Array | Add nested Metafields

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

Reference the <a href="/#model">Metafield model</a> to learn more.

## Add to Object

Add Metafields to Objects via the API.

> Definition

```bash
POST https://api.cosmicjs.com/v1/:bucket-slug/add-object
```

> Example Request

```json
{
  "title": "John Smith",
  "type_slug": "users",
  "metafields": [
    {
      "key": "first_name",
      "title": "First Name",
      "type": "text",
      "value": "John",
      "required": true
    },
    {
      "key": "last_name",
      "title": "Last Name",
      "type": "text",
      "value": "Smith",
      "required": true
    },
    {
      "key": "email",
      "title": "Email",
      "type": "text",
      "value": "john@smithbrothers.com",
      "regex": "/^([a-z0-9_\.-]+)@([\da-z\.-]+)\.([a-z\.]{2,6})$/",
      "regex_message": "You must enter a valid email."
    },
    {
      "key": "avatar",
      "title": "Avatar",
      "type": "file",
      "value": "fe93f530-dcf0-11e6-a2d3-2700818cb522-1.jpg" // file name from media object
    },
    {
      "key": "tagline",
      "title": "Tagline",
      "type": "text",
      "value": "Do or do not, there is no try."
    }
  ]
}
```

Reference the <a href="/#model">Metafield model</a> to learn more.

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

You can connect Objects to create "one to many" and "many to many relationships" using Single and Mulpile Object Metafields.  For a Single Object Metafield, add the Object ID (`_id`) as the value to connect the Object.  The full Object will be returned on the Metadata response.  For Multiple Object type Metafields, you can add the Object IDs as comma-separated values which will return the full Objects as an Array on the response.

