### 02-Premium-Calc ( Optional )

## Overview

The Premium Calculation endpoint calculates insurance premiums for cannabis cultivation businesses based on input data without creating a new quote.

## Endpoint Details

| Property | Value |
| --- | --- |
| **Method** | `POST` |
| **URL** | `{{host}}/api/v1/carma/premium_calc` |
| **Authentication** | Required - `in-auth-token: {{token}}` |
| **Content-Type** | `application/json` |

---

## Request Payload Structure

### 1\. Customer Details (`customer_details`)

Contains applicant/business information.

| Field | Type | Required | Description | Example |
| --- | --- | --- | --- | --- |
| `gnrlinfo_company_name` | String | Yes | Company/DBA name | "Green Valley Cultivation LLC" |
| `gnrlinfo_applicant_contact_name` | String | Yes | Primary contact person | "John Smith" |
| `gnrlinfo_legal_business_name` | String | Yes | Legal registered business name | "Sample Business LLC" |
| `gnrlinfo_mailing_address` | String | Yes | Full mailing address | "123 Main Street, Fairfield, NJ, United States" |
| `email` | String | Yes | Contact email address | "john.smith@gmail.com" |
| `gnrlinfo_fein_number` | String | Yes | Federal Employer Identification Number | "12-3456789" |
| `gnrlinfo_zip_code` | String | Yes | ZIP/Postal code | "07006" |
| `gnrlinfo_phone_number` | String | Yes | Contact phone number | "(505) 489-9222" |

### 2\. Coverage Selection Flags (Root Level)

Indicates which coverage types are being requested.

| Field | Type | Values | Description |
| --- | --- | --- | --- |
| `gnrlinfo_commercial_general_liability` | String | "Yes" / "No" | Commercial General Liability |
| `gnrlinfo_product_liability` | String | "Yes" / "No" | Product Liability |
| `gnrlinfo_commercial_property` | String | "Yes" / "No" | Commercial Property |
| `gnrlinfo_excess_liability` | String | "Yes" / "No" | Excess Liability |

### 3\. Business Information (Root Level)

| Field | Type | Required | Description | Example |
| --- | --- | --- | --- | --- |
| `gnrlinfo_new_venture` | String | Yes | Is this a new business venture? | "Yes" / "No" |
| `gnrlinfo_license_status` | String | Yes | Does business have valid license? | "Yes" / "No" |
| `gnrlinfo_year_established` | String | Yes | Year business was established | "2020" |
| `policy_start_date` | String | Yes | Desired policy start date (MM-DD-YYYY) | "10-30-2025" |
| `gnrlinfo_have_previous_insurance` | String | Yes | Has prior insurance coverage? | "Yes" / "No" |
| `gnrl_info_additional_comments_or_questions` | String | No | Additional notes or questions | "Sample submission..." |

### 4\. Operation Type (Root Level)

Array of location/building operations for liability coverage.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `liability_loc_no` | String | Location number | "1" |
| `liability_buildingno` | String | Building number at location | "1" |
| `optype` | String | Type of cannabis operation | "Cultivator for commercial sale" |
| `op_projected_ny_salesrevenue` | String | Projected next year sales revenue | "800000" |

**Supported Operation Types:**

- Dispensary-retail sales
    
- Dispensary and grow for own use
    
- Dispensary and commercial grow
    
- Cultivator for commercial sale
    
- Cannabis Products Manufacturing w/o solvent
    
- Cannabis Manufacturer - Processor w/solvent
    
- Laboratories/Testing of Product
    
- Distribution-Warehouse NOC
    

### 5\. Cultivator Info (`cultivator_info`)

Required when operation type is **Cultivator for commercial sale**.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `cinfo_loc_no` | String | Location number | "1" |
| `cinfo_build_no` | String | Building number | "1" |
| `gnrlinfo_type_of_growlight` | String | Type of grow lights used | "LED" |
| `gnrlinfo_how_often_growlight_replace` | String | Replacement frequency | "Every 24 months" |
| `gnrlinfo_warrant` | String | Warranty period in years | "2" |

### 6\. Manufacturing Info (`manufacturing_info`)

Required when operation type includes **Cannabis Products Manufacturing w/o solvent** Or **Cannabis Manufacturer - Processor w/solvent**

| Field | Type | Description |
| --- | --- | --- |
| `manfinfo_loc_no` | String | Location number |
| `manfinfo_build_no` | String | Building number |
| `grnl_info_extraction_method` | String | Extraction method used |
| `grnl_info_other_extraction_method` | String | Other extraction method if applicable |
| `gnrl_info_is_closedloop_extraction` | String | Uses closed-loop extraction? |
| `gnrl_info_c1d1room` | String | Has C1D1 compliant room? |
| `gnrl_info_non_extraction_process` | String | Non-extraction processes used |

