# AssetManagement
(*asset_management*)

## Overview

Helper endpoints for handling asset uploads.

### Available Operations

* [get_presigned_url](#get_presigned_url) - Get an S3 presigned URL for uploads

## get_presigned_url

Generates a temporary, secure URL that a client can use to upload a large asset directly to S3. This is the recommended workflow for assets larger than a few megabytes to avoid sending large payloads through the API server.

### Example Usage

<!-- UsageSnippet language="python" operationID="getPresignedUrl" method="post" path="/v1/assets/presign" -->
```python
import os
from que import Que


with Que(
    api_key_auth=os.getenv("QUE_API_KEY_AUTH", ""),
) as q_client:

    res = q_client.asset_management.get_presigned_url()

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