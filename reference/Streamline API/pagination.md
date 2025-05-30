---
title: Pagination
deprecated: false
hidden: false
metadata:
  robots: index
---
All endpoints that have a list as a response return 50 objects by default. You can override this by passing the query param of `limit`. The maximum objects per page is 100 at this time. You can specify the starting point by supplying the query param of `offset`.

> For example: a request with `offset=10` and `limit=100`, will return 100 results starting from the asset number 10.

The following objects will be returned in all paginated responses:

```json
"pagination": {  
    "total": 135,  
    "hasMore": true,  
    "offset": 0,
    "nextOffset": 50
  }`
```

To get the next page, you can get the `nextOffset` value from the response and pass it as the `offset` param in the following request.