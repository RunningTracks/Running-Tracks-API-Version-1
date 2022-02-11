# Running Tracks Error Codes - API Version 1
Erros within Running tracks consist of two regions where they can be displayed. For some specific endpoints additional information about the error maybe provided in the `data` array. For best practice a majority of errors will exists in the `errors` array.

```javascript
  "error":{
      "reason":"Access Attempt Unauthorized",
      "code":-1
   }
 ```
## Debugging with `system` and `constant`
We provide two additional arrays which contain important information related to your query. You can use the  `system` and `constant` arrays to find more information regarding your errors.

An example of a request without error will look as follows

```
GET https://runningtracks.net/api/v1/map/locations/?x=17&y=30
```

**Response:**
```javascript
{
   "data":[
      {
         "id":89,
         "name":"",
         "time_created":1644399722894,
         "last_updated":1644399722894,
         "status":1,
         "x":17,
         "y":30,
         "lat":71.92010495,
         "lon":-28.49126267,
         "owner":"Available",
         "population":50000,
         "online":0
      }
   ],
   "system":{
      "time":{
         "unix":1644551808,
         "universal":1644551808232,
         "zone":"UTC",
         "query":0.002263,
         "render":1644551808
      },
      "protocol":{
         "version":1,
         "status":200
      },
      "constant":{
         "requested":"\/api\/v1\/map\/locations\/",
         "auth":false,
         "id":"dev.88214runningtracks.net",
         "ip":"<user-ip>"
      },
      "authorization":{
         "success":true
      }
   },
   "errors":[
      
   ]
}
```

## 50xx Internal Errors
Errors which contain 5000 will related specifically to an internal error. When these errors occur there is nothing an end-user (you) can do to fix this. Please report the error and provide all related request information so that we can help find a remedy.

## Help
If you are having issues that you cannot resolve please reach out to us at support@runningtracks.net or via discord or our forum at https://forum.runningtracks.net/


