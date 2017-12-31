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
curl -X POST https://api.cosmicjs.com/v1/authenticate \
-d email=myname@myservice.com \
-d password=mypassword
```

```javascript
const Cosmic = require('cosmicjs')
Cosmic.authenticate({
  email: 'user@myservice.com',
  password: 'mypassword'
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
  "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXV.eyJlbWFpbCI6InNwaXJvbnlAZ21haWwuY29tIiwicGFzc3dvcmQiOiIxNzlhZDQ1YzZjZTJjYjk3Y2YxMDI5ZTIxMjA0NmU4MSIsImlhdCI6MTUxNDQ5NzI3N30.ep4cEgH_SqItQ5McJArJtljS3GSJedyEcDRlnu9yb-U"
}
```

Send your `email` and `password` to receive your access token. Your access token will be used to add Buckets to your account as well as other account-related access. You do not need to use the token to edit your Bucket. Your Bucket has its own read and write keys for restricted access.  Go to https://cosmicjs.com/signup to create an account.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
email | true | String | Your Cosmic JS login email
password | false | String | Your Cosmic JS login password