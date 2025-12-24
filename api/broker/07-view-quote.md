### API Endpoint: View Quote

This endpoint retrieves the details of a specific insurance policy based on the given `quote_id`.

### Request

- **Method**: GET
    
- **URL**: `{{base_url}}/api/v1/carma/view_quote/quote?quote_id=string`
    

#### Query Parameters
    You can take the System Generated tag values from last quote api call.

- `quote_id` (string)(System Generated): The unique identifier of the policy you wish to retrieve. This parameter is required.
    

### Response

The response will return a JSON object containing the status of the request and the details of the requested policy.

#### Sample Response Structure

- **status** (integer): Indicates the success or failure of the request. A value of `0` typically indicates success.
    
- **txt** (string): A text field that may contain additional information about the request status (usually empty).
    
- **data** (array): An array containing the policy details, where each policy object may include the following fields:
    
    - `quote_id` (string): The identifier for the quote.
        
    - `product_id` (string): The identifier of the product associated with the policy.
            
    - `customer_id` (string): The ID of the customer associated with the policy.
                

### Notes

- Ensure that the `policy_id` parameter is valid to receive the appropriate policy details.
        
- The structure of the response allows for extensibility, meaning additional fields may be included in future updates.