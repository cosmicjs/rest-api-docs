# Authentication

> Definition

```bash
POST https://api.cosmicjs.com/v1/authenticate
```

```javascript
Cosmic.authenticate()
```

> Example Request

```bash
# With shell, you can just pass your email and password
curl -X POST "https://api.cosmicjs.com/v1/authenticate" \
-d "email=you@youremail.com" \
-d "password=yourpassword"
```

```javascript
const Cosmic = require('cosmicjs')() // double parentheses to init function without token
Cosmic.authenticate({
  email: 'you@youremail.com',
  password: 'yourpassword'
}).then(data => {
	console.log(data)
}).catch(err => {
	console.log(err)
})
```

> Example Response

```json
{
  "success": true,
  "message": "Token created successfully.",
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXV.eyJlbWFpbCI6InNwaXJvbnl..."
}
```

Send your `email` and `password` to receive your access token. Your access token will be used to add Buckets to your account as well as other account-related access. <b>You do not need to use the token to access your Bucket. Your Bucket has its own read and write keys for restricted access</b>.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
email | required | String | Your Cosmic JS login email
password | required | String | Your Cosmic JS login password