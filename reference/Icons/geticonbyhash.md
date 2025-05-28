---
title: Get icon by hash
excerpt: Use this endpoint to retrieve detailed information about a specific icon.
api:
  file: public-api-stagingstreamlinehqcom-public-api-docs-json.json
  operationId: getIconByHash
hidden: false
---
If the API token belongs to a user with a (Streamline Pro subscription)\[[https://home.streamlinehq.com/pricing](https://home.streamlinehq.com/pricing)] or license, the response will include the icon’s `svg`.```
```

```Text json
{
	...
	// Other icon properties
	"svg": '<svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="-1.5 -1.5 48 48" height="48" width="48"><path stroke="#000" stroke-linecap="round" stroke-linejoin="round" d="M43.07 43.125H31.465L22.09 22.5l9.375-20.625H43.07M1.93 22.5h20.16" stroke-width="3"/></svg>',
	...
}
```