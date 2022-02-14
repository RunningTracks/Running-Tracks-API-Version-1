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
- Map
  - [Locations](#map-locations) (map/locations/)
- Inventory
  - [Available Inventory](#available-items) (inventory/available-items/)
  

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
https://runningtracks.net/api/v1/system/xp-levels/
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
https://runningtracks.net/api/v1/contests/ticket-price/
```
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


