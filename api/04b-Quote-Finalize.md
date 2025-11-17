# **POST** `/api/v1/quote`

To finalize a quote (where no modifications can be made), call the same Quote API along with the "finalize" tag as "1".

\*Please note - Once the quote has been saved, finalized and issued - Policy modifications will not allow the change of the customer's email address.

### Request

- Method: POST
    
- Endpoint: `{{host}}/api/v1/quote`
    
- Headers:
    
    - Content-Type: application/json
        
    - in-auth-token : {{token}}
        

**Request Body**  
The request body should be in JSON format and include the following parameters:

| Key | Type | Description |  |
| --- | --- | --- | --- |
| quote_id | String | Unique identifier for the quote | Optional |
| finalize | Number | 0 - Draft quote  <br>1 - Finalize quote  <br>Once finalized the quote can not be modified | Required to Finalize and Issue policy |



### Response

The response will be in JSON format and will include quote_id and premium details. quote_id should be passed if you modify any details on second time hit other wise new quote will be created.


| **Field Name** | **Type** | **Description** |
| --- | --- | --- |
| `status` | Integer | The status of the response. Typically, `0` indicates success. |
| `txt` | String | error message |
| `data` | Object | Contains the main data of the response. |