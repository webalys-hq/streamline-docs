---
title: Pagination
deprecated: false
hidden: false
metadata:
  robots: index
---
All endpoints that have a list as a response return 50 objects by default. You can override this by passing the query param of `limit`. The maximum objects per page is 100 at this time. You can specify the starting point by supplying the query param of `skip`.

The following objects will be returned in all paginated responses:

```json
"pagination": {  
    "total": 135,  
    "hasMore": true,  
    "offset": 0,
    "nextSkip": 50
  }`
```

To get the next page, you can get the `nextSkip` value from the response and pass it as the `skip` param in the following request.