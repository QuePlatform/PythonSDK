# Utility
(*utility*)

## Overview

Service-level endpoints for health checks and configuration.

### Available Operations

* [get_health_check](#get_health_check) - Service Health Check
* [get_trust_list](#get_trust_list) - Retrieve the current C2PA trust bundle

## get_health_check

Performs a basic health check of the API service. This endpoint does not require authentication and is typically used by monitoring systems.

### Example Usage

<!-- UsageSnippet language="python" operationID="getHealthCheck" method="get" path="/healthz" -->
```python
import os
from que_media import Que


with Que(
    api_key_auth=os.getenv("QUE_API_KEY_AUTH", ""),
) as que:

    res = que.utility.get_health_check()

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.HealthzResponse](../../models/healthzresponse.md)**

### Errors

| Error Type             | Status Code            | Content Type           |
| ---------------------- | ---------------------- | ---------------------- |
| errors.QueDefaultError | 4XX, 5XX               | \*/\*                  |

## get_trust_list

Fetches the latest C2PA trust list, which includes trusted certificate authorities and hardware manufacturers. This list is used by verifiers to determine if a signature on a manifest is from a trusted source.

### Example Usage

<!-- UsageSnippet language="python" operationID="getTrustList" method="get" path="/v1/trust-list" -->
```python
import os
from que_media import Que


with Que(
    api_key_auth=os.getenv("QUE_API_KEY_AUTH", ""),
) as que:

    res = que.utility.get_trust_list()

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.GetTrustListResponse](../../models/gettrustlistresponse.md)**

### Errors

| Error Type                  | Status Code                 | Content Type                |
| --------------------------- | --------------------------- | --------------------------- |
| errors.ProblemResponseError | 401, 403                    | application/problem+json    |
| errors.ProblemResponseError | 429                         | application/problem+json    |
| errors.ProblemResponseError | 500                         | application/problem+json    |
| errors.QueDefaultError      | 4XX, 5XX                    | \*/\*                       |