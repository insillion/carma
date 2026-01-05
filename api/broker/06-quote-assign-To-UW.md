# 06-Quote-Assign-To-UW

## Overview

This endpoint allows the quote to be submitted to an Underwriter (UW) for review, approval, and finalization.

## Endpoint Details

| Property | Value |
| --- | --- |
| **Method** | POST |
| **URL** | `{{host}}/api/v1/carma/assign_to` |
| **Authentication** | Required - `in-auth-token: {{token}}` |
| **Content-Type** | application/json |

## Request Body

The request body should be in JSON format with the following parameter:

| Parameter | Type | Required | Description |
| --- | --- | --- | --- |
| `policy_id` | string/number | Yes | The unique identifier of the policy to be assigned. Use`policy_id` variable. |

### Example Request Body

``` json
{
    "policy_id": "P000000001015"
}

 ```

## Response Format

### Success Response (200 OK)

``` json
{
    "status": 0,
    "txt": "",
    "data": "Assigned to G000000000006"
}

 ```

| Field | Type | Description |
| --- | --- | --- |
| `status` | integer | Status code (0 indicates success) |
| `txt` | string | Additional message text (may be empty) |
| `data` | string | Confirmation message with the agent ID the quote was assigned to |

## Notes

- Ensure the quote exists and is in a valid state before attempting assignment
    
- The `policy_id` should be obtained from a previous quote creation or update operation
    
- The response will include the agent identifier (e.g., "G000000000006") to whom the quote was assigned