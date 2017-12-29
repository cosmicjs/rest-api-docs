# Errors

The Cosmic JS API uses the following error codes:


Error Code | Meaning
---------- | -------
200 | OK -- Everything worked as expected.
400 | Bad Request -- Your request is invalid.
401 | Unauthorized -- Your access key is incorrect.
402 | Payment Required -- Your Bucket needs to be upgraded to continue use.
403 | Forbidden -- You are not allowed to access this content.
404 | Not Found -- The requested resource doesn't exist.
429 | Too Many Requests -- Too many requests hit the API too quickly. We recommend an exponential backoff of your requests.
500 | Internal Server Error -- We had a problem with our server. Try again later.
503 | Service Unavailable -- We're temporarially offline for maintanance. Please try again later.
