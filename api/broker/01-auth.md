### API Endpoint: Auth API

This `auth` endpoint allows users to authenticate and obtain access to our Insurance policy issuance system.

By default, the auth token remains valid for 30 minutes (idle period). To extend this duration for each user, kindly reach out to the admin.

We recommend making the auth request prior to each transaction.

#### Request Format

- **Method**: POST
    
- **URL**: `{{host}}/api/v1/auth`
    
- **Content-Type**: application/json
    

#### Request Body

The request body must be in JSON format and should include the following fields:

- `email` (string, required): The email address of the user.
    
- `mpwd` (string, required): The password of the user.
    
The token from this request's response is used for subsequent API calls.

**Example Request Body**:

``` json
{
    "email": "xxxx",
    "mpwd": "yyyy"
}

 ```

#### Response Format

On a successful request, the API will return a JSON response with the following structure:

| Key | Description |
| --- | --- |
| status | The status of the response. 0 indicates success. |
| txt | Error message, if any. |
| token | System generated token to access other APIs. |
| email | The email of the logged-in user. |
        

**Example Response**:

``` json
{
    "status": 0,
    "txt": "",
    "data": {
        "email": "broker@carma.sb.insillion.com",
        "first_name": "",
        "last_name": "",
        "salt_public": "41983822",
        "pepper": 0,
        "priv_level": 0,
        "fail_count": 0,
        "pass_change_dt": "2025-12-25 06:21:49",
        "author": "admin@carma.sb.insillion.com",
        "ip": "192.168.0.35, 172.17.0.1",
        "c_ts": "2025-12-25 06:17:58",
        "u_ts": "2025-12-25 06:21:49.892583",
        "token": "+lkhVoOhMULU5aYmu59/CQm60PswBB97RC7+MbSKbF58UJP4yhbNLURaQcZUggxGSz4sc/3Kwd9mLGC19XRrQheUwg+DczYh/n2u9G1HobcVMEXWwEAp"
    }
}

 ```
