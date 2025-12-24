### API Endpoint: To update quote details and refer to UW

This endpoint allows users to modify specific information within a client's quote and, because these modifications likely impact the risk assessment, premium the updated quote must then be submitted to an Underwriter (UW) for review, approval, and finalization.

#### Request Format

- **Method**: POST
    
- **URL**: `{{base_url}}/api/v1/carma/quote`
    
- **Content-Type**: application/json
    

#### Sample Request Body

This document outlines the fields present in the quote/policy JSON object, providing a description of each field and its expected data type.

Get quote id from last quote api response.

The request body must be in JSON format and should include the fields as shown on high level:

- `quote_id` (string) (System Generated): The identifier for the quote.
- `customer_first_name` (string): The first name of the customer.
- `customer_last_name` (string): The last name of the customer.
- `customer_email` (string): The email address of the customer.
- `customer_phone` (string): The phone number of the customer.
- `company_name` (string): The name of the company.
- `comapany_address_line1` (string): The first line of the company's address.
- `company_address_line2` (string): The second line of the company's address.
- `company_city` (string): The city of the company's address.
- `company_state` (string): The state of the company's address.
- `company_postal_code` (string): The postal code of the company's address.
- `location_state` (string): The state where the insured property is located.
- `construction_type` (string): The type of construction of the insured property.
- `coverage` (string): The primary type of coverage selected.
- `property_still_under_construction` (string): Indicates if the property is still under construction.
- `watchperson_service_availed` (string): Describes the status of watchperson services for the property.
- `extended_coverage` (string): Indicates if extended coverage is selected.
- `location_city` (string): The city where the insured property is located.
- `location_site_number` (string): The number identifying the location site.

**Example Request Body**:

``` json
   {
    "quote_id": "Q000000000131",
    "customer_first_name": "Rio",
    "customer_last_name": "R",
    "customer_email": "rio@anc.com",
    "customer_phone": "9887989898",
    "company_name": "Rio Company",
    "comapany_address_line1": "r street",
    "company_address_line2": "io post",
    "company_city": "chennai",
    "company_state": "tamilnadu",
    "company_postal_code": "400001",
    "location_state": "New York",
    "coverage": "Contents",
    "property_still_under_construction": "No",
    "watchperson_service_availed": "Central Station",
    "extended_coverage": "Yes",
    "location_city": "Nassau",
     "location_site_number": "3453534",
    "location_site_name": "Rio site",
    "location_address_line1": "Rio add 1",
    "location_address_line2": "Rio add 2",
    "location_county": "Nassau",
    "location_zip": "11204",
    "location_lat_long": "Lat long",
    "commercial_operating_date": "10-11-2025",
    "dc_mw": "DC",
    "ac_mw": "AD",
    "annual_output_mwh": "MWH",
    "mounting_type": "tracker",
    "inverter_make": "IM",
    "module_make": "MM",
    "oandm_provider": "O&M",
    "property_tiv": "TIVP",
    "annual_revenue_tiv": "TIVAR",
    "primary_insurer": "Rio Raj",
    "bi_waiting_period": "BI",
    "notes": "Notes",
    "panel_type": "Ground Mounted",
    "theft": "Excluded",
    "restoration_period_extension_in_days": "30",
    "waiting_period": "11-15 Days",
    "optional_coverage": "Monthly Period of Indemnity",
    "commercial_property": "1500000",
    "business_interruption": "100000",
    "equipment_breakdown_limit": "100000",
    "eb_expediting_expense_sublimit": "50000",
    "insurers_coinsurance": "1",
    "monthly_limitation": "",
    "earthquake_coverage": "Yes",
    "special_perils": "Yes",
    "broad_perils": "Yes",
    "equipment_breakdown": "Yes",
    "flood_coverage": "Yes",
    "all_other_deductible": "5000",
    "earthquake_deductible": "0.1",
    "flood_deductible": "0.1",
    "business_interruption_deductible_in_days": "30",
    "equipment_breakdown_deductible_in_dollars": "75000",
    "soft_cost__extra_expense_deductible": "10",
    "percent_exposure": "1",
    "__finalize": 1
}

 `

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

Ensure that all required parameters are included in the request body to avoid errors.

The response may contain additional nested objects and arrays that provide comprehensive details about the quote and its associated data.

Users should handle the response appropriately, especially when processing the data array for further actions or displays.
