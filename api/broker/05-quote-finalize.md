# 2C: Finalize Quote

## Overview

Although this API is named **Finalize**, the quote can still be updated later if business rules permit.  
This indicates that the quote is considered **ready on our end**.

## Endpoint Details

| Property | Value |
| --- | --- |
| **Method** | POST |
| **URL** | `{{host}}/api/v1/carma/quote_finalize` |
| **Authentication** | Required - `in-auth-token: {{token}}` |
| **Content-Type** | application/json |

## Key Difference: Update Quote vs Finalize Quote

| Aspect | 2B: Update Quote | 2C: Finalize Quote |
| --- | --- | --- |
| **quote_id in payload** | ✅ Required | ✅ Required |
| **Result** | Updates existing quote | Locks quote (immutable) |
| **Can be called multiple times** | ✅ Yes | ❌ No (one-time action) |
| **Quote data modifiable after** | ✅ Yes | ❌ No |

## Request Payload Structure

### Required Fields

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `quote_id` | String/Number | Yes | The quote ID to finalize (from step 2A or 2B) |
| `finalize` | Number | Yes | Set to `1` to finalize the quote |

### Example Request Body

``` json
{
    "quote_id":"Q000000001015",
    "finalize": 1
}

 ```

## Response Structure

### Success Response (Status: 200)

| Field | Type | Description |
| --- | --- | --- |
| `status` | Number | 0 = Success |
| `txt` | String | Status message (e.g., "Quote finalized successfully") |
| `data` | Object | Finalized quote data |
| `data.quote_id` | String | Same quote ID (now finalized) |
| `data.policy_id` | String | Policy ID associated with the quote |

## Workflow Position

```
┌─────────────────┐
│  2A: New Quote  │  (Creates quote, generates quote_id)
└────────┬────────┘
         ▼
┌─────────────────────┐
│ 2B: Update/Save     │  (Can be called multiple times)
│     Quote           │
└────────┬────────────┘
         ▼
┌─────────────────┐
│ 2C: Finalize    │  ◄── You are here
│     Quote       │      (One-time action, makes quote immutable)
└────────┬────────┘
         ▼
┌─────────────────┐
│ 3A: Assign      │  (Next step: Assign policy)
└─────────────────┘

 ```

## When to Use This Endpoint

| Scenario | Use This Endpoint? |
| --- | --- |
| Quote data is complete and verified | ✅ Yes |
| Ready to proceed to quote assignment | ✅ Yes |
| Need to lock quote to prevent changes | ✅ Yes |
| Still making changes to quote | ❌ No - Use 2B: Update Quote |
| Creating a new quote | ❌ No - Use 2A: New Quote |

## Important Notes

⚠️ **Irreversible Action**: Once a quote is finalized, it cannot be updated or modified. This is a one-way operation.

⚠️ **quote_id Required**: You must include the `quote_id` in the payload to identify which quote to finalize.

⚠️ **Finalize Flag**: The `finalize` parameter must be set to `1` to confirm the finalization action.

⚠️ **Next Step Required**: After finalization, proceed to step 3A (Assign) to complete the policy issuance workflow.

⚠️ **No Updates After**: If changes are needed after finalization, you must create a new quote using step 2A.