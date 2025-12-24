### API Endpoint: View Quote

This endpoint allows the quote to be submitted to an Underwriter (UW) for review, approval, and finalization.

### Request

- **Method**: GET
    
- **URL**: `{{base_url}}/api/v1/carma/assign_to`
    
## Purpose

Assign the finalized quote to an underwriter for review.

---

## Request Schema

| Field | Type | Required | Condition |
|------|------|----------|-----------|
| policy_id | string | Yes | Must be a valid `policy_id` generated after quote finalization |

---

## Request Example

```json
{
  "policy_id": "string"
}

## Success Response

```json
{
  "status": 0,
  "txt": "",
  "data": "Assigned to G000000000006"
}

## Error Response
 **Validation Error**
 ```json
 {
  "status": 400,
  "txt": "string",
  "data": ""
}

**System Error**
```json
{
  "status": 500,
  "txt": "string",
  "data": ""
}
```

### Notes

- Ensure that the `quote_id` parameter is valid to receive the appropriate quote details and assign them to UW.
      
- The structure of the response allows for extensibility, meaning additional fields may be included in future updates.