# View Quote

## Overview

This endpoint retrieves the details of a specific insurance policy based on the given quote_id.

## Endpoint Details

| Property | Value |
| --- | --- |
| **Method** | `GET` |
| **URL** | `{{host}}/api/v1/carma/view_quote/quote?quote_id=quote_id`  <br>Example : quote_id- Q000000001015 |
| **Authentication** | Required - `in-auth-token: {{token}}` |
| **Content-Type** | `application/json` |

## Response Structure

### Success Response (Status: 200)

``` json
{
    "status": 0,
    "txt": "",
    "data": {
        "quote_id": "Q000000001015",
        "policy_id": "P000000001015",
        "customer_details": { ... },
        "total_tax": 500,
        "premium_value": 3000,
        "total_amount": "3500.00",
        "source": "API"
    }
}

 ```

## Notes

- Ensure the `quote_id` exists in the system before making the request