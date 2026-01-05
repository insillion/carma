# 2B: Update/Save Quote - Update Existing Quote

## Overview

The Update/Save Quote endpoint **updates an existing quote** in the system by passing the `quote_id` in the request payload. Any data changes in the payload will be saved to the corresponding quote. This allows you to modify customer details, coverage selections, or any other quote information after the initial quote has been created.

## Endpoint Details

| Property | Value |
| --- | --- |
| **Method** | `POST` |
| **URL** | `{{host}}/api/v1/carma/quote` |
| **Authentication** | Required - `in-auth-token: {{token}}` |
| **Content-Type** | `application/json` |

---

## Key Difference: New Quote vs Update Quote

| Aspect | 2A: New Quote | 2B: Update Quote |
| --- | --- | --- |
| `quote_id` in payload | ❌ Not included | ✅ **Required** |
| Result | Creates new quote in system | Updates existing quote |
| Returns new IDs | Yes (auto-generated) | No (same IDs retained) |

---

## Request Payload Structure

### Required Identifier

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `quote_id` | String | **Yes** | The quote ID to update (`quote_id`) |

### Updatable Sections

All fields from the original quote can be updated:

## Example Request Body

``` json
{
    "quote_id": "Q000000001015",
    "customer_details": {
        "gnrlinfo_company_name": "Green Valley Cultivation LLC",
        "gnrlinfo_applicant_contact_name": "Jane Doe",
        "email": "jane.doe@gmail.com",
        ...
    },
    "cpi_coverage_details": [
        {
            "cpi_cd_locno": "1",
            "cpi_cd_bdno": "1",
            "cpi_cd_coverages": "Building Value",
            "cpi_cd_cover_opted": "Yes",
            "cpi_cd_suminsured": 500000
        },
        ...
    ],
    ...
}

 ```

---

## Response Structure

### Success Response (Status: 200)

| Field | Type | Description |
| --- | --- | --- |
| `status` | Number | 0 = Success |
| `txt` | String | Status message |
| `data` | Object | Updated quote data with recalculated values |
| `data.quote_id` | String | Same quote ID (unchanged) |
| `data.policy_id` | String | Same policy ID (unchanged) |
| `data.premium_value` | Number | **Recalculated** premium based on changes |
| `data.total_tax` | Number | **Recalculated** taxes/fees |
| `data.total_amount` | String | **Recalculated** total amount |

---

## Workflow Position

```
┌─────────────────┐
│  2A: New Quote  │  (Creates quote, generates quote_id)
└────────┬────────┘
         ▼
┌─────────────────────┐
│ 2B: Update/Save     │  ◄── You are here
│     Quote           │      (Can be called multiple times)
└────────┬────────────┘
         ▼
┌─────────────────┐
│ 2C: Finalize    │
└─────────────────┘

 ```

---

## Common Update Scenarios

### 1\. Update Contact Information

``` json
{
    "quote_id": "Q000000001015",
    "customer_details": {
        "gnrlinfo_applicant_contact_name": "Jane Doe",
        "email": "jane.doe@company.com"
    }
}

 ```

### 2\. Change Coverage Amount

``` json
{
    "quote_id": "Q000000001015",
    "cpi_coverage_details": [
        {
            "cpi_cd_coverages": "Building Value",
            "cpi_cd_cover_opted": "Yes",
            "cpi_cd_suminsured": 500000
        }
    ]
}

 ```

### 3\. Enable Additional Coverage

``` json
{
    "quote_id": "Q000000001015",
    "cpi_coverage_details": [
        {
            "cpi_cd_coverages": "Equipment",
            "cpi_cd_cover_opted": "Yes",
            "cpi_cd_suminsured": 75000
        }
    ]
}

 ```

---

## When to Use This Endpoint

| Scenario | Use This Endpoint? |
| --- | --- |
| Correcting customer information | ✅ Yes |
| Changing coverage selections | ✅ Yes |
| Adjusting sum insured amounts | ✅ Yes |
| Adding/removing locations | ✅ Yes |
| Changing policy start date | ✅ Yes |
| Creating a brand new quote | ❌ No - Use 2A: New Quote |
| Quote already finalized | ❌ No - Cannot update finalized quotes |

---

## Important Notes

⚠️ **quote_id Required:** You must include the `quote_id` in the payload to update an existing quote. Without it, a new quote will be created instead.

⚠️ **Full Payload Required:** Send the complete quote data, not just the changed fields. The API replaces the entire quote with the submitted data.

⚠️ **Premium Recalculation:** Any changes to coverage or operations will trigger automatic premium recalculation in the response.

⚠️ **Multiple Updates:** You can call this endpoint multiple times before finalizing. Each call updates the quote with the latest data.

⚠️ **Finalized Quotes:** Once a quote is finalized (2C), it cannot be updated. Create a new quote if changes are needed.