# AssetManagement
(*asset_management*)

## Overview

Helper endpoints for handling asset uploads.

### Available Operations

* [get_presigned_url](#get_presigned_url) - Get an S3 presigned URL for secure uploads

## get_presigned_url

Generates a temporary, cryptographically signed URL that allows secure direct upload of assets to S3 without exposing AWS credentials.

This is the recommended approach for uploading assets, especially large files, as it:
- Avoids sending large payloads through the API server
- Provides secure, time-limited access to S3
- Enables resumable uploads for better reliability
- Reduces API server memory usage and network overhead

Use the returned URL to make a PUT request with your asset file, then use the returned key for subsequent sign/verify operations.


### Example Usage

<!-- UsageSnippet language="python" operationID="getPresignedUrl" method="post" path="/v1/assets/presign" -->
```python
import os
from que_media import Que


with Que(
    api_key_auth=os.getenv("QUE_API_KEY_AUTH", ""),
) as que:

    res = que.asset_management.get_presigned_url()

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.GetPresignedURLResponse](../../models/getpresignedurlresponse.md)**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.ProblemResponseError | 401, 403                    | application/problem+json    |
| errors.ProblemResponseError | 429                         | application/problem+json    |
| errors.ProblemResponseError | 500                         | application/problem+json    |
| errors.QueDefaultError      | 4XX, 5XX                    | \*/\*                       |