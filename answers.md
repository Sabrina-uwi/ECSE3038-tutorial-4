# Tutorial 4 – Idempotence Notes

## Task 3: Repeating Requests

### 1. POST /devices

{
  "name": "probe",
  "room": "garage",
  "temp": 21.0,
  "online": true
}

First POST request: 201 Created. number of devices is 5.
Second POST request: 201 Created. number of devices is 6.

Both the requests created a new device successfully. Sending the same POST request twice resulted in two devices with the name `probe`, increasing the total device count from 4 to 6.

### 2. PUT /devices/attic

{
  "name": "attic",
  "room": "loft",
  "temp": 30.5,
  "online": true
}

First PUT request: 200 OK. number of devices is 6.
Second PUT request: 200 OK. number of device is  6.

Both the requests replaced the existing attic device with the same information. The number of devices remained unchanged at 6.

### 3. DELETE /devices/fridge


First DELETE request:  200 OK. number of devices is 5.
Second DELETE request: 404 Not Found. number of devices is 5.

The first request removed the fridge device successfully. The second request returned a 404 because the device had already been deleted. The number of devices remained at 5.

PUT and DELETE are idempotent methods because repeating the same request produces the same final system state as sending it once. Although the second DELETE request returns a 404 status code, the device remains deleted, so the system state does not change. POST is not idempotent because sending the same request twice creates two devices instead of one.