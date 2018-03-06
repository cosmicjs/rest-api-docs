# Users

## Add User to Bucket

> Definition

```bash
POST https://api.cosmicjs.com/v1/:bucket_slug/users
```

```javascript
bucket.addUser()
```

> Example Request

```bash
{
  "email": "newuser@example.com",
  "role": "editor"
}
```

```javascript
const bucket = Cosmic.bucket({
  slug: 'bucket-slug',
  write_key: ''
})
const params = {
  "email": "newuser@example.com",
  "role": "editor"
}
bucket.addUser(params).then(data => {
  console.log(data)
}).catch(err => {
  console.log(err)
})
```

> Example Response

```json
{
  "status": 200,
  "message": "User added."
}
```

Add a user to your Bucket.  Authentication token is required and must have admin level access.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
email | required | String | The new user's email
role | required | Enum | admin, developer, editor or contributor
write_key |  | String | Include if a write access key has been added to your Bucket