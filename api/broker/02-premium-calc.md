### API Endpoint: Premium Calc
This endpoint allows users to Calculate premium details based on input data without creating a new quote.

#### Request Format
- **Method**: POST
    
- **URL**: `{{base_url}}/api/v1/carma/premium_calc`
    
- **Content-Type**: application/json
    
#### Headers
- `in-auth-token` (string): An authentication token required for accessing the API.


#### Note: Handling Premium Calc

It's an optional API and it can be used as Standalone to calculate Premium. 


#### Request Body
The request body must be in JSON format and should include the following field:
- `quote_id` (string) (Required): The identifier of the existing quote to be cloned.
    
**Example Request Body**:
``` json
{
  "customer_details": {
    "gnrlinfo_company_name": "string",
    "gnrlinfo_applicant_contact_name": "string",
    "gnrlinfo_legal_business_name": "string",
    "gnrlinfo_mailing_address": "string",
    "email": "string",
    "gnrlinfo_fein_number": "string",
    "gnrlinfo_zip_code": "string",
    "gnrlinfo_phone_number": "string"
  },
  "gnrlinfo_commercial_general_liability": "string",
  "gnrlinfo_product_liability": "string",
  "gnrlinfo_commercial_property": "string",
  "gnrlinfo_excess_liability": "string",
  "gnrlinfo_new_venture": "string",
  "gnrlinfo_license_status": "string",
  "gnrlinfo_year_established": "string",
  "policy_start_date": "DD-MM-YYYY",
  "gnrlinfo_have_previous_insurance": "string",
  "gnrl_info_additional_comments_or_questions": "string",
  "operation_type": [
    {
      "liability_loc_no": "string",
      "liability_buildingno": "string",
      "optype": "string",
      "op_projected_ny_salesrevenue": "number"
    }
  ],
  "cpi_location_details": [
    {
      "cpi_loc_no": "string",
      "cpi_building_no": "string",
      "cpi_locwise_optype": "string",
      "cpi_construction_type": "string"
    }
  ],
  "cpi_coverage_details": [
    {
      "cpi_cd_locno": "string",
      "cpi_cd_bdno": "string",
      "cpi_cd_coverages": "string",
      "cpi_cd_cover_opted": "string",
      "cpi_cd_suminsured": "number"
    }
  ],
  "cultivator_info": [
    {
      "cinfo_loc_no": "string",
      "cinfo_build_no": "string",
      "gnrlinfo_type_of_growlight": "string",
      "gnrlinfo_how_often_growlight_replace": "string",
      "gnrlinfo_warrant": "string"
    }
  ],
  "manufacturing_info": [
    {
      "manfinfo_loc_no": "string",
      "manfinfo_build_no": "string",
      "grnl_info_extraction_method": "string",
      "grnl_info_other_extraction_method": "string",
      "gnrl_info_is_closedloop_extraction": "string",
      "gnrl_info_c1d1room": "string",
      "gnrl_info_non_extraction_process": "string"
    }
  ]
}

```

#### Sample Response Format

On a successful request, the API will return a JSON response with the following structure:

- `status` (integer): The status of the request (0 indicates success).
    
- `txt` (string): A message related to the status.
    
- `data` (array): An array containing details about the created quote and associated entities, including:
    
    - `policy_id`: Identifier for the policy.
        
    - `product_id`: Identifier for the product.
        
    - `quote_id`: Identifier for the quote.
        
    - `premium_value`: The calculated premium value.
        
    - `quote`: An object containing detailed information about the quote, including customer information, coverage details, and more.
        

**Example Response Body**:
``` json
 {
  "status": 0,
  "txt": "",
  "data": {
    "quote_id": "string",
    "policy_id": "string",

    "customer_details": {
      "email": "string",
      "gnrlinfo_company_name": "string",
      "gnrlinfo_applicant_contact_name": "string",
      "gnrlinfo_legal_business_name": "string",
      "gnrlinfo_mailing_address": "string",
      "gnrlinfo_country": "string",
      "gnrlinfo_state": "string",
      "gnrlinfo_city": "string",
      "gnrlinfo_zip_code": "string",
      "gnrlinfo_phone_number": "string",
      "gnrlinfo_fein_number": "string"
    },

    "gnrlinfo_commercial_general_liability": "String",
    "gnrlinfo_product_liability": "String",
    "gnrlinfo_commercial_property": "String",
    "gnrlinfo_excess_liability": "String",

    "gnrlinfo_new_venture": "String",
    "gnrlinfo_license_status": "String",
    "gnrlinfo_year_established": "string",
    "policy_start_date": "DD-MM-YYYY",
    "gnrlinfo_have_previous_insurance": "String",
    "gnrl_info_additional_comments_or_questions": "string",

    "cpi_location_details": [
      {
        "cpi_loc_no": "string",
        "cpi_building_no": "string",
        "cpi_locwise_optype": "string",
        "cpi_construction_type": "string"
      }
    ],

    "cpi_coverage_details": [
      {
        "cpi_cd_locno": "string",
        "cpi_cd_bdno": "string",
        "cpi_cd_coverages": "string",
        "cpi_cd_cover_opted": "String",
        "cpi_cd_suminsured": "number"
      }
    ],

    "operation_type": [
      {
        "liability_loc_no": "string",
        "liability_buildingno": "string",
        "optype": "string",
        "op_projected_ny_salesrevenue": "number"
      }
    ],

    "cultivator_info": [
      {
        "cinfo_loc_no": "string",
        "cinfo_build_no": "string",
        "gnrlinfo_type_of_growlight": "string",
        "gnrlinfo_how_often_growlight_replace": "string",
        "gnrlinfo_warrant": "string"
      }
    ],

    "manufacturing_info": [
      {
        "manfinfo_loc_no": "string",
        "manfinfo_build_no": "string",
        "grnl_info_extraction_method": "string",
        "grnl_info_other_extraction_method": "string",
        "gnrl_info_is_closedloop_extraction": "string",
        "gnrl_info_c1d1room": "string",
        "gnrl_info_non_extraction_process": "string"
      }
    ],

    "total_tax": "number",
    "premium_value": "number",
    "total_amount": "string",
    "source": "API"
  }
}

```