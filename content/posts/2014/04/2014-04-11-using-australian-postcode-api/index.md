---
title: "Using Australian Postcode API"
date: "2014-04-11"
slug: using-australian-postcode-api
description: ""
author: Justin-Yoo
tags:
- auspost
- australia-post
- rest
- restful
- restful-web-service
fullscreen: false
cover: ""
---

[Australia Post](http://auspost.com.au) provides several APIs for developers to use. You can find the developer centre website [here](http://auspost.com.au/devcentre). In this post, I'm going to introduce how to use [Postage Assessment Calculator and Postcode Search](http://auspost.com.au/devcentre/pacpcs.html).

Basically, postcode search is a part of postage calculation service. You are expected to search only as deep as suburb level. You can't search street names with this. Let's start with registration.

## Registration

In order to use this API, you must have an Auspost account. If you don't have one, you can signup [here](https://id.auspost.com.au/csso/customer/registration?execution=e1s1)[1](#fn-124-1) to create a new account. Once an account is created, the API key can be obtained at [here](https://auspost.com.au/forms/pacpcs-registration.html)[2](#fn-124-2).

![](https://sa0blogs.blob.core.windows.net/justinchronicles/2014/04/auspost.01.png)

As you can see the screenshot above, in order to request the API key, you must use the same email address as the one used for the Auspost account. Once you submit your request, you will receive a confirmation email from Auspost.

![](https://sa0blogs.blob.core.windows.net/justinchronicles/2014/04/auspost.02.png)

Make sure that your API key is as long as 36 characters including 4 hyphens.

## API Consumption

Now, you have received your API key to consume the postcode search API. In case your API key doesn't work, don't worry. You can send a request through [Twitter](http://www.twitter.com/auspost), [Facebook](http://www.facebook.com/australiapost) or [Website](https://auspost.com.au/forms/dev-support.html). They will soon sort out the API authentication issue.

Now, try how the API works through [Fiddler](http://www.telerik.com/fiddler). The API is a [RESTful web service](http://en.wikipedia.org/wiki/Representational_state_transfer). So, we can simply send an HTTP request to the API server and get a response with either JSON or XML format. You can find the technical specification [here](https://auspost.com.au/devcentre/assets/pdfs/pac-pcs-technical-specification.pdf)[3](#fn-124-3).

Within the technical specification document, there are actually two API servers, one for production (_https://auspost.com.au_) and the other for test (_https://test.npe.auspost.com.au_). However, your API key might not be working at the test server. Therefore, just use the production service.

**NOTE**: You might be asked to install Fiddler root certificate as Fiddler needs to decrypt HTTPS requests and responses.

```bat
AUTH-KEY: [YOUR API key of 36 characters length, including hyphens]
```

```bat
Request URL: https://auspost.com.au/api/postcode/search.json?q=3000&state=VIC
```

Put your API key into the header and set the postcode search URL like above. Make sure that your API key must contain hyphens, which is opposed to the technical specification. The document actually states the API key is 32 characters length which omits hyphens. However, this is not correct. **THE HYPHENS MUST BE INCLUDED**. The following screenshots are actual request and response.

![](https://sa0blogs.blob.core.windows.net/justinchronicles/2014/04/auspost.03.png)

![](https://sa0blogs.blob.core.windows.net/justinchronicles/2014/04/auspost.04.png)

As you can see above, the JSON response was returned.

So far, we have briefly looked into the postcode search API provided by Australia Post. It's very convenient for developers to search postcode without storing postcode data locally. Of course, as Australia Post provides the full postcode data regularly, we can download it from the website, store it into our database and use it.

* * *

2. [Auspost ID Registration](https://id.auspost.com.au/csso/customer/registration?execution=e1s1) [↩](#fnref-124-1)

4. [API Key Request](https://auspost.com.au/forms/pacpcs-registration.html) [↩](#fnref-124-2)

6. [Postcode Search Technical Specification](https://auspost.com.au/devcentre/assets/pdfs/pac-pcs-technical-specification.pdf) [↩](#fnref-124-3)
