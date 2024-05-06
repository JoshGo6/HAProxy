# FizzBuzz Cola API Documentation

This API allows you to subscribe to FizzBuzz Cola.

## Introduction
  
The FizzBuzz Cola API allows you to integrate your subscription process to FizzBuzz Cola into your existing API workflow. Add it to your grocery script and let us do the rest!

Prerequisites:

- General knowledge of Python.
- Familiarity with the Python `requests` library.
- General knowledge of JSON format.

## Subscription procedure

What follows are two simple Python scripts using the `requests` library to subscribe to the delivery service:

### Example 1

```python
import requests

# Create endpoint and payload

url = "http://www.example.com/fizzbuzz/api/v1/subscribe"

payload = {
    "address": "587 HAProxy Dr.",
    "delivery_start_date": "05/05/2024",
    "drink_flavor": "strawberry",
    "texts_enabled": "false",
}

# Send POST request and print response
response = requests.post(url, data=payload)
if response.status_code == 200:
    print("You're subscribed!")
elif response.status_code == 500:
    print("The following error occurred: \n", response.json())
else
    break
```

### Example 2

```python
import requests

# Create endpoint and payload

url = "http://www.example.com/fizzbuzz/api/v1/subscribe"

payload = {
    "address": "587 HAProxy Dr.",
    "delivery_start_date": "07/04/2024",
    "drink_flavor": "orange",
    "texts_enabled": "true",
    "texts_phone": "7037879641"
}

# Send POST request and print response
response = requests.post(url, data=payload)
if response.status_code == 200:
    print("You're subscribed!")
elif response.status_code == 500:
    print("The following error occurred: \n", response.json())
else
    break
```

## Optional: Enable SMS reminders

To receive SMS reminders before each delivery, in the `payload` JSON:

- Set `texts_enabled` to `true`
- Include your phone number as the value for `texts_phone`

```python
payload = {
    "address": "587 HAProxy Dr.",
    "delivery_start_date": "05/05/2024",
    "drink_flavor": "strawberry",
    "texts_enabled": "true", 
    "texts_phone": "7037879641"
}
```

## Unsubscribing

To unsubscribe to delivery service, send a delivery date of `01/01/1900` in the payload:

```Python
payload = {
    "address": "587 HAProxy Dr.",
    "delivery_start_date": "01/01/1900",
    "drink_flavor": "strawberry",
    "texts_enabled": "false",
}
```

## Troubleshooting

The most common error is:

```JSON
{ "error_msg": "Bad format in time."}
```
This is caused by `delivery_start_date` not being in `MM/DD/YYYY` format.


## Reference

This reference contains information on the inputs to the API call, as well as possible responses.

### Inputs

- **URL:** `http://www.example.com/fizzbuzz/api/v1/subscribe`
- **Method:** POST
- **Required Fields:**
  - `address` (string): Delivery address
  - `delivery_start_date` (string): Start date for deliveries, in `MM/DD/YYYY` format (but unsubscribes from delivery if set to `01/01/1900`)
  - `drink_flavor` (string): `classic`, `orange`, or `strawberry`
  - `texts_enabled` (bool): `true` to enable SMS reminders, otherwise `false`
- **Optional Fields:**
  - `texts_phone` (string): Phone number for SMS reminders, required if `texts_enabled` is `true`

### Responses

- **Successful Response:** `HTTP 200`, indicating subscription was successful
- **Error Response:** `HTTP 500` with JSON detailing the error
