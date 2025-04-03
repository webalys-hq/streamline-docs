---
title: Quick start guide
excerpt: Learn how to download your first icon using the Streamline API
deprecated: false
hidden: false
metadata:
  robots: index
---
Downloading your first icon using the Streamline API requires just three steps!

* [Step 1. Create a Streamline Account](quick-start-guide#create-a-streamline-account)
* [Step 2. Create a Personal API Key](quick-start-guide#create-a-personal-api-key)
* [Step 3. Start using the API](quick-start-guide#start-using-the-api)

<br />

## Create a Streamline Account

First of all, you'll have to create a Streamline account if you don't have one. If you already have a Streamline account, you can skip to [Step 2](quick-start-guide#create-a-personal-api-key).

To create an account, go to [https://www.streamlinehq.com/?auth=sign-up](https://www.streamlinehq.com/?auth=sign-up) and fill it with your email and password.

## Create a Personal API Key

As we're still in beta, you first have to request access to the Streamline API filling this form: [https://tally.so/r/mBekgN](https://tally.so/r/mBekgN)

Once we approve it, it's time to create your API Key. To do that, just go to Click on Account in the top right corner and then click on Profile, and then click on API Key(Or you can just go to [https://www.streamlinehq.com/profile?tab=api\_keys](https://www.streamlinehq.com/profile?tab=api_keys) ). Once you're on that page, click on the "Generate your API Key" button.

![](https://files.readme.io/9b46fc90ab4d320e039687d579f1d02ccf4abab627a93b9363bfac68dcf9488e-image.png)

<br />

A new modal will appear showing some extra instructions that you need to read carefully and then click on "Generate Key" button.

![](https://files.readme.io/ae52e763cd2a543e117945c09d784a5b5c4d58296d9ca0553db651eb91a71d2d-image.png)

<br />

After that, your API Key will appear, and you'll be able to copy it.

> ❗️ Do not share your API key with others or expose it in the browser or other client-side code.

## Start using the API

Now that you have your API Key, you can start using the API.

To illustrate that, let's use the Global search endpoint to search for 'home' icons:

```node node
const url = 'https://public-api.streamlinehq.com/v1/search/global?productType=icons&query=home';
const options = {
  method: 'GET',
  headers: {
    accept: 'application/json',
    Authorization: PASTE_YOUR_API_KEY_HERE
  }
};

fetch(url, options)
  .then(res => res.json())
  .then(json => console.log(json))
  .catch(err => console.error(err));
```
```shell shell
curl --request GET \
     --url 'https://public-api-staging.streamlinehq.com/search/global?productType=icons' \
     --header 'Authorization: PASTE_YOUR_API_KEY_HERE' \
     --header 'accept: application/json'
```

*Examples for more languages and more parameter details can be seen here:[Global search](doc:globalsearch)*

If you did everything right, you'll get a 200 response with the first page of icon results!

```json 200 OK
{
  "query": "home",
  "results": [
    {
      "hash": "ico_VgC1LXreoNRxANay",
      "name": "Home 2",
      "imagePreviewUrl": "icons/common-icons/home-2-vqpcd601vmikz9f3zzemzd.png/home-2-xuqkrmr56x43m3v6dkbwr",
      "isFree": true,
      "familySlug": "core-line-free",
      "familyName": "Core Line - Free",
      "categorySlug": "common-icons",
      "categoryName": "Common icons",
      "subcategorySlug": "common-icons",
      "subcategoryName": "Common icons"
    },
    {
      "hash": "ico_wEi0Iwv5LpEW0Pxk",
      "name": "Home 1",
      "imagePreviewUrl": "icons/places/home-1-e5zyd25fdm7ihkk8wq9pm.png/home-1-996o8ls1sfnvuxdevf4jt9",
      "isFree": false,
      "familySlug": "cyber-duotone",
      "familyName": "Cyber Duotone",
      "categorySlug": "category",
      "categoryName": "Category",
      "subcategorySlug": "places",
      "subcategoryName": "Places"
    },
    {
      "hash": "ico_S0kd83eAm77fuTuP",
      "name": "Home 2",
      "imagePreviewUrl": "icons/places/home-2-v5aqejpjz4u7eee8a2gu.png/home-2-dqcwi0rikbh77hreu31gvm",
      "isFree": false,
      "familySlug": "cyber-duotone",
      "familyName": "Cyber Duotone",
      "categorySlug": "category",
      "categoryName": "Category",
      "subcategorySlug": "places",
      "subcategoryName": "Places"
    },
    {
      "hash": "ico_1ZgCLpi574tbN7nj",
      "name": "Home 1",
      "imagePreviewUrl": "icons/common-icons/home-1-5l1lx9056ixu7o4fllh31h.png/home-1-5cciq59kiq2wrcwtcu3oh",
      "isFree": true,
      "familySlug": "core-line-free",
      "familyName": "Core Line - Free",
      "categorySlug": "common-icons",
      "categoryName": "Common icons",
      "subcategorySlug": "common-icons",
      "subcategoryName": "Common icons"
    },
   [...more results will appear here]
  ],
  "pagination": {
    "total": 1350,
    "hasMore": true,
    "offset": 0,
    "nextSkip": 50
  }
}
```

From here, we can get the icon hash property for any of the results and use it in the other available endpoints:

* [Download icon as PNG](doc:downloadiconaspng)
* [Download icon as SVG](doc:downloadiconassvg)
* [Get icon by hash](doc:geticonbyhash)

And that's it! You're now able to integrate our icons into your application!