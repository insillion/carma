## POST `/api/v1/auth`

This `quote` API endpoint generates an insurance quote based on the data passed for the rental

This API endpoint can also be used to save a partially completed quote that can be completed at a later time (using the quote_id).

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



### Response

The response will be in JSON format and will include quote_id and premium details. quote_id should be passed if you modify any details on second time hit other wise new quote will be created.


| **Field Name** | **Type** | **Description** |
| --- | --- | --- |
| `status` | Integer | The status of the response. Typically, `0` indicates success. |
| `txt` | String | error message |
| `data` | Object | Contains the main data of the response. |