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

<br />

## Create a Streamline Account

First of all, you'll have to create a Streamline account in case you don't have one. If you already have an account, you can skip to [Step 2](quick-start-guide#create-a-personal-api-key).

To create an account, go to [https://www.streamlinehq.com/?auth=sign-up](https://www.streamlinehq.com/?auth=sign-up) and fill it with your email and password.

## Create a Personal API Key

Now that you already have an account, it's time to create your API Key, to do that, just go to [https://www.streamlinehq.com/profile?tab=api\_keys](https://www.streamlinehq.com/profile?tab=api_keys) and then click on the "Generate your secret API Key" a new modal will appear showing some extra instructions that you need to read carefully and then click on "Generate Key" button. After that, you'll see you can copy the API Key. Remember to save it in a safe place, as it'll never be shown again.

## Start using the API

Now that you have your API Key, you can start using the API. To illustrate that, let's use the Global search endpoint to search for 'home' icons:

```node node
const url = 'https://public-api-staging.streamlinehq.com/search/global?productType=icons&query=home';
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

**Examples for more languages and more details can be seen here:[Global search](doc:globalsearch)**

If you did everything right, you'll get a 200 response with your new plan details!