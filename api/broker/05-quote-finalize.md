### API Endpoint: To finalize quote details and refer to UW

Although this API is named **Finalize**, the quote can still be updated later if business rules permit.  
This indicates that the quote is considered **ready on our end**.

#### Request Format

- **Method**: POST
    
- **URL**: `{{base_url}}/api/v1/carma/quote_finalize`
    
- **Content-Type**: application/json
    

#### Sample Request Body

This document outlines the fields present in the quote/policy JSON object, providing a description of each field and its expected data type.

with quote id get the quote details to finalize.


**Example Request Body**:

``` json
   ```json
{
  "quote_id": "string",
  "finalize": 1
}

 ```

#### Response Format

On a successful request, the API will return a JSON response with the following structure:

- `status` (integer): The status of the request (0 indicates success).
    
- `txt` (string): A message related to the status.
    
- `data` (array): An array containing details about the created quote and associated entities, including:
    
    - `policy_id`: Identifier for the policy.
        
    - `product_id`: Identifier for the product.
        
    - `quote_id`: Identifier for the quote.
        
    - `premium_value`: The calculated premium value.
        
    - `quote`: An object containing detailed information about the quote, including customer information, coverage details, and more.
        

**Example Response**:

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



### Notes

Ensure that quote id is passed in request body to avoid get that specific rcord.

The response may contain additional nested objects and arrays that provide comprehensive details about the quote and its associated data.

