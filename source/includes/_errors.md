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
429 | Too Many Requests -- Too many requests hit the API too quickly.
500, 502, 503, 504 | Internal Server Error -- Something went wrong on our end.
