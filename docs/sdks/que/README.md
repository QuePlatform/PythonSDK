# Que SDK

## Overview

Que API: Welcome to the Que Public HTTP API. Our platform provides robust tools for working with C2PA (Coalition for Content Provenance and Authenticity) manifests, enabling you to sign and verify digital assets to ensure their authenticity and provenance.

**Key Features:**
*   **Verify**: Inspect and validate C2PA manifests embedded in assets.
*   **Sign**: Embed C2PA manifests into your assets with a server-side signature.
*   **Trust Management**: Retrieve the current C2PA trust list.

**Authentication:**
All endpoints (except for `/healthz`) are secured and require an API key to be passed in the `x-api-key` header.

Usage of this API is tracked via Firehose for billing and monitoring purposes.


Find more detailed documentation and tutorials here.
<https://docs.addque.org>

### Available Operations

* [verify_asset](#verify_asset) - Verify the C2PA manifest of an asset
* [sign_asset](#sign_asset) - Sign an asset with a C2PA manifest

## verify_asset

Analyzes a digital asset (e.g., an image) to find, validate, and report on any embedded C2PA manifests. This allows you to confirm the asset's provenance and authenticity.

### Example Usage

<!-- UsageSnippet language="python" operationID="verifyAsset" method="post" path="/v1/verify" -->
```python
import os
from que import Que, models


with Que(
    api_key_auth=os.getenv("QUE_API_KEY_AUTH", ""),
) as q_client:

    res = q_client.verify_asset(asset={
        "url": "https://example.com/images/provenance-image.jpg",
    }, mode=models.VerifyRequestMode.DETAILED)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                                                                                                                                                    | Type                                                                                                                                                                                                                                                                                                                         | Required                                                                                                                                                                                                                                                                                                                     | Description                                                                                                                                                                                                                                                                                                                  |
| ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `asset`                                                                                                                                                                                                                                                                                                                      | [models.AssetRefDto](../../models/assetrefdto.md)                                                                                                                                                                                                                                                                            | :heavy_check_mark:                                                                                                                                                                                                                                                                                                           | A reference to a digital asset. The asset can be provided inline as Base64, via a public URL, or by referencing an S3 object.                                                                                                                                                                                                |
| `mode`                                                                                                                                                                                                                                                                                                                       | [Optional[models.VerifyRequestMode]](../../models/verifyrequestmode.md)                                                                                                                                                                                                                                                      | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                           | The level of detail to return in the verification report.<br/>* `summary`: A high-level pass/fail result. Fastest option.<br/>* `info`: Basic information about the manifest and its claims.<br/>* `detailed`: In-depth details of all assertions and claims.<br/>* `tree`: A hierarchical view of the manifest's ingredient relationships.<br/> |
| `retries`                                                                                                                                                                                                                                                                                                                    | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                                                                                                                                             | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                           | Configuration to override the default retry behavior of the client.                                                                                                                                                                                                                                                          |

### Response

**[models.VerifyAssetResponse](../../models/verifyassetresponse.md)**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.ProblemResponseError | 400, 401, 403, 422          | application/problem+json    |
| errors.ProblemResponseError | 429                         | application/problem+json    |
| errors.ProblemResponseError | 500                         | application/problem+json    |
| errors.QueDefaultError      | 4XX, 5XX                    | \*/\*                       |

## sign_asset

Embeds a C2PA manifest into a digital asset and signs it using a server-side key. This cryptographically links the asset to its provenance information.

### Example Usage

<!-- UsageSnippet language="python" operationID="signAsset" method="post" path="/v1/sign" -->
```python
import os
from que import Que, models


with Que(
    api_key_auth=os.getenv("QUE_API_KEY_AUTH", ""),
) as q_client:

    res = q_client.sign_asset(asset={
        "b64": "iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAQAAAC1HAwCAAAAC0lEQVR42mNkYAAAAAYAAjCB0C8AAAAASUVORK5CYII=",
    }, mode=models.SignRequestMode.SERVER_MEASURE, manifest_json={})

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                                                                                                                                                                                                                             | Type                                                                                                                                                                                                                                                                                                                                                                  | Required                                                                                                                                                                                                                                                                                                                                                              | Description                                                                                                                                                                                                                                                                                                                                                           |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `asset`                                                                                                                                                                                                                                                                                                                                                               | [models.AssetRefDto](../../models/assetrefdto.md)                                                                                                                                                                                                                                                                                                                     | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                                                    | A reference to a digital asset. The asset can be provided inline as Base64, via a public URL, or by referencing an S3 object.                                                                                                                                                                                                                                         |
| `mode`                                                                                                                                                                                                                                                                                                                                                                | [models.SignRequestMode](../../models/signrequestmode.md)                                                                                                                                                                                                                                                                                                             | :heavy_check_mark:                                                                                                                                                                                                                                                                                                                                                    | : warning: ** DEPRECATED **: This will be removed in a future release, please migrate away from it as soon as possible.<br/><br/>The signing mode to use.<br/>* `server_measure`: The server will download the asset, calculate its hash, and embed the manifest. Requires `manifest_json`.<br/>* `client_hash`: The client provides the asset hash directly. (Not yet implemented).<br/> |
| `manifest_json`                                                                                                                                                                                                                                                                                                                                                       | [Optional[models.ManifestJSON]](../../models/manifestjson.md)                                                                                                                                                                                                                                                                                                         | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                    | The C2PA manifest to embed in the asset. This is required when `mode` is `server_measure`.                                                                                                                                                                                                                                                                            |
| `retries`                                                                                                                                                                                                                                                                                                                                                             | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                                                                                                                                                                                      | :heavy_minus_sign:                                                                                                                                                                                                                                                                                                                                                    | Configuration to override the default retry behavior of the client.                                                                                                                                                                                                                                                                                                   |

### Response

**[models.SignAssetResponse](../../models/signassetresponse.md)**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.ProblemResponseError | 400, 401, 403, 422          | application/problem+json    |
| errors.ProblemResponseError | 429                         | application/problem+json    |
| errors.ProblemResponseError | 500                         | application/problem+json    |
| errors.QueDefaultError      | 4XX, 5XX                    | \*/\*                       |