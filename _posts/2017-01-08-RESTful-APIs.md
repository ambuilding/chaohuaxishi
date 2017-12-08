---
layout: post
title: RESTful APIs
---

## RESTful API

![HTTP Verbs Represent Actions](https://uploads.toptal.io/blog/image/123414/toptal-blog-image-1498567452740-6773f3fd56484fa794cbf1dbfb9ebb38.png)

- Register

```
curl -X POST http://localhost:8000/api/register \
-H "Accept: application/json" \
-H "Content-Type: application/json" \
-d '{"name": "Andy", "email": "andy@example.com", "password": "andydufresne", "password_confirmation": "andydufresne"}' | python -mjson.tool
```

- Login
  - To send the token in a request, you can do it by sending an attribute api_token in the payload
  - or as a bearer token in the request headers in the form of Authorization: Bearer api_token.



```
curl -X POST localhost:8000/api/login \
-H "Accept: appliation/json" \
-H "Content-type: application/json" \
-d "{\"email\": \"andy@example.com\", \"password\": \"andydufresne\" }" | python -mjson.tool
```

- Tips

```
$ curl http://127.0.0.1:8000/api // api postman -i
$ curl http://… | python -mjson.tool // api
$ alias prettify=“python -mjson.tool”
$ curl -I www.google.com
$ curl "https://www.google.com/search?q=mice"
$ curl -I https://www.facebook.com/
$ curl -I https://31.13.95.36/
```