### 7\. CPI Location Details (`cpi_location_details`)

Array of property locations for Commercial Property Insurance.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `cpi_loc_no` | String | Location number | "1" |
| `cpi_building_no` | String | Building number | "1" |
| `cpi_locwise_optype` | String | Operation type at this location | "Cultivator for commercial sale" |
| `cpi_construction_type` | String | Building construction type | "FRAME" |

**Supported Construction Types:**

- FRAME
    
- JOISTED MASONRY
    
- NON COMBUSTIBLE
    
- MASONRY NON COMBUSTIBLE
    
- FIRE RESISTIVE
    

### 8\. CPI Coverage Details (`cpi_coverage_details`)

Array of coverage options per location/building.

| Field | Type | Description | Example |
| --- | --- | --- | --- |
| `cpi_cd_locno` | String | Location number | "1" |
| `cpi_cd_bdno` | String | Building number | "1" |
| `cpi_cd_coverages` | String | Coverage type name | "Building Value" |
| `cpi_cd_cover_opted` | String | Is coverage selected? | "Yes" / "No" |
| `cpi_cd_suminsured` | Number | Sum insured amount (0 if not opted) | 250000 |

**Supported Coverage Types:** Building Value, Tenants Improvement & Betterments, Business Personal Property, Equipment, Business Income w/ EE, Business Income w/o EE, Finished Stock, Flowering Plants, Goods in Process, Immature Seedings, Living Plant, Loss Payee, Outdoor Sign, Pre-Vegetative Plants, Vegetative Plants, Personal Property Of Others

---

## Response Structure

### Success Response (Status Code: 200)

| Field | Type | Description |
| --- | --- | --- |
| `status` | Number | 0 = Success, Non-zero = Error |
| `txt` | String | Error message (empty on success) |
| `data` | Object | Contains all submitted data plus calculated values |
| `data.premium_value` | Number | **Calculated premium amount** |
| `data.total_tax` | Number | **Total applicable taxes/fees** |

## Important Notes

⚠️ **Prerequisites:** Must authenticate first using the Auth endpoint. Token must be passed in `in-auth-token` header.

⚠️ **Data Validation:**

- All "Yes"/"No" fields are case-sensitive.
    
- Date format must be MM-DD-YYYY.
    
- FEIN format: XX-XXXXXXX.
    
- Sum insured should be 0 (not empty) when coverage is not opted in CPI coverage details.
    
- `If gnrlinfo_commercial_property = "No", then the location and coverage arrays should be empty: "cpi_location_details": [], "cpi_coverage_details": [] or keys with empty values.`
    

**Example Sample Body**

