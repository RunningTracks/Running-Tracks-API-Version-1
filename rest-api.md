**Table of Contents**

- [Accessibility](#accessibility)
- [General Information](#general-information)
- [HTTP Return Codes](#http-return-codes)
- [Error Codes](#error-codes)
- [General Information on Endpoints](#general-information-on-endpoints)
- System Information
  - [Check Server Time](#check-server-time) (system/timestamp/)
 	- [Ping Test](#ping-test) (system/ping/)
 	- [Online Statistics](#online-statistics) (system/online/)
 	- [XP Levels](#xp-levels) (system/xp-levels/)
- Daily Contests
  - [Ticket Price](#ticket-price) (contests/ticket-price/)
  - [Schedule](#schedule) (contests/schedule/)
  - [Recent Winners](#recent-winners) (contests/recent-winners/)
- Map
  - [Locations](#map-locations) (map/locations/)
  - [Users Online](#users-online) (map/users-online/)
- Inventory
  - [Available Inventory](#available-items) (inventory/available-items/)
  - [Inventory Drops](#inventory-drops) (inventory/inventory-drops/)
- Leaderboards
  - [Leaderboard Segments](#leaderboard-segments) (leaderboards/segments/)  
  - [Leaderboards List](#leaderboards-list) (leaderboards/list/)  

# Public REST API Version 1

## Accessibility
The endpoints listed within this REST API document are considered accessible by the public.

## General Information

* Version 1 of the API is publically available
* All endpoints return a JSON object
* There are currently **`12 endpoints`** as part of version 1.
* Data returned is limited by default to 10 rows and page 1 in descending order (newest first).
* Timestamp fields vary and are labeled to their corresponding contents of **milliseconds** or **time**

## HTTP Return Codes

* HTTP `4XX` return codes are used for malformed requests where the issue exists with the sender.
* HTTP `422` return code is applied when a user input is unexpected.
* HTTP `429` return code is used when breaking a request rate limit.
* HTTP `418` return code is used when an IP has been banned automatically for continuing to send requests after receiving `429` codes.
* HTTP `5XX` return codes are used to show internal errors from the running tracks servers

## Error Codes
* Any endpoint has the ability to return an ERROR array, the following is an example of an invalid endpoint.

```javascript
{
   "data":[
      
   ],
   "system":{
      "time":{
         "unix":1644551410,
         "universal":1644551410660,
         "zone":"UTC"
      },
      "protocol":{
         "version":1,
         "status":401
      },
      "constant":{
         "requested":"\/api\/v1\/xyz\/",
         "auth":false,
         "id":"dev.86802runningtracks.net",
         "ip":"<user-ip>"
      },
      "authorization":{
         "success":false
      }
   },
   "errors":[
      
   ],
   "error":{
      "reason":"Access Attempt Unauthorized"
   }
}   
```

## General Information on Endpoints
* For `POST` endpoints, the parameters must be sent as a `query string` or in the `request body`.
* For `GET` endpoints, parameters must be sent as a `query string`.
* Parameters may be sent in any order.
* If a parameter sent in both the `query string` and `request body`, the `query string` parameter will take priority.

## Check Server Time
Test connectivity to our REST API and get the current server time with a unix timestamp and millisecond timing. 

```
GET https://runningtracks.net/api/v1/system/timestamp/
```

**Parameters:**
None

**Successful Response Payload:**
```javascript
"data":{
      "milliseconds":1644551850251,
      "unix_timestamp":1644551850
},
```

It should be noted that every request provides the user with a unix and universal (millisecond) timing.

```javascript
 "system":{
      "time":{
         "unix":1644551850,
         "universal":1644551850251,
         "zone":"UTC",
         "query":0.001093,
         "render":1644551850
      },
```

## Ping Test
Test the connectivity of the REST API and receive a millisecond timing response

```
GET https://runningtracks.net/api/v1/system/ping/
```

**Parameters:**
None

**Successful Response Payload:**
```javascript
"data":{
      "ms":1644551977823
   },
```


## Online Statistics
Provides information relatinged to users online, total registered, available land in Square Kilometers and the time at which it was last updated.

```
GET https://runningtracks.net/api/v1/system/ping/
```

**Parameters:**
None

**Successful Response Payload:**
```javascript
 "data":{
      "online":990,
      "registered":129029,
      "available_land_sqm":120,
      "last_updated":1644552182163
 },

```


## XP Levels
XP Levels are provided everytime a user passes a set threshold. XP levels are subject to change. A notes array will be provided to keep the user up to date of any changes.

```
GET https://runningtracks.net/api/v1/system/xp-levels/
```

**Parameters:**
None

**Successful Response Payload:**

```javascript
{
  
{
   "data":{
      "levels":{
         "1":{
            "from":0,
            "prize":0
         },
         "2":{
            "from":4040,
            "prize":1
         },
         "3":{
            "from":9180,
            "prize":1
         },
      
```


## Ticket Price
The daily ticket price has a cost associoated, this as of time of writing is related to the `fuel` you collect while active. The price for entry can vary based on market conditions.

The daily contests enable users to win a share of the daily prize pool [daily-prize-pool.md](./daily-prize-pool.md). 

```
GET https://runningtracks.net/api/v1/contests/ticket-price/
```

**Parameters:**
None

**Successful Response Payload:**

```javascript
"data":{
      "pament_methods":[
         {
            "method":"fuel",
            "amount":5000
         },
         {
            "method":"rntr",
            "amount":5
         }
      ],
      "last_revision":1644834944110
   },
```

## Schedule
The schedule defaults to `upcoming` and provides information related to scheduled contests.

```
GET https://runningtracks.net/api/v1/contests/schedule/
```

**Parameters:**
Name | MinLength | Required | Default | Description
------------ | ------------ | ------------ | ------------ | ------------
type | 1 | NO |  | `upcoming` or `past`. Defaults to `upcoming`
from | 1 | NO |  | Provide a unix timestamp to set the list from the time

**Successful Response Payload:**

```javascript
{
   "data":{
      "timezone":"UTC",
      "upcoming":[
         {
            "id":1,
            "timezone":"UTC",
            "time_announced":1644861939010,
            "time_start":1644883200000,
            "time_finish":1644966000000,
            "map_coordinates":"10,17",
            "participants_completed":0,
            "participants_enrolled":18720,
            "completed":0,
            "rewarded":0            
         }
    

```

## Recent Winners
A list of the 100 most recent users to be awarded tokens on the play-to-earn contests.

```
GET https://runningtracks.net/api/v1/contests/recent-winners/
```

**Parameters:**
None

**Successful Response Payload:**

```javascript
{

"data":{
      "timezone":"UTC",
      "recent":[
         {
            "id":1,
            "time_created":1644863856,
            "contest_id":109,
            "uid":1000292,
            "username":"_scoobrunner_",
            "awarded":18.484031,
            "country":"UK",
            "x":18,
            "y":27,
            "contest_runtime":1092
         }
      ]



```

## Map Locations
The endpoint provides a full list of available land with the ability to provide parameters to concentrate on a specific coordinate.
```
GET https://runningtracks.net/api/v1/map/locations/
```

**Parameters:**
Name | MinLength | Required | Default | Description
------------ | ------------ | ------------ | ------------ | ------------
x | 1 | NO |  | Provide the X coordinate, Y coordinate must also be provided
y | 1 | NO |  | Provide the Y coordinate, X coordinate must also be provided

**Successful Response Payload:**

```javascript
{
   "data":[
      {
         "id":195,
         "name":"",
         "time_created":1644400255840,
         "last_updated":1644400255840,
         "status":1,
         "x":13,
         "y":28,
         "lat":71.90210495,
         "lon":-28.52726267,
         "owner":"Available",
         "population":50000,
         "online":0
      },
```

You can request information and statistics relating specifically to a x,y plot by providing the parameters as follows:

```
GET https://runningtracks.net/api/v1/map/locations/?x=17&y=30
```

## Users Online
As part of the effort to be transparent about users on the platform, we provide this end point to provide an indication of where all users are located

```
GET https://runningtracks.net/api/v1/map/users-online/
```

**Parameters:**
Name | MinLength | Required | Default | Description
------------ | ------------ | ------------ | ------------ | ------------
map_x | 1 | NO |  | Provide the X coordinate, Y coordinate must also be provided
map_y | 1 | NO |  | Provide the Y coordinate, X coordinate must also be provided

**Successful Response Payload:**

```javascript
{
   "data":{
      "all":[
         {
            "time_created":1644896791542,
            "last_updated":1644916632961,
            "uid":1000099,
            "username":"<redacted>",
            "speed":0,
            "distance":4500.6953125,
            "map_x":0,
            "map_y":0,
            "land_x":200,
            "land_y":0.01,
            "lat":0.002,
            "lon":0.00204,
            "avgspeed":0.2268,
            "calories":450.07,
            "km_1":0,
            "km_3":0,
            "km_5":0,
            "mps":0,
            "top_speed":7.81875,
            "country":"US"
         },
         {
            "time_created":1644896792004,
            "last_updated":1644916632998,
            "uid":1000429,
            "username":"<redacted>",
            "speed":0,
            "distance":0,
            "map_x":0,
            "map_y":0,
            "land_x":200,
            "land_y":0.01,
            "lat":0.002,
            "lon":0.00204,
            "avgspeed":0,
            "calories":0,
            "km_1":0,
            "km_3":0,
            "km_5":0,
            "mps":0,
            "top_speed":0,
            "country":"US"
         },
         {
            "time_created":1644896792979,
            "last_updated":1644916633014,
            "uid":1000336,
            "username":"<redacted>",
            "speed":0,
            "distance":5262.99609375,
            "map_x":0,
            "map_y":0,
            "land_x":200.30529473,
            "land_y":0.01,
            "lat":0.00200305,
            "lon":0.00181542,
            "avgspeed":0.2653,
            "calories":526.3,
            "km_1":0,
            "km_3":0,
            "km_5":0,
            "mps":0,
            "top_speed":12,
            "country":"US"
         }
      ]
   },
```

## Available Items
A list of all the available inventory from in the game. The Fuel and XP provided by an item is subject to change. The `available_now` provides a rea time look at how many items are currently unclaimed and scattered in the running tracks metaverse.

```
GET https://runningtracks.net/api/v1/inventory/available-items/
```

**Parameters:**
None

**Successful Response Payload:**

```javascript
{
  
 "data":[
      {
         "id":1,
         "icon":"rntr",
         "name":"RNTR Token",
         "description":"",
         "fuel":1,
         "xp":1,
         "available_now":1
      },
      
```

## Inventory Drops
Inventory drops are a constant, where new inventory is released into the metaverse to be collected by players on their travels. Some inventory is more valuable, so it is less frequently dropped. For example, RNTR token is dropped as part of the daily stimulus to be picked up by users as they progress through the universe. Exact coordinates of where the inventory drops on the map are hidden.

```
GET https://runningtracks.net/api/v1/inventory/inventory-drops/
```

**Parameters:**
None

**Successful Response Payload:**

```javascript
{
   "data":[
      {
         "time":1644864224000,
         "land_x":19,
         "land_y":29,
         "type":"apple",
         "amount":20,
         "map_x":"HIDDEN",
         "map_y":"HIDDEN"
      },
      {
         "time":1644864224000,
         "land_x":1,
         "land_y":5,
         "type":"rntr",
         "amount":2,
         "map_x":"HIDDEN",
         "map_y":"HIDDEN"
      },
      {
         "time":1644864224000,
         "land_x":4,
         "land_y":3,
         "type":"apple",
         "amount":30,
         "map_x":"HIDDEN",
         "map_y":"HIDDEN"
      },
      {
         "time":1644864224000,
         "land_x":5,
         "land_y":2,
         "type":"banana",
         "amount":120,
         "map_x":"HIDDEN",
         "map_y":"HIDDEN"
      },
      {
         "time":1644864224000,
         "land_x":5,
         "land_y":5,
         "type":"apple",
         "amount":40,
         "map_x":"HIDDEN",
         "map_y":"HIDDEN"
      },
      {
         "time":1644860220000,
         "land_x":1,
         "land_y":5,
         "type":"rntr",
         "amount":2,
         "map_x":"HIDDEN",
         "map_y":"HIDDEN"
      }
   ],

```

## Leaderboard Segments
List all segments for a specific land. Segments are portions of tracks inside an individual land which are tracked for time trials. You can select between two types of leaderboards that represent the options a user has.

```
GET https://runningtracks.net/api/v1/leaderboards/segments/
```

**Parameters:**
Name | MinLength | Required | Default | Description
------------ | ------------ | ------------ | ------------ | ------------
type | 1 | YES | `hardware` | `hardware` or `controller`
x | 1 | YES |  | Provide the Map X coordinate, Y coordinate must also be provided
y | 1 | YES |  | Provide the Map Y coordinate, X coordinate must also be provided

**Successful Response Payload:**

```javascript
"data":{
      "segments":[
         {
            "segment_id":1,
            "time_created":1644912921000,
            "map_x":2,
            "map_y":18,
            "coordinates":"",
            "hardware_completed":109,
            "controller_completed":20
         }
      ]
   },
```

## Leaderboards List
Leaderboards are a constantly evolving and updating component of running tracks, therefore parameters are required. You must provide the map coordinates of the land you wish to look-up. You can provide an optional `segement_id` for the specific land.

```
GET https://runningtracks.net/api/v1/leaderboards/list/
```

**Parameters:**
Name | MinLength | Required | Default | Description
------------ | ------------ | ------------ | ------------ | ------------
type | 1 | YES | `hardware` | `hardware` or `controller`
x | 1 | YES |  | Provide the Map X coordinate, Y coordinate must also be provided
y | 1 | YES |  | Provide the Map Y coordinate, X coordinate must also be provided
segment_id | 1 | NO |  | Refer to `leaderboards/segments/` to get a list of segment ids for the land


**Successful Response Payload:**

```javascript
{
   "data":{
      "leaderboards":[
         {
            "id":0,
            "time_created":1644912590100,
            "type":"hardware",
            "segment_id":1,
            "map_x":2,
            "map_y":18,
            "uid":1928201,
            "username":"FirghtMight",
            "time_start":1644912000000,
            "time_finish":1644912589000,
            "time_runtime_ms":589000,
            "personal_best":0,
            "contest":0
         }
      ]
   },
```
