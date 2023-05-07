---
title: API Reference

language_tabs:
  - javascript

toc_footers:
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Kittn API
---

# Introduction

This is the API for the two sensors. Here you can see all API endpoins. They give information about THe sensors connected to the network and the data tehy recieved.
It is also possible to add and manipulate data.

All examples are provided in JavaScript. You can copy the examples from the right.

This example API documentation page was created with [Slate](https://github.com/slatedocs/slate). Feel free to edit it and use it as a base for your own API's documentation.

# Testing

```javascript
let text = fetch("http://80.208.228.90:8080/auth/test")
    .then((response) => response.text());

```

This endpoint confirms, that the server is online.
The output should contain <code>This is a test response.</code> as plain text message.

# Authentification

## Login

```javascript
fetch("http://80.208.228.90:8080/auth/login?userName=myUserName&password=myPassword")
    .then(response => {
  //TODO
});

```

> Make sure to replace `myUserName` and `myPassword` with your login.

This endpoint logs you in. (Stores cerdentails in cookies).

<aside class="warning">
First you need to login for further use of the API
</aside>


### HTTP Request

`GET http://80.208.228.90:8080/auth/login?userName=<username>&password=<password>`

## Logout

```javascript
fetch("http://80.208.228.90:8080/auth/logout").then((response) => {
  //TODO
});

```

This endpoint logs you out. (Removes cookies).


### HTTP Request

`DELETE http://80.208.228.90:8080/auth/logout`

# Devices

## Get all devices

```javascript
let devices = fetch("http://80.208.228.90:8080/device/list",
    {method: 'GET'})
    .then((response) => response.json());
```

> The above command returns JSON structured like this:

```json
[
    {
        "deviceUUID": "eui-a840417ee185f0b5",
        "deviceName": "LSN50v2-30B",
        "latitude": 47.35004,
        "longitude": 8.719297
    },
    {
        "deviceUUID": "eui-b199191433091337",
        "deviceName": "Filip",
        "latitude": 33.0,
        "longitude": 44.0
    }
]
```

This endpoint retrieves all devices.

### HTTP Request

`GET http://80.208.228.90:8080/device/list`

## Get a specific device

```javascript
let device = fetch("http://80.208.228.90:8080/device/get/eui-a840417ee185f0b5",
    {method: 'POST'})
    .then((response) => response.json());

```

> The above command returns JSON structured like this:

```json
{
        "deviceUUID": "eui-a840417ee185f0b5",
        "deviceName": "LSN50v2-30B",
        "latitude": 47.35004,
        "longitude": 8.719297
}
```

This endpoint retrieves a specific device.

### HTTP Request

`GET http://80.208.228.90:8080/device/get/<UUID>`

### URL Parameters

Parameter | Description
--------- | -----------
deviceUUID | the UUID of the device to retrieve

## insert a new device

```javascript
let data = '{
    "deviceUUID": "TestUUID",
    "deviceName": "TestName",
    "longitude": 10.0,
    "latitude": 10.0
}';
fetch("http://80.208.228.90:8080/device/insert", {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(data)
}).then(response => {
  //TODO
});

```

This endpoint adds a device to the database

### HTTP Request

`POST http://80.208.228.90:8080/device/insert`

### Parameters

Parameter | Description | Restrictions
--------- | ----------- | ------------
deviceUUID | The UUID of the device | 5-36 characters in length
deviceName | The Name of the device | 1-255 characters in length
longitude | The current longitude of the device | between -1000 and 1000
latutude | The current latitude of the device | between -1000 and 1000


## Update a device

```javascript
let data = '
{
    "deviceUUID": "TestUUID",
    "deviceName": "TestName",
    "longitude": 100.0,
    "latitude": 100.0
}';
fetch("http://80.208.228.90:8080/device/update", {
  method: 'PUT',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(data)
}).then(response => {
  //TODO
});

```

This endpoint updates a device with new data.

### HTTP Request

`PUT http://80.208.228.90:8080/device/update`

### Parameters

Parameter | Description | Restrictions
--------- | ----------- | ------------
deviceUUID | The UUID of the device | 5-36 characters in length
deviceName | The Name of the device | 1-255 characters in length
longitude | The current longitude of the device | between -1000 and 1000
latutude | The current latitude of the device | between -1000 and 1000



## Delete a device

```javascript
fetch("http://80.208.228.90:8080/device/delete/TestUUID", {
  method: 'DELETE',
  headers: {
    'Content-Type': 'application/json'
  }})
  .then(response => {
  //TODO
});
```


This endpoint deletes a device.

<aside class="warning">All records of a device will also be deleted</aside>

### HTTP Request

`DELETE http://80.208.228.90:8080/device/delete/<UUID>`

### URL Parameters

Parameter | Description
--------- | -----------
UUID | The ID of the device to delete

# Record

## Get all records

```javascript
let records = fetch("http://80.208.228.90:8080/record/list?time=123", {
  method: 'GET',
  headers: {
    'Content-Type': 'application/json'
  }})
  .then((response) => response.json());

```

> The above command returns JSON structured like this:

```json
[
    {
        "recordUUID": "b97dbf84-5ae4-4b57-9e2c-31cdf7d0f8db",
        "deviceUUID": "eui-a840417ee185f0b5",
        "timestamp": 1683103442000,
        "temperature": 21.5,
        "humidity": 49.3,
        "batteryv": 3.671,
        "device": {
            "deviceUUID": "eui-a840417ee185f0b5",
            "deviceName": "LSN50v2-30B",
            "latitude": 47.35004,
            "longitude": 8.719297
        }
    },
    {
        "recordUUID": "c54efe47-0910-4c8b-b3cd-2e2704c4433b",
        "deviceUUID": "eui-a840417ee185f0b5",
        "timestamp": 1683102242000,
        "temperature": 21.4,
        "humidity": 49.6,
        "batteryv": 3.671,
        "device": {
            "deviceUUID": "eui-a840417ee185f0b5",
            "deviceName": "LSN50v2-30B",
            "latitude": 47.35004,
            "longitude": 8.719297
        }
    }
]
```

This endpoint lists all records.

<aside class="notice">The URL parameter <code>time</code> is optional.</aside>

### HTTP Request

`GET http://80.208.228.90:8080/record/list`

### URL Parameters

Parameter | Description
--------- | -----------
time | how old the data is (days), default 1 day


## Get a specific record

```javascript
let record = fetch("http://80.208.228.90:8080/record/get/383050c4-0cf9-461b-b0d5-136c4d067c83", {
  method: 'GET',
  headers: {
    'Content-Type': 'application/json'
  }})
  .then((response) => response.json());

```

> The above command returns JSON structured like this:

```json
{
    "recordUUID": "383050c4-0cf9-461b-b0d5-136c4d067c83",
    "deviceUUID": "eui-a840417ee185f0b5",
    "timestamp": 1678555294000,
    "temperature": 17.4,
    "humidity": 48.9,
    "batteryv": 3.674,
    "device": {
        "deviceUUID": "eui-a840417ee185f0b5",
        "deviceName": "LSN50v2-30B",
        "latitude": 47.35004,
        "longitude": 8.719297
    }
}
```

This endpoint retrieves a specific record


### HTTP Request

`GET http://80.208.228.90:8080/record/get/<UUID>`

### URL Parameters

Parameter | Description
--------- | -----------
UUID | The UUID of the record

## Insert a new record

```javascript
let data = '{
    "deviceUUID": "TestUUID",
    "timestamp": 123123123,
    "temperature": 123.4,
    "humidity": 55.6,
    "batteryv": 12.3,
    "latitude": 23.4,
    "longitude": 12.5,
    "key": "yourKey"
}';
fetch("http://80.208.228.90:8080/record/insert", {
  method: 'POST',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(data)
}).then(response => {
  //TODO
});

```


This endpoint adds a new record to the database and updates the device position
The endpoint is used by the Sensor to push new data to the server.


<aside class="notice">You do not need to be logged in for this Request.</aside>
<aside class="warning">The parameter <code>key</code> must be you API key.</aside>

### HTTP Request

`POST http://80.208.228.90:8080/record/insert`

### Parameters

Parameter | Description | Restrictions
--------- | ----------- | ------------
deviceUUID | the UUID of the new device, has a default | 5-36 characters in length
timestamp | time of the recording (in ms, UNIX) | not Null
temperature | temperature at the recording | between -1000 and 1000
humidity | humidity at the recording | between -1000 and 1000
batteryv | battery voltage at the recording | between -1000 and 1000
latitude | latitude at this time (Position) | between -1000 and 1000
longitude | longitude at this time (Position) | between -1000 and 1000
key | API key | not Null





## Update a record

```javascript
let data = '{
    "recordUUID": "00285967-d0a0-463c-beb0-db24626591bd",
    "deviceUUID": "TestUUID",
    "timestamp": 1679585108000,
    "temperature": 17,
    "humidity": 47.6,
    "batteryv": 3.639
}';
fetch("http://80.208.228.90:8080/record/update", {
  method: 'PUT',
  headers: {
    'Content-Type': 'application/json'
  },
  body: JSON.stringify(data)
}).then(response => {
  //TODO
});

```


This endpoint updates a record.


### HTTP Request

`PUT http://80.208.228.90:8080/record/update`

### Parameters

Parameter | Description | Restrictions
--------- | ----------- | ------------
deviceUUID | the UUID of the new device, has a default | 5-36 characters in length
timestamp | time of the recording (in ms, UNIX) | not Null
temperature | temperature at the recording | between -1000 and 1000
humidity | humidity at the recording | between -1000 and 1000
batteryv | battery voltage at the recording | between -1000 and 1000


## Delete a record

```javascript
fetch("http://80.208.228.90:8080/record/delete/e7ee4e74-5e24-48dc-b4ce-65f43c7bea18", {
  method: 'DELETE',
  headers: {
    'Content-Type': 'application/json'
  }
}).then(response => {
  //TODO
});

```

This endpoint deletes a record.

### HTTP Request

`DELETE http://80.208.228.90:8080/record/delete/<UUID>`

### URL Parameters

Parameter | Description
--------- | -----------
UUID | UUID if the record