``` json
{
 "customer_details": {
        "gnrlinfo_company_name": "Green Valley Cultivation LLC",
        "gnrlinfo_applicant_contact_name": "John Smith",
        "gnrlinfo_legal_business_name": "Sample Business LLC",
        "gnrlinfo_mailing_address": "123 Main Street, Fairfield, NJ, United States",
        "email": "john.smith@gmail.com",
        "gnrlinfo_fein_number": "12-3456789",
        "gnrlinfo_zip_code": "07006",
        "gnrlinfo_phone_number": "(505) 489-9222"
 },
"gnrlinfo_commercial_general_liability": "Yes",
"gnrlinfo_product_liability": "No",
"gnrlinfo_commercial_property": "Yes",
"gnrlinfo_excess_liability": "Yes",
"gnrlinfo_new_venture": "Yes",
"gnrlinfo_license_status": "Yes",
"gnrlinfo_year_established": "2020",
"policy_start_date": "10-30-2025",
"gnrlinfo_have_previous_insurance": "Yes",
"gnrl_info_additional_comments_or_questions": "Sample submission for API integration testing.",
"operation_type": [
    {
        "liability_loc_no": "1",
        "liability_buildingno": "1",
        "optype": "Cultivator for commercial sale",
        "op_projected_ny_salesrevenue": "800000"
    }
],
 "cultivator_info": [
    {
        "cinfo_loc_no": "1",
        "cinfo_build_no": "1",
        "gnrlinfo_type_of_growlight": "LED",
        "gnrlinfo_how_often_growlight_replace": "Every 24 months",
        "gnrlinfo_warrant": "2"
    }
],
"manufacturing_info": [
    {
        "manfinfo_loc_no": "",
        "manfinfo_build_no": "",
        "grnl_info_extraction_method": "",
        "grnl_info_other_extraction_method": "",
        "gnrl_info_is_closedloop_extraction": "",
        "gnrl_info_c1d1room": "",
        "gnrl_info_non_extraction_process": ""
    }
],
"cpi_location_details": [
    {
        "cpi_loc_no": "1",
        "cpi_building_no": "1",
        "cpi_locwise_optype": "Cultivator for commercial sale",
        "cpi_construction_type": "FRAME"
    }
],
"cpi_coverage_details": [
    {
        "cpi_cd_locno": "1",
        "cpi_cd_bdno": "1",
        "cpi_cd_coverages": "Building Value",
        "cpi_cd_cover_opted": "Yes",
        "cpi_cd_suminsured": 250000
    },
    {
        "cpi_cd_locno": "1",
        "cpi_cd_bdno": "1",
        "cpi_cd_coverages": "Tenants Improvement & Betterments",
        "cpi_cd_cover_opted": "Yes",
        "cpi_cd_suminsured": 50000
    },
    {
        "cpi_cd_locno": "1",
        "cpi_cd_bdno": "1",
        "cpi_cd_coverages": "Business Personal Property",
        "cpi_cd_cover_opted": "No",
        "cpi_cd_suminsured": 0
    },
    {
        "cpi_cd_locno": "1",
        "cpi_cd_bdno": "1",
        "cpi_cd_coverages": "Equipment",
        "cpi_cd_cover_opted": "No",
        "cpi_cd_suminsured": 0
    },
    {
        "cpi_cd_locno": "1",
        "cpi_cd_bdno": "1",
        "cpi_cd_coverages": "Business Income w/ EE",
        "cpi_cd_cover_opted": "No",
        "cpi_cd_suminsured": 0
    },
    {
        "cpi_cd_locno": "1",
        "cpi_cd_bdno": "1",
        "cpi_cd_coverages": "Business Income w/o EE",
        "cpi_cd_cover_opted": "No",
        "cpi_cd_suminsured": 0
    },
    {
        "cpi_cd_locno": "1",
        "cpi_cd_bdno": "1",
        "cpi_cd_coverages": "Finished Stock",
        "cpi_cd_cover_opted": "No",
        "cpi_cd_suminsured": 0
    },        
    {
        "cpi_cd_locno": "1",
        "cpi_cd_bdno": "1",
        "cpi_cd_coverages": "Flowering Plants",
        "cpi_cd_cover_opted": "No",
        "cpi_cd_suminsured": 0
    },
    {
        "cpi_cd_locno": "1",
        "cpi_cd_bdno": "1",
        "cpi_cd_coverages": "Goods in Process",
        "cpi_cd_cover_opted": "No",
        "cpi_cd_suminsured": 0
    },
    {
        "cpi_cd_locno": "1",
        "cpi_cd_bdno": "1",
        "cpi_cd_coverages": "Immature Seedings",
        "cpi_cd_cover_opted": "No",
        "cpi_cd_suminsured": 0
    },
            {
        "cpi_cd_locno": "1",
        "cpi_cd_bdno": "1",
        "cpi_cd_coverages": "Living Plant",
        "cpi_cd_cover_opted": "No",
        "cpi_cd_suminsured": 0
    },
    {
        "cpi_cd_locno": "1",
        "cpi_cd_bdno": "1",
        "cpi_cd_coverages": "Loss Payee",
        "cpi_cd_cover_opted": "No",
        "cpi_cd_suminsured": 0
    },
    {
        "cpi_cd_locno": "1",
        "cpi_cd_bdno": "1",
        "cpi_cd_coverages": "Outdoor Sign",
        "cpi_cd_cover_opted": "No",
        "cpi_cd_suminsured": 0
    },
    {
        "cpi_cd_locno": "1",
        "cpi_cd_bdno": "1",
        "cpi_cd_coverages": "Pre-Vegetative Plants",
        "cpi_cd_cover_opted": "No",
        "cpi_cd_suminsured": 0
    },
    {
        "cpi_cd_locno": "1",
        "cpi_cd_bdno": "1",
        "cpi_cd_coverages": "Vegetative Plants",
        "cpi_cd_cover_opted": "No",
        "cpi_cd_suminsured": 0
    },
    {
        "cpi_cd_locno": "1",
        "cpi_cd_bdno": "1",
        "cpi_cd_coverages": "Personal Property Of Others",
        "cpi_cd_cover_opted": "No",
        "cpi_cd_suminsured": 0
    }
] 
}

 ```